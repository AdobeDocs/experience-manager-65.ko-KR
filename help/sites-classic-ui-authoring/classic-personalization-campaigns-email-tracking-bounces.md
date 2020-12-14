---
title: 바운스된 이메일 추적
seo-title: 바운스된 이메일 추적
description: 많은 사용자에게 뉴스레터를 전송할 때 일반적으로 목록에 유효하지 않은 이메일 주소가 포함되어 있습니다. 해당 주소로 뉴스레터를 보내면 바운스되어 돌아옵니다. AEM에서는 이러한 바운스를 관리하고 구성된 바운스 카운터를 초과할 경우 해당 주소로의 뉴스레터 전송을 중지할 수 있습니다.
seo-description: 많은 사용자에게 뉴스레터를 전송할 때 일반적으로 목록에 유효하지 않은 이메일 주소가 포함되어 있습니다. 해당 주소로 뉴스레터를 보내면 바운스되어 돌아옵니다. AEM에서는 이러한 바운스를 관리하고 구성된 바운스 카운터를 초과할 경우 해당 주소로의 뉴스레터 전송을 중지할 수 있습니다.
uuid: 749959f2-e6f8-465f-9675-132464c65f11
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: fde9027b-9057-48c3-ae34-3f3258c5b371
translation-type: tm+mt
source-git-commit: 016c705230dffec052c200b058a36cdbe0520fc4
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 81%

---


# 바운스된 이메일 추적{#tracking-bounced-emails}

>[!NOTE]
>
>Adobe은 AEM SMTP 서비스를 통해 열리거나 바운스된 이메일에 대한 추적을 추가로 개선할 계획이 없습니다.
>
>권장 사항은 [Adobe Campaign 및 AEM 통합](/help/sites-administering/campaign.md)을 활용하는 것입니다.

많은 사용자에게 뉴스레터를 전송할 때 일반적으로 목록에 유효하지 않은 이메일 주소가 포함되어 있습니다. 해당 주소로 뉴스레터를 보내면 바운스되어 돌아옵니다. AEM에서는 이러한 바운스를 관리하고 구성된 바운스 카운터를 초과할 경우 해당 주소로의 뉴스레터 전송을 중지할 수 있습니다. 기본적으로 바운스 비율은 3으로 설정되지만 구성 가능합니다.

바운스된 이메일을 추적하도록 AEM을 설정하려면, 바운스된 이메일이 수신되는 기존 사서함을 폴링하도록 AEM을 설정해야 합니다(일반적으로 바운스된 메일의 &quot;보낸 사람&quot; 이메일 주소, 즉 뉴스레터를 발송할 때 받는 사람으로 지정한 이메일 주소임). AEM은 이 받은 편지함을 폴링하고 폴링 구성에 지정된 경로 아래로 모든 이메일을 가져옵니다. 그러면 사용자 내에서 바운스된 이메일 주소를 검색하도록 워크플로우가 트리거되며 그에 따라 사용자의 bounceCounter 속성 값을 업데이트합니다. 구성된 최대 바운스 수가 초과되면 Newsletter 목록에서 사용자가 제거됩니다.

## Feed Importer 구성 {#configuring-the-feed-importer}

Feed Importer를 사용하면 외부 소스의 컨텐츠를 저장소로 반복해서 가져올 수 있습니다. Feed Importer의 이 구성을 사용하여 AEM은 보낸 사람의 편지함에서 바운스된 이메일이 있는지 확인합니다.

바운스된 이메일을 추적하기 위해 Feed Importer를 구성하려면:

1. **도구**&#x200B;에서 Feed Importer를 선택합니다.

1. **추가**&#x200B;를 클릭하여 새 구성을 만듭니다.

   ![chlimage_1](assets/chlimage_1a.png)

