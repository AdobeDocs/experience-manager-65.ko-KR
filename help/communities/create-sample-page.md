---
title: 샘플 페이지 만들기
description: 간단한 커뮤니티 사이트를 만드는 데 도움이 되는 페이지 기능만 포함하는 커뮤니티 사이트 템플릿을 만드는 방법을 알아봅니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: developing
exl-id: d66fc1ff-a669-4a2c-b45a-093060facd97
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---

# 샘플 페이지 만들기 {#create-a-sample-page}

AEM 6.1 Communities에서 샘플 페이지를 만드는 가장 쉬운 방법은 페이지 함수로 구성된 간단한 커뮤니티 사이트를 만드는 것입니다.

여기에는 [작성을 위해 구성 요소를 활성화](basics.md#accessing-communities-components)할 수 있도록 parsys 구성 요소가 포함됩니다.

샘플 구성 요소로 탐색하는 또 다른 옵션은 [커뮤니티 구성 요소 안내서](components-guide.md)에 있는 기능을 사용하는 것입니다.

## 커뮤니티 사이트 만들기 {#create-a-community-site}

이는 [AEM Communities 시작](getting-started.md)에 설명된 사이트를 만드는 것과 비슷합니다.

이 자습서에서는 간단한 커뮤니티 사이트를 만들 수 있도록 [Page 함수](functions.md#page-function)만 포함하는 커뮤니티 사이트 템플릿을 만듭니다. 이 작업은 다른 기능(모든 커뮤니티 사이트에 기본 제공되는 사전 연결된 기능 제외)에서 무료로 수행됩니다.

### 새 사이트 템플릿 만들기 {#create-new-site-template}

시작하려면 간단한 [커뮤니티 사이트 템플릿](sites.md)을 만드십시오.

작성자 인스턴스의 전역 탐색에서 **[!UICONTROL 도구]** > **[!UICONTROL 커뮤니티]** > **[!UICONTROL 사이트 템플릿]**&#x200B;을 선택합니다.

![사이트 템플릿 만들기](assets/create-site-template1.png)

* `Create button` 선택
* 기본 정보

   * `Name`: 단일 페이지 템플릿
   * `Description`: 단일 페이지 함수로 구성된 템플릿입니다.
   * `Enabled` 선택

![site-template-editor](assets/site-template-editor.png)

* 구조

   * `Page` 함수를 템플릿 빌더로 끌어서 놓습니다.
   * 구성 기능 세부 사항에 대해 다음을 입력합니다.

      * `Title`: 단일 페이지
      * `URL`: 페이지

![site-template-editor-structure](assets/site-template-editor1.png)

* 구성에 대해 **`Save`** 선택
* 사이트 서식 파일에 대해 **`Save`** 선택

### 새 커뮤니티 사이트 만들기 {#create-new-community-site}

이제 간단한 사이트 템플릿을 기반으로 커뮤니티 사이트를 만듭니다.

사이트 템플릿을 만든 후 전역 탐색에서 **[!UICONTROL 커뮤니티 > 사이트]**&#x200B;를 선택합니다.

![커뮤니티 사이트 만들기](assets/create-community-site1.png)

* **`Create`** 아이콘 선택

* `1 - Site Template`단계

   * `Title`: 단순 커뮤니티 사이트
   * `Description`: 실험을 위한 단일 페이지로 구성된 커뮤니티 사이트입니다.
   * `Community Site Root: (leave blank)`
   * `Community Site Base Language: English`
   * `Name`: 샘플

      * url = http://localhost:4502/content/sites/sample

      * `Template`: `Single Page Template` 선택

     ![create-community-site-template](assets/create-community-site-template.png)

* `Next` 선택
* `2 - Design`단계

   * 원하는 디자인 선택

* `Next` 선택
* `Next` 선택

  (모든 기본 설정 적용)

* `Create` 선택

  ![커뮤니티 사이트 만들기](assets/create-community-site.png)

## 사이트 Publish {#publish-the-site}

![publish-site](assets/publish-site.png)

[커뮤니티 사이트 콘솔](sites-console.md)에서 사이트를 게시할 게시 아이콘을 선택합니다. 기본적으로 http://localhost:4503입니다.

## 편집 모드로 작성자의 사이트 열기 {#open-the-site-on-author-in-edit-mode}

![사이트 열기](assets/open-site.png)

편집 모드에서 사이트를 볼 수 있도록 사이트 열기 아이콘을 선택합니다.

URL은 [http://localhost:4502/editor.html/content/sites/sample/en.html](http://localhost:4502/editor.html/content/sites/sample/en.html)입니다.

![author-site](assets/author-site.png)

간단한 홈 페이지에서는 커뮤니티 기능과 템플릿을 통해 미리 배선된 내용을 확인하고 커뮤니티 구성 요소를 추가 및 구성하는 작업을 수행할 수 있습니다.

## Publish에서 사이트 보기 {#view-site-on-publish}

페이지를 게시한 후 [게시 인스턴스](http://localhost:4503/content/sites/sample/en.html)에서 페이지를 열어 익명 사이트 방문자, 로그인한 구성원 또는 관리자의 기능을 실험해 보십시오. 작성 환경에 표시되는 관리 링크는 관리자가 로그인하지 않는 한 게시 환경에 표시되지 않습니다.
