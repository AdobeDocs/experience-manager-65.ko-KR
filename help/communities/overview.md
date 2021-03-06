---
title: AEM Communities 개요
seo-title: AEM Communities 개요
description: AEM Communities 기능 및 설정에 대한 개요
seo-description: AEM Communities 기능 및 설정에 대한 개요
uuid: 14405847-36ae-4958-bdc6-d799ecd05f06
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 44374006-f711-4af8-a1fe-f89164f79581
docset: aem65
exl-id: d6243dff-a067-455c-a326-5f451f225efd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1446'
ht-degree: 3%

---

# AEM Communities 개요 {#aem-communities-overview}

AEM(Adobe Experience Manager) Communities는 성능 및 사이트 관리를 향상시키고 사이트 방문자가 중요한 커뮤니티 구성원으로 전환할 수 있도록 권장하는 On-Premise 커뮤니티 사이트를 빠르게 생성하는 기능을 제공합니다.

<!--
Contact your account representative for information regarding licensing of AEM Communities as well as additional licensing for enablement features and Adobe Analytics.
-->

## 커뮤니티 기능 {#communities-features}

AEM Communities을 사용하면 사이트 방문자와의 관계를 개발할 수 있으며, 이러한 관계는 다음과 같습니다.

* **** 블로그, Q&amp;A 및 이벤트 달력,
* 반면에 **포럼, 댓글 및 기타 커뮤니티 콘텐츠를 통해 통찰력**&#x200B;을 얻는 동안(종종 사용자 생성 콘텐츠(UGC)라고 함).
* 게시 환경의 신뢰할 수 있는 구성원에 의해 **moderation**&#x200B;을 허용합니다.
* **twitter** 및 Facebook과 소셜 로그인,
* **커뮤니티** 컨텐츠의 인라인 번역,
* **게시된 커뮤니티** 사이트에서 커뮤니티 그룹 만들기,
* **** Scoringto award,
* **파일 공유**,
* **** 알림 및  **활동 스트림**,
* 사용자 생성 컨텐츠에서 **태그 지정** (@mention)된 다른 등록 구성원에게 주의를 유도할 수 있도록 허용합니다.
* 지원 구성 요소(예: 카탈로그 및 코스 재생, 할당, 파일 라이브러리)에서 **키보드 탐색**&#x200B;을 지원합니다.

커뮤니티 기능은 GitHub.com에서 공개적으로 제공되는 [AEM 데모 컴퓨터](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki)를 사용하거나 새로운 We.Retail 참조 구현을 통해 보여줄 수 있습니다.

## 커뮤니티 사이트 {#community-sites}

커뮤니티 사이트는 간단한 마법사를 사용하여 만든 AEM 사이트로서, 이를 통해 사이트에 사전 연결되는 많은 일반적인 기능이 있는 웹 사이트를 만듭니다.

[사이트 만들기 마법사](/help/communities/sites-console.md):

