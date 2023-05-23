---
title: AEM Document Services 개요
seo-title: Overview of AEM Document Services
description: AEM Document Services는 PDF 문서 생성, 어셈블 및 보안을 위한 일련의 OSGi 서비스입니다.
seo-description: AEM Document Services are a set of OSGi Services for creating, assembling, and securing PDF Documents.
uuid: 439144b7-f805-4819-9ed9-a6e9e374b5ed
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 10d406db-ac10-479b-b08b-d0735116a12b
docset: aem65
exl-id: 4c8a3877-1a3c-410d-ad1f-69c73ba4fcc1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1402'
ht-degree: 0%

---

# AEM Document Services 개요{#overview-of-aem-document-services}

AEM Document Services는 PDF 문서 생성, 어셈블 및 보안을 위한 일련의 OSGi 서비스입니다. 문서 서비스에는 다음 서비스가 포함됩니다.

## 출력 서비스 {#output-service}

[출력] 서비스를 사용하면 PDF, 레이저 프린터 형식 및 레이블 프린터 형식 등 다양한 형식의 문서를 만들 수 있습니다. 레이저 프린터 형식은 PostScript 및 PCL(Printer Control Language)입니다. 다음 목록은 레이블 프린터 형식을 지정합니다.

* 얼룩말(ZPL)
* 중간(IPL)
* Datamax (DPL)
* TecToshiba (TPCL)

문서를 네트워크 프린터, 로컬 프린터 또는 파일 시스템의 파일로 보낼 수 있습니다. 출력 서비스는 XML 양식 데이터를 양식 디자인과 병합하여 문서를 생성합니다. 출력 서비스는 XML 양식 데이터를 문서에 병합하지 않고 문서를 생성할 수 있습니다. 그러나 기본 워크플로우는 데이터를 문서에 병합하는 것입니다.

>[!NOTE]
>
>폼 디자인은 일반적으로 디자이너를 사용하여 만들어집니다. Output 서비스의 양식 디자인을 만드는 방법에 대한 자세한 내용은 디자이너 도움말을 참조하십시오.

출력 서비스를 사용하여 XML 데이터를 양식 디자인과 병합하면 비대화형 PDF 문서가 만들어집니다. 비대화형 PDF 문서에서는 사용자가 해당 필드에 데이터를 입력할 수 없습니다. 반대로 Forms 서비스를 사용하여 사용자가 해당 필드에 데이터를 입력할 수 있는 대화형 PDF 양식을 만들 수 있습니다.

다음 네 가지 출력 서비스 작업을 사용할 수 있습니다.

* **generatePDFOuput**: 양식 디자인을 데이터와 병합하여 PDF 문서를 생성합니다
* **generatePrintedOutput**: 양식 디자인을 양식 데이터와 병합하여 레이저나 라벨 네트워크 프린터로 보낼 문서를 생성합니다

* **generatePDFOutputBatch**: 한 번의 호출로 여러 템플릿을 여러 데이터 레코드와 병합하여 PDF 파일 배치를 생성합니다. 모든 PDF을 결합하여 단일 PDF을 생성하는 옵션도 있습니다
* **generatePrintedOutputBatch**: 한 번의 호출로 여러 템플릿을 여러 데이터 레코드와 병합하여 여러 인쇄 문서(PS,PCL,ZPL,DPL,IPL,TPCL)를 생성합니다. 단일 인쇄 문서를 생성하는 옵션도 있습니다.

## 어셈블러 서비스 {#assembler-service}

어셈블러 서비스를 사용하면 PDF 및 XDP 문서를 결합, 재배열 및 강화하고 PDF 문서에 대한 정보를 얻을 수 있습니다. 어셈블러 서비스에 제출된 각 작업에는 DDX(Document Description XML) 문서, 소스 문서 및 외부 리소스(문자열 및 그래픽)가 포함됩니다. DDX 문서는 소스 문서를 사용하여 결과 문서 세트를 생성하는 방법에 대한 지침을 제공합니다.

위에서 언급한 기능 외에도 어셈블러 서비스는 다음과 같습니다.

