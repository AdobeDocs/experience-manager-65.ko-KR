---
title: Commerce Integration Framework를 사용하여 AEM 및 타사 상거래 통합
description: 엔터프라이즈 기업은 상점 전원을 공급하기 위해 추가 타사 상거래 솔루션을 필요로 할 수 있습니다. 이러한 통합 시나리오에서 CIF(Commerce Integration Framework)를 사용하여 I/O Runtime을 사용하여 타사 상거래 솔루션을 Adobe Experience Manager에 연결할 수 있습니다.
thumbnail: cif-third-party-architecture.jpg
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 1%

---

# 전자 상거래 통합 프레임워크를 사용하여 AEM 및 타사 상거래 통합 {#aem-third-party}

비Adobe Commerce 솔루션의 통합은 CIF를 위한 일반적인 시나리오입니다. 다양한 API 및 스키마를 사용하는 타사 솔루션은 통합 레이어를 통해 연결됩니다.

## 아키텍처 {#architecture}

전체 아키텍처는 다음과 같습니다.

![AEM 비 Magento/타사 아키텍처 개요](../assets//AEM_nonMagento_Architecture.png)

이 통합 레이어의 목적은 지원되는 Adobe Commerce GraphQL API 및 스키마를 Experience Manager 외부에 매핑하는 것입니다. 이 캡슐화 덕분에 Experience Manager 내의 코드를 변경하지 않고도 통합 논리 및 시스템을 업데이트할 수 있습니다.

## 통합을 위한 솔루션 요구 사항

Experience Manager이 데이터를 온디맨드로 검색하므로 제품 카탈로그에 대한 실시간 API가 필요합니다.

>[!TIP]
>
>실시간 API를 사용할 수 없는 경우 통합에 API가 있는 외부 제품 캐시를 사용해야 합니다. 예 [Magento open-source](https://magento.com/products/magento-open-source).

원하는 사용 사례를 활성화하기 위해 전체 GraphQL 스키마를 구현할 필요가 없으며 스키마 객체만 구현할 수 있습니다.

## 백엔드 사용 사례

CIF는 실시간 제품 카탈로그 액세스 및 제품 경험 관리 도구를 사용하여 Experience Manager을 확장합니다. 이 원활한 통합을 통해 작성자는 컨텐츠 컨텍스트를 종료하지 않고 필요할 때마다 포함된 UI를 사용하여 상거래 데이터에 액세스할 수 있습니다.

제품 카탈로그 API를 통합하여 이러한 사용 사례를 잠금 해제해야 합니다.

## 프런트 엔드 사용 사례

[AEM CIF 코어 ](https://github.com/adobe/aem-core-cif-components) 구성 요소CIF 지원 Adobe Commerce API를 통해 데이터를 검색하고 교환합니다. 구성 요소를 다시 사용하려면 각 API를 구현해야 합니다.

성능 중요한 클라이언트측 구성 요소에 대한 권장 사항은 지연을 방지하기 위해 타사 솔루션과 직접 통신하는 것입니다.

## 통합 개발 {#develop-integration}

통합 레이어에 [Adobe I/O Runtime](https://www.adobe.io/apis/experienceplatform/runtime.html)을 사용하는 것이 좋습니다. 타사의 CIF 추가 기능에 포함되어 있습니다. 마이크로 서비스와 같은 접근 방식으로 작동하므로 여러 솔루션을 쉽게 통합하는 것이 적합합니다.

[참조 구현](https://github.com/adobe/commerce-cif-graphql-integration-reference)은 상거래 솔루션에 대한 통합을 구축하는 좋은 시작점입니다. GraphQL을 지원하지만 REST 등 다른 유형의 API와 통합할 수도 있습니다.

타사 계층(예: Mulesoft)을 사용할 수 있거나 통합 이 타사 솔루션을 기반으로 구축된 경우에는 이 통합 레이어가 필요하지 않습니다.
