---
title: SSL 사용 LDAP 서버에 대한 사용자 관리 구성
description: LDAPS를 통해 동기화가 제대로 작동하도록 SSL이 활성화된 LDAP 서버에 대한 사용자 관리를 구성하는 방법에 대해 알아봅니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 606e84f2-6728-47a9-a439-dbe2e55100ad
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---

# SSL 사용 LDAP 서버에 대한 사용자 관리 구성 {#configure-user-management-for-an-ssl-enabled-ldap-server}

LDAPS를 통해 동기화가 제대로 작동하려면 CA(인증 기관)가 발급한 LDAP 인증서가 애플리케이션 서버의 JRE(Java Runtime Environment)에 있어야 합니다. 인증서를 애플리케이션 서버의 JRE cacerts 파일로 가져옵니다(일반적으로 *[JAVA_HOME]*/jre/lib/security/cacerts 디렉터리.

1. 디렉토리 서버에서 SSL을 활성화합니다. 자세한 내용은 디렉토리 공급업체에서 제공한 설명서를 참조하십시오.
1. 디렉터리 서버에서 클라이언트 인증서를 내보냅니다.
1. keytool 프로그램을 사용하여 클라이언트 인증서 파일을 AEM Forms 애플리케이션 서버 의 기본 JVM(Java Virtual Machine™) 인증서 저장소로 가져옵니다. 이 작업의 절차는 JVM 및 클라이언트 설치 경로에 따라 다릅니다. 예를 들어 JDK 1.5와 함께 BEA WebLogic Server를 사용하는 경우 명령 프롬프트에서 다음 텍스트를 입력합니다.

   `keytool -import -alias`*별칭* `-file certificatename -keystore C:\bea\jdk15_04\jre\lib\security\cacerts`

1. 메시지가 표시되면 암호를 입력합니다. (Java의 경우 기본 암호는 입니다. `changeit`.) 인증서를 성공적으로 가져왔다는 메시지가 나타납니다.
1. 메시지가 표시되면 다음을 입력합니다. `Yes` 인증서를 신뢰할 수 있습니다.
1. 사용자 관리에서 SSL을 활성화하고 디렉터리 설정을 구성할 때 SSL 옵션에 대해 예를 선택하고 그에 따라 포트 설정을 변경합니다. 기본 포트 번호는 636입니다.

>[!NOTE]
>
>SSL을 사용하는 데 문제가 발생하는 경우 LDAP 브라우저를 사용하여 SSL을 사용할 때 LDAP 시스템에 액세스할 수 있는지 여부를 확인합니다. LDAP 브라우저가 액세스할 수 없는 경우 인증서 또는 애플리케이션 서버가 제대로 구성되지 않습니다. LDAP 브라우저가 올바르게 작동하지만 여전히 문제가 발생하는 경우 사용자 관리가 제대로 구성되지 않습니다.
