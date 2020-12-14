---
title: 템플릿 및 구성 요소 만들기 및 추가
seo-title: 템플릿 및 구성 요소 만들기 및 추가
description: 앱 템플릿과 구성 요소를 만들고 앱에 추가하는 방법에 대해 알아보려면 이 페이지를 따르십시오. 이 페이지는 샘플 앱 템플릿 및 페이지 템플릿이 포함된 앱으로 Geometrixx Unlimited 앱을 사용합니다.
seo-description: 앱 템플릿과 구성 요소를 만들고 앱에 추가하는 방법에 대해 알아보려면 이 페이지를 따르십시오. 이 페이지는 샘플 앱 템플릿 및 페이지 템플릿이 포함된 앱으로 Geometrixx Unlimited 앱을 사용합니다.
uuid: 3a93017c-8094-413f-a01c-9b72025a2b20
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: ec4ada04-e429-4ad4-a060-2dccac847cf0
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1198'
ht-degree: 0%

---


# 템플릿 및 구성 요소 만들기 및 추가 {#creating-and-adding-templates-and-components}

>[!NOTE]
>
>단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: 응답)이 필요한 프로젝트에는 SPA 편집기를 사용하는 것이 좋습니다. [추가 정보](/help/sites-developing/spa-overview.md).

AEM Mobile On-Demand는 완전히 구성된 앱 템플릿, 아티클 템플릿 및 아티클 구성 요소를 제공합니다.

We.Unlimited App은 구성 가능하고 관리하기 쉬운 AEM Mobile On-Demand 애플리케이션의 셸을 나타내는 샘플 템플릿입니다.

새 앱을 만들 때 이 샘플 템플릿을 선택하면 AEM Mobile 기능이 풍부한 대시보드가 제공됩니다.

![chlimage_1-70](assets/chlimage_1-70.png)

>[!NOTE]
>
>AEM Mobile Apps Control Center에서 응용 프로그램 및 모바일 앱 콘텐츠를 관리하려면 [AEM Mobile Application Dashboard](/help/mobile/mobile-apps-ondemand-application-dashboard.md)를 참조하십시오.

## 앱 템플릿 만들기 {#creating-app-templates}

앱 템플릿은 새 앱을 만드는 데 사용되며, 앱의 기준선 또는 기반을 나타내는 페이지 템플릿 및 구성 요소의 컬렉션 역할을 합니다. 이 템플릿은 해당 방식으로 앱을 안내하는 몇 가지 기본 속성을 스탬프화합니다. 일반적으로 고객은 총 앱이 너무 많지 않습니다.

앱 템플릿을 사용하면 AEM 내에서 새로운 앱을 제작하는 데 사용되는 개발자가 만든 기존 디자인을 손쉽게 활용할 수 있습니다.

다른 앱의 템플릿을 기반으로 새 앱을 제작할 때 앱을 만든 앱의 시작점 담당자가 있는 앱이 표시됩니다.

앱 템플릿을 기반으로 새 앱을 만드는 단계:

1. AEM Mobile 앱 카탈로그로 이동합니다.*&lt;server-url>/aem/apps.html/content/mobileapps*
1. 아래에서 보듯이 **Create** —> **App**&#x200B;을 선택합니다.

이 템플릿을 사용하여 앱을 제작하면 아티클, 배너 및 컬렉션을 앱에 추가할 수 있습니다. 다시 방문하여 아티클, 배너 및 컬렉션을 만들려면 [콘텐츠 관리 작업](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md)을 참조하십시오.

>[!NOTE]
>
>또는 AEM 개발자가 제공하는 샘플 앱 템플릿(예: **We.Unlimited** 앱)을 선택할 수도 있습니다. 앱에 이 샘플 템플릿을 사용하는 경우 일부 샘플 아티클과 컬렉션이 제대로 작동합니다. 샘플 템플릿 및 구성 요소를 사용하거나 기존 템플릿을 사용자 정의하거나 앱에 사용할 새 템플릿을 만들 수 있습니다.

