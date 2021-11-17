---
title: 구성 [!DNL Workfront for Experience Manager enhanced connector]
description: 구성 [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Integrations
source-git-commit: 8d39e1c86e5185a181400f10b7822a57c9d3aeae
workflow-type: tm+mt
source-wordcount: '1635'
ht-degree: 0%

---


# 구성 [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

에 관리자 액세스 권한이 있는 사용자 [!DNL Adobe Experience Manager] 설치 후 고급 커넥터를 구성합니다. 설치 지침은 [커넥터 설치](/help/assets/workfront-integrations.md).

>[!IMPORTANT]
>
>Adobe을 사용하려면 [!DNL Adobe Workfront for Experience Manager enhanced connector] 인증된 파트너를 통해 [!DNL Adobe Professional Services]. 인증된 파트너 또는 [!DNL Adobe Professional Services]Adobe에서 지원하지 않습니다.
>
>Adobe은 [!DNL Adobe Workfront] 및 [!DNL Adobe Experience Manager] 이렇게 하면 커넥터가 이중화됩니다. 이러한 경우 고객은 이 커넥터를 사용하는 상태에서 전환해야 할 수 있습니다.

## 이벤트 구독 구성 {#event-subscriptions}

이벤트 구독은 발생하는 이벤트를 AEM에 알리는 데 사용됩니다 [!DNL Adobe Workfront]. 3개 있습니다 [!DNL Workfront for Experience Manager enhanced connector] 작동하기 위해 이벤트 구독이 필요한 기능은 다음과 같습니다.

* 프로젝트 연결된 폴더를 자동으로 만듭니다.
* Workfront 문서 사용자 지정 양식 값의 변경 사항을 AEM 자산 메타데이터에 동기화합니다.
* 프로젝트 완료 시 Brand Portal에 자산을 자동으로 게시합니다.

이러한 기능을 사용하려면 이벤트 구독을 활성화하십시오.

* 편집 [!UICONTROL Workfront 도구] 5단계에서 만든 Cloud Services 구성을 선택하고 [!UICONTROL 이벤트 구독] 탭.
* 을(를) 선택합니다 [!UICONTROL Workfront 사용자 지정 통합] 6조에서 생성되었습니다.
* 클릭 [!UICONTROL Workfront 이벤트 구독 활성화].

   ![이벤트 구독](/help/assets/assets/event-subs.png)

## 연결된 폴더 구성 {#linked-folders}

이벤트에 가입하려면 다음 단계를 수행합니다.

1. 로 이동합니다 **[!UICONTROL 이벤트 구독]** 탭을 클릭합니다.
1. 에서 만든 사용자 지정 통합을 선택합니다 [!DNL Workfront].
1. 클릭 **[!UICONTROL Workfront 이벤트 구독 활성화]**.

### 연결된 폴더 구조 구성 {#linked-folder-structure}

1. 클라우드 서비스에서 프로젝트 연결된 폴더 탭으로 이동합니다.
1. 연결된 폴더 상위 경로: DAM에서 연결된 폴더를 만들 폴더를 선택합니다. 비워 두면 기본값은 /content/dam으로 설정됩니다. Workfront 도구 메타데이터 스키마와 Workfront 연결된 폴더 메타데이터 스키마가 선택한 폴더에 적용되었는지 확인합니다.
1. 연결된 폴더 구조: 쉼표로 구분된 값을 입력합니다. 각 값은 `DE:<some-project-custom-form-field>`, Portfolio, 프로그램, 연도, 이름 또는 일부 &quot;리터럴 문자열 값&quot;(따옴표가 있는 마지막 문자열) 현재 Portfolio,Program,Year,DE:Project Type,Name으로 설정되어 있습니다.
1. Workfront의 폴더 제목에 구조의 모든 폴더가 포함되어야 하는 경우 폴더 구조 이름 확인란을 사용하여 Workfront에서 연결된 폴더 제목을 작성 해야 합니다. 그렇지 않으면 마지막 폴더의 제목이 됩니다.
1. 하위 폴더 multifield를 사용하면 연결된 폴더의 하위 폴더로 만들어야 하는 폴더 목록을 지정할 수 있습니다.
1. 프로젝트 상태: 연결된 폴더를 만들려면 프로젝트를 설정해야 하는 상태를 선택합니다.
1. 포트폴리오를 사용하여 프로젝트에서 연결된 폴더를 만듭니다. 연결된 폴더를 만들기 위해 프로젝트가 속해 있어야 하는 Portfolio 목록입니다. 모든 프로젝트 포트폴리오에 연결된 폴더를 만들려면 이 목록을 비워 둡니다.
1. 사용자 지정 양식 필드를 사용하여 프로젝트에 연결된 폴더를 만듭니다. 사용자 지정 양식 필드와 연결된 폴더를 만들려면 프로젝트에 필요한 해당 값이 있어야 합니다. 이 구성은 비워 두면 무시됩니다. 선택 `CUSTOM FORMS: Create DAM Linked Folder` 필드 및 입력 `Yes` 참조하십시오.
1. 연결된 폴더를 자동으로 만들 수 있도록 설정을 클릭합니다. 이벤트 구독 탭으로 돌아가면 이제 하나의 만들기 이벤트가 있음을 알 수 있습니다.

![연결된 폴더 구성](/help/assets/assets/wf-linked-folder-config.png)

## 메타데이터 스키마 매핑 {#metadata-schema-mapping}

### 폴더 메타데이터 매핑 구성 {#folder-metadata-mapping}

Workfront 프로젝트와 AEM 폴더 간의 메타데이터 매핑은 AEM 폴더 메타데이터 스키마 내에 정의됩니다. AEM에서 평소대로 폴더 메타데이터 스키마를 만들고 구성해야 합니다. Workfront 도구는 각 폴더 메타데이터 스키마 양식 필드의 설정 구성 탭에 자동 완성 드롭다운을 추가합니다. 이 자동 완성 드롭다운 메뉴를 사용하면 각 AEM 폴더 속성을 매핑해야 하는 Workfront 필드를 지정할 수 있습니다.

매핑을 구성하려면 다음 단계를 수행합니다.

1. 다음으로 이동 **[!UICONTROL 도구]** > **[!UICONTROL 자산]** > **[!UICONTROL 폴더 메타데이터 스키마]**.
1. 편집할 폴더 메타데이터 스키마 양식을 선택하고 편집을 클릭합니다.
1. 편집할 폴더 메타데이터 스키마 양식 필드를 선택하고 오른쪽 패널에서 설정 탭을 선택합니다.
1. in [!UICONTROL Workfront 필드에서 매핑됨] 필드에서 선택한 AEM 폴더 속성에 매핑할 Workfront 필드의 이름을 선택합니다. 사용 가능한 옵션은 다음과 같습니다.

   * 프로젝트 사용자 지정 양식 필드
   * 프로젝트 개요 필드(ID, 이름, 설명, 참조 번호, 계획 완료 날짜, 프로젝트 소유자, 프로젝트 스폰서, Portfolio 또는 프로그램)

![메타데이터 매핑 구성](/help/assets/assets/wf-metadata-mapping-config2.png)

### 자산 메타데이터 매핑 구성 {#asset-metadata-mapping}

Adobe Workfront 문서와 자산 간의 메타데이터 매핑은 AEM 메타데이터 스키마 내에 정의됩니다. AEM에서 평소대로 메타데이터 스키마를 생성 및 구성해야 합니다. Workfront 도구는 각 메타데이터 스키마 양식 필드의 설정 구성 탭에 구성 옵션을 추가합니다. 이러한 옵션을 사용하면 각 AEM 속성을 매핑해야 하는 Workfront 필드를 지정할 수 있습니다.

매핑을 구성하려면 다음 단계를 수행합니다.

1. 다음으로 이동 **도구** > **자산** > **메타데이터 스키마**.
1. 편집할 메타데이터 스키마 양식을 선택하고 **편집** 또는 처음부터 새로운 메타데이터 스키마를 생성할 수 있습니다.
1. 편집할 메타데이터 스키마 양식 필드를 선택하고 선택합니다 **설정** 오른쪽 패널에 있는 탭입니다.
1. in [!DNL Workfront] Custom Form Field에서 [!DNL Workfront] 선택한 AEM 속성에 매핑할 필드입니다. 사용 가능한 옵션은 다음과 같습니다.

   * 문서 사용자 지정 양식 필드
   * 프로젝트 사용자 지정 양식 필드
   * 사용자 지정 양식 필드 문제
   * 작업 사용자 지정 양식 필드
   * 프로젝트 개요 필드(ID, 이름, 설명 또는 참조 번호)

1. 여기서 [!DNL Workfront] 선택한 필드 [!UICONTROL Workfront 사용자 지정 양식 필드] 는 Workfront 사용자 입력 미리 보기 필드이므로 매핑할 Workfront 사용자 필드를 지정해야 합니다. 이렇게 하려면 Workfront 참조 개체 필드에서 값 가져오기 를 선택한 다음 [!UICONTROL Workfront 사용자 지정 양식 필드] 매핑할 값을 가져올 위치.

   ![메타데이터 매핑 구성](/help/assets/assets/wf-metadata-mapping-config1.png)

## 맵 속성 {#map-property}

이 워크플로우 단계에서는 사용자가 속성을 [!DNL Workfront] 프로젝트, 작업, 문제 또는 문서의 사용자 지정 양식입니다. 다음 [!DNL Workfront] 이 단계에 영향을 주는 아티팩트는 페이로드의 상대 경로를 사용하여 조회됩니다. 매핑할 속성은 단계 대화 상자 구성 내에서 제어됩니다.

**유형**: 이 필드에서는 속성을 매핑해야 하는 Workfront 개체 유형을 선택할 수 있습니다.

**ID 속성**: 이 필드에서는 속성을 매핑해야 하는 Workfront 개체의 ID에 대한 경로를 지정할 수 있습니다. 이 필드에 지정된 경로는 워크플로우 페이로드를 기준으로 해야 합니다.

**속성 지정**: 이 다중 필드를 사용하면 AEM 속성과 Workfront 필드 간의 매핑을 지정할 수 있습니다. 다중 필드의 각 항목은 하나의 매핑을 지정합니다. 각 매핑에는 형식이 있어야 합니다 `<workfront-field>=<aem-mapped-property>`.

* 다음 `workfront-field` 다음을 수행할 수 있습니다.

   * 접두사로 식별되는 사용자 지정 양식 필드 `DE:`.
   * 이름으로 식별되는 편집 가능한 필드입니다. 필드 이름은 [[!DNL Workfront] API 탐색기](https://experience.workfront.com/s/api-explorer).

* 다음 `aem-mapped-property` 다음을 수행할 수 있습니다.

   * 리터럴 값입니다. 이러한 기호는 따옴표로 묶어야 합니다.
   * AEM 속성입니다. 이 참조는 워크플로우 페이로드를 기준으로 해야 합니다.
   * 이름이 지정된 값입니다. 이러한 요소는 대괄호로 둘러싸야 합니다.
   * 위의 3개 항목의 연결. 을 사용하여 지정합니다. `{+}`.
   * 값을 다음으로 둘러싸서 위의 3개 항목의 변경 `{replace(<value>,”old-char”,”new-char”)}`.

* 예를 들면 다음과 같습니다.

   * `status="INP"`
   * `DE:Asset Type=jcr:content/metadata/assetType`
   * `DE:Path={path}`
   * `URL=”https://my-aem-author/assets.html”{+}{path}`

![속성을 매핑하기 위한 구성](/help/assets/assets/wf-map-property-config.png)

## 상태 설정 {#set-status}

워크플로우 편집기에서 **[!UICONTROL Workfront - 상태 설정]** 에서 **[!UICONTROL 인수]** 탭.

![상태를 설정할 워크플로우 편집](/help/assets/assets/wf-set-status.png)

## 댓글 동기화 {#comments-sync}

1. in [!DNL Experience Manager], 액세스 **[!UICONTROL 도구]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Workfront 도구 구성]**&#x200B;를 클릭하고 구성을 선택한 다음 을 선택합니다 **[!UICONTROL 속성]**.

   ![주석 동기화](/help/assets/assets/comments-sync1.png)

1. 선택 **[!UICONTROL 이벤트 구독]** 탭, **[!UICONTROL 주석 동기화 사용]** on **[!UICONTROL Workfront에서 AEM으로 주석 보내기]** 선택 사항입니다.

   ![동기화가 활성화됨](/help/assets/assets/wf-comment-sync-enabled.png)

Workfront에서 AEM으로 주석의 동기화를 테스트하려면 다음 단계를 수행합니다.

1. Workfront에서 연결된 문서로 이동하고 업데이트 탭에서 설명을 추가합니다.

   ![Workfront에 주석 남기기](/help/assets/assets/comments-sync2.png)

1. AEM에서 동일한 링크된 문서로 이동하여 문서를 선택하고 [!UICONTROL 타임라인] 왼쪽 탐색 영역에서 옵션을 선택하고 [!UICONTROL 댓글]. 왼쪽 사이드바는 동기화된 설명을 표시합니다 [!DNL Workfront].

## 자산 버전 {#asset-versions}

AEM에서 자산의 버전 내역을 유지 관리하려면 AEM에서 자산 버전 지정을 구성합니다.

1. Experience Manager에서 **[!UICONTROL 도구]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Workfront 도구 구성]**, 그리고 를 엽니다. **[!UICONTROL 고급]** 탭.

