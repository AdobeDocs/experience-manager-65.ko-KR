---
title: 지원을 위한 새 커뮤니티 사이트 만들기
seo-title: 지원을 위한 새 커뮤니티 사이트 만들기
description: 지원을 위한 커뮤니티 사이트 만들기
seo-description: 지원을 위한 커뮤니티 사이트 만들기
uuid: a75fa566-a570-45fd-aabc-23651ef819cc
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: b9333558-6af9-46b2-9f03-3722645c69a6
docset: aem65
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '1728'
ht-degree: 3%

---


# 지원 {#author-a-new-community-site-for-enablement}에 대한 새 커뮤니티 사이트 만들기

## 커뮤니티 사이트 만들기 {#create-community-site}

[커뮤니티 사이트 ](/help/communities/sites-console.md) 만들기커뮤니티 사이트를 만드는 단계를 안내하는 마법사를 사용합니다. 마지막 단계에서 사이트를 커밋하기 전에 `Next` 단계 또는 `Back`로 이전 단계로 이동할 수 있습니다.

새 커뮤니티 사이트 만들기를 시작하려면 다음을 수행하십시오.

[작성자 인스턴스 사용](https://localhost:4502/)

* 관리자 권한으로 로그인하고 **[!UICONTROL 커뮤니티]** > **[!UICONTROL 사이트]**&#x200B;로 이동합니다.

* **만들기**&#x200B;를 선택합니다.

### 1단계:사이트 템플릿 {#step-site-template}

![활성 사이트 템플릿](assets/enablement-site-template.png)

**사이트 템플릿** 단계에서 제목, 설명, URL의 이름을 입력하고 커뮤니티 사이트 템플릿을 선택합니다. 예:

* **커뮤니티 사이트 제목**: `Enablement Tutorial`.

* **커뮤니티 사이트 설명**: `A site for enabling the community to learn.`

* **커뮤니티 사이트 루트**:(기본 루트에 대해서는 비워  `/content/sites`둡니다.

* **클라우드 구성**:(클라우드 구성이 지정되지 않은 경우 비워 두십시오) 지정된 클라우드 구성에 대한 경로를 제공합니다.
* **커뮤니티 사이트 기본 언어**:(단일 언어로 변경하지 않고 유지):영어) 드롭다운을 사용하여 독일어, 이탈리아어, 프랑스어, 일본어, 스페인어, 포르투갈어(브라질), 중국어(번체), 중국어(간체) 등 사용 가능한  ** 언어에서 하나 이상의 기본 언어를 선택합니다. 추가된 각 언어에 대해 하나의 커뮤니티 사이트가 생성되고 [다국어 사이트에 대한 컨텐츠 번역](/help/sites-administering/translation.md)에 설명된 우수 사례 다음에 동일한 사이트 폴더 내에 존재합니다. 각 사이트의 루트 페이지에는 선택한 언어 중 하나의 언어 코드에 의해 이름이 지정된 하위 페이지가 포함됩니다(예: 영어의 경우 &#39;en&#39;, 프랑스어의 경우 &#39;fr&#39;).

* **커뮤니티 사이트 이름**: `enable`

   * 초기 URL이 커뮤니티 사이트 이름 아래에 표시됩니다.
   * 유효한 URL의 경우 기본 언어 코드 + &quot;.html&quot;을 추가합니다.
      *예*: https://localhost:4502/content/sites/  `enable/en.html`

* **참조 사이트 템플릿**:아래로 이동하여 선택  `Reference Structured Learning Site Template`

**다음**&#x200B;을 선택합니다.

### 2단계:{#step-design} 디자인

디자인 단계는 테마와 브랜딩 배너를 선택하기 위한 2개의 섹션에 표시됩니다.

#### 커뮤니티 사이트 테마 {#community-site-theme}

템플릿에 적용할 원하는 스타일을 선택합니다. 이 옵션을 선택하면 테마가 체크 표시로 겹쳐 표시됩니다.

#### 커뮤니티 사이트 브랜딩 {#community-site-branding}

(선택 사항) 배너 이미지를 업로드하여 사이트 페이지에 표시합니다. 배너는 커뮤니티 사이트 헤더와 메뉴(탐색 링크) 사이의 브라우저의 왼쪽 가장자리에 고정됩니다. 배너 높이는 120픽셀로 잘립니다. 브라우저 폭과 120픽셀 높이에 맞게 배너의 크기를 조정할 수 없습니다.

![chlimage_1-449](assets/chlimage_1-449.png)

![chlimage_1](assets/chlimage_1.jpeg)

**다음**&#x200B;을 선택합니다.

### 3단계:설정 {#step-settings}

설정 단계에서 `Next`을 선택하기 전에 사용자 관리, 태깅, 역할, 중재, 분석, 번역 및 활성화와 관련된 구성에 대한 액세스를 제공하는 7개의 섹션이 있음을 알 수 있습니다.

#### 사용자 관리 {#user-management}

[역량 강화 커뮤니티](/help/communities/overview.md#enablement-community)은(는) 비공개로 하는 것이 좋습니다.

커뮤니티 사이트는 익명의 사이트 방문자가 액세스가 거부되면 비공개로 설정되며 자체 등록을 할 수 없으며 소셜 로그인을 사용할 수 없습니다.

[사용자 관리](/help/communities/sites-console.md#user-management)에 대해 대부분의 확인란은 선택 취소되어 있는지 확인합니다.

* 사이트 방문자가 직접 등록할 수 없도록 하십시오.
* 익명 사이트 방문자가 사이트를 보도록 허용하지 마십시오.
* 커뮤니티 구성원 간의 메시징을 허용할지 여부(선택 사항).
* Facebook 로그인을 허용하지 마십시오.
* Twitter 로그인을 허용하지 마십시오.

![사용자 관리](assets/user-mgmt.png)

#### {#tagging} 태깅

커뮤니티 콘텐츠에 적용할 수 있는 태그는 [태깅 콘솔](/help/sites-administering/tags.md#tagging-console)(예: [Tutorial 네임스페이스](/help/communities/enablement-setup.md#create-tutorial-tags))을 통해 이전에 정의된 AEM 네임스페이스를 선택하여 제어합니다.

또한 커뮤니티 사이트에 대한 태그 네임스페이스를 선택하면 카탈로그와 지원 리소스를 정의할 때 표시되는 선택 영역이 제한됩니다. 중요한 정보는 [Tagging Enablement Resources](/help/communities/tag-resources.md)을 참조하십시오.

사전 문자 검색을 사용하면 네임스페이스를 손쉽게 찾을 수 있습니다. 예,

* 유형 `tut`
* 선택 `Tutorial`

![역량 강화 태깅](assets/enablement-tagging.png)

### 역할 {#roles}

[커뮤니티 구성원 ](/help/communities/users.md) 롤은 역할 섹션의 설정을 통해 할당됩니다.

커뮤니티 구성원(또는 구성원 그룹)이 사이트를 커뮤니티 관리자로 경험하도록 하려면 사전 유형 검색을 사용하고 드롭다운의 옵션에서 구성원 또는 그룹 이름을 선택합니다.

예,

* 유형 `q`
* [퀸 하퍼](/help/communities/enablement-setup.md#publishcreateenablementmembers) 선택

>[!NOTE]
>
>[터널 ](/help/communities/deploy-communities.md#tunnel-service-on-author) 서비스를 통해 게시 환경에만 있는 구성원 및 그룹을 선택할 수 있습니다.

![활성 역할](assets/site-admin.png)

#### 중재 {#moderation}

[중재](/help/communities/sites-console.md#moderation) 사용자가 생성한 콘텐츠(UGC)에 대한 기본 전역 설정을 적용합니다.

![chlimage_1-452](assets/chlimage_1-452.png)

#### 분석 {#analytics}

드롭다운에서 이 커뮤니티 사이트에 대해 구성된 Analytics 클라우드 서비스 프레임워크를 선택합니다.

스크린샷에 표시된 `Communities`은 [구성 설명서의 프레임워크 예입니다.](/help/communities/analytics.md#aem-analytics-framework-configuration)

![chlimage_1-454](assets/chlimage_1-454.png)

#### 번역 {#translation}

[번역 설정](/help/communities/sites-console.md#translation)은 UGC를 변환할 수 있는지 여부와 변환할 수 있는 언어(있는 경우)를 지정합니다.

* **기계 번역 허용** 확인
* 기본 설정 사용

![chlimage_1-456](assets/chlimage_1-456.png)

#### 지원 {#enablement}

역량 강화 커뮤니티의 경우 하나 이상의 커뮤니티 활성화 관리자를 식별해야 합니다.

* **활성 관리자**
(필수) 
`Community Enablement Managers` 그룹을 선택하여 이 커뮤니티 사이트를 관리할 수 있습니다.

   * 유형 `s`
   * 선택 `Sirius Nilson`

* **Marketing Cloud 조직 ID**
(선택 사항) 지원 보고에  [비디오 하트비트 분석을 포함시킬 때 필요한 Adobe Analytics ](/help/communities/analytics.md#video-heartbeat-analytics) 계정의 ID입니다.

![chlimage_1-457](assets/chlimage_1-457.png)

**다음**&#x200B;을 선택합니다.

### 4단계:커뮤니티 사이트 {#step-create-community-site} 만들기

**만들기**&#x200B;를 선택합니다.

![chlimage_1-458](assets/chlimage_1-458.png)

프로세스가 완료되면 커뮤니티 > 사이트 콘솔에 새 사이트에 대한 폴더가 표시됩니다.

![enablementsitereated](assets/enablementsitecreated.png)

### 새 커뮤니티 사이트 {#publish-the-new-community-site} 게시

만들어진 사이트는 새 사이트를 만들 수 있는 콘솔과 동일한 콘솔인 커뮤니티 - 사이트 콘솔에서 관리해야 합니다.

커뮤니티 사이트의 폴더를 선택한 후 4개의 작업 아이콘이 나타나도록 사이트 아이콘 위에 마우스를 놓습니다.

![siteactionicons](assets/siteactionicons.png)

줄임표 아이콘(추가 작업 아이콘)을 선택하면 사이트 내보내기 및 사이트 삭제 옵션이 표시됩니다.

![siteaction새로운 기능](assets/siteactionsnew.png)

왼쪽에서 오른쪽으로:

* **사이트 열기**

   연필 아이콘을 선택하여 작성 편집 모드에서 커뮤니티 사이트를 열고 페이지 구성 요소를 추가 및/또는 구성합니다.

* **사이트 편집**

   속성 아이콘을 선택하여 커뮤니티 사이트를 열어 제목과 같은 속성을 수정하거나 테마를 변경할 수 있습니다.

* **게시 사이트**

   커뮤니티 사이트를 게시할 세계 아이콘을 선택합니다(기본적으로 localhost:4503으로).

* **사이트 내보내기**

   내보내기 아이콘을 선택하여 [패키지 관리자](/help/sites-administering/package-manager.md)에 모두 저장되고 다운로드한 커뮤니티 사이트의 패키지를 만듭니다.
UGC는 사이트 패키지에 포함되지 않습니다.

* **사이트 삭제**

   커뮤니티 사이트를 삭제하려면 커뮤니티 사이트 콘솔에서 마우스를 사이트 위로 가져가면 나타나는 사이트 삭제 아이콘을 선택합니다. 이 작업은 UGC, 사용자 그룹, 자산 및 데이터베이스 레코드 등 사이트와 연관된 모든 항목을 제거합니다.

   ![활성화 항목](assets/enablesiteactions.png)

#### 게시{#select-publish}를 선택합니다 

커뮤니티 사이트를 게시하려면 월드 아이콘을 선택합니다.

![chlimage_1-465](assets/chlimage_1-465.png)

그 사이트가 출판되었다는 표시가 있을 것이다.

![chlimage_1-466](assets/chlimage_1-466.png)

## 커뮤니티 사용자 및 사용자 그룹 {#community-users-user-groups}

### 새 커뮤니티 사용자 그룹 {#notice-new-community-user-groups} 알림

새 커뮤니티 사이트와 함께 다양한 관리 기능에 적절한 권한이 설정된 새 사용자 그룹이 만들어집니다. 자세한 내용은 커뮤니티 사이트에 대한 [사용자 그룹](/help/communities/users.md#usergroupsforcommunitysites)을 참조하십시오.

1단계의 사이트 이름이 &quot;활성화&quot;인 이 새 커뮤니티 사이트의 경우 게시 환경에 존재하는 새 사용자 그룹이 [커뮤니티 구성원 및 그룹 콘솔](/help/communities/members.md#groups-console)에서 표시될 수 있습니다.

![community_usergroup](assets/community_usergroup.png)

### 커뮤니티 구성원 할당 구성원 그룹 활성화 {#assign-members-to-community-enable-members-group}

작성자의 경우, 터널 서비스가 활성화되어 있으면 새로 만든 커뮤니티 사이트에 대해 초기 설정](/help/communities/enablement-setup.md#publishcreateenablementmembers) 중에 만든 [사용자를 커뮤니티 구성원 그룹에 할당할 수 있습니다.

커뮤니티 그룹 콘솔을 사용하여 구성원을 개별적으로 추가하거나 그룹의 멤버십을 통해 추가할 수 있습니다.

이 예에서 그룹 `Community Ski Class`은 구성원 `Quinn Harper`뿐만 아니라 그룹 `Community Enable Members`의 구성원으로 추가됩니다.

* **커뮤니티, 그룹** 콘솔로 이동합니다.
* *커뮤니티 구성원 활성화* 그룹 선택
* **그룹에 구성원 추가** 검색 상자에 &#39;ski&#39;를 입력합니다.
* *커뮤니티 스키 클래스*(수강생 그룹)를 선택합니다.
* 검색 상자에 &#39;퀸&#39;을 입력합니다.
* *퀸 하퍼* (지원 리소스 연락처)를 선택합니다.

* **저장**&#x200B;을 선택합니다

![chlimage_1-418](assets/chlimage_1-418.png)

## 게시 시 구성 {#configurations-on-publish}

`https://localhost:4503/content/sites/enable/en.html {#http-localhost-content-sites-enable-en-html}`

![enablement-login](assets/enablement-login.png)

### 인증 구성 오류 {#configure-for-authentication-error}

사이트가 구성되고 게시로 푸시되면 게시 인스턴스에서 [로그인 매핑](/help/communities/sites-console.md#configure-for-authentication-error)( `Adobe Granite Login Selector Authentication Handler`)을 구성합니다. 로그인 자격 증명을 올바르게 입력하지 않으면 인증 오류가 오류 메시지와 함께 커뮤니티 사이트의 로그인 페이지가 다시 표시됩니다.

다음 이름으로 `Login Page Mapping`을(를) 추가합니다.

* `/content/sites/enable/en/signin:/content/sites/enable/en`

### (선택 사항) 기본 홈 페이지 {#optional-change-the-default-home-page} 변경

데모를 위해 게시 사이트를 사용할 때 기본 홈 페이지를 새 사이트로 변경하는 것이 유용할 수 있습니다.

이렇게 하려면 [CRX|DE](https://localhost:4503/crx/de) Lite를 사용하여 게시에서 [리소스 매핑](/help/sites-deploying/resource-mapping.md) 표를 편집해야 합니다.

시작하려면 다음을 수행하십시오.

1. 게시 시 CRXDE에 액세스하고 관리자 권한으로 로그인

   * 예를 들어 [https://localhost:4503/crx/de](https://localhost:4503/crx/de)로 이동하여 `admin/admin`로 로그인합니다.

1. 프로젝트 브라우저에서 `/etc/map` 확장
1. `http` 노드 선택

   * **노드 만들기**&#x200B;를 선택합니다.

      * **** Namelocalhost.4503

         (do *not* use &#39;:&#39;)

      * **유형** [지정:매핑](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)

1. 새로 만든 `localhost.4503` 노드가 선택된 상태에서

   * 속성 추가

      * **이름** 지정:일치
      * **TypeString** 
      * **** Valuelocalhost.4503/$

   (&#39;$&#39; 문자로 끝나야 합니다.)

   * 속성 추가

      * **이름** 지정:internalRedirect
      * **TypeString** 
      * **값** /content/sites/enable/en.html


1. **모두 저장** 선택
1. (선택 사항) 검색 내역을 삭제합니다.
1. https://localhost:4503/으로 이동

   * https://localhost:4503/content/sites/enable/en.html에 도착

>[!NOTE]
>
>비활성화하려면 `sling:match` 속성 값을 &#39;x&#39; - `xlocalhost.4503/$` - 및 **모두 저장**&#x200B;과(와) 함께 프리펜드하면 됩니다.

![chlimage_1-364](assets/chlimage_1-364.png)

#### 문제 해결:맵 {#troubleshooting-error-saving-map} 저장 중 오류 발생

변경 내용을 저장할 수 없는 경우 노드 이름이 `localhost.4503`이고 &#39;dot&#39; 구분 기호가 있고 &#39;콜론&#39; 구분 기호가 있는 `localhost:4503`이 아닌 `localhost`인지 확인하십시오. 이때 &lt;a2/>는 올바른 네임스페이스 접두사가 아닙니다.

![chlimage_1-365](assets/chlimage_1-365.png)

#### 문제 해결:{#troubleshooting-fail-to-redirect} 리디렉션 실패

정규 표현식 `sling:match` 문자열의 끝에 있는 &#39;**$**&#39;은(는) 매우 중요하므로 정확히 `https://localhost:4503/`만 매핑되고, 그렇지 않으면 리디렉션 값이 URL의 server:port 다음에 존재할 수 있는 경로에 프리펜됩니다. 따라서 AEM에서 로그인 페이지로 리디렉션하려고 하면 실패합니다.

## 커뮤니티 사이트 수정 {#modifying-the-community-site}

사이트가 처음 만들어지면 작성자는 [사이트 열기 아이콘](/help/communities/sites-console.md#authoring-site-content)을 사용하여 표준 AEM 작성 활동을 수행할 수 있습니다.

또한 관리자는 [사이트 편집 아이콘](/help/communities/sites-console.md#modifying-site-properties)을 사용하여 제목과 같은 사이트의 속성을 수정할 수 있습니다.

수정 후에는 **저장**&#x200B;을(를) 기억하고 **사이트**&#x200B;게시를 다시 수행합니다.

>[!NOTE]
>
>AEM에 익숙하지 않은 경우 [기본 처리](/help/sites-authoring/basic-handling.md)에 대한 설명서와 [빠른 페이지 작성 안내서](/help/sites-authoring/qg-page-authoring.md)를 참조하십시오.

### 카탈로그 추가 {#add-a-catalog}

이 커뮤니티 사이트에 대해 선택된 커뮤니티 사이트 템플릿에는 카탈로그 기능이 포함되어야 합니다.

그렇지 않은 경우 카탈로그 함수를 쉽게 추가할 수 있습니다. 이렇게 하면 역량 강화 리소스 또는 학습 경로에 지정되지 않은 커뮤니티 다른 구성원이 카탈로그에서 지원 리소스를 선택할 수 있습니다.

사이트 구조에 이미 카탈로그 기능이 포함되어 있으면 해당 제목을 변경할 수 있습니다.

사이트의 구조를 수정하려면 **[!UICONTROL 커뮤니티]** > **[!UICONTROL 사이트]** 콘솔로 이동하여 `enable` 폴더를 열고 **사이트 편집** 아이콘을 선택하여 `Enablement Tutorial`의 속성에 액세스합니다.

[구조] 패널을 선택하여 카탈로그를 추가하거나 기존 카탈로그를 수정합니다.

* **제목**: `Ski Catalog`

* **URL**: `catalog`

* **모든 네임스페이스 선택**:기본값으로 두십시오.

* **저장**&#x200B;을 선택합니다.

![chlimage_1-299](assets/chlimage_1-299.png)

위치 아이콘을 사용하여 카탈로그 함수를 할당 후 두 번째 위치로 이동합니다.

![chlimage_1-300](assets/chlimage_1-300.png)

커뮤니티 사이트에 대한 변경 내용을 저장하려면 오른쪽 위 모서리에서 **저장**&#x200B;을 선택합니다.

그런 다음 **게시**&#x200B;사이트를 다시 게시합니다.

