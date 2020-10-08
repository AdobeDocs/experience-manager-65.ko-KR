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
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 4%

---


# 메시징 기능 {#messaging-feature}

포럼과 주석에서 발생하는 공개적으로 보이는 상호 작용 이외에도, AEM Communities의 메시지 기능을 통해 커뮤니티 회원들은 더욱 비공개로 상호 작용할 수 있습니다.

이 기능은 [커뮤니티 사이트를](/help/communities/overview.md#communitiessites) 만들 때 포함될 수 있습니다.

메시징 기능은 다음과 같은 기능을 제공합니다.

**A** - 하나 이상의 커뮤니티 멤버에게 메시지 보내기

**B** - [커뮤니티 구성원 그룹에 직접 메시지 일괄 전송](/help/communities/messaging.md#group-messaging)

**C** - 첨부 파일이 있는 메시지 보내기

**D** - 메시지 전달

**전자** - 메시지에 회신

**F** - 메시지 삭제

**G** - 삭제된 메시지 복원

![메시지 섹션](assets/messaging-section.png)

![restore-message](assets/restore-message.png)

메시징 기능을 활성화하고 수정하려면 다음을 참조하십시오.

* [관리자를 위한 메시지](/help/communities/messaging.md) 구성
* [Messaging Essentials](/help/communities/essentials-messaging.md) for developers

>[!NOTE]
>
>작성 편집 모드에서 구성 요소( `Compose Message, Message, or Message List` `Communities`구성 요소 그룹에 있음)를 페이지에 추가하는 것은 지원되지 않습니다.

## 메시징 구성 요소 구성 {#configure-messaging-components}

커뮤니티 사이트에 대한 메시징이 활성화되면 추가적인 구성 없이 설정됩니다. 기본 구성을 변경해야 할 경우 정보가 제공됩니다.

### 메시지 목록 구성(메시지 상자) {#configure-message-list-message-box}

메시지 **받은 편지함**, 보낸 **항목**&#x200B;및 **휴지통** 의 메시지 목록 구성을 수정하려면 [작성자 편집 모드Facebook에서 사이트](/help/communities/sites-console.md#authoring-site-content)를 엽니다.

1. 모드에서 `Preview` 메시지 **** 링크를 선택하여 기본 메시지 페이지를 엽니다. 그런 다음 **받은 편지함**, **보낸** 항목 **또는** 휴지통중 하나를 선택하여 해당 메시지 목록에 대한 구성 요소를 구성합니다.

1. 모드에서 `Edit` 페이지에서 구성 요소를 선택합니다.
1. 구성 대화 상자에 액세스하려면 `link` 아이콘을 선택하여 상속을 취소합니다.
상속이 취소되면 구성 아이콘을 선택하여 구성 대화 상자를 열 수 있습니다.

1. 구성이 완료되면 `broken link` 아이콘을 선택하여 상속을 복원해야 합니다.

![configure-message-list](assets/configure-message-list.png)

#### Basic tab {#basic-tab}

![basic-tab-messagelist](assets/basic-tab-messagelist.png)

* **서비스 선택기**

   (*필수***`serviceSelector.name`** ) [AEM Communities 메시징 작업 서비스에서 속성 값](/help/communities/messaging.md#messaging-operations-service)으로 설정합니다.

* **페이지 작성**

   (*필수*) 구성원이 단추를 클릭할 때 열리는 **`Reply`** 페이지입니다. 대상 페이지에는 메시지 작성 **양식이** 포함되어야 합니다.

* **리소스로 답글/보기**

   이 확인란을 선택하면 회신 URL 및 보기 URL이 리소스를 참조하고, 그렇지 않은 데이터는 URL의 쿼리 매개 변수로 전달됩니다.

* **프로필 표시 양식**

   보낸 사람 프로필을 표시하는 데 사용할 프로필 양식입니다.

* **휴지통 폴더**

   이 확인란을 선택하면 이 메시지 목록 구성 요소는 삭제된 메시지(휴지통)로 플래그가 지정된 메시지만 표시합니다.

* **폴더 경로**

   (*필수***** ) **AEM Communities 메시징 작업 서비스** 서비스의 inbox.path.name [및](/help/communities/messaging.md#messaging-operations-service)sentitems.path.name에 대해 설정된 값을참조합니다. 에 대해 구성할 때 `Inbox`inbox.path.name의 값을 사용하여 하나의 **항목을 추가합니다**. 에 대해 구성할 `Outbox`때 **sentitems.path.name 값을 사용하여 항목을 하나 추가합니다**. 을(를) 구성할 때 두 값 `Trash`으로 두 항목을 추가합니다.

#### 표시 탭 {#display-tab}

![display-tab-message-list](assets/display-tab-message-list.png)

* **읽기 단추 표시**

   이 확인란을 선택하면 메시지를 읽음으로 표시할 수 있는 `Read`단추가 표시됩니다.

* **읽지 않은 표시 단추**

   이 확인란을 선택하면 메시지를 읽음으로 표시할 수 있는 `Mark Unread` 단추가 표시됩니다.

* **삭제 단추**

   이 확인란을 선택하면 메시지를 읽음으로 표시할 수 있는 `Delete` 단추가 표시됩니다. 이 확인란을 선택하면 삭제 기능 **`Message Options`** 이 복제됩니다.

* **메시지 옵션**

   이 확인란을 선택하면 메시지 **`Reply`**&#x200B;를 **`Reply All`**&#x200B;재전송하거나 삭제할 수 있는 **`Forward`** 버튼 **`Delete`** 을 표시합니다. 이 확인란을 선택하면 삭제 기능 **`Delete Button`** 이 복제됩니다.

* **페이지당 메시지**

   지정된 수는 페이지 매김 체계의 페이지당 표시되는 최대 메시지 수입니다. 번호가 지정되지 않은 경우(비워 둔 경우) 모든 메시지가 표시되고 페이지 매김이 없습니다.

* **타임스탬프 패턴**

   하나 이상의 언어에 대한 타임스탬프 패턴을 제공합니다. 기본값은 en, de, fr, it, es, ja, zh_CN, ko_KR입니다.

* **사용자 표시**

   보낸 사람 **`Sender`** 또는 받는 사람 **`Recipients`** 을 표시할지 여부를 선택하거나 선택합니다.

### 메시지 작성 구성 {#configure-compose-message}

메시지 작성 페이지의 구성을 수정하려면 [작성 편집 모드에서 사이트를 엽니다](/help/communities/sites-console.md#authoring-site-content).

* 모드에서 `Preview` 메시지 **** 링크를 선택하여 기본 메시지 페이지를 엽니다. 그런 다음 새 메시지 단추를 선택하여 `Compose Message` 페이지를 엽니다.

* 모드에서 메시지 본문을 포함하는 페이지의 기본 구성 요소를 `Edit` 선택합니다.
* 구성 대화 상자에 액세스하려면 `link` 아이콘을 선택하여 상속을 취소합니다.
상속이 취소되면 구성 아이콘을 선택하여 구성 대화 상자를 열 수 있습니다.

* 구성이 완료되면 `broken link` 아이콘을 선택하여 상속을 복원해야 합니다.

![config-compose-message](assets/config-compose-message.png)

#### Basic tab {#basic-tab-1}

![basic-tab-compose](assets/basic-tab-compose.png)

* **리디렉션 URL**

   메시지를 보낸 후 표시되는 페이지의 URL을 입력합니다. 예, `../messaging.html`.

* **취소 URL**

   발신자가 메시지를 취소할 경우 표시되는 페이지의 URL을 입력합니다. 예, `../messaging.html`.

* **메시지 제목의 최대 길이입니다**

   제목 필드에 허용되는 최대 문자 수입니다. 예: 500. 기본값은 제한이 없습니다.

* **메시지 본문의 최대 길이입니다**

   콘텐트 필드에 허용되는 최대 문자 수입니다. 예: 10000. 기본값은 제한이 없습니다.

* **서비스 선택기**

   (*필수***`serviceSelector.name`** ) [AEM Communities 메시징 작업 서비스에서 속성 값](/help/communities/messaging.md#messaging-operations-service)으로 설정합니다.

#### 표시 탭 {#display-tab-1}

![display-tab-compose](assets/display-tab-compose.png)

* **제목 필드 표시**

   이 확인란을 선택하면 필드를 `Subject` 표시하고 메시지에 제목을 추가할 수 있습니다. 기본값은 선택되어 있지 않습니다.

* **제목 레이블**

   필드 옆에 표시할 텍스트를 `Subject` 입력합니다. 기본값은 `Subject`입니다.

* **파일 첨부 필드 표시**

   이 확인란을 선택하면 `Attachment` 필드를 표시하고 메시지에 첨부 파일을 추가할 수 있습니다. 기본값은 선택되어 있지 않습니다.

* **파일 레이블 첨부**

   필드 옆에 표시할 텍스트를 `Attachment` 입력합니다. 기본값은 **`Attach File`**&#x200B;입니다.

* **컨텐츠 필드 표시**

   이 확인란을 선택하면 필드를 `Content` 표시하고 메시지 본문 추가를 활성화합니다. 기본값은 선택되어 있지 않습니다.

* **컨텐츠 레이블**

   필드 옆에 표시할 텍스트를 `Content` 입력합니다. 기본값은 **`Body`**&#x200B;입니다.

* **리치 텍스트 편집기 사용**

   이 확인란을 선택하면 자체 리치 텍스트 편집기가 있는 사용자 지정 컨텐츠 텍스트 상자의 사용을 나타냅니다. 기본값은 선택되어 있지 않습니다.

* **타임스탬프 패턴**

   하나 이상의 언어에 대한 타임스탬프 패턴을 제공합니다. 기본값은 en, de, fr, it, es, ja, zh_CN, ko_KR입니다.

