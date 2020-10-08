---
title: '[MOCK] Initial Setup for Enablement'
seo-title: 초기 설정
description: '[MOCK] Initial Setup for Enablement'
seo-description: '[MOCK] Initial Setup for Enablement'
uuid: 873ec41d-c088-41d9-a535-de5300661de6
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: f2ac3d66-cc79-498f-83fb-dd96feb88de2
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '866'
ht-degree: 2%

---


# [MOCK] Initial Setup for Enablement  {#initial-setup-for-enablement}

## 작성 및 게시 인스턴스 시작 {#start-author-and-publish-instances}

개발 및 데모에서는 작성자 및 게시 인스턴스 하나를 실행해야 합니다.

기본 AEM 시작 [지침을](../../help/sites-deploying/deploy.md#getting-started) 따라

* localhost: [4502의 작성 환경](http://localhost:4502/)
* localhost: [4503에 게시 환경](http://localhost:4503/)

AEM Communities의 경우

* 작성 환경은 다음과 같습니다.

   * 사이트, 템플릿, 구성 요소, 역량 강화 리소스 및 학습 경로 개발
   * 역량 강화 리소스 및 학습 경로에 멤버 및 그룹 할당
   * 할당, 보기 및 게시물에 대한 보고서 생성
   * 관리 및 구성 작업

* 게시 환경은 다음과 같습니다.

   * 활성 관리자가 관리하는 항목을 기반으로 한 학습/교육
   * 주석 달기 및 등급 지원 리소스 및 학습 경로
   * 리소스 연락처에 연락하는 중입니다.

>[!NOTE]
>
>AEM에 익숙하지 않은 경우 [기본 처리](../../help/sites-authoring/basic-handling.md) 및 페이지 작성에 대한 [빠른 안내서에 대한 설명서를 봅니다](../../help/sites-authoring/qg-page-authoring.md).

## 최신 커뮤니티 릴리스 설치 {#install-latest-communities-release}

이 자습서는 [활성 커뮤니티 사이트를 만듭니다](overview.md#enablement-community). 최신 기능 팩을 설치하려면 다음을 방문하십시오.

* [최신 릴리스](deploy-communities.md#latest-releases)

참여 커뮤니티 사이트 [를 만드는 자습서를 보려면 AEM Communities](overview.md#engagement-community)로 시작하기를 참조하십시오 [](getting-started.md).

## 활성 기능 구성 {#configure-enablement-features}

이 자습서를 따르려면 MySQL 및 FFmpeg와 같은 타사 제품이 필요한 지원을 올바르게 설치하고 [구성해야](enablement.md)합니다.

## Analytics 구성 {#configure-analytics}

커뮤니티 사이트에 대해 [Adobe Analytics이 구성되면 커뮤니티 구성원](analytics.md)(수강생)에게 할당된 활성 리소스 및 학습 경로에 대해 생성된 [보고서에](reports.md) 더 많은 정보를 사용할 수 있습니다.

## 알림용 이메일 구성 {#configure-email-for-notifications}

콘솔을 사용하여 만든 모든 사이트에 대해 기본적으로 사용할 수 있는 알림 기능은 `Communities Sites` 알림에 대한 이메일 채널을 제공합니다.

사이트에 맞게 이메일을 올바르게 구성하는 데 필요한 사항

See [Configuring Email](email.md).

## 터널 서비스 활성화 {#enable-the-tunnel-service}

작성 환경에서 커뮤니티 사이트를 만들 때 터널 서비스는 게시 환경에 등록된 사용자 및 사용자 그룹(구성원)을 만들고 관리하고, 신뢰할 수 있는 커뮤니티 구성원에게 역할을 할당하고, 수강생에게 컨텐츠를 할당하는 기능을 제공합니다.

자세한 내용은 사용자 [및 사용자 그룹 관리를 참조하십시오](users.md).

터널 서비스를 활성화하는 간단한 지침은 [터널 서비스를 참조하십시오](deploy-communities.md#tunnel-service-on-author).

## 자습서 태그 만들기 {#create-tutorial-tags}

의 태그 네임스페이스를 사용하여 참여 및 활성화 튜토리얼에 사용할 태그를 만듭니다 `Tutorial`.

태깅 콘솔 [을 사용하여](../../help/sites-administering/tags.md#tagging-console) 다음 태그를 만듭니다.

* `Tutorial: Sports / Baseball`
* `Tutorial: Sports / Gymnastics`
* `Tutorial: Sports / Skiing`
* `Tutorial: Arts / Visual`
* `Tutorial: Arts / Auditory`
* `Tutorial: Arts / History`

![tutorial-tags](assets/tutorial-tags.png)

그런 다음 지침에 따라 다음을 수행합니다.

1. [태그 권한 설정](../../help/sites-administering/tags.md#setting-tag-permissions)
1. [태그 게시](../../help/sites-administering/tags.md#publishing-tags)

AEM Communities 시작하기 Tutorials에 대해 만든 태그의 샘플 패키지

[파일 가져오기](assets/communities_tutorialtags-10.zip)

## 활성 멤버 및 그룹 만들기 {#create-enablement-members-and-groups}

활성 커뮤니티 사이트의 경우 사이트 방문자는 [직접 등록하거나 소셜 로그인을 사용할 수 없습니다](sites-console.md#user-management).

대신 [터널 서비스를](#enable-the-tunnel-service) 활성화하면 [멤버 콘솔을](members.md) 사용하여 게시 환경에서 새 멤버를 등록합니다.

이 자습서에서는 게시 환경에서 세 명의 멤버가 만들어집니다. 두 명의 구성원은 학습 경로에 할당된 사용자 그룹의 구성원이 되고 세 번째 멤버는 활성 리소스 연락처가 됩니다.

네 번째 사용자는 작성 환경에서 만들어지고 커뮤니티 관리자 및 커뮤니티 활성 관리자의 역할을 할당합니다.

>[!NOTE]
>
>이러한 멤버는 [ *활성 자습서* ] 커뮤니티 사이트를 만들기 전에 제작되고 있습니다.
>
>이후에 만든 경우 멤버 생성 중에 [ *활성 자습서 구성원] 그룹의* 구성원으로 추가할 수 있습니다.
>
>대신 나중에 구성원 그룹에 [할당됩니다](enablement-create-site.md#assignuserstocommunityenablemembersgroup).

### 라일리 테일러 - 등록자 {#riley-taylor-enrollee}

[수강생 그룹(커뮤니티 스키 클래스 그룹)에 추가될 구성원을](members.md#create-new-member) 만듭니다.

* **ID**:라일리
* **이메일**:riley.taylor@mailinator.com
* **암호**:암호
* **암호 확인**:암호
* **이름**:라일리
* **성**:테일러

### 시드니 크로프트 - 등록자 {#sidney-croft-enrollee}

[Community Ski Class 그룹에 추가될 두 번째 멤버를](members.md#create-new-member) 만듭니다.

* **ID**:시드니
* **이메일**:sidney.croft@mailinator.com
* **암호**:암호
* **암호 확인**:암호
* **이름**:시드니
* **성**:크로프트

### 퀸 하퍼 - 지원 리소스 연락처 및 중재자 {#quinn-harper-enablement-resource-contact-and-moderator}

[사이트가 만들어지면 커뮤니티 사이트의 구성원 그룹에 추가될 구성원을](members.md#create-new-member) 만듭니다. 이 멤버십을 통해 사이트에 대한 활성 리소스가 생성될 때 [멤버](resources.md#settings) 가 활성 리소스 담당자로 지정될 수 있습니다.

* **ID**:퀸
* **이메일**:quinn.harper@mailinator.com
* **암호**:암호
* **암호 확인**:암호
* **이름**:퀸
* **성**:하퍼

### 사용자 그룹 추가 - 커뮤니티 스키 클래스 {#add-a-user-group-community-ski-class}

[Community Ski Class라는 새 그룹을](members.md#create-new-group) 추가합니다.

* **ID**:지역 스키 등급
* **이름**:커뮤니티 스키 클래스
* **설명**:활성 리소스 할당을 위한 샘플 그룹
* **그룹 &#39;추가&#39;에** 구성원 추가:

   * 라일리
   * 시드니

* **[!UICONTROL 저장]**&#x200B;을 선택합니다

### 커뮤니티 스키 클래스 속성 {#community-ski-class-properties}

![스키 클래스 속성](assets/ski-class-properties.png)

>[!NOTE]
>
>커뮤니티 사이트를 만드는 동안 기존 구성원 및 그룹을 커뮤니티 사이트의 구성원 그룹에 추가할 수 있습니다.

## 커뮤니티 관리자 역할 {#community-administrator-role}

커뮤니티 관리자 그룹의 구성원은 커뮤니티 사이트를 만들고 사이트를 관리하며 구성원을 관리하고(커뮤니티의 구성원을 금지할 수 있음) 콘텐트를 중재할 수 있습니다.

### 사용자 만들기 {#create-user}

커뮤니티 관리자 역할이 할당된 *작성자에*&#x200B;대한 사용자를 만듭니다.

* 작성 인스턴스에서

   * 예: [http://localhost:4502/](http://localhost:4503/)

* 관리자 권한으로 로그인

   * 예: 사용자 이름 &#39;admin&#39; / 암호 &#39;admin&#39;

* 주 콘솔에서 **[!UICONTROL 도구]** > 작업 **[!UICONTROL >]** 보안 ******[!UICONTROL >]**&#x200B;사용자로이동합니다.
* [ **[!UICONTROL 편집]** ] 메뉴에서 사용자 **[!UICONTROL 추가를 선택합니다]**.

* 대화 상자에서 다음을 `Create New User` 입력합니다.

   * **ID&amp;ast;**:시리우스
   * **이메일 주소**:sirius.nilson@mailinator.com
   * **암호;마지막;**:암호
   * **암호 확인;암호;마지막;**:암호
   * **이름**:시리우스
   * **마지막 이름;amp;ast;**:닐슨

### 커뮤니티 관리자 그룹에 Sirius 할당 {#assign-sirius-to-community-administrators-group}

아래로 스크롤: `Add User to Groups`

* 검색할 &#39;C&#39;를 입력하십시오.

   * 선택 `Community Administrators`
   * 선택 `Community Enablement Managers`

* **[!UICONTROL 저장]**&#x200B;을 선택합니다

![admin-role](assets/admin-role.png)

