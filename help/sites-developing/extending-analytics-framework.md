---
title: Adobe Analytics 프레임워크 사용자 지정
seo-title: Customizing the Adobe Analytics Framework
description: Adobe Analytics 프레임워크 사용자 지정
seo-description: null
uuid: 444a29c2-3b4e-4d21-adc0-5f317ece2b77
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 11c0aac6-a7f6-4d6b-a080-b04643045a64
exl-id: ab0d4f2e-f761-4510-ba51-4a2dcea49601
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '1618'
ht-degree: 1%

---

# Adobe Analytics 프레임워크 사용자 지정{#customizing-the-adobe-analytics-framework}

Adobe Analytics 프레임워크은 Adobe Analytics으로 추적되는 정보를 결정합니다. 기본 프레임워크를 사용자 정의하려면 javascript를 사용하여 사용자 지정 추적을 추가하고, Adobe Analytics 플러그인을 통합하며, 추적에 사용되는 프레임워크 내에서 일반 설정을 변경합니다.

## 생성된 프레임워크 Javascript 정보 {#about-the-generated-javascript-for-frameworks}

페이지가 Adobe Analytics 프레임워크과 연결되어 있고 페이지에 다음이 포함되어 있는 경우 [analytics 모듈에 대한 참조](/help/sites-administering/adobeanalytics.md)를 입력하면 페이지에 대해 analytics.sitecatalyst.js 파일이 자동으로 생성됩니다.

페이지의 javascript는 `s_gi`개체(s_code.js Adobe Analytics 라이브러리가 정의하는)를 정의하고 해당 속성에 값을 지정합니다. 개체 인스턴스의 이름은 `s`. 이 섹션에 표시되는 코드 예제에서는 이 단원을 몇 가지 참조합니다 `s` 변수를 채우는 방법을 설명합니다.

다음 예제 코드는 analytics.sitecatalyst.js 파일의 코드와 유사합니다.

```
var s_account = "my_sitecatalyst_account";
var s = s_gi(s_account);
s.fpCookieDomainPeriods = "3";
s.currencyCode= 'USD';
s.trackInlineStats= true;
s.linkTrackVars= 'None';
s.charSet= 'UTF-8';
s.linkLeaveQueryString= false;
s.linkExternalFilters= '';
s.linkTrackEvents= 'None';
s.trackExternalLinks= true;
s.linkDownloadFileTypes= 'exe,zip,wav,mp3,mov,mpg,avi,wmv,doc,pdf,xls';
s.linkInternalFilters= 'javascript:,'+window.location.hostname;
s.trackDownloadLinks= true;

s.visitorNamespace = "mynamespace";
s.trackingServer = "xxxxxxx.net";
s.trackingServerSecure = "xxxxxxx.net";

/* Plugin Config */
/*
s.usePlugins=false;
function s_doPlugins(s) {
    //add your custom plugin code here
}
s.doPlugins=s_doPlugins;
*/
```

사용자 지정 Javascript 코드를 사용하여 프레임워크를 사용자 지정하는 경우 이 파일의 콘텐츠를 변경합니다.

## Adobe Analytics 속성 구성 {#configuring-adobe-analytics-properties}

Adobe Analytics 내에는 프레임워크에서 구성할 수 있는 사전 정의된 변수가 많이 있습니다. 다음 **charset**, **cookieLifetime**, **currencyCode** 및 **trackInlineStats** 변수는 **일반 Analytics 설정** 목록을 기본적으로 표시합니다.

![aa-22](assets/aa-22.png)

변수 이름 및 값을 목록에 추가할 수 있습니다. 이러한 사전 정의된 변수와 사용자가 추가하는 모든 변수는 페이지의 속성을 구성하는 데 사용됩니다 `s` analytics.sitecatalyst.js 파일의 객체입니다. 다음 예는 가 추가된 방법을 보여줍니다. `prop10` 값 속성 `CONSTANT` 는 javascript 코드에 들어 있습니다.

