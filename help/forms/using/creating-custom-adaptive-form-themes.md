---
title: 사용자 정의 적응형 양식 테마 만들기
seo-title: 사용자 정의 적응형 양식 테마 만들기
description: 적응형 양식 테마는 적응형 양식의 스타일(모양 및 느낌)을 정의하는 데 사용하는 AEM 클라이언트 라이브러리입니다. 사용자 정의 적응형 양식 테마를 만드는 방법을 알아봅니다.
seo-description: 적응형 양식 테마는 적응형 양식의 스타일(모양 및 느낌)을 정의하는 데 사용하는 AEM 클라이언트 라이브러리입니다. 사용자 정의 적응형 양식 테마를 만드는 방법을 알아봅니다.
uuid: b25df10e-b07c-4e9d-a799-30f1c6fb3c44
content-type: reference
topic-tags: customization
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 437e6581-4eb1-4fbd-a6da-86b9c90cec89
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '825'
ht-degree: 0%

---


# 사용자 정의 응용 양식 테마 만들기 {#creating-custom-adaptive-form-themes}

>[!CAUTION]
>
>AEM Forms은 응용 양식 [테마](/help/forms/using/themes.md)을 만들고 수정하는 [테마 편집기](/help/forms/using/themes.md) 기능을 제공합니다. [테마 편집기](/help/forms/using/themes.md)가 없는 버전에서 업그레이드했으며 Less/CSS 파일(사전 테마 편집기 방법)을 사용하여 만든 테마에 대한 기존 투자가 있는 경우에만 이 문서에 나열된 단계를 수행하십시오.

## 전제 조건 {#prerequisites}

* LESS(Leaner CSS) 프레임워크에 대한 지식
* Adobe Experience Manager에서 클라이언트 라이브러리를 만드는 방법
* [만든 테마를 ](/help/forms/using/custom-adaptive-forms-templates.md) 사용하기 위한 응용 양식 템플릿 만들기

## 적응형 양식 테마 {#adaptive-form-theme}

**적응형 양식 테마**&#x200B;는 적응형 양식의 스타일(모양과 느낌)을 정의하는 데 사용하는 AEM 클라이언트 라이브러리입니다.

**적응형 템플릿**&#x200B;을 만들고 테마를 템플릿에 적용합니다. 그런 다음 이 사용자 지정 템플릿을 사용하여 **적응형 양식**&#x200B;을 만듭니다.

![적응형 양식 및 클라이언트 라이브러리](assets/hierarchy.png)

## 응용 양식 테마 {#to-create-an-adaptive-form-theme}을(를) 만들려면

>[!NOTE]
>
>다음 절차는 노드, 속성 및 폴더와 같은 AEM 객체의 샘플 이름을 사용하여 설명합니다.
>
>이름을 사용하여 이러한 단계를 수행하면 결과 템플릿이 다음 스냅샷과 유사하게 나타납니다.

![포리스트 테마 응용 양식 ](assets/thumbnail.png)
**스냅샷 그림:** *포리스트 테마 샘플*

1. `/apps` 노드 아래에 `cq:ClientLibraryFolder` 유형의 노드를 만듭니다.

   예를 들어 다음 노드를 만듭니다.

   `/apps/myAfThemes/forestTheme`

1. 다중값 문자열 속성 `categories`을 노드에 추가하고 값을 적절하게 설정합니다.

   예를 들어 속성을 다음으로 설정합니다.`af.theme.forest`.

   ![CRX 저장소 스냅샷](assets/3-2.png)

