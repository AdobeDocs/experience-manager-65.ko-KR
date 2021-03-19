---
title: HTML5 양식에 대한 사용자 정의 프로필 만들기
seo-title: HTML5 양식에 대한 사용자 정의 프로필 만들기
description: HTML5 양식 프로필은 Apache Sling의 리소스 노드입니다. 이는 HTML5 양식 렌더링 서비스의 사용자 지정된 버전을 나타냅니다.
seo-description: HTML5 양식 프로필은 Apache Sling의 리소스 노드입니다. 이는 HTML5 양식 렌더링 서비스의 사용자 지정된 버전을 나타냅니다.
uuid: b9938280-a92c-4dde-b465-04372db3ca8d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 9cd22244-9aa6-4b5f-96cf-c9cb3d6f9c8a
feature: Mobile Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 0%

---


# HTML5 양식에 대한 사용자 정의 프로필 만들기 {#creating-a-custom-profile-for-html-forms}

프로필은 [Apache Sling](https://sling.apache.org/)의 리소스 노드입니다. HTML5 양식 변환 서비스의 사용자 정의 버전을 나타냅니다. HTML5 양식 변환 서비스를 사용하여 HTML5 양식의 모양, 동작 및 상호 작용을 사용자 정의할 수 있습니다. 프로필 노드는 JCR 저장소의 `/content` 폴더에 있습니다. 노드를 `/content` 폴더 또는 `/content` 폴더의 하위 폴더 아래에 직접 배치할 수 있습니다.

프로필 노드에는 **sling:resourceSuperType** 속성이 있으며 기본값은 **xfaforms/profile**&#x200B;입니다. 노드에 대한 렌더링 스크립트는 /libs/xfaforms/profile에 있습니다.

Sling 스크립트는 JSP 스크립트입니다. 이러한 JSP 스크립트는 요청된 양식과 필요한 JS/CSS 가공물을 위한 HTML을 작성하기 위한 컨테이너 역할을 합니다. 이러한 Sling 스크립트를 **프로필 렌더러 스크립트**&#x200B;라고도 합니다. 프로필 렌더러는 Forms OSGi 서비스를 호출하여 요청된 양식을 렌더링합니다.

프로필 스크립트는 GET 및 POST 요청에 대해 html.jsp 및 html.POST.jsp에 있습니다. 하나 이상의 파일을 복사하고 수정하여 사용자 정의 설정을 재정의하고 추가할 수 있습니다. 제자리에서 변경하지 마십시오. 패치 업데이트는 이러한 변경 사항을 덮어씁니다.

프로필에는 다양한 모듈이 포함되어 있습니다. 모듈은 formRuntime.jsp, config.jsp, toolbar.jsp, formBody.jsp, nav_footer.jsp 및 footer.jsp입니다.

## formRuntime.jsp {#formruntime-jsp-br}

formRuntime.jsp 모듈은 클라이언트 라이브러리 참조를 포함합니다. 또한 요청에서 로케일 정보를 추출하는 방법을 표시하고, 요청에 현지화된 메시지를 포함하는 방법을 설명합니다. formRuntime.jsp에 고유한 customJavaScript 라이브러리 또는 스타일을 포함할 수 있습니다.

## config.jsp {#config-jsp}

config.jsp 모듈에는 로깅, 프록시 서비스 및 비헤이비어 버전과 같은 다양한 구성이 포함되어 있습니다. config.jsp 모듈에 고유한 구성 및 위젯 맞춤화를 추가할 수 있습니다. 구성.jsp 모듈에 사용자 정의 위젯 등록과 같은 구성을 추가할 수도 있습니다.

## toolbar.jsp {#toolbar-jsp}

toolbar.jsp에는 색상 있는 도구 모음을 만드는 코드가 포함되어 있습니다. 도구 모음을 제거하려면 HTML.jsp에서 toolbar.jsp를 제거합니다.

## formBody.jsp {#formbody-jsp}

formBody.jsp 모듈은 XFA 양식의 HTML 표현을 위한 것입니다.

## nav_footer.jsp {#nav-footer-jsp}

처음에는 양식의 첫 페이지만 HTML5 형식으로 렌더링합니다. 사용자가 양식을 스크롤하면 나머지 양식이 로드됩니다. 로딩 경험이 더욱 빨라집니다. nav_footer.jsp 구성 요소에는 스크롤 시 페이지 로드를 용이하게 하는 데 필요한 모든 스타일과 요소가 포함되어 있습니다.

## footer.jsp {#footer-jsp}

footer.jsp 모듈은 비어 있습니다. 사용자 상호 작용에만 사용되는 스크립트를 추가할 수 있습니다.

## 사용자 지정 프로필 만들기 {#creating-custom-profiles}

사용자 정의 프로파일을 만들려면 다음 단계를 수행하십시오.

### 프로필 노드 {#create-profile-node} 만들기

1. URL의 CRX DE 인터페이스로 이동합니다.`https://'[server]:[port]'/crx/de` 관리자 자격 증명을 사용하여 인터페이스에 로그인합니다.

1. 왼쪽 창에서 */content/xfaforms/profiles* 위치로 이동합니다.

1. 노드 기본값을 복사하고 이름이 *hrform*&#x200B;인 다른 폴더(*/content/profiles*)에 노드를 붙여 넣습니다.

1. 새 노드 *hrform*&#x200B;을 선택하고 문자열 속성을 추가합니다.*sling:resourceType* 값:*hrform/demo*.

1. 도구 모음 메뉴에서 모두 저장을 클릭하여 변경 사항을 저장합니다.

### 프로필 렌더러 스크립트 {#create-the-profile-renderer-script} 만들기

사용자 정의 프로파일을 만든 후 이 프로파일에 렌더링 정보를 추가합니다. 새 프로파일에 대한 요청을 받을 때 CRX는 렌더링할 JSP 페이지에 대한 /apps 폴더가 있는지 확인합니다. /apps 폴더에 JSP 페이지를 만듭니다.

1. 왼쪽 창에서 `/apps` 폴더로 이동합니다.
1. `/apps` 폴더를 마우스 오른쪽 단추로 클릭하고 이름이 **hrform**&#x200B;인 폴더를 만들도록 선택합니다.
1. **hrform** 폴더에 **demo**&#x200B;라는 폴더를 만듭니다.
1. **모두 저장** 단추를 클릭합니다.
1. `/libs/xfaforms/profile/html.jsp`으로 이동하여 노드 **html.jsp**&#x200B;를 복사합니다.
1. **html.jsp** 노드를 동일한 이름 **html.jsp**&#x200B;으로 위에 만든 `/apps/hrform/demo` 폴더에 붙여 넣고 **저장**&#x200B;을 클릭합니다.
1. 프로필 스크립트의 다른 구성 요소가 있는 경우 1-6단계를 수행하여 /apps/hrform/demo 폴더에 있는 구성 요소를 복사합니다.

1. 프로필이 만들어졌는지 확인하려면 URL `https://'[server]:[port]'/content/xfaforms/profiles/hrform.html`을 엽니다.

양식을 확인하려면 [로컬 파일 시스템에서 AEM Forms으로 양식](/help/forms/using/get-xdp-pdf-documents-aem.md)을 가져오고 AEM 서버 작성자 인스턴스에서 양식](/help/forms/using/previewing-forms.md)을 미리 봅니다.[
