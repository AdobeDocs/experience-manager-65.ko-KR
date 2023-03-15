---
title: Dynamic Media 에셋 전송
description: Dynamic Media 에셋 제공 방법 알아보기
uuid: 23eddf83-34f5-4aae-8b81-d1cd7a098a7e
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: e3b44330-d476-49c6-b7ba-079d0d60e500
docset: aem65
role: User, Admin
exl-id: 274af114-845a-46bd-b091-802cf589687a
feature: Asset Management,Renditions
source-git-commit: f4b7566abfa0a8dbb490baa0e849de6c355a3f06
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 25%

---

# Dynamic Media 에셋 전송{#delivering-dynamic-media-assets}

Dynamic Media 에셋(비디오와 이미지 모두)을 전달하는 방법은 웹 사이트가 구현되는 방식에 따라 다릅니다.

Dynamic Media에는 다음과 같은 몇 가지 옵션이 있습니다.

* 웹 사이트가 Adobe Experience Manager에서 호스팅되는 경우 Dynamic Media 에셋을 페이지에 바로 추가하려 합니다.
* 웹 사이트가 Experience Manager에 없는 경우 다음 중 하나를 선택할 수 있습니다.

   * 웹 사이트에 비디오 또는 이미지를 포함합니다.
   * 웹 애플리케이션에 URL 연결. 비디오 플레이어를 팝업 또는 모달 창으로 전달하려면 연결을 사용합니다.
   * 사이트가 응답형인 경우 다음을 수행할 수 있습니다. [최적화된 이미지 제공](/help/assets/responsive-site.md).

>[!NOTE]
>
>스마트 이미징은 기존 이미지 사전 설정에서 작동하며 마지막 전달 순간에 인텔리전스를 사용하여 브라우저 또는 네트워크 연결 속도에 따라 이미지 파일 크기를 더 줄입니다. 다음을 참조하십시오 [스마트 이미징](/help/assets/imaging-faq.md) 추가 정보.

자세한 내용은 다음 항목을 참조하십시오.

* [웹 페이지에 Dynamic Media 자산 추가](/help/assets/adding-dynamic-media-assets-to-pages.md)
* [웹 페이지에 비디오 또는 이미지 뷰어 포함](/help/assets/embed-code.md)
* [Dynamic Media의 핫링크 보호 활성화](/help/assets/hotlink-protection.md)
* [웹 애플리케이션에 URL 연결](/help/assets/linking-urls-to-yourwebapplication.md)
* [반응형 사이트에 최적화된 이미지 제공](/help/assets/responsive-site.md)
* [컨텐츠의 HTTP2 전달](/help/assets/http2.md)
* [Dynamic Media Classic을 통해 CDN 캐시 무효화](/help/assets/invalidate-cdn-cache-dm-classic.md)
* [규칙 세트를 사용하여 URL 변환](/help/assets/using-rulesets-to-transform-urls.md)


## Dynamic Media 자산의 HTTP/2 전달 {#http-delivery-of-dynamic-media-assets}

이제 Experience Manager은 HTTP/2를 통해 모든 Dynamic Media 컨텐츠(이미지 및 비디오)의 전달을 지원합니다. 즉, 이미지 또는 비디오에 대한 게시된 URL 또는 포함 코드를 호스팅된 에셋을 허용하는 모든 애플리케이션과 통합할 수 있습니다. 그런 다음 게시된 에셋은 HTTP/2 프로토콜을 통해 전달됩니다. 이 전달 방법은 브라우저와 서버의 통신 방식을 개선하여 모든 Dynamic Media 에셋의 응답 및 로드 시간을 향상시킵니다.

자세한 내용은 다음을 참조하십시오. [콘텐츠의 HTTP/2 전달 FAQ](/help/sites-administering/scene7-http2faq.md).
