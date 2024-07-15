---
title: We.Retail에서 응답형 레이아웃 시험 사용
description: We.Retail을 사용하여 Adobe Experience Manager에서 응답형 레이아웃 을 테스트하는 방법을 알아봅니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 6df5fb10-a7f1-4d5d-ac00-b4be3d5d3d18
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 9%

---

# We.Retail에서 응답형 레이아웃 시험 사용{#trying-out-responsive-layout-in-we-retail}

모든 We.Retail 페이지는 레이아웃 컨테이너 구성 요소를 사용하여 응답형 디자인을 구현합니다. 레이아웃 컨테이너는 응답형 그리드 내에 구성 요소를 배치할 수 있도록 해 주는 단락 시스템을 제공합니다. 이 격자를 사용하면 디바이스/창 크기 및 포맷에 따라 레이아웃을 다시 정렬할 수 있습니다. 구성 요소는 페이지 편집기의 **레이아웃** 모드와 함께 사용됩니다. 이 모드에서는 장치에 종속적인 응답형 레이아웃을 만들고 편집할 수 있습니다.

## 시험 사용 {#trying-it-out}

1. 언어 마스터 분기의 경험 섹션에서 북극 서핑 페이지를 편집합니다.

   http://localhost:4502/editor.html/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.html

1. 웹 사이트의 방문자에게 페이지가 렌더링되는 대로 보려면 **미리 보기**(으)로 전환하십시오. 문서 *노르웨이에 있는 알로하 증류주*&#x200B;의 내용으로 아래로 스크롤합니다.

   ![chlimage_1-178](assets/chlimage_1-178.png)

1. 브라우저 창의 크기를 조정하고 레이아웃이 크기 조정에 따라 동적으로 조정되는지 확인합니다.

   ![chlimage_1-179](assets/chlimage_1-179.png)

1. 레이아웃 모드로 전환합니다. 에뮬레이터 도구 모음이 자동으로 표시되어 타겟팅된 디바이스별로 레이아웃을 계획할 수 있습니다.

   구성 요소를 선택하면 구성 요소의 크기 조정 핸들과 함께 편집 메뉴에 부동 및 숨기기 옵션이 표시됩니다.

   ![chlimage_1-180](assets/chlimage_1-180.png)

1. 구성 요소의 크기 조정 핸들을 잡고 드래그하면 크기 조정에 적용할 레이아웃 격자가 자동으로 표시됩니다.

   ![chlimage_1-181](assets/chlimage_1-181.png)

## 추가 정보 {#further-information}

자세한 내용은 작성 문서 [응답형 레이아웃](/help/sites-authoring/responsive-layout.md) 또는 관리자 문서 [레이아웃 컨테이너 및 레이아웃 모드 구성](/help/sites-administering/configuring-responsive-layout.md)을 참조하십시오.
