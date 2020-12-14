---
title: 중재 콘솔
seo-title: 중재 콘솔
description: 중재 콘솔에 액세스하는 방법
seo-description: 중재 콘솔에 액세스하는 방법
uuid: d3b8a160-85b2-43f4-9891-5fafa8c48c5f
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 404582ab-bb4c-4775-9ae3-17356d376dca
docset: aem65
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '2110'
ht-degree: 3%

---


# 중재 콘솔 {#moderation-console}

AEM Communities에서는 관리자 및 커뮤니티 중재자(중재자로 지정된 신뢰할 수 있는 커뮤니티 구성원)가 커뮤니티 콘텐츠[의 일괄 중재를 작성자 및 게시 환경 모두에서 사용할 수 있습니다.](/help/communities/moderate-ugc.md)

관리자 및 커뮤니티 중재자는 게시 환경에서 [상황에 맞는 중재](/help/communities/in-context.md)를 수행할 수도 있습니다.

모든 [커뮤니티 사이트](/help/communities/sites-console.md)의 기능은 관리자 권한으로 로그인한 사용자가 사용할 수 있는 `Administration` 메뉴 항목입니다. `Administration` 링크는 중재 콘솔에 대한 액세스를 제공합니다.

중재 콘솔에서 관리자 및 커뮤니티 중재자는 중재할 권한이 있는 모든 사용자 생성 컨텐츠(UGC)에 액세스할 수 있습니다. 여러 사이트를 중재할 수 있도록 허용된 경우 모든 사이트의 게시물을 보거나 선택한 커뮤니티 사이트별로 필터링할 수 있습니다.

자세한 내용은 [사용자 및 사용자 그룹 관리](/help/communities/users.md)를 참조하십시오.

중재 콘솔에서는 다음을 지원합니다.

* 중재 작업을 일괄적으로 수행합니다.
* UGC 검색 중.
* UGC 세부 사항 보기.
* UGC 작성자 세부 사항 보기.

관리자로 로그인하거나 ` [moderator permissions](/help/communities/in-context.md#identifyingtrustedmembers)`을(를) 가진 구성원만 중재 작업을 수행할 수 있습니다.

## 게시 환경 액세스 {#publish-environment-access}

게시된 커뮤니티 사이트에서 중재 콘솔에 대한 액세스는 커뮤니티 중재자가 로그인하면 나타나는 관리 링크를 통해 이루어집니다.

![publishweretail](assets/publishweretail.png)

관리 링크를 선택하면 중재 콘솔이 표시됩니다.

![moderation-console-publish](assets/moderation-console-publish.png)

## 작성 환경 액세스 {#author-environment-access}

작성 환경에서 중재 콘솔에 도달하려면

* 전역 탐색에서 **[!UICONTROL 커뮤니티]** > **[!UICONTROL 중재]**&#x200B;를 선택합니다.

