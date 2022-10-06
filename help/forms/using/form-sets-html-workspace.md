---
title: AEM Forms 작업 공간에서 양식 작업
seo-title: Working with Formsets in AEM Forms workspace
description: 양식 세트는 HTML5 양식을 그룹화하고 최종 사용자에게 단일 양식 세트로 제공하는 컬렉션입니다. AEM Forms 작업 공간에서 양식 세트를 사용하는 방법을 알아봅니다.
seo-description: A formset is a collection of HTML5 forms grouped and presented as a single set of forms to end users. Learn how you can work with formsets in AEM Forms workspace.
uuid: 1a5f3ce8-1d6a-497e-90d0-49765e40cf3b
contentOwner: vishgupt
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: f550b747-2def-4317-9ef7-dc6c1e7bb404
docset: aem65
exl-id: 76a8f93f-eb8a-4e68-8626-efa6dc67668f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 3%

---

# AEM Forms 작업 공간에서 양식 작업{#working-with-formsets-in-aem-forms-workspace}

양식 세트는 HTML5 양식을 그룹화하고 최종 사용자에게 단일 양식 세트로 제공하는 컬렉션입니다. 최종 사용자가 양식 세트에 채우기를 시작하면 한 양식에서 다른 양식으로 원활하게 전환됩니다. 한 번의 클릭으로 양식 세트를 제출할 수 있습니다. 양식 세트 및 설정 방법에 대한 자세한 내용은 [AEM Forms의 양식](../../forms/using/formset-in-aem-forms.md).

AEM Forms 작업 공간에서 양식 세트를 지원합니다. 양식 세트를 사용하면 서비스 또는 프로세스와 관련된 여러 양식을 그룹화하여 비즈니스 프로세스를 자동화하고 최종 사용자에게 제공할 수 있습니다. 이러한 시나리오에서는 사용자가 전체 세트를 하나로 채울 수 있으며 개별 양식이나 프로세스를 파일, 제출 및 추적할 필요가 없습니다.

## AEM Forms 작업 공간 앱에서 시작점에 양식 세트 첨부 {#attaching-a-formset-to-startpoint-in-an-aem-forms-workspace-app-br}

1. Workbench에서 비즈니스 프로세스 워크플로우를 만듭니다. 자세한 내용은 [Workbench 도움말](https://www.adobe.com/go/learn_aemforms_workbench_63).
1. 시작점의 프로세스 속성에서 다음을 선택합니다 **CRX 자산 사용** 을 참조하십시오.

   ![1-3](assets/1-3.png)

1. 클릭 ![찾아보기](assets/browse.png) CRX 자산 경로 옆에 있는 (찾아보기) . 양식 자산 선택 대화 상자가 나타납니다.

   ![2-1](assets/2-1.png)

1. 을(를) 클릭합니다. **Formset** 탭에서 관련 양식 세트를 선택한 다음 **확인**.

1. 다른 관련 프로세스 속성을 업데이트한 후 응용 프로그램을 배포합니다.

## AEM Forms 작업 영역에서 양식 세트 사용 {#using-formset-in-nbsp-aem-forms-workspace}

양식 세트가 시작점에 연결되면 다른 시작점이 호출될 때 AEM Forms 작업 영역에서 시작점을 호출할 수 있습니다.

AEM Forms 작업 공간을 통해 양식 세트에서 지원되는 작업은 다음과 같습니다.

* 초안으로 저장
* 잠금
* 중단
* 제출
* 첨부 파일 추가
* 메모 추가
* 뒤로 또는 다음 단추를 사용하여 양식 세트의 양식 간을 이동합니다.

![3-1](assets/3-1.png)

>[!NOTE]
>
>양식 세트의 이전 양식과 다음 양식에서 이동하는 동안 성능 향상을 위해 관련 양식이 완전히 렌더링될 때까지 모든 작업 공간 단추(뒤로, 다음, 저장, 제출 및 ...(자세히))가 비활성화됩니다.
