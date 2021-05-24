---
title: Adobe Target과 통합하기 위한 사전 요구 사항
seo-title: Adobe Target과 통합하기 위한 사전 요구 사항
description: Adobe Target과 통합하기 위한 사전 요구 사항에 대해 알아보십시오.
seo-description: Adobe Target과 통합하기 위한 사전 요구 사항에 대해 알아보십시오.
uuid: 55d87a96-5fe7-4f7e-93c1-fdf7fbb7c971
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: ae4a6e97-c0d7-472d-a25f-b89b1abf4df3
docset: aem65
exl-id: 30813c44-51ac-4e6e-8ee6-4e8baacb1ff9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 6%

---

# Adobe Target과 통합하기 위한 사전 요구 사항{#prerequisites-for-integrating-with-adobe-target}

AEM 및 Adobe Target](/help/sites-administering/target.md)의 [통합의 일부로, Adobe Target에 등록하고, 복제 에이전트를 구성하고, 게시 노드에서 보안 활동 설정을 구성해야 합니다.

## Adobe Target {#registering-with-adobe-target}에 등록

AEM을 Adobe Target과 통합하려면 유효한 Adobe Target 계정이 있어야 합니다. 이 계정에는 최소 **승인자** 수준 권한이 있어야 합니다. Adobe Target에 등록하면 클라이언트 코드가 전송됩니다. AEM을 Adobe Target에 연결하려면 클라이언트 코드, Adobe Target 로그인 이름 및 암호가 필요합니다.

클라이언트 코드는 Adobe Target 서버를 호출할 때 Adobe Target 고객 계정을 식별합니다.

>[!NOTE]
>
>통합을 사용하려면 Target 팀이 계정을 활성화해야 합니다.
>
>그렇지 않은 경우 [고객 지원 센터 Adobe](https://docs.adobe.com/content/help/en/target/using/cmp-resources-and-contact-information.html)에 문의하십시오.

## Target 복제 에이전트 {#enabling-the-target-replication-agent} 활성화

작성자 인스턴스에서 테스트 및 Target [복제 에이전트](/help/sites-deploying/replication.md)를 활성화해야 합니다. AEM을 설치하기 위해 [nosamplecontent](/help/sites-deploying/configure-runmodes.md#using-samplecontent-and-nosamplecontent) 실행 모드를 사용한 경우에는 이 복제 에이전트가 기본적으로 활성화되지 않습니다. 프로덕션 환경 보호에 대한 자세한 내용은 [보안 검사 목록](/help/sites-administering/security-checklist.md)을 참조하십시오.

1. AEM 홈 페이지에서 **도구** > **배포** > **복제**&#x200B;를 클릭하거나 탭합니다.
1. 작성자&#x200B;**에서**&#x200B;에이전트 를 클릭하거나 탭합니다.
1. **테스트 및 Target(테스트 및 타겟)** 복제 에이전트를 클릭하거나 탭한 다음, **편집**&#x200B;을 클릭하거나 탭합니다.
1. 활성화됨 옵션을 선택한 다음 **확인**&#x200B;을 클릭하거나 탭합니다.

   >[!NOTE]
   >
   >테스트 및 Target 복제 에이전트를 구성할 때 **전송** 탭에서 URI는 기본적으로 **tnt:///**&#x200B;로 설정됩니다. 이 URI를 **https://admin.testandtarget.omniture.com**&#x200B;로 바꾸지 마십시오.
   >
   >**tnt:///**&#x200B;와의 연결을 테스트하려고 하면 오류가 발생합니다. 이 URI는 내부용이므로 예상된 동작이며 **연결 테스트**&#x200B;에서 사용해서는 안 됩니다.

## 활동 설정 노드 {#securing-the-activity-settings-node} 보호

일반 사용자가 액세스할 수 없도록 게시 인스턴스에서 활동 설정 노드 **cq:ActivitySettings**&#x200B;를 보호해야 합니다. 활동 설정 노드는 Adobe Target에 대한 활동 동기화를 처리하는 서비스만 액세스할 수 있어야 합니다.

**cq:ActivitySettings** 노드는 `/content/campaigns/*nameofbrand*`* *활동 아래의 CRXDE Lite에서 jcr:content node;* *예: `/content/campaign/we-retail/master/myactivity/jcr:content/cq:ActivitySettings`. 이 노드는 구성 요소를 타깃팅한 후에만 만들어집니다.

활동의 jcr:content 아래에 있는 **cq:ActivitySettings** 노드는 다음 ACL로 보호됩니다.

* 모든 사용자를 위해 모두 거부
* jcr:read,rep:write 허용 &quot;target-activity-authors&quot;(작성자는 이 그룹의 구성원임)
* jcr:read,rep:write 허용 &quot;targetservice&quot;

이러한 설정은 일반 사용자가 노드 속성에 액세스할 수 없도록 합니다. 작성자 및 게시에서 동일한 ACL을 사용합니다. 자세한 내용은 [사용자 관리 및 보안](/help/sites-administering/security.md)을 참조하십시오.

## AEM Link Externalizer 구성 {#configuring-the-aem-link-externalizer}

Adobe Target에서 활동을 편집할 때 AEM 작성자 노드에서 URL을 변경하지 않는 한, URL은 **localhost**&#x200B;를 가리킵니다. 내보낸 컨텐츠가 특정 *publish* 도메인을 가리키도록 하려면 AEM Link Externalizer를 구성할 수 있습니다.

>[!NOTE]
>
>또한 [클라우드 구성 추가](/help/sites-administering/experience-fragments-target.md#add-the-cloud-configuration)를 참조하십시오.

AEM 외부 도우미를 구성하려면

>[!NOTE]
>
>자세한 내용은 [URL 표면화](/help/sites-developing/externalizer.md)를 참조하십시오.

1. **https://&lt;server>:&lt;port>/system/console/configMgr.**&#x200B;의 OSGi 웹 콘솔로 이동합니다.
1. **일 CQ Link Externalizer**&#x200B;를 찾아 작성 노드의 도메인을 입력합니다.

   ![chlimage_1-120](assets/aem-externalizer-01.png)
