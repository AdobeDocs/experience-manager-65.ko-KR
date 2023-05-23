---
title: 샌드박스 애플리케이션 개발
seo-title: Develop Sandbox Application
description: 기초 스크립트를 사용한 애플리케이션 개발
seo-description: Develop application using foundation scripts
uuid: 572f68cd-9ecb-4b43-a7f8-4aa8feb6c64e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 910229a3-38b1-44f1-9c09-55f8fd6cbb1d
exl-id: 7ac0056c-a742-49f4-8312-2cf90ab9f23a
source-git-commit: 1d334c42088342954feb34f6179dc5b134f81bb8
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 5%

---

# 샌드박스 애플리케이션 개발  {#develop-sandbox-application}

이 섹션에서 템플릿을에 설정했으므로 [초기 애플리케이션](initial-app.md) 섹션에 설정된 초기 페이지 [초기 컨텐츠](initial-content.md) 섹션에서, 커뮤니티 구성 요소로 작성할 수 있는 기능을 포함하여 기초 스크립트를 사용하여 응용 프로그램을 개발할 수 있습니다. 이 섹션이 끝나면 웹 사이트가 작동합니다.

## Foundation 페이지 스크립트 사용 {#using-foundation-page-scripts}

playpage 템플릿을 렌더링하는 구성 요소가 추가되었을 때 생성된 기본 스크립트가 기본 페이지의 head.jsp 및 local body.jsp를 포함하도록 수정되었습니다.

### 슈퍼 리소스 유형 {#super-resource-type}

첫 번째 단계는 리소스 수퍼 유형 속성을 `/apps/an-scf-sandbox/components/playpage` 수퍼 유형의 스크립트와 속성을 상속하도록 노드를 지정합니다.

CRXDE Lite 사용:

1. 노드 선택 `/apps/an-scf-sandbox/components/playpage`.
1. 속성 탭에서 다음 값이 있는 새 속성을 입력합니다.

   이름: `sling:resourceSuperType`

   유형: `String`

   값: `foundation/components/page`

1. 녹색 클릭 **[!UICONTROL +추가]** 단추를 클릭합니다.
1. 클릭 **[!UICONTROL 모두 저장]**.

   ![페이지-스크립트](assets/page-script.png)

### 헤드 및 본문 스크립트 {#head-and-body-scripts}

1. 위치 **CRXDE Lite** 탐색기 창에서 다음 위치로 이동 `/apps/an-scf-sandbox/components/playpage` 파일을 두 번 클릭합니다. `playpage.jsp` 을 클릭하여 편집 창에서 엽니다.

   `/apps/an-scf-sandbox/components/playpage/playpage.jsp`

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

1. 열기/닫기 스크립트 태그를 알고 의 헤드 및 신체 부분에 대한 스크립트 포함 항목으로 &quot; // TODO ...&quot;를 바꿉니다. &lt;html>.

   의 슈퍼타입으로 `foundation/components/page`, 동일한 폴더에 정의되지 않은 모든 스크립트는 의 스크립트로 확인됩니다. `/apps/foundation/components/page` 폴더(있는 경우), 기타 를 의 스크립트에 `/libs/foundation/components/page` 폴더를 삭제합니다.

   `/apps/an-scf-sandbox/components/playpage/playpage.jsp`

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

1. 기본 스크립트 `head.jsp` 오버레이할 필요가 없지만 foundation 스크립트입니다. `body.jsp` 은(는) 비어 있습니다.

   작성을 위해 설정하려면 오버레이하십시오 `body.jsp` 로컬 스크립트를 사용하고 본문에 단락 시스템(parsys)을 포함합니다.

   1. 다음으로 이동 `/apps/an-scf-sandbox/components`.
   1. 다음 항목 선택 `playpage` 노드.
   1. 마우스 오른쪽 단추를 클릭하고 선택 `Create > Create File...`

      * 이름: **body.jsp**
   1. 클릭 **[!UICONTROL 모두 저장]**.

   열기 `/apps/an-scf-sandbox/components/playpage/body.jsp` 을 클릭하고 다음 텍스트에 붙여넣습니다.

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

1. 클릭 **[!UICONTROL 모두 저장]**.

**편집 모드의 브라우저에서 페이지 보기:**

* 표준 UI: `http://localhost:4502/editor.html/content/an-scf-sandbox/en/play.html`

머리글만 보아서는 안됩니다 **커뮤니티 재생**, 페이지 콘텐츠 편집을 위한 UI도 포함됩니다.

자산/구성 요소 사이드 패널은 사이드 패널이 모두 열려 있는 상태로 전환되고 창이 사이드 컨텐츠와 페이지 컨텐츠가 모두 표시될 수 있을 만큼 넓으면 표시됩니다.

![페이지 보기](assets/view-page.png)

* 클래식 UI: `http://localhost:4502/cf#/content/an-scf-sandbox/en/play.html`

다음은 컨텐츠 파인더(cf)와 함께 포함하여 재생 페이지가 클래식 UI에 표시되는 방법입니다.

![play-page-view](assets/play-page-view.png)

## 커뮤니티 구성 요소 {#communities-components}

작성을 위해 Communities 구성 요소를 활성화하려면 다음 지침에 따라 시작합니다.

* [커뮤니티 구성 요소 액세스](basics.md#accessing-communities-components)

이 샌드박스에서는 다음 내용으로 시작합니다. **커뮤니티** 구성 요소(상자를 선택하여 활성화):

* 댓글
* 포럼
* 등급
* 리뷰
* 리뷰 요약(표시)
* 투표

또한 을(를) 선택합니다 **[!UICONTROL 일반]** 구성 요소(예: )

* 이미지
* 표
* 텍스트
* 제목 (Foundation)

>[!NOTE]
>
>페이지 부분에 대해 활성화된 구성 요소는 의 값으로 저장소에 저장됩니다. `components` 의 속성
>
>`/etc/designs/an-scf-sandbox/jcr:content/playpage/par` 노드.

## 랜딩 페이지 {#landing-page}

다국어 환경에서 루트 페이지에는 클라이언트의 요청을 구문 분석하여 기본 언어를 결정하는 스크립트가 포함됩니다.

이 간단한 예에서 루트 페이지는 영어 페이지로 리디렉션하도록 정적으로 설정되어 있으며, 향후 재생 페이지 링크가 있는 기본 랜딩 페이지로 개발될 수 있습니다.

브라우저 URL을 루트 페이지로 변경합니다. `http://localhost:4502/editor.html/content/an-scf-sandbox.html`

* 페이지 정보 아이콘 선택
* 선택 **[!UICONTROL 속성 열기]**
* 고급 탭에서

   * 리디렉션 항목의 경우 **[!UICONTROL 웹 사이트]** > **[!UICONTROL SCF 샌드박스 사이트]** > **[!UICONTROL SCF 샌드박스]**
   * **[!UICONTROL 확인]**&#x200B;을 클릭합니다

* **[!UICONTROL 확인]**&#x200B;을 클릭합니다

사이트가 게시되면 게시 인스턴스의 루트 페이지를 탐색하면 영어 페이지로 리디렉션됩니다.

커뮤니티 SCF 구성 요소로 재생하기 전 마지막 단계는 클라이언트 라이브러리 폴더(clientlibs)를 추가하는 것입니다.... [Clienlibs 추가](add-clientlibs.md)
