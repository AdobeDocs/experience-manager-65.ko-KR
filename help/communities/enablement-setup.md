---
title: 활성화를 위한 초기 설정
seo-title: 초기 설정
description: 활성화를 위한 초기 설정
seo-description: 활성화를 위한 초기 설정
uuid: 873ec41d-c088-41d9-a535-de5300661de6
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: f2ac3d66-cc79-498f-83fb-dd96feb88de2
translation-type: tm+mt
source-git-commit: d6c8bbb9aa763a2eb6660b6b6755aba75241e394

---


# 활성화를 위한 초기 설정 {#initial-setup-for-enablement}

## 작성 및 게시 인스턴스 시작 {#start-author-and-publish-instances}

개발 및 데모를 위해 작성자 및 게시 인스턴스 하나를 실행해야 합니다.

기본 AEM 시작 [지침을](../../help/sites-deploying/deploy.md#getting-started) 따라

* 로컬 호스트의 작성 [환경:4502](http://localhost:4502/)
* localhost: [4503에 환경 게시](http://localhost:4503/)

AEM Communities,

* 작성 환경은

   * 사이트, 템플릿, 구성 요소, 역량 강화 리소스 및 학습 경로 개발
   * 역량 강화 리소스 및 학습 경로에 멤버 및 그룹 할당
   * 할당, 보기 및 게시물에 대한 보고서 생성
   * 관리 및 구성 작업

* 게시 환경은

   * 역량 강화 관리자가 관리하는 주제에 따라 학습/교육
   * 주석 달기 및 등급 지원 리소스 및 학습 경로
   * 리소스 연락처에 연락하기

>[!NOTE]
>
>AEM에 익숙하지 않은 경우 [기본 처리에](../../help/sites-authoring/basic-handling.md) 대한 설명서와 페이지 [작성에 대한](../../help/sites-authoring/qg-page-authoring.md)빠른 안내서를 봅니다.

## 최신 커뮤니티 릴리스 설치 {#install-latest-communities-release}

이 자습서는 [역량 강화 커뮤니티 사이트를](overview.md#enablement-community)만듭니다. 최신 기능 팩이 설치되어 있는지 확인하려면 다음을 참조하십시오.

* [최신 릴리스](deploy-communities.md#latest-releases)

참여 커뮤니티 사이트를 [만드는 자습서를 보려면 AEM Communities](overview.md#engagement-community)시작하기를 참조하십시오 [](getting-started.md).

## 지원 기능 구성 {#configure-enablement-features}

이 자습서를 따르려면 MySQL 및 FFmpeg와 같은 타사 제품이 필요한 지원을 [올바르게 설치하고](enablement.md)구성해야 합니다.

## Analytics 구성 {#configure-analytics}

Adobe [Analytics가 커뮤니티 사이트에](analytics.md)대해 구성되면 커뮤니티 구성원(수강생)에게 할당된 활성 리소스 및 학습 경로에 대해 생성된 [보고서에서](reports.md) 추가 정보를 사용할 수 있습니다.

## 알림용 이메일 구성 {#configure-email-for-notifications}

콘솔을 사용하여 만든 모든 사이트에 대해 기본적으로 제공되는 알림 기능은 알림을 위한 이메일 채널을 제공합니다. `Communities Sites`

사이트에 맞게 이메일을 올바르게 구성하는 데 필요한 사항은 다음과 같습니다.

See [Configuring Email](email.md).

## 터널 서비스 활성화 {#enable-the-tunnel-service}

작성 환경에서 커뮤니티 사이트를 만들 때 터널 서비스를 사용하면 게시 환경에 등록된 사용자 및 사용자 그룹(구성원)을 만들고 관리하고, 신뢰할 수 있는 커뮤니티 구성원에게 역할을 할당하고, 수강생에게 컨텐츠를 할당할 수 있습니다.

자세한 내용은 사용자 및 [사용자 그룹 관리를 참조하십시오](users.md).

터널 서비스를 활성화하는 간단한 지침은 터널 서비스를 [참조하십시오](deploy-communities.md#tunnel-service-on-author).

## 자습서 태그 만들기 {#create-tutorial-tags}

의 태그 네임스페이스를 사용하여 참여 및 역량 강화 튜토리얼에 사용할 태그를 `Tutorial`만듭니다.

태깅 [콘솔을](../../help/sites-administering/tags.md#tagging-console) 사용하여 다음 태그를 만듭니다.

* `Tutorial: Sports / Baseball`
* `Tutorial: Sports / Gymnastics`
* `Tutorial: Sports / Skiing`
* `Tutorial: Arts / Visual`
* `Tutorial: Arts / Auditory`
* `Tutorial: Arts / History`

![chlimage_1-417](assets/chlimage_1-417.png)

그런 다음 지침에 따라

1. [태그 권한 설정](../../help/sites-administering/tags.md#setting-tag-permissions)
1. [태그 게시](../../help/sites-administering/tags.md#publishing-tags)

AEM Communities 시작하기 자습서에 대해 만든 태그의 샘플 패키지

[파일 가져오기](assets/communities_tutorialtags-10.zip)

## 활성 멤버 및 그룹 만들기 {#create-enablement-members-and-groups}

활성 커뮤니티 사이트의 경우 사이트 방문자는 [직접 등록하거나 소셜 로그인을](sites-console.md#user-management)사용할 수 없습니다.

대신 [터널 서비스가](#enable-the-tunnel-service) 활성화되면 멤버 콘솔을 [](members.md) 사용하여 게시 환경에서 새 멤버를 등록합니다.

이 자습서에서는 게시 환경에서 세 명의 멤버가 만들어집니다. 두 구성원은 학습 경로에 할당된 사용자 그룹의 구성원이 되고 세 번째 멤버는 지원 리소스 연락처가 됩니다.

네 번째 사용자는 작성 환경에서 생성되며 커뮤니티 관리자 및 커뮤니티 활성화 관리자의 역할을 할당합니다.

>[!NOTE]
>
>이러한 구성원은 활성 자습서 커뮤니티 사이트를 만들기 전에 *만들어진* 것입니다.
>
>이후에 만들어진 경우, 멤버 생성 중에 활성 자습서 *멤버 그룹의* 멤버로 추가할 수 있습니다.
>
>대신, 나중에 구성원 그룹에 [할당됩니다](enablement-create-site.md#assignuserstocommunityenablemembersgroup).

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

[사이트가 만들어지면 커뮤니티 사이트의 구성원 그룹에 추가될 구성원을](members.md#create-new-member) 만듭니다. 이 멤버십을 통해 사이트에 대한 활성 리소스가 [생성될](resources.md#settings) 때 멤버를 활성 리소스 연락처로 지정할 수 있습니다.

* **ID**:퀸
* **이메일**:quinn.harper@mailinator.com
* **암호**:암호
* **암호 확인**:암호
* **이름**:퀸
* **성**:하퍼

### 사용자 그룹 추가 - 커뮤니티 스키 클래스 {#add-a-user-group-community-ski-class}

[Community Ski Class라는 새 그룹을](members.md#create-new-group) 추가합니다.

* **ID**:커뮤니티 스키 등급
* **이름**:커뮤니티 스키 클래스
* **설명**:역량 강화 리소스를 지정하기 위한 샘플 그룹
* **그룹 &#39;추가&#39;에 구성원** 추가:

   * 라일리
   * 시드니

* **[!UICONTROL 저장]**&#x200B;을 선택합니다

### 커뮤니티 스키 클래스 속성 {#community-ski-class-properties}

![chlimage_1-418](assets/chlimage_1-418.png)

>[!NOTE]
>
>커뮤니티 사이트를 만드는 동안 기존 구성원 및 그룹이 커뮤니티 사이트의 구성원 그룹에 추가될 수 있습니다.

## 커뮤니티 관리자 역할 {#community-administrator-role}

커뮤니티 관리자 그룹의 구성원은 커뮤니티 사이트를 만들고 사이트를 관리하며 구성원을 관리(커뮤니티의 구성원을 금지할 수 있음) 및 컨텐츠를 중재할 수 있습니다.

### 사용자 만들기 {#create-user}

커뮤니티 관리자의 역할이 할당된 *작성자에*&#x200B;대한 사용자를 만듭니다.

* 작성자 인스턴스에서

   * 예: [http://localhost:4502/](http://localhost:4503/)

* 관리자 권한으로 로그인

   * 예: 사용자 이름 &#39;admin&#39; / 암호 &#39;admin&#39;

* 주 콘솔에서 도구, 작업 > **[!UICONTROL 보안 > 사용자로 이동합니다.]**
* 편집 **[!UICONTROL 메뉴에서]** 사용자 **[!UICONTROL 추가를 선택합니다]**

* 대화 `Create New User` 상자에서

   * **ID&amp;ast;**:시리우스
   * **이메일 주소**:sirius.nilson@mailinator.com
   * **암호;암호;ast;**:암호
   * **암호 확인;암호;암호**&#x200B;확인;암호
   * **이름**:시리우스
   * **성;amp;ast;**:닐슨

### 커뮤니티 관리자 그룹에 Sirius 할당 {#assign-sirius-to-community-administrators-group}

아래로 스크롤: `Add User to Groups`

* 검색하려면 &#39;C&#39;를 입력하십시오.

   * 선택 `Community Administrators`
   * 선택 `Community Enablement Managers`

* **[!UICONTROL 저장]**&#x200B;을 선택합니다

![chlimage_1-419](assets/chlimage_1-419.png)

