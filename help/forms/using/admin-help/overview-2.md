---
title: 인증서 및 자격 증명 관리의 기본 사항
description: 인증서 및 자격 증명 관리의 기본 사항을 알아봅니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 74bf0e77-f47b-475a-b2a7-52cfb3baaa22
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: ht
source-wordcount: '301'
ht-degree: 100%

---

# 인증서 및 자격 증명 관리의 기본 사항 {#basics-of-managing-certificates-and-credentials}

*자격 증명*&#x200B;에는 문서에 서명하거나 문서를 식별하는 데 필요한 개인 키 정보가 포함되어 있습니다. *인증서*&#x200B;는 신뢰를 위해 구성하는 공개 키 정보입니다. AEM Forms는 인증서와 자격 증명을 여러 목적으로 사용합니다.

* Acrobat Reader DC 확장 프로그램은 자격 증명을 사용하여 PDF 문서에서 Adobe Reader 사용 권한을 활성화합니다. ([Acrobat Reader DC 확장 프로그램에서 사용할 자격 증명 구성](/help/forms/using/admin-help/configuring-credentials-acrobat-reader-dc.md#configuring-credentials-for-use-with-acrobat-reader-dc-extensions)을 참조하십시오.)
* Acrobat에서 사용할 자격 증명 중 신뢰할 수 있는 발급자의 자격 증명만 표시하도록 Rights Management를 구성할 수 있습니다. ([Rights Management 표시 설정 구성](/help/forms/using/admin-help/configuring-client-server-options.md#configure-document-security-display-settings)을 참조하십시오.) 인증서에는 CN(일반 이름)이 있어야 합니다.
* 서명 서비스는 인증서와 자격 증명에 액세스합니다. 서명 서비스에 대한 자세한 내용은 [서비스 참조](https://www.adobe.com/go/learn_aemforms_services_65)를 참조하십시오.

**키 쌍 생성**

AEM Forms는 Trust Store를 사용하여 인증서, 자격 증명, 인증서 해지 목록(CRL)을 저장하고 관리합니다. 또한 독립적인 HSM(하드웨어 보안 모듈) 장치를 사용하여 개인 키를 저장할 수 있습니다.

AEM Forms에서는 키 쌍을 생성하는 옵션을 제공하지 않습니다. 하지만 Java keytool과 같은 도구를 사용하여 키 쌍을 생성하고 AEM Forms Trust Store로 가져올 수 있습니다. Java keytool에 대한 자세한 내용은 다음 항목을 참조하십시오.

[https://docs.oracle.com/javase/tutorial/security/toolsign/step3.html](https://docs.oracle.com/javase/tutorial/security/toolsign/step3.html)

[https://docs.oracle.com/cd/E19798-01/821-1841/gjrgy/index.html](https://docs.oracle.com/cd/E19798-01/821-1841/gjrgy/index.html)

[https://helpcenter.gsx.com/hc/en-us/articles/115015960428-How-to-Generate-a-Self-Signed-Certificate-and-Private-Key-using-OpenSSL](https://helpcenter.gsx.com/hc/en-us/articles/115015960428-How-to-Generate-a-Self-Signed-Certificate-and-Private-Key-using-OpenSSL)

다음과 같은 서명 유형이 지원되며 AEM Forms로 가져올 수 있습니다.

* XML 서명
* XMLTimeStampToken
* RFC 3161 TimeStampToken
* PKCS#7
* PKCS#1
* DSA 서명

**분실되거나 손상된 키 처리**

키가 분실되거나 손상되었을 것으로 의심되는 경우 다음 조치를 취하십시오.

1. 인증 기관에 알려서 손상된 키를 인증서 해지 목록에 추가하여 키를 해지하도록 합니다.
1. 인증 기관에서 새 키와 인증서를 받습니다.
1. 손상된 키를 사용하여 서명한 문서에 새 키를 사용하여 다시 서명합니다.
