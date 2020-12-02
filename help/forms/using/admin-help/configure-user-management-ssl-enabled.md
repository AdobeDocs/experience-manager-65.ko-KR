---
title: SSL이 활성화된 LDAP 서버에 대한 사용자 관리 구성
seo-title: SSL이 활성화된 LDAP 서버에 대한 사용자 관리 구성
description: SSL이 활성화된 LDAP 서버에 대해 사용자 관리를 구성하여 LDAPS에서 동기화가 제대로 작동하도록 하는 방법을 알아봅니다.
seo-description: SSL이 활성화된 LDAP 서버에 대해 사용자 관리를 구성하여 LDAPS에서 동기화가 제대로 작동하도록 하는 방법을 알아봅니다.
uuid: 4b3f8ac7-fa38-4adf-a851-82d55fe431fe
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e6e7e2fa-579d-4b36-8598-6ced469a94b1
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---


# SSL이 활성화된 LDAP 서버 {#configure-user-management-for-an-ssl-enabled-ldap-server}에 대한 사용자 관리 구성

LDAPS에서 동기화가 제대로 작동하려면 CA(인증 기관)가 발급한 LDAP 인증서가 애플리케이션 서버의 JRE(Java Runtime Environment)에 있어야 합니다. 인증서를 응용 프로그램 서버의 JRE 클라이언트 파일로 가져옵니다. 일반적으로 *[JAVA_HOME]*/jre/lib/security/cacerts 디렉토리에 있습니다.

1. 디렉토리 서버에서 SSL을 활성화합니다. 자세한 내용은 디렉토리 공급업체에서 제공하는 설명서를 참조하십시오.
1. 디렉토리 서버에서 클라이언트 인증서를 내보냅니다.
1. keytool 프로그램을 사용하여 클라이언트 인증서 파일을 AEM forms 응용 프로그램 서버의 기본 Java virtual machine(JVM™) 인증서 저장소로 가져옵니다. 이 작업에 대한 절차는 JVM 및 클라이언트 설치 경로에 따라 달라집니다. 예를 들어 JDK 1.5와 함께 BEA WebLogic Server를 사용하는 경우 명령 프롬프트에서 다음 텍스트를 입력합니다.

   `keytool -import -alias`*별칭* `-file certificatename -keystore C:\bea\jdk15_04\jre\lib\security\cacerts`

1. 메시지가 표시되면 암호를 입력합니다. (Java의 경우 기본 암호는 `changeit`입니다.) 인증서를 성공적으로 가져오었다는 메시지가 나타납니다.
1. 메시지가 표시되면 인증서를 신뢰하려면 `Yes`을 입력합니다.
1. 사용자 관리에서 SSL을 활성화하고, 디렉토리 설정을 구성할 때 SSL 옵션에 대해 예를 선택하고 그에 따라 포트 설정을 변경합니다. 기본 포트 번호는 636입니다.

>[!NOTE]
>
>SSL을 사용하는 데 문제가 있는 경우 LDAP 브라우저를 사용하여 SSL을 사용할 때 LDAP 시스템에 액세스할 수 있는지 확인합니다. LDAP 브라우저가 액세스할 수 없는 경우 인증서 또는 애플리케이션 서버가 제대로 구성되지 않습니다. LDAP 브라우저가 올바르게 작동되고 문제가 계속 발생하면 사용자 관리가 제대로 구성되지 않습니다.

