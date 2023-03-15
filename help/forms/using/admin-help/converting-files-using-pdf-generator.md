---
title: PDF 생성기를 사용하여 파일 변환
seo-title: Converting files using PDF Generator
description: PDF 생성기를 사용하여 파일을 변환하는 방법에 대해 알아봅니다.
seo-description: Learn how to convert files using PDF Generator.
uuid: 295afb8f-130a-44f5-b0ab-e4c93c0c9e52
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 999ae2be-56ba-48c1-861b-8d4c991a0206
feature: PDF Generator
exl-id: 0e2c12b5-24c8-4aca-8826-cb661051ce4f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1167'
ht-degree: 0%

---

# PDF 생성기를 사용하여 파일 변환{#converting-files-using-pdf-generator}

PDF 생성기 웹 페이지를 사용하여 파일을 변환할 수 있습니다.

## PDF 파일 만들기 {#create-a-pdf-file}

1. 관리 콘솔에서 서비스 > PDF 생성기 > PDF 만들기 를 클릭합니다.
1. 찾아보기 를 클릭하여 파일을 찾아 선택합니다.

   >[!NOTE]
   >
   >PDF 생성기는 파일 이름에 파일 확장명이 없는 경우에도 .doc, .xls, .ppt 및 .rtf 파일의 파일 형식을 자동으로 감지할 수 있습니다. 이 기능은 .docx, .xlsx 및 .pptx 파일에서 작동하지 않습니다.

1. 구성 설정에서 사용자 지정 설정 사용 또는 설정 파일 업로드를 선택합니다.

   * 사용자 지정 설정을 사용하는 경우 Adobe PDF 설정, 보안 설정 및 파일 유형 설정을 선택하고 시간 초과를 지정합니다.

      Adobe PDF 설정은 PS-to-PDF, EPS-to-PDF, PRN-to-PDF, OCR이 설정된 이미지-to-PDF 및 기본-to-PDF 전환에만 적용할 수 있습니다. 시간 제한 설정은 전환을 완료하는 데 소요되는 최대 시간을 지정합니다. 기본값은 270초입니다. 이러한 설정은 이미지-PDF 및 OpenOffice-PDF 전환 중에는 사용되지 않습니다.

   * 설정 파일을 업로드하는 경우 상자에 해당 경로와 이름을 입력하거나 찾아보기를 눌러 파일을 찾아 선택합니다.

