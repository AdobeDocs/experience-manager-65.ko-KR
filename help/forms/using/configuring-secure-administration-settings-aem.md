---
title: JEE에서 AEM Forms에 대한 보안 관리 설정 구성
description: 개인 개발 환경에서는 필요하지만 JEE의 AEM Forms 프로덕션 환경에서는 필요하지 않은 사용자 계정 및 서비스를 관리하는 방법에 대해 알아봅니다.
content-type: reference
topic-tags: Security
products: SG_EXPERIENCEMANAGER/6.4
role: Admin,User
exl-id: 40bc01b4-a59e-4420-81d6-2887857bddce
solution: Experience Manager, Experience Manager Forms
feature: Document Security,Adaptive Forms
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '847'
ht-degree: 0%

---

# JEE에서 AEM Forms에 대한 보안 관리 설정 구성 {#configuring-secure-administration-settings-for-aem-forms-on-jee}

개인 개발 환경에서는 필요하지만 JEE의 AEM Forms 프로덕션 환경에서는 필요하지 않은 사용자 계정 및 서비스를 관리하는 방법에 대해 알아봅니다.

일반적으로 개발자는 프로덕션 환경을 사용하여 애플리케이션을 빌드하고 테스트하지 않습니다. 따라서 개인 개발 환경에서는 필요하지만 프로덕션 환경에서는 필요하지 않은 사용자 계정 및 서비스를 관리해야 합니다.

이 문서에서는 AEM Forms on JEE가 제공하는 관리 옵션을 통해 전체 공격 표면을 줄이는 방법에 대해 설명합니다.

## 서비스에 대한 필수적이지 않은 원격 액세스 비활성화 {#disabling-non-essential-remote-access-to-services}

JEE의 AEM Forms이 설치되고 구성된 후 SOAP 및 EJB(Enterprise JavaBeans™)를 통해 원격 호출에 많은 서비스를 사용할 수 있습니다. 이 경우 원격이라는 용어는 애플리케이션 서버용 SOAP, EJB 또는 AMF(Action Message Format) 포트에 대한 네트워크 액세스 권한이 있는 호출자를 의미합니다.

JEE 서비스의 AEM Forms을 사용하려면 승인된 호출자에 대해 유효한 자격 증명을 전달해야 하지만, 원격으로 액세스할 수 있어야 하는 서비스에 대한 원격 액세스만 허용해야 합니다. 제한된 액세스 가능성을 얻으려면 원격으로 액세스할 수 있는 서비스 집합을 작동하는 시스템에 대해 가능한 최소한으로 줄인 다음 필요한 추가 서비스에 대해 원격 호출을 활성화해야 합니다.

JEE의 AEM Forms 서비스에는 항상 최소한 SOAP 액세스 권한이 필요합니다. 이러한 서비스는 일반적으로 Workbench에서 사용하는 데 필요하지만 Workspace 웹 애플리케이션에서 호출하는 서비스도 포함합니다.

관리 콘솔의 응용 프로그램 및 서비스 웹 페이지를 사용하여 다음 절차를 완료합니다.

1. 웹 브라우저에 다음 URL을 입력하여 관리 콘솔에 로그인합니다.

   ```java
            https://[host name]:'port'/adminui
   ```

1. **서비스 > 응용 프로그램 및 서비스 > 환경 설정**&#x200B;을 클릭합니다.
1. 동일한 페이지에서 최대 200개의 서비스 및 끝점을 보려면 환경 설정을 설정하십시오.
1. **서비스** > **응용 프로그램 및 서비스** > **끝점 관리**&#x200B;를 클릭합니다.
1. **공급자** 목록에서 **EJB**&#x200B;을(를) 선택한 다음 **필터**&#x200B;를 클릭합니다.
1. 모든 EJB 끝점을 비활성화하려면 목록에서 각 끝점 옆의 확인란을 선택하고 **비활성화**&#x200B;를 클릭합니다.
1. **다음**&#x200B;을 클릭하고 모든 EJB 끝점에 대해 이전 단계를 반복합니다. 끝점을 비활성화하기 전에 EJB가 공급자 열에 나열되어 있는지 확인하십시오.
1. **공급자** 목록에서 **SOAP**&#x200B;을(를) 선택한 다음 **필터**&#x200B;를 클릭합니다.
1. SOAP 끝점을 제거하려면 목록에서 각 끝점 옆의 확인란을 선택하고 **제거**&#x200B;를 클릭합니다. 다음 끝점은 제거하지 마십시오.

   * 인증 관리자 서비스
   * 디렉터리 관리자 서비스
   * 작업 관리자
   * event_management_service
   * event_configuration_service
   * 프로세스 관리자
   * TemplateManager
   * RepositoryService
   * 작업 관리자 서비스
   * 작업 큐 관리자
   * TaskManagerQueryService
   * WorkspaceSingleSignOn
   * 애플리케이션 관리자

