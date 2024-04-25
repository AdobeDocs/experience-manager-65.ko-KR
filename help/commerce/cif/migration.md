---
title: AEM CIF(Commerce Integration Framework) 추가 기능으로 마이그레이션
description: 이전 버전에서 AEM CIF(Commerce Integration Framework) 추가 기능으로 마이그레이션하는 방법을 알아봅니다.
exl-id: c6c0c2fc-6cfa-4c64-b3d8-7e428b2a4b2e
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# Experience Manager 추가 기능에 대한 마이그레이션 안내서 {#cif-migration}

이 안내서 는 Experience Manager 추가 기능 마이그레이션을 위해 업데이트해야 하는 영역을 식별하는 데 도움이 됩니다.

## CIF 애드온

CIF Add-on은 소프트웨어 배포 포털](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)을 통해 AEM 6.5에 사용할 수 있습니다[. Cloud Service as a Experience Manager 용 CIF 추가 기능과 호환되며 동일한 기능을 제공합니다.

자세한 내용은 AEM 컨텐츠 및 상거래](getting-started.md) 시작하기를 참조하십시오[.

CIF를 배포하는 프로젝트를 지원하기 위해 Adobe Systems에서는 AEM CIF 코어 구성 요소를](https://github.com/adobe/aem-core-cif-components) 제공합니다[.

## 제품 카탈로그

제품 카탈로그 데이터 가져오기는 CIF 추가 기능에서 지원되지 않습니다. CIF 추가 기능 보안 주체를 사용하면 외부 상거래 솔루션에 대한 실시간 호출을 통해 제품 및 카탈로그 요청이 온디맨드로 수행됩니다. 상거래 솔루션 통합에 대해 자세히 알아보려면 통합 장으로 이동하십시오.

>[!TIP]
>
>실시간 API를 사용할 수 없는 경우 API가 있는 외부 제품 캐시를 통합에 사용해야 합니다. 예제 [Magento 오픈 소스](https://business.adobe.com/products/magento/open-source.html).

## AEM 렌더링을 사용한 제품 카탈로그 경험

클래식 CIF와 함께 카탈로그 블루프린트 를 사용하는 경우 제품 카탈로그 작업 과정 을 업데이트해야 합니다. CIF Add-on은 이제 AEM 카탈로그 템플릿을 사용하여 제품 카탈로그 경험을 즉시 렌더링합니다. 더 이상 제품 데이터 또는 제품 페이지를 복제할 필요가 없습니다.

## 캐시할 수 없는 데이터 및 쇼핑 상호 작용

캐시할 수 없는 데이터 및 상호 작용(예: 장바구니에 추가, 검색)에 대한 클라이언트측 요청은 CDN/Dispatcher를 통해 상거래 엔드포인트(상거래 솔루션 또는 통합 계층)로 직접 이동해야 합니다. AEM이 프록시일 뿐인 모든 호출을 제거.
