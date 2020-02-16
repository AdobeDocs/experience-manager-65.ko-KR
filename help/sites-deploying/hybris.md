---
title: SAP Commerce Cloud
seo-title: SAP Commerce Cloud
description: SAP Commerce Cloud를 사용하여 eCommerce를 배포하는 방법을 알아봅니다.
seo-description: SAP Commerce Cloud를 사용하여 eCommerce를 배포하는 방법을 알아봅니다.
uuid: 26ace49c-02d2-4b49-a959-e033def89bd4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: e-commerce
content-type: reference
discoiquuid: c5dcc90a-05d2-4701-a625-2b655ad0b458
docset: aem65
pagetitle: Deploying eCommerce with hybris
translation-type: tm+mt
source-git-commit: d83cd0695f69d82e49b1761df2d8c64b0037e1f9

---


# SAP Commerce Cloud{#sap-commerce-cloud}

>[!NOTE]
>
>이 페이지에는 hybris 웹 사이트에 대한 링크가 포함되어 있습니다. 특정 페이지의 경우 로그인하려면 계정이 필요합니다.

## SAP Commerce Cloud를 사용하여 eCommerce 배포 {#deploying-ecommerce-with-sap-commerce-cloud}

>[!NOTE]
>
>AEM 6.5용 커넥터가 준비되지 않았습니다.

>[!NOTE]
>
>다음 절차에서는 배포를 설명하기 위해 다음 데모 카탈로그를 사용합니다.
>
>`Geometrixx Outdoors Site English (US)`

