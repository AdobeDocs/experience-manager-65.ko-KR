---
title: 스핀 세트
description: Dynamic Media에서 스핀 세트를 사용하는 방법을 알아봅니다
uuid: 379a20a3-6a17-499a-b0f1-3a835b97aa7b
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 8e9b3815-2893-4e6b-ac41-77720b42d56b
docset: aem65
feature: 스핀 세트,자산 관리
role: Business Practitioner, Administrator
exl-id: 758ad754-15de-4e72-9b7d-ab49c51d7d4f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1829'
ht-degree: 0%

---

# 스핀 세트{#spin-sets}

스핀 세트는 개체를 돌려 검사하는 실제 동작을 시뮬레이션합니다. 스핀 세트를 사용하면 모든 각도에서 주요 시각적 세부 사항을 획득하여 항목을 볼 수 있습니다.

스핀 세트는 360도 보기 경험을 시뮬레이션합니다. Dynamic Media에서는 뷰어가 항목을 회전할 수 있는 단일 축 스핀 세트를 제공합니다. 또한 사용자는 몇 번의 간단한 마우스 클릭으로 모든 보기를 &quot;자유 형식&quot;으로 확대/축소하고 이동할 수 있습니다. 이렇게 하면 특정 시점에서 항목을 더 자세히 검사할 수 있습니다.

스핀 세트는 **[!UICONTROL SPINSET라는 이름의 배너에 의해 지정됩니다.]** 또한 스핀 세트가 게시되면 Pencilicon이 표시하 **** 는 마지막 수정 날짜와 함께 배너에 World로 표시된 게시 날짜가  **** 표시됩니다.

![chlimage_1-](assets/chlimage_1-380.png)

>[!NOTE]
>
>Assets 사용자 인터페이스에 대한 자세한 내용은 [자산 관리](/help/assets/manage-assets.md)를 참조하십시오.

## 빠른 시작:스핀 세트 {#quick-start-spin-sets}

스핀 세트를 사용하여 빠르게 시작하고 실행하려면 다음 단계를 수행합니다.

