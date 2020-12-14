---
title: SPA 소개 및 연습
seo-title: SPA 소개 및 연습
description: 이 문서에서는 SPA의 개념을 소개하고 기본적인 SPA 응용 프로그램을 저작하기 위해 사용하며 기본 AEM SPA Editor와 관련된 방식을 설명합니다.
seo-description: 이 문서에서는 SPA의 개념을 소개하고 기본적인 SPA 응용 프로그램을 저작하기 위해 사용하며 기본 AEM SPA Editor와 관련된 방식을 설명합니다.
uuid: 4b0a9e53-3892-4d60-8bd3-7ff740d2f137
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 0478afcb-b029-4ce6-b3e6-cee4bb5408ce
docset: aem65
translation-type: tm+mt
source-git-commit: 80b8571bf745b9e7d22d7d858cff9c62e9f8ed1e
workflow-type: tm+mt
source-wordcount: '2000'
ht-degree: 4%

---


# SPA 소개 및 연습{#spa-introduction-and-walkthrough}

단일 페이지 애플리케이션(SPA)을 통해 웹 사이트 사용자에게 매력적인 경험을 제공할 수 있습니다. 개발자는 SPA 프레임워크을 사용하여 사이트를 구축하고자 하며, 작성자는 이러한 프레임워크를 사용하여 구축된 사이트에서 AEM의 컨텐츠를 매끄럽게 편집하고자 합니다.

SPA Editor는 AEM 내에서 SPA을 지원하는 포괄적인 솔루션을 제공합니다. 이 문서에서는 저작에 기본 SPA 응용 프로그램을 사용하는 과정을 소개하고 기본 AEM SPA 편집기와 관련된 방법을 설명합니다.

>[!NOTE]
>
>SPA 편집기는 SPA 프레임워크 기반의 클라이언트측 렌더링(예: 반응형 또는 각도)이 필요한 프로젝트에 권장되는 솔루션입니다.

## 소개 {#introduction}

### 아티클 목표 {#article-objective}

이 문서에서는 간단한 SPA 애플리케이션을 사용하여 기본적인 컨텐츠 편집을 시연함으로써 SPA 편집기의 연습을 통해 독자를 안내하기 전에 SPA의 기본 개념을 설명합니다. 그런 다음 페이지 구성과 SPA 응용 프로그램이 AEM SPA Editor와 관련되고 상호 작용하는 방법을 자세히 다룹니다.

이 소개 및 연습의 목적은 AEM 개발자에게 SPA이 연관성 있는 이유,가 일반적으로 작동하는 방식, AEM SPA 편집기에서 SPA을 처리하는 방법 및 표준 AEM 애플리케이션과 어떻게 다른지 시연하는 것입니다.

이 연습은 표준 AEM 기능과 샘플 We.Retail Journal 앱을 기반으로 합니다. 다음 요구 사항을 충족해야 합니다.

* [AEM 버전 6.4(서비스 팩 2 이상)](/help/release-notes/sp-release-notes.md)
* [여기에서 GitHub에 있는 샘플 We.Retail Journal 앱을 설치합니다.](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal)