>[!CAUTION]
>
>***redirectTarget*** 속성 설정
>
>앱 템플릿 중 하나를 사용하는 동안 개발자는 애플리케이션의 컨텐츠를 정의합니다. 그러나 개발자는 jcr에서 애플리케이션이 만들어지는 위치와 ***redirectTarget*** 속성 값을 알고 있어야 합니다.
>
>***redirectTarget***&#x200B;은 앱 만들기 작업의 일부로 계산되며 앱 템플릿의 일부로 사용할 수 있는 redirectTarget 속성이 있고 redirectTarget의 값이 상대 값으로 정의된 경우 경로를 확인하려고 시도합니다. 앱 만들기 프로세스에서 앱 템플릿에서 redirectTarget에 대한 상대 값을 찾으면 값이 앱이 만들어진 위치의 해결된 위치에 추가됩니다.
>
>예를 들어 앱 템플릿이 &quot;*landugage-masters/en*&quot;의 값으로 ***redirectTarget***&#x200B;을 정의하고 앱이 &quot;*/content/mobileapps/fooApp*&quot;에서 만들어진 경우 앱이 만들어진 후 redirectTarget에 대한 최종 값은 &quot;&lt;a6/&quot;입니다.>/content/mobileapps/fooApp/language-masters/en *&quot;.*


## 컨텐트 템플릿 만들기 {#creating-content-templates}

각 엔티티 유형에는 2개의 기본 템플릿이 있습니다. 이 4가지 주요 원칙은 다음과 같습니다.

* **기본 템플릿:적용 가능한 기본 속성/구조를 갖는 컨텐츠 제작에** 사용됩니다.
* **가져온 템플릿:해당 기본 속성/구조를 사용하여 AEM Mobile에서 컨텐츠를 가져오는 데** 사용됩니다.

### 아티클 템플릿 {#article-templates}

무제한 아티클은 일반적인 AEM Mobile 온디맨드 아티클 레이아웃을 나타내는 샘플 템플릿입니다.

1. **아티클 관리**&#x200B;에서 **+**&#x200B;을 클릭하여 새 아티클을 만듭니다. **무제한 아티클** 또는 **리치 텍스트 아티클**&#x200B;을 선택할 수 있습니다. 아래 이미지는 이 두 집필 템플릿 중 하나를 선택할 수 있는 옵션을 보여줍니다.

1. **다음**&#x200B;을 클릭하여 아티클 이름/제목, 설명, 작성자, 개요, 부서, 축소판 이미지, 아티클 액세스 등과 같은 아티클 메타 데이터를 정의합니다.
1. 광고 속성을 채우려면 **다음**&#x200B;을 클릭합니다.
1. **다음**&#x200B;을 클릭하여 아티클 이미지 또는 소셜 미디어 이미지를 입력합니다.
1. 이 새 아티클에 대한 컬렉션 링크를 선택하려면 **다음**&#x200B;을 클릭합니다.
1. 소셜 공유에 대한 세부 사항을 입력하려면 **다음**&#x200B;을 클릭합니다.
1. **만들기**&#x200B;를 클릭하여 샘플을 사용하여 아티클을 만드는 프로세스를 완료합니다. **완료** 또는 **아티클 편집**&#x200B;을 클릭하여 이 아티클의 속성을 편집합니다.

![chlimage_1-71](assets/chlimage_1-71.png)

### 아티클 {#adding-components-to-article}에 구성 요소 추가

만든 작성자는 텍스트 및 이미지와 같은 구성 요소를 추가하여 아티클의 컨텐츠를 편집할 수 있습니다. 아티클은 AEM 페이지 템플릿의 확장자입니다.

편집할 아티클을 선택하고 **편집**&#x200B;을 클릭하여 아티클에 구성 요소를 추가합니다.

![chlimage_1-72](assets/chlimage_1-72.png) ![chlimage_1-73](assets/chlimage_1-73.png)

왼쪽 패널에서 &#39;**+**&#39;을 선택하여 아티클에 구성 요소를 추가합니다.

![chlimage_1-74](assets/chlimage_1-74.png)

### 기본 템플릿 만들기 {#creating-out-of-the-box-templates}

