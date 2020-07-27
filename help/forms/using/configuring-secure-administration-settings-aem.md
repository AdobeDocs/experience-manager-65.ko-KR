---
title: JEE의 AEM Forms에 대한 보안 관리 설정 구성
seo-title: JEE의 AEM Forms에 대한 보안 관리 설정 구성
description: 개인 개발 환경에서는 필요하지 않지만 JEE의 AEM Forms 제작 환경에서 사용자 계정 및 서비스를 관리하는 방법을 알아봅니다.
seo-description: 개인 개발 환경에서는 필요하지 않지만 JEE의 AEM Forms 제작 환경에서 사용자 계정 및 서비스를 관리하는 방법을 알아봅니다.
uuid: 04e45d06-f57d-406c-8228-15f483199430
content-type: reference
topic-tags: Security
products: SG_EXPERIENCEMANAGER/6.4
discoiquuid: d211d8b0-e75f-49c3-808d-5d0e26ad3a6b
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '884'
ht-degree: 0%

---


# JEE의 AEM Forms에 대한 보안 관리 설정 구성 {#configuring-secure-administration-settings-for-aem-forms-on-jee}

개인 개발 환경에서는 필요하지 않지만 JEE의 AEM Forms 제작 환경에서 사용자 계정 및 서비스를 관리하는 방법을 알아봅니다.

일반적으로 개발자는 제작 환경을 사용하여 애플리케이션을 구축하고 테스트하지 않습니다. 따라서, 비공개 개발 환경에서는 필요하지 않지만 제작 환경에서는 사용자 계정과 서비스를 관리해야 합니다.

이 문서에서는 JEE의 AEM Forms에서 제공하는 관리 옵션을 통해 전체 공격 표면을 줄이는 방법에 대해 설명합니다.

## 중요하지 않은 원격 서비스 액세스 비활성화 {#disabling-non-essential-remote-access-to-services}

JEE의 AEM Forms이 설치 및 구성되면 SOAP 및 EJB(Enterprise JavaBeans™)를 통한 원격 호출에서 다양한 서비스를 사용할 수 있습니다. 이 경우 원격 용어는 응용 프로그램 서버에 대한 SOAP, EJB 또는 AMF(Action Message Format) 포트에 대한 네트워크 액세스 권한이 있는 호출자를 의미합니다.

JEE 서비스의 AEM Forms에 공인 호출자에 대해 유효한 자격 증명이 필요하지만 원격 액세스 권한이 필요한 서비스만 허용해야 합니다. 제한된 접근성을 얻으려면 원격으로 액세스 가능한 서비스 세트를 작동하는 시스템에 필요한 최소 수준으로 축소한 다음 필요한 추가 서비스를 원격 호출로 설정해야 합니다.

JEE 서비스의 AEM Forms은 항상 적어도 SOAP에 액세스해야 합니다. 이러한 서비스는 일반적으로 Workbench에서 사용하지만 Workspace 웹 애플리케이션에서 호출하는 서비스도 포함합니다.

관리 콘솔의 응용 프로그램 및 서비스 웹 페이지를 사용하여 이 절차를 완료합니다.

1. 웹 브라우저에 다음 URL을 입력하여 관리 콘솔에 로그인합니다.

   ```java
            https://[host name]:'port'/adminui
   ```

1. 서비스 > **애플리케이션 및 서비스 > 기본 설정을 클릭합니다**.
1. 동일한 페이지에서 최대 200개의 서비스 및 끝점을 보도록 환경 설정을 지정합니다.
1. [ **서비스** ] > [ **응용 프로그램 및 서비스** ] > [ **끝점 관리]를 클릭합니다**.
1. [ **공급자** ] 목록에서 **EJB를** 선택한 다음 필터 **를**&#x200B;클릭합니다.
1. 모든 EJB 끝점을 비활성화하려면 목록에서 각 끝마다 옆의 확인란을 선택하고 비활성화 **를 클릭합니다**.
1. [ **다음** ]을 클릭하고 모든 EJB 끝점에 대해 이전 단계를 반복합니다. 끝점을 비활성화하기 전에 [공급자] 열에 EJB가 나열되어 있는지 확인합니다.
1. [ **공급자** ] 목록에서 SOAP를 **선택한** 다음 [ **필터]를**&#x200B;클릭합니다.
1. SOAP 끝점을 제거하려면 목록의 각 끝점 옆에 있는 확인란을 선택하고 [ **제거]를 클릭합니다**. 다음 끝점을 제거하지 마십시오.

   * AuthenticationManagerService
   * DirectoryManagerService
   * JobManager
   * event_management_service
   * event_configuration_service
   * ProcessManager
   * TemplateManager
   * RepositoryService
   * TaskManagerService
   * 작업 대기열 관리자
   * TaskManagerQueryService
   * WorkspaceSingleSignOn
   * ApplicationManager

