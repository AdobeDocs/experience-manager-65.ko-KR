---
title: Dynamic Media의 선택적 게시를 사용하여 작업
description: 폴더 수준에서 Adobe Experience Manager 또는 Dynamic Media에 또는 Dynamic Media에서 에셋을 게시 또는 게시 취소하도록 선택할 수 있습니다. Dynamic Media 인스턴스의 모든 폴더에 전역 설정을 적용하는 Dynamic Media 구성에 전적으로 의존하는 대신 게시 관리 또는 빠른 게시 를 사용할 수 있습니다.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User, Admin
exl-id: cd025e9d-6fb1-436c-9e78-795f2daaf345
feature: Publishing
solution: Experience Manager, Experience Manager Assets
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '3000'
ht-degree: 3%

---

# Dynamic Media의 폴더 수준에서 선택적 게시 구성 {#selective-publish-configure-folder}

폴더 수준에서 Adobe Experience Manager 또는 Dynamic Media에 또는 Dynamic Media에서 에셋을 게시 또는 게시 취소하도록 선택할 수 있습니다. Dynamic Media 인스턴스의 모든 폴더에 전역 설정을 적용하는 **[!UICONTROL Dynamic Media 구성]**&#x200B;에 전적으로 의존하는 대신 **[!UICONTROL 게시 관리]** 또는 **[!UICONTROL 빠른 게시]**&#x200B;를 사용할 수 있습니다.

예를 들어 선택적 게시를 사용하여 아직 라이브가 아닌 제품에 대한 에셋에서 작업할 수 있습니다. 이러한 경우 마케팅 팀은 Dynamic Media에 동기화되는 스마트 자르기 이미지 및 동적 변환에 액세스할 수 있습니다. 글로벌 전달을 위해 Dynamic Media에 이러한 자산을 게시하지 않고도 홍보 자료를 만들 수 있습니다.

>[!IMPORTANT]
>
>선택적 게시는 Dynamic Media - Scene7 모드에서만 사용할 수 있습니다.

>[!NOTE]
>
>폴더에 자산을 *복사*&#x200B;하면 해당 자산의 게시 상태가 지워집니다. 그러나 폴더 속성이 *선택적 게시*(으)로 설정된 폴더에서 자산을 **[!UICONTROL 이동]**&#x200B;하면 해당 자산의 게시 상태가 유지됩니다.

나중에 폴더의 **[!UICONTROL 선택적 게시]** 설정을 변경하기로 결정하는 경우 이러한 변경 사항은 해당 시점부터 해당 폴더에 업로드하는 새 자산에만 영향을 줍니다. 폴더에 있는 기존 자산의 게시 상태는 **[!UICONTROL 빠른 게시]** 또는 **[!UICONTROL 게시 관리]** 대화 상자에서 수동으로 변경할 때까지 그대로 유지됩니다.

폴더 수준 **[!UICONTROL Dynamic Media 게시 모드]** 옵션은 항상 **[!UICONTROL Dynamic Media 구성]**&#x200B;의 **[!UICONTROL Assets 게시]** 설정에 있는 값으로 기본 설정됩니다. 그러나 이 항목의 다음 단계에서는 다음 단계에 설명된 대로 폴더 수준에서 이 기본값을 수동으로 변경하여 **[!UICONTROL Dynamic Media 구성]** 값을 재정의하는 방법을 보여 줍니다.

다음 중 하나를 사용하는지 여부에 관계없이

* **[!UICONTROL Assets 게시]** 값이 **[!UICONTROL Dynamic Media 구성]**&#x200B;에 설정되었습니다.
* **[!UICONTROL Dynamic Media 게시 모드]** 값이 폴더 수준 속성에 설정되었습니다.

**[!UICONTROL 즉시]**, **[!UICONTROL 활성화 시]** 또는 **[!UICONTROL 선택적 게시]**&#x200B;를 선택할 수 있습니다. 예를 들어, **[!UICONTROL Dynamic Media 구성]**&#x200B;에서 **[!UICONTROL Assets 게시]** 값을 **[!UICONTROL 활성화 시]**&#x200B;로 설정할 수 있지만, 폴더 수준에서 **[!UICONTROL Dynamic Media 게시]** 모드 값을 **[!UICONTROL 선택적 게시]**&#x200B;로 설정할 수 있습니다.

