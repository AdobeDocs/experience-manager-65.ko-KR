---
title: 적응형 템플릿 렌더링
description: Adobe Experience Manager의 적응형 템플릿 렌더링에 대해 알아봅니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: 58cac3b1-b7cd-44b2-b89b-f5ee8811c198
source-git-commit: b703f356f9475eeeafb1d5408c650d9c6971a804
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 2%

---

# 적응형 템플릿 렌더링{#adaptive-template-rendering}

적응형 템플릿 렌더링은 변형이 있는 페이지를 관리하는 방법을 제공합니다. 원래 모바일 장치(예: 기능 전화와 스마트폰)에 대한 다양한 HTML 출력을 전달하는 데 유용하며, 이 기능은 다른 마크업이나 HTML 출력을 필요로 하는 다양한 장치에 경험을 전달해야 할 때 유용합니다.

## 개요 {#overview}

템플릿은 응답형 그리드 주위에 구축되며 이러한 템플릿을 기반으로 작성된 페이지는 완전히 응답형이므로 클라이언트 장치의 뷰포트에 자동으로 조정됩니다. 페이지 편집기에서 에뮬레이터 도구 모음을 사용하여 작성자는 레이아웃을 특정 디바이스로 타깃팅할 수 있습니다.

적응형 렌더링을 지원하는 템플릿을 설정할 수도 있습니다. 장치 그룹이 올바르게 구성되면 에뮬레이터 모드에서 장치를 선택할 때 URL에 다른 선택기로 페이지가 렌더링됩니다. 선택기를 사용하여 URL을 통해 특정 페이지 렌더링을 직접 호출할 수 있습니다.

장치 그룹을 설정할 때 기억하십시오.

* 모든 장치는 하나 이상의 장치 그룹에 있어야 합니다.
* 하나의 장치가 여러 장치 그룹에 있을 수 있습니다.
* 디바이스는 여러 디바이스 그룹에 있을 수 있으므로 선택기를 결합할 수 있습니다.
* 선택기의 조합은 저장소에서 지속되므로 하향식으로 평가됩니다.

>[!NOTE]
>
>장치 그룹**반응형 장치에는 선택기가 없습니다. 반응형 디자인을 지원하는 것으로 인식되는 장치에는 적응형 레이아웃이 필요하지 않은 것으로 간주되기 때문입니다

## 구성 {#configuration}

적응형 렌더링 선택기는 기존 장치 그룹에 대해 구성하거나 [직접 만든 그룹입니다.](/help/sites-developing/mobile.md#device-groups)

이 예에서는 기존 장치 그룹을 구성합니다 **스마트폰** 적응형 렌더링 선택기를 의 일부로 사용 **경험 페이지** We.Retail 내의 템플릿입니다.

1. 에서 적응형 선택기가 필요한 장치 그룹 편집 `http://localhost:4502/miscadmin#/etc/mobile/groups`

   옵션 설정 **에뮬레이터 사용 안 함** 저장하십시오.

   ![chlimage_1-157](assets/chlimage_1-157.png)

1. 선택기는 다음에 사용할 수 있습니다. **블랙베리®** 및 **IPHONE 4** 장치 그룹 제공 **스마트폰** 가 다음 단계에서 템플릿 및 페이지 구조에 추가됩니다.

   ![chlimage_1-158](assets/chlimage_1-158.png)

1. CRXDE Lite을 사용하면 장치 그룹을 다중 값 문자열 속성에 추가하여 템플릿에서 사용할 수 있습니다 `cq:deviceGroups` 템플릿의 구조에서 참조할 수 있습니다.

   `/conf/<your-site>/settings/wcm/templates/<your-template>/structure/jcr:content`

   예를 들어, 스마트 폰 장치 그룹을 추가하려는 경우:

   `/conf/we-retail/settings/wcm/templates/experience-page/structure/jcr:content`

   ![chlimage_1-159](assets/chlimage_1-159.png)

1. CRXDE Lite을 사용하여 장치 그룹을 다중 값 문자열 속성에 추가하여 사이트에서 사용할 수 있도록 허용합니다 `cq:deviceGroups` 사이트의 구조에서.

   `/content/<your-site>/jcr:content`

   예를 들어 **스마트폰** 장치 그룹:

   `/content/we-retail/jcr:content`

   ![chlimage_1-160](assets/chlimage_1-160.png)

이제 을(를) 사용할 때 [에뮬레이터](/help/sites-authoring/responsive-layout.md#layout-definitions-device-emulation-and-breakpoints) 페이지 편집기 내(예: [레이아웃 수정](/help/sites-authoring/responsive-layout.md)) 구성된 장치 그룹의 장치를 선택하면 페이지가 URL의 일부로 선택기로 렌더링됩니다.

이 예에서 다음을 기반으로 페이지를 편집할 때 **경험 페이지** 템플릿을 선택하고 에뮬레이터에서 iPhone 4를 선택하면 다음과 같이 선택기가 포함된 페이지가 렌더링됩니다. `arctic-surfing-in-lofoten.smart.html` 대신 `arctic-surfing-in-lofoten.html`

이 선택기를 사용하여 페이지를 직접 호출할 수도 있습니다.

![chlimage_1-161](assets/chlimage_1-161.png)
