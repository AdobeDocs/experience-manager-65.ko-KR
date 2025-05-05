---
title: 양식 관리 소개
description: AEM Forms은 적응형 Forms 및 관련 에셋을 관리하는 도구를 제공합니다. 이 문서에서는 주요 양식 관리 기능 및 사용자 인터페이스 요소를 소개합니다.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager, introduction
docset: aem65
exl-id: 3e063456-7f96-483d-86a3-6a414746db8a
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, User
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '1566'
ht-degree: 1%

---

# 양식 관리 소개 {#introduction-to-managing-forms}

AEM [!DNL Forms]은(는) 양식, 문서, 테마, 편지, 문서 단편, 데이터 사전 및 관련 자산을 만들고 관리할 수 있는 간단하면서도 강력한 사용자 인터페이스를 제공합니다. 개발자의 데스크탑에서 오퍼링에 이르기까지 양식, 문서 및 관련 자산의 전체 라이프사이클을 관리하는 데 도움이 됩니다
최종 사용자를 위한 포털 서버에 있습니다. AEM [!DNL Forms] 사용자 인터페이스를 사용하여 다음을 수행할 수 있습니다.

* AEM [!DNL Forms] 구성 요소에 액세스
* AEM [!DNL Forms] 구성에 액세스

>[!NOTE]
>
>다른 AEM 도구 및 옵션에 대한 자세한 내용은 [작성](/help/sites-authoring/author.md)을 참조하십시오.

## AEM Forms 구성 요소 액세스 {#access-aem-forms-components}

양식, 문서 및 관련 에셋을 만들 수 있는 옵션과 함께 AEM은 사이트, 에셋을 만들고 AEM 인스턴스를 관리하는 옵션 등을 제공합니다. ![adobeexperiencemanager](assets/adobeexperiencemanager.png) Experience Manager 로고를 클릭하여 사용 가능한 모든 도구로 이동할 수 있습니다. 다른 구성 요소의 콘솔에 대한 링크와 함께 AEM [!DNL Forms]에 대한 링크도 포함됩니다. AEM [!DNL Forms] (으)로 이동하려면 Experience Manager 로고 ![adobeexperiencemanager](assets/adobeexperiencemanager.png) > 탐색 ![나침반](assets/compass.png) > **[!UICONTROL Forms]**&#x200B;을 클릭합니다. 다음 콘솔의 링크가 표시됩니다.

* 양식 및 문서
* 테마
* 편지
* 문서 단편
* 데이터 사전

  ![AEM Forms 콘솔](assets/aem_forms_console_new.png)

### 양식 및 문서  {#forms-documents}

Forms 및 문서는 대화형 통신, 적응형 양식, 적응형 양식 단편 및 양식 세트를 만드는 옵션을 제공합니다. JEE의 AEM [!DNL Forms]에 대해서만 Forms 및 Documents는 로컬 저장소에서 파일을 가져오고 AEM [!DNL Forms] 자산을 Workbench와 동기화하는 옵션을 제공합니다.

만들기 단추는 AEM [!DNL Forms] 자산을 만들거나 업로드하는 프로세스의 시작점입니다. 다음을 만들 수 있는 옵션을 제공합니다.

* **대화형 통신**: 대화형 통신은 개인 맞춤화되고, 대화형 및 장치 친화적인 HTML 기반 디지털 서신, 문 또는 문서입니다. 대화형 커뮤니케이션은 기본적으로 응답하고 사용자 장치 및 설정을 기반으로 자동으로 레이아웃 및 디자인을 변경합니다. 자세한 내용은 [대화형 통신 개요](/help/forms/using/interactive-communications-overview.md)를 참조하십시오.

* **적응형 양식:** 적응형 양식은 매력적인 반응형 양식입니다. 사용자 응답, 장치 또는 작업 환경에 따라 양식 섹션을 추가하거나 제거하여 사용자 입력에 동적으로 적응하는 적응형 양식을 작성할 수 있습니다. [적응형 양식 작성 소개](../../forms/using/introduction-forms-authoring.md) 문서에서는 적응형 양식에 대한 자세한 정보를 제공합니다.

