---
title: 양식 관리 소개
seo-title: 양식 관리 소개
description: AEM Forms은 적응형 Forms 및 관련 에셋을 관리하는 도구를 제공합니다. 이 문서에서는 주요 양식 관리 기능과 사용자 인터페이스 요소를 소개합니다.
seo-description: AEM Forms은 적응형 Forms 및 관련 에셋을 관리하는 도구를 제공합니다. 이 문서에서는 주요 양식 관리 기능과 사용자 인터페이스 요소를 소개합니다.
uuid: 2275a0b6-b31e-4d8e-8154-ccdfff3705aa
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager, introduction
discoiquuid: c0e4c9bb-e12a-4f9a-a8fa-1a8ad41d3995
docset: aem65
translation-type: tm+mt
source-git-commit: 46f2ae565fe4a8cfea49572eb87a489cb5d9ebd7
workflow-type: tm+mt
source-wordcount: '1593'
ht-degree: 1%

---


# 양식 관리 소개 {#introduction-to-managing-forms}

AEM [!DNL Forms]은 양식, 문서, 테마, 편지, 문서 단편, 데이터 사전 및 관련 에셋을 만들고 관리할 수 있는 간단하면서도 강력한 사용자 인터페이스를 제공합니다. 개발자의 데스크탑에서 솔루션 제공에 이르기까지 양식, 문서 및 관련 자산의 전체 라이프사이클을 관리할 수 있습니다.
최종 사용자를 위한 포털 서버에서 제공됩니다. AEM [!DNL Forms] 사용자 인터페이스를 사용하여 다음을 수행할 수 있습니다.

* AEM [!DNL Forms] 구성 요소에 액세스
* AEM [!DNL Forms] 구성 액세스

>[!NOTE]
>
>다른 AEM 도구 및 옵션에 대한 자세한 내용은 [제작](/help/sites-authoring/author.md)을 참조하십시오.

## AEM Forms 구성 요소 {#access-aem-forms-components} 액세스

양식, 문서 및 관련 에셋을 만드는 옵션과 함께 AEM은 사이트 만들기, 에셋, AEM 인스턴스 관리 등의 옵션을 제공합니다. ![adobeexperiencemanager](assets/adobeexperiencemanager.png) Experience Manager 로고를 클릭하여 사용 가능한 모든 도구로 이동할 수 있습니다. 다른 구성 요소의 콘솔에 대한 링크와 함께 AEM [!DNL Forms]에 대한 링크도 포함되어 있습니다. AEM [!DNL Forms]으로 이동하려면 Experience Manager 로고 ![adobeexperienemanager](assets/adobeexperiencemanager.png) > 탐색 ![compass](assets/compass.png) > **[!UICONTROL Forms]**&#x200B;을 클릭합니다. 다음 콘솔의 링크가 표시됩니다.

* 양식 및 문서
* 테마
* 편지
* 문서 단편
* 데이터 사전

   ![AEM Forms 콘솔](assets/aem_forms_console_new.png)

### 양식 및 문서  {#forms-documents}

Forms &amp; 문서는 대화형 통신, 적응형 양식, 적응형 양식 단편 및 양식 세트를 만드는 옵션을 제공합니다. JEE의 AEM [!DNL Forms]에 대해서만 Forms &amp; Documents는 로컬 저장소에서 파일을 가져오고 Workbench와 AEM [!DNL Forms] 자산을 동기화할 수 있는 옵션을 제공합니다.

만들기 단추는 AEM [!DNL Forms] 자산을 만들거나 업로드하는 프로세스의 시작점입니다. 다음과 같은 만들기 옵션을 제공합니다.

* **인터랙티브 커뮤니케이션**:인터랙티브 커뮤니케이션은 개인화되고 인터랙티브한 디바이스용 HTML 기반의 디지털 커뮤니케이션, 명세서 또는 문서를 제공합니다. 인터랙티브한 커뮤니케이션은 응답 속도가 빠르며 사용자 디바이스 및 설정에 따라 레이아웃 및 디자인을 자동으로 변경할 수 있습니다. 자세한 내용은 [대화형 통신 개요](/help/forms/using/interactive-communications-overview.md)를 참조하십시오.

