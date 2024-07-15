---
title: eCommerce 개요
description: AEM 일반 eCommerce는 표준 설치의 일부로 사용할 수 있으며 eCommerce 프레임워크의 전체 기능을 제공합니다.
feature: Commerce Integration Framework
exl-id: 3567bd28-73aa-401a-8aa9-a62a99d2a613
solution: Experience Manager,Commerce
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 2%

---

# eCommerce 개요{#ecommerce-overview}

AEM 일반 eCommerce는 표준 설치의 일부로 사용할 수 있으며 eCommerce 프레임워크의 전체 기능을 제공합니다.

Adobe은 두 가지 버전의 Commerce integration framework을 제공합니다.

|                         | CIF 온-프레미스 | CIF Cloud |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| 지원되는 AEM 버전 | AEM 온-프레미스 또는 AMS 6.x | AEM AMS 6.4 및 6.5 |
| 백엔드 | - AEM, Java™ <br> - Monolithic 통합, 빌드 전 매핑(템플릿)<br> - JCR 저장소 | - Adobe Commerce <br>- Java 및 JavaScript <br>- JCR 저장소에 저장된 Commerce 데이터가 없음 |
| 프론트엔드 | AEM 서버측 렌더링 페이지 | 혼합 페이지 애플리케이션(하이브리드 렌더링) |
| 제품 카탈로그 | - AEM <br>의 제품 가져오기, 편집기, 캐싱 - AEM 또는 프록시 페이지를 포함하는 일반 카탈로그 | - 제품 가져오기 없음 <br>- 일반 템플릿 <br>- 커넥터를 통한 온디맨드 데이터 |
| 확장성 | - 최대 몇 백만 개의 제품을 지원할 수 있음(사용 사례에 따라 다름) <br> - Dispatcher에서 캐싱 | - 볼륨 제한 없음 <br>- Dispatcher 또는 CDN에서 캐싱 |
| 표준화된 데이터 모델 | 아니요 | 예, Adobe Commerce GraphQL 스키마 |
| 사용 가능 | 예:<br> - SAP Commerce Cloud(AEM 6.4 및 Hybris 5(기본값)를 지원하도록 확장이 업데이트되었으며 Hybris 4 <br>- Salesforce Commerce Cloud(AEM 6.4를 지원하도록 오픈 소스로 제공되는 커넥터)와의 호환성을 유지합니다. | GitHub를 통해 오픈 소스를 통해 지원. <br> Adobe Commerce(2.3.2(기본값)를 지원하고 2.3.1과 호환) |
| 사용 시기 | 제한된 사용 사례: 작은 시나리오의 경우 필요에 따라 정적 카탈로그를 가져옵니다. | 대부분의 사용 사례에서 선호하는 솔루션 |


## 다른 구현 배포 {#deploying-other-implementations}

AEM 및 Adobe Commerce의 경우 [Commerce integration framework](/help/commerce/cif/introduction.md)을(를) 사용하여 [AEM 및 Adobe Commerce 통합](/help/commerce/cif/integrating/magento.md)을 참조하십시오.

>[!NOTE]
>
>eCommerce 구현 개념 및 관리에 대한 자세한 내용은 [eCommerce 관리](/help/commerce/cif-classic/administering/ecommerce.md)를 참조하십시오.
>
>전자 상거래 기능 확장에 대한 자세한 내용은 [전자 상거래 개발](/help/commerce/cif-classic/developing/ecommerce.md)을 참조하십시오.
