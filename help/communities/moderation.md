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
source-git-commit: f7e5afe46100db7837647ac89aaf58cf101143b0

---


# 중재 콘솔 {#moderation-console}

AEM Communities에서는 관리자 및 커뮤니티 중재자(중재자로 지정된 신뢰할 수 있는 커뮤니티 구성원)가 작성 환경과 게시 환경 모두에서 커뮤니티 컨텐츠를 [일괄](/help/communities/moderate-ugc.md) 중재할 수 있습니다.

관리자 및 커뮤니티 중재자는 게시 환경에서 [상황에 맞는 중재를](/help/communities/in-context.md) 수행할 수도 있습니다.

모든 [커뮤니티 사이트의](/help/communities/sites-console.md) 기능은 관리자 권한으로 로그인한 사용자가 사용할 수 있는 `Administration` 메뉴 항목입니다. 이 `Administration` 링크를 통해 중재 콘솔에 액세스할 수 있습니다.

중재 콘솔에서 관리자 및 커뮤니티 중재자는 중재할 권한이 있는 모든 사용자 생성 콘텐츠(UGC)에 액세스할 수 있습니다. 여러 사이트를 중재할 수 있도록 허용된 경우 모든 사이트의 게시물을 보거나 선택한 커뮤니티 사이트별로 필터링할 수 있습니다.

자세한 내용은 사용자 및 [사용자 그룹 관리를 참조하십시오](/help/communities/users.md).

중재 콘솔에서는 다음을 지원합니다.

* 일괄 중재 작업 수행
* UGC를 검색하는 중입니다.
* UGC 세부 사항 보기를 참조하십시오.
* UGC 작성자 세부 정보 보기를 참조하십시오.

관리자로 로그인하거나 함께 구성원으로 로그인된 경우에만 중재 작업을 수행할 ` [moderator permissions](/help/communities/in-context.md#identifyingtrustedmembers)`수 있습니다.

## 게시 환경 액세스 {#publish-environment-access}

게시된 커뮤니티 사이트에서 중재 콘솔에 대한 액세스는 커뮤니티 중재자가 로그인하면 표시되는 관리 링크를 통해 이루어집니다.

![발행물 소매](assets/publishweretail.png)

관리 링크를 선택하면 중재 콘솔이 나타납니다.

![moderationconsole-publish](assets/moderationconsole-publish.png)

## 작성 환경 액세스 {#author-environment-access}

작성 환경에서 중재 콘솔에 도달하려면

* 글로벌 탐색에서 커뮤니티 > **[!UICONTROL 중재를]** 선택합니다 ****.

