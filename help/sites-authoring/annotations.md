---
title: 컨텐츠 페이지 편집 시 주석
description: 콘텐츠와 직접 관련된 많은 구성 요소를 사용하여 주석을 추가할 수 있습니다.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
exl-id: de1ae7e3-db3a-4b5e-8a4f-ae111227181f
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 33%

---

# 페이지 편집 시 주석{#annotations-when-editing-a-page}

웹 사이트의 페이지에 콘텐츠를 추가하는 것은 종종 실제로 게시되기 전에 토론이 진행될 수 있습니다. 이를 돕기 위해 콘텐츠와 직접 관련된 많은 구성 요소(예: 레이아웃과 반대)를 사용하여 주석을 추가할 수 있습니다.

주석을 달면 페이지에 색상이 있는 마커/스티커 메모가 생깁니다. 주석을 사용하는 사용자(또는 다른 사용자)는 다른 작성자/검토자에 대한 댓글 및/또는 질문을 할 수 있습니다.

>[!NOTE]
>
>개별 구성 요소의 정의에 따라 해당 구성 요소의 인스턴스에 주석을 달 수 있는지 여부가 결정됩니다.

>[!NOTE]
>
>클래식 UI에서 생성된 주석은 터치 지원 UI에 표시됩니다. 그러나 스케치는 UI별로 다르며 스케치가 만들어진 UI에만 표시됩니다.

>[!CAUTION]
>
>리소스(예: 단락)를 삭제하면 해당 리소스에 첨부된 주석과 스케치가 페이지에서의 위치와 관계없이 모두 삭제됩니다.

>[!NOTE]
>
>필요에 따라 주석이 추가, 업데이트 또는 삭제될 때 알림 메시지를 보내는 워크플로우를 개발할 수도 있습니다.

## 주석 {#annotations}

주석을 작성 및 확인하는 데 특수 [모드](/help/sites-authoring/author-environment-tools.md#page-modes)가 사용됩니다.

>[!NOTE]
>
>잊지 마 [댓글](/help/sites-authoring/basic-handling.md#timeline) 또한 페이지에 대한 피드백을 제공할 수도 있습니다.

>[!NOTE]
>
>다양한 리소스에 주석을 달 수 있습니다.
>
>* [에셋에 주석 달기](/help/assets/manage-assets.md#annotating)
>* [비디오 자산에 주석 달기](/help/assets/managing-video-assets.md#annotate-video-assets)
>

### 구성 요소에 주석 달기 {#annotating-a-component}

주석 모드에서는 콘텐츠의 주석을 만들기, 편집, 이동 또는 삭제할 수 있습니다.

1. 페이지를 편집할 때 도구 모음(오른쪽 상단)의 아이콘을 사용하여 주석 모드에 들어갈 수 있습니다.

   ![주석](do-not-localize/screen_shot_2018-03-22at110414.png)

   이제 기존의 모든 주석을 볼 수 있습니다.

   >[!NOTE]
   >
   >주석 모드를 종료하려면 상단 도구 모음 오른쪽에 있는 주석 아이콘(x 기호)을 클릭합니다.

1. 주석 추가를 시작하려면 주석 추가 아이콘(도구 모음 왼쪽의 더하기 기호)을 클릭합니다.

   >[!NOTE]
   >
   >주석 추가를 중지하고 보기로 돌아가려면 상단 도구 모음 왼쪽에 있는 취소 아이콘(흰색 원의 x 기호)을 클릭합니다.

1. 필요한 구성 요소(파란색 테두리로 강조 표시되고 주석을 추가할 수 있는 구성 요소)를 클릭하여 주석을 추가하고 대화 상자를 엽니다.

   ![screen_shot_2018-03-22at110606](assets/screen_shot_2018-03-22at110606.png)

   이 대화 상자에서는 적절한 필드 및/또는 아이콘을 사용하여 다음 작업을 할 수 있습니다.

   * 주석 텍스트를 입력합니다.
   * 스케치(선과 모양)를 만들어 구성 요소 영역을 강조 표시합니다.

     스케치를 생성할 때 커서는 크로스와이어로 변경됩니다. 서로 구분되는 여러 선을 그릴 수 있습니다. 스케치 선은 주석 색상을 반영하며 화살표, 원 또는 타원 중 하나일 수 있습니다.

     ![Sketch](do-not-localize/screen_shot_2018-03-22at110640.png)

   * 색상 선택/변경:

     ![색상 선택/변경](do-not-localize/chlimage_1-19.png)

   * 주석 삭제

     ![주석 삭제](do-not-localize/screen_shot_2018-03-22at110647.png)

1. 대화 상자 외부를 클릭/탭하여 주석 대화 상자를 닫을 수 있습니다. 스케치와 함께 주석의 잘린 보기(첫 번째 단어)가 표시됩니다.

   ![screen_shot_2018-03-22at110850](assets/screen_shot_2018-03-22at110850.png)

1. 특정 주석의 편집이 끝나면 다음 작업을 수행할 수 있습니다.

   * 텍스트 표시자를 클릭하여 주석을 엽니다. 열면 전체 텍스트를 보고, 변경 내용을 적용하거나 주석을 삭제할 수 있습니다.

      * 스케치는 주석과 독립적으로 삭제할 수 없습니다.

   * 텍스트 마커 위치 변경.
   * 스케치 선을 클릭하여 해당 스케치를 선택하고 원하는 위치로 드래그합니다.
   * 구성 요소 이동 또는 복사

      * 모든 관련 주석과 해당 스케치가 이동 또는 복사되며 단락을 기준으로 해당 위치가 그대로 유지됩니다.

1. 주석 모드를 종료하고 이전에 사용한 모드로 돌아가려면 상단 도구 모음 오른쪽에 있는 주석 아이콘(x 기호)을 클릭합니다.

>[!NOTE]
>
>다른 사용자가 잠근 페이지에는 주석을 추가할 수 없습니다.

### 주석 표시기 {#annotation-indicator}

주석은 편집 모드에 나타나지는 않지만, 도구 모음 상단 오른쪽에 있는 배지에 현재 페이지에 대해 존재하는 주석의 수가 표시됩니다. 배지는 기본 [주석] 아이콘을 대신하며 주석 모드로/에서 전환하는 빠른 링크로 작동합니다.

![주석 표시기](assets/chlimage_1-242.png)
