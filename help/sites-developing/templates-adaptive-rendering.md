---
title: 적응형 템플릿 렌더링
seo-title: 적응형 템플릿 렌더링
description: 'null'
seo-description: 'null'
uuid: 97226ae1-e42a-40ae-a5e0-886cd77559d8
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: f5cb0e98-0d6e-4f14-9b94-df1a9d8cbe5b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 3%

---


# 적응형 템플릿 렌더링{#adaptive-template-rendering}

적응형 템플릿 렌더링에서는 변형된 페이지를 관리하는 방법을 제공합니다. 모바일 장치에 대한 다양한 HTML 출력(예: 기능폰과 스마트폰)을 전달하는 데 본래 유용하며, 이 기능은 다른 마크업 또는 HTML 출력이 필요한 다양한 장치에 경험을 전달해야 하는 경우에 유용합니다.

## 개요 {#overview}

템플릿은 일반적으로 응답형 격자를 기반으로 구축되며, 이러한 템플릿을 기반으로 만든 페이지는 응답 속도가 빠른 것으로 클라이언트 장치의 뷰포트에 자동으로 조정됩니다. 작성자는 페이지 편집기의 에뮬레이터 도구 모음을 사용하여 특정 장치에 레이아웃을 타깃팅할 수 있습니다.

적응형 렌더링을 지원하도록 템플릿을 설정할 수도 있습니다. 장치 그룹이 올바르게 구성되면 에뮬레이터 모드에서 장치를 선택할 때 페이지가 URL의 다른 선택기로 렌더링됩니다. 선택기를 사용하면 URL을 통해 특정 페이지 렌더링을 직접 호출할 수 있습니다.

장치 그룹을 설정할 때 다음 사항을 기억하십시오.

* 모든 장치는 하나 이상의 장치 그룹에 있어야 합니다.
* 장치는 여러 장치 그룹에 있을 수 있습니다.
* 장치가 여러 장치 그룹에 있을 수 있으므로 선택기를 결합할 수 있습니다.
* 선택기의 조합은 저장소에서 유지될 때 위에서 아래로 평가됩니다.

>[!NOTE]
>
>응답형 디자인을 지원하는 것으로 인식되는 장치는 적응형 레이아웃이 필요하지 않다고 간주되므로 장치 그룹 **응답형 장치**&#x200B;에는 선택기가 없습니다

## 구성 {#configuration}

응용 렌더링 선택기는 기존 장치 그룹 또는 사용자가 직접 만든 [그룹에 대해 구성할 수 있습니다.](/help/sites-developing/mobile.md#device-groups)

이 예에서는 We.Retail 내에 있는 **경험 페이지** 템플릿의 일부로 기존 장치 그룹 **스마트 폰**&#x200B;에 적응형 렌더링 선택기가 있도록 구성합니다.

1. `http://localhost:4502/miscadmin#/etc/mobile/groups`에서 응용 선택기가 필요한 장치 그룹을 편집합니다.

   **에뮬레이터 비활성화** 옵션을 설정하고 저장합니다.

   ![chlimage_1-157](assets/chlimage_1-157.png)

1. 다음 단계에서 장치 그룹 **스마트 폰**&#x200B;이 템플릿 및 페이지 구조에 추가된 경우 **Blackberry** 및 **iPhone 4**&#x200B;에 대해 선택기를 사용할 수 있습니다.

   ![chlimage_1-158](assets/chlimage_1-158.png)

1. CRX DE Lite를 사용하면 템플릿 구조의 다중 값 문자열 속성 `cq:deviceGroups`에 장치 그룹을 추가하여 템플릿에 사용할 수 있습니다.

   `/conf/<your-site>/settings/wcm/templates/<your-template>/structure/jcr:content`

   예를 들어 스마트폰 장치 그룹을 추가하려면:

   `/conf/we-retail/settings/wcm/templates/experience-page/structure/jcr:content`

   ![chlimage_1-159](assets/chlimage_1-159.png)

1. CRX DE Lite를 사용하면 사이트 구조의 다중 값 문자열 속성 `cq:deviceGroups`에 장치 그룹을 추가하여 사이트에서 장치 그룹을 사용할 수 있습니다.

   `/content/<your-site>/jcr:content`

   예를 들어 **스마트 폰** 장치 그룹을 허용하려는 경우:

   `/content/we-retail/jcr:content`

   ![chlimage_1-160](assets/chlimage_1-160.png)

이제 페이지 편집기에서 [에뮬레이터](/help/sites-authoring/responsive-layout.md#layout-definitions-device-emulation-and-breakpoints)를 사용하고 구성된 장치 그룹의 장치를 선택하는 경우 페이지가 URL의 일부로 선택기로 렌더링됩니다.[](/help/sites-authoring/responsive-layout.md)

이 예제에서는 **경험 페이지** 템플릿을 기반으로 페이지를 편집하고 에뮬레이터에서 iPhone 4를 선택하면 선택기를 포함하는 페이지가 `arctic-surfing-in-lofoten.html` 대신 `arctic-surfing-in-lofoten.smart.html`로 렌더링됩니다

이 선택기를 사용하여 페이지를 직접 호출할 수도 있습니다.

![chlimage_1-161](assets/chlimage_1-161.png)

