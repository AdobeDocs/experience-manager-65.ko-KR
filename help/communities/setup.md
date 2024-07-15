---
title: 초기 설정
description: Adobe Experience Manager 커뮤니티를 처음 설정하는 방법을 알아봅니다.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
exl-id: 6bda0f09-7ae5-4540-b035-9dd249ac3186
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 1%

---

# 초기 설정 {#initial-setup}

## 작성자 및 Publish 인스턴스 시작 {#start-author-and-publish-instances}

개발 및 데모를 위해 작성자 하나와 게시 인스턴스 하나를 실행해야 합니다.

이렇게 하려면 기본 Adobe Experience Manager(AEM) [시작하기](../../help/sites-deploying/deploy.md#getting-started) 지침을 따르십시오. 그러면 다음과 같은 결과가 나타납니다.

* [localhost:4502](http://localhost:4502/)의 작성자 환경
* [localhost:4503](http://localhost:4503/)의 Publish 환경

AEM Communities의 경우

* 작성 환경은 다음과 같습니다.

   * 사이트, 템플릿 및 구성 요소 개발
   * 관리 및 구성 작업.

* Publish 환경은 다음과 같습니다.

   * 콘텐츠 게시 및 중재에 대한 커뮤니티 경험.
   * 커뮤니티 그룹, 구성원 및 구성원 그룹 만들기

>[!NOTE]
>
>AEM에 익숙하지 않은 경우 [기본 처리](../../help/sites-authoring/basic-handling.md)에 대한 설명서와 [페이지 작성에 대한 빠른 안내서](../../help/sites-authoring/qg-page-authoring.md)를 참조하세요.

## 최신 Communities 릴리스 설치 {#install-latest-communities-release}

이 자습서에서는 [참여 커뮤니티 사이트](overview.md#engagement-community)를 만들고 AEM Communities 6.2 기능 팩 버전 1.10을 기반으로 합니다.

최신 기능 팩이 설치되었는지 확인하려면 다음을 방문하십시오.

* [최신 릴리스](deploy-communities.md#latest-releases)

## Analytics 구성 {#configure-analytics}

커뮤니티 사이트에 대해 [Adobe Analytics이 구성되면](analytics.md) 커뮤니티 활동에 대한 정보를 사용할 수 있습니다. 이 정보는 커뮤니티 구성원의 경험을 개선하고 사이트 관리자에게 피드백을 제공합니다.

Adobe Analytics과의 통합은 선택 사항입니다.

## 알림용 이메일 구성 {#configure-email-for-notifications}

`Communities Sites` 콘솔을 사용하여 만든 모든 사이트에서 기본적으로 사용할 수 있는 알림 기능은 알림을 위한 전자 메일 채널을 제공합니다.

필요한 사항은 사이트에 대해 이메일을 올바르게 구성하는 것입니다.

[전자 메일 구성](email.md)을 참조하세요.

## 터널 서비스 활성화 {#enable-the-tunnel-service}

작성 환경에서 커뮤니티 사이트를 만들 때 터널 서비스를 사용하면 Publish 환경에 등록된 신뢰할 수 있는 커뮤니티 구성원에게 역할을 할당할 수 있습니다. 또한 터널 서비스를 통해 작성자 환경의 [구성원 및 그룹 콘솔](members.md)에서 커뮤니티 구성원에 액세스할 수 있습니다.

이 규칙은 작성자 환경에서 *다시 만들 수 없음*&#x200B;을 위해 Publish 환경에서 만든 구성원 및 구성원 그룹을 위한 것입니다. 자세한 내용은 [사용자 및 사용자 그룹 관리](users.md)를 참조하십시오.

**작성자** 인스턴스에서 터널 서비스를 사용하도록 설정하는 간단한 지침은 [터널 서비스](deploy-communities.md#tunnel-service-on-author)를 참조하십시오.

## 커뮤니티 관리자 역할 {#community-administrator-role}

커뮤니티 관리자 그룹의 구성원은 커뮤니티 사이트를 만들고, 사이트를 관리하고, 구성원을 관리하고(커뮤니티에서 구성원을 금지할 수 있음), 콘텐츠를 중재할 수 있습니다.

### 사용자 만들기 {#create-user}

커뮤니티 관리자 역할이 할당된 *작성자*&#x200B;의 사용자 만들기:

* 작성자 인스턴스에서

   * 예: [http://localhost:4502/](http://localhost:4503/)

* 관리자 권한으로 로그인

   * 예를 들어 사용자 이름 &#39;admin&#39; / 암호 &#39;admin&#39;입니다.

* 기본 콘솔에서 **[!UICONTROL 도구]** > **[!UICONTROL 작업]** > **[!UICONTROL 보안]** > **[!UICONTROL 사용자]**&#x200B;로 이동합니다.
* **편집** 메뉴에서 **[!UICONTROL 사용자 추가]**&#x200B;를 선택합니다.

* `Create New User` 대화 상자에서 다음을 입력합니다.

   * **[!UICONTROL ID]**: sirius
   * **[!UICONTROL 전자 메일 주소]**: sirius.nilson@mailinator.com
   * **[!UICONTROL 암호]**: 암호
   * **[!UICONTROL 암호 확인&amp;ast;]**: 암호
   * **[!UICONTROL 이름]**: Sirius
   * **[!UICONTROL 성]**: 닐슨

### 커뮤니티 관리자 그룹에 Sirius 할당 {#assign-sirius-to-community-administrators-group}

`Add User to Groups`(으)로 아래로 스크롤:

* 검색하려면 &#39;C&#39;를 입력하십시오.

   * `Community Administrators` 선택
   * `Community Enablement Managers` 선택

* **[!UICONTROL 저장]**&#x200B;을 선택합니다.

![사용자 만들기](assets/create-user.png)

## 소셜 로그인 활성화 {#enable-social-login}

facebook 및 Twitter을 사용하는 소셜 로그인의 데모 버전을 사용하려면 먼저 다음을 수행해야 합니다.

1. 수정 팩 또는 [최신 기능 팩](deploy-communities.md#latestfeaturepack)을 설치하십시오(2017년 3월 Facebook API 변경용).
1. 게시 환경에서 [OAuth 공급자를 사용](social-login.md#adobe-granite-oauth-authentication-handler)합니다.

프로덕션 서버의 경우 소셜 로그인을 제공하는 데 필요한 클라우드 서비스를 만들어야 합니다.

[Facebook 및 Twitter을 사용한 소셜 로그인](social-login.md)을 참조하세요.

## 튜토리얼 태그 만들기 {#create-tutorial-tags}

`Tutorial`의 태그 네임스페이스를 사용하여 참여 튜토리얼에 사용할 수 있도록 태그를 만드십시오.

[태그 지정 콘솔](../../help/sites-administering/tags.md#tagging-console)을 사용하여 다음 태그를 만드십시오.

* `Tutorial: Sports / Baseball`
* `Tutorial: Sports / Gymnastics`
* `Tutorial: Sports / Skiing`
* `Tutorial: Arts / Visual`
* `Tutorial: Arts / Auditory`
* `Tutorial: Arts / History`

![자습서 태그](assets/tutorial-tags.png)

그런 다음 지침에 따라 다음을 수행합니다.

1. [태그 권한을 설정합니다](../../help/sites-administering/tags.md#setting-tag-permissions).
1. [태그를 Publish](../../help/sites-administering/tags.md#publishing-tags)합니다.

AEM Communities 시작 Tutorials을 위해 만들어진 태그의 샘플 패키지

[파일 가져오기](assets/tutorial_tags-v63.zip)

## MongoDB for UGC Common Store {#mongodb-for-ugc-common-store}

게시 및/또는 작성자 환경에서 모든 UGC를 유연하게 중재하도록 [MSRP](msrp.md)(MongoDB)를 [일반 저장소](working-with-srp.md)(으)로 설정하는 것이 좋지만 선택 사항입니다.

자세한 지침은 [데모용 MongoDB를 설정하는 방법](demo-mongo.md)을 참조하세요.

기본적으로 작성자 및 게시 AEM 인스턴스를 설치하면 UGC(사용자 생성 컨텐츠)가 [JSRP](jsrp.md)를 사용하여 액세스하는 [JCR Tar 저장소](../../help/sites-deploying/platform.md)에 저장됩니다. JSRP는 일반 저장소가 아닙니다. 즉, UGC가 입력된 인스턴스에서만 볼 수 있습니다. 일반적으로 UGC는 게시 인스턴스에 입력되며 작성 환경에 표시되지 않으므로 게시 인스턴스를 사용해야 하는 모든 중재 작업이 발생합니다.
