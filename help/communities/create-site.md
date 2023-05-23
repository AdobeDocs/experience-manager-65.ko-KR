---
title: 새 커뮤니티 사이트 작성자
seo-title: Author a New Community Site
description: 새 AEM Communities 사이트를 작성하는 방법
seo-description: How to author a new AEM Communities site
uuid: 4f609f5f-ef07-44fc-aeb3-1c616e120d46
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 8ae324ea-8b84-47a3-aabf-1fee2a3bd46d
docset: aem65
exl-id: d4c1895f-421c-4146-b94a-8d11065ef9e3
source-git-commit: 4dbbcc41757843d3b2d5a3bbb2656ef587e83d2c
workflow-type: tm+mt
source-wordcount: '1601'
ht-degree: 2%

---

# 새 커뮤니티 사이트 작성자{#author-a-new-community-site}

## 커뮤니티 사이트 만들기 {#create-a-community-site}

작성자 인스턴스를 사용하여 커뮤니티 사이트를 만듭니다. AEM 작성자 인스턴스에서 다음을 수행합니다.

1. 관리자 권한으로 로그인합니다.
1. 전역 탐색에서 다음으로 이동 **[!UICONTROL 커뮤니티]** > **[!UICONTROL 사이트]**.

커뮤니티 사이트 콘솔은 커뮤니티 사이트를 만드는 단계를 안내하는 마법사를 제공합니다. 다음으로 이동할 수 있습니다. `Next` 단계 또는 `Back` 마지막 단계에서 사이트를 커밋하기 전에 이전 단계로 이동합니다.

새 커뮤니티 사이트를 만들려면 다음 작업을 수행하십시오.

* 다음 항목 선택 `Create` 단추를 클릭합니다.

![createcommunitysite](assets/createcommunitysite.png)

### 1단계: 사이트 템플릿 {#step-site-template}

![사이트를 만들 템플릿](assets/create-site.png)

