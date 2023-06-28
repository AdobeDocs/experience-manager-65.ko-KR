---
title: 구성 [!DNL Workfront for Experience Manager enhanced connector]
description: 구성 [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Integrations
exl-id: 2660de7c-0281-4884-98d9-e78f20cf571c
hide: true
source-git-commit: 39930967e2f423b7fbbc79bcb85f78d15809e97d
workflow-type: tm+mt
source-wordcount: '1737'
ht-degree: 1%

---

# 구성 [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기를 클릭하십시오.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets-view/integrations/workfront-connector-configure.html?lang=en) |
| AEM 6.5 | 이 문서 |

에서 관리자 액세스 권한이 있는 사용자 [!DNL Adobe Experience Manager] 향상된 커넥터를 설치한 후 구성합니다. 설치에 대한 지침은 [커넥터 설치](/help/assets/workfront-integrations.md).

>[!IMPORTANT]
>
>* Adobe을 사용하려면 [!DNL Adobe Workfront for Experience Manager enhanced connector] 인증된 파트너를 통해서만 또는 [!DNL Adobe Professional Services]. 공인 파트너 없이 구축 및 구성된 경우 또는 [!DNL Adobe Professional Services], Adobe에서 지원되지 않습니다.
>
>* Adobe은 다음에 대한 업데이트를 릴리스할 수 있습니다. [!DNL Adobe Workfront] 및 [!DNL Adobe Experience Manager] 따라서 이 커넥터가 이중화됩니다. 이 경우 고객은 이 커넥터를 사용하지 않도록 전환해야 할 수 있습니다.
>
>* Adobe은 향상된 커넥터 버전 1.7.4 이상을 지원합니다. 이전 프리릴리스 및 사용자 지정 버전은 지원되지 않습니다. 향상된 커넥터 버전을 확인하려면 `digital.hoodoo` 의 왼쪽 창에서 사용할 수 있는 그룹 [패키지 관리자](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en).
>
>* 다음을 참조하십시오 [Workfront for Experience Manager Assets 강화 커넥터에 대한 파트너 인증 시험](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). 시험에 대한 자세한 내용은 [시험 안내서](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).

## 이벤트 구독 구성 {#event-subscriptions}

이벤트 구독은에서 발생하는 이벤트를 AEM에 알리는 데 사용됩니다. [!DNL Adobe Workfront]. 세 개 있습니다 [!DNL Workfront for Experience Manager enhanced connector] 작동하기 위해 이벤트 구독이 필요한 기능은 다음과 같습니다.

* 프로젝트 연결 폴더의 자동 생성.
* Workfront 문서 사용자 정의 양식 값의 변경 내용을 AEM 에셋 메타데이터에 동기화.
* 프로젝트 완료 시 Brand Portal에 에셋을 자동으로 게시합니다.

이러한 기능을 사용하려면 이벤트 구독을 활성화하십시오.

* 편집 [!UICONTROL Workfront 도구] 5단계에서 생성한 Cloud Services 구성을 선택하고 [!UICONTROL 이벤트 구독] 탭.
* 다음 항목 선택 [!UICONTROL Workfront 사용자 정의 통합] 섹션 6에서 을(를) 만들었습니다.
* 클릭 [!UICONTROL Workfront 이벤트 구독 활성화].

  ![이벤트 구독](/help/assets/assets/event-subs.png)

## 연결된 폴더 구성 {#linked-folders}

이벤트를 구독하려면 다음 단계를 수행합니다.

1. 다음 위치로 이동 **[!UICONTROL 이벤트 구독]** 클라우드 서비스의 탭입니다.
1. 에서 생성된 사용자 정의 통합 선택 [!DNL Workfront].
1. 클릭 **[!UICONTROL Workfront 이벤트 구독 활성화]**.

### 연결된 폴더 구조 구성 {#linked-folder-structure}

1. 클라우드 서비스의 프로젝트 연결 폴더 탭으로 이동합니다.
1. 연결된 폴더 상위 경로: 연결된 폴더를 만들려는 DAM의 폴더를 선택합니다. 비워 두면 기본값은 /content/dam으로 설정됩니다. Workfront 도구 메타데이터 스키마 및 Workfront 연결된 폴더 메타데이터 스키마가 선택한 폴더에 적용되었는지 확인합니다.
1. 연결된 폴더 구조: 쉼표로 구분된 값을 입력합니다. 각 값은 다음과 같아야 합니다 `DE:<some-project-custom-form-field>`, Portfolio, 프로그램, 연도, 이름 또는 일부 &quot;리터럴 문자열 값&quot;(따옴표가 있는 마지막 값). 현재 Portfolio,프로그램,연도,DE:프로젝트 유형,이름으로 설정되어 있습니다.
1. Workfront의 폴더 제목에 구조의 모든 폴더가 포함되어야 하는 경우 폴더 구조 이름 확인란을 사용하여 Workfront에서 연결된 폴더 제목을 작성해야 합니다. 그렇지 않으면 마지막 폴더의 제목이 됩니다.
1. 하위 폴더 다중 필드를 사용하면 연결된 폴더의 하위 폴더로 만들어야 하는 폴더 목록을 지정할 수 있습니다.
1. 프로젝트 상태: 연결된 폴더를 만들기 위해 프로젝트를 설정해야 하는 상태를 선택합니다.
1. 포트폴리오가 있는 프로젝트에서 연결된 폴더 만들기: 연결된 폴더를 만들기 위해 프로젝트가 속해야 하는 Portfolio 목록입니다. 모든 프로젝트 포트폴리오에 대해 연결된 폴더를 만들려면 이 목록을 비워 두십시오.
1. 사용자 정의 양식 필드가 있는 프로젝트에 연결된 폴더를 만듭니다. 사용자 정의 양식 필드 및 연결된 폴더를 만들기 위해 프로젝트에 있어야 하는 해당 값. 비워 두면 이 구성이 무시됩니다. 선택 `CUSTOM FORMS: Create DAM Linked Folder` 필드 및 입력 `Yes` 을 누릅니다.
1. 연결된 폴더의 자동 생성 활성화를 클릭합니다. 이벤트 구독 탭으로 돌아가면 이제 이벤트 만들기가 한 개 있습니다.

![연결된 폴더 구성](/help/assets/assets/wf-linked-folder-config.png)

## 메타데이터 스키마 매핑 {#metadata-schema-mapping}

### 폴더 메타데이터 매핑 구성 {#folder-metadata-mapping}

Workfront 프로젝트와 AEM 폴더 간의 메타데이터 매핑은 AEM 폴더 메타데이터 스키마 내에 정의됩니다. 폴더 메타데이터 스키마는 AEM에서 평소대로 생성 및 구성해야 합니다. Workfront 도구는 각 폴더 메타데이터 스키마 양식 필드의 설정 구성 탭에 자동 완성 드롭다운을 추가합니다. 이 자동 완성 드롭다운 메뉴를 사용하여 각 AEM 폴더 속성을 매핑할 Workfront 필드를 지정할 수 있습니다.

매핑을 구성하려면 다음 단계를 수행합니다.

1. 다음으로 이동 **[!UICONTROL 도구]** > **[!UICONTROL 에셋]** > **[!UICONTROL 폴더 메타데이터 스키마]**.
1. 편집하려는 폴더 메타데이터 스키마 양식을 선택하고 편집을 누릅니다.
1. 편집하려는 폴더 메타데이터 스키마 양식 필드를 선택하고 오른쪽 패널에서 설정 탭을 선택합니다.
1. 위치 [!UICONTROL Workfront 필드에서 매핑됨] 필드에서 선택한 AEM 폴더 속성에 매핑할 Workfront 필드의 이름을 선택합니다. 사용 가능한 옵션은 다음과 같습니다.

   * 프로젝트 사용자 정의 양식 필드
   * 프로젝트 개요 필드(ID, 이름, 설명, 참조 번호, 계획된 완료 일자, 프로젝트 소유자, 프로젝트 스폰서, Portfolio 또는 프로그램)

![메타데이터 매핑 구성](/help/assets/assets/wf-metadata-mapping-config2.png)

### 자산 메타데이터 매핑 구성 {#asset-metadata-mapping}

Adobe Workfront 문서와 에셋 간의 메타데이터 매핑은 AEM 메타데이터 스키마 내에 정의됩니다. 메타데이터 스키마는 AEM에서 평소대로 생성 및 구성해야 합니다. Workfront 도구는 각 메타데이터 스키마 양식 필드의 설정 구성 탭에 구성 옵션을 추가합니다. 이 옵션을 사용하면 각 AEM 속성을 매핑할 Workfront 필드를 지정할 수 있습니다.

매핑을 구성하려면 다음 단계를 수행합니다.

1. 다음으로 이동 **도구** > **에셋** > **메타데이터 스키마**.
1. 편집할 메타데이터 스키마 양식을 선택하고 을(를) 클릭합니다. **편집** 또는 처음부터 새 메타데이터 스키마를 만들 수 있습니다.
1. 편집하고 선택할 메타데이터 스키마 양식 필드를 선택합니다 **설정** 오른쪽 패널의 탭입니다.
1. 위치 [!DNL Workfront] 사용자 정의 양식 필드 [!DNL Workfront] 선택한 AEM 속성에 매핑할 필드입니다. 사용 가능한 옵션은 다음과 같습니다.

   * 문서 사용자 정의 양식 필드
   * 프로젝트 사용자 정의 양식 필드
   * 문제 사용자 정의 양식 필드
   * 작업 사용자 정의 양식 필드
   * 프로젝트 개요 필드(ID, 이름, 설명 또는 참조 번호)

1. 다음과 같은 경우 [!DNL Workfront] 다음에서 선택된 필드: [!UICONTROL Workfront 사용자 정의 양식 필드] 는 Workfront 사용자 유형 앞뒤 필드이며 매핑할 Workfront 사용자 필드를 지정해야 합니다. 이렇게 하려면 Workfront 참조 개체 필드에서 값 가져오기 를 선택한 다음 의 이름을 지정합니다. [!UICONTROL Workfront 사용자 정의 양식 필드] 매핑할 값을 검색할 소스.

   ![메타데이터 매핑 구성](/help/assets/assets/wf-metadata-mapping-config1.png)

## 맵 속성 {#map-property}

이 워크플로 단계에서는 사용자가 속성에 속성을 매핑할 수 있습니다. [!DNL Workfront] 프로젝트, 작업, 문제 또는 문서의 사용자 정의 양식입니다. 다음 [!DNL Workfront] 이 단계가 영향을 주는 아티팩트는 페이로드의 상대 경로를 사용하여 조회됩니다. 매핑될 속성은 단계 대화 상자 구성 내에서 제어됩니다.

**유형**: 이 필드에서는 속성을 매핑해야 하는 Workfront 오브젝트 유형을 선택할 수 있습니다.

**ID 속성**: 이 필드에서는 속성을 매핑해야 하는 Workfront 개체의 ID에 대한 경로를 지정할 수 있습니다. 이 필드에 지정된 경로는 워크플로 페이로드에 상대적이어야 합니다.

**속성 할당**: 이 다중 필드를 사용하면 AEM 속성과 Workfront 필드 간의 매핑을 지정할 수 있습니다. 다중 필드의 각 항목은 하나의 매핑을 지정합니다. 각 매핑에는 형식이 있어야 합니다. `<workfront-field>=<aem-mapped-property>`.

* 다음 `workfront-field` 다음이 될 수 있음:

   * 접두사로 식별되는 사용자 정의 양식 필드 `DE:`.
   * 이름으로 식별되는 편집 가능한 필드. 필드 이름은에 있습니다. [[!DNL Workfront] API 탐색기](https://experience.workfront.com/s/api-explorer).

* 다음 `aem-mapped-property` 다음과 같을 수 있습니다.

   * 리터럴 값. 따옴표로 묶어야 합니다.
   * AEM 속성입니다. 이 참조는 워크플로우 페이로드에 상대적이어야 합니다.
   * 명명된 값입니다. 이러한 요소는 괄호로 묶어야 합니다.
   * 위의 3개 항목의 연결입니다. 다음을 사용하여 지정 `{+}`.
   * 값을 로 둘러싸서 위의 3개 항목 변경 `{replace(<value>,"old-char","new-char")}`.

* 예를 들면 다음과 같습니다.

   * `status="INP"`
   * `DE:Asset Type=jcr:content/metadata/assetType`
   * `DE:Path={path}`
   * `URL="https://my-aem-author/assets.html"{+}{path}`

![속성을 매핑하는 구성](/help/assets/assets/wf-map-property-config.png)

## 상태 설정 {#set-status}

워크플로우 편집기에서 속성을 편집합니다. **[!UICONTROL Workfront - 상태 설정]** 다음에서 **[!UICONTROL 인수]** 탭.

![상태를 설정할 워크플로 편집](/help/assets/assets/wf-set-status.png)

## 주석 동기화 {#comments-sync}

1. 위치 [!DNL Experience Manager], 액세스 **[!UICONTROL 도구]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Workfront 도구 구성]**&#x200B;을 클릭하고 구성을 선택한 다음 을 선택합니다 **[!UICONTROL 속성]**.

   ![댓글 동기화](/help/assets/assets/comments-sync1.png)

1. 선택 **[!UICONTROL 이벤트 구독]** 탭을 클릭하고 **[!UICONTROL 댓글 동기화 활성화]** 날짜 **[!UICONTROL Workfront에서 작성한 주석을 AEM에 보내기]** 옵션을 선택합니다.

   ![동기화가 활성화됨](/help/assets/assets/wf-comment-sync-enabled.png)

Workfront에서 AEM으로의 주석 동기화를 테스트하려면 다음 단계를 수행하십시오.

1. Workfront에서 연결된 문서로 이동하여 업데이트 탭에 댓글을 추가합니다.

   ![Workfront에 주석 남기기](/help/assets/assets/comments-sync2.png)

1. AEM에서 연결된 동일한 문서로 이동하여 문서를 선택하고 [!UICONTROL 타임라인] 왼쪽 탐색 메뉴에서 옵션을 선택한 다음 [!UICONTROL 댓글]. 왼쪽 사이드바에 동기화된 주석이 표시됩니다. [!DNL Workfront].

## 에셋 버전 {#asset-versions}

AEM에서 에셋의 버전 기록을 유지 관리하려면 AEM에서 에셋 버전 관리를 구성합니다.

1. Experience Manager에서 액세스 **[!UICONTROL 도구]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Workfront 도구 구성]**&#x200B;를 클릭하고 **[!UICONTROL 고급]** 탭.

