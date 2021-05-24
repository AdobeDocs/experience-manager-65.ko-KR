---
title: AEM 6.5의 저장소 구조 변경
seo-title: AEM 6.5의 저장소 구조 변경
description: AEM 6.5의 저장소 구조 변경 이면의 기본 사항과 논리에 대해 알아봅니다
seo-description: AEM 6.5의 저장소 구조 변경 이면의 기본 사항과 논리에 대해 알아봅니다
uuid: e9cd3e88-e352-44a8-9b97-69488d3267cb
contentOwner: chaikels
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: fc879b0b-823b-4bdc-aaa6-36f53a33fb22
feature: 업그레이드
exl-id: 2572aa8d-2a3a-4e5b-ae5f-07e1017ea0f4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---

# AEM 6.5에서의 저장소 구조 변경{#repository-restructuring-in-aem}

## 소개 {#introduction}

AEM 6.4 이전에는 업그레이드 시 변경될 수 있는 JCR의 예측할 수 없는 영역에 고객 코드가 배포되었습니다. 이러한 이유로 공식 AEM 릴리스에서 사용자 지정 코드, 구성 또는 컨텐츠를 덮어쓰는 것이 일반적이었습니다. 또한 고객이 변경했을 때 AEM 제품 코드 또는 컨텐츠가 오버라이드되어 제품 기능이 손상되는 경우가 있습니다.

AEM 제품 코드 및 고객 코드에 대한 계층을 명확히 설명함으로써 이러한 충돌을 피할 수 있습니다.

이를 위해 AEM 6.4부터 향후 릴리스에서 컨텐츠를 계속 사용할 수 있도록 다음과 같은 높은 수준의 규칙을 준수하면서 컨텐츠의 위치에 대한 지침과 함께 저장소의 다른 폴더로 컨텐츠가 재구성됩니다.

* AEM 제품 코드는 항상 /libs에 삽입되며, 사용자 지정 코드로 덮어쓰지 않아야 합니다
* 사용자 지정 코드는 /apps, /content 및 /conf에 삽입해야 합니다

## 6.5 업그레이드에 미치는 영향 {#impact-on-upgrades}

AEM 6.5로 업그레이드할 때 /etc 아래에 있는 컨텐츠의 큰 하위 세트가 저장소의 다른 폴더에 복제됩니다. 이러한 새 위치는 컨텐츠를 참조하는 기본 위치입니다. 그러나 AEM 6.5 업그레이드가 /etc 폴더의 이전 위치와 이전 호환되도록 모든 시도가 수행되었으므로 대부분의 경우 변경 사항이 활성 상태가 될 때까지 및 대부분의 경우 수동으로 고객의 애플리케이션에서 수행될 때까지 AEM 코드에서 이전 위치를 계속 참조합니다. 타임라인 관점에서 변경 사항에는 두 가지 카테고리가 있습니다.

* 6.5 업그레이드 포함 - 일부 /etc 재구성 변경 사항은 이전 버전과 호환되지 않으므로 AEM 6.5 업그레이드의 일부로 수정 사항을 계획하고 구현해야 합니다.
* 향후 업그레이드 전 - 향후 업그레이드 후 어느 시점까지 /etc 재구성 변경 사항 대부분을 지연할 수 있습니다. 이전에 언급했듯이 AEM 6.5 코드는 수정 사항이 고객 릴리스의 일부로 구현될 때까지 이전 위치를 계속 참조합니다. 변경해야 하는 강제 타임라인은 없지만, 향후 기능은 참조되는 새 위치에 따라 사용될 수 있으므로 향후 업그레이드 전에 수행하는 것이 좋습니다. 또한 주어진 기능에 대한 설명서는 새 위치를 참조하므로 이전 위치가 계속 사용되고 있는 경우 혼동될 수 있습니다.

### 구조 조정 지침 {#restructuring-guidance}

AEM 6.5로 업그레이드를 계획하는 동안 작업 노력을 평가하려면 다음의 솔루션 당 페이지를 참조해야 합니다.

* [모든 AEM 솔루션에 공통으로 사용되는 저장소 구조 변경](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md)
* [AEM Sites 저장소 구조 변경](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md)
* [AEM Assets 저장소 구조 변경](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md)
* [AEM Assets Dynamic Media 저장소 구조 변경](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md)
* [AEM Forms 저장소 구조 변경](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md)
* [AEM Communities 저장소 구조 변경](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md)
* [AEM Commerce 저장소 구조 변경](/help/sites-deploying/ecommerce-repository-restructuring-in-aem-6-5.md)

각 페이지에는 필요한 변경 사항의 긴급성에 해당하는 두 개의 섹션이 있습니다. 6.5 업그레이드 사용 섹션 아래의 모든 것은 AEM 6.5 업그레이드 프로젝트의 일부로 해결되어야 합니다. &quot;향후 업그레이드 전&quot;에 포함된 모든 항목은 업그레이드 후 까지 선택적으로 지연될 수 있습니다.

페이지의 각 항목에는 &quot;구조 조정 지침&quot; 필드가 포함되어 있습니다. 이 필드에는 새 위치가 /etc 폴더 아래에 이전에 있는 컨텐츠에 대해 참조되도록 새 6.5 저장소 모델과 정렬하기 위해 권장되는 기술 전략이 자세히 설명되어 있습니다. 추가 &quot;참고&quot; 필드는 유용한 추가 컨텍스트를 제공합니다.
