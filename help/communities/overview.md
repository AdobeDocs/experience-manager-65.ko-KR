---
title: AEM Communities 개요
seo-title: AEM Communities 개요
description: AEM Communities 기능 및 설정 개요
seo-description: AEM Communities 기능 및 설정 개요
uuid: 14405847-36ae-4958-bdc6-d799ecd05f06
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 44374006-f711-4af8-a1fe-f89164f79581
docset: aem65
translation-type: tm+mt
source-git-commit: 48afa2146d0dcbab4beaa1044645c269b49fd7ff

---


# AEM Communities 개요 {#aem-communities-overview}

AEM(Adobe Experience Manager) Communities는 성능 및 사이트 관리를 향상시키고 사이트 방문자가 중요한 커뮤니티 구성원으로 전환할 수 있도록 권장하는 On-Premise 커뮤니티 사이트를 빠르게 생성하는 기능을 제공합니다.

AEM Communities 라이선스와 지원 기능 및 Adobe Analytics에 대한 추가 라이선스에 대한 자세한 내용은 계정 담당자에게 문의하십시오.

## 커뮤니티 기능 {#communities-features}

AEM Communities를 사용하면 사이트 방문자와의 관계를 개발할 수 있습니다.

* **블로그** , Q&amp;A 및 이벤트 일정을 통해 알려줍니다.
* 포럼, 주석 및 기타 커뮤니티 컨텐츠를 통해 통찰력을 **** 얻는 동안 UGC(사용자 생성 컨텐츠)라고도 합니다.
* 게시 환경에서 신뢰할 수 있는 구성원이 **중재할** 수 있도록 해줍니다.
* **Twitter 및 Facebook을 통한 소셜 로그인** ,
* **커뮤니티 콘텐츠의 인라인 번역** ,
* **게시된 커뮤니티 사이트에서 커뮤니티 그룹 만들기** ,
* **배지** 수상을 위한 점수,
* **파일 공유**,
* **알림** 및 **활동 스트림**,
* 사용자 생성 컨텐츠에 등록된 다른 구성원에 대한 **태그 지정** (@mention)을 허용하여 관심을 유도할 수 있습니다.
* 활성 구성 요소(예: 카탈로그 및 강좌 재생, 할당, 파일 라이브러리)에서 **키보드 탐색을** 지원합니다.

커뮤니티 기능은 GitHub.com [에서 공개적으로](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki) 제공되는 AEM Demo Machine 또는 새로운 We.Retail 참조 구현을 통해 입증될 수 있습니다.

## 커뮤니티 사이트 {#community-sites}

커뮤니티 사이트는 간단한 마법사를 사용하여 만든 AEM 사이트로서, 사이트에 미리 연결된 많은 일반적인 기능이 있는 웹 사이트를 만듭니다.

사이트 [만들기 마법사](/help/communities/sites-console.md):

