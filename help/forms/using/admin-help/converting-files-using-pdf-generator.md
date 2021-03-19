---
title: PDF Generator를 사용하여 파일 변환
seo-title: PDF Generator를 사용하여 파일 변환
description: PDF Generator를 사용하여 파일을 변환하는 방법을 살펴볼 수 있습니다.
seo-description: PDF Generator를 사용하여 파일을 변환하는 방법을 살펴볼 수 있습니다.
uuid: 295afb8f-130a-44f5-b0ab-e4c93c0c9e52
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 999ae2be-56ba-48c1-861b-8d4c991a0206
feature: PDF 생성기
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1182'
ht-degree: 0%

---


# PDF Generator{#converting-files-using-pdf-generator}를 사용하여 파일 변환

PDF Generator 웹 페이지를 사용하여 파일을 변환할 수 있습니다.

## PDF 파일 {#create-a-pdf-file} 만들기

1. 관리 콘솔에서 서비스 > PDF Generator > PDF 만들기를 클릭합니다.
1. 찾아보기를 클릭하여 파일을 찾아 선택합니다.

   >[!NOTE]
   >
   >PDF Generator는 파일 이름에 파일 확장자가 없는 경우에도 .doc, .xls, .ppt 및 .rtf 파일 유형을 자동으로 감지할 수 있습니다. 이 기능은 .docx, .xlsx 및 .pptx 파일에서 작동하지 않습니다.

1. 구성 설정에서 사용자 지정 설정 사용 또는 설정 파일 업로드를 선택합니다.

   * 사용자 정의 설정을 사용하는 경우 Adobe PDF 설정, 보안 설정 및 파일 유형 설정을 선택하고 시간 초과를 지정합니다.

      Adobe PDF 설정은 PS-to-PDF, EPS-to-PDF, PRN에서 PDF로 변환, OCR을 통한 이미지-PDF 변환 및 기본-PDF 변환에만 적용됩니다. 시간 초과 설정은 변환이 완료되는 데 걸리는 최대 시간을 지정합니다. 기본값은 270초입니다. 이러한 설정은 이미지-PDF 및 OpenOffice-PDF로 변환하는 동안에는 사용되지 않습니다.

   * 설정 파일을 업로드하는 경우 상자에 해당 경로와 이름을 입력하거나 [찾아보기]를 클릭하여 파일을 찾아 선택합니다.

