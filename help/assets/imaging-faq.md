---
title: 스마트 이미징
description: 스마트 이미징은 각 사용자의 고유한 보기 특성을 활용하여 경험에 맞게 최적화된 이미지를 자동으로 제공하여 향상된 성능과 참여를 유도합니다.
uuid: c11e52ba-8d64-4dc5-b30a-fc10c2b704e5
contentOwner: Rick Brough
topic-tags: dynamic-media
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: bf8c6bbd-847d-43d7-9ff4-7231bfd8d107
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# 스마트 이미징 {#smart-imaging}

## 스마트 이미징이란 무엇입니까? {#what-is-smart-imaging}

스마트 이미징은 각 사용자의 고유한 보기 특성을 활용하여 경험에 맞게 최적화된 이미지를 자동으로 제공하여 향상된 성능과 참여를 유도합니다. 스마트 이미징은 기존 이미지 사전 설정과 연동되며 전달 마지막 순간에 지능적인 기능을 사용하여 브라우저 또는 네트워크 연결 속도에 따라 이미지 파일 크기를 더욱 줄일 수 있습니다.

고급 프리미엄 CDN 서비스와 완벽하게 통합되는 향상된 성능을 통해 지능적인 이미징 기능을 활용할 수 있습니다. 이 서비스는 서버, 네트워크 및 피어링 지점 간의 최적의 인터넷 경로를 찾으며 지연 시간이 가장 낮으며 인터넷상의 기본 경로보다 패킷 손실 비율이 낮습니다.

## 스마트 이미징의 주요 이점은 무엇입니까? {#what-are-the-key-benefits-of-smart-imaging}

스마트 이미징은 사용자 특성에 따라 이미지 파일 크기를 자동으로 최적화하여 향상된 이미지 전달 성능을 제공합니다. 이미지가 페이지 로드 시간의 대부분을 구성하므로 성능 향상은 높은 전환, 사이트에서 보낸 시간, 낮은 사이트 이탈률 등과 같은 비즈니스 KPI에 엄청난 영향을 미칠 수 있습니다. Adobe는 다양한 파일 포맷, 브라우저 및 품질(QLT) 설정에 대한 기본 이미지 전달 성능과 스마트 이미징의 성능을 비교했습니다. 전반적인 경우 기존 이미지 사전 설정 설정과 특정 최종 사용자 특성에 따라 22-47% 성능이 향상될 것으로 예상할 수 있습니다.

![image2017-11-14_133226](assets/image2017-11-14_133226.png)

## 스마트 이미징과 관련된 라이선스 비용이 있습니까? {#are-there-any-licensing-costs-associated-with-smart-imaging}

아니오. 스마트 이미징은 Dynamic Media Classic(Scene7) 또는 Dynamic Media의 기존 라이선스에 포함되어 있습니다. 이 새로운 기능을 이용하는 데 추가 비용이 들지 않습니다.

## 스마트 이미징은 어떻게 작동합니까? {#how-does-smart-imaging-work}

소비자가 처음으로 이미지를 요청하는 경우 Adobe는 사용자 특성을 확인하고 브라우저를 기반으로 적절한 이미지 형식으로 변환합니다. 또한 모든 형식 변환을 동시에 만들어 CDN에서 캐시합니다. 다른 브라우저의 소비자가 나중에 해당 이미지를 요청하면 올바른 이미지 형식이 CDN 캐시에서 바로 자동으로 전달됩니다. 이러한 형식 변환은 시각적 품질을 저하시키지 않는 손실 없는 방식으로 수행됩니다. 스마트 이미징은 다음과 같이 브라우저 기능을 기반으로 이미지를 다른 형식으로 자동으로 변환합니다.

* Chrome, Android 및 Opera와 같은 WebP 형식을 지원하는 브라우저를 위해 손실 없는 WebP로 자동 변환할 수 있습니다.
* Internet Explorer 9+와 같이 JPEGXR 형식을 지원하는 브라우저용 손실 없는 JPEG로 자동 변환합니다.
* Safari와 같은 JPEG2000 형식을 지원하는 브라우저를 위해 손실 없는 JPEG2000으로 자동 변환할 수 있습니다.
* 이러한 형식을 지원하지 않는 브라우저의 경우 원래 요청한 이미지 형식이 제공됩니다.

## 지원되는 이미지 포맷은 무엇입니까? {#what-image-formats-are-supported}

스마트 이미징에는 다음 이미지 형식이 지원됩니다.

* RGB JPEG
* RGB PNG
* RGB TIFF
* CMYK JPEG
* CMYK TIFF

## 이미 사용 중인 기존 이미지 사전 설정과 함께 스마트 이미징은 어떻게 작동합니까? {#how-does-smart-imaging-work-with-our-existing-image-presets-that-are-already-in-use}

스마트 이미징은 기존 이미지 사전 설정과 연동되므로 크기, 품질, 선명하게 하기 등과 같은 거의 모든 이미지 설정을 확인할 수 있습니다. 이미지 형식 또는 네트워크 연결 속도가 느린 경우 품질 설정이 변경됩니다. 포맷 변환의 경우 이미지 사전 설정 설정에 정의된 대로 전체 시각적 품질을 그대로 유지하면서 파일 크기가 작습니다.

