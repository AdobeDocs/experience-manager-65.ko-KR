---
title: AEM CIF(Commerce Integration Framework) Add-on으로의 마이그레이션
description: 이전 버전에서 AEM CIF(Commerce Integration Framework) Add-On으로 마이그레이션하는 방법
translation-type: tm+mt
source-git-commit: d92a635d41cf1b14e109c316bd7264cf7d45a9fe
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 4%

---

# Experience Manager 추가 기능에 대한 마이그레이션 안내서 {#cif-migration}

이 안내서는 Experience Manager 추가 기능 마이그레이션을 위해 업데이트해야 하는 영역을 식별하는 데 도움이 됩니다.

## CIF 추가 기능

CIF Add-on은 [소프트웨어 배포 포털](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)을 통해 AEM 6.5에서 사용할 수 있습니다. 호환 가능하고 Cloud Service용 CIF 추가 기능과 동일한 기능을 제공합니다.

[AEM 컨텐트 및 상거래 시작](getting-started.md)을 참조하십시오.

CIF Adobe 배포 프로젝트를 지원하려면 [AEM CIF 핵심 구성 요소](https://github.com/adobe/aem-core-cif-components)를 제공합니다.

## 제품 카탈로그

CIF Add-On에서는 제품 카탈로그 데이터를 가져올 수 없습니다. CIF Add-on 주도자를 사용하면 제품 및 카탈로그 요청은 외부 상거래 솔루션에 대한 실시간 호출을 통해 on-demand로 수행됩니다. 상거래 솔루션 통합에 대한 자세한 내용은 통합으로 이동합니다.

>[!TIP]
>
>실시간 API를 사용할 수 없는 경우 API가 포함된 외부 제품 캐시를 통합에 사용해야 합니다. 예 [Magento open-source](https://magento.com/products/magento-open-source).

## AEM 렌더링을 통한 제품 카탈로그 경험

Classic CIF에서 카탈로그 블루프린트를 사용하는 경우 제품 카탈로그 워크플로우를 업데이트해야 합니다. 이제 CIF Add-on은 AEM 카탈로그 템플릿을 사용하여 제품 카탈로그 경험을 신속하게 렌더링합니다. 더 이상 제품 데이터 또는 제품 페이지를 복제할 필요가 없습니다.

## 액세스 불가능한 데이터 및 쇼핑 상호 작용

액세스 불가능한 데이터 및 상호 작용(예: 장바구니에 추가, 검색)에 대한 클라이언트측 요청은 CDN/Dispatcher를 통해 상거래 끝점(상거래 솔루션 또는 통합 레이어)으로 바로 이동해야 합니다. AEM이 프록시였던 모든 호출을 제거합니다.
