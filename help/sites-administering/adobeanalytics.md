---
title: Adobe Analytics와 통합
seo-title: Adobe Analytics와 통합
description: AEM과 Adobe Analytics을 통합하는 방법을 살펴보십시오.
seo-description: AEM과 Adobe Analytics을 통합하는 방법을 살펴보십시오.
uuid: d8548263-6ac5-45fb-8c70-52ecd4161bbb
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 444c522e-2f33-4f41-846c-8d317e799659
docset: aem65
translation-type: tm+mt
source-git-commit: ca25e66b280db479f69c487753a557b0240233da
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 5%

---


# Adobe Analytics와 통합{#integrating-with-adobe-analytics}

Adobe Analytics 및 AEM 통합을 통해 웹 페이지 활동을 추적할 수 있습니다.

* Adobe Analytics 구성을 통해 AEM은 Adobe Analytics에 대한 인증을 수행할 수 있습니다.
* 프레임워크는 Adobe Analytics 보고서 세트로 전송된 데이터를 식별합니다.

데이터에는 페이지 및 사용자 데이터가 포함됩니다.예를 들면 다음과 같습니다.

* aem 구성 요소가 수집하는 데이터
* 링크 클릭 수
* 비디오 사용 정보
* adobe analytics에서 페이지 방문 횟수

다음 페이지에서는 통합을 구성하는 데 도움이 됩니다.

* [Adobe Analytics 및 Creating Frameworks에 연결](/help/sites-administering/adobeanalytics-connect.md)
* [Adobe Analytics에 대한 링크 추적 구성](/help/sites-administering/adobeanalytics-link.md)
* [Adobe Analytics 속성을 사용하여 구성 요소 데이터 매핑](/help/sites-administering/adobeanalytics-mapping.md)
* [Adobe Analytics에 대한 비디오 추적 구성](/help/sites-administering/adobeanalytics-video.md)
* [Adobe 분류](/help/sites-administering/adobeanalytics-classifications.md)

[옵트인 마법사](/help/sites-administering/opt-in.md)를 사용하여 손쉽게 통합을 수행할 수도 있습니다.

>[!NOTE]
>
>방법 기술문서를 참조하십시오.[DTM](https://helpx.adobe.com/experience-manager/using/integrate-digital-marketing-solutions.html)을(를) 사용하여 AEM과 Adobe Target 및 Adobe Analytics 통합

## 추가 정보 {#further-information}

다음을 참조하십시오.

* [Adobe Analytics ](/help/sites-developing/extending-analytics.md) 통합 확장을 참조하십시오.
* Adobe Analytics 통합 문제 해결에 대한 자세한 내용은 기술 자료 문서 [Adobe Analytics 통합 - 문제 해결](https://helpx.adobe.com/experience-manager/kb/sitecatalystintegrationtroubleshooting.html).

>[!NOTE]
>
>사용자 지정 프록시 구성과 함께 Adobe Analytics을 사용하는 경우 ](/help/sites-deploying/configuring-osgi.md)Apache HTTP 클라이언트&#x200B;**프록시 구성에 필요한 두 개의 OSGi 번들[(예: 웹 콘솔 포함)을 구성해야 합니다.** AEM의 일부 기능에서는 3.x API를 사용하고 다른 기능에서는 4.x API를 사용합니다. 구성:
>
>* **3.x API** 를 구성하는 Day Commons HTTP Client 3.1;
   >  예: [https://localhost:4502/system/console/configMgr/com.day.commons.httpclient](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
   >
   >
* **4.x API를** 구성하기 위한 Apache HTTP 구성 요소 프록시 구성;
   >  예: [https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)

>



