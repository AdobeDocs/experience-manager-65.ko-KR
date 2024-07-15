---
title: Adobe Target과 통합하기 위한 사전 요구 사항
description: Adobe Target과 통합하기 위한 사전 요구 사항에 대해 알아봅니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: 30813c44-51ac-4e6e-8ee6-4e8baacb1ff9
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: eae057caed533ef16bb541b4ad41b8edd7aaa1c7
workflow-type: tm+mt
source-wordcount: '528'
ht-degree: 7%

---

# Adobe Target과 통합하기 위한 사전 요구 사항{#prerequisites-for-integrating-with-adobe-target}

AEM과 Adobe Target의 [통합](/help/sites-administering/target.md)의 일부로 Adobe Target에 등록하고, 복제 에이전트를 구성하고, 게시 노드에서 활동 설정을 보호해야 합니다.

## Adobe Target에 등록 {#registering-with-adobe-target}

AEM을 Adobe Target과 통합하려면 유효한 Adobe Target 계정이 있어야 합니다. 이 계정에는 최소한 **승인자** 수준의 권한이 있어야 합니다. Adobe Target에 등록하면 클라이언트 코드를 받습니다. AEM을 Adobe Target에 연결하려면 클라이언트 코드와 Adobe Target 로그인 이름과 암호가 필요합니다.

클라이언트 코드는 Adobe Target 서버를 호출할 때 Adobe Target 고객 계정을 식별합니다.

>[!NOTE]
>
>통합을 사용하려면 Target 팀이 계정을 활성화해야 합니다.
>
>그렇지 않은 경우 [고객 지원 Adobe](https://experienceleague.adobe.com/docs/target/using/cmp-resources-and-contact-information.html)에 문의하십시오.

## 대상 복제 에이전트 활성화 {#enabling-the-target-replication-agent}

작성자 인스턴스에서 테스트 및 대상 [복제 에이전트](/help/sites-deploying/replication.md)을(를) 사용하도록 설정해야 합니다. AEM 설치에 [nosamplecontent](/help/sites-deploying/configure-runmodes.md#using-samplecontent-and-nosamplecontent) 실행 모드를 사용한 경우 이 복제 에이전트는 기본적으로 활성화되지 않습니다. 프로덕션 환경 보호에 대한 자세한 내용은 [보안 검사 목록](/help/sites-administering/security-checklist.md)을 참조하십시오.

1. AEM 홈페이지에서 **도구** > **배포** > **복제**&#x200B;를 클릭합니다.
1. **작성자의 에이전트**&#x200B;을(를) 클릭합니다.
1. **테스트 및 대상(테스트 및 대상)** 복제 에이전트를 클릭한 다음 **편집**&#x200B;을 클릭합니다.
1. 사용 옵션을 선택한 다음 **확인**&#x200B;을 클릭합니다.

   >[!NOTE]
   >
   >테스트 및 대상 복제 에이전트를 구성할 때 **전송** 탭에서 URI는 기본적으로 **tnt:///**(으)로 설정됩니다. 이 URI를 **https://admin.testandtarget.omniture.com**(으)로 바꾸지 마십시오.
   >
   >**tnt:///**&#x200B;과의 연결을 테스트하려고 하면 오류가 발생합니다. 이 URI는 내부 전용이므로 예상되는 동작입니다. **연결 테스트**&#x200B;에는 사용하지 마십시오.

## 활동 설정 노드 보안 설정 {#securing-the-activity-settings-node}

일반 사용자가 액세스할 수 없도록 게시 인스턴스에서 활동 설정 노드 **cq:ActivitySettings**&#x200B;를 보호합니다. 활동 설정 노드는 Adobe Target에 대한 활동 동기화를 처리하는 서비스에만 액세스할 수 있어야 합니다.

**cq:ActivitySettings** 노드는 CRXDE lite에서 `/content/campaigns/*nameofbrand*`* *활동 jcr:content 노드 아래의* *예: `/content/campaign/we-retail/master/myactivity/jcr:content/cq:ActivitySettings`에서 사용할 수 있습니다. 이 노드는 구성 요소를 타겟팅한 후에만 만들어집니다.

활동의 jcr:content 아래에 있는 **cq:ActivitySettings** 노드는 다음 ACL에 의해 보호됩니다.

* 모든 사용자에 대해 모두 거부
* &quot;target-activity-authors&quot;에 대해 jcr:read, rep:write 허용(작성자는 기본 제공 이 그룹의 구성원임)
* &quot;targetservice&quot;에 대해 jcr:read, rep:write 허용

이러한 설정은 일반 사용자가 노드 속성에 액세스할 수 없도록 합니다. 작성자 및 게시에서 동일한 ACL을 사용합니다. 자세한 내용은 [사용자 관리 및 보안](/help/sites-administering/security.md)을 참조하십시오.

## AEM 링크 외부화 구성 {#configuring-the-aem-link-externalizer}

Adobe Target에서 활동을 편집할 때 AEM 작성자 노드에서 URL을 변경하지 않으면 URL이 **localhost**&#x200B;을(를) 가리킵니다. 내보낸 콘텐츠가 특정 *publish* 도메인을 가리키도록 하려면 AEM 링크 외부화를 구성할 수 있습니다.

>[!NOTE]
>
>[클라우드 구성 추가](/help/sites-administering/experience-fragments-target.md#add-the-cloud-configuration)도 참조하세요.

AEM 외부화를 구성하려면:

>[!NOTE]
>
>자세한 내용은 [URL 외부화](/help/sites-developing/externalizer.md)를 참조하십시오.

1. **https://&lt;server>:&lt;port>/system/console/configMgr에서 OSGi 웹 콘솔로 이동합니다.**
1. **일 CQ 링크 외부화**&#x200B;를 찾아 작성자 노드의 도메인을 입력하십시오.

   ![일 CQ 링크 외부화](assets/aem-externalizer-01.png)
