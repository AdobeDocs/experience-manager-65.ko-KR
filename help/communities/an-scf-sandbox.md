---
title: SCF 샌드박스 만들기
seo-title: SCF 샌드박스 만들기
description: 이 자습서는 주로 개발자를 위한 것으로 SCF 구성 요소 사용에 관심이 있는 AEM을 처음 사용하는 사람에게만 제공됩니다.  SCF 샌드박스 사이트 생성을 안내합니다.
seo-description: 이 자습서는 주로 개발자를 위한 것으로 SCF 구성 요소 사용에 관심이 있는 AEM을 처음 사용하는 사람에게만 제공됩니다.  SCF 샌드박스 사이트 생성을 안내합니다.
uuid: ee52e670-e1e6-4bcd-9548-c963142e6704
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: e1b5c25d-cbdd-421c-b81a-feb6039610a3
translation-type: tm+mt
source-git-commit: 548e19b0fc76ede8685ea938ed871fbdc8c3858f
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 0%

---



# SCF 샌드박스 만들기 {#create-an-scf-sandbox}


AEM 6.1 Communities의 경우 샌드박스를 빠르게 만드는 가장 쉬운 방법은 커뮤니티 사이트를 만드는 것입니다. [AEM Communities 시작하기](getting-started.md)를 참조하십시오.

개발자에게 유용한 다른 도구는 커뮤니티 구성 요소 및 기능에 대한 탐색 및 빠른 프로토타입을 작성할 수 있는 [커뮤니티 구성 요소 안내서](components-guide.md)입니다.

웹 사이트 만들기의 연습은 커뮤니티 기능을 포함할 수 있는 AEM 웹 사이트의 구조를 이해하는 데 유용할 수 있으며, [소셜 구성 요소 프레임워크(SCF)](scf.md)에서 작업해야 할 간단한 페이지를 제공합니다.

이 자습서는 주로 개발자를 위한 것으로 SCF 구성 요소 사용에 관심이 있는 AEM을 처음 사용하는 사람에게만 제공됩니다. 탐색, 로고, 검색, 도구 모음 및 하위 페이지 나열 등과 같은 사이트 구조에 중점을 두는 [완전한 기능을 갖춘 인터넷 웹 사이트 만들기 방법](../../help/sites-developing/website.md)에 대한 자습서와 유사한 SCF 샌드박스 사이트 만들기를 안내합니다.

개발은 작성자 인스턴스에서 진행되며, 사이트에 대한 실험은 게시 인스턴스에 가장 적합합니다.

이 자습서의 단계는 다음과 같습니다.

* [웹 사이트 구조 설정](setup-website.md)
* [초기 샌드박스 응용 프로그램](initial-app.md)
* [초기 샌드박스 컨텐츠](initial-content.md)
* [샌드박스 응용 프로그램 개발](develop-app.md)
* [Clientlibs 추가](add-clientlibs.md)
* [샌드박스 컨텐츠 개발](develop-content.md)

>[!CAUTION]
>
>이 자습서에서는 [커뮤니티 사이트 콘솔](sites-console.md)을 사용하여 만든 기능이 있는 커뮤니티 사이트를 만들지 않습니다. 예를 들어 이 자습서에서는 로그인, 자가 등록, [소셜 로그인](social-login.md), 메시지, 프로필 등을 설정하는 방법에 대해 설명하지 않습니다.
>
>간단한 커뮤니티 사이트가 선호되는 경우 [샘플 페이지 만들기](create-sample-page.md) 자습서를 따릅니다.

## 전제 조건 {#prerequisites}

이 자습서에서는 [최신 릴리스](deploy-communities.md#latest-releases)의 AEM 작성자 및 AEM 게시 인스턴스가 설치되어 있다고 가정합니다.

다음은 AEM 플랫폼을 처음 사용하는 개발자에게 유용한 링크입니다.

* [시작하기](../../help/sites-deploying/deploy.md#getting-started):을 참조하십시오.

   * [기본 사항](../../help/sites-developing/the-basics.md):를 참조하십시오.
   * [작성자를 위한 첫 번째 단계](../../help/sites-authoring/first-steps.md):을 참조하십시오.

## CRXDE Lite 개발 환경 사용 {#using-crxde-lite-development-environment}

AEM 개발자는 제작 인스턴스의 [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) 개발 환경에서 많은 시간을 보냅니다. CRXDE Lite은 CRX 저장소에 대한 제한된 액세스 권한을 덜 제공합니다. 클래식 UI 도구 및 터치 지원 UI 콘솔에서는 CRX 저장소의 특정 부분에 보다 구조화된 액세스를 제공합니다.

관리자 권한으로 로그인한 후에는 다양한 방법으로 CRXDE Lite에 액세스할 수 있습니다.

1. 전역 탐색에서 탐색 **[!UICONTROL 도구 > CRXDE Lite]**&#x200B;을 선택합니다.

   ![crxde-lite](assets/tools-crxde.png)

2. [클래식 UI 시작 페이지](http://localhost:4502/welcome.html)에서 아래로 스크롤하고 오른쪽 패널에서 **[!UICONTROL CRXDE Lite]**&#x200B;을 클릭합니다.

   ![classic-ui-crxde](assets/classic-ui-crxde.png)

3. `CRXDE Lite`으로 바로 이동합니다.`<server>:<port>/crx/de`

   예를 들어 로컬 작성자 인스턴스에서 다음을 수행합니다.[http://localhost:4502/crx/de](http://localhost:4502/crx/de)

CRXDE Lite을 사용하려면 개발자 또는 관리자 권한으로 로그인해야 합니다. 기본 localhost 인스턴스의 경우

* `username: admin`
* `password: admin`


**이** 로그인이 시간 초과되고 CRXDe Lite 도구 모음의 오른쪽 끝에서 풀다운을 사용하여 정기적으로 다시 로그인해야 합니다.

로그인하지 않은 경우 JCR 저장소를 탐색하거나 편집/저장 작업을 수행할 수 없습니다.

***확실하지 않은 경우 다시 로그인하십시오!***

![재로그인](assets/relogin.png)
