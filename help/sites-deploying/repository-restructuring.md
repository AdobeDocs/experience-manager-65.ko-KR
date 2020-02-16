---
title: AEM 6.5의 저장소 재구성
seo-title: AEM 6.5의 저장소 재구성
description: AEM 6.5의 저장소 구조 조정의 기본 사항 및 이유를 알아봅니다.
seo-description: AEM 6.5의 저장소 구조 조정의 기본 사항 및 이유를 알아봅니다.
uuid: e9cd3e88-e352-44a8-9b97-69488d3267cb
contentOwner: chaikels
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: fc879b0b-823b-4bdc-aaa6-36f53a33fb22
translation-type: tm+mt
source-git-commit: 97b2da315fac6f84fcba6d4464bf8dd1d690cfd1

---


# AEM 6.5의 저장소 재구성{#repository-restructuring-in-aem}

## 소개 {#introduction}

AEM 6.4 이전에 고객 코드는 업그레이드 시 변경될 수 있는 JCR의 예측할 수 없는 영역에 배포되었습니다. 이러한 이유로, 공식적인 AEM 릴리스가 사용자 지정 코드, 구성 또는 컨텐츠를 덮어쓰는 것이 일반적입니다. 또한 고객이 AEM 제품 코드 또는 컨텐츠를 덮어써서 제품 기능을 깨는 경우도 있습니다.

AEM 제품 코드 및 고객 코드에 대한 계층 구조를 명확하게 구분함으로써 이러한 충돌을 방지할 수 있습니다.

이를 위해 AEM 6.4부터 시작하여 향후 릴리스에서 계속 진행할 예정인 컨텐츠는 다음과 같은 고급 규칙을 준수하면서 컨텐츠의 위치에 대한 지침과 함께 저장소의 다른 폴더로 재구성됩니다.

* AEM 제품 코드는 항상 /libs에 삽입되며, 이 코드는 사용자 지정 코드로 덮어쓰지 않아야 합니다.
* 사용자 정의 코드는 /apps, /content 및 /conf에 삽입해야 합니다.

## 6.5 업그레이드에 대한 영향 {#impact-on-upgrades}

AEM 6.5로 업그레이드하면 /etc 아래에 있는 컨텐츠의 큰 하위 세트가 저장소의 다른 폴더에 복제됩니다. 이러한 새 위치는 컨텐츠를 참조하는 기본 위치입니다. 그러나 AEM 6.5 업그레이드는 /etc 폴더의 이전 위치와 역호환되도록 모든 시도가 수행되었으므로 대부분의 경우 변경 사항이 적극적으로 또는 수동으로 고객 애플리케이션에서 수행될 때까지 이전 위치가 AEM 코드로 계속 참조됩니다. 타임라인 관점에서는 두 가지 변경 사항이 있습니다.

* 6.5 업그레이드 포함 - 일부 /etc 재구성 변경 사항은 역호환하지 않으므로 AEM 6.5 업그레이드의 일부로 수정 사항을 계획하고 구현해야 합니다.
* 향후 업그레이드 전 - 향후 업그레이드 후 어느 시점까지 /etc 재구성 변경 사항의 상당 부분을 유예할 수 있습니다. 앞서 언급했듯이 AEM 6.5 코드는 수정 사항이 고객 릴리스의 일부로 구현될 때까지 이전 위치를 계속 참조합니다. 변경 작업을 수행해야 하는 강제된 타임라인이 없지만 향후 기능이 참조되는 새 위치에 의존할 수 있으므로 향후 업그레이드 전에 수행하는 것이 좋습니다. 또한 지정된 기능에 대한 설명서는 새 위치를 참조하므로 이전 위치를 계속 사용하고 있는 경우 혼란을 일으킬 수 있습니다.

### 구조 조정 지침 {#restructuring-guidance}

AEM 6.5로의 업그레이드를 계획하는 동안 작업 노력을 평가하려면 다음 솔루션별 페이지를 참조해야 합니다.

* [모든 AEM 솔루션에 공통으로 적용되는 저장소 재구성](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md)
* [AEM Sites 리포지토리 재조정](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md)
* [AEM Assets 리포지토리 재구성](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md)
* [AEM Assets Dynamic Media 리포지토리 재구성](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md)
* [AEM Forms 리포지토리 재구성](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md)
* [AEM Communities 리포지토리 재구성](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md)
* [AEM Commerce 리포지토리 재구성](/help/sites-deploying/ecommerce-repository-restructuring-in-aem-6-5.md)

각 페이지에는 필요한 변경 사항의 긴급성에 해당하는 두 개의 섹션이 있습니다. &quot;6.5 업그레이드 포함&quot; 섹션의 내용은 AEM 6.5 업그레이드 프로젝트의 일부로 다루어져야 합니다. &quot;향후 업그레이드 전&quot; 아래의 모든 내용은 업그레이드 후 때까지 선택적으로 연기될 수 있습니다.

페이지의 각 항목에는 &quot;구조 조정 지침&quot; 필드가 포함되어 있습니다. 이 필드에는 새 위치가 이전에 /etc 폴더 아래에 있는 컨텐츠에 대해 참조되도록 새 6.5 저장소 모델과 정렬하기 위한 권장 기술 전략이 자세히 설명되어 있습니다. 추가 &quot;메모&quot; 필드는 추가적인 유용한 컨텍스트를 제공합니다.
