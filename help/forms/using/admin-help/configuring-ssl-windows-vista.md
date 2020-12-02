---
title: Windows Vista에서 SSL 구성
seo-title: Windows Vista에서 SSL 구성
description: Windows Vista에서 SSL을 구성하는 방법을 알아봅니다.
seo-description: Windows Vista에서 SSL을 구성하는 방법을 알아봅니다.
uuid: 20bfcefb-ec84-4c55-bceb-6af106d883d7
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 667645a0-53d0-4f9b-a0ba-cc7e366a23a1
translation-type: tm+mt
source-git-commit: d3719a9ce2fbb066f99445475af8e1f1e7476f4e
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 0%

---


# Windows Vista {#configuring-ssl-on-windows-vista}에서 SSL 구성

Windows Vista™에서 SSL을 구성하려면 인증에 RSA 키가 있는 SSL 인증서가 필요합니다. Java 키 도구를 사용하여 인증서를 만들 수 있습니다.

>[!NOTE]
>
>Windows Vista는 DSA 키와 함께 작동하지 않습니다.

인증서와 키 저장소를 만드는 데 필요한 모든 정보가 포함된 단일 명령을 사용하여 키 도구를 실행할 수 있습니다.

**SSL 인증서 만들기**

1. 명령 프롬프트에서 *`[JAVA HOME]`*/bin으로 이동하고 다음 명령을 입력하여 인증서 및 키 저장소를 만듭니다.

   `keytool -genkey -keyalg RSA -dname "CN=`*호스트* `, OU=`*이름* `, O=`*그룹* `,L=`*이름 회사* `, S=`** `, C=`*이름City* `" -alias`*NameStateCountry 코드* `-keypass` `key`*&quot;LC Cert&quot;* ** `-keystore`*_passwordkeystorname* `.keystore`

   >[!NOTE]
   >
   >*`[JAVA_HOME]`을(를) JDK가 설치된 디렉토리로 바꾸고 기울임꼴로 된 텍스트를 환경에 해당하는 값으로 바꿉니다.*

1. 암호로 `changeit`을 입력합니다. 이 비밀번호는 Java 설치에 대한 기본 암호이며 시스템 관리자가 암호를 변경했을 수 있습니다.

