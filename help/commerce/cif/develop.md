---
title: AEM Commerce 개발
description: AEM 프로젝트 원형형을 사용하여 상거래 기반의 AEM 프로젝트를 생성하는 방법을 살펴볼 수 있습니다. 로컬 개발 환경에 프로젝트를 빌드하고 배포하는 방법을 알아봅니다.
topics: Commerce, Development
feature: 전자 상거래 통합 프레임워크
doc-type: tutorial
kt: 5826
thumbnail: 39476.jpg
translation-type: tm+mt
source-git-commit: 8ead3d1b24177effa4d40141408c5676eaabcc30
workflow-type: tm+mt
source-wordcount: '875'
ht-degree: 7%

---


# AEM Commerce {#develop} 개발

AEM용 CIF(Commerce Integration Framework)를 기반으로 하는 AEM Commerce 프로젝트를 개발하는 경우 다른 AEM 프로젝트와 동일한 규칙 및 우수 사례를 따릅니다. 다음 사항을 먼저 검토하십시오.

- [AEM 6.5 개발 사용 안내서](/help/sites-developing/home.md)
- [AEM 코어 개념](/help/sites-developing/the-basics.md)
- [AEM 개발 - 지침 및 우수 사례](/help/sites-developing/dev-guidelines-bestpractices.md)
- [Apache Maven을 사용하여 AEM 프로젝트를 작성하는 방법](/help/sites-developing/ht-projects-maven.md)

## AEM Commerce용 로컬 개발 {#local}

CIF 프로젝트 작업을 수행하려면 로컬 개발 환경을 사용하는 것이 좋습니다.

>[!NOTE]
>
>다음 지침은 AEM 6.5에 초점을 맞춘 CIF를 사용하여 AEM Commerce용 로컬 AEM 개발 환경을 설정하는 데 도움이 됩니다.) AEM을 Cloud Service으로 사용하는 경우 [AEM 커머스를 Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/commerce/home.html) 문서로 참조하십시오.

AEM 6.5용 AEM Commerce Add-On. CIF Add-On은 로컬 개발 및 AEM 패키지로 제공됩니다. [소프트웨어 배포 포털](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)에서 기능 팩으로 다운로드할 수 있습니다.

### 필수 소프트웨어

다음은 로컬에 설치해야 합니다.

