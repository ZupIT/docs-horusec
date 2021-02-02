---
title: Atualize os Enums
weight: 18
description: 'Passo 3: Atualizando Enums'
---

---

Você também precisa adicionar a nova ferramenta nos enums de ferramentas aceitas. Se for uma linguagem que ainda não é suportada pelo Horusec, será necessário adicioná-la ao enum de linguagens.

{{% alert color="info" %}}

O enum de ferramentas se encontra no diretório:`development-kit/pkg/enums/tools/tools.go`

{{% /alert %}}

Veja o exemplo abaixo:

```text
...
const (
	...
	TfSec Tool = "TfSec"
)
...
```

O enum de linguagens se encontra no diretório:

`development-kit/pkg/enums/languages/languages.go`

Veja um exemplo abaixo:

```text
...
const (
	...
	HCL Language = "HCL"
)
...
```