```
var s_account = "my_sitecatalyst_account";
var s = s_gi(s_account);
s.fpCookieDomainPeriods = "3";
s.currencyCode= 'USD';
s.trackInlineStats= true;
s.linkTrackVars= 'None';
s.charSet= 'UTF-8';
s.linkLeaveQueryString= false;
s.linkExternalFilters= '';
s.linkTrackEvents= 'None';
s.trackExternalLinks= true;
s.linkDownloadFileTypes= 'exe,zip,wav,mp3,mov,mpg,avi,wmv,doc,pdf,xls';
s.prop10= 'CONSTANT';
s.linkInternalFilters= 'javascript:,'+window.location.hostname;
s.trackDownloadLinks= true;

s.visitorNamespace = "mynamespace";
s.trackingServer = "xxxxxxx.net";
s.trackingServerSecure = "xxxxxxx.net";
```

다음 절차를 사용하여 목록에 변수를 추가합니다.

1. Adobe Analytics 프레임워크 페이지에서 **일반 Analytics 설정** 영역.
1. 변수 목록 아래에서 항목 추가 를 클릭하여 목록에 새 변수를 추가합니다.
1. 왼쪽 셀에서 변수 이름을 입력합니다(예: ) `prop10`.

1. 오른쪽 열에 변수 값을 입력합니다(예: ) `CONSTANT`.

1. 변수를 제거하려면 변수 옆에 있는 (-) 버튼을 클릭합니다.

>[!NOTE]
>
>변수와 값을 입력할 때 변수가 올바르게 형식화되고 맞춤법이 적용되었는지 또는 **호출이 전송되지 않음** 올바른 값/변수 쌍과 함께 사용할 수 있습니다. 철자가 잘못된 변수와 값이 있으면 호출이 발생하지 않도록 할 수 있습니다.
>
>이러한 변수가 올바르게 설정되었는지 확인하려면 Adobe Analytics 담당자에게 문의하십시오.

>[!CAUTION]
>
>이 목록의 일부 변수는 다음과 같습니다 **필수** Adobe Analytics 호출이 올바르게 작동하려면(예: **currencyCode**, **charSet**)
>
>따라서 프레임워크 자체에서 제거되더라도 Adobe Analytics 호출이 수행될 때 기본값이 여전히 첨부됩니다.

### Adobe Analytics 프레임워크에 사용자 지정 자바스크립트 추가 {#adding-custom-javascript-to-an-adobe-analytics-framework}

Javascript에서 사용 가능한 상자 **일반 Analytics 설정** 영역을 사용하면 Adobe Analytics 프레임워크에 사용자 지정 코드를 추가할 수 있습니다.

![aa-21](assets/aa-21.png)

추가하는 코드가 analytics.sitecatalyst.js 파일에 추가됩니다. 따라서 `s` 변수로서, `s_gi` 에 정의된 javascript 개체 `s_code.js`. 예를 들어 다음 코드를 추가하는 것은 라는 변수를 추가하는 것과 같습니다 `prop10` 값 `CONSTANT`: 이전 섹션의 예입니다.

`s.prop10= 'CONSTANT';`

의 코드 [analytics.sitecatalyst.js](/help/sites-developing/extending-analytics-components.md) 파일(Adobe Analytics의 컨텐츠가 포함됨) `s-code.js` file)에는 다음 코드가 포함되어 있습니다.

`if (s.usePlugins) s.doPlugins(s)`

다음 절차는 Javascript 상자를 사용하여 Adobe Analytics 추적을 사용자 지정하는 방법을 보여줍니다. Javascript에서 Adobe Analytics 플러그인을 사용해야 하는 경우, [통합](/help/sites-administering/adobeanalytics.md) AEM으로 전환합니다.

