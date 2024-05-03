---
title: HTML5 양식에 대한 사용자 지정 프로필 만들기
description: HTML5 양식 프로필은 Apache Sling의 리소스 노드입니다. HTML5 양식 렌더링 서비스의 사용자 지정 버전을 나타냅니다.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 9cd22244-9aa6-4b5f-96cf-c9cb3d6f9c8a
feature: HTML5 Forms
exl-id: cf86c810-c466-4894-acc2-d4faf49754cc
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 0%

---

# HTML5 양식에 대한 사용자 지정 프로필 만들기 {#creating-a-custom-profile-for-html-forms}

프로필은 의 리소스 노드입니다. [Apache Sling](https://sling.apache.org/). 사용자 정의 버전의 HTML5 양식 렌디션 서비스를 나타냅니다. HTML5 양식 렌디션 서비스를 사용하여 HTML5 양식의 모양, 동작 및 상호 작용을 사용자 지정할 수 있습니다. 프로필 노드가에 있음 `/content` JCR 저장소의 폴더 노드 바로 아래에 배치할 수 있습니다. `/content` 폴더 또는 폴더의 하위 폴더 `/content` 폴더를 삭제합니다.

프로필 노드에는 **sling:resourceSuperType** 속성 및 기본값은 입니다. **xfaforms/profile**. 노드에 대한 렌더링 스크립트는 /libs/xfaforms/profile에 있습니다.

Sling 스크립트는 JSP 스크립트입니다. 이러한 JSP 스크립트는 요청된 양식에 대한 HTML과 필요한 JS/CSS 아티팩트를 결합하는 컨테이너 역할을 합니다. 이러한 Sling 스크립트는 **프로필 렌더러 스크립트**. 프로필 렌더러는 Forms OSGi 서비스를 호출하여 요청된 양식을 렌더링합니다.

GET 및 POST 요청에 대한 POST 스크립트는 html.jsp 및 html.profile.jsp에 있습니다. 하나 이상의 파일을 복사하고 수정하여 사용자 정의를 재정의하고 추가할 수 있습니다. 즉시 변경하지 마십시오. 패치 업데이트는 이러한 변경 사항을 덮어씁니다.

프로필에는 다양한 모듈이 포함되어 있습니다. 모듈은 formRuntime.jsp, config.jsp, toolbar.jsp, formBody.jsp, nav_footer.jsp 및 footer.jsp입니다.

## formRuntime.jsp {#formruntime-jsp-br}

formRuntime.jsp 모듈에는 클라이언트 라이브러리에 대한 참조가 포함되어 있습니다. 또한 요청에서 로케일 정보를 추출하고 현지화된 메시지를 요청에 포함하는 방법을 설명합니다. formRuntime.jsp에 고유한 customJavaScript 라이브러리 또는 스타일을 포함할 수 있습니다.

## config.jsp {#config-jsp}

config.jsp 모듈에는 로깅, 프록시 서비스 및 동작 버전과 같은 다양한 구성이 포함되어 있습니다. config.jsp 모듈에 자체 구성 및 위젯 사용자 정의를 추가할 수 있습니다. 사용자 정의 위젯 등록과 같은 구성을 config.jsp 모듈에 추가할 수도 있습니다.

## toolbar.jsp {#toolbar-jsp}

toolbar.jsp에는 색상이 지정된 도구 모음을 만드는 코드가 포함되어 있습니다. 도구 모음을 제거하려면 HTML.jsp에서 toolbar.jsp를 제거합니다

## formBody.jsp {#formbody-jsp}

formBody.jsp 모듈은 XFA 양식의 HTML 표시를 위한 것입니다.

## nav_footer.jsp {#nav-footer-jsp}

처음에는 HTML5 폼이 폼의 첫 페이지만 렌더링합니다. 사용자가 양식을 스크롤하면 나머지 양식이 로드됩니다. 로드 경험이 빨라집니다. nav_footer.jsp 구성 요소에는 스크롤할 때 페이지를 쉽게 로드할 수 있도록 모든 스타일과 필수 요소가 포함되어 있습니다.

## footer.jsp {#footer-jsp}

footer.jsp 모듈이 비어 있습니다. 사용자 상호 작용에만 사용되는 스크립트를 추가할 수 있습니다.

## 사용자 지정 프로필 만들기 {#creating-custom-profiles}

사용자 지정 프로필을 만들려면 다음 단계를 수행하십시오.

### 프로필 노드 만들기 {#create-profile-node}

1. 다음 URL에서 CRX DE 인터페이스로 이동합니다. `https://'[server]:[port]'/crx/de` 관리자 자격 증명으로 인터페이스에 로그인합니다.

1. 왼쪽 창에서 다음 위치로 이동합니다 */content/xfaforms/profiles*.

1. 노드 기본값을 복사하고 노드를 다른 폴더에 붙여넣습니다(*/content/profiles*)(이름 포함) *hrform*.

1. 새 노드 선택, *hrform*&#x200B;을 클릭하고 문자열 속성을 추가합니다. *sling:resourceType* 값: *hraform/demo*.

1. 도구 모음 메뉴에서 모두 저장 을 클릭하여 변경 사항을 저장합니다.

### 프로필 렌더러 스크립트 만들기 {#create-the-profile-renderer-script}

사용자 지정 프로필을 만든 후 이 프로필에 렌더링 정보를 추가합니다. 새 프로필에 대한 요청을 받으면 CRX는 렌더링할 JSP 페이지에 대한 /apps 폴더가 있는지 확인합니다. /apps 폴더에 JSP 페이지를 만듭니다.

1. 왼쪽 창에서 `/apps` 폴더를 삭제합니다.
1. 마우스 오른쪽 단추 클릭 `/apps` 폴더 및 이름으로 폴더 만들기 선택 **hrform**.
1. 참가자 **hrform** 폴더 다음 이름의 폴더 만들기 **데모**.
1. 다음을 클릭합니다. **모두 저장** 단추를 클릭합니다.
1. 다음으로 이동 `/libs/xfaforms/profile/html.jsp` 노드 복사 **html.jsp**.
1. 붙여넣기 **html.jsp** 노드를 로 `/apps/hrform/demo` 같은 이름으로 위에서 만든 폴더 **html.jsp** 및 클릭 **저장**.
1. 프로필 스크립트의 다른 구성 요소가 있는 경우 1-6단계를 따라 /apps/hrform/demo 폴더에 구성 요소를 복사합니다.

1. 프로필이 만들어졌는지 확인하려면 URL을 엽니다. `https://'[server]:[port]'/content/xfaforms/profiles/hrform.html`

양식을 확인하려면 [양식 가져오기](/help/forms/using/get-xdp-pdf-documents-aem.md) 로컬 파일 시스템에서 AEM Forms 및 [양식 미리 보기](/help/forms/using/previewing-forms.md) AEM 서버 작성자 인스턴스에서 다음을 수행합니다.
