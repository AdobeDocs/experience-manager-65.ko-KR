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
source-git-commit: d6c8bbb9aa763a2eb6660b6b6755aba75241e394

---


# Clientlibs 추가 {#add-clientlibs}

## ClientLibraryFolder 추가(clientlibs) {#add-a-clientlibraryfolder-clientlibs}

사이트의 페이지를 렌더링하는 데 사용되는 JS 및 CSS가 `clientlibs`포함될 ClientLibraryFolder를 만듭니다.

이 클라이언트 라이브러리에 지정된 `categories`속성 값은 컨텐츠 페이지에서 이 clientlib을 직접 포함하거나 다른 clientlibs에 임베드하는 데 사용되는 식별자입니다.

1. CRXDE **Lite를 사용하여**&#x200B;확장 `/etc/designs`

1. 마우스 오른쪽 버튼을 클릭하여 `an-scf-sandbox` 선택 `Create Node`

   * 이름 : `clientlibs`
   * 유형 : `cq:ClientLibraryFolder`

1. **확인**&#x200B;을 클릭합니다

![chlimage_1-47](assets/chlimage_1-47.png)

새 **노드의 속성** 탭에서 `clientlibs` categories **** 속성을 입력합니다.

* 이름: **카테고리**
* 유형:문자열 ****
* 값: **apps.an-scf-sandbox**
* **추가**&#x200B;를 클릭합니다
* 모두 **저장을 클릭합니다.**

참고:&#39;apps&#39;로 카테고리 값 미리 보기 는 &#39;소유 응용 프로그램&#39;이 /libs가 아닌 /apps 폴더에 있는 것으로 식별하기 위한 규칙입니다.  중요:자리 표시자 `js.tx`t 및 **`css.txt`** 파일 추가 공식적으로 cq:ClientLibraryFolder가 없는 것은 아닙니다.

1. 마우스 오른쪽 단추 클릭 **`/etc/designs/an-scf-sandbox/clientlibs`**
1. 파일 **만들기...를 선택합니다.**
1. Enter **Name:** `css.txt`
1. 파일 **만들기...를 선택합니다.**
1. Enter **Name:** `js.txt`
1. 모두 **저장을 클릭합니다.**

![chlimage_1-48](assets/chlimage_1-48.png)

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

### SCF Clientlibs 포함 {#embed-scf-clientlibs}

노드의 **속성** 탭에서 다중 값 문자열 속성 `clientlibs` 포함을 ****&#x200B;입력합니다. 이렇게 하면 SCF 구성 요소에 [](/help/communities/client-customize.md#clientlibs-for-scf)필요한 클라이언트측 라이브러리(clientlibs)가 포함됩니다. 이 자습서에서는 Communities 구성 요소에 필요한 많은 Clientlibs가 추가됩니다.

**모든** 페이지에 대해 다운로드된 클라이언트의 크기/속도 및 편의에 대한 고려 사항이 있기 때문에 프로덕션 사이트에 사용하기 위한 원하는 접근 방식이 될 수도 있고 아닐 수도 있습니다.