1. 다음 javascript 코드를 다음과 같이 상자에 추가합니다 `s.doPlugins` 가 실행됨:

   ```
   s.usePlugins=true;
   function s_doPlugins(s) {
       //add your custom code here
   }
   s.doPlugins=s_doPlugins;
   ```

   >[!CAUTION]
   >
   >이 코드는 기본 드래그 앤 드롭 인터페이스에서 또는 Adobe Analytics 보기의 인라인 javascript를 통해 수행할 수 없는 방식으로 사용자 지정된 방식으로 사용자 지정된 Adobe Analytics 호출에서 변수를 전송하려는 경우 필요합니다.
   >
   >사용자 지정 변수가 s_doPlugins 함수 외부에 있는 경우 Adobe Analytics 호출에서 *정의되지 않음 *으로 전송됩니다

1. 에 javascript 코드를 추가합니다. **s_doPlugins** 함수 위에 있어야 합니다.

다음 예제에서는 &quot;|&quot;의 공통 구분자를 사용하여 페이지에 캡처된 데이터를 계층 순서로 연결합니다.

Adobe Analytics 프레임워크에는 다음 구성이 있습니다.

* 다음 `prop2` Adobe Analytics 변수가 `pagedata.sitesection` 사이트 속성을 사용합니다.

* 다음 `prop3` Adobe Analytics 변수가 `pagedata.subsection` 사이트 속성을 사용합니다.

* 다음 코드가 자유 형식 javascript 상자에 추가됩니다.

   ```
   s.usePlugins=true;
    function s_doPlugins(s) {
    s.prop1 = s.prop2+'|'+s.prop3;
    }
    s.doPlugins=s_doPlugins;
   ```

* 프레임워크를 사용하는 웹 페이지를 방문하거나 편집 모드에서 페이지를 다시 로드하거나 미리 볼 때 Adobe Analytics 호출이 수행됩니다.

예를 들어 Adobe Analytics에서 다음 값이 생성됩니다.

![aa-20](assets/aa-20.png)

### 모든 Adobe Analytics 프레임워크에 대한 글로벌 사용자 지정 코드 추가 {#adding-global-custom-code-for-all-adobe-analytics-frameworks}

모든 Adobe Analytics 프레임워크에 통합된 사용자 지정 javascript 코드를 제공합니다. 페이지의 Adobe Analytics 프레임워크에 사용자 지정 항목이 없는 경우 [자유 형식 javascript](/help/sites-administering/adobeanalytics.md)로 지정하는 경우 /libs/cq/analytics/components/sitecatalyst/config.js.jsp 스크립트가 생성하는 javascript가 [analytics.sitecatalyst.js](/help/sites-administering/adobeanalytics.md) 파일. 기본적으로 스크립트는 주석 처리되므로 영향을 주지 않습니다. 코드도 설정됩니다 `s.usePlugins` to `false`:

```
/* Plugin Config */
/*
s.usePlugins=false;
function s_doPlugins(s) {
    //add your custom plugin code here
}
s.doPlugins=s_doPlugins;
*/
```

analytics.sitecatalyst.js 파일(Adobe Analytics s_code.js 파일의 컨텐츠가 포함됨)의 코드에는 다음 코드가 포함되어 있습니다.

if (s.usePlugins) s.doPlugins(s)

따라서 Javascript가 설정되어야 합니다 `s.usePlugins` to `true` 따라서 `s_doPlugins` 함수가 실행됩니다. 코드를 사용자 지정하려면 고유한 javascript를 사용하는 파일을 사용하여 config.js.jsp 파일을 오버레이합니다. Javascript에서 Adobe Analytics 플러그인을 사용해야 하는 경우, [통합](/help/sites-administering/adobeanalytics.md) AEM으로 전환합니다.

>[!NOTE]
>
>/libs/cq/analytics/components/sitecatalyst/config.js.jsp 파일은 편집하지 마십시오. 특정 AEM 업그레이드 또는 유지 관리 작업은 원본 파일을 다시 설치하여 변경 사항을 제거할 수 있습니다.

