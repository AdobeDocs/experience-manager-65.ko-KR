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
source-git-commit: 7daf89f7e69d3e2e938780ff98fd2df46723e708

---


# 스마트 이미징 {#smart-imaging}

## &quot;스마트 이미징&quot;이란 무엇입니까? {#what-is-smart-imaging}

Smart Imaging 기술은 Adobe Sensei AI 기능을 활용하고 기존 &quot;이미지 사전 설정&quot;과 연동하여 클라이언트 브라우저 기능을 기반으로 이미지 포맷, 크기 및 품질을 자동으로 최적화하여 이미지 전달 성능을 향상시킵니다.

스마트 이미징은 Adobe의 동급 최강의 프리미엄 CDN 서비스와 완벽하게 통합됨으로써 향상된 성능을 제공합니다. 이 서비스는 서버, 네트워크 및 피어링 지점 간의 최적의 인터넷 경로를 찾으며 지연 시간이 가장 낮으며 인터넷상의 기본 경로보다 패킷 손실 비율이 낮습니다.

다음 이미지 자산 예는 추가된 스마트 이미징 최적화를 보여줍니다.

| Image<br>(URL) | 썸네일 | 크기<br> (JPEG) | 크기(WebP)<br> (스마트 이미징 포함) | % 감소 |
|---|---|---|---|---|
| [이미지 1](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_6?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture1](/help/assets/assets-dm/picture1.png) | 73.75KB | 45.92KB | 38% |
| [이미지 2](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_3?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture2](/help/assets/assets-dm/picture2.png) | 191KB | 70.66KB | 63% |
| [이미지 3](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_2?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture3](/help/assets/assets-dm/picture3.png) | 96.64KB | 39.44KB | 59% |
| [이미지 4](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_1?hei=500&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture4](/help/assets/assets-dm/picture4.png) | 315.80KB | 178.19KB | 44% |
|  |  |  |  | 평균 = 51% |

위와 마찬가지로 Adobe는 라이브 고객 사이트에서 7009 URL을 사용하여 테스트를 실시했으며 스마트 이미징 기능 덕분에 JPEG에 대한 파일 크기 최적화와 WebP 포맷의 PNG에 대한 파일 크기 최적화를 평균 38% 더 향상시킬 수 있었습니다.

## 최신 스마트 이미징의 주요 이점은 무엇입니까? {#what-are-the-key-benefits-of-smart-imaging}

이미지가 페이지 로드 시간의 대부분을 구성하므로 성능 향상은 높은 전환, 사이트에서 보낸 시간, 낮은 사이트 이탈률 등 비즈니스 KPI에 엄청난 영향을 미칠 수 있습니다.

고급 이미징 최신 버전의 향상된 기능:

* 런타임 시 최적화된 컨텐츠를 즉시 제공합니다.
* Adobe Sensei 기술을 사용하여 이미지 요청에 지정된 품질(qlt)에 따라 변환합니다.
* &quot;bfc&quot; URL 매개 변수를 사용하여 스마트 이미징을 끌 수 있습니다.
* TTL(Time To Live) 독립적입니다. 이전에는, 스마트 이미징이 작동하기 위해서는 최소 TTL이 12시간이었다.
* 이전에는 원본 이미지와 파생 이미지가 모두 캐시되었으며 캐시를 무효화하는 2단계 프로세스였습니다. 최신 Smart Imaging에서는 파생물만 캐시되어 단일 단계 캐시 무효화 프로세스를 허용합니다.
* 규칙 세트에서 사용자 지정 헤더를 사용하는 고객(예: &quot;타이밍 [출처 허용&quot;, &quot;X-Robot&quot;, 이미지 응답에 사용자 지정 헤더 값 추가|Dynamic Media Classic](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/add-custom-header-val-image.html))은 이전 버전의 Smart Imaging과 달리 헤더가 차단되지 않으므로 최신 스마트 이미징 기능을 활용할 수 있습니다.

## 스마트 이미징과 관련된 라이선스 비용이 있습니까? {#are-there-any-licensing-costs-associated-with-smart-imaging}

아니오. 스마트 이미징은 Dynamic Media Classic(Scene7) 또는 AEM Dynamic Media(On Prem, AMS 및 AEM을 클라우드 서비스로 사용)의 기존 라이선스에 포함되어 있습니다.

