---
title: 사용자 지정 적응형 양식 테마 만들기
seo-title: Creating custom adaptive form themes
description: 적응형 양식 테마는 적응형 양식의 스타일(모양 및 느낌)을 정의하는 데 사용하는 AEM 클라이언트 라이브러리입니다. 사용자 정의 적응형 양식 테마를 만드는 방법을 알아봅니다.
seo-description: An adaptive form theme is an AEM client library that you use to define the styles (look and feel) for an adaptive form. Learn how you can create custom adaptive form themes.
uuid: b25df10e-b07c-4e9d-a799-30f1c6fb3c44
content-type: reference
topic-tags: customization
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 437e6581-4eb1-4fbd-a6da-86b9c90cec89
exl-id: 73b0057f-082d-4502-90e2-5e41b52c1185
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 0%

---

# 사용자 지정 적응형 양식 테마 만들기 {#creating-custom-adaptive-form-themes}

>[!CAUTION]
>
>AEM Forms은 [테마 편집기](/help/forms/using/themes.md) 적응형 양식 작성 및 수정 기능 [테마](/help/forms/using/themes.md). 가 없는 버전에서 업그레이드한 경우에만 이 문서에 나열된 단계를 수행하십시오 [테마 편집기](/help/forms/using/themes.md) 또한 Less/CSS 파일(사전 테마 편집기 방법)을 사용하여 만든 테마에 대한 기존 투자를 이용할 수 있습니다.

## 사전 요구 사항 {#prerequisites}

* LESS(Leaner CSS) 프레임워크에 대한 지식
* Adobe Experience Manager에서 클라이언트 라이브러리를 만드는 방법
* [적응형 양식 템플릿 만들기](/help/forms/using/custom-adaptive-forms-templates.md) 사용자가 만드는 테마 사용

## 적응형 양식 테마 {#adaptive-form-theme}

An **적응형 양식 테마** 적응형 양식의 스타일(모양 및 느낌)을 정의하는 데 사용하는 AEM 클라이언트 라이브러리입니다.

을(를) 만듭니다 **적응형 템플릿** 테마를 템플릿에 적용합니다. 그런 다음 이 사용자 지정 템플릿을 사용하여 **적응형 양식**.

![적응형 양식 및 클라이언트 라이브러리](assets/hierarchy.png)

## 적응형 양식 테마를 만들려면 {#to-create-an-adaptive-form-theme}

>[!NOTE]
>
>다음 절차는 노드, 속성 및 폴더와 같은 AEM 객체의 샘플 이름을 사용하여 설명합니다.
>
>이름을 사용하여 이러한 단계를 수행하면 결과 템플릿이 다음 스냅샷과 유사하게 나타납니다.

![포리스트 테마 응용 양식 스냅숏](assets/thumbnail.png)
**그림:** *포리스트 테마 샘플*

1. 유형의 노드 만들기 `cq:ClientLibraryFolder` 아래에 `/apps`노드 아래에 있어야 합니다.

   예를 들어 다음 노드를 만듭니다.

   `/apps/myAfThemes/forestTheme`

1. 여러 값을 갖는 문자열 속성 추가 `categories` 로 값을 설정하고 해당 값을 적절하게 설정합니다.

   예를 들어 속성을 다음과 같이 설정합니다. `af.theme.forest`.

   ![CRX 저장소 스냅샷](assets/3-2.png)

