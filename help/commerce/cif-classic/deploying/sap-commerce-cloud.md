---
title: SAP Commerce Cloud으로 eCommerce 배포
description: SAP Commerce Cloud을 사용하여 eCommerce를 배포하는 방법을 알아봅니다.
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
exl-id: ecbd0097-c407-4581-bab2-4729a71df4a3
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 2%

---

# SAP Commerce Cloud{#sap-commerce-cloud}

>[!NOTE]
>
>이 페이지에는 hybris 웹 사이트에 대한 링크가 포함되어 있습니다. 특정 페이지의 경우 로그인하려면 계정이 필요합니다.

## SAP Commerce Cloud으로 eCommerce 배포 {#deploying-ecommerce-with-sap-commerce-cloud}

>[!NOTE]
>
>다음 절차에서는 다음 데모 카탈로그를 사용하여 배포를 보여 줍니다.
>
>`Geometrixx Outdoors Site English (US)`

배포 [필요한 eCommerce 패키지](#packages-needed-for-ecommerce-with-hybris) hybris 구현(데모 카탈로그 포함)과 함께 제공된 eCommerce 기능의 참조 구현과 함께 eCommerce 프레임워크의 전체 기능을 제공합니다

영어(미국) 분기( `/content/geometrixx-outdoors/en_US`)을 만들 수 있습니다.

* [제품 정보](#productinformationwithcolorvariants) (해당되는 경우 색상 변형 사용)

* [장바구니 컨텐츠 개요](#shoppingcartcontentoverview)
* [고객 등록](#customersignup) 및 [고객 로그인](#customersignin)

* [hybris 관리 콘솔에 액세스](#accesstothehybrismanagementconsole)

### 기술 요구 사항 - hybris 서버 {#technical-requirements-hybris-server}

eCommerce Integration Framework의 hybris 확장이 Hybris 5(기본값)를 지원하도록 업데이트되었으며, [Hybris 4](/help/commerce/cif-classic/developing/sap-commerce-cloud.md#developing-for-hybris).

>[!NOTE]
>
>* 버전 18.11 이상을 지원합니다.
>* 를 실행하려면 Java 7이 필요합니다 [hybris 5 서버.](https://www.hybris.com/en/architecture-technology)
>* hybris 추가 기능, [Telco Accelerator](https://www.hybris.com/en/products/telecommunication)은 AEM 확장에서 지원되지 않습니다.
>


### hybris를 사용하는 eCommerce에 필요한 패키지 {#packages-needed-for-ecommerce-with-hybris}

eCommerce 기능을 설치하려면 다음을 수행해야 합니다.

* hybris 서버
* AEM eCommerce 프레임워크:

   * 표준 AEM 설치의 일부입니다

* AEM Geometrixx-모든 패키지:

   * `cq-geometrixx-all-pkg`

* AEM hybris 컨텐츠 패키지:

   * `cq-hybris-content-6.3.2`
   * hybris 특정 API 구현
   * `cq-geometrixx-hybris-content-6.3.2`
   * hybris 사용을 설명하는 참조 구현( `geometrixx-outdoors/en_US`)

### hybris를 사용한 eCommerce 설치 {#installation-of-ecommerce-with-hybris}

완전한 구성(데모 카탈로그 사용)을 설치하려면 기본 단계는 다음과 같습니다.

1. [AEM 설치](/help/sites-deploying/deploy.md).
1. 모든 Geometrixx 패키지 설치

   1. ` [cq-geometrixx-all-pkg](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq60/product/cq-geometrixx-all-pkg)`

1. 를 사용하여 데모 컨텐츠 패키지 설치 [패키지 관리자](/help/sites-administering/package-manager.md):

   1. ` [cq-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-hybris-content)`
   1. ` [cq-geometrixx-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-geometrixx-hybris-content)`

1. [hybris 서버 다운로드 및 빌드](#download-and-build-your-hybris-server).
1. eCommerce 엔진에서 카탈로그를 구성합니다.

   1. [Geometrixx 아웃도어 스토어 설정](#setup-the-geometrixx-outdoors-store).

1. [작성자](/help/sites-authoring/qg-page-authoring.md) AEM에서 필요한 모든 보조 페이지.

>[!CAUTION]
>
>hybris 서버를 사용하려면 별도의 hybris 라이센스가 필요합니다.

>[!NOTE]
>
>개발자용 [API 설명서](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation) 을 다운로드할 수도 있습니다.

### hybris 서버 다운로드 및 빌드 {#download-and-build-your-hybris-server}

이 절차의 단계는 hybris 서버를 다운로드하고 빌드합니다. 또한 hybris와 cq 간의 연결에 필요한 초기 구성을 만듭니다. 그러면 기본 설정에서 확장을 사용할 수 있습니다.

>[!CAUTION]
>
>5.5.1 이전의 hybris 버전은 지원되지 않습니다.

>[!NOTE]
>
>이 작업을 완료하려면 [그로비](https://groovy-lang.org/) 시스템에 설치되었습니다.

1. 다운로드 **hybris Commerce Suite** hybris 다운로드 사이트에서 배포.

   >[!CAUTION]
   >
   >여기에 액세스하려면 계정(hybris에서)이 필요합니다.

1. 배포 파일을 필요한 위치(즉, &lt;hybris-root-directory>).
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
   >누르기 `Return` 필요한 경우.

1. 다음 파일을 추출된 hybris 배포의 루트 폴더로 다운로드합니다.

   ```
       <hybris-root-directory>
   ```


[파일 가져오기](/help/sites-deploying/assets/setup.groovy)

   >[!NOTE]
   >
   >hybris 5.6.0 이상의 경우 다음 setup.groovy를 사용하십시오.

   5.6.0 이상

[파일 가져오기](/help/sites-deploying/assets/setup-1.groovy)

1. 명령줄에서 다음을 실행하여 다음 작업을 수행합니다.

   * hybris 서버의 구성 업데이트(확장에서 필요한 경우)
   * 수정된 구성으로 hybris 서버를 다시 빌드합니다.
   * 서버 시작

   ```shell
   groovy setup.groovy
   cd bin/platform
   ant clean all
   sh hybrisserver.sh
   ```

   >[!NOTE]
   >
   >시스템에 따라 이러한 단계 중 일부를 완료하는 데 몇 분이 걸릴 수 있습니다.

1. 브라우저에서 **hybris 관리 콘솔** at:

   [http://localhost:9002](http://localhost:9002)

1. 클릭 **초기화** 그런 다음 초기화 작업을 확인합니다(기존 데이터를 삭제함).

   진행률이 콘솔에 표시되고 `FINISHED` 완료를 나타냅니다.

   >[!NOTE]
   >
   >시스템에 따라 완료하는 데 몇 분이 걸릴 수 있습니다.

### Geometrixx Outdoors 저장소 설정 {#setup-the-geometrixx-outdoors-store}

이 절차는 데모 스토어 - Geometrixx 온라인 을 업로드하고 구성합니다.

1. hybris 인스턴스를 시작합니다. 명령줄에서 다음을 실행합니다.

   ```shell
   cd <hybris-root-directory>/bin/platform
   sh hybrisserver.sh
   ```

1. 브라우저에서 **hybris 관리 콘솔** at:

   [https://localhost:9002/backoffice](https://localhost:9002/backoffice)

   다음 자격 증명을 사용합니다.
   * 사용자 이름: 관리
   * 암호: 님다

1. 사이드바 탐색에서 를 확장합니다. **시스템** 및 **도구**. 그런 다음 을(를) 선택합니다 **가져오기** 열다 **마법사: CSV 가져오기** 창을 엽니다.
1. 에서 **구성** 탭, **업로드** 다음 **파일 가져오기**:

[파일 가져오기](/help/sites-deploying/assets/geometrixx-outdoors-export.csv)

1. 설정 **로케일 설정** 변환:

   `en_US - English (United States)`

1. 를 엽니다. **리소스** 탭.
1. **업로드** 다음 **Media-Zip**:

[파일 가져오기](/help/sites-deploying/assets/geometrixx-outdoors-images.zip)

1. 클릭 **시작** 지정한 파일을 가져오려면 다음을 수행하십시오. 다음 **결과** 모든 로그 항목이 탭에 표시됩니다.

1. 클릭 **완료** 을 클릭하여 가져오기 창을 닫습니다.

1. 사이드바에서 **시스템**, 그런 다음 **도구**, 그런 다음 **가져오기**.

1. **업로드** 다음 **파일 가져오기**:

[파일 가져오기](/help/sites-deploying/assets/base-store.csv)

   hybris 5.7의 경우 다음을 사용하십시오.

[파일 가져오기](/help/sites-deploying/assets/base-store-5_7.csv)

1. 설정 **로케일 설정** 변환:

   `en_US - English (United States)`

1. 클릭 **시작** 지정한 파일을 가져오려면 다음을 수행하십시오. 다음 **결과** 모든 로그 항목이 탭에 표시됩니다.

1. 클릭 **완료** 을 클릭하여 가져오기 창을 닫습니다.

1. 이제 제품 조종실을 사용하여 가져온 카탈로그와 제품을 볼 수 있습니다.

   [http://localhost:9002/productcockpit](http://localhost:9002/productcockpit)
