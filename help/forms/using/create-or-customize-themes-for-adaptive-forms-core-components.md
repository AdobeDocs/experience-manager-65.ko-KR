---
title: 적응형 양식 테마를 만들거나 사용자 지정하는 방법
description: BEM 사양을 사용하여 적응형 Forms 핵심 구성 요소에 대한 테마를 만들거나 사용자 지정하는 방법에 대해 알아봅니다
keywords: 적응형 양식 핵심 구성 요소 테마 만들기, 새 테마 만들기, 테마 맞춤화, 새 테마 업로드, 양식에서 테마 사용, 테마 삭제, AEM 6.5 양식에서 테마 만들기
contentOwner: Khushwant Singh
topic-tags: Adaptive Forms
docset: aem65
role: Admin, Developer
feature: Adaptive Forms,Core Components
exl-id: 9f9b35a3-0479-4179-9fad-994a482c96b6
solution: Experience Manager, Experience Manager Forms
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1939'
ht-degree: 5%

---

# 적응형 양식 테마 만들기 또는 사용자 지정 {#introduction-to-theme}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/using-themes-in-core-components.html) |
| AEM 6.5 | 이 문서 |


<!--**Applies to:** ✅ Adaptive Form Core Components ❎ [Adaptive Form Foundation Components](/help/forms/using/create-adaptive-form.md).-->

AEM Forms 6.5에서 테마는 적응형 양식의 스타일(모양 및 느낌)을 정의하는 데 사용하는 AEM 클라이언트 라이브러리입니다. 테마에는 구성 요소 및 패널에 대한 스타일 지정 세부 사항이 포함되어 있습니다. 스타일에는 배경색, 상태 색상, 투명도, 정렬과 크기와 같은 속성이 포함됩니다. 테마를 적용하면 지정된 스타일은 해당 구성 요소에 반영됩니다. 테마는 적응형 양식에 대한 참조 없이 독립적으로 관리되며 여러 적응형 Forms에서 재사용할 수 있습니다.

## 사용 가능한 테마 {#available-theme}

AEM 6.5 환경은 적응형 Forms 기반의 핵심 구성 요소에 대해 아래에 나열된 테마를 제공합니다.

