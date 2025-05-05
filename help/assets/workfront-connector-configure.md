---
title: ' [!DNL Workfront for Experience Manager enhanced connector] 구성'
description: ' [!DNL Workfront for Experience Manager enhanced connector] 구성'
role: Admin
feature: Workfront Integrations and Apps
exl-id: 2660de7c-0281-4884-98d9-e78f20cf571c
hide: true
solution: Experience Manager, Workfront
source-git-commit: 5ccac0aadce3971e66da052d393cbd33b61e94f7
workflow-type: tm+mt
source-wordcount: '1698'
ht-degree: 1%

---

# 구성 [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/integrations/workfront-connector-configure.html?lang=en) |
| AEM 6.5 | 이 문서 |

[!DNL Adobe Experience Manager]에서 관리자 액세스 권한이 있는 사용자가 향상된 커넥터를 설치한 후 구성합니다. 설치 지침은 [커넥터 설치](/help/assets/workfront-integrations.md)를 참조하십시오.

>[!IMPORTANT]
>
>* Adobe을 사용하려면 인증된 파트너 또는 [!DNL Adobe Professional Services]을(를) 통해서만 [!DNL Adobe Workfront for Experience Manager enhanced connector]을(를) 배포하고 구성해야 합니다. 인증 파트너 또는 [!DNL Adobe Professional Services] 없이 배포 및 구성된 경우 Adobe에서 지원하지 않습니다.
>
>* Adobe은 이 커넥터를 중복 커넥터로 만드는 [!DNL Adobe Workfront] 및 [!DNL Adobe Experience Manager]에 대한 업데이트를 릴리스할 수 있습니다. 이러한 경우 고객은 이 커넥터를 사용하지 않도록 전환해야 할 수 있습니다.
>
>* Adobe은 향상된 커넥터 버전 1.7.4 이상을 지원합니다. 이전 프리릴리스 및 사용자 지정 버전은 지원되지 않습니다. 향상된 커넥터 버전을 확인하려면 [패키지 관리자](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en)의 왼쪽 창에서 사용할 수 있는 `digital.hoodoo` 그룹으로 이동하십시오.
>
>* [Workfront for Experience Manager Assets 강화 커넥터에 대한 파트너 인증 시험](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html)을 참조하세요. 시험에 대한 자세한 내용은 [시험 가이드](https://express.adobe.com/page/Tc7Mq6zLbPFy8/)를 참조하세요.

## 이벤트 구독 구성 {#event-subscriptions}

이벤트 구독은 [!DNL Adobe Workfront]에서 발생하는 이벤트를 AEM에 알리는 데 사용됩니다. 이벤트 구독을 통해 작동하는 세 가지 [!DNL Workfront for Experience Manager enhanced connector] 기능이 있습니다. 해당 기능은 다음과 같습니다.

* 프로젝트 연결 폴더의 자동 생성.
* Workfront 문서 사용자 정의 양식 값의 변경 내용을 AEM 에셋 메타데이터에 동기화.
* 프로젝트 완료 시 Brand Portal에 에셋을 자동으로 게시합니다.

이러한 기능을 사용하려면 이벤트 구독을 활성화하십시오.

* 5단계에서 만든 [!UICONTROL Workfront 도구] Cloud Service 구성을 편집하고 [!UICONTROL 이벤트 구독] 탭을 선택합니다.
* 섹션 6에서 만든 [!UICONTROL Workfront 사용자 지정 통합]을(를) 선택하십시오.
* [!UICONTROL Workfront 이벤트 구독 활성화]를 클릭합니다.

  ![이벤트 구독](/help/assets/assets/event-subs.png)

## 연결된 폴더 구성 {#linked-folders}

이벤트를 구독하려면 다음 단계를 수행합니다.

1. 클라우드 서비스의 **[!UICONTROL 이벤트 구독]** 탭으로 이동합니다.
1. [!DNL Workfront]에서 만든 사용자 지정 통합을 선택하십시오.
1. **[!UICONTROL Workfront 이벤트 구독 활성화]**&#x200B;를 클릭합니다.

### 연결된 폴더 구조 구성 {#linked-folder-structure}

1. 클라우드 서비스의 프로젝트 연결 폴더 탭으로 이동합니다.
1. 연결된 폴더 상위 경로: 연결된 폴더를 만들려는 DAM의 폴더를 선택합니다. 비워 두면 기본값은 /content/dam으로 설정됩니다. Workfront 도구 메타데이터 스키마 및 Workfront 연결된 폴더 메타데이터 스키마가 선택한 폴더에 적용되었는지 확인합니다.
1. 연결된 폴더 구조: 쉼표로 구분된 값을 입력합니다. 각 값은 `DE:<some-project-custom-form-field>`, Portfolio, 프로그램, 연도, 이름 또는 일부 &quot;리터럴 문자열 값&quot;(따옴표가 있는 마지막 값)이어야 합니다. 현재 Portfolio,프로그램,연도,DE:프로젝트 유형,이름으로 설정되어 있습니다.
1. 권한 구성: `wf-workfront-users` 그룹에 대해 `/conf/workfront-tools/settings/cloudconfigs`에 `jcr:all permissions` 권한을 추가합니다.
1. Workfront의 폴더 제목에 구조의 모든 폴더가 포함되어야 하는 경우 폴더 구조 이름 확인란을 사용하여 Workfront에서 연결된 폴더 제목을 작성해야 합니다. 그렇지 않으면 마지막 폴더의 제목입니다.
1. 하위 폴더 다중 필드를 사용하면 연결된 폴더의 하위 폴더로 만들어야 하는 폴더 목록을 지정할 수 있습니다.
1. 프로젝트 상태: 연결된 폴더를 만들 프로젝트의 상태를 선택합니다.
1. 포트폴리오가 있는 프로젝트에서 연결된 폴더 만들기: 연결된 폴더를 만들기 위해 프로젝트가 속해야 하는 Portfolio 목록입니다. 모든 프로젝트 포트폴리오에 대해 연결된 폴더를 만들려면 이 목록을 비워 두십시오.
1. 사용자 정의 양식 필드: 사용자 정의 양식 필드 및 프로젝트가 연결된 폴더를 만들기 위해 필요한 해당 값으로 프로젝트에 연결된 폴더를 만듭니다. 비워 두면 이 구성은 무시됩니다. 필드에 `CUSTOM FORMS: Create DAM Linked Folder`을(를) 선택하고 값에 `Yes`을(를) 입력합니다.
1. 연결된 폴더의 자동 생성 활성화를 클릭합니다. 이벤트 구독 탭으로 돌아가면 이제 이벤트 만들기가 한 개 있습니다.

![연결된 폴더 구성](/help/assets/assets/wf-linked-folder-config.png)

## 메타데이터 스키마 매핑 {#metadata-schema-mapping}

### 폴더 메타데이터 매핑 구성 {#folder-metadata-mapping}

Workfront 프로젝트와 AEM 폴더 간의 메타데이터 매핑은 AEM 폴더 메타데이터 스키마 내에 정의됩니다. 폴더 메타데이터 스키마는 AEM에서 평소대로 생성 및 구성해야 합니다. Workfront 도구는 각 폴더 메타데이터 스키마 양식 필드의 설정 구성 탭에 자동 완성 드롭다운을 추가합니다. 이 자동 완성 드롭다운 메뉴를 사용하여 각 AEM 폴더 속성을 매핑할 Workfront 필드를 지정할 수 있습니다.

매핑을 구성하려면 다음 단계를 수행합니다.

1. `wf-workfront-users` 그룹에 대해 `/conf/global/settings/dam/adminui-extension/foldermetadataschema`에 `jcr:read` 권한을 추가하십시오.
1. **[!UICONTROL 도구]** > **[!UICONTROL Assets]** > **[!UICONTROL 폴더 메타데이터 스키마]**&#x200B;로 이동합니다.
1. 편집하려는 폴더 메타데이터 스키마 양식을 선택하고 편집을 누릅니다.
1. 편집하려는 폴더 메타데이터 스키마 양식 필드를 선택하고 오른쪽 패널에서 설정 탭을 선택합니다.
1. [!UICONTROL Workfront 필드에서 매핑됨] 필드에서 선택한 AEM 폴더 속성에 매핑할 Workfront 필드의 이름을 선택합니다. 사용 가능한 옵션은 다음과 같습니다.

   * 프로젝트 사용자 정의 양식 필드
   * 프로젝트 개요 필드(ID, 이름, 설명, 참조 번호, 계획된 완료 일자, 프로젝트 소유자, 프로젝트 스폰서, Portfolio 또는 프로그램)

![메타데이터 매핑 구성](/help/assets/assets/wf-metadata-mapping-config2.png)

### 자산 메타데이터 매핑 구성 {#asset-metadata-mapping}

Adobe Workfront 문서와 Assets 간의 메타데이터 매핑은 AEM 메타데이터 스키마 내에 정의됩니다. 메타데이터 스키마는 AEM에서 평소대로 생성 및 구성해야 합니다. Workfront 도구는 각 메타데이터 스키마 양식 필드의 설정 구성 탭에 구성 옵션을 추가합니다. 이 옵션을 사용하면 각 AEM 속성을 매핑할 Workfront 필드를 지정할 수 있습니다.

매핑을 구성하려면 다음 단계를 수행합니다.

1. **도구** > **Assets** > **메타데이터 스키마**&#x200B;로 이동합니다.
1. 편집할 메타데이터 스키마 양식을 선택하고 **편집**&#x200B;을 클릭하거나 메타데이터 스키마를 처음부터 만드십시오.
1. 편집할 메타데이터 스키마 양식 필드를 선택하고 오른쪽 패널에서 **설정** 탭을 선택합니다.
1. [!DNL Workfront] 사용자 정의 양식 필드에서 선택한 AEM 속성에 매핑할 [!DNL Workfront] 필드의 이름을 선택합니다. 사용 가능한 옵션은 다음과 같습니다.

   * 문서 사용자 정의 양식 필드
   * 프로젝트 사용자 정의 양식 필드
   * 문제 사용자 정의 양식 필드
   * 작업 사용자 정의 양식 필드
   * 프로젝트 개요 필드(ID, 이름, 설명 또는 참조 번호)

1. [!UICONTROL Workfront 사용자 정의 양식 필드]에서 선택한 [!DNL Workfront] 필드가 Workfront 사용자 유형 미리 필드인 경우 매핑할 Workfront 사용자 필드를 지정해야 합니다. 이렇게 하려면 Workfront 참조 개체 필드에서 값 가져오기 를 선택한 다음 매핑할 값을 검색할 [!UICONTROL Workfront 사용자 정의 양식 필드]의 이름을 지정하십시오.

   ![메타데이터 매핑 구성](/help/assets/assets/wf-metadata-mapping-config1.png)

## 맵 속성 {#map-property}

이 워크플로 단계를 통해 사용자는 속성을 프로젝트, 작업, 문제 또는 문서의 [!DNL Workfront] 사용자 정의 양식에 매핑할 수 있습니다. 이 단계가 영향을 주는 [!DNL Workfront] 아티팩트는 페이로드의 상대 경로를 사용하여 조회됩니다. 매핑될 속성은 단계 대화 상자 구성 내에서 제어됩니다.

**유형**: 이 필드에서는 속성을 매핑해야 하는 Workfront 개체 유형을 선택할 수 있습니다.

**ID 속성**: 이 필드에서는 속성을 매핑해야 하는 Workfront 개체의 ID에 대한 경로를 지정할 수 있습니다. 이 필드에 지정된 경로는 워크플로 페이로드에 상대적이어야 합니다.

**속성 할당**: 이 다중 필드를 사용하면 AEM 속성과 Workfront 필드 간의 매핑을 지정할 수 있습니다. 다중 필드의 각 항목은 하나의 매핑을 지정합니다. 각 매핑에는 `<workfront-field>=<aem-mapped-property>` 형식이 있어야 합니다.

* `workfront-field`은(는) 다음과 같을 수 있습니다

   * 접두사 `DE:`(으)로 식별된 사용자 정의 양식 필드.
   * 이름으로 식별되는 편집 가능한 필드. 필드 이름이 [[!DNL Workfront] API 탐색기](https://experience.workfront.com/s/api-explorer)에 있습니다.

* `aem-mapped-property`은(는) 다음과 같을 수 있습니다.

   * 리터럴 값. 따옴표로 묶어야 합니다.
   * AEM 속성입니다. 이 참조는 워크플로우 페이로드에 상대적이어야 합니다.
   * 명명된 값입니다. 이러한 요소는 괄호로 묶어야 합니다.
   * 위의 3개 항목의 연결입니다. `{+}`을(를) 사용하여 지정하십시오.
   * 값을 `{replace(<value>,"old-char","new-char")}`(으)로 둘러싸서 위의 3개 항목을 변경하는 것입니다.

* 예를 들면 다음과 같습니다.

   * `status="INP"`
   * `DE:Asset Type=jcr:content/metadata/assetType`
   * `DE:Path={path}`
   * `URL="https://my-aem-author/assets.html"{+}{path}`

![속성을 매핑하는 구성](/help/assets/assets/wf-map-property-config.png)

## 상태 설정 {#set-status}

워크플로 편집기에서 **[!UICONTROL 인수]** 탭에서 **[!UICONTROL Workfront - 상태 설정]**&#x200B;의 속성을 편집합니다.

![상태를 설정할 워크플로 편집](/help/assets/assets/wf-set-status.png)

## 주석 동기화 {#comments-sync}

1. [!DNL Experience Manager]에서 **[!UICONTROL 도구]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Workfront 도구 구성]**&#x200B;에 액세스하여 구성을 선택하고 **[!UICONTROL 속성]**&#x200B;을 선택합니다.

   ![댓글 동기화](/help/assets/assets/comments-sync1.png)

1. **[!UICONTROL 이벤트 구독]** 탭을 선택하고 **[!UICONTROL Workfront에서 만든 댓글을 AEM으로 보내기]** 옵션에서 **[!UICONTROL 댓글 동기화 사용]**&#x200B;을 클릭합니다.

   ![동기화가 활성화됨](/help/assets/assets/wf-comment-sync-enabled.png)

Workfront에서 AEM으로의 주석 동기화를 테스트하려면 다음 단계를 수행하십시오.

1. Workfront에서 연결된 문서로 이동하여 업데이트 탭에 댓글을 추가합니다.

   ![Workfront에 주석 남기기](/help/assets/assets/comments-sync2.png)

1. AEM에서 연결된 동일한 문서로 이동하여 문서를 선택하고 왼쪽 탐색에서 [!UICONTROL 타임라인] 옵션을 연 다음 [!UICONTROL 설명]을 선택합니다. 왼쪽 사이드바에 [!DNL Workfront]에서 동기화된 댓글이 표시됩니다.

## 에셋 버전 {#asset-versions}

AEM에서 에셋의 버전 기록을 유지 관리하려면 AEM에서 에셋 버전 관리를 구성합니다.

1. Experience Manager에서 **[!UICONTROL 도구]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Workfront 도구 구성]**&#x200B;에 액세스하여 **[!UICONTROL 고급]** 탭을 엽니다.

