---
title: 혼합 미디어 세트
description: Dynamic Media에서 혼합 미디어 세트를 사용하는 방법을 알아봅니다
uuid: cecad772-ed05-46f6-ba44-107195866b0d
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: ed84157a-e6b4-4dde-af2e-a1e0b6259628
docset: aem65
feature: Mixed Media Sets,Asset Management
role: User, Admin
exl-id: 70a72fb9-a289-4eda-abcc-300edf9f1961
source-git-commit: 7b29fc96768dc2238ebf9596b136ec10fa71aca9
workflow-type: tm+mt
source-wordcount: '1493'
ht-degree: 17%

---

# 혼합 미디어 세트{#mixed-media-sets}

혼합 미디어 세트를 사용하면 이미지, 이미지 세트, 스핀 세트 및 비디오를 한 프레젠테이션에 혼합할 수 있습니다.

Mixed Media Sets are designated by a banner with the word **[!UICONTROL MixedMediaSet]**. In addition, if the Mixed Media Set is published, then the publish date, indicated by the **[!UICONTROL World]** icon is on the banner along with the last modification date, indicated by the **[!UICONTROL Pencil]** icon displays.

![chlimage_1-137](assets/chlimage_1-348.png)

>[!NOTE]
>
>Assets 사용자 인터페이스에 대한 자세한 내용은 [자산 관리](/help/assets/manage-assets.md).

## 빠른 시작: 혼합 미디어 집합 {#quick-start-mixed-media-sets}

혼합 미디어 세트를 사용하여 빠르게 시작하고 실행하려면 다음 단계를 수행합니다.

