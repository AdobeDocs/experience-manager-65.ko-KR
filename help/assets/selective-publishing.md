---
title: Dynamic Media에서 선택적 게시 사용
description: 동적 미디어에서 선택적 게시로 작업하는 방법에 대한 정보입니다.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
translation-type: tm+mt
source-git-commit: 6e7368663d18dd0b5b46be9e292dba17577acf70
workflow-type: tm+mt
source-wordcount: '2934'
ht-degree: 2%

---


# Dynamic Media의 폴더 수준에서 선택적 게시 구성 {#selective-publish-configure-folder}

게시 **[!UICONTROL 관리]** 또는 **[!UICONTROL 빠른 게시]** 를 사용하여 폴더 수준에서 AEM 또는 Dynamic Media에 자산을 게시하거나 게시 **[!UICONTROL 취소할 수 있습니다. 단, Dynamic Media 인스턴스의 모든 폴더에 설정이 전역]** 상태인Dynamic Media 구성에만 의존하지않습니다.

예를 들어, 선택적 게시에서는 아직 라이브가 아닌 제품의 자산으로 작업할 수 있습니다. 이러한 경우 마케팅 팀은 글로벌 전달을 위해 Dynamic Media에 이러한 자산을 게시하지 않고도 홍보 자료를 만들 수 있도록 다이내믹 미디어와 동기화된 스마트 자르기 이미지 및 다이내믹 표현물에 액세스할 수 있습니다.

>[!IMPORTANT]
>
>선택적 게시는 다이내믹 미디어 - Scene7 모드에서만 사용할 수 있습니다.

>[!NOTE]
>
>*자산을 폴더로 복사하면* 해당 자산의 게시 상태가 지워집니다. 하지만 폴더 속성이 *선택적 게시로 설정된 폴더 간에 자산을 이동할* 경우 ****&#x200B;해당 자산의 게시 상태가 유지됩니다.

나중에 폴더에서 **[!UICONTROL 선택적 게시]** 설정을 변경하기로 결정한 경우, 이러한 변경 사항은 해당 시점부터 해당 폴더에 업로드한 새 자산에만 영향을 줍니다. 빠른 게시 **[!UICONTROL 또는 게시]** 관리 대화 상자에서 수동으로 변경할 때까지 폴더에 있는 기존 자산의 게시 상태는 그대로 유지됩니다 **** .

폴더 수준 **[!UICONTROL 다이내믹 미디어 게시 모드]** 옵션은 항상 **[!UICONTROL 다이내믹 미디어 구성의 자산]** 게시 **[!UICONTROL 설정에 있는 값]**&#x200B;으로 기본 설정됩니다. 하지만 이 항목의 다음 단계에서는 폴더 수준에서 이 기본값을 수동으로 변경(다음 단계에 설명된 대로)하여 **[!UICONTROL 다이내믹 미디어 구성]** 값을 무시하는 방법을 보여 줍니다.

다이내믹 미디어 구성 **[!UICONTROL 또는]** 다이내믹 미디어 구성 **[!UICONTROL 에 설정된]**&#x200B;게시 자산 **[!UICONTROL 값]** 에 대해 상관 없이, 폴더 속성에 설정된 **[!UICONTROL 게시 게시 게시 모드]**&#x200B;모드 값 **[!UICONTROL 에 관계없이, 동적 미디어]**&#x200B;를 즉시 선택할 수 있습니다. 다이내믹 미디어, 즉시 사용 가능 **[!UICONTROL , Dynamic Upon Activation, Photo PublishFeel, 선택적Publish]** Dynamic PriateEvar이이이이이이이이 될 수 있습니다. 예를 들어, **[!UICONTROL 동적 미디어 구성]** 에서 자산 **** 게시 **[!UICONTROL 값을 활성화]****[!UICONTROL 시]** 로 설정하되, 폴더 수준에서 **[!UICONTROL 다이내믹 미디어 게시 모드 값을 설정하여 선택적으로 게시, 게시]**, 버그가 되게 하거나 반대로 작동하도록 설정할 수 있습니다.

