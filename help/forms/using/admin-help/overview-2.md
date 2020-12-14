---
title: 인증서 및 자격 증명 관리에 대한 기본 사항
seo-title: 인증서 및 자격 증명 관리에 대한 기본 사항
description: 인증서 및 자격 증명을 관리하는 기본 사항에 대해 알아봅니다.
seo-description: 인증서 및 자격 증명을 관리하는 기본 사항에 대해 알아봅니다.
uuid: f421e206-e7b5-416c-b9fb-974094f10a66
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 986d16fc-4c81-4785-b1f3-fe8bd7ff669e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 0%

---


# 인증서 및 자격 증명 관리에 대한 기본 사항 {#basics-of-managing-certificates-and-credentials}

*자격 증명*&#x200B;에는 문서를 서명하거나 식별하는 데 필요한 개인 키 정보가 포함되어 있습니다. *인증서*&#x200B;는 신뢰도를 위해 구성하는 공개 키 정보입니다. AEM 양식은 여러 목적으로 인증서 및 자격 증명을 사용합니다.

* Acrobat Reader DC 익스텐션은 자격 증명을 사용하여 PDF 문서에서 Adobe Reader 사용 권한을 활성화합니다. ([Acrobat Reader DC 확장](/help/forms/using/admin-help/configuring-credentials-acrobat-reader-dc.md#configuring-credentials-for-use-with-acrobat-reader-dc-extensions)에 사용할 자격 증명 구성을 참조하십시오.)
* 신뢰할 수 있는 발행자의 자격 증명에만 Acrobat에서 사용할 자격 증명을 표시하도록 Rights Management을 구성할 수 있습니다. ([Rights Management 표시 설정 구성](/help/forms/using/admin-help/configuring-client-server-options.md#configure-document-security-display-settings)을 참조하십시오.) 인증서에 CN(일반 이름)이 있어야 합니다.
* 서명 서비스는 인증서 및 자격 증명에 액세스합니다. 서명 서비스에 대한 자세한 내용은 [서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

**쌍 키 생성**

AEM 양식은 Trust Store를 사용하여 인증서, 자격 증명 및 CRL(인증서 해지 목록)을 저장 및 관리합니다. 또한 독립적인 HSM(Hardware Security Module) 디바이스를 사용하여 개인 키를 저장할 수 있습니다.

AEM 양식은 키 쌍을 생성하는 옵션을 제공하지 않습니다. 그러나 Java 키 도구와 같은 도구를 사용하여 생성하고 AEM 양식 Trust Store에서 가져올 수 있습니다. Java 키 도구에 대한 자세한 내용은 다음을 참조하십시오.

[https://docs.oracle.com/javase/tutorial/security/toolsign/step3.html](https://docs.oracle.com/javase/tutorial/security/toolsign/step3.html)

[https://docs.oracle.com/cd/E19798-01/821-1841/gjrgy/index.html](https://docs.oracle.com/cd/E19798-01/821-1841/gjrgy/index.html)

[https://blogs.adobe.com/livecycle/2010/01/creating_ssl_keys_and_certific.html](https://blogs.adobe.com/livecycle/2010/01/creating_ssl_keys_and_certific.html)

다음 서명 유형이 지원되며 AEM 양식에서 가져올 수 있습니다.

* XML 서명
* XMLTimeStampToken
* RFC 3161 TimeStampToken
* PKCS#7
* PKCS#1
* DSA 서명

**손실되거나 손상된 키 처리**

키가 손실되거나 손상되지 않은 것으로 의심되는 경우 다음 작업을 수행합니다.

1. 인증 기관에 알려 인증서 해지 목록에 손상된 키를 추가하여 키를 취소하도록 합니다.
1. 인증 기관에서 새 키와 해당 인증서를 얻습니다.
1. 새 키를 사용하여 손상된 키를 사용하여 서명된 문서에 다시 서명합니다.

