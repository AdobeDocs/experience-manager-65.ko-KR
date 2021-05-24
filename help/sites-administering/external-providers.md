---
title: 외부 공급자의 Analytics
seo-title: 외부 공급자의 Analytics
description: 외부 공급자의 Analytics에 대해 알아봅니다.
seo-description: 외부 공급자의 Analytics에 대해 알아봅니다.
uuid: 31a773ca-901e-45f2-be8f-951c26f9dbc5
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: bab465bc-1ff4-4f21-9885-e4a875c73a8d
docset: aem65
exl-id: 9bf818f9-6e33-4557-b2e4-b0d4900f2a05
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 3%

---

# 외부 공급자의 Analytics {#analytics-with-external-providers}

Analytics에서는 웹 사이트 사용 방식에 대한 중요하고도 흥미로운 정보를 제공할 수 있습니다.

적절한 서비스와 통합할 때 다음과 같은 다양한 기본 구성을 사용할 수 있습니다.

* [Adobe Analytics](/help/sites-administering/adobeanalytics.md)
* [Adobe Target](/help/sites-administering/target.md)

또한 **일반 Analytics 코드 조각**&#x200B;의 자체 인스턴스를 구성하여 새 서비스 구성을 정의할 수도 있습니다.

그런 다음 웹 페이지에 추가되는 작은 코드 조각을 통해 정보를 수집합니다. 예:

>[!CAUTION]
>
>스크립트는 `script` 태그로 묶으면 안 됩니다.

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

이러한 코드 조각을 사용하면 데이터를 수집하고 보고서를 생성할 수 있습니다. 수집된 실제 데이터는 사용되는 공급자 및 실제 코드 조각에 따라 다릅니다. 통계 예는 다음과 같습니다.

* 시간에 따른 방문자 수
* 방문한 페이지 수
* 사용된 검색어
* 랜딩 페이지

>[!CAUTION]
>
>Geometrixx-Outdoors 데모 사이트는 페이지 속성에 제공된 속성이 해당 `</html>` 종료 태그 바로 위에 있는 html 소스 코드에 추가되도록 구성됩니다.`js`
>
>자신의 `/apps`이 기본 페이지 구성 요소( `/libs/foundation/components/page`)에서 상속되지 않는 경우 사용자(또는 개발자)는 해당 `cq/cloudserviceconfigs/components/servicescomponents` 스크립트를 포함하거나 유사한 메커니즘을 사용하여 해당 `js` 스크립트가 포함되어 있는지 확인해야 합니다.
>
>이렇게 하지 않으면 서비스(일반, Analytics, Target 등)가 작동하지 않습니다.

## 일반 코드 조각 {#creating-a-new-service-with-a-generic-snippet}으로 새 서비스 만들기

기본 구성의 경우:

1. **도구** 콘솔을 엽니다.
1. 왼쪽 창에서 **Cloud Services 구성**&#x200B;을 확장합니다.
1. **일반 Analytics 코드 조각**&#x200B;을 두 번 클릭하여 페이지를 엽니다.

   ![](assets/analytics_genericoverview.png)

1. 대화 상자를 사용하여 새 구성을 추가하려면 + 를 클릭합니다.최소한 이름(예: google analytics)을 할당합니다.

   ![](assets/analytics_addconfig.png)

1. **만들기**&#x200B;를 클릭하면 코드 조각 대화 상자가 즉시 열립니다. 적절한 Javascript 조각을 필드에 붙여 넣습니다.

   ![](assets/analytics_snippet.png)

1. **확인**&#x200B;을 클릭하여 저장합니다.

## 페이지에서 새 서비스 사용 {#using-your-new-service-on-pages}

서비스 구성을 만들었으면 이제 이 구성을 사용하도록 필요한 페이지를 구성해야 합니다.

1. 페이지로 이동합니다.
1. 사이드킥에서 **페이지 속성**&#x200B;을 연 다음, **Cloud Services** 탭을 엽니다.
1. **서비스 추가**&#x200B;를 클릭한 다음 필요한 서비스를 선택합니다.예: **일반 Analytics 코드 조각**:

   ![](assets/analytics_selectservice.png)

1. **확인**&#x200B;을 클릭하여 저장합니다.
1. **Cloud Services** 탭으로 돌아갑니다. 이제 **일반 Analytics 코드 조각**&#x200B;이 `Configuration reference missing` 메시지와 함께 나열됩니다. 드롭다운 목록을 사용하여 특정 서비스 인스턴스를 선택합니다.예를 들면 google-analytics입니다.

   ![](assets/analytics_selectspecificservice.png)

1. **확인**&#x200B;을 클릭하여 저장합니다.

   이제 페이지에 대한 페이지 소스를 볼 경우 코드 조각을 볼 수 있습니다.

   적절한 시간이 경과하면 수집된 통계를 볼 수 있습니다.

   >[!NOTE]
   >
   >구성이 하위 페이지가 있는 페이지에 첨부된 경우 해당 서비스도 상속됩니다.
