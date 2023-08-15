---
title: 관리 콘솔
seo-title: Moderation Console
description: 중재 콘솔에 액세스하는 방법
seo-description: How to access the Moderation console
uuid: d3b8a160-85b2-43f4-9891-5fafa8c48c5f
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 404582ab-bb4c-4775-9ae3-17356d376dca
docset: aem65
role: Admin
exl-id: 829da16a-4083-43c1-857d-f2666b363bfc
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '2041'
ht-degree: 4%

---

# 관리 콘솔 {#moderation-console}

AEM Communities에서 일괄 처리 [커뮤니티 콘텐츠 중재](/help/communities/moderate-ugc.md) 는 관리자 및 커뮤니티 중재자(중재자로 할당된 신뢰할 수 있는 커뮤니티 구성원)가 작성 및 게시 환경 모두에서 사용할 수 있습니다.

관리자 및 커뮤니티 중재자도 다음을 수행할 수 있습니다. [컨텍스트 내 중재](/help/communities/in-context.md) 게시 환경에 포함될 수 있습니다.

모든 기능 [커뮤니티 사이트](/help/communities/sites-console.md) 은(는) `Administration` 관리자 권한으로 로그인하는 사용자가 사용할 수 있는 메뉴 항목입니다. 다음 `Administration` 링크는 중재 콘솔에 대한 액세스를 제공합니다.

관리자 및 커뮤니티 중재자는 중재 콘솔에서, 중재 권한이 있는 모든 사용자 생성 콘텐츠(UGC)에 액세스할 수 있습니다. 여러 사이트를 중재하도록 허용된 경우 모든 사이트에서 게시물을 보거나 선택한 커뮤니티 사이트별로 필터링할 수 있습니다.

자세한 내용은 다음을 참조하십시오. [사용자 및 사용자 그룹 관리](/help/communities/users.md).

중재 콘솔은 다음을 지원합니다.

* 중재 작업을 일괄적으로 수행하고 있습니다.
* UGC를 검색하는 중입니다.
* UGC 세부 정보 보기.
* UGC 작성자 세부 사항 보기.

관리자 또는 을(를) 통해 구성원으로 로그인한 경우에만 ` [moderator permissions](/help/communities/in-context.md#identifyingtrustedmembers)`, 중재 작업이 수행될 수 있습니다.

## 게시 환경 액세스 {#publish-environment-access}

게시된 커뮤니티 사이트에서 중재 콘솔에 대한 액세스는 커뮤니티 중재자가 로그인할 때 표시되는 관리 링크를 통해 수행됩니다.

![publishweretail](assets/publishweretail.png)

관리 링크를 선택하면 중재 콘솔이 표시됩니다.

![moderation-console-publish](assets/moderation-console-publish.png)

## 작성 환경 액세스 {#author-environment-access}

작성 환경에서 중재 콘솔에 도달하려면

* 전역 탐색에서 을 선택합니다. **[!UICONTROL 커뮤니티]** > **[!UICONTROL 중재]**.

