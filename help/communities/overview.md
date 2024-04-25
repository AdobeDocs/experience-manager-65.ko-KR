---
title: AEM Communities 개요
description: Adobe Experience Manager Communities 기능 및 설정의 기본 사항에 대해 알아봅니다.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
exl-id: d6243dff-a067-455c-a326-5f451f225efd
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1204'
ht-degree: 2%

---

# AEM Communities 개요 {#aem-communities-overview}

Adobe Experience Manager(AEM) 커뮤니티를 사용하면 성능이 향상되고 사이트 관리가 개선되었으며 사이트 방문자를 가치 있는 커뮤니티 구성원으로 전환할 수 있는 온프레미스 커뮤니티 사이트를 빠르게 만들 수 있습니다.

## 커뮤니티 기능 {#communities-features}

AEM Communities을 사용하면 사이트 방문자와의 관계를 다음과 같이 개발할 수 있습니다.

* **알림** 블로그, Q&amp;A 및 이벤트 캘린더를 통해
* While **통찰력 얻기** 종종 사용자 생성 콘텐츠(UGC)라고도 하는 포럼, 댓글 및 기타 커뮤니티 콘텐츠를 통해
* 허용 **중재** 게시 환경의 신뢰할 수 있는 멤버인 경우
* **소셜 로그인** twitter 및 Facebook 사용,
* **인라인 번역** 커뮤니티 콘텐츠,
* **커뮤니티 그룹 만들기** 게시된 커뮤니티 사이트에서
* **채점** 배지를 수여하려면
* **파일 공유**,
* **알림** 및 **활동 스트림**,
* 허용 **태깅** (@mention) 그 밖에 이용자 제작 콘텐츠의 관심을 끌기 위하여 등록한 회원

커뮤니티 기능은 다음을 사용하여 시연할 수 있습니다. [AEM 데모 컴퓨터](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki) GitHub.com에서 공개적으로 사용하거나 `We.Retail` 참조 구현입니다.

## 커뮤니티 사이트 {#community-sites}

커뮤니티 사이트는 간단한 마법사를 사용하여 만든 AEM 사이트입니다. 이 마법사를 사용하면 사이트에 미리 연결되어 있는 여러 가지 공통 기능이 있는 웹 사이트가 생성됩니다.

다음 [사이트 생성 마법사](/help/communities/sites-console.md):

