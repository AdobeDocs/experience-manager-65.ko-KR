---
title: 적응형 양식 재사용
seo-title: 적응형 양식 재사용
description: 기존 적응형 양식을 재사용하여 새로운 적응형 양식을 만들 수 있습니다.
seo-description: 기존 적응형 양식을 재사용하여 새로운 적응형 양식을 만들 수 있습니다.
uuid: f1d0fb70-e255-4dd9-8e6d-fd65eaf2e81a
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: ef564750-f107-41cb-887e-fc6d22b7d32e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 적응형 양식 재사용 {#reusing-adaptive-forms}

## 소개 {#introduction}

기존 적응형 양식의 속성 중 일부를 사용하여 새 양식을 만들려면 복사-붙여넣기 기능을 사용하면 됩니다. 또한 새 적응형 양식을 원하는 폴더 경로에 붙여넣을 수 있습니다. 모든 메타데이터 속성이 복제되고 XFA 및 XSD 기반 응용 양식의 XFA 및 XSD도 복사됩니다.

>[!NOTE]
>
>상태 및 검토 세부 정보는 복사되지 않습니다. 예를 들어 적응형 양식이 게시되어 있는 경우 붙여넣은 적응형 양식이 게시 취소 상태입니다. 마찬가지로, 복사된 자산이 검토 중인 경우 붙여넣은 자산은 동일한 검토 아래에 있지 않습니다.

### 적응형 양식 복사 {#copy-an-adaptive-form}

다음 방법 중 하나를 사용하여 적응형 양식을 복사합니다.

1. 빠른 ![작업에서 aem6forms_copy](assets/aem6forms_copy.png) 아이콘 복사를 클릭합니다.

   >[!NOTE]
   >
   >빠른 작업은 마우스로 가리키면 축소판 위에 표시되는 작업 항목입니다.

1. 적응형 양식을 선택합니다. 보기 수에 따라 선택 프로세스가 다릅니다.

   카드 보기에서는 aem6forms_check-circle ![선택](assets/aem6forms_check-circle.png) 아이콘을 클릭하여 선택 모드로 이동하고 복사할 모든 적응형 양식을 클릭합니다.

   목록 보기에 있는 경우 모든 적응형 양식의 확인란을 클릭하여 선택합니다.

   >[!NOTE]
   >
   >복사-붙여넣기 기능은 적응형 양식에만 지원되므로 선택한 모든 에셋이 적응형 양식이어야 하며 선택한 모든 에셋이 동일한 폴더에 있어야 합니다.

   자산을 선택한 후 도구 모음에 ![있는 aem6forms_copy](assets/aem6forms_copy.png) 복사 아이콘을 클릭하여 선택한 적응형 양식을 복사합니다.

### 적응형 양식 붙여넣기 {#paste-an-adaptive-form}

복사 작업을 클릭하면 선택 모드가 자동으로 종료되고 붙여넣기 ![aem6forms_paste](assets/aem6forms_paste.png) 아이콘이 표시됩니다. 이제 원하는 폴더 경로로 이동하고 ![aem6forms_paste](assets/aem6forms_paste.png) 아이콘을 클릭하여 복사한 적응형 양식을 붙여 넣습니다.

동일한 폴더 또는 CRX 저장소에 저장된 동일한 노드 이름을 가진 다른 파일을 이 대상 폴더에 붙여넣는 경우 1은 접미사에 추가됩니다(예: myaf1은 myaf1이 되고 myaf1이 같은 위치에 있으면 myaf2가 됩니다.) 다른 모든 속성은 원래 응용 양식과 동일하게 유지됩니다.

aem6forms_paste ![](assets/aem6forms_paste.png) 아이콘을 클릭하면 다시 숨겨집니다. 한 번에 한 번만 붙여넣을 수 있습니다. 동일한 자산의 사본을 다시 만들려면 다시 복사합니다.

### 새로운 적응형 양식의 내용 변경 {#change-contents-of-new-adaptive-form}

붙여넣은 적응형 양식의 내용은 다음 방법을 사용하여 복사한 양식과 다르게 변경할 수 있습니다.

1. **메타데이터 속성 변경:**

   적응형 양식의 메타데이터 속성(예: 제목 및 설명)을 변경할 수 있습니다. 메타데이터 속성 및 메타데이터 변경 방법에 대한 자세한 내용은 양식 메타데이터 [관리를 참조하십시오](/help/forms/using/manage-form-metadata.md)

1. **XFA/XSD 기반 적응형 양식의 XFA/XSD 변경:**

   적응형 양식에 사용된 XFA/XSD를 변경할 수 있습니다. 이러한 적응형 양식을 변경할 수 있는 방법에 대해 알아보려면 양식 [메타데이터 관리를 참조하십시오](/help/forms/using/manage-form-metadata.md)

1. **재게시:**

   붙여넣은 자산은 복사한 자산과 다릅니다. 최종 사용자가 사용할 수 있도록 새 자산으로 게시할 수 있습니다. 자산을 게시하는 방법에 대한 자세한 내용은 양식 게시 [및 게시 취소를 참조하십시오.](/help/forms/using/publishing-unpublishing-forms.md)

