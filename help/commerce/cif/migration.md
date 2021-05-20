---
title: AEM CIF(Commerce Integration Framework) 추가 기능으로 마이그레이션
description: 이전 버전에서 CIF(AEM Commerce Integration Framework) 추가 기능으로 마이그레이션하는 방법
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 4%

---

# Experience Manager 추가 기능에 대한 마이그레이션 안내서 {#cif-migration}

이 안내서는 Experience Manager 추가 기능 마이그레이션에 대해 업데이트해야 하는 영역을 식별하는 데 도움이 됩니다.

## CIF 추가 기능

CIF 추가 기능은 [소프트웨어 배포 포털](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)을 통해 AEM 6.5에 사용할 수 있습니다. 호환되며 Cloud Service으로 Experience Manager에 대한 CIF 추가 기능과 동일한 기능을 제공합니다.

[AEM Content and Commerce](getting-started.md) 시작 을 참조하십시오.

CIF 배포를 지원하기 위해 Adobe은 [AEM CIF 코어 구성 요소](https://github.com/adobe/aem-core-cif-components)를 제공합니다.

## 제품 카탈로그

CIF 추가 기능에서는 제품 카탈로그 데이터를 가져올 수 없습니다. CIF 추가 기능 주도자를 사용하는 제품 및 카탈로그 요청은 외부 상거래 솔루션에 대한 실시간 호출을 통해 온디맨드 상태입니다. 전자 상거래 솔루션 통합에 대한 자세한 내용을 보려면 통합 장으로 이동하십시오.

>[!TIP]
>
>실시간 API를 사용할 수 없는 경우 통합에 API가 있는 외부 제품 캐시를 사용해야 합니다. 예 [Magento open-source](https://magento.com/products/magento-open-source).

## AEM 렌더링을 사용한 제품 카탈로그 경험

클래식 CIF에서 카탈로그 블루프린트를 사용하는 경우 제품 카탈로그 워크플로우를 업데이트해야 합니다. 이제 CIF 추가 기능이 AEM 카탈로그 템플릿을 사용하여 제품 카탈로그 경험을 즉시 렌더링합니다. 더 이상 제품 데이터 또는 제품 페이지를 복제할 필요가 없습니다.

## 캐시할 수 없는 데이터 및 쇼핑 상호 작용

캐시할 수 없는 데이터 및 상호 작용(예: 장바구니에 추가, 검색)에 대한 클라이언트측 요청은 CDN/Dispatcher를 통해 상거래 종단점(상거래 솔루션 또는 통합 계층)으로 직접 이동해야 합니다. AEM이 단지 프록시였던 모든 호출을 제거합니다.
