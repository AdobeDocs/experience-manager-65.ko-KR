---
title: 메시지 구성
seo-title: 메시징 구성
description: 커뮤니티 메시지
seo-description: 커뮤니티 메시지
uuid: 159dcf9d-7948-4a3d-9f51-a5b4d03e172b
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 232a0ec1-8dfc-41ec-84cc-69f9db494ea0
docset: aem65
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '826'
ht-degree: 1%

---


# 메시지 구성 {#configure-messaging}

## 개요 {#overview}

AEM Communities의 메시징 기능은 로그인 사이트 방문자(구성원)가 사이트에 로그인할 때 액세스할 수 있는 다른 사람에게 메시지를 보내는 기능을 제공합니다.

커뮤니티 사이트를 만드는 동안 상자를 선택하면 커뮤니티 사이트에 대한 [메시징이 활성화됩니다](/help/communities/sites-console.md).

이 페이지에는 기본 구성 및 가능한 조정에 대한 정보가 있습니다.

개발자를 위한 자세한 내용은 [메시지 요점을 참조하십시오](/help/communities/essentials-messaging.md).

## 메시징 작업 서비스 {#messaging-operations-service}

구성 [](https://localhost:4502/system/console/configMgr/com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl) AEM Communities 메시징 작업 서비스는 메시징 관련 요청을 처리하는 종단점, 서비스가 메시지를 저장하는 데 사용해야 하는 폴더, 메시지에 첨부 파일이 포함되어 있을 수 있는 경우 허용되는 파일 유형을 식별합니다.

를 사용하여 만든 커뮤니티 사이트의 경우 받은 편지함 `Communities Sites console`이 설정된 서비스 인스턴스가 이미 있습니다 `/mail/inbox`.

### 커뮤니티 메시징 작업 서비스 {#community-messaging-operations-service}

아래와 같이 [사이트 만들기 마법사로 만든 사이트에 대한 서비스 구성이 있습니다](/help/communities/sites-console.md). 구성 옆에 있는 연필 아이콘을 선택하여 구성을 보거나 편집할 수 있습니다.

![메시징 작업](assets/messaging-operations.png)

### 새 구성 추가 {#add-new-configuration}

새 구성을 추가하려면 서비스 이름 옆에 있는 더하기&#x200B;**&#39;**+s&#39; 아이콘을 선택합니다.

* **메시지 필드 허용 목록에 추가하다**

   사용자가 편집하고 유지할 수 있는 메시지 작성 구성 요소의 속성을 지정합니다. 새로운 양식 요소가 추가된 경우 SRP에 저장하려면 요소 ID를 추가해야 합니다. 기본값은 두 개의 항목입니다. *제목* 및 *컨텐츠*.

* **메시지 상자 크기 제한**

   각 사용자의 메시지 상자에 있는 최대 바이트 수입니다. 기본값은 *1073741824* (1GB)입니다.

* **메시지 수 제한**

   사용자당 허용되는 총 메시지 수입니다. 값이 -1이면 메시지 상자 크기 제한에 따라 허용되는 메시지 수가 무제한임을 나타냅니다. 기본값은 *10000* (10k)입니다.

* **배달 실패 알림**

   이 확인란을 선택하면 일부 받는 사람에게 메시지 배달이 실패할 경우 발신자에게 알립니다. 기본값은 *선택되었습니다*.

* **배달 보낸 사람 ID 실패**

   배달 실패 메시지에 나타나는 보낸 사람의 이름입니다. 기본값은 *failureNotifier입니다*.

* **실패 메시지 템플릿 경로**

   배달 실패 메시지 템플릿 루트 절대 경로입니다. 기본값은 */etc/notification/messaging/default입니다*.

* **재시도 횟수**

   배달되지 못한 메시지를 다시 보내는 데 필요한 횟수입니다. 기본값은 *3입니다*.

* **재시도 간격 대기**

   전송 실패 시 메시지를 다시 전송하려는 시도 사이의 대기 시간(초)입니다. 기본값은 *100* (초)입니다.

* **업데이트 풀 크기 계산**

   카운트 업데이트에 사용되는 동시 스레드 수입니다. 기본값은 *10입니다*.

* **받은 편지함 경로**

   (*필수*)*폴더에 사용할 사용자 노드(/home/users/* username `inbox` )에 상대적인경로입니다. 경로는 후행 슬래시 &#39;/&#39;로 끝나야 합니다. 기본값은 */mail/inbox입니다*.

* **보낸 항목 경로**

   (*필수*)*폴더에 사용할 사용자 노드(/home/users/* username `sent items` )에 상대적인경로입니다. 경로는 후행 슬래시 &#39;/&#39;로 끝나야 합니다. 기본값은 */mail/sentims입니다* .

* **첨부 파일 지원**

   이 확인란을 선택하면 사용자가 메시지에 첨부 파일을 추가할 수 있습니다. 기본값은 *선택되었습니다*.

* **그룹 메시지 사용**

   선택한 경우 등록된 사용자는 구성원 그룹에 일괄 메시지를 보낼 수 있습니다. 기본값은 *선택 해제입니다*.

* **최대 아니요. 총 받는 사람 수**

   그룹 메시징을 사용하는 경우 한 번에 보낼 수 있는 그룹 메시지를 받는 사람의 최대 수를 지정합니다. 기본값은 *100입니다*.

* **배치 크기**

   여러 받는 사람에게 보낼 때 함께 보낼 메시지 수입니다. 기본값은 *100입니다*.

* **총 첨부 파일 크기**

   supportAttachments를 선택하는 경우 이 값은 모든 첨부 파일의 허용되는 최대 총 크기(바이트)를 지정합니다. 기본값은 *104857600* (100MB)입니다.

* **첨부 유형 차단 목록에 추가하다**

   파일 이름 확장자차단 목록에 추가하다의에 &#39;가 접두사로 추가되었습니다&#x200B;**.**&#39;, 시스템에 의해 거부됩니다. 그렇지 차단 목록에 추가된 않으면 확장이 허용됩니다. &#39;**+**&#39; 및 &#39;**-**&#39; 아이콘을 사용하여 익스텐션을 추가하거나 제거할 수있습니다.

* **허용되는 첨부 파일 유형**

   **(*작업 필요*** )허용 목록에 추가하다의 반대쪽에 있는 파일 이름 확장자차단 목록에 추가하다의입니다. 파일 이름 확장자를 제외한 모든 파일 이름차단 목록에 추가된을 허용하려면 &#39;**-**&#39; 아이콘을 사용하여 빈 항목 하나를 제거합니다.

* **서비스 선택기**

   (*필수*) 서비스가 호출되는 절대 경로(끝점)입니다(가상 리소스). 선택한 경로의 루트는 OSGi 구성의 *실행 경로* 구성 설정 [ 에 포함되어야 `Apache Sling Servlet/Script Resolver and Error Handler`](https://localhost:4502/system/console/configMgr/org.apache.sling.servlets.resolver.SlingServletResolver)합니다(예: `/bin/`, `/apps/`및 `/services/`). 사이트의 메시징 기능에 대해 이 구성을 선택하려면 이 끝점이 해당 **`Service selector`** 의 값으로 `Message List and Compose Message components` 제공됩니다( [메시지 기능](/help/communities/configure-messaging.md)참조).

   기본값은 */bin/messaging입니다* .

* **필드 허용 목록에 추가하다**

   메시지 **필드 허용 목록에 추가하다를 사용합니다**.

>[!CAUTION]
>
>편집을 위해 `Messaging Operations Service` `allowedAttachmentTypes.name` 구성을 열 때마다, 제거된 경우 빈 항목이 다시 추가되어 속성을 구성할 수 있습니다. 비어 있는 단일 항목은 파일 첨부 파일을 효과적으로 비활성화합니다.
>
>파일 이름 확장자를 제외한 모든 파일 이름차단 목록에 추가된을 허용하려면 &#39;**-**&#39; 아이콘을 사용하여 [저장]을 클릭하기 전에 비어 있는 단일 항목을 다시 **제거합니다**.

## Group Messaging {#group-messaging}

등록된 사용자가 사용자 그룹에 직접 메시지를 일괄적으로 보낼 수 있도록 하려면 다음 두 가지 메시지 작업 서비스 구성 **에서 그룹 메시지** 사용을 **활성화해야** 합니다.

* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-console`
* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-messaging`

**메시징 작업 서비스:소셜 콘솔**

![social-console-op-service](assets/social-console-op-service.png)

**메시징 작업 서비스:소셜 메시지**

![social-message-op-service](assets/social-message-op-service.png)

## 문제 해결 {#troubleshooting}

문제를 해결하는 한 가지 방법은 로그에서 [디버깅 메시지를 활성화하는 것입니다.](/help/sites-administering/troubleshooting.md)

로거 [및 개인 정보 서비스 작가도 참조하십시오](/help/sites-deploying/configure-logging.md#loggers-and-writers-for-individual-services).

모니터링할 패키지 `com.adobe.cq.social.messaging`가 있습니다.
