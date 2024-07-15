---
title: Clientlibs 추가
description: 사이트 페이지를 렌더링하는 데 사용되는 JavaScript 및 계단식 스타일 시트를 포함하는 데 사용되는 ClientLibraryFolder(clientlibs)를 추가하는 방법에 대해 알아봅니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 569f2052-b4fe-4f7f-aec9-657217cba091
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 0%

---

# Clientlibs 추가 {#add-clientlibs}

## ClientLibraryFolder 추가(clientlibs) {#add-a-clientlibraryfolder-clientlibs}

사이트의 페이지를 렌더링하는 데 사용되는 JavaScript(JS) 및 CSS(계단식 스타일 시트)가 포함된 이름이 `clientlibs`인 ClientLibraryFolder를 만듭니다.

이 클라이언트 라이브러리에 제공된 `categories` 속성 값은 콘텐츠 페이지에서 이 clientlib을 직접 포함하거나 다른 clientlib에 임베드하는 데 사용되는 식별자입니다.

1. **CRXDE Lite**&#x200B;을(를) 사용하여 `/etc/designs` 확장

1. `an-scf-sandbox`을(를) 마우스 오른쪽 단추로 클릭하고 `Create Node`을(를) 선택합니다

   * 이름: `clientlibs`
   * 유형: `cq:ClientLibraryFolder`

1. **확인** 클릭

![add-client-library](assets/add-client-library.png)

새 `clientlibs` 노드의 **속성** 탭에서 **categories** 속성을 입력하십시오.

* 이름: **범주**
* 유형: **문자열**
* 값: **apps.an-scf-sandbox**
* **추가** 클릭
* **모두 저장** 클릭

참고: 카테고리 값에 &#39;앱&#39;을 앞에 붙입니다. 는 &#39;소유 애플리케이션&#39;을 /libs가 아닌 /apps 폴더에 있는 것으로 식별하는 규칙입니다. 중요: 자리 표시자 `js.tx`t 및 **`css.txt`** 파일을 추가하십시오. (이러한 폴더가 없는 공식적으로 cq:ClientLibraryFolder는 아닙니다.)

1. **`/etc/designs/an-scf-sandbox/clientlibs`**&#x200B;을(를) 마우스 오른쪽 단추로 클릭
1. **파일 만들기...** 선택
1. **이름:** `css.txt` 입력
1. **파일 만들기...** 선택
1. **이름:** `js.txt` 입력
1. **모두 저장** 클릭

![clientlibs-css](assets/clientlibs-css.png)

css.txt 및 js.txt의 첫 번째 행은 다음 파일 목록을 찾을 기본 위치를 식별합니다.

css.txt의 콘텐츠를 다음으로 설정

```
#base=.
 style.css
```

그런 다음 style.css라는 clientlibs 아래에 파일을 만들고 컨텐츠를 로 설정합니다.

`body {`

`background-color: #b0c4de;`

`}`

### SCF Clientlibs 포함 {#embed-scf-clientlibs}

`clientlibs` 노드의 **속성** 탭에서 다중 값 문자열 속성 **embed**&#x200B;을(를) 입력하십시오. SCF 구성 요소에 필요한 [클라이언트측 라이브러리(clientlibs)를 임베드합니다](/help/communities/client-customize.md#clientlibs-for-scf). 이 자습서의 경우 Communities 구성 요소에 필요한 많은 clientlib이 추가됩니다.

모든 페이지에 대해 다운로드한 클라이언트 라이브러리의 크기/속도에 대한 편의성 고려 사항이 있으므로 이 방법은 프로덕션 사이트에 사용하는 것이 바람직하거나 적합하지 않을 수 있습니다.

한 페이지에서 하나의 기능만 사용하는 경우 해당 기능의 전체 clientlib을 페이지에 직접 포함할 수 있습니다. 예를 들면 다음과 같습니다.

`% ui:includeClientLib categories=cq.social.hbs.forum" %`

이 경우 이들 모두를 포함하여 작성자 clientlib인 보다 기본적인 SCF clientlib이 선호됩니다.

* 이름: **`embed`**
* 유형: **`String`**
* **`Multi`** 클릭
* 값: **`cq.social.scf`**

   * 대화창이 뜨고
다음 clientlib 범주를 추가하려면 각 항목 뒤에 있는 **`+`**&#x200B;을(를) 클릭하십시오.

      * **`cq.ckeditor`**
      * **`cq.social.author.hbs.comments`**
      * **`cq.social.author.hbs.forum`**
      * **`cq.social.author.hbs.rating`**
      * **`cq.social.author.hbs.reviews`**
      * **`cq.social.author.hbs.voting`**
      * **확인** 클릭

* **모두 저장** 클릭

![scf-clientlibs](assets/scf-clientlibs.png)

