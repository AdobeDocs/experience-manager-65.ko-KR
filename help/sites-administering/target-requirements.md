---
title: Adobe Target과 통합하기 위한 사전 요구 사항
description: Adobe Target과 통합하기 위한 사전 요구 사항에 대해 알아봅니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: 30813c44-51ac-4e6e-8ee6-4e8baacb1ff9
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '528'
ht-degree: 7%

---

# Adobe Target과 통합하기 위한 사전 요구 사항{#prerequisites-for-integrating-with-adobe-target}

의 일부로 [AEM과 Adobe Target 통합](/help/sites-administering/target.md), Adobe Target에 등록하고, 복제 에이전트를 구성하고, 게시 노드에서 보안 활동 설정을 해야 합니다.

## Adobe Target에 등록 {#registering-with-adobe-target}

AEM을 Adobe Target과 통합하려면 유효한 Adobe Target 계정이 있어야 합니다. 이 계정에는 다음이 있어야 합니다. **승인자** 최소한 권한 레벨만 지정할 수 있습니다. Adobe Target에 등록하면 클라이언트 코드를 받습니다. AEM을 Adobe Target에 연결하려면 클라이언트 코드와 Adobe Target 로그인 이름과 암호가 필요합니다.

클라이언트 코드는 Adobe Target 서버를 호출할 때 Adobe Target 고객 계정을 식별합니다.

>[!NOTE]
>
>통합을 사용하려면 Target 팀이 계정을 활성화해야 합니다.
>
>그렇지 않은 경우 다음으로 문의하십시오. [Adobe 고객 지원 센터](https://experienceleague.adobe.com/docs/target/using/cmp-resources-and-contact-information.html).

## 대상 복제 에이전트 활성화 {#enabling-the-target-replication-agent}

테스트 및 타겟 [복제 에이전트](/help/sites-deploying/replication.md) 작성자 인스턴스에서 을 활성화해야 합니다. 다음을 사용한 경우 이 복제 에이전트는 기본적으로 활성화되지 않습니다. [nosamplecontent](/help/sites-deploying/configure-runmodes.md#using-samplecontent-and-nosamplecontent) AEM 설치를 위한 실행 모드입니다. 프로덕션 환경 보호에 대한 자세한 내용은 [보안 검사 목록](/help/sites-administering/security-checklist.md).

1. AEM 홈페이지에서 **도구** > **배포** > **복제**.
1. 클릭 **작성자의 에이전트**.
1. 다음을 클릭합니다. **테스트 및 타겟(테스트 및 타겟)** 복제 에이전트를 선택하고 **편집**.
1. 활성화 옵션을 선택한 다음 를 클릭합니다. **확인**.

   >[!NOTE]
   >
   >Test and Target 복제 에이전트를 구성할 때에서 **전송** 탭에서 URI는 기본적으로 로 설정됩니다. **tnt:///**. 이 URI를 다음으로 바꾸기 금지 **https://admin.testandtarget.omniture.com**.
   >
   >과의 연결을 테스트하려는 경우 **tnt:///**, 오류가 발생합니다. 이 URI는 내부용이므로 예상되는 동작입니다. **연결 테스트**.

## 활동 설정 노드 보안 설정 {#securing-the-activity-settings-node}

일반 사용자가 액세스할 수 없도록 게시 인스턴스에서 활동 설정 노드 **cq:ActivitySettings**&#x200B;를 보호합니다. 활동 설정 노드는 Adobe Target에 대한 활동 동기화를 처리하는 서비스에만 액세스할 수 있어야 합니다.

다음 **cq:ActivitySettings** 노드는 아래의 CRXDE lite에서 사용할 수 있습니다 `/content/campaigns/*nameofbrand*`* *활동 jcr:content 노드 아래에* *예, `/content/campaign/we-retail/master/myactivity/jcr:content/cq:ActivitySettings`. 이 노드는 구성 요소를 타겟팅한 후에만 만들어집니다.

다음 **cq:ActivitySettings** 활동의 jcr:content 아래에 있는 노드는 다음 ACL에 의해 보호됩니다.

* 모든 사용자에 대해 모두 거부
* &quot;target-activity-authors&quot;에 대해 jcr:read, rep:write 허용(작성자는 기본 제공 이 그룹의 구성원임)
* &quot;targetservice&quot;에 대해 jcr:read, rep:write 허용

이러한 설정은 일반 사용자가 노드 속성에 액세스할 수 없도록 합니다. 작성자 및 게시에서 동일한 ACL을 사용합니다. 다음을 참조하십시오 [사용자 관리 및 보안](/help/sites-administering/security.md) 추가 정보.

## AEM 링크 외부화 구성 {#configuring-the-aem-link-externalizer}

Adobe Target에서 활동을 편집할 때 URL은 다음을 가리킵니다. **localhost** AEM 작성자 노드의 URL을 변경하지 않는 한, 내보낸 콘텐츠가 특정 콘텐츠를 가리키도록 하려면 AEM 링크 외부화를 구성할 수 있습니다 *게시* 도메인.

>[!NOTE]
>
>참조: [클라우드 구성 추가](/help/sites-administering/experience-fragments-target.md#add-the-cloud-configuration).

AEM 외부화를 구성하려면:

>[!NOTE]
>
>자세한 내용은 다음을 참조하십시오. [URL 표면화](/help/sites-developing/externalizer.md).

1. 의 OSGi 웹 콘솔로 이동합니다. **https://&lt;server>:&lt;port>/system/console/configMgr.**
1. 찾기 **일별 CQ 링크 외부화** 작성자 노드의 도메인을 입력합니다.

   ![일별 CQ 링크 외부화](assets/aem-externalizer-01.png)
