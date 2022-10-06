---
title: 랜딩 페이지와 Adobe Analytics 통합
seo-title: Integrating Landing Pages with Adobe Analytics
description: 랜딩 페이지를 Adobe Analytics과 통합하는 방법을 알아봅니다.
seo-description: Learn how to integrate landing pages with Adobe Analytics.
uuid: 8f6672d1-497f-4ccb-b3cc-f6120fc467ba
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 8ae7ccec-489b-4d20-ac56-6101402fb18a
exl-id: da3f7b7e-87e5-446a-9a77-4b12b850a381
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 26%

---

# 랜딩 페이지와 Adobe Analytics 통합{#integrating-landing-pages-with-adobe-analytics}

AEM은 랜딩 페이지 솔루션을 [Adobe Analytics](https://www.omniture.com/en/products/analytics/sitecatalyst) 다음의 클릭유도문안(CTA) 구성 요소를 사용하여 다음을 수행하십시오.

1. 클릭스루 구성 요소
1. 그래픽 링크 구성 요소

이러한 구성 요소는 Adobe Analytics 변수(트래픽, 전환 변수)와 정보를 Adobe Analytics에 보내는 성공 이벤트를 통해 매핑할 수 있는 특정 특성을 노출합니다.

## 사전 요구 사항 {#prerequisites}

Adobe은 [기존 AEM-Adobe Analytics 통합](/help/sites-administering/adobeanalytics.md) 이 통합이 작동하는 방식을 이해하려면 다음을 수행하십시오.

## 매핑에 사용할 수 있는 구성 요소 {#components-available-for-mapping}

AEM에서 **클릭유도문안** 구성 요소 - **ClickThroughLink** 및 **GraphicalLink** - 사이드킥에 여기에 표시되는 를 Adobe Analytics 변수에 매핑할 수 있습니다.

![chlimage_1-21](assets/chlimage_1-21a.jpeg)

### 랜딩 페이지 구성 요소를 Adobe Analytics에 매핑 {#mapping-landing-page-components-to-adobe-analytics}

랜딩 페이지 구성 요소를 Adobe Analytics에 매핑하려면

1. Adobe Analytics 구성을 만들고 새 프레임워크를 만든 후 드롭다운 메뉴에서 적절한 보고 세트를 선택합니다. 따라서 Adobe Analytics 변수가 가져와서 콘텐츠 파인더에 표시됩니다.
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
   <td>CTA 이미지의 제목입니다 </td>
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

1. 이러한 노출된 특성을 콘텐츠 파인더의 모든 Adobe Analytics 변수와 매핑합니다. 이제 프레임워크를 사용할 준비가 되었습니다.
1. 이제 새 랜딩 페이지를 만들거나 기존 CTA 구성 요소가 있는 기존 랜딩 페이지를 열고 를 클릭할 수 있습니다 **Cloud Services** 탭 **페이지 속성** 사이드 킥에서(터치에 적합한 UI에서) **속성 열기** 을(를) 클릭합니다. **Cloud Services**)을 설정하고 랜딩 페이지에 사용할 프레임워크를 구성합니다. 드롭다운 목록에서 프레임워크를 선택합니다.

   ![chlimage_1-25](assets/chlimage_1-25a.png)

1. 랜딩 페이지로 프레임워크를 구성한 후 구현된 구성 요소를 사용할 수 있으며 CTA에 대한 모든 클릭이 Adobe Analytics에 기록됩니다.
