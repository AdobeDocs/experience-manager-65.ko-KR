---
title: Content Services
description: AEM Mobile Content Services를 사용하여 AEM에서 관리하는 콘텐츠를 요청하는 방법에 대해 알아봅니다.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
exl-id: 955ffb1c-4fa9-43bb-8e5b-2df7f2d17951
solution: Experience Manager
feature: Mobile
role: Developer
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 2%

---

# Content Services{#content-services}

{{ue-over-mobile}}

>[!CAUTION]
>
>콘텐츠 서비스 기능은 미리보기 용도로만 문서화됩니다.
>
>6.3 서비스 팩 1의 릴리스와 함께 변경될 수 있습니다.

AEM Mobile Content Services는 AEM에서 관리하는 콘텐츠를 요청하기 위한 간단한 기능입니다. 이렇게 하면 모든 앱 개발자가 AEM의 JCR(콘텐츠 저장소) 및 Sling(웹 프레임워크)에 대한 깊은 지식이 없이도 콘텐츠를 검색할 수 있는 고성능 방법을 제공합니다. 이를 통해 요청한 애플리케이션을 콘텐츠 저장소에서 분리할 수 있습니다.

Content Services는 개발자가 AEM 관리 콘텐츠의 저장소 구조를 알지 못하고 해당 콘텐츠에 액세스할 수 있도록 하는 몇 가지 새로운 AEM 구문을 제공합니다.

이러한 구성은 AEM 관리 콘텐츠와 콘텐츠를 사용하는 모바일 앱 사이에 추상화 계층을 제공하여 유연성을 유지하고 향후 확장을 활성화하는 데 필요합니다. 이를 통해 AEM Content Services는 기본 애플리케이션의 콘텐츠 요구 사항과 AEM 콘텐츠 저장소 사이에서 추상화 계층으로 작동할 수 있습니다.

Content Services는 컨텐츠를 에셋, 패키지된 HTML(HTML/CSS/JS) 또는 채널 독립적인 컨텐츠로 제공할 수 있습니다.

>[!CAUTION]
>
>**필수 구성 요소:**
>
>Content Services를 시작하기 전에 Content Services 플래그를 활성화해야 합니다. 앱에서 모델을 생성하고 관리하려면 구성 브라우저에서 데이터 모델을 활성화합니다.
>
>자세한 내용은 **[콘텐츠 서비스 관리](/help/mobile/developing-content-services.md)** 및 [구성 브라우저](/help/sites-administering/configurations.md) 설명서를 참조하십시오.

![chlimage_1-143](assets/chlimage_1-143.png)

Content Services 플래그를 설정하고 구성 브라우저에서 데이터 모델을 활성화한 후 아래 리소스를 참조하여 AEM Mobile Content Services를 시작하십시오. 모델 관리, 엔티티 관리, AEM Mobile Content Services의 컨텐츠 전달/렌더링 등 컨텐츠 서비스 개념에 익숙해집니다.

* 저장소의 모델
* 렌더링 및 게재
