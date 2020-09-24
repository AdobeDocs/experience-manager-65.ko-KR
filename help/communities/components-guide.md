---
title: 커뮤니티 구성 요소 안내서
seo-title: 커뮤니티 구성 요소 안내서
description: 소셜 구성 요소 프레임워크(SCF)를 시작하기 위한 대화형 개발 도구
seo-description: 소셜 구성 요소 프레임워크(SCF)를 시작하기 위한 대화형 개발 도구
uuid: 120e56d1-b93c-4f92-bab4-6bb5e40e0ddf
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a777a3f1-b39f-4d90-b9b6-02d3e321a86f
translation-type: tm+mt
source-git-commit: 3da113e88784def54e0a94e280bf1a965de015ed
workflow-type: tm+mt
source-wordcount: '1203'
ht-degree: 2%

---


# 커뮤니티 구성 요소 안내서  {#community-components-guide}

커뮤니티 구성 요소 안내서는 [소셜 구성 요소 프레임워크(SCF)에 대한 대화형 개발 도구입니다](scf.md). 사용 가능한 AEM Communities 구성 요소 또는 여러 구성 요소로 구성된 더 복잡한 기능 목록을 제공합니다.

이 가이드는 각 구성 요소에 대한 기본 정보와 함께 SCF 구성 요소/기능의 작동 방식과 구성 또는 사용자 정의 방법을 실험해 볼 수 있도록 해줍니다.

각 구성 요소와 관련된 개발 필수 요소에 대한 자세한 내용은 [Feature 및 Component Essentials를 참조하십시오](essentials.md).

## 시작하기 {#getting-started}

이 안내서는 작성자(localhost:4502) 및 게시(localhost:4503) 인스턴스의 개발 설치 시 사용하기 위한 것입니다.

커뮤니티 구성 요소 사이트는

