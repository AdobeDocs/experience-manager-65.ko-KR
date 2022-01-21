---
title: Dynamic Media의 선택적 게시를 사용하여 작업
description: 폴더 수준에서 Adobe Experience Manager 또는 Dynamic Media으로 또는에서 자산을 게시 또는 게시 취소하도록 선택할 수 있습니다. Dynamic Media 인스턴스의 모든 폴더에 전역 설정을 적용하는 Dynamic Media 구성에 전적으로 의지하는 대신 Manage Publication 또는 Quick Publish를 사용할 수 있습니다.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User, Admin
exl-id: cd025e9d-6fb1-436c-9e78-795f2daaf345
feature: Publishing
source-git-commit: 664e22cc4c6acd74f285a4ec1a0dbd7d301240b7
workflow-type: tm+mt
source-wordcount: '3000'
ht-degree: 4%

---

# Dynamic Media의 폴더 수준에서 선택적 게시 구성 {#selective-publish-configure-folder}

폴더 수준에서 Adobe Experience Manager 또는 Dynamic Media으로 또는에서 자산을 게시 또는 게시 취소하도록 선택할 수 있습니다. 다음 중 하나를 사용할 수 있습니다 **[!UICONTROL 게시 관리]** 또는 **[!UICONTROL 빠른 게시]** 전적으로 의지하는 대신에 **[!UICONTROL Dynamic Media 구성]** Dynamic Media 인스턴스의 모든 폴더에 전역 설정을 적용하는 것이 좋습니다.

예를 들어 선택적 게시 기능을 사용하면 아직 라이브가 아닌 제품의 자산으로 작업할 수 있습니다. 이러한 경우 마케팅 팀은 Dynamic Media에 동기화된 스마트 자르기 이미지 및 동적 변환에 액세스할 수 있습니다. 글로벌 배송을 위해 Dynamic Media에 해당 자산을 게시하지 않고도 홍보 자료를 만들 수 있습니다.

>[!IMPORTANT]
>
>선택적 게시 는 Dynamic Media - Scene7 모드에서만 사용할 수 있습니다.

>[!NOTE]
>
>*복사* 폴더 간 및 폴더 간 자산은 해당 자산의 게시 상태를 지웁니다. 하지만, *이동* 폴더 속성이 **[!UICONTROL 선택적 게시]**&#x200B;로 설정되면 해당 자산의 게시 상태가 유지됩니다.

나중에 을(를) 변경하기로 결정하는 경우 **[!UICONTROL 선택적 게시]** 폴더의 설정에서는 해당 변경 사항이 해당 시점부터 해당 폴더에 업로드하는 새 자산에만 영향을 줍니다. 폴더에 있는 기존 자산의 게시 상태는 다음 중 하나에서 수동으로 변경할 때까지 그대로 유지됩니다 **[!UICONTROL 빠른 게시]** 또는 **[!UICONTROL 게시 관리]** 대화 상자

폴더 수준 **[!UICONTROL Dynamic Media 게시 모드]** 옵션은 항상 기본적으로 **[!UICONTROL 자산 게시]** 에서 설정 **[!UICONTROL Dynamic Media 구성]**. 그러나 이 항목의 다음 단계에서는 폴더 수준에서 이 기본값을 수동으로 변경하여 다음 단계에 설명된 대로 **[!UICONTROL Dynamic Media 구성]** 값.

다음 중 하나에 의존하는지 여부에 관계없이

* **[!UICONTROL 자산 게시]** 값 설정 **[!UICONTROL Dynamic Media 구성]**.
* **[!UICONTROL Dynamic Media 게시 모드]** 폴더 수준 속성에 설정된 값입니다.

선택할 수 있습니다 **[!UICONTROL 즉시]**, **[!UICONTROL 활성화 시]**, 또는 **[!UICONTROL 선택적 게시]**. 예를 들어 **[!UICONTROL 자산 게시]** 값 **[!UICONTROL Dynamic Media 구성]** to **[!UICONTROL 활성화 시]**&#x200B;로 설정되지만 **[!UICONTROL Dynamic Media 게시]** 폴더 수준의 모드 값에서 로 **[!UICONTROL 선택적 게시]**, 및 반대로

