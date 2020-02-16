---
title: 메시징 기능
seo-title: 메시징 기능
description: 메시징 구성 요소 구성
seo-description: 메시징 구성 요소 구성
uuid: 8b99ded1-aec2-40c9-82d5-e2e404f614ca
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 9d952604-f9ef-498f-937b-871817c80226
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# 메시징 기능{#messaging-feature}

포럼 및 댓글에 나타나는 공개 표시 상호 작용 이외에도****AEM Communities의 메시징 기능을 사용하면 커뮤니티 구성원은 상호 작용을 보다 비공개로 할 수 있습니다.

이 기능은 [커뮤니티 사이트를](/help/communities/overview.md#communitiessites) 만들 때 포함될 수 있습니다.

메시징 기능은 다음과 같은 기능을 제공합니다.

**하나** 이상의 커뮤니티 멤버에게&#x200B;**** 메시지 보내기 - [C](/help/communities/messaging.md#group-messaging)-C **** - 직접 메시지를&#x200B;**커뮤니티 멤버에게** 보내기BulkD 첨부 파일 보내기 - Forward 메시지**E*Reply **** to a Forward 메시지 회신* To a Delete Message * Delete*

![messaging-section](assets/messaging-section.png) restore- ![message](assets/restore-message.png)

메시징 기능을 활성화하고 수정하려면 다음을 참조하십시오.

* [관리자용 메시지](/help/communities/messaging.md) 구성
* [Messaging Essentials](/help/communities/essentials-messaging.md) for developers

>[!NOTE]
>
>작성 편집 모드에서 구성 요소( `Compose Message, Message, or Message List` `Communities`구성 요소 그룹에 있음)를 페이지에 추가하는 것은 지원되지 않습니다.

## 메시징 구성 요소 구성 {#configure-messaging-components}

커뮤니티 사이트에 대한 메시징이 활성화되면 추가 구성 없이 설정됩니다. 기본 구성을 변경해야 할 경우 정보가 제공됩니다.

### 메시지 목록 구성(메시지 상자) {#configure-message-list-message-box}

받은 편지함, 보낸 **항목**&#x200B;및 메시징 기능의 ** **휴지통 ****&#x200B;페이지에 대한 메시지 목록 구성을 수정하려면 [작성 편집 모드에서](/help/communities/sites-console.md#authoring-site-content)사이트를 엽니다.

1. 모드에서 ** `Preview`Messages **링크를 선택하여 기본 메시징 페이지를 엽니다. 그런 다음 받은 **편지함**, **보낸 편지함 **또는 **휴지통 **을 선택하여 해당 메시지 목록에 대한 구성 요소를 구성합니다.

1. 모드에서 페이지에서 구성 요소를 `Edit` 선택합니다.
1. 구성 대화 상자에 액세스하려면 `link`아이콘을 선택하여 상속을 취소합니다.
상속이 취소되면 구성 아이콘을 선택하여 구성 대화 상자를 열 수 있습니다.

1. 구성이 완료되면 `broken link` 아이콘을 선택하여 상속을 복원해야 합니다.

![configure-message-list](assets/configure-message-list.png)

#### Basic tab {#basic-tab}

![basic-tab-messagelist](assets/basic-tab-messagelist.png)

* **서비스 선택기**(*필수*)`serviceSelector.name`AEM Communities Messaging Operations Service에서 속성** [*](/help/communities/messaging.md#messaging-operations-service)의 값으로 설정합니다.

* **페이지 작성**(*필수*)`Reply`구성원이 ****버튼을 클릭할 때 열리는 페이지입니다. 대상 페이지에는 메시지 작성 **양식이 포함되어야** 합니다.

* **리소스로 답글/**&#x200B;보기이 확인란을 선택하면 회신 URL 및 보기 URL은 리소스를 참조하며, 그렇지 않으면 데이터는 URL에서 쿼리 매개 변수로 전달됩니다.

* **프로필 표시**&#x200B;양식발신자 프로필을 표시하는 데 사용할 프로필 양식입니다.

* **휴지통 폴더**&#x200B;이 확인란을 선택하면 이 메시지 목록 구성 요소는 삭제된 것으로 표시된 메시지(휴지통)만 표시합니다.

* **폴더 경로**(*필수*) **AEM Communities Messaging Operations Service의** inbox.path.name [및 **sentitems.path.name **에 대해 설정된 값을](/help/communities/messaging.md#messaging-operations-service)참조합니다. 를 구성할 `Inbox`때 **inbox.path.name**&#x200B;값을 사용하여 항목을 하나 추가합니다. 에 대해 구성할 `Outbox`때 **sentitems.path.name**&#x200B;값을 사용하여 한 항목을 추가합니다. 를 구성할 `Trash`때 두 값을 모두 포함하는 두 항목을 추가합니다.

#### 표시 탭 {#display-tab}

![display-tab-message-list](assets/display-tab-message-list.png)

* **읽기 단추**&#x200B;표시를 선택하면 메시지를 읽음으로 표시할 수 있는 `Read`단추를 표시합니다.

* **읽지 않음 단추**&#x200B;이 확인란을 선택하면 메시지를 읽음으로 표시할 수 있는 `Mark Unread` 단추가 표시됩니다.

* **삭제**&#x200B;단추 이 확인란을 선택하면 메시지를 읽음으로 표시할 수 있는 `Delete`단추가 표시됩니다. 이 확인란을 선택하면 삭제 기능이 복제됩니다. **`Message Options`**

* **메시지**&#x200B;옵션 이 확인란을 선택하면 메시지를 다시 전송하거나 삭제할 수 **`Reply`**&#x200B;있도록 **`Reply All`****`Forward`**및 **`Delete`**단추를 표시합니다. 이 확인란을 선택하면 삭제 기능이 복제됩니다. **`Delete Button`**

* **페이지당 메시지**&#x200B;지정된 수는 페이지 매김 구성표에서 페이지당 표시되는 최대 메시지 수입니다. 번호가 지정되지 않은 경우(비워 둔 경우) 모든 메시지가 표시되고 페이지가 표시되지 않습니다.

* **타임스탬프 패턴**&#x200B;하나 이상의 언어에 대한 타임스탬프 패턴을 제공합니다. 기본값은 en, de, fr, it, es, ja, zh_CN, ko_KR입니다.

* **사용자**&#x200B;표시 **`Sender`**`Recipients`또는 ****를 선택하여 발신자 또는 수신자를 표시할지 여부를 결정합니다.

### 메시지 작성 구성 {#configure-compose-message}

메시지 작성 페이지의 구성을 수정하려면 [작성 편집 모드에서](/help/communities/sites-console.md#authoring-site-content)사이트를 엽니다.

* 모드에서 ** `Preview`Messages **링크를 선택하여 기본 메시징 페이지를 엽니다. 그런 다음 새 메시지 단추를 선택하여 `Compose Message` 페이지를 엽니다.

* 모드에서 메시지 본문을 포함하는 페이지의 기본 구성 요소를 `Edit` 선택합니다.
* 구성 대화 상자에 액세스하려면 `link`아이콘을 선택하여 상속을 취소합니다.
상속이 취소되면 구성 아이콘을 선택하여 구성 대화 상자를 열 수 있습니다.

* 구성이 완료되면 `broken link`아이콘을 선택하여 상속을 복원해야 합니다.

![config-compose-message](assets/config-compose-message.png)

#### Basic tab {#basic-tab-1}

![basic-tab-compose](assets/basic-tab-compose.png)

* **리디렉션 URL**&#x200B;메시지가 전송된 후 표시되는 페이지의 URL을 입력합니다. 예, `../messaging.html`.

* **URL**&#x200B;취소 발신자가 메시지를 취소할 경우 표시되는 페이지의 URL을 입력합니다. 예, `../messaging.html`.

* **메시지 제목**&#x200B;최대 길이제목 필드에 허용되는 최대 문자 수입니다. 예: 500. 기본값은 제한이 없습니다.

* **메시지 본문의 최대 길이컨텐츠**&#x200B;필드에 허용되는 최대 문자 수입니다. 예: 10000. 기본값은 제한이 없습니다.

* **서비스 선택기**(*필수*)`serviceSelector.name`AEM Communities Messaging Operations Service에서 속성** [*](/help/communities/messaging.md#messaging-operations-service)의 값으로 설정합니다.

#### 표시 탭 {#display-tab-1}

![display-tab-compose](assets/display-tab-compose.png)

* **제목 필드**&#x200B;표시를 선택한 경우 `Subject` 필드를 표시하고 메시지에 제목을 추가할 수 있습니다. 기본값은 선택되어 있지 않습니다.

* **제목**&#x200B;레이블필드 옆에 표시할 텍스트를 `Subject` 입력합니다. 기본값은 `Subject`입니다.

* **파일 첨부 필드**&#x200B;표시를 선택한 경우 `Attachment` 필드를 표시하고 메시지에 첨부 파일을 추가할 수 있습니다. 기본값은 선택되어 있지 않습니다.

* **파일 레이블**&#x200B;첨부 `Attachment` 필드 옆에 표시할 텍스트를 입력합니다. 기본값은 **`Attach File`**&#x200B;입니다.

* **컨텐츠 필드**&#x200B;표시 이 확인란을 선택하면 `Content` 필드를 표시하고 메시지 본문을 추가할 수 있습니다. 기본값은 선택되어 있지 않습니다.

* **컨텐츠**&#x200B;레이블필드 옆에 표시할 텍스트를 `Content` 입력합니다. 기본값은 **`Body`**&#x200B;입니다.

* **리치 텍스트 편집기**&#x200B;를 선택한 경우 자체 리치 텍스트 편집기가 있는 사용자 정의 컨텐츠 텍스트 상자의 사용을 나타냅니다. 기본값은 선택되어 있지 않습니다.

* **타임스탬프 패턴**&#x200B;하나 이상의 언어에 대한 타임스탬프 패턴을 제공합니다. 기본값은 en, de, fr, it, es, ja, zh_CN, ko_KR입니다.