1. 유형을 선택하고 폴링 URL에 호스트 및 포트를 구성하기 위한 정보를 추가하여 새 구성을 추가합니다. 또한 일부 메일 및 프로토콜 특정 매개 변수를 URL 쿼리에 추가해야 합니다. 적어도 하루에 한 번 이상 폴링을 수행하도록 구성을 설정합니다.

   모든 구성에는 폴링 URL의 다음에 대한 정보가 필요합니다.

   `username`: 연결하는 데 사용하는 사용자 이름

   `password`: 연결하는 데 사용하는 암호

   또한 프로토콜에 따라 특정 설정을 구성할 수 있습니다.

   **POP3 구성 속성:**

   `pop3.leave.on.server`: 메시지를 서버에 둘 것인지를 정의합니다. 메시지를 서버에 두려면 true로 설정하고 그렇지 않으면 false로 설정합니다. 기본값은 true입니다.

   **POP3 예제:**

   | pop3s://pop.gmail.com:995/INBOX?username=user&amp;password=secret | SSL을 통해 pop3를 사용하여 user/secret으로 포트 995의 GMail에 연결하고 기본적으로 서버에 메시지를 남겨 둠 |
   |---|---|
   | pop3s://pop.gmail.com:995/INBOX?username=user&amp;password=secret&amp;pop3.leave.on.server=false | pop3s://pop.gmail.com:995/INBOX?username=user&amp;password=secret&amp;pop3.leave.on.server=false |

   **IMAP 구성 속성:**

   검색할 플래그를 설정할 수 있습니다.

   `imap.flag.SEEN`:새 메시지/보지 않은 메시지의 경우 false로설정, 이미 읽은 메시지의 경우 true로설정

   전체 플래그 목록을 보려면 [https://java.sun.com/products/javamail/javadocs/javax/mail/Flags.Flag.html](https://java.sun.com/products/javamail/javadocs/javax/mail/Flags.Flag.html)을 참조하십시오.

   **IMAP 예제:**

   | imaps://imap.gmail.com:993/inbox?username=user&amp;password=secret | SSL을 통해 IMAP를 사용하여 user/secret으로 포트 993의 GMail에 연결. 기본적으로 새 메시지만 가져옴. |
   |---|---|
   | imaps://imap.gmail.com:993/inbox?username=user&amp;password=secret&amp;imap.flag.SEEN=true | SSL을 통해 IMAP를 사용하여 user/secret으로 GMail 993에 연결, 이미 읽은 메시지만 가져옴. |
   | imaps://imap.gmail.com:993/inbox?username=user&amp;password=secret&amp;imap.flag.SEEN=true&amp;imap.flag.SEEN=false | SSL을 통해 IMAP를 사용하여 user/secret으로 GMail 993에 연결, 이미 읽은 메시지 또는 새 메시지만 가져옴. |

1. 구성을 저장합니다.

## Newsletter 서비스 구성 요소 구성  {#configuring-the-newsletter-service-component}

Feed Importer를 구성한 후에 보낸 사람 주소 및 바운스 카운터를 구성해야 합니다.

뉴스레터 서비스를 구성하려면:

1. `<host>:<port>/system/console/configMgr`의 OSGi 콘솔에서 **MCM Newsletter**&#x200B;로 이동합니다.

1. 서비스를 구성을 마친 후 변경 사항을 저장합니다.

   ![chlimage_1-1](assets/chlimage_1-1a.png)

   동작을 조정하기 위해 다음 구성을 설정할 수 있습니다.

   | 최대 바운스 카운터(max.bounce.count) | Newsletter를 전송할 때 사용자를 받는 사람 목록에서 제거하는 바운스 수를 정의합니다. 이 값을 0으로 설정하면 바운스 검사가 완전히 비활성화됩니다. |
   |---|---|
   | 활동 캐시 없음(sent.activity.nocache) | Newsletter 전송 활동에 사용할 캐시 설정을 정의합니다. |

   일단 저장되면 Newsletter MCM 서비스는 다음을 수행합니다.

   * 뉴스레터를 성공적으로 전송할 때 사용자 숨김 스트림에 활동을 기록합니다.
   * 바운스가 검색되고 사용자 바운스 카운터가 변경되면 활동을 기록합니다.
