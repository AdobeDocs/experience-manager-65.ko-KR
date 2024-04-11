---
title: 콘텐츠 조각의 참조 사용에 대해 알아보기
description: 콘텐츠, 다른 조각과 자산(미디어)의 콘텐츠 조각에서 참조를 사용하는 방법에 대해 알아봅니다. Headless CMS 작성에서 중첩된 조각의 필요성과 메커니즘을 소개합니다.
exl-id: d54a0a40-a8af-456a-9bf5-219d84540c97
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments
role: Admin, Architect,Data Architect,Developer,User,Leader
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 95%

---

# 콘텐츠 조각의 참조 사용에 대해 알아보기 {#author-headless-references}

## 지금까지의 스토리 {#story-so-far}

[AEM Headless 콘텐츠 작성자 여정](overview.md) 시작 부분의 [소개](introduction.md)에서는 Headless 작성과 관련된 기본 개념 및 용어를 다룹니다.

AEMaaCS를 통한 작성, 특히 콘텐츠 조각 작성에 대한 소개와 함께 Headless CMS 작성의 기본 사항에 대해 알아보았습니다.

이 문서는 해당 사항을 기본으로 하며, 이를 통해 참조를 사용하여 자체 AEM Headless 프로젝트의 콘텐츠를 작성하는 방법을 이해할 수 있습니다.

## 목표 {#objective}

* **대상자**: 고급
* **목표**: Headless CMS 작성에 대한 참조 사용을 소개합니다. 사용 가능한 참조의 종류와 참조 목적은 무엇입니까?

   * 콘텐츠 참조
   * 자산/미디어 참조
   * 조각 참조
   * 텍스트 블록 내 애드혹 참조

## 참조란 무엇입니까? {#what-are-references}

참조는 다른 콘텐츠, 자산(이미지에서와 같이) 또는 다른 조각 등 리소스를 연결하는 메커니즘일 뿐입니다. 매우 유사하지만 차이점이 몇 가지 있습니다.

일부 참조에는 전용 데이터 유형(예: 콘텐츠 참조 및 조각 참조)이 있지만 다른 참조는 텍스트 블록 내 참조로 추가됩니다(자산 참조 및 애드혹 참조).

![콘텐츠 조각 - 참조](/help/journey-headless/author/assets/headless-journey-author-references-01.png)

## 콘텐츠 참조 {#content-references}

콘텐츠 참조는 다른 모든 콘텐츠를 참조할 수 있도록 해 줍니다. 이러면 콘텐츠 항목을 선택할 수 있는 브라우저가 열립니다.

## 자산/미디어 참조 {#assets-media-references}

**자산 삽입** 옵션을 사용하여 텍스트 블록 내에서 자산(예: 이미지 또는 미디어)을 참조할 수 있습니다. 이러면 자산 항목을 선택할 수 있는 브라우저가 열립니다.

![콘텐츠 조각 - 자산 삽입](/help/journey-headless/author/assets/headless-journey-author-references-02.png)

## 조각 참조 {#fragment-references}

다시 한 번, 조각 참조는 다른 조각을 참조할 수 있도록 해줍니다. 이 작업이 중요한 이유에 대해 자세히 알아봅니다.

예를 들어 다음 콘텐츠 조각 모델을 정의할 수도 있습니다.

* 도시
* 회사
* 개인
* 상

매우 간단한 것처럼 보이지만 회사에는 CEO와 직원이 있습니다.이 모두 사람이고 각각은 개인으로 정의됩니다.

개인에게 상 한 개(또는 두 개)가 제공될 수 있습니다.

* 내 회사 - 회사
   * CEO - 개인
   * 직원 - 개인
      * 개인 상 - 상

시작에만 적용되는 과정입니다. 복잡도에 따라 상은 회사별로 지정되거나 회사의 본사는 특정 도시에 있을 수 있습니다.