* **적응형 양식 단편:** 모든 양식은 특정 목적을 위해 디자인되었지만 대부분의 양식에는 이름과 주소, 가족 정보, 소득 정보 등과 같은 개인 정보를 제공하기 위한 공통 세그먼트가 있습니다. 이러한 섹션에 대해 개별 에셋을 생성할 수 있습니다. 이러한 재사용 가능한 독립형 세그먼트를 적응형 양식 조각이라고 합니다. 자세한 내용은 [적응형 양식 조각](../../forms/using/adaptive-form-fragments.md) 문서를 참조하십시오.

* **양식 집합:** 양식 집합은 함께 그룹화되어 최종 사용자에게 단일 양식 집합으로 표시되는 HTML5 양식의 컬렉션입니다. 최종 사용자가 양식 세트를 채우기 시작하면 양식이 한 양식에서 다른 양식으로 원활하게 전환됩니다. 마지막에 사용자는 한 번의 클릭으로 모든 양식을 단일 엔티티로 제출할 수 있습니다. 자세한 내용은 [AEM Forms에 설정된 양식](../../forms/using/formset-in-aem-forms.md)을 참조하세요.

* **폴더:** AEM [!DNL Forms] 사용자 인터페이스는 폴더를 사용하여 자산을 정렬합니다. 다음 두 가지 유형의 폴더를 지원합니다.

   * **일반 폴더:** 이러한 폴더는 AEM [!DNL Forms] 사용자 인터페이스 내에서 만들어진 자산에 사용됩니다. 이러한 폴더에는 엄격한 폴더 구조가 없습니다. 이러한 폴더에 적응형 양식, 대화형 통신, 적응형 양식 단편, 양식 템플릿(XDP), PDF forms, 문서 및 관련 에셋의 이름을 바꾸고, 하위 폴더를 만들고, 저장할 수 있습니다.
   * **Forms Workflow 폴더:** Forms 워크플로 폴더는 Workbench 프로세스(LiveCycle 아카이브)가 마이그레이션되고 AEM [!DNL Forms] 사용자 인터페이스와 동기화될 때 만들어집니다. 이름 변경, 하위 폴더 만들기, 대화형 통신, 적응형 양식 조각 또는 대화형 통신을 만들 수 없습니다. 또한 버전 폴더를 삭제하거나 적응형 양식, 적응형 양식 단편 또는 대화형 통신을 버전 폴더와 병렬로 만들어 업로드할 수 없습니다.

  ![폴더](assets/folders.png)

  **A.** 일반 폴더 **B.** Forms Workflow 폴더

Forms 및 문서 패널에서는 다음 옵션도 제공됩니다.

* **로컬 저장소에서 파일 가져오기:** PDF forms 및 문서, 양식 서식 파일(XFA 양식) 및 기타 리소스(XSD용 이미지 및 XML 스키마)를 가져올 수 있습니다. 단계별 지침은 [AEM Forms으로 에셋 가져오기 및 내보내기](../../forms/using/import-export-forms-templates.md)를 참조하십시오.
* **AEM Forms 자산을 Workbench와 동기화:** Workbench의 파일 옵션을 사용하여 AEM Forms 사용자 인터페이스와 Workbench 간에 자산을 동기화할 수 있습니다. AEM [!DNL Forms] 사용자 인터페이스와 Workbench의 crx-repository 에셋 선택에서 모든 에셋을 사용할 수 있습니다.

### 테마  {#themes}

테마에는 구성 요소 및 패널에 대한 스타일 지정 세부 사항이 포함되어 있습니다. 테마는 독립적인 정체성을 가지고 있다. 따라서 여러 적응형 양식에서 테마를 재사용할 수 있습니다. 구성 요소의 스타일을 지정하거나 양식에서 사용되는 다양한 구성 요소의 CSS 속성을 수정할 수 있습니다. 스타일에는 배경색, 상태 색상, 투명도 및 크기와 같은 속성이 포함됩니다. 테마에 사용자 지정을 저장하고 양식의 구성 요소에 사전 설정으로 포팅할 수 있습니다. 양식에 테마를 추가하면 지정된 스타일이 양식의 해당 구성 요소를 반영합니다. AEM 6.2 [!DNL Forms]을(를) 사용하면 테마를 만들어 양식에 적용할 수 있습니다.