1. (선택 사항) XMP 메타데이터 파일에서 XMP 파일의 경로와 이름을 입력하거나 찾아보기를 눌러 파일을 찾아 선택합니다. XMP 파일을 사용하여 표준 메타데이터 정보를 포함할 수 있습니다. (참조: [XMP 파일 정보](converting-files-using-pdf-generator.md#about-xmp-files).)
1. 만들기를 클릭합니다. 파일이 생성되면 파일에 대한 링크가 나타납니다. 변환 중에 오류가 발생하면 경고가 나타납니다. Postscript 파일을 만드는 경우 경고에 로그 파일에 대한 링크도 포함되어 있습니다.
1. PDF 파일에 대한 링크를 클릭합니다. 파일이 Acrobat에서 열립니다.

### XMP 파일 정보 {#about-xmp-files}

PDF 생성기가 Acrobat 5.0 이상에서 만드는 PDF 문서에는 XML 형식의 문서 메타데이터가 포함됩니다. *메타데이터* 에는 작성자 이름, 키워드 및 검색 유틸리티에서 사용할 수 있는 저작권 정보 등 문서 및 문서에 대한 정보가 포함되어 있습니다.

문서 메타데이터에는 Acrobat의 문서 속성 대화 상자에 있는 설명 탭에도 나타나는 정보가 포함되어 있지만 이에 국한되지는 않습니다. 설명 탭에서 변경한 내용은 문서 메타데이터에 반영됩니다. 문서 메타데이터는 서드파티 제품을 사용하여 확장 및 수정할 수 있습니다.

XMP(Adobe 확장 가능한 메타데이터 플랫폼)은 Adobe 애플리케이션에서 게시 작업 과정 간의 문서 메타데이터 작성, 처리 및 교환을 표준화하는 공통 XML 프레임워크를 제공합니다. 문서 메타데이터 XML 소스 코드를 XMP 형식으로 저장하고 가져올 수 있으므로 다양한 문서 간에 메타데이터를 쉽게 공유할 수 있습니다. XMP 파일에 대한 자세한 내용은 [확장 가능한 메타데이터 플랫폼(XMP)](https://www.adobe.com/products/xmp/) 및 [Adobe XMP 개발자 센터](https://www.adobe.com/devnet/xmp.html).

Acrobat에서 XMP 파일을 만들 수 있습니다.

## HTML 파일 또는 ZIP 파일을 PDF으로 변환 {#convert-an-html-file-or-zip-file-to-pdf}

PDF 생성기 를 사용하여 다음 유형의 파일을 Adobe PDF으로 변환할 수 있습니다.

* HTML 파일 - HTML 파일을 업로드하거나 웹 페이지나 웹 사이트의 URL을 지정하여 변환할 수 있습니다.
* HTML 파일, 이미지 파일 또는 두 가지 모두를 포함할 수 있는 보관된 파일(ZIP).

ZIP 파일의 폴더 계층 구조의 가장 낮은 수준에 둘 이상의 HTML 파일이 포함되어 있는 경우 ZIP 파일에는 index.htm 또는 index.html 파일도 포함되어야 합니다.

>[!NOTE]
>
>* PDF HTML 기능을 사용하려면 시스템 글꼴 디렉토리에 특정 글꼴이 있어야 합니다. Linux, Solaris 및 AIX 시스템의 경우 시스템 글꼴 디렉토리에 Courier 글꼴이 포함되어야 합니다. Windows 시스템의 경우 시스템 글꼴 디렉토리에는 Times New Roman이 포함되어야 합니다.
>
>* (UNIX 기반 시스템에만 해당) 일본어 글꼴이 있는 웹 페이지를 PDF 문서로 변환하려면 AEM Forms 서버에서 다음 일본어 글꼴 중 하나를 사용할 수 있습니다.
>
>  * &quot;사자나미 고딕&quot;
>  * &quot;Kozuka Gothic Pro-VI&quot;
>  * &quot;Kozuka Mincho Pro-VI&quot;
>  * &quot;사자나미 고딕&quot;
>  * &quot;Kozuka Mincho Pr6N&quot;
>  * &quot;사자나미 민초&quot;
>  * &quot;Adobe Heiti Std&quot;
>  * &quot;Adobe Song Std&quot;
>
>* 로컬 파일 시스템에서 파일을 업로드하려면 PDF HTML 페이지에서 파일 업로드 옵션을 사용합니다.


1. 관리 콘솔에서 서비스 > PDF 생성기 > PDF HTML 를 클릭합니다.
1. 다음 작업 중 하나를 수행하여 변환할 파일을 지정합니다.

   * 업로드 파일에 HTML 파일 또는 ZIP 파일의 경로와 파일 이름을 입력하거나 찾아보기를 클릭하여 찾아 선택합니다.
   * URL 지정 상자에 변환할 페이지나 웹 사이트의 URL을 입력합니다.

   >[!NOTE]
   >
   >변환하려는 파일의 파일 확장명은 .html, .htm 또는 .zip이어야 합니다.

1. 구성 설정을 지정합니다.

   * 사용자 지정 설정을 사용하려면 [사용자 지정 설정 사용]을 선택하고 보안 및 파일 형식 설정을 지정한 다음 시간 초과 값을 지정합니다. 기본값은 270초입니다.
   >[!NOTE]
   >
   >Acrobat WebCapture를 사용하도록 PDF 생성 서비스를 구성한 경우 이 페이지에서 선택한 파일 유형 설정은 생성된 PDF에 영향을 주지 않습니다. 대신 서버에 설치된 Acrobat 버전을 적절하게 변경합니다.

   * 기존 설정 파일을 사용하려면 설정 파일 업로드 를 선택하고 찾아보기 를 클릭하여 파일 위치로 이동합니다.


1. XMP 파일을 업로드하려면 찾아보기 를 클릭하고 파일 위치로 이동합니다. XMP 파일을 사용하여 표준 메타데이터 정보를 포함할 수 있습니다. (참조: [XMP 파일 정보](converting-files-using-pdf-generator.md#about-xmp-files).)
1. 만들기를 클릭합니다. 파일이 생성되면 PDF 파일에 대한 링크가 나타납니다.
1. Acrobat에서 PDF 문서를 보려면 링크를 클릭하십시오.

## PDF 파일을 다른 파일 형식으로 내보내기(Windows에만 해당) {#export-a-pdf-file-to-another-file-format-windows-only}

의 PDF 서비스 생성 장에 설명된 대로 PDF 파일을 다양한 파일 형식으로 내보낼 수 있습니다 [서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

1. 관리 콘솔에서 서비스 > PDF 생성기 > Export PDF 를 클릭합니다.
1. 찾아보기 를 클릭하여 내보낼 PDF 파일을 찾습니다.
1. 내보낼 Export PDF 파일에서 PDF 파일을 내보낼 형식을 선택합니다.
1. 시간 제한 지정 상자에 응용 프로그램 시간이 초과되기 전에 대기할 시간을 입력합니다. 기본값은 270초입니다.

   파일을 변환할 때 표시되는 변환 시간은 여기에서 지정한 값보다 클 수 있습니다. 변환 시간 에는 스레드 또는 프로세스를 기다리는 시간, 파일을 변환하는 데 걸리는 시간 및 대체 변환기에 걸리는 시간(해당하는 경우)이 포함됩니다. 시간. Specify a Timeout 값은 파일을 변환하는 데 걸리는 시간입니다.

1. (선택 사항) **사용자 지정 Preflight 프로필 지정** 옵션을 선택하고 찾아보기를 클릭한 다음 [사용자 지정 Preflight 프로필](https://helpx.adobe.com/acrobat/using/preflight-profiles-acrobat-pro.html). Preflight 프로필은 문서를 PDF 아카이브(PDF/A) 형식으로 변환하는 동안에만 사용됩니다.
1. 내보내기를 클릭합니다. 변환이 완료되면 내보낸 파일에 대한 링크가 나타납니다.
1. 변환된 파일을 보려면 링크를 클릭합니다.

## PDF 최적화(Windows에만 해당) {#optimize-a-pdf}

PDF 생성기는 PDF 파일 크기를 줄일 수 있도록 지원합니다.

>[!NOTE]
>
>디지털 서명된 문서를 최적화하면 디지털 서명이 제거되고 무효화됩니다.

1. 관리 콘솔에서 서비스 > PDF 생성기 > Optimize PDF 를 클릭합니다.
1. 찾아보기 를 클릭하여 최적화할 PDF 파일을 찾습니다.
1. 구성 설정을 지정합니다.

   * 사용자 지정 설정을 사용하려면 [사용자 지정 설정 사용]을 선택하고 파일 형식 설정을 지정한 다음 시간 초과 값을 지정합니다. 기본값은 270초입니다.
   * 기존 설정 파일을 사용하려면 설정 파일 업로드 를 선택하고 찾아보기 를 클릭하여 파일 위치로 이동합니다.

1. 만들기를 클릭합니다.
