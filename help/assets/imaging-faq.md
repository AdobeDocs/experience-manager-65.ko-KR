---
title: 스마트 이미징
description: 스마트 이미징은 각 사용자의 고유한 보기 특성을 활용하여 경험에 최적화된 적합한 이미지를 자동으로 제공하여 향상된 성능과 참여를 유도합니다.
uuid: c11e52ba-8d64-4dc5-b30a-fc10c2b704e5
contentOwner: Rick Brough
topic-tags: dynamic-media
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: bf8c6bbd-847d-43d7-9ff4-7231bfd8d107
translation-type: tm+mt
source-git-commit: f786b35e77c6b862f7fc6e45d3d0af56a51e3e95
workflow-type: tm+mt
source-wordcount: '1870'
ht-degree: 1%

---


# 스마트 이미징 {#smart-imaging}

## &quot;스마트 이미징&quot;이란 무엇입니까?{#what-is-smart-imaging}

스마트 이미징 기술은 Adobe Sensei AI 기능을 활용하고 기존의 &quot;이미지 사전 설정&quot;과 연동하여 클라이언트 브라우저 기능을 기반으로 이미지 포맷, 크기 및 품질을 자동으로 최적화하여 이미지 전달 성능을 향상시킵니다.

스마트 이미징은 또한 Adobe의 동급 최강의 프리미엄 CDN 서비스와 완벽하게 통합됨으로써 향상된 성능을 제공합니다. 이 서비스는 서버의 기본 경로보다 지연 시간이 가장 짧은 서버, 네트워크 및 피어링 지점 간의 최적의 인터넷 경로를 찾아냅니다.

다음 이미지 자산 예는 추가된 스마트 이미징 최적화를 보여줍니다.

