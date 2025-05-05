---
title: 스마트 이미징
description: 스마트 이미징은 각 사용자의 고유한 보기 특성을 적용하여 경험에 맞게 자동으로 최적화된 적합한 이미지를 제공하므로 향상된 성능과 참여를 제공합니다.
contentOwner: Rick Brough
topic-tags: dynamic-media
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
feature: Asset Management,Renditions
role: User, Admin
exl-id: e427d4ee-d5c8-421b-9739-f3cf2de36e41
solution: Experience Manager, Experience Manager Assets
source-git-commit: 7fb3ec9654b56605321f0d12a4c1e23d2e18dab9
workflow-type: tm+mt
source-wordcount: '3322'
ht-degree: 0%

---

# 스마트 이미징 {#smart-imaging}

스마트 이미징은 각 사용자의 고유한 보기 특성을 적용하여 경험에 맞게 자동으로 최적화된 적합한 이미지를 제공하므로 향상된 성능과 참여를 제공합니다.

## 스마트 이미징 기본 정보 {#what-is-smart-imaging}

스마트 이미징 기술은 Adobe Sensei AI 기능을 적용하며 기존 &quot;이미지 사전 설정&quot;과 함께 작동합니다. 클라이언트 브라우저 기능을 기반으로 이미지 형식, 크기 및 품질을 자동으로 최적화하여 이미지 제공 성능을 향상시키는 데 사용됩니다.

이제 AVIF 및 WebP가 모두 지원되는 향상된 스마트 이미징을 통해 LCP(최대 콘텐츠풀 페인트)에 대한 더 나은 Google 코어 웹 바이탈 점수를 얻으십시오.

>[!IMPORTANT]
>
>스마트 이미징을 사용하려면 Adobe Experience Manager - Dynamic Media과 번들로 제공되는 기본 CDN(Content Delivery Network)을 사용해야 합니다. 다른 모든 사용자 지정 CDN은 이 기능에서 지원되지 않습니다.

