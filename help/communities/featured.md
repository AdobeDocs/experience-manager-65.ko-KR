---
title: 특별 포함된 컨텐츠 기능
seo-title: Featured Content Feature
description: 주요 콘텐츠 기능을 사용하면 로그인한 사이트 방문자가 콘텐츠를 강조 표시할 수 있습니다
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

# 특별 포함된 컨텐츠 기능 {#featured-content-feature}

## 소개 {#introduction}

주요 콘텐츠 기능은 게시 환경의 로그인한 사이트 방문자(커뮤니티 구성원)가 콘텐츠를 강조 표시할 수 있는 영역을 제공합니다.

* [블로그](blog-feature.md)
* [캘린더](calendar.md)
* [포럼](forum.md)
* [아이디어](ideation-feature.md)
* [QnA](working-with-qna.md)

추천 콘텐츠로 플래그가 지정되면 이 구성 요소 내에 나열됩니다. 특정 랜딩 페이지나 커뮤니티 회원의 관심을 쉽게 끌 수 있는 영역에 배치될 수 있습니다.

구성 요소별로 콘텐츠 기능 활성화가 허용되거나 비활성화될 수 있습니다.

설명서의 이 섹션에서는 다음 사항에 대해 설명합니다.

* 커뮤니티 사이트에 주요 콘텐츠 추가.
* 에 대한 구성 설정 `Featured Content` 구성 요소.

## 페이지에 주요 콘텐츠 추가 {#adding-featured-content-to-a-page}

을(를) 추가하려면 `Featured Content` 구성 요소를 페이지에 추가하려면 작성자 모드에서 구성 요소 브라우저를 사용하여

* `Communities / Featured Content`

을 클릭하고 추천 컨텐츠가 나타나야 하는 페이지에 있는 위치로 드래그합니다.

필요한 정보는 다음을 참조하십시오. [커뮤니티 구성 요소 기본 사항](basics.md).

다음의 경우 [필수 클라이언트측 라이브러리](essentials-featured.md#essentials-for-client-side) 포함됩니다. 이렇게 하면 `Featured Content` 구성 요소가 표시됩니다.

![featuredcontent](assets/featuredcontent.png)

## 주요 콘텐츠 구성 {#configuring-featured-content}

배치된 을(를) 선택합니다 `Featured Content` 에 액세스하고 선택할 구성 요소 `Configure` 편집 대화 상자를 여는 아이콘.

![새로 구성](assets/configure-new.png)

![featuredcontent1](assets/featuredcontent1.png)

### 설정 탭 {#settings-tab}

아래 **[!UICONTROL 설정]** 탭에서 기능을 수행할 콘텐츠를 식별합니다.

* **[!UICONTROL 표시 이름]**

   추천 콘텐츠 목록에 대한 제목입니다. 예 `Featured Questions` 또는 `Featured Ideas`. 기본값은 입니다 `Featured Content` 비워 두면

* **[!UICONTROL 특별 포함된 컨텐츠의 위치]**

   *(필수)* 기능이 될 수 있는 콘텐츠가 포함된 페이지로 이동합니다(해당 페이지의 구성 요소는 주요 콘텐츠를 허용하도록 구성되어야 함). (예: `/content/sites/engage/en/forum`)

* **[!UICONTROL 표시 제한]**

   표시할 최대 추천 콘텐츠 수입니다. 기본값은 5입니다.

## 사이트 방문자 경험 {#site-visitor-experience}

콘텐츠를 추천 콘텐츠로 플래그를 지정하려면 중재자 권한이 필요합니다.

중재자가 게시된 콘텐츠를 볼 때 새로운 콘텐츠가 포함된 컨텍스트 내 중재 플래그에 액세스할 수 있습니다 `Feature` 플래그.

![사이트 방문자 경험](assets/site-visitor-experience.png)

기능으로 플래그가 지정되면 전환 플래그가 다음과 같이 됩니다. `Unfeature`.

다음 항목이 포함된 페이지 `Featured Content` 구성 요소에 이제 이 게시물이 포함됩니다.

![site-visitor-experience1](assets/site-visitor-experience1.png)

`Read More` 는 실제 게시물에 대한 링크입니다.

## 추가 정보 {#additional-information}

자세한 내용은 [특별 포함된 컨텐츠](essentials-featured.md) 개발자용 페이지입니다.

주요 기능으로 콘텐츠에 플래그를 지정하는 방법은 를 참조하십시오. [사용자 생성 컨텐츠 중재](moderate-ugc.md).