| 이미지<br>(URL) | 썸네일 | 크기<br>(JPEG) | 크기(WebP)<br>(스마트 이미징 포함) | % 감소 |
|---|---|---|---|---|
| [이미지 1](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_6?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture1](/help/assets/assets-dm/picture1.png) | 73.75KB | 45.92KB | 38% |
| [이미지 2](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_3?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![그림2](/help/assets/assets-dm/picture2.png) | 191KB | 70.66KB | 63% |
| [이미지 3](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_2?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![그림3](/help/assets/assets-dm/picture3.png) | 96.64KB | 39.44KB | 59% |
| [이미지 4](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_1?hei=500&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![그림4](/help/assets/assets-dm/picture4.png) | 315.80KB | 178.19KB | 44% |
|  |  |  |  | 평균 = 51% |

위와 마찬가지로 Adobe은 라이브 고객 사이트에서 7009개의 URL을 사용하여 테스트를 실시했으며 스마트 이미징 기능 덕분에 JPEG에 대한 평균 38% 이상의 파일 크기 최적화 및 WebP 포맷의 PNG에 대한 31% 이상의 파일 크기 최적화를 수행할 수 있었습니다.

## 최신 스마트 이미징의 주요 이점은 무엇입니까?{#what-are-the-key-benefits-of-smart-imaging}

이미지가 페이지 로드 시간의 대부분을 차지하기 때문에 성능 향상은 높은 전환, 사이트에서 보낸 시간, 낮은 사이트 이탈률 등 비즈니스 KPI에 엄청난 영향을 미칠 수 있습니다.

스마트 이미징 최신 버전의 향상된 기능:

* 런타임 시 최적화된 컨텐츠를 즉시 제공합니다.
* Adobe Sensei 기술을 사용하여 이미지 요청에 지정된 품질(qlt)에 따라 변환합니다.
* &quot;bfc&quot; URL 매개 변수를 사용하여 스마트 이미징을 끌 수 있습니다.
* TTL(Time To Live) 독립적입니다. 이전에는, 스마트 이미징이 작동하려면 최소 TTL이 12시간이다.
* 이전에는 원본 이미지와 파생 이미지가 모두 캐시되었으며 캐시를 무효화하는 2단계 프로세스였습니다. 최신 Smart Imaging에서는 파생상품만 캐시되어 단일 단계 캐시 무효화 프로세스를 허용합니다.
* 사용자 지정 헤더를 규칙 세트에 사용하는 고객(예: [이미지 응답에 사용자 지정 헤더 값 추가|Dynamic Media Classic](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/add-custom-header-val-image.html))은 이전 버전의 Smart Imaging과는 달리, 헤더가 차단되지 않으므로 최신 스마트 이미징의 이점을 제공합니다.

## 스마트 이미징과 관련된 라이선스 비용이 있습니까?{#are-there-any-licensing-costs-associated-with-smart-imaging}

아니오. 스마트 이미징은 Dynamic Media Classic 또는 Adobe Experience Manager - Dynamic Media(On Prem, AMS 및 AEM을 Cloud Service으로 사용)의 기존 라이선스에 포함되어 있습니다.

>[!NOTE]
>
>Dynamic Media - 하이브리드 고객은 스마트 이미징을 사용할 수 없습니다.


## 스마트 이미징은 어떻게 작동합니까?{#how-does-smart-imaging-work}

소비자가 이미지를 요청할 때 Adobe는 사용자 특성을 확인하고 사용 중인 브라우저를 기반으로 적절한 이미지 형식으로 변환합니다. 이러한 형식 변환은 시각적 품질을 저하시키지 않는 방식으로 수행됩니다. 스마트 이미징은 브라우저 기능을 기반으로 이미지를 다른 형식으로 자동으로 변환합니다.

* 다음 브라우저를 위해 WebP로 자동 변환:
   * Chrome
   * Firefox
   * Microsoft Edge
   * Safari 14.0 +
      * iOS 14.0 이상 및 macOS BigSur 이상이 설치된 Safari 14 전용
   * Android
   * Opera
* 다음에 대한 기존 브라우저 지원:

   | 브라우저 | 브라우저/OS 버전 | 형식 |
   | --- | --- | --- |
   | Safari | iOS 14.0 이전 버전 | JPEG2000 |
   | Edge | 18 이하 | JPEGXR |
   | Internet Explorer | 9+ | JPEGXR |
* 이러한 형식을 지원하지 않는 브라우저의 경우 원래 요청한 이미지 형식이 제공됩니다.

원본 이미지 크기가 스마트 이미징에서 만드는 크기보다 작은 경우 원본 이미지가 제공됩니다.

## 지원되는 이미지 형식은 무엇입니까?{#what-image-formats-are-supported}

스마트 이미징에 대해 다음 이미지 형식이 지원됩니다.
* JPEG
* PNG

<!-- For any other format mentioned in a URL, you should explicity turn off Smart Imaging.  Append modifier `bfc=off` to the URL for file formats other than JPEG and PNG. You can accomplish this by using either one of the following methods:

* Use a ruleset if the `fmt` modifier is mentioned in the URL. 
* Append in URL modifiers field of the presets concerned.

Adobe is working on a permanent fix that does not require you to append `bfc=off` for `fmt !=JPEG` or `fmt !=PNG`. This topic will be updated after the fix is delivered. -->

## 스마트 이미징은 이미 사용 중인 기존 이미지 사전 설정과 어떻게 작동합니까?{#how-does-smart-imaging-work-with-our-existing-image-presets-that-are-already-in-use}

스마트 이미징은 기존의 &quot;이미지 사전 설정&quot;과 연동되며 요청된 파일 형식이 JPEG 또는 PNG인 경우 품질(qlt) 및 형식(fmt)을 제외하고 모든 이미지 설정을 준수합니다. 포맷 변환의 경우 이미지 사전 설정 설정에 의해 정의된 대로 전체 시각적 품질을 유지하지만 파일 크기는 작습니다. 원본 이미지 크기가 스마트 이미징에서 만드는 크기보다 작은 경우 원본 이미지가 제공됩니다.

<!-- In addition, if your image presets are used to return `fmt !=JPEG` or `fmt !=PNG`, be sure append `bfc=off` in the preset modifier field to return the requested file format. -->

## URL, 이미지 사전 설정을 변경하거나 Smart Imaging을 위해 내 사이트에 새로운 코드를 배포해야 합니까?{#will-i-have-to-change-any-urls-image-presets-or-deploy-any-new-code-on-my-site-for-smart-imaging}

스마트 이미징은 기존 사용자 정의 도메인에 스마트 이미징을 구성하는 경우 기존 이미지 URL 및 이미지 사전 설정과 원활하게 작동합니다. 또한 Smart Imaging에서는 사용자의 브라우저를 감지하기 위해 웹 사이트에 코드를 추가할 필요가 없습니다. 이 모든 것은 자동으로 처리됩니다.

스마트 이미징을 사용하도록 새 사용자 지정 도메인을 구성해야 하는 경우 이 사용자 지정 도메인을 반영하도록 URL을 업데이트해야 합니다.

또한 [스마트 이미징을 사용할 수 있습니까?를 참조하십시오.](#am-i-eligible-to-use-smart-imaging) 고급 이미징의 전제 조건을 이해하려면

<!-- No. Smart Imaging works seamlessly with your existing image URLs and image presets. In addition, Smart Imaging does not require you to add any code on your website to detect a user's browser. All of this is handled automatically. -->

<!-- As mentioned earlier, Smart Imaging supports only JPEG and PNG image formats. For other formats, you need to append the `bfc=off` modifier to the URL as described earlier. -->

## 스마트 이미징은 HTTPS를 사용합니까? HTTP/2는 어떻습니까?{#does-smart-imaging-working-with-https-how-about-http}

스마트 이미징은 HTTP 또는 HTTPS를 통해 제공되는 이미지와 연동됩니다. 또한 HTTP/2에서도 작동합니다.

## 스마트 이미징을 사용할 수 있습니까?{#am-i-eligible-to-use-smart-imaging}

스마트 이미징을 사용하려면 회사의 AEM 계정에 있는 Dynamic Media Classic 또는 Dynamic Media이 다음 요구 사항을 충족해야 합니다.

* Adobe 번들 CDN(Content Delivery Network)을 라이선스의 일부로 사용할 수 있습니다.
* 일반 도메인이 아닌 전용 도메인(예: `images.company.com` 또는 `mycompany.scene7.com`)을 사용합니다(예: `s7d1.scene7.com`, `s7d2.scene7.com` 또는 `s7d13.scene7.com`).

도메인을 찾으려면 [Dynamic Media Classic 데스크톱 응용 프로그램](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)을 열고 회사 계정 또는 계정에 로그인합니다.

**[!UICONTROL 설정 > 응용 프로그램 설정 > 일반 설정을 누릅니다.]** 게시된 서버 이름 **[!UICONTROL 이라는 필드를 찾습니다.]** 현재 범용 도메인을 사용하고 있는 경우 기술 지원 티켓을 제출할 때 이 전환의 일부로 사용자 지정 도메인으로 이동을 요청할 수 있습니다.

첫 번째 사용자 정의 도메인은 Dynamic Media 라이선스에 대한 추가 비용이 없습니다.

## 내 계정에 대해 스마트 이미징을 활성화하는 프로세스는 무엇입니까?{#what-is-the-process-for-enabling-smart-imaging-for-my-account}

스마트 이미징 사용을 요청해야 합니다.자동으로 활성화되지 않습니다.

1. [Admin Console을 사용하여 지원 사례를 만듭니다.](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)
1. 지원 케이스에 다음 정보를 제공합니다.

   1. 기본 연락처 이름, 이메일, 전화.
   1. 스마트 이미징을 사용하도록 설정할 모든 도메인(즉, `images.company.com` 또는 `mycompany.scene7.com`).

      도메인을 찾으려면 [Dynamic Media Classic 데스크톱 응용 프로그램](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)을 열고 회사 계정 또는 계정에 로그인합니다.

      **[!UICONTROL 설정 > 응용 프로그램 설정 > 일반 설정을 클릭합니다.]**

      **[!UICONTROL 게시된 서버 이름]** 레이블이 있는 필드를 찾습니다.
   1. Adobe을 통해 CDN을 사용하고 있고 직접 관계로 관리되지 않는지 확인합니다.
   1. `images.company.com` 또는 `mycompany.scene7.com`과 같은 전용 도메인을 사용하고 있고 `s7d1.scene7.com`, `s7d2.scene7.com`, `s7d13.scene7.com` 등의 일반 도메인이 아닌지 확인합니다.

      도메인을 찾으려면 [Dynamic Media Classic 데스크톱 응용 프로그램](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)을 열고 회사 계정 또는 계정에 로그인합니다.

      **[!UICONTROL 설정 > 응용 프로그램 설정 > 일반 설정을 클릭합니다.]**

      **[!UICONTROL 게시된 서버 이름 필드를 찾습니다.]** 현재 범용 Dynamic Media Classic 도메인을 사용하고 있는 경우 이 전환의 일부로 사용자 정의 도메인으로 이동을 요청할 수 있습니다.
   1. HTTP/2 이상에서 작업하는 경우에도 이 기능이 필요한지 여부를 표시합니다.

1. 기술 지원에서 요청을 제출한 순서에 따라 스마트 이미징 고객 대기 목록에 추가합니다.
1. Adobe이 요청을 처리할 준비가 되면 지원 담당자가 타겟 날짜를 조정하고 설정하기 위해 사용자에게 연락합니다.
1. **옵션**:Adobe에서 새 기능을 프로덕션으로 푸시하기 전에 스테이징에서 스마트 이미징을 테스트할 수 있습니다.
1. 지원이 완료되면 알림 메시지가 표시됩니다.
1. 스마트 이미징의 성능 향상을 최대화하려면 Adobe에서 TTL(Time To Live)을 24시간 이상으로 설정하는 것이 좋습니다. TTL은 CDN이 자산을 캐시하는 기간을 정의합니다. 이 설정을 변경하려면:

   1. Dynamic Media Classic을 사용하는 경우 **[!UICONTROL 설정 > 응용 프로그램 설정 > 제작 설정 > 이미지 서버를 클릭합니다.]** 기본  **[!UICONTROL 클라이언트 캐시 시간을 Livvalue]** 로 24 이상으로 설정합니다.
   1. Dynamic Media을 사용하는 경우 [다음 지침](config-dynamic.md)을 따릅니다. **[!UICONTROL 만료]** 값을 24시간 이상 설정합니다.

## 스마트 이미징으로 계정을 활성화할 수 있는 시기는 언제입니까?{#when-can-i-expect-my-account-to-be-enabled-with-smart-imaging}

요청은 대기 목록에 따라 기술 지원 센터에서 수신한 순서대로 처리됩니다.

>[!NOTE]
스마트 이미징을 활성화하면 Adobe이 캐시를 지우므로 리드 타임이 길어질 수 있습니다. 따라서 지정된 시간에 일부 고객 전환만 처리할 수 있습니다.

## 스마트 이미징을 사용하도록 전환하면 어떤 위험이 있습니까?{#what-are-the-risks-with-switching-over-to-use-smart-imaging}

고객 웹 페이지에 대한 위험은 없습니다. 그러나 Smart Imaging로의 전환은 AEM에서 Dynamic Media Classic 또는 Dynamic Media의 새로운 구성으로 이동하는 것을 포함하므로 CDN의 캐시를 지웁니다.

초기 전환 중에 캐시되지 않은 이미지는 캐시를 다시 작성할 때까지 Adobe의 원본 서버를 직접 히트합니다. 이러한 이유로 Adobe은 한 번에 몇 개의 고객 전환을 처리하여 원본 고객의 요청을 가져올 때 허용되는 성능을 유지할 수 있도록 합니다. 대부분의 고객의 경우 캐시는 1~2일 이내에 CDN에 완전히 재구성됩니다.

## 스마트 이미징이 예상대로 작동하는지 확인하려면 어떻게 해야 합니까? {#how-can-i-verify-whether-smart-imaging-is-working-as-expected}

1. 계정을 스마트 이미징으로 구성한 후 브라우저에서 Dynamic Media Classic 또는 Adobe Experience Manager - Dynamic Media 이미지 URL을 로드합니다.
1. 브라우저에서 **[!UICONTROL 보기 > 개발자 > 개발자 도구]**&#x200B;를 클릭하여 크롬 개발자 창을 엽니다. 또는 원하는 브라우저 개발자 도구를 선택합니다.

1. 개발자 도구가 열려 있을 때 캐시가 비활성화되었는지 확인합니다.

   * Windows의 경우 - 개발자 도구 창의 설정으로 이동한 다음 **[!UICONTROL 캐시 비활성화(장치 도구가 열려 있는 동안)]** 확인란을 선택합니다.
   * Mac - 개발자 창의 **[!UICONTROL 네트워크]** 탭에서 **[!UICONTROL 캐시 비활성화]**&#x200B;를 선택합니다.

1. 컨텐트 유형이 적절한 형식으로 변형됨을 확인합니다. 다음 스크린샷은 Chrome에서 WebP로 동적으로 변환되는 PNG 이미지를 보여줍니다.
1. 다른 브라우저 및 사용자 조건에서 이 테스트를 반복합니다.

>[!NOTE]
일부 이미지는 변환되지 않습니다. 스마트 이미징에서는 성능을 개선하기 위해 전환이 필요한지 여부를 결정합니다. 성능 증가가 예상되지 않거나 형식이 JPEG 또는 PNG가 아닌 경우 이미지가 변환되지 않는 경우도 있습니다.

![image2017-11-14_15398](assets/image2017-11-14_15398.png)

## 요청에 따라 스마트 이미징을 끌 수 있습니까?{#turning-off-smart-imaging}

예. URL에 수정자 `bfc=off`을 추가하여 스마트 이미징을 끌 수 있습니다.

## 어떤 &quot;조정&quot;을 사용할 수 있습니까? 정의할 수 있는 설정 또는 동작이 있습니까? (#tuning-settings)

현재 스마트 이미징을 활성화하거나 비활성화할 수도 있습니다. 다른 조정은 사용할 수 없습니다.

## 스마트 이미징이 품질 설정을 관리하는 경우 설정할 수 있는 최소 및 최대 수가 있습니까? 예를 들어 &quot;60 미만&quot; 및 &quot;80보다 큰 품질&quot;을 설정할 수 있습니까? (#minimum-maximum)

현재 스마트 이미징에는 이러한 제공 기능이 없습니다.

## 경우에 따라 JPEG 이미지가 WebP 이미지 대신 크롬으로 반환되는 경우가 있습니다. 왜 그런 일이 생기죠? (#jpeg-webp)

스마트 이미징은 변환이 유익한지 여부를 결정합니다. 변환 결과 비교 가능한 품질과 파일 크기가 작은 경우에만 새 이미지를 반환합니다.
