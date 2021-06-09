---
title: Horusec Swift
weight: 2
description: Nesta seção, você vai encontrar mais informações sobre vulnerabilidades que o Horusec encontra em projetos Swift.
---

---

## **O que é?**

O  [**Horusec-Swift**]({{< ref path="/cli/analysis-tools/open-source-horusec-engine/horusec-kotlin.md#horusec-swift-cli" lang="pt-br">}}) é uma ferramenta SAST criado pela equipe do Horusec para fazer a busca de vulnerabilidades em projetos Swift.

## **Exemplos de vulnerabilidades**

{{% alert color="info" %}}

A seguir, você encontra todas as regras para o Horusec-Swift. O conteúdo foi traduzido, porém também foi mantido em inglês porque é assim que a mensagem aparece no sistema. 

{{% /alert %}}

### Weak Cipher Mode

DES é um hash fraco, que pode gerar hashes repetidos.

> DES is a weak hash, which can generate repeated hashes.

### Weak Cipher Mode

MD5 é um hash fraco, que pode gerar hashes repetidos. Para obter mais informações, verifique CWE-327 (https://cwe.mitre.org/data/definitions/327.html).

> MD5 is a weak hash, which can generate repeated hashes. For more information checkout the CWE-327 (https://cwe.mitre.org/data/definitions/327.html) advisory.

### Reverse engineering

Este aplicativo pode ter recursos de detecção de engenharia reversa.

> This App may have Reverse engineering detection capabilities.


### TLS 1.3 not used

TLS 1.3 deve ser usado. Versão antiga detectada - TLS 1.2.

> TLS 1.3 should be used. Detected old version - TLS 1.2.


### DTLS 1.2 not used

DTLS 1.2 deve ser usado. Versão antiga detectada - DTLS 1.0.

> DTLS 1.2 should be used. Detected old version - DTLS 1.0.


### CoreData Database

O aplicativo usa o banco de dados CoreData. As informações confidenciais devem ser criptografadas.

> App uses CoreData Database. Sensitive Information should be encrypted.


### SQLite Database

O aplicativo usa banco de dados SQLite. As informações confidenciais devem ser criptografadas.

> App uses SQLite Database. Sensitive Information should be encrypted.


### Javascript injection

A entrada do usuário em "loadHTMLString" resultará na injeção de JavaScript.

> User input in "loadHTMLString" will result in JavaScript Injection.


### Jailbreak detection

Este aplicativo pode ter recursos de detecção de Jailbreak.

> This App may have Jailbreak detection capabilities.


### SHA1 collision

SHA1 é um hash fraco conhecido por ter colisões de hash.

> SHA1 is a weak hash known to have hash collisions.

### MD2 collision

MD2 é um hash fraco conhecido por ter colisões de hash.

> MD2 is a weak hash known to have hash collisions.


### MD4 collision

MD4 é um hash fraco conhecido por ter colisões de hash.

> MD4 is a weak hash known to have hash collisions.



### MD5 collision

MD5 é um hash fraco conhecido por ter colisões de hash.

> MD5 is a weak hash known to have hash collisions.


### MD6 collision

MD6 é um hash fraco conhecido por ter colisões de hash.

> MD6 is a weak hash known to have hash collisions.


### WebView Safari

Recomenda-se usar WKWebView em vez de SFSafariViewController ou UIWebView para evitar a navegação em URLs arbitrários.

> It is recommended to use WKWebView instead of SFSafariViewController or UIWebView to prevent navigating to arbitrary URLs.


### File protection

O arquivo não possui proteções especiais associadas a ele.

> The file has no special protections associated with it.


### UIPasteboard

Este aplicativo usa UIPasteboard, o uso impróprio desta classe pode levar a problemas de segurança.

> This application uses UIPasteboard, improper use of this class can lead to security issues.


### Keyboard cache

O cache do teclado deve ser desativado para todas as entradas de dados confidenciais.

> Keyboard cache should be disabled for all sensitive data inputs.


### Deperected tls property

Uso da propriedade deprecada tlsMinimumSupportedProtocol. Para evitar potenciais riscos de segurança, use tlsMinimumSupportedProtocolVersion

> Use of deprecated property tlsMinimumSupportedProtocol. To avoid potential security risks, use tlsMinimumSupportedProtocolVersion


### Realm Database

O aplicativo usa Realm Database. As informações confidenciais devem ser criptografadas.

> App uses Realm Database. Sensitive Information should be encrypted.

