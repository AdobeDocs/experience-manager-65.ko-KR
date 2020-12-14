---
title: 초기 설정
seo-title: 초기 설정
description: 커뮤니티 설정
seo-description: 커뮤니티 설정
uuid: c53d280c-c5ae-47cf-8038-f0dea68e15ff
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 0d462ad1-5619-4bb6-9609-bc8987c40a0c
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 2%

---


# 초기 설정 {#initial-setup}

## 작성자 및 게시 인스턴스 시작 {#start-author-and-publish-instances}

개발 및 데모를 위해 작성자 및 게시 인스턴스 하나를 실행해야 합니다.

이렇게 하려면 기본 AEM [시작하기](../../help/sites-deploying/deploy.md#getting-started) 지침을 따르십시오. 그러면 다음이 수행됩니다.

* [localhost:4502의 작성 환경](http://localhost:4502/)
* [localhost:4503에 환경 게시](http://localhost:4503/)

AEM Communities의 경우

* 작성 환경은 다음과 같습니다.

   * 사이트, 템플릿 및 구성 요소 개발
   * 관리 및 구성 작업.

* 게시 환경은 다음과 같습니다.

   * 컨텐츠를 게시하고 중재하는 커뮤니티 경험입니다.
   * 커뮤니티 그룹, 구성원 및 구성원 그룹 만들기

>[!NOTE]
>
>AEM에 익숙하지 않은 경우 [기본 처리](../../help/sites-authoring/basic-handling.md)에 대한 설명서와 [빠른 페이지 작성 안내서](../../help/sites-authoring/qg-page-authoring.md)를 참조하십시오.

## 최신 커뮤니티 릴리스 {#install-latest-communities-release} 설치

이 자습서는 [참여 커뮤니티 사이트](overview.md#engagement-community)를 만들며 AEM Communities 6.2 기능 팩 버전 1.10을 기반으로 합니다.

최신 기능 팩이 설치되었는지 확인하려면 다음을 참조하십시오.

* [최신 릴리스](deploy-communities.md#latest-releases)

[지원 커뮤니티 사이트](overview.md#enablement-community)를 만드는 자습서를 보려면 [AEM Communities for Enablement](getting-started-enablement.md)를 방문하십시오.

## Analytics 구성 {#configure-analytics}

[Adobe Analytics이 커뮤니티 사이트](analytics.md)에 대해 구성되면 커뮤니티 구성원의 경험을 향상시키고 사이트 관리자에게 피드백을 제공하는 커뮤니티 활동에 대한 정보를 사용할 수 있습니다.

Adobe Analytics와의 통합은 선택 사항입니다.

## 알림 이메일 구성 {#configure-email-for-notifications}

기본적으로 `Communities Sites` 콘솔을 사용하여 만든 모든 사이트에 사용할 수 있는 알림 기능은 알림에 대한 이메일 채널을 제공합니다.

사이트에 맞게 이메일을 올바르게 구성하는 데 필요한 것은 다음과 같습니다.

[이메일 ](email.md) 구성을 참조하십시오.

## 터널 서비스 {#enable-the-tunnel-service} 활성화

작성 환경에서 커뮤니티 사이트를 만들 때 터널 서비스를 사용하면 게시 환경에 등록된 신뢰할 수 있는 커뮤니티 구성원에게 역할을 할당할 수 있습니다. 또한 이 터널 서비스를 통해 작성 환경의 [구성원 및 그룹 콘솔](members.md)에서 커뮤니티 구성원에 액세스할 수도 있습니다.

게시 환경에서 만든 구성원 및 구성원 그룹이 작성 환경에서 다시 만들지 *말고*&#x200B;에 대한 규칙입니다. 자세한 내용은 [사용자 및 사용자 그룹 관리](users.md)를 참조하십시오.

**author** 인스턴스에서 터널 서비스를 활성화하는 간단한 지침은 [터널 서비스](deploy-communities.md#tunnel-service-on-author)를 참조하십시오.

## 커뮤니티 관리자 역할 {#community-administrator-role}

커뮤니티 관리자 그룹의 구성원은 커뮤니티 사이트를 만들고 사이트를 관리하며 구성원을 관리하고(커뮤니티 구성원을 금지할 수 있음) 콘텐트를 중재할 수 있습니다.

### 사용자 만들기 {#create-user}

커뮤니티 관리자 역할이 할당된 *author*&#x200B;에 사용자를 만듭니다.

* 작성 인스턴스에서

   * 예: [http://localhost:4502/](http://localhost:4503/)

* 관리자 권한으로 로그인

   * 예: 사용자 이름 &#39;admin&#39; / 암호 &#39;admin&#39;

* 주 콘솔에서 **[!UICONTROL 도구]** > **[!UICONTROL 작업]** > **[!UICONTROL 보안]** > **[!UICONTROL 사용자]**&#x200B;로 이동합니다.
* **편집** 메뉴에서 **[!UICONTROL 사용자 추가]**&#x200B;를 선택합니다.

* `Create New User` 대화 상자에서 다음을 입력합니다.

   * **[!UICONTROL ID]**:시리우스
   * **[!UICONTROL 이메일 주소]**:sirius.nilson@mailinator.com
   * **[!UICONTROL 암호]**:암호
   * **[!UICONTROL 암호 확인(&amp;A);]**:암호
   * **[!UICONTROL 이름]**:시리우스
   * **[!UICONTROL 성]**:Nilson

### 커뮤니티 관리자 그룹 {#assign-sirius-to-community-administrators-group}에 Sirius 할당

아래로 스크롤하여 `Add User to Groups`:

* 검색할 &#39;C&#39;를 입력하십시오.

   * 선택 `Community Administrators`
   * 선택 `Community Enablement Managers`

* **[!UICONTROL 저장]**&#x200B;을 선택합니다.

![사용자 만들기](assets/create-user.png)

## 소셜 로그인 활성화 {#enable-social-login}

Facebook 및 Twitter의 소셜 로그인 데모 버전을 사용하려면 먼저

1. 수정 팩 또는 [최신 기능 팩](deploy-communities.md#latestfeaturepack)(2017년 3월 Facebook API 변경 사항) 설치
1. [게시 환경에서 OAuth ](social-login.md#adobe-granite-oauth-authentication-handler) 공급자를 활성화합니다.

프로덕션 서버의 경우 소셜 로그인을 제공하는 데 필요한 클라우드 서비스를 만들어야 합니다.

[Facebook 및 Twitter와 소셜 로그인](social-login.md)을 참조하십시오.

## 자습서 태그 {#create-tutorial-tags} 만들기

`Tutorial`의 태그 네임스페이스를 사용하여 참여 및 지원 자습서에 사용할 태그를 만듭니다.

[태깅 콘솔](../../help/sites-administering/tags.md#tagging-console)을 사용하여 다음 태그를 만듭니다.

* `Tutorial: Sports / Baseball`
* `Tutorial: Sports / Gymnastics`
* `Tutorial: Sports / Skiing`
* `Tutorial: Arts / Visual`
* `Tutorial: Arts / Auditory`
* `Tutorial: Arts / History`

![tutorial-tags](assets/tutorial-tags.png)

그런 다음 지침에 따라 다음을 수행합니다.

1. [태그 권한을 설정합니다](../../help/sites-administering/tags.md#setting-tag-permissions).
1. [태그를 게시합니다](../../help/sites-administering/tags.md#publishing-tags).

AEM Communities 시작하기 Tutorials에 대해 만든 태그의 샘플 패키지

[파일 가져오기](assets/tutorial_tags-v63.zip)

## UGC 공용 스토어용 MongoDB {#mongodb-for-ugc-common-store}

게시 및/또는 작성 환경에서 모든 UGC를 유연하게 중재할 수 있도록 [MSRP](msrp.md)(MongoDB)을 [공통 스토어](working-with-srp.md)로 설정하는 것이 좋습니다.

자세한 내용은 [How to Setup MongoDB for Demo](demo-mongo.md)을 참조하십시오.

기본적으로 작성자 및 게시 AEM 인스턴스를 설치하면 사용자가 생성한 내용(UGC)이 [JSRP](jsrp.md)을(를) 사용하여 액세스되는 [JCR Tar 저장소](../../help/sites-deploying/platform.md)에 저장됩니다. JSRP는 공용 저장소가 아니므로 UGC는 입력한 인스턴스에서만 표시됩니다. 일반적으로 UGC는 게시 인스턴스에 입력되어 작성 환경에 표시되지 않으므로 게시 인스턴스를 사용해야 하는 모든 중재 작업이 발생합니다.