1. (선택 사항) XMP 메타데이터 파일에서 XMP 파일의 경로와 이름을 입력하거나 찾아보기를 클릭하여 파일을 찾아 선택합니다. XMP 파일은 표준 메타데이터 정보를 포함하는 데 사용할 수 있습니다. ([XMP 파일 정보](converting-files-using-pdf-generator.md#about-xmp-files)를 참조하십시오.)
1. 만들기를 클릭합니다. 파일이 만들어지면 해당 파일에 대한 링크가 나타납니다. 변환 중 오류가 발생하면 경고가 표시됩니다. Postscript 파일을 만드는 경우 경고에는 로그 파일에 대한 링크도 포함되어 있습니다.
1. PDF 파일의 링크를 클릭합니다. Acrobat에서 파일이 열립니다.

### XMP 파일 {#about-xmp-files} 정보

PDF Generator가 Acrobat 5.0 이상에서 만든 PDF 문서에는 XML 형식의 문서 메타데이터가 포함되어 있습니다. *메타데이터* 는 문서 및 해당 컨텐츠에 대한 정보(예: 검색 유틸리티에서 사용할 수 있는 작성자 이름, 키워드 및 저작권 정보)를 포함합니다.

문서 메타데이터에는 Acrobat의 [문서 속성] 대화 상자의 [설명] 탭에도 표시되는 정보가 포함되어 있습니다(이에 제한되지 않음). [설명] 탭에서 변경한 내용은 문서 메타데이터에 반영됩니다. 문서 메타데이터는 타사 제품을 사용하여 확장 및 수정할 수 있습니다.

XMP(Adobe Extensible Metadata Platform)는 출판 워크플로우 전반에 걸쳐 문서 메타데이터를 작성, 처리 및 교환하는 것을 표준화하는 공통 XML 프레임워크를 Adobe 애플리케이션에 제공합니다. 문서 메타데이터 XML 소스 코드를 XMP 형식으로 저장하고 가져올 수 있으므로 다양한 문서 간에 메타데이터를 쉽게 공유할 수 있습니다. XMP 파일에 대한 자세한 내용은 [XMP(Extensible Metadata Platform)](https://www.adobe.com/products/xmp/) 및 [Adobe XMP Developer Center](https://www.adobe.com/devnet/xmp.html)를 참조하십시오.

Acrobat에서 XMP 파일을 만들 수 있습니다.

## HTML 파일 또는 ZIP 파일을 PDF {#convert-an-html-file-or-zip-file-to-pdf}로 변환

PDF Generator를 사용하여 다음 유형의 파일을 Adobe PDF으로 변환할 수 있습니다.

* HTML 파일을 업로드하거나 웹 페이지 또는 웹 사이트의 URL을 지정하여 변환할 수 있는 HTML 파일입니다.
* HTML 파일, 이미지 파일 또는 둘 다를 포함할 수 있는 보관된 파일(ZIP).

ZIP 파일에 폴더 계층 구조의 가장 낮은 수준에 있는 둘 이상의 HTML 파일이 포함되어 있는 경우 ZIP 파일에는 index.htm 또는 index.html 파일도 포함되어야 합니다.

>[!NOTE]
>
>* HTML을 PDF로 변환 기능을 사용하려면 시스템 글꼴 디렉토리에 특정 글꼴이 있어야 합니다. Linux, Solaris 및 AIX 시스템의 경우 시스템 글꼴 디렉토리에 Courier 글꼴이 포함되어야 합니다. Windows 시스템의 경우 시스템 글꼴 디렉토리에는 Times New Roman이 포함되어야 합니다.
   >
   >
* (UNIX 기반 시스템 전용) 일본어 글꼴이 포함된 웹 페이지를 PDF 문서로 변환하려면 AEM Forms 서버에서 다음 일본어 글꼴 중 하나를 사용할 수 있어야 합니다.
   >
   >  
* 사자나미 고딕
>  * &quot;Kozuka Gothic Pro-VI&quot;
>  * &quot;Kozuka Mincho Pro-VI&quot;
>  * 사자나미 고딕
>  * &quot;Kozuka Mincho Pro6N&quot;
>  * &quot;사자나미 민초&quot;
>  * &quot;Adobe 하이티 성병&quot;
>  * &quot;Adobe Song Std&quot;

   >
   >
* 로컬 파일 시스템에서 파일을 업로드하려면 HTML에서 PDF로 파일 업로드 옵션을 사용합니다.


1. 관리 콘솔에서 서비스 > PDF Generator > HTML을 PDF로 클릭합니다.
1. 다음 작업 중 하나를 수행하여 변환할 파일을 지정합니다.

   * [파일 업로드]에서 HTML 파일 또는 ZIP 파일의 경로와 파일 이름을 입력하거나 [찾아보기]를 클릭하여 파일을 찾아 선택합니다.
   * [URL 지정] 상자에 변환할 페이지 또는 웹 사이트의 URL을 입력합니다.

   >[!NOTE]
   >
   >변환할 파일의 파일 이름 확장자는 .html, .htm 또는 .zip이어야 합니다.

1. 구성 설정을 지정합니다.

   * 사용자 정의 설정을 사용하려면 [사용자 정의 설정 사용]을 선택하고 보안 및 파일 유형 설정을 지정하고 시간 초과 값을 지정합니다. 기본값은 270초입니다.
   >[!NOTE]
   >
   >Acrobat WebCapture를 사용하도록 PDF 생성 서비스를 구성한 경우 이 페이지에서 선택하는 파일 유형 설정은 생성된 PDF에 영향을 주지 않습니다. 대신 서버에 설치된 Acrobat 버전을 적절하게 변경합니다.

   * 기존 설정 파일을 사용하려면 [설정 파일 업로드]를 선택하고 [찾아보기]를 클릭하여 파일 위치로 이동합니다.


1. XMP 파일을 업로드하려면 찾아보기를 클릭하고 파일 위치로 이동합니다. XMP 파일은 표준 메타데이터 정보를 포함하는 데 사용할 수 있습니다. ([XMP 파일 정보](converting-files-using-pdf-generator.md#about-xmp-files)를 참조하십시오.)
1. 만들기를 클릭합니다. 파일이 만들어지면 PDF 파일에 대한 링크가 나타납니다.
1. 링크를 클릭하여 Acrobat에서 PDF 문서를 봅니다.

## PDF 파일을 다른 파일 형식(Windows 전용) {#export-a-pdf-file-to-another-file-format-windows-only}

[서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)의 [PDF 서비스 생성] 장에 설명된 대로 PDF 파일을 다양한 파일 형식으로 내보낼 수 있습니다.

1. 관리 콘솔에서 서비스 > PDF 생성기 > Export PDF을 클릭합니다.
1. 찾아보기를 클릭하여 내보낼 PDF 파일을 찾습니다.
1. 목록에서 PDF 파일을 내보낼 형식을 선택합니다.
1. [시간 초과 지정] 상자에 응용 프로그램이 시간 초과되기 전에 대기할 시간을 입력합니다. 기본값은 270초입니다.

   파일을 변환할 때 표시되는 변환 시간은 여기에서 지정한 값보다 클 수 있습니다. 변환 시간은 스레드 또는 프로세스를 기다리는 데 걸리는 시간, 파일 변환에 걸리는 시간 및 폴백 변환기에 걸린 시간(해당하는 경우)을 포함합니다. 시간. Specify a Timeout 값은 파일을 변환하는 데 걸리는 시간입니다.

1. (선택 사항) **사용자 정의 프리플라이트 프로필 지정** 옵션에서 [찾아보기]를 클릭하고 [사용자 정의 프리플라이트 프로필](https://helpx.adobe.com/acrobat/using/preflight-profiles-acrobat-pro.html)을 선택합니다. 프리플라이트 프로필은 문서를 PDF 보관(PDF/A) 형식으로 변환하는 경우에만 사용됩니다.
1. 내보내기를 클릭합니다. 변환이 완료되면 내보낸 파일에 대한 링크가 나타납니다.
1. 변환된 파일을 보려면 링크를 클릭합니다.

## PDF 최적화(Windows 전용) {#optimize-a-pdf}

PDF Generator를 사용하면 PDF 파일의 크기를 줄일 수 있습니다.

>[!NOTE]
>
>디지털 서명된 문서를 최적화하면 디지털 서명이 제거되고 무효화됩니다.

1. 관리 콘솔에서 서비스 > PDF 생성기 > Optimize PDF을 클릭합니다.
1. 찾아보기를 클릭하여 최적화할 PDF 파일을 찾습니다.
1. 구성 설정을 지정합니다.

   * 사용자 정의 설정을 사용하려면 [사용자 정의 설정 사용]을 선택하고 파일 유형 설정을 지정하고 시간 초과 값을 지정합니다. 기본값은 270초입니다.
   * 기존 설정 파일을 사용하려면 [설정 파일 업로드]를 선택하고 [찾아보기]를 클릭하여 파일 위치로 이동합니다.

1. 만들기를 클릭합니다.

