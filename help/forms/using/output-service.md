---
title: 출력 서비스
description: AEM Document Services의 일부인 출력 서비스에 대해 설명합니다.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
docset: aem65
feature: Document Services,Output Service
exl-id: 82b0293a-711f-4769-9b11-b4cff4fec021
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 5%

---

# 출력 서비스{#output-service}

## 개요 {#overview}

출력 서비스는 AEM Document Services의 일부인 OSGi 서비스입니다. 출력 서비스는 AEM Forms Designer의 다양한 출력 형식 및 출력 디자인 기능을 지원합니다. 출력 서비스는 XFA 템플릿 및 XML 데이터를 변환하여 다양한 형식의 인쇄 문서를 생성할 수 있습니다.

Output 서비스를 사용하면 다음과 같은 기능을 제공하는 애플리케이션을 만들 수 있습니다.

* XML 데이터로 템플릿 파일을 채워 최종 양식 문서를 생성합니다.
* 비대화형 PDF, PostScript, PCL 및 ZPL 인쇄 스트림을 포함하여 다양한 형식의 출력 양식을 생성합니다.
* XFA 양식 PDF에서 인쇄 PDF를 생성합니다.
* 제공된 템플릿과 여러 데이터 세트를 병합하여 PDF, PostScript, PCL 및 ZPL 문서를 대량으로 생성합니다.

>[!NOTE]
>
>출력 서비스는 32비트 응용 프로그램입니다. Microsoft Windows에서는 32비트 애플리케이션에서 최대 2GB의 메모리를 사용할 수 있습니다. 이 제한은 출력 서비스에도 적용됩니다.

## 비대화형 양식 문서 만들기 {#creating-non-interactive-form-documents}

![usingoutput_modified](assets/usingoutput_modified.png)

일반적으로 AEM Forms Designer을 사용하여 템플릿을 만듭니다. 출력 서비스의 `generatePDFOutput` 및 `generatePrintedOutput` API를 사용하면 이러한 템플릿을 PDF, PostScript, ZPL, PCL을 비롯한 다양한 형식으로 직접 변환할 수 있습니다.

`generatePDFOutput` 작업은 PDF을 생성하는 반면 `generatePrintedOutput` 작업은 PostScript, ZPL 및 PCL 형식을 생성합니다. 두 작업의 첫 번째 매개 변수는 템플릿 파일(예: `ExpenseClaim.xdp`)의 이름 또는 템플릿을 포함하는 Document 개체를 허용합니다. 템플릿 파일의 이름을 지정할 때 컨텐트 루트도 템플릿이 들어 있는 폴더의 경로로 지정합니다. `PDFOutputOptions` 또는 `PrintedOutputOptions` 매개 변수를 사용하여 콘텐츠 루트를 지정할 수 있습니다. 이러한 매개 변수를 사용하여 지정할 수 있는 기타 옵션에 대한 자세한 내용은 Javadoc을 참조하십시오.

두 번째 매개 변수는 출력 문서를 생성하는 동안 템플릿과 병합되는 XML 문서를 허용합니다.

`generatePDFOutput` 작업에서는 XFA 기반 PDF 양식을 입력으로 허용하고 비대화형 버전의 PDF 양식을 출력으로 반환할 수도 있습니다.

## 비대화형 양식 문서 생성 {#generating-non-interactive-form-documents}

하나 이상의 템플릿과 각 템플릿에 대한 여러 XML 데이터 레코드가 있는 시나리오를 고려하십시오.

출력 서비스의 `generatePDFOutputBatch` 및 `generatePrintedOutputBatch` 작업을 사용하여 각 레코드에 대한 인쇄 문서를 생성합니다.

레코드를 하나의 문서로 결합할 수도 있습니다. 두 작업 모두 4개의 매개 변수를 사용합니다.

첫 번째 매개 변수는 임의의 문자열을 키로 포함하고 템플릿 파일의 이름을 값으로 포함하는 맵입니다.

두 번째 매개변수는 값이 XML 데이터가 포함된 문서 객체인 다른 맵입니다. 키는 첫 번째 매개변수에 지정한 키와 동일합니다.

`generatePDFOutputBatch` 또는 `generatePrintedOutputBatch`에 대한 세 번째 매개 변수는 각각 `PDFOutputOptions` 또는 `PrintedOutputOptions` 형식입니다.

매개 변수 형식은 `generatePDFOutput` 및 `generatePrintedOutput` 작업에 대한 매개 변수 형식과 동일하며 동일한 효과를 갖습니다.

네 번째 매개 변수는 각 레코드에 대해 별도의 파일을 생성할 수 있는지 여부를 지정하는 데 사용하는 `BatchOptions` 형식입니다. 이 매개 변수의 기본값은 false입니다.

`generatePrintedOutputBatch`과(와) `generatePDFOutputBatch`이(가) 모두 `BatchResult` 형식의 값을 반환합니다. 값에는 생성된 문서 목록이 포함됩니다. 또한 생성된 각 문서와 관련된 정보가 들어 있는 XML 형식의 메타데이터 문서가 포함되어 있습니다.
