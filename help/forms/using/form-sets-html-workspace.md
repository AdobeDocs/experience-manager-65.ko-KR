---
title: AEM Forms Workspace에서 양식 집합 작업
description: formset은 그룹화되어 최종 사용자에게 단일 양식 세트로 제공되는 HTML5 양식의 컬렉션입니다. AEM Forms 작업 영역에서 양식 세트를 사용하여 작업하는 방법을 알아봅니다.
contentOwner: vishgupt
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
exl-id: 76a8f93f-eb8a-4e68-8626-efa6dc67668f
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 97aafc4b-2598-52d6-9012-295a95969e38
    internal-label: HTML5 Forms
  - id: 59f95943-e802-56ac-990d-21ab923984c1
    internal-label: Mobile Forms
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 8%
---
# AEM Forms Workspace에서 양식 집합 작업{#working-with-formsets-in-aem-forms-workspace}

formset은 그룹화되어 최종 사용자에게 단일 양식 세트로 제공되는 HTML5 양식의 컬렉션입니다. 최종 사용자가 양식 세트를 채우기 시작하면 한 양식에서 다른 양식으로 원활하게 전환됩니다. 그런 다음 한 번의 클릭으로 양식 세트를 제출할 수 있습니다. 양식 집합 및 설정 방법에 대한 자세한 내용은 [AEM Forms의 양식 집합](../../forms/using/formset-in-aem-forms.md)을 참조하세요.

AEM Forms 작업 영역은 양식 세트를 지원합니다. 양식 세트를 사용하면 서비스 또는 프로세스와 관련된 여러 양식을 그룹화하여 비즈니스 프로세스를 자동화하고 최종 사용자에게 제공할 수 있습니다. 이러한 시나리오에서는 사용자가 전체 세트를 하나로 채울 수 있으며 개별 양식 또는 프로세스를 파일, 제출 및 추적할 필요가 없습니다.

## AEM Forms 작업 영역 앱에서 시작 지점에 양식 세트 첨부 {#attaching-a-formset-to-startpoint-in-an-aem-forms-workspace-app-br}

1. Workbench에서 업무 프로세스 워크플로우를 생성합니다. 자세한 내용은 [Workbench 도움말](https://www.adobe.com/go/learn_aemforms_workbench_63)을 참조하세요.
1. 시작 지점의 프로세스 속성에서 프레젠테이션 및 데이터의 **CRX 자산 사용**&#x200B;을 선택합니다.

   ![1-3](assets/1-3.png)

1. CRX 자산 경로 옆에 있는 ![찾아보기](assets/browse.png)(찾아보기)를 클릭합니다. 양식 에셋 선택 대화 상자가 나타납니다.

   ![2-1](assets/2-1.png)

1. **Formset** 탭을 클릭하고 목록에서 관련 Formset을 선택한 다음 **확인**&#x200B;을 클릭합니다.

1. 다른 관련 프로세스 속성을 업데이트한 후 애플리케이션을 배포합니다.

## AEM Forms 작업 영역에서 양식 세트 사용 {#using-formset-in-nbsp-aem-forms-workspace}

Formset이 startpoint에 연결되면 AEM Forms 작업 영역에서 다른 startpoint가 호출될 때 startpoint를 호출할 수 있습니다.

AEM Forms 작업 영역을 통해 formset에서 지원되는 작업은 다음과 같습니다.

* 초안으로 저장
* 잠금
* 중단
* 제출
* 첨부 파일 추가
* 메모 추가
* 뒤로 또는 다음 단추를 사용하여 양식 세트에서 양식 간에 이동

![3-1](assets/3-1.png)

>[!NOTE]
>
>양식 세트의 이전 및 다음 양식에서 이동하는 동안 성능 향상을 위해 관련 양식이 완전히 렌더링될 때까지 모든 작업 영역 버튼(뒤로, 다음, 저장, 제출 및 ... (계속))이 비활성화됩니다.
