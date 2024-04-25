---
title: SCF 샌드박스 만들기
description: 이 자습서는 주로 SCF 구성 요소 사용에 관심이 있는 AEM을 처음 사용하는 개발자를 위한 것입니다. SCF 샌드박스 사이트를 만드는 과정을 안내합니다
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 89858814-6625-4a56-8359-cc1eca402816
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 0%

---

# SCF 샌드박스 만들기  {#create-an-scf-sandbox}

AEM 6.1 Communities에서 샌드박스를 빠르게 생성하는 가장 쉬운 방법은 커뮤니티 사이트를 생성하는 것입니다. 다음을 참조하십시오 [AEM Communities 시작하기](getting-started.md).

개발자에게 유용한 또 다른 도구는 입니다. [커뮤니티 구성 요소 안내서](components-guide.md): 커뮤니티 구성 요소 및 기능을 탐색하고 빠르게 프로토타이핑할 수 있습니다.

웹 사이트를 만드는 연습은 커뮤니티 기능이 포함될 수 있는 AEM 웹 사이트의 구조를 이해하고, 작업을 탐색할 간단한 페이지를 제공하는 데 유용합니다. [소셜 구성 요소 프레임워크(SCF)](scf.md).

이 자습서는 주로 SCF 구성 요소 사용에 관심이 있는 AEM을 처음 사용하는 개발자를 위한 것입니다. 다음 자습서와 유사한 SCF 샌드박스 사이트를 만드는 과정을 안내합니다 [완벽한 기능을 갖춘 인터넷 웹 사이트를 만드는 방법](../../help/sites-developing/website.md) 탐색, 로고, 검색, 도구 모음 및 하위 페이지 나열 등 사이트 구조에 중점을 둡니다.

개발은 작성자 인스턴스에서 수행되지만 게시 인스턴스에서는 사이트를 실험하는 것이 가장 좋습니다.

이 자습서의 단계는 다음과 같습니다.

* [웹 사이트 구조 설정](setup-website.md)
* [초기 샌드박스 애플리케이션](initial-app.md)
* [초기 샌드박스 콘텐츠](initial-content.md)
* [샌드박스 애플리케이션 개발](develop-app.md)
* [Clientlibs 추가](add-clientlibs.md)
* [샌드박스 콘텐츠 개발](develop-content.md)

>[!CAUTION]
>
>이 자습서에서는 를 사용하여 만든 기능이 있는 커뮤니티 사이트를 만들지 않습니다. [커뮤니티 사이트 콘솔](sites-console.md). 예를 들어 이 튜토리얼에서는 로그인, 자가 등록, [소셜 로그인](social-login.md), 메시징, 프로필 등.
>
>간단한 커뮤니티 사이트를 선호하는 경우 다음을 따르십시오. [샘플 페이지 만들기](create-sample-page.md) 튜토리얼.

## 사전 요구 사항 {#prerequisites}

이 자습서에서는 AEM 작성자와 AEM 게시 인스턴스가 하나씩 설치되어 있고 [최신 릴리스](deploy-communities.md#latest-releases) 커뮤니티.

다음은 AEM 플랫폼을 처음 사용하는 개발자에게 유용한 링크입니다.

* [시작](../../help/sites-deploying/deploy.md#getting-started): AEM 인스턴스 배포용

   * [기본 사항](../../help/sites-developing/the-basics.md): 웹 사이트 및 기능 개발자용
   * [작성자를 위한 첫 번째 단계](../../help/sites-authoring/first-steps.md): 페이지 컨텐츠 작성용

## CRXDE Lite 개발 환경 사용 {#using-crxde-lite-development-environment}

AEM 개발자는 대부분의 시간을 [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) 작성자 인스턴스의 개발 환경입니다. CRXDE Lite은 CRX 저장소에 대한 액세스 제한을 줄입니다. 클래식 UI 도구 및 터치 지원 UI 콘솔은 CRX 저장소의 특정 부분에 대해 보다 구조화된 액세스를 제공합니다.

관리자 권한으로 로그인한 후 다양한 방법으로 CRXDE Lite에 액세스할 수 있습니다.

1. 전역 탐색에서 탐색을 선택합니다. **[!UICONTROL 도구 > CRXDE Lite]**.

   ![crxde-lite](assets/tools-crxde.png)

2. 다음에서 [클래식 UI 시작 페이지](http://localhost:4502/welcome.html), 아래로 스크롤하고 클릭 **[!UICONTROL CRXDE Lite]** 오른쪽 패널에서

   ![classic-ui-crxde](assets/classic-ui-crxde.png)

3. 다음으로 직접 검색 `CRXDE Lite`: `<server>:<port>/crx/de`

   예를 들어 로컬 작성자 인스턴스에서 다음을 수행합니다. [http://localhost:4502/crx/de](http://localhost:4502/crx/de)

CRXDE Lite으로 작업하려면 개발자 또는 관리자 권한으로 로그인해야 합니다. 기본 localhost 인스턴스의 경우

* `username: admin`
* `password: admin`


이 로그인은 시간 초과되므로 CRXDE Lite 도구 모음의 오른쪽 끝에 있는 풀다운 메뉴를 사용하여 정기적으로 다시 로그인해야 합니다.

로그인하지 않은 경우 JCR 저장소를 탐색하거나 편집/저장 작업을 수행할 수 없습니다.

***확실하지 않은 경우 다시 로그인합니다!***

![재로그인](assets/relogin.png)