* [https://&lt;server>:&lt;port>/content/community-components/en.html](http://localhost:4502/content/community-components/en.html)

Communities 구성 요소와의 상호 작용은 다음과 같은 경우에 따라 달라집니다.

* 서버(작성자 또는 게시)입니다.
* 사이트 방문자의 로그인 여부.
* 로그인하면 멤버에 할당된 권한입니다.
* 기본 SRP, [JSRP가](jsrp.md)사용 중인지 여부

작성자의 경우 편집 모드로 전환하려면 서버 이름 뒤에 `editor.html` 또 `cf#` 는 첫 번째 경로 세그먼트로 삽입합니다.

* 표준 UI:

   [https://&lt;server>:&lt;port>/editor.html/content/community-components/en.html](http://localhost:4502/editor.html/content/community-components/en.html)

* 클래식 UI:

   [https://&lt;server>:&lt;port>/cf#/content/community-components/en.html](http://localhost:4502/cf#/content/community-components/en.html)

>[!NOTE]
>
>편집 모드에서 작성자의 경우 페이지의 링크가 활성화되지 않습니다.
>
>구성 요소 페이지로 이동하려면 먼저 미리 보기 모드를 선택하여 링크를 활성화합니다.
>
>구성 요소 페이지가 브라우저에 표시되면 구성 요소의 편집 대화 상자를 열려면 편집 모드로 돌아갑니다.
>
>일반 작성 정보는 페이지 작성에 대한 [빠른 안내서를 참조하십시오](../../help/sites-authoring/qg-page-authoring.md).
>
>AEM에 익숙하지 않은 경우 [기본 처리에 대한 설명서를 참조하십시오](../../help/sites-authoring/basic-handling.md).


### 홈페이지 {#home-page}

안내서에서는 페이지 왼쪽에 있는 미리 보기 및 프로토타이핑에 사용할 수 있는 SCF 구성 요소 목록을 제공합니다.

편집 모드에서 작성자 인스턴스에서 보는 구성 요소 안내서:

![community-component1](assets/community-component1.png)

## 구성 요소 페이지 {#component-pages}

페이지의 왼쪽에 있는 목록에서 구성 요소를 선택합니다.

![community-component-pages](assets/community-component2.png)

안내서의 본문은 다음과 같습니다.

1. 제목:선택한 구성 요소의 이름
1. [클라이언트측 라이브러리](#client-side-libraries):하나 이상의 필수 카테고리 목록
1. [포함 가능](scf.md#add-or-include-a-communities-component):구성 요소를 동적으로 포함할 수 있는 경우, 작성 편집 모드에서 상태를 전환할 수 있습니다.

   * 추가된 경우 표시되는 텍스트는 다음과 같습니다.&quot;이 구성 요소는 해당 par 노드를 통해 포함됩니다.&quot;
   * 포함된 경우 표시되는 텍스트는 다음과 같습니다.&quot;이 구성 요소는 동적으로 포함됩니다.&quot;
   * 포함하지 않는 경우 텍스트가 표시되지 않습니다.

1. 샘플 구성 요소 또는 기능:구성 요소나 피쳐의 활성 인스턴스. 구성 요소의 경우 탭 섹션에 제공된 템플릿, CSS 및 데이터의 변경 사항으로 변경될 수 있습니다.

>[!NOTE]
>
>왼쪽에서 선택한 구성 요소는 브라우저 창이 너무 좁을 때 구성 요소 목록이 아니라 아래에 나타납니다.

### 작성자 상호 작용 {#author-interactions}

작성 인스턴스에서 안내서를 사용하는 경우 대화 상자를 열어 구성 요소를 구성할 수 있습니다. 개발자를 위한 정보는 설명서의 [구성 요소 및 기능 필수](essentials.md) 사항 섹션에서 제공되며 대화 상자 설정은 작성자를 위한 커뮤니티 구성 요소 [](author-communities.md) 섹션에 설명되어 있습니다.

커뮤니티 구성 요소 안내서의 경우 일부 구성 요소 대화 상자 설정은 포함 가능 [전환](scf.md#add-or-include-a-communities-component) 상태로 오버레이됩니다. 기존 리소스 또는 동적으로 포함된 리소스 간에 전환하려면 편집 모드에서 구성 요소와 포함 가능한 텍스트를 모두 선택하고 두 번 클릭하여 편집 대화 상자를 엽니다.

![community-component3](assets/community-component3.png)

템플릿 **탭** 아래에서

![community-component4](assets/community-component4.png)

* **sling:include로 하위 구성 요소 포함**

   선택 취소하면 구성 요소 가이드는 저장소의 기존 리소스(par 노드의 자식인 jcr 노드)를 사용합니다.

   * 표시되는 텍스트:&quot;이 구성 요소는 해당 par 노드를 통해 포함됩니다.&quot;

   이 확인란을 선택하면 구성 요소 안내서가 sling을 사용하여 하위 노드의 resourceType(존재하지 않는 리소스)의 구성 요소를 동적으로 포함합니다.

   * 표시되는 텍스트:&quot;이 구성 요소는 동적으로 포함됩니다.&quot;

   기본값은 선택 취소입니다.

### 게시 상호 작용 {#publish-interactions}

게시 인스턴스의 안내서를 사용하는 경우 구성 요소 및 기능을 사이트 방문자(로그인하지 않은 경우)로서 그리고 로그인할 때 다양한 권한이 있는 구성원으로 체험할 수 있습니다.

>[!NOTE]
>
>SRP의 기본값이 [JSRP로](jsrp.md)남아 있는 경우 게시 인스턴스에 입력된 UGC는 게시 *에만 표시되며 작성 인스턴스의* 중재 [콘솔에서는 표시되지](moderate-ugc.md) 않습니다.

## 클라이언트측 라이브러리 {#client-side-libraries}

각 구성 요소에 대해 나열된 클라이언트측 라이브러리(clientlibs)는 구성 요소를 페이지에 배치할 때 참조해야 *하는* 라이브러리입니다. clientlibs는 브라우저에서 구성 요소를 렌더링하는 데 사용되는 Javascript 및 CSS의 다운로드를 관리하고 최적화하는 방법을 제공합니다.

자세한 내용은 커뮤니티 구성 [요소용 Clientlibs를 참조하십시오](clientlibs.md).

## 가장 {#impersonation}

작성자 인스턴스에서 관리자 또는 개발자로 로그인하는 경우가 많습니다. 구성 요소가 다른 사용자로 로그인되어 있는 것을 경험하려면 가장 **** 단추 왼쪽에 있는 텍스트 상자를 사용하여 사용자 이름을 입력하거나 풀다운 목록에서 선택한 다음 단추를 클릭합니다. [되돌리기]를 클릭하여 로그아웃하고 가장을 종료합니다.

게시 인스턴스는 가장할 필요가 없습니다. [로그인/로그아웃] 링크를 사용하여 데모 사용자 [와 같은 다양한 사용자를 가장합니다](tutorials.md#demo-users).

## 사용자 정의 {#customization}

활성화되면 구성 요소의 템플릿, CSS 및 데이터를 일시적으로 수정하여 가능한 사용자 지정을 위한 각 SCF 구성 요소를 프로토타입을 작성할 수 있습니다.

### 사용자 정의 활성화 {#enabling-customization}

>[!NOTE]
>
>**이 도구는 읽기 전용입니다**. 템플릿, CSS 또는 데이터에 대한 편집 내용은 저장소에 저장되지 않습니다.

사용자 지정을 빠르게 테스트하려면 구성 요소 페이지의 컨텐츠 JCR 노드에 `scg:showIde`속성을 추가하고 true로 설정해야 합니다.

주석 구성 요소를 예로 사용하여 작성자 또는 게시 인스턴스에서 관리자 권한으로 로그인됨:

1. CRXDE Lite [찾아보기](../../help/sites-developing/developing-with-crxde-lite.md)

   예: [http://localhost:4503/crx/de](http://localhost:4503/crx/de)

1. 구성 요소의 노드 `jcr:content` 선택

   예, `/content/community-components/en/comments/jcr:content`

1. 속성 추가

   * **이름** `scg:showIde`
   * **유형** `String`
   * **값** `true`

1. 모두 **[!UICONTROL 저장 선택]**
1. 안내서에서 댓글 페이지 다시 로드

   [http://localhost:4503/content/community-components/en/comments.html](http://localhost:4503/content/community-components/en/comments.html)

1. 이제 템플릿, CSS 및 데이터를 위한 3개의 탭이 있습니다.

![community-component5](assets/community-component5.png)

![community-component6](assets/community-component6.png)

### 템플릿 탭 {#templates-tab}

템플릿 탭을 선택하여 구성 요소와 연관된 템플릿을 확인합니다.

템플릿 편집기를 사용하면 저장소의 구성 요소에 영향을 주지 않고 페이지 상단에 있는 샘플 구성 요소 인스턴스에 로컬 편집 내용을 컴파일하고 적용할 수 있습니다.

로컬 편집 시 컴파일을 실행하면 도트를 간격 안에 놓고 텍스트를 빨간색으로 표시하여 오류를 강조 표시합니다.

### CSS 탭 {#css-tab}

CSS 탭을 선택하여 구성 요소와 연관된 CSS를 확인합니다.

구성 요소가 여러 구성 요소를 합성한 경우 일부 CSS가 다른 구성 요소 중 하나에 나열될 수 있습니다.

CSS 편집기를 사용하면 CSS를 수정하여 페이지 상단의 샘플 구성 요소 인스턴스에 적용할 수 있습니다.

간격 내의 규칙 옆에 있는 을 클릭하여 해당 규칙을 사용하여 DOM의 부분을 강조하도록 규칙을 선택할 수 있습니다.

### 데이터 탭 {#data-tab}

데이터 탭을 선택하여 .social.json 끝점 데이터를 표시합니다. 이 데이터는 편집 가능하며 샘플 구성 요소 인스턴스에 적용됩니다.

구문 오류는 편집기에 강조 표시된 것뿐만 아니라 간격에도 표시될 수 있습니다.
