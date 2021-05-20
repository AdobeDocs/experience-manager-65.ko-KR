---
title: AEM Content and Commerce 시작하기
description: AEM Content and Commerce 프로젝트를 배포하는 방법을 알아봅니다.
topics: Commerce
feature: 전자 상거래 통합 프레임워크
thumbnail: 37843.jpg
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 5%

---

# AEM Content and Commerce 시작하기 {#start}

AEM Content and Commerce를 시작하려면 AEM 6.5용 AEM Content and Commerce Add-On을 설치해야 합니다.

## 최소 소프트웨어 요구 사항

[AEM 6.5 서비스 팩 ](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)  7 이상이 필요합니다.

## 온보딩 {#onboarding}

AEM Content and Commerce에 대한 온보딩은 두 단계로 구성됩니다.

1. AEM 6.5용 AEM 컨텐츠 및 Commerce 추가 기능 설치

2. 전자 상거래 솔루션과 AEM 연결

### AEM 6.5용 AEM 컨텐츠 및 Commerce 추가 기능 설치 {#install-add-on}

[소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) 포털에서 AEM 6.5용 AEM Commerce 추가 기능을 다운로드하여 설치합니다.

필요한 AEM 6.5 서비스 팩을 시작하고 설치합니다. 사용 가능한 마지막 서비스 팩을 설치하는 것이 좋습니다.

>[!NOTE]
>
>이 작업은 AEM Managed Service용 CSE에서 수행합니다.

### 전자 상거래 시스템에 AEM 연결 {#connect}

AEM은 AEM용 GraphQL 엔드포인트가 있는 모든 상거래 시스템에 연결할 수 있습니다. 이러한 종단점은 일반적으로 공개적으로 사용할 수 있거나 개별 프로젝트 설정에 따라 개인 VPN 또는 로컬 연결을 통해 연결할 수 있습니다.

선택적으로 인증을 필요로 하는 추가 CIF 기능을 사용하기 위해 인증 헤더를 제공할 수 있습니다.

[AEM Project Archetype](https://github.com/adobe/aem-project-archetype)에서 생성된 프로젝트와 [기본 구성](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json)에 이미 포함된 [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)를 조정해야 합니다.

`com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json`에 있는 `url` 값을 상거래 시스템의 GraphQL 종단점으로 바꿉니다. 이 구성은 OSGI 콘솔을 통해 또는 프로젝트를 통해 OSGI 구성을 배포하여 수행할 수 있습니다. 스테이징 및 프로덕션 시스템에 대한 다양한 구성은 다른 AEM 실행 모드를 사용하여 지원됩니다.

AEM Content and Commerce Add-On 및 CIF 핵심 구성 요소는 AEM 서버측 및 클라이언트측 연결을 모두 사용합니다. 클라이언트측 CIF 코어 구성 요소 및 CIF 추가 기능 작성 도구는 기본적으로 `/api/graphql`에 연결됩니다. 필요한 경우 CIF Cloud Service 구성을 통해 이 문제를 조정할 수 있습니다(아래 참조).

CIF 추가 기능은 [로컬 개발](develop.md)에 선택적으로 사용할 수 있는 `/api/graphql`에 GraphQL 프록시 서블릿을 제공합니다. 프로덕션 배포의 경우 AEM Dispatcher를 통해 또는 다른 네트워크 계층(예: CDN)에서 상거래 GraphQL 종단점에 역방향 프록시를 설정하는 것이 좋습니다.

## 저장소 및 카탈로그 구성 {#catalog}

추가 기능 및 [CIF 코어 구성 요소](https://github.com/adobe/aem-core-cif-components)는 다른 상거래 저장소에 연결된 여러 AEM 사이트 구조(또는 스토어 보기 등)에서 사용할 수 있습니다. 기본적으로 CIF 추가 기능이 Adobe Commerce의 기본 저장소 및 카탈로그(Magento)에 연결하는 기본 구성과 함께 배포됩니다.

이 구성은 다음 단계에 따라 CIF Cloud Service 구성을 통해 프로젝트에 대해 조정할 수 있습니다.

1. AEM에서 도구 -> Cloud Services -> CIF 구성으로 이동합니다.

2. 변경할 상거래 구성을 선택합니다

3. 작업 표시줄을 통해 구성 속성을 엽니다

![CIF Cloud Services 구성](/help/commerce/cif/assets/cif-cloud-service-config.png)

다음 속성을 구성할 수 있습니다.

- GraphQL 클라이언트 - 상거래 백엔드 통신을 위해 구성된 GraphQL 클라이언트를 선택합니다. 이 기능은 일반적으로 기본적으로 유지됩니다.
- 저장소 보기 - (Magento) 저장소 보기 식별자입니다. 비어 있으면 기본 저장소 보기가 사용됩니다.
- GraphQL 프록시 경로 - AEM의 URL 경로 GraphQL 프록시가 상거래 백엔드 GraphQL 끝점에 요청을 프록시할 때 사용합니다.
   >[!NOTE]
   >
   > 대부분의 설정에서 기본값 `/api/graphql`은 변경할 수 없습니다. 제공된 GraphQL 프록시를 사용하지 않는 고급 설정만 이 설정을 변경해야 합니다.
- 카탈로그 UID 지원 활성화 - 상거래 백엔드 GraphQL 호출에서 ID 대신 UID에 대한 지원을 활성화합니다.
   >[!NOTE]
   >
   > UID에 대한 지원이 Adobe Commerce(Magento) 2.4.2에서 도입되었습니다. 상거래 백엔드가 버전 2.4.2 이상의 GraphQL 스키마를 지원하는 경우에만 활성화하십시오.
- 카탈로그 루트 카테고리 식별자 - 저장소 카탈로그 루트의 식별자(UID 또는 ID)입니다

위에 표시된 구성은 참조용입니다. 프로젝트는 자체 구성을 제공해야 합니다.

다른 전자 상거래 카탈로그와 결합된 여러 AEM 사이트 구조를 사용하는 보다 복잡한 설정을 알려면 [Commerce Multi-Store Setup](configuring/multi-store-setup.md) 자습서를 참조하십시오.

## 추가 리소스 {#additional-resources}

- [AEM 프로젝트 전형](https://github.com/adobe/aem-project-archetype)
- [AEM Venia 참조 저장소](https://github.com/adobe/aem-cif-guides-venia)
- [상거래 다중 스토어 설정](configuring/multi-store-setup.md)
