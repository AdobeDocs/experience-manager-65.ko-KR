---
title: AEM 컨텐츠 및 상거래 시작하기
description: AEM 콘텐츠 및 상거래 프로젝트를 배포하는 방법을 알아봅니다.
topics: Commerce
feature: 전자 상거래 통합 프레임워크
thumbnail: 37843.jpg
translation-type: tm+mt
source-git-commit: 8ead3d1b24177effa4d40141408c5676eaabcc30
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 5%

---

# AEM 콘텐츠 및 상거래 시작하기 {#start}

AEM Content and Commerce를 시작하려면 AEM 6.5용 AEM Content and Commerce Add-On을 설치해야 합니다.

## 최소 소프트웨어 요구 사항

[AEM 6.5 서비스 팩](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) 7 이상이 필요합니다.

## 온보딩 {#onboarding}

AEM 컨텐츠 및 상거래에 대한 온보딩은 2단계 프로세스입니다.

1. AEM 6.5용 AEM Content and Commerce Add-On 설치

2. 상거래 솔루션과 AEM 연결

### AEM 6.5용 AEM Content 및 Commerce Add-on 설치

[소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) 포털에서 AEM 6.5용 AEM Commerce 추가 기능을 다운로드하고 설치합니다.

필요한 AEM 6.5 서비스 팩을 시작하고 설치합니다. 마지막으로 사용 가능한 서비스 팩을 설치하는 것이 좋습니다.

    >[!참고]
    >
    >AEM Managed Service 고객을 위한 CSE에서 수행합니다.

### 전자 상거래 시스템에 AEM 연결

AEM은 액세스 가능한 AEM용 GraphQL 끝점이 있는 모든 상거래 시스템에 연결할 수 있습니다. 이러한 끝점은 일반적으로 공개적으로 사용할 수 있거나 개별 프로젝트 설정에 따라 개인 VPN 또는 로컬 연결을 통해 연결할 수 있습니다.

선택적으로 인증이 필요한 추가 CIF 기능을 사용하기 위해 인증 헤더를 제공할 수 있습니다.

[AEM Project Tranype](https://github.com/adobe/aem-project-archetype)에 의해 생성된 프로젝트와 이미 [기본 구성](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json)에 포함된 [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)에 의해 생성된 프로젝트는 조정되어야 합니다.

`com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json`의 `url` 값을 상거래 시스템의 GraphQL 끝점으로 바꿉니다. 이 구성은 OSGI 콘솔을 통해 하거나 프로젝트를 통해 OSGI 구성을 배포하여 수행할 수 있습니다. 스테이징 및 프로덕션 시스템에 대한 구성은 서로 다른 AEM 실행 모드를 사용하여 지원됩니다.

AEM Content and Commerce Add-On 및 CIF Core Components는 AEM 서버측 및 클라이언트측 연결을 모두 사용합니다. 클라이언트측 CIF 핵심 구성 요소 및 CIF 추가 기능 작성 도구는 기본적으로 `/api/graphql`에 연결됩니다. 필요한 경우 CIF Cloud Service 구성을 통해 조정할 수 있습니다(아래 참조).

CIF Add-on은 `/api/graphql`에 GraphQL 프록시 서블릿을 제공하며, 이 서블릿은 선택적으로 [로컬 개발](develop.md)에 사용할 수 있습니다. 프로덕션 배포의 경우 AEM Dispatcher나 기타 네트워크 레이어(예: CDN)를 통해 커머스 GraphQL 끝점에 역방향 프록시를 설정하는 것이 좋습니다.

## {#catalog} 스토어 및 카탈로그 구성

추가 기능 및 [CIF 핵심 구성 요소](https://github.com/adobe/aem-core-cif-components)는 다른 상거래 스토어에 연결된 여러 AEM 사이트 구조(또는 스토어 보기 등)에서 사용할 수 있습니다. 기본적으로 CIF Add-On은 Adobe Commerce의 기본 스토어 및 카탈로그(Magento)에 연결하는 기본 구성으로 배포됩니다.

이 구성은 다음 단계에 따라 CIF Cloud Service 구성을 통해 프로젝트에 맞게 조정할 수 있습니다.

1. AEM에서 도구 -> Cloud Services -> CIF 구성으로 이동합니다.

2. 변경할 상거래 구성을 선택합니다.

3. 작업 표시줄을 통해 구성 속성 열기

![CIF Cloud Services 구성](/help/commerce/cif/assets/cif-cloud-service-config.png)

다음 속성을 구성할 수 있습니다.

- GraphQL 클라이언트 - 상거래 백엔드 통신을 위해 구성된 GraphQL 클라이언트를 선택합니다. 일반적으로 이 값은 기본적으로 유지되어야 합니다.
- 스토어 보기 - (Magento) 스토어 보기 식별자입니다. 비어 있으면 기본 스토어 보기가 사용됩니다.
- GraphQL 프록시 경로 - AEM의 URL 경로 GraphQL 프록시를 사용하여 상거래 백엔드 GraphQL 끝점에 대한 요청을 프록시합니다.
   >[!NOTE]
   >
   > 대부분의 설정에서 기본값 `/api/graphql`은(는) 변경할 수 없습니다. 제공된 GraphQL 프록시를 사용하지 않는 고급 설정만 이 설정을 변경해야 합니다.
- 카탈로그 UID 지원 활성화 - 상거래 백엔드 GraphQL 호출에서 ID 대신 UID에 대한 지원을 활성화합니다.
   >[!NOTE]
   >
   > UID에 대한 지원이 Adobe 상거래(Magento) 2.4.2에 도입되었습니다. 상거래 백엔드가 버전 2.4.2 이상의 GraphQL 스키마를 지원하는 경우에만 이 기능을 활성화합니다.
- 카탈로그 루트 카테고리 식별자 - 저장소 카탈로그 루트의 식별자(UID 또는 ID)

위에 표시된 구성은 참조용입니다. 프로젝트는 고유한 구성을 제공해야 합니다.

다른 상거래 카탈로그와 결합된 여러 AEM 사이트 구조를 사용하는 보다 복잡한 설정을 사용하려면 [상거래 다중 스토어 설정](configuring/multi-store-setup.md) 자습서를 참조하십시오.

## 추가 리소스 {#additional-resources}

- [AEM 프로젝트 전형](https://github.com/adobe/aem-project-archetype)
- [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
- [상거래 다중 스토어 설정](configuring/multi-store-setup.md)
