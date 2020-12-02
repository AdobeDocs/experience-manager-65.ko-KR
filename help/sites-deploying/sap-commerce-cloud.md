---
title: SAP Commerce Cloud
seo-title: SAP Commerce Cloud
description: SAP Commerce Cloud을 사용하여 e커머스를 배포하는 방법을 알아봅니다.
seo-description: SAP Commerce Cloud을 사용하여 e커머스를 배포하는 방법을 알아봅니다.
uuid: a16ae42b-9c33-4da8-a130-52b72a779ec7
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: e-commerce
content-type: reference
discoiquuid: 44dfa10f-497e-473f-95d4-8dccae7ebf8e
pagetitle: Deploying eCommerce with SAP Commerce Cloud
translation-type: tm+mt
source-git-commit: 328e13eb2ce034b0b1ec7e5e0fb184de9435d1bc
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 2%

---


# SAP Commerce Cloud{#sap-commerce-cloud}

>[!NOTE]
>
>이 페이지에는 hybris 웹 사이트에 대한 링크가 포함되어 있습니다. 특정 페이지의 경우 로그인하려면 계정이 필요합니다.

## SAP Commerce Cloud {#deploying-ecommerce-with-sap-commerce-cloud}을(를) 사용하여 eCommerce 배포

>[!NOTE]
>
>다음 절차에서는 배포를 설명하기 위해 다음 데모 카탈로그를 사용합니다.
>
>`Geometrixx Outdoors Site English (US)`