1. [자산 업로드](#uploading-assets).

   Start by uploading the images and videos for your Mixed Media Sets. If necessary, create your [Image Sets](/help/assets/image-sets.md) and [Spin Sets](/help/assets/spin-sets.md). 사용자는 혼합 미디어 세트 뷰어에서 이미지를 확대할 수 있으므로 이미지를 신중하게 선택하십시오. Make sure that the images are least 2000 pixels in the largest dimension.

   자세한 내용은 [Dynamic Media - 지원되는 래스터 이미지 형식](/help/assets/assets-formats.md#supported-raster-image-formats-dynamic-media) 혼합 미디어 집합에서 지원하는 형식 목록입니다.

1. [혼합 미디어 집합 만들기](#creating-mixed-media-sets).

   혼합 미디어 세트를 만들려면 자산 페이지에서 **[!UICONTROL 만들기]** > **[!UICONTROL 혼합 미디어 세트]** 그런 다음 세트의 이름을 지정하고, 자산을 선택하고, 이미지가 나타나는 순서를 선택합니다.

   자세한 내용은 [선택기를 사용한 작업](/help/assets/working-with-selectors.md).

1. 설정 [혼합 미디어 뷰어 사전 설정](/help/assets/managing-viewer-presets.md)필요한 경우 ).

   Administrators can create or modify Mixed Media Set Viewer Presets. To see your mixed media with a viewer preset, select the mixed media set, and in the left-rail drop-down menu, select **[!UICONTROL Viewers]**.

   뷰어 사전 설정을 만들거나 편집하려면 다음을 참조하십시오 **[!UICONTROL 도구]** > **[!UICONTROL 자산]** > **[!UICONTROL 뷰어 사전 설정]**.

   자세한 내용은 [뷰어 사전 설정 추가 및 편집](/help/assets/managing-viewer-presets.md).

1. [혼합 미디어 집합 미리 보기](#previewing-mixed-media-sets).

   혼합 미디어 세트를 선택하면 미리 볼 수 있습니다. 선택한 뷰어에서 혼합 미디어 세트를 검사할 수 있도록 축소판 아이콘을 선택합니다. 에서 다른 뷰어를 선택할 수 있습니다 **[!UICONTROL 뷰어]** 메뉴 아래의 왼쪽 레일 드롭다운 메뉴에서 사용할 수 있습니다.

1. [혼합 미디어 집합 게시](#publishing-mixed-media-sets).

   혼합 미디어 세트를 게시하면 URL 및 포함 문자열이 활성화됩니다. 또한 다음을 수행해야 합니다 [뷰어 사전 설정 게시](/help/assets/managing-viewer-presets.md#publishing-viewer-presets).

1. [웹 응용 프로그램에 URL 연결](/help/assets/linking-urls-to-yourwebapplication.md) 또는 [비디오 또는 이미지 뷰어 포함](/help/assets/embed-code.md).

   Adobe Experience Manager Assets는 혼합 미디어 세트에 대한 URL 호출을 만들고 혼합 미디어 세트를 게시한 후 활성화합니다. 자산을 미리 볼 때 이러한 URL을 복사할 수 있습니다. 또는 웹 사이트에 포함할 수 있습니다.

   혼합 미디어 세트를 선택한 다음 왼쪽 레일 드롭다운 메뉴에서 을 선택합니다 **[!UICONTROL 뷰어]**.

   자세한 내용은 [웹 페이지에 혼합 미디어 집합 연결](/help/assets/linking-urls-to-yourwebapplication.md) 및 [비디오 또는 이미지 뷰어 포함](/help/assets/embed-code.md).

필요한 경우 편집할 수 있습니다 [혼합 미디어 집합](#editing-mixed-media-sets). 또한 를 보고 수정할 수 있습니다 [혼합 미디어 집합 속성](/help/assets/manage-assets.md#editing-properties).

>[!NOTE]
>
>세트를 만드는 데 문제가 있다면 다음을 참조하십시오 [Dynamic Media 문제 해결 - Scene7 모드](/help/assets/troubleshoot-dms7.md).

## 자산 업로드 {#uploading-assets}

먼저 혼합 미디어 세트에 대한 이미지 및 비디오를 업로드하십시오. 사용자는 혼합 미디어 세트 뷰어에서 이미지를 확대할 수 있으므로 이미지를 신중하게 선택하십시오. 가장 큰 차원에서 이미지가 2000픽셀 이상인지 확인합니다.

또한 혼합 미디어 세트에 스핀 세트 또는 이미지 세트를 추가하려면 해당 세트도 만드십시오.

자세한 내용은 [Dynamic Media - 지원되는 래스터 이미지 형식](/help/assets/assets-formats.md#supported-raster-image-formats-dynamic-media) 혼합 미디어 집합에서 지원하는 형식 목록입니다.

## 혼합 미디어 세트 만들기 {#creating-mixed-media-sets}

이미지, 이미지 세트, 스핀 세트 및 비디오를 혼합 미디어 세트에 추가할 수 있습니다. 혼합 미디어 세트에 추가하기 전에 파일, 이미지 세트 및 스핀 세트를 게시할 준비가 되었는지 확인합니다.

세트에 자산을 추가하면 자동으로 영숫자 순서로 추가됩니다. 자산이 추가된 후 자산을 수동으로 재정렬하거나 정렬할 수 있습니다.

**혼합 미디어 세트를 만들려면:**

1. 자산에서 혼합 미디어 세트를 만들 위치로 이동하여 을 선택합니다 **[!UICONTROL 만들기]**, 을(를) 선택하고 을(를) 선택합니다. **[!UICONTROL 혼합 미디어 세트]**. You can also create the set from inside a folder that contains your assets. The Mixed Media Set Editor displays.

   ![chlimage_1-138](assets/chlimage_1-349.png)

1. 혼합 미디어 세트 편집기에서 **[!UICONTROL 제목]**&#x200B;를 입력합니다. 혼합 미디어 세트의 이름을 입력합니다. 이 이름은 혼합 미디어 집합 전체의 배너에 표시됩니다. 설명을 입력합니다(선택적).

   ![chlimage_1-139](assets/chlimage_1-350.png)

   >[!NOTE]
   >
   >혼합 미디어 세트를 생성할 때 혼합 미디어 세트 축소판을 변경하거나 혼합 미디어 세트의 자산을 기반으로 Experience Manager이 자동으로 축소판을 선택할 수 있습니다. 축소판을 선택하려면 **[!UICONTROL 축소판 변경]** 이미지를 선택합니다(다른 폴더로 이동하여 이미지를 찾을 수도 있습니다.). 축소판을 선택한 다음 혼합 미디어 집합에서 생성할 Experience Manager을 선택한 경우 **[!UICONTROL 자동 축소판으로 전환]**.

1. 혼합 미디어 세트에 포함할 자산을 선택할 수 있도록 자산 선택기를 선택합니다. 선택한 다음 선택합니다 **[!UICONTROL 선택]**.

   With the Asset Selector, you can search for assets by typing in a keyword and tapping **[!UICONTROL Return]**. You can also apply filters to refine your search results. You can filter by path, collection, file type, and tag. 필터를 선택한 다음 **[!UICONTROL 필터]** 아이콘 을 클릭하여 제품에서 사용할 수 있습니다. Change the view by selecting the **[!UICONTROL View]** icon and selecting **[!UICONTROL List View]**, **[!UICONTROL Column View]**, or **[!UICONTROL Card View]**.

   자세한 내용은 [선택기를 사용한 작업](/help/assets/working-with-selectors.md).

   ![chlimage_1-140](assets/chlimage_1-383.png)

1. 자산을 목록의 위나 아래로 드래그하여 재정렬합니다(반드시 **[!UICONTROL 재정렬]** 아이콘)만 로드하는 것입니다.

   ![chlimage_1-141](assets/chlimage_1-352.png)

   축소판을 추가하려면 **+** **[!UICONTROL 축소판]** 이미지 옆에 있는 아이콘을 클릭하고 원하는 축소판으로 이동합니다. 모든 축소판 이미지를 선택하면 **[!UICONTROL 저장]**.

   >[!NOTE]
   >
   >자산을 추가하려면 을 선택합니다 **[!UICONTROL 자산 추가]**.

1. 자산을 삭제하려면 해당 확인란을 선택하고 을(를) 선택합니다 **[!UICONTROL 자산 삭제]**.
1. 사전 설정을 적용하려면 **[!UICONTROL 사전 설정]** 오른쪽 상단 모서리에서 사전 설정을 선택하여 자산에 적용합니다.
1. **[!UICONTROL 저장]**&#x200B;을 선택합니다. 새로 만든 혼합 미디어 세트가 만든 폴더에 나타납니다.

## 혼합 미디어 집합 편집 {#editing-mixed-media-sets}

사용자 인터페이스에서 직접 혼합 미디어 세트의 자산에 대한 다양한 편집 작업을 수행할 수 있습니다 [자산에서 모든 자산을](/help/assets/manage-assets.md). 혼합 미디어 세트에서 다음 작업을 수행할 수도 있습니다.

* 혼합 미디어 세트에 자산을 추가합니다.
* 혼합 미디어 집합에서 자산 재정렬입니다.
* 혼합 미디어 집합에서 자산을 삭제합니다.
* 뷰어 사전 설정을 적용합니다.
* 기본 축소판을 변경합니다.

**혼합 미디어 세트를 편집하려면:**

1. 다음 중 하나를 수행합니다.

   * 혼합 미디어 세트 자산을 마우스로 가리킨 다음, 을 선택합니다 **[!UICONTROL 편집]** (연필 아이콘).
   * 혼합 미디어 세트 자산을 마우스로 가리킨 다음, 을 선택합니다 **[!UICONTROL 선택]** (확인 표시 아이콘)을 선택한 다음 **[!UICONTROL 편집]** 클릭합니다.

   * 혼합 미디어 세트 자산을 선택한 다음 을 선택합니다 **[!UICONTROL 편집]** (연필 아이콘)을 클릭하여 제품에서 사용할 수 있습니다.

1. 혼합 미디어 세트 편집기에서 다음 중 하나를 수행합니다.

   * 자산 순서를 조정하려면 - 왼쪽 패널에서 를 선택합니다 **[!UICONTROL 자산]** (그림 아이콘) 자산을 새 위치로 드래그합니다.
   * 자산을 추가하려면 - 도구 모음에서 를 선택합니다 **[!UICONTROL 자산 추가]**. 자산으로 이동합니다. 추가하려는 각 자산에 대해, 자산의 이미지(자산 이름이 아님)를 마우스로 가리킨 다음, 확인 표시 아이콘을 선택합니다. 오른쪽 위 모서리에서 을(를) 선택합니다 **[!UICONTROL 선택]**.

   * 자산을 삭제하려면 - 왼쪽 패널에서 **[!UICONTROL 자산]** (그림 아이콘)를 선택한 다음 자산을 선택합니다. 도구 모음 모음에서 를 선택합니다 **[!UICONTROL 자산 삭제]**.

   * 자산을 오름차순이나 내림차순으로 정렬하려면 왼쪽 패널에서 를 선택합니다 **[!UICONTROL 자산]** (그림 아이콘) 오른쪽 **[!UICONTROL 자산]** 제목에서 위쪽 또는 아래쪽 캐럿 아이콘을 선택합니다.

      >[!NOTE]
      >
      >* 모든 보기 모드(예: **[!UICONTROL 카드 보기]** 또는 **[!UICONTROL 열 보기]**) 혼합 미디어 세트로 이동합니다. 자산을 마우스로 가리킨 다음, 선택하도록 확인 표시 아이콘을 선택합니다. 누르기 **[!UICONTROL 백스페이스]** 키보드에서 를 선택하거나 **[!UICONTROL 자세히]** (세 점)을 도구 모음에서 를 선택한 다음 **[!UICONTROL 삭제]**.
      >
      >* 세트로 이동한 다음 를 클릭하여 혼합 미디어 세트에서 자산을 편집할 수 있습니다 **[!UICONTROL 구성원 설정]** 왼쪽 레일에 있습니다. 을(를) 선택합니다 **[!UICONTROL 연필]** 아이콘을 클릭하여 개별 자산에서 편집 창에서 엽니다.


1. 선택 **[!UICONTROL 저장]** 편집을 완료하면 됩니다.

   >[!NOTE]
   >
   >* To edit the assets in a Mixed Media Set - Navigate to the Mixed Media Set. Experience Manager 세트 미리 보기 페이지에서 열리도록 세트를 탭(선택하지 않음)합니다. 왼쪽 레일에서 드롭다운 캐럿을 선택하여 드롭다운 목록을 연 다음 을 선택합니다 **[!UICONTROL 구성원 설정]**. 구성원 설정 페이지에서 자산을 마우스로 가리킨 다음 을 선택합니다 **[!UICONTROL 편집]** (연필 아이콘)을 클릭하여 편집 페이지를 엽니다.
   >
   >* To delete an entire Mixed Media Set - From any viewing mode (such as Card view or Column view), navigate to the Mixed Media Set. 세트를 마우스로 가리킨 다음, 을 선택합니다 **선택** (확인 표시 아이콘) 누르기 **[!UICONTROL 백스페이스]** 키보드에서 을(를) 선택하거나 **[!UICONTROL 자세히]** (세 점 행)을 선택한 다음 **[!UICONTROL 삭제]**.


## 혼합 미디어 세트 미리 보기 {#previewing-mixed-media-sets}

자세한 내용은 [자산 미리 보기](/help/assets/previewing-assets.md) 혼합 미디어 세트를 미리 보는 방법에 대한 자세한 내용을 참조하십시오.

## 혼합 미디어 집합 게시 {#publishing-mixed-media-sets}

자세한 내용은 [자산 게시](/help/assets/publishing-dynamicmedia-assets.md) 혼합 미디어 세트를 게시하는 방법에 대한 자세한 내용.

>[!NOTE]
>
>처음 게시할 때 혼합 미디어 세트가 게재 서비스에서 완전히 종료되지 않은 경우 혼합 미디어 세트를 두 번째로 게시합니다.
