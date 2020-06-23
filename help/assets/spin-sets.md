---
title: 스핀 세트
description: Dynamic Media에서 스핀 세트를 사용하여 작업하는 방법 살펴보기
uuid: 379a20a3-6a17-499a-b0f1-3a835b97aa7b
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 8e9b3815-2893-4e6b-ac41-77720b42d56b
docset: aem65
translation-type: tm+mt
source-git-commit: e916f70549197ac9f95443e972401a78735b0560
workflow-type: tm+mt
source-wordcount: '1830'
ht-degree: 0%

---


# 스핀 세트{#spin-sets}

회전 세트는 개체를 돌려 검사하는 실제 동작을 시뮬레이션합니다. 회전 집합을 사용하면 모든 각도에서 항목을 볼 수 있으므로 모든 각도에서 주요 시각적 세부 사항을 얻을 수 있습니다.

스핀 세트는 360도 보기 환경을 시뮬레이션합니다. Dynamic Media은 사용자가 항목을 회전할 수 있는 단일 축 회전 집합을 제공합니다. 또한 사용자는 몇 번의 마우스 클릭만으로 모든 보기를 &quot;자유로운 형식&quot;으로 확대/축소하고 이동할 수 있습니다. 이러한 방식으로 사용자는 특정 관점에서 항목을 더 자세히 검사할 수 있습니다.

스핀 세트는 SPINSET이라는 이름의 배너에 **[!UICONTROL 의해 지정됩니다.]** 또한 스핀 세트가 게시되면 **[!UICONTROL 월드]** 아이콘으로 표시된 게시 날짜가 마지막 수정 날짜와 함께 배너에 **[!UICONTROL 연필]** 아이콘으로 표시됩니다.

![chlimage_1-](assets/chlimage_1-380.png)

>[!NOTE]
>
>자산 사용자 인터페이스에 대한 자세한 내용은 터치 UI를 사용하여 [자산 관리를 참조하십시오](/help/assets/managing-assets-touch-ui.md).

## 빠른 시작: 스핀 세트 {#quick-start-spin-sets}

스핀 세트를 사용하여 빠르게 작업하고 실행하려면 다음 단계를 따르십시오.

