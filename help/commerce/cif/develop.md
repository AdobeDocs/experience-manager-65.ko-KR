---
title: AEM Commerce 개발
description: AEM Project Archetype을 사용하여 상거래 지원 AEM 프로젝트를 생성하는 방법을 알아봅니다. 프로젝트를 빌드하고 로컬 개발 환경에 배포하는 방법에 대해 알아봅니다.
topics: Commerce, Development
feature: Commerce Integration Framework
doc-type: tutorial
kt: 5826
thumbnail: 39476.jpg
exl-id: 48479725-8b52-4ff2-a599-d20958b26ee6
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '871'
ht-degree: 10%

---

# AEM Commerce 개발 {#develop}

AEM용 CIF(Commerce Integration Framework)를 기반으로 AEM Commerce 프로젝트를 개발하는 것은 다른 AEM 프로젝트와 동일한 규칙 및 모범 사례를 따릅니다. 먼저 다음 사항을 검토하십시오.

- [AEM 6.5 개발 사용 안내서](/help/sites-developing/home.md)
- [AEM 코어 개념](/help/sites-developing/the-basics.md)
- [AEM 개발 - 지침 및 우수 사례](/help/sites-developing/dev-guidelines-bestpractices.md)
- [Apache Maven을 사용하여 AEM 프로젝트를 작성하는 방법](/help/sites-developing/ht-projects-maven.md)

## AEM Commerce를 위한 로컬 개발 {#local}

CIF 프로젝트로 작업하려면 로컬 개발 환경이 권장됩니다.

>[!NOTE]
>
>다음 지침은 AEM 6.5에 대한 포커스와 CIF를 사용하여 AEM Commerce용 로컬 AEM 개발 환경을 설정하는 데 도움이 됩니다. AEM을 as a Cloud Service으로 사용하는 경우 [AEM Commerce as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content-and-commerce/home.html) 설명서를 참조하십시오.

