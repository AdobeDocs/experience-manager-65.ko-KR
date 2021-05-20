---
title: 템플릿 및 구성 요소 만들기 및 추가
seo-title: 템플릿 및 구성 요소 만들기 및 추가
description: 앱에 템플릿 및 구성 요소를 만들고 추가하는 방법에 대해 알려면 이 페이지를 따르십시오. 이 페이지에서는 샘플 앱 템플릿 및 페이지 템플릿을 포함하는 앱으로 Geometrixx Unlimited 앱을 사용합니다.
seo-description: 앱에 템플릿 및 구성 요소를 만들고 추가하는 방법에 대해 알려면 이 페이지를 따르십시오. 이 페이지에서는 샘플 앱 템플릿 및 페이지 템플릿을 포함하는 앱으로 Geometrixx Unlimited 앱을 사용합니다.
uuid: 3a93017c-8094-413f-a01c-9b72025a2b20
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: ec4ada04-e429-4ad4-a060-2dccac847cf0
exl-id: 5f050baa-fe10-4acc-ad32-de20793edc13
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1198'
ht-degree: 0%

---

# 템플릿 및 구성 요소 만들기 및 추가 {#creating-and-adding-templates-and-components}

>[!NOTE]
>
>단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: React)이 필요한 프로젝트에 SPA 편집기를 사용하는 것이 좋습니다. [추가 정보](/help/sites-developing/spa-overview.md).

AEM Mobile 온디맨드는 완전히 구성된 앱 템플릿, 문서 템플릿 및 문서 구성 요소를 제공합니다.

We.Unlimited App은 구성 가능하고 관리하기 쉬운 AEM Mobile On-Demand 애플리케이션의 셸을 나타내는 샘플 템플릿입니다.

새 앱을 만들 때 이 샘플 템플릿을 선택하면 AEM Mobile 기능이 풍부한 대시보드가 제공됩니다.

![chlimage_1-70](assets/chlimage_1-70.png)

>[!NOTE]
>
>AEM Mobile Apps Control Center에서 애플리케이션 및 모바일 앱 콘텐츠를 관리하려면 [AEM Mobile Application Dashboard](/help/mobile/mobile-apps-ondemand-application-dashboard.md)를 참조하십시오.

## 앱 템플릿 만들기 {#creating-app-templates}

앱 템플릿은 새 앱을 만드는 데 사용되며 앱의 기준선 또는 기반을 나타내는 페이지 템플릿 및 구성 요소의 컬렉션 역할을 합니다. 템플릿은 적절한 방식으로 앱을 안내하는 몇 가지 기본 속성을 스탬프합니다. 일반적으로 고객은 통틀어 너무 많은 앱을 만들지 않습니다.

앱 템플릿을 사용하면 AEM 내에서 새로운 앱을 만드는 데 사용되는 개발자가 만든 기존 디자인을 쉽게 활용할 수 있습니다.

다른 앱의 템플릿을 기반으로 새 앱을 만들 때 앱이 만들어진 시작점을 나타내는 앱이 표시됩니다.

앱 템플릿을 기반으로 새 앱을 만드는 단계:

1. AEM Mobile 앱 카탈로그로 이동합니다.*&lt;server-url>/aem/apps.html/content/mobileapps*
1. **만들기** —> **앱**&#x200B;을 아래와 같이 선택합니다

이 템플릿을 사용하여 앱을 만들면 문서, 배너 및 컬렉션을 앱에 추가할 수 있습니다. 다시 방문하여 문서, 배너 및 컬렉션을 만들려면 [컨텐츠 관리 작업](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md)을 참조하십시오.

>[!NOTE]
>
>또는 AEM 개발자가 제공하는 샘플 앱 템플릿(예: **We.Unlimited** 앱)을 선택할 수도 있습니다. 앱에 대해 이 샘플 템플릿을 사용하는 경우 작업할 일부 샘플 문서와 컬렉션이 제공됩니다. 샘플 템플릿 및 구성 요소를 사용하거나, 기존 템플릿 및 구성 요소를 사용자 지정하거나, 앱에 대해 새 템플릿을 만드는 선택 사항이 제공됩니다.

