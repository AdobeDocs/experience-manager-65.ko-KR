---
title: 커뮤니티 사이트 작성자
description: Adobe Experience Manager Communities 사이트를 작성하는 방법을 알아봅니다.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: d4c1895f-421c-4146-b94a-8d11065ef9e3
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1556'
ht-degree: 0%

---

# 커뮤니티 사이트 작성자{#author-a-new-community-site}

## 커뮤니티 사이트 만들기 {#create-a-community-site}

작성자 인스턴스를 사용하여 커뮤니티 사이트를 만듭니다. AEM 작성자 인스턴스에서 다음을 수행합니다.

1. 관리자 권한으로 로그인합니다.
1. 전역 탐색에서 **[!UICONTROL 커뮤니티]** > **[!UICONTROL 사이트]**(으)로 이동합니다.

커뮤니티 사이트 콘솔은 커뮤니티 사이트를 만드는 단계를 안내하는 마법사를 제공합니다. 마지막 단계에서 사이트를 커밋하기 전에 `Next` 단계 또는 `Back` 이전 단계로 이동할 수 있습니다.

커뮤니티 사이트를 만들려면 다음 작업을 수행하십시오.

* `Create` 단추를 선택하십시오.

![createcommunitysite](assets/createcommunitysite.png)

### 1단계: 사이트 템플릿 {#step-site-template}

사이트를 만들 ![템플릿](assets/create-site.png)

