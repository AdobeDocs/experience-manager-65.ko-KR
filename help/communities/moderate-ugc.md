---
title: 커뮤니티 콘텐츠 중재
seo-title: Moderating Community Content
description: 조정 개념 및 작업
seo-description: Moderation concepts and actions
uuid: 5c991d3a-0037-4d78-8f91-bb62e44441fa
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 6866d209-5789-4ef9-bc3c-d644d4fb4b1c
docset: aem65
role: Admin
exl-id: 22276580-e6bc-41c5-9ac3-e8f291f676b7
source-git-commit: 812b9f3af3ad04343e648a8d07d53f8442978b82
workflow-type: tm+mt
source-wordcount: '1516'
ht-degree: 0%

---

# 커뮤니티 콘텐츠 중재 {#moderating-community-content}

## 개요 {#overview}

사용자 생성 컨텐츠(UGC)라고도 하는 커뮤니티 컨텐츠는 구성원(로그인한 사이트 방문자)이 다음 커뮤니티 구성 요소 중 하나와의 상호 작용을 통해 게시된 커뮤니티 사이트의 컨텐츠를 게시하면 생성됩니다.

* [블로그](/help/communities/blog-feature.md): 구성원은 블로그 기사 또는 댓글을 게시합니다.
* [달력](/help/communities/calendar.md): 구성원은 달력 이벤트 또는 댓글을 게시합니다.
* [댓글](/help/communities/comments.md): 구성원은 댓글에 댓글 또는 답글을 게시한다.

* [포럼](/help/communities/forum.md): 구성원은 새 주제를 게시하거나 주제에 답글을 답니다.
* [관념화](/help/communities/ideation-feature.md): 회원들은 아이디어나 의견을 게시한다.
* [QnA](/help/communities/working-with-qna.md): 구성원은 질문을 만들거나 질문에 답합니다.
* [검토](/help/communities/reviews.md): 항목에 등급을 매길 때 구성원이 댓글을 게시합니다.

UGC를 중재하는 것은 긍정적인 기여도를 인식하는 동시에 음성 기여도(예: 스팸 및 학대 언어)를 제한하는 데 유용합니다. UGC는 몇 가지 환경에서 중재할 수 있습니다.

* [커뮤니티 컨텐츠 저장소](working-with-srp.md)

* [벌크 중재 콘솔](moderation.md)

   관리 콘솔은 관리자 및 [커뮤니티 중재자](/help/communities/users.md) 작성 환경의 관리자뿐만 아니라 공개 환경에서도 사용됩니다. 이는 커뮤니티 컨텐츠가 [일반 상점](/help/communities/working-with-srp.md).

* [컨텍스트 내 중재](in-context.md)

   게시 환경의 중재는 컨텐츠가 게시된 페이지에서 바로 관리자 및 커뮤니티 중재자가 수행할 수 있습니다.

## 중재 작업 {#moderation-actions}

게시된 콘텐츠(UGC)에서 수행할 수 있는 작업은 사용자 ID 및 환경에 따라 다릅니다. 아래 표는 다음 용어를 사용하여 사용자 ID에 따라 다양한 역할을 설명합니다.

* `Admin`

   의 멤버인 사용자 [community-administrators](users.md) 그룹에 속해 있어야 합니다.

