---
title: Commerce Integration Framework를 사용한 AEM 및 제3자 상거래 통합
description: 기업 기업은 스토어를 가동하기 위해 제3자 상거래 솔루션을 추가로 요구할 수 있습니다. 이러한 통합 시나리오에서 CIF(Commerce Integration Framework)를 사용하여 I/O 런타임을 사용하여 제3자 상거래 솔루션을 Adobe Experience Manager에 연결할 수 있습니다.
thumbnail: cif-third-party-architecture.jpg
translation-type: tm+mt
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 1%

---

# 상거래 통합 프레임워크를 사용한 AEM 및 제3자 상거래 통합 {#aem-third-party}

비Adobe 상거래 솔루션의 통합은 CIF에 대한 일반적인 시나리오입니다. 서로 다른 API 및 스키마를 사용하는 제3자 솔루션은 통합 레이어를 통해 연결됩니다.

## 아키텍처 {#architecture}

전체 아키텍처는 다음과 같습니다.

![AEM 비 Magento/타사 아키텍처 개요](../assets//AEM_nonMagento_Architecture.png)

이 통합 레이어의 목적은 지원되는 Adobe Commerce GraphQL API 및 Experience Manager 외부에서 스키마를 기준으로 타사 API 및 스키마를 매핑하는 것입니다. 이 캡슐화 덕분에 Experience Manager 내의 코드를 변경하지 않고도 통합 논리 및 시스템을 업데이트할 수 있습니다.

## 통합을 위한 솔루션 요구 사항

Experience Manager은 On-Demand 데이터를 검색하므로 제품 카탈로그에 대한 실시간 API가 필요합니다.

>[!TIP]
>
>실시간 API를 사용할 수 없는 경우 API가 포함된 외부 제품 캐시를 통합에 사용해야 합니다. 예 [Magento open-source](https://magento.com/products/magento-open-source).

전체 GraphQL 스키마를 구현할 필요가 없으며 원하는 사용 사례를 활성화하기 위해 스키마 개체만 구현할 수 있습니다.

## 백엔드 활용 사례

CIF는 실시간 제품 카탈로그 액세스 및 제품 경험 관리 툴을 통해 Experience Manager을 확장합니다. 이러한 매끄러운 통합을 통해 작성자는 컨텐츠 컨텍스트를 종료하지 않고도 필요할 때마다 포함된 UI를 사용하여 상거래 데이터에 액세스할 수 있습니다.

제품 카탈로그 API를 통합하면 이러한 사용 사례를 잠금 해제할 수 있습니다.

## 프런트 엔드 사용 사례

[AEM CIF 핵심 ](https://github.com/adobe/aem-core-cif-components) 구성 요소CIF 지원 Adobe 상거래 API를 통해 데이터를 검색하고 교환할 수 있습니다. 구성 요소를 다시 사용하려면 각 API를 구현해야 합니다.

성능에 중요한 클라이언트측 구성 요소에 대한 권장 사항은 지연을 방지하기 위해 제3자 솔루션과 직접 통신하는 것입니다.

## 통합 {#develop-integration} 개발

통합 레이어에 [Adobe I/O Runtime](https://www.adobe.io/apis/experienceplatform/runtime.html)을 사용하는 것이 좋습니다. 제3자를 위한 CIF 추가 기능에 포함되어 있습니다. 마이크로 서비스와 유사한 접근 방식을 통해 여러 솔루션을 손쉽게 통합할 수 있습니다.

[참조 구현](https://github.com/adobe/commerce-cif-graphql-integration-reference)은 상거래 솔루션에 대한 통합을 구축할 수 있는 좋은 시작점입니다. GraphQL을 지원하지만 REST와 같은 다른 유형의 API와 통합할 수도 있습니다.

제3자 레이어를 사용할 수 있거나(예: Mulesoft) 제3자 솔루션을 기반으로 통합을 만든 경우에는 이 통합 레이어가 필요하지 않습니다.
