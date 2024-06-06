---
title: 모든 기능을 갖춘 웹 사이트(JSP) 만들기
description: 이 튜토리얼에서는 Adobe Experience Manager(AEM)를 사용하여 모든 기능을 갖춘 웹 사이트를 만드는 방법을 설명합니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: d7cf843c-c837-4b97-b6c5-0fbd6793bdd4
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: ed7183efa57db6d97941e3acc99d126c2fc0f6c5
workflow-type: tm+mt
source-wordcount: '4919'
ht-degree: 3%

---

# 모든 기능을 갖춘 웹 사이트(JSP) 만들기{#create-a-fully-featured-website-jsp}

>[!NOTE]
>
>이 문서에서는 JSP를 사용하고 클래식 UI를 기반으로 하는 웹 사이트를 만드는 방법을 설명합니다. Adobe은 이 문서에 자세히 설명된 대로 웹 사이트에 최신 Adobe Experience Manager(AEM) 기술을 사용하는 것을 권장합니다 [AEM Sites 개발 시작](/help/sites-developing/getting-started.md).

이 자습서를 통해 AEM에서 모든 기능을 갖춘 웹 사이트를 만들 수 있습니다. 웹 사이트는 일반 웹 사이트를 기반으로 하며 주로 웹 개발자를 대상으로 합니다. 모든 개발은 작성자 환경 내에서 수행됩니다.

이 튜토리얼에서는 다음 방법을 설명합니다.

1. AEM을 설치합니다.
1. 액세스 CRXDE Lite(개발 환경).
1. CRXDE Lite에서 프로젝트 구조를 설정합니다.
1. 컨텐츠 페이지 작성의 기반으로 사용되는 템플릿, 구성 요소 및 스크립트를 작성합니다.
1. 웹 사이트의 루트 페이지를 만든 다음 컨텐츠 페이지를 만듭니다.
1. 페이지에서 사용할 다음 구성 요소를 만듭니다.

   * 위쪽 탐색
   * 하위 목록
   * 로고
   * 이미지
   * Text-Image
   * 검색

1. 다양한 기초 구성 요소를 포함합니다.

모든 단계를 수행한 후 페이지는 다음과 같이 표시되어야 합니다.

![chlimage_1-24](assets/chlimage_1-24.png)

**최종 결과 다운로드**

연습을 수행하지 않고 자습서와 함께 따르려면 website-1.0.zip을 다운로드합니다. 이 파일은 이 자습서의 결과를 포함하는 AEM 콘텐츠 패키지입니다. 사용 [패키지 관리자](/help/sites-administering/package-manager.md) 패키지를 작성자 인스턴스에 설치합니다.

**참고:** 이 패키지를 설치하면 이 자습서를 사용하여 만든 작성 인스턴스의 모든 리소스를 덮어씁니다.

웹 사이트 컨텐츠 패키지

[파일 가져오기](assets/website-1_0.zip)

## Adobe Experience Manager 설치 {#installing-adobe-experience-manager}

