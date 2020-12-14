---
title: Salesforce Commerce Cloud
seo-title: Salesforce Commerce Cloud / Demandware
description: Salesforce Commerce Cloud/Demandware를 사용하여 eCommerce를 배포하는 방법을 알아봅니다.
seo-description: Salesforce Commerce Cloud/Demandware를 사용하여 eCommerce를 배포하는 방법을 알아봅니다.
uuid: c0270632-bdd2-4dba-bbbe-312757ea20f4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: e-commerce
content-type: reference
discoiquuid: 52cc3162-b638-410d-854a-383399e2effb
docset: aem65
pagetitle: Deploying eCommerce with Demandware
redirecttarget: https //github.com/adobe/commerce-salesforce
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 2%

---


# Salesforce Commerce Cloud{#salesforce-commerce-cloud}

필요한 eCommerce 패키지를 배포하면 Salesforce Commerce Cloud/Demandware 구현(데모 카탈로그 포함)과 함께 eCommerce 기능의 참조 구현과 함께 eCommerce 프레임워크의 모든 기능을 제공합니다.

## Salesforce Commerce Cloud {#packages-needed-for-ecommerce-with-salesforce-commerce-cloud}이 있는 eCommerce에 필요한 패키지

eCommerce 기능을 설치하려면 다음 작업이 필요합니다.

* AEM eCommerce 프레임워크:

   * 표준 AEM 설치에 포함되어 있습니다.

* AEM Demandware Commerce 컨텐츠 패키지

   * cq-6.4.0-featurepack-10262

>[!NOTE]
>
>이 통합은 OAPI 버전 17.6 이상을 사용하도록 구성된 Salesforce Commerce Cloud/Demandware 인스턴스를 지원합니다.

### Salesforce Commerce Cloud {#installation-of-ecommerce-with-salesforce-commerce-cloud}과 함께 eCommerce 설치

Demandware Commerce 통합 구성(데모 카탈로그, Geometrixx Outdoors 사용)을 사용하여 AEM을 설치하려면 기본 단계는 다음과 같습니다.

1. [AEM을 설치합니다](/help/sites-deploying/deploy.md).
1. [패키지 관리자](/help/sites-administering/package-manager.md)를 사용하여 콘텐트 패키지를 설치합니다.
1. [aem](/help/sites-authoring/page-authoring.md) 에서 필요한 추가 페이지를 제작합니다.

>[!NOTE]
>
>패키지를 다운로드하려면 [패키지 공유](/help/sites-administering/package-manager.md#package-share)로 이동하십시오.

AEM과 Demandware 샌드박스 간의 서버 연결을 구성해야 합니다. 대부분의 구성은 기본 경로, 라이브러리 등을 사용하여 제공된 SiteGenisis 데모 컨텐츠 패키지로 작업하도록 이미 미리 구성되어 있습니다. 커넥터가 다른 사이트 및 라이브러리와 함께 사용되는 경우 이 구성을 업데이트해야 합니다.

1. [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)로 이동합니다.
1. **Demandware 클라이언트**&#x200B;를 클릭합니다.
1. 필요에 따라 **인스턴스 끝점 ip 또는 호스트 이름**&#x200B;을 입력합니다.

   ![chlimage_1-5](assets/chlimage_1-5.png)

1. **저장**&#x200B;을 클릭합니다.
1. WebDAV **용** Demandware TransportHandler Plugin을 클릭합니다.
1. **WebDAV 사용자** 및 **WebDAV 사용자 암호**&#x200B;를 설정합니다.

   ![chlimage_1-6](assets/chlimage_1-6.png)

1. **저장**&#x200B;을 클릭합니다.

#### 복제 {#replication}

패키지 설치 후 복제를 활성화해야 합니다. 여기서 확인할 수 있습니다.[https://localhost:4502/etc/replication/agents.author/demandware.html](https://localhost:4502/etc/replication/agents.author/demandware.html)

>[!NOTE]
>
>기본적으로 복제 에이전트가 정보 로그 수준으로 구성됩니다. 자세한 내용을 보려면 로그 수준을 디버그로 전환할 수 있습니다.

#### OAuth {#oauth}

OAuth 클라이언트는 Demandware 샌드박스 인스턴스에서 작동하도록 구성되어 있습니다. 테스트 목적으로 변경할 필요가 없습니다.

스테이징 및 프로덕션 시스템의 경우 OAuth 클라이언트는 적절한 클라이언트 ID 및 암호로 구성해야 합니다.

1. [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)로 이동합니다.
1. **Demandware 액세스 토큰 공급자**&#x200B;를 클릭합니다.

   ![chlimage_1-7](assets/chlimage_1-7.png)

1. 필요에 따라 값을 수정하고 **저장**&#x200B;을 클릭합니다.

### Salesforce Commerce Cloud 샌드박스 {#salesforce-commerce-cloud-sandbox}

새로운 Velocity 템플릿 엔진을 실행하려면 Demandware Sandbox를 구성해야 합니다.

>[!NOTE]
>
>다음 마법사는 AEM Demandware 커넥터의 일부가 아닙니다. SiteGenesis 데모 페이지를 빠르게 설정하는 데 도움이 되도록 데모 컨텐츠 패키지의 일부로 제공됩니다.

1. [https://localhost:4502/etc/demandware/init.html](https://localhost:4502/etc/demandware/init.html)로 이동합니다.
1. **편집**&#x200B;을 클릭합니다.
1. 값을 확인하고 **확인**&#x200B;을 클릭합니다.
1. **초기화**&#x200B;를 클릭합니다.
1. WebDAV 폴더로 이동하여 게시된 템플릿 파일을 확인합니다(예: `adobe01-tech-prtnr-na01-dw.demandware.net/on/demandware.servlet/webdav/Sites/Dynamic/SiteGenesis`).

   >[!NOTE]
   >
   >확장자는 `.vs`입니다.

1. 내보낸 JS 및 CSS 파일도 확인합니다(예: `adobe01-tech-prtnr-na01-dw.demandware.net/on/demandware.servlet/webdav/Sites/Libraries/SiteGenesisSharedLibrary`).

