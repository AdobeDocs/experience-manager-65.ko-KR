---
title: 스마트 이미징
description: 스마트 이미징은 각 사용자의 고유한 보기 특성을 적용하여 환경에 최적화된 적합한 이미지를 자동으로 제공하므로 향상된 성능과 참여를 제공합니다.
uuid: c11e52ba-8d64-4dc5-b30a-fc10c2b704e5
contentOwner: Rick Brough
topic-tags: dynamic-media
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: bf8c6bbd-847d-43d7-9ff4-7231bfd8d107
feature: 자산 관리
role: Business Practitioner, Administrator
exl-id: e427d4ee-d5c8-421b-9739-f3cf2de36e41
source-git-commit: 8d27457ad88cb84e670e78bab4c40da36fcfc629
workflow-type: tm+mt
source-wordcount: '1912'
ht-degree: 1%

---


# 스마트 이미징 {#smart-imaging}

## 스마트 이미징이란 무엇입니까?{#what-is-smart-imaging}

스마트 이미징 기술은 Adobe Sensei AI 기능을 적용하고 기존 &quot;이미지 사전 설정&quot;과 함께 작동하여 클라이언트 브라우저 기능을 기반으로 이미지 형식, 크기 및 품질을 자동으로 최적화하여 이미지 전달 성능을 향상시킵니다.

>[!NOTE]
>
>이 기능을 사용하려면 Adobe Experience Manager Dynamic Media과 함께 번들로 제공되는 기본 CDN(Content Delivery Network)을 사용해야 합니다. 다른 모든 사용자 지정 CDN은 이 기능에서 지원되지 않습니다.

스마트 이미징은 또한 Adobe의 동급 최강의 프리미엄 CDN 서비스와 완전히 통합되는 향상된 성능 증대의 이점을 제공합니다. 이 서비스는 서버, 네트워크 및 피어링 지점 간의 최적의 인터넷 경로를 찾습니다. 인터넷에서 기본 경로를 사용하는 대신 지연 시간이 가장 짧고 패킷 손실률이 가장 낮은 경로를 찾습니다.

다음 이미지 자산 예는 추가된 스마트 이미징 최적화를 보여줍니다.

