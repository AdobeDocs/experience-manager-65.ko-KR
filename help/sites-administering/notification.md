---
title: 이메일 알림 구성
seo-title: 이메일 알림 구성
description: AEM에서 이메일 알림을 구성하는 방법을 알아봅니다.
seo-description: AEM에서 이메일 알림을 구성하는 방법을 알아봅니다.
uuid: 6cbdc312-860b-4a69-8bbe-2feb32204a27
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 6466d7b8-e308-43c5-acdc-dec15f796f64
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 이메일 알림 구성{#configuring-email-notification}

AEM은 다음과 같은 사용자에게 이메일 알림을 보냅니다.

* 페이지 이벤트(예: 수정 또는 복제)를 구독했습니다. [ [알림 받은](/help/sites-classic-ui-authoring/author-env-inbox.md#subscribing-to-notifications) 편지함] 섹션에서는 이러한 이벤트에 가입하는 방법에 대해 설명합니다.

* 포럼 이벤트에 가입했습니다.
* 워크플로우에서 단계를 수행해야 합니다. 참가자 [단계](/help/sites-developing/workflows-step-ref.md#participant-step) 섹션에서는 워크플로우에서 이메일 알림을 트리거하는 방법에 대해 설명합니다.

전제 조건:

* 사용자의 프로필에 유효한 이메일 주소가 정의되어 있어야 합니다.
* Day **CQ Mail** Service를 제대로 구성해야 합니다.

사용자가 알림을 받으면 프로필에 정의된 언어로 이메일을 수신합니다. 각 언어에는 사용자 지정할 수 있는 고유한 템플릿이 있습니다. 새 언어에 대한 새 이메일 템플릿을 추가할 수 있습니다.

>[!NOTE]
>
>When working with AEM there are several methods of managing the configuration settings for such services; see [Configuring OSGi](/help/sites-deploying/configuring-osgi.md) for more details and the recommended practices.

## 메일 서비스 구성 {#configuring-the-mail-service}

AEM에서 이메일을 보낼 수 있으려면 **요일** CQ 메일 서비스를 제대로 구성해야 합니다. 웹 콘솔에서 구성을 볼 수 있습니다. When working with AEM there are several methods of managing the configuration settings for such services; see [Configuring OSGi](/help/sites-deploying/configuring-osgi.md) for more details and the recommended practices.

다음 제한 사항이 적용됩니다.

* SMTP **서버 포트는** 25 이상이어야 합니다.

* SMTP **서버 호스트 이름은** 비워둘 수 없습니다.
* &quot;보낸 사람&quot; **주소는** 비워둘 수 없습니다.

Day CQ Mail Service **의 문제를**&#x200B;디버깅하는 데 도움이 되도록 다음과 같은 서비스 로그를 볼 수 있습니다.

`com.day.cq.mailer.DefaultMailService`

구성은 웹 콘솔에서 다음과 같이 표시됩니다.

![chlimage_1-276](assets/chlimage_1-276.png)

## 이메일 알림 채널 구성 {#configuring-the-email-notification-channel}

페이지 또는 포럼 이벤트 알림에 가입하면 보낸 사람 이메일 주소가 `no-reply@acme.com` 기본적으로 설정됩니다. 웹 콘솔에서 알림 이메일 채널 **서비스를 구성하여 이** 값을 변경할 수 있습니다.

이메일 주소를 구성하려면 저장소에 `sling:OsgiConfig` 노드를 추가합니다. CRXDE Lite를 사용하여 노드를 직접 추가하려면 다음 절차를 따르십시오.

1. CRXDE Lite에서 응용 프로그램 폴더 `config` 아래에 명명된 폴더를 추가합니다.
1. 구성 폴더에서 다음 이름의 노드를 추가합니다.

   `com.day.cq.wcm.notification.email.impl.EmailChannel` 유형 `sling:OsgiConfig`

1. 명명된 노드에 `String` 속성을 `email.from`추가합니다. 값에 사용할 이메일 주소를 지정합니다.

1. 모두 **저장을 클릭합니다**.

다음 절차를 사용하여 컨텐츠 패키지 소스 폴더의 노드를 정의합니다.

1. 에서 `jcr_root/apps/*app_name*/config folder``com.day.cq.wcm.notification.email.impl.EmailChannel.xml`

1. 노드를 나타내는 다음 XML을 추가합니다.

   `<?xml version="1.0" encoding="UTF-8"?> <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0" jcr:primaryType="sling:OsgiConfig" email.from="name@server.com"/>`
1. 속성()의 `email.from` 값을 이메일 `name@server.com`주소로 바꿉니다.

1. 파일을 저장합니다.

## 워크플로우 이메일 알림 서비스 구성 {#configuring-the-workflow-email-notification-service}

워크플로우 이메일 알림을 받으면 보낸 사람 이메일 주소와 호스트 URL 접두사가 모두 기본값으로 설정됩니다. 웹 콘솔에서 일 CQ Workflow 이메일 **알림 서비스를 구성하여 이러한** 값을 변경할 수 있습니다. 이렇게 하면 저장소의 변경 사항을 유지하는 것이 좋습니다.

기본 구성은 웹 콘솔에서 다음과 같이 표시됩니다.

![chlimage_1-277](assets/chlimage_1-277.png)

### 페이지 알림용 이메일 템플릿 {#email-templates-for-page-notification}

페이지 알림에 대한 이메일 템플릿은 아래에 있습니다.

`/etc/notification/email/default/com.day.cq.wcm.core.page`

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

페이지 알림에 대한 영어 이메일 템플릿을 사용자 정의하려면

1. CRXDE에서 파일을 엽니다.

   `/etc/notification/email/default/com.day.cq.wcm.core.page/en.txt`

1. 필요에 따라 파일을 수정합니다.
1. 변경 사항을 저장합니다.

템플릿에는 다음 형식이 있어야 합니다.

```
 subject=<text_1>
 header=<text_2>
 message=<text_3>
 footer=<text_4>
```

여기서 &lt;text_x>은(는) 정적 텍스트와 동적 문자열 변수의 혼합일 수 있습니다. 페이지 알림의 이메일 템플릿 내에서 다음 변수를 사용할 수 있습니다.

* `${time}`, the event date and time.

* `${userFullName}`를 채우는 것이 좋습니다.

* `${userId}`, 이벤트를 트리거한 사용자의 ID.
* `${modifications}`에서는 페이지 이벤트의 유형과 페이지 경로를 다음과 같은 형식으로 설명합니다.

   &lt;페이지 이벤트 유형> => &lt;페이지 경로>

   예:

   PageModified => /content/geometrixx/en/products

### 포럼 알림용 이메일 템플릿 {#email-templates-for-forum-notification}

포럼 알림에 대한 이메일 템플릿은 다음 위치에 있습니다.

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

#### 포럼 알림에 대한 이메일 템플릿 사용자 지정 {#customizing-email-templates-for-forum-notification}

포럼 알림에 대한 영어 이메일 템플릿을 사용자 정의하려면

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

정적 텍스트와 동적 문자열 변수가 혼합되어 있을 `<text_x>` 수 있습니다.

포럼 알림에 대해 이메일 템플릿 내에서 다음 변수를 사용할 수 있습니다.

* `${time}`, the event date and time.

* `${forum.path}`을 클릭합니다.

### 워크플로우 알림을 위한 이메일 템플릿 {#email-templates-for-workflow-notification}

워크플로우 알림에 대한 이메일 템플릿(영어)은 다음 위치에 있습니다.

`/etc/workflow/notification/email/default/en.txt`

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

#### 워크플로우 알림을 위한 이메일 템플릿 사용자 정의 {#customizing-email-templates-for-workflow-notification}

워크플로우 이벤트 알림에 대해 영어 이메일 템플릿을 사용자 정의하려면

1. CRXDE에서 파일을 엽니다.

   `/etc/workflow/notification/email/default/en.txt`

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
>정적 텍스트와 동적 문자열 변수가 혼합되어 있을 `<text_x>` 수 있습니다. 백슬래시가 없으면 `<text_x>` 문자열 변수의 끝을 나타내는 마지막 인스턴스를 제외하고 항목의 각 행은 백슬래시( `\``<text_x>` )로 끝나야 합니다.
>
>템플릿 형식에 대한 자세한 내용은 Properties.load() [메서드의](https://docs.oracle.com/javase/8/docs/api/java/util/Properties.html#load-java.io.InputStream-) javadocs를 참조하십시오.

이 메서드는 작업 항목의 페이로드 경로를 `${payload.path.open}` 표시합니다. 예를 들어, 사이트의 페이지에 대해서는 `payload.path.open` 이와 비슷합니다 `/bin/wcmcommand?cmd=open&path=…`.;서버 이름이 없는 경우이므로 템플릿에 이 접두사가 `${host.prefix}`붙습니다.

이메일 템플릿 내에서 다음 변수를 사용할 수 있습니다.

* `${event.EventType}`, 이벤트 유형
* `${event.TimeStamp}`, 이벤트 날짜 및 시간
* `${event.User}`, 이벤트를 트리거한 사용자
* `${initiator.home}`, 이니시에이터 노드 경로

* `${initiator.name}`, 이니시에이터 이름

* `${initiator.email}`, 이니시에이터의 이메일 주소
* `${item.id}`, 작업 항목의 id
* `${item.node.id}`, 이 작업 항목과 연관된 워크플로우 모델의 노드 ID
* `${item.node.title}`, title of work item
* `${participant.email}`, 참가자의 이메일 주소
* `${participant.name}`, 참가자 이름
* `${participant.familyName}`, 참가자의 가족 이름
* `${participant.id}`, 참가자 ID
* `${participant.language}`, 참가자 언어
* `${instance.id}`, 워크플로 ID
* `${instance.state}`, 워크플로 상태
* `${model.title}`, workflow 모델의 제목
* `${model.id}`, 워크플로 모델의 ID

* `${model.version}`, 워크플로 모델의 버전
* `${payload.data}`, payload

* `${payload.type}`, 페이로드 유형
* `${payload.path}`, 페이로드 경로
* `${host.prefix}`, 호스트 접두사, 예:http://localhost:4502

### 새 언어용 이메일 템플릿 추가 {#adding-an-email-template-for-a-new-language}

새 언어에 대한 템플릿을 추가하려면:

1. CRXDE에서 `<language-code>.txt` 아래 파일을 추가합니다.

   * `/etc/notification/email/default/com.day.cq.wcm.core.page` :페이지 알림
   * `/etc/notification/email/default/com.day.cq.collab.forum` :포럼 알림
   * `/etc/workflow/notification/email/default` :워크플로우 알림

1. 파일을 언어에 맞게 변경합니다.
1. 변경 사항을 저장합니다.

>[!NOTE]
>
>이메일 템플릿의 파일 이름으로 `<language-code>` 사용되는 언어는 AEM에서 인식하는 두 글자 소문자 언어 코드여야 합니다. 언어 코드의 경우 AEM은 ISO-639-1을 사용합니다.

## AEM 자산 이메일 알림 구성 {#assetsconfig}

AEM 자산의 컬렉션이 공유되거나 공유되지 않으면 사용자는 AEM으로부터 이메일 알림을 받을 수 있습니다. 이메일 알림을 구성하려면 다음 단계를 따르십시오.

1. 메일 서비스 구성에 설명된 대로 이메일 서비스를 [구성합니다](/help/sites-administering/notification.md#configuring-the-mail-service).
1. AEM에 관리자로 로그인합니다. 도구 **> 작업** **** > 웹 **콘솔을** 클릭하여 웹 콘솔구성을 엽니다.
1. CQ **DAM 리소스 수집 서블릿을 편집합니다**. 이메일 **보내기를 선택합니다**. **저장**&#x200B;을 클릭합니다.

