---
title: PDF 문서에서 유효하고 만료된 인증서 인식
description: PDF 문서에서 유효하고 만료된 인증서를 인식하는 방법에 대해 알아봅니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: dfe2823a-3a0d-4e45-8765-f618529e22dd
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---

# PDF 문서에서 유효하고 만료된 인증서 인식 {#recognizing-valid-and-expired-certificates-in-pdf-documents}

Reader 확장에서 적용한 사용 권한이 있는 PDF 문서를 Adobe Reader에서 열면 PDF 문서에 활성화된 특정 사용 권한을 설명하는 상태 표시줄이 나타납니다.

PDF 문서에 대한 사용 권한을 지정하는 디지털 인증서가 만료되고 PDF 문서가 Adobe Reader에서 열리면 대화 상자에서 PDF 문서에 사용 권한이 있지만 사용 권한은 비활성화되어 있다고 사용자에게 알립니다. 메시지는 PDF 문서가 변경되었거나 변조되었음을 나타내지만, 반드시 그러할 필요는 없습니다. 인증서가 만료되거나 문서가 수정되면 Adobe Reader에서 이 메시지를 표시합니다. Adobe Reader 7.0.x 이상에서는 현재 문제가 되는 사례를 확인할 수 없습니다.

대화 상자를 닫으면 Adobe Reader에서 PDF 문서를 엽니다. Acrobat Reader DC 확장을 사용하여 적용된 사용 권한은 예상대로 사용할 수 없습니다. PDF 문서가 대화형 양식인 경우 양식 필드가 잠기고 사용자가 양식 데이터를 변경할 수 없습니다.
