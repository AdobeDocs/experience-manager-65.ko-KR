---
title: 적응형 양식을 만드는 방법
seo-title: Learn how to create a Core Components based Adaptive Form on AEM 6.5 Forms.
description: 을 사용하여 적응형 양식을 만드는 방법 알아보기 [!DNL Experience Manager Forms]. 적응형 Forms은 정보 수집 및 처리를 간소화하는 반응형 HTML 5 양식입니다. 양식 데이터 모델 및 XML 또는 JSON 스키마를 기반으로 적응형 양식을 만드는 방법에 대해 자세히 알아보십시오.
seo-description: Learn how to create an Adaptive Form using [!DNL Experience Manager Forms]. Adaptive Forms are responsive HTML5 forms that streamline information gathering and processing. Dig deeper on how to create an Adaptive Form based on a Form Data Model and XML or JSON schema.
Keywords: create adaptive form core component, create core component based adaptive form, creare adaptive form
products: SG_EXPERIENCEMANAGER/6.5/FORMS
contentOwner: Khushwant Singh
topic-tags: Adaptive Forms
docset: aem65
role: Admin, Developer
source-git-commit: daf97f3d5c5f3c92ff5caeccff583e54f3f57364
workflow-type: tm+mt
source-wordcount: '1869'
ht-degree: 4%

---


# 핵심 구성 요소 기반 적응형 양식 만들기 {#creating-an-adaptive-form-core-components}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM 6.5 | 이 문서 |
| AEM as a Cloud Service | [여기를 클릭하십시오.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form-core-components.html) |

적응형 양식을 사용하여 멋지고, 반응이 빠르고, 동적이고, 적응력이 뛰어난 양식을 만들 수 있습니다. AEM Forms은 적응형 Forms을 신속하게 만들 수 있는 비즈니스 사용자 친화적 UI를 제공합니다. UI에서는 사전 구성된 템플릿, 스타일, 필드 및 제출 옵션을 손쉽게 선택하여 적응형 양식을 만들 수 있는 빠른 탭 탐색 기능을 제공합니다.

시작하기 전에 사용 가능한 Forms 구성 요소 유형에 대해 알아보십시오.

* [적응형 Forms 핵심 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ko): 표준화된 데이터 캡처 구성 요소입니다. 이러한 구성 요소는 사용자 지정 기능, 개발 시간 단축 및 디지털 등록 환경에 대한 유지 관리 비용 절감을 제공합니다. 개발자는 이러한 구성 요소를 손쉽게 맞춤화하고 스타일을 지정할 수 있습니다. Adobe은 이러한 현대적이고 확장 가능한 구성 요소를 활용하여 적응형 Forms을 개발할 것을 권장합니다.

* [적응형 Forms Foundation 구성 요소](creating-adaptive-form.md): 클래식(이전) 데이터 캡처 구성 요소입니다. 적응형 양식 기반의 기존 기초 구성 요소를 편집하는 데 계속 사용할 수 있습니다. Adobe 양식을 만드는 경우 다음을 사용하는 것이 좋습니다.  [적응형 Forms 핵심 구성 요소](/help/forms/using/create-adaptive-form.md) 를 클릭하여 적응형 Forms을 만듭니다.

## 전제 조건

적응형 양식을 만들려면 다음 항목이 필요합니다.

* **환경에 맞는 적응형 Forms 핵심 구성 요소 활성화**: AEM Archetype 프로젝트 버전 41 이상은 다음 경우에 필요합니다. [환경에 맞는 핵심 구성 요소 활성화](/help/forms/using/enable-adaptive-forms-core-components.md). 환경에 대한 핵심 구성 요소 활성화 시 **적응형 Forms(핵심 구성 요소)** 템플릿 및 캔버스 테마가 환경에 추가됩니다.