1. CRXDE Lite에서 /apps/cq/analytics/components 폴더 구조를 만듭니다.

   1. /apps 폴더를 마우스 오른쪽 단추로 클릭하고 만들기 > 폴더 만들기 를 클릭합니다.
   1. 지정 `cq` 을 폴더 이름으로 사용하고 확인을 클릭합니다.
   1. 마찬가지로, `analytics` 및 `components` 폴더.

1. 마우스 오른쪽 단추를 클릭합니다. `components` 방금 만든 폴더를 클릭한 다음 만들기 > 구성 요소 만들기를 클릭합니다. 다음 속성 값을 지정합니다.

   * 레이블: `sitecatalyst`
   * 제목: `sitecatalyst`
   * Super Type: `/libs/cq/analytics/components/sitecatalyst`
   * 그룹: `hidden`

1. 확인 단추가 활성화될 때까지 다음 을 계속 클릭하고 확인을 클릭합니다.

   Sitecatalyst 구성 요소에는 자동으로 생성된 sitecatalyst.jsp 파일이 포함되어 있습니다.

1. Sitecatalyst.jsp 파일을 마우스 오른쪽 단추로 클릭하고 삭제를 클릭합니다.

1. Sitecatalyst 구성 요소를 마우스 오른쪽 단추로 클릭하고 만들기 > 파일 만들기 를 클릭합니다. 이름을 지정합니다 `config.js.jsp` 확인을 클릭합니다.

   config.js.jsp 파일이 자동으로 열리고 편집할 수 있습니다.

1. 파일에 다음 텍스트를 추가한 다음 모두 저장을 클릭합니다.

   ```java
   <%@page session="true"%>
   /* Plugin Config */
   s.usePlugins=true;
   function s_doPlugins(s) {
       //add your custom plugin code here
   }
   s.doPlugins=s_doPlugins;
   ```

   이제 /apps/cq/analytics/components/sitecatalyst/config.js.jsp 스크립트가 생성하는 Javascript 코드가 Adobe Analytics 프레임워크을 사용하는 모든 페이지의 analytics.sitecatalyst.js 파일에 삽입됩니다.

1. 에서 실행할 Javascript 코드를 추가합니다. `s_doPlugins` 함수를 클릭한 다음 모두 저장을 클릭합니다.

>[!CAUTION]
>
>텍스트가 페이지 프레임워크의 자유 형식 javascript(공백만)에 있는 경우 config.js.jsp는 무시됩니다.

### AEM에서 Adobe Analytics 플러그인 사용 {#using-adobe-analytics-plugins-in-aem}

Adobe Analytics 플러그인에 대한 Javascript 코드를 가져와 AEM의 Adobe Analytics 프레임워크에 통합합니다. 카테고리의 클라이언트 라이브러리 폴더에 코드를 추가합니다 `sitecatalyst.plugins` 사용자 지정 javascript 코드에 사용할 수 있도록 해줍니다.

예를 들어 `getQueryParams` 플러그인을 호출하려면 `s_doPlugins` 사용자 지정 javascript의 함수입니다. 다음 예제 코드는에서 쿼리 문자열을 전송합니다 **&quot;pid&quot;** 레퍼러의 URL에서 **eVar1**&#x200B;인 경우, Adobe Analytics 호출이 트리거될 때

```
s.usePlugins=true;
function s_doPlugins(s) {
   // take the query string from the referrer
   s.eVar1=s.getQueryParam('pid','',document.referrer);
}
s.doPlugins=s_doPlugins;
```

AEM은 기본적으로 사용할 수 있도록 다음 Adobe Analytics 플러그인을 설치합니다.

* getQueryParam()
* getPreviousValue()
* split()

/libs/cq/analytics/clientlibs/sitecatalyst/plugins 클라이언트 라이브러리 폴더에는 sitecatalyst.plugins 카테고리에 이러한 플러그인이 포함되어 있습니다.

