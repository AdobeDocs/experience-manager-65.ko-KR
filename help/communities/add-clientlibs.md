---
title: Clientlibs 추가
seo-title: Clientlibs 추가
description: ClientLibraryFolder 추가
seo-description: ClientLibraryFolder 추가
uuid: 2944923d-caca-4607-81a4-4122a2ce8e41
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 46f81c3f-6512-43f1-8ec1-cc717ab6f6ff
docset: aem65
translation-type: tm+mt
source-git-commit: fcdae5363e7a0070b5d6b76227e5c65efb71bc03
workflow-type: tm+mt
source-wordcount: '687'
ht-degree: 2%

---


# Clientlibs {#add-clientlibs} 추가

## ClientLibraryFolder(clientlibs) {#add-a-clientlibraryfolder-clientlibs} 추가

사이트의 페이지를 렌더링하는 데 사용되는 JS와 CSS를 포함할 `clientlibs`이라는 ClientLibraryFolder를 만듭니다.

이 클라이언트 라이브러리에 지정된 `categories` 속성 값은 컨텐츠 페이지에서 이 clientlib을 직접 포함하거나 다른 clientlibs에 포함하는 데 사용되는 식별자입니다.

1. **CRXDE Lite**&#x200B;을 사용하여 `/etc/designs`를 확장합니다.

1. `an-scf-sandbox`을 마우스 오른쪽 단추로 클릭하고 `Create Node` 선택

   * 이름 : `clientlibs`
   * 유형 : `cq:ClientLibraryFolder`

1. **확인**&#x200B;을 클릭합니다

![add-client-library](assets/add-client-library.png)

새 `clientlibs` 노드의 **속성** 탭에서 **categories** 속성을 입력합니다.

* 이름:**categories**
* 유형:**문자열**
* 값:**apps.an-scf-sandbox**
* **추가**&#x200B;를 클릭합니다
* **모두 저장**&#x200B;을 클릭합니다.

참고:&#39;apps&#39;로 카테고리 값 미리 보기 는 &#39;소유 응용 프로그램&#39;이 /libs가 아닌 /apps 폴더에 있는 것으로 식별하기 위한 규칙입니다.  중요:자리 표시자 `js.tx`t 및 **`css.txt`** 파일을 추가합니다. (cq:ClientLibraryFolder가 없는 것은 아닙니다.)

1. **`/etc/designs/an-scf-sandbox/clientlibs`** 마우스 오른쪽 단추 클릭
1. **파일 만들기...를 선택합니다.**
1. **이름:** `css.txt` 입력
1. **파일 만들기...를 선택합니다.**
1. **이름:** `js.txt` 입력
1. **모두 저장**&#x200B;을 클릭합니다.

![clientlibs-css](assets/clientlibs-css.png)

css.txt 및 js.txt의 첫 번째 행은 다음 파일 목록을 찾을 기본 위치를 식별합니다.

css.txt의 컨텐츠를

```
#base=.
 style.css
```

그런 다음 style.css라는 clientlibs 아래에 파일을 만들고

`body {`

`background-color: #b0c4de;`

`}`

### SCF Clientlibs {#embed-scf-clientlibs} 포함

`clientlibs` 노드의 **속성** 탭에서 다중 값 문자열 속성 **embed**&#x200B;을 입력합니다. 여기에는 SCF 구성 요소](/help/communities/client-customize.md#clientlibs-for-scf)에 필요한 [클라이언트측 라이브러리(clientlibs)가 포함됩니다. 이 자습서의 경우 커뮤니티 구성 요소에 필요한 많은 클라이언트가 추가되었습니다.

**각 페이지에 대해 다운로드된 클라이언트의 크기/속도 및 편의에 대한 고려 사항이 있기 때문에 프로덕션 사이트에서 사용하기 원하는 접근 방식이 될지** 여부에 관계 없이 이러한 접근 방식이 적절하지 않을 수 있습니다.

