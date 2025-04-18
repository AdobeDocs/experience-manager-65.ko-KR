---
title: 양식 및 관련 리소스 삭제
description: AEM Forms에서 양식 또는 에셋을 삭제하는 방법 및 참조된 에셋 및 XFA 양식에 미치는 영향
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
role: Admin,User
exl-id: b31f9f56-dd33-4478-ad34-01ac7d5a1b40
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---

# 양식 및 관련 리소스 삭제 {#deleting-forms-and-related-resources}

양식 및 에셋을 삭제하여 저장소에서 이러한 에셋을 제거할 수 있습니다. 삭제 작업은 모든 자산 유형 및 폴더에서 작동합니다.

작성자 인스턴스에서 자산을 삭제하는 경우 해당 자산도 Publish 인스턴스에서 삭제됩니다. AEM Forms 서버는 작성자 및 Publish 인스턴스로 구성됩니다. 작성자 인스턴스는 양식 에셋 및 리소스를 만들고 관리하기 위한 것입니다. Publish 인스턴스에는 최종 사용자가 사용할 수 있는 게시된 양식 에셋 및 관련 리소스가 포함되어 있습니다.

## 양식을 삭제하는 방법 {#how-to-delete-a-form}

1. `https://[hostname]:'port'/aem/forms.html.`에 액세스하여 AEM Forms 사용자 인터페이스에 로그인합니다
1. 삭제할 양식으로 이동하여 선택합니다. 도구 모음에서 ![aem6forms_delete2](assets/aem6forms_delete2.png) 삭제를 클릭하고 삭제 작업을 확인합니다.

   >[!NOTE]
   >
   >한 번에 하나의 양식만 삭제할 수 있습니다. 여러 양식을 개별적으로 삭제하거나 상위 폴더를 삭제합니다.

1. 에셋을 삭제하기 전에 AEM Forms에서 참조를 확인하고 명시적 확인을 요청합니다. 관계 상태에 관계없이 에셋을 삭제하려면 강제 삭제 를 클릭합니다.

   >[!NOTE]
   >
   >다른 에셋에서 참조하는 에셋을 삭제하면 기능 문제가 발생할 수 있습니다.

   >[!NOTE]
   >
   >선택한 에셋이 폴더이고 계층 구조에 해당 에셋이 포함되어 있는 경우 다른 에셋을 개별적으로 삭제하거나 전체 폴더를 삭제합니다.

## 참조된 XFA 양식 삭제의 영향 {#impact-of-deleting-a-referenced-xfa-form}

AEM Forms에서 XFA 양식 템플릿은 적응형 양식 또는 다른 XFA 양식 템플릿으로 참조할 수 있습니다. 또한 템플릿은 리소스 또는 다른 XFA 템플릿을 참조할 수 있습니다.

적응형 양식에서 참조하는 XFA 양식은 적응형 양식을 손상시킬 수 있으므로 삭제하지 않는 것이 좋습니다. 적응형 양식이 XFA 양식을 참조하는 경우 해당 필드가 바인딩됩니다. XFA를 삭제한 후 적응형 양식은 해당 필드를 XFA 필드와 동기화할 수 없으며 해당 필드에 대한 오류 메시지를 표시합니다. 참조된 XFA 삭제의 영향 및 더티 AF에 대한 자세한 내용은 [참조된 XFA 양식 업데이트](/help/forms/using/get-xdp-pdf-documents-aem.md#p-updating-referenced-xfa-forms-p)를 참조하십시오.

이러한 XFA 양식을 삭제하려면 적응형 양식을 업데이트하고 XFA 필드가 있는 바인딩을 제거합니다.