1. 옵션 선택 **[!UICONTROL 기존 에셋의 버전과 동일한 이름으로 에셋 저장]**. 선택하면 이 옵션을 사용하여 업로드된 에셋을 기존 에셋 버전과 동일한 위치에 저장할 수 있습니다. 선택하지 않으면 다른 이름으로 새 에셋이 만들어집니다(예: `asset-name.pdf` 및 `asset-name-1.pdf`).

1. 옵션 선택 **[!UICONTROL 새 버전을 만들 때 자산 메타데이터 업데이트]**. 선택하면 이 옵션은 자산의 새 버전이 생성될 때마다 자산 메타데이터를 업데이트합니다. 선택하지 않으면 에셋은 새 버전을 만들기 전에 보유했던 메타데이터를 유지합니다.

![에셋 버전 관리 구성](/help/assets/assets/wf-config-versioning.png)

>[!NOTE]
>
>링크된 폴더에서는 버전 관리가 지원되지 않습니다. 를 만들 때 [!DNL Workfront] 연결된 폴더 내에 문서가 있는 증명에서는 이전 버전의 자산에 대한 댓글 및 주석이 제거됩니다.

## 사용자 정의 양식 첨부 {#attach-custom-forms}

이 워크플로 단계를 통해 사용자는 사용자 정의 양식을 [!DNL Workfront] 아티팩트. 이 워크플로 단계는 모든 워크플로 모델에 추가할 수 있습니다. 다음 [!DNL Workfront] 이 단계가 영향을 주는 아티팩트는 페이로드의 상대 경로를 사용하여 조회됩니다.