* 선택한 항목을 기반으로 사이트의 기능을 어셈블합니다. [커뮤니티 사이트 템플릿](/help/communities/sites.md) 즉,

   * 빌드 원본 [커뮤니티 기능](#community-functions)
   * 선택 사항 [커뮤니티 그룹](#communitygroups) 기능

* 설정을 사용하여 다음을 구성합니다.

   * 중재
   * 로그인
   * 번역

* 다음과 같은 필수 기능을 제공합니다.

   * 반응형 디자인: 사용 [Twitter Bootstrap 테마](https://getbootstrap.com)

   * 로그인 : 자가 등록, [소셜 로그인](/help/communities/social-login.md), 사용자 프로필

      * 알림: 멤버에게 관련성 있는 이벤트와 사용자가 생성한 컨텐츠가 있는 위치 [@mentioned](/help/communities/overview.md#mentionssupport).

      * 메시징: 구성원은 커뮤니티 사이트 내에서 메시지를 보내거나 받을 수 있습니다.
      * 검색: 커뮤니티 사이트 내에서 검색할 수 있습니다.
      * 언어 전환: 언어 선택 기능 [다언어 부위](/help/sites-administering/translation.md).

      * 관리: 권한이 있는 구성원이 커뮤니티 사이트 내에서 사용자를 중재하고 관리할 수 있도록 액세스할 수 있습니다.

* 다음과 같은 많은 페이지 수준 작성 단계를 생략할 수 있습니다.

   * 브랜딩: 커뮤니티 사이트의 모든 페이지에 표시할 배너 이미지 업로드(선택 사항)
   * 탐색 메뉴: 커뮤니티 사이트 템플릿에 포함된 기능에 대한 탐색 링크가 제공됩니다.

커뮤니티 사이트를 간편하게 만들려면 다음을 방문하십시오. [AEM Communities 시작하기](/help/communities/getting-started.md).

## 커뮤니티 콘텐츠 지속성 {#community-content-persistence}

커뮤니티 콘텐츠의 성능과 동기화를 향상시키기 위해 AEM Communities에는 모든 AEM(작성자 및 게시) 인스턴스 간에 공유되는 사용자 생성 콘텐츠(UGC)에 특별히 공통된 저장소가 필요합니다.

커뮤니티 컨텐츠는 SRP(Storage Resource Provider)를 통해 쉽게 액세스할 수 있습니다. SRP는 기본 토폴로지와 액세스를 분리하는 계층을 제공하고 UGC에 대한 공통 저장소를 지원합니다.

커뮤니티 콘텐츠 지속성 및 권장 배포에 대한 자세한 내용은 다음을 참조하십시오.

* [커뮤니티 콘텐츠 저장소](/help/communities/working-with-srp.md)—UGC에 사용 가능한 SRP 스토리지 옵션에 대해 설명합니다.
* [권장 토폴로지](/help/communities/topologies.md)—사용 사례 및 SRP 선택에 따른 토폴로지에 대해 설명합니다.
* [AEM 6.5 커뮤니티로 업그레이드](/help/communities/upgrade.md)- AEM 6.5로 이동할 때 UGC에 대한 유용한 정보를 제공합니다.

## 커뮤니티 콘솔 {#communities-consoles}

작성 환경에서 전역 탐색 콘솔은에 대한 액세스를 제공합니다. [커뮤니티 콘솔](/help/communities/consoles.md), 다음 포함:

* [Sites](/help/communities/sites-console.md) 콘솔

   * 사이트 생성
   * 사이트 편집
   * 사이트 관리
   * [커뮤니티 그룹](/help/communities/groups.md) 콘솔

* [중재](/help/communities/moderation.md) 콘솔

   * 작성자 및 게시 환경에 대한 일반적인 벌크 중재 UI.
   * 새로운 필터링 기준.

* [구성원 및 그룹](/help/communities/members.md) 관리 콘솔

   * 작성자 환경에서 게시측 사용자(구성원)를 만들고 관리할 수 있습니다.
   * 구성원을 금지할 수 있습니다.
   * 작성 환경에서 게시측 사용자 그룹(구성원 그룹)을 만들고 관리할 수 있습니다.

* [보고서](/help/communities/reports.md) 콘솔

   * 할당, 게시물 및 보기에 대한 보고서를 생성할 수 있습니다.

전역 도구 콘솔에서는 다음 Communities 도구에 액세스할 수 있습니다.

* [사이트 템플릿](/help/communities/tools.md#sitetemplatesconsole) 콘솔

   * 커뮤니티 사이트 템플릿을 만들고 관리합니다.

* [그룹 템플릿](/help/communities/tools.md#grouptemplatesconsole) 콘솔

   * 커뮤니티 그룹 템플릿을 만들고 관리합니다.

* [커뮤니티 기능](/help/communities/tools.md#communityfunctionsconsole) 콘솔

   * 커뮤니티 기능을 만들고 관리합니다.

* [스토리지 구성](/help/communities/tools.md#storageconfiguratonconsole) 콘솔

   * 을(를) 선택하고 구성합니다 [공동 저장소](/help/communities/working-with-srp.md) 사이트용.

* [구성 요소 가이드](/help/communities/components-guide.md)

   * 샘플 사이트, [커뮤니티 구성 요소](https://localhost:4502/editor.html/content/community-components/en.html) 는 모든 Communities 구성 요소의 샘플과 기본 구성 및 이를 실험할 수 있는 기능을 제공합니다.

## 커뮤니티 사이트 템플릿 {#community-site-templates}

커뮤니티 사이트 생성은 샘플 사이트와 독립적인 커뮤니티 사이트를 빠르게 설정하기 위한 커뮤니티 사이트 템플릿 선택을 기반으로 합니다.

커뮤니티 기능과 커뮤니티 그룹 템플릿으로 구성된 커뮤니티 사이트 템플릿은 커뮤니티 사이트의 구조를 제공합니다. 여기에는 로그인, 사용자 프로필, 메시지, 사이트 메뉴, 검색, 테마 및 브랜딩 기능이 포함됩니다.

다음을 참조하십시오. [사이트 템플릿 콘솔](/help/communities/sites.md).

## 커뮤니티 기능 {#community-functions}

커뮤니티 경험에 대해 예상되는 기능은 잘 알려져 있습니다. AEM Communities에서 이러한 기능은 커뮤니티 기능이라고 하는 빌딩 블록으로 사용할 수 있습니다.

커뮤니티 기능은 일반적인 AEM 페이지이며 커뮤니티 사이트 템플릿에 쉽게 통합되는 기능에 함께 연결된 구성 요소가 포함됩니다.

다음을 참조하십시오. [커뮤니티 기능 콘솔](/help/communities/functions.md).

## 커뮤니티 그룹 및 그룹 템플릿 {#community-groups-and-group-templates}

커뮤니티 그룹 기능은 승인된 사용자와 작성 및 게시 환경의 커뮤니티 멤버가 커뮤니티 사이트 내에서 하위 커뮤니티를 동적으로 만들 수 있는 기능입니다.

작성자 환경에서 템플릿 구조에 가 포함된 경우 커뮤니티 그룹(하위 커뮤니티)을 기존 커뮤니티 사이트 내에 만들거나 기존 그룹 내에 중첩할 수 있습니다. [그룹 기능](/help/communities/functions.md#groups-function).

커뮤니티 그룹을 생성하려면 커뮤니티 그룹 페이지의 디자인을 제공하는 커뮤니티 그룹 템플릿을 선택해야 합니다. 템플릿 구조에 그룹 기능이 추가되면 그룹 템플릿을 하나 지정하거나 새 커뮤니티 그룹을 만들 때 템플릿을 선택하도록 구성됩니다.

추가 참조:

* [사이트 그룹 콘솔](/help/communities/groups.md) 작성 환경에서 하위 커뮤니티를 만들기 위해 사용됩니다.
* [그룹 템플릿 콘솔](/help/communities/tools-groups.md) 를 참조하십시오.
* [AEM Communities 시작하기](/help/communities/getting-started.md) 중첩된 그룹을 포함하는 커뮤니티 사이트를 빠르게 만드는 방법에 대한 자습서입니다.

## 커뮤니티 구성 요소 {#community-components}

다음 [커뮤니티 구성 요소](/help/communities/author-communities.md) 커뮤니티 사이트가 내장된 를 사용하여 모든 AEM 사이트에 커뮤니티 기능을 추가할 수 있습니다.

다음 [커뮤니티 구성 요소 안내서](/help/communities/components-guide.md) 구성 요소를 대화식으로 탐색할 수 있습니다.

## 참여 커뮤니티 {#engagement-community}

참여 커뮤니티는 고객이 커뮤니티 구성원으로 상호 작용할 수 있도록 알리고, 피드백을 요청하고, 유도하는 데 중점을 둔 커뮤니티 사이트입니다.

참여 커뮤니티의 기능은 다음과 같습니다.

* 로그인
* 메시지
* 포럼
* 댓글
* 리뷰
* 등급
* 투표
* 블로그
* 그룹
* 캘린더
* 번역
* 관리
* 알림
* 채점 및 배지
* Analytics 보고

참여 커뮤니티를 신속하게 쉽게 만들 수 있도록 하려면 다음을 방문하십시오. [AEM Communities 시작하기](/help/communities/getting-started.md).

## AEM 데모 컴퓨터 {#aem-demo-machine}

다음 [AEM 데모 컴퓨터](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine) AEM에 대한 데모 관리 및 실행 [사이트](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Sites), [에셋](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Assets), [커뮤니티](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Communities), [앱](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Apps) 및 [Forms](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Forms)를 설정하는 것이 간편하지만 빠른 시작 인스턴스를 시작하는 것보다 더 많은 시간이 필요합니다. AEM 데모 컴퓨터는 추가 기능을 설정합니다. [인프라](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Infrastructure) MongoDB, Solr, MySQL, FFmpeg 및 이메일 서버 등

AEM 데모 시스템에는 다음이 포함됩니다.

* A [그래픽 유저 인터페이스](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/User%20Interface).
* 구성 가능한 Apache ANT 스크립트 [속성](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Properties) 및 [타겟](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Command%20Line).

* 설치할 패키지.

AEM 데모 머신은 Windows, macOS 및 Linux®에서 CQ 5.5, CQ 5.6.1, AEM 6.0, AEM 6.1, AEM 6.2, AEM 6.3 및 AEM 6.4로 성공적으로 테스트되었습니다.

AEM 데모 컴퓨터에는 유효한 AEM 라이센스가 필요합니다.

>[!NOTE]
>
>보기 [비디오 소개](https://www.youtube.com/watch?v=zEE_zkR9fVQ&amp;feature=youtu.be) 를 AEM 데모 컴퓨터에 복사합니다(13:26).

## AEM Communities 설명서 {#aem-communities-documentation}

* 방문 [커뮤니티 배포](deploy-communities.md) 권장되는 배포에 대해 알아볼 수 있습니다.
* 방문 [커뮤니티 사이트 관리](administer-landing.md) 커뮤니티 사이트 만들기, 커뮤니티 그룹 추가, 커뮤니티 사이트 템플릿 구성, 커뮤니티 콘텐츠 중재, 구성원 관리, 태그 지정, 알림, 점수 및 배지에 대해 알아볼 수 있습니다.
* 방문 [개발 커뮤니티](communities.md) 소셜 구성 요소 프레임워크(SCF)와 커뮤니티 구성 요소 및 기능 맞춤화에 대해 알아볼 수 있습니다.
* 방문 [커뮤니티 구성 요소 작성](author-communities.md) 커뮤니티 구성 요소를 사용하여 작성하고 구성하는 방법을 배울 수 있는 곳입니다.