- 로컬 AEM 6.5
- [AEM 6.5 서비스 팩](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) 7 이상
- [Java 11](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/general.html)
- [Apache Maven](https://maven.apache.org/) (3.3.9 이상)
- [노드 LTS](https://nodejs.org/en/)
- [npm 6+](https://www.npmjs.com/)
- [Git](https://git-scm.com/)

### CIF Add-on 액세스

CIF Add-on은 [소프트웨어 배포 포털](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)에서 다운로드할 수 있으며 &#39;AEM Commerce add-on&#39;을 검색할 수 있습니다.

>[!TIP]
>
>항상 최신 CIF Add-On 버전을 사용하십시오.

### 로컬 설정

AEM 및 CIF Add-on을 사용하는 로컬 CIF 프로젝트 개발의 경우 다음 단계를 수행하십시오.

1. AEM 6.5 릴리스를 다운로드하고 AEM 6.5 서비스 팩을 설치합니다. AEM 6.5 서비스 팩 7이 필요하지만 마지막으로 사용 가능한 서비스 팩을 설치하는 것이 좋습니다.

1. AEM .jar의 압축을 풀고 `crx-quickstart` 폴더를 만듭니다. 다음을 실행합니다.

   ```bash
   java -jar <jar name> -unpack
   ```

1. `crx-quickstart/install` 폴더 만들기

1. Software Distribution portal에서 다운로드한 모든 패키지에 대한 CIF Add-on을 `crx-quickstart/install` 폴더로 복사합니다.

>[!TIP]
>
>또는 패키지 관리자를 통해 CIF 추가 기능 패키지를 설치할 수도 있습니다.

1. AEM 빠른 시작

OSGI 콘솔을 통해 설정을 확인합니다. `http://localhost:4502/system/console/osgi-installer`. 목록에는 CIF Add-on 관련 번들, 컨텐츠 패키지 및 OSGI 구성이 포함되어야 합니다. 모든 번들이 시작되었는지 확인합니다.

## 프로젝트 설정 {#project}

CIF를 사용하여 AEM Commerce 프로젝트를 시작하는 방법에는 두 가지가 있습니다.

### AEM 프로젝트 원형 사용

[AEM 프로젝트 원형](https://github.com/adobe/aem-project-archetype)은 CIF로 시작하기 위해 미리 구성된 프로젝트를 부트스트래핑하는 주 도구입니다. CIF 핵심 구성 요소 및 필요한 모든 구성을 하나의 추가 옵션을 사용하여 생성된 프로젝트에 포함할 수 있습니다.

>[!TIP]
>
>프로젝트를 생성하려면 [AEM Project Tranype 25 이상](https://github.com/adobe/aem-project-archetype/releases) 을 사용합니다.

AEM 프로젝트를 생성하는 방법은 AEM 프로젝트 원형 [사용 지침](https://github.com/adobe/aem-project-archetype#usage)을 참조하십시오. 프로젝트에 CIF를 포함하려면 `includeCommerce` 옵션을 사용합니다.

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

CIF 핵심 구성 요소는 제공된 `all` 패키지를 포함하거나 CIF 컨텐츠 패키지 및 관련 OSGI 번들을 사용하는 개별 패키지를 포함하여 모든 프로젝트에서 사용할 수 있습니다. 프로젝트에 CIF 핵심 구성 요소를 수동으로 추가하려면 다음 종속성을 사용합니다.

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

### AEM Venia Reference Store 사용

CIF 프로젝트를 시작하는 두 번째 옵션은 [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)를 복제하여 사용하는 것입니다. AEM Venia Reference Store는 AEM용 CIF Core Components의 사용을 보여 주는 샘플 참조 스토어프런트 응용 프로그램입니다. 이 프레임워크는 모범 사례 세트 및 고유한 기능을 개발할 수 있는 잠재적 시작점으로 고안되었습니다.

Venia Reference Store를 시작하려면 [Git 리포지토리](https://github.com/adobe/aem-cif-guides-venia)를 복제하고 필요에 따라 프로젝트를 사용자 정의합니다.

>[!NOTE]
>
>Venia Reference Store 프로젝트에는 Cloud Service 및 AEM 6.5의 AEM용 빌드 프로필이 2개 포함되어 있습니다. [project readme.md](https://github.com/adobe/aem-cif-guides-venia/blob/main/README.md)에서 해당 프로필이 어떻게 사용되는지 확인하십시오. AEM 6.5의 경우 `classic` 프로파일을 사용합니다.

### 전자 상거래 시스템에 AEM 연결

프로젝트를 상거래 시스템 AEM에 연결하려면 상거래 시스템의 GraphQL 끝점으로 구성해야 합니다.

두 프로젝트 모두 [AEM Project Tranype](https://github.com/adobe/aem-project-archetype) 또는 [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)에 의해 생성된 프로젝트에 조정해야 하는 [기본 구성](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json)이 이미 포함되어 있습니다.

`com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json`의 `url` 값을 프로젝트에 사용되는 상거래 시스템의 GraphQL 끝점으로 바꿉니다.

AEM Commerce Add-On 및 CIF 핵심 구성 요소는 AEM 서버를 통해 브라우저를 통해 직접 상거래 GraphQL 끝점에 연결합니다. 클라이언트측 CIF 핵심 구성 요소 및 CIF 추가 기능 작성 도구는 기본적으로 `/api/graphql`에 연결합니다. 필요한 경우 CIF Cloud Service 구성을 통해 조정할 수 있습니다(아래 참조).

CIF 추가 기능은 `/api/graphql`에 GraphQL 프록시 서블릿을 제공합니다. 로컬 AEM Dispatcher를 사용하지 않을 경우 GraphQL 프록시 서블릿을 구성하는 것이 좋습니다.

http://localhost:4502/system/console/configMgr으로 이동하여 `Adobe CIF GraphQL Proxy Configuration` 서비스에 대한 OSGI 구성을 만듭니다. 위의 GraphQL 클라이언트에 사용되는 것과 동일한 상거래 시스템의 GraphQL 끝점을 사용합니다.

## 추가 리소스

- [AEM 프로젝트 전형](https://github.com/adobe/aem-project-archetype)
- [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
