---
title: 주요 컨텐츠 기능
seo-title: Featured Content Feature
description: 주요 컨텐츠 기능을 사용하면 로그인한 사이트 방문자가 컨텐츠를 강조 표시할 수 있습니다
seo-description: The Featured Content feature lets signed-in site visitors highlight content
uuid: 7a2ff570-01bb-46fb-8d66-3b47e2efa72e
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: ee39435d-80f5-4758-ae01-1ea0d221b00b
exl-id: 76b76e0e-531b-4f80-be70-68532ef81a7f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '336'
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
* 에 대한 구성 설정 `Featured Content` 구성 요소.

## 페이지에 주요 컨텐츠 추가 {#adding-featured-content-to-a-page}

을(를) 추가하려면 `Featured Content` 구성 요소를 페이지에 작성자 모드에서 사용하려면 구성 요소 브라우저를 사용하여 를 찾습니다

* `Communities / Featured Content`

주요 컨텐츠가 표시될 페이지에 해당 컨텐츠를 드래그합니다.

필요한 정보를 보려면 [커뮤니티 구성 요소 기본 사항](basics.md).

이 [필수 클라이언트 측 라이브러리](essentials-featured.md#essentials-for-client-side) 포함된 경우, 다음과 같이 하십시오 `Featured Content` 구성 요소가 표시됩니다.

![featuredcontent](assets/featuredcontent.png)

## 주요 컨텐츠 구성 {#configuring-featured-content}

배치된 항목을 선택합니다 `Featured Content` 액세스하여 선택할 구성 요소 `Configure` 아이콘 편집 대화 상자를 엽니다.

![configure-new](assets/configure-new.png)

![featuredcontent1](assets/featuredcontent1.png)

### 설정 탭 {#settings-tab}

아래에 **[!UICONTROL 설정]** 탭에서 기능을 확인할 컨텐츠를 식별합니다.

* **[!UICONTROL 표시 이름]**

   주요 컨텐츠 목록의 제목입니다. 예 `Featured Questions` 또는 `Featured Ideas`. 기본값은 입니다. `Featured Content` 비워 두면

* **[!UICONTROL 특별 포함된 컨텐츠의 위치]**

   *(필수)* 기능이 될 수 있는 컨텐츠가 들어 있는 페이지로 이동합니다(해당 페이지의 구성 요소는 주요 컨텐츠 허용으로 구성해야 함). (예: `/content/sites/engage/en/forum`)

* **[!UICONTROL 표시 제한]**

   표시할 주요 컨텐츠의 최대 수입니다. 기본값은 5입니다.

## 사이트 방문자 경험 {#site-visitor-experience}

주요 컨텐츠로 컨텐츠를 플래그를 지정하는 기능에는 중재자 권한이 필요합니다.

중재자가 게시한 컨텐츠를 볼 때, 게시된 컨텐츠에는 새로운 컨텐츠를 포함하는 컨텍스트 내 중재 플래그에 액세스할 수 있습니다 `Feature` 플래그.

![site-visitor-experience](assets/site-visitor-experience.png)

피쳐로 플래그가 지정되면 이동 플래그는 다음과 같이 됩니다. `Unfeature`.

가 포함된 페이지 `Featured Content` 구성 요소, 이제 이 게시물을 포함합니다.

![site-visitor-experience1](assets/site-visitor-experience1.png)

`Read More` 는 실제 게시물에 대한 링크입니다.

## 추가 정보 {#additional-information}

자세한 내용은 [주요 콘텐츠](essentials-featured.md) 개발자를 위한 페이지입니다.

주요 컨텐츠에 대한 플래그 지정에 대해서는 다음을 참조하십시오 [사용자가 생성한 컨텐츠 중재](moderate-ugc.md).