예를 들어 이미지 사전 설정이 크기 500x500, 품질=85, 언샵 마스크=0.1,1,5로 정의되었다고 가정합니다. 사용자가 Chrome 브라우저에 있는 것을 감지하면 이미지는 500x500, quality=85 및 unsharp mask=0.1,1,5의 손실 없는 WebP 포맷으로 변환됩니다.

## URL, 이미지 사전 설정을 변경하거나 스마트 이미징을 위해 사이트에 새로운 코드를 배포해야 합니까? {#will-i-have-to-change-any-urls-image-presets-or-deploy-any-new-code-on-my-site-for-smart-imaging}

아니오. 스마트 이미징은 기존 이미지 URL 및 이미지 사전 설정과 완벽하게 호환됩니다. 또한 스마트 이미징은 브라우저, 대역폭, 장치 등 다양한 사용자 특성을 감지하기 위해 웹 사이트에 코드를 추가하지 않아도 됩니다. 이 모든 작업은 Adobe에서 자동으로 처리됩니다.

필요한 유일한 변경은 TTL(Time To Live) **[!UICONTROL 설정을 업데이트하는]** 것입니다. 이 설정은 CDN이 자산을 캐시하는 기간을 정의합니다. 스마트 이미징의 성능을 최대화하려면 TTL을 24시간 이상으로 설정하는 것이 좋습니다. 이 설정을 변경하려면:

* Dynamic Media Classic을 사용하는 경우 설정 > 응용 프로그램 **[!UICONTROL 설정 > 게시 설정 > 이미지 서버를 누릅니다]**. 기본 **[!UICONTROL 클라이언트 캐시 시간을 라이브]** 값으로 24 이상으로 설정합니다.

* Dynamic Media를 사용하는 경우, 지침에 따라 [Dynamic Media 이미지 설정](config-dynamic.md) 구성 만료 **[!UICONTROL 값을]** 24시간 이상으로 설정하십시오.

>[!NOTE]
>
>TTL &lt;= 1시간을 설정하면 스마트 이미징이 작동하지 않습니다.

## 스마트 이미징은 HTTPS를 사용하여 작동합니까? HTTP/2는 어떻습니까? {#does-smart-imaging-working-with-https-how-about-http}

스마트 이미징은 HTTP 또는 HTTPS를 통해 제공되는 이미지와 연동됩니다. 또한 HTTP/2에서도 작동합니다.

## 스마트 이미징을 사용할 수 있습니까? {#am-i-eligible-to-use-smart-imaging}

스마트 이미징을 사용하려면 회사의 AEM 계정에서 Dynamic Media Classic 또는 다이내믹 미디어가 다음 요구 사항을 충족해야 합니다.

* Adobe 번들 CDN(Content Delivery Network)을 라이선스의 일부로 사용할 수 있습니다.
* 일반 도메인(즉, `images.company.com` 또는 `mycompany.scene7.com``s7d1.scene7.com`)이 아닌 전용 도메인(즉, `s7d2.scene7.com`또는 `s7d13.scene7.com`)을 사용합니다.

   도메인을 찾으려면 회사 계정 또는 계정에 로그인합니다.

   설정 **[!UICONTROL > 애플리케이션 설정 > 일반 설정을 누릅니다]**. 게시된 서버 이름 레이블이 **[!UICONTROL 있는 필드를 찾습니다]**. 현재 일반 도메인을 사용 중인 경우 이 전환의 일부로 사용자 지정 도메인으로 이동을 요청할 수 있습니다.

* CMYK JPEG 이미지를 요청하지 마십시오. 처리 과정의 일부로 스마트 이미징은 CMYK JPEG 이미지를 RGB로 변환합니다. CMYK JPEG 이미지를 가져와야 하는 경우 스마트 이미징을 사용할 수 없습니다.

## 계정에 대한 스마트 이미징을 활성화하는 프로세스는 무엇입니까? {#what-is-the-process-for-enabling-smart-imaging-for-my-account}

스마트 이미징 사용을 요청해야 합니다.자동으로 활성화되지 않습니다.

1. 기술 지원 요청 시작(이메일:s7support@adobe.com).
1. 지원 요청에서 다음 정보를 제공합니다.

   1. 기본 연락처 이름, 이메일, 전화.
   1. 스마트 이미징에 사용할 수 있는 모든 도메인(즉, images.company.com 또는 mycompany.scene7.com)입니다.

      도메인을 찾으려면 회사 계정 또는 계정에 로그인합니다.

      설정 **[!UICONTROL > 애플리케이션 설정 > 일반 설정을 클릭합니다]**.

      게시된 서버 이름 레이블이 **[!UICONTROL 있는 필드를 찾습니다]**.
   1. Adobe를 통해 CDN을 사용하고 있고 직접적인 관계로 관리되지 않는지 확인합니다.
   1. 일반 도메인이 아닌 `images.company.com` 또는 `mycompany.scene7.com`같은 전용 도메인을 사용하고 있는지 `s7d1.scene7.com`확인합니다. `s7d2.scene7.com`예를 `s7d13.scene7.com`들어,

      도메인을 찾으려면 회사 계정 또는 계정에 로그인합니다.

      설정 **[!UICONTROL > 애플리케이션 설정 > 일반 설정을 클릭합니다]**.

      게시된 서버 이름 레이블이 **[!UICONTROL 있는 필드를 찾습니다]**. 현재 일반 Dynamic Media Classic 도메인을 사용 중인 경우 이 전환의 일부로 사용자 지정 도메인으로 이동을 요청할 수 있습니다.
   1. HTTP/2를 통해 작업해야 하는지 여부를 표시합니다.