사용자(작성자)와 Headless 애플리케이션 모두가 이해하므로 조각 참조를 사용하여 해당 상호 관계를 나타낼 수 있습니다.

작성자는 해당 관계(콘텐츠 조각 모델 생성 시 콘텐츠 설계자가 수행하는 작업)를 정의할 책임이 없지만 참조를 인식하고 편집하는 방법에 대해 알아야 합니다.

### 중첩된 조각을 작성하는 방법 {#author-nested-fragment}

조각 참조 작성은 매우 간단합니다(필드는 일반적으로 **조각 참조**&#x200B;로 레이블이 지정되지 않음). 참조를 직접 입력하거나 폴더 아이콘을 선택하여(선택 가능성이 높음) 필요한 조각을 탐색하고 선택할 수 있는 브라우저를 열 수 있습니다.

![콘텐츠 조각 - 참조](/help/journey-headless/author/assets/headless-journey-author-references-03.png)

콘텐츠 조각 모델 컨트롤 정의:

* 여러 참조를 추가하도록 사용할지 여부
* 선택 가능한 콘텐츠 조각의 모델 유형인 콘텐츠 조각 모델은 참조에 허용되는 조각 모델을 정의하므로 AEM은 해당 모델을 기반으로 하는 조각만 제공합니다.

### 중첩된 조각을 탐색하는 방법 {#navigate-nested-fragment}

콘텐츠 조각 편집기의 **구조 트리** 탭을 사용하여 조각에서 참조하는 조각을 탐색한 다음 이에 포함될 수 있는 모든 참조를 탐색할 수 있습니다. 참조를 선택하면 편집용 조각이 열립니다.

>[!NOTE]
>
>기본 패널에서 탐색 표시를 사용하여 시작점으로 돌아갈 수 있습니다.

![콘텐츠 조각 구조 트리](/help/assets/content-fragments/assets/cfm-structuretree-02.png)

## 애드혹 참조 {#adhoc-references}

애드혹 참조는 텍스트 블록 내에서 간단한 링크로 추가할 수 있습니다.

![콘텐츠 조각 - 애드혹 참조](/help/journey-headless/author/assets/headless-journey-author-references-04.png)

## 다음 단계 {#whats-next}

이제 콘텐츠 조각의 참조 및 구조에 대해 배웠으므로 다음 단계는 [메타데이터 및 태그 지정에 대해 알아보기](metadata-tagging.md)입니다. 콘텐츠 조각의 메타데이터 및 태그를 정의하는 방법을 소개하고 자세히 설명합니다.

## 추가 리소스 {#additional-resources}

* [콘텐츠 조각을 사용하여 작업](/help/assets/content-fragments/content-fragments.md)

   * [콘텐츠 조각 관리](/help/assets/content-fragments/content-fragments-managing.md)

      * [자산 폴더에 구성 적용](/help/assets/content-fragments/content-fragments-configuration-browser.md#apply-the-configuration-to-your-assets-folder)

      * [콘텐츠 조각 만들기](/help/assets/content-fragments/content-fragments-managing.md#creating-a-content-fragment)

   * [변형 - 콘텐츠 조각 작성](/help/assets/content-fragments/content-fragments-variations.md)

   * [콘텐츠 조각 모델](/help/assets/content-fragments/content-fragments-models.md)

      * [콘텐츠 조각 모델 - 데이터 형식](/help/assets/content-fragments/content-fragments-models.md#data-types)

      * [콘텐츠 조각 모델 - 속성](/help/assets/content-fragments/content-fragments-models.md#properties)

* 시작 안내서
   * [에셋 폴더 헤드리스 빠른 시작 안내서 만들기](/help/sites-developing/headless/getting-started/create-assets-folder.md)

* [AEM Headless 콘텐츠 설계자 여정](/help/journey-headless/architect/overview.md)

* [AEM Headless 번역 여정](/help/journey-headless/translation/overview.md)
