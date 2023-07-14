---
title: 초기 샌드박스 콘텐츠
description: 콘텐츠 만들기
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 068a0fff-ca48-4847-ba3f-d78416c97f6d
source-git-commit: 260f71acd330167572d817fdf145a018b09cbc65
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 4%

---

# 초기 샌드박스 콘텐츠 {#initial-sandbox-content}

이 섹션에서는 다음 페이지를 만들어 모두 [페이지 템플릿](initial-app.md#createthepagetemplate):

* SCF 샌드박스 사이트 - 기본 페이지의 영어 버전으로 리디렉션합니다.

   * SCF 샌드박스 - 사이트의 영어 버전에 대한 메인 페이지.

   * SCF 재생 - 재생할 기본 페이지의 하위 항목.

이 자습서에서는 다음을 자세히 다루지 않습니다 [언어 복사](../../help/sites-administering/tc-prep.md), 루트 페이지가 HTML 헤더를 통해 사용자에 대한 기본 언어 감지를 구현하고 해당 언어에 대한 적절한 기본 페이지로 리디렉션할 수 있도록 설계되었습니다. 이 규칙은 페이지의 노드 이름에 두 글자로 된 국가 코드를 사용하는 것입니다. 예를 들어 영어는 &quot;en&quot;, 프랑스어는 &quot;fr&quot;입니다.

## 첫 페이지 만들기 {#create-first-pages}

이제 다음 항목이 있습니다. [페이지 템플릿](initial-app.md#createthepagetemplate)/content 디렉토리에서 웹 사이트의 루트 페이지를 설정할 수 있습니다.

1. 표준 UI는 현재 사이트를 만들기 위한 블루프린트를 제공합니다. 이 자습서에서는 간단한 사이트를 만들 때 클래식 UI가 유용합니다.

   클래식 UI로 전환하려면 전역 탐색 을 선택하고 프로젝트 아이콘의 오른쪽에 마우스를 가져다 놓습니다. 다음 항목 선택 *클래식 UI로 전환* 아이콘:

   ![classic-ui](assets/classic-ui.png)

   클래식 UI로 전환하는 기능은 다음과 같아야 합니다. [관리자가 활성화함](../../help/sites-administering/enable-classic-ui.md).

1. 다음에서 [클래식 UI 시작 페이지](http://localhost:4502/welcome.html), 선택 **[!UICONTROL 웹 사이트]**.

   ![classic-ui-website](assets/classic-ui-website.png)

   또는 을 찾아 웹 사이트용 클래식 UI에 직접 액세스합니다. [/siteadmin.](http://localhost:4502/siteadmin)

1. 탐색기 창에서 다음을 선택합니다. **[!UICONTROL 웹 사이트]** 그런 다음 도구 모음에서 를 선택합니다. **[!UICONTROL 신규]** > **[!UICONTROL 새 페이지]**.

   다음에서 **[!UICONTROL 페이지 만들기]** 대화 상자에서 다음을 입력합니다.

   * 제목: `SCF Sandbox Site`
   * 이름: `an-scf-sandbox`
   * 선택 **[!UICONTROL SCF 샌드박스 재생 템플릿]**
   * **[!UICONTROL 만들기]**&#x200B;를 클릭합니다

   ![classic-ui-create-page](assets/classic-ui-create-page.png)

1. 탐색기 창에서 만든 페이지를 선택합니다. `/Websites/SCF Sandbox Site`, 및 클릭 **[!UICONTROL 신규]** > **[!UICONTROL 새 페이지]**:

   * 제목: `SCF Sandbox`
   * 이름: `en`
   * 선택 **[!UICONTROL SCF 샌드박스 재생 템플릿]**
   * **[!UICONTROL 만들기]**&#x200B;를 클릭합니다

1. 탐색기 창에서 만든 페이지를 선택합니다. `/Websites/SCF Sandbox Site/SCF Sandbox`, 및 클릭 **[!UICONTROL 신규]** > **[!UICONTROL 새 페이지]**

   * 제목: `SCF Play`
   * 이름: `play`
   * 선택 **[!UICONTROL SCF 샌드박스 재생 템플릿]**
   * **[!UICONTROL 만들기]**&#x200B;를 클릭합니다

1. 이제 웹 사이트가 웹 사이트 콘솔에 표시되는 방식입니다. 탐색기 창에서 선택한 항목의 하위 페이지는 관리할 수 있는 오른쪽 창에 표시됩니다.

   ![classic-ui-website-page](assets/classic-ui-website-page.png)

   다음은 웹 사이트 도구 및 템플릿을 사용하여 작성된 항목의 저장소 보기입니다.

   ![classic-ui-repository-view](assets/classic-ui-repository-view.png)

## 디자인 경로 추가 {#add-the-design-path}

날짜 ` [/etc/designs/an-scf-sandbox](setup-website.md#setupthedesigntreeetcdesigns)` 은(는) 도구 콘솔의 디자인 섹션인 &quot; 속성을 사용하여 만들어졌습니다.

* `cq:template="/libs/wcm/core/templates/designpage"`

를 사용하여 스크립트에서 디자인 자산을 참조하는 선택적 기능을 제공하는 가 정의되었습니다. `currentDesign.getPath()`. 예

* `% String favIcon = currentDesign.getPath() + "/favicon.ico"; %`


   * 이름: `cq:designPath`
   * 유형: `String`
   * 값: `/etc/designs/an-scf-sandbox`

* 녹색 클릭 `[+] Add`

저장소는 다음과 같이 표시됩니다.

![classic-ui-repository-path](assets/classic-ui-repository-path.png)

* 클릭 **[!UICONTROL 모두 저장]**

구성을 저장하는 데 문제가 있으면 다시 로그인하고 다시 구성하십시오.

>[!NOTE]
>
>사용 `cq:designPath` 는 선택 사항이며 와 관련이 없습니다. [clientlibs 사용](develop-app.md#includeclientlibsintemplate): SCF 구성 요소가 [clientlibs](client-customize.md#clientlibs-for-scf) JS 및 CSS 관리
