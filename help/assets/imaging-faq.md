---
title: 스마트 이미징
description: 스마트 이미징은 각 사용자의 고유한 보기 특성을 적용하여 환경에 최적화된 적합한 이미지를 자동으로 제공하므로 향상된 성능과 참여를 제공합니다.
contentOwner: Rick Brough
topic-tags: dynamic-media
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: bf8c6bbd-847d-43d7-9ff4-7231bfd8d107
feature: Asset Management,Renditions
role: User, Admin
exl-id: e427d4ee-d5c8-421b-9739-f3cf2de36e41
source-git-commit: 9b02a5363d32771cd9c039f97044e8a1d72fe286
workflow-type: tm+mt
source-wordcount: '3518'
ht-degree: 1%

---

# 스마트 이미징 {#smart-imaging}

## 스마트 이미징이란 무엇입니까? {#what-is-smart-imaging}

스마트 이미징 기술은 Adobe Sensei AI 기능을 적용하고 기존 &quot;이미지 사전 설정&quot;에서 작동합니다. 클라이언트 브라우저 기능을 기반으로 이미지 형식, 크기 및 품질을 자동으로 최적화하여 이미지 전달 성능을 향상시키는 데 도움이 됩니다.

이제 AVIF 및 WebP 지원과 함께 제공되는 향상된 스마트 이미징으로 LCP(Largest Contentful Paint)에 대해 더 나은 Google Core Web Vital 점수를 얻습니다.

>[!IMPORTANT]
>
>스마트 이미징을 사용하려면 Adobe Experience Manager - Dynamic Media과 번들로 제공되는 기본 CDN(Content Delivery Network)을 사용해야 합니다. 다른 모든 사용자 지정 CDN은 이 기능에서 지원되지 않습니다.

스마트 이미징은 Adobe의 동급 최강의 프리미엄 CDN(Content Delivery Network) 서비스와 완벽하게 통합되는 향상된 성능 증대의 이점을 제공합니다. 이 서비스는 서버, 네트워크 및 피어링 지점 간의 최적의 인터넷 경로를 찾습니다. 인터넷에서 기본 경로를 사용하는 대신 지연 시간이 가장 짧고 패킷 손실률이 가장 낮은 경로를 찾습니다.

다음 이미지 자산 예는 추가된 스마트 이미징 최적화를 보여줍니다.