* **적응형 양식 템플릿**: 템플릿은 기본 구조를 제공하고 적응형 양식의 모양(레이아웃 및 스타일)을 정의합니다. 여기에는 특정 속성 및 콘텐츠 구조를 포함하는 미리 형식이 지정된 구성 요소가 있습니다. 또한 테마 및 제출 액션을 정의하는 옵션을 제공합니다. 테마는 모양과 느낌을 정의하고 제출 작업은 적응형 양식 제출 시 수행할 작업을 정의합니다. (예: 수집된 데이터를 데이터 소스로 전송) 템플릿 이름: `blank` 지원되는 OOTB:

   * 다음 `blank` 템플릿은 모든 최신 AEM Forms 온-프레미스 및 AMS 환경에 포함됩니다.
   * 패키지 관리자를 통해 참조 패키지를 설치하여 `blank` AEM Forms 온-프레미스 및 AMS 환경에 대한 템플릿
   * 다음을 수행할 수도 있습니다. [새 적응형 Forms 템플릿(핵심 구성 요소) 만들기](template-editor.md) 처음부터.

  >[!NOTE]
  >
  > 없으시면, **적응형 Forms(핵심 구성 요소)** 사용자 환경의 템플릿, [환경에 맞는 적응형 Forms 핵심 구성 요소 활성화](/help/forms/using/enable-adaptive-forms-core-components.md). 환경에 대한 핵심 구성 요소 활성화 시 **적응형 Forms(핵심 구성 요소)** 템플릿이 환경에 추가됩니다.

* **적응형 양식 테마**: 테마에는 구성 요소 및 패널에 대한 스타일 세부 사항이 포함되어 있습니다. 스타일에는 배경색, 상태 색상, 투명도, 정렬 및 크기와 같은 속성이 포함됩니다. 테마를 적용하면 지정된 스타일이 해당 구성 요소에 반영됩니다.  다음 `Canvas` 환경에 대해 핵심 구성 요소를 활성화하면 기본적으로 테마가 추가됩니다. 다음을 수행할 수도 있습니다. [참조 테마 다운로드 및 사용자 지정](create-or-customize-themes-for-adaptive-forms-core-components.md).

* **권한**: 사용자 추가 [!DNL forms-users] 그룹입니다. 의 멤버 [!DNL forms-users] 그룹은 적응형 양식을 만들 수 있는 권한이 있습니다. 양식별 사용자 그룹의 자세한 목록은 [그룹 및 권한](forms-groups-privileges-tasks.md).

## 적응형 양식 만들기 {#create-an-adaptive-form}

1. 로컬 로그인 [AEM 작성자 인스턴스](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html?lang=en#author-and-publish-installs).

1. Experience Manager 로그인 페이지에 자격 증명을 입력합니다. 로그인 후 왼쪽 상단 모서리에서 을 누릅니다 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms 및 문서]**.

1. 누르기 **[!UICONTROL 만들기]**  > **[!UICONTROL 적응형 Forms 만들기]**.

1. 적응형 Forms 핵심 구성 요소 템플릿을 선택하고 **[!UICONTROL 다음]**.

1. 다음 **[!UICONTROL 속성 추가]** 가 표시됩니다. 다음 속성 필드에 대한 값을 지정합니다. 제목 및 이름 필드는 필수입니다.

   * **[!UICONTROL 제목:]** 양식의 표시 이름을 지정합니다. 제목을 통해 다음에서 양식을 식별할 수 있습니다. [!DNL Experience Manager Forms] 사용자 인터페이스.
   * **[!UICONTROL 이름:]** 양식 이름을 지정합니다. 지정된 이름의 노드가 저장소에 생성됩니다. 제목 입력을 시작하면 이름 필드에 대한 값이 자동으로 생성됩니다. 제안 값을 변경할 수 있습니다. 이름 필드에는 영숫자, 하이픈 및 밑줄만 포함할 수 있습니다.
   * **[!UICONTROL 설명:]** 양식에 대한 자세한 정보를 지정합니다.
   * **[!UICONTROL 테마 클라이언트 라이브러리]:** 적응형 양식의 테마를 지정합니다. 기본적으로 `adaptiveform.theme.canvas3` 테마를 선택했습니다. 에서 다른 테마를 선택할 수도 있습니다. **[!UICONTROL 테마 클라이언트 라이브러리]** 드롭다운 메뉴.
   * **[!UICONTROL 구성 컨테이너:]**  적응형 Forms에 대한 구성 파일이 저장되는 위치를 정의합니다. 이러한 구성 파일에는 적응형 Forms의 비헤이비어 및 모양과 관련된 설정 및 속성이 포함되어 있습니다.
   * **[!UICONTROL 태그:]** 적응형 양식을 고유하게 식별할 태그를 지정합니다. 태그는 양식 검색에 도움이 됩니다. 태그를 만들려면 **[!UICONTROL 태그]** 상자.
