---
title: 새 폴더를 만들어 양식을 분류합니다.
seo-title: 새 폴더를 만들어 양식을 분류합니다.
description: 폴더를 사용하여 양식 템플릿, PDF, 리소스 및 적응형 양식을 구성할 수 있습니다.
seo-description: 폴더를 사용하여 양식 템플릿, PDF, 리소스 및 적응형 양식을 구성할 수 있습니다.
uuid: 63fcb807-c9cf-49ae-ad69-6b1187543470
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: 2a8f4380-8d0f-4354-b2da-4e0c02a545e3
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 새 폴더를 만들어 양식을 분류합니다. {#create-new-folders-to-categorize-forms}

폴더를 사용하여 자산을 보다 효율적으로 구성할 수 있습니다. AEM Forms는 양식 템플릿, PDF, 문서, 리소스, 적응형 양식 등 다양한 유형의 자산을 지원하므로 폴더를 사용하여 원하는 기준에 따라 양식을 분류할 수 있습니다.

AEM Forms를 사용하면 폴더의 제목을 변경할 수 있습니다. 제목은 폴더가 저장소에 저장된 노드의 이름과 다릅니다. 대신 제목은 폴더의 메타데이터로 유지됩니다. 폴더의 제목을 변경할 경우 폴더 내에 있는 자산의 경로는 영향을 받지 않습니다.

## 폴더 만들기 {#create-a-folder}

다음 방법 중 하나를 사용하여 AEM Forms에서 폴더를 만들 수 있습니다.

* 원하는 폴더 구조의 에셋이 포함된 ZIP 파일 업로드(AEM Forms [에서 XDP 및 PDF 문서 가져오기 참조](/help/forms/using/get-xdp-pdf-documents-aem.md))

* 새 빈 폴더 만들기

1. 에서 AEM Forms 사용자 인터페이스에 로그인합니다 `https://<server>:<port>/aem/forms.html`.
1. 폴더를 만들 위치로 이동합니다.
1. 도구 모음에서 ![aem6forms_add](assets/aem6forms_add.png) 아이콘을 클릭한 다음 폴더 **[!UICONTROL 만들기를 선택합니다]**.

1. 다음 세부 정보를 입력합니다.

   * **** 제목:폴더의 표시 이름
   * **** 이름:( *필수)* 보관소에 폴더를 저장할 노드 이름
   >[!NOTE]
   >
   >기본적으로 이름 필드의 값은 제목에서 자동으로 채워집니다. 이름에는 영숫자나 하이픈(-) 및 밑줄(_) 특수 문자만 사용할 수 있습니다. 제목에 입력한 다른 특수 문자는 자동으로 하이픈으로 대체되며 새 이름을 확인하는 메시지가 표시됩니다. 제안된 이름을 계속 사용하거나 추가로 편집할 수 있습니다.

1. 제출을 **[!UICONTROL 클릭합니다].**

   정의한 제목이 있는 새 폴더가 자산 목록의 현재 위치에 표시됩니다.

   지정된 이름의 폴더가 있는 경우 오류가 발생하여 제출이 실패합니다. 이름 필드 옆에 표시되는 ![aem6forms_error_alert](assets/aem6forms_error_alert.png) 아이콘 위로 마우스를 가져가면 오류 메시지를 볼 수 있습니다.

### 폴더 제목 편집 {#edit-the-folder-title-br}

1. 제목을 편집할 폴더를 선택합니다.
1. 도구 모음에서 ![aem6forms_edit](assets/aem6forms_edit.png) 편집 아이콘을 클릭합니다.
1. 새 제목을 입력합니다. 텍스트 필드는 폴더 제목의 현재 값으로 미리 채워집니다. 새 값으로 변경할 수 있습니다.
1. 제출을 **[!UICONTROL 클릭합니다].**

