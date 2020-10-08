---
title: 초기 샌드박스 컨텐츠
seo-title: 초기 샌드박스 컨텐츠
description: 콘텐츠 만들기
seo-description: 콘텐츠 만들기
uuid: 9810fe47-8d1a-4238-9b9c-0cc47c63d97a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: e8f28cd5-7950-4aab-bf62-3d4ed3d33cbd
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 5%

---


# 초기 샌드박스 컨텐츠 {#initial-sandbox-content}

이 섹션에서는 모두 [페이지 템플릿을 사용하는 다음 페이지를 만듭니다](initial-app.md#createthepagetemplate).

* 기본 페이지의 영어 버전으로 리디렉션되는 SCF 샌드박스 사이트.

   * SCF 샌드박스 - 사이트의 영어 버전에 대한 기본 페이지입니다.

   * SCF 재생 - 재생할 주 페이지의 하위 페이지입니다.

이 자습서는 [언어 사본](../../help/sites-administering/tc-prep.md)내용을 다루지는 않지만, 루트 페이지가 HTML 헤더를 통해 사용자에 대한 기본 언어 탐지를 구현하고 해당 언어의 기본 페이지로 리디렉션할 수 있도록 디자인되었습니다. 이 규칙은 페이지의 노드 이름에 2자로 된 국가 코드를 사용합니다(예: 영어의 경우 &quot;en&quot;, 프랑스어의 경우 &quot;fr&quot; 등).

## 첫 페이지 만들기 {#create-first-pages}

이제 [페이지 템플릿이](initial-app.md#createthepagetemplate)있으므로 /content 디렉토리에 웹 사이트의 루트 페이지를 설정할 수 있습니다.

1. 표준 UI는 현재 사이트를 만드는 청사진을 제공합니다. 이 튜토리얼은 간단한 사이트를 만들기 때문에 클래식 UI가 유용합니다.

   클래식 UI로 전환하려면 전역 탐색을 선택하고 프로젝트 아이콘 오른쪽에 마우스를 놓습니다. 나타나는 클래식 UI *로* 전환 아이콘을 선택합니다.

   ![클래식 UI](assets/classic-ui.png)

   클래식 UI로 전환하는 기능은 관리자가 [활성화해야 합니다](../../help/sites-administering/enable-classic-ui.md).

1. 클래식 UI [시작 페이지에서](http://localhost:4502/welcome.html)웹 **[!UICONTROL 사이트를 선택합니다]**.

   ![classic-ui-website](assets/classic-ui-website.png)

   또는, /siteadmin으로 이동하여 웹 사이트에 대한 클래식 UI에 직접 [액세스합니다.](http://localhost:4502/siteadmin)

1. 탐색기 창에서 **[!UICONTROL 웹 사이트]** 를 선택한 다음 도구 모음에서 **[!UICONTROL 새로 만들기]** > **[!UICONTROL 새 페이지]**&#x200B;를선택합니다.

   페이지 **[!UICONTROL 만들기]** 대화 상자에서 다음을 입력합니다.

   * 제목: `SCF Sandbox Site`
   * 이름: `an-scf-sandbox`
   * SCF **[!UICONTROL 샌드박스 재생 템플릿 선택]**
   * **[!UICONTROL 만들기]**&#x200B;를 클릭합니다

   ![classic-ui-create-page](assets/classic-ui-create-page.png)

1. 탐색기 창에서 방금 만든 페이지를 선택하고 새로 `/Websites/SCF Sandbox Site`만들기 **[!UICONTROL > 새 페이지]** 를 클릭합니다 ****.

   * 제목: `SCF Sandbox`
   * 이름: `en`
   * SCF **[!UICONTROL 샌드박스 재생 템플릿 선택]**
   * **[!UICONTROL 만들기]**&#x200B;를 클릭합니다

1. 탐색기 창에서 방금 만든 페이지를 선택하고 새로 만들기 `/Websites/SCF Sandbox Site/SCF Sandbox`> **[!UICONTROL 새]** 페이지 **[!UICONTROL 를 클릭합니다]**

   * 제목: `SCF Play`
   * 이름: `play`
   * SCF **[!UICONTROL 샌드박스 재생 템플릿 선택]**
   * **[!UICONTROL 만들기]**&#x200B;를 클릭합니다

1. 이제 웹 사이트가 웹 사이트 콘솔에 표시되는 방식입니다. 탐색기 창에서 선택한 항목의 하위 페이지가 관리될 수 있는 오른쪽 창에 표시됩니다.

   ![classic-ui-website-page](assets/classic-ui-website-page.png)

   웹 사이트 도구 및 템플릿을 사용하여 만든 항목의 저장소 보기입니다.

   ![classic-ui-repository-view](assets/classic-ui-repository-view.png)

## 디자인 패스 추가 {#add-the-design-path}

도구 콘솔의 디자인 섹션을 사용하여 만든 경우 속성 &quot; ` [/etc/designs/an-scf-sandbox](setup-website.md#setupthedesigntreeetcdesigns)`

* `cq:template="/libs/wcm/core/templates/designpage"`

가 정의되었습니다. 이 정의를 사용하면 스크립트에서 디자인 에셋을 참조할 수 있습니다(선택 사항) `currentDesign.getPath()`. 예

* `% String favIcon = currentDesign.getPath() + "/favicon.ico"; %`


   * 이름: `cq:designPath`
   * 유형: `String`
   * 값: `/etc/designs/an-scf-sandbox`

* 녹색 `[+] Add`

응답은 다음과 같이 표시됩니다.

![classic-ui-repository-path](assets/classic-ui-repository-path.png)

* 모두 **[!UICONTROL 저장을 클릭합니다.]**

구성을 저장하는 데 문제가 발생하면 다시 로그인하고 다시 구성하십시오.

>[!NOTE]
>
>The use of `cq:designPath` is optional and is disrelate to the [use of clientlibs](develop-app.md#includeclientlibsintemplate), which are re본질적으로 required as the SCF components use [](client-customize.md#clientlibs-for-scf) clientlibs to manage their JS and CSS.
