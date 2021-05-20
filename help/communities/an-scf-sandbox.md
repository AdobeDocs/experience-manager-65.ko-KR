---
title: SCF 샌드박스 만들기
seo-title: SCF 샌드박스 만들기
description: 이 튜토리얼은 주로 개발자를 위한 것으로, SCF 구성 요소를 사용하는 데 관심이 있는 AEM을 처음 사용하는 개발자를 위한 것입니다.  SCF 샌드박스 사이트 생성을 안내합니다
seo-description: 이 튜토리얼은 주로 개발자를 위한 것으로, SCF 구성 요소를 사용하는 데 관심이 있는 AEM을 처음 사용하는 개발자를 위한 것입니다.  SCF 샌드박스 사이트 생성을 안내합니다
uuid: ee52e670-e1e6-4bcd-9548-c963142e6704
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: e1b5c25d-cbdd-421c-b81a-feb6039610a3
exl-id: 89858814-6625-4a56-8359-cc1eca402816
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 0%

---

# SCF 샌드박스 {#create-an-scf-sandbox} 만들기


AEM 6.1 Communities에서 샌드박스를 빨리 만드는 가장 쉬운 방법은 커뮤니티 사이트를 만드는 것입니다. [AEM Communities 시작하기](getting-started.md)를 참조하십시오.

개발자에게 유용한 또 다른 도구는 [커뮤니티 구성 요소 안내서](components-guide.md)입니다. 이 안내서에서는 커뮤니티 구성 요소 및 기능을 탐색하고 신속하게 프로토타이핑할 수 있습니다.

웹 사이트 만들기 연습은 커뮤니티 기능을 포함할 수 있는 AEM 웹 사이트의 구조를 이해하는 데 도움이 될 수 있으며 [소셜 구성 요소 프레임워크(SCF)](scf.md) 작업을 탐색할 수 있는 간단한 페이지를 제공할 수도 있습니다.

이 튜토리얼은 주로 개발자를 위한 것으로, SCF 구성 요소를 사용하는 데 관심이 있는 AEM을 처음 사용하는 개발자를 위한 것입니다. 이 안내서는 탐색, 로고, 검색, 도구 모음 및 하위 페이지 나열 등의 사이트 구조에 중점을 둔 [완전 기능을 갖는 인터넷 웹 사이트를 만드는 방법](../../help/sites-developing/website.md)에 대한 자습서와 유사한 SCF 샌드박스 사이트 생성을 안내합니다.

개발은 작성자 인스턴스에서 발생하며, 사이트 실험은 게시 인스턴스에서 가장 좋습니다.

이 자습서의 단계는 다음과 같습니다.

* [웹 사이트 구조 설정](setup-website.md)
* [초기 샌드박스 애플리케이션](initial-app.md)
* [초기 샌드박스 컨텐츠](initial-content.md)
* [샌드박스 애플리케이션 개발](develop-app.md)
* [Clientlibs 추가](add-clientlibs.md)
* [샌드박스 콘텐츠 개발](develop-content.md)

>[!CAUTION]
>
>이 자습서에서는 [커뮤니티 사이트 콘솔](sites-console.md)을 사용하여 만든 기능을 사용하는 커뮤니티 사이트를 만들지 않습니다. 예를 들어 이 자습서에서는 로그인, 자체 등록, [소셜 로그인](social-login.md), 메시징, 프로필 등을 설정하는 방법에 대해 설명합니다.
>
>단순 커뮤니티 사이트가 선호되는 경우 [샘플 페이지 만들기](create-sample-page.md) 자습서를 따르십시오.

## 전제 조건 {#prerequisites}

이 자습서에서는 Communities의 [최신 릴리스](deploy-communities.md#latest-releases)가 있는 AEM 작성자 및 AEM 게시 인스턴스가 하나 설치되어 있다고 가정합니다.

다음은 AEM 플랫폼을 처음 사용하는 개발자에게 유용한 몇 가지 링크입니다.

* [시작하기](../../help/sites-deploying/deploy.md#getting-started):AEM 인스턴스 배포에 사용할 수 있습니다.

   * [기본 사항](../../help/sites-developing/the-basics.md):웹 사이트 및 기능 개발자용.
   * [작성자를 위한 첫 번째 단계](../../help/sites-authoring/first-steps.md):페이지를 작성하는 데 사용할 수 있습니다.

## CRXDE Lite 개발 환경 사용 {#using-crxde-lite-development-environment}

AEM 개발자는 많은 시간을 작성자 인스턴스의 [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) 개발 환경에서 보냅니다. CRXDE Lite은 CRX 저장소에 대한 액세스 권한을 더 적게 제공합니다. 클래식 UI 도구 및 터치 지원 UI 콘솔에서는 CRX 저장소의 특정 부분에 대해 더 구조화된 액세스를 제공합니다.

관리 권한으로 로그인한 후에는 CRXDE Lite에 액세스하는 다양한 방법이 있습니다.

1. 전역 탐색에서 탐색 **[!UICONTROL 도구 > CRXDE Lite]**&#x200B;를 선택합니다.

   ![crxde-lite](assets/tools-crxde.png)

2. [클래식 UI 시작 페이지](http://localhost:4502/welcome.html)에서 아래로 스크롤하여 오른쪽 패널에서 **[!UICONTROL CRXDE Lite]**&#x200B;을 클릭하십시오.

   ![classic-ui-crxde](assets/classic-ui-crxde.png)

3. `CRXDE Lite`(으)로 바로 이동합니다.`<server>:<port>/crx/de`

   예를 들어 로컬 작성자 인스턴스에서 다음을 수행합니다.[http://localhost:4502/crx/de](http://localhost:4502/crx/de)

CRXDE Lite을 사용하려면 개발자 또는 관리자 권한으로 로그인해야 합니다. 기본 localhost 인스턴스의 경우

* `username: admin`
* `password: admin`


**이** 로그인이 시간 초과되며 CRXDe Lite 도구 모음의 오른쪽 상단에 있는 풀다운을 사용하여 주기적으로 다시 로그인해야 합니다.

로그인하지 않은 경우 JCR 저장소를 탐색하거나 편집/저장 작업을 수행할 수 없습니다.

***확실하지 않은 경우 다시 로그인하십시오.***

![재로그인](assets/relogin.png)
