---
title: PDF Generator 사용 소개
description: 다양한 파일 형식을 PDF로 변환하는 방법을 알아봅니다. 또한 PDF를 다른 파일 형식으로 변환하고 PDF 문서 크기를 최적화합니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: PDF Generator
exl-id: 08e2381e-c7e8-4690-9cbf-6934064a04f8
solution: Experience Manager, Experience Manager Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: b26425d0-6fde-5e02-bfd6-e560e2fa86c9
    internal-label: PDF Generator
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 100%
---
# PDF Generator 사용 소개 {#introduction-to-working-with-pdf-generator}

PDF Generator는 다양한 파일 형식을 PDF로 변환합니다. 또한 PDF를 다른 파일 형식으로 변환하고 PDF 문서 크기를 최적화합니다. 지원되는 파일 형식 목록은 [PDF Generator를 위한 소프트웨어 지원](/help/forms/using/aem-forms-jee-supported-platforms.md)을 참조하십시오.

**처리할 파일을 PDF Generator로 보내기**

PDF Generator로 파일을 보내 처리하는 방법에는 세 가지가 있습니다.

* 관리자는 관리 콘솔에서 PDFG 페이지에 액세스할 수 있습니다. ([PDF Generator를 사용하여 파일 변환](/help/forms/using/admin-help/converting-files-using-pdf-generator.md)을 참조하십시오.)
* 사용자는 `http(s)://'[server]:[port]'/pdfgui.`에 로그인하여 PDFG 최종 사용자 페이지에 액세스할 수 있습니다. 여기에서 PDFG 네트워크 프린터, PDF 만들기, HTML-PDF, PDF 내보내기, PDF 최적화 페이지에 액세스할 수 있습니다.
* 서비스에 대한 엔드포인트를 구성할 수 있습니다. 자세한 내용은 <!--Fix broken link to Managing Endpoints --> [PDF 생성 서비스 권장 사항](configuring-watched-folder-endpoints.md#generate-pdf-service-recommendations)을 참조하십시오.