1. 선택 옵션 **[!UICONTROL 기존 자산의 버전과 동일한 이름으로 자산을 저장합니다]**. 이 옵션을 선택하면 기존 자산 버전과 동일한 이름 및 위치에 업로드된 자산을 저장할 수 있습니다. 선택하지 않으면 다른 이름으로 새 자산이 만들어집니다(예: `asset-name.pdf` 및 `asset-name-1.pdf`).

1. 선택 옵션 **[!UICONTROL 새 버전을 만들 때 자산 메타데이터 업데이트]**. 이 옵션을 선택하면 자산의 새 버전이 생성될 때마다 자산 메타데이터가 업데이트됩니다. 이 옵션을 선택하지 않으면 새로운 버전을 만들기 전에 자산이 보유한 메타데이터를 유지합니다.

![자산 버전 관리 구성](/help/assets/assets/wf-config-versioning.png)

>[!NOTE]
>
>연결된 폴더에서는 버전 관리가 지원되지 않습니다. 만들기 [!DNL Workfront] 연결된 폴더 내에 문서가 있는 증명, 이전 버전의 자산에 대한 댓글 및 주석이 제거됩니다.

## 사용자 지정 양식 첨부 {#attach-custom-forms}

이 워크플로우 단계에서는 사용자가 사용자 지정 양식을 [!DNL Workfront] 아티팩트. 이 워크플로우 단계는 모든 워크플로우 모델에 추가할 수 있습니다. 다음 [!DNL Workfront] 이 단계에 영향을 주는 아티팩트는 페이로드의 상대 경로를 사용하여 조회됩니다.

