---
title: 하이브리드 앱이 AEM Mobile용으로 준비되었습니까?
seo-title: 하이브리드 앱이 AEM Mobile용으로 준비되었습니까?
description: 최신 앱에 대해 알아보려면 이 페이지를 따르십시오. AEM의 앱은 일반적으로 두 부분으로 나뉘어집니다. 'shell'과 'content' 및 이 페이지는 이러한 항목에 대한 더 많은 통찰력을 제공합니다.
seo-description: 최신 앱에 대해 알아보려면 이 페이지를 따르십시오. AEM의 앱은 일반적으로 두 부분으로 나뉘어집니다. 'shell'과 'content' 및 이 페이지는 이러한 항목에 대한 더 많은 통찰력을 제공합니다.
uuid: cbcce3fa-9100-46ea-9f24-931b42666709
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: b7fd7954-f2a5-402d-b259-e18b5a618be9
pagetitle: Is your hybrid app ready for AEM Mobile?
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '780'
ht-degree: 0%

---


# 하이브리드 앱이 AEM Mobile용으로 준비되었습니까?{#is-your-hybrid-app-ready-for-aem-mobile}

>[!NOTE]
>
>단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: 응답)이 필요한 프로젝트에는 SPA 편집기를 사용하는 것이 좋습니다. [추가 정보](/help/sites-developing/spa-overview.md).

이제 Hybrid PhoneGap 또는 Cordova 앱을 AEM으로 가져오셨다면 어떻게 하시겠습니까? 앱에 작성 가능한 콘텐츠를 추가할 수 있습니다. 이 작업을 수행하려면 AEM 앱의 구조를 이해해야 합니다. AEM의 앱은 일반적으로 두 부분으로 나뉘어집니다. &#39;shell&#39;과 &#39;content&#39;입니다. &#39;shell&#39;은 앱의 정적 부분으로 구성됩니다.PhoneGap 구성 파일, 앱 프레임워크 및 내비게이션 컨트롤과 같은 작업을 할 수 있습니다. 가져온 아카이브의 내용은 셸의 일부로 저장됩니다. 이 문서의 컨텍스트에서 셸은 앱 개발자가 빌드한 하이브리드 PhoneGap 앱의 AEM이 아닌 모든 컨텐츠 작성입니다.

컨텐츠는 AEM Developer가 작성한 AEM에서 만든 구성 요소, 템플릿 및 제작된 페이지를 나타냅니다. 컨텐츠는 개발자 컨텐츠 또는 제작된 컨텐트로 분류됩니다. 구성 요소, 디자인 및 페이지 템플릿은 개발자가 빌드하므로 개발 콘텐츠로 간주됩니다. 작성자 컨텐츠는 구성 요소 및 템플릿을 사용하여 작성된 페이지입니다. 이러한 작업은 일반적으로 디자이너나 마케터가 수행합니다.

제작된 AEM 페이지를 하이브리드 앱에 추가하려면 앱 개발자와 AEM 개발자 간의 조정이 필요합니다. 제작된 콘텐츠를 추가하려는 앱의 모든 위치에서 앱 개발자는 AEM에서 오버레이할 수 있는 구조로 이러한 페이지를 구성해야 합니다. 앱 개발자는 AEM에서 제작한 컨텐츠를 추가할 경로를 AEM 개발자에게 제공한 다음 AEM 개발자가 페이지 컨텐츠를 제작한 후 대체할 하이브리드 앱에 자리 표시자 페이지를 제공할 수 있어야 합니다.

설명을 더 쉽게 따르기 위해 AEM Marketing Cloud을 사용할 것입니다.AEM Mobile 하이브리드 참조를 참조하십시오. 하이브리드 참조 앱은 사이드 메뉴가 있는 웹 페이지로 구성됩니다.

![chlimage_1-76](assets/chlimage_1-76.png)

이 예에서는 애플리케이션의 시작 페이지를 작성하려고 합니다. 소스 [https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/hybrid-app/www/js/app.js#L75](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/hybrid-app/www/js/app.js#L75)을(를) 봅니다. 앱 개발자가 시작 페이지를 정의하고 앱에서 렌더링하는 페이지에 대한 템플릿을 제공했음을 확인할 수 있습니다. 여기에서 앱 개발자와 AEM 개발자가 협력해야 합니다. 하이브리드 참조 앱에서 시작 페이지 템플릿의 경로는 &quot;content/mobileapps/hybrid-reference-app/en/welcome.template.html&quot;로 정의됩니다. AEM 개발자가 동일한 경로를 사용하여 AEM 저장소에서 시작 페이지를 작성하므로 이 경로는 매우 중요합니다.

![chlimage_1-77](assets/chlimage_1-77.png)

하이브리드 앱과 AEM 제작 컨텐츠의 경우 콘텐츠 동기화를 사용하여 콘텐츠를 오버레이하여 하이브리드 앱에 새 페이지를 추가할 수 있으므로 동일한 경로를 사용해야 합니다. 가져오기 프로세스의 일부로 하이브리드 앱을 AEM으로 가져올 때 콘텐츠 동기화 구성이 설정됩니다.

![chlimage_1-78](assets/chlimage_1-78.png)

앱 대시보드에서 &#39;소스 다운로드&#39;할 때 ContentSync 스크립트는 하이브리드 앱의 아카이브를 조합하기 위해 실행됩니다.

![chlimage_1-79](assets/chlimage_1-79.png)

ContentSync는 먼저 앱의 &#39;shell&#39;을 가져옵니다. 이 앱은 하이브리드 앱의 모든 개발 콘텐츠를 저장한 다음 앱의 &#39;content&#39;를 가져옵니다. 이제 &#39;content&#39;의 경로와 동일한 경로를 갖는 &#39;shell&#39;의 페이지가 있는 경우 &#39;shell&#39; 아래의 페이지가 &#39;content&#39; 아래의 페이지로 (교체)됩니다. 즉, ContentSync를 실행할 때 &quot;content/mobileapps/hybrid-reference-app/en/welcome.template.html&quot;과 같은 경로를 가진 AEM에서 페이지를 만드는 경우 하이브리드 참조 앱 샘플에서 AEM에 있는 모든 것을 사용하여 하이브리드 참조 앱의 일부인 페이지를 오버레이합니다. 오버레이는 ContentSync에서 처리되므로 앱을 사용하는 사용자의 경우 AEM 제작 콘텐츠가 포함된 앱 업데이트가 매끄럽게 표시되므로 앱을 다시 빌드할 필요가 없습니다. 따라서 앱을 실행하면 시작 페이지가 다음과 같이 표시됩니다.

![chlimage_1-80](assets/chlimage_1-80.png)
