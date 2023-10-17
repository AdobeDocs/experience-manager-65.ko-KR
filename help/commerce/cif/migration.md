---
title: CIF(AEM Commerce integration framework) 추가 기능으로 마이그레이션
description: 이전 버전에서 AEM Commerce integration framework(CIF) 추가 기능으로 마이그레이션하는 방법.
exl-id: c6c0c2fc-6cfa-4c64-b3d8-7e428b2a4b2e
source-git-commit: eaffc71c23c18d26ec5cbb2bbb7524790c4826fe
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 4%

---

# Experience Manager 추가 기능에 대한 마이그레이션 안내서 {#cif-migration}

이 안내서는 Experience Manager 추가 기능 마이그레이션을 위해 업데이트해야 하는 영역을 식별하는 데 도움이 됩니다.

## CIF 추가 기능

CIF 추가 기능은 를 통해 AEM 6.5에서 사용할 수 있습니다. [소프트웨어 배포 포털](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). 호환되며 Experience Manager as a Cloud Service용 CIF 추가 기능과 동일한 기능을 제공합니다.

다음을 참조하십시오 [AEM Content 및 Commerce 시작하기](getting-started.md).

CIF을 배포하는 프로젝트를 지원하기 위해 Adobe은 [AEM CIF 핵심 구성 요소](https://github.com/adobe/aem-core-cif-components).

## 제품 카탈로그

CIF 추가 기능에서는 제품 카탈로그 데이터 가져오기가 지원되지 않습니다. CIF 추가 기능 주체를 사용하면 외부 상거래 솔루션에 대한 실시간 호출을 통해 제품 및 카탈로그 요청이 온디맨드로 수행됩니다. 상거래 솔루션 통합에 대한 자세한 내용을 보려면 통합 장으로 이동합니다.

>[!TIP]
>
>사용 가능한 실시간 API가 없는 경우 API가 있는 외부 제품 캐시를 사용하여 통합해야 합니다. 예 [Magento 오픈 소스](https://business.adobe.com/products/magento/open-source.html).

## AEM 렌더링을 사용한 제품 카탈로그 경험

클래식 CIF과 함께 카탈로그 블루프린트를 사용하는 경우 제품 카탈로그 워크플로우를 업데이트해야 합니다. 이제 CIF 추가 기능은 AEM 카탈로그 템플릿을 사용하여 제품 카탈로그 경험을 즉시 렌더링합니다. 더 이상 제품 데이터 또는 제품 페이지 복제가 필요하지 않습니다.

## 캐시 불가능 데이터 및 쇼핑 상호 작용

캐시할 수 없는 데이터 및 상호 작용(예: 장바구니에 추가, 검색)에 대한 클라이언트측 요청은 CDN/Dispatcher를 통해 상거래 끝점(상거래 솔루션 또는 통합 계층)으로 직접 이동해야 합니다. AEM이 프록시였던 모든 호출을 제거합니다.