| 이미지(URL) | 썸네일 | 크기(JPEG) | 스마트 이미징을 사용한 크기(WebP) | 스마트 이미징을 사용한 크기(AVIF) | WebP를 사용한 % 감소 | AVIF를 사용한 % 감소 |
|---|---|---|---|---|---|---|
| [이미지 1](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_6?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![그림1](/help/assets/assets-dm/picture1.png) | 145KB | 106KB | 90.2KB | 26.89% | 37.79% |
| [이미지 2](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_3?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![그림2](/help/assets/assets-dm/picture2.png) | 412KB | 346KB | 113KB | 16.01% | 72.57% |
| [이미지 3](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_2?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![그림3](/help/assets/assets-dm/picture3.png) | 221KB | 189KB | 87.1KB | 14.47% | 60.58% |
| [이미지 4](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_1?hei=500&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![그림 4](/help/assets/assets-dm/picture4.png) | 594KB | 545KB | 286KB | 8.25% | 51.85% |

위와 유사하게, Adobe은 더 큰 샘플 세트를 사용하여 테스트를 실행하기도 했습니다. AVIF 형식은 WebP에 비해 20% 더 큰 크기 감소를 제공했는데, 이는 JPEG에 비해 27% 더 줄어든 것이다. 모두 동일한 시각적 품질입니다. 총 AVIF는 JPEG에 비해 최대 41%의 평균 크기 감소를 제공합니다.

WebP 및 AVIF를 PNG와 비교하면 WebP에 84%, AVIF에 87%의 크기를 줄일 수 있습니다. 또한 WebP와 AVIF 형식은 투명도와 여러 이미지 애니메이션을 모두 지원하므로 투명한 PNG 및 GIF 파일에 적합합니다.

참조 - [차세대 이미지 형식을 사용한 이미지 최적화(WebP 및 AVIF)](https://medium.com/adobetech/image-optimisation-with-next-gen-image-formats-webp-and-avif-248c75afacc4)

<!-- HIDDEN ON MAY 19, 2022 BASED ON CQDOC-19280 On the mobile web, the challenges are compounded by two factors:

* Large variety of devices with different form factors and high-resolution displays.
* Constrained network bandwidth.

In terms of images, the goal is to serve the best quality images as efficiently as possible. -->

## 최신 스마트 이미징의 주요 이점은 무엇입니까? {#what-are-the-key-benefits-of-smart-imaging}

스마트 이미징은 사용 중인 클라이언트 브라우저, 장치 디스플레이 및 네트워크 조건에 따라 이미지 파일 크기를 자동으로 최적화하여 이미지 전달 성능을 향상시킵니다. 이미지가 페이지 로드 시간의 대부분을 구성하므로 성능 향상은 높은 전환율, 사이트에서 보낸 시간, 낮은 사이트 바운스 비율 등 비즈니스 KPI에 큰 영향을 줄 수 있습니다.

최신 스마트 이미징의 최신 주요 이점은 다음과 같습니다.

* 이제 차세대 AVIF 형식을 지원합니다.
* 이제 PNG에서 WebP로 및 AVIF로 손실 변환을 지원합니다. PNG는 무손실 형식이므로 배달되는 이전 WebP 및 AVIF는 손실되지 않았습니다.
* 브라우저 형식 변환(`bfc`)
* 장치 픽셀 비율(`dpr`)
* 네트워크 대역폭(`network`)

### 브라우저 형식 변환(bfc) 정보 {#bfc}

다음을 추가하여 브라우저 형식 변환 켜기 `bfc=on` 이미지 URL을 사용하면 JPEG 및 PNG가 다른 브라우저의 경우 손실 AVIF, 손실 WebP, 손실 JPEGXR, 손실 JPEG2000으로 자동으로 변환됩니다. 이러한 형식을 지원하지 않는 브라우저의 경우 스마트 이미징은 JPEG 또는 PNG를 계속 제공합니다. 형식과 함께 새 형식의 품질은 스마트 이미징에서 다시 계산됩니다.

다음을 추가하여 스마트 이미징을 끌 수도 있습니다 `bfc=off` 추가 작업이 필요합니다.

참조 - [bfc](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-bfc.html?lang=en) ( Dynamic Media 이미지 제공 및 렌더링 API) 아래에 그룹화됩니다.

### 장치 픽셀 비율(dpr) 최적화 기본 정보 {#dpr}

CSS 픽셀 비율이라고도 하는 DPR(장치 픽셀 비율)은 장치의 실제 픽셀과 논리 픽셀 간의 관계입니다. 특히 최신 모바일 기기들의 화소 해상도는 망막 스크린의 출현으로 빠른 속도로 높아지고 있다.

장치 픽셀 비율 최적화를 활성화하면 이미지가 화면의 기본 해상도로 렌더링되므로 선명하게 표시됩니다.

현재 디스플레이의 픽셀 밀도는 Akamai CDN 헤더 값에서 가져옵니다.

| 이미지 URL에 허용되는 값 | 설명 |
|---|---|
| `dpr=off` | 개별 이미지 URL 수준에서 DPR 최적화를 끄십시오. |
| `dpr=on,dprValue` | 스마트 이미징에서 감지한 DPR 값을 사용자 지정 값(클라이언트측 논리 또는 기타 방법으로 감지됨)으로 재정의합니다. 허용되는 값 `dprValue` 0보다 큰 숫자입니다. |

>[!NOTE]
>
>* 다음을 사용할 수 있습니다 `dpr=on,dprValue` 회사 수준 DPR이 설정된 경우라도.
>* DPR 최적화로 인해 결과 이미지가 MaxPix Dynamic Media 설정보다 클 때 이미지의 종횡비를 유지하여 MaxPix 너비가 항상 인식됩니다.


| 요청한 이미지 크기 | 장치 픽셀 비율(dpr) 값 | 배달된 이미지 크기 |
|---|---|---|
| 816 x 500 | 1 | 816 x 500 |
| 816 x 500 | 2 | 1632 x 1000 |

참조 - [이미지 작업 시](/help/assets/adding-dynamic-media-assets-to-pages.md#when-working-with-images) 및 [스마트 자르기 작업](/help/assets/adding-dynamic-media-assets-to-pages.md#when-working-with-smart-crop).

### 네트워크 대역폭 최적화 기본 정보 {#network}

네트워크 대역폭을 켜면 실제 네트워크 대역폭을 기반으로 제공되는 이미지 품질이 자동으로 조정됩니다. 네트워크 대역폭 성능이 낮은 경우 이미 켜져 있더라도 DPR(장치 픽셀 비율) 최적화는 자동으로 꺼집니다.

원하는 경우, 회사는 다음을 추가하여 개별 이미지 수준에서 네트워크 대역폭 최적화를 옵트아웃할 수 있습니다 `network=off` 추가 작업이 필요합니다.

| 이미지의 URL에 허용되는 값 | 설명 |
|---|---|
| `network=off` | 개별 이미지 URL 수준에서 네트워크 최적화를 해제합니다. |

DPR 및 네트워크 대역폭 값은 번들 CDN의 감지된 클라이언트측 값을 기반으로 합니다. 이러한 값은 때때로 부정확합니다. 예를 들어, DPR=2가 있는 iPhone 5 및 iPhone12 `dpr=3`, 둘 다 표시 `dpr=2`. 여전히 고해상도 장치의 경우 `dpr=2` 보내는 것보다 낫습니다. `dpr=1`. 그러나 이러한 부정확성을 극복하는 가장 좋은 방법은 클라이언트측 DPR을 사용하여 100% 정확한 값을 제공하는 것입니다. 그리고 Apple이든 다른 어떤 장치든 그것은 실행된 모든 장치에서 작동합니다. 자세한 내용은 [클라이언트 측 장치 픽셀 비율이 있는 스마트 이미징 사용](/help/assets/client-side-dpr.md).

### 스마트 이미징의 추가적인 주요 이점

* 최신 스마트 이미징을 사용하는 웹 페이지의 Google SEO 등급을 개선했습니다.
* 런타임 시 최적화된 컨텐츠를 즉시 제공합니다.
* Adobe Sensei 기술을 사용하여 품질에 따라 변환(`qlt`)가 이미지 요청에 지정됩니다.
* TTL(Time To Live)과 독립적입니다. 이전에는 스마트 이미징이 작동하려면 최소 TTL이 12시간이었습니다.
* 이전에는 원본 이미지와 파생 이미지가 모두 캐시되었으며 캐시를 무효화하는 2단계 프로세스였습니다. 최신 Smart Imaging에서는 파생자만 캐시되므로 단일 단계 캐시 무효화 프로세스를 허용합니다.
* 규칙 세트에 사용자 지정 헤더를 사용하는 고객은 이전 버전의 Smart Imaging과 달리 이러한 헤더가 차단되지 않으므로 최신 Smart Imaging을 활용할 수 있습니다. 예를 들어, &quot;Timing Allow Origin&quot;, &quot;X-Robot&quot;에서 설명한 대로 [이미지 응답에 사용자 지정 헤더 값 추가|Dynamic Media Classic](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/add-custom-header-val-image.html).

## 스마트 이미징과 관련된 라이센스 비용이 있습니까? {#are-there-any-licensing-costs-associated-with-smart-imaging}

아니요. 스마트 이미징은 기존 라이선스에 포함되어 있습니다. 이 규칙은 Dynamic Media Classic 또는 Experience Manager - Dynamic Media(On-prem, AMS 및 Experience Manager)에 대해 적용됩니다.

>[!NOTE]
>
>Dynamic Media - 하이브리드 고객은 스마트 이미징을 사용할 수 없습니다.

## 스마트 이미징은 어떻게 작동합니까? {#how-does-smart-imaging-work}

소비자가 이미지를 요청하면 스마트 이미징은 사용자 특성을 확인하고 사용 중인 브라우저를 기반으로 적절한 이미지 형식으로 변환합니다. 이러한 형식 변환은 시각적 품질을 저하시키지 않는 방식으로 수행됩니다. 스마트 이미징은 다음과 같은 방식으로 브라우저 기능에 따라 이미지를 다른 형식으로 자동으로 변환합니다.

* 브라우저가 형식을 지원하는 경우 자동으로 AVIF로 변환
* AVIF 변환이 유익하지 않거나 브라우저가 AVIF를 지원하지 않는 경우 자동으로 WebP으로 변환
* Safari가 WebP를 지원하지 않는 경우 JPEG2000으로 자동 변환
* IE 9+용 JPEGXR로 자동 변환하거나 Edge에서 WebP를 지원하지 않는 경우\
   | 이미지 형식 | 지원되는 브라우저 | |—|—| | AVIF | [https://caniuse.com/avif](https://caniuse.com/avif) | | WebP | [https://caniuse.com/webp](https://caniuse.com/webp) | | JPEG 2000 | [https://caniuse.com/jpeg2000](https://caniuse.com/jpeg2000) | | JPEGXR | [https://caniuse.com/jpegxr](https://caniuse.com/jpegxr) |
* 이러한 형식을 지원하지 않는 브라우저의 경우 원래 요청한 이미지 형식이 제공됩니다.

원본 이미지 크기가 스마트 이미징에서 만드는 이미지 크기보다 작으면 원본 이미지가 제공됩니다.

## 지원되는 이미지 형식은 무엇입니까? {#what-image-formats-are-supported}

스마트 이미징에 대해 다음 이미지 형식이 지원됩니다.

* JPEG
* PNG

JPEG 이미지 파일 형식의 경우 스마트 이미징에서 새 형식의 품질을 다시 계산합니다.

PNG와 같은 투명도를 지원하는 이미지 파일 형식의 경우, 손실 AVIF 및 WebP을 제공하도록 스마트 이미징을 구성할 수 있습니다. 손실 형식 변환의 경우 Smart Imaging은 이미지의 URL에 언급된 화질을 사용하거나 Dynamic Media 회사 계정에 구성된 품질을 사용합니다.

## 이미 사용 중인 기존 이미지 사전 설정에서 스마트 이미징은 어떻게 작동합니까? {#how-does-smart-imaging-work-with-our-existing-image-presets-that-are-already-in-use}

스마트 이미징은 기존 이미지 사전 설정에서 작동하며 모든 이미지 설정을 준수합니다. 변경 사항은 이미지 형식, 품질 설정 또는 둘 다입니다. 형식 변환을 위해 스마트 이미징은 이미지 사전 설정 설정에 정의된 대로 전체 시각적 품질을 유지하지만 더 작은 파일 크기로 유지합니다.

예를 들어, 이미지 사전 설정이 JPEG 형식, 크기 500 x 500, quality=85, 언샵 마스크=0.1,1,5로 정의된다고 가정합니다. 스마트 이미징에서 사용자가 Chrome 브라우저에 있음을 감지하면 이미지가 500 x 500의 WebP 형식으로 변환되고, WebP 품질에서 가능한 한 가까운 JPEG 품질과 일치하는 WebP 품질에서 0.1,1,5로 변환됩니다. 해당 WebP 전환의 사용 풋프린트와 JPEG이 비교되고 두 항목 중 작은 부분이 반환됩니다.

## URL, 이미지 사전 설정을 변경하거나 스마트 이미징을 위해 내 사이트에 새 코드를 배포해야 합니까? {#will-i-have-to-change-any-urls-image-presets-or-deploy-any-new-code-on-my-site-for-smart-imaging}

아니요. 스마트 이미징은 기존 이미지 URL 및 이미지 사전 설정과 원활하게 작동합니다. 또한 스마트 이미징에서는 사용자의 브라우저를 감지하기 위해 웹 사이트에 코드를 추가할 필요가 없습니다. 이 모든 기능은 자동으로 처리됩니다.

<!-- Smart Imaging works seamlessly with your existing image URLs and image presets if you configure Smart Imaging on your existing custom domain. In addition, Smart Imaging does not require you to add any code on your website to detect a user's browser. It is all handled automatically.

In case you must configure a new custom domain to use Smart Imaging, the URLs must be updated to reflect this custom domain.

To understand pre-requisites for Smart Imaging, see [Am I eligible to use Smart Imaging?](#am-i-eligible-to-use-smart-imaging) -->

<!-- OLD As mentioned earlier, Smart Imaging supports only JPEG and PNG image formats. For other formats, you need to append the `bfc=off` modifier to the URL as described earlier. -->

## 스마트 이미징이 HTTPS에서 작동합니까? HTTP/2는 어떻습니까? {#does-smart-imaging-working-with-https-how-about-http}

스마트 이미징은 HTTP 또는 HTTPS를 통해 전달된 이미지에서 작동합니다. 또한 HTTP/2에서도 작동합니다.

## 스마트 이미징을 사용할 수 있습니까? {#am-i-eligible-to-use-smart-imaging}

Smart Imaging을 사용하려면 회사의 Experience Manager 또는 Dynamic Media Classic 계정의 Dynamic Media이 다음 요구 사항을 충족해야 합니다.

* Adobe 번들 CDN(Content Delivery Network)을 라이센스의 일부로 사용합니다.
* 전용 도메인 사용(예: `images.company.com` 또는 `mycompany.scene7.com`). 일반 도메인이 아닙니다(예: `s7d1.scene7.com`, `s7d2.scene7.com`, 또는 `s7d13.scene7.com`).

도메인을 찾으려면 [Dynamic Media Classic 데스크탑 애플리케이션](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)그런 다음 회사 계정 또는 계정에 로그인합니다.

이동 **[!UICONTROL 설정]** > **[!UICONTROL 애플리케이션 설정]** > **[!UICONTROL 일반 설정]**. 레이블이 지정된 필드를 찾습니다 **[!UICONTROL 게시된 서버 이름]**. 현재 일반 도메인을 사용하는 경우 사용자 지정 도메인으로 이동을 요청할 수 있습니다. 지원 사례를 제출할 때 이 전환 요청을 수행합니다.

첫 번째 사용자 지정 도메인은 Dynamic Media 라이센스를 통해 추가 비용이 들지 않습니다.

## 내 계정에 대해 스마트 이미징을 활성화하는 프로세스는 무엇입니까? {#what-is-the-process-for-enabling-smart-imaging-for-my-account}

스마트 이미징 사용을 위한 요청을 시작합니다. 자동으로 활성화되지 않습니다.

아래 설명된 대로 지원 사례를 만듭니다. 지원 사례에서 계정에 활성화할 다음 스마트 이미징 기능(하나 이상) 중 어느 것을 명시해야 합니다.

* WebP
* AVIF
* DPR 및 네트워크 대역폭 최적화
* PNG에서 손실 AVIF 또는 손실 WebP로

WebP에서 이미 스마트 이미징을 활성화했지만 위에 나열된 다른 새로운 기능을 원하는 경우 지원 사례를 만들어야 합니다.

**계정에서 스마트 이미징을 사용하도록 지원 사례를 만들려면:**

1. [Admin Console을 사용하여 새 지원 사례 만들기를 시작합니다](https://helpx.adobe.com/kr/enterprise/using/support-for-experience-cloud.html).
1. 지원 사례에 다음 정보를 제공하십시오.

   * 기본 연락처 이름, 이메일, 전화

   * 계정에서 활성화할 다음 스마트 이미징 기능(하나 이상) 중 하나를 나열합니다.
      * WebP
      * AVIF
      * DPR 및 네트워크 대역폭 최적화
      * PNG에서 손실 AVIF 또는 손실 WebP로
   * 스마트 이미징에 사용할 수 있는 모든 도메인(즉, `images.company.com` 또는 `mycompany.scene7.com`).

      도메인을 찾으려면 [Dynamic Media Classic 데스크탑 애플리케이션](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)그런 다음 회사 계정 또는 계정에 로그인합니다.

      이동 **[!UICONTROL 설정]** > **[!UICONTROL 애플리케이션 설정]** > **[!UICONTROL 일반 설정]**.

      레이블이 지정된 필드를 찾습니다 **[!UICONTROL 게시된 서버 이름]**.

   * Adobe을 통해 CDN을 사용하고 있으며 직접 관계로 관리하지 않는지 확인합니다.

   * 다음과 같은 전용 도메인을 사용하고 있는지 확인합니다. `images.company.com` 또는 `mycompany.scene7.com`, 및 과 같은 일반 도메인이 아님 `s7d1.scene7.com`, `s7d2.scene7.com`, `s7d13.scene7.com`.

      도메인을 찾으려면 [Dynamic Media Classic 데스크탑 애플리케이션](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)그런 다음 회사 계정 또는 계정에 로그인합니다.

      이동 **[!UICONTROL 설정]** > **[!UICONTROL 애플리케이션 설정]** > **[!UICONTROL 일반 설정]**.

      레이블이 지정된 필드를 찾습니다 **[!UICONTROL 게시된 서버 이름]**. 현재 일반 Dynamic Media Classic 도메인을 사용 중인 경우, 이 전환의 일부로 고유한 사용자 지정 도메인으로 이동을 요청할 수 있습니다.

   * HTTP/2에서 작동하도록 할지 여부를 지정합니다.


1. Adobe 고객 지원 팀에서는 요청을 제출한 순서에 따라 스마트 이미징 고객 대기 목록에 추가합니다.
1. Adobe이 요청을 처리할 준비가 되면 고객 지원 팀에서 대상 날짜를 조정하고 설정해야 합니다.
1. **선택 사항입니다**: Adobe이 새 기능을 프로덕션에 푸시하기 전에 스테이징에서 스마트 이미징을 선택적으로 테스트할 수 있습니다.
1. 고객 지원 센터에서 완료 후 알림을 받습니다.
1. 스마트 이미징의 성능 향상을 극대화하려면 Adobe에서 TTL(Time To Live)을 24시간 이상으로 설정하는 것이 좋습니다. TTL은 CDN에 의해 자산이 캐시되는 기간을 정의합니다. 이 설정을 변경하려면 다음을 수행하십시오.

   1. Dynamic Media Classic을 사용하는 경우 **[!UICONTROL 설정]** > **[!UICONTROL 애플리케이션 설정]** > **[!UICONTROL 게시 설정]** > **[!UICONTROL 이미지 서버]**. 설정 **[!UICONTROL 기본 클라이언트 캐시 Time To Live]** 값 을 24 이상으로 설정합니다.
   1. Dynamic Media을 사용하는 경우 다음을 수행합니다 [이러한 지침은](/help/assets/dm-publish-settings.md#common-thumbnail-attributes-tab). 설정 **[!UICONTROL 만료]** 값 24시간 이상

## 언제 내 계정이 스마트 이미징으로 활성화될 수 있습니까? {#when-can-i-expect-my-account-to-be-enabled-with-smart-imaging}

요청은 대기 목록에 따라 고객 지원에서 수신하는 순서로 처리됩니다.

>[!NOTE]
>
>스마트 이미징을 활성화하면 Adobe이 캐시를 지우므로 리드 타임이 오래 걸릴 수 있습니다. 따라서 지정된 시간에 몇 개의 고객 전환만 처리할 수 있습니다.

## 스마트 이미징을 사용하도록 전환하면 어떤 위험이 있습니까? {#what-are-the-risks-with-switching-over-to-use-smart-imaging}

고객 웹 페이지에는 위험이 없습니다. 그러나 스마트 이미징으로 전환하면 CDN 캐시가 지워집니다. 이 작업에는 Experience Manager 시 Dynamic Media Classic 또는 Dynamic Media의 새 구성으로 이동하는 작업이 포함됩니다.

초기 전환 중에 캐싱되지 않은 이미지는 캐시가 다시 빌드될 때까지 Adobe의 원본 서버에 직접 연결됩니다. 따라서 Adobe은 한 번에 몇 개의 고객 전환을 처리하여 오리진에서 요청을 가져올 때 허용되는 성능을 유지할 수 있도록 계획합니다. 대부분의 고객의 경우 캐시가 1~2일 내에 CDN에서 다시 완전히 빌드됩니다.

## 스마트 이미징이 예상대로 작동하는지 확인하려면 어떻게 해야 합니까?{#how-can-i-verify-whether-smart-imaging-is-working-as-expected}

1. 계정이 스마트 이미징으로 구성된 후 브라우저에서 Dynamic Media Classic 또는 Adobe Experience Manager - Dynamic Media 이미지 URL을 로드합니다.
1. 로 이동하여 Chrome 개발자 창을 엽니다. **[!UICONTROL 보기]** > **[!UICONTROL 개발자]** > **[!UICONTROL 개발자 도구]** 클릭합니다. 또는 원하는 브라우저 개발자 도구를 선택합니다.

1. 개발자 도구가 열려 있을 때 캐시가 비활성화되어 있는지 확인합니다.

   * Windows®에서 개발자 도구 창의 설정으로 이동한 후 를 선택합니다 **[!UICONTROL 캐시 비활성화(devtools가 열려 있는 동안)]** 확인란을 선택합니다.
   * macOS의 개발자 창에서 **[!UICONTROL 네트워크]** 탭, 선택 **[!UICONTROL 캐시 비활성화]**.

1. 컨텐츠 유형이 적절한 형식으로 변형됩니다. 다음 스크린샷은 Chrome에서 WebP로 동적으로 변환되는 PNG 이미지를 보여줍니다. 도메인에 AVIF가 활성화되어 있는 경우 콘텐츠 유형에서 AVIF가 표시될 수도 있습니다.
1. 다른 브라우저 및 사용자 조건에서 이 테스트를 반복합니다.

>[!NOTE]
>
>일부 이미지는 변환되지 않습니다. 스마트 이미징에서는 전환이 성능을 향상시킬 수 있는지 여부를 결정합니다. 예상 성능 이점이 없거나 형식이 JPEG 또는 PNG가 아닌 경우 이미지가 변환되지 않는 경우가 있습니다.

![image2017-11-14_15398](/help/assets/assets/image2017-11-14_15398.png)

## 성능이 향상되는지 어떻게 알 수 있습니까? 스마트 이미징의 이점을 알 수 있는 방법이 있습니까? {#benefits}

스마트 이미징 헤더는 스마트 이미징의 이점을 결정합니다. 스마트 이미징이 활성화되면 이미지를 요청한 후 **[!UICONTROL 응답 헤더]** 제목, `-X-Adobe-Smart-Imaging` 강조 표시된 다음 예제에서 볼 수 있습니다.

![스마트 이미징 헤더](/help/assets/assets-dm/smart-imaging-header2.png)

이 헤더는 다음을 알려줍니다.

* 스마트 이미징이 회사에서 일하고 있습니다.
* 양수 값은 전환이 성공했음을 의미합니다. 이 경우 새 WebP 이미지가 반환됩니다.
* 음수 값은 변환이 실패했음을 의미합니다. 이 경우 원본 요청된 이미지가 반환됩니다(지정하지 않은 경우 기본적으로 JPEG).
* 양수 값은 요청한 이미지와 새 이미지 간의 바이트 차이를 보여줍니다. 위의 예에서 저장된 바이트는 `75048` 또는 1개 이미지에 약 75KB.
* 음수 값은 요청한 이미지가 새 이미지보다 작음을 의미합니다. 음수 크기 차이가 표시되지만 제공된 이미지는 원래 요청된 이미지입니다.

>[!NOTE]
>
>**X-Adobe-스마트-이미징 = -1(WebP가 제공됨)**
>
>값이 `X-Adobe-Smart-Imaging` is -1이고 WebP가 아직 배달되고 있으므로 Smart Imaging이 작동하고 있지만 오래된 캐시로 인해 크기 이점이 계산되지 않았습니다. 다음을 사용할 수 있습니다 `cache=update` (한 번만 해당) 이미지 URL에서 이 문제를 해결합니다.
>수정자 사용의 예:
>`https://smartimaging.scene7.com/is/image/SmartImaging/sample1?cache=update`
>전체 캐시를 무효화하려면 지원 사례를 만들어야 합니다.

## 스마트 이미징에서 AVIF 최적화를 비활성화하려면 어떻게 해야 합니까?{#disable-avif}

기본적으로 서비스 제공 WebP로 다시 전환하려면 이에 대한 지원 사례를 만드십시오. 평소대로 매개 변수를 추가하여 스마트 이미징을 끌 수 있습니다 `bfc=off` 추가 작업이 필요합니다. 그러나 스마트 이미징용 URL 수정자에서 WebP 또는 AVIF를 선택할 수는 없습니다. 이 기능은 회사 계정 수준에서 유지됩니다.

## 요청에 대해 스마트 이미징을 끌 수 있습니까?{#turning-off-smart-imaging}

예. 다음 수정자 중 하나를 추가하여 스마트 이미징을 끌 수 있습니다.

* `bfc=off` 브라우저 형식 변환을 끄려면 다음을 수행하십시오. 참조 - [브라우저 형식 변환](#bfc).
* `dpr=off` 장치 픽셀 비율을 해제하려면 다음을 수행하십시오. 참조 - [장치 픽셀 비율](#dpr).
* `network=off` 네트워크 대역폭을 해제하려면 다음을 수행하십시오. 참조 - [네트워크 대역폭](#network).

## &quot;조정&quot;은 무엇입니까? 정의할 수 있는 설정이나 동작이 있습니까? {#tuning-settings}

스마트 이미징에는 활성화하거나 비활성화할 수 있는 세 가지 옵션이 있습니다.

* [브라우저 형식 변환](#bfc)
* [장치 픽셀 비율](#dpr)
* [네트워크 대역폭](#network)

## Chrome 웹 브라우저에 fmt=tif가 있는 URL이 있습니다. 그러나 ImageServer 오류로 인해 내 요청이 실패합니다. 왜? {#fmt-tif}

계정에 스마트 이미징이 활성화되지 않은 경우에는 이 오류가 발생하지 않습니다. 스마트 이미징은 JPEG 또는 PNG 형식에서만 작동합니다.

이 오류를 방지하려면 다음 중 하나를 수행할 수 있습니다.

* JPEG 또는 PNG 또는
* 를 사용하지 않음 `fmt` 수정자이거나
* 스마트 이미징에서 정의한 브라우저 기본 설정 형식을 사용합니다. 예를 들어 Chrome용 WebP 웹 브라우저를 사용할 수 있습니다.

## 이미지 URL에서 TIFF 이미지를 다운로드하고 싶습니다. 어떻게 하죠? {#download-tif}

추가 `fmt=tif` 및 `bfc=off` 이미지의 URL 경로에 연결할 수도 있습니다.

## 스마트 이미징은 이미지 형식만 관리합니까, 아니면 최상의 결과를 위해 이미지 품질 설정도 관리합니까?

스마트 이미징은 형식과 품질을 모두 사용합니다. 이미지 URL에서 요청한 경우 나머지 매개 변수는 동일하게 유지됩니다.

## 스마트 이미징이 품질 설정을 관리하는 경우 설정할 수 있는 최소값과 최대값이 있습니까? 즉, 60보다 크지 않고 80보다 크지 않은 품질인가요? {#quality-setting}

현재 그러한 프로비저닝이 없습니다.

## 스마트 이미징은 자동으로 백분율 품질 출력 설정을 조정합니까, 아니면 수동으로 조정되며 모든 이미지에 적용됩니까? 어느 범위요? {#percent-quality}

스마트 이미징은 자동으로 품질 비율을 조정합니다. 이 품질 퍼센트는 Adobe이 개발한 기계 학습 알고리즘을 사용하여 결정됩니다. 이 백분율은 범위가 특정적이지 않습니다.

## 스마트 이미징에서는 어떤 이미지 제공 명령이 지원되거나 무시됩니까? {#support-ignore}

무시되는 명령만 `fmt` 및 `qlt`. 나머지 명령은 모두 지원됩니다.

## JPEG 이미징만 스마트 이미징으로 대체됩니까? WebP, PNG 등을 요청하면 어떻게 합니까? {#replace-request}

이 기능은 JPEG 및 PNG에만 작동합니다.

## JPEG 이미지가 WebP가 아닌 Chrome으로 가끔 반환되는 이유는 무엇입니까? {#jpeg-returned}

스마트 이미징은 전환이 유용한지 여부를 결정합니다. 전환의 새 이미지만 반환합니다.

## 복합 이미지에서 장치 픽셀 비율(dpr) 기능이 예상대로 작동하지 않는 이유는 무엇입니까? {#composite-images}

복합 이미지에 레이어가 너무 많은 경우 위치 수정자를 사용하는 동안 dpr 기능에 영향을 줄 수 있습니다. 이 문제는 알려진 문제이며 향후 스마트 이미징 릴리스에서 수정됩니다. 다른 스마트 이미징 기능이 제대로 작동하지 않는 경우 지원 사례를 만들어 문제를 보고할 수 있습니다.

## 스마트 이미징 PNG가 여전히 무손실 WebP/AVIF로 변환되는 이유는 무엇입니까? {#convert-to-lossless}

PNG는 무손실 형식이므로 배달되는 이전 WebP 및 AVIF는 손실이 없으므로 예상보다 큰 크기입니다. 이제 스마트 이미징이 손실 전환을 지원합니다. 수정자를 사용할 수 있습니다 `cache=update` (한 번만) 이미지 요청에서 이 문제를 수정했습니다. 이 수정자 사용의 예:

`https://smartimaging.scene7.com/is/image/SmartImaging/sample1?cache=update`

전체 캐시를 무효화하려면 이러한 작업을 요청하는 지원 사례를 만들어야 합니다.

## Smart Imaging에서 PNG를 무손실 변환으로 계속 사용할 수 있습니까? {#continue-using}

이제 스마트 이미징은 품질 수준에 따라 손실 전환을 지원합니다. 손실 없는 변환을 계속 사용하려면 회사의 설정에 따라 설정되거나 를 사용하여 이미지의 URL을 통해 100가지 품질을 사용할 수 있습니다 `qlt=100` 을 가리키도록 업데이트하는 것이 좋습니다.