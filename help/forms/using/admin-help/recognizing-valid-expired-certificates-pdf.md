---
title: PDF 문서에서 유효 및 만료된 인증서 인식
seo-title: PDF 문서에서 유효 및 만료된 인증서 인식
description: PDF 문서에서 유효 및 만료된 인증서를 인식하는 방법을 알아봅니다.
seo-description: PDF 문서에서 유효 및 만료된 인증서를 인식하는 방법을 알아봅니다.
uuid: ceeff57a-586f-4f7b-852f-2a637f003d7e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4559218a-65ba-4577-ad26-7721e28971bc
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---


# PDF 문서 {#recognizing-valid-and-expired-certificates-in-pdf-documents}에서 유효하고 만료된 인증서 인식

Reader Extensions에서 사용 권한이 적용된 PDF 문서를 Adobe Reader에서 열면 PDF 문서에서 활성화된 특정 사용 권한을 설명하는 상태 표시줄이 나타납니다.

PDF 문서의 사용 권한을 지정하는 디지털 인증서가 만료되고 PDF 문서가 Adobe Reader에서 열리면 PDF 문서에 사용 권한이 있지만 이 권한은 사용하지 않도록 설정되었음을 사용자에게 알리는 대화 상자가 나타납니다. PDF 문서가 변경되었거나 무단 변경되었음을 알리는 메시지가 표시되지만 반드시 그렇지는 않습니다. Adobe Reader은 인증서가 만료되거나 문서를 수정할 때 이 메시지를 표시합니다. Adobe Reader 7.0.x 이상에서는 현재 문제가 되는 케이스를 확인할 수 없습니다.

대화 상자를 닫으면 Adobe Reader에서 PDF 문서가 열립니다. Acrobat Reader DC 확장을 사용하여 적용된 사용 권한은 예상대로 사용할 수 없습니다. PDF 문서가 대화형 양식인 경우 양식 필드가 잠겨 사용자가 양식 데이터를 변경할 수 없습니다.