다음은 `/etc/designs/an-scf-sandbox/clientlibs`이(가) 저장소에 표시되는 방식입니다.

![scf-clientlibs-view](assets/scf-clientlibs1.png)

### PlayPage 템플릿에 Clientlib 포함 {#include-clientlibs-in-playpage-template}

페이지에 `apps.an-scf-sandbox` ClientLibraryFolder 범주를 포함하지 않으면 필요한 JavaScript 및 CSS 스타일을 사용할 수 없으므로 SCF 구성 요소가 작동하지 않거나 스타일이 지정되지 않습니다.

예를 들어 clientlibs를 포함하지 않으면 SCF 주석 구성 요소가 스타일이 지정되지 않은 상태로 표시됩니다.

![clientlibs-comment](assets/clientlibs-comment.png)

apps.an-scf-sandbox clientlibs가 포함되면 SCF 주석 구성 요소 스타일이 지정됩니다.

![clientlibs-comment-styled](assets/clientlibs-comment1.png)

include 문은 `html` 스크립트의 `head` 섹션에 속합니다. 기본 **`foundation head.jsp`**&#x200B;에 오버레이할 수 있는 스크립트가 포함되어 있습니다. **`headlibs.jsp`**.

**headlibs.jsp 복사 및 clientlibs 포함:**

1. **CRXDE Lite**&#x200B;을(를) 사용하여 **`/libs/foundation/components/page/headlibs.jsp`**&#x200B;을(를) 선택하십시오.

1. 마우스 오른쪽 단추를 클릭하고 **복사**&#x200B;를 선택하거나 도구 모음에서 복사 를 선택합니다.
1. **`/apps/an-scf-sandbox/components/playpage`** 선택
1. 마우스 오른쪽 단추를 클릭하고 **붙여넣기**&#x200B;를 선택합니다(또는 도구 모음에서 붙여넣기 선택).
1. **`headlibs.jsp`**&#x200B;을(를) 두 번 클릭하여 열 수 있습니다.
1. 파일 끝에 다음 줄을 추가합니다
   **`<ui:includeClientLib categories="apps.an-scf-sandbox"/>`**

1. **모두 저장** 클릭

```xml
<%@ page session="false" %><%
%><%@include file="/libs/foundation/global.jsp" %><%
%><ui:includeClientLib categories="cq.foundation-main"/><%
%>
<cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
<% currentDesign.writeCssIncludes(pageContext); %>
<ui:includeClientLib categories="apps.an-scf-sandbox"/>
```

브라우저에 웹 사이트를 로드하고 배경이 파란색 음영이 아닌지 확인합니다.

[https://localhost:4502/content/an-scf-sandbox/en/play.html](https://localhost:4502/content/an-scf-sandbox/en/play.html)

![커뮤니티 재생](assets/community-play.png)

### 지금까지 작업 저장 {#saving-your-work-so-far}

이 시점에는 최소 샌드박스가 존재합니다. 재생하는 동안 저장소가 손상되어 다시 시작하려는 경우 서버를 끌 수 있도록 패키지로 저장할 가치가 있을 수 있습니다. 그런 다음 crx-quickstart/ 폴더의 이름을 바꾸거나 삭제하고, 서버를 켜고, 이 저장된 패키지를 업로드하고 설치합니다. 이러한 가장 기본적인 단계를 반복하지 않아도 됩니다.

이 패키지는 [샘플 페이지 만들기](/help/communities/create-sample-page.md) 자습서에 있습니다. 바로 시작하여 재생을 시작할 때까지 기다릴 수 없는 사용자를 위한 것입니다.

패키지를 만들려면 다음을 수행하십시오.

* CRXDE Lite에서 [패키지 아이콘](https://localhost:4502/crx/packmgr/)을 클릭하세요.
* **패키지 만들기** 클릭

   * 패키지 이름: an-scf-sandbox-minimal-pkg
   * 버전: 0.1
   * 그룹: `leave as default`
   * **확인** 클릭

* **편집** 클릭

   * **필터** 탭 선택

      * **필터 추가** 클릭
      * 루트 경로: `/apps/an-scf-sandbox` 찾아보기
      * **완료** 클릭
      * **필터 추가** 클릭
      * 루트 경로: `/etc/designs/an-scf-sandbox` 찾아보기
      * **완료** 클릭
      * **필터 추가** 클릭
      * 루트 경로: `/content/an-scf-sandbox**` 찾아보기
      * **완료** 클릭

   * **저장** 클릭

* **빌드** 클릭

이제 **다운로드**&#x200B;를 선택하여 디스크에 저장하고 다른 곳에서 **패키지 업로드**&#x200B;를 선택한 다음 **자세히 > 복제**&#x200B;를 선택하여 샌드박스를 localhost 게시 인스턴스로 푸시하여 샌드박스의 영역을 확장할 수 있습니다.
