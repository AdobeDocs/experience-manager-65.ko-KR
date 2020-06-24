---
title: Adobe Target과 통합을 위한 전제 조건
seo-title: Adobe Target과 통합을 위한 전제 조건
description: Adobe Target과 통합하기 위한 전제 조건에 대해 알아봅니다.
seo-description: Adobe Target과 통합하기 위한 전제 조건에 대해 알아봅니다.
uuid: 55d87a96-5fe7-4f7e-93c1-fdf7fbb7c971
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: ae4a6e97-c0d7-472d-a25f-b89b1abf4df3
docset: aem65
translation-type: tm+mt
source-git-commit: 70b18dbe351901abb333d491dd06a6c1c1c569d6
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 3%

---


# Adobe Target과 통합을 위한 전제 조건{#prerequisites-for-integrating-with-adobe-target}

AEM 및 Adobe Target [의](/help/sites-administering/target.md)통합의 일부로, 게시 노드에서 Adobe Target에 등록하고, 복제 에이전트를 구성하고, 보안 활동 설정을 구성해야 합니다.

## Adobe Target 등록 {#registering-with-adobe-target}

AEM을 Adobe Target과 통합하려면 유효한 Adobe Target 계정이 있어야 합니다. 이 계정에는 최소 **승인자** 수준 권한이 있어야 합니다. Adobe Target에 등록하면 클라이언트 코드를 받게 됩니다. AEM을 Adobe Target에 연결하려면 클라이언트 코드와 Adobe Target 로그인 이름 및 암호가 필요합니다.

클라이언트 코드는 Adobe Target 서버를 호출할 때 Adobe Target 고객 계정을 식별합니다.

>[!NOTE]
>
>통합을 사용하려면 Target 팀이 계정을 활성화해야 합니다.
>
>그렇지 않은 경우 [Adobe 고객 지원 센터에 문의하십시오](https://docs.adobe.com/content/help/en/target/using/cmp-resources-and-contact-information.html).

## Target 복제 에이전트 활성화 {#enabling-the-target-replication-agent}

작성자 인스턴스에서 테스트 및 Target [복제 에이전트를](/help/sites-deploying/replication.md) 활성화해야 합니다. AEM을 설치하기 위해 nosamplecontent [실행 모드를 사용한 경우 기본적으로 이 복제 에이전트가](/help/sites-deploying/configure-runmodes.md#using-samplecontent-and-nosamplecontent) 활성화되지 않습니다. 프로덕션 환경 보안에 대한 자세한 내용은 [보안 체크리스트를 참조하십시오](/help/sites-administering/security-checklist.md).

1. AEM 홈 페이지에서 **도구** > **배포** > **복제를**&#x200B;클릭하거나탭합니다.
1. 작성자의 **에이전트를 클릭하거나 탭합니다**.
1. 테스트 **및 Target(테스트 및 대상)** 복제 에이전트를 클릭하거나 탭한 다음 **편집을 클릭하거나 탭합니다**.
1. 활성화 옵션을 선택한 다음 확인을 클릭하거나 **누릅니다**.

   >[!NOTE]
   >
   >테스트 및 Target 복제 에이전트를 구성할 때 **전송** 탭에서 URI는 기본적으로 tnt:///으로 **설정됩니다**. 이 URI를 https://admin.testandtarget.omniture.com으로 **바꾸지 마십시오**.
   >
   >tnt:///으로 연결을 테스트하려고 하면 **오류가**&#x200B;발생합니다. 이 URI는 내부용이므로 **테스트 연결과 함께 사용해서는 안 됩니다**.

## 활동 설정 노드 보안 {#securing-the-activity-settings-node}

You must secure the activity settings node **cq:ActivitySettings** on the publish instance so that it is inaccessible to normal users. 활동 설정 노드는 Adobe Target에 대한 활동 동기화를 처리하는 서비스만 액세스할 수 있어야 합니다.

cq: **ActivitySettings** 노드는 CRXDE lite 아래의 활동 jcr:content 노드 `/content/campaigns/*nameofbrand*`* *에서 사용할 수 있습니다.* *예 `/content/campaign/we-retail/master/myactivity/jcr:content/cq:ActivitySettings`. 이 노드는 구성 요소를 타깃팅한 후에만 만들어집니다.

활동의 **jcr:content 아래의 cq:ActivitySettings** 노드는 다음 ACL에 의해 보호됩니다.

* 모든 사람 모두 거부
* &quot;target-activity-authors&quot;에 jcr:read,rep:write 허용(작성자는 즉시 이 그룹의 구성원임)
* &quot;targetservice&quot;에 대해 jcr:read,rep:쓰기 허용

이러한 설정을 통해 일반 사용자가 노드 속성에 액세스할 수 없도록 합니다. 작성자와 게시 시 동일한 ACL을 사용합니다. 자세한 내용은 [사용자](/help/sites-administering/security.md) 관리 및 보안을 참조하십시오.

## AEM Link Externalizer 구성 {#configuring-the-aem-link-externalizer}

Adobe Target에서 활동을 편집할 때 AEM 작성자 노드에서 URL을 변경하지 않는 한 URL은 **localhost** 를 가리킵니다. 내보낸 콘텐츠가 특정 *게시* 도메인을 가리키도록 하려는 경우 AEM Link Externalizer를 구성할 수 있습니다.

>[!NOTE]
>
>클라우드 [구성 추가를 참조하십시오](/help/sites-administering/experience-fragments-target.md#add-the-cloud-configuration).

AEM Externalizer를 구성하려면:

>[!NOTE]
>
>자세한 내용은 URL [외부화를 참조하십시오](/help/sites-developing/externalizer.md).

1. https://&lt;server>:&lt;port>/system/console/configMgr의 **OSGi 웹 콘솔로 이동합니다.**
1. Day **CQ Link Externalizer를** 찾아 작성 노드의 도메인을 입력합니다.

   ![chlimage_1-120](assets/aem-externalizer-01.png)

