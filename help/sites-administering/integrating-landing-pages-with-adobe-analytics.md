---
title: 랜딩 페이지를 Adobe Analytics과 통합
seo-title: 랜딩 페이지를 Adobe Analytics과 통합
description: 랜딩 페이지를 Adobe Analytics과 통합하는 방법을 알아봅니다.
seo-description: 랜딩 페이지를 Adobe Analytics과 통합하는 방법을 알아봅니다.
uuid: 8f6672d1-497f-4ccb-b3cc-f6120fc467ba
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 8ae7ccec-489b-4d20-ac56-6101402fb18a
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 25%

---


# 랜딩 페이지를 Adobe Analytics{#integrating-landing-pages-with-adobe-analytics}과 통합

AEM은 다음 CTA(Call-to-Action) 구성 요소를 사용하여 랜딩 페이지 솔루션을 [Adobe Analytics](https://www.omniture.com/en/products/analytics/sitecatalyst)과(와) 통합했습니다.

1. 클릭스루 구성 요소
1. 그래픽 링크 구성 요소

이러한 구성 요소는 Adobe Analytics 변수(트래픽, 전환 변수)와 정보를 Adobe Analytics에 보내는 성공 이벤트를 통해 매핑할 수 있는 특정 속성을 노출합니다.

## 전제 조건 {#prerequisites}

Adobe은 이 통합이 어떻게 작동하는지를 이해하려면 [기존 AEM-Adobe Analytics 통합](/help/sites-administering/adobeanalytics.md)을(를) 거치는 것이 좋습니다.

## 매핑에 사용할 수 있는 구성 요소 {#components-available-for-mapping}

AEM에서 사이드킥에 표시된 **Call to Action** 구성 요소 - **ClickThroughLink** 및 **GraphicalLink**)는 Adobe Analytics 변수에 매핑할 수 있습니다.

![chlimage_1-21](assets/chlimage_1-21a.jpeg)

### 랜딩 페이지 구성 요소를 Adobe Analytics {#mapping-landing-page-components-to-adobe-analytics}에 매핑

랜딩 페이지 구성 요소를 Adobe Analytics에 매핑하려면:

1. Adobe Analytics 구성을 만들고 새 프레임워크를 만든 후 드롭다운 메뉴에서 적절한 보고 세트를 선택합니다. 그러면 Adobe Analytics 변수가 Content Finder에 표시됩니다.
1. 사이드킥의 클릭유도문안(CTA) 구성 요소를 페이지의 중앙에 있는 매핑 영역으로 적절히 드래그 드롭합니다.

<table>
 <tbody>
  <tr>
   <td><strong>구성 요소 이름</strong></td>
   <td><strong>노출된 특성</strong></td>
   <td><strong>특성의 의미</strong></td>
  </tr>
  <tr>
   <td><strong>CTA 클릭스루 링크</strong></td>
   <td><i>eventdata.clickthroughLinkLabel</i> <br /> </td>
   <td>링크에 있는 레이블이나 링크의 텍스트 </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.clickthroughLinkTarget</i> <br /> </td>
   <td>링크를 클릭하면 이동하는 대상 </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.events.clickthroughLinkClick</i> <br /> </td>
   <td>클릭 이벤트 </td>
  </tr>
  <tr>
   <td><strong>CTA 그래픽 링크</strong></td>
   <td><i>eventdata.clicktroughImageLabel</i> <br /> </td>
   <td>CTA 이미지의 제목 </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.clicktroughImageTarget</i> <br /> </td>
   <td>링크가 들어 있는 이미지를 클릭하면 이동하는 대상</td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.clicktroughImageAsset</i> <br /> </td>
   <td>보관소에 있는 이미지 자산 경로 </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.events.clicktroughImageClick</i> <br /> </td>
   <td>클릭 이벤트</td>
  </tr>
 </tbody>
</table>

1. 이러한 노출된 특성을 컨텐츠 파인더의 모든 Adobe Analytics 변수와 매핑합니다. 이제 프레임워크를 사용할 준비가 되었습니다.
1. 이제 새 랜딩 페이지를 만들거나 기존 CTA 구성 요소가 있는 기존 랜딩 페이지를 열고 사이드킥의 **페이지 속성**&#x200B;에 있는 **Cloud Services** 탭을 클릭하고(터치에 적합한 UI에서 **속성 열기**&#x200B;를 선택하고 **Cloud Services**&#x200B;을 클릭합니다.) 랜딩 페이지에 사용할 수 있습니다. 드롭다운 목록에서 프레임워크를 선택합니다.

   ![chlimage_1-25](assets/chlimage_1-25a.png)

1. 랜딩 페이지와 함께 프레임워크를 구성한 후에는 구현된 구성 요소를 사용할 수 있으며 CTA에 대한 모든 클릭은 Adobe Analytics에 기록됩니다.

