---
title: PDF Generator를 사용하여 파일 변환
description: PDF Generator 서비스는 기본 파일 형식을 PDF로 변환합니다. 또한 PDF를 다른 파일 형식으로 변환하고 PDF 문서 크기를 최적화합니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: PDF Generator
exl-id: 0e2c12b5-24c8-4aca-8826-cb661051ce4f
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '1185'
ht-degree: 100%

---

# PDF Generator를 사용하여 파일 변환{#converting-files-using-pdf-generator}

>[!NOTE]
> 
> 사용자에게 관리자 콘솔에 액세스할 수 있는 관리자 권한이 있는지 확인하십시오.

PDF Generator 웹 페이지에서 파일을 변환할 수 있습니다.

## PDF 파일 만들기 {#create-a-pdf-file}

1. 관리 콘솔에서 서비스 > PDF Generator > PDF 만들기를 클릭합니다.
1. 찾아보기를 클릭하여 파일을 찾아 선택합니다.

   >[!NOTE]
   >
   >PDF Generator는 파일 이름에 확장자가 없는 경우에도 .doc, .xls, .ppt, .rtf 파일의 파일 유형을 자동으로 감지할 수 있습니다. 이 기능은 .docx, .xlsx, .pptx 파일에서는 작동하지 않습니다.

1. 구성 설정에서 사용자 정의 설정 사용 또는 설정 파일 업로드를 선택합니다.

   * 사용자 정의 설정을 사용하는 경우 Adobe PDF 설정, 보안 설정, 파일 유형 설정을 선택하고 시간 초과를 지정합니다.

     Adobe PDF 설정은 PS-PDF, EPS-PDF, PRN-PDF, OCR이 켜진 이미지-PDF, 네이티브-PDF 변환에만 적용할 수 있습니다. 시간 초과 설정은 변환을 완료하는 데 걸리는 최대 시간을 지정합니다. 기본값은 270초입니다. 해당 설정은 이미지-PDF 및 OpenOffice-PDF 변환 중에는 사용되지 않습니다.

   * 설정 파일을 업로드하는 경우 상자에 해당 경로와 이름을 입력하거나 찾아보기를 클릭하여 파일을 찾아 선택합니다.