>[!CAUTION]
>
>이 문서에서는 데모용으로만 [We.Retail 저널 앱](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal)을 사용합니다. 어떤 프로젝트 작업에도 사용되어서는 안 됩니다.
>
>모든 AEM 프로젝트는 React 또는 Angular를 사용하여 SPA 프로젝트를 지원하고 SPA SDK를 활용하는 [AEM Project Tranype](https://docs.adobe.com/content/help/ko-KR/experience-manager-core-components/using/developing/archetype/overview.html)을 활용해야 합니다.

### SPA 소개{#what-is-a-spa}

단일 페이지 애플리케이션(SPA)은 클라이언트 측에서 렌더링되고 주로 Javascript를 기반으로 하며 데이터를 로드하고 페이지를 동적으로 업데이트하는 Ajax 호출에 의존한다는 점에서 일반 페이지와 다릅니다. 대부분의 또는 모든 컨텐츠는 페이지와의 사용자 상호 작용에 따라 필요에 따라 비동기적으로 로드된 추가 리소스를 사용하여 단일 페이지를 로드할 때 한 번 검색됩니다.

이를 통해 페이지 새로 고침이 필요하지 않으며, 매끄럽고 빠르며 기본 앱 경험과 같은 경험을 사용자에게 제공합니다.

SPA Editor를 사용하면 프런트 엔드 개발자는 AEM 사이트에 통합할 수 있는 SPA을 제작할 수 있으므로 컨텐츠 작성자는 다른 AEM 컨텐츠처럼 손쉽게 SPA 컨텐츠를 편집할 수 있습니다.

### SPA을 사용해야 하는 이유{#why-a-spa}

SPA은 기본 애플리케이션과 마찬가지로 빨라지고 유연하며 보다 매력적인 경험을 제공함으로써 웹 페이지 방문자뿐만 아니라 SPA 작업 방식의 특성상 마케터와 개발자에게 매력적인 경험을 제공합니다.

![screen_shot_2018-08-20at135550](assets/screen_shot_2018-08-20at135550.png)

**방문자 수**

* 방문자는 컨텐츠와 상호 작용할 때 원초적인 경험을 원합니다.
* 페이지가 빠르게 전환할수록 더 많은 전환이 발생한다는 명확한 데이터가 있습니다.

**마케터**

* 마케터는 방문자가 컨텐츠에 완전히 매료되도록 유도할 수 있는 토착적이고 풍부한 경험을 제공하고자 합니다.
* 개인화를 통해 이러한 경험을 보다 매력적으로 만들 수 있습니다.

**개발자**

* 개발자는 컨텐츠와 프레젠테이션에 대한 우려 사항을 명확하게 구분해야 합니다.
* 깔끔한 분리를 통해 시스템은 확장 가능하고 독립적인 프런트 엔드 개발을 할 수 있습니다.

### SPA 작동 방식{#how-does-a-spa-work}

SPA의 기본 아이디어는 SPA이 기본 애플리케이션의 응답성에 접근하도록 서버 호출로 인한 지연을 최소화하기 위해 서버에 대한 호출과 의존도를 줄이는 것입니다.

기존의 순차적 웹 페이지에서는 바로 페이지에 필요한 데이터만 로드됩니다. 즉, 방문자가 다른 페이지로 이동할 때 추가 리소스를 위해 서버가 호출됩니다. 방문자가 페이지의 요소와 상호 작용하므로 추가 호출이 필요할 수 있습니다. 페이지가 방문자의 요청을 따라잡아야 하므로 이러한 여러 개의 호출로 인해 지연이나 지연이 생길 수 있습니다.

![screen_shot_2018-08-20at140449](assets/screen_shot_2018-08-20at140449.png)

보다 유동적인 경험을 위해 SPA은 방문자가 모바일, 기본 앱에서 기대하는 대로 방문자를 처음 로드할 때 필요한 모든 데이터를 로드합니다. 처음에는 시간이 조금 더 걸릴 수 있지만 이 경우 추가 서버 호출을 수행할 필요가 없습니다.

클라이언트 쪽에서 렌더링하면 페이지 요소는 빠르게 반응하며 방문자가 페이지와의 상호 작용은 즉시 수행됩니다. 필요한 추가 데이터는 페이지 속도를 최대화하기 위해 비동기식으로 호출됩니다.

>[!NOTE]
>
>AEM에서 SPA이 작동하는 방법에 대한 기술적인 자세한 내용은 AEM에서 SPA 시작[ 문서를 참조하십시오.](/help/sites-developing/spa-getting-started-react.md)
>
>SPA 편집기의 디자인, 아키텍처 및 기술 작업 과정에 대한 자세한 내용은 [SPA 편집기 개요](/help/sites-developing/spa-overview.md) 문서를 참조하십시오.

## SPA {#content-editing-experience-with-spa}의 컨텐츠 편집 경험

AEM SPA Editor를 활용할 수 있도록 SPA을 구축하면 컨텐츠 작성자는 컨텐츠를 편집하고 제작할 때 아무런 차이도 표시되지 않습니다. 일반적인 AEM 기능을 사용할 수 있으며 작성자의 워크플로우를 변경할 필요가 없습니다.

>[!NOTE]
>
>이 연습은 표준 AEM 기능과 샘플 We.Retail Journal 앱을 기반으로 합니다. 다음 요구 사항을 충족해야 합니다.
>
>* [AEM 버전 6.4(서비스 팩 2)](/help/release-notes/sp-release-notes.md)
>* [여기에서 GitHub에 있는 샘플 We.Retail Journal 앱을 설치합니다.](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal)

>



1. AEM에서 We.Retail Journal 앱을 편집합니다.

   `https://localhost:4502/editor.html/content/we-retail-journal/react.html`

   ![screen_shot_2018-06-07at142533](assets/screen_shot_2018-06-07at142533.png)

1. 제목 구성 요소를 선택하면 다른 구성 요소에 대해 도구 모음이 표시됩니다. **편집**&#x200B;을 선택하십시오.

   ![screen_shot_2018-06-07at142937](assets/screen_shot_2018-06-07at142937.png)

1. AEM 내에서 컨텐츠를 정상적으로 편집하고 변경 사항이 지속됨을 확인합니다.

   ![screen_shot_2018-06-07at143419](assets/screen_shot_2018-06-07at143419.png)

   >[!NOTE]
   >즉석 텍스트 편집기 및 SPA에 대한 자세한 내용은 [SPA 편집기 개요](spa-overview.md#requirements-limitations)를 참조하십시오.

1. 자산 브라우저를 사용하여 새 이미지를 이미지 구성 요소로 드래그하여 놓습니다.

   ![screen_shot_2018-06-07at143530](assets/screen_shot_2018-06-07at143530.png)

1. 변경 사항이 지속됩니다.

   ![screen_shot_2018-06-07at143732](assets/screen_shot_2018-06-07at143732.png)

페이지에서 추가 구성 요소를 드래그 앤 드롭하거나, 구성 요소를 다시 정렬하고, 레이아웃을 수정하는 것과 같은 추가 제작 도구는 SPA이 아닌 다른 응용 프로그램에서처럼 지원됩니다.

>[!NOTE]
>
>SPA 편집기는 응용 프로그램의 DOM을 수정하지 않습니다. SPA 자체도 DOM을 책임집니다.
>
>이 작동 방식을 보려면 이 문서 [SPA Apps 및 AEM SPA Editor](/help/sites-developing/spa-walkthrough.md#spa-apps-and-the-aem-spa-editor)의 다음 섹션으로 계속하십시오.

## SPA 앱 및 AEM SPA 편집기 {#spa-apps-and-the-aem-spa-editor}

SPA이 최종 사용자에게 동작하고 SPA 페이지를 검사하는 방법을 통해 AEM에서 SPA 편집기와 SAP 앱이 작동하는 방식을 더 잘 이해할 수 있습니다.

### SPA 응용 프로그램 사용 {#using-an-spa-application}

1. We.Retail 저널 응용 프로그램을 게시 서버에 로드하거나 페이지 편집기의 **페이지 정보** 메뉴에서 **게시됨으로 보기** 옵션을 사용하여 로드합니다.

   `/content/we-retail-journal/react.html`

   ![screen_shot_2018-06-08at102650](assets/screen_shot_2018-06-08at102650.png)

   하위 페이지 탐색, 날씨 위젯 및 아티클로의 페이지 구조를 확인합니다.

1. 메뉴를 사용하여 하위 페이지로 이동하고 새로 고칠 필요 없이 페이지가 즉시 로드되는지 확인합니다.

   ![screen_shot_2018-06-08at102815](assets/screen_shot_2018-06-08at102815.png)

1. 브라우저에서 내장된 개발자 도구를 열고 하위 페이지를 탐색할 때 네트워크 활동을 모니터링할 수 있습니다.

   ![screen_shot_2018-06-08at103922](assets/screen_shot_2018-06-08at103922.png)

   앱에서 페이지로 이동할 때 트래픽이 거의 없습니다. 페이지가 다시 로드되지 않고 새 이미지만 요청됩니다.

   SPA은 클라이언트 측에서 완전히 컨텐츠와 라우팅을 관리합니다.

하위 페이지를 탐색할 때 페이지가 다시 로드되지 않으면 어떻게 로드됩니까?

다음 섹션인 [SPA 응용 프로그램 로드](/help/sites-developing/spa-walkthrough.md#loading-an-spa-application)에서는 SPA을 로드하는 역학 및 컨텐츠를 동기적으로 및 비동기적으로 로드하는 방법에 대해 자세히 알아봅니다.

### SPA 응용 프로그램 로드 중 {#loading-an-spa-application}

1. 아직 로드되지 않은 경우, We.Retail 저널 애플리케이션을 게시 서버에 로드하거나 페이지 편집기의 **페이지 정보** 메뉴에서 **게시됨으로 보기** 옵션을 사용하여 로드합니다.

   `/content/we-retail-journal/react.html`

   ![screen_shot_2018-06-07at144736](assets/screen_shot_2018-06-07at144736.png)

1. 브라우저의 내장된 도구를 사용하여 페이지의 소스를 봅니다.
1. 소스의 내용은 극히 제한되어 있습니다.

   ```
   <!DOCTYPE HTML>
   <html lang="en-CH">
       <head>
       <meta charset="UTF-8">
       <title>We.Retail Journal</title>
   
       <meta name="template" content="we-retail-react-template"/>
   
   <link rel="stylesheet" href="/etc.clientlibs/we-retail-journal/react/clientlibs/we-retail-journal-react.css" type="text/css">
   
   <link rel="stylesheet" href="/libs/wcm/foundation/components/page/responsive.css" type="text/css">
   
   </head>
       <body class="page basicpage">
   
   <div id="page"></div>
   
   <script type="text/javascript" src="/etc.clientlibs/we-retail-journal/react/clientlibs/we-retail-journal-react.js"></script>
   
       </body>
   </html>
   ```

   페이지에 본문 내에 내용이 없습니다. 이것은 주로 스타일 시트 및 React 스크립트( `we-retail-journal-react.js`)에 대한 호출로 구성됩니다.

   이 React 스크립트는 이 애플리케이션의 기본 드라이버이며 모든 컨텐츠를 렌더링하는 책임을 집니다.

1. 브라우저에 내장된 툴을 사용하여 페이지를 검사할 수 있습니다. 완전히 로드된 DOM의 컨텐츠를 확인합니다.

   ![screen_shot_2018-06-07at151848](assets/screen_shot_2018-06-07at151848.png)

1. 관리자의 네트워크 탭으로 전환하고 페이지를 다시 로드합니다.

   이미지 요청을 무시하고 페이지에 대해 로드된 기본 리소스는 페이지 자체, CSS, React Javascript, 해당 종속성 및 페이지에 대한 JSON 데이터입니다.

   ![screen_shot_2018-06-07at152155](assets/screen_shot_2018-06-07at152155.png)

1. 새 탭에서 `react.model.json`을 로드합니다.

   `/content/we-retail-journal/react.model.json`

   ![screen_shot_2018-06-07at152636](assets/screen_shot_2018-06-07at152636.png)

   AEM SPA 편집기는 [AEM Content Services](/help/assets/content-fragments/content-fragments.md)를 활용하여 페이지의 전체 컨텐츠를 JSON 모델로 전달합니다.

   Sling Models는 특정 인터페이스를 구현하여 SPA에 필요한 정보를 제공합니다. JSON 데이터 배달은 각 구성 요소(페이지, 단락, 구성 요소 등)에 아래쪽으로 위임됩니다.

   각 구성 요소는 표시되는 내용과 렌더링되는 방식을 선택합니다(HTL과 함께 서버측 또는 반응과 클라이언트측). 물론 이 문서는 React를 사용한 클라이언트측 렌더링에 중점을 둡니다.

1. 또한 모델은 동기적으로 로드되도록 페이지를 그룹화하여 필요한 페이지 다시 로드 수를 줄일 수도 있습니다.

   We.Retail 저널의 예에서 방문자는 일반적으로 모든 페이지를 방문하므로 `home`, `blog` 및 `aboutus` 페이지가 동기식으로 로드됩니다. 그러나 방문자가 페이지를 방문할 가능성이 적기 때문에 `weather` 페이지가 비동기식으로 로드됩니다.

   이 동작은 필수가 아니며 완전히 정의할 수 있습니다.

   ![screen_shot_2018-06-07at153945](assets/screen_shot_2018-06-07at153945.png)

1. 동작의 이러한 차이를 보려면 페이지를 다시 로드하고 관리자의 네트워크 활동을 지웁니다. 페이지 메뉴에서 블로그 및 Adobe 정보 페이지로 이동하여 보고된 네트워크 활동이 없음을 확인합니다.

   날씨 페이지로 이동하여 `weather.model.json`이(가) 비동기적으로 호출되는지 확인합니다.

   ![screen_shot_2018-06-07at155738](assets/screen_shot_2018-06-07at155738.png)

### SPA 편집기와의 상호 작용 {#interaction-with-the-spa-editor}

샘플 We.Retail 저널 애플리케이션을 사용하면 앱이 어떻게 동작하고 게시 시 로드되는지 명확히 알 수 있으며, JSON 컨텐츠 전달을 위한 컨텐츠 서비스와 리소스 비동기적 로딩을 활용할 수 있습니다.

또한 컨텐츠 작성자의 경우 SPA 편집기를 사용하여 컨텐츠를 만드는 것은 AEM 내에서 매끄럽게 이루어집니다.

다음 섹션에서는 SPA Editor가 SPA 구성 요소 내의 구성 요소를 AEM 구성 요소와 연계하여 이러한 매끄러운 편집 환경을 제공할 수 있도록 하는 계약을 살펴봅니다.

1. 편집기에서 We.Retail 저널 애플리케이션을 로드하고 **미리 보기** 모드로 전환합니다.

   `https://localhost:4502/editor.html/content/we-retail-journal/react.html`

1. 브라우저의 내장된 개발자 도구를 사용하여 페이지의 컨텐츠를 검사합니다. 선택 도구를 사용하여 페이지에서 편집 가능한 구성 요소를 선택하고 요소 세부 사항을 봅니다.

   구성 요소에는 새 데이터 속성 `data-cq-data-path`이 있습니다.

   ![screen_shot_2018-06-08at095124](assets/screen_shot_2018-06-08at095124.png)

   예

   `data-cq-data-path="root/responsivegrid/paragraph_1`

   이 경로를 사용하면 각 구성 요소의 편집 컨텍스트 구성 객체를 검색하고 연결할 수 있습니다.

   편집자가 SPA 내에서 이 구성 요소를 편집 가능한 구성 요소로 인식하는 데 필요한 유일한 마크업 속성입니다. 이 속성을 기반으로 SPA 편집기는 구성 요소와 연결된 편집 가능한 구성을 판단하여 올바른 프레임, 도구 모음 등을 확인합니다. 가 로드되었습니다.

   자리 표시자를 표시하거나 자산 드래그하여 놓기 기능을 위해 일부 특정 클래스 이름도 추가되었습니다.

   >[!NOTE]
   >
   >이것은 AEM의 서버 쪽 렌더링된 페이지에서 편집 가능한 각 구성 요소에 대해 `cq` 요소가 삽입되는 동작의 변화입니다.
   >
   >
   >SPA에서 이 방법을 사용하면 사용자 정의 요소를 주입하거나 추가 데이터 속성만 의존하지 않아도 되므로 프런트 엔드 개발자에게 마크업이 더 간편해집니다.

## 다음 단계 {#next-steps}

이제 AEM의 SPA 편집 경험과 SPA이 SPA 편집기와 어떻게 관련이 있는지 이해했다면 SPA의 구축 방법을 보다 심도 있게 살펴볼 수 있습니다.

* [AEM에서 SPA 시작하기](/help/sites-developing/spa-getting-started-react.md) 는 AEM에서 SPA 편집기로 작동하는 기본 SPA을 빌드하는 방법을 보여줍니다
* [SPA ](/help/sites-developing/spa-overview.md) Editor Overview를 통해 AEM과 SPA 간의 통신 모델에 대해 더 자세히 살펴봅니다.
* [AEM용 SPA 개발](/help/sites-developing/spa-architecture.md) 은 AEM용 SPA을 개발하기 위해 프런트 엔드 개발자의 참여를 유도하는 방법뿐만 아니라 SPA과 AEM 아키텍처가 어떻게 상호작용하는지를 설명합니다.
