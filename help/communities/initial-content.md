---
title: 초기 샌드박스 콘텐츠
description: 샌드박스에서 페이지 템플릿을 사용하여 영어 버전의 웹 사이트에 대한 기본 페이지와 기본 페이지의 하위 페이지를 만드는 방법에 대해 알아봅니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 068a0fff-ca48-4847-ba3f-d78416c97f6d
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 2%

---

# 초기 샌드박스 콘텐츠 {#initial-sandbox-content}

이 섹션에서는 [페이지 템플릿](initial-app.md#createthepagetemplate)을 사용하는 다음 페이지를 만듭니다.

* SCF 샌드박스 사이트 - 기본 페이지의 영어 버전으로 리디렉션합니다.

   * SCF 샌드박스 - 사이트의 영어 버전에 대한 메인 페이지.

   * SCF 재생 - 재생할 기본 페이지의 하위 항목.

이 자습서에서는 [언어 사본](../../help/sites-administering/tc-prep.md)을 다루지 않습니다. 대신 루트 페이지가 HTML 헤더를 통해 사용자의 기본 언어 감지를 구현하고 해당 언어의 적절한 메인 페이지로 리디렉션할 수 있도록 디자인되었습니다. 이 규칙은 페이지의 노드 이름에 두 글자로 된 국가 코드를 사용하는 것입니다. 예를 들어 영어는 &quot;en&quot;, 프랑스어는 &quot;fr&quot;입니다.

## 첫 페이지 만들기 {#create-first-pages}

[페이지 템플릿](initial-app.md#createthepagetemplate)이 있으므로 이제 /content 디렉터리에 웹 사이트의 루트 페이지를 설정할 수 있습니다.

1. 표준 UI는 현재 사이트를 만들기 위한 블루프린트를 제공합니다. 이 자습서에서는 간단한 사이트를 만들 때 클래식 UI가 유용합니다.

   클래식 UI로 전환하려면 전역 탐색 을 선택하고 프로젝트 아이콘의 오른쪽에 마우스를 가져다 놓습니다. 표시되는 *클래식 UI로 전환* 아이콘을 선택합니다.

   ![클래식 ui](assets/classic-ui.png)

   클래식 UI로 전환하는 기능은 관리자가 [사용할 수 있도록 설정](../../help/sites-administering/enable-classic-ui.md)해야 합니다.

1. [클래식 UI 시작 페이지](http://localhost:4502/welcome.html)에서 **[!UICONTROL 웹 사이트]**&#x200B;를 선택합니다.

   ![classic-ui-website](assets/classic-ui-website.png)

   또는 [/siteadmin으로 이동하여 웹 사이트의 클래식 UI에 직접 액세스하십시오.](http://localhost:4502/siteadmin)

1. 탐색기 창에서 **[!UICONTROL 웹 사이트]**&#x200B;를 선택한 다음 도구 모음에서 **[!UICONTROL 새로 만들기]** > **[!UICONTROL 새 페이지]**&#x200B;를 선택합니다.

   **[!UICONTROL 페이지 만들기]** 대화 상자에서 다음을 입력합니다.

   * 제목: `SCF Sandbox Site`
   * 이름: `an-scf-sandbox`
   * **[!UICONTROL SCF 샌드박스 재생 템플릿 선택]**
   * **[!UICONTROL 만들기]**&#x200B;를 클릭합니다.

   ![classic-ui-create-page](assets/classic-ui-create-page.png)

1. 탐색기 창에서 만든 페이지 `/Websites/SCF Sandbox Site`을(를) 선택하고 **[!UICONTROL 새로 만들기]** > **[!UICONTROL 새 페이지]**&#x200B;를 클릭합니다.

   * 제목: `SCF Sandbox`
   * 이름: `en`
   * **[!UICONTROL SCF 샌드박스 재생 템플릿 선택]**
   * **[!UICONTROL 만들기]**&#x200B;를 클릭합니다.

1. 탐색기 창에서 만든 페이지 `/Websites/SCF Sandbox Site/SCF Sandbox`을(를) 선택하고 **[!UICONTROL 새로 만들기]** > **[!UICONTROL 새 페이지]**&#x200B;를 클릭합니다

   * 제목: `SCF Play`
   * 이름: `play`
   * **[!UICONTROL SCF 샌드박스 재생 템플릿 선택]**
   * **[!UICONTROL 만들기]**&#x200B;를 클릭합니다.

1. 이제 웹 사이트가 웹 사이트 콘솔에 표시되는 방식입니다. 탐색기 창에서 선택한 항목의 하위 페이지는 관리할 수 있는 오른쪽 창에 표시됩니다.

   ![classic-ui-website-page](assets/classic-ui-website-page.png)

   다음은 웹 사이트 도구 및 템플릿을 사용하여 작성된 항목의 저장소 보기입니다.

   ![classic-ui-repository-view](assets/classic-ui-repository-view.png)

## 디자인 경로 추가 {#add-the-design-path}

도구 콘솔의 디자인 섹션을 사용하여 ` [/etc/designs/an-scf-sandbox](setup-website.md#setupthedesigntreeetcdesigns)`을(를) 만들면 속성 &quot;

* `cq:template="/libs/wcm/core/templates/designpage"`

`currentDesign.getPath()`을(를) 사용하여 스크립트에서 디자인 자산을 참조하는 선택적 기능을 제공하는 가 정의되었습니다. 예

* `% String favIcon = currentDesign.getPath() + "/favicon.ico"; %`


   * 이름: `cq:designPath`
   * 유형: `String`
   * 값: `/etc/designs/an-scf-sandbox`

* 녹색 `[+] Add` 클릭

저장소는 다음과 같이 표시됩니다.

![classic-ui-repository-path](assets/classic-ui-repository-path.png)

* **[!UICONTROL 모두 저장]** 클릭

구성을 저장하는 데 문제가 있으면 다시 로그인하고 다시 구성하십시오.

>[!NOTE]
>
>`cq:designPath` 사용은 선택 사항이며 SCF 구성 요소가 [clientlibs](client-customize.md#clientlibs-for-scf)를 사용하여 JS 및 CSS를 관리하므로 필요한 [clientlibs 사용](develop-app.md#includeclientlibsintemplate)과(와) 관련이 없습니다.