>[!CAUTION]
>
>***redirectTarget*** 속성 설정
>
>앱 템플릿 중 하나를 사용하는 동안 개발자는 애플리케이션의 콘텐츠를 정의합니다. 그러나 개발자는 jcr에서 애플리케이션이 만들어지는 위치와 ***redirectTarget*** 속성 값을 알고 있어야 합니다.
>
>***redirectTarget***&#x200B;은 앱 만들기 작업의 일부로 계산되며, 앱 템플릿의 일부로 사용할 수 있는 redirectTarget 속성이 있고, redirectTarget의 값이 상대적인 것으로 정의된 경우 경로 확인을 시도합니다. 앱 만들기 프로세스에서 앱 템플릿에서 redirectTarget에 대한 상대 값을 찾으면 값이 앱이 만들어진 확인된 위치에 추가됩니다.
>
>예를 들어 앱 템플릿이 &quot;*lanuguage-masters/en*&quot;의 값으로 ***redirectTarget***&#x200B;을 정의하고, 앱이 &quot;*/content/mobileapps/fooApp*&quot;에서 만들어진 경우, 앱을 만든 후 redirectTarget에 대한 최종 값은 &quot;*/content/mobileapps/fooApp/language-masters/en*&quot;이 됩니다.


## 컨텐츠 템플릿 만들기 {#creating-content-templates}

각 엔티티 유형에는 두 개의 기본 템플릿이 있습니다. 이 4가지 주요 원칙은 다음과 같습니다.

* **기본 템플릿:** 적용 가능한 기본 속성/구조가 있는 컨텐츠 작성에 사용됩니다
* **가져온 템플릿:** 적용 가능한 기본 속성/구조를 사용하여 AEM Mobile에서 콘텐츠를 가져오는 데 사용됩니다

### 문서 템플릿 {#article-templates}

무제한 문서는 일반적인 AEM Mobile 온디맨드 문서 레이아웃을 나타내는 샘플 템플릿입니다.

1. **문서 관리**&#x200B;에서 **+**&#x200B;을 클릭하여 새 문서를 만듭니다. **무제한 문서** 또는 **리치 텍스트 문서**&#x200B;를 선택할 수 있습니다. 아래 이미지는 이러한 두 문서 템플릿 중에서 선택할 수 있는 옵션을 보여줍니다.

1. **다음**&#x200B;을 클릭하여 문서 이름/제목, 설명, 작성자, 요약, 부서, 축소판 이미지, 문서 액세스 등과 같은 문서 메타 데이터를 정의합니다.
1. 광고 속성을 채우려면 **다음**&#x200B;을 클릭하십시오.
1. **다음** 을 클릭하여 문서 이미지 또는 소셜 미디어 이미지를 입력합니다
1. **다음**&#x200B;을 클릭하여 이 새 문서가 작성될 컬렉션 링크를 선택합니다.
1. **다음**&#x200B;을 클릭하여 소셜 공유에 대한 세부 정보를 입력합니다.
1. **만들기**&#x200B;를 클릭하여 샘플을 사용하여 문서를 만드는 프로세스를 완료합니다. **완료** 또는 **문서 편집**&#x200B;을 클릭하여 이 문서의 속성을 편집합니다.

![chlimage_1-71](assets/chlimage_1-71.png)

### 문서 {#adding-components-to-article}에 구성 요소 추가

만들어진 작성자는 텍스트 및 이미지와 같은 구성 요소를 추가하여 문서의 컨텐츠를 편집할 수 있습니다. 문서는 AEM 페이지 템플릿의 확장입니다.

편집할 문서를 선택하고 **편집**&#x200B;을 클릭하여 문서에 구성 요소를 추가합니다.

![chlimage_1-72](assets/chlimage_1-72.png) ![chlimage_1-73](assets/chlimage_1-73.png)

왼쪽 패널에서 &#39;**+**&#39;를 선택하여 문서에 구성 요소를 추가합니다.

![chlimage_1-74](assets/chlimage_1-74.png)