즉시 사용 가능한 아티클 템플릿이 없지만 사용자 정의 템플릿이 확장되어야 하는 기본 템플릿이 있습니다. Geometrixx Unlimited 앱의 [아티클 템플릿 샘플](http://localhost:4502/crx/de/index.jsp#/apps/geometrixx-unlimited-app/templates/article)을 참조하십시오.

일반 AEM 템플릿 이외의 주요 속성은 필수 속성이며,

***dps-resourceType=&quot;dps:Article&quot;***

이 속성을 사용하면 AEM 페이지가 AEM Mobile 타깃팅된 아티클 페이지로 인식됩니다.

AEM 템플릿에 따라 템플릿의 ***jcr:content***&#x200B;에 모든 기본 속성 또는 하위 노드를 추가할 수 있습니다.

### 배너 및 컬렉션 템플릿 {#banner-and-collection-templates}

>[!CAUTION]
>
>배너 및 컬렉션에는 콘텐츠가 없으므로 배너 제작에서 사용자 정의 템플릿을 지원하지 않습니다.

## 구성 요소 만들기 및 추가 {#creating-and-adding-components}

구성 요소는 위젯을 사용하고 액세스할 수 있도록 허용하며 이러한 위젯은 컨텐츠를 렌더링하는 데 사용됩니다.

단순 구성 요소는 코드 저장소에 포함되며, 이 구성 요소의 소스는 AEM에서 찾을 수 있습니다. 그런 다음 CRXDE Lite에서 로컬로 열 수도 있습니다.

>[!NOTE]
>
>현재 AEM Mobile에 대해 제공된 특별 구성 요소가 없습니다.


페이지에 구성 요소를 추가할 수 있습니다. 모든 구성 요소는 AEM Mobile 앱에서 사용할 수 있지만 적용될 때 제대로 렌더링되지 않을 수 있습니다.

그러나 AEM에서 렌더링되는 사용자 정의 내보내기 내용 동기화 핸들러가 없으면 사용자 정의 구성 요소를 내보내고 AEM Mobile On-demand Services에 업로드할 수 없습니다.

구성 요소가 이미 AEM 페이지에 포함되어 있고 몇 가지 다른 구성 요소 역시 함께 포함되어 있으면 페이지에 다른 구성 요소를 추가하거나 기존 구성 요소를 편집할 수 있습니다.

**페이지에 다른 구성 요소를 추가하려면:**

1. 해당 페이지를 선택하고 편집기 머리글 오른쪽 상단의 드롭다운을 통해 편집 모드에 있는지 확인합니다
1. 편집기 헤더에서 가장 왼쪽 아이콘을 사용하여 사이드 패널 켜기/끄기
1. **구성 요소** 탭을 선택합니다.
1. 사용 가능한 구성 요소 중 하나를 페이지로 드래그하여 놓습니다.

![chlimage_1-75](assets/chlimage_1-75.png)

**기존 구성 요소를 편집하려면:**

1. 해당 페이지를 선택하고 **편집** 모드에 있는지 확인하고 구성 요소를 선택합니다
1. 구성 요소를 구성하려면 렌치 아이콘을 누릅니다.

>[!NOTE]
>
>AEM에서 구성 요소를 만들고 [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)으로 개발을 사용하여 동일한 구성 요소를 사용자 정의할 수 있습니다. 기존 구성 요소를 요구 사항에 맞게 사용자 지정했으면 위 그림에 표시된 대로 **아티클 관리**&#x200B;의 **편집** 옵션을 사용하여 페이지에 추가할 수 있습니다.

>[!NOTE]
>
>AEM Mobile의 [템플릿 및 구성 요소 개발 모범 사례](/help/mobile/best-practices-aem-mobile.md)를 참조하십시오.

### 다음 단계 {#the-next-steps}

* [컨텐츠 속성을 사용하여 컨텐츠 내보내기](/help/mobile/on-demand-content-properties-exporting.md)
* [컨텐츠 동기화를 통한 모바일](/help/mobile/mobile-ondemand-contentsync.md)