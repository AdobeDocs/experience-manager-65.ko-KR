---
title: AEM Forms 워크플로우에서 로깅
seo-title: AEM Forms 워크플로우에서 로깅
description: 로그를 사용하여 AEM Forms 워크플로우 문제를 디버깅합니다.
seo-description: 로그를 사용하여 AEM Forms 워크플로우 문제를 디버깅합니다.
uuid: 869d0271-c7e3-4b6d-8e63-893dc6af8b8a
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 14bb521a-42ea-4fe2-90fb-202e7ddf917a
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 5%

---


# AEM Forms 작업 과정 로그인{#logging-in-aem-forms-workflows}

Forms 워크플로우 단계에서는 워크플로우 관련 문제를 편리하게 디버깅하는 세부 로그를 제공합니다. AEM Forms 작업 과정에 대한 디버그 로깅을 활성화하여 로그를 봅니다.

기본적으로 모든 로깅 정보는 */crx-repository/logs/* 디렉토리의 **error.log** 파일에서 사용할 수 있습니다.

양식 워크플로우의 디버그 로그에는 다음이 포함됩니다.

* 각 워크플로우 단계의 시작. 예:\
   `[DEBUG] "Executing Invoke DDX Process step"`

* 각 워크플로우 단계를 종료합니다. 예:\
   `[DEBUG] "Successfully finished Invoke DDX Process step"`

* 서비스 호출 메시지. 예:\
   `[DEBUG] Invoking Adobe Sign Service for creating agreement`

* 서비스 종료 메시지. 예:\
   `[DEBUG] Agreement created successfully with agreement id <agreement id>`

* 메타데이터 맵에서 읽은 변수입니다. 예:\
   `[DEBUG] Successfully retrieved variable <variable name> from workflow meta data map`

* JCR 저장소에 기록된 변수입니다. 예:

   ```verilog
      [DEBUG] Successfully written variable <variable name> into meta data node at <JCR path where meta data is being written>
   ```

* 전체 스택 추적이 있는 예외 메시지입니다. 예:\
   `[DEBUG] Exception in Adobe Sign Service <complete stack trace>`

* 동적 단계 메타데이터 매개 변수. 예:

   ```verilog
   [DEBUG] Document of Record to be generated for adaptive form <path of adaptive form>
    [DEBUG] Locale to be used for Document of Record is <locale>
   ```

다음 예제에서는 문서 서명 단계의 로그를 보여 줍니다.

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

* 올바른 adobe sign 구성을 사용하고 있습니다.
* 계약을 성공적으로 만든 후 Adobe Sign 서비스가 종료됩니다.
* 문서 서명 단계는 성공 메시지와 함께 종료됩니다.

예외가 있는 경우 전체 스택 추적을 보고 오류의 원인을 평가할 수 있습니다.

## AEM Forms 작업 과정에 대한 디버그 로깅 활성화 {#enable-debug-logging-for-aem-forms-workflows}

AEM Forms 워크플로우에 대한 디버그 로깅을 활성화하려면 다음 단계를 수행하십시오.

1. AEM 웹 콘솔 구성 관리자로 이동:

   https://&#39;[서버]:[포트]&#39;/system/console/configMgr

1. **[!UICONTROL Sling]** > **[!UICONTROL 로그 지원]**&#x200B;을 선택합니다.
1. **[!UICONTROL 새 로거 추가를 누릅니다.]**
1. **[!UICONTROL Debug]**&#x200B;를 **[!UICONTROL 로그 수준]**&#x200B;으로 선택합니다.
1. 로그 파일의 위치를 지정합니다. 로그 파일의 기본 위치는 다음과 같습니다.*logs\error.log*
1. 패키지의 이름을 **[!UICONTROL Logger]** 열에서 **com.adobe.granite.workflow.core**&#x200B;로 지정합니다.

   이러한 단계를 실행하면 **com.adobe.granite.workflow.core** 패키지에 대한 디버그 로그를 저장할 수 있습니다. **[!UICONTROL +]**&#x200B;을 누르고 다음 패키지 이름을 목록에 추가합니다.

   * com.adobe.fd.workflow
   * com.adobe.fd.workspace