폴더에서 선택적 게시를 구성한 후에는 다음 중 하나를 수행할 수 있습니다.

* [게시 관리를 사용하여 선택적으로 자산을 Dynamic Media 또는 AEM에 게시할 수 있습니다.](#selective-publish-manage-publication)
* [게시 관리를 사용하여 Dynamic Media 또는 AEM에서 선택적으로 자산을 게시 취소합니다.](#selective-unpublish-manage-publication)
* [빠른 게시를 사용하여 Dynamic Media 또는 AEM에 자산 게시](#quick-publish-aem-dm)
* [검색 결과를 통해 선택적으로 자산을 게시하거나 게시 취소합니다.](#selective-publish-unpublish-search-results)

**Dynamic Media의 폴더 수준에서 선택적 게시를 구성하려면**

1. AEM에서 AEM 로고를 눌러 글로벌 탐색 콘솔에 액세스합니다. 왼쪽에서 탐색 아이콘(도구 아이콘 바로 위)을 누른 다음 **[!UICONTROL 자산 > 파일을 누릅니다.]**
1. 다음 중 하나를 수행하십시오.
   * 기존 폴더의 속성 편집 - 카드 보기 **[!UICONTROL ,]**&#x200B;열 보기 **[!UICONTROL 또는]**&#x200B;목록 보기 **[!UICONTROL 에서]**&#x200B;속성을 편집할 폴더를 탐색합니다. 폴더를 선택한 다음 도구 모음에서 속성을 **[!UICONTROL 누릅니다.]**
   * 새 폴더의 속성 편집 - **[!UICONTROL 카드 보기]**, **[!UICONTROL 열 보기]**&#x200B;또는 **[!UICONTROL 목록]**&#x200B;보기에서 **[!UICONTROL 페이지의 오른쪽 위 모서리 근처에 있는 만들기 > 폴더를 탭합니다.]** 폴더 **[!UICONTROL 만들기]** 대화 상자에서 폴더의 제목(필수)을 입력한 다음 **[!UICONTROL 만들기를 누릅니다.]** 폴더를 선택한 다음 도구 모음에서 속성을 **[!UICONTROL 누릅니다.]**

1. 동기화 **[!UICONTROL 모드]** 드롭다운 목록에서 다음 중 하나를 선택합니다.
| 동기화 모드 | 설명 |
| — | — |
| **[!UICONTROL 상속됨]** | 폴더에 명시적 동기화 값이 없습니다.대신 폴더는 상위 폴더 중 하나 또는 **[!UICONTROL Dynamic Media 구성에 설정된 기본 모드에서 동기화 값을 상속받습니다]**. 상속됨 **[!UICONTROL 에]** 대한 세부 상태는 도구 설명을 통해 표시됩니다. |
| **[!UICONTROL 이 폴더 하위 트리의 모든 항목을 동적 미디어로 동기화]** | 성공적으로 Dynamic Media에 게시하려면 자산을 Dynamic Media에 동기화해야 합니다. 이 옵션을 선택하면 Dynamic Media와 동기화할 이 하위 트리에 있는 모든 자산이 포함됩니다. 폴더별 설정은 **[!UICONTROL 다이내믹 미디어 구성의 기본 설정을 덮어씁니다]**. |
| **[!UICONTROL 이 폴더 하위 트리의 모든 항목을 dynamicmedia 동기에서 제외]** | 이 하위 트리의 모든 자산을 Dynamic Media와 동기화하지 않도록 제외합니다. |

   ![폴더 수준 선택적 게시](/help/assets/assets-dm/createfolder-properties-selectivepublish.png)

1. Dynamic **[!UICONTROL Media 게시 모드]** 드롭다운 목록에서 옵션을 선택합니다. [ **[!UICONTROL 다이내믹 미디어 게시 모드]** ] 옵션은 항상 **[!UICONTROL 다이내믹 미디어 구성에 설정된 값으로 기본값이 설정됩니다]**. 하지만 다음 옵션 중 하나를 사용하여 이 기본 **[!UICONTROL Dynamic Media 구성]** 값을 수동으로 재정의할 수 있습니다.

   >[!IMPORTANT]
   >
   >선택한 다이내믹 미디어 게시 모드 옵션에 관계없이 나중에 *이미* 게시된 자산에 대한 업데이트를 추가 사용자 작업 없이 바로 게시된다는 점을 참고하십시오.

   | 다이내믹 미디어 게시 모드 옵션 | 설명 |
   | --- | --- |
   | **[!UICONTROL 즉시]** | 에셋이 이 폴더에 업로드되면 시스템이 에셋을 AEM에 인제스트하고 URL/포함을 즉시 제공합니다. 이 옵션은 AEM 게시 전용이며 자산을 게시하는 데 필요한 사용자 개입이 없습니다.<br>이전 단계의 동기화 모드에서 *이 폴더 하위 트리* 의 모든 항목을 동적 미디어 동기화에서 **[!UICONTROL 제외를 선택한 경우에는 이 옵션을 사용할 수]** 없습니다 **** . |
   | **[!UICONTROL 활성화 시]** | 에셋이 이 폴더에 업로드되면 URL/포함 링크가 제공되기 전에 먼저 명시적으로 에셋을 게시해야 합니다. 이 옵션은 AEM 게시에만 연결되어 있습니다.<br>이전 단계의 동기화 모드에서 *이 폴더 하위 트리* 의 모든 항목을 동적 미디어 동기화에서 **[!UICONTROL 제외를 선택한 경우에는 이 옵션을 사용할 수]** 없습니다 **** . |
   | **[!UICONTROL 선택적 게시]** | 자산은 공개 도메인에서 전달되도록 AEM 또는 Dynamic Media 중 하나를 선택하여 원하는 미디어에 게시됩니다. 두 게시 방법은 서로 배타적입니다.  즉, DMS7에 자산을 게시하여 스마트 자르기 또는 동적 표현물과 같은 기능을 사용할 수 있습니다. 또는 AEM에만 에셋을 게시하여 안전하게 미리 볼 수 있습니다.동일한 에셋은 공용 도메인에 전달되기 위해 DMS7에 게시되지 *않습니다* . 이전 단계의 [동기화 모드 **에서 이 폴더 하위 트리에서]** **** 모든 항목 제외를 선택한 경우에는 이 옵션을 사용할 수 없습니다. |
1. 페이지의 오른쪽 맨 위에서 **[!UICONTROL 저장 및 닫기를]**&#x200B;누른 다음 **[!UICONTROL 확인을]** 눌러 AEM Assets으로 돌아갑니다.

## 게시 관리를 사용하여 선택적으로 Dynamic Media 또는 AEM에 자산 게시{#selective-publish-manage-publication}

게시 **[!UICONTROL 관리]** 를 사용하여 자산을 Dynamic Media나 AEM에 선택적으로 게시하려면 먼저 **[!UICONTROL 다이내믹 미디어 구성의]** 자산 **[!UICONTROL 게시 옵션]** 을 선택적 게시 **[!UICONTROL 또는]** 선택적 게시로설정했거나, 폴더 수준에서 선택적 게시로 구성했는지 확인하십시오.

다이내믹 [미디어 구성](#configuring-dynamic-media-cloud-services) 만들기 또는 [Dynamic Media의 폴더 수준에서 선택적 게시 구성을 참조하십시오.](#selective-publish-configure-folder)

>[!IMPORTANT]
>
>선택적 게시는 다이내믹 미디어 - Scene7 모드에서만 사용할 수 있습니다.

>[!NOTE]
>
>*자산을 폴더로 복사하면* 해당 자산의 게시 상태가 지워집니다. 하지만 폴더 속성이 *선택적 게시로 설정된 폴더 간에 자산을 이동할* 경우 ****&#x200B;해당 자산의 게시 상태가 유지됩니다.

**게시 관리를 사용하여 자산을 Dynamic Media 또는 AEM에 선택적으로 게시하려면**

1. AEM에서 AEM 로고를 눌러 글로벌 탐색 콘솔에 액세스합니다. 왼쪽에서 탐색 아이콘(도구 아이콘 바로 위)을 누른 다음 **[!UICONTROL 자산 > 파일을 누릅니다.]**
1. 카드 **[!UICONTROL 보기]**, 열 **[!UICONTROL 보기]**&#x200B;또는 **[!UICONTROL 목록 보기에서]**&#x200B;다음 중 하나를 수행합니다.
   * 자산을 게시할 폴더로 이동합니다. 폴더를 선택한 다음 도구 모음에서 게시 **[!UICONTROL 관리를 누릅니다.]**  특정 폴더의 게시 상태를 보다 쉽게 확인할 수 있도록 **[!UICONTROL 목록]** 보기를 사용하는 것이 도움이 될 수 있습니다.
   * 자산을 게시할 폴더로 이동합니다. 폴더를 연 다음 하나 이상의 자산을 선택합니다. 도구 모음에서 게시 **[!UICONTROL 관리를 누릅니다]**. 특정 자산의 게시 상태를 보다 쉽게 확인할 수 있도록 **[!UICONTROL 목록]** 보기를 사용하는 것이 도움이 될 수 있습니다.

      >[!NOTE]
      >
      >도구 모음에 **[!UICONTROL 게시]** 관리 **[!UICONTROL 기능이 표시되지 않으면 줄임표 단추를 누른 다음 목록 메뉴에서]** 게시관리를 선택합니다.

1. 게시 **[!UICONTROL 관리 - 옵션]** 페이지의 **[!UICONTROL 작업]**아래에서 원하는 활성화 유형을 선택합니다.
| 동작 | 설명 |
| — | — |
| **[!UICONTROL 게시]** (AEM) | 안전한 미리 보기를 위해 AEM에 자산을 게시하려면 이 옵션을 선택합니다. |
| **[!UICONTROL Dynamic Media에 게시]** | 공용 도메인에 전달하기 위해 Dynamic Media에 자산을 게시하거나 스마트 자르기 또는 동적 표현물과 같은 기능을 사용할 수 있도록 하려면 이 옵션을 선택하십시오.<br>이 옵션은 폴더 속성에서 **[!UICONTROL 다이내믹 미디어 게시 모드]** 가 **[!UICONTROL 선택적 게시]** 로설정된 경우에만 사용할 수 있습니다. |
1. 예약 **[!UICONTROL 에서]**게시 시간을 설정합니다.
| 일정 | 설명 |
| — | — |
| **[!UICONTROL 지금]** | 자산을 즉시 게시하려면 선택합니다. |
| **[!UICONTROL 나중에]** | 특정 날짜 및 시간에 자산을 게시하려면 선택합니다. |
1. [게시 **[!UICONTROL 관리]** ] 페이지의 오른쪽 맨 위에서 [다음]을 **[!UICONTROL 누릅니다]**.
1. 게시 **[!UICONTROL 관리 - 범위]** 페이지에서 다음 중 하나를 수행합니다.
   * 필요한 경우 게시에서 제거할 자산을 하나 이상 선택합니다.
   * [게시 **[!UICONTROL 관리 - 범위]** ] 페이지의 오른쪽 맨 위에서 **[!UICONTROL 게시]** 또는 **[!UICONTROL Dynamic Media에게시를누릅니다.]**
1. 확인을 **[!UICONTROL 누릅니다]**.

### 게시 관리를 사용하여 Dynamic Media 또는 AEM에서 선택적으로 자산 게시 취소 {#selective-unpublish-manage-publication}

1. AEM에서 AEM 로고를 눌러 글로벌 탐색 콘솔에 액세스합니다. 왼쪽에서 탐색 아이콘(도구 아이콘 바로 위)을 누른 다음 **[!UICONTROL 자산 > 파일을 누릅니다.]**
1. 카드 **[!UICONTROL 보기]**, 열 **[!UICONTROL 보기]**&#x200B;또는 **[!UICONTROL 목록 보기에서]**&#x200B;다음 중 하나를 수행합니다.
   * 게시 취소할 에셋이 있는 폴더로 이동합니다. 폴더를 선택한 다음 도구 모음에서 게시 **[!UICONTROL 관리를 누릅니다.]**  특정 폴더의 게시 상태를 보다 쉽게 확인할 수 있도록 **[!UICONTROL 목록]** 보기를 사용하는 것이 도움이 될 수 있습니다.
   * 게시 취소할 에셋이 있는 폴더로 이동합니다. 폴더를 연 다음 하나 이상의 자산을 선택합니다. 도구 모음에서 게시 **[!UICONTROL 관리를 누릅니다]**. 특정 자산의 게시 상태를 보다 쉽게 확인할 수 있도록 **[!UICONTROL 목록]** 보기를 사용하는 것이 도움이 될 수 있습니다.

      >[!NOTE]
      >
      >도구 모음에 **[!UICONTROL 게시]** 관리 **[!UICONTROL 기능이 표시되지 않으면 줄임표 단추를 누른 다음 목록 메뉴에서]** 게시관리를 선택합니다.

1. 게시 **[!UICONTROL 관리 - 옵션]** 페이지의 **[!UICONTROL 작업]**아래에서 원하는 비활성화 유형을 선택합니다.
| 동작 | 설명 |
| — | — |
| **[!UICONTROL 게시]** 취소(AEM) | AEM에서 자산을 게시 취소하려면 이 옵션을 선택합니다. |
| **[!UICONTROL Dynamic Media에서 게시 취소]** | Dynamic Media에서 자산을 게시 취소하려면 이 옵션을 선택합니다.<br>이 옵션은 폴더 속성에서 **[!UICONTROL 다이내믹 미디어 게시 모드]** 가 **[!UICONTROL 선택적 게시]** 로설정된 경우에만 사용할 수 있습니다.  |
1. 예약 **[!UICONTROL 에서]**비활성화 시간을 설정합니다.
| 일정 | 설명 |
| — | — |
| **[!UICONTROL 지금]** | 자산을 즉시 게시 취소하려면 선택합니다. |
| **[!UICONTROL 나중에]** | 특정 날짜와 시간에 자산을 게시 취소하려면 선택합니다. |
1. [게시 **[!UICONTROL 관리]** ] 페이지의 오른쪽 맨 위에서 [다음]을 **[!UICONTROL 누릅니다]**.
1. 게시 **[!UICONTROL 관리 - 범위]** 페이지에서 다음 중 하나를 수행합니다.
   * 게시 취소에서 제거할 자산을 하나 이상 선택합니다.
   * [게시 **[!UICONTROL 관리 - 범위]** ] 페이지의 오른쪽 맨 위에서 Dynamic Media **[!UICONTROL 에서 게시]** 취소 **[!UICONTROL 또는]**&#x200B;게시 취소를 누릅니다.
1. 확인을 **[!UICONTROL 누릅니다]**.

## 빠른 게시를 사용하여 Dynamic Media 또는 AEM에 자산 게시 {#quick-publish-aem-dm}

간단한 에셋 **[!UICONTROL 활성화]** 케이스에 빠른 게시를 사용할 수 있습니다. **[!UICONTROL 빠른 게시]** 기능은 추가 사용자 상호 작용 없이 선택한 자산을 즉시 게시합니다. 이로 인해 게시되지 않은 참조도 자동으로 게시됩니다.

>[!NOTE]
>
>빠른 게시 **[!UICONTROL 를]** 사용하여 자산을 Dynamic Media 또는 AEM에 게시하려면 **[!UICONTROL 선택적 게시]** 가 **[!UICONTROL Dynamic Media 구성]** 또는 선택한 폴더의 폴더속성에서활성화되어 있어야 합니다.

**빠른 게시를 사용하여 Dynamic Media 또는 AEM에 자산을 게시하려면**

1. AEM에서 AEM 로고를 눌러 글로벌 탐색 콘솔에 액세스합니다. 페이지 왼쪽에서 내비게이션 아이콘(도구 아이콘 바로 위)을 누른 다음 페이지의 오른쪽에서 **[!UICONTROL 자산 > 파일을 누릅니다.]**
1. 카드 **[!UICONTROL 보기]**, 열 **[!UICONTROL 보기]**&#x200B;또는 **[!UICONTROL 목록 보기에서]**&#x200B;다음 중 하나를 수행합니다.
   * 자산을 게시할 폴더로 이동합니다. 폴더를 선택한 다음 도구 모음에서 **[!UICONTROL 빠른 게시를 누릅니다.]**  특정 폴더의 게시 상태를 보다 쉽게 확인할 수 있도록 **[!UICONTROL 목록]** 보기를 사용하는 것이 도움이 될 수 있습니다.
   * 자산을 게시할 폴더로 이동합니다. 폴더를 연 다음 하나 이상의 자산을 선택합니다. 도구 모음에서 **[!UICONTROL 빠른 게시를 누릅니다]**. 특정 자산의 게시 상태를 보다 쉽게 확인할 수 있도록 **[!UICONTROL 목록]** 보기를 사용하는 것이 도움이 될 수 있습니다.

      >[!NOTE]
      >
      >도구 모음에 **[!UICONTROL 빠른 게시]** 가 표시되지 않으면 줄임표 단추를 누른 다음 목록 메뉴에서 **[!UICONTROL 빠른 게시]** 를 선택합니다.

      ![Dynamic Media에 폴더 수준 빠른 게시](/help/assets/assets-dm/selective-publish-folder-quick-publish-to-dm.png)
1. 빠른 게시 메뉴 목록에서 다음 옵션 중 **[!UICONTROL 하나를]** 선택합니다.
| 빠른 게시 옵션 | 기능 |
| — | — |
| AEM에 게시 | 선택한 자산을 AEM에 즉시 게시합니다. |
| 브랜드 포털에 게시 | 선택한 자산을 **[!UICONTROL 브랜드 포털에 즉시 게시합니다]**.<br>이 옵션은 AEM Assets 인스턴스에 이미 **[!UICONTROL 브랜드 포털이 구성된 경우에만 사용할]** 수 있습니다. |
| 다이내믹 미디어에 게시 | 선택한 자산을 Dynamic Media에 즉시 게시합니다.<br>자산은 이미 Dynamic Media에 동기화되어야 합니다. 필요한 경우 폴더 속성의 **[!UICONTROL 동기화 모드]** 가 이 폴더 하위 트리의 모든 것 **[!UICONTROL 동기화에서 동적 미디어로 이미 설정되어 있는지 확인하십시오]**. |
1. 확인을 **[!UICONTROL 누른]**&#x200B;다음 **[!UICONTROL 닫기를 누릅니다]**.

## 검색 결과를 통해 선택적으로 자산 게시 또는 게시 취소 {#selective-publish-unpublish-search-results}

검색 결과는 Dynamic Media 게시 설정이 다른 자산 폴더에서 나온 자산을 표시할 수 있습니다. 검색 결과에서 하나 이상의 자산을 선택한 경우, 자산에 다른 Dynamic Media 게시 모드 설정이 있는 경우, 도구 모음에서 **[!UICONTROL 게시]** 관리를 트리거하여 게시하거나 게시를 취소할 수 있습니다.

AEM에서 [자산 검색을 참조하십시오.](/help/assets/search-assets.md)

**검색 결과를 통해 선택적으로 자산을 게시하거나 게시 취소하려면**

1. AEM 페이지의 왼쪽 위 모서리에서 AEM 로고를 눌러 글로벌 탐색 콘솔에 액세스합니다. 페이지 왼쪽에서 탐색 아이콘(도구 아이콘 바로 위)을 누른 다음 **[!UICONTROL 자산 > 파일을 누릅니다.]**
1. 페이지의 오른쪽 위 모서리 근처에 있는 도구 모음에서 검색 아이콘(확대경)을 누릅니다.
1. 검색할 **[!UICONTROL 유형]** 텍스트 필드에 키워드를 입력한 다음 Enter 키를 **[!UICONTROL 누릅니다]**.
1. 페이지의 오른쪽 위 모서리 근처에 있는 목록 보기 **[!UICONTROL 아이콘을]** 누릅니다.
1. 페이지의 왼쪽 위 모서리 근처에 있는 필터 **[!UICONTROL 아이콘을]** 누릅니다.

   ![검색 결과의 목록 보기 및 필터](/help/assets/assets-dm/select-publish-search-result.png)

1. 왼쪽 패널에서 **[!UICONTROL 상태]**&#x200B;를 확장한 다음 **[!UICONTROL 동적 미디어]** 검색 조건자를 확장합니다.
1. 게시된 **[!UICONTROL 자산]** 및 **[!UICONTROL 게시]** 취소 확인란을 사용하여 게시된 Dynamic Media 자산의상태를 기반으로 검색 결과를 더 세분화합니다.
원할 경우, 이 확인란을 **[!UICONTROL 게시]** 검색 술어와 함께 사용하여 게시됨 및 게시되지 않은 **[!UICONTROL AEM]** 자산의 **[!UICONTROL 검색 결과를]** 조정할수있습니다.
1. 다음 중 하나를 수행하십시오.
   * 게시하거나 게시를 취소할 자산을 하나 이상 선택합니다.
   * [검색 결과] 페이지의 오른쪽 **[!UICONTROL 위 모서리]** 근처에 있는 **[!UICONTROL 모두 선택을 탭합니다]**.
1. 도구 모음에서 게시 **[!UICONTROL 관리를 누릅니다]**. 도구 모음에서 줄임표 아이콘을 눌러 게시 **[!UICONTROL 관리를 볼 수 있습니다]**.
1. 게시 **[!UICONTROL 관리 - 옵션]** 페이지에서 원하는 작업을 선택합니다.

   | 선택한 작업 | 다이내믹 미디어 구성에서 자산 게시 설정 | 자산은 |
   | --- | --- | --- |
   | 게시 | 즉시 또는 활성화 시 | AEM 및 Dynamic Media에 게시되었습니다. |
   | 게시 | 선택적 게시 | AEM에만 게시됨 |
   | 게시 취소 | 즉시 또는 활성화 시 | AEM 및 Dynamic Media에서 게시 취소됨 |
   | 게시 취소 | 선택적 게시 | AEM에서만 게시 취소됨. |
   | Dynamic Media에 게시 | 즉시 또는 활성화 시 | AEM, Dynamic Media 또는 두 가지 모두에 게시되지 않습니다. |
   | Dynamic Media에 게시 | 선택적 게시 | Dynamic Media에만 게시되었습니다. |
   | Dynamic Media에서 게시 취소 | 즉시 또는 활성화 시 | AEM, Dynamic Media 또는 두 가지 모두에서 게시 취소되지 않습니다. |
   | Dynamic Media에서 게시 취소 | 선택적 게시 | Dynamic Media에서만 게시 취소됩니다. |
1. 예약 **[!UICONTROL 에서]**비활성화 시간을 설정합니다.
| 선택한 일정 | 발생하는 일 |
| — | — |
| 지금 | 선택한 작업이 즉시 수행됩니다. |
| 나중에 | 선택한 작업이 선택한 특정 날짜 및 시간에 실행됩니다. |
1. [게시 관리 - 옵션] **[!UICONTROL 페이지의 오른쪽 맨 위에서 [다음]을]** 누릅니다 ****.
1. (선택 사항) **[!UICONTROL 게시 관리 - 범위]** 페이지에서 선택한 자산에 대한 테이블의 **[!UICONTROL 게시 Target]** 열을검토하십시오.

   | 다이내믹 미디어 구성에서 자산 게시 설정 | 선택한 작업 | 게시 대상 |
   | --- | --- | --- |
   | 즉시 또는 <br>활성화 시 | 게시 | AEM 및 Dynamic Media |
   | 즉시 또는 <br>활성화 시 | Dynamic Media에 게시 | 없음 |
   | 선택적 게시 | 게시 | AEM |
   | 선택적 게시 | Dynamic Media에 게시 | 다이내믹 미디어 |
   | 즉시 또는 <br>활성화 시 | 게시 취소 | AEM 및 Dynamic Media |
   | 즉시 또는 <br>활성화 시 | Dynamic Media에서 게시 취소 | 없음 |
   | 선택적 게시 | 게시 취소 | AEM |
   | 선택적 게시 | Dynamic Media에서 게시 취소 | 다이내믹 미디어 |

1. 게시 **[!UICONTROL 관리 - 범위]** 페이지에서 다음 중 하나를 수행합니다.
   * 게시 또는 게시 취소에서 제거할 자산을 하나 이상 선택합니다.
   * [게시 **[!UICONTROL 관리 - 범위]** ] 페이지의 오른쪽 맨 위에서 **[!UICONTROL 게시]** 또는 게시 **[!UICONTROL 취소]** 를 눌러 작업을시작합니다.
1. 확인을 **[!UICONTROL 누릅니다]**.

## 자산의 게시 상태 확인 {#check-publish-status-of-asset}

AEM에서 **** 카드 보기 **[!UICONTROL , 열 보기]**&#x200B;또는 **[!UICONTROL 목록 보기]**&#x200B;를 사용하여 **** 자산의 게시 상태를 빠르게 확인할 수 있습니다.

**자산의 게시 상태를 확인하려면**

1. AEM 페이지의 왼쪽 위 모서리에서 AEM 로고를 눌러 글로벌 탐색 콘솔에 액세스합니다. 페이지 왼쪽에서 탐색 아이콘(도구 아이콘 바로 위)을 누른 다음 **[!UICONTROL 자산 > 파일을 누릅니다.]**
1. [ **[!UICONTROL 카드 보기]**], [ **[!UICONTROL 열 보기]**] 또는 [ **[!UICONTROL 목록 보기]** ](아래 스크린샷은 **[!UICONTROL 목록 보기]**)에서 게시했거나 게시 취소된 자산이 들어 있는 폴더를 엽니다.
1. 확인 표시가 있는 에셋을 선택합니다. 예를 들어 아래 스크린샷을 참조하십시오.
1. 페이지의 왼쪽 위 모서리 근처에 있는 드롭다운 메뉴에서 **[!UICONTROL 타임라인을 선택합니다]**. 왼쪽 **[!UICONTROL 패널의 상태]** 영역에는 선택한 자산의 게시 상태가 표시됩니다.
목록 보기 **[!UICONTROL 를]**&#x200B;사용하면 **[!UICONTROL Dynamic Media]** 게시 상태에 대한 추가 열이나타납니다.
   * Dynamic Media에 동기화하도록 구성된 폴더는 기본적으로 **[!UICONTROL Dynamic Media]** 열을 표시합니다.
   * Dynamic Media에 동기화하도록 *구성되지* 않은 폴더는 Dynamic Media 열을 표시하지 않습니다.
      ![목록 보기 및 타임라인](/help/assets/assets-dm/selective-publish-status-timeline.png)

## 선택적 게시 문제 해결 {#selective-publish-troubleshoot}

Dynamic Media와 동기화되지 않았지만 Dynamic Media 게시 동작이 트리거된 에셋으로 인해 다음 오류 메시지와 솔루션이 발생합니다.

![선택적 게시 오류](/help/assets/assets-dm/selective-publish-error.png)

