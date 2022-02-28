---
title: Commerce Integration Framework를 사용하여 AEM 및 타사 상거래 통합
description: 엔터프라이즈 기업은 상점 전원을 공급하기 위해 추가 타사 상거래 솔루션을 필요로 할 수 있습니다. 이러한 통합 시나리오에서 CIF(Commerce Integration Framework)를 사용하여 I/O Runtime을 사용하여 타사 상거래 솔루션을 Adobe Experience Manager에 연결할 수 있습니다.
thumbnail: cif-third-party-architecture.jpg
exl-id: e99899a4-df86-4108-991a-8b30d303a279
source-git-commit: 885d0763fca9ad4eab499081adca9b83875b27e1
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# Commerce Integration Framework를 사용하여 AEM 및 타사 상거래 통합 {#aem-third-party}

비Adobe Commerce 솔루션의 통합은 CIF에 대한 일반적인 시나리오입니다. 다양한 API 및 스키마를 사용하는 타사 솔루션은 통합 레이어를 통해 연결됩니다.

## 아키텍처 {#architecture}

전체 아키텍처는 다음과 같습니다.

![AEM 비 Magento/타사 아키텍처 개요](../assets//AEM_nonMagento_Architecture.png)

이 통합 레이어의 목적은 지원되는 Adobe Commerce GraphQL API 및 스키마를 Experience Manager 외부에 매핑하는 것입니다. 이 캡슐화 덕분에 Experience Manager 내의 코드를 변경하지 않고도 통합 논리 및 시스템을 업데이트할 수 있습니다.

## 통합을 위한 솔루션 요구 사항

Experience Manager이 데이터를 온디맨드로 검색하므로 제품 카탈로그에 대한 실시간 API가 필요합니다.

>[!TIP]
>
>실시간 API를 사용할 수 없는 경우 통합에 API가 있는 외부 제품 캐시를 사용해야 합니다. 예 [Magento 오픈 소스](https://business.adobe.com/products/magento/open-source.html).

원하는 사용 사례를 활성화하기 위해 전체 GraphQL 스키마를 구현할 필요가 없으며 스키마 객체만 구현할 수 있습니다.

## 백엔드 사용 사례

CIF는 실시간 제품 카탈로그 액세스 및 제품 경험 관리 도구를 사용하여 Experience Manager을 확장합니다. 이 원활한 통합을 통해 작성자는 컨텐츠 컨텍스트를 종료하지 않고 필요할 때마다 포함된 UI를 사용하여 상거래 데이터에 액세스할 수 있습니다.

제품 카탈로그 API를 통합하여 이러한 사용 사례를 잠금 해제해야 합니다.

## 프런트 엔드 사용 사례

[AEM CIF 코어 구성 요소](https://github.com/adobe/aem-core-cif-components) cif 지원 Adobe Commerce API를 통해 데이터를 검색하고 교환합니다. 구성 요소를 다시 사용하려면 각 API를 구현해야 합니다.

성능 중요한 클라이언트측 구성 요소에 대한 권장 사항은 지연을 방지하기 위해 타사 솔루션과 직접 통신하는 것입니다.

## 통합 개발 {#develop-integration}

을 사용하는 것이 좋습니다 [Adobe I/O Runtime](https://www.adobe.io/apis/experienceplatform/runtime.html) 통합 레이어의 경우 타사의 CIF 추가 기능에 포함되어 있습니다. 마이크로 서비스와 같은 접근 방식으로 작동하므로 여러 솔루션을 쉽게 통합하는 것이 적합합니다.

다음 [참조 구현](https://github.com/adobe/commerce-cif-graphql-integration-reference) 는 상거래 솔루션에 대한 통합을 구축하는 중요한 시작점입니다. GraphQL을 지원하지만 REST 등 다른 유형의 API와 통합할 수도 있습니다.

타사 계층(예: Mulesoft)을 사용할 수 있거나 통합 이 타사 솔루션을 기반으로 구축된 경우에는 이 통합 레이어가 필요하지 않습니다.

## 사전 설치된 커넥터 {#connectors}

커넥터는 프로젝트에 좋은 시작을 제공합니다. 여기에는 상거래 솔루션별 연결 및 기본 API 매핑이 제공됩니다. 이러한 커넥터는 Adobe에 의해 유지 관리되지 않고 타사에 의해 구축됩니다. 자세한 내용은 해당 파트너에게 문의하십시오.

* [SAP Commerce](https://github.com/diconium/commerce-cif-graphql-integration-hybris)사전 설정된
* [상거래 도구](https://github.com/diconium/commerce-cif-graphql-integration-commercetool)사전 설정된

>[!TIP]
>
>커넥터는 커머스 통합을 가속화하기 위해 프로젝트를 지원하지만 플러그인은 아닙니다. 엔터프라이즈 커머스 솔루션은 일반적으로 사용자 지정 수준이 높으며 사용자 지정 통합이 필요합니다. 상거래 플랫폼, Adobe Commerce GraphQL 스키마 및 Adobe I/O Runtime에 대한 올바른 지식이 필요합니다.
