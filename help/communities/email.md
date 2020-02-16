---
title: 이메일 구성
seo-title: 이메일 구성
description: 커뮤니티를 위한 이메일 구성
seo-description: 커뮤니티를 위한 이메일 구성
uuid: e8422cc2-1594-43b0-b587-82825636cec1
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: b4d38e45-eaa0-4ace-a885-a2e84fdfd5a1
pagetitle: Configuring Email
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d

---


# 이메일 구성 {#configuring-email}

AEM Communities,

* [커뮤니티 알림](notifications.md)
* [커뮤니티 구독](subscriptions.md)

기본적으로 이메일 기능은 SMTP 서버 및 SMTP 사용자의 사양이 필요하므로 작동하지 않습니다.

>[!CAUTION]
>
>알림 및 구독에 대한 이메일은 [기본 게시자에서만](deploy-communities.md#primary-publisher)구성해야 합니다.

## 기본 메일 서비스 구성 {#default-mail-service-configuration}

기본 메일 서비스는 알림과 구독 모두에 필요합니다.

* 기본 게시자에서
* 관리자 권한으로 로그인
* 웹 [콘솔 액세스](../../help/sites-deploying/configuring-osgi.md)

   * 예: [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* Locate the `Day CQ Mail Service`
* 편집 아이콘 선택

이메일 알림 구성에 대한 설명서를 [기반으로](../../help/sites-administering/notification.md)하지만 필드가 `"From" address` 필요하지 *않고* 비워 두어야 한다는 점에서 차이가 있습니다.

예를 들어, (삽화를 위한 값으로만 채워진):

![chlimage_1-98](assets/chlimage_1-98.png)

* **[!UICONTROL SMTP 서버 호스트 이름]**:(필수) ** 사용할 SMTP 서버입니다.

* **[!UICONTROL SMTP 서버 포트]** *(필수)* SMTP 서버 포트는 25 이상이어야 합니다.

* **[!UICONTROL SMTP 사용자]**:(필수) ** SMTP 사용자입니다.

* **[!UICONTROL SMTP 암호]**:(필수) ** SMTP 사용자의 암호입니다.

* **[!UICONTROL &quot;보낸 사람&quot; 주소]**:비워 둡니다.
* **[!UICONTROL SMTP SSL 사용]**:이 확인란을 선택하면 보안 이메일을 보냅니다. 포트가 SMTP 서버에 대해 필요에 따라 465로 설정되어 있는지 확인합니다.
* **[!UICONTROL 디버그 이메일]**:이 확인란을 선택하면 SMTP 서버 상호 작용 로깅을 활성화합니다.

## AEM Communities 이메일 구성 {#aem-communities-email-configuration}

기본 메일 서비스가 [구성되면 릴리스에 포함된 OSGi 구성의 기존](#default-mail-service-configuration) `AEM Communities Email Reply Configuration` 두 인스턴스가 작동합니다.

이메일로 회신을 허용할 때는 구독 인스턴스만 추가로 구성해야 합니다.

1. ` [email](#configuration-for-notifications)` instance

   회신 이메일을 지원하지 않고 변경해서는 안 되는 알림입니다.

1. ` [subscriptions-email](#configuration-for-subscriptions)` instance

   회신 이메일에서 게시물 작성을 완전히 활성화하는 구성 필요

커뮤니티 이메일 구성 인스턴스에 도달하려면 다음을 수행하십시오.

* 기본 게시자에서
* 관리자 권한으로 로그인
* 웹 [콘솔 액세스](../../help/sites-deploying/configuring-osgi.md)

   * 예: [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* 찾기 `AEM Communities Email Reply Configuration`

![chlimage_1-99](assets/chlimage_1-99.png)

### 알림 구성 {#configuration-for-notifications}

이름 이메일이 `AEM Communities Email Reply Configuration` 있는 OSGi 구성의 인스턴스는 알림 기능입니다. 이 기능에는 이메일 회신이 포함되지 않습니다.

이 구성은 변경하지 마십시오.

* Locate the `AEM Communities Email Reply Configuration`
* 편집 아이콘 선택
* 이름 **확인** : `email`

* 회신 **이메일에서** 게시물 만들기가 `unchecked`

![chlimage_1-100](assets/chlimage_1-100.png)

### 가입 구성 {#configuration-for-subscriptions}

커뮤니티 구독의 경우, 회원이 이메일에 회신하여 컨텐츠를 게시할 수 있는 기능을 활성화하거나 비활성화할 수 있습니다.

* Locate the `AEM Communities Email Reply Configuration`
* 편집 아이콘 선택
* 이름 **확인** : `subscriptions-email`

![chlimage_1-101](assets/chlimage_1-101.png)

* **[!UICONTROL 이름]** :(필수) **`subscriptions-email`. 편집하지 마십시오.

* **[!UICONTROL 회신 이메일에서]**&#x200B;게시물 만들기:이 확인란을 선택하면 구독 이메일을 받는 사람이 답글을 보내 컨텐츠를 게시할 수 있습니다. 기본값은 선택되어 있습니다.
* **[!UICONTROL 헤더에]**&#x200B;추적된 ID 추가:기본값은 `Reply-To`입니다.

* **[!UICONTROL 제목 최대 길이]**:추적기 ID가 제목 줄에 추가되는 경우 추적된 ID를 제외하고 피사체의 최대 길이이며 그 이후는 트리밍됩니다. 추적된 ID 정보가 손실되지 않도록 하려면 가능한 한 작아야 합니다. 기본값은 200입니다.
* **[!UICONTROL 이메일 &quot;보낸 사람&quot; 주소]**:( *필수)* 알림 이메일을 배달할 주소. **기본 메일 서비스에** 대해 지정된 것과 동일한 SMTP 사용자일 [](#configuredefaultmailservice)수 있습니다. 기본값은 `no-reply@example.com`입니다.

* **[!UICONTROL 회신 구분 기호]**:추적기 ID 파섹 기본값은 `+` (더하기 기호)입니다.

* **[!UICONTROL 주체의]**&#x200B;추적기 ID 접두사:추적기 ID가 제목 줄에 추가되면 이 접두사가 사용됩니다. 기본값은 `post#`입니다.

* **[!UICONTROL 메시지 본문에]**&#x200B;있는 추적기 ID 접두사:추적기 ID가 메시지 본문에 추가되는 경우 이 접두사가 사용됩니다. 기본값은 `Please do not remove this:`입니다.

* **[!UICONTROL HTML로 이메일]**:이 확인란을 선택하면 컨텐츠 유형이 로 `"text/html;charset=utf-8"`설정됩니다. 기본값은 선택되어 있습니다.

* **[!UICONTROL 기본 사용자 이름]**:이 이름은 이름 사용자가 없는 경우 사용됩니다. 기본값은 `no-reply@example.com`입니다.

* **[!UICONTROL 템플릿 루트 경로]**:이메일은 이 루트 경로에 저장된 템플릿을 사용하여 작성합니다. 기본값은 `/etc/community/templates/subscriptions-email`입니다.

## 폴링 가져오기 구성 {#configure-polling-importer}

이메일을 저장소로 가져오려면 폴링 가져오기를 구성하고 저장소에 속성을 수동으로 구성해야 합니다.

### 새 폴링 가져오기 추가 {#add-new-polling-importer}

* 기본 게시자에서
* 관리자 권한으로 로그인
* 폴링 가져오기 콘솔 탐색예: [http://localhost:4503/etc/importers/polling.html](http://localhost:4503/etc/importers/polling.html)
* 추가 **[!UICONTROL 선택]**

![chlimage_1-102](assets/chlimage_1-102.png)

* **[!UICONTROL 유형]**: *(필수)* 풀다운하여 선택 `POP3 (over SSL).`

* **[!UICONTROL URL]**:(필수) ** 아웃바운드 메일 서버입니다. 예, `pop.gmail.com:995/INBOX?username=community-emailgmail.com&password=****`

* **[!UICONTROL 패스로 가져오기]**(&amp;P);ast;: *(필수)* 폴더를 `/content/usergenerated/mailFolder/postEmails`검색하여 `postEmails`로 설정하고 **확인을 선택합니다.**

* **[!UICONTROL 업데이트 간격(초)]**:(선택 사항) ** 기본 메일 서비스에 대해 구성된 메일 서버에는 업데이트 간격 값에 대한 요구 사항이 있을 수 있습니다. 예를 들어 Gmail의 경우 간격이 필요할 수 `300`있습니다.

* **[!UICONTROL 로그인]**: *(선택 사항)*

* **[!UICONTROL 암호]**: *(선택 사항)*

* 확인 **[!UICONTROL 선택]**

### 새 폴링 가져오기를 위한 프로토콜 조정 {#adjust-protocol-for-new-polling-importer}

새 폴링 구성이 저장되면 프로토콜을 에서 `POP3` 로 변경하려면 구독 이메일 가져오기의 속성을 추가로 수정해야 합니다 `emailreply`

CRXDE [Lite 사용](../../help/sites-developing/developing-with-crxde-lite.md):

* 기본 게시자에서
* 관리자 권한으로 로그인
* https://&lt; [server>:&lt;port>/crx/de/index.jsp#/etc/importers/polling으로 이동합니다.](http://localhost:4503/crx/de/index.jsp#/etc/importers/polling)
* 새로 만든 구성 선택
* 다음 속성 수정

   * **feedType**:다음으로 `pop3s` 바꾸기 **`emailreply`**
   * **소스**:소스 프로토콜을 다음으로 `pop3s://` 바꾸기 **`emailreply://`**

![chlimage_1-103](assets/chlimage_1-103.png)

빨간색 삼각형은 수정된 속성을 나타냅니다. 다음 변경 사항을 저장해야 합니다.

* 모두 **[!UICONTROL 저장을 선택합니다.]**

