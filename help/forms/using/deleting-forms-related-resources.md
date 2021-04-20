---
title: 양식 및 관련 리소스 삭제
seo-title: 양식 및 관련 리소스 삭제
description: AEM Forms에서 양식이나 자산을 삭제하는 방법, 참조된 자산과 참조 자산 및 XFA 양식에 미치는 영향
seo-description: AEM Forms에서 양식이나 자산을 삭제하는 방법, 참조된 자산과 참조 자산 및 XFA 양식에 미치는 영향
uuid: df522b87-59d8-4678-922d-c9aab82b1381
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: c8519eec-f841-4867-baa9-a9e03042755e
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 0%

---


# 양식 및 관련 리소스 삭제 중 {#deleting-forms-and-related-resources}

양식과 자산을 삭제하여 보관소에서 이러한 자산을 제거할 수 있습니다. 삭제 작업은 모든 자산 유형 및 폴더에서 작동합니다.

작성자 인스턴스에서 자산을 삭제하면 게시 인스턴스에서도 자산이 삭제됩니다. AEM Forms 서버는 작성자 및 게시 인스턴스로 구성됩니다. 작성 인스턴스는 양식 자산 및 리소스를 만들고 관리하는 데 사용됩니다. 게시 인스턴스에는 게시된 양식 에셋과 최종 사용자가 사용할 수 있는 관련 리소스가 포함되어 있습니다.

## {#how-to-delete-a-form} 양식을 삭제하는 방법

1. `https://[hostname]:'port'/aem/forms.html.`에 액세스하여 AEM Forms 사용자 인터페이스에 로그인합니다.
1. 삭제할 양식으로 이동하여 선택합니다. 도구 모음에서 ![aem6forms_delete2](assets/aem6forms_delete2.png) 삭제를 클릭하고 삭제 작업을 확인합니다.

   >[!NOTE]
   >
   >한 번에 하나의 양식만 삭제할 수 있습니다. 여러 양식을 개별적으로 삭제하거나 상위 폴더를 삭제합니다.

1. 자산을 삭제하기 전에 AEM Forms은 참조를 확인하고 명시적 확인을 요청합니다. 관계 상태와 관계없이 자산을 삭제하려면 강제 삭제를 클릭합니다.

   >[!NOTE]
   >
   >다른 자산에서 참조하는 자산을 삭제하면 기능 문제가 발생할 수 있습니다.

   >[!NOTE]
   >
   >선택한 자산이 폴더이고 해당 계층에 해당 자산이 포함되어 있는 경우 다른 자산을 개별적으로 삭제하거나 전체 폴더를 삭제합니다.

## 참조된 XFA 양식 {#impact-of-deleting-a-referenced-xfa-form} 삭제의 영향

AEM Forms에서 XFA 양식 템플릿을 적응형 양식 또는 다른 XFA 양식 템플릿으로 참조할 수 있습니다. 또한 템플릿은 리소스 또는 다른 XFA 템플릿을 참조할 수 있습니다.

적응형 양식이 참조하는 XFA 양식을 삭제하는 것은 적응형 양식을 손상시킬 수 있으므로 바람직하지 않습니다. 응용 양식이 XFA 양식을 참조하면 해당 필드가 바인딩됩니다. XFA 삭제 후 적응형 양식은 해당 필드를 XFA 필드와 동기화할 수 없으며 해당 필드에 대한 오류 메시지를 표시합니다. 참조된 XFA 삭제의 영향과 AF에 대한 자세한 내용은 [참조된 XFA 양식 업데이트](/help/forms/using/get-xdp-pdf-documents-aem.md#p-updating-referenced-xfa-forms-p)를 참조하십시오.

이러한 XFA 양식을 삭제하려면 적응형 양식을 업데이트하고 XFA 필드로 바인딩을 제거합니다.
