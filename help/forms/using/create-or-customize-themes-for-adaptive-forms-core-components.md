---
title: 적응형 양식 테마를 만들거나 사용자 지정하는 방법
description: BEM 사양을 사용하여 적응형 Forms 핵심 구성 요소에 대한 테마를 만들거나 사용자 지정하는 방법에 대해 알아봅니다
keywords: 적응형 양식 핵심 구성 요소 테마 만들기, 새 테마 만들기, 테마 맞춤화, 새 테마 업로드, 양식에서 테마 사용, 테마 삭제, AEM 6.5 양식에서 테마 만들기
contentOwner: Khushwant Singh
topic-tags: Adaptive Forms
docset: aem65
role: Admin, Developer
exl-id: 9f9b35a3-0479-4179-9fad-994a482c96b6
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '1933'
ht-degree: 6%

---

# 적응형 양식 테마 만들기 또는 사용자 지정 {#introduction-to-theme}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/using-themes-in-core-components.html) |
| AEM 6.5 | 이 문서 |


**적용 대상:** ✅ 양식 핵심 구성 요소 ❎ [적응형 양식 기초 구성 요소](/help/forms/using/themes.md).

AEM Forms 6.5에서 테마는 적응형 양식의 스타일(모양 및 느낌)을 정의하는 데 사용하는 AEM 클라이언트 라이브러리입니다. 테마에는 구성 요소 및 패널에 대한 스타일 지정 세부 사항이 포함되어 있습니다. 스타일에는 배경색, 상태 색상, 투명도, 정렬과 크기와 같은 속성이 포함됩니다. 테마를 적용하면 지정된 스타일은 해당 구성 요소에 반영됩니다. 테마는 적응형 양식에 대한 참조 없이 독립적으로 관리되며 여러 적응형 Forms에서 재사용할 수 있습니다.

## 사용 가능한 테마 {#available-theme}

AEM 6.5 환경은 적응형 Forms 기반의 핵심 구성 요소에 대해 아래에 나열된 테마를 제공합니다.