관리자로 로그인하거나 [중재자 권한](/help/communities/in-context.md#identifyingtrustedmembers)을(를) 가진 구성원으로서 로그인하는 경우에만 중재 작업을 수행할 수 있습니다. 로그인된 구성원이 중재할 수 있는 커뮤니티 콘텐츠만 표시됩니다.

>[!NOTE]
>
>선택한 SRP가 공용 저장소를 구현하는 경우에만 게시 환경의 UGC가 작성자에게만 표시됩니다. 예를 들어 기본적으로 JSRP는 작성자 및 게시를 위한 일반적인 스토어가 아닙니다. [커뮤니티 콘텐츠 저장소](/help/communities/working-with-srp.md)를 참조하십시오.

![moderationconsole작성자](assets/moderationconsoleauthor.png)

## 중재 콘솔 UI {#moderation-console-ui}

왼쪽 탐색 레일(작성자에는 나타나지만 게시에는 나타나지 않음)을 제외하고 중재 UI에는 다음과 같은 주요 영역이 있습니다.

* **[위쪽 내비게이션 막대](#top-navigation-bar)**
* **[도구 모음](#toolbar)**
* **[컨텐츠 영역](#content-area)**

### 위쪽 탐색 모음 {#top-navigation-bar}

상단 내비게이션 막대는 모든 콘솔에 대해 상수입니다. 자세한 내용은 [기본 처리](/help/sites-authoring/basic-handling.md)를 참조하십시오.

### 도구 모음 {#toolbar}

위쪽 내비게이션 막대 아래에 있는 도구 모음은 왼쪽에 다음과 같은 전환 스위치를 제공합니다.

* [필터 ](/help/communities/moderation.md#filterrail)
레일에서는 컨텐츠를 필터링할 속성을 선택할 수 있는 레일을 엽니다.

위쪽 내비게이션 막대 아래에 있는 도구 모음은 왼쪽에 다음과 같은 전환 스위치를 제공합니다.

![톱니바퀴](assets/toggleswitch.png)

[필터 ](/help/communities/moderation.md#filterrail)
레일에서는 검색을 선택하면 컨텐츠를 필터링할 속성을 선택할 수 있는 레일이 열립니다.

![필레](assets/filterrail.png)

### 컨텐츠 영역 {#content-area}

컨텐츠 영역에는 게시된 UGC에 대한 정보가 포함되어 있습니다.

* UGC 게시됨
* 멤버 이름
* 멤버 아바타
* 게시물의 위치입니다.
* 게시되었을 때
* 게시물에 대한 답글 수입니다.
* [게시물](/help/communities/moderate-ugc.md#sentiment) 과 연결된 센티멘트
* 승인되면 확인 표시가 표시됩니다.
* 첨부 파일이 있으면 페이퍼클립이 표시됩니다.

>[!NOTE]
> 
>콘텐트 영역에는 *무한 스크롤*&#x200B;이 있습니다. 즉, 컨텐츠가 끝날 때까지 계속 스크롤할 수 있습니다. 도구 모음은 스크롤하는 중에도 컨텐츠 영역 위에 표시되는 고정된 위치에 있습니다.

### 필터 레일 {#ootbfilters}

![오픈 파일](assets/open-filterrail.png)

사이드 패널 아이콘은 필터 레일을 엽니다. 컨텐츠 영역 왼쪽에 나타나는 필터 레일은 서로 다른 필터를 제공하므로 각 필터는 컨텐츠 영역에 나타나는 참조된 UGC에 즉시 영향을 줍니다.

각 카테고리 내의 필터는 **OR**&#39;이고, 다른 카테고리의 필터는 **AND**&#x200B;입니다.

예를 들어 **질문**&#x200B;과 **대답**&#x200B;을 모두 선택하면 **질문** *또는&#x200B;**대답**인 컨텐츠가 표시됩니다.*

그러나 **질문** 및 **보류 중**&#x200B;을 선택하면 **질문**&#x200B;이고 **보류 중**&#x200B;인 컨텐츠만 표시됩니다.

>[!NOTE]
>
>커뮤니티 중재자는 중재 콘솔 UI에 사전 정의된 필터를 책갈피로 지정할 수 있습니다. 이러한 필터가 쿼리 문자열 매개 변수로 URL의 끝 부분에 추가되므로, 중재자는 나중에 책갈피가 표시된 필터로 다시 돌아가서 이러한 링크도 공유할 수 있습니다.

![searchicon](assets/searchicon.png)

필터 레일이 열려 있으면 검색 아이콘을 통해 사이드 패널을 닫도록 전환합니다. 하지만 필터 레일을 닫고 사용자가 생성한 컨텐츠만 보려면 검색 아이콘을 클릭하고 컨텐츠 전용 옵션을 선택합니다.

#### 컨텐츠 경로 {#content-path}

컨텐츠 경로는 지정된 컨텐츠 저장소에 배치된 게시물에 표시되는 참조 UGC를 제한합니다.

![content-path](assets/content-path.png)

#### 텍스트 검색 {#text-search}

텍스트 검색은 입력한 텍스트가 포함된 게시물에 표시된 참조된 UGC를 제한합니다.

![텍스트 검색](assets/text-search.png)

#### 사이트 {#site}

사이트에서 선택된 커뮤니티 사이트에 게시물에 표시되는 참조된 UGC를 제한합니다. 사이트를 선택하지 않으면 UGC에 대한 모든 참조가 표시됩니다.

![site-panel](assets/site-panel.png)

>[!NOTE]
>
>관리자가 벌크 중재 콘솔에 액세스하면 Geometrixx 샘플과 같이 [사이트 만들기 마법사](/help/communities/sites-console.md)로 만들지 않은 사이트를 비롯하여 UGC에 대한 모든 참조가 표시됩니다.
>
>신뢰할 수 있는 커뮤니티 구성원이 게시 시 벌크 중재 콘솔에 액세스하면 멤버가 중재할 수 있는 권한이 있는 커뮤니티 사이트에 대해 만들어진 UGC 참조만 표시되며 사이트 필터로 필터링할 수 있습니다.

#### 컨텐츠 유형 {#content-type}

컨텐츠 유형은 선택한 리소스 유형의 게시물에 표시된 참조된 UGC를 제한합니다. 다음 유형 중 하나 이상을 선택할 수 있습니다. 선택하지 않으면 모든 유형이 표시됩니다.

* **주석**
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

#### 추가 컨텐츠 유형 {#additional-content-types}

필터링할 추가 리소스를 추가하려면:

* 작성자 인스턴스에 관리자로 로그인합니다.
* [웹 콘솔](https://localhost:4502/system/console/configMgr)을(를) 엽니다.
* `AEM Communities Moderation Dashboard Filters`을(를) 찾습니다.
* 편집 모드에서 열 구성을 선택합니다.
* 필터링할 구성 요소의 ResourceType을 입력합니다.

   * 예를 들어 포함된 투표 구성 요소를 필터링하려면 다음을 입력합니다.

      `Voting=social/tally/components/hbs/voting`
   ![additional contenttype](assets/additional-contenttype.png)

* 저장을 선택합니다.
* 커뮤니티 - 중재 콘솔을 새로 고칩니다.

그 결과 `Content Type` 필터 그룹 아래의 `Voting`에 대해 선택 가능한 새 필터가 됩니다.

해당 필터가 선택되면 대시보드 컨텐츠에 입력한 ResourceTypes 중 하나와 일치하는 UGC가 표시됩니다.

#### 상태 {#status}

상태는 선택된 상태의 게시물에 표시된 참조된 UGC를 제한합니다. 이 게시물은 [대기 중], [승인됨], [거부됨] 또는 [닫힘], [블로그 기사 초안] 또는 [예약됨], [QnA 질문에 대해 답변됨] 또는 [답변 없음]의 하나 이상이 될 수 있습니다. 아무 것도 선택하지 않으면 모두 표시됩니다.

>[!NOTE]
>
>해결책이 제시되지 않음 상태만 선택된 경우, 중재자는 답변된 질문을 제외한 모든 컨텐츠 유형(모든 컨텐츠 유형)을 볼 수 있습니다. 답변하지 않은 질문 및 포럼 주제, 블로그 기사 또는 댓글과 같은 기타 컨텐츠에 답변된 질문에 대한 책임이 있는 속성이 없기 때문입니다.

![상태](assets/statuses.png)

#### 플래그 지정 {#flagging}

플래그를 지정하면 플래그 지정되거나 숨겨진 게시물에 표시된 참조된 UGC가 제한됩니다.

한 컨텐츠의 플래그가 지정되면 해당 단일 컨텐트의 플래그를 해제할 때까지 **플래그** 단추를 다시 한 번 선택하여 플래그가 지정됩니다. 중요 또는 팔로우와 같은 플래그 지정 수준은 없습니다.

![플래그](assets/flagging.png)

#### 구성원 {#members}

멤버는 입력한 멤버 이름으로 게시된 UGC에 표시되는 참조된 UGC를 제한합니다.

![구성원](assets/members.png)

#### 마지막에 게시된 항목 {#posted-in-the-last}

마지막 게시물에서 참조된 UGC가 지난 시간, 일, 주, 월 또는 연도의 게시물에 표시됩니다.

![게시 마지막](assets/posted-last.png)

#### 감정 {#sentiment}

[감정](/help/communities/moderate-ugc.md#sentiment) 은 참조된 UGC가 긍정, 부정 또는 중립적인 감정 값으로 게시물에 제한됩니다.

![감정](assets/sentiment.png)

## 사용자 정의 필터 {#custom-filters}

[필터 레일](/help/communities/moderation.md#ootbfilters)의 기본 필터 이외에 메타데이터에 대한 추가 사용자 지정 필터를 중재 UI에 추가할 수 있습니다. 개발자는 Github의 샘플 코드를 사용하여 기존 중재 UI 필터를 확장할 수 있습니다.

![custom-tag-filter](assets/custom-tag-filter.png)

Github의 [샘플 프로젝트](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/main/aem-communities-moderation-filter)는 태그 필터를 구현하여 특정 태그가 사용자 생성 콘텐츠에 적용되었는지 여부를 기준으로 UGC 목록을 필터링합니다. 샘플 코드를 따라 기타 유사한 UGC 메타데이터 필드에 대한 분석 필터를 만들 수 있습니다.

태그 필터에 대한 샘플을 설치하려면:

1. AEM 작성자([https://[aem-author]:4502/crx/packmgr/index.jsp](https://aem65-communities-demo.corp.adobe.com:4502/crx/packmgr/index.jsp)) 인스턴스와 AEM 게시([https://[aem-publish]:4503/crx/packmgr/index.jsp](https://aem65-communities-demo.corp.adobe.com:4502/crx/packmgr/index.jsp)) 인스턴스에 패키지 관리자를 엽니다.
1. Github 코드에서 `com.adobe.social.sample.moderation.filter.ui.apps-1.0-SNAPSHOT.zip` 패키지를 빌드하고 동일한 패키지를 설치하고 활성화합니다.
1. AEM 작성자( `https://[aem-author]:4502/system/console/bundles`) 인스턴스와 AEM 게시( `https://[aem-publish]:4503/system/console/bundles`) 인스턴스에서 번들 콘솔을 엽니다.
1. Github에서 ` [com](https://sample-moderation-filter.com/).adobe.social.sample.moderation.filter.core-1.0-SNAPSHOT.jar` 패키지를 빌드하고 동일한 패키지를 설치하고 활성화합니다.
1. AEM 작성자([https://[aem-author]:4502/crx/de/index.jsp#/apps/social/moderation/facets](https://aem65-communities-demo.corp.adobe.com:4502/crx/de/index.jsp#/apps/social/moderation/facets))의 **/apps/social/moderation/facets**) 및 AEM 게시([https://#[aem-publish]:4502/crx/de/index.jsp#/apps/social/moderation/partion/a5/>) 인스턴스로 이동합니다.](https://aem65-communities-demo.corp.adobe.com:4502/crx/de/index.jsp#/apps/social/moderation/facets)
1. `jcr:read` 권한이 있는 기술 사용자 **communities-utility-reader**&#x200B;를 추가합니다.

기존 커뮤니티 사이트에 사용자 정의 필터를 표시하려면:

1. 기존 중재 페이지 `/content/we-retail/us/en/community/moderation/shell3/jcr:content/head/clientlibs.`의 `Clientlibs` 편집

   * 새 카테고리 `cq.social.hbs.moderation.v2.` 추가

1. 다음으로 이동:`/content/we-retail/us/en/community/moderation/shell3/jcr:content/rails/searchWell/items/filters.`

   * 새 구성 요소 `sling:resourceType = social/moderation/v2/filters.`으로 설정

1. 이동 `/content/we-retail/us/en/community/moderation/shell3/jcr:content/views/content/items/modcontainer`.

   * 새 구성 요소 `sling:resourceType = social/moderation/v2/modcontainer`으로 설정합니다.

## 중재 작업 {#moderation-actions}

[컨텐츠 ](/help/communities/moderate-ugc.md#moderation-actions) 영역에 있는 하나 이상의 선택 사항이나 컨텐츠 세부 사항을 볼 때 중재 작업이 수행됩니다.

게시물을 일괄적으로 중재하려면 컨텐츠 영역에서 게시물의 선택(![선택 아이콘](assets/selecticon.png)) 아이콘을 클릭하여 마우스(데스크톱)로 게시물 위에 마우스를 올려 놓거나 게시물(모바일)에서 손가락을 누른 상태로 나타납니다. 이렇게 하면 다중 선택 모드로 전환되고 이후 게시물을 클릭하기만 하면 일괄 중재할 후속 게시물을 선택할 수 있습니다. 도구 모음에 표시되는 단추를 사용하여 선택한 게시물에 대해 중재 작업을 수행합니다. 모든 작업이 확인 메시지를 표시합니다.

컨텐츠 영역의 단일 게시물을 중재하려면 마우스(데스크톱)로 마우스를 가져가거나 게시물(모바일)에서 손가락을 누른 상태에서 해당 단추가 게시물에 표시됩니다. 단일 컨텐츠 세부 정보로 작업하는 경우, 삭제 작업만 확인 메시지를 표시합니다.

### 여러 게시물 중재 {#moderating-multiple-posts}

게시물에서 `Select` 아이콘을 클릭하여 벌크 선택 모드로 들어갑니다.

![select-icon](assets/select-icon.png)

벌크 선택 모드를 종료하려면 도구 모음에서 취소(x) 아이콘을 선택합니다.

여러 게시물에 대해 수행할 수 있는 중재 작업은 다음과 같습니다.

* 거부
* 삭제
* 게시물 닫기/다시 열기

이러한 작업을 허용하는 아이콘은 여러 게시물을 선택한 경우에만 도구 모음에 표시됩니다.

![불순물](assets/bulkmoderate.png)

### 단일 게시물 중재{#moderating-a-single-post}

단일 선택 모드에서 다음을 수행할 수 있습니다.

* 사용자 이름을 선택하여 사용자 세부 사항을 봅니다.
* 게시물에 대한 링크를 선택하여 상황에 맞는 게시물을 봅니다.
* [답글](#reply)
* [허용](#allow)
* [거부](#deny)
* [삭제](#delete)
* [닫기](#close)
* [중재 내역 보기](#moderation-history)
* [세부 사항 보기](#viewdetails)

중재 작업 아이콘 위의 카드 보기에 있는 것은 게시물의 텍스트이고 아래는 다음을 나타내는 데이터입니다.

* 답글이 있을 경우 답글 개수가 앞에 옵니다.
* 플래그가 지정된 경우
* 승인된 경우.
* UGC가 게시되었을 때.

![singleselectmode](assets/singleselectmode.png)

#### 답글 {#reply}

![회신](assets/reply.png)

단일 게시물을 사용하여 작업할 때 UGC 유형이 응답을 지원하고 응답을 허용하도록 구성된 경우 답글 아이콘이 표시됩니다.

#### 허용 {#allow}

![허용](assets/allow.png)

단일 게시물을 사용하여 작업할 때 게시물이 플래그 지정되거나 거부되면 허용 아이콘이 표시됩니다. 플래그가 지정된 경우 허용을 선택하면 모든 플래그가 지워집니다.

#### 거부 {#deny}

![거부](assets/deny.png)

**거부** 중재 동작은 중재된 컨텐츠에만 사용할 수 있으며, 다중 선택 모드를 제외한 중재되지 않은 컨텐츠에는 나타나지 않습니다.

중재되지 않은 컨텐츠는 항상 승인됩니다.

중재되는 컨텐츠는 처음에 보류 중 상태로 전환되며 나중에 승인되거나 거부되도록 수정할 수 있습니다.

보류 상태를 유지하는 컨텐츠는 보류 중인 상태로 되돌릴 수 없습니다. 승인됨 또는 거부됨으로 표시된 컨텐츠는 언제든지 다른 상태로 변경할 수 있습니다.

#### 삭제 {#delete}

![삭제](assets/delete.png)

단일 선택 또는 벌크 모드에서 항목을 선택하고 삭제할 수 있습니다. 삭제 작업을 수행하면 확인 대화 상자가 나타납니다. 삭제된 항목은 컨텐츠 영역에서 즉시 사라집니다. **UGC가 삭제되면 저장소에서 영구적으로 제거되고 나중에 검색할 수 없습니다**.

#### 닫기 {#close}

![닫기](assets/close.png)

단일 게시물을 사용하여 작업할 때 UGC 유형이 해당 리소스에 대한 추가 게시물을 방지하는 기능을 지원하는 경우 닫기 아이콘이 표시됩니다.

#### 관리 내역 {#moderation-history}

![중재](assets/moderation.png)

단일 게시물을 사용하여 작업할 때 마우스로 가리키면 중재 내역 아이콘이 표시됩니다. 아이콘을 선택하면 UGC 게시물과 관련된 작업 내역이 포함된 창이 표시됩니다.

여러 UGC 게시물의 컨텐츠 영역 표시로 돌아가려면 보기 세부 사항 창의 오른쪽 맨 위에 있는 X를 선택합니다.

예:

![중재 내역](assets/moderation-history.png)

#### 세부 사항 보기 {#view-detail}

![보기](assets/view.png)

단일 게시물을 사용하여 작업할 때 세부 사항 모드에서 UGC를 열어 자세한 내용을 볼 수 있습니다.

이렇게 하려면 게시물 위로 마우스를 가져가 `View Detail` 아이콘을 표시하고 이를 선택하여 게시물에 대한 자세한 정보가 포함된 패널을 표시합니다.

여러 UGC 게시물의 컨텐츠 영역 표시로 돌아가려면 보기 세부 사항 창의 오른쪽 맨 위에 있는 X를 선택합니다.

예:

![view1](assets/view1.png)

