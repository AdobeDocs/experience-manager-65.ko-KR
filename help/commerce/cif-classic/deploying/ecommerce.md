---
title: eCommerce 개요
seo-title: eCommerce Overview
description: AEM 일반 eCommerce는 표준 설치의 일부로 사용할 수 있으며 eCommerce 프레임워크의 전체 기능을 제공합니다.
seo-description: AEM generic eCommerce is available as part of the standard installation and provides you with the full functionality of the eCommerce framework.
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
docset: aem65
feature: Commerce Integration Framework
exl-id: 3567bd28-73aa-401a-8aa9-a62a99d2a613
source-git-commit: a467009851937c4a10b165a3d253c47bf990bbc5
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 3%

---

# eCommerce 개요{#ecommerce-overview}

AEM 일반 eCommerce는 표준 설치의 일부로 사용할 수 있으며 eCommerce 프레임워크의 전체 기능을 제공합니다.

Adobe은 두 가지 버전의 Commerce Integration Framework를 제공합니다.

|  | CIF on-prem | CIF Cloud |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| 지원되는 AEM 버전 | AEM on-prem 또는 AMS 6.x | AEM AMS 6.4 및 6.5 |
| 백엔드 | - AEM, Java <br> - 단일 통합, 빌드 전 매핑(템플릿)<br> - JCR 저장소 | - Adobe Commerce <br>- Java 및 Javascript <br>- JCR 저장소에 저장된 상거래 데이터가 없습니다 |
| 프런트엔드 | AEM 서버측 렌더링 페이지 | 혼합 페이지 애플리케이션(하이브리드 렌더링) |
| 제품 카탈로그 | - AEM에서 제품 가져오기, 편집기, 캐싱 <br>- AEM 또는 프록시 페이지를 사용하는 일반 카탈로그 | - 제품 가져오기 없음 <br>- 일반 템플릿 <br>- 커넥터를 통한 온디맨드 데이터 |
| 확장성 | - 최대 수백만 개의 제품을 지원할 수 있습니다(사용 사례에 따라 다름). <br> - Dispatcher에서 캐싱 | - 볼륨 제한 없음 <br>- Dispatcher 또는 CDN에 캐싱 |
| 표준화된 데이터 모델 | 아니요 | 예, Adobe Commerce GraphQL 스키마 |
| 사용 가능 | 예:<br> - SAP Commerce Cloud(AEM 6.4 및 Hybris 5(기본값)를 지원하도록 업데이트되고 Hybris 4와의 호환성을 유지합니다. <br>- Salesforce Commerce Cloud(AEM 6.4를 지원하도록 커넥터가 열려 있음) | GitHub를 통해 오픈 소스를 통해 지원. <br> Adobe Commerce(2.3.2(기본값)를 지원하고 2.3.1과 호환됩니다.) |
| 사용 시기 | 제한된 사용 사례: 작은 정적 카탈로그를 가져와야 하는 시나리오의 경우 | 대부분의 사용 사례에서 선호하는 솔루션 |


## 다른 구현 배포 {#deploying-other-implementations}

AEM 및 Adobe Commerce의 경우 다음을 참조하십시오. [AEM 및 Adobe Commerce 통합](/help/commerce/cif/integrating/magento.md) 사용 [전자 상거래 통합 프레임워크](/help/commerce/cif/introduction.md).

>[!NOTE]
>
>개념 및 eCommerce 구현 관리에 대한 자세한 내용은 [eCommerce 관리](/help/commerce/cif-classic/administering/ecommerce.md).
>
>eCommerce 기능 확장에 대한 자세한 내용은 [eCommerce 개발](/help/commerce/cif-classic/developing/ecommerce.md).
