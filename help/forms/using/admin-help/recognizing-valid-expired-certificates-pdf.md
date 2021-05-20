---
title: PDF 문서에서 유효하고 만료된 인증서 인식
seo-title: PDF 문서에서 유효하고 만료된 인증서 인식
description: PDF 문서에서 유효하고 만료된 인증서를 인식하는 방법을 알아봅니다.
seo-description: PDF 문서에서 유효하고 만료된 인증서를 인식하는 방법을 알아봅니다.
uuid: ceeff57a-586f-4f7b-852f-2a637f003d7e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4559218a-65ba-4577-ad26-7721e28971bc
exl-id: dfe2823a-3a0d-4e45-8765-f618529e22dd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---

# PDF 문서에서 유효하고 만료된 인증서 인식 {#recognizing-valid-and-expired-certificates-in-pdf-documents}

Reader 확장에서 적용된 사용 권한이 있는 PDF 문서를 Adobe Reader에서 열면 PDF 문서에서 활성화된 특정 사용 권한을 설명하는 상태 표시줄이 나타납니다.

PDF 문서의 사용 권한을 지정하는 디지털 인증서가 만료되고 PDF 문서가 Adobe Reader에 열리면 PDF 문서에 사용 권한이 있지만 이러한 권한은 비활성화되어 있음을 사용자에게 알려주는 대화 상자가 나타납니다. PDF 문서가 변경되었거나 훼손되었음을 알리는 메시지가 표시되지만 반드시 그렇지 않을 수도 있습니다. Adobe Reader은 인증서가 만료되거나 문서가 수정되면 이 메시지를 표시합니다. Adobe Reader 7.0.x 이상에서는 현재 어느 사례가 문제인지 확인할 수 없습니다.

대화 상자를 닫으면 Adobe Reader에서 PDF 문서가 열립니다. Acrobat Reader DC 확장을 사용하여 적용된 사용 권한을 예상대로 사용할 수 없습니다. PDF 문서가 대화형 양식인 경우 양식 필드가 잠겨 사용자가 양식 데이터를 변경할 수 없습니다.
