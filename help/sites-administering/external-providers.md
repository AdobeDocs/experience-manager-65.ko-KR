---
title: 외부 공급자의 Analytics
description: 고유한 일반 Analytics 조각 인스턴스를 구성하여 새로운 서비스 구성을 정의하는 방법을 알아봅니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: 9bf818f9-6e33-4557-b2e4-b0d4900f2a05
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 1%

---


# 외부 공급자의 Analytics {#analytics-with-external-providers}

Analytics는 웹 사이트가 사용되는 방식에 대한 중요하고 흥미로운 정보를 제공할 수 있습니다.

적절한 서비스와 통합할 수 있는 기본 구성은 다음과 같습니다.

* [Adobe Analytics](/help/sites-administering/adobeanalytics.md)
* [Adobe Target](/help/sites-administering/target.md)

의 고유한 인스턴스를 구성할 수도 있습니다. **범용 Analytics 조각** 새 서비스 구성을 정의합니다.

그런 다음 웹 페이지에 추가되는 작은 코드 조각에서 정보를 수집합니다. 예:

>[!CAUTION]
>
>스크립트를에 묶지 마십시오 `script` 태그 사이에 코드를 삽입하지 마십시오.

```
var _gaq = _gaq || [];
_gaq.push(['_setAccount', 'UA-XXXXX-X']);
_gaq.push(['_trackPageview']);

(function() {
    var ga = document.createElement('script'); ga.type = 'text/javascript'; ga.async = true;
    ga.src = ('https:' == document.location.protocol ? 'https://ssl' : 'https://www') + '.google-analytics.com/ga.js';
    var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(ga, s);
})();
```

이러한 스니펫을 사용하면 데이터를 수집하고 보고서를 생성할 수 있습니다. 수집된 실제 데이터는 공급자와 사용된 실제 코드 조각에 따라 다릅니다. 예제 통계는 다음과 같습니다.

* 시간 경과에 따른 방문자 수
* 방문한 페이지 수
* 사용된 검색어
* 랜딩 페이지

>[!CAUTION]
>
>Geometrixx-Outdoors 데모 사이트는 페이지 속성에 제공된 속성이 html 소스 코드에 추가되도록 구성됩니다(위의 `</html>` end 태그)를 추가합니다. `js` 스크립트.
>
>본인 소유인 경우 `/apps` 기본 페이지 구성 요소에서 상속하지 않음( `/libs/foundation/components/page`) 사용자(또는 개발자)는 `js` 스크립트는 예를 들어 다음 중 하나에 의해 포함됩니다. `cq/cloudserviceconfigs/components/servicescomponents`또는 유사한 메커니즘을 사용하는 경우입니다.
>
>이렇게 하지 않으면 어떤 서비스(일반, Analytics, Target 등)도 작동하지 않습니다.

## 일반 코드 조각을 사용하여 서비스 만들기 {#creating-a-new-service-with-a-generic-snippet}

기본 구성의 경우:

1. 를 엽니다. **도구** 콘솔.
1. 왼쪽 창에서 을 확장합니다. **Cloud Service 구성**.
1. 두 번 클릭 **범용 Analytics 코드 조각** 페이지를 열려면 다음을 수행하십시오.

   ![범용 Analytics 코드 조각](assets/analytics_genericoverview.png)

1. 대화 상자를 사용하여 새 구성을 추가하려면 +를 클릭합니다. 최소한 다음과 같은 이름을 지정하십시오. (예: Google Analytics)

   ![구성 만들기](assets/analytics_addconfig.png)

1. 클릭 **만들기**, 코드 조각 대화 상자가 즉시 열립니다. 해당 JavaScript 코드 조각을 필드에 붙여 넣습니다.

   ![구성 요소 편집](assets/analytics_snippet.png)

1. 클릭 **확인** 저장.

## 페이지에서 새 서비스 사용 {#using-your-new-service-on-pages}

서비스 구성을 만든 후에는 이를 사용할 필수 페이지를 구성해야 합니다.

1. 페이지로 이동합니다.
1. 를 엽니다. **페이지 속성** 사이드 킥에서 **Cloud Service** 탭.
1. 클릭 **서비스 추가**&#x200B;필요한 서비스를 선택합니다. 예를 들어 **범용 Analytics 코드 조각**:

   ![클라우드 서비스 추가](assets/analytics_selectservice.png)

1. 클릭 **확인** 저장.
1. (으)로 돌아갑니다. **Cloud Service** 탭. 다음 **범용 Analytics 코드 조각** 은(는) 이제 메시지와 함께 나열됩니다. `Configuration reference missing`. 드롭다운 목록을 사용하여 특정 서비스 인스턴스를 선택합니다. 예를 들어 google-analytics는

   ![클라우드 서비스 구성 추가 중](assets/analytics_selectspecificservice.png)

1. 클릭 **확인** 저장.

   이제 페이지의 페이지 소스를 보면 코드 조각을 볼 수 있습니다.

   시간이 경과하면 수집된 통계를 볼 수 있습니다.

   >[!NOTE]
   >
   >구성이 하위 페이지가 있는 페이지에 첨부된 경우 서비스도 상속됩니다.