관리자로 로그인하거나 [중재자 권한](/help/communities/in-context.md#identifyingtrustedmembers), 중재 작업을 수행할 수 있습니다. 표시된 유일한 커뮤니티 콘텐츠는 로그인한 멤버가 중재할 수 있는 콘텐츠입니다.

>[!NOTE]
>
>게시 환경의 UGC는 선택한 SRP가 일반 저장소를 구현하는 경우에만 작성자에게 표시됩니다. 예를 들어 기본적으로 저장소는 JSRP이며, 이는 작성자 및 게시의 공통 저장소가 아닙니다. 다음을 참조하십시오 [커뮤니티 콘텐츠 저장소](/help/communities/working-with-srp.md).

![moderationconsoleauthor](assets/moderationconsoleauthor.png)

## 중재 콘솔 UI {#moderation-console-ui}

왼쪽 탐색 레일(작성자에게는 표시되지만 게시에는 표시되지 않음)을 제외하고 중재 UI에는 다음과 같은 기본 영역이 있습니다.

* **[상단 탐색 막대](#top-navigation-bar)**
* **[도구 모음](#toolbar)**
* **[콘텐츠 영역](#content-area)**

### 상단 탐색 막대 {#top-navigation-bar}

상단 탐색 막대는 모든 콘솔에 대해 일정합니다. 자세한 내용은 [기본 처리](/help/sites-authoring/basic-handling.md).

### 도구 모음 {#toolbar}

위쪽 탐색 모음 아래에 있는 도구 모음은 왼쪽에 다음과 같은 전환 스위치를 제공합니다.

* [레일 필터링](/help/communities/moderation.md#filterrail)
콘텐츠를 필터링할 속성을 선택할 수 있는 레일을 엽니다.

위쪽 탐색 모음 아래에 있는 도구 모음은 왼쪽에 다음과 같은 전환 스위치를 제공합니다.

![토글 스위치](assets/toggleswitch.png)

[레일 필터링](/help/communities/moderation.md#filterrail)
검색 선택 시 콘텐츠를 필터링할 속성을 선택할 수 있는 레일을 엽니다.

![필터레일](assets/filterrail.png)

### 컨텐츠 영역 {#content-area}

콘텐츠 영역에는 게시된 UGC에 대한 정보가 포함되어 있습니다.

* UGC 게시
* 멤버 이름
* 구성원 아바타
* 게시물 위치.
* 게시되었을 때입니다.
* 게시물에 대한 답글 수.
* [감정](/help/communities/moderate-ugc.md#sentiment) 게시물과 연결됨
* 승인되면 확인 표시가 표시됩니다.
* 첨부 파일이 있는 경우 페이퍼 클립이 표시됩니다.

>[!NOTE]
> 
>콘텐츠 영역은 *무한 스크롤*&#x200B;즉, 콘텐츠 끝에 도달할 때까지 스크롤을 계속할 수 있습니다. 도구 모음은 스크롤하는 동안에도 컨텐츠 영역 위에 고정되어 표시되는 위치에 유지됩니다.

### 레일 필터링 {#ootbfilters}

![open-filterrail](assets/open-filterrail.png)

사이드 패널 아이콘으로 필터 레일이 열립니다. 콘텐츠 영역 왼쪽에 표시되는 필터 레일은 콘텐츠 영역에 나타나는 참조된 UGC에 즉각적인 영향을 주는 서로 다른 필터를 제공합니다.

각 범주 내의 필터는 다음과 같습니다 **또는**&#x200B;을 함께 사용하며, 다른 카테고리의 필터는 다음과 같습니다. **및**&#x200B;같이.

예를 들어, 두 가지를 모두 선택하면 **질문** 및 **답변**, 다음 중 하나의 콘텐츠가 표시됩니다. **질문** *또는* an **답변**.

하지만 다음을 확인하면 **질문** 및 **보류 중**, 인 콘텐츠만 표시됩니다. **질문** 및 **보류 중**.

>[!NOTE]
>
>커뮤니티 중재자는 중재 콘솔 UI에 사전 정의된 필터를 책갈피로 지정할 수 있습니다. 이러한 필터가 URL 끝에 추가되므로(쿼리 문자열 매개 변수로) 중재자는 나중에 책갈피가 지정된 필터로 다시 돌아가서 이러한 링크도 공유할 수 있습니다.

![검색 아이콘](assets/searchicon.png)

필터 레일이 열리면 검색 아이콘이 사이드 패널이 닫힌 상태로 전환합니다. 그러나 필터 레일을 닫고 사용자가 생성한 컨텐츠만 보려면 검색 아이콘을 클릭하고 컨텐츠 전용 옵션을 선택합니다.

#### 컨텐츠 경로 {#content-path}

콘텐츠 경로 는 지정된 콘텐츠 저장소에 배치된 게시물에 표시되는 참조 UGC를 제한합니다.

![content-path](assets/content-path.png)

#### 텍스트 검색 {#text-search}

텍스트 검색은 표시된 참조된 UGC를 입력한 텍스트가 포함된 게시물로 제한합니다.

![텍스트 검색](assets/text-search.png)

#### Site {#site}

사이트는 선택한 커뮤니티 사이트에 게시하는 게시물에 표시되는 참조된 UGC를 제한합니다. 선택된 사이트가 없으면 UGC에 대한 모든 참조가 표시됩니다.

![사이트 패널](assets/site-panel.png)

>[!NOTE]
>
>관리자가 벌크 중재 콘솔에 액세스하면 로 작성되지 않은 사이트를 포함하여 UGC에 대한 모든 참조가 표시됩니다. [사이트 생성 마법사](/help/communities/sites-console.md)예: Geometrixx 샘플.
>
>신뢰할 수 있는 커뮤니티 회원이 게시할 때 벌크 중재 콘솔에 액세스하면 해당 회원이 중재하도록 승인된 커뮤니티 사이트에 대해 만든 UGC에 대한 참조만 표시되며 사이트 필터로 필터링될 수 있습니다.

#### 콘텐츠 유형 {#content-type}

콘텐츠 유형은 선택한 리소스 유형의 게시물에 표시되는 참조된 UGC를 제한합니다. 다음 유형 중 하나 이상을 선택할 수 있습니다. 선택하지 않으면 모든 유형이 표시됩니다.

* **댓글**
* **포럼 주제**
* **포럼 답글**
* **QnA 질문**
* **QnA 답변**
* **블로그 항목**
* **블로그 댓글**
* **달력 이벤트**
* **달력 댓글**
* **파일 라이브러리 폴더**
* **파일 라이브러리 문서**
* **아이디어**
* **관념화 댓글**

![content-types](assets/content-types.png)

#### 추가 콘텐츠 유형 {#additional-content-types}

필터링할 추가 리소스를 추가하려면 다음 작업을 수행하십시오.

* 작성자 인스턴스에 관리자로 로그인합니다.
* 열기 [웹 콘솔](https://localhost:4502/system/console/configMgr).
* 찾기 `AEM Communities Moderation Dashboard Filters`.
* 편집 모드에서 열 구성을 선택합니다.
* 필터링할 구성 요소의 ResourceType을 입력합니다.

   * 예를 들어 포함된 투표 구성 요소를 필터링하려면 다음을 입력합니다.

     `Voting=social/tally/components/hbs/voting`

  ![additional-contenttype](assets/additional-contenttype.png)

* 저장을 선택합니다.
* 커뮤니티 - 중재 콘솔을 새로 고칩니다.

그 결과 다음에 대한 새로운 선택 가능 필터가 `Voting` 다음 아래에 `Content Type` 필터 그룹.

해당 필터를 선택하면 대시보드 컨텐츠에 입력한 ResourceTypes와 일치하는 UGC가 표시됩니다.

#### 상태 {#status}

상태는 선택한 상태의 게시물에 표시되는 참조되는 UGC를 제한합니다. 이 게시물은 보류 중, 승인됨, 거부됨 또는 닫힘, 초안 또는 블로그 문서에 대해 예약됨, QnA 질문에 대해 답변됨 또는 답변되지 않음 중 하나 이상일 수 있습니다. 아무 것도 선택하지 않으면 모두 표시됩니다.

>[!NOTE]
>
>답변되지 않음 상태만 선택하면 중재자에게 답변된 질문을 제외한 모든 콘텐츠(모든 콘텐츠 유형에 대해)가 표시됩니다. 답변되지 않은 질문 및 포럼 주제, 블로그 기사 또는 댓글과 같은 기타 콘텐츠의 경우 답변된 질문에 대한 책임 재산이 존재하지 않기 때문입니다.

![상태](assets/statuses.png)

#### 플래그 지정 {#flagging}

플래그 지정은 플래그가 지정되거나 숨겨진 게시물에 표시되는 참조된 UGC를 제한합니다.

컨텐츠에 플래그가 지정된 후에는 다음 중 하나를 선택하여 해당 단일 컨텐츠에 플래그를 해제할 때까지 플래그가 지정된 상태로 유지됩니다. **플래그** 단추를 다시 한 번 클릭합니다. 중요 또는 후속 조치와 같은 플래그 지정 수준은 없습니다.

![플래그 지정](assets/flagging.png)

#### 구성원 {#members}

구성원은 입력한 구성원 이름이 게시한 UGC에 표시되는 참조된 UGC를 제한합니다.

![구성원](assets/members.png)

#### 마지막에 게시된 항목 {#posted-in-the-last}

게시됨 마지막 날짜에서 참조된 UGC는 마지막 시간, 일, 주, 월 또는 년에 작성된 게시물에 표시됩니다.

![posted-last](assets/posted-last.png)

#### 감정 {#sentiment}

[감정](/help/communities/moderate-ugc.md#sentiment) 양수, 음수 또는 중립의 감정 값이 있는 게시물에 표시되는 참조된 UGC를 제한합니다.

![감정](assets/sentiment.png)

## 사용자 정의 필터 {#custom-filters}

의 기본 제공 필터 제외 [레일 필터링](/help/communities/moderation.md#ootbfilters)를 통해 메타데이터에 대한 추가 사용자 정의 필터를 중재 UI에 추가할 수 있습니다. 개발자는 Github의 샘플 코드를 사용하여 기존 중재 UI 필터를 확장할 수 있습니다.

![custom-tag-filter](assets/custom-tag-filter.png)

다음 [샘플 프로젝트](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/main/aem-communities-moderation-filter) github에서 태그 필터를 구현하여 특정 태그가 사용자 생성 콘텐츠에 적용되는지 여부를 기반으로 UGC 목록을 필터링합니다. 샘플 코드를 따라 유사한 다른 UGC 메타데이터 필드에 대한 유사 필터를 빌드할 수 있습니다.

태그 필터용 샘플을 설치하려면:

1. AEM 작성자에서 패키지 관리자를 엽니다(`https://[aem-author]:4502/crx/packmgr/index.jsp`) 인스턴스 및 AEM 게시(`https://[aem-publish]:4503/crx/packmgr/index.jsp`) 인스턴스.
1. 패키지 빌드 `com.adobe.social.sample.moderation.filter.ui.apps-1.0-SNAPSHOT.zip` github 코드에서 를 참조하고 동일한 코드를 설치하고 활성화합니다.
1. AEM 작성자에서 번들 콘솔을 엽니다( `https://[aem-author]:4502/system/console/bundles`) 인스턴스 및 AEM 게시( `https://[aem-publish]:4503/system/console/bundles`) 인스턴스.
1. 패키지 빌드(`[com](https://sample-moderation-filter.com/).adobe.social.sample.moderation.filter.core-1.0-SNAPSHOT.jar`) Github에서 을 설치하고 활성화합니다.
1. 다음으로 이동 **/apps/social/moderation/facet** AEM 작성자의 노드(`https://[aem-author]:4502/crx/de/index.jsp#/apps/social/moderation/facets`) 및 AEM 게시(`https://[aem-publish]:4502/crx/de/index.jsp#/apps/social/moderation/facets`) 인스턴스.
1. 기술 사용자 추가 **communities-utility-reader** 포함 `jcr:read` 사용 권한.

기존 커뮤니티 사이트에 사용자 지정 필터를 노출하려면 다음을 수행하십시오.

1. 편집 `Clientlibs` / 기존 중재 페이지 `/content/we-retail/us/en/community/moderation/shell3/jcr:content/head/clientlibs.`

   * 새 범주 추가 `cq.social.hbs.moderation.v2.`

1. 다음으로 이동:`/content/we-retail/us/en/community/moderation/shell3/jcr:content/rails/searchWell/items/filters.`

   * 새 구성 요소로 설정 `sling:resourceType = social/moderation/v2/filters.`

1. `/content/we-retail/us/en/community/moderation/shell3/jcr:content/views/content/items/modcontainer`로 이동합니다.

   * 새 구성 요소로 설정 `sling:resourceType = social/moderation/v2/modcontainer`.

## 중재 작업 {#moderation-actions}

[중재 작업](/help/communities/moderate-ugc.md#moderation-actions) 콘텐츠 영역에서 선택한 하나 이상에 대해 수행하거나 콘텐츠 세부 정보를 볼 때 수행할 수 있습니다.

게시물을 일괄 중재하려면 컨텐츠 영역에서 선택 ( )을 클릭합니다.![선택성](assets/selecticon.png))을 클릭하여 마우스로 가리키거나(데스크탑) 게시물을 누른 상태에서 손가락을 누른 채 표시되는 게시물의 아이콘(모바일). 이렇게 하면 다중 선택 모드로 전환되고 이제 클릭하기만 하면 일괄 조정할 후속 게시물을 선택할 수 있습니다. 도구 모음에 표시된 버튼을 사용하여 선택한 게시물에 대한 중재 작업을 수행합니다. 모든 작업은 확인 메시지를 표시합니다.

콘텐츠 영역의 단일 게시물을 중재하려면 마우스로 가리키거나(데스크톱) 게시물에 단추가 나타나도록 게시물(모바일)을 누른 상태에서 손가락을 놓습니다. 단일 콘텐츠 세부 정보에서 작업할 때 삭제 작업에만 확인 메시지가 표시됩니다.

### 여러 게시물 중재 {#moderating-multiple-posts}

다음을 클릭하여 일괄 선택 모드로 들어갑니다. `Select` 게시물의 아이콘:

![select-icon](assets/select-icon.png)

일괄 선택 모드를 종료하려면 도구 모음에서 취소 (x) 아이콘을 선택합니다.

여러 게시물에서 수행할 수 있는 중재 작업은 다음과 같습니다.

* 거부
* 삭제
* 게시물 닫기/다시 열기

이러한 작업을 허용하는 아이콘은 여러 게시물을 선택한 경우에만 도구 모음에 표시됩니다.

![bulkmoderate](assets/bulkmoderate.png)

### 단일 게시물 중재 {#moderating-a-single-post}

단일 선택 모드에서 다음을 수행할 수 있습니다.

* 사용자 이름을 선택하여 사용자 세부 정보를 봅니다.
* 게시물에 대한 링크를 선택하여 컨텍스트 내에서 게시물을 봅니다.
* [답글](#reply)
* [허용](#allow)
* [거부](#deny)
* [삭제](#delete)
* [닫기](#close)
* 보기 [중재 내역](#moderation-history)
* [세부 정보 보기](#viewdetails)

카드 보기 위에 있는 중재 작업 아이콘은 게시물의 텍스트이고 아래는 다음을 나타내는 데이터입니다.

* 에 답글이 있는 경우, 있는 경우 답글 수 앞에 옵니다.
* 플래그가 지정된 경우.
* 승인된 경우.
* UGC가 게시되었을 때입니다.

![singleclemode](assets/singleselectmode.png)

#### 답글 {#reply}

![답변](assets/reply.png)

단일 게시물로 작업할 때 UGC 유형이 회신을 지원하고 회신을 허용하도록 구성된 경우 회신 아이콘이 표시됩니다.

#### 허용 {#allow}

![허용](assets/allow.png)

단일 게시물로 작업할 때 게시물에 플래그가 지정되거나 거부되면 허용 아이콘이 표시됩니다. 플래그가 지정된 경우 허용을 선택하면 모든 플래그가 지워집니다.

#### 거부 {#deny}

![거부](assets/deny.png)

다음 **거부** 중재 작업은 중재된 컨텐츠에만 사용할 수 있으며 다중 선택 모드를 제외한 중재되지 않은 컨텐츠에는 표시되지 않습니다.

중재되지 않은 콘텐츠는 항상 승인됩니다.

처음에 중재된 콘텐츠는 보류 중 상태로 전환되고 나중에 승인 또는 거부되도록 수정할 수 있습니다.

보류 상태를 벗어나는 콘텐츠는 보류 상태로 돌아갈 수 없습니다. 승인됨 또는 거부됨으로 표시된 콘텐츠는 언제든지 다른 상태로 변경할 수 있습니다.

#### 삭제 {#delete}

![삭제](assets/delete.png)

단일 선택 또는 벌크 모드에서 항목을 선택하고 삭제할 수 있습니다. 삭제 작업을 수행하면 확인 대화 상자가 표시됩니다. 삭제된 항목은 콘텐츠 영역에서 즉시 사라집니다. **UGC가 삭제되면 저장소에서 영구적으로 제거되며 나중에 검색할 수 없습니다**.

#### 닫기 {#close}

![닫기](assets/close.png)

단일 게시물로 작업할 때 UGC 유형이 해당 리소스에 대한 추가 게시물을 방지하는 기능을 지원하는 경우 닫기 아이콘이 표시됩니다.

#### 관리 내역 {#moderation-history}

![중재](assets/moderation.png)

단일 게시물로 작업할 때 마우스로 가리키면 중재 내역 아이콘이 표시됩니다. 아이콘을 선택하면 UGC 게시물과 관련하여 수행한 작업 내역이 포함된 창이 표시됩니다.

여러 UGC 게시물의 콘텐츠 영역 표시로 돌아가려면 세부 정보 보기 창의 오른쪽 상단 모서리에 있는 X를 선택합니다.

예를 들면 다음과 같습니다.

![관리 기록](assets/moderation-history.png)

#### 세부 사항 보기 {#view-detail}

![보기](assets/view.png)

단일 게시물로 작업할 때 세부 정보 모드에서 UGC를 열어 더 많은 세부 정보를 볼 수 있습니다.

이렇게 하려면 게시물 위로 마우스를 가져가 `View Detail` 을(를) 클릭하고 선택하여 게시물에 대한 자세한 내용이 포함된 패널을 표시합니다.

여러 UGC 게시물의 콘텐츠 영역 표시로 돌아가려면 세부 정보 보기 창의 오른쪽 상단 모서리에 있는 X를 선택합니다.

예를 들면 다음과 같습니다.

![view1](assets/view1.png)