* [캔버스 테마](https://github.com/adobe/aem-forms-theme-canvas)
* [WKND 테마](https://github.com/adobe/aem-forms-theme-wknd)
* [이젤 테마](https://github.com/adobe/aem-forms-theme-easel)
* [FSI 테마](https://github.com/adobe/aem-forms-theme-fsi)
* [의료 테마](https://github.com/adobe/aem-forms-theme-healthcare)
* [공개 테마](https://github.com/adobe/aem-forms-theme-public)
* [제조 테마](https://github.com/adobe/aem-forms-theme-manufacturing)

## 테마 구조 이해 {#understanding-structure-of-theme}

테마는 CSS 파일, JavaScript 파일 및 적응형 Forms의 스타일을 정의하는 리소스(예: 아이콘)를 포함하는 패키지입니다. 적응형 양식 테마는 다음 구성 요소로 구성된 특정 조직을 따릅니다.

* `src/theme.scss`: 이 폴더에는 전체 테마에 광범위한 영향을 주는 CSS 파일이 포함되어 있습니다. 중앙 집중식 위치 역할을 하여 테마의 스타일 및 동작을 정의하고 관리할 수 있습니다. 이 파일을 편집하여 테마 전체에 공통으로 적용되는 변경 내용을 적용할 수 있으며, 이 변경 내용은 적응형 Forms 및 AEM Sites 페이지 모두의 모양 및 기능에 영향을 줍니다.

* `src/site`: 이 폴더에는 전체 AEM 사이트의 페이지에 적용되는 CSS 파일이 포함되어 있습니다. 이러한 파일은 AEM 사이트 페이지의 전체 기능 및 레이아웃에 영향을 주는 코드와 스타일로 구성됩니다. 여기서 수정한 사항은 사이트의 모든 페이지에 반영됩니다.

* `src/components`: 이 폴더의 CSS 파일은 개별 AEM 핵심 구성 요소용으로 디자인되었습니다. 구성 요소의 각 전용 폴더에는 적응형 양식 내에서 특정 구성 요소를 스타일링하는 `.scss` 파일이 포함되어 있습니다. 예를 들어 `/src/components/button/_button.scss` 파일에는 적응형 Forms 단추 구성 요소에 대한 스타일 정보가 포함되어 있습니다.

  ![캔버스 테마 구조](/help/forms/using/assets/component-based-theme-folder-structure.png)

* `src/resources`: 이 폴더에는 아이콘, 로고 및 글꼴과 같은 정적 파일이 포함되어 있습니다. 이러한 리소스는 테마의 시각적 요소와 전반적인 디자인을 개선하는 데 사용됩니다.

## 테마 만들기

AEM Forms 6.5는 적응형 Forms 기반의 핵심 구성 요소에 대해 아래에 나열된 테마를 제공합니다.

* [캔버스 테마](https://github.com/adobe/aem-forms-theme-canvas)
* [WKND 테마](https://github.com/adobe/aem-forms-theme-wknd)
* [이젤 테마](https://github.com/adobe/aem-forms-theme-easel)
* [공개 테마](https://github.com/adobe/aem-forms-theme-public)
* [제조 테마](https://github.com/adobe/aem-forms-theme-manufacturing)

[이러한 테마를 맞춤화하여 테마를 만들 수 있습니다](#customize-a-theme-core-components).

## 테마 맞춤화 {#customize-a-theme-core-components-based-adaptive-forms}

테마 맞춤화란 테마의 모양을 수정하고 개인화하는 프로세스를 말합니다. 테마를 사용자 지정할 때 해당 디자인 요소, 레이아웃, 색상, 타이포그래피 및 경우에 따라 기본 코드가 변경됩니다. 이를 통해 테마가 제공하는 기본 구조와 기능을 유지하면서 웹 사이트 또는 애플리케이션에 고유하고 맞춤화된 디자인을 만들 수 있습니다.

>[!NOTE]
>
> * 패키지 관리자를 사용하여 모든 작성자 및 Publish 인스턴스에 테마를 배포할 수 있습니다.
> * 테마 클라이언트 라이브러리는 다른 패키지와 마찬가지로 패키지 관리자를 통해 가져오거나 내보냅니다.

### 테마를 맞춤화하기 위한 사전 요구 사항 {#prerequisites}

* 환경에 대해 [적응형 Forms 핵심 구성 요소 사용](/help/forms/using/enable-adaptive-forms-core-components.md).

* [Apache Maven의 최신 릴리스를 설치하십시오.](https://maven.apache.org/download.cgi) Apache Maven은 일반적으로 Java™ 프로젝트에 사용되는 빌드 자동화 도구입니다. 최신 릴리스를 설치하면 테마 맞춤화에 필요한 종속성이 확보됩니다.

* Adobe Experience Manager[&#128279;](https://experienceleague.adobe.com/docs/experience-manager-65/developing/introduction/clientlibs.html)에서 클라이언트 라이브러리를 만드는 방법을 알아봅니다. AEM은 클라이언트측 코드를 저장소에 저장하고, 범주로 구성하고, 각 코드 범주가 클라이언트에 제공되는 시기와 방법을 정의할 수 있는 클라이언트 라이브러리를 제공합니다.

* 일반 텍스트 편집기를 설치합니다. 예를 들어 Microsoft® Visual Studio Code입니다. Microsoft® 같은 일반 텍스트 편집기를 사용하면 Visual Studio Code에서 테마 파일을 편집하고 수정할 수 있는 사용자 친화적인 환경을 제공합니다.

* AEM Forms 환경이 실행 중인지 확인합니다.

### 테마 맞춤화를 위한 고려 사항 {#consideration}

* [환경에서 적응형 Forms 핵심 구성 요소](/help/forms/using/enable-adaptive-forms-core-components.md)를 활성화하는 데 사용되는 Archetype 프로젝트를 사용하여 테마를 맞춤화하는지 확인하십시오.

* 적응형 양식을 게시할 때 클라이언트 라이브러리는 Publish 인스턴스에 자동으로 게시되지 않습니다. 적응형 양식에서 참조된 클라이언트 라이브러리를 Publish 환경에 수동으로 게시해야 합니다.

* Adobe은 클라이언트 라이브러리의 클래스 이름을 변경하지 않는 것을 권장합니다.

### 테마 맞춤화 {#customize-a-theme-core-components}

테마를 만들거나 사용자 지정하는 프로세스는 여러 단계입니다. 테마를 만들거나 맞춤화하려면 나열된 순서로 단계를 수행하십시오.

1. [테마 복제](#clone-git-repo-of-theme)
1. [테마 모양 사용자 지정](#customize-the-theme)
1. [로컬 배포에 대한 테마 준비](#generate-the-clientlib)
1. [로컬 환경에 테마 배포](#deploy-the-theme-on-a-local-environment)
1. [프로덕션 환경에 테마 배포](#5-deploy-a-theme-on-your-production-environment)

<!--
 ![Theme Customization workflow](/help/forms/using/assets/custom-theme-steps.png)
-->

문서에 제공된 예제는 **캔버스** 테마를 기반으로 하지만 동일한 지침을 사용하여 모든 테마를 복제하고 사용자 지정할 수 있습니다. 이러한 지침은 모든 테마에 적용되므로 특정 요구 사항에 따라 테마를 수정할 수 있습니다.

#### 1. 테마의 Git 저장소 복제 {#clone-git-repo-of-theme}

적응형 Forms 기반의 핵심 구성 요소에 대한 테마를 복제하려면 다음 테마 중 하나를 선택하십시오.

* [캔버스 테마](https://github.com/adobe/aem-forms-theme-canvas)
* [WKND 테마](https://github.com/adobe/aem-forms-theme-wknd)
* [이젤 테마](https://github.com/adobe/aem-forms-theme-easel)

테마를 복제하려면 다음 지침을 수행하십시오.

1. 로컬 개발 환경에서 명령 프롬프트 또는 터미널 창을 엽니다.

1. `git clone` 명령을 실행하여 테마를 복제합니다.

   ```
      git clone [Path of Git Repository of the theme]
   ```

   테마의 Git 저장소의 [경로]을(를) 테마의 해당 Git 저장소의 실제 URL로 바꿉니다.

   예를 들어 캔버스 테마를 복제하려면 다음 명령을 실행합니다.

   ```
      git clone https://github.com/adobe/aem-forms-theme-canvas
   ```

1. **상위 폴더에 있는 모든 파일의 작성자 신뢰**&#x200B;를 선택하고 **예, 작성자를 신뢰함**&#x200B;을 클릭합니다.

명령을 성공적으로 실행한 후에는 `aem-forms-theme-canvas` 폴더의 컴퓨터에서 테마의 로컬 복사본을 사용할 수 있습니다.

#### 2. 테마 맞춤화 {#customize-the-theme}

개별 구성 요소를 사용자 정의하거나 테마의 전역 변수를 사용하여 테마 수준을 유연하게 변경할 수 있습니다. 전역 변수를 수정하면 모든 개별 구성 요소에 연쇄적으로 영향을 미칩니다. 예를 들어 전역 변수를 사용하여 적응형 양식 내에 있는 모든 구성 요소의 테두리 색상을 변경하거나 CTA(Call to Action) 버튼에 생생한 채우기 색상을 적용할 수 있습니다. 다음과 같은 작업을 수행할 수 있습니다.

* [테마 수준 스타일 설정](#theme-customization-global-level)

* [구성 요소 수준 스타일 설정](#component-based-customization)

##### 테마 수준 스타일 설정 {#theme-customization-global-level}

`variable.scss` 파일에 테마의 전역 변수가 포함되어 있습니다. 이러한 변수를 업데이트하여 테마 수준에서 스타일 관련 변경 사항을 적용할 수 있습니다. 테마 수준 스타일을 적용하려면 다음 단계를 수행합니다.

1. 편집할 `<your-theme-sources>/src/site/_variables.scss` 파일을 엽니다.
1. 모든 속성의 값을 변경합니다. 예를 들어 기본 오류 색상은 빨간색입니다. 오류 색상을 빨간색에서 파란색으로 변경하려면 `$error` 변수의 색상 16진수 코드를 변경합니다. 예: `$error: #196ee5`

   ![예: 파란색으로 설정된 오류 색상](/help/forms/using/assets/theme-level-changes.png)

1. 파일을 저장하고 닫습니다.


마찬가지로 `variable.scss` 파일을 사용하여 글꼴 모음과 문자, 테마와 글꼴 색상, 글꼴 크기, 테마 간격, 오류 아이콘, 테마 테두리 스타일 및 여러 적응형 양식 구성 요소에 영향을 주는 더 많은 변수를 설정할 수 있습니다.

##### 구성 요소 수준 스타일 설정 {#component-based-customization}

또한 글꼴, 색상, 크기 및 단추, 확인란, 컨테이너, 바닥글 등과 같은 특정 적응형 양식 핵심 구성 요소의 기타 CSS 속성을 사용자 지정하는 옵션이 있습니다. 특정 구성 요소와 연결된 CSS 파일을 편집하여 해당 스타일을 조직의 브랜딩에 맞출 수 있습니다. 구성 요소의 스타일을 사용자 지정하려면 다음 단계를 따르십시오.

1. 편집할 `<your-theme-sources>/src/components/<component>/<component.scss>` 파일을 엽니다. 예를 들어 단추 구성 요소의 글꼴 색을 변경하려면 `<your-theme-sources>/src/components/button/button.scss`, 파일 을 엽니다.
1. 요구 사항에 따라 의 값을 변경합니다. 예를 들어 마우스 가리키기 시 단추 구성 요소의 색상을 녹색으로 변경하려면 `cmp-adaptiveform-button__widget:hover` 클래스의 `color: $white` 속성 값을 16진수 코드 #12b453 또는 다른 녹색 음영으로 변경합니다. 최종 코드는 다음과 같습니다.

   ```
    .cmp-adaptiveform-button__widget:hover {
    background: $dark-gray;
    color: #12b453;
    }
   ```


1. 파일을 저장하고 닫습니다.

<!--

   ![Example: Hover color set to green](/help/forms/using/assets/button-customization.png)

-->

>[!NOTE]
>
> 스타일이 테마와 구성 요소 수준에서 모두 정의되면 구성 요소 수준에서 정의된 스타일이 우선합니다.

#### 3. 배포할 테마 준비 {#generate-the-clientlib}

AEM 인스턴스에 테마를 배포하려면 클라이언트 라이브러리로 변환해야 합니다. 테마를 클라이언트 라이브러리로 변환하려면 다음 단계를 따르십시오.

1. 명령 프롬프트 또는 터미널 창을 엽니다.
1. `<your-theme-sources>` 폴더로 이동합니다. 예, `C:\aem-forms-theme-canvas`
1. 다음 명령을 실행합니다.

   ```
      npm run create-clientlib --category=adaptiveform.theme.[yourtheme]
   ```

   `[yourtheme]`을(를) 사용자 지정 테마 이름으로 바꾸십시오. 예를 들어 사용자 지정 테마의 이름이 `customcanvastheme`인 경우 다음 명령을 실행합니다

   ```
       npm run create-clientlib --category=adaptiveform.theme.customcanvastheme
   ```

   명령을 성공적으로 실행하면 클라이언트 라이브러리 폴더가 `themerepo\theme-clientlibs\[yourtheme]`에 만들어집니다.

   ![클라이언트 라이브러리 생성](/help/forms/using/assets/clientlib_created.png)


   ![클라이언트 라이브러리 위치](/help/forms/using/assets/adaptiveform.theme.easel.png)

#### 4. 로컬 환경에 테마 배포 {#deploy-the-theme-on-a-local-environment}

테마를 로컬 개발 또는 테스트 환경에 배포하려면 다음 단계를 따르십시오.

1. 이전 섹션에서 만든 클라이언트 라이브러리를 다음 경로의 Archetype 프로젝트에 복사합니다.

   `/ui.apps/src/main/content/jcr_root/apps/[AEM Archetype Project Folder]/clientlibs/<yourtheme>`

1. 명령 프롬프트 또는 터미널을 엽니다.
1. 적응형 양식 핵심 구성 요소를 활성화하는 데 사용되는 프로젝트인 AEM Archetype 프로젝트의 루트 디렉토리로 이동합니다.
1. 다음 명령을 실행하여 환경에 사용자 지정 테마를 배포합니다.

   `mvn clean install`

   ![클라이언트 라이브러리 빌드](/help/forms/using/assets/mvndeploy.png)

<!--

#### 5. Test the theme with a local Adaptive Form {#test-the-theme-with-a-local-adaptive-form}

To apply and test the customized theme with an Adaptive Form:

**Apply theme while creating an Adaptive Form**

1. Log in to your AEM Forms author instance. 

1. Select **Adobe Experience Manager** > **Forms** > **Forms & Documents**.

1. Click **Create** > **Adaptive Forms**. The wizard for creating Adaptive Form opens.

1. Select the core component template in the **Source** tab.
1. Select the theme in the **Style** tab.
1. Click **Create**.

An Adaptive Form with the selected theme is created. 

**Apply theme to an existing Adaptive Form**

1. Log in to your AEM Forms author instance. 

1. Select **Adobe Experience Manager** > **Forms** > **Forms & Documents**.

1. Select an Adaptive Form and click Properties. 

1. For the **Theme Client Library** option, select the theme. 

1. Click **Save & Close**.

The selected theme is applied to the Adaptive Form. 
-->

#### 5. 프로덕션 환경에 테마 배포 {#deploy-theme}

로컬 개발 환경에서 테마를 성공적으로 테스트하면 작성 및 Publish 인스턴스를 모두 포함하여 프로덕션 환경에 테마를 배포할 수 있습니다. 다음 단계에 따라 프로덕션 환경에 테마를 배포합니다.

1. AEM 환경에 로그인합니다.
1. 패키지 관리자를 엽니다. 기본 URL은 `https://localhost:4502/crx/packmgr/index.jsp`입니다.
1. **패키지 업로드**&#x200B;를 클릭하고 **찾아보기**&#x200B;를 클릭합니다.
1. `[AEM Archetype Project Folder]\all\target[appid].all-[version].zip`(으)로 이동하여 선택합니다. **열기**&#x200B;를 클릭합니다.
1. 설치를 클릭합니다. 모든 프로덕션 환경에서 단계를 반복합니다.


패키지를 설치하면 테마를 선택할 수 있습니다.

![테마 클라이언트 라이브러리](/help/forms/using/assets/themeclientlibrary.png)

>[!NOTE]
>
>
> 패키지 관리자를 통해 패키지를 설치하기 위해 게시 인스턴스의 로그인 대화 상자에 액세스하는 데 문제가 발생하는 경우 다음 URL을 통해 로그인해 보십시오. `http://[Publish Server URL]:[PORT]/system/console`. 이렇게 하면 Publish 인스턴스에 로그인할 수 있으므로 설치 프로세스를 진행할 수 있습니다.

## 적응형 양식에 테마 적용 {#using-theme-in-adaptive-form}

적응형 양식에 테마를 적용하는 단계는 다음과 같습니다.

1. 로컬 AEM 작성자 인스턴스에 로그인합니다.
1. Experience Manager 로그인 페이지에서 자격 증명을 입력합니다. **Adobe Experience Manager** > **Forms** > **Forms 및 문서**&#x200B;를 선택합니다.
1. **만들기** > **적응형 Forms**&#x200B;을 클릭합니다.
1. 적응형 Forms 핵심 구성 요소 템플릿을 선택하고 **다음**&#x200B;을(를) 클릭합니다. **속성 추가**&#x200B;가 나타납니다.
1. 적응형 양식에 대해 **이름**&#x200B;을(를) 지정하십시오.


   >[!NOTE]
   >
   > * 기본적으로 `adaptiveform.theme.canvas3` 테마가 선택되어 있습니다.
   > * **테마 클라이언트 라이브러리** 드롭다운 메뉴에서 다른 테마를 선택할 수 있습니다.

1. **만들기**&#x200B;를 클릭합니다.

적응형 양식 테마는 적응형 양식을 작성하는 동안 스타일을 정의하는 적응형 양식 템플릿의 일부로 사용됩니다.

## 테마 삭제 {#delete-a-theme}

사용하지 않거나 원치 않는 테마를 제거하려면 다음을 수행하십시오.

1. 작성자 인스턴스에 로그인합니다.
1. `http://[Publish Server URL]:[PORT]/crx/de/index.jsp` 열기
1. 다음으로 이동 `apps/[AEM Archetype Project Folder]/clientlibs/[yourtheme]`.
1. 테마 폴더를 삭제하고 변경 내용을 저장합니다.


## 자주 묻는 질문 {#faq}

**Q:** 글로벌 수준과 구성 요소 수준 모두에서 테마 폴더를 사용자 지정할 때 우선 순위가 높은 사용자 지정은 무엇입니까?

**Ans:** 테마와 구성 요소 수준 모두에서 스타일이 정의된 경우 구성 요소 수준에서 정의된 스타일이 우선합니다.

**Q:** 사용자 지정 테마가 **[!UICONTROL 테마 클라이언트 라이브러리]**&#x200B;에 표시되지 않으면 어떤 단계를 수행해야 합니까?

**Ans:** 사용자 지정 테마가 **[!UICONTROL 테마 클라이언트 라이브러리]** 드롭다운에 나타나지 않는 경우 다음 단계를 수행하십시오.

1. 사용자 지정 테마 클라이언트 라이브러리를 추가한 위치로 이동합니다. 권장 경로는 `/ui.apps/src/main/content/jcr_root/apps[AEM Archetype Project Folder]/clientlibs/<yourtheme>`입니다.

1. `.content.xml` 파일을 열고 다음 메타데이터를 포함합니다.

   ```
       formstheme:true
       allowproxy:true
   ```

1. 파일을 저장하고 테마를 다시 배포합니다.

## 추가 참조

* [핵심 구성 요소 기반 적응형 양식 만들기](create-an-adaptive-form-core-components.md)
* [규칙 편집기를 사용하여 양식에 동적 동작 추가](rule-editor.md)
* [적응형 Forms 기반의 핵심 구성 요소에 대한 테마 만들기 또는 사용자 지정](create-or-customize-themes-for-adaptive-forms-core-components.md)
* [적응형 Forms 기반의 핵심 구성 요소용 템플릿 만들기](template-editor.md)
* [AEM Sites 페이지 또는 경험 조각에 적응형 양식 만들기 또는 추가](create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [샘플 테마 템플릿 및 양식 데이터 모델](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html)