AEM 6.5용 AEM Commerce 추가 기능(예: CIF 추가 기능은 로컬 개발에도 사용할 수 있으며 AEM 패키지로 제공됩니다. 다음에서 다운로드할 수 있습니다. [소프트웨어 배포 포털](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) 기능 팩으로 사용됩니다.

### 필수 소프트웨어

다음은 로컬에 설치해야 합니다.

- 로컬 AEM 6.5
- [AEM 6.5 서비스 팩](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) 7 이상
- [Java 11](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/general.html)
- [Apache Maven](https://maven.apache.org/) (3.3.9 이상)
- [노드 LTS](https://nodejs.org/en/)
- [npm 6+](https://www.npmjs.com/)
- [Git](https://git-scm.com/)

### CIF 추가 기능 액세스

CIF 추가 기능은 [소프트웨어 배포 포털](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html), &#39;AEM Commerce 추가 기능&#39;을 검색합니다.

>[!TIP]
>
>항상 최신 CIF 추가 기능 버전을 사용하십시오.

### 로컬 설정

AEM 및 CIF 추가 기능을 사용하여 로컬 CIF 프로젝트를 개발하는 경우 다음 단계를 수행하십시오.

1. AEM 6.5 릴리스를 가져와 AEM 6.5 서비스 팩을 설치합니다. AEM Adobe 6.5 서비스 팩 7이 필요하지만 사용 가능한 마지막 서비스 팩을 설치하는 것이 좋습니다.

1. AEM .jar 압축을 풀고 `crx-quickstart` 폴더, 실행:

   ```bash
   java -jar <jar name> -unpack
   ```

1. 만들기 `crx-quickstart/install` 폴더

1. 소프트웨어 배포 포털에서 다운로드한 CIF 추가 기능 모든 패키지를 `crx-quickstart/install` 폴더를 삭제합니다.

>[!TIP]
>
>또는 패키지 관리자를 통해 CIF 추가 기능 패키지를 설치할 수도 있습니다.

1. AEM 빠른 시작 시작

OSGI 콘솔을 통해 설정을 확인합니다. `http://localhost:4502/system/console/osgi-installer`. 목록에는 CIF 추가 기능 관련 번들, 콘텐츠 패키지 및 OSGI 구성이 포함되어야 합니다. 모든 번들이 시작되었는지 확인하십시오.

## 프로젝트 설정 {#project}

CIF를 사용하여 AEM Commerce 프로젝트를 시작하는 방법에는 두 가지가 있습니다.

### AEM Project Archetype 사용

다음 [AEM Project Archetype](https://github.com/adobe/aem-project-archetype) 는 CIF를 시작하기 위해 사전 구성된 프로젝트를 부트스트랩하는 주요 도구입니다. CIF 코어 구성 요소 및 모든 필수 구성은 하나의 추가 옵션과 함께 생성된 프로젝트에 포함될 수 있습니다.

>[!TIP]
>
>사용 [AEM Project Archetype 25 이상](https://github.com/adobe/aem-project-archetype/releases) 프로젝트를 생성합니다.

AEM 프로젝트 원형 을 참조하십시오. [사용 지침](https://github.com/adobe/aem-project-archetype#usage) AEM 프로젝트를 생성하는 방법에 대해 설명합니다. 프로젝트에 CIF를 포함하려면 `includeCommerce` 옵션을 선택합니다.

예:

```bash
mvn -B archetype:generate \
 -D archetypeGroupId=com.adobe.granite.archetypes \
 -D archetypeArtifactId=aem-project-archetype \
 -D aemVersion=6.5.5 \
 -D appTitle="My Site" \
 -D appId="mysite" \
 -D groupId="com.mysite" \
 -D frontendModule=general \
 -D includeExamples=n \
 -D includeCommerce=y
```

제공된 를 포함하여 모든 프로젝트에서 CIF 코어 구성 요소를 사용할 수 있습니다 `all` cif 콘텐츠 패키지 및 관련 OSGI 번들을 사용하여 패키지 또는 개인을 만듭니다. 프로젝트에 CIF 핵심 구성 요소를 수동으로 추가하려면 다음 종속성을 사용하십시오.

```java
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-apps</artifactId>
    <type>zip</type>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-config</artifactId>
    <type>zip</type>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-core</artifactId>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>graphql-client</artifactId>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>magento-graphql</artifactId>
    <version>x.y.z</version>
</dependency>
```

### AEM Venia 참조 저장소 사용

CIF 프로젝트를 시작하는 두 번째 옵션은 [AEM Venia 참조 저장소](https://github.com/adobe/aem-cif-guides-venia). AEM Venia 참조 저장소는 AEM용 CIF 코어 구성 요소의 사용을 보여 주는 샘플 참조 상점 응용 프로그램입니다. 모범 사례 세트 및 고유한 기능을 개발하기 위한 잠재적인 시작점으로 설계되었습니다.

Venia Reference Store를 시작하려면 다음을 복제하십시오. [Git 저장소](https://github.com/adobe/aem-cif-guides-venia) 필요에 따라 프로젝트를 맞춤화하십시오.

>[!NOTE]
>
>Venia 참조 스토어 프로젝트에는 AEM as a Cloud Service과 AEM 6.5용 빌드 프로필이 두 개 포함되어 있습니다. 다음 확인: [프로젝트 readme.md](https://github.com/adobe/aem-cif-guides-venia/blob/main/README.md) 어떻게 사용되는지 알아보십시오. AEM 6.5의 경우 `classic` 프로필.

### 상거래 시스템에 AEM 연결

프로젝트를 상거래 시스템에 연결하려면 상거래 시스템의 GraphQL 끝점을 사용하여 AEM을 구성해야 합니다.

둘 다, 프로젝트에서 생성됨 [AEM Project Archetype](https://github.com/adobe/aem-project-archetype) 또는 [AEM Venia 참조 저장소](https://github.com/adobe/aem-cif-guides-venia), 이미 다음 포함 [기본 구성](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json) 조정해야 합니다.

값 바꾸기 `url` 위치: `com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json` 프로젝트에서 사용하는 상거래 시스템의 GraphQL 엔드포인트

AEM Commerce 추가 기능 및 CIF 핵심 구성 요소는 AEM 서버를 통해 직접 브라우저를 통해 commerce GraphQL 엔드포인트에 연결합니다. 클라이언트측 CIF 핵심 구성 요소 및 CIF 추가 기능 제작 도구는 기본적으로 다음 위치에 연결됨 `/api/graphql`. 필요한 경우 CIF Cloud Service 구성을 통해 조정할 수 있습니다(아래 참조).

CIF 추가 기능은에서 GraphQL 프록시 서블릿을 제공합니다. `/api/graphql`. 로컬 AEM Dispatcher를 사용할 계획이 없는 경우 GraphQL 프록시 서블릿도 구성하는 것이 좋습니다.

http://localhost:4502/system/console/configMgr으로 이동하여 `Adobe CIF GraphQL Proxy Configuration` 서비스. 위의 GraphQL 클라이언트에 사용된 것과 동일한 상거래 시스템의 GraphQL 엔드포인트를 사용합니다.

## 추가 리소스

- [AEM Project Archetype](https://github.com/adobe/aem-project-archetype)
- [AEM Venia 참조 저장소](https://github.com/adobe/aem-cif-guides-venia)
