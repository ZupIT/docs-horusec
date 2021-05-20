---
title: Gestão de repositórios
weight: 34
description: Nesta seção, você vai encontrar mais informações sobre a gestão de repositórios.
---

---

Este recurso permite que você visualize na plataforma todos os repositórios da sua organização, além de fazer a gestão do token e dos usuários que fazem parte de cada repo cadastrado. 

Ao criar um repositório, você tem algumas funcionalidades como:

* Gerenciar quais usuários da organização tem acesso;
* Gerenciar tokens de acesso do repositório.

![](/docs/ptbr/web/services/manager/repository-management/1-repository-organization.gif)

### Token de repositório

Assim como na organização, o token no repositório pode ser usado para todas as análises que você fizer e tem como principal objetivo ajudar o Horusec a identificar a organização e o repositório das análises enviadas pela [**CLI**]({{< ref path="/cli/overview.md" lang="pt-br">}}). 

O token de repositório é único e só pode ser criado por quem tem acesso de administrador dentro do repositório ou da organização. 

Por exemplo, se você adicionar este token em sua pipeline, o Horusec irá enviar a análise e armazená-la para ter uma visão analítica das [**vulnerabilidades**]({{< ref path="/web/services/vulnerability" lang="pt-br">}}) do seu repositório.

{{% alert color="warning" %}}
Lembre-se de que, ao criar um token de acesso, ele será visto apenas uma vez.
{{% /alert %}}

O token também pode ser configurado para ser expirável a fim de garantir a segurança da sua organização onde após a data de sua expiração o token não será mais válido para novas análises, caso a caixa de selação "É expirável" esteja **desmarcado** então este token não terá tempo de expiração.

![](/docs/ptbr/web/services/manager/repository-management/2-token-repository.gif)

### Usuários do repositório

Você pode convidar novos usuários para fazer parte do repositório. Ao fazer esse convite, é possível adicionar as seguintes permissões para o usuário:

* **Administrador do repositório**

  * Gerenciar repositório \(editar, visualizar, remover\);
  * Gerenciar usuários do repositório\(convidar, visualizar, atualizar, remover\);
  * Gerenciar tokens de acesso do repositório\(criar, visualizar, revogar\);
  * Gerenciar as vulnerabilidades do repositório que o usuário tem acesso;
  * Visualizar o dashboard dos repositórios que o usuário tem acesso.

* **Supervisor do repositório**
  * Gerenciar as vulnerabilidades do repositório que o usuário tem acesso;
  * Visualizar o dashboard dos repositórios que o usuário tem acesso.

* **Usuário do repositório**
  * Visualizar o dashboard dos repositórios que o usuário tem acesso.

Veja no gif abaixo um exemplo de convite de novos usuários para o repositório: 

![](/docs/ptbr/web/services/manager/repository-management/3-invite-user.gif)
