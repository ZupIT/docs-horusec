---
title: Horusec Dart
weight: 9
description: In this section, you will find more information about vulnerabilities that Horusec finds in DART projects.
---

---

## **What is?**

[**Horusec-Dart**]({{< ref path="/cli/analysis-tools/open-source-horusec-engine/horusec-dart.md" lang="en">}}) is a SAST tool created by the Horusec team to search for vulnerabilities on Dart projects.

## Rules

{{% alert color="info" %}}
Next, you find all the rules for Horusec-Dart.
{{% /alert %}}


### **Usage Local Data Without Cryptography**
{{% alert color="info" %}}
ID: "HS-DART-1"
{{% /alert %}}

While useful to speed applications up on the client side, it can be dangerous to store sensitive information this way because the data is not encrypted by default and any script on the page may access it. This rule raises an issue when the SharedPreferences and localstorage API's are used. For more information checkout the OWSAP A3:2017 (https://owasp.org/www-project-top-ten/2017/A3_2017-Sensitive_Data_Exposure.html) advisory.

### **No Send Sensitive Information in alternative channels (sms, mms, notifications)**
{{% alert color="info" %}}
ID: "HS-DART-2"
{{% /alert %}}

Sensitive information should never send for this channels sms, mms, notifications. For more information checkout the CWE-532 (https://cwe.mitre.org/data/definitions/532.html) advisory.

### **No use biometrics types face or fingerprint for login in account**
{{% alert color="info" %}}
ID: "HS-DART-3"
{{% /alert %}}

If the mobile app uses a feature like TouchID, it suffers from insecure authentication. For more information checkout the OWSAP M4:2016 (https://owasp.org/www-project-mobile-top-10/2016-risks/m4-insecure-authentication) advisory.

### **XML Reader External Entity Expansion**
{{% alert color="info" %}}
ID: "HS-DART-4"
{{% /alert %}}

XML External Entity (XXE) vulnerabilities occur when applications process untrusted XML data without disabling external entities and DTD processing. Processing untrusted XML data with a vulnerable parser can allow attackers to extract data from the server, perform denial of service attacks, and in some cases gain remote code execution. The XmlReaderSettings and XmlTextReader classes are vulnerable to XXE attacks when setting the DtdProcessing property to DtdProcessing.Parse or the ProhibitDtd property to false. To prevent XmlReader XXE attacks, avoid using the deprecated ProhibitDtd property. Set the DtdProcessing property to DtdProcessing.Prohibit. For more information checkout the CWE-611 (https://cwe.mitre.org/data/definitions/611.html) advisory.

### **No use connection without SSL**
{{% alert color="info" %}}
ID: "HS-DART-5"
{{% /alert %}}

Insecure Implementation of SSL. Trusting all the certificates or accepting self signed certificates is a critical Security Hole. This application is vulnerable to MITM attacks. For more information checkout the CWE-295 (https://cwe.mitre.org/data/definitions/295.html) advisory.

### **Send SMS**
{{% alert color="info" %}}
ID: "HS-DART-6"
{{% /alert %}}

Send SMS. For more information checkout the OWASP-M3 (https://owasp.org/www-project-mobile-top-10/2016-risks/m3-insecure-communication) advisory.

### **Prevent XSS Attack**
{{% alert color="info" %}}
ID: "HS-DART-7"
{{% /alert %}}

A potential Cross-Site Scripting (XSS) was found. The endpoint returns a variable from the client entry that has not been coded. Always encode untrusted input before output, regardless of validation or cleaning performed. For more information checkout the CWE-79 (https://cwe.mitre.org/data/definitions/79.html) advisory.

### **No Log Sensitive Information in console**
{{% alert color="info" %}}
ID: "HS-DART-8"
{{% /alert %}}
The App logs information. Sensitive information should never be logged. For more information checkout the CWE-532 (https://cwe.mitre.org/data/definitions/532.html) advisory.

### **Weak hashing function md5 or sha1**
{{% alert color="info" %}}
ID: "HS-DART-9"
{{% /alert %}}

MD5 or SHA1 have known collision weaknesses and are no longer considered strong hashing algorithms. For more information checkout the CWE-326 (https://cwe.mitre.org/data/definitions/326.html) advisory.

### **No Use Self Signed Certificate**
{{% alert color="info" %}}
ID: "HS-DART-10"
{{% /alert %}}

Insecure Implementation of SSL. Trusting all the certificates or accepting self signed certificates is a critical Security Hole. This application is vulnerable to MITM attacks. For more information checkout the CWE-295 (https://cwe.mitre.org/data/definitions/295.html) advisory.

### **No use biometrics types face or fingerprint for login in account**
{{% alert color="info" %}}
ID: "HS-DART-11"
{{% /alert %}}

If the mobile app uses a feature like TouchID, it suffers from insecure authentication. For more information checkout the OWSAP M4:2016 (https://owasp.org/www-project-mobile-top-10/2016-risks/m4-insecure-authentication) advisory.

### **No List changes on the clipboard**
{{% alert color="info" %}}
ID: "HS-DART-12"
{{% /alert %}}

The application allows you to list the changes on the Clipboard. Some malware also lists changes to the Clipboard.

### **SQL Injection**
{{% alert color="info" %}}
ID: "HS-DART-13"
{{% /alert %}}

The input values included in SQL queries need to be passed in safely. Bind variables in prepared statements can be used to easily mitigate the risk of SQL injection. Alternatively to prepare statements, each parameter can be escaped manually. For more information checkout the CWE-89 (https://cwe.mitre.org/data/definitions/89.html) advisory.

### **No use NSTemporaryDirectory**
{{% alert color="info" %}}
ID: "HS-DART-14"
{{% /alert %}}

User use in \"NSTemporaryDirectory ()\" is unreliable, it can result in vulnerabilities in the directory. For more information checkout the CWE-22 (https://cwe.mitre.org/data/definitions/22.html) advisory.

### **No Use Cipher mode**
{{% alert color="info" %}}
ID: "HS-DART-15"
{{% /alert %}}

This mode is not recommended because it opens the door to various security exploits. If the plain text to be encrypted contains substantial repetitions, it is possible that the cipher text will be broken one block at a time. You can also use block analysis to determine the encryption key. In addition, an active opponent can replace and exchange individual blocks without detection, which allows the blocks to be saved and inserted into the stream at other points without detection. ECB and OFB mode will produce the same result for identical blocks. The use of AES in CBC mode with an HMAC is recommended, ensuring integrity and confidentiality. https://docs.microsoft.com/en-us/visualstudio/code-quality/ca5358?view=vs-2019. For more information checkout the CWE-326 (https://cwe.mitre.org/data/definitions/326.html) and CWE-327 (https://cwe.mitre.org/data/definitions/327.html) advisory.

### **CORS Allow Origin Wild Card**
{{% alert color="info" %}}
ID: "HS-DART-16"
{{% /alert %}}

Cross-Origin Resource Sharing (CORS) allows a service to disable the browser’s Same-origin policy, which prevents scripts on an attacker-controlled domain from accessing resources and data hosted on a different domain. The CORS Access-Control-Allow-Origin HTTP header specifies the domain with permission to invoke a cross-origin service and view the response data. Configuring the Access-Control-Allow-Origin header with a wildcard (*) can allow code running on an attacker-controlled domain to view responses containing sensitive data. For more information checkout the CWE-942 (https://cwe.mitre.org/data/definitions/942.html) advisory.

### **Using shell interpreter when executing OS commands**
{{% alert color="info" %}}
ID: "HS-DART-17"
{{% /alert %}}

Arbitrary OS command injection vulnerabilities are more likely when a shell is spawned rather than a new process, indeed shell meta-chars can be used (when parameters are user-controlled for instance) to inject OS commands. For more information checkout the CWE-78 (https://cwe.mitre.org/data/definitions/78.html) advisory.
