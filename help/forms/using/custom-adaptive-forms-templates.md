---
title: 사용자 정의 응용 양식 템플릿 만들기
seo-title: 사용자 정의 응용 양식 템플릿 만들기
description: 이 문서에서는 사용자 정의 응용 양식 템플릿을 만드는 방법에 대해 설명합니다.
seo-description: 이 문서에서는 사용자 정의 응용 양식 템플릿을 만드는 방법에 대해 설명합니다.
uuid: 11b5f8cd-c56a-4525-97d5-1938ef5f183d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: affba49e-9712-4d29-858b-2f8ec4f2b1f1
docset: aem65
translation-type: tm+mt
source-git-commit: 4ecf5efc568cd21f11801a71d491c3d75ca367fe

---


# 사용자 정의 응용 양식 템플릿 만들기{#creating-a-custom-adaptive-form-template}

>[!NOTE]
>
>AEM Forms에서 동적 템플릿을 도입했습니다. AEM Sites 템플릿 편집기를 사용하여 동적 템플릿을 [만들거나 편집할 수 있습니다](../../forms/using/template-editor.md). 아래 문서에 언급된 템플릿은 정적 템플릿입니다. 기본 설치에서는 사용할 수 없습니다. [호환성 패키지를](../../forms/using/compatibility-package.md) 설치하여 환경에 이러한 템플릿을 사용할 수 있습니다.

## 전제 조건 {#prerequisites}