>[!NOTE]
>
>Dynamic Media - 하이브리드 고객은 스마트 이미징을 사용할 수 없습니다.


## 스마트 이미징은 어떻게 작동합니까? {#how-does-smart-imaging-work}

Smart Imaging은 Adobe Sensei를 사용하여 브라우저 기능을 기반으로 이미지를 가장 적합한 형식, 크기 및 품질로 자동 변환합니다.

* Chrome, Firefox, Microsoft Edge, Android 및 Opera와 같은 브라우저의 경우 WebP로 자동 변환할 수 있습니다.
* Safari와 같은 브라우저의 경우 JPEG2000으로 자동 변환됩니다.
* Internet Explorer 9+와 같은 브라우저의 경우 자동으로 JPEG로 변환할 수 있습니다.
* 이러한 형식을 지원하지 않는 브라우저의 경우 원래 요청한 이미지 형식이 제공됩니다.

원본 이미지 크기가 스마트 이미징에서 만든 크기보다 작은 경우 원본 이미지가 제공됩니다.

## 지원되는 이미지 포맷은 무엇입니까? {#what-image-formats-are-supported}

스마트 이미징에 대해 지원되는 이미지 형식은 다음과 같습니다.
* JPEG
* PNG

<!-- For any other format mentioned in a URL, you should explicity turn off Smart Imaging.  Append modifier `bfc=off` to the URL for file formats other than JPEG and PNG. You can accomplish this by using either one of the following methods:

* Use a ruleset if the `fmt` modifier is mentioned in the URL. 
* Append in URL modifiers field of the presets concerned.

Adobe is working on a permanent fix that does not require you to append `bfc=off` for `fmt !=JPEG` or `fmt !=PNG`. This topic will be updated after the fix is delivered. -->

## 이미 사용 중인 기존 이미지 사전 설정과 함께 스마트 이미징은 어떻게 작동합니까? {#how-does-smart-imaging-work-with-our-existing-image-presets-that-are-already-in-use}

스마트 이미징은 기존의 &quot;이미지 사전 설정&quot;과 연동되며 요청된 파일 형식이 JPEG 또는 PNG인 경우 품질(qlt) 및 포맷(fmt)을 제외하고 모든 이미지 설정을 확인합니다. 포맷 변환의 경우 이미지 사전 설정 설정에 정의된 대로 전체 시각적 품질을 그대로 유지하면서 파일 크기가 작습니다. 원본 이미지 크기가 스마트 이미징에서 만든 크기보다 작은 경우 원본 이미지가 제공됩니다.

<!-- In addition, if your image presets are used to return `fmt !=JPEG` or `fmt !=PNG`, be sure append `bfc=off` in the preset modifier field to return the requested file format. -->

## URL, 이미지 사전 설정을 변경하거나 Smart Imaging을 위해 내 사이트에 새로운 코드를 배포해야 합니까? {#will-i-have-to-change-any-urls-image-presets-or-deploy-any-new-code-on-my-site-for-smart-imaging}

아니오. 스마트 이미징은 기존 이미지 URL 및 이미지 사전 설정과 완벽하게 호환됩니다. 또한 Smart Imaging에서는 사용자의 브라우저를 감지하기 위해 웹 사이트에 코드를 추가할 필요가 없습니다. 이 모든 것이 자동으로 처리됩니다.

<!-- As mentioned earlier, Smart Imaging supports only JPEG and PNG image formats. For other formats, you need to append the `bfc=off` modifier to the URL as described earlier. -->