웹 사이트 개발을 위한 AEM 인스턴스를 설치하려면 [작성자 및 게시 인스턴스가 포함된 배포 환경](/help/sites-deploying/deploy.md#author-and-publish-installs)또는 다음을 수행합니다. [일반 설치](/help/sites-deploying/deploy.md#default-local-install). 일반 설치에는 AEM Quickstart JAR 파일을 다운로드하고, JAR 파일과 동일한 디렉토리에 license.properties 파일을 배치한 다음 JAR 파일을 두 번 클릭하는 작업이 포함됩니다.

AEM을 설치한 후 시작 페이지에서 CRXDE Lite 링크를 클릭하여 CRXDE Lite 개발 환경에 액세스합니다.

![chlimage_1-25](assets/chlimage_1-25.png)

>[!NOTE]
>
>기본 포트를 사용하여 로컬에 설치된 AEM 작성 인스턴스의 CRXDE Lite URL은 입니다. [https://localhost:4502/crx/de/](https://localhost:4502/crx/de/).

### CRXDE Lite에서 프로젝트 구조 설정 {#setting-up-the-project-structure-in-crxde-lite}

CRXDE Lite을 사용하여 저장소에서 mywebsite 애플리케이션 구조를 생성합니다.

1. CRXDE Lite 왼쪽에 있는 트리에서 **`/apps`** 폴더 및 클릭 **만들기** > **만들기** **폴더**. 다음에서 **폴더 만들기** 대화 상자, 유형 `mywebsite` 을 폴더 이름으로 사용하고 **확인**.
1. 마우스 오른쪽 단추 클릭 **`/apps/mywebsite`** 폴더 및 클릭 **만들기** > **폴더 만들기**. 다음에서 **폴더 만들기** 대화 상자, 유형 `components` 을 폴더 이름으로 사용하고 **확인**.
1. 마우스 오른쪽 단추 클릭 **`/apps/mywebsite`** 폴더 및 클릭 **만들기** > **폴더 만들기**. 다음에서 **폴더 만들기** 대화 상자, 유형 `templates` 을 폴더 이름으로 사용하고 **확인**.

   이제 트리의 구조는 다음과 같이 표시되어야 합니다.

   ![chlimage_1-26](assets/chlimage_1-26.png)

1. **모두 저장**&#x200B;을 클릭합니다.

### 디자인 설정 {#setting-up-the-design}

이 단원에서는 디자이너 도구를 사용하여 응용 프로그램의 디자인을 만듭니다. 디자인은 웹 사이트에 대한 CSS 및 이미지 리소스를 제공합니다.

>[!NOTE]
>
>mywebsite.zip을 다운로드하려면 다음 링크를 클릭하십시오. 아카이브에는 디자인에 대한 static.css 및 이미지 파일이 포함되어 있습니다.

샘플 static.css 파일 및 이미지

[파일 가져오기](assets/mywebsite.zip)

1. AEM 시작 페이지에서 **도구**. ([https://localhost:4502/libs/cq/core/content/welcome.html](https://localhost:4502/libs/cq/core/content/welcome.html))

   ![chlimage_1-27](assets/chlimage_1-27.png)

1. 폴더 트리에서 **디자인** 폴더를 클릭한 다음 **신규** > **새 페이지**. 유형 `mywebsite` 을 제목으로 사용하고 클릭 **만들기**.

1. mywebsite 항목이 테이블에 표시되지 않으면 트리 또는 테이블을 새로 고칩니다.

1. [WebDAV 사용](/help/sites-administering/webdav-access.md) https://localhost:4502에서 URL에 액세스하여 샘플을 복사합니다. `static.css` 파일 및 `images` 다운로드한 mywebsite.zip 파일의 폴더를 `/etc/designs/mywebsite` 폴더를 삭제합니다.

   ![chlimage_1-28](assets/chlimage_1-28.png)

### Contentpage 템플릿, 구성 요소 및 스크립트 만들기 {#creating-the-contentpage-template-component-and-script}

이 섹션에서는 다음을 만듭니다.

* 예제 웹 사이트에서 컨텐츠 페이지를 만드는 데 사용되는 컨텐츠 페이지 템플릿입니다.
* 컨텐츠 페이지를 렌더링하는 데 사용되는 contentpage 구성 요소입니다.
* contentpage 스크립트.

#### Contentpage 템플릿 만들기 {#creating-the-contentpage-template}

사이트의 웹 페이지의 기반으로 사용할 템플릿을 만듭니다.

템플릿은 새 페이지의 기본 콘텐츠를 정의합니다. 복잡한 웹 사이트에서는 사이트에서 서로 다른 유형의 페이지를 만들기 위해 여러 템플릿을 사용할 수 있습니다. 이 연습에서는 모든 페이지가 하나의 간단한 템플릿을 기반으로 합니다.

1. CRXDE Lite의 폴더 트리에서 마우스 오른쪽 단추를 클릭합니다 `/apps/mywebsite/templates` 및 클릭 **만들기** > **템플릿 만들기**.

1. 템플릿 만들기 대화 상자에서 다음 값을 입력한 다음 **다음**:

   * **레이블**: contentpage
   * **제목**: 내 웹 사이트 콘텐츠 페이지 템플릿
   * **설명**: 내 웹 사이트 콘텐츠 페이지 템플릿입니다.
   * **리소스 유형:** mywebsite/components/contentpage

   Ranking 속성에 기본값을 사용합니다.

   ![chlimage_1-29](assets/chlimage_1-29.png)

   리소스 유형은 페이지를 렌더링하는 구성 요소를 식별합니다. 이 경우 contentpage 템플릿을 사용하여 만든 모든 페이지는 `mywebsite/components/contentpage` 구성 요소.

1. 이 템플릿을 사용할 수 있는 페이지 경로를 지정하려면 더하기 버튼을 클릭하고 을 입력합니다 `/content(/.*)?` 표시되는 텍스트 상자에 입력합니다. 그런 다음 을 클릭합니다. **다음**.

   ![chlimage_1-30](assets/chlimage_1-30.png)

   허용되는 경로 속성의 값은 입니다. *정규 표현식입니다.* 표현식과 일치하는 경로가 있는 페이지는 템플릿을 사용할 수 있습니다. 이 경우 정규 표현식은 의 경로와 일치합니다 **/content** 폴더 및 모든 하위 페이지.

   작성자가 /content 아래에 페이지를 만들 때 **contentpage** 사용할 수 있는 템플릿 목록에 템플릿이 나타납니다.

1. 클릭 **다음** 다음에서 **허용된 상위** 및 **허용된 하위** 패널 및 클릭 **확인**. CRXDE Lite에서 **모두 저장**.

   ![chlimage_1-31](assets/chlimage_1-31.png)

#### Contentpage 구성 요소 만들기 {#creating-the-contentpage-component}

만들기 *구성 요소* 콘텐츠를 정의하고 contentpage 템플릿을 사용하는 페이지를 렌더링합니다. 구성 요소의 위치는 contentpage 템플릿의 리소스 유형 속성 값과 일치해야 합니다.

1. CRXDE Lite에서 마우스 오른쪽 단추 클릭 `/apps/mywebsite/components` 및 클릭 **만들기** > **구성 요소**.
1. 다음에서 **구성 요소 만들기** 대화 상자에서 다음 속성 값을 입력합니다.

   * **레이블**: contentpage
   * **제목**: 내 웹 사이트 콘텐츠 페이지 구성 요소
   * **설명**: 내 웹 사이트 콘텐츠 페이지 구성 요소입니다

   ![chlimage_1-32](assets/chlimage_1-32.png)

   새 구성 요소의 위치는 입니다. `/apps/mywebsite/components/contentpage`. 이 경로는 contentpage 템플릿의 리소스 유형( 초기 포함)에 해당합니다. **`/apps/`** 경로의 일부).

   이 서신은 템플릿을 구성 요소에 연결하고 웹 사이트의 올바른 기능에 중요합니다.

1. 클릭 **다음** 대화 상자의 [허용된 하위] 패널이 나타날 때까지 을 클릭하고 **확인**. CRXDE Lite에서 **모두 저장**.

   이제 구조는 다음과 같습니다.

   ![chlimage_1-33](assets/chlimage_1-33.png)

#### Contentpage 구성 요소 스크립트 개발 {#developing-the-contentpage-component-script}

contentpage.jsp 스크립트에 코드를 추가하여 페이지 콘텐츠를 정의합니다.

1. CRXDE Lite에서 파일을 엽니다. `contentpage.jsp` 위치: `/apps/mywebsite/components/contentpage`. 파일에는 기본적으로 다음 코드가 포함되어 있습니다.

   ```java
   <%--
   
     My Website Content Page Component component.
   
     This is My Website Content Page Component.
   
   --%><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   %><%@page session="false" %><%
   %><%
       /* TODO add you code here */
   %>
   ```

1. 다음 코드를 복사하여 기본 코드 뒤에 contentpage.jsp에 붙여넣습니다.

   ```java
   <%@ page language="java" contentType="text/html; charset=ISO-8859-1"
       pageEncoding="ISO-8859-1"%>
   <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN"
   "https://www.w3.org/TR/html4/loose.dtd">
   <html>
   <head>
   <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
   <title>My title</title>
   </head>
   <body>
   <div>My body</div>
   </body>
   </html>
   ```

1. 클릭 **모두 저장** 변경 사항을 저장합니다.

### 웹 사이트 페이지 및 컨텐츠 페이지 만들기 {#creating-your-website-page-and-content-pages}

이 섹션에서는 내 웹 사이트, 영어, 제품, 서비스 및 고객 페이지에서 컨텐츠 페이지 템플릿을 사용하는 페이지를 만듭니다.

1. AEM 시작 페이지 ([https://localhost:4502/libs/cq/core/content/welcome.html](https://localhost:4502/libs/cq/core/content/welcome.html)) 웹 사이트를 클릭합니다.

   ![chlimage_1-34](assets/chlimage_1-34.png)

1. 폴더 트리에서 **웹 사이트** 폴더를 클릭한 다음 **신규** > **새 페이지**.
1. 다음에서 **페이지 만들기** 창에서 다음을 입력합니다.

   * 제목: `My Website`
   * 이름: `mywebsite`
   * 다음 항목 선택 `My Website Content Page Template`

   ![chlimage_1-35](assets/chlimage_1-35.png)

1. **만들기**&#x200B;를 클릭합니다. 폴더 트리에서 **/Websites/내 웹 사이트** 페이지 및 클릭 **신규** > **새 페이지**.
1. [페이지 만들기] 대화 상자에서 다음 속성 값을 입력한 다음 [만들기]를 클릭합니다.

   * 제목: 영어
   * 이름: en
   * 내 웹 사이트 컨텐츠 페이지 템플릿 선택

1. 폴더 트리에서 **/Websites/내 웹 사이트/영어** 페이지 및 클릭 **신규**> **새 페이지**.
1. 다음에서 **페이지 만들기** 대화 상자에서 다음 속성 값을 입력한 다음 **만들기**:

   * 제목: Products
   * 내 웹 사이트 컨텐츠 페이지 템플릿 선택

1. 폴더 트리에서 **/Websites/내 웹 사이트/영어** 페이지 및 클릭 **신규** > **새 페이지**.
1. 다음에서 **페이지 만들기** 대화 상자에서 다음 속성 값을 입력한 다음 **만들기**:

   * 제목: 서비스
   * 내 웹 사이트 컨텐츠 페이지 템플릿 선택

1. 폴더 트리에서 **/Websites/내 웹 사이트/영어** 페이지 및 클릭 **신규** > **새 페이지**.
1. 다음에서 **페이지 만들기** 대화 상자에서 다음 속성 값을 입력한 다음 **만들기**:

   * 제목: 고객
   * 내 웹 사이트 컨텐츠 페이지 템플릿 선택

   구조는 다음과 같습니다.

   ![chlimage_1-36](assets/chlimage_1-36.png)

1. 페이지를 mywebsite 디자인에 연결하려면 CRXDE Lite에서 `/content/mywebsite/en/jcr:content` 노드. 속성 탭에서 새 속성에 대해 다음 값을 입력한 다음 추가를 클릭합니다.

   * 이름: cq:designPath
   * 유형: 문자열
   * 값: /etc/designs/mywebsite

   ![chlimage_1-37](assets/chlimage_1-37.png)

1. 새 웹 브라우저 탭 또는 창에서 을 엽니다. [https://localhost:4502/content/mywebsite/en/products.html](https://localhost:4502/content/mywebsite/en/products.html) 제품 페이지를 보려면 다음 작업을 수행하십시오.

   ![chlimage_1-38](assets/chlimage_1-38.png)

### Contentpage 스크립트 향상 {#enhancing-the-contentpage-script}

이 섹션에서는 AEM foundation 구성 요소 스크립트를 사용하고 고유한 스크립트를 작성하여 콘텐츠 페이지 스크립트를 향상시키는 방법에 대해 설명합니다.

작업을 마치면 **제품** 페이지는 다음과 같아야 합니다.

![chlimage_1](assets/chlimage_1.jpeg)

#### Foundation 페이지 스크립트 사용 {#using-the-foundation-page-scripts}

이 연습에서는 상위 유형이 AEM Page 구성 요소가 되도록 pagecontent 구성 요소를 구성합니다. 구성 요소는 슈퍼타입의 기능을 상속받기 때문에 page 컨텐츠는 페이지 구성 요소의 스크립트와 속성을 상속받습니다.

예를 들어 구성 요소 JSP 코드에서 슈퍼타입 구성 요소가 구성 요소에 포함된 것처럼 제공하는 스크립트를 참조할 수 있습니다.

1. CRXDE Lite에서 속성을 `/apps/mywebsite/components/contentpage` 노드.

   1. 다음 항목 선택 `/apps/mywebsite/components/contentpage` 노드.
   1. 속성 탭 하단에 다음 속성 값을 입력한 다음 추가를 클릭합니다.

      * **이름:** sling:resourceSuperType
      * **유형:** 문자열
      * **값:** foundation/components/page

   1. 모두 저장을 클릭합니다.

1. 를 엽니다. `contentpage.jsp` 파일: `/apps/mywebsite/components/contentpage` 기존 코드를 다음 코드로 바꿉니다.

   ```xml
   <%@include file="/libs/foundation/global.jsp"%><%
   %><%@page session="false" contentType="text/html; charset=utf-8" %><%
   %><!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "https://www.w3.org/TR/html4/strict.dtd">
   <html>
   <cq:include script="head.jsp"/>
   <cq:include script="body.jsp"/>
   </html>
   ```

1. 변경 사항을 저장합니다.
1. 브라우저에서 제품 페이지를 다시 로드합니다. 이는 다음과 같습니다.

   ![chlimage_1-1](assets/chlimage_1-1.jpeg)

   페이지 소스를 열어 head.jsp 및 body.jsp 스크립트가 생성한 JavaScript 및 HTML 요소를 확인합니다. 페이지를 열면 다음 스크립트 코드 조각이 Sidekick에 열립니다.

   ```java
   CQ.WCM.launchSidekick("/content/mywebsite/en/products",
               {propsDialog: "/libs/foundation/components/page/dialog",
                  locked: false locked: false
                });
   ```

#### 자체 스크립트 사용 {#using-your-own-scripts}

이 섹션에서는 페이지 본문의 일부를 각각 생성하는 몇 개의 스크립트를 만듭니다. 그런 다음 pageContent 구성 요소에 body.jsp 파일을 생성하여 AEM Page 구성 요소의 body.jsp를 재정의합니다. body.jsp 파일에 페이지 본문의 다른 부분을 생성하는 스크립트를 포함합니다.

**팁:** 구성 요소의 슈퍼타입으로 파일과 이름 및 상대 위치가 같은 파일이 구성 요소에 포함되어 있으면 이 파일을 이라고 합니다 *오버레이*.

1. CRXDE Lite에서 파일을 만듭니다. `left.jsp` 아래에 `/apps/mywebsite/components/contentpage`:

   1. 노드를 마우스 오른쪽 버튼으로 클릭합니다. `/apps/mywebsite/components/contentpage`그런 다음 **만들기**then을 선택합니다. **파일 만들기**.

   1. 창에서 을(를) 입력합니다 `left.jsp` (으)로 **이름** 및 클릭 **확인**.

1. 파일 편집 `left.jsp` 기존 콘텐츠를 제거하고 다음 코드로 바꾸려면 다음을 수행합니다.

   ```java
   <%@include file="/libs/foundation/global.jsp"%><%
   %><div class="left">
   <div>logo</div>
   <div>newslist</div>
   <div>search</div>
   </div>
   ```

1. 변경 사항을 저장합니다.
1. CRXDE Lite에서 파일을 만듭니다. `center.jsp` 아래에 `/apps/mywebsite/components/contentpage`:

   1. 노드를 마우스 오른쪽 버튼으로 클릭합니다. `/apps/mywebsite/components/contentpage`, 선택 **만들기**, 그런 다음 **파일 만들기**.

   1. 대화 상자에서 다음을 입력합니다. `center.jsp` 다음으로: **이름** 및 클릭 **확인**.

1. 파일 편집 `center.jsp` 기존 콘텐츠를 제거하고 다음 코드로 바꾸려면 다음을 수행합니다.

   ```java
   <%@include file="/libs/foundation/global.jsp"%><%
   %><div class="center">
   <div>trail</div>
   <div>title</div>
   <div>parsys</div>
   </div>
   ```

1. 변경 사항을 저장합니다.
1. CRXDE Lite에서 파일을 만듭니다. `right.jsp` 아래에 `/apps/mywebsite/components/contentpage`:

   1. 노드를 마우스 오른쪽 버튼으로 클릭합니다. `/apps/mywebsite/components/contentpage`, 선택 **만들기**, 그런 다음 **파일 만들기**.

   1. 대화 상자에서 다음을 입력합니다. `right.jsp` 다음으로: **이름** 및 클릭 **확인**.

1. 파일 편집 `right.jsp` 기존 콘텐츠를 제거하고 다음 코드로 바꾸려면 다음을 수행합니다.

   ```java
   <%@include file="/libs/foundation/global.jsp"%><%
   %><div class="right">
   <div>iparsys</div>
   </div>
   ```

1. 변경 사항을 저장합니다.
1. CRXDE Lite에서 파일을 만듭니다. `body.jsp` 아래에 `/apps/mywebsite/components/contentpage`:
1. 파일 편집 `body.jsp` 기존 콘텐츠를 제거하고 다음 코드로 바꾸려면 다음을 수행합니다.

   ```java
   <%@include file="/libs/foundation/global.jsp"%><%
   %><body>
   <div id="CQ">
   <div class="topnav">topnav</div>
   <div class="content">
   <cq:include script="left.jsp" />
   <cq:include script="center.jsp" />
   <cq:include script="right.jsp" />
   </div>
   <div class="footer">
   <div class="toolbar">toolbar</div>
   </div>
   </div>
   </body>
   ```

1. 변경 사항을 저장합니다.
1. 브라우저에서 제품 페이지를 다시 로드합니다. 이는 다음과 같습니다.

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

### 상단 탐색 구성 요소 만들기 {#creating-the-top-navigation-component}

이 섹션에서는 쉽게 탐색할 수 있도록 웹 사이트의 모든 최상위 페이지에 대한 링크를 표시하는 구성 요소를 만듭니다. 이 구성 요소 콘텐츠는 콘텐츠 페이지 템플릿을 사용하여 만든 모든 페이지의 맨 위에 표시됩니다.

위쪽 탐색 구성 요소의 첫 번째 버전(topnav)에서 탐색 항목은 텍스트 링크입니다. 두 번째 버전에서는 이미지 탐색 링크와 함께 topnav를 구현합니다.

완료되면 위쪽 탐색은 다음과 같이 표시됩니다.

![chlimage_1-39](assets/chlimage_1-39.png)

#### 상단 탐색 구성 요소 만들기 {#creating-the-top-navigation-component-1}

1. CRXDE Lite에서 마우스 오른쪽 단추 클릭 `/apps/mywebsite/components`, 선택 **만들기**, 그런 다음 **구성 요소 만들기**.
1. 다음에서 **구성 요소 만들기** 창에서 다음을 입력합니다.

   * **레이블**: `topnav`

   * **제목**: `My Top Navigation Component`

   * **설명**: `This is My Top Navigation Component`

1. 클릭 **다음** 을 클릭하는 마지막 창이 나타날 때까지 **확인**. 변경 사항을 저장합니다.

#### 텍스트 링크를 사용하여 위쪽 탐색 스크립트 만들기 {#creating-the-top-navigation-script-with-textual-links}

상위 탐색에 렌더링 스크립트를 추가하여 하위 페이지에 대한 텍스트 링크를 생성합니다.

1. CRXDE Lite에서 파일을 엽니다. `topnav.jsp` 아래에 `/apps/mywebsite/components/topnav`.
1. 다음 코드를 복사하여 붙여 넣어 있는 코드를 바꿉니다.

   ```xml
   <%@include file="/libs/foundation/global.jsp"%><%
   %><%@ page import="java.util.Iterator,
           com.day.text.Text,
           com.day.cq.wcm.api.PageFilter, com.day.cq.wcm.api.Page" %><%
       /* get starting point of navigation */
       Page navRootPage = currentPage.getAbsoluteParent(2);
       if (navRootPage == null && currentPage != null) {
       navRootPage = currentPage;
       }
       if (navRootPage != null) {
           Iterator<Page> children = navRootPage.listChildren(new PageFilter(request));
           while (children.hasNext()) {
               Page child = children.next();
               %><a href="<%= child.getPath() %>.html"><%=child.getTitle() %></a><%
           }
       }
   %>
   ```

#### Contentpage 구성 요소에 위쪽 탐색 포함 {#including-top-navigation-in-the-contentpage-component}

contentpage 구성 요소에 topnav를 포함하려면 다음을 수행합니다.

1. CRXDE Lite에서 `body.jsp` 아래에 `/apps/mywebsite/components/contentpage`및 바꾸기:

   ```xml
   <div class="topnav">topnav</div>
   ```

   포함:

   ```xml
   <cq:include path="topnav" resourceType="mywebsite/components/topnav" />
   ```

1. 변경 사항을 저장합니다.
1. 브라우저에서 제품 페이지를 다시 로드합니다. 위쪽 탐색은 다음과 같이 나타납니다.

   ![chlimage_1-40](assets/chlimage_1-40.png)

#### 자막으로 페이지 향상 {#enhancing-pages-with-subtitles}

페이지 구성 요소는 페이지에 캡션을 제공할 수 있는 속성을 정의합니다. 페이지 콘텐츠에 대한 정보를 제공하는 캡션을 추가합니다.

1. 브라우저에서 **제품** 페이지를 가리키도록 업데이트하는 중입니다.
1. Sidekick **페이지** 탭을 클릭하고 **페이지 속성**.
1. 대화 상자의 기본 탭에서 을 확장합니다. **기타 제목 및 설명,** 및 **부제** 속성, 유형 **우리가 하는 일**. **확인**&#x200B;을 클릭합니다.
1. 자막을 추가하려면 이전 단계를 반복하십시오. **서비스 정보** (으)로 **서비스** 페이지를 가리키도록 업데이트하는 중입니다.
1. 자막을 추가하려면 이전 단계를 반복하십시오. **우리가 얻는 신뢰** (으)로 **고객** 페이지를 가리키도록 업데이트하는 중입니다.

   **팁:** CRXDE Lite에서 /content/mywebsite/en/products/jcr:content 노드를 선택하여 자막 속성이 추가되었는지 확인합니다.

#### 이미지 링크를 사용하여 위쪽 탐색 기능 향상 {#enhance-top-navigation-by-using-image-links}

탐색 컨트롤에 하이퍼텍스트 대신 이미지 링크를 사용하도록 topnav 구성 요소의 렌더링 스크립트를 개선합니다. 이미지에는 링크 대상의 제목과 부제가 포함되어 있습니다.

이 연습에서는 [Sling 요청 처리](/help/sites-developing/the-basics.md#sling-request-processing). 페이지 탐색 링크에 사용할 이미지를 동적으로 생성하는 스크립트를 호출하도록 topnav.jsp 스크립트가 수정되었습니다. 이 연습에서는 Sling이 이미지 소스 파일의 URL을 구문 분석하여 이미지 렌더링에 사용할 스크립트를 결정합니다.

예를 들어 제품 페이지에 대한 이미지 링크의 소스는 https://localhost:4502/content/mywebsite/en/products.navimage.png일 수 있습니다. Sling은 이 URL을 구문 분석하여 리소스 유형과 리소스 렌더링에 사용할 스크립트를 결정합니다.

1. Sling은 리소스의 경로를 `/content/mwebysite/en/products.png.`
1. Sling은 이 경로를 `/content/mywebsite/en/products` 노드.
1. Sling이 다음을 결정합니다. `sling:resourceType` /이 노드의 `mywebsite/components/contentpage`.

1. Sling은 이 구성 요소에서 URL 선택기와 가장 일치하는 스크립트를 찾습니다( `navimage`) 및 파일 이름 확장명( `png`).

이 연습에서는 Sling이 이러한 URL을 사용자가 만드는 /apps/mywebsite/components/contentpage/navimage.png.java 스크립트와 일치시킵니다.

1. CRXDE Lite에서 `topnav.jsp` 아래에 `/apps/mywebsite/components/topnav.`앵커 요소의 내용(14행)을 찾습니다.

   ```xml
   <%=child.getTitle() %>
   ```

1. 앵커 콘텐츠를 다음 코드로 바꿉니다.

   ```xml
   <img alt="<%= child.getTitle() %>" src="<%= child.getPath() %>.navimage.png">
   ```

1. 변경 사항을 저장합니다.
1. 마우스 오른쪽 단추 클릭 `/apps/mywebsite/components/contentpage` 노드 및 클릭 **만들기** > **파일 만들기**.
1. 다음에서 **파일 만들기** 창, as **이름**, 유형 `navimage.png.java`.

   .java 파일 이름 확장명은 Apache Sling Scripting Java™ 지원을 사용하여 스크립트를 컴파일하고 서블릿을 생성해야 함을 Sling에 나타냅니다.

1. 다음 코드를에 복사합니다 `navimage.png.java.`이 코드는 AbstractImageServlet 클래스를 확장합니다.

   * [AbstractImageServlet](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.html) 현재 리소스의 속성을 저장하는 ImageContext 개체를 만듭니다.
   * 리소스의 상위 페이지는 ImageContext 개체에서 추출됩니다. 그런 다음 페이지 제목과 자막을 얻습니다.
   * [이미지 도우미](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/ImageHelper.html) 사이트 디자인, 페이지 제목 및 페이지 부제의 navimage_bg.jpg 파일에서 이미지를 생성하는 데 사용됩니다.

   ```java
   package apps.mywebsite.components.contentpage;
   
   import java.awt.Color;
   import java.awt.Paint;
   import java.awt.geom.Rectangle2D;
   
   import java.io.IOException;
   import javax.jcr.RepositoryException;
   
   import com.day.cq.wcm.api.Page;
   import com.day.cq.wcm.api.PageManager;
   import com.day.cq.wcm.api.components.Component;
   import com.day.cq.wcm.api.designer.Designer;
   
   import com.day.cq.commons.SlingRepositoryException;
   import com.day.cq.wcm.commons.WCMUtils;
   import com.day.cq.wcm.commons.AbstractImageServlet;
   import com.day.cq.commons.ImageHelper;
   
   import com.day.image.Font;
   import com.day.image.Layer;
   
   import org.apache.sling.api.SlingHttpServletRequest;
   import org.apache.sling.api.SlingHttpServletResponse;
   import org.apache.sling.api.resource.Resource;
   import org.apache.sling.api.servlets.SlingSafeMethodsServlet;
   
   /**
     * Renders the navigation image
     */
   public class navimage_png extends AbstractImageServlet {
   
         protected Layer createLayer(ImageContext ctx)
                throws RepositoryException, IOException {
            PageManager pageManager = ctx.resolver.adaptTo(PageManager.class);
            Page currentPage = pageManager.getContainingPage(ctx.resource);
   
            /* constants for image appearance */
            int scale = 6;
            int paddingX = 24;
            int paddingY = 24;
            Color bgColor = new Color(0x004a565c, true);
   
            /* obtain the page title */
            String title = currentPage.getTitle();
            if (title == null) {
                title = currentPage.getName();
            }
   
            /* format the title text */
            title = title.toUpperCase();
            Paint titleColor = Color.WHITE;
            Font titleFont = new Font("Myriad Pro", 10 * scale, Font.BOLD);
            int titleBase = 10 * scale;
   
            /* obtain and format the page subtitle */
            String subtitle = currentPage.getProperties().get("subtitle", "");
            Paint subtitleColor = new Color(0xffa9afb1, true);
            Font subTitleFont = new Font("Tahoma", 7);
            int subTitleBase = 20;
   
            /* create a layer that contains the background image from the mywebsite design */
            Designer dg = ctx.resolver.adaptTo(Designer.class);
            String imgPath = new String(dg.getDesignPath(currentPage)+"/images/navimage_bg.jpg");
            Layer bg = ImageHelper.createLayer(ctx.resolver.resolve(imgPath));
   
            /* draw the title text (4 times bigger) */
            Rectangle2D titleExtent = titleFont.getTextExtent(0, 0, 0, 0, title, Font.ALIGN_LEFT, 0, 0);
            Rectangle2D subtitleExtent = subTitleFont.getTextExtent(0, 0, 0, 0, subtitle, Font.ALIGN_LEFT, 0, 0);
   
            /* ensure subtitleExtent is wide enough */
            if ( subtitle.length() > 0 ) {
                int titleWidth = (int)titleExtent.getWidth() / scale;
                if ( subtitleExtent.getWidth() > titleWidth && subtitleExtent.getWidth() + 2 * paddingX >
    bg.getWidth() ) {
                    int charWidth = (int)subtitleExtent.getWidth() / subtitle.length();
                    int maxWidth = (bg.getWidth() > titleWidth + 2  * paddingX ? bg.getWidth() - 2 * paddingX : titleWidth);
                    int len = (maxWidth - ( 2 * charWidth) ) / charWidth;
                    subtitle = subtitle.substring(0, len) + "...";
                    subtitleExtent = subTitleFont.getTextExtent(0, 0, 0, 0, subtitle, Font.ALIGN_LEFT, 0, 0);
                }
            }
            int width = Math.max((int) titleExtent.getWidth(), (int) subtitleExtent.getWidth());
           /* create the text layer */
            Layer text = new Layer(width, (int) titleExtent.getHeight() + 40, new Color(0x01ffffff, true));
            text.setPaint(titleColor);
            text.drawText(0, titleBase, 0, 0, title, titleFont, Font.ALIGN_LEFT | Font.ALIGN_BASE, 0, 0);
            text.resize(text.getWidth() / scale, text.getHeight() / scale);
            text.setX(0);
            text.setY(0);
   
            if (subtitle.length() > 0) {
                /* draw the subtitle normal sized */
                text.setPaint(subtitleColor);
                text.drawText(0, subTitleBase, 0, 0, subtitle, subTitleFont, Font.ALIGN_LEFT | Font.ALIGN_BASE, 0, 0);
            }
   
            /* merge the image and text layers */
            text.setY(paddingY);
            text.setX(paddingX);
            text.setBackgroundColor(bgColor);
   
            int bgWidth = bg.getWidth();
            if ( text.getWidth() + 2 * paddingX > bgWidth ) {
                bgWidth = text.getWidth() + 2 * paddingX;
                bg.resize(bgWidth, bg.getHeight());
            }
            bg.merge(text);
   
            return bg;
        }
    }
   ```

1. 변경 사항을 저장합니다.
1. 브라우저에서 제품 페이지를 다시 로드합니다. 이제 위쪽 탐색이 다음과 같이 표시됩니다.

   ![screen_shot_2012-03-07at10047pm](assets/screen_shot_2012-03-07at10047pm.png)

### 하위 목록 구성 요소 만들기 {#creating-the-list-children-component}

페이지 제목, 설명 및 날짜(예: 제품 페이지)를 포함하는 페이지 링크 목록을 생성하는 listchildren 구성 요소를 만듭니다. 이 링크는 현재 페이지의 하위 페이지 또는 구성 요소 대화 상자에 지정된 루트 페이지의 하위 페이지를 대상으로 합니다.

![chlimage_1-41](assets/chlimage_1-41.png)

#### 제품 페이지 만들기 {#creating-product-pages}

제품 페이지 아래에 두 페이지를 만듭니다. 두 개의 특정 제품을 설명하는 각 페이지에 대해 제목, 설명 및 날짜를 설정합니다.

1. 웹 사이트 페이지의 폴더 트리에서 웹 사이트/내 웹 사이트/영어/제품 항목을 선택하고 새로 만들기 > 새 페이지 를 클릭합니다.
1. 대화 상자에서 다음 속성 값을 입력한 다음 [만들기]를 클릭합니다.

   * 제목: 제품 1.
   * 이름: product1.
   * 내 웹 사이트 컨텐츠 페이지 템플릿 선택

1. 다음 속성 값을 사용하여 Products 아래에 다른 페이지를 만듭니다.

   * 제목: 제품 2
   * 이름: product2
   * 내 웹 사이트 컨텐츠 페이지 템플릿 선택

1. CRXDE Lite에서 제품 1 페이지에 대한 설명 및 날짜를 설정합니다.

   1. 다음 항목 선택 `/content/mywebsite/en/products/product1/jcr:content` 노드.
   1. 다음에서 **속성** 탭에서 다음 값을 입력합니다.

      * 이름: `jcr:description`
      * 유형: `String`
      * 값: `This is a description of the Product 1!.`

   1. 클릭 **추가**.
   1. 다음에서 **속성** 탭에서 다음 값을 사용하여 다른 속성을 만듭니다.

      * 이름: 날짜
      * 유형: 문자열
      * 값: 2008/02/14
      * 추가를 클릭합니다.

   1. 모두 저장을 클릭합니다.

1. CRXDE Lite에서 제품 2 페이지에 대한 설명 및 날짜를 설정합니다.

   1. /content/mywebsite/en/products/product2/jcr:content 노드를 선택합니다.
   1. 다음에서 **속성** 탭에서 다음 값을 입력합니다.

      * 이름: jcr:description
      * 유형: 문자열
      * 값: 제품 2에 대한 설명입니다.

   1. 클릭 **추가**.
   1. 동일한 텍스트 상자에서 이전 값을 다음 값으로 바꿉니다.

      * 이름: 날짜
      * 유형: 문자열
      * 값: 2012/05/11
      * 추가를 클릭합니다.

   1. 모두 저장을 클릭합니다.

#### 하위 목록 구성 요소 만들기 {#creating-the-list-children-component-1}

listchildren 구성 요소를 만들려면 다음을 수행하십시오.

1. CRXDE Lite에서 마우스 오른쪽 단추 클릭 `/apps/mywebsite/components`, 선택 **만들기**, 그런 다음 **구성 요소 만들기**.
1. 대화 상자에서 다음 속성 값을 입력한 후 다음을 클릭합니다.

   * 레이블: listchildren
   * 제목: 내 Listchildren 구성 요소
   * 설명: 내 Listchildren 구성 요소입니다.

1. [허용된 하위] 패널이 나타날 때까지 [다음]을 계속 클릭한 다음 [확인]을 클릭합니다.

#### 하위 목록 스크립트 만들기 {#creating-the-list-children-script}

listchildren 구성 요소에 대한 스크립트를 개발합니다.

1. CRXDE Lite에서 파일을 엽니다. `listchildren.jsp` 아래에 `/apps/mywebsite/components/listchildren`.
1. 기본 코드를 다음 코드로 바꿉니다.

   ```xml
   <%@include file="/libs/foundation/global.jsp"%><%
   %><%@ page import="java.util.Iterator,
            com.day.cq.wcm.api.PageFilter"%><%
        /* Create a Page object using the path of the current page */
         String listroot = properties.get("listroot", currentPage.getPath());
        Page rootPage = pageManager.getPage(listroot);
        /* iterate through the child pages and gather properties */
        if (rootPage != null) {
            Iterator<Page> children = rootPage.listChildren(new PageFilter(request));
            while (children.hasNext()) {
                Page child = children.next();
                String title = child.getTitle() == null ? child.getName() : child.getTitle();
                String date = child.getProperties().get("date","");
                %><div class="item">
                <a href="<%= child.getPath() %>.html"><b><%= title %></b></a>
                <span><%= date %></code><br>
                <%= child.getProperties().get("jcr:description","") %><br>
                </div><%
            }
        }
    %>
   ```

1. 변경 사항을 저장합니다.

#### 하위 목록 대화 상자 만들기 {#creating-the-list-children-dialog}

listchildren 구성 요소 속성을 구성하는 데 사용되는 대화 상자를 만듭니다.

1. listchildren 구성 요소 아래에 대화 상자 노드를 만듭니다.

   1. CRXDE Lite에서 `/apps/mywebsite/components/listchildren`노드 및 클릭 **만들기** > **대화 상자 만들기**.

   1. 대화 상자에서 다음 등록 정보 값을 입력하고 확인을 클릭합니다

      * **레이블**: `dialog`

      * **제목**: `Edit Component` 및 클릭 **확인**.

   ![screen_shot_2012-03-07at45818pm](assets/screen_shot_2012-03-07at45818pm.png)

   다음 속성을 사용합니다.

   ![screen_shot_2012-03-07at50415pm](assets/screen_shot_2012-03-07at50415pm.png)

1. 다음 항목 선택 `/apps/mywebsite/components/listchildren/dialog/items/items/tab1` 노드.
1. 속성 탭에서 값을 변경합니다. **제목** 다음으로 속성: `List Children`

   ![chlimage_1-42](assets/chlimage_1-42.png)

1. tab1 노드를 선택하고 만들기 > 노드 만들기를 클릭하고 다음 속성 값을 입력한 다음 확인을 클릭합니다.

   * 이름: 항목
   * 유형: cq:WidgetCollection

   ![screen_shot_2012-03-07at51018pm](assets/screen_shot_2012-03-07at51018pm.png)

1. 다음 속성 값을 사용하여 항목 노드 아래에 노드를 만듭니다.

   * 이름: listroot
   * 유형: cq:Widget

   ![screen_shot_2012-03-07at51031pm](assets/screen_shot_2012-03-07at51031pm.png)

1. listroot 노드의 속성을 추가하여 텍스트 필드로 구성합니다. 다음 표의 각 행은 속성을 나타냅니다. 완료되면 모두 저장 을 클릭합니다.

   | 이름 | 유형 | 값 |
   |---|---|---|
   | fieldLabel | 문자열 | 목록 루트의 경로 |
   | 이름 | 문자열 | ./listroot |
   | xtype | 문자열 | 텍스트 필드 |

   ![screen_shot_2012-03-07at51433pm](assets/screen_shot_2012-03-07at51433pm.png)

#### Contentpage 구성 요소에 목록 하위 포함 {#including-list-children-in-the-contentpage-component}

listchildren 구성 요소를 contentpage 구성 요소에 포함하려면 다음과 같이 진행합니다.

1. CRXDE Lite에서 파일을 엽니다. `left.jsp` 아래에 `/apps/mywebsite/components/contentpage` 다음 코드(4행)를 찾습니다.

   ```xml
   <div>newslist</div>
   ```

1. 해당 코드를 다음 코드로 바꿉니다.

   ```xml
   <cq:include path="newslist" resourceType="mywebsite/components/listchildren" />
   ```

1. 변경 사항을 저장합니다.

#### 페이지에서 목록 하위 보기 {#viewing-list-children-in-a-page}

이 구성 요소의 전체 작업을 보려면 제품 페이지를 확인하십시오.

* 상위 페이지(&quot;목록 루트의 경로&quot;)가 정의되지 않은 경우.
* 상위 페이지(&quot;목록 루트의 경로&quot;)가 정의된 경우.

1. 브라우저에서 제품 페이지를 다시 로드합니다. listchildren 구성 요소는 다음과 같이 표시됩니다.

   ![chlimage_1-43](assets/chlimage_1-43.png)

1. ![chlimage_1-44](assets/chlimage_1-44.png)

1. 목록 루트의 경로로 다음을 입력합니다. `/content/mywebsite/en`. 확인을 클릭합니다. 이제 페이지의 listchildren 구성 요소는 다음과 같습니다.

   ![chlimage_1-45](assets/chlimage_1-45.png)

### 로고 구성 요소 만들기 {#creating-the-logo-component}

회사 로고를 표시하고 사이트의 홈 페이지에 대한 링크를 제공하는 구성 요소를 만듭니다. 구성 요소에는 사이트 디자인(/etc/designs/mywebsite)에 속성 값을 저장할 수 있는 디자인 모드 대화 상자가 포함되어 있습니다.

* 속성 값은 디자인을 사용하는 페이지에 추가되는 구성 요소의 모든 인스턴스에 적용됩니다.
* 디자인을 사용하는 페이지에 있는 구성 요소의 인스턴스를 사용하여 속성을 구성할 수 있습니다.

디자인 모드 대화 상자에는 이미지와 링크 경로를 설정하는 속성이 포함되어 있습니다. 로고 구성 요소는 웹 사이트의 모든 페이지에서 왼쪽 상단에 배치됩니다.

작업을 마치면 다음과 같이 표시됩니다.

![chlimage_1-46](assets/chlimage_1-46.png)

>[!NOTE]
>
>Adobe Experience Manager은 더 많은 기능을 갖춘 로고 구성 요소( `/libs/foundation/components/logo`).

#### 로고 구성 요소 노드 만들기 {#creating-the-logo-component-node}

로고 구성 요소를 만들려면 다음 단계를 수행하십시오.

1. CRXDE Lite에서 /apps/mywebsite/components 를 마우스 오른쪽 버튼으로 클릭하고 다음을 선택합니다. **만들기**, 그런 다음 **구성 요소 만들기**.
1. 구성 요소 만들기 대화 상자에서 다음 속성 값을 입력하고 다음을 클릭합니다.

   * 레이블: `logo`.
   * 제목: `My Logo Component`.
   * 설명: `This is My Logo Component`.

1. 대화 상자의 최종 패널에 도달할 때까지 다음 을 클릭한 다음 을 클릭합니다 **확인**.

#### 로고 스크립트 만들기 {#creating-the-logo-script}

이 섹션에서는 홈 페이지에 대한 링크가 있는 로고 이미지를 표시하는 스크립트를 만드는 방법을 설명합니다.

1. CRXDE Lite에서 파일을 엽니다. `logo.jsp` 아래에 `/apps/mywebsite/components/logo`.
1. 다음 코드는 사이트 홈 페이지에 대한 링크를 만들고 로고 이미지에 대한 참조를 추가합니다. 코드 복사 대상 `logo.jsp`:

   ```xml
   <%@include file="/libs/foundation/global.jsp"%><%
   %><%@ page import="com.day.text.Text,
                      com.day.cq.wcm.foundation.Image,
                      com.day.cq.commons.Doctype" %><%
       /* obtain the path for home */
       long absParent = currentStyle.get("absParent", 2L);
       String home = Text.getAbsoluteParent(currentPage.getPath(), (int) absParent);
       /* obtain the image */
       Resource res = currentStyle.getDefiningResource("imageReference");
       if (res == null) {
           res = currentStyle.getDefiningResource("image");
       }
       /* if no image use text link, otherwise draw the image */
       %>
   <a href="<%= home %>.html"><%
       if (res == null) {
           %>Home<%
       } else {
           Image img = new Image(res);
           img.setItemName(Image.NN_FILE, "image");
           img.setItemName(Image.PN_REFERENCE, "imageReference");
           img.setSelector("img");
           img.setDoctype(Doctype.fromRequest(request));
           img.setAlt("Home");
           img.draw(out);
       }
       %></a>
   ```

1. 변경 사항을 저장합니다.

#### 로고 디자인 대화 상자 만들기 {#creating-the-logo-design-dialog}

디자인 모드에서 로고 구성 요소를 구성하는 대화 상자를 만듭니다. 디자인 모드 대화 상자 노드의 이름을 지정해야 합니다. `design_dialog`.

1. 로고 구성 요소 아래에 대화 상자 노드를 만듭니다.

   1. 마우스 오른쪽 단추 클릭 `/apps/mywebsite/components/logo` 노드 및 클릭 **만들기** > **대화 상자 만들기**.

   1. 다음 속성 값을 입력한 다음 [확인]을 클릭합니다.

      * **레이블:** `design_dialog`

      * **제목:** `Logo (Design)`

1. design_dialog 분기에서 tab1 노드를 마우스 오른쪽 버튼으로 클릭하고 삭제를 클릭합니다. 모두 저장을 클릭합니다.
1. 아래 `design_dialog/items/items`노드, 다음 이름의 노드 만들기 `img` 유형 `cq:Widget`. 다음 속성을 추가한 다음 모두 저장을 클릭합니다.

   | 이름 | 유형 | 값 |
   |---|---|---|
   | fileNameParameter | 문자열 | ./imageName |
   | fileReferenceParameter | 문자열 | ./imageReference |
   | 이름 | 문자열 | ./image |
   | 제목 | 문자열 | 이미지 |
   | xtype | 문자열 | html5smartimage |

   ![chlimage_1-47](assets/chlimage_1-47.png)

#### 로고 렌더링 스크립트 만들기 {#creating-the-logo-render-script}

로고 이미지를 검색하고 페이지에 작성하는 스크립트를 만듭니다.

1. 로고 구성 요소 노드를 마우스 오른쪽 버튼으로 클릭하고 만들기 > 파일 만들기 를 클릭하여 img.GET.java라는 스크립트 파일을 만듭니다.
1. 파일을 열고 다음 코드를 파일에 복사한 다음 모두 저장을 클릭합니다.

```java
package apps.mywebsite.components.logo;

import java.io.IOException;
import java.io.InputStream;

import javax.jcr.RepositoryException;
import javax.jcr.Property;
import javax.servlet.http.HttpServletResponse;

import com.day.cq.wcm.foundation.Image;
import com.day.cq.wcm.commons.RequestHelper;
import com.day.cq.wcm.commons.WCMUtils;
import com.day.cq.wcm.commons.AbstractImageServlet;
import com.day.cq.commons.SlingRepositoryException;
import com.day.image.Layer;
import org.apache.commons.io.IOUtils;
import org.apache.sling.api.SlingHttpServletRequest;
import org.apache.sling.api.SlingHttpServletResponse;
import org.apache.sling.api.resource.Resource;
import org.apache.sling.api.resource.ValueMap;
import org.apache.sling.api.servlets.SlingSafeMethodsServlet;

/**
 * Renders an image
 */
public class img_GET extends AbstractImageServlet {

    protected Layer createLayer(ImageContext c)
            throws RepositoryException, IOException {
        /* do not create the layer yet. handle everything later */
        return null;
    }

    protected void writeLayer(SlingHttpServletRequest req,
                              SlingHttpServletResponse resp,
                              ImageContext c, Layer layer)
            throws IOException, RepositoryException {

        Image image = new Image(c.resource);
        image.setItemName(Image.NN_FILE, "image");
        image.setItemName(Image.PN_REFERENCE, "imageReference");
        if (!image.hasContent()) {
            resp.sendError(HttpServletResponse.SC_NOT_FOUND);
            return;
        }
        /* get pure layer */
        layer = image.getLayer(false, false, false);

        /* do not re-encode layer, just spool */
        Property data = image.getData();
        InputStream in = data.getStream();
        resp.setContentLength((int) data.getLength());
        String contentType = image.getMimeType();
        if (contentType.equals("application/octet-stream")) {
            contentType=c.requestImageType;
        }
        resp.setContentType(contentType);
        IOUtils.copy(in, resp.getOutputStream());
        in.close();

        resp.flushBuffer();
    }
}
```

#### Contentpage 구성 요소에 로고 구성 요소 추가 {#adding-the-logo-component-to-the-contentpage-component}

1. CRXDE Lite에서 `left.jsp` 아래에 `/apps/mywebsite/components/contentpage file` 다음 코드 행을 찾습니다.

   ```xml
   <div>logo</div>
   ```

1. 해당 코드를 다음 코드 줄로 바꿉니다.

   ```xml
   <cq:include path="logo" resourceType="mywebsite/components/logo" />
   ```

1. 변경 사항을 저장합니다.
1. 브라우저에서 제품 페이지를 다시 로드합니다. 로고는 현재 기본 링크만 표시하지만 다음과 같이 표시됩니다.

   ![chlimage_1-48](assets/chlimage_1-48.png)

#### 페이지에서 로고 이미지 설정 {#setting-the-logo-image-in-a-page}

이 섹션에서는 디자인 모드 대화 상자를 사용하여 이미지를 로고로 설정하는 방법에 대해 설명합니다.

1. 브라우저에서 제품 페이지를 연 상태에서 Sidekick 하단의 디자인 단추를 클릭하여 디자인 모드로 전환합니다.

   ![오른쪽 사각형으로 표시된 디자인 단추.](do-not-localize/chlimage_1-1.png)

1. 로고 표시줄의 디자인에서 편집 을 클릭하여 대화 상자를 통해 로고 구성 요소의 설정을 편집합니다.
1. 대화 상자에서 이미지 탭의 패널을 클릭하고 mywebsite.zip 파일에서 추출한 logo.png 이미지를 찾은 다음 확인 을 클릭합니다.

   ![chlimage_1-49](assets/chlimage_1-49.png)

1. 편집 모드로 돌아가려면 Sidekick 제목 표시줄에서 삼각형을 클릭합니다.

   ![chlimage_1-3](assets/chlimage_1-3.jpeg)

1. CRXDE Lite에서 다음 노드로 이동하여 저장된 속성 값을 확인합니다.

   `/etc/designs/mywebsite/jcr:content/contentpage/logo`

### 이동 경로 구성 요소 포함 {#including-the-breadcrumb-component}

이 섹션에서는 기초 구성 요소 중 하나인 탐색 표시(트레일) 구성 요소를 포함합니다.

1. CRXDE Lite에서 `/apps/mywebsite/components/contentpage`, 파일을 엽니다. `center.jsp`, 및 바꾸기:

   ```java
   <div>trail</div>
   ```

   포함:

   ```xml
   <cq:include path="trail" resourceType="foundation/components/breadcrumb" />
   ```

1. 변경 사항을 저장합니다.
1. 브라우저에서 **제품 1** 페이지를 가리키도록 업데이트하는 중입니다. 트레일 구성 요소는 다음과 같습니다.

   ![chlimage_1-50](assets/chlimage_1-50.png)

### 제목 구성 요소 포함 {#including-the-title-component}

이 섹션에서는 기초 구성 요소 중 하나인 제목 구성 요소를 포함합니다.

1. CRXDE Lite에서 `/apps/mywebsite/components/contentpage`, 파일을 엽니다. `center.jsp`, 및 바꾸기:

   ```xml
   <div>title</div>
   ```

   포함:

   ```xml
   <cq:include path="title" resourceType="foundation/components/title" />
   ```

1. 변경 사항을 저장합니다.
1. 브라우저에서 제품 페이지를 다시 로드합니다. 제목 구성 요소는 다음과 같습니다.

   ![chlimage_1-51](assets/chlimage_1-51.png)

   **참고**: 편집 모드에서 다른 제목 과 유형/크기를 설정할 수 있습니다.

### 단락 시스템 구성 요소 포함 {#including-the-paragraph-system-component}

단락 시스템(parsys)은 단락 목록을 관리하기 때문에 웹 사이트에서 중요한 부분입니다. 이를 통해 작성자는 페이지에 단락 구성 요소를 추가할 수 있으며 구조를 제공합니다.

parsys 구성 요소(foundation 구성 요소 중 하나)를 contentpage 구성 요소에 추가합니다.

1. CRXDE Lite에서 `/apps/mywebsite/components/contentpage`, 파일을 엽니다. `center.jsp`를 클릭하고 다음 코드 행을 찾습니다.

   ```xml
   <div>parsys</div>
   ```

1. 해당 코드 행을 다음 코드로 바꾼 다음 변경 사항을 저장합니다.

   ```xml
   <cq:include path="par" resourceType="foundation/components/parsys" />
   ```

1. 브라우저에서 제품 페이지를 새로 고칩니다. 이제 parsys 구성 요소가 있으며 이는 다음과 같이 표시됩니다.

   ![chlimage_1-52](assets/chlimage_1-52.png)

### 이미지 구성 요소 만들기 {#creating-the-image-component}

단락 시스템에 이미지를 표시하는 구성 요소를 만듭니다. 시간을 절약하기 위해 이미지 구성 요소는 일부 속성 변경 사항과 함께 로고 구성 요소의 사본으로 만들어집니다.

>[!NOTE]
>
>Adobe Experience Manager은 보다 모든 기능을 갖춘 이미지 구성 요소( `/libs/foundation/components/image`).

#### 이미지 구성 요소 만들기 {#creating-the-image-component-1}

1. 마우스 오른쪽 단추 클릭 `/apps/mywebsite/components/logo` 노드를 클릭하고 복사를 클릭합니다.
1. 마우스 오른쪽 단추 클릭 `/apps/mywebsite/components` 노드를 클릭하고 붙여넣기를 클릭합니다.
1. 마우스 오른쪽 단추 클릭 `Copy of logo` 노드를 클릭하고 이름 바꾸기를 클릭한 다음 기존 텍스트와 유형을 삭제합니다. `image`.

1. 다음 항목 선택 `image` 구성 요소 노드를 클릭하고 다음 속성 값을 변경합니다.

   * `jcr:title:` 내 이미지 구성 요소.
   * `jcr:description`: 내 이미지 구성 요소입니다.

1. 에 속성 추가 `image` 다음 속성 값이 있는 노드:

   * 이름: componentGroup
   * 유형: 문자열
   * 값: 내 웹 사이트

1. 아래 `image` 노드, 이름 바꾸기 `design_dialog` 노드 대상 `dialog`.

1. 이름 바꾸기 `logo.jsp` 끝 `image.jsp.`

1. GET img.domain.java를 열고 패키지를 다음으로 변경 `apps.mywebsite.components.image`.

![chlimage_1-53](assets/chlimage_1-53.png)

#### 이미지 스크립트 만들기 {#creating-the-image-script}

이 섹션에서는 이미지 스크립트를 만드는 방법을 설명합니다.

1. 열기 `/apps/mywebsite/components/image/` `image.jsp`
1. 기존 코드를 다음 코드로 바꾼 다음 변경 사항을 저장합니다.

   ```xml
   <%@include file="/libs/foundation/global.jsp"%><%
   %><%@ page import="com.day.cq.commons.Doctype,
                       com.day.cq.wcm.foundation.Image,
                       com.day.cq.wcm.api.components.DropTarget,
                       com.day.cq.wcm.api.components.EditConfig,
                       com.day.cq.wcm.commons.WCMUtils" %><%
    /* global.jsp provides access to the current resource through the resource object */
           Image img = new Image(resource);
           img.setItemName(Image.NN_FILE, "image");
           img.setItemName(Image.PN_REFERENCE, "imageReference");
           img.setSelector("img");
           img.setDoctype(Doctype.fromRequest(request));
           img.setAlt("Home");
           img.draw(out); %>
   ```

1. 변경 사항을 저장합니다.

#### 이미지 cq:editConfig 노드 만들기 {#creating-the-image-cq-editconfig-node}

다음 `cq:editConfig` 노드 유형을 사용하면 속성을 편집할 때 구성 요소의 특정 동작을 구성할 수 있습니다.

이 섹션에서는 cq:editConfig 노드를 사용하여 콘텐츠 파인더의 자산을 이미지 구성 요소로 끌 수 있습니다.

1. CRXDE Lite 시 /apps/mywebsite/components/image 노드 아래에 다음과 같이 노드를 만듭니다.

   * 이름: cq:editConfig.
   * 유형: cq:EditConfig.

1. cq:editConfig 노드 아래에 다음과 같이 노드를 만듭니다.

   * 이름: cq:dropTargets
   * 유형: cq:DropTargetConfig.

1. cq:dropTargets 노드 아래에서 다음과 같이 노드를 만듭니다.

   * 이름: 이미지
   * 유형: nt:unstructured.

1. CRXDE에서 속성을 다음과 같이 설정합니다.

| 이름 | 유형 | 값 |
|---|---|---|
| 동의 | 문자열 | image/(gif | jpeg | png) |
| 그룹 | 문자열 | 미디어 |
| propertyName | 문자열 | ./imageReference |

![chlimage_1-54](assets/chlimage_1-54.png)

#### 아이콘 추가 {#adding-the-icon}

이 섹션에서는 Sidekick에 나열될 때 이미지 구성 요소 옆에 표시되는 아이콘을 추가합니다.

1. CRXDE Lite에서 파일을 마우스 오른쪽 단추로 클릭합니다 `/libs/foundation/components/image/icon.png` 및 선택 **알았다.**
1. 노드를 마우스 오른쪽 버튼으로 클릭합니다. `/apps/mywebsite/components/image` 및 클릭 **붙여넣기**&#x200B;을 클릭한 다음 을 클릭합니다 **모두 저장**.

#### 이미지 구성 요소 사용 {#using-the-image-component}

이 섹션에서는 **제품** 페이지를 만들고 이미지 구성 요소를 단락 시스템에 추가합니다.

1. 브라우저에서 **제품** 페이지를 가리키도록 업데이트하는 중입니다.
1. Sidekick에서 **디자인 모드** 아이콘.
1. 편집(Edit) 단추를 눌러 파트의 설계(Design) 대화상자를 편집합니다.
1. 대화 상자에서 **허용된 구성 요소** 이 표시됩니다. 다음으로 이동 **내 웹 사이트**&#x200B;를 선택하고 **내 이미지 구성 요소**, 및 클릭 **좋아.**
1. 다음으로 돌아가기: **편집 모드입니다.**
1. parsys 프레임을 두 번 클릭합니다(켜기 **여기에 구성 요소 또는 자산을 끌어 놓으십시오.**). 다음 **새 구성 요소 삽입** 및 **Sidekick** 선택기는 다음과 같습니다.

   ![chlimage_1-4](assets/chlimage_1-4.jpeg)

### 도구 모음 구성 요소 포함 {#including-the-toolbar-component}

이 단원에서는 기초 구성 요소 중 하나인 도구 모음 구성 요소를 포함합니다.

편집 모드와 디자인 모드에는 몇 가지 옵션이 있습니다.

1. CRXDE Lite에서 다음으로 이동 `/apps/mywebsite/components/contentpage`를 열고 `body.jsp` 파일을 참조하고 다음 코드를 찾습니다.

   ```java
   <div class="toolbar">toolbar</div>
   ```

1. 해당 코드를 다음 코드로 바꾸고 변경 사항을 저장합니다.

   ```java
   <cq:include path="toolbar" resourceType="foundation/components/toolbar"/>
   ```

1. AEM 웹 사이트 페이지의 폴더 트리에서 웹 사이트/내 웹 사이트/영어를 선택한 다음 새로 만들기 > 새 페이지를 클릭합니다. 다음 속성 값을 지정하고 [만들기]를 클릭합니다.

   * 제목: 도구 모음
   * 내 웹 사이트 컨텐츠 페이지 템플릿 선택

1. 페이지 목록에서 도구 모음 페이지를 마우스 오른쪽 단추로 클릭하고 속성을 클릭합니다. 탐색에서 숨기기를 선택하고 확인을 클릭합니다.

   탐색 숨기기 옵션을 사용하면 topnav 및 listchildren과 같은 탐색 구성 요소에 페이지가 표시되지 않습니다.

1. 도구 모음에서 다음 페이지를 만듭니다.

   * 연락처
   * 피드백
   * 로그인
   * 검색

1. 브라우저에서 제품 페이지를 다시 로드합니다. 이는 다음과 같습니다.

   ![chlimage_1-55](assets/chlimage_1-55.png)

### 검색 구성 요소 만들기 {#creating-the-search-component}

이 섹션에서는 웹 사이트에서 컨텐츠를 검색하는 구성 요소를 만듭니다. 이 검색 구성 요소는 모든 페이지의 단락 시스템(예: 특수 검색 결과 페이지)에 배치할 수 있습니다.

완료되면 검색 입력란은 다음과 같이 표시됩니다. **영어** 페이지:

![chlimage_1-56](assets/chlimage_1-56.png)

#### 검색 구성 요소 만들기 {#creating-the-search-component-1}

1. CRXDE Lite에서 마우스 오른쪽 단추 클릭 `/apps/mywebsite/components`, 선택 **만들기**, 그런 다음 **구성 요소 만들기**.
1. 대화 상자를 사용하여 구성 요소를 구성합니다.

   1. 첫 번째 패널에서 다음 속성 값을 지정합니다.

      * 레이블: 검색
      * 제목: 내 검색 구성 요소
      * 설명: 내 검색 구성 요소입니다
      * 그룹: 내 웹 사이트

   1. 다음 을 클릭한 후 다음 을 다시 클릭합니다.
   1. [허용된 상위] 패널에서 + 단추를 클릭하고 을 입력합니다 `*/parsys`.
   1. 다음 을 클릭한 다음 확인 을 클릭합니다.

1. 모두 저장을 클릭합니다.
1. 다음 노드를 복사하여 apps/mywebsite/components/search 노드에 붙여넣습니다.

   * `/libs/foundation/components/search/dialog`
   * &quot; `/libs/foundation/components/search/i18n`

   * `/libs/foundation/components/search/icon.png`

1. 모두 저장을 클릭합니다.

#### 검색 스크립트 만들기 {#creating-the-search-script}

이 섹션에서는 검색 스크립트를 만드는 방법을 설명합니다.

1. 를 엽니다. `/apps/mywebsite/components/search/search.jsp` 파일.
1. 다음 코드를에 복사합니다. `search.jsp`:

   ```java
   <%@ page import="com.day.cq.wcm.foundation.Search,com.day.cq.tagging.TagManager" %>
   <%@include file="/libs/foundation/global.jsp" %><%
   %><cq:setContentBundle/><%
       Search search = new Search(slingRequest);
   
       String searchIn = (String) properties.get("searchIn");
       String requestSearchPath = request.getParameter("path");
       if (searchIn != null) {
           /* only allow the "path" request parameter to be used if it
            is within the searchIn path configured */
           if (requestSearchPath != null && requestSearchPath.startsWith(searchIn)) {
               search.setSearchIn(requestSearchPath);
           } else {
               search.setSearchIn(searchIn);
           }
       } else if (requestSearchPath != null) {
           search.setSearchIn(requestSearchPath);
       }
   
       pageContext.setAttribute("search", search);
       TagManager tm = resourceResolver.adaptTo(TagManager.class);
   %><c:set var="trends" value="${search.trends}"/><%
   %><center>
     <form action="${currentPage.path}.html">
       <input size="41" maxlength="2048" name="q" value="${fn:escapeXml(search.query)}"/>
       <input value="<fmt:message key="searchButtonText"/>" type="submit" />
     </form>
   </center>
   <br/>
   <c:set var="result" value="${search.result}"/>
   <c:choose>
     <c:when test="${empty result && empty search.query}">
     </c:when>
     <c:when test="${empty result.hits}">
       <c:if test="${result.spellcheck != null}">
         <p><fmt:message key="spellcheckText"/> <a href="<c:url value="${currentPage.path}.html"><c:param name="q" value="${result.spellcheck}"/></c:url>"><b><c:out value="${result.spellcheck}"/></b></a></p>
       </c:if>
       <fmt:message key="noResultsText">
         <fmt:param value="${fn:escapeXml(search.query)}"/>
       </fmt:message>
     </c:when>
     <c:otherwise>
       <p class="searchmeta">Results ${result.startIndex + 1} - ${result.startIndex + fn:length(result.hits)} of ${result.totalMatches} for <b>${fn:escapeXml(search.query)}</b>. (${result.executionTime} seconds)</p>
      <br/>
   
     <div class="searchresults">
       <div class="results">
         <c:forEach var="hit" items="${result.hits}" varStatus="status">
           <div class="hit">
           <a href="${hit.URL}">${hit.title}</a>
           <div class="excerpt">${hit.excerpt}</div>
          <div class="hiturl"> ${hit.URL}<c:if test="${!empty hit.properties['cq:lastModified']}"> - <c:catch><fmt:formatDate value="${hit.properties['cq:lastModified'].time}" dateStyle="medium"/></c:catch></c:if> - <a href="${hit.similarURL}"><fmt:message key="similarPagesText"/></a>
           </div></div>
         </c:forEach>
       </div>
         <br/>
   
        <div class="searchRight">
             <c:if test="${fn:length(trends.queries) > 0}">
                 <p><fmt:message key="searchTrendsText"/></p>
                 <div class="searchTrends">
                     <c:forEach var="query" items="${trends.queries}">
                         <a href="<c:url value="${currentPage.path}.html"><c:param name="q" value="${query.query}"/></c:url>"><span style="font-size:${query.size}px"><c:out value="${query.query}"/></code></a>
                     </c:forEach>
                 </div>
             </c:if>
             <c:if test="${result.facets.languages.containsHit}">
                 <p>Languages</p>
                 <c:forEach var="bucket" items="${result.facets.languages.buckets}">
                     <c:set var="bucketValue" value="${bucket.value}"/>
                     <c:set var="label" value='<%= new java.util.Locale((String) pageContext.getAttribute("bucketValue")).getDisplayLanguage(request.getLocale()) %>'/>
                     <c:choose>
                         <c:when test="${param.language != null}">${label} (${bucket.count}) - <a href="<cq:requestURL><cq:removeParam name="language"/></cq:requestURL>">remove filter</a></c:when>
                         <c:otherwise><a title="filter results" href="<cq:requestURL><cq:addParam name="language" value="${bucket.value}"/></cq:requestURL>">${label} (${bucket.count})</a></c:otherwise>
                     </c:choose><br/>
                 </c:forEach>
             </c:if>
             <c:if test="${result.facets.tags.containsHit}">
                 <p>Tags</p>
                 <c:forEach var="bucket" items="${result.facets.tags.buckets}">
                     <c:set var="bucketValue" value="${bucket.value}"/>
                     <c:set var="tag" value="<%= tm.resolve((String) pageContext.getAttribute("bucketValue")) %>"/>
                     <c:if test="${tag != null}">
                         <c:set var="label" value="${tag.title}"/>
                         <c:choose>
                             <c:when test="<%= request.getParameter("tag") != null && java.util.Arrays.asList(request.getParameterValues("tag")).contains(pageContext.getAttribute("bucketValue")) %>">${label} (${bucket.count}) - <a href="<cq:requestURL><cq:removeParam name="tag" value="${bucket.value}"/></cq:requestURL>">remove filter</a></c:when>
                             <c:otherwise><a title="filter results" href="<cq:requestURL><cq:addParam name="tag" value="${bucket.value}"/></cq:requestURL>">${label} (${bucket.count})</a></c:otherwise>
                         </c:choose><br/>
                     </c:if>
                 </c:forEach>
             </c:if>
             <c:if test="${result.facets.mimeTypes.containsHit}">
                 <jsp:useBean id="fileTypes" class="com.day.cq.wcm.foundation.FileTypes"/>
                 <p>File types</p>
                 <c:forEach var="bucket" items="${result.facets.mimeTypes.buckets}">
                     <c:set var="bucketValue" value="${bucket.value}"/>
                     <c:set var="label" value="${fileTypes[bucket.value]}"/>
                     <c:choose>
                         <c:when test="<%= request.getParameter("mimeType") != null && java.util.Arrays.asList(request.getParameterValues("mimeType")).contains(pageContext.getAttribute("bucketValue")) %>">${label} (${bucket.count}) - <a href="<cq:requestURL><cq:removeParam name="mimeType" value="${bucket.value}"/></cq:requestURL>">remove filter</a></c:when>
                         <c:otherwise><a title="filter results" href="<cq:requestURL><cq:addParam name="mimeType" value="${bucket.value}"/></cq:requestURL>">${label} (${bucket.count})</a></c:otherwise>
                     </c:choose><br/>
                 </c:forEach>
             </c:if>
             <c:if test="${result.facets.lastModified.containsHit}">
                 <p>Last Modified</p>
                 <c:forEach var="bucket" items="${result.facets.lastModified.buckets}">
                     <c:choose>
                         <c:when test="${param.from == bucket.from && param.to == bucket.to}">${bucket.value} (${bucket.count}) - <a href="<cq:requestURL><cq:removeParam name="from"/><cq:removeParam name="to"/></cq:requestURL>">remove filter</a></c:when>
                         <c:otherwise><a title="filter results" href="<cq:requestURL><cq:removeParam name="from"/><cq:removeParam name="to"/><c:if test="${bucket.from != null}"><cq:addParam name="from" value="${bucket.from}"/></c:if><c:if test="${bucket.to != null}"><cq:addParam name="to" value="${bucket.to}"/></c:if></cq:requestURL>">${bucket.value} (${bucket.count})</a></c:otherwise>
                     </c:choose><br/>
                 </c:forEach>
             </c:if>
   
         <c:if test="${fn:length(search.relatedQueries) > 0}">
   
          <br/><br/><div class="related">
           <fmt:message key="relatedSearchesText"/>
           <c:forEach var="rq" items="${search.relatedQueries}">
               <a href="${currentPage.path}.html?q=${rq}"><c:out value="${rq}"/></a>
           </c:forEach></div>
         </c:if>
         </div>
   
         <c:if test="${fn:length(result.resultPages) > 1}">
           <div class="pagination">
               <fmt:message key="resultPagesText"/>
           <c:if test="${result.previousPage != null}">
             <a href="${result.previousPage.URL}"><fmt:message key="previousText"/></a>
           </c:if>
           <c:forEach var="page" items="${result.resultPages}">
             <c:choose>
               <c:when test="${page.currentPage}">${page.index + 1}</c:when>
               <c:otherwise>
                 <a href="${page.URL}">${page.index + 1}</a>
               </c:otherwise>
             </c:choose>
           </c:forEach>
           <c:if test="${result.nextPage != null}">
             <a href="${result.nextPage.URL}"><fmt:message key="nextText"/></a>
           </c:if>
           </div>
         </c:if>
         </div>
   
     </c:otherwise>
   </c:choose>
   ```

1. 변경 사항을 저장합니다.

#### Contentpage 구성 요소에 검색 상자 포함 {#including-a-search-box-in-the-contentpage-component}

콘텐츠 페이지의 왼쪽 섹션에 검색 입력 상자를 포함하려면 다음과 같이 진행합니다.

1. CRXDE Lite에서 파일을 엽니다. `left.jsp` 아래에 `/apps/mywebsite/components/contentpage` 다음 코드(2행)를 찾습니다.

   ```xml
   %><div class="left">
   ```

1. 다음 코드를 삽입합니다 **다음 이전** 해당 줄:

   ```java
   %><%@ page import="com.day.text.Text"%><%
   %><% String docroot = currentDesign.getPath();
   String home = Text.getAbsoluteParent(currentPage.getPath(), 2);%><%
   ```

1. 다음 코드 행을 찾습니다.

   ```xml
   <div>search</div>
   ```

1. 해당 코드를 다음 코드로 바꾸고 변경 사항을 저장합니다.

   ```java
   <div class="form_1">
        <form class="geo" action="<%= home %>/toolbar/search.html" id="form" >
             <p>
                  <input class="geo" type="text" name="q"><br>
                  <a href="<%= home %>/toolbar/search.html" class="link_1">advanced search</a>
             </p>
        </form>
   </div>
   ```

1. 브라우저에서 제품 페이지를 다시 로드합니다. 검색 구성 요소는 다음과 같습니다.

   ![chlimage_1-57](assets/chlimage_1-57.png)

#### 검색 페이지에 검색 구성 요소 포함 {#including-the-search-component-in-the-search-page}

이 섹션에서는 검색 구성 요소를 단락 시스템에 추가합니다.

1. 브라우저에서 검색 페이지를 엽니다.
1. Sidekick에서 디자인 모드 아이콘을 클릭합니다.
1. 검색 제목 아래의 조각 블록 디자인에서 편집 을 클릭합니다.
1. 대화 상자에서 아래로 스크롤하여  **내 웹 사이트** 그룹, 선택 **내 검색 구성 요소**, 및 클릭 **확인**.
1. Sidekick 시 삼각형을 클릭하여 편집 모드로 돌아갑니다.
1. Sidekick에서 내 검색 구성 요소를 parsys 프레임으로 드래그합니다. 이는 다음과 같습니다.

   ![chlimage_1-58](assets/chlimage_1-58.png)

1. 제품 페이지로 이동합니다. 입력란에서 고객을 검색하고 Enter 키를 누릅니다. 검색 페이지로 리디렉션됩니다. 미리 보기 모드로 전환: 출력은 다음과 유사한 형식입니다.

   ![chlimage_1-59](assets/chlimage_1-59.png)

### Iparsys 구성 요소 포함 {#including-the-iparsys-component}

이 섹션에서는 기초 구성 요소 중 하나인 상속 단락 시스템(iparsys) 구성 요소를 포함합니다. 이 구성 요소를 사용하면 상위 페이지에 단락 구조를 만들고 하위 페이지에 단락이 상속되도록 할 수 있습니다.

이 구성 요소의 경우 편집 모드와 디자인 모드 모두에서 여러 매개 변수를 설정할 수 있습니다.

1. CRXDE Lite에서 다음으로 이동 `/apps/mywebsite/components/contentpage`, 파일을 엽니다. `right.jsp`, 및 바꾸기:

   ```java
   <div>iparsys</div>
   ```

   포함:

   ```java
   <cq:include path="rightpar" resourceType="foundation/components/iparsys" />
   ```

1. 변경 사항을 저장합니다.
1. 브라우저에서 ** 제품** 페이지를 다시 로드합니다. 전체 페이지는 다음과 같습니다.

   ![chlimage_1-5](assets/chlimage_1-5.jpeg)
