---
title: 초기 샌드박스 컨텐츠
seo-title: Initial Sandbox Content
description: 콘텐츠 만들기
seo-description: Create content
uuid: 9810fe47-8d1a-4238-9b9c-0cc47c63d97a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: e8f28cd5-7950-4aab-bf62-3d4ed3d33cbd
exl-id: 068a0fff-ca48-4847-ba3f-d78416c97f6d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 5%

---

# 초기 샌드박스 컨텐츠 {#initial-sandbox-content}

이 섹션에서는 모든 사용자가 [페이지 템플릿](initial-app.md#createthepagetemplate):

* 기본 페이지의 영어 버전으로 리디렉션되는 SCF 샌드박스 사이트입니다.

   * SCF 샌드박스 - 사이트의 영어 버전에 대한 기본 페이지입니다.

   * SCF 재생 - 재생할 기본 페이지의 하위 페이지입니다.

이 자습서에서는 다음을 자세히 다루지 않습니다 [언어 복사](../../help/sites-administering/tc-prep.md)를 설정하는 경우, 루트 페이지가 HTML 헤더를 통해 사용자의 기본 언어 탐지를 구현하고 해당 언어에 대한 기본 페이지로 리디렉션할 수 있도록 설계되었습니다. 이 규칙은 페이지의 노드 이름에 두 문자로 이루어진 국가 코드를 사용하는 것입니다. 예를 들어, &quot;en&quot;은 영어로, &quot;fr&quot;은 프랑스어로 사용됩니다.

## 첫 번째 페이지 만들기 {#create-first-pages}

이제 [페이지 템플릿](initial-app.md#createthepagetemplate)/content 디렉토리에 웹 사이트의 루트 페이지를 설정할 수 있습니다.

1. 표준 UI는 현재 사이트 작성에 대한 청사진을 제공합니다. 이 자습서에서는 간단한 사이트를 만들 수 있으므로 클래식 UI가 유용합니다.

   클래식 UI로 전환하려면 전역 탐색 을 선택하고 프로젝트 아이콘 오른쪽을 마우스로 가리킵니다. 을(를) 선택합니다 *클래식 UI로 전환* 아이콘 표시:

   ![클래식 ui](assets/classic-ui.png)

   클래식 UI로 전환하는 기능은 [관리자가 사용](../../help/sites-administering/enable-classic-ui.md).

1. 에서 [클래식 UI 시작 페이지](http://localhost:4502/welcome.html), 선택 **[!UICONTROL 웹 사이트]**.

   ![classic-ui-website](assets/classic-ui-website.png)

   또는 웹 사이트용 클래식 UI에 직접 액세스하여 [/siteadmin](http://localhost:4502/siteadmin)

1. 탐색기 창에서 **[!UICONTROL 웹 사이트]** 그런 다음 도구 모음에서 를 선택합니다 **[!UICONTROL 새로 만들기]** > **[!UICONTROL 새 페이지]**.

   에서 **[!UICONTROL 페이지 만들기]** 대화 상자에서 다음을 입력합니다.

   * 제목: `SCF Sandbox Site`
   * 이름: `an-scf-sandbox`
   * 선택 **[!UICONTROL SCF 샌드박스 재생 템플릿]**
   * **[!UICONTROL 만들기]**&#x200B;를 클릭합니다

   ![classic-ui-create-page](assets/classic-ui-create-page.png)

1. 탐색기 창에서 방금 만든 페이지를 선택합니다. `/Websites/SCF Sandbox Site`를 클릭하고 **[!UICONTROL 새로 만들기]** > **[!UICONTROL 새 페이지]**:

   * 제목: `SCF Sandbox`
   * 이름: `en`
   * 선택 **[!UICONTROL SCF 샌드박스 재생 템플릿]**
   * **[!UICONTROL 만들기]**&#x200B;를 클릭합니다

1. 탐색기 창에서 방금 만든 페이지를 선택합니다. `/Websites/SCF Sandbox Site/SCF Sandbox`를 클릭하고 **[!UICONTROL 새로 만들기]** > **[!UICONTROL 새 페이지]**

   * 제목: `SCF Play`
   * 이름: `play`
   * 선택 **[!UICONTROL SCF 샌드박스 재생 템플릿]**
   * **[!UICONTROL 만들기]**&#x200B;를 클릭합니다

1. 웹 사이트 콘솔에 웹 사이트가 표시되는 방식입니다. 탐색기 창에서 선택한 항목의 하위 페이지가 관리할 수 있는 오른쪽 창에 표시됩니다.

   ![classic-ui-website-page](assets/classic-ui-website-page.png)

   웹 사이트 도구 및 템플릿을 사용하여 만든 저장소 보기입니다.

   ![classic-ui-repository-view](assets/classic-ui-repository-view.png)

## 디자인 경로 추가 {#add-the-design-path}

When ` [/etc/designs/an-scf-sandbox](setup-website.md#setupthedesigntreeetcdesigns)` 도구 콘솔의 디자인 섹션인 &quot; 속성을 사용하여 만들었습니다.

* `cq:template="/libs/wcm/core/templates/designpage"`

가 정의되었습니다. 이 정의된 값은 `currentDesign.getPath()`. 예

* `% String favIcon = currentDesign.getPath() + "/favicon.ico"; %`


   * 이름: `cq:designPath`
   * 유형: `String`
   * 값: `/etc/designs/an-scf-sandbox`

* 녹색 클릭 `[+] Add`

응답은 다음과 같이 표시됩니다.

![classic-ui-repository-path](assets/classic-ui-repository-path.png)

* 클릭 **[!UICONTROL 모두 저장]**

구성을 저장하는 동안 문제가 발생하면 다시 로그인하고 다시 구성합니다.

>[!NOTE]
>
>의 사용 `cq:designPath` 은 선택 사항이며 와 관련이 없습니다 [clientlibs 사용](develop-app.md#includeclientlibsintemplate)기본적으로 SCF 구성 요소가 사용할 때 필요합니다 [clientlibs](client-customize.md#clientlibs-for-scf) at.js 및 CSS를 관리