1. [ **다음** ]을 클릭하고 위 목록에 없는 SOAP 끝점에 대해 이전 단계를 반복합니다. 끝점을 제거하기 전에 공급자 열에 SOAP가 나열되어 있는지 확인합니다.

## 필수 불가결한 익명 서비스 이용 비활성화 {#disabling-non-essential-anonymous-access-to-services}

일부 양식 서버 서비스는 일부 작업의 인증되지 않은(익명) 호출을 허용합니다. 즉, 서비스에 의해 노출된 하나 이상의 작업이 인증된 사용자로 호출되거나 인증된 사용자가 전혀 포함되지 않을 수 있습니다.

1. 웹 브라우저에 다음 URL을 입력하여 관리 콘솔에 로그인합니다.

   ```java
            https://[host name]:'port'/adminui
   ```

1. 서비스 > **애플리케이션 및 서비스 > 서비스 관리를 클릭합니다**.
1. 비활성화할 서비스의 이름(예: AuthenticationManagerService)을 클릭합니다.
1. [ **보안] 탭을**&#x200B;클릭하고 [익명 액세스 허용 **]을 선택 해제한**&#x200B;다음 [ **저장]을**&#x200B;클릭합니다.
1. 다음 서비스에 대해 3단계와 4단계를 완료합니다.

   * AuthenticationManagerService
   * EJB
   * 이메일
   * JobManager
   * 감시 폴더
   * UsermanagerUtilService
   * Remoting
   * RepositoryProviderService
   * EMCDocumentRepositoryProvider
   * IBMFilenetRepositoryProvider
   * FormAugmenter
   * TaskManagerService
   * TaskManagerConnector
   * TaskManagerQueryService
   * 작업 대기열 관리자
   * 작업 끝점 관리자
   * UserService
   * WorkspaceSearchTemplateService
   * WorkspacePropertyService
   * OutputService
   * FormsService

   원격 호출을 위해 이러한 서비스를 노출하려는 경우 이러한 서비스에 대한 익명 액세스 비활성화도 고려해야 합니다. 그렇지 않으면 이 서비스에 대한 네트워크 액세스 권한이 있는 호출자는 유효한 자격 증명을 전달하지 않고 서비스를 호출할 수 있습니다.

   필요하지 않은 모든 서비스에는 익명 액세스를 사용할 수 없습니다. 대부분의 내부 서비스는 사전 인증 없이 시스템의 모든 사용자가 호출해야 하므로 익명 인증을 활성화해야 합니다.

## 기본 전역 시간 초과 변경 {#changing-the-default-global-time-out}

최종 사용자는 워크벤치, AEM Forms 웹 애플리케이션 또는 AEM Forms 서버 서비스를 호출하는 사용자 정의 애플리케이션을 통해 AEM Forms에 인증할 수 있습니다. 한 글로벌 시간 초과 설정은 사용자가 다시 인증되기 전에 AEM Forms(SAML 기반 어설션 사용)과 상호 작용할 수 있는 기간을 지정하는 데 사용됩니다. 기본 설정은 2시간입니다. 제작 환경에서는 허용되는 최소 시간(분)으로 시간을 단축해야 합니다.

### 재인증 시간 제한 최소화 {#minimize-reauthentication-time-limit}

1. 웹 브라우저에 다음 URL을 입력하여 관리 콘솔에 로그인합니다.

   ```java
            https://[host name]:'port'/adminui
   ```

1. 설정 **> 사용자 관리 > 구성 > 구성 파일 가져오기 및 내보내기를 클릭합니다**.
1. 내보내기 **를** 클릭하여 기존 AEM Forms 설정으로 config.xml 파일을 생성합니다.
1. 편집기에서 XML 파일을 열고 다음 항목을 찾습니다.

   `<entry key=”assertionValidityInMinutes” value=”120”/>`

1. 값을 5보다 큰 숫자(분)로 변경하고 파일을 저장합니다.
1. 관리 콘솔에서 구성 파일 가져오기 및 내보내기 페이지로 이동합니다.
1. 수정된 config.xml 파일의 경로를 입력하거나 찾아보기를 클릭하여 해당 파일로 이동합니다.
1. 가져오기를 **클릭하여** 수정된 config.xml 파일을 업로드한 다음 **확인을 클릭합니다**.