e커머스 패키지를 [](#packages-needed-for-ecommerce-with-hybris) 배포하면 e커머스 프레임워크의 모든 기능과 하이브리스 구현(데모 카탈로그 포함)에 제공된 e커머스 기능의 참조 구현 기능을 제공합니다

Geometrixx Outdoors 사이트의 영어(미국) 분기( `/content/geometrixx-outdoors/en_US`)에서 사용할 수 있습니다.

* [제품 정보](#productinformationwithcolorvariants) (해당되는 경우 색상 변형 포함)

* [장바구니 컨텐츠 개요](#shoppingcartcontentoverview)
* [고객 등록](#customersignup) 및 [고객 로그인](#customersignin)

* [hybris 관리 콘솔 액세스](#accesstothehybrismanagementconsole)

### 기술 요구 사항 - hybris Server {#technical-requirements-hybris-server}

eCommerce Integration Framework의 hybris 확장이 Hybris 5(기본값)를 지원하도록 업데이트되었으며 Hybris 4와 이전 버전과의 호환성을 유지하고 [있습니다](/help/sites-developing/hybris.md#developing-for-hybris).

>[!NOTE]
>
>* OCC 버전 2에서 최대 hybris 6.4를 지원합니다.
>* hybris 5 서버를 실행하려면 Java 7이 [필요합니다.](https://www.hybris.com/en/architecture-technology)
>* AEM 익스텐션에서 Telco [Accelerator](https://www.hybris.com/en/products/telecommunication)hybris 추가 기능을 지원하지 않습니다.
>



### hybris를 사용한 전자 상거래에 필요한 패키지 {#packages-needed-for-ecommerce-with-hybris}

eCommerce 기능을 설치하려면 다음 작업이 필요합니다.

* hybris 서버, [hybris](#configureandbuildthehybrisserver)사용 가능
* AEM eCommerce 프레임워크:

   * 표준 AEM 설치의 일부입니다

* AEM Geometrixx-all 패키지:

   * `cq-geometrixx-all-pkg`

* AEM hybris 컨텐츠 패키지:&quot;

   * 
       &quot;
 cq-hybris-content-6.3.2     
     
     &quot;
   
   * hybris 전용 API 구현
   * `cq-geometrixx-hybris-content-6.3.2`
   * hybris( `geometrixx-outdoors/en_US`) 사용을 설명하기 위한 참조 구현


### 하이브리스를 이용한 전자상거래 설치 {#installation-of-ecommerce-with-hybris}

완전한 구성을 설치하려면(데모 카탈로그 사용, Geometrixx Outdoors) 기본 단계는 다음과 같습니다.

1. [AEM 설치](/help/sites-deploying/deploy.md).
1. Geometrixx-all 패키지 설치

   1. ` [cq-geometrixx-all-pkg](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq60/product/cq-geometrixx-all-pkg)`

1. 데모 컨텐츠 패키지를 [패키지 관리자를](/help/sites-administering/package-manager.md)사용하여 설치합니다.

   1. ` [cq-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-hybris-content)`
   1. ` [cq-geometrixx-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-geometrixx-hybris-content)`

1. [hybris Server를 다운로드하여 구축할 수 있습니다](#download-and-build-your-hybris-server).
1. eCommerce 엔진에서 카탈로그를 구성합니다.

   1. [Geometrixx Outdoor Store를 설치합니다](#setup-the-geometrixx-outdoors-store).

1. [AEM에서](/help/sites-authoring/page-authoring.md) 필요한 추가 페이지를 작성합니다.

>[!CAUTION]
>
>hybris 서버를 사용하려면 별도의 hybris 라이센스가 필요합니다.

>[!NOTE]
>
>개발자의 [경우 API 설명서를](/help/sites-developing/ecommerce.md#api-documentation) 다운로드할 수도 있습니다.

### hybris 서버 다운로드 및 빌드 {#download-and-build-your-hybris-server}

이 절차의 단계에서는 hybris 서버를 다운로드하고 만듭니다. 또한 hybris와 cq 간의 연결에 필요한 초기 구성을 만들 수 있습니다. 그런 다음 기본 설정에서 익스텐션을 사용할 수 있습니다.

>[!CAUTION]
>
>5.5.1 이전의 Hybris 버전은 지원되지 않습니다.

>[!NOTE]
>
>이 작업을 완료하려면 시스템에 [Group](https://groovy-lang.org/) 이 설치되어 있어야 합니다.

1. hybris 다운로드 사이트에서 **hybris Commerce Suite **배포를 다운로드합니다.

   >[!CAUTION]
   >
   >이 항목에 액세스하려면 (hybris에서) 계정이 필요합니다.

1. 배포 파일의 압축을 필요한 위치(예: &lt;hybris-root-directory>)로 해제합니다.
1. 명령줄에서 다음을 실행합니다.

   ```shell
   cd <hybris-root-directory>/bin/platform
   . ./setantenv.sh
   ant clean all
   cd ../..
   ```

   >[!NOTE]
   >
   >실행 시:
   >
   >
   >`ant clean all`
   >
   >
   >필요할 `Return` 때 키를 누릅니다.

1. 다음 파일을 추출된 hybris 배포의 루트 폴더로 다운로드합니다.

   ```
       <<i>hybris-root-directory</i>>
   ```

   :

   [파일 가져오기](assets/setup.groovy)

   >[!NOTE]
   >
   >hybris 5.6.0 이상 버전의 경우 다음 setup.group을 사용하십시오.

   5.6.0 이상

   [파일 가져오기](assets/setup-1.groovy)

1. 명령줄에서 다음을 실행합니다.

   * hybris 서버 구성 업데이트(익스텐션에서 필요한 경우)
   * 수정한 구성으로 hybris 서버 다시 빌드
   * 서버 시작

   ```shell
   groovy setup.groovy
   cd bin/platform
   ant clean all
   sh hybrisserver.sh
   ```

   >[!NOTE]
   >
   >시스템에 따라 이러한 단계를 완료하는 데 몇 분이 걸릴 수 있습니다.

1. 브라우저에서 다음 위치에서 **hybris 관리 콘솔로** 이동합니다.

   [https://localhost:9002](https://localhost:9002)

1. 초기화를 **** 클릭한 다음 초기화 작업을 확인합니다(기존 데이터를 삭제하므로).

   완료를 `FINISHED` 나타내는 진행 상태가 콘솔에 표시됩니다.

   >[!NOTE]
   >
   >시스템에 따라 이 작업을 완료하는 데 몇 분이 걸릴 수 있습니다.

### Geometrixx Outdoors 스토어 설정 {#setup-the-geometrixx-outdoors-store}

이 절차는 데모 스토어 - Geometrixx Online을 업로드하고 구성합니다.

1. 하이브리스 인스턴스를 시작합니다. 명령줄에서 다음을 실행합니다.

   ```shell
   cd <hybris-root-directory>/bin/platform
   sh hybrisserver.sh
   ```

1. 브라우저에서 다음 위치에서 **hybris 관리 콘솔로** 이동합니다.

   [https://localhost:9002/hmc/hybris](https://localhost:9002/hmc/hybris)

1. 사이드바 탐색에서 시스템 및 **도구를** **설명합니다**. 그런 다음 가져오기를 **선택하여** 마법사를 **엽니다.CSV 가져오기** 창.
1. 구성 **탭에서** **다음** 가져오기 **파일을**&#x200B;업로드합니다.

   [파일 가져오기](assets/geometrixx-outdoors-export.csv)

1. 로케일 **설정을** 다음으로 설정:

   `en_US - English (United States)`

1. Open the **Resources** tab.
1. **다음 미디어** - **Zip을 업로드합니다**.

   [파일 가져오기](assets/geometrixx-outdoors-images.zip)

1. 시작을 **클릭하여** 지정된 파일을 가져옵니다. 결과 **탭에** 모든 로그 항목이 표시됩니다.

1. 완료를 **클릭하여** 가져오기 창을 닫습니다.

1. 세로 막대에서 시스템, **도구**, **가져오기**&#x200B;순으로 **선택합니다**.

1. **다음 가져오기** 파일을 **업로드합니다**.

   [파일 다운로드](assets/base-store.csv)hybris 5.7의 경우 다음을 사용하십시오.

   [파일 가져오기](assets/base-store-5_7.csv)

1. 로케일 **설정을** 다음으로 설정:

   `en_US - English (United States)`

1. 시작을 **클릭하여** 지정된 파일을 가져옵니다. 결과 **탭에** 모든 로그 항목이 표시됩니다.

1. 완료를 **클릭하여** 가져오기 창을 닫습니다.

1. 이제 제품 조종실을 사용하여 가져온 카탈로그 및 제품을 볼 수 있습니다.

   [https://localhost:9002/productcockpit](https://localhost:9002/productcockpit)

