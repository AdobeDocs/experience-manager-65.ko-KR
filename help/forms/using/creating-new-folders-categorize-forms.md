---
title: 양식을 분류할 새 폴더 만들기
seo-title: Create new folders to categorize forms
description: 양식 템플릿, PDF, 리소스 및 적응형 양식을 구성하려면 폴더를 사용하십시오.
seo-description: Use folders to organize your form templates, PDFs, resources, and adaptive forms.
uuid: 63fcb807-c9cf-49ae-ad69-6b1187543470
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: 2a8f4380-8d0f-4354-b2da-4e0c02a545e3
role: Admin
exl-id: f8af1ac3-6a95-4f91-8979-6b41a7e02ca4
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 0%

---

# 양식을 분류할 새 폴더 만들기 {#create-new-folders-to-categorize-forms}

폴더를 사용하여 자산을 더 잘 구성할 수 있습니다. AEM Forms은 양식 템플릿, PDF, 문서, 리소스, 적응형 양식 등의 여러 유형의 자산을 다양한 메타데이터로 지원하므로 폴더를 사용하여 원하는 기준에 따라 양식을 분류할 수 있습니다.

AEM Forms을 사용하면 폴더의 제목을 변경할 수 있습니다. 제목은 폴더가 저장소에 저장되는 노드의 이름과 다릅니다. 대신, 제목은 폴더의 메타데이터로 유지됩니다. 폴더의 제목을 변경할 경우 폴더 내에 있는 모든 자산의 경로가 영향을 받지 않습니다.

## 폴더를 만듭니다 {#create-a-folder}

다음 방법 중 하나로 AEM Forms에서 폴더를 만들 수 있습니다.

* 원하는 폴더 구조에서 자산이 포함된 ZIP 파일을 업로드합니다(참조: [AEM Forms에서 XDP 및 PDF 문서 가져오기](/help/forms/using/get-xdp-pdf-documents-aem.md))

* 새 빈 폴더 만들기

1. 의 AEM Forms 사용자 인터페이스에 로그인합니다. `https://<server>:<port>/aem/forms.html`.
1. 폴더를 만들 위치로 이동합니다.
1. 을(를) 클릭합니다. ![aem6forms_add](assets/aem6forms_add.png) 아이콘을 클릭한 다음 **[!UICONTROL 폴더 만들기]**.

1. 다음 세부 정보를 입력합니다.

   * **제목:** 폴더의 이름 표시
   * **이름:** *(필수입니다)* 저장소에 폴더를 저장할 노드 이름

   >[!NOTE]
   >
   >기본적으로 이름 필드의 값은 제목에서 자동으로 채워집니다. 이름에는 영숫자만 사용할 수 있고 하이픈(-)과 밑줄(_) 특수 문자만 사용할 수 있습니다. 제목에 입력한 다른 특수 문자는 하이픈으로 자동 대체되며 새 이름을 확인하라는 메시지가 표시됩니다. 제안된 이름을 계속 사용하거나 추가로 편집할 수 있습니다.

1. 클릭 **[!UICONTROL 제출].**

   정의한 제목이 있는 새 폴더가 자산 목록의 현재 위치에 표시됩니다.

   지정된 이름의 폴더가 있는 경우 오류가 발생하여 제출이 실패합니다. 마우스를 오류 위로 가져가면 오류 메시지를 볼 수 있습니다 ![aem6forms_error_alert](assets/aem6forms_error_alert.png) 이름 필드 옆에 표시되는 아이콘입니다.

### 폴더 제목을 편집합니다 {#edit-the-folder-title-br}

1. 제목을 편집할 폴더를 선택합니다.
1. 편집을 클릭합니다 ![aem6forms_edit](assets/aem6forms_edit.png) 아이콘 을 클릭하여 제품에서 사용할 수 있습니다.
1. 새 제목을 입력합니다. 텍스트 필드는 폴더 제목의 현재 값으로 미리 채워집니다. 새 값으로 변경할 수 있습니다.
1. 클릭 **[!UICONTROL 제출].**