또한 스마트 [이미징을 사용할 수 있습니까?를 참조하십시오.](#am-i-eligible-to-use-smart-imaging) to understand for Smart Imaging.

## Smart Mmaging은 HTTPS를 사용하여 작동합니까? HTTP/2는 어떻습니까? {#does-smart-imaging-working-with-https-how-about-http}

스마트 이미징은 HTTP 또는 HTTPS를 통해 제공되는 이미지와 연동됩니다. 또한 HTTP/2에서도 작동합니다.

## 스마트 이미징을 사용할 수 있습니까? {#am-i-eligible-to-use-smart-imaging}

스마트 이미징을 사용하려면 회사의 AEM 계정에서 Dynamic Media Classic 또는 다이내믹 미디어가 다음 요구 사항을 충족해야 합니다.

* Adobe 번들 CDN(Content Delivery Network)을 라이선스의 일부로 사용할 수 있습니다.
* 일반 도메인(예: `images.company.com` , `mycompany.scene7.com`또는 `s7d1.scene7.com`)이 아닌 전용 도메인(예: `s7d2.scene7.com`또는 `s7d13.scene7.com`)을 사용합니다.

도메인을 찾으려면 회사 계정 또는 계정에 로그인합니다.

설정 **[!UICONTROL > 애플리케이션 설정 > 일반 설정을 누릅니다]**. 게시된 서버 이름 레이블이 **[!UICONTROL 있는 필드를 찾습니다]**. 현재 일반 도메인을 사용 중인 경우 기술 지원 티켓을 제출할 때 이 전환의 일부로 사용자 지정 도메인으로 이동을 요청할 수 있습니다.

Dynamic Media 라이선스를 사용하면 첫 번째 사용자 정의 도메인을 추가 비용이 들지 않습니다.

## 계정에 대해 스마트 이미징을 활성화하는 프로세스는 무엇입니까? {#what-is-the-process-for-enabling-smart-imaging-for-my-account}

스마트 이미징 사용을 요청해야 합니다.자동으로 활성화되지 않습니다.

1. 기술 지원 요청 시작(이메일: `s7support@adobe.com`).
1. 지원 요청에서 다음 정보를 제공합니다.

   1. 기본 연락처 이름, 이메일, 전화.
   1. 스마트 이미징을 사용하도록 설정할 모든 도메인( `images.company.com` 또는 `mycompany.scene7.com`).

      도메인을 찾으려면 회사 계정 또는 계정에 로그인합니다.

      설정 **[!UICONTROL > 애플리케이션 설정 > 일반 설정을 클릭합니다]**.

      게시된 서버 이름 레이블이 **[!UICONTROL 있는 필드를 찾습니다]**.
   1. Adobe를 통해 CDN을 사용하고 있고 직접적인 관계로 관리되지 않는지 확인합니다.
   1. 일반 도메인이 아닌 `images.company.com` 또는 `mycompany.scene7.com`같은 전용 도메인을 사용하고 있는지 `s7d1.scene7.com`확인합니다. `s7d2.scene7.com`예를 `s7d13.scene7.com`들어,

      도메인을 찾으려면 회사 계정 또는 계정에 로그인합니다.

      설정 **[!UICONTROL > 애플리케이션 설정 > 일반 설정을 클릭합니다]**.

      게시된 서버 이름 레이블이 **[!UICONTROL 있는 필드를 찾습니다]**. 현재 일반 Dynamic Media Classic 도메인을 사용 중인 경우 이 전환의 일부로 사용자 지정 도메인으로 이동을 요청할 수 있습니다.
   1. HTTP/2를 통해 작업하는 경우에도 이 기능이 필요한지 여부를 표시합니다.

1. 기술 지원에서 요청을 제출한 순서에 따라 스마트 이미징 고객 대기 목록에 추가합니다.
1. Adobe에서 요청을 처리할 준비가 되면 지원 담당자가 타겟 날짜를 조정하고 설정하기 위해 연락합니다.
1. **선택 사항**:Adobe에서 새로운 기능을 프로덕션으로 푸시하기 전에 스테이징에서 스마트 이미징을 테스트할 수 있습니다.
1. 지원이 완료되면 알림 메시지가 표시됩니다.
1. 스마트 이미징의 성능 향상을 최대화하려면 TTL(Time To Live)을 24시간 이상으로 설정하는 것이 좋습니다. TTL은 CDN이 자산을 캐시하는 기간을 정의합니다. 이 설정을 변경하려면:

   1. Dynamic Media Classic을 사용하는 경우 설정 > 응용 프로그램 **[!UICONTROL 설정 > 게시 설정 > 이미지 서버를 클릭합니다]**. 기본 **[!UICONTROL 클라이언트 캐시 시간을 라이브]** 값으로 24 이상으로 설정합니다.
   1. Dynamic Media를 사용하는 경우 [다음 지침을](config-dynamic.md)따르십시오. 만료 **[!UICONTROL 값을]** 24시간 이상 설정합니다.

## Smart Imaging을 사용하여 계정을 언제 활성화할 수 있습니까? {#when-can-i-expect-my-account-to-be-enabled-with-smart-imaging}

요청은 대기 목록에 따라 기술 지원 센터에서 수신하는 순서대로 처리됩니다.

>[!NOTE]
Smart Imaging을 활성화하면 Adobe가 캐시를 지우게 되므로 리드 타임이 길어질 수 있습니다. 따라서 특정 시간에 일부 고객 전환만 처리할 수 있습니다.

## 스마트 이미징 사용을 위해 전환하면 어떤 위험이 발생합니까? {#what-are-the-risks-with-switching-over-to-use-smart-imaging}

고객 웹 페이지에 대한 위험은 없습니다. 그러나 Smart Imaging으로 전환하는 경우 AEM에서 Dynamic Media Classic 또는 Dynamic Media의 새로운 구성으로 이동해야 하므로 CDN에서 캐시를 지웁니다.

초기 전환 동안 캐시되지 않은 이미지는 캐시를 다시 다시 만들 때까지 Adobe의 원본 서버에 직접 도달합니다. 이러한 이유로 Adobe는 고객의 전환을 한 번에 처리할 계획이므로 당사의 요청을 가져올 때 허용되는 성능을 유지할 수 있습니다. 대부분의 고객의 경우 캐시는 1~2일 이내에 CDN에서 완전히 다시 구성됩니다.

## 스마트 이미징이 예상대로 작동하는지 확인하려면 어떻게 해야 합니까?  {#how-can-i-verify-whether-smart-imaging-is-working-as-expected}

1. 계정이 스마트 이미징으로 구성된 후 브라우저에서 Dynamic Media Classic(Scene7)/Dynamic Media 이미지 URL을 로드합니다.
1. 브라우저에서 보기 > 개발자 > **[!UICONTROL 개발자 도구를 클릭하여]** Chrome 개발자 창을 엽니다. 원하는 브라우저 개발자 도구를 선택할 수 있습니다.

1. 개발자 도구가 열려 있을 때 캐시가 비활성화되어 있는지 확인합니다.

   * Windows에서 개발자 도구 창의 설정으로 이동한 다음 캐시 **[!UICONTROL 비활성화(장치 도구가 열려 있는 동안)]** 확인란을 선택합니다.
   * Mac - 개발자 창의 네트워크 **[!UICONTROL 탭에서 캐시]** **[!UICONTROL 비활성화 를 선택합니다]** .

1. 컨텐츠 유형이 적절한 형식으로 변형됨을 확인합니다. 다음 스크린샷은 Chrome에서 WebP로 동적으로 변환되는 PNG 이미지를 보여줍니다.
1. 다른 브라우저 및 사용자 조건에서 이 테스트를 반복합니다.

>[!NOTE]
일부 이미지는 변환되지 않습니다. 스마트 이미징은 성능 향상을 위해 변환이 필요한지 여부를 결정합니다. 경우에 따라 성능 증가가 예상되지 않거나 형식이 JPEG 또는 PNG가 아닌 이미지는 변환되지 않습니다.

![image2017-11-14_15398](assets/image2017-11-14_15398.png)

## 요청에 따라 스마트 이미징을 끌 수 있습니까? {#turning-off-smart-imaging}

예. URL에 수정자를 추가하여 스마트 이미지를 끌 `bfc=off` 수 있습니다.

## 어떤 &quot;조정&quot;을 사용할 수 있습니까? 정의할 수 있는 설정 또는 동작이 있습니까? (#tuning-settings)

현재, 선택적으로 스마트 이미징을 활성화하거나 비활성화할 수 있습니다. 다른 튜닝을 사용할 수 없습니다.

## Smart Imaging이 품질 설정을 관리하는 경우 설정할 수 있는 최소 및 최대 수가 있습니까? 예를 들어 &quot;60 미만&quot;과 &quot;80 미만 품질&quot;을 설정할 수 있습니까? (#minimum-maximum)

현재 스마트 이미징에는 이러한 프로비저닝 기능이 없습니다.

## 경우에 따라 JPEG 이미지는 WebP 이미지 대신 Chrome으로 반환됩니다. 왜 그런 일이 생기죠? (#jpeg-webp)

스마트 이미징은 전환이 유익한지 여부를 결정합니다. 변환 결과 파일 크기가 비슷한 품질과 더 작아진 경우에만 새 이미지를 반환합니다.
