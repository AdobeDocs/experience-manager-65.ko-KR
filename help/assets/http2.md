---
title: 컨텐츠의 HTTP2 전달
description: HTTP/2가 브라우저와 서버의 통신 방식을 개선하여 필요한 처리 능력을 줄이면서 정보를 더 빠르게 전송하는 방법에 대해 알아봅니다.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
role: User, Admin
exl-id: 9eb9f309-33e5-4694-84d2-fb2cd3de50a6
feature: Publishing,Configuration
solution: Experience Manager, Experience Manager Assets
source-git-commit: f749892bf7fba9889adfc930771178154b92fa5d
workflow-type: tm+mt
source-wordcount: '735'
ht-degree: 3%

---

# 콘텐츠의 HTTP/2 전달 {#http-delivery-of-content}

Adobe에서는 전반적인 성능이 개선된 HTTP/2 콘텐츠 제공을 발표하게 되었습니다.

>[!NOTE]
>
>이 기능을 사용하려면 Adobe Experience Manager Dynamic Media와 번들로 제공되는 기본 CDN을 사용해야 합니다. 다른 모든 사용자 지정 CDN은 이 기능에서 지원되지 않습니다.

## HTTP/2란? {#what-is-http}

HTTP/2는 브라우저와 서버의 통신 방식을 향상시켜 필요한 처리 능력을 줄이면서 정보를 더 빠르게 전송할 수 있도록 합니다.

다음 웹 사이트에서는 HTTP/2와 그 이점을 간단하고 간단하게 설명합니다.

[HTTP/2에 대해 알고 있어야 하는 사항](https://www.engadget.com/2015-02-24-what-you-need-to-know-about-http-2.html)

## 컨텐츠 전달을 위해 HTTP/2로 이동하면 얻을 수 있는 주요 이점은 무엇입니까? {#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

성능 향상은 크게 다를 수 있습니다. 웹 사이트의 코드, Dynamic Media 사용 방법, 소비자의 장치, 화면 및 위치와 같은 많은 요소를 기반으로 합니다.

Adobe 자체 테스트에서 다음과 같은 결과가 도출되었습니다.

* 이미지의 경우 디바이스 및 브라우저에 따라 응답 시간이 7~28% 향상되었습니다. 가장 눈에 띄는 성능 향상은 iOS 장치에서 이루어졌습니다.
* 뷰어의 경우 로드 시간 성능이 15% 향상되었습니다.

<!--
The following demonstration illustrates the difference between HTTP/1 versus HTTP/2 loading:

[https://http2.akamai.com/demo](https://http2.akamai.com/demo) -->

## HTTP/2로 전환할 수 있습니까? {#am-i-eligible-to-switch-over-to-http}

HTTP/2를 사용하려면 다음 요구 사항을 충족해야 합니다.

* 리치 미디어 요청에 보안 HTTPS를 사용합니다.
* Adobe 번들 CDN(Content Delivery Network)을 Dynamic Media 라이선스의 일부로 사용합니다.
* 전용(company-h.assetsadobe#.com이 아닌) 도메인을 사용합니다.

  이미 전용 도메인이 있는 경우 Adobe 고객 지원 을 통해 옵트인할 수 있습니다.

  전용 도메인이 없는 경우, Adobe은 2018년에 HTTP/2로 전환하는 일정을 계획합니다.

## 내 Dynamic Media 계정에 대해 HTTP/2를 활성화하는 프로세스는 무엇입니까? {#what-is-the-process-for-enabling-http-for-my-dynamic-media-account}

요청을 시작하여 HTTP/2로 전환합니다. 이 작업은 자동으로 수행되지 않습니다.

1. HTTP/2로 전환하려면 Adobe 고객 지원 요청을 시작합니다. [지원 티켓 열기](https://experienceleague.adobe.com/?support-solution=General&lang=en&support-tab=home#support)를 참조하세요.

   1. 지원 요청에 다음 정보를 제공합니다.

      1. 기본 담당자 이름, 이메일, 전화.
      1. HTTP/2로 전환할 모든 도메인.
      1. 리치 미디어 요청에 보안 HTTPS를 사용하는지 확인합니다.
      1. Adobe을 통해 CDN을 사용하고 있으며 직접적인 관계로 관리되지 않는지 확인합니다.
      1. 전용 도메인을 사용하는지 확인합니다. Dynamic Media를 사용하는 경우 전용 도메인을 사용합니다.

   1. 고객 지원에서 요청이 제출된 순서에 따라 HTTP/2 고객 대기자 명단에 사용자를 추가합니다.
   1. Adobe에서 요청을 처리할 준비가 되면 고객 지원 팀에서 연락하여 전환을 조정하고 목표 날짜를 설정합니다.
   1. 완료 후 알림이 전송되며 HTTP2로의 성공적인 전환을 확인할 수 있습니다.

      브라우저는 이 사실을 기술하지 않으므로 확장을 다운로드해야 합니다.

      Firefox 및 Chrome의 경우 &quot;HTTP/2 및 SPDY 표시기&quot;라는 확장이 있습니다. 브라우저는 http/2만 안전하게 지원하므로, URL을 https로 호출하여 확인해야 합니다. http/2가 지원되는 경우 확장은 i를 나타냅니다. 확장은 파란색 Flash 기호 형식이며 헤더 `X-Firefox-Spdy`: `h2`입니다.

## HTTP/2로의 전환은 언제 발생합니까? {#when-can-i-expect-to-be-transitioned-over-to-http}

요청은 고객 지원 센터에서 받은 순서대로 처리됩니다.

>[!NOTE]
>
>HTTP/2로의 전환에는 캐시 지우기가 포함되므로 리드 타임이 길 수 있습니다. 따라서 한 번에 몇 개의 고객 전환만 처리할 수 있습니다.

## HTTP/2로 이동할 때 발생하는 위험은 무엇입니까? {#what-are-the-risks-with-moving-to-http}

HTTP/2로 전환하면 새 CDN 구성으로 이동하는 작업이 포함되므로 CDN에서 캐시가 지워집니다.

캐싱되지 않은 콘텐츠는 캐시가 다시 빌드될 때까지 Adobe의 원본 서버에 직접 도달합니다. 이와 같이 Adobe은 원점에서 요청을 가져올 때 수용 가능한 성능이 유지되도록 한 번에 몇 개의 고객 전환을 처리할 계획입니다.

## URL 또는 웹 사이트가 HTTP/2로 활성화되었는지 어떻게 확인할 수 있습니까? {#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

브라우저는 이 사실을 기술하지 않으므로 확장을 다운로드해야 합니다.

Firefox 및 Chrome의 경우 &quot;HTTP/2 및 SPDY 표시기&quot;라는 확장이 있습니다. 브라우저는 http/2만 안전하게 지원하므로, URL을 https로 호출하여 확인해야 합니다. http/2가 지원되는 경우 확장이 이를 나타냅니다. 확장은 파란색 Flash 기호 형식이며 헤더 `X-Firefox-Spdy`: `h2`입니다.
