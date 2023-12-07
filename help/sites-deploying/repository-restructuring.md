---
title: AEM 6.5의 저장소 재구성
description: AEM 6.5에서 저장소 구조 변경의 기본 사항과 추리에 대해 알아봅니다.
contentOwner: chaikels
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
feature: Upgrading
exl-id: 2572aa8d-2a3a-4e5b-ae5f-07e1017ea0f4
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 0%

---

# AEM 6.5의 저장소 재구성{#repository-restructuring-in-aem}

## 소개 {#introduction}

AEM 6.4 이전에는 고객 코드가 업그레이드 시 변경될 수 있었던 JCR의 예측 불가능한 영역에 배포되었습니다. 이러한 이유로 공식 AEM 릴리스는 사용자 지정 코드, 구성 또는 콘텐츠를 덮어쓰는 것이 일반적이었습니다. 또한 고객 변경 사항이 AEM 제품 코드나 콘텐츠를 덮어쓰면서 제품 기능을 손상시키는 경우도 있었습니다.

AEM 제품 코드 및 고객 코드에 대한 계층을 명확하게 기술하면 이러한 충돌을 피할 수 있습니다.

이를 위해 AEM 6.4부터 시작하여 향후 릴리스에서 계속 컨텐츠가 다음과 같은 높은 수준의 규칙을 준수하며 컨텐츠 위치에 대한 지침과 함께 /etc에서 저장소의 다른 폴더로 재구성되고 있습니다.

* AEM 제품 코드는 항상 /libs에 배치되며, 이는 사용자 지정 코드로 덮어쓸 수 없습니다
* 사용자 지정 코드는 /apps, /content 및 /conf에 배치해야 합니다.

## 6.5 업그레이드에 미치는 영향 {#impact-on-upgrades}

AEM 6.5로 업그레이드할 때 /etc 아래의 큰 콘텐츠 하위 세트는 저장소의 다른 폴더에 복제됩니다. 이러한 새 위치는 콘텐츠를 참조하는 기본 설정 위치입니다. 그러나 AEM 6.5 업그레이드가 /etc 폴더의 이전 위치와 역호환되도록 모든 시도가 이루어졌습니다. 따라서 대부분의 경우 이전 위치는 고객 애플리케이션에서 적극적으로(그리고 많은 경우 수동으로) 변경될 때까지 AEM 코드에서 계속 참조됩니다. 타임라인 관점에서 보면 두 가지 범주의 변경 사항이 있습니다.

* 6.5 업그레이드 사용 - 일부 /etc 재구성 변경 사항은 이전 버전과 호환되지 않으므로 AEM 6.5 업그레이드의 일부로 수정 사항을 계획하고 구현해야 합니다.
* 향후 업그레이드 이전 - /etc 재구조화 변경의 대부분은 향후 업그레이드 이후 일정 시간이 될 때까지 연기될 수 있습니다. 앞에서 언급했듯이 AEM 6.5 코드는 수정 사항이 고객 릴리스의 일부로 구현될 때까지 이전 위치를 계속 참조합니다. 변경해야 하는 강제 타임라인은 없지만, 향후 기능은 참조되는 새 위치에 따라 달라질 수 있으므로 향후 업그레이드 전에 변경하는 것이 좋습니다. 또한 특정 기능에 대한 설명서는 규칙에서 새 위치를 참조하므로 이전 위치가 계속 사용되고 있는지 헷갈릴 수 있습니다.

### 구조 조정 지침 {#restructuring-guidance}

AEM 6.5로의 업그레이드를 계획하는 동안 다음의 솔루션별 페이지를 참조하여 작업 노력을 평가해야 합니다.

* [모든 AEM 솔루션에 공통되는 저장소 재구성](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md)
* [AEM Sites 저장소 재구성](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md)
* [AEM Assets 저장소 재구성](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md)
* [AEM Assets Dynamic Media 저장소 재구성](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md)
* [AEM Forms 저장소 재구성](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md)
* [AEM Communities 저장소 재구성](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md)
* [AEM Commerce 저장소 재구성](/help/sites-deploying/ecommerce-repository-restructuring-in-aem-6-5.md)

각 페이지에는 필요한 변경 사항의 긴급성에 해당하는 두 개의 섹션이 포함되어 있습니다. AEM 6.5 업그레이드 프로젝트의 일부로 &quot;6.5 업그레이드 사용&quot; 섹션의 모든 항목을 처리해야 합니다. &quot;향후 업그레이드 이전&quot; 아래의 모든 항목은 업그레이드 이후 까지 선택적으로 연기할 수 있습니다.

페이지의 각 항목에는 &quot;재구성 지침&quot; 필드가 포함되어 있으며, 이 필드에서는 이전에 /etc 폴더 아래에 있던 콘텐츠에 대해 새 위치가 참조되도록 새 6.5 저장소 모델에 맞춰 정렬하는 데 권장되는 기술 전략을 자세히 설명합니다. 추가 &quot;메모&quot; 필드는 유용한 추가 컨텍스트를 제공합니다.