| 이미지<br>(URL) | 썸네일 | 크기<br> (JPEG) | 크기(WebP)<br>(스마트 이미징 포함) | % 감소 |
|---|---|---|---|---|
| [이미지 1](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_6?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![그림1](/help/assets/assets-dm/picture1.png) | 73.75KB | 45.92KB | 38% |
| [이미지 2](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_3?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![그림2](/help/assets/assets-dm/picture2.png) | 191KB | 70.66KB | 63% |
| [이미지 3](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_2?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![그림3](/help/assets/assets-dm/picture3.png) | 96.64KB | 39.44KB | 59% |
| [이미지 4](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_1?hei=500&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![그림 4](/help/assets/assets-dm/picture4.png) | 315.80KB | 178.19KB | 44% |
|  |  |  |  | 평균 = 51% |

위와 유사하게, Adobe은 라이브 고객 사이트에서 7009 URL을 사용하는 테스트도 실행했습니다. JPEG에 대해 평균 38%의 파일 크기 최적화를 수행할 수 있었습니다. WebP 포맷의 PNG의 경우 평균 31% 더 많은 파일 크기 최적화를 수행할 수 있었습니다. 스마트 이미징의 기능 때문에 이러한 유형의 최적화가 가능합니다.

## 최신 스마트 이미징의 주요 이점은 무엇입니까?{#what-are-the-key-benefits-of-smart-imaging}

이미지가 페이지 로드 시간의 대부분을 구성하므로 성능 향상은 높은 전환, 사이트에서 보낸 시간, 낮은 사이트 바운스 비율 등과 같이 비즈니스에 큰 영향을 줄 수 있습니다.

최신 버전의 스마트 이미징 개선 사항:

* 최신 스마트 이미징을 활용하여 웹 페이지의 Google SEO 등급을 개선했습니다.
* 최적화된 컨텐츠를 런타임 시 즉시 제공합니다.
* Adobe Sensei 기술을 사용하여 이미지 요청에 지정된 품질(qlt)에 따라 변환합니다.
* 스마트 이미징은 &quot;bfc&quot; URL 매개 변수를 사용하여 해제할 수 있습니다.
* TTL(Time To Live)과 독립적입니다. 이전에는 스마트 이미징이 작동하려면 최소 TTL이 12시간이었습니다.
* 이전에는 원본 이미지와 파생 이미지가 모두 캐시되었으며 캐시를 무효화하는 2단계 프로세스였습니다. 최신 Smart Imaging에서는 파생자만 캐시되므로 단일 단계 캐시 무효화 프로세스를 허용합니다.
* 규칙 세트에 사용자 지정 헤더를 사용하는 고객은 이전 버전의 Smart Imaging과 달리 이러한 헤더가 차단되지 않으므로 최신 Smart Imaging을 활용할 수 있습니다. 예를 들어, [이미지 응답에 사용자 지정 헤더 값을 추가하는 경우 &quot;Timing Allow Origin&quot;, &quot;X-Robot&quot;이 권장됩니다|Dynamic Media Classic](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/add-custom-header-val-image.html).

## 스마트 이미징과 관련된 라이센스 비용이 있습니까?{#are-there-any-licensing-costs-associated-with-smart-imaging}

아니오. 스마트 이미징은 Dynamic Media Classic 또는 Adobe Experience Manager - Dynamic Media(온-프레미스, AMS 및 Adobe Experience Manager as a Cloud Service)의 기존 라이센스에 포함되어 있습니다.

>[!NOTE]
>
>Dynamic Media - 하이브리드 고객은 스마트 이미징을 사용할 수 없습니다.

## 스마트 이미징은 어떻게 작동합니까?{#how-does-smart-imaging-work}

소비자가 이미지를 요청하면 스마트 이미징은 사용자 특성을 확인하고 사용 중인 브라우저를 기반으로 적절한 이미지 형식으로 변환합니다. 이러한 형식 변환은 시각적 품질을 저하시키지 않는 방식으로 수행됩니다. 스마트 이미징은 다음과 같은 방식으로 브라우저 기능에 따라 이미지를 다른 형식으로 자동으로 변환합니다.

<!--   * Safari 14.0 +
    * Safari 14 only with iOS 14.0 and above and macOS BigSur and above -->

* 다음 브라우저의 경우 자동으로 WebP로 변환합니다.
   * Chrome
   * Firefox
   * Microsoft® Edge
   * Safari(iOS, macOS, iPadOS에서), WebP를 지원하는 브라우저 및 OS 버전 제공
   * Android™
   * Opera
* 기존 브라우저는 다음을 지원합니다.

   | 브라우저 | 브라우저/OS 버전 | 형식 |
   | --- | --- | --- |
   | Safari | iOS/iPad 14.0 또는 macOS BigSur 이전 | JPEG2000 |
   | Edge | 18보다 이전 | JPEGXR |
   | Internet Explorer | 9+ | JPEGXR |
* 이러한 형식을 지원하지 않는 브라우저의 경우 원래 요청한 이미지 형식이 제공됩니다.

원본 이미지 크기가 스마트 이미징에서 만드는 이미지 크기보다 작으면 원본 이미지가 제공됩니다.

## 지원되는 이미지 형식은 무엇입니까?{#what-image-formats-are-supported}

스마트 이미징에 대해 다음 이미지 형식이 지원됩니다.

* JPEG
* PNG

<!-- CQDOC-15846 For any other format mentioned in a URL, you should explicity turn off Smart Imaging.  Append modifier `bfc=off` to the URL for file formats other than JPEG and PNG. You can accomplish this by using either one of the following methods:

* Use a ruleset if the `fmt` modifier is mentioned in the URL. 
* Append in URL modifiers field of the presets concerned.

Adobe is working on a permanent fix that does not require you to append `bfc=off` for `fmt !=JPEG` or `fmt !=PNG`. This topic will be updated after the fix is delivered. -->

## 이미 사용 중인 기존 이미지 사전 설정에서 스마트 이미징은 어떻게 작동합니까?{#how-does-smart-imaging-work-with-our-existing-image-presets-that-are-already-in-use}

스마트 이미징은 기존 &quot;이미지 사전 설정&quot;에서 작동하며 요청된 파일 형식이 JPEG 또는 PNG인 경우 품질(`qlt`) 및 형식(`fmt`)을 제외한 모든 이미지 설정을 준수합니다. 형식 변환을 위해 스마트 이미징은 이미지 사전 설정 설정에 정의된 대로 전체 시각적 품질을 유지하지만 더 작은 파일 크기로 유지합니다. 원본 이미지 크기가 스마트 이미징에서 만드는 이미지 크기보다 작은 경우 원본 이미지가 제공됩니다.

<!-- CQDOC-15846 In addition, if your image presets are used to return `fmt !=JPEG` or `fmt !=PNG`, be sure append `bfc=off` in the preset modifier field to return the requested file format. -->

## URL, 이미지 사전 설정을 변경하거나 스마트 이미징을 위해 내 사이트에 새 코드를 배포해야 합니까?{#will-i-have-to-change-any-urls-image-presets-or-deploy-any-new-code-on-my-site-for-smart-imaging}

기존 사용자 지정 도메인에서 스마트 이미징을 구성하는 경우 스마트 이미징이 기존 이미지 URL 및 이미지 사전 설정과 원활하게 작동합니다. 또한 스마트 이미징에서는 사용자의 브라우저를 감지하기 위해 웹 사이트에 코드를 추가할 필요가 없습니다. 모두 자동으로 처리됩니다.

스마트 이미징을 사용하도록 새 사용자 지정 도메인을 구성해야 하는 경우 이 사용자 지정 도메인을 반영하도록 URL을 업데이트해야 합니다.

스마트 이미징의 사전 요구 사항을 이해하려면 [스마트 이미징을 사용할 수 있습니까?](#am-i-eligible-to-use-smart-imaging) 를 참조하십시오.

<!-- No. Smart Imaging works seamlessly with your existing image URLs and image presets. In addition, Smart Imaging does not require you to add any code on your website to detect a user's browser. All of this is handled automatically. -->

<!-- As mentioned earlier, Smart Imaging supports only JPEG and PNG image formats. For other formats, you need to append the `bfc=off` modifier to the URL as described earlier. -->

## 스마트 이미징이 HTTPS에서 작동합니까? HTTP/2는 어떻습니까?{#does-smart-imaging-working-with-https-how-about-http}

스마트 이미징은 HTTP 또는 HTTPS를 통해 전달된 이미지에서 작동합니다. 또한 HTTP/2에서도 작동합니다.

## 스마트 이미징을 사용할 수 있습니까?{#am-i-eligible-to-use-smart-imaging}

스마트 이미징을 사용하려면 회사의 Dynamic Media Classic 또는 Experience Manager 계정의 Dynamic Media이 다음 요구 사항을 충족해야 합니다.

* Adobe 번들 CDN(Content Delivery Network)을 라이센스의 일부로 사용합니다.
* 일반 도메인(예: `s7d1.scene7.com`, `s7d2.scene7.com` 또는 `s7d13.scene7.com`)이 아닌 전용 도메인(예: `images.company.com` 또는 `mycompany.scene7.com`)을 사용하십시오.

도메인을 찾으려면 [Dynamic Media Classic 데스크탑 응용 프로그램](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)을 연 다음 회사 계정 또는 계정에 로그인합니다.

**[!UICONTROL 설정 > 응용 프로그램 설정 > 일반 설정]**&#x200B;을 누릅니다. **[!UICONTROL 게시된 서버 이름]**&#x200B;이라는 레이블이 지정된 필드를 찾습니다. 현재 일반 도메인을 사용 중인 경우 기술 지원 티켓을 제출할 때 이 전환의 일부로 고유한 사용자 지정 도메인으로 이동을 요청할 수 있습니다.

첫 번째 사용자 지정 도메인은 Dynamic Media 라이센스를 통해 추가 비용이 들지 않습니다.

## 내 계정에 대해 스마트 이미징을 활성화하는 프로세스는 무엇입니까?{#what-is-the-process-for-enabling-smart-imaging-for-my-account}

스마트 이미징 사용 요청을 시작합니다.자동으로 활성화되지 않습니다.

1. [Admin Console을 사용하여 지원 사례를 만듭니다.](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)
1. 지원 사례에 다음 정보를 제공하십시오.

   1. 기본 연락처 이름, 이메일, 전화
   1. 스마트 이미징에 대해 활성화할 모든 도메인(즉, `images.company.com` 또는 `mycompany.scene7.com`)입니다.

      도메인을 찾으려면 [Dynamic Media Classic 데스크탑 응용 프로그램](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)을 연 다음 회사 계정 또는 계정에 로그인합니다.

      **[!UICONTROL 설정 > 응용 프로그램 설정 > 일반 설정]**&#x200B;을 클릭합니다.

      **[!UICONTROL 게시된 서버 이름.]** 필드를 찾습니다.
   1. Adobe을 통해 CDN을 사용하고 있으며 직접 관계로 관리하지 않는지 확인합니다.
   1. `images.company.com` 또는 `mycompany.scene7.com` 등의 전용 도메인을 사용하고 있고 `s7d1.scene7.com`, `s7d2.scene7.com`, `s7d13.scene7.com` 등의 일반 도메인이 아닌지 확인합니다.

      도메인을 찾으려면 [Dynamic Media Classic 데스크탑 응용 프로그램](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)을 연 다음 회사 계정 또는 계정에 로그인합니다.

      **[!UICONTROL 설정 > 응용 프로그램 설정 > 일반 설정]**&#x200B;을 클릭합니다.

      **[!UICONTROL 게시된 서버 이름]**&#x200B;이라는 레이블이 지정된 필드를 찾습니다. 현재 일반 Dynamic Media Classic 도메인을 사용 중인 경우, 이 전환의 일부로 고유한 사용자 지정 도메인으로 이동을 요청할 수 있습니다.
   1. HTTP/2에서 작업하기 위해 스마트 이미징이 필요한지 여부를 나타냅니다.

1. Adobe 고객 지원 팀에서는 요청이 제출된 순서에 따라 스마트 이미징 고객 대기 목록에 추가합니다.
1. Adobe이 요청을 처리할 준비가 되면 지원 담당자가 대상 날짜를 조정하고 설정해야 합니다.
1. **선택** 사항:Adobe이 새 기능을 프로덕션에 푸시하기 전에 스테이징에서 스마트 이미징을 선택적으로 테스트할 수 있습니다.
1. 고객 지원 센터에서 이 작업을 완료하면 알림을 받게 됩니다.
1. 스마트 이미징의 성능 향상을 극대화하려면 Adobe에서 TTL(Time To Live)을 24시간 이상으로 설정하는 것이 좋습니다. TTL은 CDN에 의해 자산이 캐시되는 기간을 정의합니다. 이 설정을 변경하려면 다음을 수행하십시오.

   1. Dynamic Media Classic을 사용하는 경우 **[!UICONTROL 설정 > 애플리케이션 설정 > 게시 설정 > 이미지 서버]**&#x200B;를 클릭합니다. **[!UICONTROL 기본 클라이언트 캐시 시간을 Live]** 값으로 24 이상으로 설정합니다.
   1. Dynamic Media을 사용하는 경우 [다음 지침](config-dynamic.md)을 따르십시오. **[!UICONTROL 만료]** 값을 24시간 이상 설정합니다.

## 언제 내 계정이 스마트 이미징으로 활성화될 수 있습니까?{#when-can-i-expect-my-account-to-be-enabled-with-smart-imaging}

요청은 대기 목록에 따라 고객 지원에서 수신하는 순서로 처리됩니다.

>[!NOTE]
>
>스마트 이미징을 활성화하면 Adobe이 캐시를 지우므로 리드 타임이 오래 걸릴 수 있습니다. 따라서 지정된 시간에 몇 개의 고객 전환만 처리할 수 있습니다.

## 스마트 이미징을 사용하도록 전환하면 어떤 위험이 있습니까?{#what-are-the-risks-with-switching-over-to-use-smart-imaging}

고객 웹 페이지에는 위험이 없습니다. 하지만 스마트 이미징으로 전환하면 Experience Manager 시 Dynamic Media Classic 또는 Dynamic Media의 새 구성으로 이동해야 하므로 CDN에서 캐시를 지웁니다.

초기 전환 중에 캐싱되지 않은 이미지는 캐시가 다시 빌드될 때까지 Adobe의 원본 서버에 직접 연결됩니다. 따라서 Adobe은 한 번에 몇 개의 고객 전환을 처리하여 오리진에서 요청을 가져올 때 허용 가능한 성능이 유지되도록 할 계획입니다. 대부분의 고객의 경우 캐시가 1~2일 내에 CDN에서 다시 완전히 빌드됩니다.

## 스마트 이미징이 예상대로 작동하는지 확인하려면 어떻게 해야 합니까?{#how-can-i-verify-whether-smart-imaging-is-working-as-expected}

1. 계정이 스마트 이미징으로 구성된 후 브라우저에서 Dynamic Media Classic 또는 Adobe Experience Manager - Dynamic Media 이미지 URL을 로드합니다.
1. 브라우저에서 **[!UICONTROL 보기 > 개발자 > 개발자 도구]**&#x200B;를 클릭하여 Chrome 개발자 창을 엽니다. 또는 원하는 브라우저 개발자 도구를 선택합니다.

1. 개발자 도구가 열려 있을 때 캐시가 비활성화되어 있는지 확인합니다.

   * Windows®에서 개발자 도구 창의 설정으로 이동한 다음 **[!UICONTROL 캐시 비활성화(devtools가 열려 있는 동안)]** 확인란을 선택합니다.
   * macOS의 개발자 창의 **[!UICONTROL 네트워크]** 탭에서 **[!UICONTROL 캐시 비활성화]**&#x200B;를 선택합니다.

1. 컨텐츠 유형이 적절한 형식으로 변형됩니다. 다음 스크린샷은 Chrome에서 WebP로 동적으로 변환되는 PNG 이미지를 보여줍니다.
1. 다른 브라우저 및 사용자 조건에서 이 테스트를 반복합니다.

>[!NOTE]
>
>일부 이미지는 변환되지 않습니다. 스마트 이미징에서는 전환이 성능을 향상시킬 수 있는지 여부를 결정합니다. 예상 성능 이점이 없거나 JPEG 또는 PNG가 아닌 이미지가 변환되지 않는 경우가 있습니다.

![image2017-11-14_15398](assets/image2017-11-14_15398.png)

## 요청에 대해 스마트 이미징을 끌 수 있습니까?{#turning-off-smart-imaging}

예. URL에 수정자 `bfc=off`을 추가하여 스마트 이미징을 끌 수 있습니다.

## &quot;조정&quot;은 무엇입니까? 정의할 수 있는 설정이나 동작이 있습니까? (#tuning-settings)

현재 선택적으로 스마트 이미징을 활성화하거나 비활성화할 수 있습니다. 다른 튜닝은 사용할 수 없습니다.

## 스마트 이미징이 품질 설정을 관리하는 경우 설정할 최소 및 최대 수가 있습니까? 예를 들어 &quot;60보다 크지 않음&quot; 및 &quot;80보다 크지 않음&quot;을 설정할 수 있습니까? (#minimum-maximum)

현재 Smart Imaging에는 이러한 프로비저닝 기능이 없습니다.

## 경우에 따라 JPEG 이미지가 WebP 이미지 대신 Chrome으로 반환됩니다. 왜? (#jpeg-webp)

스마트 이미징은 전환이 유용한지 여부를 결정합니다. 비교 가능한 품질과 함께 파일 크기가 더 작은 경우에만 새 이미지를 반환합니다.
