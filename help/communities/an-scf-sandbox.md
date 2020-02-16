---
title: SCF 샌드박스 만들기
seo-title: SCF 샌드박스 만들기
description: 이 자습서는 주로 SCF 구성 요소 사용에 관심이 있는 개발자를 위한 것입니다. AEM을 처음 사용하는 개발자는 이 자습서를 사용합니다.  SCF 샌드박스 사이트 생성을 안내합니다.
seo-description: 이 자습서는 주로 SCF 구성 요소 사용에 관심이 있는 개발자를 위한 것입니다. AEM을 처음 사용하는 개발자는 이 자습서를 사용합니다.  SCF 샌드박스 사이트 생성을 안내합니다.
uuid: ee52e670-e1e6-4bcd-9548-c963142e6704
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: e1b5c25d-cbdd-421c-b81a-feb6039610a3
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---



# SCF 샌드박스 만들기 {#create-an-scf-sandbox}


AEM 6.1 Communities의 경우, 샌드박스를 신속하게 만드는 가장 쉬운 방법은 커뮤니티 사이트를 만드는 것입니다. See [Getting Started with AEM Communities](getting-started.md).

개발자에게 유용한 또 다른 도구는 커뮤니티 구성 [요소 안내서입니다](components-guide.md). 이 가이드에서는 커뮤니티 구성 요소 및 기능을 탐색하고 신속하게 프로토타이핑할 수 있습니다.

웹 사이트 만들기의 연습은 커뮤니티 기능이 포함될 수 있는 AEM 웹 사이트의 구조를 이해하는 데 유용하고 [소셜 구성 요소 프레임워크(SCF)](scf.md)작업을 탐색할 수 있는 간단한 페이지를 제공합니다.

이 자습서는 주로 SCF 구성 요소 사용에 관심이 있는 개발자를 위한 것입니다. AEM을 처음 사용하는 개발자는 이 자습서를 사용합니다. 탐색, 로고, 검색, 도구 모음 및 하위 페이지 목록과 같은 사이트 구조에 [중점을](../../help/sites-developing/website.md) 두는 완벽한 기능을 갖춘 인터넷 웹 사이트를 만드는 방법에 대한 자습서와 유사한 SCF 샌드박스 사이트 만들기에 대해 설명합니다.

개발은 작성자 인스턴스에서 진행되며, 사이트 실험은 게시 인스턴스에서 가장 적합합니다.

이 자습서의 단계는 다음과 같습니다.

* [웹 사이트 구조 설정](setup-website.md)
* [초기 샌드박스 애플리케이션](initial-app.md)
* [초기 샌드박스 컨텐츠](initial-content.md)
* [샌드박스 애플리케이션 개발](develop-app.md)
* [Clientlibs 추가](add-clientlibs.md)
* [샌드박스 컨텐츠 개발](develop-content.md)

>[!CAUTION]
>
>이 자습서에서는 커뮤니티 사이트 콘솔을 [사용하여 만든 기능이 있는 커뮤니티 사이트를 만들지](sites-console.md)않습니다. 예를 들어 이 자습서에서는 로그인, 자체 등록, [소셜 로그인](social-login.md), 메시지, 프로필 등을 설정하는 방법에 대해 설명하지 않습니다.
>
>간단한 커뮤니티 사이트를 선호하는 경우 샘플 페이지 [만들기 자습서를](create-sample-page.md) 따르십시오.

## 전제 조건 {#prerequisites}

이 자습서에서는 Communities의 [최신 릴리스가](deploy-communities.md#latest-releases) 설치된 AEM 작성자 및 AEM 게시 인스턴스 하나가 설치되어 있다고 가정합니다.

다음은 AEM 플랫폼을 처음 사용하는 개발자에게 유용한 링크입니다.

* [시작하기](../../help/sites-deploying/deploy.md#getting-started) - AEM 인스턴스 배포

   * [기본](../../help/sites-developing/the-basics.md) 사항 - 웹 사이트 및 기능 개발자
   * [작성자를 위한 첫 번째](../../help/sites-authoring/first-steps.md) 단계 - 페이지 컨텐츠 작성

## CRXDE Lite 개발 환경 사용 {#using-crxde-lite-development-environment}

AEM 개발자는 제작 인스턴스에서 CRXDE [Lite](../../help/sites-developing/developing-with-crxde-lite.md) 개발 환경에서 많은 시간을 보냅니다. CRXDE Lite를 사용하면 CRX 저장소에 대한 액세스 권한을 줄일 수 있습니다. 클래식 UI 도구 및 터치 지원 UI 콘솔은 CRX 저장소의 특정 부분에 보다 구조화된 액세스를 제공합니다.

관리자 권한으로 로그인한 후에는 다양한 방법으로 CRXDE Lite에 액세스할 수 있습니다.

1. 전역 탐색에서 탐색 도구 > CRXDE **[!UICONTROL Lite를 선택합니다]**.

   ![chlimage_1-350](assets/chlimage_1-350.png)

2. 클래식 UI [시작 페이지에서](http://localhost:4502/welcome.html)아래로 스크롤하고 오른쪽 **[!UICONTROL 패널에서 CRXDE]** Lite를 클릭합니다.

   ![chlimage_1-351](assets/chlimage_1-351.png)

3. 바로 `CRXDE Lite`탐색: `<server>:<port>/crx/de`

   예를 들어 로컬 작성자 인스턴스에서 다음을 수행합니다. ` [http://localhost:4502/crx/de](http://localhost:4502/crx/de)`

CRXDE Lite를 사용하려면 개발자 또는 관리자 권한으로 로그인해야 합니다. 기본 localhost 인스턴스의 경우

* `username: admin`
* `password: admin`


**이 로그인은 시간 초과되며 CRXDe Lite 도구 모음의 오른쪽 끝에 있는 풀다운을 사용하여 정기적으로 다시 로그인해야 합니다** .

로그인하지 않은 경우 JCR 저장소를 탐색하거나 편집/저장 작업을 수행할 수 없습니다.

***확실하지 않으면 다시 로그인하십시오!***

![chlimage_1-352](assets/chlimage_1-352.png)
