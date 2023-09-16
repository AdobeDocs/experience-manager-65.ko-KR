---
title: SAP Commerce Cloud을 사용하여 eCommerce 구축
description: SAP Commerce Cloud과 함께 eCommerce를 배포하는 방법에 대해 알아봅니다.
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
exl-id: ecbd0097-c407-4581-bab2-4729a71df4a3
source-git-commit: b00ed4ed146b89aece9af1d267c890a360a236e9
workflow-type: tm+mt
source-wordcount: '714'
ht-degree: 2%

---

# SAP COMMERCE CLOUD{#sap-commerce-cloud}

>[!NOTE]
>
>이 페이지에는 hybris 웹 사이트에 대한 링크가 포함되어 있습니다. 특정 페이지의 경우 로그인할 계정이 필요합니다.

## SAP Commerce Cloud을 사용하여 eCommerce 배포 {#deploying-ecommerce-with-sap-commerce-cloud}

>[!NOTE]
>
>다음 절차는 다음 데모 카탈로그를 사용하여 배포를 보여 줍니다.
>
>`Geometrixx Outdoors Site English (US)`

배포 [필요한 전자 상거래 패키지](#packages-needed-for-ecommerce-with-hybris) 는 hybris 구현(데모 카탈로그 포함)에 제공된 대로 eCommerce 기능의 참조 구현과 함께 eCommerce 프레임워크의 전체 기능을 제공합니다

영어(미국) 분기( `/content/geometrixx-outdoors/en_US`Geometrixx Outdoors )을 클릭하여 제품에서 사용할 수 있습니다.

* [제품 정보](#productinformationwithcolorvariants) (해당되는 경우 색상 변형 포함)

* [장바구니 콘텐츠 개요](#shoppingcartcontentoverview)
* [고객 등록](#customersignup) 및 [고객 로그인](#customersignin)

* [Hybris 관리 콘솔에 액세스](#accesstothehybrismanagementconsole)

### 기술 요구 사항 - hybris 서버 {#technical-requirements-hybris-server}

이전 버전과의 호환성을 유지하면서 eCommerce Integration Framework의 hybris 확장이 Hybris 5(기본값)를 지원하도록 업데이트되었습니다 [하이브리스](/help/commerce/cif-classic/developing/sap-commerce-cloud.md#developing-for-hybris).

>[!NOTE]
>
>* 버전 18.11 이상을 지원합니다.
>* 를 실행하려면 Java™ 7이 필요합니다. [hybris 5 서버.](https://www.sap.com/products/crm.html)
* hybris 추가 기능, [Telco Accelerator](https://www.sap.com/products/crm.html)는 AEM 확장에서 지원되지 않습니다.
>

### Hybris가 있는 전자 상거래에 필요한 패키지 {#packages-needed-for-ecommerce-with-hybris}

eCommerce 기능을 설치하려면 다음을 수행해야 합니다.

* hybris 서버
* AEM 전자 상거래 프레임워크:

   * 표준 AEM 설치의 일부입니다.

* AEM Geometrixx 전체 패키지:

   * `cq-geometrixx-all-pkg`

* AEM hybris 콘텐츠 패키지:

   * `cq-hybris-content-6.3.2`
   * hybris별 API 구현
   * `cq-geometrixx-hybris-content-6.3.2`
   * hybris 사용을 보여주는 참조 구현( `geometrixx-outdoors/en_US`)

### hybris를 사용한 eCommerce 설치 {#installation-of-ecommerce-with-hybris}

데모 카탈로그, Geometrixx Outdoors을 사용하여 완전한 구성을 설치하려면 다음 기본 단계를 수행하십시오.

1. [AEM 설치](/help/sites-deploying/deploy.md).
1. Geometrixx 전체 패키지 설치

   1. ` [cq-geometrixx-all-pkg](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq60/product/cq-geometrixx-all-pkg)`

1. 를 사용하여 데모 콘텐츠 패키지 설치 [패키지 관리자](/help/sites-administering/package-manager.md):

   1. ` [cq-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-hybris-content)`
   1. ` [cq-geometrixx-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-geometrixx-hybris-content)`

1. [hybris 서버 다운로드 및 빌드](#download-and-build-your-hybris-server).
1. 전자 상거래 엔진에서 카탈로그를 구성합니다.

   1. [Geometrixx Outdoor Store 설정](#setup-the-geometrixx-outdoors-store).

1. [작성자](/help/sites-authoring/qg-page-authoring.md) AEM에서 필요한 모든 보조 페이지.

>[!CAUTION]
>
hybris 서버를 사용하려면 별도의 hybris 라이센스가 필요합니다.

>[!NOTE]
>
개발자용, [API 설명서](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation) 을 다운로드할 수도 있습니다.

### hybris 서버 다운로드 및 구축 {#download-and-build-your-hybris-server}

이 절차의 단계는 hybris 서버를 다운로드하고 빌드합니다. 또한 hybris와 cq 간의 연결에 필요한 초기 구성을 만듭니다. 그런 다음 확장 기능을 기본 설정과 함께 사용할 수 있습니다.

>[!CAUTION]
>
5.5.1 이전 버전의 Hybris는 지원되지 않습니다.

>[!NOTE]
>
이 작업을 완료하려면 [그루비](https://groovy-lang.org/) 이(가) 시스템에 설치되었습니다.

1. 다운로드 **hybris Commerce Suite** hybris 다운로드 사이트에서 배포

   >[!CAUTION]
   >
   이에 액세스하려면 (hybris에서) 계정이 필요합니다.

1. 배포 파일을 필요한 위치에 압축 해제합니다(참조: &lt;hybris-root-directory>).
1. 명령줄에서 다음을 실행합니다.

   ```shell
   cd <hybris-root-directory>/bin/platform
   . ./setantenv.sh
   ant clean all
   cd ../..
   ```

   >[!NOTE]
   >
   실행 시:
   >
   `ant clean all`
   >
   누르기 `Return` 필요한 경우.

1. 다음 파일을 추출된 hybris 배포의 루트 폴더에 다운로드합니다.

   ```
       <hybris-root-directory>
   ```


[파일 가져오기](/help/sites-deploying/assets/setup.groovy)

   >[!NOTE]
   >
   hybris 5.6.0 이상의 경우 setup.groovy를 사용합니다.

   5.6.0 이상

[파일 가져오기](/help/sites-deploying/assets/setup-1.groovy)

1. 명령줄에서 다음을 실행하여 다음을 수행합니다.

   * hybris 서버의 구성을 업데이트합니다( 확장에 필요한 경우)
   * 수정된 구성으로 hybris 서버 다시 빌드
   * 서버 시작

   ```shell
   groovy setup.groovy
   cd bin/platform
   ant clean all
   sh hybrisserver.sh
   ```

   >[!NOTE]
   >
   시스템에 따라 이러한 몇 가지 단계를 완료하는 데 몇 분이 걸릴 수 있습니다.

1. 브라우저에서 다음 위치로 이동합니다. **hybris 관리 콘솔** 위치:

   [http://localhost:9002](http://localhost:9002)

1. 클릭 **초기화** 그런 다음 초기화 작업을 확인합니다(기존 데이터가 삭제됨).

   진행 상황이 콘솔에 표시되며, `FINISHED` 완료를 나타냅니다.

   >[!NOTE]
   >
   시스템에 따라 완료하는 데 몇 분 정도 걸릴 수 있습니다.

### Geometrixx Outdoors 저장소 설정 {#setup-the-geometrixx-outdoors-store}

이 절차에서는 데모 스토어 - Geometrixx 온라인을 업로드하고 구성합니다.

1. hybris 인스턴스를 시작합니다. 명령줄에서 다음을 실행합니다.

   ```shell
   cd <hybris-root-directory>/bin/platform
   sh hybrisserver.sh
   ```

1. 브라우저에서 다음 위치로 이동합니다. **hybris 관리 콘솔** 위치:

   [https://localhost:9002/backoffice](https://localhost:9002/backoffice)

   다음 자격 증명 사용:
   * 사용자 이름: admin
   * 암호: nimda

1. 사이드바 탐색에서 를 확장합니다. **시스템** 및 **도구**. 그런 다음 을 선택합니다 **가져오기** 을(를) 열려면 **마법사: CSV 가져오기** 창.
1. 다음에서 **구성** 탭, **업로드** 다음 **파일 가져오기**:

[파일 가져오기](/help/sites-deploying/assets/geometrixx-outdoors-export.csv)

1. 설정 **로케일 설정** 끝:

   `en_US - English (United States)`

1. 를 엽니다. **리소스** 탭.
1. **업로드** 다음 **Media-Zip**:

[파일 가져오기](/help/sites-deploying/assets/geometrixx-outdoors-images.zip)

1. 클릭 **시작** 을 눌러 지정된 파일을 가져옵니다. 다음 **결과** 탭에는 모든 로그 항목이 표시됩니다.

1. 클릭 **완료** 가져오기 창을 닫습니다.

1. 사이드바에서 을 선택합니다. **시스템**, 그런 다음 **도구**, 그런 다음 **가져오기**.

1. **업로드** 다음 **파일 가져오기**:

[파일 가져오기](/help/sites-deploying/assets/base-store.csv)

   hybris 5.7의 경우 다음을 사용합니다.

[파일 가져오기](/help/sites-deploying/assets/base-store-5_7.csv)

1. 설정 **로케일 설정** 끝:

   `en_US - English (United States)`

1. 클릭 **시작** 을 눌러 지정된 파일을 가져옵니다. 다음 **결과** 탭에는 모든 로그 항목이 표시됩니다.

1. 클릭 **완료** 가져오기 창을 닫습니다.

1. 이제 제품 관리실을 사용하여 가져온 카탈로그 및 제품을 볼 수 있습니다.

   [http://localhost:9002/productcockpit](http://localhost:9002/productcockpit)
