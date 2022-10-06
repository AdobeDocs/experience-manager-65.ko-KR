---
title: 전자 메일 알림 구성
seo-title: Configuring Email Notification
description: AEM에서 이메일 알림을 구성하는 방법을 알아봅니다.
seo-description: Learn how to configure Email Notification in AEM.
uuid: 6cbdc312-860b-4a69-8bbe-2feb32204a27
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 6466d7b8-e308-43c5-acdc-dec15f796f64
exl-id: 918fcbbc-a78a-4fab-a933-f183ce6a907f
source-git-commit: ea5abbbe8f928a63b7d3d6f96f3007a3c82706e0
workflow-type: tm+mt
source-wordcount: '2116'
ht-degree: 12%

---

# 전자 메일 알림 구성{#configuring-email-notification}

AEM에서 다음과 같은 사용자에게 이메일 알림을 보냅니다.

* 수정 또는 복제와 같은 페이지 이벤트에 가입했습니다. 다음 [알림 받은 편지함](/help/sites-classic-ui-authoring/author-env-inbox.md#subscribing-to-notifications) 섹션에서 해당 이벤트에 가입하는 방법을 설명합니다.

* 포럼 이벤트를 구독했습니다.
* 워크플로우에서 단계를 수행해야 합니다. 다음 [참가자 단계](/help/sites-developing/workflows-step-ref.md#participant-step) 섹션에서 워크플로우에서 이메일 알림을 트리거하는 방법을 설명합니다.

전제 조건:

* 사용자의 프로필에 유효한 이메일 주소가 정의되어 있어야 합니다.
* 다음 **일 CQ 메일 서비스** 를 올바르게 구성해야 합니다.

사용자에게 알림이 전송되면 프로필에 정의된 언어로 이메일을 받게 됩니다. 각 언어에는 사용자 지정할 수 있는 자체 템플릿이 있습니다. 새 언어에 대한 새 이메일 템플릿을 추가할 수 있습니다.

>[!NOTE]
>
>AEM을 사용하여 작업하는 경우 이러한 서비스에 대한 구성 설정을 관리하는 방법에는 몇 가지가 있습니다. 참조 [OSGi 구성](/help/sites-deploying/configuring-osgi.md) 자세한 내용 및 권장 지침

## 메일 서비스 구성 {#configuring-the-mail-service}

AEM에서 이메일을 보내려면 **일 CQ 메일 서비스** 를 올바르게 구성해야 합니다. 웹 콘솔에서 구성을 볼 수 있습니다. AEM을 사용하여 작업하는 경우 이러한 서비스에 대한 구성 설정을 관리하는 방법에는 몇 가지가 있습니다. 참조 [OSGi 구성](/help/sites-deploying/configuring-osgi.md) 자세한 내용 및 권장 지침

다음 제한 사항이 적용됩니다.

* 다음 **SMTP 서버 포트** 는 25 이상이어야 합니다.

* 다음 **SMTP 서버 호스트 이름** 비워 둘 수 없습니다.
* 다음 **&quot;보낸 사람&quot; 주소** 비워 둘 수 없습니다.

을 사용하여 문제를 디버깅하는 데 도움이 되도록 **일 CQ 메일 서비스**, 서비스 로그를 볼 수 있습니다.

`com.day.cq.mailer.DefaultMailService`

구성은 웹 콘솔에서 다음과 같습니다.

![chlimage_1-276](assets/chlimage_1-276.png)

## 이메일 알림 채널 구성 {#configuring-the-email-notification-channel}

페이지 또는 포럼 이벤트 알림에 구독하면 보낸 메일 주소가 `no-reply@acme.com` 기본적으로 사용됩니다. 이 값은 **알림 이메일 채널** 서비스를 클릭합니다.

이메일 주소를 구성하려면 `sling:OsgiConfig` 노드에 대한 섹션을 참조하십시오. CRXDE Lite을 사용하여 노드를 직접 추가하려면 다음 절차를 따르십시오.

1. CRXDE Lite에서 `config` 아래의 애플리케이션 폴더를 참조하십시오.
1. 구성 폴더에서 다음 노드를 추가합니다.

   `com.day.cq.wcm.notification.email.impl.EmailChannel` 유형 `sling:OsgiConfig`

1. 추가 `String` 이름이 지정된 노드에 대한 속성 `email.from`. 값에 사용할 이메일 주소를 지정합니다.

1. 클릭 **모두 저장**.

다음 절차를 사용하여 컨텐츠 패키지 소스 폴더에서 노드를 정의합니다.

1. 사용자 `jcr_root/apps/*app_name*/config folder`로 명명된 파일을 만듭니다. `com.day.cq.wcm.notification.email.impl.EmailChannel.xml`

1. 노드를 나타내려면 다음 XML을 추가하십시오.

   `<?xml version="1.0" encoding="UTF-8"?> <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0" jcr:primaryType="sling:OsgiConfig" email.from="name@server.com"/>`
1. 의 값 바꾸기 `email.from` 특성( `name@server.com`)에 사용할 수 있습니다.

1. 파일을 저장합니다.

## 워크플로우 이메일 알림 서비스 구성 {#configuring-the-workflow-email-notification-service}

워크플로우 이메일 알림을 받으면 보낸 사람 이메일 주소와 호스트 URL 접두사가 모두 기본값으로 설정됩니다. 이러한 값은 **Day CQ Workflow Email Notification Service** 참조하십시오. 이 경우 리포지토리에서 변경 사항을 유지하는 것이 좋습니다.

기본 구성은 웹 콘솔에서 다음과 같습니다.

![chlimage_1-277](assets/chlimage_1-277.png)

### 페이지 알림용 이메일 템플릿 {#email-templates-for-page-notification}

페이지 알림용 이메일 템플릿은 아래에 있습니다.

`/libs/settings/notification-templates/com.day.cq.wcm.core.page`

기본 영어 템플릿( `en.txt`)은 다음과 같이 정의됩니다.

```xml
subject=[CQ Page Event Notification]: Page Event

header=-------------------------------------------------------------------------------------\n \
Time: ${time}\n \
User: ${userFullName} (${userId})\n \
-------------------------------------------------------------------------------------\n\n

message=The following pages were affected by the event: \n \
 \n \
${modifications} \n \
 \n\n
footer=\n \
-------------------------------------------------------------------------------------\n \
This is an automatically generated message. Please do not reply.
```

#### 페이지 알림에 대한 이메일 템플릿 사용자 정의 {#customizing-email-templates-for-page-notification}

페이지 알림에 대한 영어 이메일 템플릿을 사용자 지정하는 방법은 다음과 같습니다.

1. CRXDE에서 파일을 엽니다.

   `/libs/settings/notification-templates/com.day.cq.wcm.core.page/en.txt`

1. 필요에 따라 파일을 수정합니다.
1. 변경 사항을 저장합니다.

템플릿에는 다음 형식이 있어야 합니다.

```
 subject=<text_1>
 header=<text_2>
 message=<text_3>
 footer=<text_4>
```

위치 &lt;text_x> 정적 텍스트와 동적 문자열 변수를 혼합하여 사용할 수 있습니다. 페이지 알림의 이메일 템플릿 내에서 다음 변수를 사용할 수 있습니다.

* `${time}`, 이벤트 날짜 및 시간을 지정합니다.

* `${userFullName}`: 이벤트를 트리거한 사용자의 전체 이름입니다.

* `${userId}`: 이벤트를 트리거한 사용자의 ID입니다.
* `${modifications}`에서는 페이지 이벤트 유형 및 페이지 경로를 형식으로 설명합니다.

   &lt;page event=&quot;&quot; type=&quot;&quot;> => &lt;page path=&quot;&quot;>

   예:

   PageModified => /content/geometrixx/en/products

### 포럼 알림용 이메일 템플릿 {#email-templates-for-forum-notification}

포럼 알림용 이메일 템플릿은 다음 위치에 있습니다.

`/etc/notification/email/default/com.day.cq.collab.forum`

기본 영어 템플릿( `en.txt`)은 다음과 같이 정의됩니다.

```xml
subject=[CQ Forum Notification]

header=-------------------------------------------------------------------------------------\n \
Time: Time: ${time}\n \
Forum Page Path: ${forum.path}\n \
-------------------------------------------------------------------------------------\n\n

message=Page: ${host.prefix}${forum.path}.html\n

footer=\n \
-------------------------------------------------------------------------------------\n \
This is an automatically generated message. Please do not reply.
```

#### 포럼 알림용 이메일 템플릿 사용자 정의 {#customizing-email-templates-for-forum-notification}

포럼 알림에 대한 영어 이메일 템플릿을 사용자 지정하려면 다음을 수행하십시오.

1. CRXDE에서 파일을 엽니다.

   `/etc/notification/email/default/com.day.cq.collab.forum/en.txt`

1. 필요에 따라 파일을 수정합니다.
1. 변경 사항을 저장합니다.

템플릿에는 다음 형식이 있어야 합니다.

```
 subject=<text_1>
 header=<text_2>
 message=<text_3>
 footer=<text_4>
```

위치 `<text_x>` 정적 텍스트와 동적 문자열 변수를 혼합하여 사용할 수 있습니다.

포럼 알림에 대해 이메일 템플릿 내에서 다음 변수를 사용할 수 있습니다.

* `${time}`, 이벤트 날짜 및 시간을 지정합니다.

* `${forum.path}`를 채울 수 있습니다.

### 워크플로우 알림용 이메일 템플릿 {#email-templates-for-workflow-notification}

워크플로우 알림에 대한 이메일 템플릿(영어)은 다음 위치에 있습니다.

`/libs/settings/workflow/notification/email/default/en.txt`

다음과 같이 정의됩니다.

```xml
subject=Workflow notification: ${event.EventType}

header=-------------------------------------------------------------------------------------\n \
Time: ${event.TimeStamp}\n \
Step: ${item.node.title}\n \
User: ${participant.name} (${participant.id})\n \
Workflow: ${model.title}\n \
-------------------------------------------------------------------------------------\n\n

message=Content: ${host.prefix}${payload.path.open}\n

footer=\n \
-------------------------------------------------------------------------------------\n \
View the overview in your ${host.prefix}/aem/inbox\n \
-------------------------------------------------------------------------------------\n \
This is an automatically generated message. Please do not reply.
```

#### 워크플로우 알림에 대한 이메일 템플릿 사용자 정의 {#customizing-email-templates-for-workflow-notification}

워크플로우 이벤트 알림에 대한 영어 이메일 템플릿을 사용자 정의하려면

1. CRXDE에서 파일을 엽니다.

   `/libs/settings/workflow/notification/email/default/en.txt`

1. 필요에 따라 파일을 수정합니다.
1. 변경 사항을 저장합니다.

템플릿에는 다음 형식이 있어야 합니다.

```
subject=<text_1>
 header=<text_2>
 message=<text_3>
 footer=<text_4>
```

>[!NOTE]
>
>위치 `<text_x>` 정적 텍스트와 동적 문자열 변수를 혼합하여 사용할 수 있습니다. 각 행 `<text_x>` 항목은 백슬래시로 끝나야 합니다. `\`). 마지막 인스턴스를 제외하고, 백슬래시가 없으면 `<text_x>` 문자열 변수를 채우는 방법을 설명합니다.
>
>템플릿 형식에 대한 자세한 내용은 [Properties.load()의 javadocs](https://docs.oracle.com/javase/8/docs/api/java/util/Properties.html#load-java.io.InputStream-) 메서드를 사용합니다.

메서드 `${payload.path.open}` 작업 항목의 페이로드에 대한 경로를 표시합니다. 예를 들어 Sites의 페이지에 대해 다음 작업을 수행합니다 `payload.path.open` 과 비슷합니다 `/bin/wcmcommand?cmd=open&path=…`.; 서버 이름이 없으므로 템플릿 접두사가 `${host.prefix}`.

이메일 템플릿 내에서 다음 변수를 사용할 수 있습니다.

* `${event.EventType}`, 이벤트 유형
* `${event.TimeStamp}`, 이벤트 날짜 및 시간
* `${event.User}`, 이벤트를 트리거한 사용자
* `${initiator.home}`, 개시자 노드 경로

* `${initiator.name}`, 이니시에이터 이름

* `${initiator.email}`, 개시자의 이메일 주소
* `${item.id}`, 작업 항목의 id
* `${item.node.id}`, 이 작업 항목과 연결된 워크플로우 모델의 노드 id
* `${item.node.title}`, 작업 항목의 제목
* `${participant.email}`, 참가자의 이메일 주소
* `${participant.name}`, 참여자의 이름
* `${participant.familyName}`, 참여자의 가족명
* `${participant.id}`, 참여자의 id
* `${participant.language}`, 참가자 언어
* `${instance.id}`, 워크플로우 id
* `${instance.state}`, 워크플로우 상태
* `${model.title}`, 워크플로우 모델의 제목
* `${model.id}`, 워크플로우 모델의 id

* `${model.version}`, 워크플로우 모델의 버전
* `${payload.data}`, 페이로드

* `${payload.type}`, 페이로드 유형
* `${payload.path}`, 페이로드 경로
* `${host.prefix}`, 호스트 접두사, 예: http://localhost:4502

### 새 언어용 이메일 템플릿 추가 {#adding-an-email-template-for-a-new-language}

새 언어의 템플릿을 추가하려면 다음을 수행합니다.

1. CRXDE에서 파일을 추가합니다 `<language-code>.txt` 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래 아래

   * `/libs/settings/notification-templates/com.day.cq.wcm.core.page` : 페이지 알림용
   * `/etc/notification/email/default/com.day.cq.collab.forum` : 포럼 알림용
   * `/libs/settings/workflow/notification/email/default` : 워크플로우 알림용

1. 언어에 맞게 파일을 조정합니다.
1. 변경 사항을 저장합니다.

>[!NOTE]
>
>다음 `<language-code>` 전자 메일 템플릿의 파일 이름으로 사용되는 경우 AEM에서 인식하는 두 글자 하위 언어 코드가 있어야 합니다. 언어 코드의 경우 AEM은 ISO-639-1을 사용합니다.

## AEM Assets 이메일 알림 구성 {#assetsconfig}

AEM Assets의 컬렉션이 공유되거나 공유되지 않으면 사용자는 AEM에서 이메일 알림을 받을 수 있습니다. 이메일 알림을 구성하려면 다음 단계를 수행합니다.

1. 위에 설명된 대로 이메일 서비스를 구성합니다. [메일 서비스 구성](/help/sites-administering/notification.md#configuring-the-mail-service).
1. 관리자로 AEM에 로그인합니다. 클릭 **도구** >  **작업** >  **웹 콘솔** 웹 콘솔 구성을 엽니다.
1. 편집 **일 CQ DAM 리소스 수집 서블릿**. 선택 **전자 메일 보내기**. **저장**&#x200B;을 클릭합니다.

## OAuth 설정 {#setting-up-oauth}

AEM은 조직이 보안 이메일 요구 사항을 준수할 수 있도록 통합 Mail Service에 대한 OAuth2 지원을 제공합니다.

아래에 설명된 대로 여러 이메일 공급자에 대해 OAuth를 구성할 수 있습니다.

>[!NOTE]
>
>이 절차는 게시 인스턴스의 예제입니다. 작성자 인스턴스에서 이메일 알림을 활성화하려면 작성자에서 동일한 단계를 따라야 합니다.

### Gmail {#gmail}

1. 에서 프로젝트를 만듭니다. `https://console.developers.google.com/projectcreate`
1. 프로젝트를 선택한 다음 **API 및 서비스** - **대시보드 - 자격 증명**
1. 요구 사항에 따라 OAuth 동의 화면 구성
1. 다음에 나오는 업데이트 화면에서 다음 두 범위를 추가합니다.
   * `https://mail.google.com/`
   * `https://www.googleapis.com//auth/gmail.send`
1. 범위를 추가했으면 다시 로 이동합니다 **자격 증명** 왼쪽 메뉴에서 **자격 증명 만들기** - **OAuth 클라이언트 ID** - **데스크탑 앱**
1. 클라이언트 ID 및 클라이언트 암호가 포함된 새 창이 열립니다.
1. 자격 증명을 저장합니다.

**AEM 측 구성**

>[!NOTE]
>
>Adobe 관리 서비스 고객은 고객 서비스 엔지니어와 협력하여 프로덕션 환경을 변경할 수 있습니다.

먼저 메일 서비스를 구성합니다.

1. 로 이동하여 AEM 웹 콘솔을 엽니다. `http://serveraddress:serverport/system/console/configMgr`
1. 을(를) 찾은 다음 을(를) 클릭합니다. **일 CQ 메일 서비스**
1. 다음 설정을 추가합니다.
   * SMTP 서버 호스트 이름: `smtp.gmail.com`
   * SMTP 서버 포트: `25` 또는 `587`, 요구 사항에 따라
   * 티켓에 대한 **SMPT에서 StarTLS 사용** 및 **SMTP에는 StarTLS가 필요합니다.**
   * 확인 **OAuth 흐름** 을(를) 클릭합니다. **저장**.

그런 다음 아래 절차에 따라 SMTP OAuth 공급자를 구성합니다.

1. 로 이동하여 AEM 웹 콘솔을 엽니다. `http://serveraddress:serverport/system/console/configMgr`
1. 을(를) 찾은 다음 을(를) 클릭합니다. **CQ Mail SMTP OAuth2 공급자**
1. 다음과 같이 필요한 정보를 입력합니다.
   * 인증 URL: `https://accounts.google.com/o/oauth2/auth`
   * 토큰 URL: `https://accounts.google.com/o/oauth2/token`
   * 범위: `https://www.googleapis.com/auth/gmail.send` 및 `https://mail.google.com/`. 를 눌러 두 개 이상의 범위를 추가할 수 있습니다 **+** 구성된 각 범위의 오른쪽에 있는 단추입니다.
   * 클라이언트 ID 및 클라이언트 암호: 위의 단락에 설명된 대로 검색한 값으로 이러한 필드를 구성합니다.
   * 새로 고침 토큰 URL: `https://accounts.google.com/o/oauth2/token`
   * 새로 고침 토큰 만료: 절대
1. **저장**&#x200B;을 클릭합니다.

<!-- clarify refresh token expiry, currrently not present in the UI -->

구성이 완료되면 설정은 다음과 같습니다.

![oauth smtp 공급자](assets/oauth-smtpprov2.png)

이제 OAuth 구성 요소를 활성화합니다. 다음을 통해 이 작업을 수행할 수 있습니다.

1. 다음 URL을 방문하여 구성 요소 콘솔로 이동합니다. `http://serveraddress:serverport/system/console/components`
1. 다음 구성 요소를 찾습니다
   * `com.day.cq.mailer.oauth.servlets.handler.OAuthCodeGenerateServlet`
   * `com.day.cq.mailer.oauth.servlets.handler.OAuthCodeAccessTokenGenerator`
1. 구성 요소 왼쪽에 있는 재생 아이콘을 누릅니다

   ![구성 요소](assets/oauth-components-play.png)

마지막으로 다음 방법으로 구성을 확인합니다.

1. 게시 인스턴스의 주소로 이동하고 관리자로 로그인합니다.
1. 브라우저에서 새 탭을 열고 다음 위치로 이동합니다. `http://serveraddress:serverport/services/mailer/oauth2/authorize`. 이렇게 하면 SMTP 공급자의 페이지로 리디렉션됩니다(이 경우 Gmail).
1. 필요한 권한을 부여하는 로그인 및 동의
1. 동의하면 토큰이 저장소에 저장됩니다. 아래에 액세스할 수 있습니다 `accessToken` 게시 인스턴스에서 이 URL에 직접 액세스하여 다음 작업을 수행할 수 있습니다. `http://serveraddress:serverport/crx/de/index.jsp#/conf/global/settings/mailer/oauth`
1. 각 게시 인스턴스에 대해 위의 를 반복합니다

<!-- clarify if the ip/server address in the last procedure is that of the publish instance -->

### Microsoft Outlook {#microsoft-outlook}

1. [https://portal.azure.com/](https://portal.azure.com/)으로 이동한 다음 로그인합니다.
1. 검색창에서 **Azure Active Directory**&#x200B;를 검색한 다음 결과를 클릭합니다. 또는 [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)에서 바로 검색할 수 있습니다.
1. **앱 등록** - **신규 등록**&#x200B;을 클릭합니다.

   ![](assets/oauth-outlook1.png)

1. 요구 사항에 따라 정보를 입력한 다음 **등록**&#x200B;을 클릭합니다.
1. 새로 생성된 앱으로 이동하여 **API 권한**&#x200B;을 선택합니다.
1. **권한 추가** - **그래프 권한** - **위임된 권한**&#x200B;으로 이동합니다.
1. 아래의 앱에 대한 권한을 선택한 다음 **권한 추가**&#x200B;를 클릭합니다.
   * `SMTP.Send`
   * `Mail.Read`
   * `Mail.Send`
   * `openid`
   * `offline_access`
1. 이동 **인증** - **플랫폼 추가** - **웹**, 및에서 **리디렉션 Url** 섹션에서 OAuth 코드를 리디렉션하기 위한 다음 URL을 추가한 다음 키를 누릅니다 **구성**:
   * `http://localhost:4503/services/mailer/oauth2/token`
1. 각 게시 인스턴스에 대해 위의 를 반복합니다
1. 요구 사항에 따라 설정을 구성합니다
1. 그런 다음 **증명서 및 보안**&#x200B;으로 이동하고 **신규 클라이언트 보안**&#x200B;을 클릭한 후 화면에 표시되는 단계에 따라 보안을 생성합니다. 나중에 사용할 수 있도록 이러한 보안 내용을 메모해 두십시오.
1. 왼쪽 창에서 **개요**&#x200B;를 누르고 나중에 사용할 수 있도록 **애플리케이션(클라이언트) ID** 및 **디렉터리(테넌트) ID**&#x200B;의 값을 복사합니다.

다시 매핑하려면 AEM 측에서 Mail 서비스에 대해 OAuth2를 구성하려면 다음 정보가 필요합니다.

* 테넌트 ID로 구성되는 인증 URL 형식: `https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/authorize`
* 테넌트 ID로 구성되는 토큰 URL 형식: `https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/token`
* 테넌트 ID로 구성되는 새로 고침 URL 형식: `https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/token`
* 클라이언트 ID
* 클라이언트 보안

**AEM 측 구성**

다음으로, OAuth2 설정을 AEM과 통합합니다.

1. 로 이동하여 로컬 인스턴스의 웹 콘솔로 이동합니다. `http://serveraddress:serverport/system/console/configMgr`
1. 을(를) 찾고 을(를) 클릭합니다. **일 CQ 메일 서비스**
1. 다음 설정을 추가합니다.
   * SMTP 서버 호스트 이름: `smtp.office365.com`
   * SMTP 사용자: 이메일 형식의 사용자 이름
   * &quot;보낸 사람&quot; 주소: 메일러가 보낸 메시지의 &quot;보낸 사람:&quot; 필드에 사용할 전자 메일 주소입니다
   * SMTP 서버 포트: `25` 또는 `587` 요구 사항에 따라
   * 티켓에 대한 **SMPT에서 StarTLS 사용** 및 **SMTP에는 StarTLS가 필요합니다.**
   * 확인 **OAuth 흐름** 을(를) 클릭합니다. **저장**.
1. 을(를) 찾은 다음 을(를) 클릭합니다. **CQ Mail SMTP OAuth2 공급자**
1. 다음과 같이 필요한 정보를 입력합니다.
   * 에 설명된 대로 인증 URL, 토큰 Url 및 새로 고침 토큰 URL을 구성하여 입력합니다. [이 절차의 끝](#microsoft-outlook)
   * 클라이언트 ID 및 클라이언트 암호: 위에서 설명한 대로 검색한 값으로 이러한 필드를 구성합니다.
   * 구성에 다음 범위를 추가합니다.
      * openid
      * offline_access
      * `https://outlook.office365.com/Mail.Send`
      * `https://outlook.office365.com/Mail.Read`
      * `https://outlook.office365.com/SMTP.Send`
   * AuthCode 리디렉션 Url: `http://localhost:4503/services/mailer/oauth2/token`
   * 새로 고침 토큰 URL: 위의 토큰 URL과 동일한 값이 있어야 합니다
1. **저장**&#x200B;을 클릭합니다.

구성이 완료되면 설정은 다음과 같습니다.

![](assets/oauth-outlook-smptconfig.png)

이제 OAuth 구성 요소를 활성화합니다. 다음을 통해 이 작업을 수행할 수 있습니다.

1. 다음 URL을 방문하여 구성 요소 콘솔로 이동합니다. `http://serveraddress:serverport/system/console/components`
1. 다음 구성 요소를 찾습니다
   * `com.day.cq.mailer.oauth.servlets.handler.OAuthCodeGenerateServlet`
   * `com.day.cq.mailer.oauth.servlets.handler.OAuthCodeAccessTokenGenerator`
1. 구성 요소 왼쪽에 있는 재생 아이콘을 누릅니다

![구성 요소2](assets/oauth-components-play.png)

마지막으로 다음 방법으로 구성을 확인합니다.

1. 게시 인스턴스의 주소로 이동하고 관리자로 로그인합니다.
1. 브라우저에서 새 탭을 열고 다음 위치로 이동합니다. `http://serveraddress:serverport/services/mailer/oauth2/authorize`. 이렇게 하면 SMTP 공급자의 페이지로 리디렉션됩니다(이 경우 Gmail).
1. 필요한 권한을 부여하는 로그인 및 동의
1. 동의하면 토큰이 저장소에 저장됩니다. 아래에 액세스할 수 있습니다 `accessToken` 게시 인스턴스에서 이 URL에 직접 액세스하여 다음 작업을 수행할 수 있습니다. `http://serveraddress:serverport/crx/de/index.jsp#/conf/global/settings/mailer/oauth`