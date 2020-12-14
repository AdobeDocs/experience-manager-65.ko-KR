---
title: 샘플 페이지 만들기
seo-title: 샘플 페이지 만들기
description: 샘플 커뮤니티 사이트 만들기
seo-description: 샘플 커뮤니티 사이트 만들기
uuid: 04a8f027-b7d8-493a-a9bd-5c4a6715d754
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: developing
discoiquuid: a03145f7-6697-4797-b73e-6f8d241ce469
translation-type: tm+mt
source-git-commit: 824ddd48e4680eed1d4612c6ad450a8f1bc68e7c
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 2%

---


# 샘플 페이지 {#create-a-sample-page} 만들기

AEM 6.1 Communities의 경우 샘플 페이지를 만드는 가장 쉬운 방법은 페이지 기능만으로 구성된 간단한 커뮤니티 사이트를 만드는 것입니다.

[제작 구성 요소를 활성화할 수 있도록 parsys 구성 요소가 포함됩니다](basics.md#accessing-communities-components).

샘플 구성 요소 탐색을 위한 다른 옵션은 [커뮤니티 구성 요소 안내서](components-guide.md)에 표시된 기능을 사용하는 것입니다.

## 커뮤니티 사이트 {#create-a-community-site} 만들기

이것은 [AEM Communities 시작](getting-started.md)에 설명된 새 사이트를 만드는 것과 매우 유사합니다.

주요 차이점은 이 자습서가 모든 커뮤니티 사이트에 기본적으로 사전 연결된 기능 이외의 다른 기능들이 없는 간단한 커뮤니티 사이트를 만들기 위해 [Page 함수](functions.md#page-function)만 포함된 새 커뮤니티 사이트 템플릿을 만든다는 것입니다.

### 새 사이트 템플릿 만들기 {#create-new-site-template}

시작하려면 간단한 [커뮤니티 사이트 템플릿](sites.md)을 만듭니다.

작성자 인스턴스의 전역 탐색에서 **[!UICONTROL 도구]** > **[!UICONTROL 커뮤니티]** > **[!UICONTROL 사이트 템플릿]**&#x200B;을 선택합니다.

![create-site-template](assets/create-site-template1.png)

* 선택 `Create button`
* 기본 정보

   * `Name`:단일 페이지 템플릿
   * `Description`:단일 페이지 함수로 구성된 템플릿입니다.
   * 선택 `Enabled`

![site-template-editor](assets/site-template-editor.png)

* 구조

   * `Page` 함수를 템플릿 빌더로 드래그합니다.
   * 구성 함수 세부 정보에 대해 다음을 입력합니다.

      * `Title`:단일 페이지
      * `URL`: 페이지

![site-template-editor-structure](assets/site-template-editor1.png)

* 구성에 대해 **`Save`**&#x200B;을 선택합니다.
* 사이트 템플릿의 **`Save`**&#x200B;을 선택합니다.

### 새 커뮤니티 사이트 만들기 {#create-new-community-site}

이제 간단한 사이트 템플릿을 기반으로 새로운 커뮤니티 사이트를 만들 수 있습니다.

사이트 템플릿을 만든 후 전역 탐색에서 **[!UICONTROL 커뮤니티 > 사이트]**&#x200B;를 선택합니다.

![create-community-site](assets/create-community-site1.png)

* **`Create`** 아이콘 선택

* 단계 `1 - Site Template`

   * `Title`:간단한 커뮤니티 사이트
   * `Description`:하나의 페이지로 구성된 실험용 커뮤니티 사이트.
   * `Community Site Root: (leave blank)`
   * `Community Site Base Language: English`
   * `Name`:sample

      * url = http://localhost:4502/content/sites/sample

      * `Template`:선택  `Single Page Template`

      ![create-community-site-template](assets/create-community-site-template.png)


* 선택 `Next`
* 단계 `2 - Design`

   * 원하는 디자인 선택

* 선택 `Next`
* 선택 `Next`

   (모든 기본 설정 허용)

* 선택 `Create`

   ![create-community-site](assets/create-community-site.png)

## 사이트 {#publish-the-site} 게시

![게시 사이트](assets/publish-site.png)

[커뮤니티 사이트 콘솔](sites-console.md)에서 사이트를 게시할 게시 아이콘을 기본적으로 http://localhost:4503으로 선택합니다.

## 편집 모드 {#open-the-site-on-author-in-edit-mode}에서 작성자의 사이트를 엽니다.

![개방형 사이트](assets/open-site.png)

사이트 열기 아이콘을 선택하여 편집 모드에서 사이트를 봅니다.

URL은 [http://localhost:4502/editor.html/content/sites/sample/en.html](http://localhost:4502/editor.html/content/sites/sample/en.html)입니다.

![author-site](assets/author-site.png)

간단한 홈 페이지에서 커뮤니티 기능 및 템플릿을 통해 사전에 연결된 내용을 확인하고 커뮤니티 구성 요소 추가 및 구성을 재생해 볼 수 있습니다.

## 게시 시 사이트 보기 {#view-site-on-publish}

페이지를 게시한 후 [게시 인스턴스](http://localhost:4503/content/sites/sample/en.html)에서 페이지를 열어 익명 사이트 방문자, 로그인된 구성원 또는 관리자로 기능을 실험합니다. 관리자가 로그인하지 않으면 작성 환경에 표시되는 관리 링크가 게시 환경에 나타나지 않습니다.