1. (선택 사항) XMP 메타데이터 파일에서 XMP 파일의 경로와 이름을 입력하거나 찾아보기를 클릭하여 파일을 찾아 선택합니다. XMP 파일은 표준 메타데이터 정보를 포함하는 데 사용할 수 있습니다. ([XMP 파일 정보](converting-files-using-pdf-generator.md#about-xmp-files)를 참조하십시오.)
1. 만들기를 클릭합니다. 파일이 생성되면 해당 파일 링크가 나타납니다. 변환 중에 오류가 발생하면 경고가 나타납니다. Postscript 파일을 만드는 경우 경고에는 로그 파일 링크도 포함됩니다.
1. PDF 파일 링크를 클릭합니다. 해당 파일이 Acrobat에서 열립니다.

### XMP 파일 정보 {#about-xmp-files}

PDF Generator가 Acrobat 5.0 이상에서 만드는 PDF 문서에는 XML 형식의 문서 메타데이터가 포함됩니다. *메타데이터*&#x200B;에는 작성자 이름, 키워드, 저작권 정보와 같이 검색 유틸리티에서 사용할 수 있는 문서 및 문서 콘텐츠에 대한 정보가 포함됩니다.

문서 메타데이터에는 Acrobat의 문서 속성 대화 상자에 있는 설명 탭에도 나타나는 정보가 포함되지만 이에 국한되지 않습니다. 설명 탭에서 변경한 사항은 문서 메타데이터에 반영됩니다. 문서 메타데이터는 서드파티 제품을 사용하여 확장하고 수정할 수 있습니다.

Adobe XMP(Extensible Metadata Platform)는 Adobe 애플리케이션에 공통 XML 프레임워크를 제공하여 게시 워크플로 전반에서 문서 메타데이터의 생성, 처리 및 교환을 표준화합니다. 문서 메타데이터 XML 소스 코드를 XMP 형식으로 저장하고 가져올 수 있어 다양한 문서 간에 메타데이터를 쉽게 공유할 수 있습니다. XMP 파일에 대한 자세한 내용은 [XMP(Extensible Metadata Platform)](https://www.adobe.com/kr/products/xmp/) 및 [Adobe XMP 개발자 센터](https://www.adobe.com/kr/devnet/xmp.html)를 참조하십시오.

Acrobat에서 XMP 파일을 만들 수 있습니다.

## HTML 파일 또는 ZIP 파일을 PDF로 변환 {#convert-an-html-file-or-zip-file-to-pdf}

PDF Generator를 사용하여 다음 유형의 파일을 Adobe PDF로 변환할 수 있습니다.

* HTML 파일을 업로드하거나 웹 페이지 또는 웹 사이트의 URL을 지정하여 변환할 수 있는 HTML 파일
* HTML 파일, 이미지 파일 또는 둘 다를 포함할 수 있는 보관된 파일(ZIP)

ZIP 파일의 폴더 계층에서 가장 낮은 수준에 두 개 이상의 HTML 파일이 포함되어 있는 경우 ZIP 파일에는 index.htm 또는 index.html 파일도 포함되어야 합니다.

>[!NOTE]
>
>* HTML-PDF 기능을 사용하려면 시스템 글꼴 디렉터리에 특정 글꼴이 있어야 합니다. Linux, Solaris, AIX 시스템에서는 시스템 글꼴 디렉터리에 Courier 글꼴이 있어야 합니다. Windows 시스템에서는 시스템 글꼴 디렉터리에 Times New Roman이 있어야 합니다.
>
>* (UNIX 기반 시스템만 해당) 다음과 같은 일본어 글꼴 중 하나를 AEM Forms 서버에서 사용할 수 있어야만 일본어 글꼴이 적용된 웹 페이지를 PDF 문서로 변환할 수 있습니다.
>
>  * &#39;Sazanami Gothic&#39;
>  * &#39;Kozuka Gothic Pro-VI&#39;
>  * &#39;Kozuka Mincho Pro-VI&#39;
>  * &#39;Sazanami Gothic&#39;
>  * &#39;Kozuka Mincho Pr6N&#39;
>  * &#39;Sazanami Mincho&#39;
>  * &#39;Adobe Heiti Std&#39;
>  * &#39;Adobe Song Std&#39;
>
>* 로컬 파일 시스템에서 파일을 업로드하려면 HTML-PDF 페이지에서 파일 업로드 옵션을 사용합니다.

1. 관리 콘솔에서 서비스 > PDF Generator > HTML-PDF를 클릭합니다.
1. 다음 작업 중 하나를 수행하여 변환할 파일을 지정합니다.

   * 파일 업로드에서 HTML 파일 또는 ZIP 파일의 경로와 파일 이름을 입력하거나 찾아보기를 클릭하여 해당 파일을 찾아 선택합니다.
   * URL 지정 상자에 변환할 페이지나 웹 사이트의 URL을 입력합니다.

   >[!NOTE]
   >
   >변환하려는 파일의 파일 이름 확장자는 .html, .htm 또는 .zip이어야 합니다.

1. 다음과 같은 구성 설정을 지정합니다.

   * 사용자 정의 설정을 사용하려면 사용자 정의 설정 사용을 선택하고 보안 및 파일 유형 설정을 지정한 후 시간 초과 값을 지정합니다. 기본값은 270초입니다.

   >[!NOTE]
   >
   >Acrobat WebCapture를 사용하도록 PDF 생성 서비스를 구성한 경우 이 페이지에서 선택하는 파일 유형 설정은 생성된 PDF에 영향을 미치지 않습니다. 대신 서버에 설치된 Acrobat 버전을 적절히 변경하십시오.

   * 기존 설정 파일을 사용하려면 설정 파일 업로드를 선택하고 찾아보기를 클릭하여 파일 위치로 이동합니다.

1. XMP 파일을 업로드하려면 찾아보기를 클릭하고 파일 위치로 이동합니다. XMP 파일은 표준 메타데이터 정보를 포함하는 데 사용할 수 있습니다. ([XMP 파일 정보](converting-files-using-pdf-generator.md#about-xmp-files)를 참조하십시오.)
1. 만들기를 클릭합니다. 파일이 생성되면 PDF 파일 링크가 나타납니다.
1. 해당 링크를 클릭하면 Acrobat에서 PDF 문서를 볼 수 있습니다.

## PDF 파일을 다른 파일 형식으로 내보내기(Windows 전용) {#export-a-pdf-file-to-another-file-format-windows-only}

[서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)의 PDF 생성 서비스 장에 설명된 대로 PDF 파일을 다양한 파일 형식으로 내보낼 수 있습니다.

1. 관리 콘솔에서 서비스 > PDF Generator > PDF 내보내기를 클릭합니다.
1. 찾아보기를 클릭하여 내보낼 PDF 파일을 찾습니다.
1. PDF 파일 내보내기 목록에서 PDF 파일을 내보낼 형식을 선택합니다.
1. 시간 초과 지정 상자에 애플리케이션이 시간 초과될 때까지 기다릴 시간을 입력합니다. 기본값은 270초입니다.

   파일이 변환될 때 표시되는 변환 시간은 여기에서 지정한 값보다 클 수 있습니다. 변환 시간에는 스레드 또는 프로세스를 기다리는 데 걸리는 시간, 파일을 변환하는 데 걸리는 시간, 대체 변환기(해당되는 경우)에 걸리는 시간이 포함됩니다. 시간 초과 지정 값은 단지 파일을 변환하는 데 걸리는 시간입니다.

1. (선택 사항) **사용자 정의 Preflight 프로필 지정** 옵션에서 찾아보기를 클릭하고 [사용자 정의 Preflight 프로필](https://helpx.adobe.com/kr/acrobat/using/preflight-profiles-acrobat-pro.html)을 선택합니다. Preflight 프로필은 문서를 PDF 아카이브(PDF/A) 형식으로 변환할 때만 사용됩니다.
1. 내보내기를 클릭합니다. 변환이 완료되면 내보낸 파일 링크가 나타납니다.
1. 해당 링크를 클릭하면 변환된 파일을 볼 수 있습니다.

## PDF 최적화(Windows 전용) {#optimize-a-pdf}

PDF Generator는 PDF 파일 크기를 줄이는 기능을 지원합니다.

>[!NOTE]
>
>디지털 서명된 문서를 최적화하면 디지털 서명이 제거되고 무효화됩니다.

1. 관리 콘솔에서 서비스 > PDF Generator > PDF 최적화를 클릭합니다.
1. 찾아보기를 클릭하여 최적화할 PDF 파일을 찾습니다.
1. 다음과 같은 구성 설정을 지정합니다.

   * 사용자 정의 설정을 사용하려면 사용자 정의 설정 사용을 선택하고 파일 유형 설정을 지정한 후 시간 초과 값을 지정합니다. 기본값은 270초입니다.
   * 기존 설정 파일을 사용하려면 설정 파일 업로드를 선택하고 찾아보기를 클릭하여 파일 위치로 이동합니다.

1. 만들기를 클릭합니다.