1. 1단계에서 만든 노드에 `less` 및 `css` 폴더 2개와 `css.txt` 파일을 추가합니다.

   * `less` 폴더:변수를 정의하는  `less` 변수  `less` 및 .css 스타일을 관리하는 데  `less mixins` 사용되는 변수 파일을 포함합니다.

      이 폴더는 믹서와 변수를 사용하여 스타일을 정의하는 `less` 변수 파일, `less` mixin 파일, `less` 파일로 구성됩니다. 이러한 모든 파일을 styles.less로 가져옵니다.

   * `css`폴더:테마에 사용할 정적 스타일을 정의하는 .css 파일이 포함되어 있습니다.

   **적은 변수 파일**:CSS 스타일 정의에 사용되는 변수를 정의하거나 재정의하는 파일입니다.

   적응형 양식은 다음 .less 파일에 정의된 OOTB 변수를 제공합니다.

   * `/apps/clientlibs/fd/af/guidetheme/common/less/globalvariables.less`
   * `/apps/clientlibs/fd/af/guidetheme/common/less/layoutvariables.less`

   적응형 양식은 다음에 정의된 제3자 변수를 제공합니다.

   `/apps/clientlibs/fd/af/third-party/less/variables.less`

   적응형 양식에서 제공되는 더 적은 변수를 사용하거나, 이러한 변수를 재정의하거나, 더 적은 새 변수를 만들 수 있습니다.

   >[!NOTE]
   >
   >덜 이전의 프로세서를 가져오는 동안 import 문에서 파일의 상대 경로를 지정합니다.

   변수 재정의 샘플:

   ```css
   @button-background-color: rgb(19, 102, 44);
   @button-border-color: rgb(19, 102, 44);
   @button-border-size: 0px;
   @button-padding: 10px 15px;
   @button-font-color: #ffffff;
   ```

   `less`변수를 재정의하려면:

   1. 기본 적응형 양식 변수 가져오기:

      `/apps/clientlibs/fd/af/guidetheme/common/less/globalvariables.less/apps/clientlibs/fd/af/guidetheme/common/less/layoutvariables.less`

   1. 그런 다음 재정의된 변수가 포함된 파일을 더 적게 가져옵니다.

   새 변수 정의 샘플:

   ```css
   @button-focus-bg-color: rgb(40, 208, 90);
   @button-hover-bg-color: rgb(30, 156, 67);
   ```

   **파일 혼합 감소: 변수를 인수로** 허용하는 함수를 정의할 수 있습니다. 이러한 함수의 출력은 결과 스타일입니다. CSS 스타일을 반복하지 않도록 서로 다른 스타일 내에서 이러한 혼합을 사용합니다.

   적응형 양식은 다음에 정의된 OOTB 믹스를 제공합니다.

   * `/apps/clientlibs/fd/af/guidetheme/common/less/adaptiveforms-mixins.less`

   적응형 양식은 다음에 정의된 제3자 혼합도 제공합니다.

   * `/apps/clientlibs/fd/af/third-party/less/mixins.less`

   샘플 혼합 정의:

   ```css
   .rounded-corners (@radius) {
     -webkit-border-radius: @radius;
     -moz-border-radius: @radius;
     -ms-border-radius: @radius;
     -o-border-radius: @radius;
     border-radius: @radius;
   }
   
   .border(@color, @type, @size) {
      border: @color @size @type;
   }
   ```

   **Styles.less File:** 이 파일을 사용하여 클라이언트 라이브러리에 사용해야 하는 모든 파일(변수, 혼합, 스타일)을 포함할 수 있습니다.

   다음 샘플 `styles.less` 파일에서 import 문을 임의의 순서대로 배치할 수 있습니다.

   다음 .less 파일을 가져오는 명령문은 필수입니다.

   * `globalvariables.less`
   * `layoutvariables.less`
   * `components.less`
   * `layouts.less`

   ```css
   @import "../../../clientlibs/fd/af/guidetheme/common/less/globalvariables.less";
   @import "../../../clientlibs/fd/af/guidetheme/common/less/layoutvariables.less";
   @import "forestTheme-variables";
   @import "../../../clientlibs/fd/af/guidetheme/common/less/components.less";
   @import "../../../clientlibs/fd/af/guidetheme/common/less/layouts.less";
   
   /* custom styles */
   
   .guidetoolbar {
     input[type="button"], button, .button {
       .rounded-corners (@button-radius);
       &:hover {
         background-color: @button-hover-bg-color;
       }
       &:focus {
         background-color: @button-focus-bg-color;
       }
     }
   }
   
   form {
       background-image: url(../images/forest.png);
    background-repeat: no-repeat;
    background-size: 100%;
   }
   ```

   `css.txt`에는 라이브러리에 대해 다운로드할 .css 파일 경로가 포함되어 있습니다.

   예:

   ```javascript
   #base=/apps/clientlibs/fd/af/third-party/css
   bootstrap.css
   
   #base=less
   styles.less
   
   #base=/apps/clientlibs/fd/xfaforms/xfalib/css
   datepicker.css
   listboxwidget.css
   scribble.css
   dialog.css
   ```

   >[!NOTE]
   >
   >styles.less 파일은 필수가 아닙니다. 즉, 사용자 정의 스타일, 변수 또는 혼합을 정의하지 않은 경우 이 파일을 만들 필요가 없습니다.
   >
   >그러나 style.less 파일을 만들지 않으면 css.txt 파일에서 다음 줄의 주석을 해제해야 합니다.
   >
   >**`#base=less`**
   >
   >그리고 다음 줄에 주석을 설정합니다.
   >
   >**`styles.less`**

## 적응형 양식 {#to-use-a-theme-in-an-adaptive-form}에서 테마를 사용하려면

적응형 양식 테마를 만든 후 다음 단계를 수행하여 적응형 양식으로 이 테마를 사용합니다.

1. [에서 만든 테마를 포함시켜 적응형 양식 테마](/help/forms/using/creating-custom-adaptive-form-themes.md#p-to-create-an-adaptive-form-theme-p) 섹션을 만들려면 `cq:Component` 유형의 사용자 지정 페이지를 만듭니다.

   예, `/apps/myAfCustomizations/myAfPages/forestPage`

   1. `sling:resourceSuperType` 속성을 추가하고 해당 값을 `fd/af/components/page/base`로 설정합니다.

      ![CRX 저장소 스냅샷](assets/1-2.png)

   1. 페이지에서 테마를 사용하려면 override file library.jsp를 노드에 추가해야 합니다.

      그런 다음 이 아티클의 적응형 양식 테마 섹션을 만들려면 [만들기]에서 만든 테마를 가져옵니다.

      다음 샘플 코드 조각은 `af.theme.forest` 테마를 가져옵니다.

      ```jsp
      <%@include file="/libs/fd/af/components/guidesglobal.jsp"%>
      <cq:includeClientLib categories="af.theme.forest"/>
      ```

   1. **옵션**:사용자 지정 페이지에서 필요에 따라 header.jsp, footer.jsp 및 body.jsp를 재정의합니다.

1. 사용자 정의 템플릿을 만듭니다(예:jcr:content가 이전 단계에서 만든 사용자 정의 페이지를 가리키는 `/apps/myAfCustomizations/myAfTemplates/forestTemplate`)(예:`myAfCustomizations/myAfPages/forestPage)`.

   ![CRX 저장소 스냅샷](assets/2-1.png)

1. 이전 단계에서 만든 템플릿을 사용하여 적응형 양식을 만듭니다. 적응형 양식의 모양과 느낌은 이 아티클의 적응형 양식 테마 섹션을 만들려면

