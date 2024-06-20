---
title: XFA 또는 PDF 양식 템플릿 다운로드
description: 저장소에서 로컬 시스템으로 양식을 내보내고 다운로드한 양식을 새 저장소로 마이그레이션할 수 있습니다.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
role: Admin,User
exl-id: 5b7b9816-38c1-4780-b1fc-8184971f3772
solution: Experience Manager, Experience Manager Forms
feature: Interactive Communication
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---

# XFA 또는 PDF 양식 템플릿 다운로드 {#download-an-xfa-or-a-pdf-form-template}

이름에서 알 수 있듯이 다운로드 작업을 통해 저장소에서 로컬 시스템으로 양식을 내보낼 수 있습니다. 업로드 작업과 함께 이 작업을 수행하면 양식을 한 저장소에서 다른 저장소로 마이그레이션할 수 있습니다.

AEM Forms에서 다운로드 작업은 다음 자산 유형에 대해 지원됩니다.

* 양식 템플릿(XFA Forms)
* PDF forms
* 문서(플랫 PDF 파일)

AEM Forms에서는 이러한 양식 유형을 개별적으로 또는 지원되는 하나 이상의 양식이 포함된 폴더에서 다운로드할 수 있습니다.

이러한 에셋 외에도 다음을 다운로드할 수 있습니다. `Resource` 에셋이 폴더에 있는 경우 에셋 유형입니다. 이 기능을 사용하면 양식과 함께 XFA 양식에서 참조하는 리소스를 다운로드할 수 있습니다.

## 하나 이상의 양식 다운로드 {#download-one-or-more-forms}

1. 다음 위치에서 AEM Forms 사용자 인터페이스에 로그인합니다. `https://<server>:<port>/aem/forms.html`.

1. 다운로드하려는 에셋의 위치로 이동합니다.

1. 자산을 선택합니다. 다음을 클릭합니다. **[!UICONTROL 다운로드]** ![aem6forms_download](assets/aem6forms_download.png) 아이콘을 클릭합니다.

   >[!NOTE]
   >
   >다운로드할 양식을 하나만 선택할 수 있습니다. 여러 양식을 다운로드하려면 폴더로 다운로드해야 합니다.

1. 표시되는 대화 상자에서 **[!UICONTROL 다운로드]**.

   AEM Forms은 선택한 파일 또는 선택한 폴더가 포함된 ZIP 파일을 생성합니다.

   폴더를 다운로드하는 경우 폴더 내에서 지원되는 에셋은 기존 계층 구조로 다운로드됩니다.

   ZIP 파일이 `Downloads` 폴더에 저장합니다.

## 업로드 작업에 대한 관련 고려 사항 {#related-considerations-for-the-upload-operation}

* ZIP 파일을 동일한 저장소 또는 다른 저장소의 다른 위치에 업로드할 수 있습니다
* 폴더의 에셋 계층은 업로드 작업 중에 유지됩니다
* 다운로드하기 전에 다운로드한 에셋에 대한 모든 메타데이터 변경 사항은 업로드 시 반영됩니다
