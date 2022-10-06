---
title: XFA 또는 PDF 양식 템플릿을 다운로드합니다
seo-title: Download an XFA or a PDF form template
description: 리포지토리에서 로컬 시스템으로 양식을 내보내고 다운로드한 양식을 새 리포지토리로 마이그레이션할 수 있습니다.
seo-description: You can export forms from the repository to the local system and migrate the downloaded forms to new repository.
uuid: 5f7fbd14-cb9d-4749-8708-7efe49df89d7
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: 6699e0e7-fd42-41ae-86a2-3b940d905111
role: Admin
exl-id: 5b7b9816-38c1-4780-b1fc-8184971f3772
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 0%

---

# XFA 또는 PDF 양식 템플릿을 다운로드합니다 {#download-an-xfa-or-a-pdf-form-template}

이름이 의미하듯이 다운로드 작업을 통해 리포지토리에서 로컬 시스템으로 양식을 내보낼 수 있습니다. 업로드 작업과 함께 이 작업을 사용하면 양식을 한 저장소에서 다른 저장소로 마이그레이션하는 데 도움이 됩니다.

AEM Forms에서 다운로드 작업은 다음 자산 유형에 대해 지원됩니다.

* 양식 템플릿(XFA Forms)
* PDF forms
* 문서(플랫 PDF 파일)

AEM Forms에서는 이러한 양식 유형을 개별적으로 또는 하나 이상의 지원되는 양식이 포함된 폴더에서 다운로드할 수 있습니다.

이러한 자산 외에 `Resource` 폴더에 있는 자산 유형입니다. 이 기능은 XFA 양식에서 참조하는 리소스를 양식과 함께 다운로드할 수 있도록 해줍니다.

## 하나 이상의 양식 다운로드 {#download-one-or-more-forms}

1. 의 AEM Forms 사용자 인터페이스에 로그인합니다. `https://<server>:<port>/aem/forms.html`.

1. 다운로드할 자산의 위치로 이동합니다.

1. 자산을 선택합니다. 을(를) 클릭합니다. **[!UICONTROL 다운로드]** ![aem6forms_download](assets/aem6forms_download.png) 아이콘 을 클릭하여 제품에서 사용할 수 있습니다.

   >[!NOTE]
   >
   >하나의 양식만 다운로드하도록 선택할 수 있습니다. 여러 양식을 다운로드하려면 양식을 폴더로 다운로드해야 합니다.

1. 대화 상자가 나타나면 **[!UICONTROL 다운로드]**.

   AEM Forms은 선택한 파일 또는 선택한 폴더가 포함된 ZIP 파일을 생성합니다.

   폴더를 다운로드하는 경우 폴더 내에 지원되는 자산이 기존 계층에서 다운로드됩니다.

   ZIP 파일은 `Downloads` 폴더의 이름을 지정합니다.

## 업로드 작업에 대한 관련 고려 사항 {#related-considerations-for-the-upload-operation}

* ZIP 파일을 동일한 리포지토리 또는 다른 리포지토리의 다른 위치에 업로드할 수 있습니다
* 업로드 작업 중에 폴더에 있는 자산의 계층 구조가 유지됩니다
* 다운로드 전에 다운로드한 자산에 대한 모든 메타데이터 변경 사항이 업로드 시 반영됩니다
