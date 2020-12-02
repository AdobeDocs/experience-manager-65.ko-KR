---
title: HTTP2 컨텐츠 전달
description: HTTP/2는 브라우저와 서버의 통신 방식을 개선하여 필요한 처리 능력을 줄이면서 정보를 신속하게 전송할 수 있도록 합니다.
uuid: d9deb945-bdf5-4d6b-95c8-8bae4442e618
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: c8e145ad-f021-4043-8190-62151775e296
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f
workflow-type: tm+mt
source-wordcount: '705'
ht-degree: 0%

---


# HTTP2 컨텐츠 배달 {#http-delivery-of-content}

Adobe은 향상된 성능을 통해 HTTP/2 컨텐츠 전달을 사용할 수 있음을 발표하게 되어 매우 기쁘게 생각합니다.

## HTTP/2 소개{#what-is-http}

HTTP/2는 브라우저와 서버의 통신 방식을 개선하여 정보를 보다 신속하게 전송할 수 있도록 하며 필요한 처리 능력을 감소시킵니다.

다음 웹 사이트에서는 HTTP/2 및 HTTP의 혜택에 대해 간단하고 간단하게 설명합니다.

[https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/](https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/)

## HTTP/2로 컨텐츠를 전달하여 얻을 수 있는 주요 이점은 무엇입니까?{#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

성능 개선 사항은 웹 사이트 코드, 다이내믹 미디어 사용 방법, 소비자의 디바이스, 화면 및 위치 등과 같은 요인에 따라 다릅니다.

Adobe 자체 테스트 결과:

* 이미지의 경우, 응답 시간이 디바이스와 브라우저에 따라 7%-28% 향상되었습니다. iOS 디바이스에서 가장 눈에 띄는 성능 향상
* 뷰어의 경우 로드 시간 성능이 15% 향상되었습니다.

다음 데모에서는 HTTP/1과 HTTP/2 로딩 간의 차이점을 보여 줍니다.

[https://http2.akamai.com/demo](https://http2.akamai.com/demo)

## HTTP/2로 전환할 수 있습니까?{#am-i-eligible-to-switch-over-to-http}

HTTP/2를 사용하려면 다음 요구 사항을 충족해야 합니다.

* 리치 미디어 요청에 안전한 HTTPS를 사용하십시오.
* Adobe 번들 CDN(컨텐츠 전달 네트워크)을 다이내믹 미디어 라이선스의 일부로 사용할 수 있습니다.
* 전용(company-h.assetsadobe#.com) 도메인을 사용합니다.

   이미 전용 도메인이 있는 경우 기술 지원을 통해 옵트인할 수 있습니다.

   전용 도메인이 없는 경우 Adobe은 2018년 HTTP/2로 전환을 예약합니다.

## 내 Dynamic Media 계정에 대해 HTTP/2를 활성화하는 프로세스는 무엇입니까?{#what-is-the-process-for-enabling-http-for-my-dynamic-media-account}

HTTP/2로 전환하기 위한 요청을 시작해야 합니다.자동으로 수행되지 않습니다.

1. HTTP2로 전환하려면 기술 지원 요청을 시작합니다. [AEM 지원 포털 액세스](https://helpx.adobe.com/kr/experience-manager/kb/accessing-aem-support-portal.html)를 참조하십시오.

   1. 지원 요청에서 다음 정보를 제공합니다.

      1. 기본 연락처 이름, 이메일, 전화.
      1. HTTP2로 전환할 모든 도메인.
      1. 리치 미디어 요청에 보안 HTTPS를 사용하고 있는지 확인합니다.
      1. Adobe을 통해 CDN을 사용하고 있으며 직접 관계로 관리되지 않는지 확인합니다.
      1. 전용 도메인을 사용하고 있는지 확인합니다. Dynamic Media를 사용하는 경우 이미 전용 도메인을 사용하고 있는 것입니다.
   1. 기술 지원에서 요청을 제출한 순서에 따라 HTTP/2 고객 대기 목록에 추가합니다.
   1. Adobe이 요청을 처리할 준비가 되면 지원 담당자가 전환을 조정하고 대상 날짜를 설정하도록 알려줍니다.
   1. 완료 후 알림을 받게 되며 HTTP2로 성공적으로 전환했는지 확인할 수 있습니다.

      브라우저가 이 사실을 표시하지 않으므로 익스텐션을 다운로드해야 합니다.

      Firefox 및 Chrome의 경우 &quot;HTTP/2 및 SPDY 표시기&quot;라는 확장자가 있습니다. 브라우저는 http/2만 안전하게 지원되므로 https를 사용하여 URL을 호출하여 확인해야 합니다. http/2가 지원되는 경우 파란색 Flash 기호 형태로 확장자로 표시되고 헤더 &quot;X-Firefox-Spdy&quot;가 표시됩니다.&quot;h2&quot;.


## 언제 HTTP/2로 전환할 예정입니까?{#when-can-i-expect-to-be-transitioned-over-to-http}

요청은 기술 지원 센터에서 수신되는 순서대로 처리됩니다.

>[!NOTE]
>
>HTTP/2로 전환하는 경우 캐시를 지워야 하므로 리드 타임이 오래 걸릴 수 있습니다. 따라서 일부 고객 전환만 한 번에 처리할 수 있습니다.

## HTTP/2로 전환하면 어떤 위험이 발생합니까?{#what-are-the-risks-with-moving-to-http}

HTTP/2로의 전환은 새 CDN 구성으로 이동하는 것을 포함하므로 CDN의 캐시를 지웁니다.

캐시되지 않은 컨텐츠는 캐시를 다시 빌드할 때까지 Adobe 원본 서버를 직접 히트 시킵니다. 이러한 이유로 Adobe은 한 번에 몇 개의 고객 전환을 처리하여 원본 고객의 요청을 가져올 때 허용되는 성능이 유지되도록 할 계획입니다.

## URL 또는 웹 사이트가 HTTP/2로 활성화되었는지 어떻게 확인할 수 있습니까?{#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

브라우저가 이 사실을 표시하지 않으므로 익스텐션을 다운로드해야 합니다.

Firefox 및 Chrome의 경우 &quot;HTTP/2 및 SPDY 표시기&quot;라는 확장자가 있습니다. 브라우저는 http/2만 안전하게 지원되므로 https를 사용하여 URL을 호출하여 확인해야 합니다. http/2가 지원되는 경우 파란색 Flash 기호 형태로 확장자로 표시되고 헤더 &quot;X-Firefox-Spdy&quot;가 표시됩니다.&quot;h2&quot;.
