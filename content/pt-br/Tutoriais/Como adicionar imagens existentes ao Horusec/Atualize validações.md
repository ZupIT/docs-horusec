---
title: Atualize validações
weight: 22
description: 'Passo 5: Atualize as validações'
---

---

Agora, para finalizar, é necessário atualizar as validações do Horusec. Quando você receber uma análise no servidor, você precisa checar se as ferramentas e as linguagens enviadas para ele são válidas. 

Veja o path:

 `development-kit/pkg/usecases/analysis/analysis.go`

No arquivo **`analysis.go`** você deve procurar: 

* A função **`sliceTools`**  e atualizá-la, veja como no exemplo abaixo:

```text
func (au *UseCases) sliceTools() []interface{} {
	return []interface{}{
		...
		tools.GoSec
	}
}
```

* A função **`sliceLanguages`** e atualizá-la, veja como no exemplo abaixo:

```text
func (au *UseCases) sliceLanguages() []interface{} {
	return []interface{}{
		...
		languages.Go
	}
}
```
