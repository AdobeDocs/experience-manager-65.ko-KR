---
title: 샌드박스 애플리케이션 개발
description: 기초 스크립트를 사용하고 커뮤니티 구성 요소로 작성을 활성화하는 기능이 포함된 샌드박스 애플리케이션을 개발하는 방법에 대해 알아봅니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 7ac0056c-a742-49f4-8312-2cf90ab9f23a
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 4%

---

# 샌드박스 애플리케이션 개발  {#develop-sandbox-application}

이 단원에서는 [초기 응용 프로그램](initial-app.md) 섹션에 템플릿을 설정하고 [초기 콘텐츠](initial-content.md) 섹션에 초기 페이지를 설정했으므로 응용 프로그램을 개발할 수 있습니다. 커뮤니티 구성 요소로 작성할 수 있는 기능을 포함하는 기초 스크립트를 사용하면 됩니다. 이 섹션의 끝에는 완전한 기능을 갖춘 웹 사이트가 있습니다.

## Foundation 페이지 스크립트 사용 {#using-foundation-page-scripts}

playpage 템플릿을 렌더링하는 구성 요소가 추가되었을 때 생성된 기본 스크립트가 기본 페이지의 head.jsp 및 local body.jsp를 포함하도록 수정되었습니다.

### 슈퍼 리소스 유형 {#super-resource-type}

첫 번째 단계는 `/apps/an-scf-sandbox/components/playpage` 노드에 리소스 수퍼 유형 속성을 추가하여 수퍼 유형의 스크립트와 속성을 상속하도록 하는 것입니다.

CRXDE Lite 사용:

1. `/apps/an-scf-sandbox/components/playpage` 노드를 선택하십시오.
1. 속성 탭에서 다음 값이 있는 새 속성을 입력합니다.

   이름: `sling:resourceSuperType`

   유형: `String`

   값: `foundation/components/page`

1. 녹색 **[!UICONTROL +추가]** 단추를 클릭합니다.
1. **[!UICONTROL 모두 저장]**&#x200B;을 클릭합니다.

   ![페이지-스크립트](assets/page-script.png)

### 헤드 및 본문 스크립트 {#head-and-body-scripts}

1. **CRXDE Lite** 탐색기 창에서 `/apps/an-scf-sandbox/components/playpage`(으)로 이동한 다음 `playpage.jsp` 파일을 두 번 클릭하여 편집 창에서 엽니다.

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

1. 열기/닫기 스크립트 태그를 인식하고 &quot; // TODO ...&quot;를 &lt;html>의 헤드 및 본문 부분에 대한 `includes` 스크립트로 바꾸십시오.

   수퍼 유형이 `foundation/components/page`인 경우, 이 동일한 폴더에 정의되지 않은 모든 스크립트는 `/apps/foundation/components/page` 폴더의 스크립트로 확인되거나(있는 경우) `/libs/foundation/components/page` 폴더의 스크립트로 확인됩니다.

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

1. Foundation 스크립트 `head.jsp`을(를) 오버레이할 필요는 없지만 Foundation 스크립트 `body.jsp`이(가) 비어 있습니다.

   작성을 위해 설정하려면 로컬 스크립트로 `body.jsp`을(를) 오버레이하고 본문에 단락 시스템(parsys)을 포함하십시오.

   1. 다음으로 이동 `/apps/an-scf-sandbox/components`.
   1. `playpage` 노드를 선택하십시오.
   1. 마우스 오른쪽 단추를 클릭하고 `Create > Create File...` 선택

      * 이름: **body.jsp**

   1. **[!UICONTROL 모두 저장]**&#x200B;을 클릭합니다.

   `/apps/an-scf-sandbox/components/playpage/body.jsp`을(를) 열고 다음 텍스트에 붙여 넣습니다.

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

1. **[!UICONTROL 모두 저장]**&#x200B;을 클릭합니다.

**편집 모드로 브라우저에서 페이지 보기:**

* 표준 UI: `http://localhost:4502/editor.html/content/an-scf-sandbox/en/play.html`

제목 **커뮤니티 재생**&#x200B;뿐만 아니라 페이지 콘텐츠 편집을 위한 UI도 표시되어야 합니다.

Assets/구성 요소 사이드 패널은 사이드 패널이 모두 열려 있는 상태로 전환되고 창이 사이드 컨텐츠와 페이지 컨텐츠가 모두 표시될 수 있을 만큼 넓으면 표시됩니다.

![페이지 보기](assets/view-page.png)

* 클래식 UI: `http://localhost:4502/cf#/content/an-scf-sandbox/en/play.html`

다음은 컨텐츠 파인더(cf)와 함께 포함하여 재생 페이지가 클래식 UI에 표시되는 방법입니다.

![play-page-view](assets/play-page-view.png)

## 커뮤니티 구성 요소 {#communities-components}

작성을 위해 Communities 구성 요소를 활성화하려면 다음 지침에 따라 시작합니다.

* [커뮤니티 구성 요소 액세스](basics.md#accessing-communities-components)

이 샌드박스에서는 다음 **Communities** 구성 요소로 시작합니다(상자를 선택하여 사용).

* 댓글
* 포럼
* 등급
* 리뷰
* 리뷰 요약(표시)
* 투표

또한 다음과 같은 **[!UICONTROL 일반]** 구성 요소를 선택합니다.

* 이미지
* 표
* 텍스트
* 제목(Foundation)

>[!NOTE]
>
>페이지 부분에 대해 활성화된 구성 요소는 저장소의 `components` 속성 값으로 저장소에 저장됩니다.
>
>`/etc/designs/an-scf-sandbox/jcr:content/playpage/par` 노드입니다.

## 랜딩 페이지 {#landing-page}

다국어 환경에서 루트 페이지에는 클라이언트의 요청을 구문 분석하여 기본 언어를 결정하는 스크립트가 포함됩니다.

이 예제에서 루트 페이지는 영어 페이지로 리디렉션하도록 정적으로 설정되어 있으며, 나중에 재생 페이지 링크가 있는 기본 랜딩 페이지로 개발될 수 있습니다.

브라우저 URL을 루트 페이지로 변경합니다. `http://localhost:4502/editor.html/content/an-scf-sandbox.html`

* 페이지 정보 아이콘 선택
* **[!UICONTROL 속성 열기]** 선택
* 고급 탭에서

   * 리디렉션 항목의 경우 **[!UICONTROL 웹 사이트]** > **[!UICONTROL SCF 샌드박스 사이트]** > **[!UICONTROL SCF 샌드박스]**&#x200B;로 이동합니다.
   * **[!UICONTROL 확인]** 클릭

* **[!UICONTROL 확인]** 클릭

사이트가 게시된 후 게시 인스턴스에서 루트 페이지를 탐색하면 영어 페이지로 리디렉션됩니다.

커뮤니티 SCF 구성 요소로 재생하기 전 마지막 단계는 클라이언트 라이브러리 폴더(clientlibs)를 추가하는 것입니다.... [Clientlibs 추가](add-clientlibs.md)
