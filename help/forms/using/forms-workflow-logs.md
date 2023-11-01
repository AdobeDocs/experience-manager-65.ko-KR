---
title: AEM Forms 워크플로우에서 로그인
description: AEM Forms 워크플로우 문제를 디버깅하고 AEM Forms 워크플로우에 대한 디버그 로깅을 활성화하여 로그를 보는 방법에 대해 알아봅니다.
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
docset: aem65
exl-id: 601c8d95-0d1a-4945-a522-e85d3e9fc4ae
source-git-commit: 000c22028259eb05a61625d43526a2e8314a1d60
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 5%

---

# AEM Forms 워크플로우에서 로그인{#logging-in-aem-forms-workflows}

Forms Workflow 단계는 워크플로우 관련 문제를 편리하게 디버깅하기 위한 자세한 로그를 제공합니다. AEM Forms 워크플로우에 대한 디버그 로깅을 활성화하여 로그를 봅니다.

기본적으로 모든 로깅 정보는 **error.log** 파일 위치: */crx-repository/logs/* 디렉토리.

양식 워크플로우의 디버그 로그는 다음과 같습니다.

* 각 워크플로우 단계의 항목입니다. 예:\
  `[DEBUG] "Executing Invoke DDX Process step"`

* 각 워크플로우 단계를 종료합니다. 예:\
  `[DEBUG] "Successfully finished Invoke DDX Process step"`

* 서비스 호출 메시지. 예:\
  `[DEBUG] Invoking Adobe Sign Service for creating agreement`

* 서비스 종료 메시지. 예:\
  `[DEBUG] Agreement created successfully with agreement id <agreement id>`

* 메타데이터 맵에서 변수를 읽습니다. 예:\
  `[DEBUG] Successfully retrieved variable <variable name> from workflow meta data map`

* JCR 저장소에 작성된 변수. 예:

  ```verilog
     [DEBUG] Successfully written variable <variable name> into meta data node at <JCR path where meta data is being written>
  ```

* 전체 스택 추적이 포함된 예외 메시지. 예:\
  `[DEBUG] Exception in Adobe Sign Service <complete stack trace>`

* 동적 단계 메타데이터 매개 변수. 예:

  ```verilog
  [DEBUG] Document of Record to be generated for adaptive form <path of adaptive form>
   [DEBUG] Locale to be used for Document of Record is <locale>
  ```

다음 예에서는 문서 서명 단계의 로그를 보여 줍니다.

```verilog
[DEBUG] Executing sign document step.
[DEBUG] Using adobe sign configuration: <path of adobe sign configuration>
[DEBUG] Invoking Adobe Sign Service for creating agreement
[DEBUG] Agreement created successfully with agreement id <agreement id>
[DEBUG] Exception in Adobe Sign Service <complete stack trace>
[ERROR] Exception in Adobe Sign Service
[DEBUG] Successfully finished sign document step
```

로그를 사용하여 다음을 평가합니다.

* 올바른 Adobe Sign 구성을 사용하고 있습니다.
* 계약을 성공적으로 만들면 Adobe Sign 서비스가 종료됩니다.
* 문서 서명 단계가 성공 메시지와 함께 종료됩니다.

예외가 있는 경우 전체 스택 추적을 보고 오류의 원인을 평가할 수 있습니다.

## AEM Forms 워크플로우에 대한 디버그 로깅 활성화 {#enable-debug-logging-for-aem-forms-workflows}

AEM Forms 워크플로우에 대한 디버그 로깅을 활성화할 수 있도록 다음을 수행합니다.

1. 다음 AEM 웹 콘솔 구성 관리자로 이동합니다.

   https://&#39;[server]:[포트]&#39;/system/console/configMgr

1. 선택 **[!UICONTROL 슬링]** > **[!UICONTROL 로그 지원]**.
1. 누르기 **[!UICONTROL 새 로거를 추가합니다.]**
1. 선택 **[!UICONTROL 디버그]** (으)로 **[!UICONTROL 로그 수준]**.
1. 로그 파일의 위치를 지정합니다. 로그 파일의 기본 위치는 다음과 같습니다. *logs\error.log*
1. 패키지의 이름을 다음으로 지정 **com.adobe.granite.workflow.core** 다음에서 **[!UICONTROL Logger]** 열.

   이 단계를 실행하면 디버그 로그를 저장할 수 있습니다 **com.adobe.granite.workflow.core** 패키지. 누르기 **[!UICONTROL +]** 목록에 다음 패키지 이름을 추가합니다.

   * com.adobe.fd.workflow
   * com.adobe.fd.workspace
