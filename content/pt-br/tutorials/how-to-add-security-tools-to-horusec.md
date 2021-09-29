---
title: Como adicionar uma nova ferramenta de segurança ao Horusec?
weight: 4
description: Nesta seção, você encontra o tutorial para adicionar ferramentas de segurança ao Horusec.
---

## **Como adicionar uma ferramenta de segurança?**

Horusec trabalha como uma ferramenta de análise centralizada usando diferentes scans de vulnerabilidades. Você também pode adicionar algum, se preferir contribuindo para o projeto open source ou até mesmo em seu fork.

Para adicionar siga os passos abaixo:

### **Passo 1: Crie uma imagem Docker**

O Horusec usa o docker para executar as ferramentas de análise, o que evita problemas de configuração e de ambiente. Todas as ferramentas usadas tem suas respectivas imagens docker.

Essa imagem deve ter a ferramenta desejada instalada. O resultado desse container deve ser o mais limpo possível ou um JSON com as vulnerabilidades encontradas.

Elas são separadas por linguagem, por exemplo:

* `horuszup/horusec-go`;
* `horuszup/horusec-python`;
* `horuszup/horusec-elixir`.

Se a ferramenta que você deseja adicionar já é de uma linguagem que o Horusec possui a imagem, você precisa apenas adicioná-la ao dockerfile já existente.Veja o exemplo abaixo:

```
FROM python:alpine

RUN pip install bandit
```

{{% alert color="info" %}}
A imagem deve conter apenas o necessário para não ficar muito grande.
{{% /alert %}}

### **Passo 2: Crie um Formatter e um Config**

Para cada imagem do docker, é necessário ter o arquivo de configuração. O **formatter** é o código responsável por obter o output do container e transformá-lo em um objeto padrão do Horusec. Ele também adiciona a configuração workdir, obtém o autor do commit, dentre outras funcionalidades.

O arquivo `internal/services/formatters/python/bandit/config.go` possui os comandos que serão executados dentro do container para analisar o código.

Veja abaixo o exemplo de um container config:

```go
package bandit

const CMD = `
		{{WORK_DIR}}
    bandit -r . -f json 2> /dev/null > results.json
    jq -j -M -c . results.json
  `
```

- É necessário que o código que será executado no container tenha o `{{WORK_DIR}}` no ínicio. Essa seção será substituída por um caminho específico no projeto que será analisado, se você quiser.

- Crie o código que irá ler o output do container e transformá-lo no formato padrão Horusec.

- Todos formatos devem seguir o padrão e implementar a interface `IFormatter` no arquivo `internal/services/formatters/interface.go`.

### **Passo 3: Atualize os Enums**

Você também precisa adicionar a nova ferramenta nos enums de ferramentas aceitas. Se for uma linguagem que ainda não é suportada pelo Horusec, será necessário adicioná-la ao enum de linguagens.

Veja os passos para a atualização abaixo:

**Passo 1.** Adicione no enum de ferramentas se encontra no projeto [**Horusec-DevKit**](https://github.com/ZupIT/horusec-devkit) no diretório:
```
 -pkg/
 ---enums/
 -----tools/
 -------tools.go
```
Adicione a nova linguagem como por exemplo:
```go

const (
  ...
  Bandit Tool = "Bandit"
)
```
E altere o método `func Values() []Tool` com a ferramenta nova nova

**Passo 2.** **Se for uma linguagem que o Horusec ainda não tem suporte**: adicione a nova linguagem no projeto [**Horusec-DevKit**](https://github.com/ZupIT/horusec-devkit) no diretório:
```
 -pkg/
 ---enums/
 -----languages/
 -------language.go
```
Além de adicionar o enum, você precisa atualizar os métodos no mesmo arquivo com a nova linguagem:

* `func Values() []Language`
* `func mapEnableLanguages() map[string]Language`
* `func MapLanguagesEnableInCLI() map[Language]string`


**Passo 3.** Adicione a nova imagem que o Horusec irá executar em suas análises no projeto [**Horusec-CLI**](https://github.com/ZupIT/horusec) no diretório:

```
 -internal/
 ---enums/
 -----images/
 -------images.go
```

Veja um exemplo: 

```go
const (
  ...
  Python = "horuszup/horusec-python:v1.0.0"
  ...
)
```
Agora, altere o método `MapValues() map[languages.Language]string` com a linguagem e a nova imagem. 

- Depois disso, adicione a nova linguagem na funcionalidade workdir no projeto [**Horusec-CLI**](https://github.com/ZupIT/horusec) no diretório:

```
 -internal/
 ---entities/
 -----workdir/
 -------workdir.go
```
Veja o exemplo: 

```go
type WorkDir struct {
  ...
  Python     []string `json:"python"`
  ...
}
```
Para finalizar, altere os métodos com as linguagens:
* `func NewWorkDir() *WorkDir`
* `func (w *WorkDir) Map() map[languages.Language][]string`
* `func (w *WorkDir) setEmptyOrSliceEmptyInNilContent() *WorkDir`

**Passo 4.** Adicione a nova ferramenta nas configurações de ferramentas no projeto [**Horusec-CLI**](https://github.com/ZupIT/horusec) no diretório:

```
 -internal/
 ---entities/
 -----toolsconfig/
 -------tools_config.go
```

Veja o exemplo:

```go
type ToolsConfigsStruct struct {
  ...
  Bandit ToolConfig `json:"bandit"`
  ...
}
```
E altere os métodos com as linguagens:
* `func (t *ToolsConfigsStruct) ToMap() MapToolConfig`


### **Passo 4: Chame o Formatter**
Atualize a versão do [**Horusec-DevKit**](https://github.com/ZupIT/horusec-devkit) nos pacotes da Horusec-CLI, para que o projeto consiga extrair e utilizar a nova ferramenta e linguagem que você adicionou.

Depois de finalizar a **implementação do formatter**, você deve chamar a função no **analyzer controller**. 


Veja o seguinte path:

```
 -internal
 ---controller
 -----analyser
 -------analyser.go
```

Quando o Horusec inicia sua análise ele identifica as linguagens do projeto e faz um comparativo se tem alguma linguagem que está halitada a realizar uma análise. Caso tenha, ele irá enviar para o **analyzer controller** quais são as linguagens que devem ser acionadas na análise.
Com isso o **analyzer controller** faz um controle de processos para saber se todas as ferramentas que finalizaram suas análises. Então, dentro de cada `detectVulnerability[LANGUAGE]` tem o total de processos que representa a quantidade de ferramentas para cada linguagem.

Veja abaixo como chamar a implementação do formatter no **analyzer controller**.

### **É uma nova linguagem?**

Se sim, será necessário criar uma nova função para detectar as vulnerabilidades daquela linguagem. Veja como no exemplo abaixo:

```go
func (a *Analyser) detectVulnerabilityPython(wg *sync.WaitGroup, projectSubPath string) error {
    if err := a.dockerSDK.PullImage(a.getCustomOrDefaultImage(languages.Python)); err != nil {
        return err
    }
    bandit.NewFormatter(a.formatterService).StartAnalysis(projectSubPath)
    return nil
}
```


Você também precisa adicionar uma nova linguagem ao mapa que contém a função  **`mapDetectVulnerabilityByLanguage`**. Veja o exemplo: 

```go
func (a *Analyser) detectVulnerabilityFuncs() map[languages.Language]func(string) {
	return map[languages.Language]func(string){
				...
		languages.Python: a.detectVulnerabilityPython,
	}
}
```


### **É uma linguagem existente?**

Se sim, apenas adicione a chamada do novo formatter na função já existente **`detectVulnerability[LANGUAGE]`**.

**Veja como era antes de você adicionar:**

```go
func (a *Analyser) detectVulnerabilityPython(wg *sync.WaitGroup, projectSubPath string) error {
    if err := a.dockerSDK.PullImage(a.getCustomOrDefaultImage(languages.Python)); err != nil {
        return err
    }
    safety.NewFormatter(a.formatterService).StartAnalysis(projectSubPath)
    return nil
}
```
**Veja depois que você adicionou:**

```go
func (a *Analyser) detectVulnerabilityPython(wg *sync.WaitGroup, projectSubPath string) error {
	if err := a.docker.PullImage(a.getCustomOrDefaultImage(languages.Python)); err != nil {
		return err
	}
	spawn(wg, bandit.NewFormatter(a.formatter), projectSubPath)
	safety.NewFormatter(a.formatter).StartAnalysis(projectSubPath)
	return nil
}
```

{{% alert color="warning" %}}
Todas as analises são executadas em paralelo. Caso a função que executa a analise rode somente uma ferramente não é necessário utilizar go routine ou chamar a função `spawn` pois ela já vai estar rodando em paralelo, porém caso seja necessário rodar multiplas analises dentro de uma
é recomendado que use a função `spawn` para cada analise complementar.

{{% /alert %}}

### **Passo 5: Atualize as validações**

Agora, para finalizar, é necessário atualizar as validações do Horusec.

Quando a **Horusec-CLI** envia uma análise para a sua aplicação web, alguns projetos realizam validações para conferir se os dados estão de acordo com o esperado.

Para isso vá até o projeto [**Horusec-Platform**](https://github.com/ZupIT/horusec-platform) e atualize no serviço **API** o caso de uso para aceitar a nova ferramenta e linguagem no diretório:

```
 -api/
 ---internal/
 -----usecases/
 -------analysis/
 ---------analysis.go
```

- Adicione a nova ferramenta no método `func (au *UseCases) sliceTools() []interface{}` como por exemplo:
```go
func (au *UseCases) sliceTools() []interface{} {
	return []interface{}{
    ...
		tools.Bandit,
	}
}
```

- **Se você adicionou uma linguagem nova,** adicione no método `func (au *UseCases) sliceLanguages() []interface{}` como por exemplo:
```go
func (au *UseCases) sliceLanguages() []interface{} {
	return []interface{}{
    ...
		tools.Python,
	}
}
```

{{% alert color="success" %}}
Pronto! Agora o Horusec está integrado com sua nova ferramenta de segurança e gerando reports.
{{% /alert %}}