관리자로 로그인하거나 [중재자 권한이](/help/communities/in-context.md#identifyingtrustedmembers)있는 구성원으로 로그인하는 경우에만 중재 작업을 수행할 수 있습니다. 표시된 유일한 커뮤니티 콘텐츠는 로그인한 구성원이 중재할 수 있는 것입니다.

>[!NOTE]
>
>게시 환경의 UGC는 선택한 SRP가 공용 저장소를 구현하는 경우에만 작성자에게 표시됩니다. 예를 들어, 기본적으로 스토리지는 JSRP로 작성자와 게시를 위한 일반적인 스토어가 아닙니다. 커뮤니티 [컨텐츠 저장소를 참조하십시오](/help/communities/working-with-srp.md).


![moderationconsoundeauthor](assets/moderationconsoleauthor.png)

## 중재 콘솔 UI {#moderation-console-ui}

왼쪽 탐색 레일(작성자에는 표시되지만 게시에는 표시되지 않음)을 옆으로 설정하면 중재 UI에는 다음과 같은 주요 영역이 있습니다.

* **[위쪽 내비게이션 막대](#top-navigation-bar)**
* **[도구 모음](#toolbar)**
* **[컨텐츠 영역](#content-area)**

### Top Navigation Bar {#top-navigation-bar}

상단 내비게이션 막대는 모든 콘솔에 대해 일정합니다. 자세한 내용은 기본 [처리를 참조하십시오](/help/sites-authoring/basic-handling.md).

### 도구 모음 {#toolbar}

상단 내비게이션 막대 아래에 있는 도구 모음에서는 왼쪽에 다음과 같은 전환 스위치를 제공합니다.

* [필터 레일은](/help/communities/moderation.md#filterrail)컨텐츠를 필터링할 속성을 선택할 수 있는 레일을 엽니다.

상단 내비게이션 막대 아래에 있는 도구 모음에서는 왼쪽에 다음과 같은 전환 스위치를 제공합니다.

![톱니바퀴](assets/toggleswitch.png)

[필터 레일은](/help/communities/moderation.md#filterrail)검색을 선택하면 레일을 열고 컨텐츠를 필터링할 속성을 선택할 수 있습니다.

![filterail](assets/filterrail.png)

### 컨텐츠 영역 {#content-area}

컨텐츠 영역에는 게시된 UGC에 대한 정보가 포함되어 있습니다.

* UGC 게시됨
* 멤버 이름
* 회원 아바타
* 게시물의 위치입니다.
* 게시되었을 때
* 게시물에 대한 답글 수입니다.
* [게시물과](/help/communities/moderate-ugc.md#sentiment) 연결된 센티멘트
* 승인되면 확인 표시가 표시됩니다.
* 첨부 파일이 있는 경우 종이 클립이 표시됩니다.

>[!NOTE]
> 
>콘텐트 영역에는 *무한 스크롤이*&#x200B;적용되어 있으므로 콘텐츠의 끝에 도달할 때까지 계속 스크롤할 수 있습니다. 도구 모음은 스크롤하는 동안에도 컨텐츠 영역 위에 고정되고 표시되는 위치에 남아 있습니다.


### 필터 레일 {#ootbfilters}

![chlimage_1-212](assets/chlimage_1-212.png)

사이드 패널 아이콘이 필터 레일을 엽니다. 컨텐츠 영역의 왼쪽에 표시되는 필터 레일은 서로 다른 필터를 제공하므로 각 필터는 컨텐츠 영역에 나타나는 참조된 UGC에 즉시 영향을 줍니다.

각 카테고리 내의 필터는 **모두** OR이며, 다른 범주의 필터는 **AND**&#x200B;입니다.

예를 들어 [질문] 및 [ **대답** ] **을**&#x200B;모두 **선택하면** 질문 *또는 VerizingAnswerAnswerAnswer* 에 해당하는 내용이 ****&#x200B;표시됩니다.

그러나 질문 및 **보류** 중 **옵션을**&#x200B;선택하면 **질문이며 보류 중인** 콘텐트만 **볼**&#x200B;수있습니다.

>[!NOTE]
>
>커뮤니티 중재자는 중재 콘솔 UI에 사전 정의된 필터를 책갈피로 지정할 수 있습니다. 이러한 필터는 URL 끝(쿼리 문자열 매개 변수)에 추가되므로 중재자는 나중에 책갈피가 지정된 필터로 다시 돌아가서 이러한 링크도 공유할 수 있습니다.


![searchicon](assets/searchicon.png)

필터 레일이 열려 있으면 검색 아이콘이 사이드 패널을 닫도록 전환합니다. 하지만 필터 레일을 닫고 사용자가 생성한 컨텐츠만 보려면 검색 아이콘을 클릭하고 컨텐츠 전용 옵션을 선택합니다.

#### 컨텐츠 경로 {#content-path}

컨텐츠 경로는 지정된 컨텐츠 저장소에 배치된 게시물에 표시되는 참조 UGC를 제한합니다.

![content-path](assets/content-path.png)

#### 텍스트 검색 {#text-search}

텍스트 검색은 입력한 텍스트가 들어 있는 게시물에 표시된 참조된 UGC를 제한합니다.

![chlimage_1-213](assets/chlimage_1-213.png)

#### 사이트 {#site}

사이트는 참조된 UGC가 선택된 커뮤니티 사이트에 게시물로 제한됩니다. 선택된 사이트가 없으면 UGC에 대한 모든 참조가 표시됩니다.

![chlimage_1-214](assets/chlimage_1-214.png)

>[!NOTE]
>
>관리자가 벌크 중재 콘솔에 액세스하면 Geometrixx 샘플과 같이 [사이트 만들기 마법사로](/help/communities/sites-console.md)만들지 않은 사이트를 비롯하여 UGC에 대한 모든 참조가 표시됩니다.
>
>신뢰할 수 있는 커뮤니티 구성원이 게시 시 벌크 중재 콘솔에 액세스하면 구성원이 중재할 수 있는 커뮤니티 사이트에 대해 만든 UGC에 대한 참조만 표시되며 사이트 필터로 필터링할 수 있습니다.


#### 컨텐트 유형 {#content-type}

컨텐츠 유형은 참조된 UGC가 선택한 리소스 유형의 게시물로 제한됩니다. 다음 유형 중 하나 이상을 선택할 수 있습니다. 선택하지 않으면 모든 유형이 표시됩니다.

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

필터링할 리소스를 추가하려면:

* 관리자로 작성자 인스턴스에 로그인합니다.
* 웹 [콘솔을 엽니다](https://localhost:4502/system/console/configMgr).
* 위치를 `AEM Communities Moderation Dashboard Filters`찾습니다.
* 편집 모드에서 열 구성을 선택합니다.
* 필터링할 구성 요소의 ResourceType을 입력합니다.

   * 예를 들어 포함된 투표 구성 요소에 대해 필터링하려면 다음을 입력합니다.

      `Voting=social/tally/components/hbs/voting`

![chlimage_1-215](assets/chlimage_1-215.png)

* 저장을 선택합니다.
* 커뮤니티 - 중재 콘솔을 새로 고칩니다.

그 결과 필터 그룹 `Voting` 아래에 대해 선택 가능한 새로운 필터가 `Content Type` 만들어집니다.

이 필터를 선택하면 대시보드 컨텐츠가 입력된 ResourceTypes와 일치하는 UGC를 표시합니다.

#### 상태 {#status}

상태는 선택된 상태의 게시물, 하나 이상의 보류 중, 승인됨, 거부됨 또는 닫힘, 블로그 아티클에 대한 초안 또는 예약됨, QnA 질문에 대한 답변 또는 없음 중 하나로 참조된 UGC를 제한합니다. 아무 것도 선택하지 않으면 모두 표시됩니다.

>[!NOTE]
>
>해결책이 제시되지 않음 상태만 선택된 경우 중재자는 답변된 질문을 제외한 모든 컨텐츠 유형(모든 컨텐츠 유형)을 보게 됩니다. 답변되지 않은 질문과 포럼 주제, 블로그 기사 또는 댓글과 같은 기타 컨텐츠의 경우 답변된 질문에 대한 책임이 있는 속성이 존재하지 않기 때문입니다.


![상태](assets/statuses.png)

#### 플래그 지정 {#flagging}

플래그를 지정하면 플래그 지정되거나 숨겨진 게시물에 표시되는 참조된 UGC가 제한됩니다.

컨텐츠 일부가 플래그가 지정되면 플래그 **단추를 다시 한 번 선택하여 해당 컨텐츠의 플래그를 해제할 때까지 플래그가** 지정됩니다. 중요 또는 팔로우와 같은 플래그 지정은 없습니다.

![chlimage_1-216](assets/chlimage_1-216.png)

#### 구성원 {#members}

멤버는 입력한 멤버 이름으로 게시되는 UGC에 표시된 참조된 UGC를 제한합니다.

![chlimage_1-217](assets/chlimage_1-217.png)

#### 마지막에 게시된 항목 {#posted-in-the-last}

[마지막 게시물]은 참조된 UGC가 지난 시간, 일, 주, 월 또는 연도에 수행된 게시물에 표시되도록 제한합니다.

![chlimage_1-218](assets/chlimage_1-218.png)

#### 감정 {#sentiment}

[센티멘트는](/help/communities/moderate-ugc.md#sentiment) 긍정, 부정 또는 중립 센티멘트 값이 있는 게시물에 표시되는 참조된 UGC를 제한합니다.

![chlimage_1-219](assets/chlimage_1-219.png)

## Custom Filters {#custom-filters}

필터 레일의 기본 필터 외에도 메타데이터에 [대한](/help/communities/moderation.md#ootbfilters)추가 사용자 정의 필터를 중재 UI에 추가할 수 있습니다. 개발자는 Github의 샘플 코드를 사용하여 기존 중재 UI 필터를 확장할 수 있습니다.

![custom-tag-filter](assets/custom-tag-filter.png)

Github의 [샘플 프로젝트는](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter) 태그 필터를 구현하여 특정 태그가 사용자 생성 컨텐츠에 적용되는지 여부를 기준으로 UGC 목록을 필터링합니다. 샘플 코드를 따라 다른 유사한 UGC 메타데이터 필드에 대한 분석 필터를 만들 수 있습니다.

태그 필터의 샘플을 설치하려면:

1. AEM 작성자(https://[aem-author]:[4502/crx/packmgr/index.jsp](https://aem65-communities-demo.corp.adobe.com:4502/crx/packmgr/index.jsp)) 인스턴스와 AEM 게시([https://[aem-publish]:4503/crx/packmgr/index.jsp](https://aem65-communities-demo.corp.adobe.com:4502/crx/packmgr/index.jsp)) 인스턴스에서 패키지 관리자를 엽니다.
1. Github `com.adobe.social.sample.moderation.filter.ui.apps-1.0-SNAPSHOT.zip` 코드에서 패키지를 빌드하고 동일한 패키지를 설치하고 활성화합니다.
1. AEM 작성자() 인스턴스 및 AEM 게시( `https://[aem-author]:4502/system/console/bundles``https://[aem-publish]:4503/system/console/bundles`) 인스턴스에서 번들 콘솔을 엽니다.
1. Github에서 패키지를 ` [com](https://sample-moderation-filter.com/).adobe.social.sample.moderation.filter.core-1.0-SNAPSHOT.jar` 빌드하고 동일한 패키지를 설치하고 활성화합니다.
1. AEM 작성자( **https://[aem-author]:4502/crx/de/index.jsp#/apps/social/moderation/facets** ) 및 AEM 게시([https://[aem-publish]:4502/crx/de/index.jsp#/apps/social/moderation/facet](https://aem65-communities-demo.corp.adobe.com:4502/crx/de/index.jsp#/apps/social/moderation/facets)[](https://aem65-communities-demo.corp.adobe.com:4502/crx/de/index.jsp#/apps/social/moderation/facets)) 인스턴스로 이동합니다.
1. 기술 사용자 **커뮤니티-유틸리티 판독기를** 추가할 수 있는 `jcr:read` 권한을 제공합니다.

기존 커뮤니티 사이트에 사용자 정의 필터를 표시하려면:

1. 기존 중재 `Clientlibs` 페이지 편집 `/content/we-retail/us/en/community/moderation/shell3/jcr:content/head/clientlibs.`

   * 새 카테고리 추가 `cq.social.hbs.moderation.v2.`

1. 다음으로 이동:`/content/we-retail/us/en/community/moderation/shell3/jcr:content/rails/searchWell/items/filters.`

   * 새 구성 요소로 설정 `sling:resourceType = social/moderation/v2/filters.`

1. 이동 `/content/we-retail/us/en/community/moderation/shell3/jcr:content/views/content/items/modcontainer`.

   * 새 구성 요소로 `sling:resourceType = social/moderation/v2/modcontainer`설정합니다.

## 중재 작업 {#moderation-actions}

[중재 작업은](/help/communities/moderate-ugc.md#moderation-actions) 컨텐츠 영역에서 선택한 하나 이상의 사항이나 컨텐츠 세부 사항을 볼 때 수행할 수 있습니다.

게시물을 벌크 중재하려면 컨텐츠 영역에서 게시물의 선택( ![선택](assets/selecticon.png)아이콘)을 클릭합니다. 이 아이콘은 마우스(데스크톱)를 사용하여 마우스를 위에 놓거나 게시물에서 손가락을 누른 채 나타납니다(모바일). 이렇게 하면 다중 선택 모드로 전환되고 이후 게시물을 클릭하여 일괄 중재할 게시물을 선택할 수 있습니다. 도구 모음에 표시된 단추를 사용하여 선택한 게시물에 대해 중재 작업을 수행합니다. 모든 작업이 확인 메시지를 표시합니다.

컨텐츠 영역의 단일 게시물을 중재하려면 마우스를 위에 놓고(데스크톱) 또는 게시물(모바일)을 길게 눌러 게시물에 표시되는 단추를 누릅니다. 단일 컨텐츠 세부 정보로 작업할 경우 삭제 작업만 확인 메시지가 표시됩니다.

### 여러 게시물 중재 {#moderating-multiple-posts}

게시물의 아이콘을 클릭하여 벌크 선택 모드로 `Select` 들어갑니다.

![select-icon](assets/select-icon.png)

벌크 선택 모드를 종료하려면 도구 모음에서 취소(x) 아이콘을 선택합니다.

여러 게시물에서 수행할 수 있는 중재 작업은 다음과 같습니다.

* 거부
* 삭제
* 게시물 닫기/다시 열기

이러한 작업을 허용하는 아이콘은 여러 게시물을 선택한 경우에만 도구 모음에 표시됩니다.

![불순물](assets/bulkmoderate.png)

### 단일 게시물 중재 {#moderating-a-single-post}

단일 선택 모드에서 다음을 수행할 수 있습니다.

* 사용자 이름을 선택하여 사용자 세부 사항을 봅니다.
* 게시물에 대한 링크를 선택하여 상황에 맞는 게시물을 봅니다.
* [답글](#reply)
* [허용](#allow)
* [거부](#deny)
* [삭제](#delete)
* [닫기](#close)
* 중재 [내역 보기](#moderation-history)
* [세부 사항 보기](#viewdetails)

중재 작업 아이콘 위의 카드 보기에 표시되는 것은 게시물의 텍스트이고 아래에 표시되는 데이터는 다음과 같습니다.

* 답글이 있는 경우, 그리고 있을 경우 답글 수 앞에 옵니다.
* 플래그가 지정된 경우
* 승인되었다면
* UGC가 게시되었을 때.

![singleselectmode](assets/singleselectmode.png)

#### 답글 {#reply}

![chlimage_1-220](assets/chlimage_1-220.png)

단일 게시물로 작업할 때 UGC 유형이 응답을 지원하고 답글을 허용하도록 구성된 경우 답글 아이콘이 표시됩니다.

#### 허용 {#allow}

![chlimage_1-221](assets/chlimage_1-221.png)

단일 게시물로 작업할 때 게시물이 플래그 지정되거나 거부되면 허용 아이콘이 표시됩니다. 플래그가 지정된 경우 [허용]을 선택하면 모든 플래그가 지워집니다.

#### 거부 {#deny}

![chlimage_1-222](assets/chlimage_1-222.png)

중재 **거부** 작업은 중재된 컨텐츠에만 사용할 수 있으며 다중 선택 모드를 제외한 중재되지 않은 컨텐츠에는 나타나지 않습니다.

중재되지 않은 컨텐츠는 항상 승인됩니다.

중재되는 컨텐츠는 처음에 보류 상태로 전환되며 나중에 승인되거나 거부되도록 수정할 수 있습니다.

보류 중인 상태를 유지하는 컨텐츠는 보류 중인 상태로 되돌릴 수 없습니다. 승인 또는 거부로 표시된 컨텐츠는 언제든지 다른 상태로 변경할 수 있습니다.

#### 삭제 {#delete}

![chlimage_1-223](assets/chlimage_1-223.png)

단일 선택 또는 벌크 모드에서 항목을 선택하고 삭제할 수 있습니다. 삭제 작업으로 인해 확인 대화 상자가 나타납니다. 삭제된 항목은 컨텐츠 영역에서 즉시 사라집니다. **UGC가 삭제되면 저장소에서 영구적으로 제거되고 나중에 검색할**&#x200B;수 없습니다.

#### 닫기 {#close}

![chlimage_1-224](assets/chlimage_1-224.png)

단일 게시물로 작업할 때 UGC 유형이 해당 리소스에 대한 추가 게시물을 방지하는 기능을 지원하는 경우 닫기 아이콘이 표시됩니다.

#### 관리 내역 {#moderation-history}

![chlimage_1-225](assets/chlimage_1-225.png)

단일 게시물을 사용하여 작업할 때 마우스로 가리키면 중재 내역 아이콘이 표시됩니다. 아이콘을 선택하면 UGC 게시물과 관련된 작업 내역이 포함된 창이 표시됩니다.

여러 UGC 게시물의 컨텐츠 영역 표시로 돌아가려면 보기 세부 사항 창의 오른쪽 상단 모서리에서 X를 선택합니다.

예 :

![chlimage_1-226](assets/chlimage_1-226.png)

#### 세부 사항 보기 {#view-detail}

![chlimage_1-227](assets/chlimage_1-227.png)

단일 게시물을 사용하여 작업할 때 세부 사항 모드에서 UGC를 열면 더 많은 세부 사항을 볼 수 있습니다.

이렇게 하려면 게시물 위로 마우스를 가져가면 `View Detail` 아이콘이 표시되고 이 아이콘을 선택하면 게시물에 대한 자세한 정보가 포함된 패널이 표시됩니다.

여러 UGC 게시물의 컨텐츠 영역 표시로 돌아가려면 보기 세부 사항 창의 오른쪽 상단 모서리에서 X를 선택합니다.

예 :

![chlimage_1-228](assets/chlimage_1-228.png)

