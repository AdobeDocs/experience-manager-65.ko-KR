---
title: 샘플 페이지 만들기
seo-title: Create a Sample Page
description: 샘플 커뮤니티 사이트 만들기
seo-description: Create a Sample community site
uuid: 04a8f027-b7d8-493a-a9bd-5c4a6715d754
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: developing
discoiquuid: a03145f7-6697-4797-b73e-6f8d241ce469
exl-id: d66fc1ff-a669-4a2c-b45a-093060facd97
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 2%

---

# 샘플 페이지 만들기 {#create-a-sample-page}

AEM 6.1 Communities에서 샘플 페이지를 만드는 가장 쉬운 방법은 페이지 기능만으로 구성된 간단한 커뮤니티 사이트를 만드는 것입니다.

여기에는 parsys 구성 요소가 포함되므로 다음 작업을 수행할 수 있습니다 [작성을 위한 구성 요소 활성화](basics.md#accessing-communities-components).

샘플 구성 요소를 사용하여 탐색하기 위한 또 다른 옵션은 [커뮤니티 구성 요소 안내서](components-guide.md).

## 커뮤니티 사이트 만들기 {#create-a-community-site}

이는 에 설명된 새 사이트를 만드는 것과 매우 유사합니다 [AEM Communities 시작하기](getting-started.md).

가장 큰 차이점은 이 자습서에서는 만 포함된 새 커뮤니티 사이트 템플릿을 만들 것이라는 것입니다 [페이지 함수](functions.md#page-function) 모든 커뮤니티 사이트에 대해 기본적으로 유선 전 기능 이외의 다른 기능이 없는 간단한 커뮤니티 사이트를 만들 수 있습니다.

### 새 사이트 템플릿 만들기 {#create-new-site-template}

시작하려면 간단한 [커뮤니티 사이트 템플릿](sites.md).

작성자 인스턴스의 전역 탐색에서 를 선택합니다 **[!UICONTROL 도구]** > **[!UICONTROL 커뮤니티]** > **[!UICONTROL 사이트 템플릿]**.

![create-site-template](assets/create-site-template1.png)

* 선택 `Create button`
* 기본 정보

   * `Name`: 단일 페이지 템플릿
   * `Description`: 단일 페이지 함수로 구성된 템플릿.
   * 선택 `Enabled`

![site-template-editor](assets/site-template-editor.png)

* 구조

   * 드래그 `Page` 함수 내에 있어야 합니다
   * 구성 함수 세부 정보에 대해 다음을 입력합니다.

      * `Title`: 단일 페이지
      * `URL`: 페이지

![site-template-editor-structure](assets/site-template-editor1.png)

* 선택 **`Save`** 구성
* 선택 **`Save`** 사이트 템플릿의 경우

### 새 커뮤니티 사이트 만들기 {#create-new-community-site}

이제 단순 사이트 템플릿을 기반으로 새 커뮤니티 사이트를 만듭니다.

사이트 템플릿을 만든 후 전역 탐색에서 를 선택합니다 **[!UICONTROL 커뮤니티 > 사이트]**.

![create-community-site](assets/create-community-site1.png)

* 선택 **`Create`** 아이콘

* 단계 `1 - Site Template`

   * `Title`: 단순 커뮤니티 사이트
   * `Description`: 실험용 단일 페이지로 구성된 커뮤니티 사이트.
   * `Community Site Root: (leave blank)`
   * `Community Site Base Language: English`
   * `Name`: 샘플

      * url = http://localhost:4502/content/sites/sample

      * `Template`: 선택 `Single Page Template`

      ![create-community-site-template](assets/create-community-site-template.png)


* 선택 `Next`
* 단계 `2 - Design`

   * 디자인 선택

* 선택 `Next`
* 선택 `Next`

   (모든 기본 설정 적용)

* 선택 `Create`

   ![create-community-site](assets/create-community-site.png)

## 사이트 게시 {#publish-the-site}

![publish-site](assets/publish-site.png)

에서 [커뮤니티 사이트 콘솔](sites-console.md)를 클릭하고 게시 아이콘을 선택하여 사이트를 기본적으로 http://localhost:4503으로 게시합니다.

## 편집 모드에서 작성자에 있는 사이트 열기 {#open-the-site-on-author-in-edit-mode}

![오픈 사이트](assets/open-site.png)

사이트 열기 아이콘을 선택하여 편집 모드로 사이트를 확인합니다.

URL은 [http://localhost:4502/editor.html/content/sites/sample/en.html](http://localhost:4502/editor.html/content/sites/sample/en.html)

![작성자 사이트](assets/author-site.png)

간단한 홈 페이지에서는 커뮤니티 기능 및 템플릿을 통해 미리 연결된 항목을 확인하고 커뮤니티 구성 요소 추가 및 구성으로 재생할 수 있습니다.

## 게시에서 사이트 보기 {#view-site-on-publish}

페이지를 게시한 후 페이지에서 페이지를 엽니다. [게시 인스턴스](http://localhost:4503/content/sites/sample/en.html) 익명 사이트 방문자, 로그인 구성원 또는 관리자로 기능을 실험하기 위해 작성자 환경에 표시되는 관리 링크는 관리자가 로그인하지 않는 한 게시 환경에 표시되지 않습니다.