폴더에서 선택적 게시를 구성한 후 다음 중 하나를 수행할 수 있습니다.

* [게시 관리를 사용하여 Dynamic Media 또는 Experience Manager에 자산을 선택적으로 게시합니다](#selective-publish-manage-publication).
* [게시 관리를 사용하여 Dynamic Media 또는 Experience Manager에서 자산을 선택적으로 게시 취소합니다](#selective-unpublish-manage-publication).
* [빠른 게시를 사용하여 Dynamic Media 또는 Experience Manager에 자산 게시](#quick-publish-aem-dm).
* [검색 결과를 통해 자산을 선택적으로 게시하거나 게시를 취소합니다](#selective-publish-unpublish-search-results).

**Dynamic Media의 폴더 수준에서 선택적 게시를 구성하려면:**

1. Experience Manager에서 Experience Manager 로고를 선택하여 전역 탐색 콘솔에 액세스합니다. 왼쪽에서 탐색 아이콘(도구 아이콘 바로 위)을 선택한 다음 **[!UICONTROL Assets]** > **[!UICONTROL 파일]**&#x200B;을 선택합니다.
1. 다음 중 하나를 수행하십시오.
   * 기존 폴더의 속성을 편집합니다. **[!UICONTROL 카드 보기]**, **[!UICONTROL 열 보기]** 또는 **[!UICONTROL 목록 보기]**&#x200B;에서 속성을 편집할 폴더로 이동합니다. 폴더를 선택한 다음 도구 모음에서 **[!UICONTROL 속성]**&#x200B;을 선택합니다.
   * 새 폴더의 속성을 편집합니다. **[!UICONTROL 카드 보기]**, **[!UICONTROL 열 보기]** 또는 **[!UICONTROL 목록 보기]**&#x200B;에서 페이지의 오른쪽 상단 근처에 있는 **[!UICONTROL 만들기]** > **[!UICONTROL 폴더]**&#x200B;를 선택합니다. **[!UICONTROL 폴더 만들기]** 대화 상자에서 폴더의 제목(필수)을 입력한 다음 **[!UICONTROL 만들기]**&#x200B;를 선택합니다. 폴더를 선택한 다음 도구 모음에서 **[!UICONTROL 속성]**&#x200B;을 선택합니다.

1. **[!UICONTROL 동기화 모드]** 드롭다운 목록에서 다음 중 하나를 선택합니다.

   | 동기화 모드 | 설명 |
   | --- | --- |
   | **[!UICONTROL 상속됨]** | 폴더에 명시적 동기화 값이 없습니다. 대신 폴더는 상위 폴더 중 하나 또는 **[!UICONTROL Dynamic Media 구성]**&#x200B;에 설정된 기본 모드에서 동기화 값을 상속합니다. **[!UICONTROL 상속됨]**&#x200B;에 대한 자세한 상태는 도구 설명을 통해 표시됩니다. |
   | **[!UICONTROL 이 폴더 하위 트리의 모든 항목을 Dynamic Media에 동기화]** | Dynamic Media에 게시하려면 자산을 Dynamic Media에 동기화해야 합니다. 이 옵션을 선택하면 Dynamic Media에 동기화할 이 하위 트리의 모든 자산이 포함됩니다. 폴더별 설정은 **[!UICONTROL Dynamic Media 구성]**&#x200B;의 기본 설정을 재정의합니다. |
   | **[!UICONTROL Dynamic Media 동기화에서 이 폴더 하위 트리의 모든 항목 제외]** | Dynamic Media에 동기화할 때 이 하위 트리의 모든 자산을 제외합니다. |

   ![폴더 수준 선택적 게시](/help/assets/assets-dm/createfolder-properties-selectivepublish.png)

1. **[!UICONTROL Dynamic Media 게시 모드]** 드롭다운 목록에서 옵션을 선택합니다. **[!UICONTROL Dynamic Media 게시 모드]** 옵션은 항상 **[!UICONTROL Dynamic Media 구성]**&#x200B;에 설정된 값으로 기본 설정됩니다. 그러나 다음 옵션 중 하나를 사용하여 이 기본 **[!UICONTROL Dynamic Media 구성]** 값을 수동으로 재정의할 수 있습니다.

   >[!IMPORTANT]
   >
   >선택한 Dynamic Media 게시 모드 옵션, 나중에 *이미* 게시된 에셋에 대해 수행하는 모든 업데이트는 추가 사용자 작업 없이 즉시 게시됩니다.
   >
   >게시된 비디오가 업데이트된 경우 게재 시 변경 사항을 반영하도록 다시 게시해야 합니다.

   | Dynamic Media 게시 모드 옵션 | 설명 |
   | --- | --- |
   | **[!UICONTROL 즉시]** | 에셋이 이 폴더에 업로드되면 시스템은 에셋을 Experience Manager에 수집하고 URL/임베드를 즉시 제공합니다. 이 옵션은 Experience Manager 게시에만 연결되며 에셋을 게시하는 데 필요한 사용자 개입이 없습니다.<br>이전 단계에서 *동기화 모드*&#x200B;에서 **[!UICONTROL 이 폴더 하위 트리의 모든 항목을 Dynamic Media 동기화에서 제외]**&#x200B;를 선택한 경우 이 옵션을 **[!UICONTROL 사용할 수 없음]**&#x200B;입니다. |
   | **[!UICONTROL 활성화 시]** | 에셋이 이 폴더에 업로드되는 경우 URL/포함 링크를 제공하기 전에 먼저 에셋을 명시적으로 게시해야 합니다. 이 옵션은 Experience Manager 게시에만 연결됩니다.<br>이전 단계에서 *동기화 모드*&#x200B;에서 **[!UICONTROL 이 폴더 하위 트리의 모든 항목을 Dynamic Media 동기화에서 제외]**&#x200B;를 선택한 경우 이 옵션을 **[!UICONTROL 사용할 수 없음]**&#x200B;입니다. |
   | **[!UICONTROL 선택적 게시]** | Assets은 공개 도메인에서 제공하기 위해 Experience Manager 또는 Dynamic Media 중 선택한 항목에 게시됩니다. 두 게시 방법은 상호 배타적입니다. 즉, 스마트 자르기 또는 동적 변환과 같은 기능을 사용할 수 있도록 자산을 DMS7에 게시할 수 있습니다. 또는 보안 미리 보기를 위해 Experience Manager에만 자산을 게시할 수 있습니다. 이러한 동일한 자산은 공개 도메인에서 제공하기 위해 DMS7에 게시된 *아님*&#x200B;입니다. 이전 단계에서 **[!UICONTROL 동기화 모드]**&#x200B;에서 **[!UICONTROL 이 폴더 하위 트리의 모든 항목을 Dynamic Media 동기화에서 제외]**&#x200B;를 선택한 경우에는 이 옵션을 사용할 수 없습니다. |

1. 페이지의 오른쪽 상단 모서리에서 **[!UICONTROL 저장 및 닫기]**&#x200B;를 선택한 다음 **[!UICONTROL 확인]**&#x200B;을 선택하여 Experience Manager Assets으로 돌아갑니다.

## 게시 관리를 사용하여 자산을 Dynamic Media 또는 Experience Manager에 선택적으로 게시{#selective-publish-manage-publication}

**[!UICONTROL 게시 관리]**&#x200B;를 사용하여 자산을 Dynamic Media 또는 Experience Manager에 선택적으로 게시하려면 먼저 다음 중 하나를 설정해야 합니다.

* **[!UICONTROL 선택적 게시]**&#x200B;에 대한 **[!UICONTROL Dynamic Media 구성]**&#x200B;의 **[!UICONTROL Assets 게시]** 옵션
* 폴더 수준에서 선택적 게시를 구성했습니다.

[Dynamic Media 구성 만들기](#configuring-dynamic-media-cloud-services) 또는 [Dynamic Media의 폴더 수준에서 선택적 게시 구성](#selective-publish-configure-folder)을 참조하십시오.

>[!IMPORTANT]
>
>선택적 게시는 Dynamic Media - Scene7 모드에서만 사용할 수 있습니다.

>[!NOTE]
>
>폴더에 자산을 *복사*&#x200B;하면 해당 자산의 게시 상태가 지워집니다. 그러나 폴더 속성이 *선택적 게시*(으)로 설정된 폴더에서 자산을 **[!UICONTROL 이동]**&#x200B;하면 해당 자산의 게시 상태가 유지됩니다.

**게시 관리를 사용하여 Dynamic Media 또는 Experience Manager에 자산을 선택적으로 게시하려면:**

1. Experience Manager에서 Experience Manager 로고를 선택하여 전역 탐색 콘솔에 액세스합니다. 왼쪽에서 탐색 아이콘(도구 아이콘 바로 위)을 선택한 다음 **[!UICONTROL Assets]** > **[!UICONTROL 파일]**&#x200B;을 선택합니다.
1. **[!UICONTROL 카드 보기]**, **[!UICONTROL 열 보기]** 또는 **[!UICONTROL 목록 보기]**&#x200B;에서 다음 중 하나를 실행하십시오.
   * 게시할 자산이 있는 폴더로 이동합니다. 폴더를 선택한 다음 도구 모음에서 **[!UICONTROL 게시 관리]**&#x200B;를 선택합니다. 특정 폴더의 게시 상태를 더 쉽게 확인할 수 있도록 **[!UICONTROL 목록 보기]**&#x200B;를 사용하세요.
   * 게시할 자산이 있는 폴더로 이동합니다. 폴더를 연 다음 하나 이상의 에셋을 선택합니다. 도구 모음에서 **[!UICONTROL 게시 관리]**&#x200B;를 선택합니다. 특정 자산의 게시 상태를 보다 쉽게 확인할 수 있도록 **[!UICONTROL 목록 보기]**&#x200B;를 사용하십시오.

     >[!NOTE]
     >
     >도구 모음에 **[!UICONTROL 게시 관리]**&#x200B;가 표시되지 않으면 대신 줄임표 버튼을 선택한 다음 목록 메뉴에서 **[!UICONTROL 게시 관리]**&#x200B;를 선택하십시오.

1. **[!UICONTROL 게시 관리 - 옵션]** 페이지의 **[!UICONTROL 작업]**&#x200B;에서 원하는 활성화 유형을 선택합니다.

   | 작업 | 설명 |
   | --- | --- |
   | **[!UICONTROL 게시]**(Experience Manager) | 보안 미리 보기를 위해 Experience Manager에 자산을 게시할 수 있도록 하려면 이 옵션을 선택합니다. |
   | **[!UICONTROL Dynamic Media에 게시]** | 공개 도메인에서 전달할 자산을 Dynamic Media에 게시하거나 스마트 자르기 또는 동적 변환과 같은 기능을 사용할 수 있도록 하려면 이 옵션을 선택합니다.<br>이 옵션은 폴더 속성에서 **[!UICONTROL Dynamic Media 게시 모드]**&#x200B;가 **[!UICONTROL 선택적 게시]**(으)로 설정된 경우에만 사용할 수 있습니다. |

1. **[!UICONTROL 일정]**&#x200B;에서 게시 시기를 설정하십시오.

   | 일정 | 설명 |
   | --- | --- |
   | **[!UICONTROL 지금]** | 자산을 즉시 게시하려면 을(를) 선택합니다. |
   | **[!UICONTROL 나중에]** | 특정 날짜 및 시간에 자산을 게시하려면 을(를) 선택합니다. |

1. **[!UICONTROL 게시 관리]** 페이지의 오른쪽 상단 모서리에서 **[!UICONTROL 다음]**&#x200B;을 선택합니다.
1. **[!UICONTROL 게시 관리 - 범위]** 페이지에서 다음 중 하나를 실행하십시오.

   * 필요한 경우 게시에서 제거할 자산을 하나 이상 선택합니다.
   * **[!UICONTROL 게시 관리 - 범위]** 페이지의 오른쪽 상단 모서리에서 **[!UICONTROL 게시]** 또는 **[!UICONTROL Dynamic Media에 게시]**&#x200B;를 선택합니다.
1. **[!UICONTROL 확인]**&#x200B;을 선택합니다.

### 게시 관리를 사용하여 Dynamic Media 또는 Experience Manager에서 에셋을 선택적으로 게시 취소합니다 {#selective-unpublish-manage-publication}

1. Experience Manager에서 Experience Manager 로고를 선택하여 전역 탐색 콘솔에 액세스합니다. 왼쪽에서 탐색 아이콘(도구 아이콘 바로 위)을 선택한 다음 **[!UICONTROL Assets]** > **[!UICONTROL 파일]**&#x200B;을 선택합니다.
1. **[!UICONTROL 카드 보기]**, **[!UICONTROL 열 보기]** 또는 **[!UICONTROL 목록 보기]**&#x200B;에서 다음 중 하나를 실행하십시오.
   * 게시를 취소할 에셋이 있는 폴더로 이동합니다. 폴더를 선택한 다음 도구 모음에서 **[!UICONTROL 게시 관리]**&#x200B;를 선택합니다. 특정 폴더의 게시 상태를 더 쉽게 확인할 수 있도록 **[!UICONTROL 목록 보기]**&#x200B;를 사용하세요.
   * 게시를 취소할 에셋이 있는 폴더로 이동합니다. 폴더를 연 다음 하나 이상의 에셋을 선택합니다. 도구 모음에서 **[!UICONTROL 게시 관리]**&#x200B;를 선택합니다. 특정 자산의 게시 상태를 보다 쉽게 확인할 수 있도록 **[!UICONTROL 목록 보기]**&#x200B;를 사용하십시오.

     >[!NOTE]
     >
     >도구 모음에 **[!UICONTROL 게시 관리]**&#x200B;가 표시되지 않으면 대신 줄임표 버튼을 선택한 다음 목록 메뉴에서 **[!UICONTROL 게시 관리]**&#x200B;를 선택하십시오.

1. **[!UICONTROL 게시 관리 - 옵션]** 페이지의 **[!UICONTROL 작업]**&#x200B;에서 원하는 비활성화 유형을 선택합니다.

   | 작업 | 설명 |
   | --- | --- |
   | **[!UICONTROL 게시 취소]**(Experience Manager) | Experience Manager에서 에셋 게시를 취소하려면 이 옵션을 선택합니다. |
   | **[!UICONTROL Dynamic Media에서 게시 취소]** | Dynamic Media에서 에셋 게시를 취소하려면 이 옵션을 선택합니다.<br>이 옵션은 폴더 속성에서 **[!UICONTROL Dynamic Media 게시 모드]**&#x200B;가 **[!UICONTROL 선택적 게시]**(으)로 설정된 경우에만 사용할 수 있습니다. |

1. **[!UICONTROL 일정]**&#x200B;에서 비활성화 시기를 설정합니다.

   | 일정 | 설명 |
   | --- | --- |
   | **[!UICONTROL 지금]** | 자산을 즉시 게시 취소하려면 을(를) 선택합니다. |
   | **[!UICONTROL 나중에]** | 특정 날짜 및 시간에 자산 게시를 취소하려면 을 선택합니다. |

1. **[!UICONTROL 게시 관리]** 페이지의 오른쪽 상단 모서리에서 **[!UICONTROL 다음]**&#x200B;을 선택합니다.
1. **[!UICONTROL 게시 관리 - 범위]** 페이지에서 다음 중 하나를 실행하십시오.
   * 게시 취소에서 제거할 자산을 하나 이상 선택합니다.
   * **[!UICONTROL 게시 관리 - 범위]** 페이지의 오른쪽 상단 모서리에서 **[!UICONTROL 게시 취소]** 또는 **[!UICONTROL Dynamic Media에서 게시 취소]**&#x200B;를 선택합니다.
1. **[!UICONTROL 확인]**&#x200B;을 선택합니다.

## 빠른 게시를 사용하여 Dynamic Media 또는 Experience Manager에 자산 게시 {#quick-publish-aem-dm}

간단한 에셋 활성화 사례에 **[!UICONTROL 빠른 게시]**&#x200B;를 사용할 수 있습니다. **[!UICONTROL 빠른 게시]**&#x200B;는 추가적인 사용자 상호 작용 없이 선택한 자산을 즉시 게시합니다. 이 작업으로 인해 게시되지 않은 참조도 자동으로 게시됩니다.

>[!NOTE]
>
>**[!UICONTROL 빠른 게시]**&#x200B;를 사용하여 Dynamic Media 또는 Experience Manager에 자산을 게시하려면 **[!UICONTROL Dynamic Media 구성]** 또는 선택한 폴더의 폴더 속성에서 **[!UICONTROL 선택적 게시]**&#x200B;를 사용하도록 설정해야 합니다.

**빠른 게시를 사용하여 Dynamic Media 또는 Experience Manager에 자산을 게시하려면:**

1. Experience Manager에서 Experience Manager 로고를 선택하여 전역 탐색 콘솔에 액세스합니다. 페이지의 왼쪽에서 탐색 아이콘(도구 아이콘 바로 위)을 선택한 다음 페이지의 오른쪽에서 **[!UICONTROL Assets]** > **[!UICONTROL 파일]**&#x200B;을 선택합니다.
1. **[!UICONTROL 카드 보기]**, **[!UICONTROL 열 보기]** 또는 **[!UICONTROL 목록 보기]**&#x200B;에서 다음 중 하나를 실행하십시오.
   * 게시할 자산이 있는 폴더로 이동합니다. 폴더를 선택한 다음 도구 모음에서 **[!UICONTROL 빠른 게시]**&#x200B;를 선택합니다. 특정 폴더의 게시 상태를 더 쉽게 확인할 수 있도록 **[!UICONTROL 목록 보기]**&#x200B;를 사용하세요.
   * 게시할 자산이 있는 폴더로 이동합니다. 폴더를 연 다음 하나 이상의 에셋을 선택합니다. 도구 모음에서 **[!UICONTROL 빠른 게시]**&#x200B;를 선택합니다. 특정 자산의 게시 상태를 보다 쉽게 확인할 수 있도록 **[!UICONTROL 목록 보기]**&#x200B;를 사용하십시오.

     >[!NOTE]
     >
     >도구 모음에 **[!UICONTROL 빠른 게시]**&#x200B;가 표시되지 않으면 대신 줄임표 버튼을 선택한 다음 목록 메뉴에서 **[!UICONTROL 빠른 게시]**&#x200B;을(를) 선택하십시오.

     ![Dynamic Media에 폴더 수준 빠른 게시](/help/assets/assets-dm/selective-publish-folder-quick-publish-to-dm.png)

1. **[!UICONTROL 빠른 게시]** 메뉴 목록에서 다음 옵션 중 하나를 선택하십시오.

   | 빠른 게시 옵션 | 설명 |
   | --- | --- |
   | Experience Manager에 게시 | 선택한 자산을 Experience Manager에 즉시 게시합니다. |
   | Brand Portal에 게시 | 선택한 자산을 **[!UICONTROL Brand Portal]**&#x200B;에 즉시 게시합니다.<br>이 옵션은 Experience Manager Assets 인스턴스에 이미 **[!UICONTROL Brand Portal]**&#x200B;이(가) 구성되어 있는 경우에만 사용할 수 있습니다. |
   | Dynamic Media에 게시 | 선택한 자산을 Dynamic Media에 즉시 게시합니다.<br>자산을 Dynamic Media에 동기화해야 합니다. 필요한 경우 폴더의 속성에서 **[!UICONTROL 동기화 모드]**&#x200B;가 **[!UICONTROL 이 폴더 하위 트리의 모든 항목을 Dynamic Media에 동기화]**&#x200B;하도록 이미 설정되어 있는지 확인하십시오. |

1. **[!UICONTROL 확인]**&#x200B;을 선택한 다음 **[!UICONTROL 닫기]**&#x200B;를 선택합니다.

## 검색 결과를 통해 에셋을 선택적으로 게시 또는 게시 취소 {#selective-publish-unpublish-search-results}

검색 결과는 서로 다른 Dynamic Media 게시 설정을 갖는 전체 에셋 폴더의 에셋을 표시할 수 있습니다. 검색 결과에서 여러 자산을 선택하고 각 자산에 서로 다른 Dynamic Media 게시 모드 설정이 있는 경우 도구 모음에서 **[!UICONTROL 게시 관리]**&#x200B;를 트리거하여 게시하거나 게시 취소할 수 있습니다.

[Experience Manager에서 자산 검색](/help/assets/search-assets.md)도 참조하세요.

**검색 결과를 통해 자산을 선택적으로 게시하거나 게시를 취소하려면 다음을 수행하십시오.**

1. Experience Manager의 페이지 왼쪽 상단 모서리에서 Experience Manager 로고를 선택하여 전역 탐색 콘솔에 액세스합니다. 페이지 왼쪽에서 탐색 아이콘(도구 아이콘 바로 위)을 선택한 다음 **[!UICONTROL Assets]** > **[!UICONTROL 파일]**&#x200B;을 선택합니다.
1. 페이지의 오른쪽 위 모서리 근처에 있는 도구 모음에서 검색 아이콘(돋보기)을 선택합니다.
1. **[!UICONTROL 검색하려면 입력]** 텍스트 필드에 키워드를 입력한 다음 **[!UICONTROL Enter]**&#x200B;를 누릅니다.
1. 페이지의 오른쪽 상단 모서리에서 **[!UICONTROL 목록 보기]** 아이콘을 선택합니다.
1. 페이지의 왼쪽 상단 모서리 근처에서 **[!UICONTROL 필터]** 아이콘을 선택합니다.

   ![검색 결과의 목록 보기 및 필터](/help/assets/assets-dm/select-publish-search-result.png)

1. 왼쪽 패널에서 **[!UICONTROL 상태]**&#x200B;를 확장한 다음 **[!UICONTROL Dynamic Media]** 검색 조건자를 확장합니다.
1. **[!UICONTROL 게시됨]** 및 **[!UICONTROL 게시 취소됨]** 확인란을 사용하여 Dynamic Media 자산의 게시된 상태를 기반으로 검색 결과를 세분화합니다.
선택적으로 **[!UICONTROL 게시]** 검색 조건자와 함께 이 확인란을 사용하여 **[!UICONTROL 게시됨]** 및 **[!UICONTROL 게시 취소됨]** Experience Manager 자산의 검색 결과를 구체화할 수 있습니다.
1. 다음 중 하나를 수행하십시오.
   * 게시 또는 게시 취소할 에셋을 하나 이상 선택합니다.
   * **[!UICONTROL 검색 결과]** 페이지의 오른쪽 상단 모서리에서 **[!UICONTROL 모두 선택]**&#x200B;을 선택합니다.
1. 도구 모음에서 **[!UICONTROL 게시 관리]**&#x200B;를 선택합니다. **[!UICONTROL 게시 관리]**&#x200B;를 열 수 있도록 도구 모음에서 줄임표 아이콘을 선택합니다.
1. **[!UICONTROL 게시 관리 - 옵션]** 페이지에서 원하는 작업을 선택합니다.

   | 선택한 작업 | Dynamic Media 구성의 Assets 게시 설정 | Assets은 |
   | --- | --- | --- |
   | 게시 | 즉시 또는 활성화 시 | Experience Manager 및 Dynamic Media에 게시되었습니다. |
   | 게시 | 선택적 게시 | Experience Manager에만 게시됩니다. |
   | 게시 취소 | 즉시 또는 활성화 시 | Experience Manager 및 Dynamic Media에서 게시가 취소되었습니다. |
   | 게시 취소 | 선택적 게시 | Experience Manager에서만 게시 취소됨. |
   | Dynamic Media에 게시 | 즉시 또는 활성화 시 | Experience Manager, Dynamic Media 또는 둘 다에 게시되지 않았습니다. |
   | Dynamic Media에 게시 | 선택적 게시 | Dynamic Media에만 게시됩니다. |
   | Dynamic Media에서 게시 취소 | 즉시 또는 활성화 시 | Experience Manager, Dynamic Media 또는 둘 다에서 게시가 취소되지 않았습니다. |
   | Dynamic Media에서 게시 취소 | 선택적 게시 | Dynamic Media에서만 게시가 취소되었습니다. |

1. **[!UICONTROL 일정]**&#x200B;에서 비활성화 시기를 설정합니다.

   | 선택한 일정 | 다음 단계 |
   | --- | --- |
   | 현재 | 선택한 작업이 즉시 수행됩니다. |
   | 나중에 | 선택한 작업은 선택한 특정 날짜 및 시간에 실행됩니다. |

1. **[!UICONTROL 게시 관리 - 옵션]** 페이지의 오른쪽 상단 모서리에서 **[!UICONTROL 다음]**&#x200B;을 선택합니다.
1. (선택 사항) **[!UICONTROL 게시 관리 - 범위]** 페이지에서 선택한 자산에 대한 테이블의 **[!UICONTROL 게시 대상]** 열을 검토하십시오.

   | Dynamic Media 구성의 Assets 게시 설정 | 선택한 작업 | 게시 대상 |
   | --- | --- | --- |
   | 즉시 또는 활성화 시 <br> | 게시 | Experience Manager 및 Dynamic Media |
   | 즉시 또는 활성화 시 <br> | Dynamic Media에 게시 | 없음 |
   | 선택적 게시 | 게시 | Experience Manager |
   | 선택적 게시 | Dynamic Media에 게시 | Dynamic Media |
   | 즉시 또는 활성화 시 <br> | 게시 취소 | Experience Manager 및 Dynamic Media |
   | 즉시 또는 활성화 시 <br> | Dynamic Media에서 게시 취소 | 없음 |
   | 선택적 게시 | 게시 취소 | Experience Manager |
   | 선택적 게시 | Dynamic Media에서 게시 취소 | Dynamic Media |

1. **[!UICONTROL 게시 관리 - 범위]** 페이지에서 다음 중 하나를 실행하십시오.
   * 게시 또는 게시 취소에서 제거할 자산을 하나 이상 선택합니다.
   * **[!UICONTROL 게시 관리 - 범위]** 페이지의 오른쪽 상단 모서리에서 **[!UICONTROL 게시]** 또는 **[!UICONTROL 게시 취소]**&#x200B;를 선택하여 작업을 시작합니다.
1. **[!UICONTROL 확인]**&#x200B;을 선택합니다.

## 에셋의 게시 상태 확인 {#check-publish-status-of-asset}

Experience Manager에서 **[!UICONTROL 타임라인]**&#x200B;을(를) **[!UICONTROL 카드 보기]**, **[!UICONTROL 열 보기]** 또는 **[!UICONTROL 목록 보기]**&#x200B;와 함께 사용하여 자산의 게시 상태를 빠르게 확인할 수 있습니다.

**자산의 게시 상태를 확인하려면:**

1. Experience Manager의 페이지 왼쪽 상단 모서리에서 Experience Manager 로고를 선택하여 전역 탐색 콘솔에 액세스합니다. 페이지 왼쪽에서 탐색 아이콘(도구 아이콘 바로 위)을 선택한 다음 **[!UICONTROL Assets]** > **[!UICONTROL 파일]**&#x200B;을 선택합니다.
1. **[!UICONTROL 카드 보기]**, **[!UICONTROL 열 보기]** 또는 **[!UICONTROL 목록 보기]**(아래 스크린샷에는 **[!UICONTROL 목록 보기]**&#x200B;가 표시됨)에서 게시하거나 게시를 취소한 자산이 포함된 폴더를 엽니다.
1. 선택 표시가 있는 자산을 선택합니다. 예를 들어 아래 스크린샷 을 참조하십시오.
1. 페이지의 왼쪽 위 모서리 근처에서 드롭다운 메뉴에서 **[!UICONTROL 타임라인]**&#x200B;을 선택합니다. 왼쪽 패널의 **[!UICONTROL 상태]** 영역에는 선택한 에셋의 게시 상태가 표시됩니다.
**[!UICONTROL 목록 보기]**&#x200B;를 사용하는 경우 **[!UICONTROL Dynamic Media]** 게시 상태에 대한 추가 열이 나타납니다.
   * Dynamic Media에 동기화하도록 구성된 폴더는 기본적으로 **[!UICONTROL Dynamic Media]** 열을 표시합니다.
   * Dynamic Media에 동기화하도록 구성된 *not* 폴더에는 Dynamic Media 열이 표시되지 않습니다.
     ![목록 보기 및 타임라인](/help/assets/assets-dm/selective-publish-status-timeline.png)

## 선택적 게시 문제 해결 {#selective-publish-troubleshoot}

Dynamic Media에 동기화되지 않았지만 Dynamic Media 게시 작업이 트리거된 자산은 다음과 같은 오류 메시지 및 솔루션을 초래합니다.

![선택적 게시 오류](/help/assets/assets-dm/selective-publish-error.png)