* PDF 문서를 PDF/A 표준으로 변환합니다.
* PDF forms, XML 양식(디자이너에서 생성) 및 PDF forms(Acrobat에서 생성)를 PDF/A-1b, PDF/A-2b 및 PDFA/A-3b로 변환합니다.
* 서명되거나 서명되지 않은 PDF 문서를 변환합니다(디지털 서명 필요).
* PDF/A 파일의 준수 여부를 확인하고 필요한 경우 변환합니다.

### DDX 정보 {#about-ddx}

어셈블러 서비스를 사용하는 경우 DDX(Document Description XML)라는 XML 기반 언어를 사용하여 원하는 출력을 설명합니다. DDX는 문서의 구성 요소를 나타내는 선언적 마크업 언어입니다. 이러한 구성 요소에는 PDF 문서, XDP 문서, XDP 양식 조각 및 댓글, 책갈피 및 스타일이 지정된 텍스트와 같은 기타 요소가 포함됩니다.

DDX 문서는 다음과 같은 특성을 갖는 결과 문서를 지정할 수 있습니다.

* 여러 PDF 문서에서 어셈블된 PDF 문서
* 단일 PDF 문서와 별도로 구분된 여러 PDF 문서
* 자체 포함된 사용자 인터페이스와 여러 PDF 및 비 PDF 문서를 포함하는 PDF Portfolio
* 여러 XDP 문서에서 어셈블된 XDP 문서
* XDP 문서에 동적으로 삽입되는 XML 조각이 포함된 XDP 문서
* XDP 문서를 패키지하는 PDF 문서
* PDF 문서의 특성을 보고하는 XML 파일입니다. 보고된 특성에는 텍스트, 댓글, 양식 데이터, 첨부 파일, PDF Portfolio에 사용된 파일, 책갈피 및 PDF 속성이 포함됩니다. PDF 속성에는 양식 속성, 페이지 회전 및 문서 작성자가 포함됩니다.

DDX를 사용하여 PDF 문서를 문서 어셈블리 또는 디스어셈블리의 일부로 확장할 수 있습니다. 다음 효과의 조합을 지정할 수 있습니다.

* 선택한 페이지에서 워터마크 또는 배경을 추가하거나 제거합니다.
* 선택한 페이지에서 머리글과 바닥글을 추가하거나 제거합니다.
* PDF 패키지 또는 PDF Portfolio의 구조 및 탐색 기능을 제거합니다. 따라서 단일 PDF 파일이 생성됩니다.
* 페이지 레이블의 번호를 다시 매깁니다. 페이지 레이블은 일반적으로 페이지 번호 매기기에 사용됩니다.
* 다른 소스 문서에서 메타데이터를 가져옵니다.
* 첨부 파일, 책갈피, 링크, 주석 및 JavaScript를 추가하거나 제거합니다.
* 초기 보기 특성을 설정하고 웹에서 볼 수 있도록 최적화합니다.
* 암호화된 PDF에 대한 권한을 설정합니다.
* 페이지를 회전하거나 페이지에서 내용을 회전 및 이동합니다.
* 선택한 페이지의 크기를 변경합니다.
* XFA 기반의 PDF과 데이터를 병합합니다.

단순 입력 맵을 사용하여 소스 및 결과 문서의 위치를 지정할 수 있습니다. 다음 외부 데이터 URL 유형을 사용할 수도 있습니다.

* 파일
* FTP
* HTTP/HTTPS

## Doc Assurance 서비스 {#doc-assurance-service}

Doc Assurance Service를 사용하면 문서를 암호화 및 해독하고, 추가 사용 권한으로 Adobe Reader의 기능을 확장하며, 문서에 디지털 서명을 추가할 수 있습니다. 보안, 아카이빙 및 규정 준수를 향상시키는 동시에 PDF forms 및 문서와 손쉽게 상호 작용할 수 있습니다.

Doc Assurance 서비스에는 서명, 암호화 및 리더 확장의 세 가지 서비스가 포함됩니다.

### 서명 서비스 {#signature-service}

서명 서비스를 사용하면 AEM 서버에서 디지털 서명과 문서를 사용하여 작업할 수 있습니다. 예를 들어 서명 서비스는 일반적으로 다음과 같은 경우에 사용됩니다.

* AEM 서버는 Acrobat 또는 Adobe Reader을 사용하여 열도록 사용자에게 전송되기 전에 양식을 인증합니다.
* AEM 서버는 Acrobat 또는 Adobe Reader을 사용하여 양식에 추가된 서명을 확인합니다.
* AEM 서버는 공증인을 대신하여 양식에 서명합니다.