* AEM 페이지 [템플릿](/help/sites-authoring/templates.md) 및 [적응형 양식 작성 이해](https://helpx.adobe.com/aem-forms/6-1/introduction-forms-authoring.html)

* AEM 클라이언트측 [라이브러리 이해](/help/sites-developing/clientlibs.md)

## Adaptive form template {#adaptive-form-template}

적응형 양식 템플릿은 적응형 양식을 만드는 데 사용되는 특정 속성 및 컨텐츠 구조와 함께 특수 AEM 페이지 템플릿입니다. 템플릿에는 미리 구성된 레이아웃, 스타일 및 기본 초기 컨텐츠 구조가 있습니다.

양식을 만들면 원래 템플릿 컨텐츠 구조에 대한 변경 사항이 양식에 반영되지 않습니다.

## 기본 적응형 양식 템플릿 {#default-adaptive-form-templates}

AEM QuickStart는 다음과 같은 적응형 양식 템플릿을 제공합니다.

* 설문 조사 템플릿:여러 열이 구성된 응답형 레이아웃을 사용하여 단일 페이지 적응형 양식을 만들 수 있습니다. 레이아웃은 양식을 표시할 다양한 화면의 크기에 따라 자동으로 조정됩니다.
* 간단한 등록 템플릿:마법사 레이아웃을 사용하여 다단계 응용 양식을 만들 수 있습니다. 이 레이아웃에서는 마법사가 다음 단계로 진행하기 전에 검증한 각 단계에 대한 단계 완료 표현식을 지정할 수 있습니다.
* 탭 등록 템플릿:임의 순서로 탭을 방문할 수 있는 왼쪽 탭 레이아웃을 사용하여 다중 탭 적응형 양식을 만들 수 있습니다.
* 고급 등록 템플릿:여러 개의 탭과 마법사를 사용하여 양식을 만들 수 있습니다. 탭-왼쪽 레이아웃을 사용하여 원하는 순서대로 탭을 방문할 수 있습니다. 서명 및 확인을 위해 Adobe Document Cloud 디자인 서비스를 사용합니다.
* 빈 템플릿:머리글, 바닥글 및 초기 컨텐츠 없이 양식을 만들 수 있습니다. 텍스트 상자, 단추 및 이미지와 같은 구성 요소를 추가할 수 있습니다. 빈 템플릿을 사용하면 AEM 사이트 페이지에 [포함할 수 있는 양식을 만들 수 있습니다](/help/forms/using/embed-adaptive-form-aem-sites.md).

이러한 템플릿에는 해당 페이지 구성 요소로 설정된 `sling:resourceType` 속성이 있습니다. 페이지 구성 요소는 적응형 양식 컨테이너가 포함된 CQ 페이지를 렌더링하여 적응형 양식을 렌더링합니다.

다음 표에서는 템플릿과 페이지 구성 요소 간의 연결을 열거합니다.

<table>
 <tbody>
  <tr>
   <td><p><strong>템플릿</strong></p> </td>
   <td><p><strong>페이지 구성 요소</strong></p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/af/templates/surveyTemplate</p> </td>
   <td><p>/libs/fd/af/components/page/survey</p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/af/templates/simpleEnrollmentTemplate</p> </td>
   <td><p>/libs/fd/af/components/page/base</p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/af/templates/tabbedEnrollmentTemplate</p> </td>
   <td><p>/libs/fd/af/components/page/tabbedenrollment</p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/afaddon/templates/advancedEnrollmentTemplate</p> </td>
   <td><p>/libs/fd/afaddon/components/page/advanced롤링</p> </td>
  </tr>
 </tbody>
</table>

## 템플릿 편집기를 사용하여 적응형 양식 템플릿 만들기 {#creating-an-adaptive-form-template-using-template-editor}

템플릿 편집기를 사용하여 적응형 양식의 구조와 초기 컨텐츠를 지정할 수 있습니다. 예를 들어, 모든 양식 작성자가 등록 양식에 텍스트 상자, 탐색 단추 및 제출 단추를 몇 개 포함하도록 할 수 있습니다. 작성자가 다른 등록 양식과 일치하는 양식을 만드는 데 사용할 수 있는 템플릿을 만들 수 있습니다. AEM 템플릿 편집기를 사용하여 다음을 수행할 수 있습니다.

* 구조 레이어에 양식의 머리글 및 바닥글 구성 요소 추가
* 양식의 초기 컨텐츠를 제공합니다.
* 테마를 지정합니다.
* 전송, 재설정 및 탐색과 같은 작업을 지정합니다.

자세한 내용은 템플릿 [편집기를 참조하십시오](../../forms/using/template-editor.md).

## CRXDE에서 적응형 양식 템플릿 만들기 {#creating-an-adaptive-form-template-from-crxde}

사용 가능한 템플릿을 사용하는 대신 템플릿을 만들어 적응형 양식을 만들 수 있습니다. 사용자 지정 템플릿은 적응형 양식 컨테이너 및 머리글 및 바닥글과 같은 페이지 요소를 참조하는 다양한 페이지 구성 요소를 기반으로 합니다.

웹 사이트의 기본 페이지 구성 요소를 사용하여 이러한 구성 요소를 만들 수 있습니다. 또는 기본 템플릿에서 사용하는 적응형 양식의 페이지 구성 요소를 확장할 수 있습니다.

simpleRegistrationTemplate과 같은 사용자 지정 템플릿을 만들려면 다음 단계를 수행하십시오.

1. 작성 인스턴스에서 CRXDE Lite로 이동합니다.

1. /apps 디렉토리에서 응용 프로그램의 폴더 구조를 만듭니다. 예를 들어 애플리케이션 이름이 mycompany인 경우 이 이름으로 폴더를 만듭니다. 일반적으로 응용 프로그램 폴더에는 구성 요소, 구성, 템플릿, src 및 설치 디렉토리가 포함됩니다. 이 예에서는 구성 요소, 구성 및 템플릿 폴더를 만듭니다.

1. /libs/fd/af/templates 폴더로 이동합니다.
1. 노드를 `simpleEnrollmentTemplate` 복사합니다.
1. /apps/mycompany/templates 폴더로 이동합니다. 마우스 오른쪽 버튼을 클릭하고 붙여넣기를 **[!UICONTROL 선택합니다]**.
1. 필요한 경우 복사한 템플릿 노드의 이름을 변경합니다. 예를 들어 등록 템플릿으로 이름을 변경합니다.

1. /apps/mycompany/templates/registration-template 위치로 이동합니다.

1. 노드에 대한 `jcr:title` 및 `jcr:description` 속성을 수정하여 `jcr:content` 템플릿을 복사한 템플릿과 구별합니다.

1. 수정된 템플릿의 `jcr:content` 노드에는 `guideContainer` 및 `guideformtitle` 구성 요소가 포함됩니다. `guideContainer` 는 적응형 양식을 포함하는 컨테이너입니다. 구성 `guideformtitle` 요소에는 애플리케이션 이름, 설명 등이 표시됩니다.

   대신 `guideformtitle`사용자 지정 구성 요소나 `parsys` 구성 요소를 포함할 수 있습니다. 예를 들어 사용자 지정 구성 요소나 구성 요소 노드를 `guideformtitle`제거하고 `parsys` 추가합니다. 구성 요소의 `sling:resourceType` 속성이 구성 요소를 참조하고 페이지 `component.jsp` 파일에서 동일한지 확인합니다.

1. /apps/mycompany/templates/enrollment-template/jcr:content 위치로 이동합니다.

1. 속성 **[!UICONTROL 탭을]** `cq:designPath` 열고 속성 값을 /etc/designs/mycompany로 변경합니다.

1. 이제 `cq:Page` 유형에 대해 /etc/designs/mycompany 노드를 만듭니다.

## 적응형 양식 페이지 구성 요소 만들기 {#create-an-adaptive-form-page-component}

템플릿은 페이지 구성 요소 /libs/fd/af/components/page/base를 참조하므로 사용자 지정 템플릿과 기본 스타일이 동일합니다. /apps/mycompany/templates/enrollment-template/jcr:content 노드에 `sling:resourceType` 정의된 속성으로 구성 요소 참조를 찾을 수 있습니다. 베이스는 핵심 제품 구성 요소이므로 이 구성 요소를 수정하지 마십시오.

1. /apps/mycompany/templates/regulation-template/jcr:content 노드로 이동하고 속성 값을 /apps/mycompany/components/page/enrolentpage `sling:resourceType` 로 수정합니다.
1. /libs/fd/af/components/page/base 노드를 /apps/mycompany/components/page 폴더에 복사합니다.

1. 복사된 구성 요소의 이름을 다음으로 `enrollmentpage`변경합니다.

1. **(이미 컨텐츠 페이지가 있는 경우에만 해당)** 웹 사이트에 대한 기존 `contentpage`구성 요소가 있는 경우 다음 단계(a-d)를 수행합니다. 웹 사이트에 대한 기존 `contentpage`구성 요소가 없는 경우 `resourceSuperType`속성을 그대로 두고 OOTB 기본 페이지를 가리킬 수 있습니다.

   1. 노드의 경우 `enrollmentpage` 속성 값을 mycompany/components/page/contentpage `sling:resourceSuperType` 로 설정합니다. 구성 `contentpage` 요소는 사이트의 기본 페이지 구성 요소입니다. 다른 페이지 구성 요소는 확장할 수 있습니다. 및 `enrollmentpage`를 제외한 `head.jsp`아래의 스크립트 파일을 `content.jsp`제거합니다 `library.jsp`. 이 경우 `sling:resourceSuperType` 구성 요소에 `contentpage` 이러한 모든 스크립트가 포함됩니다. 탐색 막대와 바닥글을 포함한 머리글은 `contentpage` 구성 요소에서 상속됩니다.

   1. Open the file `head.jsp`.

      JSP 파일에는 라인이 들어 `<cq.include script="library.jsp"/>`있습니다.

      이 `library.jsp` 파일에는 응용 양식에 대한 스타일이 들어 있는 `guide.theme.simpleEnrollment` 클라이언트 라이브러리가 포함되어 있습니다.

      페이지 구성 요소에는 `enrollmentpage` 구성 요소의 `head.jsp` 파일을 무시하는 전용 `head.jsp` 파일이 있습니다 `contentpage` .

   1. 구성 요소에 대한 `head.jsp` 파일의 모든 스크립트를 `contentpage` 구성 요소의 `head.jsp` `enrollmentpage` 파일에 포함합니다.
   1. 이 `content.jsp` 스크립트에서는 페이지 렌더링 시 포함된 다른 구성 요소에 페이지 컨텐츠나 참조를 추가할 수 있습니다. 예를 들어 사용자 정의 구성 요소를 추가하는 경우 JSP 파일의 구성 요소에 다음 참조를 `applicationformheader`추가해야 합니다.

      `<cq:include path="applicationformheader" resourceType="mycompany/components/applicationformheader"/>`

      마찬가지로 템플릿 노드 구조에 구성 요소를 추가하는 경우 사용자 지정 구성 요소도 포함합니다. `parsys`

## 응용 양식 클라이언트 라이브러리 만들기 {#creating-an-adaptive-form-client-library}

새 템플릿의 구성 요소 `head.jsp` 파일에는 클라이언트 라이브러리가 포함되어 `enrollmentpage` `guide.theme.simpleEnrollment`있습니다. 기본 템플릿은 이 클라이언트 라이브러리도 사용합니다. 다음 방법 중 하나를 사용하여 새 템플릿의 스타일을 변경합니다.

* 사용자 정의 테마를 정의하고 기본 테마를 사용자 정의 `guide.theme.simpleEnrollment` 테마로 바꿉니다.
* /etc/designs/mycompany 아래에 새 클라이언트 라이브러리를 정의합니다. jsp 페이지의 기본 테마 항목 뒤에 클라이언트 라이브러리를 포함합니다. 이 클라이언트 라이브러리에 재정의된 모든 스타일과 추가 Java Script 파일을 포함합니다.

>[!NOTE]
>
>테마는 적응형 양식을 렌더링하는 데 사용되는 페이지 구성 요소에 포함된 클라이언트 라이브러리를 나타냅니다. 클라이언트 라이브러리는 주로 적응형 양식의 모양을 제어합니다.