테마를 만들고 사용하는 방법에 대한 자세한 내용은 [AEM Forms의 테마](../../forms/using/themes.md)를 참조하십시오.

### 편지  {#letters}

AEM [!DNL Forms] 문자는 안전하고 개인화된 대화형 통신입니다. AEM [!DNL Forms]을(를) 사용하여 사전 승인된 콘텐츠와 사용자 지정 작성 콘텐츠의 편지(서신)를 간소화된 프로세스로 빠르게 조합할 수 있습니다.

편지 만들기 및 사용에 대한 자세한 내용은 [편지 만들기](../../forms/using/create-letter.md)를 참조하세요.

### 문서 단편 {#document-fragments}

문서 조각은 편지를 작성할 수 있는 서신의 재사용 가능한 부분 또는 구성 요소입니다. 문서 조각은 유형 텍스트, 목록, 조건 및 레이아웃 조각입니다. 문서 단편 만들기 및 사용에 대한 자세한 내용은 [문서 단편 만들기](/help/forms/using/document-fragments.md)를 참조하세요.

### 데이터 사전 {#data-dictionaries}

일반적으로 비즈니스 사용자는 XSD(XML 스키마) 및 Java 클래스와 같은 메타데이터 표현에 대한 지식이 필요하지 않습니다. 그러나 솔루션을 빌드하려면 일반적으로 이러한 데이터 구조 및 속성에 액세스해야 합니다. AEM [!DNL Forms]은(는) 비즈니스 사용자가 기본 데이터 모델에 대한 기술적인 세부 정보를 알지 못하면서 백엔드 데이터 소스의 정보를 사용할 수 있도록 해 주는 데이터 사전을 사용합니다.

데이터 사전 만들기 및 사용에 대한 자세한 내용은 데이터 사전 만들기 [문서](../../forms/using/data-dictionary.md)를 참조하십시오.

## AEM [!DNL Forms] 구성에 액세스 {#accessing-aem-forms-configurations}

AEM 도구 패널에는 다양한 구성 요소용 도구가 포함되어 있습니다. AEM Forms 관련 도구로 이동하려면 Experience Manager 로고 ![adobeexperiencemanager](assets/adobeexperiencemanager.png) > 도구 ![hammer](assets/hammer.png) > **[!UICONTROL Forms]**&#x200B;을(를) 클릭합니다. 다음 기능을 수행하는 도구가 표시됩니다.

* **감시 폴더 구성:** 관리자가 감시 폴더라고 하는 네트워크 폴더를 구성할 수 있으므로 사용자가 감시 폴더에 파일(PDF 파일 등)을 배치할 때 미리 구성된 작업이 시작되어 파일을 조작할 수 있습니다. 자세한 내용은 [감시 폴더 만들기 및 구성](/help/forms/using/creating-configure-watched-folder.md)을 참조하십시오.
* **Forms App Offline 서비스 구성:** AEM [!DNL Forms] App Offline 서비스가 양식에 사용된 리소스의 경로 또는 URL을 캐시합니다. 양식에 사용된 리소스의 경로 또는 URL을 캐시하면 서버측 성능이 향상됩니다. AEM Forms 앱의 서버측 오프라인 구성 요소를 구성하려면 [오프라인 모드에서 작업](/help/forms/using/work-offline-mode.md)을 참조하십시오.

  ![AEM Forms 도구](assets/aem_forms_tools_new.png)