서명 서비스는 신뢰 저장소에 저장된 인증서 및 자격 증명에 액세스합니다.

### 암호화 서비스 {#encryption-service}

암호화 서비스를 사용하면 문서를 암호화하고 해독할 수 있습니다. 문서가 암호화되면 해당 내용을 읽을 수 없게 됩니다. 전체 PDF 문서(컨텐츠, 메타데이터 및 첨부 파일 포함), 메타데이터 이외의 모든 문서 또는 첨부 파일만 암호화할 수 있습니다. 승인된 사용자는 문서의 내용을 해독하여 콘텐츠에 액세스할 수 있습니다. PDF 문서가 암호로 암호화된 경우 Adobe Reader 또는 Acrobat에서 문서를 보려면 열기 암호를 지정해야 합니다. PDF 문서가 인증서로 암호화되어 있는 경우 사용자는 개인 키(인증서)를 사용하여 PDF 문서의 암호를 해독해야 합니다. PDF 문서의 암호를 해독하는 데 사용되는 개인 키는 암호화에 사용되는 공개 키와 일치해야 합니다.

### Reader 확장 서비스 {#reader-extension-service}

Reader 확장 서비스를 사용하면 추가 사용 권한과 함께 Adobe Reader의 기능을 확장하여 조직에서 대화형 PDF 문서를 쉽게 공유할 수 있습니다. Reader 확장 서비스는 Adobe Reader 7.0 이상에서 작동합니다. 이 서비스는 PDF 문서에 사용 권한을 추가합니다. 이 작업은 문서에 주석 추가, 양식 채우기, 문서 저장과 같이 Adobe Reader을 사용하여 PDF 문서를 열 때 일반적으로 사용할 수 없는 기능을 활성화합니다. 서드파티 사용자는 권한이 활성화된 문서에서 작동하는 데 추가 소프트웨어나 플러그인이 필요하지 않습니다.

PDF 문서에 적절한 사용 권한이 추가되면 수신자는 Adobe Reader 내에서 다음 활동을 수행할 수 있습니다.

* 온라인 또는 오프라인에서 PDF 문서 및 양식을 완성하여 수신자가 레코드를 위해 사본을 로컬에 저장하고 추가된 정보를 그대로 유지할 수 있습니다.
* PDF 문서를 로컬 하드 드라이브에 저장하여 원본 문서와 추가 설명, 데이터 또는 첨부 파일을 유지합니다.
* PDF 문서에 파일 및 미디어 클립 첨부
* 업계 표준 PKI(공개 키 인프라) 기술을 사용하여 디지털 서명을 적용하여 PDF 문서에 서명, 인증 및 인증
* 완료 또는 주석이 있는 PDF 문서를 전자적으로 제출
* 내부 데이터베이스 및 웹 서비스에 대한 직관적인 개발 프런트 엔드로 PDF 문서 및 양식 사용
* 검토자가 직관적인 마크업 도구를 사용하여 주석을 추가할 수 있도록 PDF 문서를 다른 사용자와 공유합니다. 이러한 도구에는 전자 스티커 메모, 스탬프, 하이라이트 및 텍스트 취소선이 포함됩니다. Acrobat에서도 동일한 기능을 사용할 수 있습니다.
* 바코드 형식 디코딩을 지원합니다.

이러한 특수 사용자 기능은 권한이 활성화된 PDF 문서가 Adobe Reader 내에서 열릴 때 자동으로 활성화됩니다. 사용자가 권한이 활성화된 문서 작업을 완료하면 Adobe Reader에서 해당 기능이 다시 비활성화됩니다. 사용자가 다른 권한이 활성화된 PDF 문서를 받을 때까지 비활성화됩니다.

기본적으로 DocAssurance 서비스는 사용할 수 없습니다. DocAssurance 서비스를 구성하려면 다음을 참조하십시오 [문서 서비스 설치 및 구성](../../forms/using/install-configure-document-services.md).

## 프린터 서비스로 보내기 {#send-to-printer-service}

프린터로 보내기 서비스는 문서를 지정된 프린터로 인쇄하기 위해 보내는 API를 제공합니다.