Experience Manager의 워크플로 편집기에서 [!UICONTROL Workfront - 사용자 정의 양식 첨부] 워크플로 단계입니다.

![사용자 정의 양식](/help/assets/assets/wf-custom-forms.png).

## 자산 자동 게시 {#auto-publish-assets}

1. Experience Manager에서 액세스 **[!UICONTROL 도구]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Workfront 도구 구성]**&#x200B;를 클릭하고 **[!UICONTROL 고급]** 탭.

1. 선택 **[!UICONTROL Workfront에서 전송할 때 자산 자동 게시]**. 이 옵션을 사용하면 Workfront에서 AEM으로 에셋을 전송할 때 에셋을 자동으로 게시할 수 있습니다. 이 기능은 Workfront 사용자 정의 양식 필드 및 설정해야 하는 값을 지정하여 조건부로 활성화할 수 있습니다. 문서가 AEM으로 전송될 때마다 해당 조건을 충족하면 자산이 자동으로 게시됩니다.

1. 선택 **[!UICONTROL 프로젝트 완료 시 모든 프로젝트 에셋을 Brand Portal에 게시]**. 이 옵션을 사용하면 에셋을에 자동으로 게시할 수 있습니다. [!DNL Brand Portal] 속한 Workfront 프로젝트의 상태가 (으)로 변경될 때 `Complete`.

![자동 게시 구성](/help/assets/assets/wf-auto-publish-config.png)

## Workfront 문서 사용자 정의 양식 업데이트 {#subscribe-workfront-doc-custom-form-updates}

의 변경 사항을 구독하려면 [!DNL Workfront] 사용자 정의 양식 문서화에서 관련 옵션 선택 **[!UICONTROL 고급]** 탭. 이러한 업데이트를 구독하면 매핑된 항목이 업데이트됩니다 [!DNL Experience Manager] 의 해당 필드 시 메타데이터 필드 [!DNL Workfront] 문서 사용자 정의 양식이 변경되었습니다.

![의 Workfront 문서 사용자 정의 양식 업데이트 구성 [!DNL Experience Manager]](/help/assets/assets/wf-custom-form-update.png)
