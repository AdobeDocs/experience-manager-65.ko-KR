---
title: 메시징 핵심 사항
seo-title: 메시징 핵심 사항
description: 메시징 구성 요소 개요
seo-description: 메시징 구성 요소 개요
uuid: e0dad45e-d84d-4b28-b357-aded1c5d2605
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 98f70093-e786-4555-8aaa-d0df4c977dc0
docset: aem65
exl-id: b941b5e0-f768-4393-9a9d-ded2cd7d10c4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 3%

---

# 메시징 핵심 사항 {#messaging-essentials}

이 페이지에서는 메시징 구성 요소를 사용하여 웹 사이트에 메시징 기능을 포함하는 작업에 대한 세부 사항을 설명합니다.

## 클라이언트측 {#essentials-for-client-side}에 대한 필수 사항

**메시지 작성**

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td><p>social/messaging/components/hbs/composemessage</p> </td>
  </tr>
  <tr>
   <td> <a href="/help/communities/client-customize.md#clientlibs-for-scf" target="_blank"><strong>clientlibs</strong></a></td>
   <td><p>cq.social.hbs.messaging</p> </td>
  </tr>
  <tr>
   <td> <strong>템플릿</strong></td>
   <td>/libs/social/messaging/components/hbs/composemessage/composemessage.hbs</td>
  </tr>
  <tr>
   <td><strong>css</strong></td>
   <td>/libs/social/messaging/components/hbs/composemessage/clientlibs/composemessage.css</td>
  </tr>
  <tr>
   <td><strong>속성</strong></td>
   <td><a href="/help/communities/configure-messaging.md" target="_blank">메시징 구성</a> 을 참조하십시오.</td>
  </tr>
  <tr>
   <td><strong>관리 구성</strong></td>
   <td><a href="/help/communities/messaging.md">메시징 구성</a></td>
  </tr>
 </tbody>
</table>

**메시지 목록**

(받은 편지함, 전송 및 휴지통의 경우)

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td><p>social/messaging/components/hbs/messagebox</p> </td>
  </tr>
  <tr>
   <td> <a href="/help/communities/client-customize.md#clientlibs-for-scf" target="_blank"><strong>clientlibs</strong></a></td>
   <td><p>cq.social.hbs.messaging</p> </td>
  </tr>
  <tr>
   <td> <strong>템플릿</strong></td>
   <td>/libs/social/messaging/components/hbs/messagebox/messagebox.hbs</td>
  </tr>
  <tr>
   <td><strong>css</strong></td>
   <td>/libs/social/messaging/components/hbs/messagebox/clientlibs/messagebox.css</td>
  </tr>
  <tr>
   <td><strong>속성</strong></td>
   <td><a href="/help/communities/configure-messaging.md" target="_blank">메시징 구성</a> 을 참조하십시오.</td>
  </tr>
  <tr>
   <td><strong>관리 구성</strong></td>
   <td><a href="/help/communities/messaging.md" target="_blank">메시징 구성</a></td>
  </tr>
 </tbody>
</table>

[클라이언트측 사용자 지정](/help/communities/client-customize.md)도 참조하십시오.

## 서버측 {#essentials-for-server-side}에 대한 필수 사항

* [메시징 구성](/help/communities/configure-messaging.md)
* [SCF 구성 ](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/messaging/client/api/package-summary.html) 요소용 메시징 클라이언트 API
* [서비스](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/messaging/api/package-summary.html) 에 대한 메시징 API
* [메시징 끝점](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/messaging/client/endpoints/package-summary.html)
* [서버측 사용자 지정](/help/communities/server-customize.md)

>[!CAUTION]
>
>String 매개 변수는 다음 MessageBuilder 메서드에 대해 후행 슬래시 &quot;/&quot;를 포함하지 *않아야 합니다.*
>
>* `setInboxPath`()
>* `setSentItemsPath`()

>
>
예:
>
>
```
>valid: mb.setInboxPath( "/mail/inbox" );
> not valid: mb.setInboxPath( "/mail/inbox/" );
>```

### 커뮤니티 사이트 {#community-site}

