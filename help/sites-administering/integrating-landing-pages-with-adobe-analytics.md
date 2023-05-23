---
title: Adobe Analytics과 랜딩 페이지 통합
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
ht-degree: 0%

---

# Adobe Analytics과 랜딩 페이지 통합{#integrating-landing-pages-with-adobe-analytics}

AEM은 랜딩 페이지 솔루션을 와 통합했습니다. [Adobe Analytics](https://www.omniture.com/en/products/analytics/sitecatalyst) 다음 CTA(콜 투 액션) 구성 요소를 사용하여

1. 클릭스루 구성 요소
1. 그래픽 링크 구성 요소

이러한 구성 요소는 Adobe Analytics 변수(트래픽, 전환 변수) 및 성공 이벤트를 통해 매핑하여 정보를 Adobe Analytics에 보낼 수 있는 특정 속성을 표시합니다.

## 사전 요구 사항 {#prerequisites}

Adobe은 다음을 수행하는 것을 권장합니다. [기존 AEM-Adobe Analytics 통합](/help/sites-administering/adobeanalytics.md) 이 통합이 작동하는 방식을 이해합니다.

## 매핑에 사용할 수 있는 구성 요소 {#components-available-for-mapping}

AEM에서 **클릭 유도 문안** 구성 요소 - **클릭스루 링크** 및 **GraphicalLink** - 여기 사이드 킥에 표시되며, Adobe Analytics 변수에 매핑할 수 있습니다.

![chlimage_1-21](assets/chlimage_1-21a.jpeg)

### Adobe Analytics에 랜딩 페이지 구성 요소 매핑 {#mapping-landing-page-components-to-adobe-analytics}

랜딩 페이지 구성 요소를 Adobe Analytics에 매핑하려면 다음을 수행하십시오.

1. Adobe Analytics 구성을 만들고 새 프레임워크를 만든 후 드롭다운 메뉴에서 적절한 보고 세트를 선택합니다. 그러면 Adobe Analytics 변수를 가져와 컨텐츠 파인더에 표시됩니다.
1. 필요에 따라 사이드 킥에서 CTA(콜 투 액션) 구성 요소를 페이지 중간에 있는 매핑 영역으로 끌어서 놓습니다.

<table>
 <tbody>
  <tr>
   <td><strong>구성 요소 이름</strong></td>
   <td><strong>속성 노출됨</strong></td>
   <td><strong>속성의 의미</strong></td>
  </tr>
  <tr>
   <td><strong>CTA 클릭스루 링크</strong></td>
   <td><i>eventdata.clickthroughLinkLabel</i> <br /> </td>
   <td>링크의 레이블 또는 링크 텍스트 </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.clickthroughLinkTarget</i> <br /> </td>
   <td>링크를 클릭할 때 이동하는 대상 </td>
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
   <td>링크가 포함된 이미지를 클릭할 때 이동되는 대상</td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.clicktroughImageAsset</i> <br /> </td>
   <td>저장소의 이미지 에셋 경로 </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.events.clicktroughImageClick</i> <br /> </td>
   <td>클릭 이벤트</td>
  </tr>
 </tbody>
</table>

1. 노출된 이러한 속성을 컨텐츠 파인더의 모든 Adobe Analytics 변수와 매핑합니다. 이제 프레임워크를 사용할 준비가 되었습니다.
1. 이제 새 랜딩 페이지를 만들거나 기존 CTA 구성 요소로 기존 랜딩 페이지를 열고 **Cloud Services** 의 탭 **페이지 속성** 터치에 적합한 UI의 사이드 킥에서 을 선택합니다 **속성 열기** 및 클릭 **Cloud Services**) 랜딩 페이지에서 사용할 프레임워크를 구성합니다. 드롭다운 목록에서 프레임워크를 선택합니다.

   ![chlimage_1-25](assets/chlimage_1-25a.png)

1. 이제 랜딩 페이지로 프레임워크를 구성한 후 계측된 구성 요소를 사용할 수 있으며 CTA에 대한 모든 클릭이 Adobe Analytics에 기록됩니다.
