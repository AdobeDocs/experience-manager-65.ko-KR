---
title: 커뮤니티 콘텐츠 중재
seo-title: 커뮤니티 콘텐츠 중재
description: 중재 개념 및 작업
seo-description: 중재 개념 및 작업
uuid: 5c991d3a-0037-4d78-8f91-bb62e44441fa
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 6866d209-5789-4ef9-bc3c-d644d4fb4b1c
docset: aem65
role: 관리자
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1524'
ht-degree: 0%

---


# 커뮤니티 콘텐츠 중재 중 {#moderating-community-content}

## 개요 {#overview}

사용자 생성 컨텐츠(UGC)라고도 하는 커뮤니티 컨텐츠는 멤버(사이트 방문자에 로그인됨)가 다음 커뮤니티 구성 요소 중 하나와의 상호 작용을 통해 게시된 커뮤니티 사이트의 컨텐츠를 게시할 때 생성됩니다.

* [블로그](/help/communities/blog-feature.md):구성원은 블로그 기사 또는 댓글을 게시합니다.
* [달력](/help/communities/calendar.md):구성원은 달력 이벤트 또는 댓글을 게시합니다.
* [주석](/help/communities/comments.md):구성원은 댓글을 게시하거나 댓글에 답글을 답니다.

* [포럼](/help/communities/forum.md):구성원은 새 주제를 게시하거나 주제에 답글을 답니다.
* [아이디어](/help/communities/ideation-feature.md):구성원은 아이디어 또는 댓글을 게시합니다.
* [QnA](/help/communities/working-with-qna.md):구성원이 질문을 만들거나 질문에 답변합니다.
* [평가](/help/communities/reviews.md):회원은 항목에 등급을 매길 때 댓글을 게시합니다.

UGC를 중재하는 것은 긍정적 기여도를 인정하고 부정적인 것(예: 스팸 및 욕설 언어)을 제한하는 데 유용합니다. UGC는 다음과 같은 여러 환경에서 조정할 수 있습니다.

* [커뮤니티 컨텐츠 저장소](working-with-srp.md)

* [일괄 중재 콘솔](moderation.md)

   중재 콘솔은 관리자와 공용 환경의 [커뮤니티 중재자](/help/communities/users.md)뿐만 아니라 작성 환경의 관리자가 액세스할 수 있습니다. 이는 커뮤니티 콘텐트가 [공통 스토어](/help/communities/working-with-srp.md)에 저장되어 있을 때 가능합니다.

* [컨텍스트 내 중재](in-context.md)

   게시 환경의 중재는 컨텐츠가 게시된 페이지에서 바로 관리자 및 커뮤니티 중재자가 수행할 수 있습니다.

## 중재 작업 {#moderation-actions}

게시된 컨텐츠(UGC)에 대해 수행할 수 있는 작업은 사용자 ID 및 환경에 따라 다릅니다. 아래 표에서는 사용자 ID에 따라 다양한 역할을 설명하는 다음 용어를 사용합니다.

* `Admin`

   [community-administrators](users.md) 그룹의 구성원인 사용자입니다.

