---
title: SSL이 활성화된 LDAP 서버에 대한 사용자 관리 구성
description: SSL이 활성화된 LDAP 서버에 대한 사용자 관리를 구성하여 LDAPS를 통해 동기화가 제대로 작동하도록 하는 방법을 알아봅니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 606e84f2-6728-47a9-a439-dbe2e55100ad
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 94%
---
# SSL이 활성화된 LDAP 서버에 대한 사용자 관리 구성 {#configure-user-management-for-an-ssl-enabled-ldap-server}

LDAPS를 통해 동기화가 제대로 작동하려면 인증 기관(CA)에서 발급한 LDAP 인증서가 애플리케이션 서버의 Java 런타임 환경(JRE)에 있어야 합니다. 인증서를 애플리케이션 서버의 JRE cacerts 파일로 가져옵니다. 해당 파일은 일반적으로 *[JAVA_HOME]*/jre/lib/security/cacerts 디렉터리에 있습니다.

1. 디렉터리 서버에서 SSL을 활성화합니다. 자세한 내용은 디렉터리 공급업체에서 제공하는 설명서를 참조하십시오.
1. 디렉터리 서버에서 클라이언트 인증서를 내보냅니다.
1. keytool 프로그램을 사용하여 클라이언트 인증서 파일을 AEM Forms 애플리케이션 서버의 기본 Java 가상 머신(JVM™) 인증서 저장소로 가져옵니다. 이 작업 절차는 JVM과 클라이언트 설치 경로에 따라 다릅니다. 예를 들어 JDK 1.5와 함께 BEA WebLogic Server를 사용하는 경우 명령 프롬프트에서 다음 텍스트를 입력합니다.

   `keytool -import -alias`*alias* `-file certificatename -keystore C:\bea\jdk15_04\jre\lib\security\cacerts`

1. 메시지가 나타나면 암호를 입력합니다. (Java의 경우 기본 암호는 `changeit`입니다.) 인증서를 성공적으로 가져왔다는 메시지가 나타납니다.
1. 메시지가 나타나면 인증서를 신뢰할 수 있도록 `Yes`를 입력합니다.
1. 사용자 관리에서 SSL을 활성화하고 디렉터리 설정을 구성할 때 SSL 옵션에서 예를 선택하고 그에 따라 포트 설정도 변경합니다. 기본 포트 번호는 636입니다.

>[!NOTE]
>
>SSL을 사용하면서 문제가 발생하는 경우 LDAP 브라우저를 사용하여 SSL을 사용할 때 LDAP 시스템에 액세스할 수 있는지 여부를 확인하십시오. LDAP 브라우저에서 액세스할 수 없다면 인증서나 애플리케이션 서버가 올바르게 구성되지 않은 것입니다. LDAP 브라우저가 정상적으로 작동하는데도 여전히 문제가 발생하는 경우 사용자 관리가 올바르게 구성되지 않은 것입니다.
