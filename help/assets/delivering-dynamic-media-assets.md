---
title: Dynamic Media 자산 제공
description: Dynamic Media 자산을 제공하는 방법을 알아봅니다
uuid: 23eddf83-34f5-4aae-8b81-d1cd7a098a7e
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: e3b44330-d476-49c6-b7ba-079d0d60e500
docset: aem65
role: Business Practitioner, Administrator
exl-id: 274af114-845a-46bd-b091-802cf589687a
feature: 자산 관리,표현물
source-git-commit: c9aec973faf4caef741961d92a6f258646aeddb7
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 18%

---

# Dynamic Media 자산 제공{#delivering-dynamic-media-assets}

Dynamic Media 자산(비디오와 이미지 모두)을 전달하는 방법은 웹 사이트가 구현되는 방식에 따라 다릅니다.

Dynamic Media에는 다음의 몇 가지 선택 사항이 있습니다.

* 웹 사이트가 AEM에서 호스팅되는 경우 Dynamic Media 자산을 페이지에 바로 추가할 수 있습니다.
* 웹 사이트가 AEM에 없는 경우 다음 중 하나를 선택할 수 있습니다.

   * 웹 사이트에 비디오 또는 이미지를 포함합니다.
   * 웹 애플리케이션에 URL을 연결합니다. 비디오 플레이어를 팝업 또는 모달 창으로 전달하려는 경우 링크를 사용합니다.
   * 사이트가 응답형인 경우 [최적화된 이미지를 제공할 수 있습니다.](/help/assets/responsive-site.md)

>[!NOTE]
>
>스마트 이미징은 기존 이미지 사전 설정에서 작동하며 마지막 전달 순간에 인텔리전스를 사용하여 브라우저 또는 네트워크 연결 속도에 따라 이미지 파일 크기를 더 줄입니다. 자세한 내용은 [스마트 이미징](/help/assets/imaging-faq.md) 을 참조하십시오.

자세한 내용은 다음 항목을 참조하십시오.

* [웹 페이지에 Dynamic Media 자산 추가](/help/assets/adding-dynamic-media-assets-to-pages.md)
* [웹 페이지에 비디오 또는 이미지 뷰어 포함](/help/assets/embed-code.md)
* [Dynamic Media에서 핫링크 보호 활성화](hotlink-protection.md)
* [URL을 웹 애플리케이션에 연결](/help/assets/linking-urls-to-yourwebapplication.md)
* [응답형 사이트용으로 최적화된 이미지 제공](/help/assets/responsive-site.md)
* [컨텐츠의 HTTP2 전달](/help/assets/http2.md)
* [Dynamic Media Classic을 통해 CDN 캐시 무효화](/help/assets/invalidate-cdn-cache-dm-classic.md)
* [규칙 세트를 사용하여 URL 변환](/help/assets/using-rulesets-to-transform-urls.md)


## Dynamic Media 자산 {#http-delivery-of-dynamic-media-assets} 의 HTTP/2 전달

이제 AEM에서는 HTTP/2를 통해 모든 Dynamic Media 컨텐츠(이미지 및 비디오)의 전달을 지원합니다. 즉, 이미지나 비디오에 대해 게시된 URL 또는 포함 코드는 호스팅된 자산을 허용하는 모든 애플리케이션과 통합할 수 있습니다. 게시된 자산은 HTTP/2 프로토콜을 통해 전달됩니다. 이 전달 방법은 브라우저 및 서버의 통신 방식을 개선하여 모든 Dynamic Media 자산의 응답 및 로드 시간을 향상시킬 수 있습니다.

자세한 내용은 [HTTP/2 Delivery Of Content FAQ](/help/sites-administering/scene7-http2faq.md) 를 참조하십시오.