* 선택한 [커뮤니티 사이트 템플릿](/help/communities/sites.md)을 기반으로 사이트의 기능을 결합합니다.

   * [커뮤니티 함수](#community-functions)에서 작성
   * 옵션 [커뮤니티 그룹](#communitygroups) 기능

* 설정을 사용하여 다음을 구성합니다.

   * 중재
   * 로그인
   * 번역

* 필수 기능 제공:

   * 반응형 디자인:[Twitter Bootstrap 테마 사용](https://getbootstrap.com)

   * 로그인 :자체 등록, [소셜 로그인](/help/communities/social-login.md), 사용자 프로필

      * 알림:
구성원은 자신과 관련된 이벤트를 보고, 사용자가 생성한 컨텐츠는 [@mentioned](/help/communities/overview.md#mentionssupport)입니다.

      * 메시징:구성원은 커뮤니티 사이트 내에서 메시지를 보내거나 받을 수 있습니다.
      * 검색:커뮤니티 사이트 내에서 검색할 수 있는 기능.
      * 언어 전환:[다국어 사이트](/help/sites-administering/translation.md)에 사용할 언어를 선택할 수 있습니다.

      * 관리:커뮤니티 사이트 내에서 사용자를 중재하고 관리할 권한이 있는 구성원이 액세스할 수 있습니다.

* 페이지 수준의 여러 작성 단계가 제거됩니다.

   * 브랜딩:커뮤니티 사이트의 모든 페이지에 표시할 배너 이미지의 선택적 업로드
   * 탐색 메뉴:탐색 링크는 커뮤니티 사이트 템플릿에 포함된 기능에 대해 제공됩니다.

새 커뮤니티 사이트를 쉽게 만들 수 있도록 하려면 [AEM Communities 시작하기](/help/communities/getting-started.md)를 방문하십시오.

## 커뮤니티 컨텐츠 지속성 {#community-content-persistence}

커뮤니티 컨텐츠의 성능 및 동기화를 개선하기 위해 AEM Communities에는 모든 AEM(작성자 및 게시) 인스턴스 간에 공유되는 사용자 생성 콘텐츠(UGC)를 위한 공용 저장소가 필요합니다.

SRP(Storage Resource Provider)를 통해 쉽게 액세스할 수 있습니다. SRP는 기본 토폴로지와 별도의 액세스를 제공하고 UGC를 위한 공용 저장소를 지원합니다.

커뮤니티 컨텐츠 지속성 및 권장 배포에 대해 자세히 알아보려면:

* [UGC에 사용할 수 있는 SRP 저장소 옵션에 대해](/help/communities/working-with-srp.md) 설명하는 커뮤니티 컨텐츠 저장소
* [권장 토폴로지](/help/communities/topologies.md): 사용 사례 및 SRP 선택을 기반으로 토폴로지를 설명합니다.
* [AEM 6.5로 이동할 때 UGC에 대한 유용한 정보를 제공하는 AEM 6.5 Communities로 업그레이드](/help/communities/upgrade.md).

## 커뮤니티 콘솔 {#communities-consoles}

작성 환경에서 전역 탐색 콘솔은 다음을 포함하는 [커뮤니티 콘솔](/help/communities/consoles.md)에 액세스할 수 있습니다.

* [사이트](/help/communities/sites-console.md) 콘솔

   * 사이트 만들기
   * 사이트 편집
   * 사이트 관리
   * [커뮤니티 ](/help/communities/groups.md) 그룹콘솔

* [](/help/communities/moderation.md) Moderationconsole

   * 작성자 및 게시 환경을 위한 일반적인 벌크 조정 UI입니다.
   * 새 필터링 기준.

* [구성원 및 ](/help/communities/members.md) 그룹관리 콘솔

   * 작성 환경에서 게시 측 사용자(구성원)를 만들고 관리하는 기능을 제공합니다.
   * 구성원을 금지할 수 있는 기능을 제공합니다.
   * 작성 환경에서 게시 측 사용자 그룹(구성원 그룹)을 만들고 관리하는 기능을 제공합니다.

* [](/help/communities/reports.md) Reportconsole

   * 할당, 게시물 및 보기에 대한 보고서를 생성할 수 있는 기능을 제공합니다.

* [](/help/communities/resources.md) 리소스 콘솔

   * 지원 리소스 및 학습 경로를 만드는 기능을 제공합니다.
   * 지원 리소스 및 학습 경로에 대한 보고서에 대한 액세스 권한을 제공합니다.

전역 도구 콘솔에서는 다음 커뮤니티 도구에 액세스할 수 있습니다.

* [사이트 ](/help/communities/tools.md#sitetemplatesconsole) 템플릿 콘솔

   * 커뮤니티 사이트 템플릿을 만들고 관리합니다.

* [그룹 ](/help/communities/tools.md#grouptemplatesconsole) 템플릿 콘솔

   * 커뮤니티 그룹 템플릿을 만들고 관리합니다.

* [커뮤니티 ](/help/communities/tools.md#communityfunctionsconsole) 기능 콘솔

   * 커뮤니티 기능을 만들고 관리합니다.

* [스토리지 ](/help/communities/tools.md#storageconfiguratonconsole) 구성 콘솔

   * 사이트에 대한 [일반 저장소](/help/communities/working-with-srp.md)를 선택하고 구성합니다.

* [구성 요소 가이드](/help/communities/components-guide.md)

   * 모든 Communities 구성 요소의 샘플에 기본 구성과 실험할 수 있는 기능을 제공하는 샘플 사이트 [커뮤니티 구성 요소](https://localhost:4502/editor.html/content/community-components/en.html)

## 커뮤니티 사이트 템플릿 {#community-site-templates}

커뮤니티 사이트 만들기는 샘플 사이트와 독립적인 커뮤니티 사이트를 빠르게 설정할 수 있도록 커뮤니티 사이트 템플릿 선택에 따라 수행됩니다.

커뮤니티 기능 및 커뮤니티 그룹 템플릿으로 구성된 커뮤니티 사이트 템플릿은 로그인, 사용자 프로필, 메시징, 사이트 메뉴, 검색, 테마 및 브랜딩 기능을 포함한 커뮤니티 사이트의 구조를 제공합니다.

[사이트 템플릿 콘솔](/help/communities/sites.md)을 참조하십시오.

## 커뮤니티 기능 {#community-functions}

커뮤니티 경험에 필요한 기능은 잘 알려져 있습니다. AEM Communities을 사용하면 이러한 기능을 커뮤니티 기능이라고 하는 빌딩 블록으로 사용할 수 있습니다.

커뮤니티 함수는 일반적인 AEM 페이지에는 커뮤니티 사이트 템플릿에 쉽게 통합되는 기능에 함께 연결된 구성 요소가 포함되어 있습니다.

[커뮤니티 함수 콘솔](/help/communities/functions.md)을 참조하십시오.

## 커뮤니티 그룹 및 그룹 템플릿 {#community-groups-and-group-templates}

커뮤니티 그룹 기능은 작성자 및 게시 환경 모두에서 권한이 있는 사용자와 커뮤니티 구성원이 커뮤니티 사이트 내에서 하위 커뮤니티를 동적으로 만들 수 있는 기능입니다.

작성 환경에서 템플릿의 구조에 [그룹 함수](/help/communities/functions.md#groups-function)가 포함된 경우 기존 커뮤니티 사이트 내에 커뮤니티 그룹(하위 커뮤니티)을 만들거나 기존 그룹 내에 중첩할 수 있습니다.

커뮤니티 그룹을 만들려면 커뮤니티 그룹 페이지의 디자인을 제공하는 커뮤니티 그룹 템플릿을 선택해야 합니다. 그룹 기능이 템플릿 구조에 추가되면 그룹 템플릿을 지정하거나 새 커뮤니티 그룹을 만들 때 템플릿 선택을 제공하도록 구성됩니다.

참고 항목:

* [사이트 그룹 ](/help/communities/groups.md) 콘솔 작성 환경에서 하위 커뮤니티를 만들 수 있습니다.
* [그룹 템플릿 ](/help/communities/tools-groups.md) 콘솔 그룹에 대한 사이트 구조를 만들 수 있습니다.
* [중첩 그룹을 ](/help/communities/getting-started.md) 포함한 커뮤니티 사이트를 빠르게 만들기 위한 자습서에서는 AEM Communities 시작하기 를 참조하십시오.

## 커뮤니티 구성 요소 {#community-components}

커뮤니티 사이트가 빌드된 [커뮤니티 구성 요소](/help/communities/author-communities.md)는 AEM 사이트에 커뮤니티 기능을 추가하는 데 사용할 수 있습니다.

[커뮤니티 구성 요소 안내서](/help/communities/components-guide.md)는 구성 요소를 탐색하는 데 사용할 수 있습니다.

## 커뮤니티 유형 {#types-of-communities}

### 참여 커뮤니티 {#engagement-community}

참여 커뮤니티는 고객이 커뮤니티의 구성원으로서 상호 작용할 수 있도록 알리고, 피드백을 요청하고, 참여하도록 하는 데 중점을 둔 커뮤니티 사이트입니다.

참여 커뮤니티의 기능은 다음과 같습니다.

* 로그인
* 메시지
* 포럼
* 댓글
* 검토
* 등급
* 투표
* 블로그
* 그룹
* 달력
* 번역
* 중재
* 알림
* 점수 및 배지
* Analytics 보고

새 참여 커뮤니티를 빠르게 만들 수 있는 편리한 기능을 경험하려면 [AEM Communities 시작하기](/help/communities/getting-started.md)를 방문하십시오.

### 지원 커뮤니티 {#enablement-community}

지원 커뮤니티는 온라인 학습을 위한 기능을 포함하는 커뮤니티 사이트입니다.

지원 커뮤니티의 기능은 다음과 같습니다.

* [참여 커뮤니티](#engagement-community)의 모든 기능.
* 컨텐츠 및 학습을 할당하는 기능. 구성원 및 구성원 그룹에 대한 리소스
* 퀴즈 및 테스트와 같은 SCORM 콘텐츠를 지원합니다.
* 지정 완료 추적.
* 보고 및 분석에 대한 액세스 권한.
* 포럼, 메시징, 댓글 및 등급을 통해 학습 리소스에 대한 대화를 수행할 수 있습니다.

[지원 추가 기능이 구성된 경우 프로덕션 환경에서 사용할 추가 라이선스가 필요한 지원 커뮤니티를 만들 수 있습니다.](/help/communities/enablement.md) 지원 커뮤니티 사이트에는 [할당 함수](#community-functions)가 포함됩니다.

새 지원 커뮤니티를 쉽게 만들 수 있도록 하려면 [AEM Communities for Enablement](/help/communities/getting-started-enablement.md)를 방문하십시오.

## AEM 데모 컴퓨터 {#aem-demo-machine}

[AEM 데모 시스템](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine)은 AEM [사이트](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Sites), [자산](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Assets), [커뮤니티](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Communities), [앱](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Apps) 및 [Forms](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Forms)에 대한 데모를 관리하고 실행하며, 이 데모는 QuickStart 인스턴스를 시작하는 것보다 더 많은 설정이 필요합니다. AEM 데모 시스템은 MongoDB, Solr, MySQL, FFmpeg 및 이메일 서버와 같은 추가 [인프라](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Infrastructure)를 설정합니다.

AEM 데모 시스템에는 다음이 포함되어 있습니다.

* [그래픽 사용자 인터페이스](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/User%20Interface)
* 구성 가능한 [속성](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Properties) 및 [타겟](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Command%20Line)이 있는 Apache ANT 스크립트.

* 설치할 패키지.

AEM 데모 시스템은 Windows, MacOS 및 Linux에서 CQ 5.5, CQ 5.6.1, AEM 6.0, AEM 6.1, AEM 6.2, AEM 6.3 및 AEM 6.4를 사용하여 성공적으로 테스트되었습니다.

AEM 데모 시스템에는 유효한 AEM 라이센스가 필요합니다.

>[!NOTE]
>
>AEM 데모 컴퓨터에 대한 [비디오 소개](https://www.youtube.com/watch?v=zEE_zkR9fVQ&amp;feature=youtu.be)를 (13:26).

## AEM Communities 설명서 {#aem-communities-documentation}

* 권장 배포에 대해 알아보려면 [Communities 배포](deploy-communities.md)를 방문하십시오.
* 커뮤니티 사이트 만들기, 커뮤니티 그룹 추가, 커뮤니티 사이트 템플릿 구성, 커뮤니티 컨텐츠 중재, 구성원 관리, 태깅, 알림, 점수 책정 및 배지에 대해 알아보려면 [커뮤니티 사이트 관리](administer-landing.md)를 방문하십시오.
* SCF(소셜 구성 요소 프레임워크)에 대해 알아보고 커뮤니티 구성 요소 및 기능을 사용자 지정하려면 [커뮤니티 개발](communities.md)을 방문하십시오.
* 커뮤니티 구성 요소를 사용하여 작성하고 구성하는 방법을 배우려면 [커뮤니티 구성 요소 작성](author-communities.md)을 방문하십시오.