* **PDF Generator 구성:** 관리자가 AEM [!DNL Forms] PDF Generator 설정을 구성하고, 사용자 계정을 추가하고, PDF Generator에 구성을 가져오거나 내보낼 수 있습니다.
* **Publish 서신 관리 Assets:** AEM [!DNL Forms]을(를) 사용하면 작성자 인스턴스의 모든 편지, 문서 단편, 데이터 사전 및 관련 종속성을 한 번에 게시할 수 있습니다. 게시된 에셋에는 모든 서신 관리 에셋과 관련 의존성이 포함됩니다. 자세한 내용은 [양식 및 문서 게시 및 게시 취소](../../forms/using/publishing-unpublishing-forms.md#publishallthecorrespondencemanagementassets)를 참조하십시오.
* **응답 관리 Assets 내보내기:** AEM [!DNL Forms] 인스턴스에서 모든 응답 관리 에셋과 관련 종속성을 패키지로 다운로드할 수 있습니다. 자세한 단계는 [AEM Forms으로 자산 가져오기 및 내보내기](../../forms/using/import-export-forms-templates.md#importandexportassetsincorrespondencemanagement)를 참조하십시오.

## 사용자 인터페이스의 일반적인 요소 {#commonelements}

* **왼쪽 레일:** 왼쪽 레일 아이콘 ![railleftpng](assets/railleftpng.png)을(를) 클릭하여 AEM [!DNL Forms]의 타임라인 및 참조 기능을 표시할 수 있습니다.

   * **타임라인:** 타임라인에서 검토할 수 있는 자산에 주석을 추가하고 볼 수 있습니다. 자세한 지침은 [양식의 에셋에 대한 리뷰 만들기 및 관리](../../forms/using/create-reviews-forms.md)를 참조하십시오.
   * **참조:** AEM [!DNL Forms] 자산은 여러 AEM [!DNL Forms] 자산에서 사용할 수 있습니다. 예를 들어 문서 조각은 여러 편지로 사용할 수 있습니다. 참조는 선택한 에셋이 사용되는 에셋(기타 양식 또는 리소스) 목록과 선택한 에셋이 사용 중인 기타 에셋 목록입니다.

* **이동 경로:** 이동 경로는 현재 콘솔 또는 폴더의 제목을 나타냅니다. 이동 경로 옵션을 클릭하여 계층 구조 상단에 있는 폴더 수준 사이를 이동할 수 있습니다.
* **전환기 보기:** 전환기 보기 아이콘 ![보기 목록](assets/viewlist.png) 또는 ![보기 카드](assets/viewcard.png)를 클릭하여 목록과 카드 보기 간에 빠르게 전환할 수 있습니다. 일반적인 사용자 인터페이스 구성 요소에 대한 자세한 내용은 [작성](/help/sites-authoring/author.md)을 참조하십시오.
* **검색:** 검색 옵션 ![검색](assets/search.png)은(는) 필요한 콘텐츠와 도구를 빠르게 찾아 이동할 수 있는 기능을 제공합니다. 콘텐츠 또는 제품 기능의 이름을 입력하고 제안 사항에서 선택하십시오. 예를 들어, &quot;Documents&quot;를 입력하여 **[!UICONTROL Forms 및 문서]** 또는 문서 단편 콘솔을 빠르게 찾아 이동합니다. 검색에 대한 자세한 내용은 AEM 6.2 [검색](/help/sites-authoring/search.md) 문서를 참조하십시오.

* **작업 도구 모음**: 에셋을 선택하면 에셋 목록 위에 작업 도구 모음이 표시됩니다. 여기에는 선택한 에셋에 대한 모든 관리 도구가 포함되어 있습니다. 도구 아이콘 위로 마우스를 가져가면 해당 기능을 설명하는 도구 설명을 볼 수 있습니다

>[!NOTE]
>
>사용자가 Forms 및 문서의 콘솔을 검색할 때 레일에는 **필터 및 옵션**&#x200B;만 포함됩니다. 필터 및 옵션을 사용하여 고급 검색을 수행할 수 있습니다.

* **작업 도구 모음**: 에셋을 선택하면 에셋 목록 위에 작업 도구 모음이 표시됩니다. 여기에는 선택한 에셋에 대한 모든 관리 도구가 포함되어 있습니다. 도구 아이콘 위로 마우스를 가져가면 해당 기능을 설명하는 도구 설명을 볼 수 있습니다

  적응형 양식에 대한 ![작업 도구 모음](assets/action_toolbar_new.png)

  적응형 양식에 대한 작업 도구 모음
