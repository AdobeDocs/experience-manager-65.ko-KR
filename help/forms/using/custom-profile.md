---
title: HTML5 양식에 대한 사용자 지정 프로필 만들기
seo-title: Creating a custom profile for HTML5 forms
description: HTML5 양식 프로필은 Apache Sling의 리소스 노드입니다. 이 파일은 HTML5 forms Render 서비스의 사용자 지정된 버전을 나타냅니다.
seo-description: A HTML5 forms profile is a resource node in Apache Sling. It represents a customized version of HTML5 forms Render service.
uuid: b9938280-a92c-4dde-b465-04372db3ca8d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 9cd22244-9aa6-4b5f-96cf-c9cb3d6f9c8a
feature: Mobile Forms
exl-id: cf86c810-c466-4894-acc2-d4faf49754cc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 0%

---

# HTML5 양식에 대한 사용자 지정 프로필 만들기 {#creating-a-custom-profile-for-html-forms}

프로필은 의 리소스 노드입니다 [Apache Sling](https://sling.apache.org/). 사용자 정의 버전의 HTML5 forms 변환 서비스를 나타냅니다. HTML5 forms 변환 서비스를 사용하여 HTML5 양식의 모양, 동작 및 상호 작용을 사용자 지정할 수 있습니다. 프로필 노드는 `/content` JCR 저장소의 폴더입니다. 노드를 `/content` 폴더 또는 하위 폴더 `/content` 폴더를 입력합니다.

프로필 노드에는 **sling:resourceSuperType** 속성과 기본값은 입니다. **xfaforms/profile**. 노드에 대한 렌더링 스크립트는 /libs/xfaforms/profile에 있습니다.

Sling 스크립트는 JSP 스크립트입니다. 이러한 JSP 스크립트는 요청된 양식과 필요한 JS/CSS 아티팩트에 대한 HTML을 함께 배치하는 컨테이너 역할을 합니다. 이러한 Sling 스크립트를 이라고도 합니다 **프로필 렌더러 스크립트**. 프로필 렌더러는 Forms OSGi 서비스를 호출하여 요청된 양식을 렌더링합니다.

프로필 스크립트는 GET 및 POST 요청에 대해 html.jsp 및 html.POST.jsp에 있습니다. 하나 이상의 파일을 복사 및 수정하여 사용자 지정을 재정의하고 추가할 수 있습니다. 변경 작업을 수행하지 마십시오. 패치 업데이트가 해당 변경 사항을 덮어씁니다.

프로필에는 다양한 모듈이 포함되어 있습니다. 이러한 모듈은 formRuntime.jsp, config.jsp, toolbar.jsp, formBody.jsp, nav_footer.jsp 및 footer.jsp입니다.

## formRuntime.jsp {#formruntime-jsp-br}

formRuntime.jsp 모듈은 클라이언트 라이브러리에 대한 참조를 포함합니다. 또한 요청에서 로케일 정보를 추출하고 현지화된 메시지를 요청에 포함하는 방법을 설명합니다. formRuntime.jsp에 고유한 사용자 지정 JavaScript 라이브러리 또는 스타일을 포함할 수 있습니다.

## config.jsp {#config-jsp}

config.jsp 모듈에는 로깅, 프록시 서비스 및 동작 버전과 같은 다양한 구성이 포함되어 있습니다. config.jsp 모듈에 고유한 구성 및 위젯 사용자 지정을 추가할 수 있습니다. config.jsp 모듈에 사용자 지정 위젯 등록 등의 구성을 추가할 수도 있습니다.

## toolbar.jsp {#toolbar-jsp}

toolbar.jsp에는 색상 있는 도구 모음을 만드는 코드가 포함되어 있습니다. 도구 모음을 제거하려면 HTML.jsp에서 도구 모음.jsp를 제거합니다

## formBody.jsp {#formbody-jsp}

formBody.jsp 모듈은 XFA 양식의 HTML 표현을 위한 것입니다.

## nav_footer.jsp {#nav-footer-jsp}

처음에는 HTML5 폼에서 양식의 첫 페이지만 렌더링합니다. 사용자가 양식을 스크롤하면 나머지 양식이 로드됩니다. 이렇게 하면 로드 경험이 더 빨라집니다. nav_footer.jsp 구성 요소에는 스크롤 시 페이지를 쉽게 로드할 수 있도록 모든 스타일과 필수 요소가 포함되어 있습니다.

## footer.jsp {#footer-jsp}

footer.jsp 모듈이 비어 있습니다. 사용자 상호 작용에만 사용되는 스크립트를 추가할 수 있습니다.

## 사용자 지정 프로필 만들기 {#creating-custom-profiles}

사용자 지정 프로필을 만들려면 다음 단계를 수행하십시오.

### 프로필 노드 만들기 {#create-profile-node}

1. URL에서 CRX DE 인터페이스로 이동합니다. `https://'[server]:[port]'/crx/de` 관리자 자격 증명을 사용하여 인터페이스에 로그인합니다.

1. 왼쪽 창에서 위치로 이동합니다 */content/xfaforms/profiles*.

1. 노드 기본값을 복사하고 다른 폴더에 붙여 넣습니다(*/content/profiles*) with name *서식*.

1. 새 노드를 선택합니다. *서식*, 및 문자열 속성을 추가합니다. *sling:resourceType* 값: *양식/데모*.

1. 도구 모음 메뉴에서 모두 저장 을 클릭하여 변경 사항을 저장합니다.

### 프로필 렌더러 스크립트 만들기 {#create-the-profile-renderer-script}

사용자 지정 프로필을 만든 후 이 프로필에 렌더링 정보를 추가합니다. 새 프로필에 대한 요청을 받으면 CRX에서 렌더링할 JSP 페이지에 대한 /apps 폴더가 있는지 확인합니다. /apps 폴더에 JSP 페이지를 만듭니다.

1. 왼쪽 창에서 `/apps` 폴더를 입력합니다.
1. 을(를) 마우스 오른쪽 단추로 클릭합니다. `/apps` 폴더 및 이름을 사용하는 폴더를 만들도록 선택합니다. **서식**.
1. 내부자 **서식** 폴더 이름이 지정된 폴더 만들기 **데모**.
1. 을(를) 클릭합니다. **모두 저장** 버튼을 클릭합니다.
1. 다음으로 이동 `/libs/xfaforms/profile/html.jsp` 노드를 복사하여 **html.jsp**.
1. 붙여넣기 **html.jsp** 노드 `/apps/hrform/demo` 같은 이름의 위에 만들어진 폴더 **html.jsp** 을(를) 클릭합니다. **저장**.
1. 프로필 스크립트의 다른 구성 요소가 있는 경우 1-6단계에 따라 /apps/hrform/demo 폴더에 있는 구성 요소를 복사합니다.

1. 프로필이 만들어졌는지 확인하려면 URL을 엽니다 `https://'[server]:[port]'/content/xfaforms/profiles/hrform.html`

양식을 확인하려면 [양식 가져오기](/help/forms/using/get-xdp-pdf-documents-aem.md) 로컬 파일 시스템에서 AEM Forms 및 [양식 미리 보기](/help/forms/using/previewing-forms.md) AEM 서버 작성자 인스턴스에서 참조할 수 있습니다.