1. **다음**&#x200B;을 클릭하고 위 목록에 없는 SOAP 끝점에 대해 이전 단계를 반복합니다. 끝점을 제거하기 전에 SOAP이 공급자 열에 나열되어 있는지 확인합니다.

## 서비스에 대한 필수적이지 않은 익명 액세스 비활성화 {#disabling-non-essential-anonymous-access-to-services}

일부 Forms 서버 서비스는 일부 작업에 대해 인증되지 않은(익명의) 호출을 허용합니다. 즉, 서비스에 의해 노출된 하나 이상의 작업은 임의의 인증된 사용자로 호출되거나 인증된 사용자가 전혀 없음을 의미할 수 있다.

1. 웹 브라우저에 다음 URL을 입력하여 관리 콘솔에 로그인합니다.

   ```java
            https://[host name]:'port'/adminui
   ```

1. **서비스 > 응용 프로그램 및 서비스 > 서비스 관리**&#x200B;를 클릭합니다.
1. 비활성화할 서비스 이름(예: AuthenticationManagerService)을 클릭합니다.
1. **보안 탭**&#x200B;을 클릭하고 **익명 액세스 허용**&#x200B;을 선택 취소한 다음 **저장**&#x200B;을 클릭합니다.
1. 다음 서비스에 대해 3단계와 4단계를 완료합니다.

   * 인증 관리자 서비스
   * EJB
   * 이메일
   * 작업 관리자
   * 감시 폴더
   * UsermanagerUtilService
   * 원격
   * RepositoryProviderService
   * EMCDocumentumRepositoryProvider
   * IBMFilenetRepositoryProvider
   * FormAugmenter
   * 작업 관리자 서비스
   * 작업 관리자 커넥터
   * TaskManagerQueryService
   * 작업 큐 관리자
   * 작업 끝점 관리자
   * UserService
   * WorkspaceSearchTemplateService
   * WorkspacePropertyService
   * OutputService
   * Forms 서비스

   원격 호출을 위해 이러한 서비스를 노출하려면 이러한 서비스에 대한 익명 액세스를 비활성화하는 것도 고려해야 합니다. 그렇지 않으면, 이 서비스에 대한 네트워크 액세스 권한이 있는 모든 호출자는 유효한 자격 증명을 전달하지 않고 서비스를 호출할 수 있습니다.

   필요하지 않은 모든 서비스에 대해 익명 액세스를 비활성화해야 합니다. 많은 내부 서비스에서는 사전 승인되지 않은 상태로 시스템의 모든 사용자가 익명 인증을 호출해야 하므로 익명 인증을 활성화해야 합니다.

## 기본 전역 시간 제한 변경 {#changing-the-default-global-time-out}

최종 사용자는 AEM Forms 서버 서비스를 호출하는 Workbench, AEM Forms 웹 애플리케이션 또는 사용자 정의 애플리케이션을 통해 AEM Forms에 인증할 수 있습니다. 하나의 전역 시간 초과 설정은 이러한 사용자가 강제로 다시 인증되기 전에 AEM Forms(SAML 기반 어설션 사용)와 상호 작용할 수 있는 시간을 지정하는 데 사용됩니다. 기본 설정은 2시간입니다. 프로덕션 환경에서는 허용되는 최소 시간(분)으로 시간을 줄여야 합니다.

### 재인증 시간 제한 최소화 {#minimize-reauthentication-time-limit}

1. 웹 브라우저에 다음 URL을 입력하여 관리 콘솔에 로그인합니다.

   ```java
            https://[host name]:'port'/adminui
   ```

1. **설정 > 사용자 관리 > 구성 > 구성 파일 가져오기 및 내보내기**&#x200B;를 클릭합니다.
1. 기존 AEM Forms 설정을 사용하여 config.xml 파일을 만들려면 **내보내기**&#x200B;를 클릭합니다.
1. 편집기에서 XML 파일을 열고 다음 항목을 찾습니다.

   `<entry key="assertionValidityInMinutes" value="120"/>`

1. 값을 5보다 큰 숫자(분)로 변경하고 파일을 저장합니다.
1. 관리 콘솔에서 구성 파일 가져오기 및 내보내기 페이지로 이동합니다.
1. 수정된 config.xml 파일의 경로를 입력하거나 찾아보기를 눌러 해당 파일로 이동합니다.
1. **가져오기**&#x200B;를 클릭하여 수정된 config.xml 파일을 업로드한 다음 **확인**&#x200B;을 클릭합니다.