한 페이지에 하나의 기능을 사용하는 경우, 해당 기능의 전체 clientlib을 페이지에 직접 포함할 수 있습니다(예:

`% ui:includeClientLib categories=cq.social.hbs.forum" %`

이 경우 모든 SCF 클라이언트를 포함하여 작성자 clientlibs의 기본 SCF clientlibs가 우선합니다.

* 이름 : **`embed`**
* 유형 : **`String`**
* 클릭 **`Multi`**
* 값: **`cq.social.scf`**

   * 대화 상자가 나타나면 **`+`** 각 항목 다음에 아이콘을 클릭하여 다음 clientlib 범주를 추가합니다.

      * **`cq.ckeditor`**
      * **`cq.social.author.hbs.comments`**
      * **`cq.social.author.hbs.forum`**
      * **`cq.social.author.hbs.rating`**
      * **`cq.social.author.hbs.reviews`**
      * **`cq.social.author.hbs.voting`**
      * click **OK**

* 모두 **저장을 클릭합니다.**

![chlimage_1-49](assets/chlimage_1-49.png)

이제 `/etc/designs/an-scf-sandbox/clientlibs` 저장소에 표시되는 방법입니다.

![chlimage_1-50](assets/chlimage_1-50.png)

### PlayPage 템플릿에 Clientlibs 포함 {#include-clientlibs-in-playpage-template}

페이지에 ClientLibraryFolder `apps.an-scf-sandbox` 범주를 포함하지 않으면 SCF 구성 요소가 필수 Javascript 및 스타일로 기능하거나 스타일을 지정하지 않습니다.

예를 들어 clientlibs를 포함하지 않으면 SCF 주석 구성 요소는 스타일이 지정되지 않은 것으로 나타납니다.

![chlimage_1-51](assets/chlimage_1-51.png)

apps.an-scf-sandbox clientlibs가 포함되면, SCF 주석 구성 요소가 스타일이 지정된 것으로 나타납니다.

![chlimage_1-52](assets/chlimage_1-52.png)

include 문은 `head` 스크립트의 `html` 섹션에 속합니다. 기본적으로 오버레이할 수 있는 스크립트가 **`foundation head.jsp`** 포함되어 있습니다. **`headlibs.jsp`** Adobe

**headlibs.jsp 복사 및 clientlibs 포함:**

1. CRXDE **Lite를**&#x200B;사용하여 **`/libs/foundation/components/page/headlibs.jsp`**

1. 마우스 오른쪽 단추를 클릭하고 **복사를** 선택합니다(또는 도구 모음에서 복사 선택).
1. 선택 **`/apps/an-scf-sandbox/components/playpage`**
1. 마우스 오른쪽 단추를 클릭하고 **붙여넣기를** 선택합니다(또는 도구 모음에서 붙여넣기를 선택합니다).
1. 두 번 클릭하여 **`headlibs.jsp`** 열기
1. 파일 끝에 다음 줄을 추가합니다.
   **`<ui:includeClientLib categories="apps.an-scf-sandbox"/>`**

1. 모두 **저장을 클릭합니다.**

```xml
<%@ page session="false" %><%
%><%@include file="/libs/foundation/global.jsp" %><%
%><ui:includeClientLib categories="cq.foundation-main"/><%
%>
<cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
<% currentDesign.writeCssIncludes(pageContext); %>
<ui:includeClientLib categories="apps.an-scf-sandbox"/>
```

브라우저에서 웹 사이트를 로드하고 배경이 파란색이 아닌지 확인합니다.

[https://localhost:4502/content/an-scf-sandbox/en/play.html](https://localhost:4502/content/an-scf-sandbox/en/play.html)

![chlimage_1-53](assets/chlimage_1-53.png)

### 지금까지 작업 저장 {#saving-your-work-so-far}

이때, 최소 샌드박스는 존재하며, 이를 패키지로 저장할 가치가 있으므로, 재생하는 동안 저장소가 손상되고 다시 시작하고자 하는 경우, 서버를 끄거나, 폴더 crx-quickstart/를 삭제하거나, 서버를 켜거나, 이 저장된 패키지를 업로드 및 설치할 수 있으며, 이러한 가장 기본적인 단계를 반복할 필요가 없습니다.

이 패키지는 바로 [들어가서](/help/communities/create-sample-page.md) 재생을 시작할 때까지 기다릴 수 없는 사용자를 위해 샘플 페이지 만들기 자습서에 있습니다...

패키지를 생성하려면

* CRXDE Lite에서 패키지 [아이콘을 클릭합니다](https://localhost:4502/crx/packmgr/)
* 패키지 **만들기를 클릭합니다.**

   * 패키지 이름:an-scf-sandbox-minimal-pkg
   * 버전:0.1
   * 그룹: `leave as default`
   * **확인**&#x200B;을 클릭합니다

* **편집**&#x200B;을 클릭합니다

   * 필터 **선택** 탭

      * 필터 **추가를 클릭합니다.**
      * 루트 경로:찾아보기 `/apps/an-scf-sandbox`
      * 완료를 **클릭합니다**
      * 필터 **추가를 클릭합니다.**
      * 루트 경로:찾아보기 `/etc/designs/an-scf-sandbox`
      * 완료를 **클릭합니다**
      * 필터 **추가를 클릭합니다.**
      * 루트 경로:찾아보기 `/content/an-scf-sandbox**`
      * 완료를 **클릭합니다**
   * **저장**&#x200B;을 클릭합니다


* 빌드를 **클릭합니다**

이제 다운로드를 선택하여 **디스크에** 저장하고 다른 **곳에서 패키지** 업로드를 **선택할 수 있을 뿐만 아니라** 추가 > 복제를 선택하여 샌드박스를 localhost 게시 인스턴스로 푸시하여 샌드박스 영역을 확장할 수 있습니다.