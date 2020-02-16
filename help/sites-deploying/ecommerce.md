---
title: 전자 상거래 개요
seo-title: 전자 상거래 개요
description: AEM 일반 eCommerce는 표준 설치의 일부로 사용할 수 있으며 eCommerce 프레임워크의 전체 기능을 제공합니다.
seo-description: AEM 일반 eCommerce는 표준 설치의 일부로 사용할 수 있으며 eCommerce 프레임워크의 전체 기능을 제공합니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: e-commerce
content-type: reference
docset: aem65
translation-type: tm+mt
source-git-commit: 5d46836a8b7b66daa8f27bc6fad14319ab1f58a7

---


# 전자 상거래 개요{#ecommerce-overview}

AEM 일반 eCommerce는 표준 설치의 일부로 사용할 수 있으며 eCommerce 프레임워크의 전체 기능을 제공합니다.

Adobe는 두 가지 버전의 Commerce Integration Framework를 제공합니다.

|  | CIF on-prem | CIF Cloud |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| 지원되는 AEM 버전 | AEM on-prem 또는 AMS 6.x | AEM AMS 6.4 및 6.5 |
| 백엔드 | - AEM, Java <br> - 모놀리식 통합, 사전 빌드 매핑(템플릿)<br> - JCR 리포지토리 | - Magento <br>- Java 및 Javascript <br>- JCR 저장소에 저장된 상거래 데이터 없음 |
| 프런트 엔드 | AEM 서버측에서 렌더링된 페이지 | 혼합 페이지 애플리케이션(혼합 렌더링) |
| 제품 카탈로그 | - AEM에서 제품 가져오기, 편집기, 캐싱 <br>- AEM 또는 프록시 페이지가 있는 일반 카탈로그 | - 제품 가져오기 없음 <br>- 일반 템플릿 <br>- 커넥터를 통한 주문형 데이터 |
| 확장성 | - 최대 수백만 개의 제품(사용 사례에 따라 다름) 지원 - Dispatcher에서 <br> 캐싱 | - 볼륨 제한 없음 <br>- Dispatcher 또는 CDN에서 캐싱 |
| 표준화된 데이터 모델 | 아니오 | 예, Magento GraphQL 스키마 |
| 사용 가능 | <br> 예:- SAP Commerce Cloud(AEM 6.4 및 Hybris 5(기본값)를 지원하도록 확장 업데이트 및 Hybris 4 <br>- Salesforce Commerce Cloud(AEM 6.4를 지원하기 위한 커넥터 오픈 소스) | 예. GitHub를 통해 오픈 소스를 통해 가능합니다. <br> Magento Commerce(Magento 2.3.2(기본값) 지원 및 Magento 2.3.1과 호환 가능) |
| 사용 시기 | 제한된 사용 사례:작은 정적 카탈로그를 가져와야 하는 경우 | 대부분의 사용 사례에서 선호하는 솔루션 |


## 기타 구현 배포 {#deploying-other-implementations}

AEM 및 Magento의 경우 [Commerce Integration](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html#!AdobeDocs/commerce-cif-documentation/master/integrations/02-AEM-Magento.md) Framework를 사용한 AEM 및 [Magento 통합을 참조하십시오](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html).

>[!NOTE]
>
>eCommerce 구현 및 관리에 대한 자세한 내용은 eCommerce [관리를 참조하십시오](/help/sites-administering/ecommerce.md).
>
>전자 상거래 기능 확장에 대한 자세한 내용은 전자 상거래 [개발을 참조하십시오](/help/sites-developing/ecommerce.md).

