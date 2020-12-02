---
title: 파일 유형 설정 구성
seo-title: 파일 유형 설정 구성
description: 파일 유형 설정을 구성하는 방법을 알아봅니다.
seo-description: 파일 유형 설정을 구성하는 방법을 알아봅니다.
uuid: 58a05500-ffbb-4fa2-8ae1-8ac80ab2d099
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 89f4d3cf-eb2e-4d55-8209-16ecbba03792
translation-type: tm+mt
source-git-commit: 80b8571bf745b9e7d22d7d858cff9c62e9f8ed1e
workflow-type: tm+mt
source-wordcount: '6182'
ht-degree: 0%

---


# 파일 유형 설정 구성 중 {#configuring-file-type-settings}

PDF Generator에서는 지원되는 파일 유형에 대한 애플리케이션 설정을 설정할 수 있습니다. Windows에서는 지원되는 각 파일 유형에 대한 응용 프로그램 설정을 설정할 수 있습니다. UNIX 및 Linux에서는 HTML에서 PDF로 및 OpenOffice에 대한 응용 프로그램 설정을 설정할 수 있습니다.

파일 유형 설정 페이지에서 다음 작업을 수행할 수 있습니다.

* [파일 유형 설정 만들기 또는 편집](#create-or-edit-file-type-settings)
* 기본적으로 사용할 파일 유형 설정을 지정합니다([PDF Generator 구성 파일 가져오기 및 내보내기](https://helpx.adobe.com/aem-forms/6-2/admin-help/importing-exporting-pdf-generator-configuration.html) 참조)
* [기본 설정 변경](/help/forms/using/admin-help/configuring-file-type-settings1.md#change-the-default-settings)
* [PDF/A 지원 사용](https://helpx.adobe.com/aem-forms/6-2/admin-help/enable-pdf-a-support.html)
* [파일 유형 삭제 설정](https://helpx.adobe.com/aem-forms/6-2/admin-help/enable-pdf-a-support.html)

>[!NOTE]
>
>HTML을 PDF로 변환하는 경우 Acrobat, Microsoft PowerPoint, Microsoft Word 및 Microsoft Excel과 같은 대체 변환기에는 파일 형식 설정을 사용할 수 없습니다.

## 파일 유형 설정 {#create-or-edit-file-type-settings} 만들기 또는 편집

파일 유형 설정을 만들거나 편집하여 애플리케이션에서 지원되는 파일 유형의 변환을 처리하는 방법을 지정합니다. Windows에서는 지원되는 각 파일 유형에 대한 응용 프로그램 설정을 설정할 수 있습니다. UNIX 및 Linux에서는 HTML에서 PDF로 및 OpenOffice에 대한 응용 프로그램 설정을 설정할 수 있습니다.

1. 관리 콘솔에서 **[!UICONTROL 서비스]** > **[!UICONTROL PDF Generator]** > **[!UICONTROL 파일 유형 설정]**&#x200B;을 클릭합니다.
1. [새로 만들기]를 클릭하거나 설정 이름을 클릭합니다.
1. [파일 이름 확장자] 상자에 이 응용 프로그램에 허용되는 파일 유형에 대해 쉼표로 구분된 파일 확장자를 입력합니다. 확장 이전 또는 확장 사이의 공백을 포함하지 마십시오. 기본값은 `bmp,gif,jpeg,jpg,tif,tiff,png`입니다.
1. (선택 사항) 그래픽 또는 이미지에서 텍스트 OCR(Optical Code Recognition: 광학식 코드 인식)을 사용하려면 [OCR 사용]을 선택하고 다음 옵션을 설정합니다.

**기본 언어:** OCR 엔진이 문자를 식별하는 데 사용하는 언어입니다. 기본값은 영어(미국)입니다.

**PDF 출력 스타일:** 검색 가능한 이미지를 선택하여 전경 페이지의 비트맵 이미지를 만들고 스캔한 텍스트를 밑에 보이지 않는 레이어로 만듭니다. 페이지의 모양은 변경되지 않지만 텍스트를 선택 가능하고 읽을 수 있게 됩니다. 텍스트, 글꼴, 그림 및 기타 그래픽 요소를 사용하여 원본 페이지를 재구성하려면 서식이 지정된 텍스트 및 그래픽을 선택합니다. 기본값은 검색 가능한 이미지(정확)입니다.

**다운샘플링 이미지:** 컬러, 회색 음영 및 단색 이미지의 픽셀 수를 줄입니다. OCR이 완료된 후 스캔한 이미지의 다운샘플링이 수행됩니다. 기본값은 최저(600dpi)입니다. PDF 출력 스타일을 검색 가능한 이미지(정확)로 설정하면 이 옵션을 사용할 수 없습니다.

1. 다음 섹션에서 필요한 정보를 완료합니다.

   [PDF Generator 구성 파일 가져오기 및 내보내기](https://helpx.adobe.com/aem-forms/6-2/admin-help/importing-exporting-pdf-generator-configuration.html)

   [Adobe PDF 내보내기 설정(Windows만 해당)](#adobe-pdf-export-settings-windows-only)

   [HTML에서 PDF로 설정](#html-to-pdf-settings)

   [PDF 설정으로 비디오 Flash](#flash-videos-to-pdf-settings)

   [XPS를 PDF로 설정](#xps-to-pdf-settings)

   [PDF 최적기 설정](#pdf-optimizer-settings)

   [Microsoft Excel 설정(Windows만 해당)](/help/forms/using/admin-help/configuring-file-type-settings1.md#microsoft-excel-settings-windows-only)

   [Microsoft PowerPoint 설정(Windows 전용)](/help/forms/using/admin-help/configuring-file-type-settings1.md#microsoft-powerpoint-settings-windows-only)

   [Microsoft Project 설정(Windows만 해당)](/help/forms/using/admin-help/configuring-file-type-settings1.md#microsoft-project-settings-windows-only)

   [Microsoft Word 설정(Windows만 해당)](/help/forms/using/admin-help/configuring-file-type-settings1.md#microsoft-word-settings-windows-only)

   [Microsoft Visio 설정(Windows만 해당)](#visio)

   [Microsoft Publisher 설정(Windows만 해당)](/help/forms/using/admin-help/configuring-file-type-settings1.md#microsoft-publisher-settings-windows-only)

   [AutoCAD 설정(Windows만 해당)](/help/forms/using/admin-help/configuring-file-type-settings1.md#autocad-settings-windows-only)

   [OpenOffice 설정](/help/forms/using/admin-help/configuring-file-type-settings1.md#openoffice-settings)

   [다른 응용 프로그램의 설정(Windows만 해당)](#other-applications-settings-windows-only)

   다른 섹션으로 이동하려면 웹 페이지에서 링크를 클릭하거나 **[!UICONTROL 다음]**또는 **[!UICONTROL 이전]** 단추를 사용하십시오.

1. 모든 섹션을 완료한 후 **[!UICONTROL 저장]** 또는 **[!UICONTROL 다른 이름으로 저장]**&#x200B;을 클릭하고 설정 이름을 입력합니다.

다양한 파일 유형에 대한 지원을 사용자 정의할 수 있습니다. ([AEM 양식을 사용한 프로그래밍](https://www.adobe.com/go/learn_lc_programming_11)에서 &quot; [추가 기본 파일 형식 지원 추가](https://help.adobe.com/en_US/AEMForms/6.1/ProgramLC/WS624e3cba99b79e12e69a9941333732bac8-7756.2.html)&quot;를 참조하십시오.)

## 기본 설정 {#change-the-default-settings} 변경

새로 만든 소스에 적용되는 Adobe PDF 설정, 보안 설정 및 파일 유형 설정의 기본값을 변경할 수 있습니다. 기본값을 변경해도 기존 소스의 설정에 영향을 주지 않습니다.

1. 관리 콘솔에서 **[!UICONTROL 서비스 > PDF Generator]**&#x200B;를 클릭합니다.
1. **[!UICONTROL Adobe PDF 설정]**, **[!UICONTROL 파일 유형 설정]** 또는 **[!UICONTROL 보안 설정]** 페이지에서 **[!UICONTROL 기본 설정 설정 설정]**&#x200B;을 클릭합니다.
1. 기본 설정을 선택합니다. 다음 설정 중 하나 이상을 [기본 설정 설정] 페이지에서 사용할 수 있습니다.

   **[!UICONTROL Adobe PDF 설정]**:원래 기본값은 표준(Acrobat 6)입니다.

   **[!UICONTROL 보안 설정]**:원래 기본값은 보안 없음(Acrobat 5)입니다.

   **[!UICONTROL 파일 유형 설정]**:원래 기본값은 표준입니다.

1. **[!UICONTROL 저장]**&#x200B;을 클릭합니다.

## 파일 유형 설정 {#delete-a-file-type-setting} 삭제

더 이상 사용되지 않는 파일 형식 설정을 삭제할 수 있습니다.

1. 관리 콘솔에서 **[!UICONTROL 서비스 > PDF Generator> 파일 유형 설정]**&#x200B;을 클릭합니다.
1. 삭제할 설정 옆에 있는 확인란을 선택합니다. 여러 소스를 선택할 수 있습니다. 옆에 확인란이 없는 설정은 PDF 생성기에 항상 포함되며 삭제할 수 없습니다.
1. **[!UICONTROL 삭제]**&#x200B;를 클릭하고 삭제 확인 페이지에서 **[!UICONTROL 삭제]**&#x200B;를 클릭합니다.

## PDF로 이미지 설정 {#image-to-pdf-settings}

다음 옵션은 이미지 파일을 PDF로 변환하는 방법을 결정합니다. 이러한 설정에 액세스하는 방법에 대한 지침은 [파일 유형 설정 만들기 또는 편집](configuring-file-type-settings.md#create-or-edit-file-type-settings)을 참조하십시오.

**파일 이름** 확장자: 변환할 수 있는 파일 이름 확장명의 쉼표로 구분된 목록입니다.

**대비책 변환기 시험버전:** PDF Generator는 Java™ 또는 Acrobat을 사용하여 이미지 파일을 PDF로 변환할 수 있습니다. 이 옵션을 선택하고 변환이 실패하거나 지정된 제한 시간에 도달하면 PDF Generator는 대체 방법을 사용하여 변환을 시도합니다. 대체 방법이 실패하거나 지정된 제한 시간 내에 도달하면 로그 파일에 예외가 기록됩니다.

>[!NOTE]
>
>JPEG 2000 파일은 Acrobat을 사용해서만 변환할 수 있습니다.

**OCR 사용:** OCR(Optical Character Recognition)을 PDF에 적용할지 여부를 지정합니다. OCR 소프트웨어를 사용하면 PDF에서 텍스트를 검색, 수정 및 복사할 수 있습니다.

***참고&#x200B;**:OCR PDF(검색 가능한 PDF) 기능은 Microsoft Windows에서만 지원됩니다.*

**기본 OCR 언어:** OCR 엔진이 문자를 식별하는 데 사용할 언어를 지정합니다.

**PDF 출력 스타일:** 작성할 PDF 유형을 결정합니다. 모든 포맷은 텍스트 이미지에 OCR 및 글꼴 및 페이지 인식을 적용하고 일반 텍스트로 변환합니다.

**검색 가능한 이미지:** 텍스트를 검색 및 선택할 수 있도록 합니다. 이 옵션을 사용하면 원본 이미지를 그대로 유지하고 필요에 따라 모양을 지정한 다음 보이지 않는 텍스트 레이어를 그 위에 배치할 수 있습니다. [이미지 다운로드] 옵션은 이미지가 다운샘플링되는지 여부와 어느 정도로 판단합니다.

**검색 가능한 이미지(정확):** 텍스트를 검색 및 선택할 수 있도록 합니다. 이 옵션을 사용하면 원본 이미지가 그대로 유지되고 보이지 않는 텍스트 레이어가 그 위에 놓입니다. 원본 이미지에 대한 최대 정확도가 필요한 경우 권장됩니다.

**ClearScan:** 원본과 거의 비슷한 새 Type 3 글꼴을 합성하고 저해상도 사본을 사용하여 페이지 배경을 유지합니다.

**다운샘플링 이미지:** OCR이 완료된 후 컬러, 회색 음영 및 단색 이미지의 픽셀 수를 줄입니다. 적용할 다운샘플링 수준을 선택합니다. 번호가 높은 옵션을 사용하면 다운샘플링을 줄일 수 있으므로 고해상도 PDF를 만들 수 있습니다.

## Adobe PDF 내보내기 설정(Windows만 해당) {#adobe-pdf-export-settings-windows-only}

Adobe PDF 내보내기 설정 섹션의 [파일 유형 내보내기] 설정은 PDF 파일을 다른 형식으로 변환하는 데 사용됩니다. 기본값은 CSS(Cascading Style Sheet) 1.0(&amp;ast;.htm, &amp;ast;.html)이 있는 HTML 4.01입니다.

이 설정에 액세스하는 방법에 대한 지침은 [파일 형식 설정 만들기 또는 편집](configuring-file-type-settings.md#create-or-edit-file-type-settings)을 참조하십시오.

## HTML-PDF 설정 {#html-to-pdf-settings}

다음 옵션은 HTML 파일을 PDF로 변환하는 방법을 결정합니다. 이러한 옵션에 액세스하는 방법에 대한 지침은 [파일 유형 설정 만들기 또는 편집](configuring-file-type-settings.md#create-or-edit-file-type-settings)을 참조하십시오.

**대비책 변환기 시험버전:** PDF Generator는 Java™ 또는 Acrobat을 사용하여 HTML 파일을 PDF로 변환할 수 있습니다. 이 옵션을 선택하고 변환이 실패하거나 지정된 제한 시간에 도달하면 PDF Generator는 대체 방법을 사용하여 변환을 시도합니다. 대체 방법이 실패하거나 지정된 제한 시간 내에 도달하면 로그 파일에 예외가 기록됩니다.

**기본 인코딩:** 운영 체제 및 알파벳의 메뉴에서 파일 텍스트의 입력 인코딩을 설정합니다. HTML 소스 파일이 인코딩 유형을 지정하지 않는 경우에만 기본 인코딩 옵션에 표시된 선택 사항을 사용합니다.

**강제 선택 인코딩:** HTML 소스 파일에 지정된 인코딩을 무시하고 기본 인코딩 옵션에 표시된 선택 사항을 사용합니다.

### 할당 설정 {#spidering-settings}

*Spideringsearching web pages for links to other web pages.* 다른 웹 페이지로 연결되는 링크가 발견되면 대상 페이지가 나타나고 생성되는 PDF 문서에 포함됩니다. 가져올 레벨 수와 PDF로 변환할 레벨 수를 설정하려면 다음 옵션을 활성화합니다.

**X 레벨만 가져오기:** 스파이더를 사용하여 기본 페이지 URL에서 지정된 수준의 깊이로 페이지를 변환합니다. 값 1은 제공된 URL만 변환합니다.

**전체 사이트** 가져오기: 제공된 URL부터 전체 사이트를 변환합니다.

**동일한 경로에 유지:** 기본 URL과 동일한 상대 경로에 있지 않은 페이지를 가리키는 모든 링크는 지정하는 동안 변환되지 않습니다.

**동일한 서버에서 유지: 다른 서버의 페이지를 가리키는** 모든 링크는 지정하는 동안 변환되지 않습니다. 지정된 URL과 동일한 서버를 가리키는 링크만 변환됩니다.

### 페이지 전환 설정 {#page-conversion-settings}

이러한 옵션을 활성화하여 HTML 페이지의 변환 방법을 지정합니다. 페이지 크기에 따라 너비, 높이 및 여백 값이 그에 따라 조정됩니다.

**페이지 크기: 사용자** 지정을 선택하고 너비와 높이를 지정하거나 사전 정의된 크기를 선택합니다.

**방향:** 변환된 PDF 문서의 세로 또는 가로 중 하나를 선택합니다.

**여백:** 생성된 PDF 문서의 여백(위쪽, 아래쪽, 왼쪽 및 오른쪽)을 지정합니다.

**PDF에 책갈피 추가:** PDF 문서에 책갈피를 추가합니다.

**태그 있는 PDF 사용:** PDF 문서에 태그를 포함합니다.

**초기 보기 설정 설정:** 문서 옵션, 창 옵션 및 사용자 인터페이스 옵션을 구성할 수 있습니다. 이러한 설정에 따라 컨텐츠가 처음에 표시되는 방식이 결정됩니다.

### 문서 옵션 {#document-options}

다음 옵션을 활성화하여 컨텐츠 표시 방법, PDF 문서에서 페이지 표시 방법 및 배율 레벨을 지정하는 방법을 지정합니다.

**표시:** PDF 문서를 열 때 Acrobat에서 열 창을 선택합니다.

**페이지 레이아웃:** PDF 문서의 페이지 레이아웃 유형을 선택합니다.

**배율:** PDF 문서의 초기 보기에 대해 사전 설정 배율을 선택하거나 사용자 정의 값을 선택합니다. 기본 설정을 선택하면 기본 Acrobat 배율이 사용됩니다.

**페이지에 열기 번호:** PDF에서 여는 페이지 번호를 지정합니다.

### 창 옵션 {#window-options}

이 옵션을 활성화하여 창의 크기와 표시 방법을 지정합니다.

**초기 페이지로 창 크기 조정:** 초기 페이지 크기로 Acrobat 창의 크기를 조정합니다.

**창 중앙 화면:** 화면 가운데에 있는 창을 엽니다.

**전체 화면 모드로 열기:** 창을 전체 화면 모드로 엽니다.

**표시:** 창에 문서 제목이나 파일 이름이 표시됩니다.

### 사용자 인터페이스 옵션 {#user-interface-options}

창 모양을 지정하려면 다음 옵션을 활성화합니다.

**메뉴 막대 숨기기:** PDF 문서에서 메뉴 막대를 숨깁니다.

**툴바 숨기기:** PDF 문서의 툴바를 숨깁니다.

**창 컨트롤 숨기기:** PDF 문서에서 창 컨트롤을 숨깁니다.

## PDF 설정 {#flash-videos-to-pdf-settings}에 대한 Flash 비디오

PDF Generator는 Adobe Flash(SWF 또는 FLV 파일)용 비디오를 제출하고 Adobe Flash에 임베드된 비디오로 PDF 파일을 작성할 수 있는 기능을 지원합니다. 이 변환은 양식 서버에 Adobe Flash Player을 설치할 필요가 없습니다. 이 옵션에 액세스하는 방법에 대한 지침은 [파일 유형 설정 만들기 또는 편집](configuring-file-type-settings.md#create-or-edit-file-type-settings)을 참조하십시오.

**파일 이름** 확장자: 변환할 수 있는 파일 이름 확장명의 쉼표로 구분된 목록입니다.

## XPS를 PDF로 설정 {#xps-to-pdf-settings}

XPS(XML Paper Specification)는 Windows Printing 시스템에서 사용됩니다. Microsoft 형식이며 모든 Microsoft Office 응용 프로그램에서 만들 수 있습니다. AEM 양식은 XPS 파일 PDF를 변환하는 기능을 제공합니다.

**파일 이름** 확장자: 변환할 수 있는 모든 XPS 파일 이름 확장명의 쉼표로 구분된 목록입니다. 현재 하나의 포맷이 있습니다..xps.

## PDF 최적기 설정 {#pdf-optimizer-settings}

PDF Generator를 사용하면 PDF 파일의 크기를 줄일 수 있습니다. 이러한 설정을 모두 사용하든 몇 가지 설정만 사용하든 상관없이 파일 사용 방법과 파일에 반드시 포함해야 하는 필수 속성에 따라 달라집니다. 대부분의 경우 기본 설정은 임베디드 글꼴을 제거하고 이미지를 압축하며 더 이상 필요하지 않은 파일에서 항목을 제거하여 공간을 절약하는 등 작업의 효율성을 최대화할 수 있습니다.

>[!NOTE]
>
>디지털 서명된 문서를 최적화하면 디지털 서명이 제거되고 무효화됩니다.

이 설정에 액세스하는 방법에 대한 지침은 [파일 형식 설정 만들기 또는 편집](configuring-file-type-settings.md#create-or-edit-file-type-settings)을 참조하십시오.

**Target PDF 버전:** PDF와 호환되는 Acrobat 버전을 지정합니다.

### 글꼴 {#fonts}

1. **글꼴을 선택합니다.**
1. 다음 옵션 중 하나를 선택합니다.

   **모든 글꼴 포함 취소:** 포함된 모든 글꼴을 포함 취소합니다.

   **글꼴 포함 취소 안 함: 글꼴** 의 포함 취소 안 함

   **일부 글꼴 포함 취소:** 지정된 글꼴만 포함 취소합니다. 다음 단계에 따라 포함 취소할 글꼴을 지정합니다.

   * 필요한 경우 **글꼴 소스** 드롭다운 메뉴에서 다른 글꼴 디렉토리를 선택합니다. 이 드롭다운 메뉴에는 **홈 > 설정 > 핵심 시스템 > 핵심 구성**&#x200B;에 지정된 글꼴 디렉토리가 나열됩니다.
   * **사용 가능한 글꼴** 목록에서 하나 이상의 글꼴을 선택하고 **추가**&#x200B;를 클릭합니다. 이러한 글꼴은 **글꼴을 포함 취소** 목록에 추가합니다.
   * 양식 서버에 없는 일부 글꼴을 포함 취소하려면 **포함 취소할 글꼴 추가** 상자에 해당 글꼴의 이름을 입력합니다. **추가**&#x200B;를 클릭합니다.

   >[!NOTE]
   >
   >*문서에 하위 세트가 포함된 일부 글꼴을 포함 취소하려면 글꼴 이름에 + 기호를 접두사로 사용하십시오. 예: &quot;+Helvetica&quot;.*

1. 포함된 글꼴의 사용 중 하위 세트만 포함하려면 **포함된 모든 글꼴 하위 집합**&#x200B;을 선택합니다.

   >[!NOTE]
   >
   >*일부 글꼴 포함 취소&#x200B;**와 함께 이 옵션을 사용하는 경우 글꼴**추가&#x200B;****를 포함 취소 목록에 있는 글꼴은 그대로 포함되어 있지 않습니다.*

   >[!NOTE]
   >
   >*글꼴 하위 설정은 글꼴의 일부만을 임베드하는 기술입니다. 글꼴 하위 집합은 문서에 사용된 문자만 포함합니다.*

### 투명도 {#transparency}

PDF 문서에 투명도가 포함된 아트웍이 포함되어 있는 경우 PDF Optimizer 설정을 사용하여 투명도를 병합하고 파일 크기를 줄일 수 있습니다.

>[!NOTE]
>
>Acrobat 4.0 이상이 Target PDF 버전으로 선택된 경우 모든 투명 개체가 병합됩니다. 다른 Target PDF 버전의 경우 투명도가 지원되므로 투명도 설정을 구성할 수 있습니다.

PDF 문서를 최적화하는 동안 투명도 설정을 구성하려면 **투명도**&#x200B;를 선택합니다.

**투명도** 수준보존될 벡터 정보의 양을 지정합니다. 설정이 높을수록 더 많은 벡터 오브젝트가 보존되고, 낮은 설정은 더 많은 벡터 오브젝트를 래스터화합니다.중간 설정은 벡터 양식의 간단한 영역을 유지하고 복잡한 영역을 래스터화합니다. 가장 낮은 설정을 선택하여 모든 아트웍을 래스터화합니다.

>[!NOTE]
>
>래스터화의 양은 페이지의 복잡성과 겹쳐진 개체 유형에 따라 다릅니다.

**이미지, 벡터 아트워크,** 텍스트 및 그라디언트를 비롯한 모든 오브젝트가 래스터화되는 선 아트 및 텍스트 해상도입니다. 지원되는 값은 인치당 1픽셀(ppi)에서 9600ppi입니다.

>[!NOTE]
>
>Line Art 및 Text 해상도는 일반적으로 600-1200ppi로 설정되어야 serif 또는 작은 포인트 크기의 문자 등 고품질 래스터화를 제공할 수 있습니다.

**그라디언트 및** 메쉬를 래스터화하는 그라디언트 및 해상도. 지원되는 값은 1ppi에서 1200ppi입니다.

>[!NOTE]
>
>그라디언트 및 메쉬 해상도는 일반적으로 150-300ppi로 설정해야 합니다. 그라디언트, 그림자 및 페더의 품질은 높은 해상도로 향상되지 않지만 인쇄 시간과 파일 크기는 증가합니다.

**모든 텍스트를 윤곽선으로** 변환모든 문자 개체(포인트 문자, 영역 문자 및 패스 유형)를 윤곽선으로 변환하고 투명도가 포함된 페이지의 모든 문자 글리프 정보를 삭제합니다. 이 옵션을 사용하면 병합하는 동안 텍스트 너비가 일관되게 유지됩니다. 이 옵션을 활성화하면 Acrobat에서 보거나 저해상도 데스크탑 프린터로 인쇄할 때 작은 글꼴이 약간 두껍게 나타납니다. 고해상도 프린터나 이미지 세터에 인쇄되는 유형의 품질에는 영향을 주지 않습니다.

**모든 선을** 윤곽선으로 변환투명도가 포함된 페이지에서 모든 선을 간단한 채워진 패스로 변환합니다. 이 옵션을 사용하면 병합하는 동안 획 너비가 일관되게 유지됩니다. 이 옵션을 활성화하면 가는 선이 약간 더 두껍게 나타나고 병합 성능이 저하될 수 있습니다.

**복잡한** 영역 클립벡터 아트웍과 래스터화된 아트웍의 경계가 개체 패스에 따라 표시되도록 합니다. 이 옵션을 사용하면 결국의 일부분을 발생시키는 연결된 결함을 줄일 수 있습니다

<!--
NOTE to WRITER: Unfinished sentence above.
-->

>[!NOTE]
>
>일부 인쇄 드라이버는 래스터 및 벡터 아트를 다르게 처리하며 경우에 따라 색상 스티칭을 합니다. 일부 인쇄 드라이버별 색상 관리 설정을 비활성화하여 연결 문제를 최소화할 수 있습니다. 이러한 설정은 각 프린터에 따라 다르므로 자세한 내용은 프린터와 함께 제공되는 설명서를 참조하십시오.

중복 인쇄 유지:투명한 아트웍의 색상을 배경색과 혼합하여 중복 인쇄 효과를 만들 수 있습니다.

다음 표는 일반적인 유형의 프린터와 dpi로 측정된 해상도, 기본 화면 측정은 인치당 선 수(lpi) 및 인치당 픽셀 수(ppi)로 측정된 이미지의 리샘플링 해상도를 보여줍니다. 예를 들어 600dpi 레이저 프린터로 인쇄하는 경우 이미지를 리샘플링할 해상도에 170을 입력합니다.

**이미지** 이미지를 선택하여 색상, 회색 음영 및 단색 이미지에 대한 압축 및 리샘플링 옵션을 지정합니다. 파일 크기와 이미지 품질 간의 적절한 균형을 찾기 위해 이러한 옵션을 실험해 볼 수도 있습니다.컬러 및 회색 음영 이미지에 대한 해상도 설정은 파일이 인쇄될 라인 스크린 크기의 1.5배에서 2배여야 합니다. 단색 이미지의 해상도는 출력 장치와 동일해야 하지만 1500dpi보다 높은 해상도로 단색 이미지를 저장하면 이미지 품질을 크게 향상시키지 않고 파일 크기가 커집니다. 맵과 같이 확대되는 이미지는 더 높은 해상도가 필요할 수 있습니다.

>[!NOTE]
>
>단색 이미지를 리샘플링하면 이미지 표시 없음과 같은 예기치 않은 보기 결과가 나타날 수 있습니다. 이러한 경우 리샘플링을 끄고 파일을 다시 변환하십시오. 이 문제는 하위 샘플링에서 발생할 가능성이 가장 높고 쌍입방 다운샘플링에서도 발생할 가능성이 낮습니다.

<table>
 <tbody>
  <tr>
   <th><p><strong>프린터 해상도</strong></p> </th>
   <th><p><strong>기본 라인 화면</strong></p> </th>
   <th><p><strong>이미지 해상도</strong></p> </th>
  </tr>
  <tr>
   <td><p>300dpi(레이저 프린터)</p> </td>
   <td><p>60lpi</p> </td>
   <td><p>120ppi</p> </td>
  </tr>
  <tr>
   <td><p>600dpi(레이저 프린터)</p> </td>
   <td><p>85lpi</p> </td>
   <td><p>170ppi</p> </td>
  </tr>
  <tr>
   <td><p>1200dpi(이미지 세터)</p> </td>
   <td><p>120lpi</p> </td>
   <td><p>240ppi</p> </td>
  </tr>
  <tr>
   <td><p>2400dpi(이미지 세터)</p> </td>
   <td><p>150lpi</p> </td>
   <td><p>300ppi</p> </td>
  </tr>
 </tbody>
</table>

#### 개체 삭제 {#discard-objects}

* **개체 삭제**&#x200B;를 선택하여 PDF에서 제거할 개체를 지정하고 CAD 도면의 곡선을 최적화합니다.
* **모든 양식 제출, 가져오기 및 재설정 작업 취소**:양식 데이터 제출 또는 가져오기와 관련된 모든 작업을 비활성화하고 양식 필드를 재설정합니다. 이 옵션은 작업이 연결된 양식 개체를 유지합니다.
* **모든 JavaScript 작업** 취소:JavaScript를 사용하는 모든 작업을 PDF에서 제거합니다.
* **포함된 페이지 축소판 취소**:포함된 페이지 축소판을 제거합니다. 이 옵션은 큰 문서에서 유용합니다. 페이지 단추를 클릭하면 페이지 축소판을 그리는 데 시간이 오래 걸릴 수 있습니다.
* **부드러운 선을 곡선으로 변환**:CAD 도면에서 곡선을 만드는 데 사용되는 제어점의 수를 줄여 PDF 파일의 크기가 작아지고 화면상의 렌더링이 빨라집니다.
* **포함된 인쇄 설정 취소**:문서에서 페이지 크기 조절 및 이중 모드와 같은 임베드된 인쇄 설정을 제거합니다.
* **책갈피 삭제**:문서에서 모든 책갈피를 제거합니다.
* **양식 필드 분리**:양식 필드는 모양이 변경되지 않고 사용할 수 없게 합니다. 양식 데이터는 페이지와 병합되어 페이지 컨텐츠가 됩니다.
* **모든 대체 이미지** 취소:화면상에서 볼 수 있도록 지정된 버전을 제외한 모든 버전의 이미지를 제거합니다. 일부 PDF에는 화면 해상도가 낮은 화면 보기 및 고해상도 인쇄와 같이 다양한 용도로 동일한 이미지의 여러 버전이 포함되어 있습니다.
* **문서 태그 취소**:문서에서 태그를 제거합니다. 이 경우 텍스트에 대한 액세스 가능성 및 리플로우 기능도 제거됩니다.
* **이미지 조각 감지 및 병합**:얇게 분할된 이미지나 마스크를 찾아 단일 이미지나 마스크로 분할 영역을 병합합니다.
* **포함된 검색 색인 취소**:포함된 검색 색인을 제거하여 파일 크기를 줄입니다.

#### 사용자 데이터 삭제 {#discard-user-data}

**사용자 데이터 삭제**&#x200B;를 선택하여 다른 사용자와 배포 또는 공유하지 않으려는 개인 정보를 제거합니다.

* **모든 주석, Forms 및 멀티미디어** 삭제:PDF에서 모든 주석, 양식, 양식 필드 및 멀티미디어를 제거합니다.
* **모든 개체 데이터 삭제**:PDF에서 모든 개체를 제거합니다.
* **외부 상호 참조 삭제**:다른 문서에 대한 링크를 제거합니다. PDF 내의 다른 위치로 이동하는 링크는 제거되지 않습니다.
* **숨겨진 레이어 컨텐츠 및 보이는 레이어 분리**:파일 크기를 줄입니다. 최적화된 문서는 원본 PDF와 비슷하지만 레이어 정보는 포함되지 않습니다.
* **문서 정보 및 메타데이터** 취소:문서 정보 사전 및 모든 메타데이터 스트림의 정보를 제거합니다. 다른 이름으로 저장 명령을 사용하여 메타데이터 스트림을 PDF의 복사본으로 복원합니다.
* **첨부 파일 삭제**:PDF에 주석으로 추가된 첨부 파일을 포함하여 모든 첨부 파일을 제거합니다. (PDF Optimizer에서는 첨부 파일을 최적화하지 않습니다.)
* **다른 응용 프로그램의 개인 데이터 삭제**:문서를 만든 응용 프로그램에만 유용한 PDF 문서의 정보를 제거합니다. 이 설정은 PDF의 기능에는 영향을 주지 않지만 파일 크기는 줄어듭니다.

### {#clean-up} 정리

문서에서 불필요한 항목을 제거하려면 **정리**를 선택합니다.
이러한 항목에는 문서를 사용하기 위해 사용되지 않거나 불필요한 요소가 포함됩니다. 특정 요소를 제거하면 PDF 기능에 심각한 영향을 줄 수 있습니다. 기본적으로 기능에 영향을 주지 않는 요소만 선택됩니다. 다른 옵션 제거의 의미를 잘 모를 경우 기본 선택 항목을 사용합니다.

**압축**

드롭다운 메뉴에서 다음 압축 옵션 중 하나를 선택합니다.

* 전체 파일 압축
* 문서 구조 압축
* 압축 제거
* 압축에 영향을 주지 않음

**Flate를 사용하여 인코딩되지 않은 스트림을 인코딩합니다**.인코딩되지 않은 모든 스트림에 Flate 압축을 적용합니다.

**잘못된 책갈피 삭제**:삭제된 문서의 페이지를 가리키는 책갈피를 제거합니다.

**참조되지 않은 명명된 대상 삭제**:PDF 문서 내에서 내부적으로 참조되지 않는 명명된 대상을 제거합니다. 이 옵션은 다른 PDF 파일 또는 웹 사이트의 링크를 확인하지 않습니다.

**신속한 웹 보기를 위해 PDF 최적화**:웹 서버에서 한 번에 페이지(바이트 서비스)를 다운로드할 수 있도록 PDF 문서를 재구성합니다.

**LZW 인코딩을 사용하는 스트림에서 Flash를 대신 사용하십시오**.LZW 인코딩을 사용하는 모든 콘텐츠 스트림 및 이미지에 Create 압축을 적용합니다.

**잘못된 링크 삭제**:잘못된 대상으로 이동하는 링크를 제거합니다.

**페이지 컨텐츠 최적화**:모든 줄 끝 문자를 공백 문자로 변환하여 Flate 압축을 향상시킵니다.

## Microsoft Excel 설정(Windows 전용) {#microsoft-excel-settings-windows-only}

이러한 옵션은 Microsoft Excel 파일을 변환하는 방법을 결정합니다. 이러한 옵션에 액세스하는 방법에 대한 지침은 [파일 유형 설정 만들기 또는 편집](#create-or-edit-file-type-settings)을 참조하십시오.

**OpenOffice를 폴백 변환기로 사용해 보기**:이 옵션을 선택하고 Microsoft Excel을 사용한 변환이 실패하거나 지정된 제한 시간 내에 도달하면 PDF Generator는 OpenOffice를 사용하여 변환을 시도합니다. OpenOffice를 사용한 변환이 실패하거나 지정된 제한 시간 내에 도달하면 예외가 로그 파일에 기록됩니다.

**파일 이름 확장자**:이 응용 프로그램에 허용되는 파일 형식의 파일 이름 확장자를 쉼표로 구분하여 지정합니다. 기본값은 `xls,xlsx`입니다. 확장 이전 또는 확장 사이의 공백을 포함하지 마십시오.

**PDF/A-1a 호환 파일** 만들기:PDF/A-1b:2005 RGB Adobe PDF 설정을 강제로 사용합니다.

**Adobe PDF에 책갈피 추가**:Excel 워크시트 이름을 책갈피로 변환합니다. 이 옵션은 기본적으로 선택되어 있습니다.

**단일 페이지에 워크시트** 맞추기:단일 페이지의 워크시트에 맞게 텍스트 크기를 줄입니다.

**전체 통합 문서 변환**:Excel 파일의 모든 워크시트를 변환합니다. 이 옵션을 선택하지 않으면 현재 페이지만 변환됩니다.

**자동으로 매크로 실행**:문서를 변환하기 전에 Excel 문서에서 매크로(예: 현재 시간을 삽입하는 매크로)를 실행합니다.

**문서 정보 변환**:소스 파일의 문서 정보를 기반으로 PDF 문서 속성을 추가합니다. 여기에는 문서 제목, 작성자, 제목 및 키워드와 같은 정보가 포함됩니다.

**Adobe PDF에 링크 추가**:소스 파일의 하이퍼링크를 PDF 문서의 하이퍼링크로 변환합니다.

**소스 파일을 Adobe PDF에 첨부**:이 옵션을 선택하면 원본 Excel 스프레드시트가 생성된 PDF 문서 내에 첨부 파일로 삽입됩니다.

**태그 있는 Adobe PDF으로 액세서빌러티 및 Reflow 활성화**:PDF 문서에 태그를 삽입하여 액세서빌러티 및 리플로우를 활성화합니다.

**로드할 Excel 주소 목록**:기본적으로(보안상의 이유로) Excel 파일을 PDF로 변환할 때 Excel 추가 기능이 실행되지 않습니다. 전환 중에 특정 Excel 추가 기능을 실행할 수 있도록 하려면 Add-in의 이름에 대한 쉼표로 구분된 목록을 제공하십시오.

**변환할 워크시트 목록**:이 상자가 비어 있으면 Excel 스프레드시트의 모든 워크시트가 생성된 PDF에 포함됩니다. 워크시트 하위 집합을 선택적으로 변환하려면 워크시트 이름의 쉼표로 구분된 목록을 제공합니다.

## Microsoft PowerPoint 설정(Windows 전용) {#microsoft-powerpoint-settings-windows-only}

이러한 옵션은 Microsoft PowerPoint 파일을 변환하는 방법을 결정합니다. 이러한 옵션에 액세스하는 방법에 대한 지침은 [파일 유형 설정 만들기 또는 편집](/help/forms/using/admin-help/configuring-file-type-settings1.md#create-or-edit-file-type-settings)을 참조하십시오.

**[!UICONTROL OpenOffice를 폴백 변환기로 사용해 보기]**:이 옵션을 선택하고 Microsoft PowerPoint를 사용한 변환이 실패하거나 지정된 제한 시간 내에 도달하면 PDF Generator는 OpenOffice를 사용하여 변환을 시도합니다. OpenOffice를 사용한 변환이 실패하거나 지정된 제한 시간 내에 도달하면 예외가 로그 파일에 기록됩니다.

**[!UICONTROL 파일 이름 확장자]**:이 응용 프로그램에 허용되는 파일 형식의 파일 이름 확장자를 쉼표로 구분하여 지정합니다. 기본값은 ppt,pptx입니다. 확장 이전 또는 확장 사이의 공백을 포함하지 마십시오.

**[!UICONTROL 문서 정보 변환]**:제목, 제목, 제목, 작성자, 키워드, 관리자, 회사, 범주 및 주석을 비롯한 소스 파일의 속성 대화 상자에서 문서 정보를 추가합니다. 이 옵션은 기본적으로 선택되어 있습니다.

**[!UICONTROL Adobe PDF에 책갈피 추가]**:PowerPoint 제목을 책갈피로 변환합니다. 이 옵션은 기본적으로 선택되어 있습니다.

**[!UICONTROL 소스 파일을 Adobe PDF에 첨부]**:소스 파일을 PDF 파일에 첨부 파일로 추가합니다. 이 옵션은 기본적으로 선택 해제되어 있습니다.

**[!UICONTROL 태그 있는 Adobe PDF으로 액세서빌러티 및 Reflow 활성화]**:PDF 파일에 태그를 포함합니다. 이 옵션은 기본적으로 선택 해제되어 있습니다.

**[!UICONTROL 멀티미디어를 PDF 멀티미디어로 변환]**:가능하면 멀티미디어를 PDF 멀티미디어로 변환합니다. 이 옵션은 기본적으로 선택되어 있습니다.

**[!UICONTROL 발표자 노트 변환]**:발표자 노트를 PDF로 변환합니다.

**[!UICONTROL 자동으로 매크로 실행]**:문서를 변환하기 전에 PowerPoint 문서에서 매크로(예: 현재 시간을 삽입하는 매크로)를 실행합니다.

**[!UICONTROL PowerPoint 프린터 설정을 기반으로 한 PDF 레이아웃]**:PowerPoint 프린터 설정을 사용하여 PDF 문서의 레이아웃을 지정합니다.

**[!UICONTROL Adobe PDF에 링크 추가]**:파일을 변환할 때 기존 링크를 유지합니다. 링크의 모양은 일반적으로 변경되지 않습니다. [액세스 가능성 활성화] 옵션도 선택된 경우에만 링크를 만들 수 있습니다. 이 옵션은 기본적으로 선택 해제되어 있습니다.

**[!UICONTROL Adobe PDF에서 슬라이드 전환 저장]**:슬라이드 전환을 변환합니다. 이 옵션은 기본적으로 선택되어 있습니다.

**[!UICONTROL Adobe PDF에서 애니메이션 저장]**:변환된 애니메이션을 PDF 파일에 저장합니다.

**[!UICONTROL 숨겨진 슬라이드를 PDF 페이지로 변환]**:숨겨진 슬라이드를 변환합니다.

**[!UICONTROL PDF/A-1a 호환 파일]** 만들기:PDF/A-1b:2005 RGB Adobe PDF 설정을 강제로 사용합니다. PDF 파일을 만들 때 일부 PowerPoint 기능이 변환되지 않습니다. Acrobat에서 PowerPoint 전환이 동등한 전환을 사용하지 않는 경우 유사한 전환 대신 동일한 슬라이드에 여러 애니메이션 효과가 있는 경우 하나의 효과가 사용됩니다. 페이지 전환 및 글머리 기호가 전환됩니다.

## Microsoft Project 설정(Windows만 해당) {#microsoft-project-settings-windows-only}

이러한 옵션은 Microsoft Project 파일을 변환하는 방법을 결정합니다. 이러한 옵션에 액세스하는 방법에 대한 지침은 [파일 유형 설정 만들기 또는 편집](#create-or-edit-file-type-settings)을 참조하십시오.

1. **[!UICONTROL 파일 이름]** 확장자: 이 응용 프로그램에서 사용할 수 있는 파일 형식의 파일 이름 확장자를 쉼표로 구분하여 지정합니다. 기본값은 `mpp`입니다. 확장 이전 또는 확장 사이의 공백을 포함하지 마십시오.

1. **[!UICONTROL 문서 정보 변환]**:제목, 제목, 제목, 작성자, 키워드, 관리자, 회사, 범주 및 주석을 비롯한 소스 파일의 속성 대화 상자에서 문서 정보를 추가합니다. 이 옵션은 기본적으로 선택되어 있습니다.
1. **[!UICONTROL 소스 파일을 Adobe PDF에 첨부]**:소스 파일을 PDF 파일에 첨부 파일로 추가합니다.
1. **[!UICONTROL PDF/A-1a 호환 파일]** 만들기:PDF/A-1b:2005 RGB Adobe PDF 설정을 강제로 사용합니다.
1. **[!UICONTROL 자동으로 매크로 실행]**:문서를 변환하기 전에 Microsoft Project 문서에서 매크로(예: 현재 시간을 삽입하는 매크로)를 실행합니다.

## Microsoft Word 설정(Windows 전용) {#microsoft-word-settings-windows-only}

이러한 옵션은 Microsoft Word 파일을 변환하는 방법을 결정합니다. 이러한 옵션에 액세스하는 방법에 대한 지침은 [파일 유형 설정 만들기 또는 편집](#create-or-edit-file-type-settings)을 참조하십시오.

**[!UICONTROL OpenOffice를 폴백 변환기로 사용해 보기]**:이 옵션을 선택하고 Microsoft Word를 사용한 변환이 실패하거나 지정된 제한 시간 내에 도달하면 PDF Generator는 OpenOffice를 사용하여 변환을 시도합니다. OpenOffice를 사용한 변환이 실패하거나 지정된 제한 시간 내에 도달하면 예외가 로그 파일에 기록됩니다.

**[!UICONTROL 파일 이름 확장자]**:이 응용 프로그램에 허용되는 파일 형식의 파일 이름 확장자를 쉼표로 구분하여 지정합니다. 기본값은 `doc,docx,rtf,txt`입니다. 확장 이전 또는 확장 사이의 공백을 포함하지 마십시오.

**[!UICONTROL 문서 정보 변환]**:제목, 제목, 제목, 작성자, 키워드, 관리자, 회사, 범주 및 주석을 비롯한 소스 파일의 속성 대화 상자에서 문서 정보를 추가합니다. 이 옵션은 기본적으로 선택되어 있습니다.

**[!UICONTROL Adobe PDF에 책갈피 추가]**:제목을 책갈피로 변환합니다. 이 옵션은 기본적으로 선택되어 있습니다.

**[!UICONTROL 소스 파일을 Adobe PDF에 첨부]**:소스 파일을 PDF 파일에 첨부 파일로 추가합니다.

**[!UICONTROL 상호 참조 및 목차를 링크로 변환합니다]**.모든 상호 참조 및 목차 항목을 링크로 변환합니다. 이 옵션은 기본적으로 선택되어 있습니다.

**[!UICONTROL 태그 있는 Adobe PDF으로 액세서빌러티 및 Reflow 활성화]**:PDF 파일에 태그를 포함합니다. 이 옵션은 기본적으로 선택되어 있습니다.

**[!UICONTROL PDF/A-1a 호환 파일]** 만들기:이 옵션을 선택하면 PDF/A-1b:2005 RGB Adobe PDF 설정이 강제로 사용됩니다.

**[!UICONTROL 자동으로 매크로 실행]**:문서를 변환하기 전에 Word 문서에서 매크로(예: 현재 시간을 삽입하는 매크로)를 실행합니다.

**[!UICONTROL Adobe PDF에서 문서 마크업 유지]**:Word 문서의 마크업을 PDF 파일의 주석으로 변환합니다.

**[!UICONTROL Adobe PDF에 링크 추가]**:소스 파일의 하이퍼링크를 PDF 문서의 하이퍼링크로 변환합니다.

**[!UICONTROL 각주 및 미주 링크 변환]**:각주 및 각주 인용문의 링크를 PDF 문서의 메모에 만듭니다.

**[!UICONTROL Adobe PDF에서 표시된 주석을 메모로 변환]**:Word 문서의 주석을 PDF 문서의 텍스트 메모로 변환합니다.

**[!UICONTROL 고급 태그 지정 사용]**:향상된 접근성을 위해 고급 태그를 추가합니다.

**[!UICONTROL 모든 스타일을 책갈피로 변환]**:Word 문서의 모든 스타일을 PDF 문서의 책갈피로 변환합니다.

**[!UICONTROL 수준이 있는 스타일]**:PDF 문서에서 책갈피로 변환할 Word 문서의 스타일을 지정합니다. 책갈피 수준도 지정합니다. 이 기능을 사용하려면 **[!UICONTROL 모든 스타일을 책갈피로 변환]** 옵션을 선택 취소하고 스타일 이름을 다음 형식으로 지정합니다.

styleName1=level1[,styleName2=level2...]

Microsoft Word 스타일 이름에 쉼표(,) 또는 등호(=)가 있으면 특수 문자 앞에 이스케이프 문자(&quot;\_)를 입력합니다. 예를 들어 &quot;Heading, 1&quot;이라는 스타일을 Heading\, 1로 지정합니다.

## Microsoft Visio 설정(Windows 전용) {#visio}

**문서 정보 변환**:제목, 제목, 제목, 작성자, 키워드, 관리자, 회사, 범주 및 주석을 비롯한 소스 파일의 속성 대화 상자에서 문서 정보를 추가합니다. 이 옵션은 기본적으로 선택되어 있습니다. 이 옵션은 기본적으로 활성화되어 있습니다.

**Adobe PDF에 링크 추가**:모든 링크를 유지합니다. 이 옵션은 기본적으로 선택되어 있습니다.

**Adobe PDF에 책갈피 추가**:제목을 책갈피로 변환합니다. 이 옵션은 기본적으로 선택되어 있습니다.

**소스 파일을 Adobe PDF에 첨부**:소스 파일을 PDF 파일에 첨부 파일로 추가합니다.

**Adobe PDF에서 항상 레이어 분리:**&#x200B;모든 Visio 레이어를 병합합니다.

**모든 페이지 변환**:Visio 파일의 모든 페이지를 변환합니다.

**Adobe Acrobat에서 볼 때 레이어 패널 열기**:Visio 레이어를 병합하지 않은 경우 Acrobat을 사용하여 열 때 PDF 파일에 보존된 레이어를 지정할 수 있는 창을 엽니다. 이 옵션은 기본적으로 선택되어 있습니다.

**PDF/A-1b 호환 파일** 작성:Adobe PDF 설정 PDF/A-1b:2005(RGB)를 강제로 사용합니다.

**주석을 Adobe PDF 주석으로 변환**:Visio 노트를 PDF 주석으로 변환합니다.

## Microsoft Publisher 설정(Windows 전용) {#microsoft-publisher-settings-windows-only}

이러한 옵션은 Microsoft Publisher 파일을 변환하는 방법을 결정합니다. 이러한 옵션에 액세스하는 방법에 대한 지침은 [파일 유형 설정 만들기 또는 편집](#create-or-edit-file-type-settings)을 참조하십시오.

**[!UICONTROL 파일 이름 확장자]**:이 응용 프로그램에 허용되는 파일 형식의 파일 이름 확장자를 쉼표로 구분하여 지정합니다. 기본값은 `pub`입니다. 확장 이전 또는 확장 사이의 공백을 포함하지 마십시오.

## AutoCAD 설정(Windows 전용) {#autocad-settings-windows-only}

이러한 옵션은 AutoCAD 파일을 변환하는 방법을 결정합니다. 이러한 옵션에 액세스하는 방법에 대한 지침은 [파일 유형 설정 만들기 또는 편집](/help/forms/using/admin-help/configuring-file-type-settings1.md#create-or-edit-file-type-settings)을 참조하십시오.

**[!UICONTROL 파일 이름 확장자]**:이 응용 프로그램에 허용되는 파일 형식의 파일 이름 확장자를 쉼표로 구분하여 지정합니다. 기본값은 `dwg`입니다. 확장 이전 또는 확장 사이의 공백을 포함하지 마십시오.

**[!UICONTROL 문서 정보 변환]**:제목, 제목, 제목, 작성자, 키워드, 관리자, 회사, 범주 및 주석을 비롯한 소스 파일의 속성 대화 상자에서 문서 정보를 추가합니다. 이 옵션은 기본적으로 선택되어 있습니다.

**[!UICONTROL Adobe PDF에 책갈피 추가]**:제목을 책갈피로 변환합니다.

**[!UICONTROL Adobe PDF에서 항상 레이어 분리:]**&#x200B;모든 AutoCAD 레이어를 병합합니다.

**[!UICONTROL Adobe Acrobat에서 볼 때 레이어 창 열기]**:Acrobat에서 PDF를 열 때 레이어 구조를 표시합니다.

**[!UICONTROL PDF/E-1 호환 파일]** 만들기:PDF/E-1 규격의 파일을 만듭니다. PDF/E는 엔지니어링 및 기술 문서 교환을 위한 ISO 표준입니다. PDF/E-1에 대한 자세한 내용은 [Adobe 및 업계 표준](https://www.adobe.com/enterprise/standards/index.html)을 참조하십시오.

**[!UICONTROL 모든 레이아웃 변환]**:PDF에 모든 레이아웃 포함

**[!UICONTROL 모델 공간을 3D로 변환]**:이 옵션을 선택하면 모델 공간 레이아웃이 PDF에서 3D 주석으로 변환됩니다.

**[!UICONTROL Adobe PDF에 링크 추가]**:선택하는 경우 모든 링크가 유지됩니다.

**[!UICONTROL 소스 파일을 Adobe PDF에 첨부]**:소스 파일을 PDF 파일에 첨부 파일로 추가합니다.

**[!UICONTROL PDF/A-1b 호환 파일]** 작성:PDF/A-1b Adobe PDF 설정을 강제로 사용합니다.

**[!UICONTROL 모든 레이어 변환]**:기본적으로 PDF Generator는 파일 내의 모든 레이어 대신 AutoCAD 파일의 기본 레이어만 PDF로 변환합니다. 파일의 모든 레이어를 변환하려면 이 옵션을 선택합니다.

**[!UICONTROL 포함 비율 정보]**:드로잉 비율 정보를 그대로 유지합니다.

**[!UICONTROL 현재 레이아웃 변환]**:PDF에 현재 레이아웃만 포함합니다.

**[!UICONTROL 변환할 AutoCAD 레이아웃 목록]**:AutoCAD 드로잉에는 여러 레이아웃이 있을 수 있습니다. 이 상자가 비어 있으면 AutoCAD 드로잉의 모든 레이아웃이 생성된 PDF 문서에 포함됩니다. 레이아웃의 하위 집합을 선택적으로 변환하려면, 쉼표로 구분된 레이아웃 이름 목록을 제공합니다.

## OpenOffice 설정 {#openoffice-settings}

이러한 옵션은 OpenOffice 파일을 변환하는 방법을 결정합니다. 이러한 옵션에 액세스하는 방법에 대한 지침은 [파일 유형 설정 만들기 또는 편집](/help/forms/using/admin-help/configuring-file-type-settings1.md#create-or-edit-file-type-settings)을 참조하십시오.

**PDFMaker를 폴백 변환기로 사용해 보십시오**.이 옵션을 선택하고 OpenOffice를 사용한 변환이 실패하거나 지정된 제한 시간 내에 도달하면 PDF Generator는 PDFMaker를 사용하여 변환을 시도합니다. PDFMaker를 사용한 변환이 실패하거나 지정된 시간 제한 값에 도달하면 예외가 로그 파일에 기록됩니다.

**파일 이름 확장자**:이 응용 프로그램에 허용되는 파일 형식의 파일 이름 확장자를 쉼표로 구분하여 지정합니다. 기본값은 `odt,odp,ods,odg,odf,sxw,sxi,sxd`입니다. 확장 이전 또는 확장 사이의 공백을 포함하지 마십시오.

**범위**:모든 페이지를 변환하거나 특정 페이지 또는 페이지 범위를 지정합니다. 페이지 범위가 정의되지 않은 경우 모든 페이지가 변환됩니다. 페이지 범위를 내보내려면 3-6 형식을 사용하십시오. 단일 페이지를 내보내려면 7;9;11 형식을 사용하십시오. 3-6;8;10;12와 같은 형식을 사용하여 페이지 범위와 단일 페이지의 조합을 내보낼 수 있습니다.

**페이지 방향**:일반 텍스트 파일의 경우 변환된 PDF 문서의 세로 또는 가로 중 하나를 선택합니다.

**이미지**:이미지를 변환하는 방법을 구성합니다. 포함된 미리 보기가 있는 EPS 이미지는 미리 보기로만 내보내집니다. 포함된 미리 보기가 없는 EPS 이미지는 빈 자리 표시자로 내보내집니다. 이미지의 손실 없는 압축으로 모든 픽셀은 유지됩니다. 이미지의 JPEG 압축과 고품질 레벨의 경우 거의 모든 픽셀이 그대로 유지됩니다. 품질이 낮은 경우 일부 픽셀이 손실되고 가공물이 도입되지만 파일 크기는 줄어듭니다.

**일반**:태그가 있는 PDF를 변환하거나 Writer 및 FormCalc 문서 노트, Imate 슬라이드 전환 효과 또는 빈 페이지를 PDF로 내보내는 옵션을 활성화합니다. 태그를 내보낼 때 파일 크기가 크게 늘어날 수 있습니다. 내보낸 일부 태그는 목차, 하이퍼링크 및 컨트롤입니다.

양식 제출 방법을 지정할 수도 있습니다. 옵션은 XML, FDF, PDF 또는 HTML입니다. 이 설정은 문서에 설정한 컨트롤의 URL 속성을 무시합니다. PDF 문서에 대해 하나의 공통 설정만 선택할 수 있습니다.

* PDF(전체 문서 전송)
* FDF(컨트롤 내용 전송)
* HTML
* XML

**태그 지정된 PDF**:OpenOffice 문서에서 태그가 있는 PDF를 만들 수 있습니다. 태그 있는 PDF에는 문서 내용의 구조에 대한 정보가 포함되어 있습니다. 이 기능은 다른 화면을 사용하는 장치 및 화면 판독기 소프트웨어를 사용하는 경우 문서를 표시할 때 도움이 됩니다. 또한 액세서빌러티 소프트웨어에서 PDF 문서의 내용을 큰 소리로 읽는 등 PDF 문서를 사용하여 다양한 유용한 작업을 수행할 수 있습니다.

**내보내기 참고**:OpenOffice 문서의 노트를 생성된 PDF 문서의 메모로 변환합니다.

**전환 효과 사용**:OpenOffice 프레젠테이션의 슬라이드 전환 효과를 해당 PDF 전환 효과로 변환합니다.

**Forms 형식 제출**:PDF 문서 사용자가 작성하고 인쇄할 수 있는 PDF 양식을 만듭니다.

**자동으로 삽입된 빈 페이지 내보내기**:이 옵션을 선택하면 자동으로 삽입된 빈 페이지가 생성된 PDF 문서에 포함됩니다. PDF 문서를 양면 인쇄하는 경우 유용합니다. 예를 들어 장의 첫 번째 페이지가 항상 홀수 페이지에서 시작되도록 책을 구성할 수 있습니다. 이전 장이 홀수 페이지에서 종료되면 OpenOffice에서 빈 짝수 페이지를 설정합니다. 이 옵션은 생성된 PDF에 해당 짝수 페이지의 포함 여부를 제어합니다.

## 기타 응용 프로그램 설정(Windows만 해당) {#other-applications-settings-windows-only}

관리 콘솔을 통해 다른 응용 프로그램에 대한 설정을 변경할 수 없습니다.지원되는 파일 형식의 파일 이름 확장자를 표시합니다. 이러한 설정에 액세스하는 방법에 대한 지침은 [파일 유형 설정 만들기 또는 편집](https://help.adobe.com/en_US/AEMForms/6.1/AdminHelp/WS92d06802c76abadb-5145d5d12905ce07e7-7e42.2.html)을 참조하십시오.

* Corel WordPerfect:`wpd`
* Adobe PageMaker:`pmd, pm6, p65, pm`
* Adobe FrameMaker:`fm`
* Adobe Photoshop: `psd`

이러한 파일 유형에 대한 지원을 사용자 정의해야 할 수 있습니다. 자세한 내용은 [AEM 양식](https://www.adobe.com/go/learn_aemforms_programming_62)으로 프로그래밍의 &quot;추가 기본 파일 형식 지원 추가&quot;를 참조하십시오.

PDFG 네트워크 프린터 구성에 대한 도움말은 [PDFG 네트워크 프린터 설정(Windows만 해당)](/help/forms/using/admin-help/setting-pdfg-network-printer-windows.md)을 참조하십시오.
