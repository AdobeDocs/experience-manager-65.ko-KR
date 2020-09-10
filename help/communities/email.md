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
source-git-commit: 50c1532b2bdc41555eff2be718cd478aad1f403a
workflow-type: tm+mt
source-wordcount: '822'
ht-degree: 2%

---


# 이메일 구성 {#configuring-email}

AEM Communities은 이메일을 사용합니다.

* [커뮤니티 알림](notifications.md)
* [커뮤니티 구독](subscriptions.md)

기본적으로 이메일 기능은 SMTP 서버 및 SMTP 사용자의 사양이 필요하므로 작동하지 않습니다.

>[!CAUTION]
>
>알림 및 구독에 대한 이메일은 [기본 게시자에서만 구성해야 합니다](deploy-communities.md#primary-publisher).


## 기본 메일 서비스 구성 {#default-mail-service-configuration}

기본 메일 서비스는 알림과 구독 모두에 필요합니다.

* 관리자 권한으로 기본 게시자에 로그인하고 [웹 콘솔에 액세스합니다](../../help/sites-deploying/configuring-osgi.md).

   * 예: [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* 를 `Day CQ Mail Service`찾습니다.
* 편집 아이콘을 선택합니다.

이메일 알림 [구성에 대한](../../help/sites-administering/notification.md)문서를 기반으로 하지만 필드가 필요하지 `"From" address` 않고 *비워 두어야* 한다는 점에서 차이가 있습니다.

예를 들어(실례만을 위해 값으로 채워짐):

![chlimage_1-98](assets/chlimage_1-98.png)

* **[!UICONTROL SMTP 서버 호스트 이름]**

   *(필수)* 사용할 SMTP 서버입니다.

* **[!UICONTROL SMTP 서버 포트]**

   *(필수)* SMTP 서버 포트는 25 이상이어야 합니다.

* **[!UICONTROL SMTP 사용자]**

   *(필수)* SMTP 사용자입니다.

* **[!UICONTROL SMTP 암호]**

   *(필수)* SMTP 사용자의 암호입니다.

* **[!UICONTROL &quot;보낸 사람&quot; 주소]**

   비어 있음
* **[!UICONTROL SMTP SSL 사용]**

   이 확인란을 선택하면 보안 이메일을 보냅니다. 포트가 465로 설정되어 있거나 SMTP 서버의 필요에 따라 설정되어 있는지 확인합니다.
* **[!UICONTROL 이메일 디버그]**

   이 확인란을 선택하면 SMTP 서버 상호 작용의 로깅을 활성화합니다.

## AEM Communities 이메일 구성 {#aem-communities-email-configuration}

기본 메일 서비스 [가 구성되면](#default-mail-service-configuration) `AEM Communities Email Reply Configuration` 릴리스에 포함된 OSGi 구성의 기존 두 인스턴스가 작동합니다.

이메일로 회신을 허용할 때는 구독 인스턴스만 추가로 구성해야 합니다.

1. [이메일](#configuration-for-notifications) 인스턴스:

   회신 이메일을 지원하지 않는 알림의 경우, 변경하면 안 됩니다.

1. [구독-이메일](#configuration-for-subscriptions) 인스턴스:

   회신 이메일에서 게시물 작성을 완전히 활성화하려면 구성이 필요합니다.

커뮤니티 이메일 구성 인스턴스에 도달하려면 다음을 수행하십시오.

* 관리자 권한으로 기본 게시자에 로그인하고 [웹 콘솔에 액세스합니다.](../../help/sites-deploying/configuring-osgi.md)

   * 예: [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* 위치 `AEM Communities Email Reply Configuration`확인

![chlimage_1-99](assets/chlimage_1-99.png)

### 알림 구성 {#configuration-for-notifications}

이름 이메일이 `AEM Communities Email Reply Configuration` 있는 OSGi 구성 인스턴스는 형식 지정 기능입니다. 이 기능에는 이메일 회신이 포함되지 않습니다.

이 구성은 변경하지 마십시오.

* 를 `AEM Communities Email Reply Configuration`찾습니다.
* 편집 아이콘을 선택합니다.
* 이름이 **있는지** 확인합니다 `email`.

* 회신 **이메일에서 게시물** 만들기가 올바른지 확인합니다 `unchecked`.

![configure-email-response](assets/configure-email-reply.png)

### 가입 구성 {#configuration-for-subscriptions}

커뮤니티 구독의 경우, 회원이 이메일에 응답하여 컨텐츠를 게시할 수 있는 기능을 활성화하거나 비활성화할 수 있습니다.

* 를 `AEM Communities Email Reply Configuration`찾습니다.
* 편집 아이콘을 선택합니다.
* 이름이 **있는지** 확인합니다 `subscriptions-email`.

   ![configure-email-subscription](assets/configure-email-subscriptions.png)

* **[!UICONTROL 이름]**

   *(필수)* `subscriptions-email`. 편집하지 마십시오.

* **[!UICONTROL 회신 이메일로 게시물 만들기]**

   이 확인란을 선택하면 구독 이메일을 받은 사람이 회신을 통해 컨텐츠를 게시할 수 있습니다. 기본값은 선택되어 있습니다.
* **[!UICONTROL 헤더에 추적된 ID 추가]**

   기본값은 `Reply-To`입니다.

* **[!UICONTROL 제목의 최대 길이]**

   추적기 ID가 제목 줄에 추가된 경우 추적된 ID를 제외하고 제목의 최대 길이로, 그 뒤에 트리밍됩니다. 추적된 ID 정보가 손실되지 않도록 가능한 한 작게 표시되어야 합니다. 기본값은 200입니다.

* **[!UICONTROL &quot;회신&quot; 이메일 주소]**

   &quot;회신&quot; 이메일 주소로 사용되는 주소. 기본값은 `no-reply@example.com`입니다.

* **[!UICONTROL 회신 구분 기호]**

   추적기 ID가 회신 헤더에 추가된 경우 이 구분 기호가 사용됩니다. 기본값은 `+` (더하기 기호)입니다.

* **[!UICONTROL 제목에 추적기 ID 접두어]**

   추적기 ID가 제목 줄에 추가된 경우 이 접두어가 사용됩니다. 기본값은 `post#`입니다.

* **[!UICONTROL 메시지 본문에 있는 추적기 ID 접두사]**

   추적기 ID가 메시지 본문에 추가된 경우 이 접두사가 사용됩니다. 기본값은 `Please do not remove this:`입니다.

* **[!UICONTROL HTML로 이메일]**:이 확인란을 선택하면 컨텐츠 유형의 이메일이 로 설정됩니다 `"text/html;charset=utf-8"`. 기본값은 선택되어 있습니다.

* **[!UICONTROL 기본 사용자 이름]**

   이 이름은 이름 사용자가 없을 때 사용됩니다. 기본값은 `no-reply@example.com`입니다.

* **[!UICONTROL 템플릿 루트 경로]**

   이메일은 이 루트 경로에 저장된 템플릿을 사용하여 작성합니다. 기본값은 `/etc/community/templates/subscriptions-email`입니다.

## 폴링 가져오기 구성 {#configure-polling-importer}

이메일을 저장소로 가져오려면 폴링 가져오기를 구성하고 저장소에서 속성을 수동으로 구성해야 합니다.

### 새 폴링 가져오기 추가 {#add-new-polling-importer}

* 관리자 권한으로 기본 게시자에 로그인하고 폴링 가져오기 콘솔로 이동합니다.

   예: [http://localhost:4503/etc/importers/polling.html](http://localhost:4503/etc/importers/polling.html)

* 추가 **[!UICONTROL 선택]**

   ![chlimage_1-102](assets/chlimage_1-102.png)

* **[!UICONTROL 유형]**

   *(필수)* 아래로 끌어 선택합니다 `POP3 (over SSL)`.

* **[!UICONTROL URL]**

   *(필수)* 아웃바운드 메일 서버입니다. 예, `pop.gmail.com:995/INBOX?username=community-emailgmail.com&password=****`.

* **[!UICONTROL 패스]**&#x200B;맵으로 가져오기;ast;

   *(필수)* 폴더 `/content/usergenerated/mailFolder/postEmails`를 검색하여 `postEmails`설정하고 **확인을 선택합니다**.

* **[!UICONTROL 업데이트 간격(초)]**

   *(선택 사항)* 기본 메일 서비스에 대해 구성된 메일 서버에는 업데이트 간격 값에 대한 요구 사항이 있을 수 있습니다. 예를 들어 Gmail은 간격을 필요로 할 수 `300`있습니다.

* **[!UICONTROL 로그인]**

   *(선택 사항입니다)*

* **[!UICONTROL 암호]**

   *(선택 사항입니다)*

* 확인을 **[!UICONTROL 선택합니다]**.

### 새 폴링 가져오기 프로토콜 조정 {#adjust-protocol-for-new-polling-importer}

새 폴링 구성이 저장되면, 프로토콜을 에서 `POP3` `emailreply`

CRXDE Lite [사용](../../help/sites-developing/developing-with-crxde-lite.md):

* 관리자 권한으로 기본 게시자에 로그인하고 https://&lt;server>:&lt;port>/crx/de/index.jsp#/etc/importers/polling [으로 이동합니다](http://localhost:4503/crx/de/index.jsp#/etc/importers/polling).
* 새로 만든 구성을 선택하고 다음 속성을 수정합니다.

   * **feedType**:다음으로 `pop3s` 바꾸기 **`emailreply`**
   * **소스**:소스 프로토콜 `pop3s://` 을 **`emailreply://`**

![chlimage_1-103](assets/chlimage_1-103.png)

빨간색 삼각형은 수정된 속성을 나타냅니다. 다음 변경 사항을 저장해야 합니다.

* 모두 **[!UICONTROL 저장을 선택합니다]**.