* **적응형 양식:** 적응형 양식은 매력적이고 반응형 양식입니다. 사용자 응답, 장치 또는 작업 환경에 따라 양식 섹션을 추가하거나 제거하여 사용자 입력에 동적으로 맞게 적응할 수 있는 적응형 양식을 작성할 수 있습니다. 적응형 양식 작성 소개[ 문서에서는 적응형 양식에 대한 자세한 정보를 제공합니다.](../../forms/using/introduction-forms-authoring.md)

* **적응형 양식 조각:** 모든 양식은 특정 목적을 위해 설계되지만 이름, 주소, 가족 세부 사항, 소득 세부 사항 등과 같은 개인 세부 정보를 제공하는 등 대부분의 양식에는 몇 가지 공통 세그먼트가 있습니다. 이러한 섹션의 개별 자산을 만들 수 있습니다. 재사용 가능한 독립 실행형 세그먼트를 응용 양식 조각이라고 합니다. 자세한 내용은 [적응형 양식 조각](../../forms/using/adaptive-form-fragments.md) 아티클을 참조하십시오.

* **양식 세트:** 양식 세트는 함께 그룹화되고 최종 사용자에게 단일 양식 세트로 제공되는 HTML5 양식의 컬렉션입니다. 최종 사용자가 양식 세트를 채우기 시작하면 양식은 한 양식에서 다른 양식으로 원활하게 전환됩니다. 한 번의 클릭으로 모든 양식을 하나의 엔티티로 제출할 수 있습니다. 자세한 내용은 AEM Forms](../../forms/using/formset-in-aem-forms.md)의 [양식 세트를 참조하십시오.

* **폴더:** AEM  [!DNL Forms] 사용자 인터페이스는 폴더를 사용하여 자산을 정렬합니다. 두 가지 유형의 폴더를 지원합니다.

   * **일반 폴더:** 이러한 폴더는 AEM  [!DNL Forms] 사용자 인터페이스 내에서 만든 자산에 사용됩니다. 이러한 폴더에는 엄격한 폴더 구조가 없습니다. 이러한 폴더의 응용 양식, 인터랙티브 커뮤니케이션, 적응형 양식 조각, 양식 템플릿(XDP), PDF forms, 문서 및 관련 에셋의 이름을 변경하거나 하위 폴더를 만들고 저장할 수 있습니다.
   * **Forms Workflow 폴더: 워크벤치 프로세스(LiveCycle 아카이브)가 마이그레이션되고 AEM** 사용자 인터페이스와 동기화되면  [!DNL Forms] Forms 워크플로우 폴더가 생성됩니다. 이름 바꾸기, 하위 폴더 만들기, 대화형 통신, 응용 양식 단편 또는 대화형 통신을 만들 수 없습니다. 버전 폴더를 삭제하거나 응용 양식, 응용 양식 단편 또는 대화형 통신을 버전 폴더와 병렬로 만들고 업로드할 수도 없습니다.

   ![폴더](assets/folders.png)

   **A.** 일반 폴더  **B.** Forms Workflow 폴더

Forms 및 문서 패널은 다음 옵션도 제공합니다.

* **로컬 저장소에서 파일 가져오기:** PDF forms 및 문서, 양식 템플릿(XFA 양식) 및 기타 리소스(XSD의 이미지 및 XML 스키마)를 가져올 수 있습니다. 단계별 지침은 [AEM Forms으로 자산 가져오기 및 내보내기를 참조하십시오](../../forms/using/import-export-forms-templates.md).
* **워크벤치와 AEM Forms 자산 동기화:** 워크벤치의 파일 옵션을 사용하여 AEM Forms 사용자 인터페이스와 워크벤치 간에 자산을 동기화할 수 있습니다. 모든 에셋이 AEM [!DNL Forms] 사용자 인터페이스와 Workbench의 crx-repository 에셋 선택 시 사용 가능하게 됩니다.

### 테마  {#themes}

테마는 구성 요소 및 패널에 대한 스타일 세부 사항을 포함합니다. 테마에는 독립적인 ID가 있습니다. 따라서 여러 적응형 양식에 테마를 재사용할 수 있습니다. 구성 요소의 스타일을 지정하거나 양식에서 사용되는 다양한 구성 요소의 CSS 속성을 수정할 수 있습니다. 스타일에는 배경색, 상태 색상, 투명도 및 크기와 같은 속성이 포함됩니다. 사용자 정의 설정을 테마에 저장하고 양식 구성 요소에 사전 설정으로 포팅할 수 있습니다. 양식에 테마를 추가하면 지정된 스타일이 양식의 해당 구성 요소에 반영됩니다. AEM 6.2 [!DNL Forms]을 사용하면 테마를 만들고 양식에 적용할 수 있습니다.

테마 만들기 및 사용에 대한 자세한 내용은 AEM Forms](../../forms/using/themes.md)의 [테마를 참조하십시오.

### 편지  {#letters}

AEM [!DNL Forms] 서신은 안전하고 개인화된 인터랙티브한 메시지입니다. AEM [!DNL Forms]을 사용하여 사전 승인된 컨텐츠와 사용자 정의 제작 컨텐츠 모두에서 작성된 문자(해당 항목이라고도 함)를 빠르게 취합할 수 있습니다.

문자 만들기 및 사용에 대한 자세한 내용은 [문자 만들기](../../forms/using/create-letter.md)를 참조하십시오.

### 문서 단편 {#document-fragments}

문서 조각은 편지를 작성할 수 있는 통신 부분의 재사용 가능한 부분이나 구성 요소입니다. 문서 조각은 텍스트, 목록, 조건 및 레이아웃 조각 유형입니다. 문서 조각 만들기 및 사용에 대한 자세한 내용은 [문서 조각 만들기](/help/forms/using/document-fragments.md)를 참조하십시오.

### 데이터 사전 {#data-dictionaries}

일반적으로 비즈니스 사용자는 XSD(XML 스키마) 및 Java 클래스와 같은 메타데이터 표현에 대한 지식이 필요하지 않습니다. 그러나 일반적으로 솔루션을 구축하려면 이러한 데이터 구조 및 속성에 액세스해야 합니다. AEM [!DNL Forms]은(는) 비즈니스 사용자가 기본 데이터 모델에 대한 기술 세부 사항을 알지 않고도 백엔드 데이터 소스의 정보를 사용할 수 있도록 하는 데이터 사전을 사용합니다.

데이터 사전을 만들고 사용하는 방법에 대한 자세한 내용은 [데이터 사전 문서 만들기](../../forms/using/data-dictionary.md)

## AEM [!DNL Forms] 구성 액세스 {#accessing-aem-forms-configurations}

AEM 도구 패널에는 다양한 구성 요소를 위한 도구가 포함되어 있습니다. AEM Forms 특정 도구로 이동하려면 Experience Manager 로고 ![adobeexperienemanager](assets/adobeexperiencemanager.png) > 도구 ![망치](assets/hammer.png) > **[!UICONTROL Forms]**&#x200B;을 클릭합니다. 다음 기능을 수행하는 도구가 표시됩니다.

* **감시 폴더 구성:** 관리자가 감시 폴더에 파일(예: PDF 파일)을 배치할 때 미리 구성된 작업이 시작되고 파일을 조작하도록 감시됨 폴더라는 네트워크 폴더를 구성할 수 있습니다. 자세한 내용은 [감시 폴더 만들기 및 구성을 참조하십시오](/help/forms/using/creating-configure-watched-folder.md).
* **Forms App Offline 서비스 구성:** AEM  [!DNL Forms] 앱 오프라인 서비스는 양식에 사용된 리소스의 경로 또는 URL을 캐시합니다. 양식에서 사용되는 리소스의 경로 또는 URL을 캐시하면 서버측 성능이 향상됩니다. AEM Forms 앱의 서버측 오프라인 구성 요소를 구성하려면 [오프라인 모드에서 작업](/help/forms/using/work-offline-mode.md)을 참조하십시오.

   ![AEM Forms 툴](assets/aem_forms_tools_new.png)

* **PDF Generator 구성:** 관리자는 AEM  [!DNL Forms] PDF Generator 설정을 구성하고 사용자 계정을 추가하며 PDF Generator로 구성을 가져오거나 내보낼 수 있습니다.
* **메일 관리 자산 게시:** AEM [!DNL Forms] 을 사용하면 작성 인스턴스에서 모든 편지, 문서 조각 및 데이터 사전 및 관련 종속성을 한 번에 게시할 수 있습니다. 게시된 자산은 모든 통신 관리 자산 및 관련 종속성을 포함합니다. 자세한 내용은 [양식 및 문서 게시 및 게시 취소](../../forms/using/publishing-unpublishing-forms.md#publishallthecorrespondencemanagementassets)를 참조하십시오.
* **통신 관리 자산 내보내기:** 모든 통신 관리 자산 및 관련 종속성을 AEM 인스턴스에서 패키지로 다운로드할 수  [!DNL Forms] 있습니다. 자세한 내용은 [에셋 가져오기 및 AEM Forms으로 내보내기](../../forms/using/import-export-forms-templates.md#importandexportassetsincorrespondencemanagement)를 참조하십시오.

## 사용자 인터페이스의 공통 요소 {#commonelements}

* **왼쪽 레일:** 왼쪽 레일 아이콘  ![](assets/railleftpng.png) 레일 링크를 클릭하여 AEM의 타임라인 및 참조 기능을 표시할 수 있습니다 [!DNL Forms].

   * **타임라인:** 타임라인에서 검토할 수 있는 자산에 주석을 추가하고 볼 수 있습니다. 자세한 지침은 [양식에 있는 자산에 대한 검토 만들기 및 관리를 참조하십시오](../../forms/using/create-reviews-forms.md).
   * **참조:** AEM  [!DNL Forms] 자산은 여러 AEM 자산에 사용할 수  [!DNL Forms] 있습니다. 예를 들어 문서 조각을 여러 문자로 사용할 수 있습니다. 참조는 선택한 자산이 사용되는 자산(다른 양식 또는 리소스) 목록과 선택한 자산이 사용하는 다른 자산의 목록이기도 합니다.

* **탐색 표시:** A 탐색 표시는 현재 콘솔 또는 폴더의 제목을 나타냅니다. [탐색 표시] 옵션을 클릭하여 계층에서 더 높은 폴더 수준을 탐색할 수 있습니다.
* **전환기 보기:** [전환기 보기] 아이콘  ![](assets/viewlist.png) 보기목록이나  ![](assets/viewcard.png) 보기카드를 클릭하여 목록과 카드 보기 간을 빠르게 전환할 수 있습니다. 공통 사용자 인터페이스 구성 요소에 대한 자세한 내용은 [작성](/help/sites-authoring/author.md)을 참조하십시오.
* **검색:** 검색 옵션은  ![](assets/search.png) 필요한 컨텐츠 및 툴을 신속하게 찾아 이동할 수 있는 기능을 제공합니다. 컨텐트 또는 제품 기능의 이름을 입력하고 제안 사항(예: &quot;Documents&quot;를 입력하여 **[!UICONTROL Forms &amp; Documents]** 또는 문서 조각 콘솔로 빠르게 찾아 이동합니다.) 검색에 대한 자세한 내용은 AEM 6.2 [검색](/help/sites-authoring/search.md) 아티클을 참조하십시오.

* **작업 도구 모음**:자산을 선택하면 작업 도구 모음이 자산 목록 위에 표시됩니다. 여기에는 선택한 자산에 대한 모든 관리 도구가 포함되어 있습니다. 도구 아이콘 위에 마우스를 올려 놓으면 해당 기능에 대해 설명하는 도구 설명을 볼 수 있습니다

>[!NOTE]
>
>사용자가 Forms 및 문서의 아무 콘솔이나 검색할 때 레일에는 **필터 및 옵션**&#x200B;만 포함됩니다. 필터 및 옵션을 사용하여 고급 검색을 수행할 수 있습니다.

* **작업 도구 모음**:자산을 선택하면 작업 도구 모음이 자산 목록 위에 표시됩니다. 여기에는 선택한 자산에 대한 모든 관리 도구가 포함되어 있습니다. 도구 아이콘 위에 마우스를 올려 놓으면 해당 기능에 대해 설명하는 도구 설명을 볼 수 있습니다

   ![적응형 양식의 작업 도구 모음](assets/action_toolbar_new.png)

   적응형 양식의 작업 도구 모음