[사이트 템플릿 단계](/help/communities/sites-console.md#step2013asitetemplate)에서 제목, 설명, URL 이름을 입력하고 커뮤니티 사이트 템플릿을 선택합니다. 예를 들면 다음과 같습니다.

* **커뮤니티 사이트 제목**: `Getting Started Tutorial`
* **커뮤니티 사이트 설명**: `A site for engaging with the community.`
* **커뮤니티 사이트 루트**: (기본 루트 `/content/sites`에 대해 공백으로 남김)
* **클라우드 구성**: (클라우드 구성이 지정되지 않은 경우 공백으로 남김) 지정된 클라우드 구성의 경로를 제공합니다.
* **커뮤니티 사이트 기본 언어**: (단일 언어는 그대로 두기: 영어) 드롭다운 목록을 사용하여 사용 가능한 언어(독일어, 이탈리아어, 프랑스어, 일본어, 스페인어, 포르투갈어(브라질), 중국어(번체) 및 중국어(간체))에서 *개 이상의 기본 언어를 선택하십시오.* 추가된 언어마다 하나의 커뮤니티 사이트가 만들어지며 [다국어 사이트를 위한 콘텐츠 번역](/help/sites-administering/translation.md)에 설명된 모범 사례에 따라 동일한 사이트 폴더 내에 존재합니다. 각 사이트의 루트 페이지에는 선택한 언어 중 하나의 언어 코드로 이름이 지정된 하위 페이지(예: 영어의 경우 &#39;en&#39;, 프랑스어의 경우 &#39;fr&#39;)가 포함되어 있습니다.

* **커뮤니티 사이트 이름**: 참여

   * 사이트를 만든 후에는 쉽게 변경되지 않으므로 이름을 다시 확인하십시오
   * 커뮤니티 사이트 이름 아래에 초기 URL이 표시됩니다
   * 유효한 URL을 보려면 기본 언어 코드 + &quot;.html&quot;을 추가하십시오.
   * *예:*, https://localhost:4502/content/sites/ `engage/en.html`

* **템플릿**: 아래로 끌어다 놓아 `Reference Site` 선택

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

설정 단계에서 `Next`을(를) 선택하기 전에 사용자 관리, 태그 지정, 중재, 그룹 관리, 분석 및 번역과 관련된 구성에 대한 액세스를 제공하는 7개의 섹션이 있습니다.

#### 사용자 관리 {#user-management}

[사용자 관리](/help/communities/sites-console.md#user-management)에 대한 모든 확인란 선택

* 사이트 방문자가 자가 자가 등록할 수 있도록 하려면
* 로그인 없이 사이트 방문자가 사이트를 볼 수 있도록 하려면
* 구성원이 다른 커뮤니티 구성원의 메시지를 보내고 받을 수 있도록 허용
* 프로필을 등록하고 만드는 대신 Facebook으로 로그인할 수 있도록 허용
* 프로필을 등록하고 만드는 대신 Twitter으로 로그인을 허용하려면

>[!NOTE]
>
>프로덕션 환경의 경우 사용자 지정 Facebook 및 Twitter 애플리케이션을 만들어야 합니다. [Facebook 및 Twitter을 사용한 소셜 로그인](/help/communities/social-login.md)을 참조하세요.

![커뮤니티 사이트 설정](assets/site-settings.png)

#### 태깅 {#tagging}

커뮤니티 콘텐츠에 적용되는 태그는 이전에 [태그 지정 콘솔](/help/sites-administering/tags.md#tagging-console)을 통해 정의된 AEM 네임스페이스(예: [자습서 네임스페이스](/help/communities/setup.md#create-tutorial-tags))를 선택하여 제어합니다.

형식 사전 검색을 사용하면 네임스페이스를 쉽게 찾을 수 있습니다. 예:

* 유형 `tut`
* `Tutorial` 선택

![태그 지정](assets/tagging.png)

#### 역할 {#roles}

[커뮤니티 구성원 역할](/help/communities/users.md)이 역할 섹션의 설정을 통해 할당됩니다.

커뮤니티 구성원(또는 구성원 그룹)이 사이트를 커뮤니티 관리자로 경험하도록 하려면 미리 입력 검색을 사용하고 드롭다운의 옵션에서 구성원 또는 그룹 이름을 선택합니다.

예:

* 유형 `q`
* Select Quinn Harper

>[!NOTE]
>
>[터널 서비스](https://helpx.adobe.com/kr/experience-manager/6-3/help/communities/deploy-communities.html#tunnel-service-on-author)에서는 게시 환경에만 있는 구성원 및 그룹을 선택할 수 있습니다.

새 사이트의 ![사용자 역할](assets/site-admin-1.png)

#### 중재 {#moderation}

[사용자 생성 콘텐츠(UGC)를 중재](/help/communities/sites-console.md#moderation)하기 위한 기본 전역 설정을 사용합니다.

![중재](assets/moderation1.png)

#### 분석 {#analytics}

Adobe Analytics에 라이센스가 부여되고 Analytics Cloud 서비스 및 프레임워크가 구성된 경우 Analytics를 활성화하고 프레임워크를 선택할 수 있습니다.

[커뮤니티 기능에 대한 Analytics 구성](/help/communities/analytics.md)을 참조하세요.

![analytics](assets/analytics.png)

#### 번역 {#translation}

[번역 설정](/help/communities/sites-console.md#translation)은(는) 사이트의 기본 언어와 UGC를 번역할 수 있는지 여부 및 있는 경우 해당 언어로 번역할 수 있는지 여부를 지정합니다.

* **기계 번역 허용** 확인
* 기본 기계 번역 서비스로 번역을 위해 선택한 기본 언어 유지
* 기본 번역 제공업체 및 구성 남기기
* 언어 사본이 없기 때문에 글로벌 스토어가 필요하지 않습니다
* **전체 페이지 번역** 선택
* 기본 지속성 옵션 유지

![번역 설정](assets/translation-settings.png)

### 4단계: 커뮤니티 사이트 만들기 {#step-create-communities-site}

**만들기.** 선택

![사이트 만들기](assets/create-site2.png)

프로세스가 완료되면 새 사이트에 대한 폴더가 커뮤니티 - 사이트 콘솔에 표시됩니다.

![커뮤니티 사이트 콘솔](assets/communitiessitesconsole.png)

## 커뮤니티 사이트 Publish {#publish-the-community-site}

생성된 사이트는 새 사이트를 만들 수 있는 콘솔과 동일한 콘솔인 커뮤니티 - 사이트 콘솔에서 관리되어야 합니다.

커뮤니티 사이트의 폴더를 선택하여 연 후 사이트 아이콘을 마우스로 가리키면 다음 네 가지 작업 아이콘이 표시됩니다.

![siteactionicons-1](assets/siteactionicons-1.png)

네 번째 줄임표 아이콘(추가 작업)을 선택하면 사이트 내보내기 및 사이트 삭제 옵션이 표시됩니다.

![siteactionsnew-1](assets/siteactionsnew-1.png)

왼쪽에서 오른쪽으로 다음과 같이 표시됩니다.

* **사이트 열기**

  연필 아이콘을 선택하면 페이지 구성 요소를 추가하거나 구성할 수 있는 작성자 편집 모드로 커뮤니티 사이트가 열립니다.

* **사이트 편집**

  속성 아이콘을 선택하면 제목이나 테마 변경 등의 속성을 수정할 수 있는 커뮤니티 사이트가 열립니다.

* **Publish 사이트**

  world 아이콘을 선택하면 커뮤니티 사이트가 게시됩니다(예: 게시 서버가 로컬 컴퓨터에서 실행 중인 경우 기본적으로 localhost:4503으로).

* **사이트 내보내기**

  내보내기 아이콘을 선택하면 [패키지 관리자](/help/sites-administering/package-manager.md)에 저장되고 다운로드된 커뮤니티 사이트의 패키지가 만들어집니다. UGC는 사이트 패키지에 포함되어 있지 않습니다.

* **사이트 삭제**

  삭제 아이콘을 선택하면 **[!UICONTROL 커뮤니티 > 사이트 콘솔]** 내에서 커뮤니티 사이트가 삭제됩니다. 이 작업은 UGC, 사용자 그룹, 에셋 및 데이터베이스 레코드와 같이 사이트와 관련된 모든 항목을 제거합니다.

![siteactions](assets/siteactions.png)

>[!NOTE]
>
>게시 인스턴스에 기본 포트 4503을 사용하지 않는 경우 기본 복제 에이전트를 편집하여 포트 번호를 올바른 값으로 설정합니다.
>
>작성자 인스턴스의 기본 메뉴에서:
>
>1. **[!UICONTROL 도구]** > **[!UICONTROL 작업]** > **[!UICONTROL 복제]** 메뉴로 이동합니다.
>1. **[!UICONTROL 작성자의 에이전트]**&#x200B;을(를) 선택하십시오.
>1. **[!UICONTROL 기본 에이전트(게시)]**&#x200B;을 선택합니다.
>1. **[!UICONTROL 설정]** 옆에 있는 **[!UICONTROL 편집]**&#x200B;을 선택하세요.
>1. 에이전트 설정 팝업 대화 상자에서 **[!UICONTROL 전송]** 탭을 선택합니다.
>1. URI에서 포트 번호 4503을 원하는 포트 번호로 변경합니다. 예를 들어 포트 6103을 사용하려면 https://localhost:6103/bin/receive?sling:authRequestLogin=1 을 따르십시오.
>1. **[!UICONTROL 확인]**&#x200B;을 선택합니다.
>1. (선택 사항) 복제 큐를 재설정하려면 **[!UICONTROL 지우기]** 또는 **[!UICONTROL 다시 시도 강제]**&#x200B;를 선택하십시오.

### Publish 선택 {#select-publish}

게시 서버가 실행 중인지 확인한 후 커뮤니티 사이트를 게시할 세상 아이콘을 선택합니다.

![publish-site](assets/publish-site.png)

커뮤니티 사이트가 성공적으로 게시되면 &#39;사이트가 게시됨&#39;이라는 메시지가 짧게 표시됩니다.

### 새 커뮤니티 사용자 그룹 {#new-community-user-groups}

새 커뮤니티 사이트와 함께 다양한 관리 기능에 대해 적절한 권한이 설정된 새 사용자 그룹이 만들어집니다. 자세한 내용은 [커뮤니티 사이트의 사용자 그룹](/help/communities/users.md#usergroupsforcommunitysites)을 참조하세요.

이 새 커뮤니티 사이트의 경우 1단계에서 사이트 이름이 &quot;참여&quot;이면 [그룹 콘솔](/help/communities/members.md)에서 4개의 새 사용자 그룹을 볼 수 있습니다(전역 탐색: 커뮤니티, 그룹).

* 커뮤니티 참여 커뮤니티 관리자
* 커뮤니티 참여 그룹 관리자
* 커뮤니티 참여 구성원
* 커뮤니티 참여 중재자
* 커뮤니티 참여 권한이 있는 구성원
* 커뮤니티 참여 사이트 콘텐츠 관리자

[Aaron McDonald](/help/communities/tutorials.md#demo-users)은(는) 회원입니다.

* 커뮤니티 참여 커뮤니티 관리자
* 커뮤니티 참여 중재자
* 커뮤니티 참여 구성원(간접적으로 중재자 그룹의 구성원으로 사용)

![사용자 그룹](assets/user-group.png)

#### https://localhost:4503/content/sites/engage/en.html {#http-localhost-content-sites-engage-en-html}

![참여](assets/engage.png)

## 인증 오류 구성 {#configure-for-authentication-error}

사이트가 구성되어 게시되도록 푸시되면 게시 인스턴스에서 [매핑에서 로그를 구성](/help/communities/sites-console.md#configure-for-authentication-error)(`Adobe Granite Login Selector Authentication Handler`)합니다. 로그인 자격 증명을 올바르게 입력하지 않으면 인증 오류로 인해 커뮤니티 사이트의 로그인 페이지가 오류 메시지와 함께 다시 표시된다는 이점이 있습니다.

`Login Page Mapping`을(를) (으)로 추가

* `/content/sites/engage/en/signin:/content/sites/engage/en`

## 선택적 단계 {#optional-steps}

### 기본 홈 페이지 변경 {#change-the-default-home-page}

데모 목적으로 게시 사이트로 작업할 때 기본 홈 페이지를 새 사이트로 변경하는 것이 유용할 수 있습니다.

이렇게 하려면 [CRXDE](https://localhost:4503/crx/de) Lite를 사용하여 게시에서 [리소스 매핑](/help/sites-deploying/resource-mapping.md) 테이블을 편집해야 합니다.

시작하려면:

1. 게시 인스턴스에서 관리자 권한으로 로그인합니다.
1. [https://localhost:4503/crx/de](https://localhost:4503/crx/de)(으)로 이동합니다.
1. 프로젝트 브라우저에서 `/etc/map.`을(를) 확장합니다
1. `http` 노드 선택:

   * **노드 만들기:** 선택

      * **이름** localhost.4503
(*not* 사용 안 함: &#39;:&#39;)

      * **유형** [sling:매핑](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)

1. 새로 만든 `localhost.4503` 노드가 선택된 경우:

   * 속성 추가:

   * **이름** sling:match
      * **유형** 문자열
      * **값** localhost.4503/$
(&#39;$&#39; 문자로 끝나야 함)

   * 속성 추가:

      * **이름** sling:internalRedirect
      * **유형** 문자열
      * **값** /content/sites/engage/en.html

1. **모두 저장** 선택
1. (선택 사항) 검색 기록을 삭제합니다.
1. https://localhost:4503/으로 이동합니다.

   * https://localhost:4503/content/sites/engage/en.html에 도착

>[!NOTE]
>
>비활성화하려면 `sling:match` 속성 값의 접두사로 &#39;x&#39; - `xlocalhost.4503/$` - 및 **모두 저장**&#x200B;을 사용합니다.

![선택적 단계](assets/optional-steps.png)

#### 문제 해결: 맵을 저장하는 동안 오류 발생 {#troubleshooting-error-saving-map}

변경 내용을 저장할 수 없는 경우 `localhost`은(는) 올바른 네임스페이스 접두사가 아니므로 노드 이름이 `localhost.4503`에 &#39;점&#39; 구분 기호를 사용하고 `localhost:4503`에 &#39;콜론&#39; 구분 기호를 사용하지 않아야 합니다.

![오류 메시지](assets/error-message.png)

#### 문제 해결: 리디렉션 실패 {#troubleshooting-fail-to-redirect}

정규식 `sling:match`문자열의 끝에 있는 &#39;**$**&#39;이(가) 중요하므로 `https://localhost:4503/`만 매핑됩니다. 그렇지 않으면 리디렉션 값이 URL의 server:port 뒤에 있을 수 있는 모든 경로에 접두사로 추가됩니다. 따라서 AEM에서 로그인 페이지로 리디렉션하려고 하면 실패합니다.

### 사이트 수정 {#modify-the-site}

처음 사이트를 만든 후 작성자는 [사이트 열기 아이콘](/help/communities/sites-console.md#authoring-site-content)을 사용하여 표준 AEM 제작 활동을 수행할 수 있습니다.

또한 관리자는 [사이트 편집 아이콘](/help/communities/sites-console.md#modifying-site-properties)을 사용하여 제목과 같은 사이트 속성을 수정할 수 있습니다.

수정한 후에는 사이트를 **저장**&#x200B;하고 다시 **Publish**&#x200B;하세요.

>[!NOTE]
>
>AEM에 익숙하지 않은 경우 [기본 처리](/help/sites-authoring/basic-handling.md)에 대한 설명서와 [페이지 작성에 대한 빠른 안내서](/help/sites-authoring/qg-page-authoring.md)를 참조하세요.