1. **[!UICONTROL 기존 에셋 버전과 같은 이름의 에셋 저장]** 옵션을 선택하십시오. 선택하면 이 옵션을 사용하여 업로드된 에셋을 기존 에셋 버전과 동일한 위치에 저장할 수 있습니다. 선택하지 않으면 다른 이름으로 새 에셋이 만들어집니다(예: `asset-name.pdf` 및 `asset-name-1.pdf`).

1. **[!UICONTROL 버전을 만들 때 자산 메타데이터 업데이트]** 옵션을 선택하십시오. 선택하면 이 옵션은 자산의 새 버전이 생성될 때마다 자산 메타데이터를 업데이트합니다. 선택하지 않으면 에셋은 새 버전을 만들기 전에 보유했던 메타데이터를 유지합니다.

![자산 버전 관리 구성](/help/assets/assets/wf-config-versioning.png)

>[!NOTE]
>
>링크된 폴더에서는 버전 관리가 지원되지 않습니다. 연결된 폴더 내에 문서를 사용하여 [!DNL Workfront] 증명을 만들 때 이전 버전의 에셋에 대한 댓글 및 주석이 제거됩니다.

## 사용자 정의 양식 첨부 {#attach-custom-forms}

이 워크플로 단계를 통해 사용자는 사용자 정의 양식을 [!DNL Workfront] 아티팩트에 첨부할 수 있습니다. 이 워크플로 단계는 모든 워크플로 모델에 추가할 수 있습니다. 이 단계에 영향을 주는 [!DNL Workfront] 아티팩트는 페이로드의 상대 경로를 사용하여 조회됩니다.

