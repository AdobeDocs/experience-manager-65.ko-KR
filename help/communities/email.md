---
title: 이메일 구성
description: Adobe Experience Manager 커뮤니티에 대한 이메일 알림 및 구독을 구성하는 방법을 알아봅니다.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
pagetitle: Configuring Email
role: Admin
exl-id: bf97d388-f8ca-4e37-88e2-0c536834311e
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 0%

---

# 이메일 구성 {#configuring-email}

AEM Communities은 다음에 대해 이메일을 사용합니다.

* [커뮤니티 알림](notifications.md)
* [커뮤니티 구독](subscriptions.md)

기본적으로 전자 메일 기능은 SMTP 서버 및 SMTP 사용자 지정이 필요하므로 작동하지 않습니다.

>[!CAUTION]
>
>알림 및 구독용 전자 메일은 [기본 게시자](deploy-communities.md#primary-publisher)에서만 구성해야 합니다.

## 기본 메일 서비스 구성 {#default-mail-service-configuration}

기본 메일 서비스는 알림과 구독 모두에 필요합니다.

* 관리자 권한으로 기본 게시자에 로그인하고 [웹 콘솔](../../help/sites-deploying/configuring-osgi.md)에 액세스합니다.

   * 예: [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* `Day CQ Mail Service`을(를) 찾습니다.
* 편집 아이콘을 선택합니다.

이는 [전자 메일 알림 구성](../../help/sites-administering/notification.md)에 대한 설명서를 기반으로 하지만 `"From" address` 필드가 *필요 없음*&#x200B;이라는 차이점이 있으며 비어 있어야 합니다.

예(설명 목적으로만 값 입력):

![전자 메일 구성](assets/email-config.png)

* **[!UICONTROL SMTP 서버 호스트 이름]**

  *(필수)* 사용할 SMTP 서버입니다.

* **[!UICONTROL SMTP 서버 포트]**

  *(필수)* SMTP 서버 포트는 25 이상이어야 합니다.

* **[!UICONTROL SMTP 사용자]**

  *(필수)* SMTP 사용자.

* **[!UICONTROL SMTP 암호]**

  *(필수)* SMTP 사용자의 암호입니다.

* **[!UICONTROL &quot;보낸 사람&quot; 주소]**

  비워 둠
* **[!UICONTROL SMTP SSL 사용]**

  선택하면 보안 이메일을 전송합니다. 포트가 465로 설정되었는지 또는 SMTP 서버의 필요에 따라 설정되었는지 확인합니다.
* **[!UICONTROL 전자 메일 디버그]**

  선택하면 SMTP 서버 상호 작용 로깅이 활성화됩니다.

## AEM Communities 이메일 구성 {#aem-communities-email-configuration}

[기본 메일 서비스](#default-mail-service-configuration)가 구성되면 릴리스에 포함된 `AEM Communities Email Reply Configuration` OSGi 구성의 두 기존 인스턴스가 작동합니다.

이메일을 통한 회신을 허용할 경우 구독에 대한 인스턴스만 추가로 구성해야 합니다.

1. [전자 메일](#configuration-for-notifications) 인스턴스:

   회신 이메일을 지원하지 않으므로 변경하지 말아야 합니다.

1. [구독-이메일](#configuration-for-subscriptions) 인스턴스:

   회신 이메일에서 게시물을 만드는 것을 완전히 활성화하려면 구성이 필요합니다.

커뮤니티 이메일 구성 인스턴스에 도달하려면 다음을 수행하십시오.

* 관리자 권한으로 기본 게시자에 로그인하고 [웹 콘솔](../../help/sites-deploying/configuring-osgi.md)에 액세스합니다.

   * 예: [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* `AEM Communities Email Reply Configuration` 찾기.

![email-reply-config](assets/email-reply-config.png)

### 알림 구성 {#configuration-for-notifications}

이름 전자 메일이 포함된 `AEM Communities Email Reply Configuration` OSGi 구성의 인스턴스는 증명 기능입니다. 이 기능에는 이메일 회신이 포함되어 있지 않습니다.

이 구성을 변경하지 마십시오.

* `AEM Communities Email Reply Configuration`을(를) 찾습니다.
* 편집 아이콘을 선택합니다.
* **Name**&#x200B;이(가) `email`인지 확인하십시오.

* **회신 전자 메일로 게시물 만들기**&#x200B;가 `unchecked`인지 확인하십시오.

![configure-email-reply](assets/configure-email-reply.png)

### 구독에 대한 구성 {#configuration-for-subscriptions}

커뮤니티 구독의 경우 구성원이 전자 메일에 회신하여 콘텐츠를 게시하는 기능을 활성화하거나 비활성화할 수 있습니다.

* `AEM Communities Email Reply Configuration`을(를) 찾습니다.
* 편집 아이콘을 선택합니다.
* **Name**&#x200B;이(가) `subscriptions-email`인지 확인하십시오.

  ![configure-email-subscription](assets/configure-email-subscriptions.png)

* **[!UICONTROL 이름]**

  *(필수)* `subscriptions-email`. 편집하지 마십시오.

* **[!UICONTROL 회신 전자 메일에서 게시물 만들기]**

  선택하면 구독 이메일 수신자가 회신을 보내 콘텐츠를 게시할 수 있습니다. 기본값은 선택되어 있습니다.
* **[!UICONTROL 추적된 ID를 헤더에 추가]**

  기본값은 `Reply-To`입니다.

* **[!UICONTROL 제목의 최대 길이]**

  추적기 ID가 제목 줄에 추가된 경우, 이는 추적된 ID를 제외하고 제목의 최대 길이이며, 그 후에는 이 ID가 트림됩니다. 이는 추적된 ID 정보가 손실되지 않도록 가능한 한 작아야 합니다. 기본값은 200입니다.

* **[!UICONTROL &quot;회신&quot; 전자 메일 주소]**

  &quot;회신&quot; 이메일 주소로 사용되는 주소. 기본값은 `no-reply@example.com`입니다.

* **[!UICONTROL 회신 구분 기호]**

  추적기 ID를 회신 주소 헤더에 추가한 경우, 이 구분 기호가 사용됩니다. 기본값은 `+`(더하기 기호)입니다.

* **[!UICONTROL 제목의 추적기 ID 접두사]**

  추적기 ID를 제목 줄에 추가한 경우 이 접두사가 사용됩니다. 기본값은 `post#`입니다.

* **[!UICONTROL 메시지 본문의 추적기 ID 접두사]**

  추적기 ID를 메시지 본문에 추가하면 이 접두사가 사용됩니다. 기본값은 `Please do not remove this:`입니다.

* **[!UICONTROL 전자 메일을 HTML으로]**: 확인 표시가 되어 있으면 전자 메일의 콘텐츠 유형이 `"text/html;charset=utf-8"`(으)로 설정됩니다. 기본값은 선택되어 있습니다.

* **[!UICONTROL 기본 사용자 이름]**

  이 이름은 이름 없는 사용자에게 사용됩니다. 기본값은 `no-reply@example.com`입니다.

* **[!UICONTROL 템플릿 루트 경로]**

  이메일은 이 루트 경로에 저장된 템플릿을 사용하여 작성됩니다. 기본값은 `/etc/community/templates/subscriptions-email`입니다.

## 폴링 가져오기 구성 {#configure-polling-importer}

이메일을 저장소로 가져오려면 폴링 가져오기를 구성하고 저장소에서 해당 속성을 수동으로 구성해야 합니다.

### 새 폴링 가져오기 추가 {#add-new-polling-importer}

* 관리자 권한으로 기본 게시자에 로그인하고 폴링 가져오기 콘솔로 이동합니다.

  예: [http://localhost:4503/etc/importers/polling.html](http://localhost:4503/etc/importers/polling.html)

* **[!UICONTROL 추가]** 선택

  ![polling-importer](assets/polling-importer.png)

* **[!UICONTROL 유형]**

  *(필수)* 아래로 끌어다 놓아 `POP3 (over SSL)`을(를) 선택합니다.

* **[!UICONTROL URL]**

  *(필수)* 아웃바운드 메일 서버입니다. 예: `pop.gmail.com:995/INBOX?username=community-emailgmail.com&password=****`

* **[!UICONTROL 경로로 가져오기]**&amp;ast;

  *(필수)*&#x200B;이(가) `/content/usergenerated/mailFolder/postEmails`(으)로 설정됨
`postEmails`폴더를 찾아 **확인**&#x200B;을 선택합니다.

* **[!UICONTROL 업데이트 간격(초)]**

  *(선택 사항)* 기본 메일 서비스에 대해 구성된 메일 서버에 업데이트 간격 값에 대한 요구 사항이 있을 수 있습니다. 예를 들어 Gmail에는 `300` 간격이 필요할 수 있습니다.

* **[!UICONTROL 로그인]**

  *(선택 사항)*

* **[!UICONTROL 암호]**

  *(선택 사항)*

* **[!UICONTROL 확인]**&#x200B;을 선택합니다.

### 새 Polling Importer에 대한 프로토콜 조정 {#adjust-protocol-for-new-polling-importer}

새 폴링 구성이 저장되면 구독 전자 메일 가져오기의 속성을 추가로 수정하여 프로토콜을 `POP3`에서 `emailreply`(으)로 변경해야 합니다.

[CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) 사용:

* 관리자 권한으로 기본 게시자에 로그인하고 [https://&lt;server>:&lt;port>/crx/de/index.jsp#/etc/importers/polling](http://localhost:4503/crx/de/index.jsp#/etc/importers/polling)(으)로 이동합니다.
* 새로 생성된 구성을 선택하고 다음 속성을 수정합니다.

   * **feedType**: `pop3s`을(를) **`emailreply`**(으)로 바꾸기
   * **소스**: 소스의 프로토콜 `pop3s://`을(를) **`emailreply://`**(으)로 바꾸기

![폴링 프로토콜](assets/polling-protocol.png)

빨간색 삼각형은 수정된 속성을 나타냅니다. 변경 사항을 저장하십시오.

* **[!UICONTROL 모두 저장]**&#x200B;을 선택합니다.