1. 누르기 **[!UICONTROL 만들기]**. 적응형 양식이 만들어지고 편집할 양식을 여는 대화 상자가 나타납니다.


1. 누르기 **[!UICONTROL 편집]** 새 탭에서 새로 만든 양식을 엽니다. 편집할 양식이 열리고 템플릿에서 사용할 수 있는 콘텐츠가 표시됩니다. 또한 새로 만든 양식을 사용자 지정할 수 있는 사이드바가 표시됩니다.


## 적응형 Forms 핵심 구성 요소를 사용하여 양식 만들기

편집할 양식을 연 후 사용 가능한 적응형 Forms 핵심 구성 요소를 사용하여 양식에 양식 필드를 추가할 수 있습니다. 드래그 앤 드롭하거나 +를 사용할 수 있습니다. [구성 요소 삽입] 이러한 구성 요소를 양식에 추가하는 옵션입니다. 사용 가능한 항목에 대한 자세한 내용은 AEM 핵심 구성 요소 설명서 를 참조하십시오 [적응형 Forms 핵심 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=en#components). 다음을 방문하실 수도 있습니다. [https://aemcomponents.dev/](https://aemcomponents.dev/) 사용 가능한 핵심 구성 요소 보기

## 적응형 양식에 대한 제출 액션 구성 {#configure-submit-action-for-form}

제출 액션을 사용하면 적응형 양식을 통해 캡처된 데이터 대상을 선택할 수 있습니다. 사용자가 적응형 양식에서 제출 단추를 클릭하면 트리거됩니다. 적응형 양식에는 즉시 사용 가능한 제출 액션이 포함됩니다. 기본 제출 액션을 확장하여 자신만의 사용자 지정 제출 액션을 만들 수도 있습니다. 양식에 대해 제출 액션을 구성하려면 다음 작업을 수행하십시오.

1. 콘텐츠 브라우저를 열고 다음을 선택합니다. **[!UICONTROL 가이드 컨테이너]** 적응형 양식의 구성 요소입니다.
1. 안내서 컨테이너 속성을 클릭합니다. ![안내서 속성](/help/forms/using/assets/configure-icon.svg) 아이콘. 적응형 양식 컨테이너 대화 상자가 열립니다.

1. 다음을 클릭합니다.  **[!UICONTROL 제출]** 탭.

   ![렌치 아이콘을 클릭하여 적응형 양식 컨테이너 대화 상자를 열고 제출 액션을 구성합니다](/help/forms/using/assets/adaptive-forms-submit-message.png)

1. 선택 및 구성 **[!UICONTROL 제출 액션]**&#x200B;을 참조하십시오. 제출 액션에 대한 자세한 내용은 [적응형 양식 제출 액션](/help/forms/using/configuring-submit-actions.md)

<!--
    
    ![Click the Wrench icon to open Adaptive Form Container dialog box to configure Data Models for the Adaptive Form Container component](/help/forms/assets/adaptive-forms-container.png)

-->

## 사용자를 페이지로 리디렉션하거나 양식 제출 시 감사 메시지 표시

양식을 제출할 때 사용자를 다른 웹 페이지나 메시지로 리디렉션할 수 있습니다. 사용자를 리디렉션하거나 감사 메시지를 구성하려면:

1. 콘텐츠 브라우저를 열고 다음을 선택합니다. **[!UICONTROL 가이드 컨테이너]** 적응형 양식의 구성 요소입니다.
1. 안내서 컨테이너 속성을 클릭합니다. ![안내서 속성](/help/forms/using/assets/configure-icon.svg) 아이콘. 적응형 양식 컨테이너 대화 상자가 열립니다.
1. 를 엽니다. **[!UICONTROL 제출]** 탭.

   ![렌치 아이콘을 클릭하여 적응형 양식 컨테이너 대화 상자를 열고 리디렉션 페이지 또는 감사 메시지를 구성합니다](/help/forms/using/assets/adaptive-forms-submit-message.png)

   * 리디렉션 URL을 구성하려면 제출 시 옵션에서 **[!UICONTROL URL로 리디렉션]** 옵션을 클릭하고 AEM Sites 페이지를 검색 및 선택하거나 외부 페이지의 URL을 입력합니다.

   * 사용자 정의 메시지 또는 감사 메시지를 구성하려면 제출 시 옵션을 선택합니다. **[!UICONTROL 메시지 표시]** 옵션을 선택한 다음 **[!UICONTROL 메시지 콘텐츠]** 상자. 서식 있는 텍스트 상자입니다. 전체 화면 옵션을 사용하여 사용 가능한 모든 서식 있는 텍스트 항목을 볼 수 있습니다.

## 적응형 양식에 대한 스키마 또는 양식 데이터 모델 구성 {#configure-schema-or-data-model-for-form}

양식 데이터 모델을 사용하여 사용자 작업에 따라 데이터를 보내고 받기 위해 양식을 데이터 소스에 연결할 수 있습니다. 양식을 JSON 스키마에 연결하여 사전 정의된 형식으로 제출된 데이터를 받을 수도 있습니다. 요구 사항에 따라 양식을 JSON 스키마 또는 양식 데이터 모델에 연결합니다.

* [JSON 스키마 만들기 및 환경에 업로드](/help/forms/using/adaptive-form-json-schema-form-model.md)
* [양식 데이터 모델 만들기](/help/forms/using/create-form-data-models.md)

### 양식에 대한 JSON 스키마 또는 양식 데이터 모델 구성

양식에 대해 JSON 스키마 또는 양식 데이터 모델을 구성하려면 다음 작업을 수행하십시오.

1. 콘텐츠 브라우저를 열고 다음을 선택합니다. **[!UICONTROL 가이드 컨테이너]** 적응형 양식의 구성 요소입니다.
1. 안내서 컨테이너 속성을 클릭합니다. ![안내서 속성](/help/forms/using/assets/configure-icon.svg) 아이콘. 적응형 양식 컨테이너 대화 상자가 열립니다.
1. 를 엽니다. **[!UICONTROL 데이터 모델]** 탭.

   ![렌치 아이콘을 클릭하여 적응형 양식 컨테이너 대화 상자를 열고 JSON 스키마 또는 양식 데이터 모델을 구성합니다.](/help/forms/using/assets/adaptive-forms-select-form-data-model-or-json-schema.png)

1. 요구 사항에 따라 JSON 스키마 또는 양식 데이터 모델을 선택하고 구성합니다.

   * 다음을 선택하면 **[!UICONTROL 양식 모델]** 옵션, 사용 **[!UICONTROL 양식 데이터 모델 선택]** 미리 구성된 양식 데이터 모델을 선택하는 옵션입니다.
   * 다음을 선택하면 **[!UICONTROL 스키마]** 옵션, 사용 **[!UICONTROL 스키마]** 양식에 대한 JSON 스키마를 선택하는 옵션입니다.

1. **[!UICONTROL 완료]**&#x200B;를 클릭합니다.

## 미리 채우기 서비스 구성  {#configure-prefill-service-for-form}

미리 채우기 서비스를 사용하여 기존 데이터를 사용하는 적응형 양식의 필드를 자동으로 채울 수 있습니다. 사용자가 양식을 열면 해당 필드의 값이 미리 채워집니다. 다음과 같은 작업을 수행할 수 있습니다.

* [사용자 지정 미리 채우기 서비스 만들기](/help/forms/using/prepopulate-adaptive-form-fields.md)
* [양식 데이터 모델 미리 채우기 서비스 사용](#fdm-prefill-service)

### 양식 데이터 모델 미리 채우기 서비스를 사용하여 적응형 양식의 필드를 미리 채웁니다 {#fdm-prefill-service}

양식 데이터 모델 미리 채우기 서비스를 사용하여 양식 데이터 모델이나 사용자 지정 미리 채우기 서비스를 사용하여 적응형 양식의 필드를 미리 채울 수 있습니다. 양식 데이터 모델 미리 채우기 서비스에서는 [구성된 양식 데이터 모델의 서비스 가져오기](work-with-form-data-model.md#add-data-model-objects-and-services-add-data-model-objects-and-services) 데이터를 검색합니다. 적응형 양식에 대해 양식 데이터 모델 미리 채우기 서비스를 사용하려면

1. 콘텐츠 브라우저를 열고 다음을 선택합니다. **[!UICONTROL 가이드 컨테이너]** 적응형 양식의 구성 요소입니다.
1. 안내서 컨테이너 속성을 클릭합니다. ![안내서 속성](/help/forms/using/assets/configure-icon.svg) 아이콘. 적응형 양식 컨테이너 대화 상자가 열립니다.
1. 적응형 양식 컨테이너 속성을 클릭합니다 ![적응형 양식 컨테이너 속성](/help/forms/using/assets/configure-icon.svg) 아이콘. 데이터 모델을 구성하는 적응형 양식 컨테이너 대화 상자가 열립니다.
   ![렌치 아이콘을 클릭하여 적응형 양식 컨테이너 대화 상자를 열고 리디렉션 페이지 또는 감사 메시지를 구성합니다](/help/forms/using/assets/adaptive-forms-container-prefill-service.png)
1. 양식 데이터 모델 선택. 를 엽니다. **[!UICONTROL 기본]** 탭. 미리 채우기 서비스에서 다음을 선택합니다. **[!UICONTROL 양식 데이터 모델 미리 채우기 서비스]**.
1. **[!UICONTROL 완료]**&#x200B;를 클릭합니다. 이제 적응형 양식이 양식 데이터 모델 미리 채우기를 사용하도록 구성되었습니다. 이제 다음을 사용할 수 있습니다. [규칙 편집기](rule-editor.md) 을 클릭하여 양식의 필드를 미리 채우는 규칙을 만듭니다.

## 적응형 양식의 양식 모델 속성 편집 {#edit-form-model}

1. 적응형 양식을 선택하고 을 누릅니다 ![페이지 정보](/help/forms/using/assets/configure-icon.svg) > **[!UICONTROL 속성 열기]**. 양식 속성 페이지가 열립니다.

1. 로 이동 **[!UICONTROL 양식 모델]** 을(를) 탭하고 양식 모델을 선택합니다. 적응형 양식에 양식 모델이 없는 경우 JSON 스키마 또는 양식 데이터 모델을 선택할 수 있습니다. 반면에 적응형 양식이 이미 양식 모델을 기반으로 하는 경우 동일한 유형의 다른 양식 모델로 전환할 수 있는 옵션이 있습니다. 예를 들어 양식이 JSON 스키마를 사용하는 경우 다른 JSON 스키마로 쉽게 전환할 수 있으며, 마찬가지로 양식이 양식 데이터 모델을 사용하는 경우 다른 양식 데이터 모델로 전환할 수 있습니다.

1. 누르기 **[!UICONTROL 저장]** 속성을 저장합니다.

## 다음 단계

* [규칙 편집기를 사용하여 양식에 동적 동작 추가](rule-editor.md)
* [적응형 Forms 기반의 핵심 구성 요소에 대한 테마 만들기 또는 사용자 지정](create-or-customize-themes-for-adaptive-forms-core-components.md)
* 적응형 Forms 기반의 핵심 구성 요소용 템플릿 만들기

## 참고 항목

* [핵심 구성 요소 기반 적응형 양식 만들기](create-an-adaptive-form-core-components.md)
* [AEM Sites 페이지 또는 경험 조각에 적응형 양식 만들기 또는 추가](create-or-add-an-adaptive-form-to-aem-sites-page.md)
