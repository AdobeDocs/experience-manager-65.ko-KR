---
title: 활성화를 위한 새 커뮤니티 사이트 작성
seo-title: 활성화를 위한 새 커뮤니티 사이트 작성
description: 활성화를 위한 커뮤니티 사이트 만들기
seo-description: 활성화를 위한 커뮤니티 사이트 만들기
uuid: a75fa566-a570-45fd-aabc-23651ef819cc
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: b9333558-6af9-46b2-9f03-3722645c69a6
docset: aem65
translation-type: tm+mt
source-git-commit: 85f3b8f2a5f079954f4907037c1c722a6b25fd91

---


# 활성화를 위한 새 커뮤니티 사이트 작성 {#author-a-new-community-site-for-enablement}

## 커뮤니티 사이트 만들기 {#create-community-site}

[커뮤니티 사이트 만들기는](/help/communities/sites-console.md) 커뮤니티 사이트를 만드는 단계를 안내하는 마법사를 사용합니다. 마지막 단계에서 사이트를 커밋하기 전에 `Next` 단계나 이전 단계로 이동할 `Back` 수 있습니다.

새 커뮤니티 사이트 만들기를 시작하려면 다음을 수행하십시오.

[작성자 인스턴스 사용](https://localhost:4502/)

* 관리자 권한으로 로그인
* 커뮤니티 > **[!UICONTROL 사이트로 이동]**

* **만들기**&#x200B;를 선택합니다

### 1단계:사이트 템플릿 {#step-site-template}

![활성 사이트 템플릿](assets/enablement-site-template.png)

사이트 **템플릿** 단계에서 제목, 설명, URL의 이름을 입력하고 커뮤니티 사이트 템플릿을 선택합니다.

* **커뮤니티 사이트 제목**: `Enablement Tutorial`

* **커뮤니티 사이트 설명**: `A site for enabling the community to learn.`

* **커뮤니티 사이트 루트**:(기본 루트에 대해서는 비워 `/content/sites`둡니다.

* **클라우드 구성**:(클라우드 구성이 지정되지 않은 경우 비워 두십시오) 지정된 클라우드 구성에 대한 경로를 제공합니다.
* **커뮤니티 사이트 기본 언어**:(단일 언어 사용에 대한 제한 없음):영어) 드롭다운을 사용하여 독일어, 이탈리아어, 프랑스어, 일본어, 스페인어, 포르투갈어(브라질), 중국어(번체) 및 중국어(간체) 등 사용 가능한 언어에서 하나 *이상의* 기본 언어를 선택합니다. 추가된 각 언어에 대해 하나의 커뮤니티 사이트가 만들어지며, 다국어 사이트에 대한 컨텐츠 번역에서 설명한 우수 사례 다음에 동일한 사이트 [폴더에 존재합니다](/help/sites-administering/translation.md). 각 사이트의 루트 페이지에는 선택한 언어 중 하나의 언어 코드에 의해 이름이 지정된 하위 페이지가 포함됩니다(예: 영어의 경우 &#39;en&#39;, 프랑스어의 경우 &#39;fr&#39;).

* **커뮤니티 사이트 이름**: `enable`

   * 초기 URL이 커뮤니티 사이트 이름 아래에 표시됩니다.
   * 유효한 URL의 경우 기본 언어 코드 + &quot;.html&quot;을 추가합니다.
      *예*: https://localhost:4502/content/sites/ `enable/en.html`

* **참조 사이트 템플릿**:아래로 이동하여 선택 `Reference Structured Learning Site Template`

**다음**&#x200B;을 선택합니다

### 2단계:디자인 {#step-design}

디자인 단계는 테마와 브랜딩 배너를 선택하기 위한 두 가지 섹션으로 구성되어 있습니다.

#### COMMUNITY SITE THEME {#community-site-theme}

템플릿에 적용할 스타일을 선택합니다. 이 옵션을 선택하면 테마가 확인 표시로 겹쳐 표시됩니다.

#### COMMUNITY SITE BRANDING {#community-site-branding}

(선택 사항) 배너 이미지를 업로드하여 사이트 페이지에 표시합니다. 배너는 커뮤니티 사이트 헤더와 메뉴(탐색 링크) 사이의 브라우저의 왼쪽 가장자리에 고정됩니다. 배너 높이는 120픽셀로 잘립니다. 브라우저의 너비와 120픽셀 높이에 맞게 배너의 크기를 조정할 수 없습니다.

![chlimage_1-2](assets/chlimage_1-2.png) chlimage_ ![1](assets/chlimage_1.jpeg)

**다음**&#x200B;을 선택합니다.

### 3단계:설정 {#step-settings}

설정 단계에서는 선택하기 전에 사용자 관리, 태깅, 역할, 중재, 분석, 번역 및 활성화와 관련된 구성에 대한 액세스를 제공하는 7개의 섹션이 `Next`있습니다.

#### USER MANAGEMENT {#user-management}

활성화 [커뮤니티는](/help/communities/overview.md#enablement-community) 비공개로 설정하는 것이 좋습니다.

커뮤니티 사이트는 익명의 사이트 방문자가 액세스가 거부되면 비공개로 설정되며, 자체 등록을 할 수 없으며, 소셜 로그인을 사용할 수 없습니다.

사용자 관리에 대해 대부분의 확인란이 선택 [해제되어 있는지 확인합니다](/help/communities/sites-console.md#user-management) .

* 사이트 방문자가 직접 등록할 수 없도록 허용 안 함
* 익명 사이트 방문자가 사이트를 보도록 허용 안 함
* 커뮤니티 구성원 간의 메시지 허용 여부(선택 사항)
* Facebook 로그인 허용 안 함
* Twitter에 로그인 허용 안 함

![chlimage_1-3](assets/chlimage_1-3.png)

#### TAGGING {#tagging}

커뮤니티 컨텐츠에 적용할 수 있는 태그는 이전에 Tagging Console(예: Tutorial 네임스페이스)을 통해 정의된 [AEM](/help/sites-administering/tags.md#tagging-console) 네임스페이스를 선택하여 [제어합니다](/help/communities/enablement-setup.md#create-tutorial-tags).

또한 커뮤니티 사이트에 대해 태그 네임스페이스를 선택하면 카탈로그 및 지원 리소스를 정의할 때 표시되는 선택이 제한됩니다. 중요한 [정보는 태깅](/help/communities/tag-resources.md) 지원 리소스를 참조하십시오.

사전 입력 검색을 사용하면 네임스페이스를 손쉽게 찾을 수 있습니다. 예,

* 유형 `tut`
* 선택 `Tutorial`

![chlimage_1-4](assets/chlimage_1-4.png)

### ROLES {#roles}

[커뮤니티 구성원 역할은](/help/communities/users.md) 역할 섹션의 설정을 통해 할당됩니다.

커뮤니티 구성원(또는 구성원 그룹)이 사이트를 커뮤니티 관리자로 경험하도록 하려면 미리 유형 검색을 사용하고 드롭다운의 옵션에서 구성원 또는 그룹 이름을 선택합니다.

예,

* 유형 `q`
* 퀸 [하퍼 선택](/help/communities/enablement-setup.md#publishcreateenablementmembers)

>[!NOTE]
>
>[터널 서비스를](/help/communities/deploy-communities.md#tunnel-service-on-author) 사용하면 게시 환경에만 존재하는 구성원 및 그룹을 선택할 수 있습니다.

![역량 강화 역할](assets/site-admin.png)

#### MODERATION {#moderation}

사용자 생성 콘텐츠(UGC)를 [중재하기](/help/communities/sites-console.md#moderation) 위한 기본 전역 설정을 적용합니다.

![chlimage_1-5](assets/chlimage_1-5.png)

#### ANALYTICS {#analytics}

드롭다운에서 이 커뮤니티 사이트에 대해 구성된 Analytics 클라우드 서비스 프레임워크를 선택합니다.

스크린샷에 표시된 선택 `Communities`사항은 [구성 설명서의 프레임워크 예입니다.](/help/communities/analytics.md#aem-analytics-framework-configuration)

![chlimage_1-6](assets/chlimage_1-6.png)

#### TRANSLATION {#translation}

번역 [설정은](/help/communities/sites-console.md#translation) UGC를 변환할 수 있는지 여부와 변환할 수 있는 언어(있는 경우)를 지정합니다.

* 기계 **번역 허용 확인**
* 기본 설정 사용

![chlimage_1-7](assets/chlimage_1-7.png)

#### ENABLEMENT {#enablement}

활성 커뮤니티의 경우 하나 이상의 커뮤니티 활성 관리자를 식별해야 합니다.

* **활성 관리자**(필수) `Community Enablement Managers` 그룹의 구성원을 선택하여 이 커뮤니티 사이트를 관리할 수 있습니다.

   * 유형 `s`
   * 선택 `Sirius Nilson`

* **Marketing Cloud 조직** ID(선택 사항) 지원 보고에서 비디오 하트비트 [분석을 포함하는 데 필요한 Adobe Analytics 계정의](/help/communities/analytics.md#video-heartbeat-analytics) ID입니다.

![chlimage_1-8](assets/chlimage_1-8.png)

**다음**&#x200B;을 선택합니다.

### 4단계:커뮤니티 사이트 만들기 {#step-create-community-site}

**만들기**&#x200B;를 선택합니다.

![chlimage_1-9](assets/chlimage_1-9.png)

프로세스가 완료되면 커뮤니티 > 사이트 콘솔에 새 사이트의 폴더가 표시됩니다.

![활성 상태](assets/enablementsitecreated.png)

### 새 커뮤니티 사이트 게시 {#publish-the-new-community-site}

생성된 사이트는 새 사이트를 만들 수 있는 콘솔과 동일한 콘솔인 커뮤니티 - 사이트 콘솔에서 관리해야 합니다.

커뮤니티 사이트의 폴더를 선택한 후 사이트 아이콘 위로 마우스를 가져가면 4개의 작업 아이콘이 표시됩니다.

![siteactionicons](assets/siteactionicons.png)

줄임표 아이콘(추가 작업 아이콘)을 선택하면 사이트 내보내기 및 사이트 삭제 옵션이 표시됩니다.

![siteaction새](assets/siteactionsnew.png)

왼쪽에서 오른쪽으로 :

* **사이트 열기**

   연필 아이콘을 선택하여 작성 편집 모드에서 커뮤니티 사이트를 열고 페이지 구성 요소를 추가 및/또는 구성합니다.

* **사이트 편집**

   속성 아이콘을 선택하여 커뮤니티 사이트를 열어 제목과 같은 속성을 수정하거나 테마를 변경합니다

* **게시 사이트**

   커뮤니티 사이트를 게시할 세계 아이콘을 선택합니다(기본적으로 localhost:4503으로).

* **사이트 내보내기**

   내보내기 아이콘을 선택하여 [패키지 관리자에](/help/sites-administering/package-manager.md) 저장되고 다운로드된 커뮤니티 사이트 패키지를 만듭니다.
UGC는 사이트 패키지에 포함되지 않습니다.

* **사이트 삭제**

   커뮤니티 사이트를 삭제하려면 커뮤니티 사이트 콘솔의 사이트 위로 마우스를 가져가면 나타나는 사이트 삭제 아이콘을 선택합니다. 이 작업은 UGC, 사용자 그룹, 자산 및 데이터베이스 레코드 등 사이트와 연관된 모든 항목을 제거합니다.

![활성화](assets/enablesiteactions.png)

#### 게시{#select-publish}를 선택합니다 

커뮤니티 사이트를 게시할 세계 아이콘을 선택합니다.

![chlimage_1-10](assets/chlimage_1-10.png)

그 사이트가 게시되었다는 표시가 있을 것입니다.

![chlimage_1-11](assets/chlimage_1-11.png)

## 커뮤니티 사용자 및 사용자 그룹 {#community-users-user-groups}

### 새 커뮤니티 사용자 그룹 알림 {#notice-new-community-user-groups}

새 커뮤니티 사이트와 함께 다양한 관리 기능에 적합한 권한이 설정된 새 사용자 그룹이 만들어집니다. 자세한 내용은 커뮤니티 사이트의 [사용자 그룹을 참조하십시오](/help/communities/users.md#usergroupsforcommunitysites).

이 새 커뮤니티 사이트의 경우 1단계의 사이트 이름이 &quot;활성화&quot;인 경우 게시 환경에 있는 새 사용자 그룹이 커뮤니티 구성원 및 그룹 콘솔에서 [](/help/communities/members.md#groups-console) 볼 수 있습니다.

![chlimage_1-12](assets/chlimage_1-12.png)

### 커뮤니티 구성원 지정 구성원 그룹 활성화 {#assign-members-to-community-enable-members-group}

작성자의 경우, 터널 서비스가 활성화되어 있으면, 초기 설정 중에 만든 [사용자를 새로 만든 커뮤니티](/help/communities/enablement-setup.md#publishcreateenablementmembers) 사이트의 커뮤니티 구성원 그룹에 할당할 수 있습니다.

커뮤니티 그룹 콘솔을 사용하여 구성원을 개별적으로 추가하거나 그룹의 구성원을 통해 추가할 수 있습니다.

이 예에서 그룹은 `Community Ski Class` 구성원과 `Community Enable Members` 함께 그룹의 구성원으로 추가됩니다 `Quinn Harper`.

* 커뮤니티, **그룹 콘솔로** 이동
* 커뮤니티 *활성화 구성원* 그룹 선택
* 그룹에 구성원 추가 **검색 상자에 &#39;ski&#39;를** 입력합니다.
* 커뮤니티 *스키* 클래스 선택(수강생 그룹)
* 검색 상자에 &#39;퀸&#39;을 입력합니다.
* 퀸 *하퍼 선택* (지원 리소스 연락처)

* **저장**&#x200B;을 선택합니다

![chlimage_1-13](assets/chlimage_1-13.png)

## 게시 시 구성 {#configurations-on-publish}

`https://localhost:4503/content/sites/enable/en.html {#http-localhost-content-sites-enable-en-html}`

![chlimage_1-14](assets/chlimage_1-14.png)

### 인증 구성 오류 {#configure-for-authentication-error}

사이트를 구성하고 게시로 푸시하면 게시 인스턴스에 로그인 매핑 [(](/help/communities/sites-console.md#configure-for-authentication-error) )을 `Adobe Granite Login Selector Authentication Handler`구성합니다. 로그인 자격 증명을 올바르게 입력하지 않으면 인증 오류가 오류 메시지와 함께 커뮤니티 사이트의 로그인 페이지가 다시 표시됩니다.

다른 `Login Page Mapping` 이름으로 추가

* `/content/sites/enable/en/signin:/content/sites/enable/en`

### (선택 사항) 기본 홈 페이지 변경 {#optional-change-the-default-home-page}

데모를 위해 게시 사이트를 사용할 때 기본 홈 페이지를 새 사이트로 변경하는 것이 유용할 수 있습니다.

이렇게 하려면 CRX| [DE](https://localhost:4503/crx/de) Lite를 사용하여 [리소스 매핑](/help/sites-deploying/resource-mapping.md) 테이블을 게시하여 편집해야 합니다.

시작하려면

1. 게시 시 CRXDE에 액세스하고 관리자 권한으로 로그인

   * 예를 들어, https://localhost:4503/crx/de [으로](https://localhost:4503/crx/de) 이동하여 `admin/admin`

1. 프로젝트 브라우저에서 `/etc/map`
1. 노드 `http` 선택

   * 노드 **만들기 선택**

      * **이름** localhost.4503

         (&#39;:&#39;를 사용하지 *않음* )

      * **문자** 슬링: [매핑](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)

1. 새로 만든 `localhost.4503` 노드를 선택한 경우

   * 속성 추가

      * **이름** 슬링:일치
      * **문자열** 유형
      * **값** localhost.4503/$
   (&#39;$&#39; 문자로 끝나야 함)

   * 속성 추가

      * **이름** 슬링:internalRedirect
      * **문자열** 유형
      * **값** /content/sites/enable/en.html


1. 모두 **저장을 선택합니다.**
1. (선택 사항) 탐색 내역을 삭제합니다.
1. https://localhost:4503/으로 이동

   * https://localhost:4503/content/sites/enable/en.html에 도착

>[!NOTE]
>
>비활성화하려면 `sling:match` 속성 값을 &#39;x&#39; - `xlocalhost.4503/$` 및 [모두 저장]으로 미리 **패드하면 됩니다**.

![chlimage_1-15](assets/chlimage_1-15.png)

#### 문제 해결:맵 저장 중 오류 발생 {#troubleshooting-error-saving-map}

변경 내용을 저장할 수 없는 경우 노드 이름이 &#39;dot&#39; `localhost.4503`구분 문자로 &#39;colon&#39; 구분 기호가 아닌 `localhost:4503` 것으로 올바른 네임스페이스 접두사가 `localhost` 아닌지 확인하십시오.

![chlimage_1-16](assets/chlimage_1-16.png)

#### 문제 해결:리디렉션 실패 {#troubleshooting-fail-to-redirect}

정규 표현식&#x200B;**문자열 끝에 있는 &#39;**$ `sling:match``https://localhost:4503/` &#39;는 반드시 매핑되어야 하며, 그렇지 않은 경우 리디렉션 값이 URL의 server:port 다음에 있을 수 있는 모든 경로에 추가됩니다. 따라서 AEM이 로그인 페이지로 리디렉션하려고 하면 실패합니다.

## 커뮤니티 사이트 수정 {#modifying-the-community-site}

사이트를 처음 만든 후 작성자는 사이트 열기 아이콘을 사용하여 [표준 AEM 작성 활동을 수행할](/help/communities/sites-console.md#authoring-site-content) 수 있습니다.

또한 관리자는 사이트 편집 [아이콘을](/help/communities/sites-console.md#modifying-site-properties) 사용하여 사이트 속성(예: 제목)을 수정할 수 있습니다.

수정 후에는 사이트를 **저장하고** 다시&#x200B;**게시해야** 합니다.

>[!NOTE]
>
>AEM에 익숙하지 않은 경우 [기본 처리에](/help/sites-authoring/basic-handling.md) 대한 설명서와 페이지 [작성에 대한](/help/sites-authoring/qg-page-authoring.md)빠른 안내서를 봅니다.

### 카탈로그 추가 {#add-a-catalog}

이 커뮤니티 사이트에 대해 선택한 커뮤니티 사이트 템플릿에는 카탈로그 기능이 포함되어야 합니다.

그렇지 않으면 카탈로그 기능을 쉽게 추가할 수 있습니다. 이렇게 하면 역량 강화 리소스 또는 학습 경로에 할당되지 않은 다른 커뮤니티 구성원이 카탈로그에서 활성 리소스를 선택할 수 있습니다.

사이트 구조에 이미 카탈로그 기능이 포함되어 있는 경우 해당 제목을 변경할 수 있습니다.

사이트의 구조를 수정하려면 커뮤니티, 사이트 **콘솔로** 이동하여 `enable` 폴더를 연 다음 사이트 **편집** 아이콘을 선택하여 `Enablement Tutorial`사이트의속성에 액세스합니다.

[구조] 패널을 선택하여 카탈로그를 추가하거나 기존 카탈로그를 수정합니다.

* **제목**: `Ski Catalog`

* **URL**: `catalog`

* **모든 네임스페이스 선택**:기본값으로 두십시오.
* select **Save**

![chlimage_1-17](assets/chlimage_1-17.png)

위치 아이콘을 사용하여 카탈로그 함수를 할당 후 두 번째 위치로 이동합니다.

![chlimage_1-18](assets/chlimage_1-18.png)

오른쪽 **위** 모서리에서 저장을 선택하여 커뮤니티 사이트에 대한 변경 사항을 저장합니다.

그런 다음&#x200B;**사이트를** 다시 게시합니다.