>[!NOTE]
>
>플러그인에 대한 새 클라이언트 라이브러리 폴더를 만듭니다. 플러그인을 `/libs/cq/analytics/clientlibs/sitecatalyst/plugins` 폴더를 입력합니다. 이 연습에서는 `sitecatalyst.plugins` AEM을 다시 설치하거나 업그레이드하는 동안 카테고리를 덮어쓰지 않습니다.

다음 절차를 사용하여 플러그인에 대한 클라이언트 라이브러리 폴더를 만듭니다. 이 절차는 한 번만 수행하면 됩니다. 클라이언트 라이브러리 폴더에 플러그인을 추가하려면 다음 절차를 따르십시오.

1. 웹 브라우저에서 CRXDE Lite을 엽니다. ([http://localhost:4502/crx/de](http://localhost:4502/crx/de))

1. /apps/my-app/clientlibs 폴더를 마우스 오른쪽 단추로 클릭하고 만들기 > 노드 만들기 를 클릭합니다. 다음 속성 값을 입력한 다음 확인을 누릅니다.

   * 이름: 내 플러그인과 같은 클라이언트 라이브러리 폴더의 이름입니다.

   * 유형: cq:ClientLibraryFolder

1. 방금 만든 클라이언트 라이브러리 폴더를 선택하고 오른쪽 하단에 있는 속성 막대를 사용하여 다음 속성을 추가합니다.

   * 이름: 카테고리
   * 유형: 문자열
   * 값: sitecatalyst.plugins
   * 다중: 선택됨

   편집 창에서 확인 을 클릭하여 속성 값을 확인합니다.

1. 방금 만든 클라이언트 라이브러리 폴더를 마우스 오른쪽 단추로 클릭하고 만들기 > 파일 만들기를 클릭합니다. 파일 이름 유형 js.txt에 대해 확인을 누릅니다.

1. 모두 저장을 클릭합니다.

다음 절차를 사용하여 플러그인 코드를 가져오고, 코드를 AEM 저장소에 저장하고, 클라이언트 라이브러리 폴더에 코드를 추가합니다.

1. 에 로그인합니다. [sc.omniture.com](https://sc.omniture.com) Adobe Analytics 계정 사용.
1. 랜딩 페이지에서 도움말 > 도움말 홈으로 이동합니다.
1. 왼쪽의 목차 테이블에서 구현 플러그인을 클릭합니다.
1. 추가할 플러그인에 대한 링크를 클릭하고 페이지가 열리면 플러그인에 대한 Javascript 소스 코드를 찾은 다음 코드를 선택하고 복사합니다.

1. 클라이언트 라이브러리 폴더를 마우스 오른쪽 단추로 클릭하고 만들기 > 파일 만들기를 클릭합니다. 파일 이름에 통합할 플러그인 이름 뒤에 .js를 입력하고 확인을 클릭합니다. 예를 들어 getQueryParam 플러그인을 통합하는 경우 getQueryParam.js 파일의 이름을 getQueryParam.js로 지정합니다.

   파일을 만들면 편집을 위해 열립니다.

1. 플러그인 Javascript 코드를 파일에 붙여 넣고 모두 저장 을 클릭한 다음 파일을 닫습니다.

1. 클라이언트 라이브러리 폴더에서 js.txt 파일을 엽니다.

1. 새 행에 플러그인이 포함된 파일 이름(예: getQueryParam.js)을 추가합니다. 그런 다음 모두 저장 을 클릭하고 파일을 닫습니다.

>[!NOTE]
>
>플러그인을 사용할 때는 지원 플러그인도 통합해야 합니다. 그렇지 않으면 플러그인 javascript가 지원 플러그인의 함수에 대해 수행하는 호출을 인식하지 못합니다. 예를 들어 getPreviousValue() 플러그인을 사용하려면 split() 플러그인이 올바르게 작동해야 합니다.
>
>지원 플러그인의 이름을 **js.txt** 또한.
