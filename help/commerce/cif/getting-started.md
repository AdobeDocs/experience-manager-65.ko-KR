---
title: AEM Content and Commerce 시작하기
description: AEM 컨텐츠 및 상거래 프로젝트를 배포 하는 방법을 알아봅니다.
topics: Commerce
feature: Commerce Integration Framework
exl-id: 92b964f8-6672-4f76-8a9f-5782c3ceb83f
solution: Experience Manager,Commerce
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 3%

---

# AEM Content and Commerce 시작하기 {#start}

AEM Content 및 Commerce을 시작하려면 AEM Content 및 AEM 6.5용 Commerce 추가 기능을 설치해야 합니다.

## 최소 소프트웨어 요구 사항

[AEM 6.5 서비스 팩](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) 7 이상이 필요합니다.

## 온보딩 {#onboarding}

AEM Content 및 Commerce에 대한 온보딩은 두 단계로 구성됩니다.

1. AEM 6.5용 AEM Content and Commerce Add-On 설치

2. AEM을 상거래 솔루션과 연결

### AEM 6.5용 AEM Content 및 Commerce 추가 기능 설치 {#install-add-on}

에서 AEM 6.5용 AEM Commerce 추가 기능을 다운로드하여 설치합니다. [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) 포털.

필요한 AEM 6.5 서비스 팩을 시작 및 설치합니다. 사용 가능한 마지막 서비스 팩을 설치하는 것이 좋습니다.

>[!NOTE]
>
>이 작업은 CSE에서 AEM Managed Service 고객용으로 수행합니다.

### 상거래 시스템에 AEM 연결 {#connect}

AEM은 AEM에 액세스할 수 있는 GraphQL 종단점이 있는 모든 상거래 시스템에 연결할 수 있습니다. 이러한 엔드포인트는 일반적으로 공개적으로 사용할 수 있거나 개별 프로젝트 설정에 따라 프라이빗 VPN 또는 로컬 연결을 통해 연결할 수 있습니다.

선택적으로, 인증이 필요한 추가 CIF 기능을 사용하기 위해 인증 헤더를 제공할 수 있습니다.

AEM Project Archetype](https://github.com/adobe/aem-project-archetype) 및 [기본 구성](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json)에 [이미 포함된 AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)에서 생성된 [프로젝트를 조정해야 합니다.

상거래 시스템의 GraphQL 끝점으로 in `com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json` 의 `url` 값을 바꾸기. 이 구성은 OSGI 콘솔을 통해 또는 프로젝트를 통해 OSGI 구성을 배포하여 수행할 수 있습니다. 서로 다른 AEM 실행 모드를 사용하여 스테이징 및 프로덕션 시스템에 대한 다양한 구성이 지원됩니다.

AEM 컨텐츠 및 상거래 추가 기능과 CIF 코어 구성 요소는 AEM 서버측 및 클라이언트측 연결을 모두 사용합니다. 클라이언트측 CIF 코어 구성 요소 및 CIF 추가 기능 작성 도구는 기본적으로 `/api/graphql`. 필요한 경우 CIF Cloud Service 구성을 통해 조정할 수 있습니다(아래 참조).

CIF Add-On은 로컬 개발에](develop.md) 선택적으로 사용할 [수 있는 GraphQL 프록시 서블릿 `/api/graphql` 을 제공합니다. 프로덕션 배포의 경우 AEM Dispatcher 또는 다른 네트워크 계층(좋아요 CDN)을 통해 상거래 GraphQL 엔드포인트에 역방향 프록시를 설정하는 것이 좋습니다.

## 저장소 및 카탈로그 구성 {#catalog}

추가 기능 및 [CIF 핵심 구성 요소](https://github.com/adobe/aem-core-cif-components) 여러 상거래 상점(또는 스토어 보기 등)에 연결된 여러 AEM 사이트 구조에서 사용할 수 있습니다. 기본적으로 CIF 추가 기능은 Adobe Commerce의 기본 스토어 및 카탈로그에 연결하는 기본 구성으로 배포됩니다.

다음 단계에 따라 CIF Cloud Service 구성을 통해 프로젝트에 대해 이 구성을 조정할 수 있습니다.

1. AEM에서 도구 > Cloud Service > CIF 구성으로 이동합니다.

2. 변경할 상거래 구성 선택

3. 작업 표시줄을 통해 구성 속성 열기

![CIF Cloud Service 구성](/help/commerce/cif/assets/cif-cloud-service-config.png)

다음 속성을 구성할 수 있습니다.

- GraphQL 클라이언트 - commerce 백엔드 통신용으로 구성된 GraphQL 클라이언트를 선택합니다. 이 옵션은 일반적으로 기본값으로 유지되어야 합니다.
- 스토어 뷰 - 스토어 뷰 식별자. 비어 있으면 기본 스토어 보기가 사용됩니다.
- GraphQL 프록시 경로 - URL 경로 AEM의 GraphQL 프록시는 상거래 백엔드 GraphQL 종단점에 대한 요청을 프록시하는 데 사용합니다.

  >[!NOTE]
  >
  >대부분의 설정에서는 기본값 `/api/graphql` 을 변경하지 않아야 합니다. 제공된 GraphQL 프록시를 사용하지 않는 고급 설정만 이 설정을 변경해야 합니다.

- 카탈로그 UID 지원 활성화 - 상거래 백엔드 GraphQL 호출에서 ID 대신 UID에 대한 지원을 활성화합니다.

  >[!NOTE]
  >
  >UID에 대한 지원은 Adobe Systems Commerce 2.4.2에서 도입되었습니다. 상거래 백엔드가 버전 2.4.2 이상의 GraphQL 스키마를 지원하는 경우에만 이 기능을 활성화합니다.

- 카탈로그 루트 범주 식별자 - 스토어 카탈로그 루트의 식별자(UID 또는 ID)입니다.

  >[!CAUTION]
  >
  >CIF 핵심 구성 요소 버전 2.0.0부터 `id` 을(를) 제거하고 로 대체함 `uid`. 프로젝트에서 CIF 핵심 구성 요소 버전 2.0.0을 사용하는 경우 카탈로그 UID 지원을 활성화하고 유효한 범주 UID를 &quot;카탈로그 루트 범주 식별자&quot;로 사용해야 합니다.

위에 표시된 구성은 참조용입니다. 프로젝트는 자체 구성을 제공해야 합니다.

서로 다른 상거래 카탈로그와 결합된 여러 AEM 사이트 구조를 사용하는 더 복잡한 설정에 대해서는 다음을 참조하십시오. [Commerce 다중 스토어 설정](configuring/multi-store-setup.md) 튜토리얼.

## 추가 리소스 {#additional-resources}

- [AEM Project Archetype](https://github.com/adobe/aem-project-archetype)
- [AEM Venia 참조 저장소](https://github.com/adobe/aem-cif-guides-venia)
- [Commerce 다중 스토어 설정](configuring/multi-store-setup.md)