한 페이지에 하나의 기능을 사용하기만 하면 페이지에 해당 기능의 전체 clientlib를 직접 포함시킬 수 있습니다(예:

`% ui:includeClientLib categories=cq.social.hbs.forum" %`

이 경우, 모든 SCF 클라이언트를 포함하여 작성자 clientlibs인 보다 기본적인 SCF clientlibs가 권장됩니다.

* 이름 : **`embed`**
* 유형 : **`String`**
* 클릭 **`Multi`**
* 값: **`cq.social.scf`**

   * 대화도 하고
다음 clientlib 범주를 추가하려면 각 항목 뒤에 **`+`**&#x200B;을(를) 클릭하십시오.

      * **`cq.ckeditor`**
      * **`cq.social.author.hbs.comments`**
      * **`cq.social.author.hbs.forum`**
      * **`cq.social.author.hbs.rating`**
      * **`cq.social.author.hbs.reviews`**
      * **`cq.social.author.hbs.voting`**
      * **확인**&#x200B;을 클릭합니다

* **모두 저장**&#x200B;을 클릭합니다.

![scf-clientlibs](assets/scf-clientlibs.png)

이제 `/etc/designs/an-scf-sandbox/clientlibs`이(가) 저장소에 표시되는 방식입니다.

![scf-clientlibs-view](assets/scf-clientlibs1.png)

### PlayPage 템플릿에 Clientlibs 포함 {#include-clientlibs-in-playpage-template}

페이지에 `apps.an-scf-sandbox` ClientLibraryFolder 카테고리를 포함하지 않으면 SCF 구성 요소가 기능하거나 필요한 Javascript 및 스타일로 스타일이 적용되지 않습니다.

예를 들어 clientlibs를 포함하지 않으면 SCF 주석 구성 요소는 스타일이 지정되지 않은 것으로 나타납니다.

![clientlibs-comment](assets/clientlibs-comment.png)

apps.an-scf-sandbox clientlibs가 포함되면, SCF 댓글 구성 요소가 스타일이 적용된 것으로 나타납니다.

![clientlibs-comment-styled](assets/clientlibs-comment1.png)

include 문은 `html` 스크립트의 `head` 섹션에 속합니다. 기본 **`foundation head.jsp`**&#x200B;에는 오버레이할 수 있는 스크립트가 포함되어 있습니다.**`headlibs.jsp`**.

**headlibs.jsp 복사 및 clientlibs 포함:**

1. **CRXDE Lite**&#x200B;을 사용하여 **`/libs/foundation/components/page/headlibs.jsp`**&#x200B;를 선택합니다.

1. 마우스 오른쪽 단추를 클릭하고 **복사**&#x200B;를 선택합니다(또는 도구 모음에서 복사 선택).
1. 선택 **`/apps/an-scf-sandbox/components/playpage`**
1. 마우스 오른쪽 단추를 클릭하고 **붙여넣기**&#x200B;를 선택합니다(또는 도구 모음에서 붙여넣기 선택).
1. **`headlibs.jsp`**&#x200B;을 두 번 클릭하여 엽니다.
1. 파일 끝에 다음 줄 추가
   **`<ui:includeClientLib categories="apps.an-scf-sandbox"/>`**

1. **모두 저장**&#x200B;을 클릭합니다.

```xml
<%@ page session="false" %><%
%><%@include file="/libs/foundation/global.jsp" %><%
%><ui:includeClientLib categories="cq.foundation-main"/><%
%>
<cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
<% currentDesign.writeCssIncludes(pageContext); %>
<ui:includeClientLib categories="apps.an-scf-sandbox"/>
```

브라우저에 웹 사이트를 로드하고 배경이 파란색이 아닌지 확인합니다.

[https://localhost:4502/content/an-scf-sandbox/en/play.html](https://localhost:4502/content/an-scf-sandbox/en/play.html)

![커뮤니티 플레이](assets/community-play.png)

### 작업을 최대 {#saving-your-work-so-far} 저장

이 시점에서, 최소 샌드박스는 존재하며, 재생 중에 저장소가 손상되고 다시 시작하려는 경우, 서버를 끄거나, 폴더 crx-quickstart/를 변경하거나 삭제하고, 서버를 켜거나, 이 저장된 패키지를 업로드 및 설치할 수 있으며, 이러한 가장 기본적인 단계를 반복하지 않아도 됩니다.

이 패키지는 [샘플 페이지 만들기](/help/communities/create-sample-page.md) 튜토리얼에 있으며 빠르게 들어가서 재생을 시작할 수 있습니다!..

패키지를 생성하려면

* CRXDE Lite에서 [패키지 아이콘](https://localhost:4502/crx/packmgr/)을 클릭합니다.
* **패키지 만들기**&#x200B;를 클릭합니다.

   * 패키지 이름:an-scf-sandbox-minimal-pkg
   * 버전:0.1
   * 그룹: `leave as default`
   * **확인**&#x200B;을 클릭합니다

* **편집**&#x200B;을 클릭합니다

   * **필터** 탭 선택

      * **필터 추가**&#x200B;를 클릭합니다.
      * 루트 경로:`/apps/an-scf-sandbox` 찾아보기
      * **완료**&#x200B;를 클릭합니다.
      * **필터 추가**&#x200B;를 클릭합니다.
      * 루트 경로:`/etc/designs/an-scf-sandbox` 찾아보기
      * **완료**&#x200B;를 클릭합니다.
      * **필터 추가**&#x200B;를 클릭합니다.
      * 루트 경로:`/content/an-scf-sandbox**` 찾아보기
      * **완료**&#x200B;를 클릭합니다.
   * **저장**&#x200B;을 클릭합니다


* **빌드**&#x200B;를 클릭합니다.

이제 **다운로드**&#x200B;를 선택하여 디스크에 저장하고 다른 곳에서 **패키지 업로드**&#x200B;를 선택할 수 있을 뿐만 아니라, 샌드박스를 localhost 게시 인스턴스로 푸시하여 샌드박스의 영역을 확장하려면 **자세히 > 복제**&#x200B;를 선택합니다.