[필요한 eCommerce 패키지](#packages-needed-for-ecommerce-with-hybris)를 배포하면 hybris 구현(데모 카탈로그 포함)과 함께 제공되는 eCommerce 기능의 참조 구현과 함께 eCommerce 프레임워크의 모든 기능을 제공합니다

Geometrixx Outdoors 사이트의 영어(미국) 분기( `/content/geometrixx-outdoors/en_US`)에서 사용할 수 있습니다.

* [제품 정보](#productinformationwithcolorvariants) (해당되는 경우 색상 변형 포함)

* [장바구니 컨텐츠 개요](#shoppingcartcontentoverview)
* [고객 ](#customersignup) 로그인 및  [고객 로그인](#customersignin)

* [hybris 관리 콘솔 액세스](#accesstothehybrismanagementconsole)

### 기술 요구 사항 - hybris 서버 {#technical-requirements-hybris-server}

eCommerce Integration Framework의 hybris 확장이 [Hybris 4](/help/sites-developing/sap-commerce-cloud.md#developing-for-hybris)와의 이전 호환성을 유지하면서 Hybris 5(기본값)를 지원하도록 업데이트되었습니다.

>[!NOTE]
>
>* 18.11 이상 버전을 지원합니다.
>* [hybris 5 서버를 실행하려면 Java 7이 필요합니다.](https://www.hybris.com/en/architecture-technology)
>* hybris add-on, [Telco Accelerator](https://www.hybris.com/en/products/telecommunication)은 AEM 익스텐션에서 지원되지 않습니다.

>



### 하이브리스가 {#packages-needed-for-ecommerce-with-hybris}인 e커머스에 필요한 패키지

eCommerce 기능을 설치하려면 다음이 필요합니다.

* 하이브리스 서버
* AEM eCommerce 프레임워크:

   * 표준 AEM 설치의 일부입니다

* AEM Geometrixx-all 패키지:

   * `cq-geometrixx-all-pkg`

* AEM hybris 컨텐츠 패키지:

   * `cq-hybris-content-6.3.2`
   * hybris 특정 API 구현
   * `cq-geometrixx-hybris-content-6.3.2`
   * hybris( `geometrixx-outdoors/en_US`)의 사용을 설명하기 위한 참조 구현

### {#installation-of-ecommerce-with-hybris}과(와) 함께 전자 상거래 설치

완전한 구성을 설치하려면(데모 카탈로그, Geometrixx Outdoors 사용) 기본 단계는 다음과 같습니다.

1. [AEM을 설치합니다](/help/sites-deploying/deploy.md).
1. 모든 Geometrixx 패키지 설치

   1. ` [cq-geometrixx-all-pkg](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq60/product/cq-geometrixx-all-pkg)`

1. [패키지 관리자](/help/sites-administering/package-manager.md)를 사용하여 데모 콘텐츠 패키지를 설치합니다.

   1. ` [cq-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-hybris-content)`
   1. ` [cq-geometrixx-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-geometrixx-hybris-content)`

1. [hybris Server를 다운로드하여 구축할 수 있습니다](#download-and-build-your-hybris-server).
1. eCommerce 엔진에서 카탈로그 구성:

   1. [Geometrixx 아웃도어 스토어를 설치합니다](#setup-the-geometrixx-outdoors-store).

1. [aem](/help/sites-authoring/qg-page-authoring.md) 에서 필요한 보조 페이지를 제작할 수 있습니다.

>[!CAUTION]
>
>하이브리스 서버를 이용하려면 별도의 하이브리스 라이센스가 필요합니다.

>[!NOTE]
>
>개발자의 경우 [API 설명서](/help/sites-developing/ecommerce.md#api-documentation)를 다운로드할 수도 있습니다.

### 하이브리스 서버 다운로드 및 빌드 {#download-and-build-your-hybris-server}

이 절차의 단계는 hybris 서버를 다운로드하고 빌드합니다. 또한 hybris와 cq 간의 연결에 필요한 초기 구성이 됩니다. 그러면 기본 설정에서 확장 기능을 사용할 수 있습니다.

>[!CAUTION]
>
>5.5.1 이전의 Hybris 버전은 지원되지 않습니다.

>[!NOTE]
>
>이 작업을 완료하려면 시스템에 [Group](https://groovy-lang.org/)이(가) 설치되어 있어야 합니다.

1. hybris 다운로드 사이트에서 **hybris Commerce Suite** 배포를 다운로드합니다.

   >[!CAUTION]
   >
   >이 항목에 액세스하려면 계정(hybris에서)이 필요합니다.

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
   >`ant clean all`
   >
   >필요한 경우 `Return`을 누릅니다.

1. 다음 파일을 추출한 hybris 배포의 루트 폴더로 다운로드합니다.

   ```
       <hybris-root-directory>
   ```


   [파일 가져오기](assets/setup.groovy)

   >[!NOTE]
   >
   >hybris 5.6.0 이상 버전의 경우 다음 setup.group을 사용하십시오.

   5.6.0 이상

   [파일 가져오기](assets/setup-1.groovy)

1. 명령줄에서 다음을 실행합니다.

   * hybris 서버 구성 업데이트(익스텐션에서 필요)
   * 수정한 구성으로 hybris 서버 재구성
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

1. 브라우저에서 **hybris 관리 콘솔**&#x200B;으로 이동합니다.

   [http://localhost:9002](http://localhost:9002)

1. **초기화**&#x200B;를 클릭한 다음 초기화 작업을 확인합니다(기존 데이터를 삭제함).

   완료를 나타내는 `FINISHED`과 함께 진행 상태가 콘솔에 표시됩니다.

   >[!NOTE]
   >
   >시스템에 따라 이 작업을 완료하는 데 몇 분이 걸릴 수 있습니다.

### Geometrixx Outdoors 저장소 {#setup-the-geometrixx-outdoors-store} 설정

이 절차는 데모 스토어(Geometrixx 온라인)를 업로드하고 구성합니다.

1. 하이브리스의 예부터 시작해 명령줄에서 다음을 실행합니다.

   ```shell
   cd <hybris-root-directory>/bin/platform
   sh hybrisserver.sh
   ```

1. 브라우저에서 **hybris 관리 콘솔**&#x200B;으로 이동합니다.

   [https://localhost:9002/backoffice](https://localhost:9002/backoffice)

   다음 자격 증명을 사용하십시오.
   * 사용자 이름:admin
   * password:님다

1. 사이드바 탐색에서 **System** 및 **Tools**&#x200B;을 탐색합니다. 그런 다음 **가져오기**&#x200B;를 선택하여 **마법사를 엽니다.CSV 가져오기** 창
1. **구성** 탭에서 **업로드**&#x200B;다음 **파일 가져오기**&#x200B;를 수행합니다.

   [파일 가져오기](assets/geometrixx-outdoors-export.csv)

1. **로케일 설정**&#x200B;을 다음과 같이 설정합니다.

   `en_US - English (United States)`

1. **리소스** 탭을 엽니다.
1. **다음** 미디어- **Zip을 업로드합니다**.

   [파일 가져오기](assets/geometrixx-outdoors-images.zip)

1. **시작**&#x200B;을 클릭하여 지정된 파일을 가져옵니다. **결과** 탭에는 모든 로그 항목이 표시됩니다.

1. **완료**&#x200B;를 클릭하여 가져오기 창을 닫습니다.

1. 세로 막대에서 **시스템**&#x200B;을 선택하고 **도구**&#x200B;를 선택한 다음 **가져오기**&#x200B;를 선택합니다.

1. **다음 가져오기 파일** 을  **업로드합니다**.

   [파일 가져오기](assets/base-store.csv)

   hybris 5.7의 경우 다음을 사용하십시오.

   [파일 가져오기](assets/base-store-5_7.csv)

1. **로케일 설정**&#x200B;을 다음과 같이 설정합니다.

   `en_US - English (United States)`

1. **시작**&#x200B;을 클릭하여 지정된 파일을 가져옵니다. **결과** 탭에는 모든 로그 항목이 표시됩니다.

1. **완료**&#x200B;를 클릭하여 가져오기 창을 닫습니다.

1. 이제 제품 조종실을 사용하여 가져온 카탈로그 및 제품을 볼 수 있습니다.

   [http://localhost:9002/productcockpit](http://localhost:9002/productcockpit)