1. [여러 보기를 위해 이미지를 업로드합니다.](#uploading-assets-for-spin-sets)

   최소한 1차원 스핀 세트의 경우 항목의 8-12샷과 2차원 스핀 세트의 경우 16-24샷이 필요합니다. 정기적으로 샷을 진행해야 항목이 회전하고 뒤집히는 느낌을 줄 수 있습니다. 예를 들어 1차원 스핀 세트에 12개의 샷이 포함되어 있는 경우 각 샷에 대해 30도 (360/12) 항목을 회전합니다.

1. [스핀 세트를 만듭니다.](#creating-spin-sets)

   스핀 세트를 만들려면 **[!UICONTROL 만들기 > 스핀 세트]**&#x200B;를 선택하고 세트 이름을 지정한 다음 자산을 선택하고 이미지가 나타나는 순서를 선택합니다.

   [선택기를 사용한 작업](/help/assets/working-with-selectors.md)을 참조하십시오.

   >[!NOTE]
   >
   >[일괄처리 집합 사전 설정](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)을 통해 스핀 세트를 자동으로 만들 수도 있습니다. **중요:** 일괄 처리 집합은 자산 수집의 일부로 IPS(이미지 프로덕션 시스템)에 의해 만들어지며 Dynamic Media - Scene7 모드에서만 사용할 수 있습니다.

1. 필요에 따라 [스핀 세트 뷰어 사전 설정](/help/assets/managing-viewer-presets.md)을 설정합니다.

   관리자는 스핀 세트 뷰어 사전 설정을 만들거나 수정할 수 있습니다. 뷰어 사전 설정으로 스핀 세트를 보려면 스핀 세트를 선택하고 왼쪽 레일 드롭다운 메뉴에서 **뷰어**&#x200B;를 선택합니다.

   뷰어 사전 설정을 만들거나 편집하려면 **[!UICONTROL 도구 > 자산 > 뷰어 사전 설정]**&#x200B;을 참조하십시오.

   [뷰어 사전 설정 추가 및 편집을 참조하십시오.](/help/assets/managing-viewer-presets.md)

1. [스핀 세트 보기](#viewing-spin-sets).

   일괄처리 집합 사전 설정을 통해 만들어진 세트는 3가지 방법으로 보고 액세스할 수 있습니다. (배치 집합 사전 설정을 사용하여 생성된 집합은 사용자 인터페이스에&#x200B;*표시되지 않도록*&#x200B;하십시오.)

1. [스핀 세트를 미리 봅니다.](/help/assets/previewing-assets.md)

   스핀 세트를 선택하고 미리 볼 수 있습니다. 회전 세트를 회전합니다. 왼쪽 레일 드롭다운 메뉴에서 사용할 수 있는 **[!UICONTROL Viewers]** 메뉴에서 다른 뷰어를 선택할 수 있습니다.

1. [스핀 세트를 게시합니다.](/help/assets/publishing-dynamicmedia-assets.md)

   스핀 세트를 게시하면 URL 및 포함 문자열이 활성화됩니다. 또한 [뷰어 사전 설정을 게시](/help/assets/managing-viewer-presets.md)해야 합니다.

1. [웹 애플리케이션에 URL을 ](/help/assets/linking-urls-to-yourwebapplication.md) 연결하거나  [비디오 또는 이미지 뷰어를 포함합니다](/help/assets/embed-code.md).

   AEM Assets은 스핀 세트에 대한 URL 호출을 만들고 스핀 세트를 게시한 후 활성화합니다. 자산을 미리 볼 때 이러한 URL을 복사할 수 있습니다. 또는 웹 사이트에 포함할 수 있습니다.

   스핀 세트를 선택한 다음 왼쪽 레일 드롭다운 메뉴에서 **[!UICONTROL 뷰어를 선택합니다.]**

   [스핀 세트를 웹 페이지에 연결](/help/assets/linking-urls-to-yourwebapplication.md) 및 [비디오 또는 이미지 뷰어 포함](/help/assets/embed-code.md)을 참조하십시오.

필요한 경우 [스핀 세트를 편집](#editing-spin-sets)할 수 있습니다. 또한 [스핀 세트 속성](/help/assets/manage-assets.md#editing-properties)을 보고 수정할 수 있습니다.

## 스핀 세트에 대한 자산 업로드 {#uploading-assets-for-spin-sets}

최소한 1차원 스핀 세트의 경우 항목의 8-12샷과 2차원 스핀 세트의 경우 16-24샷이 필요합니다. 정기적으로 샷을 진행해야 항목이 회전하고 뒤집히는 느낌을 줄 수 있습니다. 예를 들어 1차원 스핀 세트에 12개의 샷이 포함되어 있는 경우 각 샷에 대해 30도 (360/12) 항목을 회전합니다.

AEM Assets](/help/assets/manage-assets.md)에서 다른 자산을 업로드하는 것처럼 스핀 세트에 대한 이미지를 업로드할 수 있습니다.[

### 스핀 세트 {#guidelines-for-shooting-spin-set-images} 이미지를 캡처하기 위한 지침

다음은 스핀 세트 이미지에 대한 몇 가지 우수 사례입니다. 일반적으로 스핀 세트에 있는 이미지가 많을수록 이미지 회전 효과가 더 좋습니다. 그러나 집합에 많은 이미지를 포함하면 이미지가 로드되는 데 걸리는 시간도 늘어납니다. AEM에서는 스핀 세트에서 사용할 이미지를 촬영하기 위해 다음 지침을 권장합니다.

* 적어도, 1차원 스핀 세트에 8-12개의 이미지와 2차원 스핀 세트에 있는 16-24개의 이미지를 사용합니다. 360도 회전을 하려면 최소 8개의 이미지가 필요합니다. 2차원 스핀 세트를 만드는 것은 노동 집약이므로 1차원 스핀 세트가 더 일반적입니다.
* 무손실 형식 사용;TIFF 및 PNG가 권장됩니다.
* 항목이 흰색이나 다른 고대비 백그라운드에 나타나도록 모든 이미지를 마스크합니다. 선택적으로 그림자를 추가합니다.
* 제품 세부 사항이 잘 조명되고 초점이 맞춰졌는지 확인하십시오.
* 패션 의류를 위한 스핀 이미지를 마네킹이나 모델로 가져가세요. 마네킹은 완전히 마스킹되거나(유리 마네킹 사용), 또는 양식화된 마네킹/드레싱이 이미지에 보여지는 경우가 많다. 각도 수를 정의하여 모델 회전 세트를 생성할 수 있습니다. 각 각도를 바닥에 있는 테이프로 표시하여 모델을 단계별로 안내하고 각 샷의 방향을 살펴봅니다.

## 스핀 세트 만들기 {#creating-spin-sets}

이 섹션에서는 AEM에서 스핀 세트를 만드는 방법을 설명합니다.

>[!NOTE]
>
>[일괄처리 집합 사전 설정](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)을 통해 스핀 세트를 자동으로 만들 수도 있습니다. **중요:** 일괄 처리 집합은 자산 수집의 일부로 IPS(이미지 프로덕션 시스템)에 의해 만들어지며 Dynamic Media - Scene7 모드에서만 사용할 수 있습니다.
>
>[Dynamic Media 구성 - Scene7 모드](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)에서 &quot;이미지 세트 및 스핀 세트를 자동으로 생성하려면 일괄처리 집합 사전 설정 만들기&quot;를 참조하십시오.


>[!NOTE]
>
>스핀 세트 물질에 이미지가 표시되는 순서입니다. 회전이 매끄러운 360도 경사가 되도록 반드시 주문하십시오.

**스핀 세트 생성하기**

1. 자산에서 스핀 세트를 만들 위치로 이동하여 **[!UICONTROL 만들기]**&#x200B;를 클릭하고 **[!UICONTROL 스핀 세트를 선택합니다.]** 자산을 포함하는 폴더 내에서 세트를 만들 수도 있습니다. 스핀 세트 편집기가 표시됩니다.

   ![6_5_spinset-createpulldownmenu](assets/6_5_spinset-createpulldownmenu.png)

1. 스핀 세트 편집기의 **[!UICONTROL 제목]** 필드에 스핀 세트의 이름을 입력합니다. 스핀 세트 위의 배너에 이름이 표시됩니다. 설명을 입력합니다(선택적).

   ![6_5_spinset-spinseteditortitle](assets/6_5_spinset-spinseteditortitle.png)

   >[!NOTE]
   >
   >스핀 세트를 만들 때 스핀 세트 축소판을 변경하거나 스핀 세트의 자산을 기반으로 축소판을 자동으로 선택하도록 AEM에서 허용할 수 있습니다. 축소판을 선택하려면 **[!UICONTROL 축소판 변경]**&#x200B;을 클릭하고 이미지를 선택합니다. 이미지를 찾으려면 다른 폴더로 이동하여 찾을 수도 있습니다. 축소판을 선택한 다음 스핀 세트에서 AEM을 생성하도록 결정하려면 **[!UICONTROL 자동 축소판으로 전환을 선택합니다.]**

1. 다음 중 하나를 수행합니다.

   * 스핀 세트 편집기 페이지의 왼쪽 위 모서리 근처에 있는 **[!UICONTROL 자산 추가]**&#x200B;를 탭합니다.

   * 스핀 세트 편집기 페이지의 중간 근처에 있는 **[!UICONTROL 탭하여 자산 선택기를 엽니다.]**
   스핀 세트에 포함할 자산을 탭하여 선택합니다. 선택한 자산에는 확인 표시 아이콘이 표시됩니다. 완료되면 페이지의 오른쪽 위 모서리 근처에 있는 **[!UICONTROL Select.]** 를 탭합니다.

   자산 선택기를 사용하여 키워드를 입력하고 **[!UICONTROL Return]**&#x200B;을 탭하여 자산을 검색할 수 있습니다. 필터를 적용하여 검색 결과를 세분화할 수도 있습니다. 경로, 컬렉션, 파일 유형 및 태그별로 필터링할 수 있습니다. 필터를 선택한 다음 도구 모음에서 **[!UICONTROL 필터]** 아이콘을 탭합니다. 보기 아이콘을 탭하고 **[!UICONTROL 열 보기]**, **[!UICONTROL 카드 보기]** 또는 **[!UICONTROL 목록 보기를 선택하여 보기를 변경합니다.]**

   [선택기를 사용한 작업](/help/assets/working-with-selectors.md)을 참조하십시오.

   ![chlimage_1-383](assets/chlimage_1-383.png)

1. 세트에 자산을 추가하면 자동으로 영숫자 순서로 추가됩니다. 자산을 추가한 후 수동으로 자산 순서를 변경하거나 정렬할 수 있습니다.

   필요한 경우 자산의 재정렬 아이콘을 자산 파일 이름의 오른쪽에 드래그하여 이미지 순서를 설정 목록의 위나 아래로 변경합니다.

   ![스핀 세트에서 프레임 11을 새 위치로 드래그하여 순서를 변경합니다.](assets/6_5_spinset-reorderassets.png)

   스핀 세트에서 프레임 11을 새 위치로 드래그하여 순서를 변경합니다.

1. (선택 사항) 다음 중 하나를 수행합니다.

   * 이미지를 삭제하려면 이미지를 선택하고 **[!UICONTROL 자산 삭제]**&#x200B;를 누릅니다.

   * 페이지의 오른쪽 위 모서리 근처에 있는 사전 설정을 적용하려면 **[!UICONTROL 사전 설정]** 을 탭한 다음, 모든 자산에 한 번에 적용할 사전 설정을 선택합니다.

1. **[!UICONTROL 저장을 클릭합니다.]** 새로 만든 스핀 세트가 생성한 폴더에 나타납니다.

## 스핀 세트 보기 {#viewing-spin-sets}

사용자 인터페이스에서 또는 [일괄처리 집합 사전 설정](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)을 사용하여 자동으로 스핀 세트를 만들 수 있습니다. 그러나 일괄처리 집합 사전 설정을 사용하여 만든 집합은 사용자 인터페이스에&#x200B;*표시되지 않도록*&#x200B;하십시오. 일괄처리 집합 사전 설정을 통해 생성된 세트에 세 가지 방법으로 액세스할 수 있습니다. (이러한 메서드는 사용자 인터페이스에서 스핀 세트를 만든 경우에도 사용할 수 있습니다.)

>[!NOTE]
>
>[스핀 세트 편집](#editing-spin-sets)에 설명된 대로 사용자 인터페이스를 통해 세트를 볼 수도 있습니다.

**스핀 세트를 보려면**

1. 개별 자산의 속성을 열 때. 속성은 선택한 자산이 어떤 세트의 구성원인지 나타냅니다(**[!UICONTROL Member of Sets]** 아래). 세트 이름을 클릭하여 전체 세트를 확인합니다.

   ![chlimage_1-156](assets/chlimage_1-384.png)

1. 모든 집합의 멤버 이미지 **[!UICONTROL 세트]** 메뉴를 선택하여 자산이 멤버인 세트를 표시합니다.

   ![chlimage_1-157](assets/chlimage_1-385.png)

1. 검색에서 **[!UICONTROL 필터]**&#x200B;를 선택한 다음 **[!UICONTROL Dynamic Media]**&#x200B;을 확장하고 **[!UICONTROL 집합.]**

   검색은 UI에서 수동으로 만들거나 일괄처리 집합 사전 설정을 통해 자동으로 생성된 일치 세트를 반환합니다. 자동 세트의 경우, `Contains` 검색 기준을 사용하는 AEM 검색과 다른 `Starts with` 검색 기준을 사용하여 검색 쿼리를 수행합니다. 필터를 **[!UICONTROL Sets]**&#x200B;로 설정하는 것이 자동화된 세트를 검색하는 유일한 방법입니다.

   ![chlimage_1-158](assets/chlimage_1-386.png)

## 스핀 세트 편집 {#editing-spin-sets}

스핀 세트에서 다음과 같은 다양한 편집 작업을 수행할 수 있습니다.

* 스핀 세트에 이미지를 추가합니다.
* 스핀 세트에서 이미지 순서를 변경합니다.
* 스핀 세트에서 자산을 삭제합니다.
* 뷰어 사전 설정을 적용합니다.
* 스핀 세트를 삭제합니다.

**스핀 세트를 편집하려면**

1. 다음 중 하나를 수행합니다.

   * 스핀 세트 자산 위로 마우스를 가져간 다음 **[!UICONTROL 편집]**(연필 아이콘)을 누릅니다.
   * 스핀 세트 자산 위로 마우스를 가져간 후 **[!UICONTROL 선택]**(확인 표시 아이콘)을 탭한 다음, 도구 모음에서 **[!UICONTROL 편집]**&#x200B;을 탭합니다.

   * 스핀 세트 자산을 탭한 다음, 도구 모음에서 **[!UICONTROL 편집]**(연필 아이콘)을 탭합니다.

1. 스핀 세트를 편집하려면 다음 중 하나를 수행합니다.

   * 이미지를 재정렬하려면 이미지를 새 위치로 드래그합니다(항목을 이동하려면 재정렬 아이콘을 선택합니다.).
   * 항목을 오름차순이나 내림차순으로 정렬하려면 열 머리글을 클릭합니다.
   * 자산을 추가하거나 기존 자산을 업데이트하려면 **[!UICONTROL 자산 추가를 클릭합니다.]** 자산으로 이동하여 선택한 다음 오른쪽 상단  **** 모서리 근처에 있는 선택 을 탭합니다.
AEM에서 축소판에 사용하는 이미지를 다른 이미지로 대체하여 삭제하면 원본 자산이 계속 표시됩니다.
   * 자산을 삭제하려면 해당 자산을 선택하고 **[!UICONTROL 자산 삭제]**&#x200B;를 클릭하거나 탭합니다.
   * 사전 설정을 적용하려면 사전 설정 아이콘을 탭하거나 클릭하고 사전 설정을 선택합니다.
   * 전체 스핀 세트를 삭제하려면 스핀 세트로 이동하여 선택한 다음 **[!UICONTROL 삭제]**&#x200B;를 선택합니다

   >[!NOTE]
   >
   >세트로 이동하여 스핀 세트에서 이미지를 편집하고 왼쪽 레일에서 **[!UICONTROL 멤버 설정]**&#x200B;을 탭한 다음, 개별 자산에서 연필 아이콘을 탭하여 편집 창을 열 수 있습니다.

1. 편집을 완료하면 **[!UICONTROL 저장]**&#x200B;을 클릭합니다.

## 스핀 세트 미리 보기 {#previewing-spin-sets}

[자산 미리 보기](/help/assets/previewing-assets.md)를 참조하십시오.

## 스핀 세트 게시 중 {#publishing-spin-sets}

[자산 게시](/help/assets/publishing-dynamicmedia-assets.md)를 참조하십시오.
