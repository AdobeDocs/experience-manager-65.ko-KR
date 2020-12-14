---
title: Adobe Target과 통합하기 위한 사전 요구 사항
seo-title: Adobe Target과 통합하기 위한 사전 요구 사항
description: Adobe Target과 통합하기 위한 사전 요구 사항을 살펴보십시오.
seo-description: Adobe Target과 통합하기 위한 사전 요구 사항을 살펴보십시오.
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
ht-degree: 6%

---


# Adobe Target{#prerequisites-for-integrating-with-adobe-target}과(와) 통합하기 위한 사전 요구 사항

AEM 및 Adobe Target](/help/sites-administering/target.md)의 [통합 과정의 일부로, 게시 노드에서 Adobe Target에 등록하고, 복제 에이전트를 구성하고, 보안 활동 설정을 구성해야 합니다.

## Adobe Target {#registering-with-adobe-target}에 등록

AEM을 Adobe Target과 통합하려면 유효한 Adobe Target 계정이 있어야 합니다. 이 계정에는 최소 **승인자** 수준 권한이 있어야 합니다. Adobe Target에 등록하면 클라이언트 코드를 받게 됩니다. AEM을 Adobe Target에 연결하려면 클라이언트 코드와 Adobe Target 로그인 이름 및 암호가 필요합니다.

클라이언트 코드는 Adobe Target 서버를 호출할 때 Adobe Target 고객 계정을 식별합니다.

>[!NOTE]
>
>통합을 사용하려면 Target 팀에서 계정을 활성화해야 합니다.
>
>그렇지 않은 경우 [Adobe 고객 지원 센터](https://docs.adobe.com/content/help/en/target/using/cmp-resources-and-contact-information.html)에 문의하십시오.

## Target 복제 에이전트 {#enabling-the-target-replication-agent} 활성화

작성자 인스턴스에서 테스트 및 Target [복제 에이전트](/help/sites-deploying/replication.md)를 사용하도록 설정해야 합니다. AEM 설치에 [nosamplecontent](/help/sites-deploying/configure-runmodes.md#using-samplecontent-and-nosamplecontent) 실행 모드를 사용한 경우 이 복제 에이전트는 기본적으로 활성화되지 않습니다. 제작 환경 보안에 대한 자세한 내용은 [보안 검사 목록](/help/sites-administering/security-checklist.md)을 참조하십시오.

1. AEM 홈 페이지에서 **도구** > **배포** > **복제**&#x200B;를 클릭하거나 탭합니다.
1. 작성자&#x200B;**의 에이전트**&#x200B;를 클릭하거나 탭합니다.
1. **테스트 및 Target(테스트 및 대상)** 복제 에이전트를 클릭하거나 탭한 다음 **편집**&#x200B;을 클릭하거나 탭합니다.
1. 사용 옵션을 선택한 다음 **확인**&#x200B;을 클릭하거나 탭합니다.

   >[!NOTE]
   >
   >테스트 및 Target 복제 에이전트를 구성할 때 **전송** 탭에서 URI는 기본적으로 **tnt:///**&#x200B;으로 설정됩니다. 이 URI를 **https://admin.testandtarget.omniture.com**&#x200B;로 바꾸지 마십시오.
   >
   >**tnt:///**&#x200B;와의 연결을 테스트하려고 하면 오류가 발생합니다. 이 URI는 내부용으로만 사용되며 **Test Connection**&#x200B;과 함께 사용해서는 안 됩니다.

## 활동 설정 노드 {#securing-the-activity-settings-node} 보안

일반 사용자가 액세스할 수 없도록 게시 인스턴스에서 활동 설정 노드 **cq:ActivitySettings**&#x200B;를 보호해야 합니다. 활동 설정 노드는 Adobe Target에 대한 활동 동기화를 처리하는 서비스만 액세스할 수 있어야 합니다.

**cq:ActivitySettings** 노드는 jcr:content 노드;**예 `/content/campaign/we-retail/master/myactivity/jcr:content/cq:ActivitySettings`의 활동 아래의 `/content/campaigns/*nameofbrand*`**&#x200B;의 CRXDE lite에서 사용할 수 있습니다. 이 노드는 구성 요소를 타깃팅한 후에만 만들어집니다.

활동의 jcr:content 아래의 **cq:ActivitySettings** 노드는 다음 ACL에 의해 보호됩니다.

* 모든 사용자를 위한 모두 거부
* &quot;target-activity-authors&quot;에 jcr:read,rep:write 허용(작성자는 즉시 이 그룹의 구성원임)
* &quot;대상 서비스&quot;에 대해 jcr:read,rep:쓰기 허용

이러한 설정을 사용하면 일반 사용자가 노드 속성에 액세스할 수 없습니다. 작성자와 게시 시 동일한 ACL을 사용합니다. 자세한 내용은 [사용자 관리 및 보안](/help/sites-administering/security.md)을 참조하십시오.

## AEM Link Externalizer {#configuring-the-aem-link-externalizer} 구성

Adobe Target에서 활동을 편집할 때 AEM 작성자 노드에서 URL을 변경하지 않는 한 URL은 **localhost**&#x200B;을 가리킵니다. 내보낸 내용이 특정 *publish* 도메인을 가리키도록 하려면 AEM 링크 외부자를 구성할 수 있습니다.

>[!NOTE]
>
>[클라우드 구성 추가](/help/sites-administering/experience-fragments-target.md#add-the-cloud-configuration)를 참조하십시오.

AEM Externalizer를 구성하려면:

>[!NOTE]
>
>자세한 내용은 [URL 외부화를 참조하십시오](/help/sites-developing/externalizer.md).

1. **https://&lt;server>:&lt;port>/system/console/configMgr.**&#x200B;의 OSGi 웹 콘솔로 이동합니다.
1. **Day CQ Link Externalizer**&#x200B;를 찾아 작성 노드의 도메인을 입력합니다.

   ![chlimage_1-120](assets/aem-externalizer-01.png)

