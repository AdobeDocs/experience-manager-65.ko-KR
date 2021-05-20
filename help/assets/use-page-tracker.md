---
title: 웹 페이지에 페이지 추적기 및 포함 코드 사용
description: Adobe Analytics이 자산에 대한 사용 데이터를 캡처할 수 있도록 웹 사이트 코드에 페이지 추적기 및 JavaScript 코드를 포함하는 방법을 알아봅니다.
contentOwner: AG
role: Architect, Administrator
feature: 자산 보고서
exl-id: 14d02015-df00-4566-a098-de76eaf42605
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 6%

---

# 웹 페이지에 페이지 추적기 및 포함 코드 사용 {#using-page-tracker-and-embed-code-in-web-pages}

페이지 추적기는 Adobe Analytics이 이러한 웹 사이트에서 [!DNL Adobe Experience Manager Assets] 주위의 사용 데이터를 캡처할 수 있도록 타사 웹 사이트의 코드에 포함하는 JavaScript 코드 부분입니다.

자산에만 해당하는 클릭 등과 같은 이벤트를 캡처하려면 타사 웹 사이트의 코드에 포함 코드를 포함합니다.

다음 샘플 코드는 페이지 추적기 코드와 포함 코드를 모두 포함하는 웹 페이지의 모습을 보여줍니다.

```html
<!DOCTYPE html>
<html>
    <head>
            <script type="text/javascript" src="http://localhost:4502/xxxx/etc.clientlibs/dam/clientlibs/sitecatalyst/appmeasurement.js"></script>
            <script type="text/javascript" src="http://localhost:4502/xxxx/etc.clientlibs/dam/clientlibs/assetinsights/pagetracker.js"></script>
            <script type="text/javascript">
                                assetAnalytics.attrTrackable = 'trackable';
                assetAnalytics.defaultTrackable = false;
                assetAnalytics.attrAssetID = 'aem-asset-id';
                assetAnalytics.assetImpressionPollInterval = 200; // interval in milliseconds
                assetAnalytics.charsLimitForGET = 2000; // bytes
                assetAnalytics.dispatcher.init("assetstesting","xxxx","xxx","list1","eVar3","event8","event7");
            </script>

    </head>

    <body>

                                <img
            src="https://10.41.52.147:4502/xxxx/content/dam/test/abc.jpg"
            data-aem-asset-id="aaid:a386f2cd78234becb66bd11575f9452d"
            data-trackable=true
            onload=assetAnalytics.core.assetLoaded(this)>

        <a
            href="https://www.adobe.com"

            onclick="assetAnalytics.core.assetClicked(this);return false">
                <img
                    src="http://localhost/xxxx/content/dam/test/xyz.jpg"
                    data-aem-asset-id="aaid:7fa01fce0ebe40268cd6dcf07e2d9cb1"
                    data-trackable=true
                    onload=assetAnalytics.core.assetLoaded(this)>
        </a>

    </body>
</html>
```

## 페이지 추적기 코드 {#adding-page-tracker-code} 추가

웹 사이트 코드의 헤더 섹션 내에 페이지 추적기 코드를 추가합니다. 다음 코드 조각은 샘플 웹 페이지에 포함된 페이지 추적기 코드를 표시합니다.

```xml
 <head>
            <script type="text/javascript" src="http://localhost:4502/xxxx/etc.clientlibs/dam/clientlibs/sitecatalyst/appmeasurement.js"></script>
            <script type="text/javascript" src="http://localhost:4502/xxxx/etc.clientlibs/dam/clientlibs/foundation/assetinsights/pagetracker.js"></script>
            <script type="text/javascript">
                                assetAnalytics.attrTrackable = 'trackable';
                assetAnalytics.defaultTrackable = false;
                assetAnalytics.attrAssetID = 'aem-asset-id';
                assetAnalytics.assetImpressionPollInterval = 200; // interval in millis
                assetAnalytics.charsLimitForGET = 2000; // bytes
                assetAnalytics.dispatcher.init("assetstesting","abc.net","bee","list1","eVar3","event8","event7");
            </script>

 </head>
```

## 포함 코드 추가 {#add-embed-code}

웹 사이트 코드 본문에 포함 코드를 추가합니다. 다음 코드 조각은 샘플 웹 페이지에 포함된 포함 코드를 표시합니다.

```xml
<body>

      <img
            src="http://localhost:4502/xxxx/content/dam/test/xyz.jpg"
            data-aem-asset-id="aaid:a386f2cd78234becb66bd11575f9452d"
            data-trackable=true
            onload=assetAnalytics.core.assetLoaded(this)>

        <a
            href="https://www.adobe.com"

            onclick="assetAnalytics.core.assetClicked(this);return false">
           <img
                    src="http://localhost:4502/xxxx/content/dam/test/xyz.jpg"
                    data-aem-asset-id="aaid:7fa01fce0ebe40268cd6dcf07e2d9cb1"
                    data-trackable=true
                    onload=assetAnalytics.core.assetLoaded(this)>
        </a>

    </body>
```