Experience Manager의 워크플로 편집기에서 [!UICONTROL Workfront - 사용자 정의 양식 첨부] 워크플로 단계의 속성을 편집합니다.

![사용자 정의 양식](/help/assets/assets/wf-custom-forms.png).

## 자산 자동 게시 {#auto-publish-assets}

1. Experience Manager에서 **[!UICONTROL 도구]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Workfront 도구 구성]**&#x200B;에 액세스하여 **[!UICONTROL 고급]** 탭을 엽니다.

1. **[!UICONTROL Workfront에서 전송할 때 자동으로 자산 게시]**&#x200B;를 선택합니다. 이 옵션을 사용하면 Workfront에서 AEM으로 에셋을 전송할 때 에셋을 자동으로 게시할 수 있습니다. 이 기능은 Workfront 사용자 정의 양식 필드 및 설정해야 하는 값을 지정하여 조건부로 활성화할 수 있습니다. 문서가 AEM으로 전송될 때마다 해당 조건을 충족하면 자산이 자동으로 게시됩니다.

1. 프로젝트 완료 시 **[!UICONTROL Publish에 모든 프로젝트 자산을 Brand Portal으로 선택]**&#x200B;합니다. 이 옵션을 사용하면 에셋이 속한 Workfront 프로젝트의 상태가 `Complete`(으)로 변경될 때 에셋을 [!DNL Brand Portal]에 자동으로 게시할 수 있습니다.

![자동 게시 구성](/help/assets/assets/wf-auto-publish-config.png)

## Workfront 문서 사용자 정의 양식 업데이트 {#subscribe-workfront-doc-custom-form-updates}

[!DNL Workfront] 문서 사용자 정의 양식의 변경 내용을 구독하려면 **[!UICONTROL 고급]** 탭에서 관련 옵션을 선택하십시오. 이 업데이트를 구독하면 [!DNL Workfront] 문서 사용자 지정 양식의 해당 필드가 변경될 때 매핑된 [!DNL Experience Manager] 메타데이터 필드가 업데이트됩니다.

[!DNL Experience Manager]![&#128279;](/help/assets/assets/wf-custom-form-update.png)의 Workfront 문서 사용자 지정 양식 업데이트 구성