* [캔버스 테마](https://github.com/adobe/aem-forms-theme-canvas)
* [WKND 테마](https://github.com/adobe/aem-forms-theme-wknd)
* [이젤 테마](https://github.com/adobe/aem-forms-theme-easel)

## 테마 구조 이해 {#understanding-structure-of-theme}

테마는 CSS 파일, JavaScript 파일 및 적응형 Forms의 스타일을 정의하는 리소스(예: 아이콘)를 포함하는 패키지입니다. 적응형 양식 테마는 다음 구성 요소로 구성된 특정 조직을 따릅니다.

* `src/theme.scss`: 이 폴더에는 전체 테마에 광범위한 영향을 주는 CSS 파일이 포함되어 있습니다. 중앙 집중식 위치 역할을 하여 테마의 스타일 및 동작을 정의하고 관리할 수 있습니다. 이 파일을 편집하여 테마 전체에 공통으로 적용되는 변경 내용을 적용할 수 있으며, 이 변경 내용은 적응형 Forms 및 AEM Sites 페이지 모두의 모양 및 기능에 영향을 줍니다.

* `src/site`: 이 폴더에는 전체 AEM 사이트의 페이지에 적용되는 CSS 파일이 포함되어 있습니다. 이러한 파일은 AEM 사이트 페이지의 전체 기능 및 레이아웃에 영향을 주는 코드와 스타일로 구성됩니다. 여기서 수정한 사항은 사이트의 모든 페이지에 반영됩니다.

* `src/components`: 이 폴더의 CSS 파일은 개별 AEM 핵심 구성 요소용으로 설계되었습니다. 구성 요소의 각 전용 폴더에는 `.scss` 적응형 양식 내에서 특정 구성 요소의 스타일을 지정하는 파일입니다. 예: `/src/components/button/_button.scss` 파일에는 적응형 Forms 버튼 구성 요소에 대한 스타일 정보가 포함되어 있습니다.

  ![캔버스 테마 구조](/help/forms/using/assets/component-based-theme-folder-structure.png)

* `src/resources`: 이 폴더에는 아이콘, 로고 및 글꼴과 같은 정적 파일이 포함되어 있습니다. 이러한 리소스는 테마의 시각적 요소와 전반적인 디자인을 개선하는 데 사용됩니다.

## 테마 만들기

AEM Forms 6.5는 적응형 Forms 기반의 핵심 구성 요소에 대해 아래에 나열된 테마를 제공합니다.

* [캔버스 테마](https://github.com/adobe/aem-forms-theme-canvas)
* [WKND 테마](https://github.com/adobe/aem-forms-theme-wknd)
* [이젤 테마](https://github.com/adobe/aem-forms-theme-easel)

다음을 수행할 수 있습니다. [테마를 만들려면 다음 테마 중 하나를 맞춤화하십시오](#customize-a-theme-core-components).

## 테마 맞춤화 {#customize-a-theme-core-components-based-adaptive-forms}

테마 맞춤화란 테마의 모양을 수정하고 개인화하는 프로세스를 말합니다. 테마를 사용자 지정할 때 해당 디자인 요소, 레이아웃, 색상, 타이포그래피 및 경우에 따라 기본 코드가 변경됩니다. 이를 통해 테마가 제공하는 기본 구조와 기능을 유지하면서 웹 사이트 또는 애플리케이션에 고유하고 맞춤화된 디자인을 만들 수 있습니다.

>[!NOTE]
>
> * 패키지 관리자를 사용하여 모든 작성 및 게시 인스턴스에 테마를 배포할 수 있습니다.
> * 테마 클라이언트 라이브러리는 다른 패키지와 마찬가지로 패키지 관리자를 통해 가져오거나 내보냅니다.

### 테마를 맞춤화하기 위한 사전 요구 사항 {#prerequisites}

* [적응형 Forms 핵심 구성 요소 활성화](/help/forms/using/enable-adaptive-forms-core-components.md) 을 참조하십시오.

* 의 최신 릴리스 설치 [아파치 메이븐](https://maven.apache.org/download.cgi) Apache Maven은 Java™ 프로젝트에 일반적으로 사용되는 빌드 자동화 도구입니다. 최신 릴리스를 설치하면 테마 맞춤화에 필요한 종속성이 확보됩니다.

* 을(를) 만드는 방법 알아보기 [Adobe Experience Manager의 클라이언트 라이브러리](https://experienceleague.adobe.com/docs/experience-manager-65/developing/introduction/clientlibs.html). AEM은 클라이언트측 코드를 저장소에 저장하고, 범주로 구성하고, 각 코드 범주가 클라이언트에 제공되는 시기와 방법을 정의할 수 있는 클라이언트 라이브러리를 제공합니다.

* 일반 텍스트 편집기를 설치합니다. 예를 들어 Microsoft® Visual Studio Code입니다. Microsoft® 같은 일반 텍스트 편집기를 사용하면 Visual Studio Code에서 테마 파일을 편집하고 수정할 수 있는 사용자 친화적인 환경을 제공합니다.

* AEM Forms 환경이 실행 중인지 확인합니다.

### 테마 맞춤화를 위한 고려 사항 {#consideration}

* 다음을 사용하는지 확인합니다. [적응형 Forms 핵심 구성 요소를 활성화하는 데 사용되는 Archetype 프로젝트](/help/forms/using/enable-adaptive-forms-core-components.md) 을 추가하여 테마를 맞춤화할 수 있습니다.

* 적응형 양식을 게시할 때 클라이언트 라이브러리는 게시 인스턴스에 자동으로 게시되지 않습니다. 적응형 양식에서 참조된 클라이언트 라이브러리를 게시 환경에 수동으로 게시해야 합니다.

* Adobe은 클라이언트 라이브러리의 클래스 이름을 변경하지 않는 것을 권장합니다.

### 테마 맞춤화 {#customize-a-theme-core-components}

테마를 만들거나 사용자 지정하는 프로세스는 여러 단계입니다. 테마를 만들거나 맞춤화하려면 나열된 순서로 단계를 수행하십시오.

1. [테마 복제](#clone-git-repo-of-theme)
1. [테마 모양 사용자 지정](#customize-the-theme)
1. [로컬 배포용 테마 준비](#generate-the-clientlib)
1. [로컬 환경에 테마 배포](#deploy-the-theme-on-a-local-environment)
1. [프로덕션 환경에 테마 배포](#5-deploy-a-theme-on-your-production-environment)

<!--
 ![Theme Customization workflow](/help/forms/using/assets/custom-theme-steps.png)
-->

이 문서에 제공된 예제는 **캔버스** 테마를 선택할 수 있지만, 동일한 지침을 사용하여 모든 테마를 복제하고 맞춤화할 수 있습니다. 이러한 지침은 모든 테마에 적용되므로 특정 요구 사항에 따라 테마를 수정할 수 있습니다.

#### 1. 테마의 Git 저장소 복제 {#clone-git-repo-of-theme}

적응형 Forms 기반의 핵심 구성 요소에 대한 테마를 복제하려면 다음 테마 중 하나를 선택하십시오.

* [캔버스 테마](https://github.com/adobe/aem-forms-theme-canvas)
* [WKND 테마](https://github.com/adobe/aem-forms-theme-wknd)
* [이젤 테마](https://github.com/adobe/aem-forms-theme-easel)

테마를 복제하려면 다음 지침을 수행하십시오.

1. 로컬 개발 환경에서 명령 프롬프트 또는 터미널 창을 엽니다.

1. 실행 `git clone` 테마를 복제하는 명령.

   ```
      git clone [Path of Git Repository of the theme]
   ```

   바꾸기 [테마의 Git 저장소 경로] 해당 테마의 Git 저장소의 실제 URL 사용

   예를 들어 캔버스 테마를 복제하려면 다음 명령을 실행합니다.

   ```
      git clone https://github.com/adobe/aem-forms-theme-canvas
   ```

1. **상위 폴더에 있는 모든 파일의 작성자 신뢰**&#x200B;를 선택하고 **예, 작성자를 신뢰함**&#x200B;을 클릭합니다.

명령을 성공적으로 실행한 후에는 컴퓨터의 시스템에서 테마의 로컬 복사본을 사용할 수 있습니다.  `aem-forms-theme-canvas` 폴더를 삭제합니다.

#### 2. 테마 맞춤화 {#customize-the-theme}

개별 구성 요소를 사용자 정의하거나 테마의 전역 변수를 사용하여 테마 수준을 유연하게 변경할 수 있습니다. 전역 변수를 수정하면 모든 개별 구성 요소에 연쇄적으로 영향을 미칩니다. 예를 들어 전역 변수를 사용하여 적응형 양식 내에 있는 모든 구성 요소의 테두리 색상을 변경하거나 CTA(Call to Action) 버튼에 생생한 채우기 색상을 적용할 수 있습니다. 다음과 같은 작업을 수행할 수 있습니다.

* [테마 수준 스타일 설정](#theme-customization-global-level)

* [구성 요소 수준 스타일 설정](#component-based-customization)

##### 테마 수준 스타일 설정 {#theme-customization-global-level}

다음 `variable.scss` 파일에는 테마의 전역 변수가 포함되어 있습니다. 이러한 변수를 업데이트하여 테마 수준에서 스타일 관련 변경 사항을 적용할 수 있습니다. 테마 수준 스타일을 적용하려면 다음 단계를 수행합니다.

1. 를 엽니다. `<your-theme-sources>/src/site/_variables.scss` 편집할 파일입니다.
1. 모든 속성의 값을 변경합니다. 예를 들어 기본 오류 색상은 빨간색입니다. 오류 색상을 빨간색에서 파란색으로 변경하려면 `$error`변수를 채우는 방법에 따라 페이지를 순서대로 표시합니다. 예: `$error: #196ee5`

   ![예: 오류 색상이 파란색으로 설정됨](/help/forms/using/assets/theme-level-changes.png)

1. 파일을 저장하고 닫습니다.


마찬가지로 `variable.scss` 글꼴 모음 및 유형, 테마 및 글꼴 색상, 글꼴 크기, 테마 간격, 오류 아이콘, 테마 테두리 스타일 및 여러 적응형 양식 구성 요소에 영향을 주는 더 많은 변수를 설정할 파일입니다.

##### 구성 요소 수준 스타일 설정 {#component-based-customization}

또한 글꼴, 색상, 크기 및 단추, 확인란, 컨테이너, 바닥글 등과 같은 특정 적응형 양식 핵심 구성 요소의 기타 CSS 속성을 사용자 지정하는 옵션이 있습니다. 특정 구성 요소와 연결된 CSS 파일을 편집하여 해당 스타일을 조직의 브랜딩에 맞출 수 있습니다. 구성 요소의 스타일을 사용자 지정하려면 다음 단계를 따르십시오.

1. 파일 열기 `<your-theme-sources>/src/components/<component>/<component.scss>` 편집할 수 있습니다. 예를 들어 버튼 구성 요소의 글꼴 색상을 변경하려면 `<your-theme-sources>/src/components/button/button.scss`, 파일 을 참조하십시오.
1. 요구 사항에 따라 의 값을 변경합니다. 예를 들어, 마우스 오버 시 버튼 구성 요소의 색상을 녹색으로 변경하려면 의 값을 변경합니다. `color: $white` 의 속성 `cmp-adaptiveform-button__widget:hover` 클래스에서 16진수 코드 #12b453 또는 다른 녹색 음영으로 변환할 수 있습니다. 최종 코드는 다음과 같습니다.

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
1. 다음 위치로 이동 `<your-theme-sources>` 폴더를 삭제합니다. 예, `C:\aem-forms-theme-canvas`
1. 다음 명령을 실행합니다.

   ```
      npm run create-clientlib --category=adaptiveform.theme.[yourtheme]
   ```

   바꾸기 `[yourtheme]` (사용자 지정 테마 이름 포함) 예를 들어 사용자 지정 테마의 이름이 `customcanvastheme`, 다음 명령 실행

   ```
       npm run create-clientlib --category=adaptiveform.theme.customcanvastheme
   ```

   명령이 성공적으로 실행되면에 클라이언트 라이브러리 폴더가 만들어집니다. `themerepo\theme-clientlibs\[yourtheme]`.

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

로컬 개발 환경에서 테마를 성공적으로 테스트하면 작성 및 게시 인스턴스를 포함하여 프로덕션 환경에 테마를 배포할 수 있습니다. 다음 단계에 따라 프로덕션 환경에 테마를 배포합니다.

1. AEM 환경에 로그인합니다.
1. 패키지 관리자를 엽니다. 기본 URL은 `https://localhost:4502/crx/packmgr/index.jsp`.
1. 클릭 **패키지 업로드** 및 클릭 **찾아보기**.
1. 로 이동하여 선택 `[AEM Archetype Project Folder]\all\target[appid].all-[version].zip`. 클릭 **열기**.
1. 설치를 클릭합니다. 모든 프로덕션 환경에서 단계를 반복합니다.


패키지를 설치하면 테마를 선택할 수 있습니다.

![테마 클라이언트 라이브러리](/help/forms/using/assets/themeclientlibrary.png)

>[!NOTE]
>
>
> 패키지 관리자를 통해 패키지를 설치하기 위해 게시 인스턴스의 로그인 대화 상자에 액세스하는 데 문제가 발생하는 경우 다음 URL을 통해 로그인해 보십시오. `http://[Publish Server URL]:[PORT]/system/console`. 이렇게 하면 게시 인스턴스에 로그인할 수 있으므로 설치 프로세스를 진행할 수 있습니다.

## 적응형 양식에 테마 적용 {#using-theme-in-adaptive-form}

적응형 양식에 테마를 적용하는 단계는 다음과 같습니다.

1. 로컬 AEM 작성자 인스턴스에 로그인합니다.
1. Experience Manager 로그인 페이지에서 자격 증명을 입력합니다. 선택 **Adobe Experience Manager** > **Forms** > **Forms 및 문서**.
1. 클릭 **만들기** > **적응형 Forms**.
1. 적응형 Forms 핵심 구성 요소 템플릿을 선택하고 **다음**. 다음 **속성 추가** 표시
1. 다음을 지정합니다. **이름** 적응형 양식용.


   >[!NOTE]
   >
   > * 기본적으로 `adaptiveform.theme.canvas3` 테마를 선택했습니다.
   > * 다음에서 다른 테마를 선택할 수 있습니다. **테마 클라이언트 라이브러리** 드롭다운 메뉴.

1. **만들기**&#x200B;를 클릭합니다.

적응형 양식 테마는 적응형 양식을 작성하는 동안 스타일을 정의하는 적응형 양식 템플릿의 일부로 사용됩니다.

## 테마 삭제 {#delete-a-theme}

사용하지 않거나 원치 않는 테마를 제거하려면 다음을 수행하십시오.

1. 작성자 인스턴스에 로그인합니다.
1. 열기 `http://[Publish Server URL]:[PORT]/crx/de/index.jsp`
1. 다음으로 이동 `apps/[AEM Archetype Project Folder]/clientlibs/[yourtheme]`.
1. 테마 폴더를 삭제하고 변경 내용을 저장합니다.


## 자주 묻는 질문 {#faq}

**Q:** 글로벌 수준과 구성 요소 수준 모두에서 테마 폴더를 맞춤화할 때 우선 순위가 필요한 맞춤화는 무엇입니까?

**Ans:** 테마 및 구성 요소 수준 모두에서 스타일을 정의하면 구성 요소 수준에서 정의된 스타일이 우선합니다.

**Q:** 사용자 지정 테마가 다음에서 표시되지 않는 경우 수행할 단계 **[!UICONTROL 테마 클라이언트 라이브러리]**?

**Ans:**  사용자 지정 테마가 **[!UICONTROL 테마 클라이언트 라이브러리]** 드롭다운에서 다음 단계를 수행합니다.

1. 사용자 지정 테마 클라이언트 라이브러리를 추가한 위치로 이동합니다. 권장 경로는 다음과 같습니다. `/ui.apps/src/main/content/jcr_root/apps[AEM Archetype Project Folder]/clientlibs/<yourtheme>`.

1. 를 엽니다. `.content.xml` 파일을 만들고 다음 메타데이터를 포함합니다.

   ```
       formstheme:true
       allowproxy:true
   ```

1. 파일을 저장하고 테마를 다시 배포합니다.

## 참고 항목

* [핵심 구성 요소 기반 적응형 양식 만들기](create-an-adaptive-form-core-components.md)
* [규칙 편집기를 사용하여 양식에 동적 동작 추가](rule-editor.md)
* [적응형 Forms 기반의 핵심 구성 요소에 대한 테마 만들기 또는 사용자 지정](create-or-customize-themes-for-adaptive-forms-core-components.md)
* [적응형 Forms 기반의 핵심 구성 요소용 템플릿 만들기](template-editor.md)
* [AEM Sites 페이지 또는 경험 조각에 적응형 양식 만들기 또는 추가](create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [샘플 테마 템플릿 및 양식 데이터 모델](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html)
