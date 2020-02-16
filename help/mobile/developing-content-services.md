---
title: 컨텐츠 서비스
seo-title: 컨텐츠 서비스
description: 'null'
seo-description: 'null'
uuid: 7bd09c91-3931-400b-bdfc-b064b9ca9668
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: 6a7e5472-cb57-4c78-b183-7c6dcac11a4e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 컨텐츠 서비스{#content-services}

>[!NOTE]
>
>단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: 응답)이 필요한 프로젝트에 SPA 편집기를 사용하는 것이 좋습니다. [추가 정보](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>콘텐츠 서비스 기능은 미리 보기 용도로만 문서화됩니다.
>
>6.3 GA 서비스 팩 1이 릴리스되면 변경될 수 있습니다.

AEM Mobile Content Services는 AEM 파섹 이렇게 하면 모든 앱 개발자는 AEM의 컨텐츠 저장소(JCR) 및 웹 프레임워크(Sling)에 대한 심층적인 지식이 없어도 컨텐츠를 검색할 수 있는 높은 성능을 경험할 수 있습니다. 컨텐츠 저장소에서 요청 애플리케이션을 분리할 수 있습니다.

컨텐츠 서비스는 개발자가 해당 컨텐츠의 저장소 구조에 대한 지식 없이도 AEM 관리 컨텐츠에 액세스할 수 있도록 해주는 몇 가지 새로운 AEM 구문을 제공합니다.

이러한 구문은 AEM 관리 콘텐츠와 콘텐츠를 사용하는 모바일 앱 간에 추상화 레이어를 제공하여 유연성을 유지하고 향후 확장을 활성화하는 데 필요합니다. 이를 통해 AEM Content Services는 기본 애플리케이션의 컨텐츠 요구 사항과 AEM 컨텐츠 저장소 간의 추상 레이어로 작업할 수 있습니다.

콘텐츠 서비스는 콘텐츠를 자산, 패키징된 HTML(HTML/CSS/JS) 또는 채널 독립적인 컨텐츠로 제공할 수 있습니다.

>[!CAUTION]
>
>**전제 조건:**
>
>콘텐츠 서비스를 시작하기 전에 콘텐츠 서비스 플래그를 활성화해야 합니다. 앱에서 모델을 만들고 관리하려면 구성 브라우저에서 데이터 모델을 활성화해야 합니다.
>
>자세한 **[내용은 콘텐츠 서비스](/help/mobile/developing-content-services.md)**관리를 참조하십시오.

![chlimage_1-143](assets/chlimage_1-143.png)

구성 브라우저에서 콘텐츠 서비스 플래그와 활성화된 데이터 모델을 설정한 후에는 아래 리소스를 참조하여 AEM Mobile Content Services를 시작하고 모델 관리, 개체 관리, AEM Mobile Content Services용 콘텐츠 전달/렌더링 등과 같은 콘텐츠 서비스 개념을 익힐 수 있습니다.

* 저장소의 모델
* 렌더링 및 전달

