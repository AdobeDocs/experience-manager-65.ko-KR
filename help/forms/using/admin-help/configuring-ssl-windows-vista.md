---
title: Windows Vista에서 SSL 구성
description: Windows Vista에서 SSL을 구성하는 방법을 알아봅니다. Java Keytool을 실행하여 인증을 위한 RSA 키가 포함된 SSL 인증서를 생성합니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 36c4300d-7a44-41f4-b294-06f32bb01686
solution: Experience Manager, Experience Manager Forms
feature: Document Security
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 50158d81-1c06-57f7-8bd7-e8ff76a93f85
    internal-label: Document Security
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 100%
---
# Windows Vista에서 SSL 구성 {#configuring-ssl-on-windows-vista}

Windows Vista™에서 SSL을 구성하려면 인증을 위한 RSA 키가 포함된 SSL 인증서가 필요합니다. Java keytool을 사용하여 인증서를 만들 수 있습니다.

>[!NOTE]
>
>Windows Vista는 DSA 키와 함께 작동하지 않습니다.

인증서와 키 저장소를 만드는 데 필요한 모든 정보가 포함된 단일 명령을 사용하여 keytool을 실행할 수 있습니다.

**SSL 인증서 만들기**

1. 명령 프롬프트에서 *`[JAVA HOME]`*/bin으로 이동하고 다음 명령을 입력하여 인증서와 키 저장소를 만듭니다.

   `keytool -genkey -keyalg RSA -dname "CN=`*Host Name* `, OU=`*Group Name* `, O=`*Company Name* `,L=`*City Name* `, S=`*State* `, C=`*Country Code* `" -alias`*&quot;LC Cert&quot;* `-keypass` `key`*_* *password* `-keystore`*keystorename* `.keystore`

   >[!NOTE]
   >
   >*`[JAVA_HOME]`을 JDK가 설치된 디렉터리로 바꾸고 기울임꼴 텍스트를 사용자 환경에 맞는 값으로 바꾸십시오.*

1. 암호로 `changeit`을 입력합니다. 이 암호는 Java 설치 시 설정된 기본값이며 시스템 관리자가 해당 암호를 변경했을 수 있습니다.
