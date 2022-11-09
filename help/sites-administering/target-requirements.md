---
title: Adobe Target과 통합하기 위한 사전 요구 사항
seo-title: Prerequisites for Integrating with Adobe Target
description: Adobe Target과 통합하기 위한 사전 요구 사항에 대해 알아보십시오.
seo-description: Find out about the prerequisites for integrating with Adobe Target.
uuid: 55d87a96-5fe7-4f7e-93c1-fdf7fbb7c971
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: ae4a6e97-c0d7-472d-a25f-b89b1abf4df3
docset: aem65
exl-id: 30813c44-51ac-4e6e-8ee6-4e8baacb1ff9
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Adobe Target과 통합하기 위한 사전 요구 사항{#prerequisites-for-integrating-with-adobe-target}

의 일부로 [AEM 및 Adobe Target 통합](/help/sites-administering/target.md), Adobe Target에 등록하고, 복제 에이전트를 구성하고, 게시 노드에서 보안 활동 설정을 구성해야 합니다.

## Adobe Target에 등록 {#registering-with-adobe-target}

AEM을 Adobe Target과 통합하려면 유효한 Adobe Target 계정이 있어야 합니다. 이 계정에는 **승인자** 최소 수준의 권한. Adobe Target에 등록하면 클라이언트 코드가 전송됩니다. AEM을 Adobe Target에 연결하려면 클라이언트 코드, Adobe Target 로그인 이름 및 암호가 필요합니다.

클라이언트 코드는 Adobe Target 서버를 호출할 때 Adobe Target 고객 계정을 식별합니다.

>[!NOTE]
>
>통합을 사용하려면 Target 팀이 계정을 활성화해야 합니다.
>
>그렇지 않은 경우 [고객 지원 Adobe](https://experienceleague.adobe.com/docs/target/using/cmp-resources-and-contact-information.html).

## Target 복제 에이전트 활성화 {#enabling-the-target-replication-agent}

테스트 및 Target [복제 에이전트](/help/sites-deploying/replication.md) 작성자 인스턴스에서 을 활성화해야 합니다. 이 복제 에이전트는 [nosamplecontent](/help/sites-deploying/configure-runmodes.md#using-samplecontent-and-nosamplecontent) AEM 설치를 위한 실행 모드. 프로덕션 환경 보호에 대한 자세한 내용은 [Security 검사 목록](/help/sites-administering/security-checklist.md).

1. AEM 홈페이지에서 을 클릭하거나 탭합니다 **도구** > **배포** > **복제**.
1. 클릭 또는 탭 **작성자의 에이전트**.
1. 을 클릭하거나 탭합니다 **테스트 및 Target(테스트 및 타겟)** 복제 에이전트 를 클릭한 다음 **편집**.
1. Enabled 옵션을 선택한 다음 을 클릭하거나 탭합니다 **확인**.

   >[!NOTE]
   >
   >테스트 및 Target 복제 에이전트를 구성할 때 **전송** 탭하면 기본적으로 URI가 로 설정됩니다. **tnt:///**. 이 URI를 **https://admin.testandtarget.omniture.com**.
   >
   >연결을 테스트하려고 할 경우 **tnt:///**&#x200B;로 설정되면 오류가 발생합니다. 이 URI는 내부용이므로 예상된 동작이며 **연결 테스트**.

## 활동 설정 노드 보호 {#securing-the-activity-settings-node}

일반 사용자가 액세스할 수 없도록 게시 인스턴스에서 활동 설정 노드 **cq:ActivitySettings**&#x200B;를 보호해야 합니다. 활동 설정 노드는 Adobe Target에 대한 활동 동기화를 처리하는 서비스에만 액세스할 수 있어야 합니다.

다음 **cq:ActivitySettings** 노드는 아래의 CRXDE Lite에서 사용할 수 있습니다 `/content/campaigns/*nameofbrand*`* *활동 아래의 jcr:content node;* *예 `/content/campaign/we-retail/master/myactivity/jcr:content/cq:ActivitySettings`. 이 노드는 구성 요소를 타깃팅한 후에만 만들어집니다.

다음 **cq:ActivitySettings** 활동의 jcr:content 아래에 있는 노드는 다음 ACL로 보호됩니다.

* 모든 사용자를 위해 모두 거부
* jcr:read,rep:write 허용 &quot;target-activity-authors&quot;(작성자는 이 그룹의 구성원임)
* jcr:read,rep:write 허용 &quot;targetservice&quot;

이러한 설정은 일반 사용자가 노드 속성에 액세스할 수 없도록 합니다. 작성자 및 게시에서 동일한 ACL을 사용합니다. 자세한 내용은 [사용자 관리 및 보안](/help/sites-administering/security.md) 추가 정보.

## AEM Link Externalizer 구성 {#configuring-the-aem-link-externalizer}

Adobe Target에서 활동을 편집할 때 URL은 **localhost** AEM 작성자 노드에서 URL을 변경하지 않는 한. 내보낸 컨텐츠가 특정 항목을 가리키도록 하려면 AEM Link Externalizer를 구성할 수 있습니다 *게시* 도메인.

>[!NOTE]
>
>참조 - [클라우드 구성 추가](/help/sites-administering/experience-fragments-target.md#add-the-cloud-configuration).

AEM 외부 도우미를 구성하려면

>[!NOTE]
>
>자세한 내용은 [URL 표면화](/help/sites-developing/externalizer.md).

1. 에서 OSGi 웹 콘솔로 이동합니다 **https://&lt;server>:&lt;port>/system/console/configMgr.**
1. 찾기 **Day CQ Link Externalizer** 작성자 노드의 도메인을 입력합니다.

   ![chlimage_1-120](assets/aem-externalizer-01.png)