1. 기술 지원에서 요청을 제출한 순서에 따라 스마트 이미징 고객 대기 목록에 추가합니다.
1. Adobe에서 요청을 처리할 준비가 되면 지원 담당자가 타겟 날짜를 조정하고 설정하기 위해 연락합니다.
1. 선택 사항:Adobe에서 새로운 기능을 프로덕션으로 푸시하기 전에 스테이징에서 스마트 이미징을 테스트할 수 있습니다.
1. 지원이 완료되면 알림 메시지가 표시됩니다.
1. 스마트 이미징의 성능을 최대화하려면 TTL(Time To Live)을 24시간 이상으로 설정하는 것이 좋습니다. TTL은 CDN이 자산을 캐시하는 기간을 정의합니다. 이 설정을 변경하려면:

   1. Dynamic Media Classic을 사용하는 경우 설정 > 응용 프로그램 **[!UICONTROL 설정 > 게시 설정 > 이미지 서버를 클릭합니다]**. 기본 **[!UICONTROL 클라이언트 캐시 시간을 라이브]** 값으로 24 이상으로 설정합니다.
   1. Dynamic Media를 사용하는 경우 [다음 지침을](config-dynamic.md)따르십시오. 만료 **[!UICONTROL 값을]** 24시간 이상 설정합니다.

## 언제 내 계정이 스마트 이미징으로 활성화될 예정입니까? {#when-can-i-expect-my-account-to-be-enabled-with-smart-imaging}

요청은 대기 목록에 따라 기술 지원 센터에서 수신하는 순서대로 처리됩니다.

>[!NOTE]
스마트 이미징을 활성화하면 캐시를 지우므로 리드 타임이 길어질 수 있습니다. 따라서 특정 시간에 일부 고객 전환만 처리할 수 있습니다.

## 고급 이미징 사용을 위해 전환하면 어떤 위험이 발생합니까? {#what-are-the-risks-with-switching-over-to-use-smart-imaging}

스마트 이미징으로 전환하면 AEM에서 Dynamic Media Classic 또는 Dynamic Media의 새로운 구성으로 이동해야 하므로 CDN에서 캐시를 지웁니다.

초기 전환 동안 캐시되지 않은 이미지는 캐시를 다시 다시 만들 때까지 Adobe의 원본 서버에 직접 도달합니다. 이러한 이유로 Adobe는 고객의 전환을 한 번에 처리할 계획이므로 당사의 요청을 가져올 때 허용되는 성능을 유지할 수 있습니다. 대부분의 고객의 경우 캐시는 1~2일 이내에 CDN에서 완전히 다시 구성됩니다.

## 스마트 이미징이 예상대로 작동하는지 확인하려면 어떻게 해야 합니까?  {#how-can-i-verify-whether-smart-imaging-is-working-as-expected}

1. 계정을 스마트 이미징으로 구성한 후 브라우저에서 Dynamic Media Classic(S7)/Dynamic Media 이미지 URL을 로드합니다.
1. 브라우저에서 보기 > 개발자 > **[!UICONTROL 개발자 도구를 클릭하여]** Chrome 개발자 창을 엽니다. 원하는 브라우저 개발자 툴을 선택할 수 있습니다.

1. 개발자 도구가 열려 있을 때 캐시가 비활성화되어 있는지 확인합니다.

   1. Windows에서 개발자 도구 창의 설정으로 이동한 다음 캐시 **[!UICONTROL 비활성화(장치 도구가 열려 있는 동안)]** 확인란을 선택합니다.
   1. Mac의 개발자 창의 네트워크 **[!UICONTROL 탭에서 캐시]** **[!UICONTROL 비활성화]** 를 선택합니다.

1. 초기 요청에서 이미지는 최적화되지 않습니다. 일반적으로 CDN 캐시에 없는 경우 최적화된 이미지를 반환하는 데 약 15분이 소요됩니다.
1. 컨텐츠 유형이 적절한 형식으로 변형됨을 확인합니다. 다음 스크린샷은 Chrome에서 PNG 이미지가 동적으로 WebP로 변환되는 것을 보여줍니다.
1. 다른 브라우저 및 사용자 조건에서 이 테스트를 반복합니다.

>[!NOTE]
일부 이미지는 변환되지 않습니다. 스마트한 이미징은 성능을 개선하기 위해 변환이 필요한지 여부를 결정합니다. 예상 성능 증가가 없는 경우 이미지가 변환되지 않는 경우도 있습니다.

![image2017-11-14_15398](assets/image2017-11-14_15398.png)