폴더에서 선택적 게시를 구성한 후 다음 중 하나를 수행할 수 있습니다.

* [게시 관리를 사용하여 Dynamic Media 또는 Experience Manager에 자산을 선택적으로 게시](#selective-publish-manage-publication).
* [게시 관리를 사용하여 Dynamic Media 또는 Experience Manager에서 선택적으로 자산 게시 취소](#selective-unpublish-manage-publication).
* [빠른 게시를 사용하여 Dynamic Media 또는 Experience Manager에 자산 게시](#quick-publish-aem-dm).
* [검색 결과를 통해 자산을 선택적으로 게시 또는 게시 취소합니다](#selective-publish-unpublish-search-results).

**Dynamic Media의 폴더 수준에서 선택적 게시를 구성하려면:**

1. Experience Manager에서 Experience Manager 로고를 선택하여 전역 탐색 콘솔에 액세스합니다. 왼쪽의 탐색 아이콘(도구 아이콘 바로 위)을 선택한 다음 을 선택합니다 **[!UICONTROL 자산]** > **[!UICONTROL 파일]**.
1. 다음 중 하나를 수행하십시오.
   * 기존 폴더의 속성 편집 - 위치 **[!UICONTROL 카드 보기]**, **[!UICONTROL 열 보기]**, 또는 **[!UICONTROL 목록 보기]**&#x200B;속성을 편집할 폴더로 이동합니다. 폴더를 선택한 다음 도구 모음에서 를 선택합니다 **[!UICONTROL 속성]**.
   * 새 폴더의 속성 편집 - 위치 **[!UICONTROL 카드 보기]**, **[!UICONTROL 열 보기]**, 또는 **[!UICONTROL 목록 보기]**&#x200B;페이지의 오른쪽 위 모서리 근처에 있는 를 선택하고 **[!UICONTROL 만들기]** > **[!UICONTROL 폴더]**. 에서 **[!UICONTROL 폴더 만들기]** 대화 상자에서 폴더의 제목(필수)을 입력한 다음 을 선택합니다 **[!UICONTROL 만들기]**. 폴더를 선택한 다음 도구 모음에서 를 선택합니다 **[!UICONTROL 속성]**.

1. 에서 **[!UICONTROL 동기화 모드]** 드롭다운 목록에서 다음 중 하나를 선택합니다.

   | 동기화 모드 | 설명 |
   | --- | --- |
   | **[!UICONTROL 상속됨]** | 폴더에 명시적 동기화 값이 없습니다. 대신 폴더는 상위 폴더 또는 **[!UICONTROL Dynamic Media 구성]**. 에 대한 자세한 상태 **[!UICONTROL 상속됨]** 도구 설명을 통해 표시합니다. |
   | **[!UICONTROL 이 폴더 하위 트리의 모든 항목을 Dynamic Media에 동기화]** | Dynamic Media에 게시하려면 자산을 Dynamic Media에 동기화해야 합니다. 이 옵션을 선택하면 Dynamic Media과 동기화할 이 하위 트리의 모든 자산이 포함됩니다. 폴더별 설정은 **[!UICONTROL Dynamic Media 구성]**. |
   | **[!UICONTROL Dynamic Media 동기화에서 이 폴더 하위 트리의 모든 항목 제외]** | 이 하위 트리의 모든 자산이 Dynamic Media과 동기화되지 않도록 제외합니다. |

   ![폴더 수준 선택적 게시](/help/assets/assets-dm/createfolder-properties-selectivepublish.png)

1. 에서 **[!UICONTROL Dynamic Media 게시 모드]** 드롭다운 목록에서 옵션을 선택합니다. 다음 **[!UICONTROL Dynamic Media 게시 모드]** 옵션은 항상 기본적으로 **[!UICONTROL Dynamic Media 구성]**. 그러나 이 기본값을 수동으로 재정의할 수 있습니다 **[!UICONTROL Dynamic Media 구성]** 다음 옵션 중 하나를 사용하여 값을 설정합니다.

   >[!IMPORTANT]
   >
   >선택한 Dynamic Media 게시 모드 옵션에 관계없이 나중에 가 자산 *이미* 게시됨: 추가 사용자 작업 없이 해당 업데이트가 즉시 게시됩니다.
   >
   >게시된 비디오가 업데이트되면 게재의 변경 사항을 반영하려면 다시 게시해야 합니다.

   | Dynamic Media 게시 모드 옵션 | 설명 |
   | --- | --- |
   | **[!UICONTROL 즉시]** | 자산이 이 폴더에 업로드되면 시스템은 자산을 Experience Manager에 수집하고 URL/포함을 즉시 제공합니다. 이 옵션은 Experience Manager 게시에만 연결되어 있으며 자산을 게시하는 데 사용자 개입이 필요하지 않습니다.<br>이 옵션은 다음과 같습니다 *not* 선택한 경우 사용 가능 **[!UICONTROL Dynamic Media 동기화에서 이 폴더 하위 트리의 모든 항목 제외]** in **[!UICONTROL 동기화 모드]** 를 클릭하십시오. |
   | **[!UICONTROL 활성화 시]** | 자산을 이 폴더에 업로드할 때 URL/포함 링크가 제공되기 전에 먼저 자산을 명시적으로 게시해야 합니다. 이 옵션은 Experience Manager 게시에만 연결되어 있습니다.<br>이 옵션은 다음과 같습니다 *not* 선택한 경우 사용 가능 **[!UICONTROL Dynamic Media 동기화에서 이 폴더 하위 트리의 모든 항목 제외]** in **[!UICONTROL 동기화 모드]** 를 클릭하십시오. |
   | **[!UICONTROL 선택적 게시]** | 자산은 공개 Experience Manager에서 전달을 위해 또는 Dynamic Media 중 선택한 항목에 게시됩니다. 두 게시 방법은 서로 사용할 수 없습니다. 즉, 자산을 DMS7에 게시하여 스마트 자르기 또는 동적 변환과 같은 기능을 사용할 수 있습니다. 또는 보안 미리 보기를 위해 자산만 Experience Manager에 게시할 수 있습니다. 같은 자산 *not* 공개 도메인에 전달을 위해 DMS7에 게시되었습니다. 선택한 경우에는 이 옵션을 사용할 수 없습니다 **[!UICONTROL Dynamic Media 동기화에서 이 폴더 하위 트리의 모든 항목 제외]** in **[!UICONTROL 동기화 모드]** 를 클릭하십시오. |

1. 페이지의 오른쪽 위 모서리에서 을(를) 선택합니다 **[!UICONTROL 저장 및 닫기]**&#x200B;를 선택하고 을 선택합니다. **[!UICONTROL 확인]** Experience Manager Assets으로 돌아갑니다.

## 게시 관리를 사용하여 Dynamic Media 또는 Experience Manager에 자산을 선택적으로 게시{#selective-publish-manage-publication}

를 사용하기 전에 **[!UICONTROL 게시 관리]** 자산을 Dynamic Media 또는 Experience Manager에 선택적으로 게시하려면 다음 중 하나를 설정해야 합니다.

* 다음 **[!UICONTROL 자산 게시]** 옵션 **[!UICONTROL Dynamic Media 구성]** to **[!UICONTROL 선택적 게시]**
* 폴더 수준에서 선택적 게시를 구성했습니다.

자세한 내용은 [Dynamic Media 구성 만들기](#configuring-dynamic-media-cloud-services) 또는 [Dynamic Media의 폴더 수준에서 선택적 게시 구성](#selective-publish-configure-folder)

>[!IMPORTANT]
>
>선택적 게시 는 Dynamic Media - Scene7 모드에서만 사용할 수 있습니다.

>[!NOTE]
>
>*복사* 폴더 간 및 폴더 간 자산은 해당 자산의 게시 상태를 지웁니다. 하지만, *이동* 폴더 속성이 **[!UICONTROL 선택적 게시]**&#x200B;로 설정되면 해당 자산의 게시 상태가 유지됩니다.

**게시 관리를 사용하여 Dynamic Media 또는 Experience Manager에 자산을 선택적으로 게시하려면 다음을 수행하십시오.**

1. Experience Manager에서 Experience Manager 로고를 선택하여 전역 탐색 콘솔에 액세스합니다. 왼쪽의 탐색 아이콘(도구 아이콘 바로 위)을 선택한 다음 을 선택합니다 **[!UICONTROL 자산]** > **[!UICONTROL 파일]**.
1. in **[!UICONTROL 카드 보기]**, **[!UICONTROL 열 보기]**, 또는 **[!UICONTROL 목록 보기]**&#x200B;다음 중 하나를 수행합니다.
   * 자산을 게시하려는 폴더로 이동합니다. 폴더를 선택한 다음 도구 모음에서 를 선택합니다 **[!UICONTROL 게시 관리]**. 사용 **[!UICONTROL 목록 보기]** 따라서 특정 폴더의 게시 상태를 보다 쉽게 확인할 수 있습니다.
   * 자산을 게시하려는 폴더로 이동합니다. 폴더를 열고 하나 이상의 자산을 선택합니다. 도구 모음에서 를 선택합니다 **[!UICONTROL 게시 관리]**. 사용 **[!UICONTROL 목록 보기]** 따라서 특정 자산의 게시 상태를 보다 쉽게 확인할 수 있습니다.

      >[!NOTE]
      >
      >If **[!UICONTROL 게시 관리]** 이 도구 모음에 표시되지 않으면 대신 줄임표 단추를 선택한 다음 를 선택합니다 **[!UICONTROL 게시 관리]** 목록 메뉴에서 를 클릭합니다.

1. 에서 **[!UICONTROL 게시 관리 - 옵션]** 페이지, 아래의 **[!UICONTROL 작업]**&#x200B;원하는 활성화 유형을 선택합니다.

   | 작업 | 설명 |
   | --- | --- |
   | **[!UICONTROL 게시]** (대상 Experience Manager) | 보안 미리 보기를 위해 자산을 Experience Manager에 게시할 수 있도록 이 옵션을 선택합니다. |
   | **[!UICONTROL Dynamic Media에 게시]** | 공개 도메인에 전달을 위해 Dynamic Media에 자산을 게시하거나 스마트 자르기 또는 동적 변환과 같은 기능을 사용할 수 있도록 이 옵션을 선택합니다.<br>이 옵션은 **[!UICONTROL Dynamic Media 게시 모드]** 가 로 설정되어 있습니다. **[!UICONTROL 선택적 게시]** 를 클릭합니다. |

1. 아래 **[!UICONTROL 예약]**, 게시 타이밍을 설정합니다.

   | 일정 | 설명 |
   | --- | --- |
   | **[!UICONTROL 지금]** | 을(를) 선택하여 자산을 즉시 게시합니다. |
   | **[!UICONTROL 나중에]** | 을(를) 선택하여 특정 날짜 및 시간에 자산을 게시합니다. |

1. 의 오른쪽 위 모서리에서 **[!UICONTROL 게시 관리]** 페이지를 선택하고 **[!UICONTROL 다음]**.
1. 에서 **[!UICONTROL 게시 관리 - 범위]** 페이지에서 다음 중 하나를 수행합니다.

   * 필요한 경우 게시에서 제거할 자산을 한 개 이상 선택합니다.
   * 의 오른쪽 위 모서리에서 **[!UICONTROL 게시 관리 - 범위]** 페이지를 선택하고 **[!UICONTROL 게시]** 또는 **[!UICONTROL Dynamic Media에 게시]**.
1. 선택 **[!UICONTROL 확인]**.

### 게시 관리를 사용하여 Dynamic Media 또는 Experience Manager에서 선택적으로 자산 게시 취소 {#selective-unpublish-manage-publication}

1. Experience Manager에서 Experience Manager 로고를 선택하여 전역 탐색 콘솔에 액세스합니다. 왼쪽의 탐색 아이콘(도구 아이콘 바로 위)을 선택한 다음 을 선택합니다 **[!UICONTROL 자산]** > **[!UICONTROL 파일]**.
1. in **[!UICONTROL 카드 보기]**, **[!UICONTROL 열 보기]**, 또는 **[!UICONTROL 목록 보기]**&#x200B;다음 중 하나를 수행합니다.
   * 자산을 게시 취소하려는 폴더로 이동합니다. 폴더를 선택한 다음 도구 모음에서 를 선택합니다 **[!UICONTROL 게시 관리]**. 사용 **[!UICONTROL 목록 보기]** 따라서 특정 폴더의 게시 상태를 보다 쉽게 확인할 수 있습니다.
   * 자산을 게시 취소하려는 폴더로 이동합니다. 폴더를 열고 하나 이상의 자산을 선택합니다. 도구 모음에서 를 선택합니다 **[!UICONTROL 게시 관리]**. 사용 **[!UICONTROL 목록 보기]** 따라서 특정 자산의 게시 상태를 보다 쉽게 확인할 수 있습니다.

      >[!NOTE]
      >
      >If **[!UICONTROL 게시 관리]** 이 도구 모음에 표시되지 않으면 대신 줄임표 단추를 선택한 다음 를 선택합니다 **[!UICONTROL 게시 관리]** 목록 메뉴에서 를 클릭합니다.

1. 에서 **[!UICONTROL 게시 관리 - 옵션]** 페이지, 아래의 **[!UICONTROL 작업]**&#x200B;원하는 비활성화 유형을 선택합니다.

   | 작업 | 설명 |
   | --- | --- |
   | **[!UICONTROL 게시 취소]** (Experience Manager에서) | Experience Manager에서 자산 게시를 취소하려면 이 옵션을 선택합니다. |
   | **[!UICONTROL Dynamic Media에서 게시 취소]** | Dynamic Media에서 자산 게시를 취소하려면 이 옵션을 선택합니다.<br>이 옵션은 **[!UICONTROL Dynamic Media 게시 모드]** 가 로 설정되어 있습니다. **[!UICONTROL 선택적 게시]** 를 클릭합니다. |

1. 아래 **[!UICONTROL 예약]**&#x200B;를 비활성화하는 데 필요한 시간을 설정합니다.

   | 일정 | 설명 |
   | --- | --- |
   | **[!UICONTROL 지금]** | 자산을 즉시 게시 취소하려면 을(를) 선택합니다. |
   | **[!UICONTROL 나중에]** | 특정 날짜 및 시간에 대한 자산 게시를 취소하려면 을(를) 선택합니다. |

1. 의 오른쪽 위 모서리에서 **[!UICONTROL 게시 관리]** 페이지를 선택하고 **[!UICONTROL 다음]**.
1. 에서 **[!UICONTROL 게시 관리 - 범위]** 페이지에서 다음 중 하나를 수행합니다.
   * 게시 취소에서 제거할 자산을 한 개 이상 선택합니다.
   * 의 오른쪽 위 모서리에서 **[!UICONTROL 게시 관리 - 범위]** 페이지를 선택하고 **[!UICONTROL 게시 취소]** 또는 **[!UICONTROL Dynamic Media에서 게시 취소]**.
1. 선택 **[!UICONTROL 확인]**.

## 빠른 게시를 사용하여 Dynamic Media 또는 Experience Manager에 자산 게시 {#quick-publish-aem-dm}

다음을 사용할 수 있습니다 **[!UICONTROL 빠른 게시]** 단순 자산 활성화 사례에 사용됩니다. **[!UICONTROL 빠른 게시]** 는 추가 사용자 상호 작용 없이 선택한 자산을 즉시 게시합니다. 이 작업 때문에 게시되지 않은 참조도 자동으로 게시됩니다.

>[!NOTE]
>
>를 사용하려면 **[!UICONTROL 빠른 게시]** 자산을 Dynamic Media 또는 Experience Manager에 게시하려면 다음을 수행하십시오 **[!UICONTROL 선택적 게시]** 이 활성화되었을 때 **[!UICONTROL Dynamic Media 구성]** 또는 선택한 폴더의 폴더 속성에서 사용할 수 있습니다.

**빠른 게시를 사용하여 Dynamic Media 또는 Experience Manager에 자산을 게시하려면 다음을 수행하십시오.**

1. Experience Manager에서 Experience Manager 로고를 선택하여 전역 탐색 콘솔에 액세스합니다. 페이지 왼쪽에서, 탐색 아이콘(도구 아이콘 바로 위)을 선택한 다음 페이지의 오른쪽에서 을 선택합니다 **[!UICONTROL 자산]** > **[!UICONTROL 파일]**.
1. in **[!UICONTROL 카드 보기]**, **[!UICONTROL 열 보기]**, 또는 **[!UICONTROL 목록 보기]**&#x200B;다음 중 하나를 수행합니다.
   * 자산을 게시하려는 폴더로 이동합니다. 폴더를 선택한 다음 도구 모음에서 를 선택합니다 **[!UICONTROL 빠른 게시]**. 사용 **[!UICONTROL 목록 보기]** 따라서 특정 폴더의 게시 상태를 보다 쉽게 확인할 수 있습니다.
   * 자산을 게시하려는 폴더로 이동합니다. 폴더를 열고 하나 이상의 자산을 선택합니다. 도구 모음에서 를 선택합니다 **[!UICONTROL 빠른 게시]**. 사용 **[!UICONTROL 목록 보기]** 따라서 특정 자산의 게시 상태를 보다 쉽게 확인할 수 있습니다.

      >[!NOTE]
      >
      >If **[!UICONTROL 빠른 게시]** 이 도구 모음에 표시되지 않으면 대신 줄임표 단추를 선택한 다음 를 선택합니다 **[!UICONTROL 빠른 게시]** 목록 메뉴에서 를 클릭합니다.

      ![폴더 수준 Dynamic Media에 빠른 게시](/help/assets/assets-dm/selective-publish-folder-quick-publish-to-dm.png)

1. 다음 옵션 중 하나를 선택합니다 **[!UICONTROL 빠른 게시]** 메뉴 목록

   | 빠른 게시 옵션 | 설명 |
   | --- | --- | 
   | Experience Manager에 게시 | 선택한 자산을 즉시 Experience Manager에 게시합니다. |
   | Brand Portal에 게시 | 선택한 자산을에 즉시 게시합니다. **[!UICONTROL Brand Portal]**.<br>이 옵션은 Experience Manager Assets 인스턴스에 **[!UICONTROL Brand Portal]** 이미 구성되어 있습니다. |
   | Dynamic Media에 게시 | 선택한 자산을 즉시 Dynamic Media에 게시합니다.<br>자산을 Dynamic Media에 동기화해야 합니다. 필요한 경우 다음을 확인하십시오 **[!UICONTROL 동기화 모드]** 폴더의 속성이 이미 **[!UICONTROL 이 폴더 하위 트리의 모든 항목을 Dynamic Media에 동기화]**. |

1. 선택 **[!UICONTROL 확인]**&#x200B;를 선택하고 을 선택합니다. **[!UICONTROL 닫기]**.

## 검색 결과를 통해 자산을 선택적으로 게시 또는 게시 취소합니다 {#selective-publish-unpublish-search-results}

검색 결과에 다른 Dynamic Media 게시 설정이 있는 자산 폴더에서 자산이 표시될 수 있습니다. 검색 결과에서 여러 자산을 선택하고 각 자산에는 서로 다른 Dynamic Media 게시 모드 설정이 있는 경우 트리거할 수 있습니다 **[!UICONTROL 게시 관리]** 도구 모음에서 게시 또는 게시 취소

참조 - [Experience Manager에서 자산 검색](/help/assets/search-assets.md).

**검색 결과를 통해 자산을 선택적으로 게시 또는 게시 취소하려면,**

1. 페이지의 왼쪽 위 모서리에서 Experience Manager 로고를 선택하여 전역 탐색 콘솔에 액세스합니다. 페이지 왼쪽에서, 탐색 아이콘(도구 아이콘 바로 위)을 선택하고 을 선택합니다 **[!UICONTROL 자산]** > **[!UICONTROL 파일]**.
1. 페이지의 오른쪽 위 모서리 근처에 있는 도구 모음에서 검색 아이콘(확대경)을 선택합니다.
1. 에서 **[!UICONTROL 검색할 유형]** 텍스트 필드에 키워드를 입력한 다음 키를 누릅니다 **[!UICONTROL Enter 키]**.
1. 페이지의 오른쪽 위 모서리 근처에 있는 **[!UICONTROL 목록 보기]** 아이콘.
1. 페이지의 왼쪽 위 모서리 근처에 있는 **[!UICONTROL 필터]** 아이콘.

   ![검색 결과의 목록 보기 및 필터](/help/assets/assets-dm/select-publish-search-result.png)

1. 왼쪽 패널에서 를 확장합니다. **[!UICONTROL 상태]**&#x200B;를 확장한 다음 **[!UICONTROL Dynamic Media]** 검색 조건자입니다.
1. 를 사용하십시오 **[!UICONTROL 게시됨]** 및 **[!UICONTROL 게시 취소됨]** 게시된 Dynamic Media 자산 상태에 따라 검색 결과를 세분화하기 위한 확인란을 선택합니다.
선택적으로, **[!UICONTROL 게시]** 검색 조건자를 사용하여 **[!UICONTROL 게시됨]** 및 **[!UICONTROL 게시 취소됨]** Experience Manager 자산.
1. 다음 중 하나를 수행하십시오.
   * 게시하거나 게시 취소하려는 자산을 한 개 이상 선택합니다.
   * 의 오른쪽 위 모서리 근처에 있습니다. **[!UICONTROL 검색 결과]** 페이지를 선택하고 **[!UICONTROL 모두 선택]**.
1. 도구 모음에서 를 선택합니다 **[!UICONTROL 게시 관리]**. 도구 모음에서 줄임표 아이콘을 선택하여 열 수 있습니다 **[!UICONTROL 게시 관리]**.
1. 설정 **[!UICONTROL 게시 관리 - 옵션]** 페이지에서 원하는 작업을 선택합니다.

   | 선택한 작업 | Dynamic Media 구성의 자산 게시 설정 | 자산은 다음과 같습니다 |
   | --- | --- | --- |
   | 게시 | 즉시 또는 활성화 시 | Experience Manager 및 Dynamic Media에 게시되었습니다. |
   | 게시 | 선택적 게시 | Experience Manager에만 게시됩니다. |
   | 게시 취소 | 즉시 또는 활성화 시 | Experience Manager 및 Dynamic Media에서 게시 취소되었습니다. |
   | 게시 취소 | 선택적 게시 | Experience Manager 전용 게시 취소됨. |
   | Dynamic Media에 게시 | 즉시 또는 활성화 시 | Experience Manager, Dynamic Media 또는 둘 다에 게시되지 않습니다. |
   | Dynamic Media에 게시 | 선택적 게시 | Dynamic Media에만 게시됩니다. |
   | Dynamic Media에서 게시 취소 | 즉시 또는 활성화 시 | Experience Manager, Dynamic Media 또는 둘 다에서 게시 취소되지 않았습니다. |
   | Dynamic Media에서 게시 취소 | 선택적 게시 | Dynamic Media에서만 게시 취소됨. |

1. 아래 **[!UICONTROL 예약]**&#x200B;를 비활성화하는 데 필요한 시간을 설정합니다.

   | 선택한 예약 | 어떻게 됩니까 |
   | --- | --- |
   | 지금 | 선택한 작업이 즉시 수행됩니다. |
   | 나중에 | 선택한 작업은 선택한 특정 날짜 및 시간에 실행됩니다. |

1. 의 오른쪽 위 모서리에서 **[!UICONTROL 게시 관리 - 옵션]** 페이지를 선택하고 **[!UICONTROL 다음]**.
1. (선택 사항)에서 **[!UICONTROL 게시 관리 - 범위]** 페이지에서 **[!UICONTROL 게시 Target]** 선택한 자산에 대한 테이블의 열.

   | Dynamic Media 구성의 자산 게시 설정 | 선택한 작업 | 게시 대상 |
   | --- | --- | --- |
   | 즉시 또는 <br>활성화 시 | 게시 | Experience Manager 및 Dynamic Media |
   | 즉시 또는 <br>활성화 시 | Dynamic Media에 게시 | 없음 |
   | 선택적 게시 | 게시 | Experience Manager |
   | 선택적 게시 | Dynamic Media에 게시 | Dynamic Media |
   | 즉시 또는 <br>활성화 시 | 게시 취소 | Experience Manager 및 Dynamic Media |
   | 즉시 또는 <br>활성화 시 | Dynamic Media에서 게시 취소 | 없음 |
   | 선택적 게시 | 게시 취소 | Experience Manager |
   | 선택적 게시 | Dynamic Media에서 게시 취소 | Dynamic Media |

1. 에서 **[!UICONTROL 게시 관리 - 범위]** 페이지에서 다음 중 하나를 수행합니다.
   * 게시 또는 게시 취소에서 제거할 자산을 한 개 이상 선택합니다.
   * 의 오른쪽 위 모서리에서 **[!UICONTROL 게시 관리 - 범위]** 페이지를 선택하고 **[!UICONTROL 게시]** 또는 **[!UICONTROL 게시 취소]** 작업을 시작합니다.
1. 선택 **[!UICONTROL 확인]**.

## 자산의 게시 상태를 확인합니다 {#check-publish-status-of-asset}

다음을 사용할 수 있습니다 **[!UICONTROL 타임라인]** with **[!UICONTROL 카드 보기]**, **[!UICONTROL 열 보기]**, 또는 **[!UICONTROL 목록 보기]** Experience Manager에서 자산의 게시 상태를 빠르게 확인합니다.

**자산의 게시 상태를 확인하려면:**

1. 페이지의 왼쪽 위 모서리에서 Experience Manager 로고를 선택하여 전역 탐색 콘솔에 액세스합니다. 페이지 왼쪽에서, 탐색 아이콘(도구 아이콘 바로 위)을 선택하고 을 선택합니다 **[!UICONTROL 자산]** > **[!UICONTROL 파일]**.
1. in **[!UICONTROL 카드 보기]**, **[!UICONTROL 열 보기]**, 또는 **[!UICONTROL 목록 보기]** (아래 스크린샷은 **[!UICONTROL 목록 보기]**), 게시했거나 게시 취소된 자산이 들어 있는 폴더를 엽니다.
1. 확인 표시가 있는 자산이 나타나도록 자산을 선택합니다. 예를 들어 아래 스크린샷을 참조하십시오.
1. 페이지의 왼쪽 위 모서리 근처에 있는 드롭다운 메뉴에서 을(를) 선택합니다 **[!UICONTROL 타임라인]**. 다음 **[!UICONTROL 상태]** 왼쪽 패널의 영역에는 선택한 자산의 게시 상태가 표시됩니다.
사용 시 **[!UICONTROL 목록 보기]**, 다음에 대한 추가 열 **[!UICONTROL Dynamic Media]** 게시 상태가 나타납니다.
   * Dynamic Media에 동기화하도록 구성된 폴더에 **[!UICONTROL Dynamic Media]** 기본적으로 열이 사용됩니다.
   * 폴더: *not* Dynamic Media에 동기화하도록 구성된 경우 Dynamic Media 열이 표시되지 않습니다.
      ![목록 보기 및 타임라인](/help/assets/assets-dm/selective-publish-status-timeline.png)

## 선택적 게시 문제 해결 {#selective-publish-troubleshoot}

Dynamic Media에 동기화되지 않지만 Dynamic Media 게시 작업이 트리거된 자산에서 다음 오류 메시지와 솔루션이 발생합니다.

![선택적 게시 오류](/help/assets/assets-dm/selective-publish-error.png)
