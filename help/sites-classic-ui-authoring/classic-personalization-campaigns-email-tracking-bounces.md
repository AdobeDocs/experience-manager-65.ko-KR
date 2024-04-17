---
title: 반송된 이메일 추적
description: 많은 사용자에게 뉴스레터를 보낼 때 일반적으로 목록에 일부 잘못된 이메일 주소가 있습니다. 해당 주소로 뉴스레터를 전송하는 경우 다시 반송됩니다. AEM은 이러한 바운스를 관리할 수 있으며 구성된 바운스 카운터가 초과된 후 해당 주소로 뉴스레터 전송을 중지할 수 있습니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: 6cda0a68-0df9-44e7-ae4f-9951411af6dd
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 0%

---

# 반송된 이메일 추적{#tracking-bounced-emails}

>[!NOTE]
>
>Adobe은 AEM SMTP 서비스에서 보낸 열림/반송된 이메일의 추적을 더 강화하지 않을 계획입니다.
>
>권장 사항은 다음과 같습니다. [Adobe Campaign 및 해당 AEM 통합 사용](/help/sites-administering/campaign.md).

많은 사용자에게 뉴스레터를 보낼 때 일반적으로 목록에 일부 잘못된 이메일 주소가 있습니다. 해당 주소로 뉴스레터를 전송하는 경우 다시 반송됩니다. AEM은 이러한 바운스를 관리할 수 있으며 구성된 바운스 카운터가 초과된 후 해당 주소로 뉴스레터 전송을 중지할 수 있습니다. 기본적으로 바운스 비율은 3으로 설정되지만 구성할 수 있습니다.

반송된 이메일을 추적하도록 AEM을 설정하려면 반송된 이메일이 수신되는 기존 사서함을 폴링하도록 AEM을 설정하십시오. 일반적으로 이 위치는 뉴스레터를 보내는 위치를 지정하는 &quot;보낸 사람&quot; 이메일 주소입니다. AEM은 이 받은 편지함을 폴링하고 폴링 구성에 지정된 경로 아래의 모든 전자 메일을 가져옵니다. 그런 다음 사용자 내에서 반송된 이메일 주소를 검색하고 그에 따라 사용자의 bounceCounter 속성 값을 업데이트하도록 워크플로우가 트리거됩니다. 구성된 최대 바운스를 초과하면 사용자가 뉴스레터 목록에서 제거됩니다.

## 피드 가져오기 구성 {#configuring-the-feed-importer}

피드 가져오기를 사용하면 외부 소스의 콘텐츠를 저장소로 반복적으로 가져올 수 있습니다. 피드 임포터의 이러한 구성을 통해 AEM은 보낸 사람의 사서함에서 반송된 이메일을 확인합니다.

반송된 이메일을 추적하도록 피드 가져오기를 구성하려면 다음을 수행합니다.

1. 위치 **도구**&#x200B;피드 가져오기를 선택합니다.

1. 클릭 **추가** 구성을 만듭니다.

   ![chlimage_1](assets/chlimage_1a.png)

1. 호스트 및 포트를 구성할 수 있도록 유형을 선택하고 폴링 URL에 정보를 추가하여 구성을 추가합니다. 또한 일부 메일 및 프로토콜별 매개 변수를 URL 쿼리에 추가하십시오. 하루에 한 번 이상 폴링하도록 구성을 설정하십시오.

   모든 구성은 폴링 URL에 다음에 대한 정보가 필요합니다.

   `username`: 연결에 사용되는 사용자 이름

   `password`: 연결에 사용되는 암호

   또한 프로토콜에 따라 특정 설정을 구성할 수도 있습니다.

   **POP3 구성 속성:**

   `pop3.leave.on.server`: 서버에 메시지를 남길지 여부를 정의합니다. 서버에 메시지를 남기려면 true로 설정하고, 그렇지 않으면 false로 설정합니다. 기본값은 true입니다.

   **POP3 예:**

   | pop3s://pop.gmail.com:995/INBOX?username=user&amp;password=secret | SSL을 통해 pop3를 사용하여 사용자/암호로 포트 995의 GMail에 연결하고 기본적으로 서버에 메시지 남김 |
   |---|---|
   | pop3s://pop.gmail.com:995/INBOX?username=user&amp;password=secret&amp;pop3.leave.on.server=false | pop3s://pop.gmail.com:995/INBOX?username=user&amp;password=secret&amp;pop3.leave.on.server=false |

   **IMAP 구성 속성:**

   검색할 플래그를 설정할 수 있습니다.

   `imap.flag.SEEN`:새/보이지 않는 메시지에 대해 false를 설정하고, 이미 읽은 메시지에 대해 true를 설정합니다.

   다음을 참조하십시오 [https://javaee.github.io/javamail/docs/api/index.html?javax/mail/Flags.Flag.html](https://javaee.github.io/javamail/docs/api/index.html?javax/mail/Flags.Flag.html) 플래그 전체 목록.

   **IMAP 예:**

   | imaps://imap.gmail.com:993/inbox?username=user&amp;password=secret | SSL을 통해 IMAP을 사용하여 사용자/암호로 포트 993의 GMail에 연결합니다. 기본적으로만 새 메시지를 가져옵니다. |
   |---|---|
   | imaps://imap.gmail.com:993/inbox?username=user&amp;password=secret&amp;imap.flag.SEEN=true | SSL을 통해 IMAP을 사용하여 사용자/암호로 GMail 993에 연결하면 이미 표시된 메시지만 표시됩니다. |
   | imaps://imap.gmail.com:993/inbox?username=user&amp;password=secret&amp;imap.flag.SEEN=true&amp;imap.flag.SEEN=false | SSL을 통해 IMAP을 사용하여 사용자/암호로 GMail 993에 연결하고 이미 읽거나 새 메시지를 받았습니다. |

1. 구성을 저장합니다.

## 뉴스레터 서비스 구성 요소 구성 {#configuring-the-newsletter-service-component}

Feed Importer를 구성한 후 From 주소 및 바운스 카운터를 구성합니다.

뉴스레터 서비스를 구성하려면:

1. OSGi 콘솔에서, `<host>:<port>/system/console/configMgr`, 다음으로 이동 **MCM 뉴스레터**.

1. 서비스를 구성하고 완료되면 변경 사항을 저장합니다.

   ![chlimage_1-1](assets/chlimage_1-1a.png)

   다음 구성을 설정하여 동작을 조정할 수 있습니다.

   | 바운스 카운터 최대(max.bounce.count) | 뉴스레터를 전송할 때 사용자가 생략되기 전까지의 바운스 수를 정의합니다. 이 값을 0으로 설정하면 바운스 검사가 완전히 비활성화됩니다. |
   |---|---|
   | 활동 캐시 없음(sent.activity.nocache) | 뉴스레터 전송 활동에 사용할 캐시 설정을 정의합니다. |

   저장되면 뉴스레터 MCM 서비스는 다음을 수행합니다.

   * 뉴스레터를 성공적으로 보내면 사용자의 숨겨진 스트림에 활동을 기록합니다.
   * 바운스가 감지되고 사용자가 바운스 카운터를 변경하면 활동을 기록합니다.