마법사를 사용하여 만든 커뮤니티 사이트 구조에는 선택한 경우 메시징 기능이 포함됩니다. [커뮤니티 사이트 콘솔](/help/communities/sites-console.md#user-management)의 `User Management` 설정을 참조하십시오.

### 샘플 코드:메시지 수신 알림 {#sample-code-message-received-notification}

소셜 메시징 기능에서 작업에 대한 이벤트를 표시합니다(예: `send`, `marking read`, `marking delete`). 이러한 이벤트를 포착하고 이벤트에 포함된 데이터에 대한 작업을 수행할 수 있습니다.

다음 예제는 `message sent` 이벤트를 수신하고 `Day CQ Mail Service` 이벤트를 사용하여 모든 메시지 수신자에게 이메일을 보내는 이벤트 처리기입니다.

서버측 샘플 스크립트를 시도하려면 개발 환경과 OSGi 번들을 빌드하는 기능이 필요합니다.

1. ` [CRXDE|Lite](https://localhost:4502/crx/de)`에 관리자로 로그인합니다.
1. `/apps/engage/install`에서 다음과 같은 임의 이름을 사용하여 `bundle node`을 만듭니다.

   * 기호 이름: `com.engage.media.social.messaging.MessagingNotification`
   * 이름:시작하기 자습서 메시지 알림
   * 설명:사용자가 메시지를 받을 때 사용자에게 이메일 알림을 전송하는 샘플 서비스
   * 패키지: `com.engage.media.social.messaging.notification`

1. `/apps/engage/install/com.engage.media.social.messaging.MessagingNotification/src/main/java/com/engage/media/social/messaging/notification` 로 이동한 다음,

   1. 자동으로 생성된 `Activator.java` 클래스를 삭제합니다.
   1. `MessageEventHandler.java` 클래스를 만듭니다.
   1. 아래 코드를 복사하여 `MessageEventHandler.java`에 붙여넣습니다.

1. **모두 저장**&#x200B;을 클릭합니다.
1. `/apps/engage/install/com.engage.media.social.messaging.MessagingNotification/com.engage.media.social.messaging.MessagingNotification.bnd` 로 이동하고 `MessageEventHandler.java` 코드에 기록된 대로 모든 가져오기 구문을 추가합니다.
1. 번들을 빌드합니다.
1. `Day CQ Mail Service`OSGi 서비스가 구성되어 있는지 확인합니다.
1. 데모 사용자로 로그인하고 다른 사용자에게 이메일을 보냅니다.
1. 수신자가 새 메시지에 대한 이메일을 받습니다.

#### MessageEventHandler.java {#messageeventhandler-java}

```java
package com.engage.media.social.messaging.notification;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Properties;
import org.apache.felix.scr.annotations.Property;
import org.apache.felix.scr.annotations.Service;
import org.apache.felix.scr.annotations.Reference;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.api.resource.ResourceResolverFactory;
import org.apache.sling.api.resource.Resource;
import org.apache.commons.mail.Email;
import org.apache.commons.mail.EmailException;
import org.apache.commons.mail.SimpleEmail;
import org.apache.commons.mail.HtmlEmail;
import java.util.List;
import org.osgi.service.event.Event;
import org.osgi.service.event.EventHandler;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import com.adobe.cq.social.messaging.api.Message;
import com.adobe.cq.social.messaging.api.MessagingEvent;
import com.day.cq.mailer.MessageGatewayService;
import com.day.cq.mailer.MessageGateway;

@Component(immediate=true)
@Service(EventHandler.class)
@Properties({
        @Property(name = "event.topics", value = "com/adobe/cq/social/message")
})
public class MessagingEventHandler implements EventHandler {
    private Logger logger = LoggerFactory.getLogger(MessagingEventHandler.class);

    @Reference
    ResourceResolverFactory resourceResolverFactory;

    @Reference
    private MessageGatewayService messageGatewayService;

    ResourceResolver resourceResolver=null;
    MessageGateway messageGateway=null;

    public void sendMail(String from, String to,String subject, String content){
        Email email = new SimpleEmail();
        messageGateway = messageGatewayService.getGateway(SimpleEmail.class);
        try {
         email.addTo(to);
            email.addReplyTo(from);
            email.setFrom(from);
            email.setMsg(content);
            email.setSubject(subject);
         messageGateway.send(email);
        } catch(EmailException ex) {
            logger.error("MessageNotificaiton : Error sending email : "+ex.getMessage());
        }
        logger.info("**** MessageNotification **** Mail sent to " + to);
    }

    public void handleEvent(Event event) {
        //Get Message Path and originator User's ID from event
        String messagePath = (String) event.getProperty("path");
        String senderId = (String) event.getProperty("userId");
        MessagingEvent.MessagingActions action = (MessagingEvent.MessagingActions) event.getProperty("action");
        try{
            if(MessagingEvent.MessagingActions.MessageSent.equals(action)){
                resourceResolver = resourceResolverFactory.getAdministrativeResourceResolver(null);

                //Read message
                Resource resource = resourceResolver.getResource(messagePath);
                Message msg = resource.adaptTo(Message.class);

                //Get list of recipient Ids from message
                //For Getting Started Tutorial, Id is same as email. If that is not the case in your site,
                //an additional step is needed to retrieve the email for the Id
                List<String> reclist = msg.getRecipientIdList();
                for(int i=0;i<reclist.size();i++){
                    //Send Email using Mailing Service
                    sendMail("admin@cqadmin.qqq",reclist.get(i),"New message on Getting Started Tutorial", "Hi\nYou have received a new message from  " +  senderId + ". To read it, sign in to Getting Started Tutorial.\n\n-Engage Admin");
                }
            }
        } catch(Exception ex){
            logger.error("Error getting message info : " + ex.getMessage());
        } finally {
            resourceResolver.close();
        }

    }
}
```
