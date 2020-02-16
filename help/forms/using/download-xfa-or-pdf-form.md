---
title: XFA 또는 PDF 양식 템플릿 다운로드
seo-title: XFA 또는 PDF 양식 템플릿 다운로드
description: 저장소에서 로컬 시스템으로 양식을 내보내고 다운로드한 양식을 새 저장소로 마이그레이션할 수 있습니다.
seo-description: 저장소에서 로컬 시스템으로 양식을 내보내고 다운로드한 양식을 새 저장소로 마이그레이션할 수 있습니다.
uuid: 5f7fbd14-cb9d-4749-8708-7efe49df89d7
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: 6699e0e7-fd42-41ae-86a2-3b940d905111
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# XFA 또는 PDF 양식 템플릿 다운로드 {#download-an-xfa-or-a-pdf-form-template}

다운로드 작업은 이름에 따라 저장소에서 로컬 시스템으로 양식을 내보낼 수 있습니다. 이 작업은 업로드 작업과 함께 양식을 한 저장소에서 다른 저장소로 마이그레이션하는 데 도움이 됩니다.

AEM Forms에서 다운로드 작업은 다음 자산 유형에 대해 지원됩니다.

* 양식 템플릿(XFA 양식)
* PDF 양식
* 문서(일반 PDF 파일)

AEM Forms에서는 이러한 양식 유형을 개별적으로 또는 하나 이상의 지원되는 양식이 포함된 폴더에서 다운로드할 수 있습니다.

이러한 에셋 외에도 폴더에 있는 에셋 `Resource` 유형을 다운로드할 수 있습니다. 이 기능은 양식과 함께 XFA 양식에서 참조한 리소스를 다운로드할 수 있도록 제공됩니다.

## 하나 이상의 양식 다운로드 {#download-one-or-more-forms}

1. 에서 AEM Forms 사용자 인터페이스에 로그인합니다 `https://<server>:<port>/aem/forms.html`.

1. 다운로드할 자산의 위치로 이동합니다.

1. 자산을 선택합니다. 도구 모음에서 **[!UICONTROL aem]** 6forms_download ![](assets/aem6forms_download.png) 다운로드 아이콘을 클릭합니다.

   >[!NOTE]
   >
   >다운로드할 양식을 하나만 선택할 수 있습니다. 여러 양식을 다운로드하려면 폴더로 다운로드해야 합니다.

1. 대화 상자가 나타나면 다운로드를 **[!UICONTROL 클릭합니다]**.

   AEM Forms에서 선택한 파일이나 선택한 폴더를 포함하는 ZIP 파일을 생성합니다.

   폴더를 다운로드하는 경우 폴더 내의 지원되는 자산이 기존 계층에 다운로드됩니다.

   ZIP 파일이 시스템의 `Downloads` 폴더에 저장됩니다.

## 업로드 작업에 대한 관련 고려 사항 {#related-considerations-for-the-upload-operation}

* ZIP 파일을 동일한 저장소 또는 다른 저장소의 다른 위치에 업로드할 수 있습니다
* 업로드 작업 동안 폴더의 자산 계층이 유지됩니다
* 다운로드하기 전에 다운로드한 자산에 대한 모든 메타데이터 변경 사항은 업로드 시 반영됩니다.