* `Moderator`

   의 구성원 [커뮤니티 중재자](users.md#publishenvironmentusersandgroups) 그룹(있음) [중재자 권한](in-context.md#moderatorpermissions)).

* `Creator`

   컨텐츠를 게시한 사용자입니다.

* `Member`

   특수 권한이 없는 로그인한 사용자입니다.

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
   <td><strong>사전 중재됨</strong></td>
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

### 편집 / 삭제 {#edit-delete}

게시물이 만들어지면 작성자, 관리자 또는 커뮤니티 중재자가 게시물을 편집하거나 삭제할 수 있습니다.

UGC가 삭제되면 저장소에서 제거되고 복구되지 않을 수 있습니다.

### 잘라내기 {#cut}

관리자 또는 커뮤니티 중재자가 하나 이상의 포럼 주제나 QnA 질문을 한 위치에서 다른 위치로 이동할 수 있습니다. 여기에는 한 커뮤니티 사이트에서 다른 커뮤니티 사이트까지 포함됩니다. 동일한 구성원이 두 사이트 모두에 중재 권한을 가지고 있는 경우 이에 포함됩니다.

잘라내기 작업을 선택하면 컨텐츠가 클립보드에 복사됩니다. 여러 게시물을 그룹으로 복사하고 새 위치로 이동할 수 있습니다.

![cutugc](assets/cutugc.png)

![putbackugc](assets/putbackugc.png)

다른 위치에서는 클립보드에 컨텐츠가 있으면 붙여넣을 게시물의 수를 식별하는 숫자가 있는 새 게시물 옆에 붙여넣기 단추가 표시됩니다. 붙여넣기 단추에는 붙여넣기가 아닌 클립보드를 지울 수 있는 옵션이 포함되어 있습니다.

![대지](assets/pasteugc.png)

![pasteugc1](assets/pasteugc1.png)

### 거부 {#deny}

중재자는 UGC가 게시된 사이트에 계속 표시되도록 할 수 없습니다. 관리자 및 커뮤니티 중재자에게 게시물은 계속 사용할 수 있으며 스팸으로 주석을 답니다.

### 닫기/다시 열기 {#close-reopen}

닫기 작업은 전체 대화 스레드(포럼 주제 또는 초기 댓글)에서 작동하며 모든 후속 게시물 또는 답글을 포함합니다.

닫히면 더 이상 답글을 쓸 수 없으며 중재 작업도 허용되지 않습니다.

작업을 수행하려면 항목이나 설명을 다시 열어야 합니다.

닫기/다시 열기 작업은 관리자 또는 커뮤니티 중재자가 수행할 수 있습니다.

### 플래그/플래그 해제 {#flag-unflag}

플래그 지정은 컨텐츠 작성자를 제외하고, 게시물의 컨텐츠에 문제가 있음을 나타내기 위해 로그인한 구성원을 위한 방법입니다. 플래그가 지정되면 동일한 구성원이 컨텐츠 플래그를 해제할 수 있는 플래그 해제 아이콘이 표시됩니다.

게시물에 플래그를 지정할 때 구성원이 이유를 선택할 수 있도록 컨텍스트 내 조정을 구성할 수 있습니다. 사용자 지정 사유를 입력할 수 있는지 여부를 포함하여 선택 가능한 플래그 이유 목록을 구성할 수 있습니다. 플래그 이유는 UGC로 저장되지만, 이유는 특정 작업을 트리거하지 않습니다. 플래그 수만 알림을 트리거합니다. 플래그가 지정된 컨텐츠에 주석을 달아서 중재자가 작동할 수 있습니다.

시스템은 플래그가 지정된 모든 플래그, 플래그 이유 및 임계값에 도달하면 이벤트를 전송합니다. 커뮤니티 중재자가 UGC를 허용하면 이 플래그가 보관됩니다. 허용 및 보관 후에, 후속 플래그가 있는 경우 이전 플래그가 없는 것처럼 보관됩니다.

### 허용 {#allow}

허용 작업은 미리 중재된 시스템에서 플래그 지정, 거부 또는 승인되지 않은 UGC에 대한 옵션입니다. 허용 작업을 수행하면 플래그가 지정되거나 거부됨/스팸 상태가 지워지고 플래그가 지정된 데이터가 보관됩니다.

## 일반 중재 개념 {#common-moderation-concepts}

### Premoderation {#premoderation}

UGC가 사전 중재되면 중재 작업에 의해 승인될 때까지 게시된 사이트에 게시물이 표시되지 않습니다. 생성 중 [커뮤니티 사이트](/help/communities/sites-console.md), 상자 선택 [컨텐츠가 미리 중재됨](sites-console.md#moderation) 전체 사이트에 대해 사전 조정을 활성화합니다. 구성 요소가 페이지에 배치되면 편집 대화 상자의 설정을 사용하여 조정을 지원하는 구성 요소를 사전 조정을 위해 구성할 수 있습니다.

* [댓글](comments.md) 및 [검토](reviews.md)
in **[!UICONTROL 사용자 중재]** > **[!UICONTROL 사전 중재]**.

* [포럼](/help/communities/forum.md), [관념화](/help/communities/ideation-feature.md), [QnA](/help/communities/working-with-qna.md), 및 [달력](/help/communities/calendar.md)
in **[!UICONTROL 설정]** > **[!UICONTROL 중재됨]**.

### 스팸 감지 {#spam-detection}

스팸 감지는 자동 중재 기능으로서, 사용자가 생성한 컨텐츠를 스팸으로 표시하여 부적절한 제출 콘텐츠를 필터링합니다. 활성화되면 사용자가 생성한 컨텐츠가 스팸인지 또는 사전에 구성된 스팸 단어 모음을 기반으로 식별됩니다. 기본 스팸 단어는 다음 위치에 제공됩니다.

`/libs/settings/community/sites/moderation/spamdetector-conf/profiles/spam_words.txt`.

그러나 기본 스팸 단어를 사용자 지정하거나 확장하려면 다음을 통해 기본 스팸 단어의 구조에 따라 /apps 디렉토리에 단어 세트를 만듭니다 [오버레이](/help/communities/overlay-comments.md).

스팸 단어가 포함된 모든 콘텐츠 유형(예: 블로그, 포럼 및 댓글)에 대해 사용자가 생성한 게시물은 게시물 위에 &quot;이 게시물이 스팸으로 분류됨&quot;이라는 텍스트가 표시됩니다.

중재자는 이러한 게시물을 보고 해당 게시물이 사이트에 나타나지 않도록 표시하거나 표시를 변경할 수 있습니다. 이러한 게시물에 대한 중재 작업은 컨텍스트 내 또는 벌크 중재 UI를 통해 수행할 수 있습니다.

![spamdetection](assets/spamdetection.png)

스팸 감지 엔진을 활성화하려면 다음 단계를 수행하십시오.

1. 열기 [웹 콘솔](https://localhost:4502/system/console/configMgr), 다음 위치로 이동 `/system/console/configMgr`.

1. 찾기 **AEM Communities 자동 중재** 구성 및 편집
1. 추가 **[!UICONTROL SpamProcess]** 을 입력합니다.

![spamprocess](assets/spamprocess.png)

>[!NOTE]
>
>스팸 감지는 영어 로케일에 대해서만 구현됩니다.

### 감정 {#sentiment}

감성은 양수 및 음수 키워드([어워치](#configuringwatchwords))가 게시물(UGC)에 있는 경우

감정 분석에서는 사전 구성된 규칙 세트를 사용하고 UGC의 감정을 계산합니다. 기본 규칙은 다음 위치에 있습니다. `/libs/cq/workflow/components/workflow/social/sentiments/rules.`

규칙이 생성하는 값은 1(모두 음수, 양수 단어 없음)에서 10(모두 양수, 음수 단어 없음)입니다. 감정 값 5는 중립 정답이며 기본값입니다.

/libs 구성 요소에 정의된 규칙은 다음과 같습니다.

* 규칙 1: 긍정적인 단어가 없고 음수가 하나 이상 있는 경우 값을 1로 설정합니다.
* 규칙 2: 음수가 없고 긍정적인 단어가 하나 이상 있는 경우 값을 10으로 설정합니다.
* 규칙 3: 긍정적인 단어보다 음수가 많은 경우 값을 3으로 설정합니다.
* 규칙 4: 음수 단어보다 긍정적인 단어가 더 있으면 값을 8로 설정합니다.

규칙을 덮어쓰거나 추가하려면 기본 규칙 구조를 따라 /apps 디렉토리에 규칙 세트를 만듭니다. 감정 구성을 편집하여 규칙의 위치를 식별합니다.

분석되면 UGC와 함께 감정이 저장됩니다.

에서 [벌크 중재 콘솔](/help/communities/moderation.md)를 설정하는 경우, 감정이 부정적인지, 중립적인지 또는 긍정적인지 여부에 따라 UGC를 필터링하고 볼 수 있습니다.

#### Watchwords {#watchwords}

AEM communities에서 다음을 제공합니다. *watword 분석기* 평가 프로세스의 한 단계로서 [감정](#sentiment). 워치워드에서 제공되는 감정 값에 대한 기여는 게시된 컨텐츠에 사용되는 음성과 긍정적인 감시 단어 및 금지된 단어를 비교한 것입니다.

#### 감정 및 Watchwords 구성 {#configure-sentiment-and-watchwords}

긍정 및 부정적 관찰자의 목록은 감정 규칙이 될 수 있으므로 사용자 지정할 수 있습니다.

기본 watchwords 목록은 기본값과 비슷하거나 OSGi 서비스를 구성하여 기본값을 재정의하여 응답에서 노드의 속성으로 입력할 수 있습니다 `sentimentprocess.name` 라는 단어를 사용하여 검색할 수 있습니다.

다음 **sentimentprocess.name** 사용자 지정 감정 규칙 세트의 위치를 참조하도록 수정할 수도 있습니다.

감정 및 감시 단어를 구성하려면:

* 관리자로 작성자 인스턴스에 로그인합니다.
* 열기 [웹 콘솔](https://localhost:4502/system/console/configMgr).
* 찾기 `sentimentprocess.name`.
* 편집 모드에서 열 구성을 선택합니다.

![감정 처리](assets/sentimentprocess.png)

* **긍정적인 감시 단어**

   기본값을 무시하는 긍정적인 정서에 기여하는 단어를 쉼표로 구분한 목록입니다. 기본값은 빈 목록입니다.

* **음성 감시 단어**

   기본값을 무시하는 음수 정서에 기여하는 단어의 쉼표로 구분된 목록입니다. 기본값은 빈 목록입니다.

* **Watchwords 노드에 대한 명시적 경로**

   기본값이 포함된 노드의 저장소 위치 `positive` 및 `negative` 기본 watchwords를 지정하는 속성입니다. 기본값은 입니다. `/libs/settings/community/watchwords/default`.

* **감정 규칙**

   양수 및 음수 감지를 기반으로 하여 감정을 계산하기 위한 규칙의 저장소 위치입니다. 기본값은 입니다. `/libs/cq/workflow/components/workflow/social/sentiments/rules` (그러나 더 이상 관련된 워크플로우가 없습니다.)

다음은 기본 감시 단어에 대한 사용자 정의 항목의 예입니다. `Explicit Path to Watchwords Node` 가 로 설정되어 있습니다. `/libs/settings/community/watchwords/default`.

![crxde](assets/crxde.png)

### 중재자 권한 {#moderator-permissions}

다음 권한은 동일한 리소스에 지정된 경우 집합적으로 라고 합니다 `moderator permissions`:

* `Read`
* `Modify`
* `Create`
* `Delete`
* `Replicate`
