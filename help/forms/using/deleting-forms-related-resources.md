---
title: 양식 및 관련 리소스 삭제
seo-title: Deleting forms and related resources
description: AEM Forms에서 양식 또는 자산을 삭제하는 방법, 참조 및 참조 자산 및 XFA 양식에 미치는 영향
seo-description: How to delete a form or an asset in AEM Forms and the impact on referenced and referring assets and XFA forms.
uuid: df522b87-59d8-4678-922d-c9aab82b1381
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: c8519eec-f841-4867-baa9-a9e03042755e
role: Admin
exl-id: b31f9f56-dd33-4478-ad34-01ac7d5a1b40
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---

# 양식 및 관련 리소스 삭제 {#deleting-forms-and-related-resources}

양식과 자산을 삭제하여 저장소에서 이러한 자산을 제거할 수 있습니다. 삭제 작업은 모든 자산 유형 및 폴더에서 작동합니다.

작성자 인스턴스에서 자산을 삭제하는 경우 게시 인스턴스에서도 자산이 삭제됩니다. AEM Forms 서버는 작성자 및 게시 인스턴스로 구성됩니다. 작성 인스턴스는 양식 자산 및 리소스를 만들고 관리하기 위한 것입니다. 게시 인스턴스에는 최종 사용자가 사용할 수 있는 게시된 양식 자산 및 관련 리소스가 포함되어 있습니다.

## 양식을 삭제하는 방법 {#how-to-delete-a-form}

1. 에 액세스하여 AEM Forms 사용자 인터페이스에 로그인 `https://[hostname]:'port'/aem/forms.html.`
1. 로 이동하고 삭제할 양식을 선택합니다. 삭제 를 클릭합니다 ![aem6forms_delete2](assets/aem6forms_delete2.png) 도구 모음에서 삭제 작업을 확인합니다.

   >[!NOTE]
   >
   >한 번에 하나의 양식만 삭제할 수 있습니다. 여러 양식을 개별적으로 삭제하거나 상위 폴더를 삭제합니다.

1. 자산을 삭제하기 전에 AEM Forms에서 참조를 확인하고 명시적 확인을 요청합니다. 관계 상태에 관계없이 자산을 삭제하려면 강제 삭제 를 클릭합니다.

   >[!NOTE]
   >
   >다른 자산에서 참조하는 자산을 삭제하면 기능 문제가 발생할 수 있습니다.

   >[!NOTE]
   >
   >선택한 자산이 폴더이고 해당 계층의 그러한 자산이 포함되어 있는 경우 개별적으로 다른 자산을 삭제하거나 전체 폴더를 삭제합니다.

## 참조된 XFA 양식 삭제에 따른 영향 {#impact-of-deleting-a-referenced-xfa-form}

AEM Forms에서 XFA 양식 템플릿은 적응형 양식 또는 다른 XFA 양식 템플릿에서 참조할 수 있습니다. 또한 템플릿은 리소스 또는 다른 XFA 템플릿을 참조할 수 있습니다.

적응형 양식을 손상시킬 수 있으므로 적응형 양식에서 참조되는 XFA 양식을 삭제하는 것이 좋습니다. 적응형 양식이 XFA 양식을 참조할 때 해당 필드가 바인딩됩니다. XFA 삭제 후에는 적응형 양식이 해당 필드를 XFA 필드와 동기화할 수 없으며 이러한 필드에 대한 오류 메시지를 표시합니다. 참조된 XFA 삭제의 영향 및 더러운 AF에 대한 자세한 내용은 다음을 참조하십시오 [참조된 XFA 양식 업데이트](/help/forms/using/get-xdp-pdf-documents-aem.md#p-updating-referenced-xfa-forms-p).

이러한 XFA 양식을 삭제하려면 적응형 양식을 업데이트하고 XFA 필드로 바인딩을 제거합니다.
