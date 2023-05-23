---
title: 하이브리드 앱이 AEM Mobile에 대해 준비되었습니까?
seo-title: Is your hybrid app ready for AEM Mobile?
description: 이 페이지를 따라 hribrid 앱에 대해 알아보십시오. AEM의 앱은 일반적으로 두 부분으로 나뉩니다. "쉘" 및 "콘텐츠"와 이 페이지에서는 이러한 주제에 대한 자세한 정보를 제공합니다.
seo-description: Follow this page to learn about hrybrid apps. An app in AEM is commonly divided into two parts. The 'shell' and 'content' and this page provides more insight on these topics.
uuid: cbcce3fa-9100-46ea-9f24-931b42666709
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: b7fd7954-f2a5-402d-b259-e18b5a618be9
pagetitle: Is your hybrid app ready for AEM Mobile?
exl-id: 4625890c-2b76-4c78-88e8-23741bc09f5b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 0%

---

# 하이브리드 앱이 AEM Mobile에 대해 준비되었습니까?{#is-your-hybrid-app-ready-for-aem-mobile}

>[!NOTE]
>
>Adobe 단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: React)이 필요한 프로젝트에는 SPA Editor를 사용하는 것이 좋습니다. [자세히 알아보기](/help/sites-developing/spa-overview.md).

하이브리드 PhoneGap 또는 Cordova 앱을 AEM으로 가져왔습니다. 이제 어떻게 하시겠습니까? 작성 가능한 콘텐츠를 앱에 추가할 수 있습니다. 이 작업을 수행하려면 AEM 앱의 구조에 대한 일반적인 이해가 필요합니다. AEM의 앱은 일반적으로 두 부분으로 나뉩니다. 쉘 및 콘텐츠 &#39;셸&#39;은 PhoneGap 구성 파일, 앱 프레임워크 및 탐색 컨트롤과 같은 앱의 정적 부분으로 구성됩니다. 가져온 아카이브의 콘텐츠는 셸의 일부로 저장됩니다. 이 문서의 컨텍스트에서 셸은 앱 개발자가 빌드한 하이브리드 PhoneGap 앱의 모든 비 AEM 작성 콘텐츠입니다.

콘텐츠는 AEM Developer가 작성한 AEM에서 작성된 구성 요소, 템플릿 및 작성된 페이지를 나타냅니다. 콘텐츠는 개발자 콘텐츠 또는 작성된 콘텐츠로 분류됩니다. 구성 요소, 디자인 및 페이지 템플릿은 개발자가 빌드하므로 개발 콘텐츠로 간주됩니다. 작성자-콘텐츠 는 구성 요소 및 템플릿을 사용하여 작성된 페이지입니다. 이러한 작업은 일반적으로 디자이너 또는 마케터가 수행합니다.

작성된 AEM 페이지를 하이브리드 앱에 추가하려면 앱 개발자와 AEM 개발자 간의 조정이 필요합니다. 작성된 콘텐츠를 추가하려는 앱의 모든 위치에서 앱 개발자는 이러한 페이지를 AEM에서 오버레이할 수 있는 구조로 구성해야 합니다. 앱 개발자는 AEM 개발자에게 AEM이 작성한 콘텐츠가 추가될 경로에 대한 경로를 제공한 다음 AEM 개발자가 페이지 콘텐츠를 작성한 후 대체될 하이브리드 앱의 자리 표시자 페이지를 제공할 수 있어야 합니다.

설명을 더 쉽게 따라하기 위해 AEM Marketing Cloud: AEM Mobile 하이브리드 참조 를 사용하여 개념을 설명합니다. 하이브리드 참조 앱은 사이드 메뉴가 있는 워크플로우 페이지로 구성됩니다.

![chlimage_1-76](assets/chlimage_1-76.png)

이 예제에서는 애플리케이션의 시작 페이지를 작성하겠습니다. 소스 살펴보기 [https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/hybrid-app/www/js/app.js#L75](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/hybrid-app/www/js/app.js#L75). 앱 개발자가 시작 페이지를 정의하고 앱에서 렌더링한 페이지에 대한 템플릿을 제공했음을 알 수 있습니다. 여기에서 앱 개발자와 AEM 개발자가 조정해야 합니다. 하이브리드 참조 앱의 시작 페이지 템플릿 경로는 &quot;content/mobileapps/hybrid-reference-app/en/welcome.template.html&quot;로 정의됩니다. AEM 개발자는 동일한 경로를 사용하여 AEM 저장소에서 시작 페이지를 작성하므로 이 경로는 매우 중요합니다.

![chlimage_1-77](assets/chlimage_1-77.png)

Content Sync를 사용하여 콘텐츠를 오버레이하여 새 페이지를 Hybrid 앱에 추가하기 때문에 하이브리드 앱과 AEM에서 작성한 콘텐츠가 동일한 경로를 사용하는 것이 중요합니다. 가져오기 프로세스의 일부로 하이브리드 앱을 AEM으로 가져오면 Content Sync 구성이 설정됩니다.

![chlimage_1-78](assets/chlimage_1-78.png)

앱 대시보드에서 &#39;소스 다운로드&#39;를 수행하면 이러한 ContentSync 스크립트가 실행되어 하이브리드 앱의 아카이브를 어셈블합니다.

![chlimage_1-79](assets/chlimage_1-79.png)

ContentSync는 먼저 하이브리드 앱의 모든 앱 개발 콘텐츠가 저장된 앱의 &#39;쉘&#39;을 가져온 다음 앱의 &#39;콘텐츠&#39;를 가져옵니다. 이제 &#39;shell&#39;에 &#39;content&#39;의 페이지와 경로가 동일한 페이지가 있으면 &#39;shell&#39;의 페이지는 &#39;content&#39;의 페이지로 대체(대체)됩니다. 즉, 하이브리드 참조 앱 샘플의 경우 ContentSync를 실행할 때 AEM에 &quot;content/mobileapps/hybrid-reference-app/en/welcome.template.html&quot;과 동일한 경로를 가진 페이지를 만들면 해당 위치에서 AEM에 있는 모든 항목을 사용하여 하이브리드 참조 앱의 일부인 페이지를 오버레이합니다. 오버레이는 ContentSync에서 처리되므로 앱을 사용하는 사용자의 경우 AEM 작성 콘텐츠가 있는 앱에 대한 업데이트가 원활하게 보이므로 앱을 다시 빌드할 필요가 없습니다. 따라서 앱을 실행할 때 시작 페이지가 다음과 같이 표시됩니다.

![chlimage_1-80](assets/chlimage_1-80.png)