### 기본 템플릿 만들기 {#creating-out-of-the-box-templates}

기본 제공 문서 템플릿은 없지만 사용자 지정 템플릿을 확장해야 하는 기본 템플릿이 있습니다. Geometrixx Unlimited 앱의 [문서 템플릿 샘플](http://localhost:4502/crx/de/index.jsp#/apps/geometrixx-unlimited-app/templates/article)을 참조하십시오.

일반 AEM 템플릿 이상의 주요 속성은 다음과 같습니다.

***dps-resourceType=&quot;dps:Article&quot;***

이 속성을 사용하면 AEM 페이지가 AEM Mobile 타깃팅된 문서 페이지로 인식됩니다.

AEM 템플릿에 따라 기본 속성 또는 하위 노드를 템플릿의 ***jcr:content***&#x200B;에 추가할 수 있습니다.

### 배너 및 컬렉션 템플릿 {#banner-and-collection-templates}

>[!CAUTION]
>
>배너 및 컬렉션에는 콘텐츠가 없으므로 만든 콘텐츠가 사용자 지정 템플릿을 지원하지 않습니다.

## 구성 요소 만들기 및 추가 {#creating-and-adding-components}

구성 요소는 위젯을 사용하고 액세스할 수 있도록 하며, 이 구성 요소는 컨텐츠를 렌더링하는 데 사용됩니다.

단순 구성 요소는 코드 저장소에 포함되며 이 구성 요소의 소스가 AEM에서 찾을 수 있습니다. 그런 다음 CRXDE Lite에서 로컬로 열 수도 있습니다.

>[!NOTE]
>
>현재 AEM Mobile에 대해 기본적으로 제공되는 구성 요소가 없습니다.


페이지에 구성 요소를 추가할 수 있습니다. 모든 구성 요소는 AEM Mobile 앱에서 사용할 수 있지만 적용할 때 올바르게 렌더링되지 않을 수 있습니다.

그러나 AEM에서 렌더링되는 사용자 지정 내보내기 컨텐츠 동기화 핸들러가 없으면 사용자 지정 구성 요소를 AEM Mobile On-demand Services으로 올바로 내보내고 업로드할 수 없습니다.

구성 요소가 이미 AEM 페이지에 일부 다른 빌딩 블록 구성 요소와 함께 포함되면, 페이지에 다른 구성 요소를 추가하거나 기존 구성 요소를 편집할 수 있습니다.

**페이지에 다른 구성 요소를 추가하려면:**

1. 해당 페이지를 선택하고 편집기 헤더의 오른쪽 상단에 있는 드롭다운을 통해 편집 모드에 있는지 확인합니다
1. 편집기 헤더에서 맨 왼쪽 아이콘을 사용하여 사이드 패널을 전환합니다.
1. **구성 요소** 탭을 선택합니다
1. 사용 가능한 구성 요소 중 하나를 페이지로 끌어다 놓습니다

![chlimage_1-75](assets/chlimage_1-75.png)

**기존 구성 요소를 편집하려면**

1. 해당 페이지를 선택하고 **편집** 모드에 있는지 확인하고 구성 요소를 선택합니다
1. 공구모양 아이콘을 눌러 구성 요소를 구성합니다

>[!NOTE]
>
>AEM에서 구성 요소를 만들고 [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)로 개발을 사용하여 구성 요소를 사용자 지정할 수 있습니다. 기존 구성 요소를 요구 사항으로 사용자 지정하고 나면 위의 그림과 같이 **문서 관리**&#x200B;에서 **편집** 옵션을 사용하여 페이지에 추가할 수 있습니다.

>[!NOTE]
>
>AEM Mobile의 [템플릿 및 구성 요소 개발에 대한 우수 사례](/help/mobile/best-practices-aem-mobile.md)를 참조하십시오.

### 다음 단계 {#the-next-steps}

* [컨텐츠 속성을 사용하여 컨텐츠 내보내기](/help/mobile/on-demand-content-properties-exporting.md)
* [콘텐츠 동기화가 있는 모바일](/help/mobile/mobile-ondemand-contentsync.md)