>[!TIP]
>
>Dynamic Media [_스냅숏_](https://snapshot.scene7.com/)을(를) 사용하여 Dynamic Media 이미지 수정자 및 스마트 이미징의 이점을 알아보십시오.
>
>스냅샷은 Dynamic Media의 최적화된 동적 이미지 제공 기능을 보여 주기 위해 설계된 시각적 데모 도구입니다. 테스트 이미지 또는 Dynamic Media URL로 실험하여 다양한 Dynamic Media 이미지 수정자의 출력을 시각적으로 관찰하고 다음에 대한 스마트 이미징 최적화를 확인하십시오.
>
>* 파일 크기(WebP 및 AVIF 게재 포함)
>* 네트워크 대역폭
>* DPR(장치 픽셀 비율)
>
>스냅숏을 사용하는 것이 얼마나 쉬운지 알아보려면 [스냅숏 교육 비디오](https://experienceleague.adobe.com/ko/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot)를 재생하세요(3분 17초).

스마트 이미징은 Adobe의 동급 최고의 프리미엄 CDN(Content Delivery Network) 서비스와 완전히 통합되어 향상된 성능을 활용할 수 있습니다. 이 서비스는 서버, 네트워크, 피어링 포인트 사이의 최적의 인터넷 경로를 찾는다. 인터넷에서 기본 경로를 사용하지 않고 지연 시간이 가장 낮고 패킷 손실률이 가장 낮은 경로를 찾습니다.

다음 이미지 자산 예는 추가된 스마트 이미징 최적화를 설명합니다.

| 이미지(URL) | 썸네일 | 크기(JPEG) | 스마트 이미징을 사용한 크기(WebP) | 스마트 이미징을 사용한 크기(AVIF) | WebP를 통한 % 감소 | AVIF를 사용한 % 감소 |
|---|---|---|---|---|---|---|
| [이미지 1](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_6?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![그림1](/help/assets/assets-dm/picture1.png) | 145 KB | 106 KB | 90.2 KB | 26.89% | 37.79% |
| [이미지 2](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_3?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![사진2](/help/assets/assets-dm/picture2.png) | 412 KB | 346 KB | 113 KB | 16.01% | 72.57% |
| [이미지 3](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_2?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![그림3](/help/assets/assets-dm/picture3.png) | 221 KB | 189 KB | 87.1 KB | 14.47% | 60.58% |
| [이미지 4](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_1?hei=500&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![그림4](/help/assets/assets-dm/picture4.png) | 594 KB | 545 KB | 286 KB | 8.25% | 51.85% |

위와 유사하게, Adobe은 더 큰 샘플 세트로 테스트를 실행했습니다. 형식 AVIF는 WebP에 비해 20%의 추가 크기 감소를 제공했으며, 이는 JPEG에 비해 27%의 추가 크기 감소를 제공했습니다. 모두 동일한 시각적 품질입니다. 전체적으로 AVIF는 JPEG 대비 최대 41%의 평균 크기 감소를 제공합니다.

WebP 및 AVIF를 PNG와 비교하면, WebP의 경우 84%, AVIF의 경우 87%의 크기 감소를 확인할 수 있습니다. 또한 WebP 및 AVIF 형식 모두 투명도와 여러 이미지 애니메이션을 지원하므로 투명 PNG 및 GIF 파일을 대체할 수 있습니다.

[차세대 이미지 형식(WebP 및 AVIF)을 사용한 이미지 최적화](https://blog.developer.adobe.com/image-optimisation-with-next-gen-image-formats-webp-and-avif-248c75afacc4)도 참조하세요.

<!-- HIDDEN ON MAY 19, 2022 BASED ON CQDOC-19280 On the mobile web, the challenges are compounded by two factors:

* Large variety of devices with different form factors and high-resolution displays.
* Constrained network bandwidth.

In terms of images, the goal is to serve the best quality images as efficiently as possible. -->

## 스마트 이미징의 이점 {#what-are-the-key-benefits-of-smart-imaging}

스마트 이미징은 사용자의 브라우저, 장치 표시 및 네트워크 상태에 따라 파일 크기를 자동으로 최적화하여 이미지 제공을 향상시킵니다. 이 접근 방식을 사용하면 로드 시간이 빨라지고 다양한 환경에서 더 나은 보기 환경을 구현할 수 있습니다. 이미지는 페이지의 로드 시간 대부분을 구성하므로 성능 향상은 다음과 같은 비즈니스 KPI에 지대한 영향을 줄 수 있습니다.

* 전환율이 높아집니다.
* 사이트에서 보낸 시간.
* 사이트 바운스 비율 감소.

최신 스마트 이미징의 최신 주요 이점은 다음과 같습니다.

* 차세대 AVIF 형식을 지원합니다.
* PNG에서 WebP로의 변환 및 AVIF는 이제 손실 변환을 지원합니다. PNG가 무손실 포맷이므로, 이전 WebP 및 AVIF가 전달되지 않았습니다.
* 브라우저 형식 변환(`bfc`)
* 장치 픽셀 비율(`dpr`)
* 네트워크 대역폭(`network`)

### 브라우저 형식 변환 정보(bfc) {#bfc}

이미지 URL에 `bfc=on`을(를) 추가하여 브라우저 형식 변환을 켜면 JPEG 및 PNG가 자동으로 다른 브라우저에 대해 손실 AVIF, 손실 WebP, 손실 JPEGXR, 손실 JPEG2000으로 변환됩니다. 이러한 형식을 지원하지 않는 브라우저의 경우 Smart Imaging에서 JPEG 또는 PNG를 계속 제공합니다. 스마트 이미징은 형식 변경과 함께 새 형식의 품질을 다시 계산합니다.

이미지의 URL에 `bfc=off`을(를) 추가하여 스마트 이미징을 끌 수 있습니다.

Dynamic Media 이미지 제공 및 렌더링 API의 [bfc](https://experienceleague.adobe.com/ko/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-bfc)도 참조하세요.

### 장치 픽셀 비율(DPR) 최적화 정보 {#dpr}

CSS 픽셀 비율이라고도 하는 디바이스 픽셀 비율(DPR)은 디바이스의 물리적 픽셀과 논리 픽셀 간의 관계를 나타냅니다. Retina 디스플레이의 부상과 함께, 최신 모바일 장치의 픽셀 해상도는 빠르게 증가하고 있다.

장치 픽셀 비율 최적화를 활성화하면 화면의 기본 해상도로 이미지가 렌더링되므로 선명해집니다.

현재 디스플레이의 픽셀 밀도는 Akamai CDN 헤더 값에서 가져옵니다.

| 이미지의 URL에 허용된 값 | 설명 |
|---|---|
| `dpr=off` | 개별 이미지 URL 수준에서 DPR 최적화를 해제합니다. |
| `dpr=on,dprValue` | 사용자 지정 값(클라이언트측 논리 또는 기타 수단으로 감지된 값)으로 스마트 이미징에서 감지된 DPR 값을 재정의합니다. `dprValue`에 대해 허용되는 값이 0보다 큰 수입니다. |

>[!NOTE]
>
>* 회사 수준 DPR 설정이 꺼진 경우에도 `dpr=on,dprValue`을(를) 사용할 수 있습니다.
>* DPR 최적화로 인해 결과 이미지가 MaxPix Dynamic Media 설정보다 클 경우 이미지의 종횡비를 유지하여 MaxPix 너비를 항상 인식합니다.

| 요청한 이미지 크기 | 장치 픽셀 비율(dpr) 값 | 게재된 이미지 크기 |
|---|---|---|
| 816 x 500 | 1 | 816 x 500 |
| 816 x 500 | 2 | 1632 x 1000 |

[이미지로 작업할 때](/help/assets/adding-dynamic-media-assets-to-pages.md#when-working-with-images) 및 [스마트 자르기로 작업할 때](/help/assets/adding-dynamic-media-assets-to-pages.md#when-working-with-smart-crop)도 참조하세요.

### 네트워크 대역폭 최적화 기본 정보 {#network}

네트워크 대역폭을 켜면 실제 네트워크 대역폭에 따라 제공되는 이미지 품질이 자동으로 조정됩니다. 네트워크 대역폭이 낮은 경우 DPR(장치 픽셀 비율) 최적화가 이미 설정되어 있더라도 자동으로 꺼집니다.

회사에서 이미지 URL에 `network=off`을(를) 추가하여 개별 이미지에 대한 네트워크 대역폭 최적화를 비활성화할 수 있습니다.

| 이미지의 URL에서 허용되는 값 | 설명 |
|---|---|
| `network=off` | 개별 이미지 URL 수준에서 네트워크 최적화를 끕니다. |

DPR 및 네트워크 대역폭 값은 번들 CDN의 감지된 클라이언트측 값을 기반으로 합니다. 이러한 값은 때때로 부정확합니다. 예를 들어 DPR=2인 iPhone5와 `dpr=3`인 iPhone12는 모두 `dpr=2`을(를) 표시합니다. 고해상도 장치의 경우 `dpr=2`을(를) 보내는 것이 `dpr=1`을(를) 보내는 것보다 좋습니다. 그러나 이러한 부정확성을 극복하는 가장 좋은 방법은 클라이언트측 DPR을 사용하여 100% 정확한 값을 제공하는 것입니다. 또한 Apple 또는 출시된 다른 디바이스 등 어떤 디바이스에서도 작동합니다. [클라이언트측 장치 픽셀 비율로 스마트 이미징 사용](/help/assets/client-side-dpr.md)을 참조하세요.

### 스마트 이미징의 추가적인 주요 이점

* 최신 스마트 이미징을 사용하는 웹 페이지에 대한 Google SEO 등급이 개선되었습니다.
* 최적화된 컨텐츠를 즉시 제공합니다(런타임 시).
* Adobe Sensei 기술을 사용하여 이미지 요청에 지정된 품질(`qlt`)에 따라 변환합니다.
* TTL(Time To Live) 독립적. 이전에는 스마트 이미징이 작동하려면 최소 TTL이 12시간 이상이어야 했습니다.
* 이전에는 원본 이미지와 파생 이미지가 모두 캐시되었으며 캐시를 무효화하는 2단계 프로세스였습니다. 최신 스마트 이미징에서는 파생 함수만 캐시되므로 한 단계의 캐시 무효화 프로세스를 사용할 수 있습니다.
* 규칙 세트에서 사용자 지정 헤더를 사용하는 고객은 이전 버전의 스마트 이미징과 달리 이러한 헤더가 차단되지 않으므로 최신 스마트 이미징의 혜택을 받을 수 있습니다. 예를 들어, [이미지 응답에 사용자 지정 헤더 값 추가|Dynamic Media Classic](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/add-custom-header-val-image.html)에 제시된 대로 &quot;Timing Allow Origin&quot; 및 &quot;X-Robot&quot;이 있습니다.

## 자주 묻는 질문

+++스마트 이미징과 관련된 라이선스 비용이 있습니까?

아니요. 스마트 이미징은 기존 라이선스에 포함되어 있습니다. 이 규칙은 Dynamic Media Classic 또는 Experience Manager - Dynamic Media(온프레미스, AMS 및 Experience Manager as a Cloud Service)에 적용됩니다.

>[!NOTE]
>
>Dynamic Media - 하이브리드 고객은 스마트 이미징을 사용할 수 없습니다.

+++

+++스마트 이미징은 어떻게 작동합니까?

소비자가 이미지를 요청하면 스마트 이미징이 사용자 특성을 분석해 브라우저에 따라 적합한 포맷으로 전환한다. 이러한 형식 변환은 시각적 충실도를 저하시키지 않는 방식으로 수행된다. 스마트 이미징은 다음과 같은 방식으로 브라우저 기능에 따라 이미지를 다른 형식으로 자동으로 변환합니다.

* 브라우저에서 형식을 지원하는 경우 자동으로 AVIF로 변환
* AVIF 전환이 유용하지 않거나 브라우저가 AVIF를 지원하지 않는 경우 자동으로 WebP로 전환합니다.
* Safari에서 WebP를 지원하지 않는 경우 자동으로 JPEG2000으로 전환
* IE 9+용 JPEGXR로 자동 변환하거나 Edge에서 WebP를 지원하지 않는 경우

  | 이미지 형식 | 지원되는 브라우저 |
  |---|---|
  | AVIF | [https://caniuse.com/avif](https://caniuse.com/avif) |
  | 웹P | [https://caniuse.com/webp](https://caniuse.com/webp) |
  | 2000 JPEG | [https://caniuse.com/jpeg2000](https://caniuse.com/jpeg2000) |
  | JPEGXR | [https://caniuse.com/jpegxr](https://caniuse.com/jpegxr) |

* 이러한 형식을 지원하지 않는 브라우저의 경우 원래 요청한 이미지 형식이 제공됩니다.

원본 이미지 크기가 Smart Imaging에서 생성하는 크기보다 작으면 원본 이미지가 제공됩니다.

+++

+++지원되는 이미지 형식은 무엇입니까?

스마트 이미징에 지원되는 이미지 형식은 다음과 같습니다.

* JPEG
* PNG

스마트 이미징은 새 형식으로 변환할 때 JPEG 이미지 파일 형식의 품질을 다시 계산합니다.

PNG와 같이 투명성을 지원하는 이미지 파일 형식의 경우 손실 AVIF 및 WebP를 전달하도록 스마트 이미징을 구성할 수 있습니다. 손실 형식 변환의 경우, 스마트 이미징은 이미지의 URL에서 언급된 품질을 사용하거나 Dynamic Media 회사 계정에 구성된 품질을 사용합니다.

+++

+++스마트 이미징은 이미 사용 중인 기존 이미지 사전 설정에서 어떻게 작동합니까?

스마트 이미징은 모든 이미지 설정을 기준으로 기존 이미지 사전 설정과 원활하게 통합됩니다.

조정에는 이미지 형식, 품질 또는 둘 다가 포함됩니다. 형식 변환 중에 스마트 이미징은 사전 설정된 설정에 따라 완전한 시각적 품질을 유지하지만 더 작은 파일 크기를 제공합니다. 기존 URL 또는 사전 설정에 `bfc=on`, `dpr=on,dprValue`, `network=on` 또는 세 매개 변수 설정을 모두 추가하여 활성화하면 됩니다.

예를 들어 이미지 사전 설정이 JPEG 형식을 500×500픽셀, `quality=85` 및 `unsharp mask=0.1,1,5`로 지정한다고 가정해 보겠습니다. 스마트 이미징은 사용자가 Chrome 브라우저를 사용하고 있는지 감지합니다. 그런 다음 이미지가 동일한 크기(500× 500)와 JPEG 설정과 일치하는 언샵 마스크를 사용하는 WebP로 변환됩니다. 그런 다음 시스템은 WebP 및 JPEG 버전의 파일 크기를 비교하여 작은 파일 크기를 사용자에게 제공합니다.

+++

<!--

### Do I have to change any URLs, image presets, or deploy any new code on my site for Smart Imaging? 

No. Smart Imaging works seamlessly with your existing image URLs and image presets. In addition, Smart Imaging does not require you to add code to your website to detect a user's browser. All of this functionality is handled automatically.

<!-- Smart Imaging works seamlessly with your existing image URLs and image presets if you configure Smart Imaging on your existing custom domain. In addition, Smart Imaging does not require you to add any code on your website to detect a user's browser. It is all handled automatically.

In case you must configure a new custom domain to use Smart Imaging, the URLs must be updated to reflect this custom domain.

To understand pre-requisites for Smart Imaging, see [Am I eligible to use Smart Imaging?](#am-i-eligible-to-use-smart-imaging) -->

<!-- OLD As mentioned earlier, Smart Imaging supports only JPEG and PNG image formats. For other formats, you need to append the `bfc=off` modifier to the URL as described earlier. -->

+++스마트 이미징이 HTTPS에서 작동합니까? HTTP/2는 어떻습니까?

스마트 이미징은 HTTP 또는 HTTPS를 통해 제공되는 이미지에서 작동합니다. 또한 HTTP/2에서도 작동합니다.

+++

+++스마트 이미징을 사용할 수 있습니까?

스마트 이미징은 모든 고객에게 즉시 제공됩니다. 혜택을 누리려면 기존 URL 또는 사전 설정에 `bfc=on`, `dpr=on,dprValue`, `network=on` 또는 세 매개 변수 설정을 모두 추가하기만 하면 됩니다.

Smart Imaging을 사용하려면 Experience Manager 계정의 회사 Dynamic Media Classic 또는 Dynamic Media에 Adobe 번들 CDN(Content Delivery Network)이 라이선스의 일부로 포함되어야 합니다.

+++

+++계정에 대해 스마트 이미징을 활성화하는 프로세스는 무엇입니까?

스마트 이미징을 사용하려면 기존 URL 또는 사전 설정에 `bfc=on`, `dpr=on,dprValue` 또는 `network=on` 또는 세 매개 변수 설정을 모두 추가하십시오. 이러한 변경 작업을 수동으로 수행하지 않으려면 지원 사례를 만들어 기본적으로 스마트 이미징을 활성화할 수 있습니다.

지원 사례를 만들 때 계정에서 활성화할 스마트 이미징 기능을 지정합니다.

* 브라우저 형식 변환(WebP 또는 AVIF)
* 네트워크 대역폭 최적화

>[!NOTE]
>
>DPR에서는 올바른 `dprValue`을(를) 결정하기 위해 클라이언트측 조정이 필요합니다. Adobe 따라서 `dpr=on,dprValue`을(를) 추가하여 URL을 통해 DPR을 활성화하는 것이 좋습니다.

**계정에 스마트 이미징을 사용하도록 설정하는 지원 사례를 만들려면:**

1. [Admin Console을 사용하여 새 지원 사례 만들기를 시작합니다](https://helpx.adobe.com/kr/enterprise/using/support-for-experience-cloud.html).
1. 지원 사례에 다음 정보를 제공하십시오.

   * **기본 연락처 세부 정보:**

      * 이름, 이메일 및 전화번호를 입력합니다.

   * **사용할 스마트 이미징 기능:**

      * 계정에 대해 원하는 기능을 나열합니다.

         * 브라우저 형식 변환: WebP 또는 AVIF
         * 네트워크 대역폭 최적화
         * DPR: DPR에서는 올바른 `dprValue`을(를) 결정하기 위해 클라이언트측을 조정해야 합니다. Adobe 따라서 `dpr=on,dprValue`을(를) 추가하여 URL을 통해 DPR을 활성화하는 것이 좋습니다.

   * **스마트 이미징용 도메인:**

      * *`company.com`* 또는 *`mycompany.scene7.com`*&#x200B;과(와) 같은 모든 관련 도메인을 나열합니다.
      * 스마트 이미징은 일반 도메인과 사용자 지정 도메인을 모두 지원합니다.
      * 도메인을 식별하려면 [Dynamic Media Classic 데스크톱 응용 프로그램](https://experienceleague.adobe.com/ko/docs/dynamic-media-classic/using/getting-started/signing-out#getting-started)을 열고 회사 계정에 로그인하세요.

         1. **[!UICONTROL 설정]** > **[!UICONTROL 응용 프로그램 설정]** > **[!UICONTROL 일반 설정]**(으)로 이동합니다.
         1. 도메인을 확인하려면 **[!UICONTROL 게시된 서버 이름]** 필드를 찾으십시오.
         1. 다른 공급자가 관리하는 CDN이 아니라 Adobe의 CDN을 사용 중인지 확인합니다.

   * **HTTP/2 지원 표시:**

      * HTTP/2에서 작동하는 데 스마트 이미징이 필요한지 여부를 지정합니다.

1. Adobe 고객 지원에서는 요청된 스마트 이미징 기능을 기본적으로 활성화하므로 매개 변수를 URL에 수동으로 추가할 필요가 없습니다.
1. Adobe 캐싱을 통해 성능을 극대화하려면 TTL(Time To Live)을 최소 24시간으로 설정하는 것이 좋습니다.
TTL을 조정하려면 다음을 수행하십시오.

   1. **Dynamic Media Classic의 경우:**
      1. **[!UICONTROL 설치]** > **[!UICONTROL 응용 프로그램 설치]** > **[!UICONTROL Publish 설치]** > **[!UICONTROL 이미지 서버]**&#x200B;로 이동합니다.
      1. **[!UICONTROL 기본 클라이언트 캐시 시간을 Live로 설정]** 값을 24시간 이상으로 설정합니다.
   1. **Adobe Experience Manager의 Dynamic Media:**
      1. [다음 지침](/help/assets/dm-publish-settings.md#common-thumbnail-attributes-tab)을 따르십시오.
      1. 24시간 이상 동안 **[!UICONTROL Expiration]** 값을 설정하십시오.

+++

+++스마트 이미징을 사용하여 계정을 활성화할 수 있는 시기는 언제입니까?

고객 지원 팀은 대기 목록에 따라 요청을 받은 순서대로 요청을 처리합니다.

>[!NOTE]
>
>스마트 이미징을 활성화하면 Adobe이 캐시를 지우므로 리드 타임이 길 수 있습니다. 따라서 특정 시간에 몇 개의 고객 전환만 처리할 수 있습니다.

+++

+++스마트 이미징을 사용하도록 전환할 때의 위험은 무엇입니까?

고객 웹 페이지에는 위험이 없습니다. 그러나 스마트 이미징으로 전환하면 CDN 캐시가 지워집니다. 이 작업에는 Experience Manager 시 Dynamic Media Classic 또는 Dynamic Media의 새 구성으로 이동하는 작업이 포함됩니다.

초기 전환 중에 캐시가 다시 빌드될 때까지 캐시가 아닌 이미지가 Adobe 원본 서버에 직접 히트합니다. 이와 같이 Adobe은 원점에서 요청을 가져올 때 수용 가능한 성능이 유지되도록 한 번에 몇 개의 고객 전환을 처리할 계획입니다. 대부분의 고객의 경우 캐시는 ~1~2일 내에 CDN에서 다시 완전히 빌드됩니다.

+++

+++스마트 이미징이 예상대로 작동하는지 확인하려면 어떻게 해야 합니까?

1. 계정이 Smart Imaging으로 구성된 후 브라우저에서 Dynamic Media Classic 또는 Adobe Experience Manager - Dynamic Media 이미지 URL을 로드합니다.
1. 브라우저에서 **[!UICONTROL 보기]** > **[!UICONTROL 개발자]** > **[!UICONTROL 개발자 도구]**(으)로 이동하여 Chrome 개발자 창을 엽니다. 또는 원하는 브라우저 개발자 도구를 선택합니다.

1. 개발자 도구가 열려 있을 때 캐시가 비활성화되었는지 확인합니다.

   * Windows®에서 개발자 도구 창의 설정으로 이동한 다음 **[!UICONTROL 캐시 사용 안 함(devtools가 열려 있는 동안)]** 확인란을 선택합니다.
   * macOS의 개발자 창의 **[!UICONTROL 네트워크]** 탭에서 **[!UICONTROL 캐시 비활성화]**&#x200B;를 선택합니다.

1. 콘텐츠 유형이 적절한 형식으로 변환되는지 확인합니다. 다음 스크린샷은 Chrome에서 PNG 이미지가 WebP로 동적으로 변환되는 모습을 보여 줍니다. 도메인에 AVIF가 활성화되어 있으면 콘텐츠 유형에 AVIF가 표시될 수도 있습니다.
1. 다른 브라우저 및 사용자 조건에서 이 테스트를 반복합니다.

>[!NOTE]
>
>일부 이미지는 변환되지 않습니다. 스마트 이미징은 전환이 성능을 향상시킬 수 있는지 여부를 결정합니다. 예상되는 성능 향상이 없거나 형식이 JPEG 또는 PNG가 아닌 경우 이미지가 변환되지 않는 경우가 있습니다.

![image2017-11-14_15398](/help/assets/assets/image2017-11-14_15398.png)

+++

+++성능 향상을 어떻게 알 수 있습니까? 스마트 이미징의 이점을 알 수 있는 방법이 있습니까?

스마트 이미징 헤더는 스마트 이미징의 이점을 결정합니다. 스마트 이미징을 사용하도록 설정하면 이미지를 요청한 후 **[!UICONTROL 응답 헤더]** 제목 아래에 다음 강조 표시된 예와 같이 `-X-Adobe-Smart-Imaging`이(가) 표시됩니다.

![스마트 이미징 헤더](/help/assets/assets-dm/smart-imaging-header2.png)

이 헤더에는 다음 사항이 표시됩니다.

* 스마트 이미징이 회사에서 작동 중입니다.
* 양수 값은 전환이 성공했음을 의미합니다. 이 경우 새 WebP 이미지가 반환됩니다.
* 음수 값은 전환이 성공하지 않았음을 의미합니다. 이 경우, 요청된 원본 이미지가 반환됩니다(지정되지 않은 경우 기본적으로 JPEG).
* 양수 값은 요청된 이미지와 새 이미지 간의 바이트 차이를 보여 줍니다. 위의 예에서 저장된 바이트는 하나의 이미지에 대해 `75048` 또는 약 75KB입니다.
* 음수 값은 요청된 이미지가 새 이미지보다 작음을 의미합니다. 음수 크기 차이가 표시되지만, 제공된 이미지는 원래 요청된 이미지입니다.

>[!NOTE]
>
>**X-Adobe-Smart-Imaging = -1(WebP 제공)**
>
>`X-Adobe-Smart-Imaging`의 값이 -1이고 WebP가 계속 배달 중인 경우 스마트 이미징이 활성화됩니다. 그러나 캐시가 오래되어 크기 이점이 계산되지 않았습니다. 이미지의 URL에서 `cache=update`(한 번만)을 사용하여 이 문제를 해결할 수 있습니다.
>수정자 사용의 예:
>`https://smartimaging.scene7.com/is/image/SmartImaging/sample1?cache=update`
>전체 캐시를 무효화하려면 지원 사례를 만들어야 합니다.

+++

+++스마트 이미징에서 AVIF 최적화를 비활성화하려면 어떻게 해야 합니까?

기본적으로 WebP를 제공하는 것으로 다시 전환하려면 동일한 것에 대한 지원 사례를 만듭니다. 평소와 같이 매개 변수 `bfc=off`을(를) 이미지의 URL에 추가하여 스마트 이미징을 끌 수 있습니다. 그러나 스마트 이미징의 URL 수정자에서 WebP 또는 AVIF는 선택할 수 없습니다. 이 기능은 회사 계정 수준에서 유지됩니다.

+++

+++요청에 대해 스마트 이미징을 끌 수 있습니까?

예. 다음 수정자를 추가하여 스마트 이미징을 끌 수 있습니다.

* `bfc=off`(으)로 브라우저 형식 전환을 사용하지 않도록 설정합니다. [브라우저 형식 변환](#bfc)도 참조하세요.
* 장치 픽셀 비율을 해제하려면 `dpr=off`을(를) 사용하십시오. [장치 픽셀 비율](#dpr)도 참조하세요.
* `network=off`(으)로 네트워크 대역폭을 끕니다. [네트워크 대역폭](#network)도 참조하세요.

+++

+++어떤 &quot;조정&quot;을 사용할 수 있습니까? 정의할 수 있는 설정 또는 동작이 있습니까?

스마트 이미징에는 활성화 또는 비활성화할 수 있는 세 가지 옵션이 있습니다.

* [브라우저 형식 변환](#bfc)
* [장치 픽셀 비율](#dpr)
* [네트워크 대역폭](#network)

+++

+++Chrome 웹 브라우저에 fmt=tif가 있는 URL이 있습니다. 하지만 ImageServer 오류로 인해 요청이 실패합니다. 왜일까요?

계정에 스마트 이미징이 활성화되지 않은 경우에는 이 오류가 발생하지 않습니다. 스마트 이미징은 JPEG 또는 PNG 형식에서만 작동합니다.

이 오류를 방지하기 위해 다음 중 하나를 수행할 수 있습니다.

* JPEG 또는 PNG 지정 또는
* `fmt` 한정자를 사용하지 않거나
* 스마트 이미징에서 정의한 브라우저 기본 형식을 사용합니다. 예를 들어 Chrome 웹 브라우저용으로 WebP를 사용할 수 있습니다.

+++

+++이미지의 URL에서 TIFF 이미지를 다운로드하려고 합니다. 어떻게 해야 합니까?

이미지의 URL 경로에 `fmt=tif` 및 `bfc=off`을(를) 추가합니다.

+++

+++스마트 이미징에서 이미지 형식만 관리합니까, 아니면 최상의 결과를 위해 이미지 품질 설정도 관리합니까?

스마트 이미징은 형식과 품질을 모두 사용합니다. 나머지 매개 변수는 이미지의 URL에서 요청한 경우 동일하게 유지됩니다.

+++

+++스마트 이미징에서 품질 설정을 관리하는 경우 설정할 수 있는 최소 및 최대 수가 있습니까? 즉, 60보다 작지 않고 80보다 크지 않은 품질입니까?

현재 그러한 프로비저닝이 없습니다.

+++

+++스마트 이미징에서 자동으로 품질 백분율 출력 설정을 조정합니까? 또는 수동으로 조정된 설정이며 모든 이미지에 적용됩니까? 어떤 범위내에서?

스마트 이미징은 품질 비율을 자동으로 조정합니다. 이러한 품질은 Adobe이 개발한 머신 러닝 알고리즘을 이용하여 결정된다. 이 비율은 범위에 특정하지 않습니다.

+++

+++스마트 이미징에서 어떤 이미지 제공 명령이 지원되거나 무시됩니까?

`fmt` 및 `qlt` 명령만 무시됩니다. 나머지 모든 명령은 지원됩니다.

+++

+++JPEG 이미지만 스마트 이미징으로 대체됩니까? WebP, PNG 또는 다른 것을 요청하면 어떻게 됩니까?

이 기능은 JPEG 및 PNG에만 작동합니다.

+++

+++JPEG 이미지가 때때로 WebP 대신 Chrome으로 반환되는 이유는 무엇입니까?

스마트 이미징은 전환이 유익한지 여부를 결정합니다. 이렇게 하면 변환에 대한 유익한 새 이미지만 반환됩니다.

+++

+++장치 픽셀 비율(dpr) 기능이 합성 이미지에서 예상대로 작동하지 않는 이유는 무엇입니까?

합성 이미지에 너무 많은 레이어가 포함된 경우 위치 수정자를 사용하는 동안 dpr 기능에 영향을 줄 수 있습니다. 이 문제는 알려져 있으며 향후 스마트 이미징 릴리스에서 수정해야 합니다. 다른 스마트 이미징 기능이 예상대로 작동하지 않는 경우 지원 사례를 만들어 문제를 보고할 수 있습니다.

+++

+++스마트 이미징 PNG가 무손실 WebP/AVIF로 변환하는 이유는 무엇입니까?

PNG가 무손실 포맷이므로, 이전 WebP 및 AVIF가 전달되지 않았으므로, 크기가 예상보다 큽니다. 스마트 이미징에서 이제 손실 변환을 지원합니다. 이 문제를 해결하기 위해 이미지 요청에서 수정자 `cache=update`(한 번만)을(를) 사용할 수 있습니다. 이 수정자 사용의 예:

`https://smartimaging.scene7.com/is/image/SmartImaging/sample1?cache=update`

전체 캐시를 무효화하려면 이러한 노력을 요청하는 지원 사례를 만들어야 합니다.

+++

+++스마트 이미징에서 PNG를 사용하여 무손실 변환을 계속하려면 어떻게 해야 합니까?

이제 스마트 이미징에서 품질 수준에 따라 손실 변환을 지원합니다. 회사 설정을 통해 또는 이미지의 URL 경로에 `qlt=100`을(를) 추가하여 품질을 100으로 설정하여 무손실 변환을 계속 사용할 수 있습니다.

+++

