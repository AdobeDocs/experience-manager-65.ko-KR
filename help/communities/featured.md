---
title: 주요 컨텐츠 기능
seo-title: 주요 컨텐츠 기능
description: 주요 컨텐츠 기능을 사용하면 로그인한 사이트 방문자가 컨텐츠를 강조 표시할 수 있습니다
seo-description: 주요 컨텐츠 기능을 사용하면 로그인한 사이트 방문자가 컨텐츠를 강조 표시할 수 있습니다
uuid: 7a2ff570-01bb-46fb-8d66-3b47e2efa72e
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: ee39435d-80f5-4758-ae01-1ea0d221b00b
exl-id: 76b76e0e-531b-4f80-be70-68532ef81a7f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 5%

---

# 주요 컨텐츠 기능 {#featured-content-feature}

## 소개 {#introduction}

주요 컨텐츠 기능은 게시 환경에서 다음과 같은 컨텐츠를 강조 표시하기 위해 로그인한 사이트 방문자(커뮤니티 구성원)를 위한 영역을 제공합니다.

* [블로그](blog-feature.md)
* [달력](calendar.md)
* [포럼](forum.md)
* [아이디어](ideation-feature.md)
* [QnA](working-with-qna.md)

컨텐츠에 특성으로 플래그가 지정되면 이 구성 요소 내에 나열되며 특정 랜딩 페이지 또는 커뮤니티 구성원의 주의를 쉽게 파악할 수 있는 영역에 배치할 수 있습니다.

구성 요소별로 컨텐츠를 기능은 허용하거나 허용되지 않을 수 있습니다.

설명서의 이 섹션에서는 다음 사항에 대해 설명합니다.

* 커뮤니티 사이트에 주요 컨텐츠 추가
* `Featured Content` 구성 요소에 대한 구성 설정입니다.

## 페이지에 주요 컨텐츠 추가 {#adding-featured-content-to-a-page}

작성자 모드의 페이지에 `Featured Content` 구성 요소를 추가하려면 구성 요소 브라우저를 사용하여 을 찾습니다

* `Communities / Featured Content`

주요 컨텐츠가 표시될 페이지에 해당 컨텐츠를 드래그합니다.

필요한 정보를 보려면 [커뮤니티 구성 요소 기본 사항](basics.md)을 방문하십시오.

필요한 [클라이언트 측 라이브러리](essentials-featured.md#essentials-for-client-side)가 포함된 경우 이 방법으로 `Featured Content` 구성 요소가 표시됩니다.

![featuredcontent](assets/featuredcontent.png)

## 추천 콘텐츠 구성 {#configuring-featured-content}

액세스할 배치된 `Featured Content` 구성 요소를 선택하고 편집 대화 상자를 여는 `Configure` 아이콘을 선택합니다.

![configure-new](assets/configure-new.png)

![featuredcontent1](assets/featuredcontent1.png)

### 설정 탭 {#settings-tab}

**[!UICONTROL 설정]** 탭에서 기능을 수행할 콘텐츠를 식별합니다.

* **[!UICONTROL 표시 이름]**

   주요 컨텐츠 목록의 제목입니다. 예: `Featured Questions` 또는 `Featured Ideas` 기본값은 `Featured Content`입니다(비워 두면).

* **[!UICONTROL 특별 포함된 컨텐츠의 위치]**

   *(필수)* 기능일 수 있는 컨텐츠가 들어 있는 페이지를 찾아봅니다(해당 페이지의 구성 요소를 중요 컨텐츠 허용으로 구성해야 함). 예, `/content/sites/engage/en/forum`.

* **[!UICONTROL 표시 제한]**

   표시할 주요 컨텐츠의 최대 수입니다. 기본값은 5입니다.

## 사이트 방문자 경험 {#site-visitor-experience}

주요 컨텐츠로 컨텐츠를 플래그를 지정하는 기능에는 중재자 권한이 필요합니다.

중재자가 게시한 컨텐츠를 볼 때, 게시된 컨텐츠에는 새 `Feature` 플래그를 포함하는 컨텍스트 내 중재 플래그에 액세스할 수 있습니다.

![site-visitor-experience](assets/site-visitor-experience.png)

피쳐로 플래그가 지정되면 이동 플래그는 `Unfeature`이 됩니다.

`Featured Content` 구성 요소가 포함된 페이지에 이제 이 게시물이 포함됩니다.

![site-visitor-experience1](assets/site-visitor-experience1.png)

`Read More` 는 실제 게시물에 대한 링크입니다.

## 추가 정보 {#additional-information}

개발자를 위한 [주요 콘텐츠](essentials-featured.md) 페이지에서 자세한 정보를 찾을 수 있습니다.

주요 컨텐츠에 대한 플래그 지정에 대해서는 [사용자 생성 컨텐츠 중재](moderate-ugc.md)를 참조하십시오.
