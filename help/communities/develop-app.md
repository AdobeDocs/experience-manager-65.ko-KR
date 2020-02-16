---
title: 샌드박스 애플리케이션 개발
seo-title: 샌드박스 애플리케이션 개발
description: 기본 스크립트를 사용하여 애플리케이션 개발
seo-description: 기본 스크립트를 사용하여 애플리케이션 개발
uuid: 572f68cd-9ecb-4b43-a7f8-4aa8feb6c64e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 910229a3-38b1-44f1-9c09-55f8fd6cbb1d
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 샌드박스 애플리케이션 개발 {#develop-sandbox-application}

이 섹션에서는 템플릿이 [초기 애플리케이션](initial-app.md) 섹션에 설정되었으며 [초기 컨텐츠](initial-content.md) 섹션에 설정된 초기 페이지를 제공하므로, Communities 구성 요소를 사용하여 작성할 수 있는 기능을 포함하는 기초 스크립트를 사용하여 애플리케이션을 개발할 수 있습니다. 이 섹션의 끝에서 웹 사이트가 작동합니다.

## 기본 페이지 스크립트 사용 {#using-foundation-page-scripts}

재생 페이지 템플릿을 렌더링하는 구성 요소가 추가될 때 생성되는 기본 스크립트는 기본 페이지의 head.jsp 및 로컬 body.jsp를 포함하도록 수정됩니다.

### 슈퍼 리소스 유형 {#super-resource-type}

첫 번째 단계는 `/apps/an-scf-sandbox/components/playpage` 노드에 리소스 super 유형 속성을 추가하여 super 유형의 스크립트 및 속성을 상속합니다.

CRXDE Lite 사용:

<!--Resolve steps below-->
    * 이름:&#39;sling:resourceSuperType&#39;
    * 유형:&#39;String&#39;
    * 값:&#39;foundation/components/page&#39;

1. 녹색 **[!UICONTROL [+]추가를 클릭합니다]**
1. 모두 **[!UICONTROL 저장을 클릭합니다.]**

![chlimage_1-231](assets/chlimage_1-231.png)

### 헤드 및 바디 스크립트 {#head-and-body-scripts}

1. CRXDE **Lite** 탐색기 창에서 파일을 `/apps/an-scf-sandbox/components/playpage` 찾아 두 번 클릭하여 편집 창에서 파일을 `playpage.jsp` 엽니다.

#### /apps/an-scf-sandbox/components/playpage/playpage.jsp {#apps-an-scf-sandbox-components-playpage-playpage-jsp}

```xml
<%--

  An SCF Sandbox Play Component component.

  This is the component which renders content for An SCF Sandbox page.

--%><%
%><%@include file="/libs/foundation/global.jsp"%><%
%><%@page session="false" %><%
%><%
 // TODO add your code here
%>
```

1. 스크립트 태그가 열려 있거나 닫혀 있는 경우 &quot; // TODO ...&quot;를 바꾸십시오. &lt;html>의 헤드 및 본문 부분에 대한 스크립트 포함

   수퍼 유형이 `foundation/components/page`있는 경우, 동일한 폴더에 정의되어 있지 않은 스크립트는 `/apps/foundation/components/page` 폴더의 스크립트로 확인되고(있는 경우), 다른 스크립트는 `/libs/foundation/components/page` 폴더에 있습니다.

#### /apps/an-scf-sandbox/components/playpage/playpage.jsp {#apps-an-scf-sandbox-components-playpage-playpage-jsp-1}

```xml
<%--

    An SCF Sandbox Play Component component: playpage.jsp

  This is the component which renders content for An SCF Sandbox page.

--%><%
%><%@include file="/libs/foundation/global.jsp"%><%
%><%@page session="false" %>
<html>
  <cq:include script="head.jsp"/>
  <cq:include script="body.jsp"/>
</html>
```

1. 기본 스크립트를 오버레이할 `head.jsp` 필요는 없지만 기본 스크립트가 `body.jsp` 비어 있습니다.

   작성을 위해 설정하려면 로컬 스크립트와 오버레이하고 본문에 단락 시스템(parsys)을 `body.jsp` 포함하십시오.

   1. navigate to `/apps/an-scf-sandbox/components`
   1. `playpage`노드 선택
   1. 마우스 오른쪽 버튼을 클릭하고 선택 `Create > Create File...`

      * 이름: **body.jsp**
   1. 모두 **[!UICONTROL 저장을 클릭합니다.]**
   다음 텍스트를 열고 `/apps/an-scf-sandbox/components/playpage/body.jsp` 붙여 넣습니다.

   ```xml
   <%--
   
       An SCF Sandbox Play Component component: body.jsp
   
     This is the component which renders content for An SCF Sandbox page.
   
   --%><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   %><%@page session="false" %>
   <body>
       <h2>Community Play</h2>
       <cq:include path="par" resourceType="foundation/components/parsys" />
   </body>
   ```

1. 모두 **[!UICONTROL 저장을 클릭합니다.]**

**편집 모드에서 브라우저에서 페이지 보기:**

* 표준 UI: [http://localhost:4502/editor.html/content/an-scf-sandbox/en/play.html](http://localhost:4502/editor.html/content/an-scf-sandbox/en/play.md)

커뮤니티 재생 제목뿐만 아니라 페이지 **컨텐츠**&#x200B;편집용 UI도 표시됩니다.

자산/구성 요소 사이드 패널은 사이드 패널이 모두 열리고 창이 충분히 넓어서 사이드 컨텐츠와 페이지 컨텐츠가 모두 표시될 때 표시됩니다.

![chlimage_1-232](assets/chlimage_1-232.png)

* 클래식 UI: [http://localhost:4502/cf#/content/an-scf-sandbox/en/play.html](http://localhost:4502/cf#/content/an-scf-sandbox/en/play.html)

다음은 컨텐츠 파인더(cf)를 포함하여 클래식 UI에 재생 페이지가 표시되는 방식입니다.

![chlimage_1-233](assets/chlimage_1-233.png)

## 커뮤니티 구성 요소 {#communities-components}

저작용 커뮤니티 구성 요소를 활성화하려면 다음 지침에 따라 시작합니다.

* [커뮤니티 구성 요소 액세스](basics.md#accessing-communities-components)

이 샌드박스의 목적을 위해 다음 커뮤니티 **구성** 요소로 시작합니다(상자를 선택하여 활성화).

* 댓글
* 포럼
* 등급
* 검토
* 검토 요약(표시)
* 투표

또한 일반 **** 구성 요소(예:

* 이미지
* 표
* 텍스트
* 제목(Foundation)

>[!NOTE]
>
>페이지 패드에 대해 활성화된 구성 요소는 `components`
>`/etc/designs/an-scf-sandbox/jcr:content/playpage/par` node.

## 랜딩 페이지 {#landing-page}

다중 언어 환경에서 루트 페이지에는 기본 언어를 결정하기 위해 클라이언트의 요청을 분석하는 스크립트가 포함됩니다.

이 간단한 예에서는 루트 페이지가 영어 페이지로 리디렉션되도록 정적으로 설정되어 있는데, 이 페이지는 향후 개발 페이지에서 재생 페이지에 대한 링크가 있는 기본 랜딩 페이지로 연결될 수 있습니다.

브라우저 URL을 루트 페이지로 변경합니다. [http://localhost:4502/editor.html/content/an-scf-sandbox.html](https://locahost:4502/editor.html/content/an-scf-sandbox.html)

* 페이지 정보 아이콘 선택
* 속성 **[!UICONTROL 열기 선택]**
* 고급 탭에서

   * 리디렉션 항목의 경우 웹 사이트 > SCF **[!UICONTROL 샌드박스 사이트 > SCF 샌드박스로 이동합니다.]**
   * **[!UICONTROL 확인]**&#x200B;을 클릭합니다

* **[!UICONTROL 확인]**&#x200B;을 클릭합니다

사이트가 게시되면 게시 인스턴스에서 루트 페이지로 이동하면 영어 페이지로 리디렉션됩니다.

커뮤니티 SCF 구성 요소를 사용하기 전의 마지막 단계는 클라이언트 라이브러리 폴더(clientlibs)를 추가하는 것입니다.... **[⇒](add-clientlibs.md)**