1. [여러 뷰에 맞게 이미지를 업로드합니다.](#uploading-assets-for-spin-sets)

   1차원 스핀 세트의 경우 최소 8-12개의 샷과 2차원 스핀 세트의 경우 16-24개의 샷이 필요합니다. 항목이 회전하고 뒤집어지고 있다는 인상을 주기 위해 샷을 정기적으로 촬영해야 합니다. 예를 들어 1차원 회전 집합에 12개의 샷이 있는 경우 각 샷에 대해 30도(360/12)를 회전합니다.

1. [스핀 세트를 만듭니다.](#creating-spin-sets)

   스핀 세트를 만들려면 **[!UICONTROL 만들기 > 스핀]** 세트를 선택한 다음 세트 이름을 지정하고 자산을 선택한 다음 이미지가 나타나는 순서를 선택합니다.

   See [Working with Selectors](/help/assets/working-with-selectors.md).

   >[!NOTE]
   >
   >또한 [일괄 세트 사전 설정을 통해 자동으로 스핀 세트를 만들 수도 있습니다](/help/assets/config-dms7.md#creating%20batch%20set%20presets%20to%20auto-generate%20image%20sets%20and%20spin%20sets). **중요:** 배치 세트는 IPS(Image Production System)에 의해 자산 수정의 일부로 생성되며 Dynamic Media - Scene7 모드에서만 사용할 수 있습니다.

1. 필요에 따라 [스핀 세트 뷰어 사전 설정을](/help/assets/managing-viewer-presets.md)설정합니다.

   관리자는 스핀 세트 뷰어 사전 설정을 만들거나 수정할 수 있습니다. 뷰어 사전 설정으로 스핀 세트를 보려면 스핀 세트를 선택하고 왼쪽 레일 드롭다운 메뉴에서 **뷰어를 선택합니다**.

   뷰어 **[!UICONTROL 사전 설정을 만들거나 편집하려면 도구 > 자산 > 뷰어 사전]** 설정을 참조하십시오.

   뷰어 사전 [설정 추가 및 편집을 참조하십시오.](/help/assets/managing-viewer-presets.md)

1. [스핀 세트 보기를 참조하십시오](#viewing-spin-sets).

   세 가지 방법으로 묶음 집합 사전 설정을 통해 만든 세트를 보고 액세스할 수 있습니다. (배치 집합 사전 설정을 사용하여 만든 세트는 사용자 인터페이스에 *나타나지 않습니다* .)

1. [스핀 세트를 미리 봅니다.](/help/assets/previewing-assets.md)

   스핀 세트를 선택하면 미리 볼 수 있습니다. 회전 집합을 회전합니다. 왼쪽 레일 드롭다운 메뉴에서 **[!UICONTROL 뷰어]** 메뉴에서 다른 뷰어를 선택할 수 있습니다.

1. [스핀 세트 게시를 참조하십시오.](/help/assets/publishing-dynamicmedia-assets.md)

   스핀 세트를 게시하면 URL 및 포함 문자열이 활성화됩니다. 또한 뷰어 사전 설정을 [게시해야 합니다](/help/assets/managing-viewer-presets.md).

1. [웹 응용 프로그램에 URL을 연결하거나 비디오 또는 이미지 뷰어](/help/assets/linking-urls-to-yourwebapplication.md)[를 포함합니다](/help/assets/embed-code.md).

   AEM Assets은 스핀 세트에 대한 URL 호출을 생성하고 스핀 세트를 게시한 후 이를 활성화합니다. 자산을 미리 볼 때 이러한 URL을 복사할 수 있습니다. 또는 웹 사이트에 포함할 수 있습니다.

   스핀 세트를 선택한 다음 왼쪽 레일 드롭다운 메뉴에서 뷰어를 **[!UICONTROL 선택합니다.]**

   회전 [집합을 웹 페이지에 연결](/help/assets/linking-urls-to-yourwebapplication.md) 및 [비디오 또는 이미지 뷰어 포함을 참조하십시오](/help/assets/embed-code.md).

필요한 경우 스핀 세트를 [편집할 수 있습니다](#editing-spin-sets). 또한 스핀 세트 속성을 보고 수정할 [수 있습니다](/help/assets/managing-assets-touch-ui.md#editing-properties).

## 스핀 세트에 대한 자산 업로드 {#uploading-assets-for-spin-sets}

1차원 스핀 세트의 경우 최소 8-12개의 샷과 2차원 스핀 세트의 경우 16-24개의 샷이 필요합니다. 항목이 회전하고 뒤집어지고 있다는 인상을 주기 위해 샷을 정기적으로 촬영해야 합니다. 예를 들어 1차원 회전 집합에 12개의 샷이 있는 경우 각 샷에 대해 30도(360/12)를 회전합니다.

AEM Assets의 다른 자산을 [업로드하는 것처럼 스핀 세트에 대한 이미지를 업로드할 수 있습니다](/help/assets/managing-assets-touch-ui.md).

### 스핀 세트에 대한 이미지 캡처에 대한 지침 {#guidelines-for-shooting-spin-set-images}

다음은 회전 집합 이미지에 대한 몇 가지 우수 사례입니다. 일반적으로 스핀 세트에 이미지가 많을수록 이미지 회전 효과가 더 좋습니다. 하지만 세트에 많은 이미지를 포함하면 이미지를 로드하는 데 걸리는 시간도 증가합니다. AEM에서는 스핀 세트에 사용할 이미지를 촬영하는 데 다음 지침을 권장합니다.

* 1차원 스핀 세트의 경우 최소 8-12개의 이미지와 2차원 스핀 세트의 16-24개의 이미지를 사용합니다. 360도 회전을 위해서는 최소 8장의 이미지가 필요합니다. 2차원 스핀 세트를 만들면 노동 집약적인 경우 1차원 스핀 세트가 더 일반적입니다.
* 손실 없는 형식 사용; TIFF 및 PNG가 권장됩니다.
* 항목이 흰색 또는 기타 고대비 배경에 나타나도록 모든 이미지에 마스크를 적용합니다. 선택적으로 그림자를 추가할 수 있습니다.
* 제품 세부 사항에 대한 충분한 밝기와 집중력을 유지할 수 있습니다.
* 마네킹이나 모델로 패션 의류를 위한 회전 이미지를 만들 수 있습니다. 종종 마네킹이 완전히 마스크되거나(유리 마네킹을 사용) 이미지에 스타일이 적용된 마네킹/드레스가 표시됩니다. 각도 수를 정의하여 모델 내 스핀 세트를 생성할 수 있습니다. 각 각도를 바닥에 테이프로 표시하여 모델이 단계별로 안내하고 각 샷의 방향을 확인합니다.

## 스핀 세트 만들기 {#creating-spin-sets}

이 섹션에서는 AEM에서 스핀 세트를 만드는 방법에 대해 설명합니다.

>[!NOTE]
>
>또한 [일괄 세트 사전 설정을 통해 자동으로 스핀 세트를 만들 수도 있습니다](/help/assets/config-dms7.md#creating%20batch%20set%20presets%20to%20auto-generate%20image%20sets%20and%20spin%20sets). **중요:** 배치 세트는 IPS(Image Production System)에 의해 자산 수정의 일부로 생성되며 Dynamic Media - Scene7 모드에서만 사용할 수 있습니다.
>
>Dynamic Media 구성 - Scene7 모드에서 &quot;이미지 세트 및 스핀 세트를 자동으로 생성하기 위한 배치 세트 사전 설정 만들기&quot;를 [참조하십시오](/help/assets/config-dms7.md#creating%20batch%20set%20presets%20to%20auto-generate%20image%20sets%20and%20spin%20sets).


>[!NOTE]
>
>회전 집합 항목에 이미지가 표시되는 순서. 회전이 매끄러운 360도 보기일 수 있도록 주문해 주십시오.

**스핀 세트를 생성하려면**

1. 자산에서 스핀 세트를 만들 위치로 이동하고 **[!UICONTROL 만들기를]**&#x200B;클릭하고 스핀 **[!UICONTROL 세트를 선택합니다.]** 에셋이 포함된 폴더 내에서 세트를 만들 수도 있습니다. 스핀 세트 편집기가 표시됩니다.

   ![6_5_spinset-createpulldownmenu](assets/6_5_spinset-createpulldownmenu.png)

1. 스핀 세트 편집기의 **[!UICONTROL 제목]** 필드에 스핀 세트 이름을 입력합니다. 스핀 세트의 배너에 이름이 나타납니다. 설명을 입력합니다(선택적).

   ![6_5_spinset-spinseteditortitle](assets/6_5_spinset-spinseteditortitle.png)

   >[!NOTE]
   >
   >스핀 세트를 만들 때 스핀 세트 축소판을 변경하거나 AEM에서 스핀 세트의 자산을 기반으로 축소판을 자동으로 선택하도록 허용할 수 있습니다. 축소판을 선택하려면 축소판 **[!UICONTROL 변경을]** 클릭하고 이미지를 선택합니다. 다른 폴더로 이동하여 이미지를 찾을 수도 있습니다. 축소판을 선택한 다음 스핀 세트에서 AEM을 생성하도록 선택한 경우 자동 축소판으로 **[!UICONTROL 전환을 선택합니다.]**

1. 다음 중 하나를 수행합니다.

   * 스핀 세트 편집기 페이지의 왼쪽 위 모서리 근처에 있는 자산 **[!UICONTROL 추가를 누릅니다.]**

   * 스핀 세트 편집기 페이지의 중간 근처에 있는 탭하여 자산 선택기 **[!UICONTROL 를 엽니다.]**
   스핀 세트에 포함할 자산을 선택하려면 을 누릅니다. 선택한 자산에 확인 표시 아이콘이 표시됩니다. 완료되면 페이지의 오른쪽 위 모서리 근처에 있는 선택을 **[!UICONTROL 누릅니다.]**

   자산 선택기를 사용하여 키워드를 입력하고 **[!UICONTROL Return을 탭하여 자산을 검색할 수 있습니다**. 필터를 적용하여 검색 결과를 조정할 수도 있습니다. 경로, 컬렉션, 파일 유형 및 태그별로 필터링할 수 있습니다. 필터를 선택한 다음 도구 모음에서 **[!UICONTROL 필터]** 아이콘을 누릅니다. 보기 아이콘을 탭하고 열 보기, **[!UICONTROL 카드 보기]**&#x200B;또는 목록 보기 **[!UICONTROL 를 선택하여]**&#x200B;보기를 **[!UICONTROL 변경합니다.]**

   See [Working with Selectors](/help/assets/working-with-selectors.md).

   ![chlimage_1-383](assets/chlimage_1-383.png)

1. 세트에 자산을 추가하면 자동으로 영숫자 순서로 추가됩니다. 자산을 추가한 후 자산을 수동으로 다시 정렬하거나 정렬할 수 있습니다.

   필요한 경우 자산의 순서 변경 아이콘을 자산 파일 이름의 오른쪽으로 드래그하여 이미지 순서를 설정 목록의 위나 아래로 변경합니다.

   ![회전 집합에서 프레임 11의 순서를 새 위치로 드래그하여 변경합니다.](assets/6_5_spinset-reorderassets.png)

   회전 집합에서 프레임 11의 순서를 새 위치로 드래그하여 변경합니다.

1. (선택 사항) 다음 중 하나를 수행합니다.

   * 이미지를 삭제하려면 이미지를 선택하고 자산 **[!UICONTROL 삭제를 누릅니다.]**

   * 사전 설정을 적용하려면 페이지의 오른쪽 위 모서리 근처에 있는 사전 **[!UICONTROL 설정을]**&#x200B;누른 다음 사전 설정을 선택하여 모든 자산에 한 번에 적용할 수 있습니다.

1. **[!UICONTROL 저장을 클릭합니다.]** 새로 만든 스핀 세트가 만든 폴더에 나타납니다.

## 스핀 세트 보기 {#viewing-spin-sets}

사용자 인터페이스에서 또는 [일괄 세트 사전 설정을 사용하여 자동으로 스핀 세트를 만들 수 있습니다](/help/assets/config-dms7.md#creating%20batch%20set%20presets%20to%20auto-generate%20image%20sets%20and%20spin%20sets). 하지만 배치 집합 사전 설정을 사용하여 만든 세트는 사용자 인터페이스에 *나타나지 않습니다* . 세 가지 방법으로 일괄 세트 사전 설정을 통해 만든 세트에 액세스할 수 있습니다. (사용자 인터페이스에서 스핀 세트를 생성한 경우에도 이러한 방법을 사용할 수 있습니다.)

>[!NOTE]
>
>스핀 세트 편집에 설명된 대로 사용자 인터페이스를 통해 세트를 볼 수도 [있습니다](#editing-spin-sets).

**스핀 세트를 보려면**

1. 개별 자산의 속성을 열 때. 속성은 선택한 자산이 (세트 구성원 아래) 멤버인 **[!UICONTROL 것을]**&#x200B;나타냅니다. 전체 세트를 보려면 세트 이름을 클릭합니다.

   ![chlimage_1-156](assets/chlimage_1-384.png)

1. 모든 세트의 멤버 이미지에서 자산이 **[!UICONTROL 속한]** 세트를 표시하려면 세트 메뉴를 선택합니다.

   ![chlimage_1-157](assets/chlimage_1-385.png)

1. 검색에서 필터 **[!UICONTROL 를]**&#x200B;선택한 다음 **[!UICONTROL Dynamic Media]** 을 확장하고 **[!UICONTROL 세트를선택할 수있습니다.]**

   검색은 UI에서 수동으로 만들거나 배치 집합 사전 설정을 통해 자동으로 생성된 일치 집합을 반환합니다. 자동화된 세트의 경우, 검색 `Starts with` `Contains` 기준을 사용하는 AEM 검색과는 다른 검색 기준을 사용하여 검색 쿼리를 수행합니다. 필터를 **[!UICONTROL 세트로]** 설정하면 자동화된 세트를 검색할 수 있습니다.

   ![chlimage_1-158](assets/chlimage_1-386.png)

## 스핀 세트 편집 {#editing-spin-sets}

다음과 같은 다양한 회전 집합 편집 작업을 수행할 수 있습니다.

* 스핀 세트에 이미지를 추가합니다.
* 회전 세트에서 이미지 순서를 변경합니다.
* 스핀 세트에서 자산을 삭제합니다.
* 뷰어 사전 설정을 적용합니다.
* 스핀 세트를 삭제합니다.

**스핀 세트를 편집하려면**

1. 다음 중 하나를 수행합니다.

   * 스핀 세트 자산 위로 마우스를 가져간 다음 **[!UICONTROL 편집]** (연필 아이콘)을 누릅니다.
   * 스핀 세트 자산 위로 마우스를 가져간 다음 **[!UICONTROL 선택]** (확인 표시 아이콘)을 누른 다음 도구 모음에서 **[!UICONTROL 편집을]** 누릅니다.

   * 스핀 세트 자산을 누른 다음 도구 모음에서 **[!UICONTROL 편집]** (연필 아이콘)을 누릅니다.

1. 스핀 세트를 편집하려면 다음 중 하나를 수행합니다.

   * 이미지의 순서를 바꾸려면 이미지를 새 위치로 드래그합니다(항목을 이동하려면 순서 변경 아이콘 선택).
   * 항목을 오름차순 또는 내림차순으로 정렬하려면 열 제목을 클릭합니다.
   * 자산을 추가하거나 기존 자산을 업데이트하려면 자산 **[!UICONTROL 추가를 클릭합니다.]** 자산으로 이동하여 선택한 다음 오른쪽 위 모서리 **[!UICONTROL 근처에서 선택을]** 누릅니다.
AEM에서 축소판에서 사용하는 이미지를 다른 이미지로 대체하여 삭제하면 원래 자산이 계속 표시됩니다.
   * 자산을 삭제하려면 해당 자산을 선택하고 자산 삭제를 클릭하거나 **[!UICONTROL 탭합니다.]**
   * 사전 설정을 적용하려면 사전 설정 아이콘을 누르거나 클릭하고 사전 설정을 선택합니다.
   * 전체 스핀 세트를 삭제하려면 스핀 세트로 이동하고 선택한 다음 **[!UICONTROL 삭제를 선택합니다]**

   >[!NOTE]
   >
   >세트로 이동한 다음 왼쪽 레일에서 멤버 **** 설정을 누른 다음 개별 자산의 연필 아이콘을 눌러 편집 창을 열어 이미지를 편집할 수 있습니다.

1. 편집을 **[!UICONTROL 마치면 저장을]** 클릭합니다.

## 스핀 세트 미리 보기 {#previewing-spin-sets}

자산 [미리 보기를 참조하십시오](/help/assets/previewing-assets.md).

## 스핀 세트 게시 {#publishing-spin-sets}

자산 [게시를 참조하십시오](/help/assets/publishing-dynamicmedia-assets.md).