1. 폴더 두 개 추가, `less` 및 `css`, 및 파일 `css.txt` 1단계에서 생성된 노드에 대한 내용은 다음과 같습니다.

   * `less` 폴더: 다음 포함 `less` 사용자가 정의하는 변수 파일 `less` 변수와 `less mixins` .css 스타일을 관리하는 데 사용됩니다.

      이 폴더는 `less` 변수 파일, `less` mixin 파일, `less` mixin 및 변수를 사용하여 스타일을 정의하는 파일입니다. 그리고 이러한 적은 파일은 모두 style.less로 가져옵니다.

   * `css`폴더: 테마에 사용할 정적 스타일을 정의하는 .css 파일을 포함합니다.

   **변수 파일 감소**: CSS 스타일을 정의하는 데 사용되는 변수를 정의하거나 재정의하는 파일입니다.

   적응형 양식은 다음 .less 파일에 정의된 OOTB 변수를 제공합니다.

   * `/apps/clientlibs/fd/af/guidetheme/common/less/globalvariables.less`
   * `/apps/clientlibs/fd/af/guidetheme/common/less/layoutvariables.less`

   적응형 양식은 다음에 정의된 타사 변수를 제공합니다.

   `/apps/clientlibs/fd/af/third-party/less/variables.less`

   적응형 양식에 제공된 변수를 적게 사용하거나, 이러한 변수를 재정의하거나, 새로운 변수를 덜 만들 수 있습니다.

   >[!NOTE]
   >
   >덜 적은 사전 프로세서의 파일을 가져오는 동안 가져오기 문에서 파일의 상대 경로를 지정합니다.

   변수 대체 샘플:

   ```css
   @button-background-color: rgb(19, 102, 44);
   @button-border-color: rgb(19, 102, 44);
   @button-border-size: 0px;
   @button-padding: 10px 15px;
   @button-font-color: #ffffff;
   ```

   를 재정의하려면 `less`변수:

   1. 기본 적응형 양식 변수 가져오기:

      `/apps/clientlibs/fd/af/guidetheme/common/less/globalvariables.less/apps/clientlibs/fd/af/guidetheme/common/less/layoutvariables.less`

   1. 그런 다음 재정의된 변수를 포함하는 파일을 적게 가져옵니다.

   샘플 새 변수 정의:

   ```css
   @button-focus-bg-color: rgb(40, 208, 90);
   @button-hover-bg-color: rgb(30, 156, 67);
   ```

   **작은 혼합 파일:** 변수를 인수로 허용하는 함수를 정의할 수 있습니다. 이러한 함수의 결과는 결과 스타일입니다. CSS 스타일을 반복하지 않으려면 다른 스타일 내에서 이러한 mixin을 사용하십시오.

   적응형 양식은 에 정의된 OOTB 믹싱을 제공합니다.

   * `/apps/clientlibs/fd/af/guidetheme/common/less/adaptiveforms-mixins.less`

   적응형 양식은 다음에 정의된 타사 Mixin도 제공합니다.

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

   **Styles.less 파일:** 이 파일을 사용하여 클라이언트 라이브러리에서 사용해야 하는 파일(변수, mixin, 스타일)이 모두 적습니다.

   다음 샘플에서 `styles.less` 파일에서 가져오기 문은 순서에 관계없이 배치할 수 있습니다.

   다음 .less 파일을 가져올 문은 필수입니다.

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

   다음 `css.txt` 라이브러리에 대해 다운로드할 .css 파일의 경로를 포함합니다.

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
   >style.less 파일은 필수가 아닙니다. 즉, 사용자 지정 스타일, 변수 또는 mixin을 정의하지 않은 경우에는 이 파일을 만들 필요가 없습니다.
   >
   >그러나 style.less 파일을 만들지 않는 경우 css.txt 파일에서 다음 줄의 주석을 해제해야 합니다.
   >
   >**`#base=less`**
   >
   >그리고 다음 줄에 주석을 답니다.
   >
   >**`styles.less`**

## 적응형 양식에서 테마를 사용하려면 {#to-use-a-theme-in-an-adaptive-form}

적응형 양식 테마를 만든 후 다음 단계를 수행하여 이 테마를 적응형 양식으로 사용합니다.

1. 에서 만든 테마를 포함하려면 [적응형 양식 테마를 만들려면](/help/forms/using/creating-custom-adaptive-form-themes.md#p-to-create-an-adaptive-form-theme-p) 섹션, 유형의 사용자 지정 페이지 만들기 `cq:Component`.

   예, `/apps/myAfCustomizations/myAfPages/forestPage`

   1. 추가 `sling:resourceSuperType` 속성을 설정하고 해당 값을 `fd/af/components/page/base`.

      ![CRX 저장소 스냅샷](assets/1-2.png)

   1. 페이지에서 테마를 사용하려면 override file library.jsp를 노드에 추가해야 합니다.

      그런 다음 이 문서의 적응형 양식 테마 섹션을 만들려면

      다음 샘플 코드 조각은 `af.theme.forest` 테마.

      ```jsp
      <%@include file="/libs/fd/af/components/guidesglobal.jsp"%>
      <cq:includeClientLib categories="af.theme.forest"/>
      ```

   1. **선택 사항입니다**: 사용자 지정 페이지에서 필요에 따라 header.jsp, footer.jsp 및 body.jsp를 재정의합니다.

1. 사용자 지정 템플릿을 만듭니다(예: `/apps/myAfCustomizations/myAfTemplates/forestTemplate`jcr:content가 이전 단계에서 만든 사용자 지정 페이지를 가리키는 ). 예를 들어 `myAfCustomizations/myAfPages/forestPage)`.

   ![CRX 저장소 스냅샷](assets/2-1.png)

1. 이전 단계에서 만든 템플릿을 사용하여 적응형 양식을 만듭니다. 적응형 양식의 모양과 느낌은 이 문서의 적응형 양식 테마 섹션을 만들려면
