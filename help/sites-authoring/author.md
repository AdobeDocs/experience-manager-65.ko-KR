---
title: 작성
seo-title: 작성
description: AEM에서 작성의 개념
seo-description: AEM에서 작성의 개념
uuid: eaa5f613-a138-4215-8f84-dfc962fe7fa7
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 81ff6f6f-11b3-4f8e-80e6-b3e104158394
docset: aem65
translation-type: tm+mt
source-git-commit: 44eb94b917fe88b7c90c29ec7da553e15be391db

---


# 작성{#authoring}

## Concept of Authoring (and Publishing) {#concept-of-authoring-and-publishing}

AEM에서는 두 가지 환경을 제공합니다.

* 작성
* 게시

두 환경은 상호 작용하여 컨텐츠를 방문자가 읽을 수 있도록 웹 사이트에서 사용 가능하게 만들어 줍니다.

작성 환경에서는 컨텐츠를 실제로 게시하기 전에 만들고, 업데이트하고 검토하는 메커니즘을 제공합니다.

* 작성자는 컨텐츠를 만들고, 검토합니다. (컨텐츠는 페이지, 자산, 발행물 등의 몇 가지 유형일 수 있습니다.)
* 이 컨텐츠는 어느 시점에서 웹 사이트에 게시됩니다.

![chlimage_1-132](assets/chlimage_1-132.png)

작성 환경에서는 두 가지 UI를 통해 AEM의 기능을 사용할 수 있도록 되어 있습니다. 게시 환경의 경우 사용자가 사용할 수 있도록 만들어진 인터페이스의 전체 모양 및 느낌을 디자인합니다.

>[!NOTE]
>
>AEM 자체는 AEM 설명서를 작성하는 데 사용됩니다.
>
>디스패처와 함께 게시에도 사용됩니다.

### 작성 환경 {#author-environment}

The author works in what is known as the **author environment**. This provides an easy to use interface (graphical user interface (GUI or UI)) for creating the content. It is usually located behind a company&#39;s firewall that provides full protection and requires the author to login, using an account that has been assigned the appropriate access rights.

>[!NOTE]
>
>컨텐츠를 만들거나 편집하거나 게시하려면 계정에 적절한 액세스 권한이 있어야 합니다.

작성자의 인스턴스와 개인의 액세스 권한이 어떻게 구성되었는지에 따라 컨텐츠에서 다음을 비롯한 다양한 작업을 수행할 수 있습니다.

* 페이지에서 새 컨텐츠 생성, 또는 기존 컨텐츠 편집
* 사전 정의된 템플릿을 사용하여 새 컨텐츠 페이지 작성
* 자산 및 컬렉션 생성, 편집 및 관리
* 발행물 작성, 편집 및 관리
* 캠페인 및 관련 리소스 개발
* 커뮤니티 사이트 개발 및 관리
* 컨텐츠 페이지, 자산 등 이동, 복사 또는 삭제
* 페이지, 자산 등 게시(또는 게시 취소)

컨텐츠를 관리하는 데 도움이 되는 관리 작업들도 있습니다.

* 게시 전 검토 진행과 같이 변경 사항의 관리 방식을 제어하는 워크플로우
* 개별 작업을 편성하는 프로젝트

>[!NOTE]
>
>AEM은 작성 환경에서도 [대부분의 작업에 대해 ](/help/sites-administering/home.md)관리됩니다.

#### 게시 환경 {#publish-environment}

When ready, the AEM site&#39;s content is published to the **publish environment**. 이 환경에서는 의도했던 대상이 디자인된 인터페이스의 모양 및 느낌에 따라 웹 사이트의 페이지를 사용할 수 있게 되어 있습니다.

일반적으로 게시 환경은 비무장 지대 안에 있습니다. 다시 말해 여기에서는 인터넷에 연결되지만 내부 네트워크의 보호 기능이 완벽하게 적용되지는 않습니다.

AEM 사이트가 [커뮤니티 사이트](/help/communities/overview.md)이거나 [커뮤니티 구성 요소](/help/communities/author-communities.md)를 포함하면 로그인된 사이트 방문자(구성원)는 커뮤니티 기능과 상호 작용할 수도 있습니다. 예를 들어 포럼에 게시하거나 댓글을 게시하거나 다른 구성원을 팔로우할 수 있습니다. 구성원에게는 새 페이지(커뮤니티 그룹)를 작성하거나, 기사를 블로그에 기록하거나, 다른 구성원의 게시물을 조정하는 등, 일반적으로 작성 환경으로 제한되는 활동을 수행할 수 있는 권한이 부여될 수 있습니다.

>[!NOTE]
>
>안타깝게도 사용된 용어에 겹치는 경우가 있습니다. 다음과 같은 경우입니다.
>
>* **게시/게시 취소**
   >  게시 환경에서 컨텐츠를 공개적으로 사용할 수 있도록(또는 사용할 수 없도록) 하는 작업에 대한 기본 용어입니다.
   >
   >
* **활성화/비활성화**
   >  이러한 용어는 게시/게시 취소와 동의어입니다.
   >
   >
* **복제**
   >  이러한 용어는 한 환경에서 다른 환경으로의 데이터(예: 페이지 컨텐츠, 파일, 코드, 사용자 댓글) 이동을 나타내는 데 사용되는 기술 용어입니다.예를 들어 사용자 댓글을 게시하거나 역복제할 때
>



#### Dispatcher {#dispatcher}

To optimize performance for visitors to your website, the **[dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html)**implements load balancing and caching.
