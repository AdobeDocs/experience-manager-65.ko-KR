---
title: Commerce integration framework을 사용한 AEM 및 타사 Commerce 통합
description: 기업 비즈니스의 매장 환경을 향상하기 위해 추가 타사 상거래 솔루션이 필요할 수 있습니다. 이러한 통합 시나리오에서는 Commerce integration framework(CIF)를 사용하여 I/O Runtime을 사용하여 서드파티 상거래 솔루션을 Adobe Experience Manager에 연결할 수 있습니다.
thumbnail: cif-third-party-architecture.jpg
exl-id: e99899a4-df86-4108-991a-8b30d303a279
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 0%

---

# Commerce integration framework을 사용한 AEM 및 타사 Commerce 통합 {#aem-third-party}

비 Adobe Commerce 솔루션 통합은 CIF의 일반적인 시나리오입니다. 다른 API 및 스키마를 사용하는 서드파티 솔루션은 통합 계층을 통해 연결됩니다.

## 아키텍처 {#architecture}

전반적인 아키텍처는 다음과 같습니다.

![AEM Magento/타사 아키텍처 개요](../assets//AEM_nonMagento_Architecture.png)

이 통합 레이어의 목적은 타사 API 및 스키마를 지원되는 Adobe Commerce GraphQL API 및 Experience Manager 외부의 스키마에 매핑하는 것입니다. 이러한 캡슐화 덕분에 Experience Manager 내의 코드를 변경하지 않고도 통합 논리 및 시스템을 업데이트할 수 있습니다.

## 통합을 위한 솔루션 요구 사항

Experience Manager이 데이터를 온디맨드로 검색하므로 제품 카탈로그에 대한 실시간 API가 필요합니다.

>[!TIP]
>
>사용 가능한 실시간 API가 없는 경우 API가 있는 외부 제품 캐시를 사용하여 통합해야 합니다. 예제 [Magento 오픈 소스](https://business.adobe.com/kr/products/magento/open-source.html).

원하는 사용 사례를 활성화하기 위해 전체 GraphQL 스키마를 구현할 필요가 없이 스키마 객체만 구현합니다.

## 백엔드 사용 사례

CIF은 실시간 제품 카탈로그 액세스 및 제품 경험 관리 도구를 통해 Experience Manager을 확장합니다. 이 매끄러운 통합을 통해 작성자가 콘텐츠 컨텍스트를 종료하지 않고 필요할 때마다 임베드된 UI를 사용하여 상거래 데이터에 액세스할 수 있습니다.

이러한 사용 사례를 잠금 해제하려면 제품 카탈로그 API의 통합이 필요합니다.

## 프론트엔드 사용 사례

[AEM CIF 핵심 구성 요소](https://github.com/adobe/aem-core-cif-components) CIF에서 지원하는 Adobe Commerce API를 통해 데이터를 검색하고 교환합니다. 구성 요소를 재사용하려면 해당 API를 구현해야 합니다.

성능에 중요한 클라이언트측 구성 요소에 대한 권장 사항은 지연을 방지하기 위해 서드파티 솔루션과 직접 통신하는 것입니다.

## 통합 개발 {#develop-integration}

Adobe은 통합 레이어에 [Adobe I/O Runtime](https://developer.adobe.com/apis/experienceplatform/runtime.html)을(를) 사용하는 것을 권장합니다. 타사 CIF 추가 기능에 포함되어 있습니다. 마이크로서비스와 유사한 접근 방식으로 작동하므로 쉽게 여러 솔루션을 통합하는 것이 적합합니다.

[참조 구현](https://github.com/adobe/commerce-cif-graphql-integration-reference)은(는) 상거래 솔루션에 대한 통합을 빌드하기 위한 좋은 시작점입니다. GraphQL을 지원하지만 REST와 같은 다른 유형의 API와도 통합할 수 있습니다.

타사 계층(예: Mulesoft)을 사용할 수 있거나 통합이 타사 솔루션 위에 구축된 경우에는 이 통합 계층이 필요하지 않습니다.

## 사전 빌드된 커넥터 {#connectors}

커넥터는 프로젝트를 잘 시작할 수 있도록 도와줍니다. 상거래 솔루션별 연결 및 기본 API 매핑이 함께 제공됩니다. 이러한 커넥터는 타사에서 빌드하며 Adobe에서 유지 관리하지 않습니다. 자세한 내용은 해당 파트너에게 문의하십시오.

* [SAP Commerce](https://github.com/diconium/commerce-cif-graphql-integration-hybris), Diconium에서 작성
* [Commercetools](https://github.com/diconium/commerce-cif-graphql-integration-commercetool), Diconium에서 작성

>[!TIP]
>
>커넥터는 프로젝트에서 상거래 통합을 가속화하는 데 도움이 되지만 플러그 인 플레이는 아닙니다. 엔터프라이즈 상거래 솔루션은 사용자 지정이 매우 까다로우며 사용자 정의 통합이 필요합니다. 상거래 플랫폼, Adobe Commerce GraphQL 스키마 및 Adobe I/O Runtime에 대한 올바른 지식이 필요합니다.
