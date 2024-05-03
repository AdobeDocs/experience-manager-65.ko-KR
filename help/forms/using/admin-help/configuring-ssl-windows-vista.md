---
title: Windows Vista에서 SSL 구성
description: Windows Vista에서 SSL을 구성하는 방법에 대해 알아봅니다. Java Keytool 을 사용하고 실행하여 인증에 RSA 키를 사용하여 SSL 인증서를 생성합니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 36c4300d-7a44-41f4-b294-06f32bb01686
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---

# Windows Vista에서 SSL 구성 {#configuring-ssl-on-windows-vista}

Windows Vista™에서 SSL을 구성하려면 인증을 위해 RSA 키가 포함된 SSL 인증서가 필요합니다. Java 키 도구를 사용하여 인증서를 생성할 수 있습니다.

>[!NOTE]
>
>Windows Vista는 DSA 키에서 작동하지 않습니다.

인증서 및 키 저장소를 만드는 데 필요한 모든 정보가 포함된 단일 명령을 사용하여 키 도구를 실행할 수 있습니다.

**SSL 인증서 만들기**

1. 명령 프롬프트에서 다음 위치로 이동합니다. *`[JAVA HOME]`*/bin에 다음 명령을 입력하여 인증서와 키 저장소를 만듭니다.

   `keytool -genkey -keyalg RSA -dname "CN=`*호스트 이름* `, OU=`*그룹 이름* `, O=`*회사 이름* `,L=`*도시 이름* `, S=`*시/도* `, C=`*국가 코드* `" -alias`*&quot;LC 인증서&quot;* `-keypass` `key`*_* *암호* `-keystore`*keystorename* `.keystore`

   >[!NOTE]
   >
   >바꾸기 *`[JAVA_HOME]`JDK가 설치된 디렉터리로 바꾸고 텍스트를 사용자 환경에 해당하는 값으로 기울임꼴로 바꿉니다.*

1. 유형 `changeit` 을 암호로 사용하십시오. 이 암호는 Java 설치의 기본값이며 시스템 관리자가 변경했을 수 있습니다.