* 선택한 [커뮤니티 사이트 템플릿을](/help/communities/sites.md) 기반으로 사이트의 기능 취합:

   * 커뮤니티 기능을 통해 [구축](#community-functions)
   * 선택적 [커뮤니티 그룹](#communitygroups) 기능

* 설정을 사용하여 다음을 구성합니다.

   * 중재
   * login
   * 번역

* 필수 기능 제공:

   * 반응형 디자인:twitter [Bootstrap 테마 사용](https://getbootstrap.com)

   * 로그인:자가 등록, [소셜 로그인](/help/communities/social-login.md), 사용자 프로필

      * 알림:구성원은 관련성 이벤트를 보고, 사용자가 생성한 컨텐츠는 [@에 명시되어](/help/communities/overview.md#mentionssupport)있습니다.

      * 메시지:회원은 커뮤니티 사이트 내에서 메시지를 보내거나 받을 수 있습니다.
      * 검색:커뮤니티 사이트 내에서 검색할 수 있는 기능
      * 언어 전환:다국어 사이트의 [](/help/sites-administering/translation.md)언어를 선택할 수 있는 기능

      * 관리:권한이 있는 구성원이 커뮤니티 사이트 내에서 사용자를 중재하고 관리할 수 있는 액세스.

* 다음과 같은 여러 페이지 수준 작성 단계를 수행하지 않아도 됩니다.

   * 브랜딩:커뮤니티 사이트의 모든 페이지에 표시할 배너 이미지의 선택적 업로드
      * 탐색 메뉴:탐색 링크는 커뮤니티 사이트 템플릿에 포함된 기능에 대해 제공됩니다.

새 커뮤니티 사이트를 빠르게 만드는 데 도움이 되도록 하려면 AEM Communities [시작하기를 참조하십시오](/help/communities/getting-started.md).

## 커뮤니티 컨텐츠 지속성 {#community-content-persistence}

커뮤니티 콘텐츠의 성능 및 동기화를 개선하기 위해 AEM Communities는 모든 AEM(작성자 및 게시) 인스턴스 간에 공유된 사용자 생성 콘텐츠(UGC)에 대한 공용 저장소가 필요합니다.

커뮤니티 컨텐츠는 SRP(Storage Resource Provider)를 통해 쉽게 액세스할 수 있습니다. SRP는 기본 토폴로지와 별도로 액세스할 수 있는 레이어를 제공하며 UGC에 대한 공통 저장소를 지원합니다.

커뮤니티 컨텐츠 지속성 및 권장 배포에 대한 자세한 내용은 다음을 참조하십시오.

* [UGC에](/help/communities/working-with-srp.md)사용할 수 있는 SRP 스토리지 옵션에 대해 설명하는 커뮤니티 컨텐츠 스토리지
* [사용 사례](/help/communities/topologies.md)및 SRP 선택에 따라 토폴로지를 설명하는 권장 토폴로지
* [AEM 6.5 Communities로 업그레이드하면](/help/communities/upgrade.md)AEM 6.5로 이동할 때 UGC에 대한 유용한 정보를 제공합니다.

## 커뮤니티 콘솔 {#communities-consoles}

작성 환경에서 전역 탐색 콘솔은 다음을 포함하는 [커뮤니티 콘솔에](/help/communities/consoles.md)대한 액세스를 제공합니다.

* [사이트](/help/communities/sites-console.md) 콘솔

   * 사이트 제작
   * 사이트 편집
   * 사이트 관리
   * [커뮤니티 그룹](/help/communities/groups.md) 콘솔

* [중재](/help/communities/moderation.md) 콘솔

   * 작성 및 게시 환경을 위한 공통 벌크 중재 UI.
   * 새로운 필터링 기준.

* [구성원 및 그룹](/help/communities/members.md) 관리 콘솔

   * 작성 환경에서 게시 측 사용자(구성원)를 만들고 관리하는 기능을 제공합니다.
   * 구성원을 금지하는 기능을 제공합니다.
   * 작성 환경에서 게시 측 사용자 그룹(구성원 그룹)을 만들고 관리하는 기능을 제공합니다.

* [보고서](/help/communities/reports.md) 콘솔

   * 할당, 게시물 및 보기에 대한 보고서를 생성하는 기능을 제공합니다.

* [리소스](/help/communities/resources.md) 콘솔

   * 역량 강화 리소스 및 학습 경로를 만들 수 있는 기능을 제공합니다.
   * 역량 강화 리소스 및 학습 경로에 대한 보고서에 액세스할 수 있습니다.

전역 도구 콘솔에서는 다음 커뮤니티 도구에 액세스할 수 있습니다.

* [사이트 템플릿](/help/communities/tools.md#sitetemplatesconsole) 콘솔

   * 커뮤니티 사이트 템플릿 만들기 및 관리

* [그룹 템플릿](/help/communities/tools.md#grouptemplatesconsole) 콘솔

   * 커뮤니티 그룹 템플릿 만들기 및 관리

* [커뮤니티 기능](/help/communities/tools.md#communityfunctionsconsole) 콘솔

   * 커뮤니티 기능 만들기 및 관리

* [스토리지 구성](/help/communities/tools.md#storageconfiguratonconsole) 콘솔

   * 사이트에 대한 [공통 저장소를](/help/communities/working-with-srp.md) 선택하고 구성합니다.

* [구성 요소 가이드](/help/communities/components-guide.md)

   * 모든 커뮤니티 구성 [요소의 샘플과](https://localhost:4502/editor.html/content/community-components/en.html)기본 구성을 제공하고 이를 실험해 볼 수 있는 기능을 제공하는 샘플 사이트 커뮤니티 구성 요소입니다.

## 커뮤니티 사이트 템플릿 {#community-site-templates}

커뮤니티 사이트 만들기는 커뮤니티 사이트 템플릿 선택을 기반으로 하여 샘플 사이트와 독립적인 커뮤니티 사이트를 신속하게 설정할 수 있습니다.

커뮤니티 기능과 커뮤니티 그룹 템플릿으로 구성된 커뮤니티 사이트 템플릿은 로그인, 사용자 프로필, 메시지, 사이트 메뉴, 검색, 테마 및 브랜딩 기능을 포함하여 커뮤니티 사이트의 구조를 제공합니다.

사이트 [템플릿 콘솔을](/help/communities/sites.md)참조하십시오.

## 커뮤니티 기능 {#community-functions}

커뮤니티 경험에 필요한 기능은 잘 알려져 있습니다. AEM Communities에서는 이러한 기능을 커뮤니티 기능이라고 하는 빌드 블록으로 사용할 수 있습니다.

커뮤니티 기능은 일반적인 AEM 페이지로서 커뮤니티 사이트 템플릿에 쉽게 통합되는 기능에 연결된 구성 요소를 포함합니다.

커뮤니티 [기능 콘솔을](/help/communities/functions.md)참조하십시오.

## 커뮤니티 그룹 및 그룹 템플릿 {#community-groups-and-group-templates}

커뮤니티 그룹 기능은 권한이 있는 사용자 및 작성자 및 게시 환경 모두에서 커뮤니티 구성원이 커뮤니티 사이트 내에서 하위 커뮤니티를 동적으로 만들 수 있는 기능입니다.

작성 환경에서 템플릿 구조에 그룹 함수가 [들어 있으면 기존 커뮤니티 사이트 내에 커뮤니티 그룹(하위 커뮤니티)을 만들거나 기존 그룹 내에 중첩될 수](/help/communities/functions.md#groups-function)있습니다.

커뮤니티 그룹을 만들려면 커뮤니티 그룹 페이지의 디자인을 제공하는 커뮤니티 그룹 템플릿을 선택해야 합니다. 그룹 함수가 템플릿 구조에 추가되면, 그룹 템플릿을 하나 지정하거나 새 커뮤니티 그룹을 만들 때 템플릿 선택을 제공하도록 구성됩니다.

참고 항목:

* [사이트 그룹 콘솔을](/help/communities/groups.md) 참조하십시오.
* [그룹 템플릿 콘솔을](/help/communities/tools-groups.md) 참조하십시오.
* [AEM Communities](/help/communities/getting-started.md) 시작하기를 참조하십시오.

## 커뮤니티 구성 요소 {#community-components}

커뮤니티 사이트가 빌드되는 [커뮤니티 구성 요소는](/help/communities/author-communities.md) 모든 AEM 사이트에 커뮤니티 기능을 추가하는 데 사용할 수 있습니다.

구성 요소에 대한 대화형 탐색을 위해 [커뮤니티 구성 요소 안내서를](/help/communities/components-guide.md) 사용할 수 있습니다.

## 커뮤니티 유형 {#types-of-communities}

### 참여 커뮤니티 {#engagement-community}

참여 커뮤니티는 고객의 참여를 유도하고 피드백을 요청하며 고객이 커뮤니티 멤버로 상호 작용할 수 있도록 하는 커뮤니티 사이트입니다.

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
* 분석 보고

새 참여 커뮤니티를 빠르게 만드는 쉬운 방법을 살펴보려면 AEM Communities [시작하기를 참조하십시오](/help/communities/getting-started.md).

### 지원 커뮤니티 {#enablement-community}

역량 강화 커뮤니티는 온라인 학습을 위한 기능을 포함하는 커뮤니티 사이트입니다.

지원 커뮤니티의 기능은 다음과 같습니다.

* 모든 [참여 커뮤니티의](#engagement-community)기능
* 컨텐츠 및 학습 할당 리소스를 멤버 및 멤버 그룹에 추가합니다.
* 퀴즈 및 테스트와 같은 SCORM 컨텐츠를 지원합니다.
* 지정 완료 추적.
* 보고 및 분석에 액세스
* 포럼, 메시징, 댓글 및 등급을 통해 학습 리소스에 대한 대화를 나눌 수 있습니다.

활성화 Add-on이 구성되면 [](/help/communities/enablement.md)활성화 커뮤니티를 만들 수 있으며, 프로덕션 환경에서 사용하려면 추가 라이선스가 필요합니다. 활성 커뮤니티 사이트에는 [할당 기능이](#community-functions)포함됩니다.

새로운 활성 커뮤니티를 손쉽게 만들려면 AEM Communities [for Enablement 시작하기를 참조하십시오](/help/communities/getting-started-enablement.md).

## AEM Demo Machine {#aem-demo-machine}

AEM [Demo 시스템은](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine) QuickStart 인스턴스를 시작하는 것보다 훨씬 더 많은 설정이 필요한 AEM Sites [Assets](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Sites), CommunitiesRuns, CommunitiesAppsAnd FormsEngages [를](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Assets)실행하는 AEM Sites [](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Communities)[](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Apps) [](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Forms)데모를 관리하고 데모를 관리합니다. AEM 데모 시스템은 MongoDB, Solr, MySQL, FFmpeg 및 이메일 서버와 같은 추가 [인프라를](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Infrastructure) 설정합니다.

AEM Demo Machine에는 다음이 포함됩니다.

* 그래픽 [유저 인터페이스](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/User%20Interface).
* 구성 가능한 [속성](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Properties) 및 [타겟이](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Command%20Line)있는 Apache ANT 스크립트

* 설치할 패키지.

AEM 데모 시스템은 Windows, MacOS 및 Linux에서 CQ 5.5, CQ 5.6.1, AEM 6.0, AEM 6.1, AEM 6.2, AEM 6.3 및 AEM 6.4에서 테스트되었습니다.

AEM 데모 시스템에는 유효한 AEM 라이선스가 필요합니다.

>[!NOTE]
>
>AEM 데모 시스템에 대한 [비디오 소개](https://www.youtube.com/watch?v=zEE_zkR9fVQ&amp;feature=youtu.be) 보기(13:26)


## AEM Communities 설명서 {#aem-communities-documentation}

* 권장 [배포에 대해](deploy-communities.md) 알려면 커뮤니티 배포를 참조하십시오.
* 커뮤니티 사이트 [관리를](administer-landing.md) 방문하여 커뮤니티 사이트 만들기, 커뮤니티 그룹 추가, 커뮤니티 사이트 템플릿 구성, 커뮤니티 콘텐츠 중재, 구성원 관리, 태그 지정, 알림, 점수 및 배지에 대해 알아보십시오.
* SCF [](communities.md) (소셜 구성 요소 프레임워크)에 대해 알아보고 커뮤니티 구성 요소 및 기능을 사용자 정의하려면 커뮤니티 개발을 참조하십시오.
* 커뮤니티 [구성 요소를](author-communities.md) 사용하여 작성하고 구성하는 방법을 알아보려면 커뮤니티 구성 요소를 참조하십시오.