* `Moderator`

   [커뮤니티 중재자](users.md#publishenvironmentusersandgroups) 그룹의 구성원([중재자 권한](in-context.md#moderatorpermissions) 포함)

* `Creator`

   컨텐츠를 게시한 사용자입니다.

* `Member`

   특별한 권한이 없는 로그인 사용자입니다.

* `Visitor`

   익명의 사용자입니다.

<table>
 <tbody>
  <tr>
   <td> </td>
   <td><strong>관리자</strong></td>
   <td><strong>중재자 </strong></td>
   <td><strong>작성자</strong></td>
   <td><strong>구성원</strong></td>
   <td><strong>방문자</strong></td>
   <td><strong>이벤트<br /> 트리거됨</strong></td>
   <td><strong>사전 조정</strong></td>
  </tr>
  <tr>
   <td><strong>편집/<br /> 삭제</strong></td>
   <td>X</td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>잘라내기</strong></td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>거부</strong></td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td>X</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>닫기/<br /> 다시 열기</strong></td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td>X</td>
   <td>X<br /> </td>
  </tr>
  <tr>
   <td><strong>플래그/<br /> 플래그 해제</strong></td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td>X</td>
   <td> </td>
   <td>X</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>허용</strong></td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td>X</td>
   <td>X</td>
  </tr>
 </tbody>
</table>

### {#edit-delete} 편집 / 삭제

게시물이 만들어지면 작성자, 관리자 또는 커뮤니티 중재자가 게시물을 편집하거나 삭제할 수 있습니다.

UGC가 삭제되면 저장소에서 제거되고 복구할 수 없습니다.

### 잘라내기 {#cut}

관리자나 커뮤니티 중재자가 하나 이상의 포럼 주제 또는 QnA 질문을 한 위치에서 다른 위치로 이동할 수 있습니다. 동일한 구성원에게 두 사이트 모두에 대한 중재 권한이 있는 경우 한 커뮤니티 사이트에서 다른 커뮤니티 사이트로의 중재 권한이 포함됩니다.

잘라내기 작업을 선택하면 내용이 클립보드에 복사됩니다. 여러 게시물을 복사하여 새 위치로 그룹으로 이동할 수 있습니다.

![cutugc](assets/cutugc.png)

![putbackugc](assets/putbackugc.png)

다른 위치에서는 콘텐트가 클립보드에 있을 때 붙여넣을 게시물의 수를 식별하는 숫자가 있는 새 게시물 옆에 붙여넣기 단추가 표시됩니다. [붙여넣기] 단추에는 붙여넣는 대신 클립보드를 지우는 옵션이 있습니다.

![pasteugc](assets/pasteugc.png)

![pasteugc1](assets/pasteugc1.png)

### 거부 {#deny}

사회자는 UGC가 게시된 사이트에 계속 표시되도록 허용하지 않을 수 있습니다. 관리자 및 커뮤니티 중재자에게 게시물은 여전히 사용할 수 있으며 스팸으로 주석을 달 수 있습니다.

### {#close-reopen} 닫기/다시 열기

닫기 동작은 대화 스레드(포럼 주제 또는 초기 주석)에 적용되며 이후의 모든 게시물 또는 답글을 포함합니다.

닫으면 더 이상 답글을 달 수 없을 뿐만 아니라 중재 작업도 허용되지 않습니다.

작업을 수행하려면 주제 또는 댓글이 다시 열려야 합니다.

닫기/다시 열기 작업은 관리자 또는 커뮤니티 중재자가 수행할 수 있습니다.

### 플래그 / 플래그 해제 {#flag-unflag}

플래그 지정은 컨텐츠 작성자를 제외한 모든 로그인한 구성원이 게시물의 컨텐츠에 문제가 있음을 나타내는 수단입니다. 플래그가 지정되면 동일한 멤버가 컨텐츠의 플래그를 해제할 수 있는 플래그 해제 아이콘이 표시됩니다.

게시물에 플래그를 지정하면 구성원이 이유를 선택할 수 있도록 컨텍스트 내 중재를 구성할 수 있습니다. 사용자 지정 이유를 입력할 수 있는지 여부를 포함하여 선택 가능한 플래그 이유 목록을 구성할 수 있습니다. 플래그 이유는 UGC와 함께 저장되지만 이유는 특정 작업을 트리거하지 않습니다. 플래그 수만 알림을 트리거합니다. 플래그가 달린 컨텐츠는 이에 대해 중재자가 행동할 수 있도록 이와 같이 주석을 달 수 있습니다.

시스템은 플래그가 달린 모든 플래그, 플래그 이유를 추적하며 임계값 제한에 도달하면 이벤트를 전송합니다. 커뮤니티 중재자가 UGC를 허용하면 이러한 플래그가 보관됩니다. 허용 및 보관 후, 다음 플래그가 있으면 이전 플래그가 없는 것처럼 보관됩니다.

### 허용 {#allow}

허용 작업은 플래그가 지정되었거나 거부되었거나 사전 중재된 시스템에서 승인되지 않은 UGC에 대한 옵션입니다. 허용 작업을 수행하면 플래그가 지정되거나 거부됨/스팸 상태가 표시되고 플래그가 지정된 데이터가 보관됩니다.

## 일반 중재 개념 {#common-moderation-concepts}

### 사전 중재 {#premoderation}

UGC가 사전 중재되는 경우 중재 작업에 의해 승인될 때까지 게시물은 게시된 사이트에 표시되지 않습니다. [커뮤니티 사이트](/help/communities/sites-console.md)를 만드는 동안 [컨텐츠가 사전 중재됨](sites-console.md#moderation) 상자를 선택하면 전체 사이트에 대한 사전 조정을 사용할 수 있습니다. 구성 요소를 페이지에 배치하면 편집 대화 상자의 설정을 사용하여 조정을 지원하는 구성 요소를 사전 중재하도록 구성할 수 있습니다.

* [사용자 ](comments.md) 중재  [](reviews.md)
> 사전 중재 **[!UICONTROL 에서]**   **[!UICONTROL 주석]** 및검토.

* [포럼](/help/communities/forum.md)  [아이디어](/help/communities/ideation-feature.md),  [Qn](/help/communities/working-with-qna.md)A [](/help/communities/calendar.md)
 및  **[!UICONTROL 일정]**   ****&#x200B;설정>Moderated.

### 스팸 감지 {#spam-detection}

스팸 감지는 자동 중재 기능으로, 제출된 사용자 생성 콘텐츠를 스팸으로 표시하여 부적절한 컨텐트를 필터링합니다. 활성화되면 사용자가 생성한 컨텐츠가 스팸인지 또는 사전 구성된 스팸 단어 모음을 기반으로 하지 않는지를 식별합니다. 기본 스팸 단어는

`/libs/settings/community/sites/moderation/spamdetector-conf/profiles/spam_words.txt`.

그러나 기본 스팸 단어를 사용자 정의하거나 확장하려면 [overlay](/help/communities/overlay-comments.md)을 통해 기본 스팸 단어 구조에 따라 /apps 디렉토리에 단어 집합을 만듭니다.

스팸 단어가 포함된 사용자 생성 게시물(예: 블로그, 포럼 및 댓글)(모든 컨텐츠 유형)은 게시물 위의 &quot;이 게시물이 스팸으로 분류됨&quot;이라는 텍스트로 표시됩니다.

사회자는 이러한 게시물을 보고 동일한 게시물을 표시함으로써 사이트에 나타나는 것을 허용하거나 거부할 수 있습니다. 이러한 게시물에 대한 중재 작업은 컨텍스트 내 또는 일괄 중재 UI를 통해 수행할 수 있습니다.

![spamdetection](assets/spamdetection.png)

스팸 감지 엔진을 활성화하려면 다음 단계를 수행합니다.

1. `/system/console/configMgr`으로 이동하여 [웹 콘솔](https://localhost:4502/system/console/configMgr)을 엽니다.

1. **AEM Communities 자동 중재** 구성을 찾아 편집합니다.
1. **[!UICONTROL SpamProcess]** 항목을 추가합니다.

![주파](assets/spamprocess.png)

>[!NOTE]
>
>스팸 감지는 영어 로케일에만 구현됩니다.

### 감정 {#sentiment}

감정은 게시물(UGC)에 있는 긍정적 및 부정적 키워드([watchwords](#configuringwatchwords))의 수를 기반으로 계산됩니다.

센티멘트 분석은 사전 구성된 규칙 세트를 사용하고 UGC의 센티멘트를 계산합니다. 기본 규칙은 다음 위치에 있습니다.`/libs/cq/workflow/components/workflow/social/sentiments/rules.`

규칙이 생성하는 값은 1(모두 음수입니다. 긍정적인 단어는 아니요)부터 10(모두 양수, 음수 단어 없음)까지입니다. 센티멘트 값인 5는 중립 센티멘트이며 기본값입니다.

/libs 구성 요소에 정의된 규칙은 다음과 같습니다.

* 규칙 1:긍정적인 단어가 없고 음수가 하나 이상 있으면 값을 1로 설정합니다.
* 규칙 2:음수가 없고 긍정적인 단어가 하나 이상 있으면 값을 10으로 설정합니다.
* 규칙 3:긍정적인 단어보다 부정적인 단어가 더 많은 경우 값을 3으로 설정합니다.
* 규칙 4:부정적인 단어보다 긍정적인 단어가 더 있으면 값을 8으로 설정합니다.

규칙을 덮어쓰거나 추가하려면 기본 규칙 구조에 따라 /apps 디렉토리에 규칙 세트를 만듭니다. 센티멘트 구성을 편집하여 규칙의 위치를 식별합니다.

분석하면 센티멘트가 UGC에 저장됩니다.

[벌크 중재 콘솔](/help/communities/moderation.md)에서 센티멘트가 부정, 중립 또는 긍정인지 여부에 따라 UGC를 필터링하고 볼 수 있습니다.

#### Watchwords {#watchwords}

AEM 커뮤니티는 [센티멘트](#sentiment)를 평가하는 프로세스의 한 단계로 *watchword 분석기*&#x200B;를 제공합니다. 감시자가 제공하는 센티멘트 값에 대한 기여는 게시된 컨텐츠에 사용된 네거티브 및 긍정 감시어와 금지된 단어를 비교하기 때문입니다.

#### 센티멘트 및 감시 단어 구성 {#configure-sentiment-and-watchwords}

센티멘트 규칙처럼 긍정 및 부정 감시자 목록을 사용자 지정할 수 있습니다.

기본 감시어 목록은 기본값과 유사하거나 단어 목록으로 OSGi 서비스 `sentimentprocess.name`을 구성하여 기본값을 덮어써서 응답의 노드의 속성으로 입력할 수 있습니다.

**센티멘트프로세스.name**&#x200B;도 사용자 지정 센티멘트 규칙 세트의 위치를 참조하도록 수정할 수 있습니다.

센티멘트 및 감시 단어를 구성하려면:

* 관리자로 작성자 인스턴스에 로그인합니다.
* [웹 콘솔](https://localhost:4502/system/console/configMgr)을(를) 엽니다.
* `sentimentprocess.name`을(를) 찾습니다.
* 편집 모드에서 열 구성을 선택합니다.

![센티멘트프로세스](assets/sentimentprocess.png)

* **긍정적인 감시자**

   기본값을 무시하는 긍정적인 감정에 기여하는 단어의 쉼표로 구분된 목록. 기본값은 빈 목록입니다.

* **네거티브 감시어**

   기본값을 무시하는 네거티브 센티멘트에 기여하는 단어로 쉼표로 구분된 목록. 기본값은 빈 목록입니다.

* **감시 단어 노드의 명시적 경로**

   기본 감시 단어를 지정하는 기본 `positive` 및 `negative` 속성을 포함하는 노드의 저장소 위치입니다. 기본값은 `/libs/settings/community/watchwords/default`입니다.

* **센티멘트 규칙**

   긍정 및 부정 감시 단어를 기반으로 센티멘트를 계산하기 위한 규칙의 저장소 위치입니다. 기본값은 `/libs/cq/workflow/components/workflow/social/sentiments/rules`입니다. 그러나 더 이상 관련된 워크플로가 없습니다.

`Explicit Path to Watchwords Node`이(가) `/libs/settings/community/watchwords/default`으로 설정된 경우 기본 감시자에 대한 사용자 정의 항목의 예는 다음과 같습니다.

![crxde](assets/crxde.png)

### 중재자 권한 {#moderator-permissions}

동일한 리소스에 할당된 다음 권한을 통칭하여 `moderator permissions`이라고 합니다.

* `Read`
* `Modify`
* `Create`
* `Delete`
* `Replicate`