Experience Manager의 워크플로우 편집기에서 [!UICONTROL Workfront - 사용자 지정 양식 첨부] 워크플로우 단계.

![사용자 지정 양식](/help/assets/assets/wf-custom-forms.png).

## 자산 자동 게시 {#auto-publish-assets}

1. Experience Manager에서 **[!UICONTROL 도구]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Workfront 도구 구성]**, 그리고 를 엽니다. **[!UICONTROL 고급]** 탭.

1. 선택 **[!UICONTROL Workfront에서 보낼 때 자동으로 자산 게시]**. 이 옵션을 사용하면 자산을 Workfront에서 AEM으로 전송할 때 자산을 자동으로 게시할 수 있습니다. 이 기능은 Workfront 사용자 지정 양식 필드와 이 필드를 설정해야 하는 값을 지정하여 조건부로 활성화할 수 있습니다. 문서가 AEM으로 전송될 때마다 조건이 충족되면 자산이 자동으로 게시됩니다.

1. 선택 **[!UICONTROL 프로젝트 완료 시 모든 프로젝트 자산을 Brand Portal에 게시]**. 이 옵션을 사용하면 자산을 [!DNL Brand Portal] 이 프로젝트가 속한 Workfront 프로젝트의 상태가 `Complete`.

![자동 게시 구성](/help/assets/assets/wf-auto-publish-config.png)

## Workfront 문서 사용자 지정 양식 업데이트 {#subscribe-workfront-doc-custom-form-updates}

의 변경 사항에 가입하려면 [!DNL Workfront] 문서 사용자 지정 양식의 **[!UICONTROL 고급]** 탭. 이러한 업데이트를 구독하면 매핑된 콘텐츠가 업데이트됩니다 [!DNL Experience Manager] 에 해당 필드가 있을 때 메타데이터 필드 [!DNL Workfront] 문서 사용자 지정 양식이 변경되었습니다.

![Workfront 문서 사용자 지정 양식 업데이트 구성 [!DNL Experience Manager]](/help/assets/assets/wf-custom-form-update.png)