다음에서 [사이트 템플릿 단계](/help/communities/sites-console.md#step2013asitetemplate)을(를) 통해 제목, 설명, URL 이름을 입력하고 커뮤니티 사이트 템플릿을 선택합니다. 예를 들면 다음과 같습니다.

* **커뮤니티 사이트 제목**: `Getting Started Tutorial`
* **커뮤니티 사이트 설명**: `A site for engaging with the community.`
* **커뮤니티 사이트 루트**: (기본 루트는 비워 둡니다.) `/content/sites`)
* **클라우드 구성**: (클라우드 구성이 지정되지 않은 경우 공백으로 남김) 지정된 클라우드 구성의 경로를 제공합니다.
* **커뮤니티 사이트 기본 언어**: (단일 언어: 영어의 경우 그대로 유지) 드롭다운 목록을 사용하여 하나 선택 *이상* 독일어, 이탈리아어, 프랑스어, 일본어, 스페인어, 포르투갈어(브라질), 중국어(번체) 및 중국어(간체)의 기본 언어 커뮤니티 사이트는에 설명된 모범 사례에 따라 추가된 언어마다 하나씩 만들어지며 동일한 사이트 폴더 내에 존재합니다. [다국어 사이트를 위한 콘텐츠 번역](/help/sites-administering/translation.md). 각 사이트의 루트 페이지에는 선택한 언어 중 하나의 언어 코드로 이름이 지정된 하위 페이지(예: 영어의 경우 &#39;en&#39;, 프랑스어의 경우 &#39;fr&#39;)가 포함됩니다.

* **커뮤니티 사이트 이름**: engage

   * 사이트를 만든 후에는 쉽게 변경되지 않으므로 이름을 다시 확인하십시오
   * 커뮤니티 사이트 이름 아래에 초기 URL이 표시됩니다
   * 유효한 URL을 보려면 기본 언어 코드 + &quot;.html&quot;을 추가하십시오.
   * *예*, https://localhost:4502/content/sites/ `engage/en.html`

* **템플릿**: 풀다운하여 선택 `Reference Site`

* **다음**&#x200B;을 선택합니다.

### 2단계: 디자인 {#step-design}

디자인 단계는 테마 및 브랜딩 배너를 선택하기 위한 두 개의 섹션으로 표시됩니다.

#### 커뮤니티 사이트 테마 {#community-site-theme}

템플릿에 적용할 스타일을 선택합니다. 선택하면 테마가 확인 표시로 오버레이됩니다.

#### 커뮤니티 사이트 브랜딩 {#community-site-branding}

(선택 사항) 사이트 페이지에 표시할 배너 이미지를 업로드합니다. 배너는 커뮤니티 사이트 헤더와 탐색 링크 사이의 브라우저 왼쪽 가장자리에 고정됩니다. 배너 높이는 120픽셀로 잘립니다. 브라우저 너비와 120픽셀 높이에 맞게 배너의 크기를 조정할 수 없습니다.

![커뮤니티 사이트 브랜딩](assets/community-site-branding.png)

![upload-image-site](assets/upload-image-site.png)

**다음**&#x200B;을 선택합니다.

### 3단계: 설정 {#step-settings}

설정 단계에서 을 선택한 다음 `Next`, 사용자 관리, 태그 지정, 중재, 그룹 관리, 분석 및 번역과 관련된 구성에 대한 액세스 권한을 제공하는 7개의 섹션이 있습니다.

#### 사용자 관리 {#user-management}

모든 확인란 선택 [사용자 관리](/help/communities/sites-console.md#user-management)

* 사이트 방문자가 자가 자가 등록할 수 있도록 하려면
* 로그인 없이 사이트 방문자가 사이트를 볼 수 있도록 하려면
* 구성원이 다른 커뮤니티 구성원의 메시지를 보내고 받을 수 있도록 허용
* 프로필을 등록하고 만드는 대신 Facebook으로 로그인할 수 있도록 허용
* 프로필을 등록하고 만드는 대신 Twitter으로 로그인을 허용하려면

>[!NOTE]
>
>프로덕션 환경의 경우 사용자 지정 Facebook 및 Twitter 애플리케이션을 만들어야 합니다. 다음을 참조하십시오 [facebook 및 Twitter을 사용한 소셜 로그인](/help/communities/social-login.md).

![커뮤니티 사이트 설정](assets/site-settings.png)

#### 태깅 {#tagging}

커뮤니티 콘텐츠에 적용할 수 있는 태그는 를 통해 이전에 정의된 AEM 네임스페이스를 선택하여 제어됩니다. [태깅 콘솔](/help/sites-administering/tags.md#tagging-console) (예: [튜토리얼 네임스페이스](/help/communities/setup.md#create-tutorial-tags)).

형식 사전 검색을 사용하면 네임스페이스를 쉽게 찾을 수 있습니다. 예를 들어

* 유형 `tut`
* 선택 `Tutorial`

![태깅](assets/tagging.png)

#### 역할 {#roles}

[커뮤니티 구성원 역할](/help/communities/users.md) 은 역할 섹션의 설정을 통해 할당됩니다.

커뮤니티 구성원(또는 구성원 그룹)이 사이트를 커뮤니티 관리자로 경험하도록 하려면 미리 입력 검색을 사용하고 드롭다운의 옵션에서 구성원 또는 그룹 이름을 선택합니다.

예를 들어

* 유형 `q`
* Select Quinn Harper

>[!NOTE]
>
>[터널 서비스](https://helpx.adobe.com/experience-manager/6-3/help/communities/deploy-communities.html#tunnel-service-on-author) 게시 환경에만 존재하는 구성원 및 그룹을 선택할 수 있습니다.

![새 사이트의 사용자 역할](assets/site-admin-1.png)

#### 중재 {#moderation}

에 대한 기본 전역 설정 적용 [중재](/help/communities/sites-console.md#moderation) 사용자 생성 컨텐츠(UGC).

![중재](assets/moderation1.png)

#### 분석 {#analytics}

Adobe Analytics에 라이센스가 부여되고 Analytics 클라우드 서비스 및 프레임워크가 구성된 경우 Analytics를 활성화하고 프레임워크를 선택할 수 있습니다.

다음을 참조하십시오 [커뮤니티 기능에 대한 Analytics 구성](/help/communities/analytics.md).

![분석](assets/analytics.png)

#### 번역 {#translation}

다음 [번역 설정](/help/communities/sites-console.md#translation) 사이트의 기본 언어와 UGC를 번역할 수 있는지 여부와 언어(있는 경우)를 지정합니다.

* 확인 **기계 번역 허용**
* 기본 기계 번역 서비스로 번역을 위해 선택한 기본 언어 유지
* 기본 번역 제공업체 및 구성 남기기
* 언어 사본이 없기 때문에 글로벌 스토어가 필요하지 않습니다
* 선택 **전체 페이지 번역**
* 기본 지속성 옵션 유지

![번역 설정](assets/translation-settings.png)

### 4단계: 커뮤니티 사이트 만들기 {#step-create-communities-site}

**만들기**&#x200B;를 선택합니다.

![create-site](assets/create-site2.png)

프로세스가 완료되면 새 사이트에 대한 폴더가 커뮤니티 - 사이트 콘솔에 표시됩니다.

![커뮤니티 콘솔](assets/communitiessitesconsole.png)

## 커뮤니티 사이트 게시 {#publish-the-community-site}

생성된 사이트는 새 사이트를 만들 수 있는 콘솔과 동일한 콘솔인 커뮤니티 - 사이트 콘솔에서 관리되어야 합니다.

커뮤니티 사이트의 폴더를 선택하여 연 후 사이트 아이콘을 마우스로 가리키면 다음 네 가지 작업 아이콘이 표시됩니다.

![siteactionicons-1](assets/siteactionicons-1.png)

네 번째 줄임표 아이콘(추가 작업)을 선택하면 사이트 내보내기 및 사이트 삭제 옵션이 표시됩니다.

![siteactionsnew-1](assets/siteactionsnew-1.png)

왼쪽에서 오른쪽으로 다음과 같이 표시됩니다.

* **사이트 열기**

   페이지 구성 요소를 추가 및/또는 구성하려면 연필 아이콘을 선택하여 작성자 편집 모드에서 커뮤니티 사이트를 엽니다

* **사이트 편집**

   속성 아이콘을 선택하여 커뮤니티 사이트를 열고 제목과 같은 속성을 수정하거나 테마를 변경합니다

* **게시 사이트**

   커뮤니티 사이트를 게시하려면 월드 아이콘을 선택합니다(예: 게시 서버가 로컬 컴퓨터에서 실행 중인 경우 기본적으로 localhost:4503으로).

* **사이트 내보내기**

   내보내기 아이콘을 선택하여 저장된 커뮤니티 사이트의 패키지를 생성합니다. [패키지 관리자](/help/sites-administering/package-manager.md) 다운로드되었습니다.
UGC는 사이트 패키지에 포함되지 않습니다.

* **사이트 삭제**

   내에서 커뮤니티 사이트를 삭제하려면 삭제 아이콘을 선택합니다 **[!UICONTROL 커뮤니티 > 사이트 콘솔]**. 이 작업은 UGC, 사용자 그룹, 에셋 및 데이터베이스 레코드와 같이 사이트와 관련된 모든 항목을 제거합니다.

![siteactions](assets/siteactions.png)

>[!NOTE]
>
>게시 인스턴스에 기본 포트 4503을 사용하지 않는 경우 기본 복제 에이전트를 편집하여 포트 번호를 올바른 값으로 설정합니다.
>
>작성자 인스턴스의 기본 메뉴에서:
>
>1. 다음으로 이동 **[!UICONTROL 도구]** > **[!UICONTROL 작업]** > **[!UICONTROL 복제]** 메뉴 아래의 제품에서 사용할 수 있습니다.
>1. 선택 **[!UICONTROL 작성자의 에이전트]**.
>1. 선택 **[!UICONTROL 기본 에이전트(게시)]**.
>1. 다음 **[!UICONTROL 설정]**, 선택 **[!UICONTROL 편집]**.
>1. [에이전트 설정]의 팝업 대화 상자에서 다음을 선택합니다 **[!UICONTROL 전송]** 탭.
>1. URI에서 포트 번호 4503을 원하는 포트 번호로 변경합니다. 예를 들어 포트 6103을 사용하려면 https://localhost:6103/bin/receive?sling:authRequestLogin=1 을 따르십시오.
>1. 선택 **[!UICONTROL 확인]**.
>1. (선택 사항) 선택 **[!UICONTROL 지우기]** 또는 **[!UICONTROL 강제 다시 시도]** 복제 큐를 재설정합니다.


### 게시 선택 {#select-publish}

게시 서버가 실행 중인지 확인한 후 커뮤니티 사이트를 게시할 세상 아이콘을 선택합니다.

![publish-site](assets/publish-site.png)

커뮤니티 사이트가 성공적으로 게시되면 &#39;사이트가 게시됨&#39;이라는 메시지가 짧게 표시됩니다.

### 새 커뮤니티 사용자 그룹 {#new-community-user-groups}

새 커뮤니티 사이트와 함께 다양한 관리 기능에 대해 적절한 권한이 설정된 새 사용자 그룹이 만들어집니다. 자세한 내용은 다음을 참조하십시오. [커뮤니티 사이트에 대한 사용자 그룹](/help/communities/users.md#usergroupsforcommunitysites).

이 새 커뮤니티 사이트의 경우 1단계에서 사이트 이름이 &quot;참여&quot;인 경우 4개의 새 사용자 그룹은 [그룹 콘솔](/help/communities/members.md) (전역 탐색: 커뮤니티, 그룹):

* 커뮤니티 참여 커뮤니티 관리자
* 커뮤니티 참여 그룹 관리자
* 커뮤니티 참여 구성원
* 커뮤니티 참여 중재자
* 커뮤니티 참여 권한이 있는 구성원
* 커뮤니티 참여 사이트 콘텐츠 관리자

참고: [애런 맥도널드](/help/communities/tutorials.md#demo-users) 의 멤버임

* 커뮤니티 참여 커뮤니티 관리자
* 커뮤니티 참여 중재자
* 커뮤니티 참여 구성원(간접적으로 중재자 그룹의 구성원으로 사용)

![사용자 그룹](assets/user-group.png)

#### https://localhost:4503/content/sites/engage/en.html {#http-localhost-content-sites-engage-en-html}

![참여](assets/engage.png)

## 인증 오류 구성 {#configure-for-authentication-error}

사이트가 구성되어 게시로 푸시되면 [로그인 매핑 구성](/help/communities/sites-console.md#configure-for-authentication-error) ( `Adobe Granite Login Selector Authentication Handler`)을 클릭하여 게시합니다. 로그인 자격 증명을 올바르게 입력하지 않으면 인증 오류로 인해 커뮤니티 사이트의 로그인 페이지가 오류 메시지와 함께 다시 표시된다는 이점이 있습니다.

추가 `Login Page Mapping` 다음으로:

* `/content/sites/engage/en/signin:/content/sites/engage/en`

## 선택적 단계 {#optional-steps}

### 기본 홈 페이지 변경 {#change-the-default-home-page}

데모 목적으로 게시 사이트로 작업할 때 기본 홈 페이지를 새 사이트로 변경하는 것이 유용할 수 있습니다.

이렇게 하려면 를 사용해야 합니다. [CRXDE](https://localhost:4503/crx/de) 를 편집하려면 라이트 [리소스 매핑](/help/sites-deploying/resource-mapping.md) 게시의 테이블입니다.

시작하려면:

1. 게시 인스턴스에서 관리자 권한으로 로그인합니다.
1. 다음으로 이동 [https://localhost:4503/crx/de](https://localhost:4503/crx/de).
1. 프로젝트 브라우저에서 `/etc/map.`
1. 다음 항목 선택 `http` 노드:

   * 선택 **노드 만들기:**

      * **이름** localhost.4503 (do *아님* &#39;:&#39; 사용)

      * **유형** [sling:매핑](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)

1. 새로 만든 경우 `localhost.4503` 선택한 노드:

   * 속성 추가:

   * **이름** sling:match
      * **유형** 문자열
      * **값** localhost.4503/$(&#39;$&#39; 문자로 끝나야 함)
   * 속성 추가:

      * **이름** sling:internalRedirect
      * **유형** 문자열
      * **값** /content/sites/engage/en.html


1. 선택 **모두 저장.**
1. (선택 사항) 검색 기록을 삭제합니다.
1. https://localhost:4503/으로 이동합니다.

   * https://localhost:4503/content/sites/engage/en.html에 도착

>[!NOTE]
>
>비활성화하려면 접두사로 을 사용합니다. `sling:match` &#39;x&#39;가 있는 속성 값 - `xlocalhost.4503/$` - 및 **모두 저장**.

![옵션 단계](assets/optional-steps.png)

#### 문제 해결: 맵을 저장하는 동안 오류 발생 {#troubleshooting-error-saving-map}

변경 사항을 저장할 수 없는 경우 노드 이름이 `localhost.4503`, &#39;점&#39; 구분 기호 포함, 아님 `localhost:4503` 와 같이 &#39;콜론&#39; 구분 기호 사용 `localhost`은(는) 유효한 네임스페이스 접두사가 아닙니다.

![오류 메시지](assets/error-message.png)

#### 문제 해결: 리디렉션 실패 {#troubleshooting-fail-to-redirect}

&#39;**$**&#x200B;정규 표현식의 끝에 있는 &#39; `sling:match`문자열이 중요하므로 `https://localhost:4503/` 가 매핑되거나, URL의 server:port 뒤에 있을 수 있는 모든 경로에 리디렉션 값이 접두사로 추가됩니다. 따라서 AEM에서 로그인 페이지로 리디렉션하려고 하면 실패합니다.

### 사이트 수정 {#modify-the-site}

사이트가 처음 만들어진 후 작성자는 [사이트 열기 아이콘](/help/communities/sites-console.md#authoring-site-content) 를 사용하여 표준 AEM 작성 활동을 수행할 수 있습니다.

또한 관리자는 [사이트 편집 아이콘](/help/communities/sites-console.md#modifying-site-properties) 을 클릭하여 제목과 같은 사이트의 속성을 수정합니다.

수정 사항이 있으면 다음을 잊지 마십시오. **저장** 및 재방문&#x200B;**게시** 사이트.

>[!NOTE]
>
>AEM에 익숙하지 않은 경우 [기본 처리](/help/sites-authoring/basic-handling.md) 및 a [페이지 작성에 대한 빠른 안내](/help/sites-authoring/qg-page-authoring.md).
