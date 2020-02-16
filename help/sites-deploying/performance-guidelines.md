---
title: 성능 지침
seo-title: 성능 지침
description: 이 문서에서는 AEM 배포의 성능을 최적화하는 방법에 대한 일반적인 지침을 제공합니다.
seo-description: 이 문서에서는 AEM 배포의 성능을 최적화하는 방법에 대한 일반적인 지침을 제공합니다.
uuid: 38cf8044-9ff9-48df-a843-43f74b0c0133
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 9ccbc39e-aea7-455e-8639-9193abc1552f
translation-type: tm+mt
source-git-commit: a678716e2c0520891e4228bc49b075f070ea45b7

---


# 성능 지침{#performance-guidelines}

이 페이지에서는 AEM 배포의 성능을 최적화하는 방법에 대한 일반적인 지침을 제공합니다. AEM을 처음 사용하는 경우 성능 지침을 읽기 전에 다음 페이지를 살펴보십시오.

* [AEM Basic 개념](/help/sites-deploying/deploy.md#basic-concepts)
* [AEM의 스토리지 개요](/help/sites-deploying/storage-elements-in-aem-6.md#overview-of-storage-in-aem)
* [권장 배포](/help/sites-deploying/recommended-deploys.md)
* [기술 요구 사항](/help/sites-deploying/technical-requirements.md)

아래 그림에는 AEM에 사용할 수 있는 배포 옵션(모든 옵션을 보려면 스크롤)이 있습니다.

<table>
 <tbody>
  <tr>
   <td><p><strong>AEM</strong></p> <p><strong>제품</strong></p> </td>
   <td><p><strong>토폴로지</strong></p> </td>
   <td><p><strong>운영 체제</strong></p> </td>
   <td><p><strong>응용 프로그램 서버</strong></p> </td>
   <td><p><strong>JRE</strong></p> </td>
   <td><p><strong>보안</strong></p> </td>
   <td><p><strong>마이크로 커널</strong></p> </td>
   <td><p><strong>데이터 저장소</strong></p> </td>
   <td><p><strong>색인 생성</strong></p> </td>
   <td><p><strong>웹 서버</strong></p> </td>
   <td><p><strong>브라우저</strong></p> </td>
   <td><p><strong>Marketing Cloud</strong></p> </td>
  </tr>
  <tr>
   <td><p>사이트</p> </td>
   <td><p>비-HA</p> </td>
   <td><p>Windows</p> </td>
   <td><p>CQSE</p> </td>
   <td><p>Oracle</p> </td>
   <td><p>LDAP</p> </td>
   <td><p>Tar</p> </td>
   <td><p>세그먼트</p> </td>
   <td><p>속성</p> </td>
   <td><p>Apache</p> </td>
   <td><p>Edge</p> </td>
   <td><p>타겟</p> </td>
  </tr>
  <tr>
   <td><p>자산</p> </td>
   <td><p>Publish-HA</p> </td>
   <td><p>Solaris</p> </td>
   <td><p>WebLogic</p> </td>
   <td><p>IBM</p> </td>
   <td><p>SAML</p> </td>
   <td><p>MongoDB</p> </td>
   <td><p>파일</p> </td>
   <td><p>Lucene</p> </td>
   <td><p>IIS</p> </td>
   <td><p>IE</p> </td>
   <td><p>분석</p> </td>
  </tr>
  <tr>
   <td><p>커뮤니티</p> </td>
   <td><p>작성자-CS</p> </td>
   <td><p>Red Hat</p> </td>
   <td><p>WebSphere</p> </td>
   <td><p>HP</p> </td>
   <td><p>Oauth</p> </td>
   <td><p>RDB/Oracle</p> </td>
   <td><p>S3/Azure</p> </td>
   <td><p>Solr</p> </td>
   <td><p>iPlanet</p> </td>
   <td><p>FireFox</p> </td>
   <td><p>캠페인</p> </td>
  </tr>
  <tr>
   <td><p>양식</p> </td>
   <td><p>작성자-오프로드</p> </td>
   <td><p>HP-UX</p> </td>
   <td><p>Tomcat</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>RDB/DB2</p> </td>
   <td><p>MongoDB</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>Chrome</p> </td>
   <td><p>Social</p> </td>
  </tr>
  <tr>
   <td><p>모바일</p> </td>
   <td><p>작성자-클러스터</p> </td>
   <td><p>IBM AIX</p> </td>
   <td><p>JBoss</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>RDB/MySQL</p> </td>
   <td><p>RDBMS</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>Safari</p> </td>
   <td><p>속성을 확인하는</p> </td>
  </tr>
  <tr>
   <td><p>다중 사이트</p> </td>
   <td><p>ASRP</p> </td>
   <td><p>SUSE</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>RDB/SQLS파섹</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>자산</p> </td>
  </tr>
  <tr>
   <td><p>상거래</p> </td>
   <td><p>MSRP</p> </td>
   <td><p>Apple OS</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>활성화</p> </td>
  </tr>
  <tr>
   <td><p>다이내믹 미디어</p> </td>
   <td><p>JSRP</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>모바일</p> </td>
  </tr>
  <tr>
   <td><p>브랜드 포털</p> </td>
   <td><p>J2E</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>AoD</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>LiveFyre</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>스크린</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>문서 보안</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>프로세스 관리</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>데스크탑 앱</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>성능 지침은 주로 AEM Sites에 적용됩니다.

## 성능 지침 사용 시기 {#when-to-use-the-performance-guidelines}

다음과 같은 경우에는 성능 지침을 사용해야 합니다.

* **최초 배포**:AEM Sites 또는 Assets를 처음 배포할 계획이라면 마이크로 커널, 노드 스토어 및 데이터 저장소를 구성할 때 사용할 수 있는 옵션을 이해하는 것이 중요합니다(기본 설정과 비교). 예를 들어 TarMK용 데이터 저장소의 기본 설정을 파일 데이터 저장소로 변경합니다.
* **새 버전으로**&#x200B;업그레이드:새 버전으로 업그레이드할 때 실행 환경과 비교하여 성능 차이를 이해하는 것이 중요합니다. 예를 들어 AEM 6.1에서 6.2로 업그레이드하거나 AEM 6.0 CRX2에서 6.2 OAK로 업그레이드할 수 있습니다.
* **응답 시간이 느립니다**.선택한 Nodestore 아키텍처가 요구 사항을 충족하지 않을 경우 다른 토폴로지 옵션과 비교하여 성능 차이를 이해하는 것이 중요합니다. 예를 들어 MongoMK 대신 TarMK를 배포하거나 Amazon S3 또는 Microsoft Azure Data Store 대신 파일 데이터 저장소를 사용합니다.
* **작성자**&#x200B;추가:권장 TarMK 토폴로지가 성능 요구 사항을 충족하지 않고 Author 노드의 업사이징이 사용 가능한 최대 용량에 도달하면 MongoMK를 3개 이상의 Author 노드에서 사용하는 것과 비교하여 성능 차이를 이해하는 것이 중요합니다. 예를 들어 TarMK 대신 MongoMK를 배포합니다.
* **추가 컨텐츠**:권장 데이터 저장소 아키텍처가 요구 사항을 충족하지 않을 경우 다른 데이터 저장소 옵션과 비교하여 성능 차이를 이해하는 것이 중요합니다. 예:파일 데이터 저장소 대신 Amazon S3 또는 Microsoft Azure 데이터 저장소를 사용합니다.

## 소개 {#introduction}

이 장에서는 AEM 아키텍처 및 가장 중요한 구성 요소에 대한 일반적인 개요를 제공합니다. 또한 개발 지침을 제공하며 TarMK 및 MongoMK 벤치마크 테스트에 사용되는 테스트 시나리오에 대해 설명합니다.

### AEM Platform {#the-aem-platform}

AEM 플랫폼은 다음 구성 요소로 구성됩니다.

![chlimage_1](assets/chlimage_1a.png)

AEM 플랫폼에 대한 자세한 내용은 AEM이란 [것을 참조하십시오](/help/sites-deploying/deploy.md#what-is-aem).

### AEM 아키텍처 {#the-aem-architecture}

AEM 배포에는 세 가지 중요한 구성 요소가 있습니다. 컨텐츠 **작성자** , 편집자 및 승인자가 컨텐츠를 만들고 검토할 때 사용하는 작성자 인스턴스. 컨텐츠가 승인되면 최종 사용자가 액세스할 수 있는 **게시 인스턴스라는** 두 번째 인스턴스 유형에 게시됩니다. 세 번째 빌딩 블록은 **캐싱** 및 URL 필터링을 처리하고 웹 서버에 설치되는 모듈인 Dispatcher입니다. AEM 아키텍처에 대한 자세한 내용은 일반적인 배포 [시나리오를 참조하십시오](/help/sites-deploying/deploy.md#typical-deployment-scenarios).

![chlimage_1-1](assets/chlimage_1-1a.png)

### 마이크로 커널 {#micro-kernels}

마이크로 커널은 AEM에서 지속성 관리자 역할을 합니다. AEM에 사용되는 세 가지 유형의 마이크로 커널이 있습니다.TarMK, MongoDB 및 관계형 데이터베이스(제한적 지원 아래). 고려하고 있는 인스턴스의 목적 및 배포 유형에 따라 본인의 요구에 맞는 것을 하나 선택합니다. 마이크로 커널에 대한 자세한 내용은 권장 [배포 페이지를](/help/sites-deploying/recommended-deploys.md) 참조하십시오.

![chlimage_1-2](assets/chlimage_1-2a.png)

### 노데스토르 {#nodestore}

AEM에서 이진 데이터는 컨텐츠 노드와 독립적으로 저장할 수 있습니다. 이진 데이터가 저장되는 위치를 데이터 **저장소라고**&#x200B;하고 컨텐츠 노드 및 속성의 위치는 노드 **저장소라고 합니다**.

>[!NOTE]
>
>Adobe에서는 TarMK가 AEM 작성자 및 게시 인스턴스 모두에 대해 고객이 사용하는 기본 지속성 기술로 권장됩니다.

>[!CAUTION]
>
>관계형 데이터베이스 마이크로 커널이 제한적으로 지원됩니다. 이 [유형의 마이크로 커널을](https://helpx.adobe.com/marketing-cloud/contact-support.html) 사용하기 전에 Adobe 고객 지원 센터에 문의하십시오.

![chlimage_1-3](assets/chlimage_1-3a.png)

### Data Store {#data-store}

많은 바이너리를 처리할 때 성능을 최대화하기 위해 기본 노드 저장소 대신 외부 데이터 저장소를 사용하는 것이 좋습니다. 예를 들어 프로젝트에 많은 미디어 에셋이 필요한 경우 파일 또는 Azure/S3 데이터 저장소 아래에 저장하면 MongoDB에 직접 저장하는 것보다 더 빠르게 액세스할 수 있습니다.

사용 가능한 구성 옵션에 대한 자세한 내용은 노드 및 데이터 [저장소 구성을 참조하십시오](/help/sites-deploying/data-store-config.md).

>[!NOTE]
>
>Adobe는 Adobe Managed Services를 사용하여 Azure 또는 Amazon Web Services(AWS)에 AEM을 배포하는 옵션을 선택하는 것이 좋습니다. 고객은 이러한 클라우드 컴퓨팅 환경에서 AEM을 배포 및 운영하는 경험과 기술을 보유한 팀의 혜택을 받을 수 있습니다. Adobe Managed Services에 대한 [추가 설명서를 참조하십시오](https://www.adobe.com/marketing-cloud/enterprise-content-management/managed-services-cloud-platform.html?aemClk=t).
>
>Azure 또는 AWS에 AEM을 배포하는 방법에 대한 권장 사항은 Adobe Managed Services 외부에서 클라우드 공급자나 원하는 클라우드 환경에서 AEM 배포를 지원하는 Adobe 파트너와 직접 작업하는 것이 좋습니다. 선택한 클라우드 제공업체 또는 파트너는 고객의 특정 성능, 로드, 확장성 및 보안 요구 사항을 충족하기 위해 지원하는 아키텍처의 크기 지정, 설계 및 구현을 책임지고 있습니다.
>
>자세한 내용은 [기술 요구 사항](/help/sites-deploying/technical-requirements.md#supported-platforms) 페이지를 참조하십시오.

### 검색 {#search-features}

이 섹션에 나열된 것은 AEM과 함께 사용되는 사용자 지정 인덱스 공급자입니다. 색인에 대한 자세한 내용은 Oak 쿼리 [및 색인을 참조하십시오](/help/sites-deploying/queries-and-indexing.md).

>[!NOTE]
>
>대부분의 배포의 경우 Lucene 색인을 사용하는 것이 좋습니다. 전문적이고 복잡한 배포에서는 Solr를 사용해야 합니다.

![chlimage_1-4](assets/chlimage_1-4a.png)

### 개발 지침 {#development-guidelines}

**성능 및 확장성을**&#x200B;목표로 하는 AEM용으로 개발해야 합니다. 아래 제시된 우수 사례는 다음과 같습니다.

**DO**

* 프레젠테이션, 논리 및 컨텐츠 분리를 적용할 수 있습니다.
* 기존 AEM API 사용(예:Sling) 및 툴(예:복제)
* 실제 컨텐츠 컨텍스트에서 개발
* 최적의 액세서빌러티를 위한 개발
* 저장 수 최소화(예:임시 워크플로우 사용
* 모든 HTTP 끝점이 RESTful인지 확인
* JCR 관찰 범위 제한
* 비동기 스레드에 주의하십시오.

**DON&#39;T**

* 가능한 경우 JCR API를 직접 사용하지 마십시오
* /libs를 변경하지 말고 오버레이를 사용하십시오.
* 가능하면 쿼리를 사용하지 마십시오
* Sling Bindings를 사용하여 Java 코드로 OSGi 서비스를 가져오지 말고 대신 사용하십시오.

   * @DS 구성 요소의 참조
   * @Sling 모델에서 삽입
   * Sightly 사용 클래스의 sling.getService()
   * sling.getService() in a JSP
   * a ServiceTracker
   * osgi 서비스 레지스트리에 대한 직접 액세스

AEM에서 개발하는 방법에 대한 자세한 내용은 개발 [- 기본 사항을 참조하십시오](/help/sites-developing/the-basics.md). 추가 우수 사례를 보려면 개발 [우수 사례를 참조하십시오](/help/sites-developing/best-practices.md).

### 벤치마크 시나리오 {#benchmark-scenarios}

>[!NOTE]
>
>이 페이지에 표시된 모든 벤치마크 테스트가 실험실 설정에서 수행되었습니다.

아래에 설명된 테스트 시나리오는 TarMK, MongoMk 및 TarMK 및 MongoMk 장의 벤치마크 섹션에 사용됩니다. 특정 벤치마크 테스트에 사용된 시나리오를 보려면 기술 사양 [표에서 시나리오 필드를](/help/sites-deploying/performance-guidelines.md#tarmk-performance-benchmark) 참조하십시오.

**단일 제품 시나리오**

AEM Assets:

* 사용자 상호 작용:자산 검색/자산 검색/자산 다운로드/자산 메타데이터 읽기/자산 메타데이터 업데이트/자산 업로드/자산 업로드 워크플로우 실행
* 실행 모드:동시 사용자, 사용자당 단일 상호 작용

**제품 혼합 시나리오**

AEM Sites + 자산:

* 사이트 사용자 상호 작용:아티클 페이지 읽기/페이지 읽기/단락 만들기/단락 편집/콘텐츠 페이지 만들기/콘텐츠 페이지 활성화/작성자 검색
* 자산 사용자 상호 작용:자산 검색/자산 검색/자산 다운로드/자산 메타데이터 읽기/자산 메타데이터 업데이트/자산 업로드/자산 업로드 워크플로우 실행
* 실행 모드:동시 사용자, 사용자당 상호 작용 혼합

**수직 사용 사례 시나리오**

미디어:

* 문서 페이지 읽기(27.4%), 읽기 페이지(10.9%), 세션 만들기(2.6%), 콘텐츠 페이지 활성화(1.7%), 콘텐츠 페이지 만들기(0.4%), 단락 만들기(4.3%), 단락 편집(0.9%), 이미지 구성 요소 검색(0.9%), 자산(20%), 자산 메타데이터 읽기(8.5%), 자산 다운로드(4.2%), 자산 검색(0.2%), 자산 메타데이터 업데이트(2.4%), 자산 업로드(1.2%), 프로젝트 검색(4.9%), 프로젝트 읽기(6.6%), 프로젝트 추가(1.2 %), 프로젝트 추가 사이트(1.2%), 프로젝트 만들기(0.1%), 작성자 검색(0.4%)
* 실행 모드:동시 사용자, 사용자당 상호 작용 혼합

## TarMK {#tarmk}

이 장에서는 최소 아키텍처 요구 사항과 설정 구성을 지정하는 TarMK에 대한 일반적인 성능 지침을 제공합니다. 벤치마크 테스트도 명확하게 하기 위해 제공됩니다.

Adobe에서는 TarMK가 AEM 작성자 및 게시 인스턴스 모두에 대해 모든 배포 시나리오에서 고객이 사용하는 기본 지속성 기술로 권장하고 있습니다.

TarMK에 대한 자세한 내용은 배포 [시나리오](/help/sites-deploying/recommended-deploys.md#deployment-scenarios) 및 Tar 스토리지를 [참조하십시오](/help/sites-deploying/storage-elements-in-aem-6.md#tar-storage).

### TarMK 최소 아키텍처 지침 {#tarmk-minimum-architecture-guidelines}

>[!NOTE]
>
>아래에 명시된 최소 아키텍처 지침은 제작 환경 및 트래픽 사이트에 적용됩니다. AEM을 실행하는 데 필요한 **최소 사양은** [](/help/sites-deploying/technical-requirements.md#prerequisites) 아닙니다.

TarMK를 사용할 때 뛰어난 성능을 얻으려면 다음 아키텍처에서 시작해야 합니다.

* 하나의 작성자 인스턴스
* 두 개의 게시 인스턴스
* Two Dispatcher

아래 그림에는 AEM 사이트 및 AEM 자산에 대한 아키텍처 지침이 나와 있습니다.

>[!NOTE]
>
>파일 데이터 저장소가 공유되는 **경우 바이너리** 없는 복제를 켜야 합니다.

**AEM Sites에 대한 Tar 아키텍처 지침**

![chlimage_1-5](assets/chlimage_1-5a.png)

**AEM 자산에 대한 Tar 아키텍처 지침**

![chlimage_1-6](assets/chlimage_1-6a.png)

### TarMK 설정 지침 {#tarmk-settings-guideline}

성능을 높이려면 아래 나와 있는 설정 지침을 따라야 합니다. 설정을 변경하는 방법에 대한 지침은 이 페이지를 [참조하십시오](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html).

<table>
 <tbody>
  <tr>
   <td><strong>설정</strong></td>
   <td><strong>매개 변수</strong></td>
   <td><strong>값</strong></td>
   <td><strong>설명</strong></td>
  </tr>
  <tr>
   <td>Sling 작업 큐</td>
   <td><code>queue.maxparallel</code></td>
   <td>값을 CPU 코어 수의 반으로 설정합니다. </td>
   <td>기본적으로 작업 대기열당 동시 스레드 수는 CPU 코어 수와 같습니다.</td>
  </tr>
  <tr>
   <td>[MOCK] Granite Temporary Workflow Queue</td>
   <td><code>Max Parallel</code></td>
   <td>값을 CPU 코어 수의 반으로 설정</td>
   <td> </td>
  </tr>
  <tr>
   <td>JVM 매개 변수</td>
   <td><p><code>Doak.queryLimitInMemory</code></p> <p><code>Doak.queryLimitReads</code></p> <p><code>Dupdate.limit</code></p> <p><code>Doak.fastQuerySize</code></p> </td>
   <td><p>500000</p> <p>100000</p> <p>250000</p> <p>True</p> </td>
   <td>AEM 시작 스크립트에 이러한 JVM 매개 변수를 추가하여 광범위한 쿼리가 시스템을 오버로드하지 못하도록 합니다.</td>
  </tr>
  <tr>
   <td>Lucene 인덱스 구성</td>
   <td><p><code>CopyOnRead</code></p> <p><code>CopyOnWrite</code></p> <p><code>Prefetch Index Files</code></p> </td>
   <td><p>활성화됨</p> <p>활성화됨</p> <p>활성화됨</p> </td>
   <td>사용 가능한 매개 변수에 대한 자세한 내용은 <a href="https://jackrabbit.apache.org/oak/docs/query/lucene.html">이 페이지를</a>참조하십시오.</td>
  </tr>
  <tr>
   <td>데이터 저장소 = S3 데이터 저장소</td>
   <td><p><code>maxCachedBinarySize</code></p> <p><code>cacheSizeInMB</code></p> </td>
   <td><p>1048576(1MB) 이하</p> <p>최대 더미 크기의 2-10%</p> </td>
   <td>데이터 <a href="/help/sites-deploying/data-store-config.md#data-store-configurations">저장소 구성을 참조하십시오</a>.</td>
  </tr>
  <tr>
   <td>DAM 자산 업데이트 워크플로우</td>
   <td><code>Transient Workflow</code></td>
   <td>선택함</td>
   <td>이 워크플로우는 자산 업데이트를 관리합니다.</td>
  </tr>
  <tr>
   <td>DAM 메타 데이터 원본에 쓰기</td>
   <td><code>Transient Workflow</code></td>
   <td>선택함</td>
   <td>이 워크플로우는 원본 바이너리에 대한 XMP 다시 쓰기를 관리하고 JCR에서 마지막으로 수정한 날짜를 설정합니다.</td>
  </tr>
 </tbody>
</table>

### TarMK 성능 벤치마크 {#tarmk-performance-benchmark}

#### 기술 사양 {#technical-specifications}

벤치마크 테스트는 다음 사양에 대해 수행되었습니다.

|  | **작성자 노드** |
|---|---|
| 서버 | Bare Metal 하드웨어(HP) |
| 운영 체제 | RedHat Linux |
| CPU/코어 | Intel(R) Xeon(R) CPU E5-2407 @2.40GHz, 8 코어 |
| RAM | 32GB |
| 디스크 | 자석 |
| Java | Oracle JRE 버전 8 |
| JVM Heap | 16GB |
| 제품 | AEM 6.2 |
| 노데스토르 | TarMK |
| 데이터 저장소 | 파일 DS |
| 시나리오 | 단일 제품:자산/동시 스레드 30개 |

#### 성능 벤치마크 결과 {#performance-benchmark-results}

>[!NOTE]
>
>아래에 표시된 숫자는 기준선으로 1로 표준화되었으며 실제 처리량은 아닙니다.

![chlimage_1-7](assets/chlimage_1-7a.png) chlimage_ ![1-8](assets/chlimage_1-8a.png)

## MongoMK {#mongomk}

TarMK보다 MongoMK 지속성 백엔드를 선택하는 주된 이유는 인스턴스를 가로로 크기 조절하기 위함입니다. 즉, 두 개 이상의 활성 작성자 인스턴스가 항상 실행되고 MongoDB를 지속성 스토리지 시스템으로 사용할 수 있습니다. 일반적으로 모든 동시 작성 활동을 지원하는 단일 서버의 CPU 및 메모리 용량이 더 이상 지속 가능하지 않다는 사실에서 두 개 이상의 작성자 인스턴스를 실행해야 합니다.

TarMK에 대한 자세한 내용은 배포 시나리오 [및](/help/sites-deploying/recommended-deploys.md#deployment-scenarios) Mongo 스토리지를 [참조하십시오](/help/sites-deploying/storage-elements-in-aem-6.md#mongo-storage).

### MongoMK 최소 아키텍처 지침 {#mongomk-minimum-architecture-guidelines}

MongoMK를 사용할 때 뛰어난 성능을 얻으려면 다음 아키텍처에서 시작해야 합니다.

* 3개의 작성자 인스턴스
* 두 개의 게시 인스턴스
* 세 개의 MongoDB 인스턴스
* Two Dispatcher

>[!NOTE]
>
>운영 환경에서 MongoDB는 항상 운영 및 2개의 보조가 있는 복제본 세트로 사용됩니다. 읽기 및 쓰기는 주 서버로 이동하고 읽기는 보조 서버로 이동할 수 있습니다. 스토리지를 사용할 수 없는 경우 보조 노드 중 하나를 중재자로 대체할 수 있지만 MongoDB 복제본 세트는 항상 인스턴스 수가 너무 적어야 합니다.

>[!NOTE]
>
>파일 데이터 저장소가 공유되는 **경우 바이너리** 없는 복제를 켜야 합니다.

![chlimage_1-9](assets/chlimage_1-9a.png)

### MongoMK 설정 지침 {#mongomk-settings-guidelines}

성능을 높이려면 아래 나와 있는 설정 지침을 따라야 합니다. 설정을 변경하는 방법에 대한 지침은 이 페이지를 [참조하십시오](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html).

<table>
 <tbody>
  <tr>
   <td><strong>설정</strong></td>
   <td><strong>매개 변수</strong></td>
   <td><strong>값(기본값)</strong></td>
   <td><strong>설명</strong></td>
  </tr>
  <tr>
   <td>Sling 작업 큐</td>
   <td><code>queue.maxparallel</code></td>
   <td>값을 CPU 코어 수의 반으로 설정합니다. </td>
   <td>기본적으로 작업 대기열당 동시 스레드 수는 CPU 코어 수와 같습니다.</td>
  </tr>
  <tr>
   <td>[MOCK] Granite Temporary Workflow Queue</td>
   <td><code>Max Parallel</code></td>
   <td>값을 CPU 코어 수의 반으로 설정합니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td>JVM 매개 변수</td>
   <td><p><code>Doak.queryLimitInMemory</code></p> <p><code>Doak.queryLimitReads</code></p> <p><code>Dupdate.limit</code></p> <p><code>Doak.fastQuerySize</code></p> <p><code>Doak.mongo.maxQueryTimeMS</code></p> </td>
   <td><p>500000</p> <p>100000</p> <p>250000</p> <p>True</p> <p>60000</p> </td>
   <td>AEM 시작 스크립트에 이러한 JVM 매개 변수를 추가하여 광범위한 쿼리가 시스템을 오버로드하지 못하도록 합니다.</td>
  </tr>
  <tr>
   <td>Lucene 인덱스 구성</td>
   <td><p><code>CopyOnRead</code></p> <p><code>CopyOnWrite</code></p> <p><code>Prefetch Index Files</code></p> </td>
   <td><p>활성화됨</p> <p>활성화됨</p> <p>활성화됨</p> </td>
   <td>사용 가능한 매개 변수에 대한 자세한 내용은 <a href="https://jackrabbit.apache.org/oak/docs/query/lucene.html">이 페이지를</a>참조하십시오.</td>
  </tr>
  <tr>
   <td>데이터 저장소 = S3 데이터 저장소</td>
   <td><p><code>maxCachedBinarySize</code></p> <p><code>cacheSizeInMB</code></p> </td>
   <td><p>1048576(1MB) 이하</p> <p>최대 더미 크기의 2-10%</p> </td>
   <td>데이터 <a href="/help/sites-deploying/data-store-config.md#data-store-configurations">저장소 구성을 참조하십시오</a>.</td>
  </tr>
  <tr>
   <td>DocumentNodeStoreService</td>
   <td><p><code>cache</code></p> <p><code>nodeCachePercentage</code></p> <p><code>childrenCachePercentage</code></p> <p><code>diffCachePercentage</code></p> <p><code>docChildrenCachePercentage</code></p> <p><code>prevDocCachePercentage</code></p> <p><code>persistentCache</code></p> </td>
   <td><p>2048</p> <p>35 (25)</p> <p>20 (10)</p> <p>30 (5)</p> <p>10 (3)</p> <p>4 (4)</p> <p>./cache,size=2048,binary=0,-compact,-compress</p> </td>
   <td><p>캐시의 기본 크기는 256MB로 설정됩니다.</p> <p>캐시 무효화를 수행하는 데 걸리는 시간에 영향을 줍니다.</p> </td>
  </tr>
  <tr>
   <td>오크 관측</td>
   <td><p><code>thread pool</code></p> <p><code>length</code></p> </td>
   <td><p>최소 및 최대 = 20</p> <p>50000</p> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### MongoMK 성능 벤치마크 {#mongomk-performance-benchmark}

### 기술 사양 {#technical-specifications-1}

벤치마크 테스트는 다음 사양에 대해 수행되었습니다.

|  | **작성자 노드** | **MongoDB 노드** |
|---|---|---|
| 서버 | Bare Metal 하드웨어(HP) | Bare Metal 하드웨어(HP) |
| 운영 체제 | RedHat Linux | RedHat Linux |
| CPU/코어 | Intel(R) Xeon(R) CPU E5-2407 @2.40GHz, 8 코어 | Intel(R) Xeon(R) CPU E5-2407 @2.40GHz, 8 코어 |
| RAM | 32GB | 32GB |
| 디스크 | 마그네틱 - 1k IOPS 이상 | 마그네틱 - 1k IOPS 이상 |
| Java | Oracle JRE 버전 8 | N/A |
| JVM Heap | 16GB | N/A |
| 제품 | AEM 6.2 | MongoDB 3.2 WiredTiger |
| 노데스토르 | MongoMK | N/A |
| 데이터 저장소 | 파일 DS | N/A |
| 시나리오 | 단일 제품:자산/동시 스레드 30개 | 단일 제품:자산/동시 스레드 30개 |

### 성능 벤치마크 결과 {#performance-benchmark-results-1}

>[!NOTE]
>
>아래에 표시된 숫자는 기준선으로 1로 표준화되었으며 실제 처리량은 아닙니다.

![chlimage_1-10](assets/chlimage_1-10a.png) chlimage_ ![1-11](assets/chlimage_1-11a.png)

## TarMK와 MongoMK {#tarmk-vs-mongomk}

두 가지 중 하나를 선택할 때 고려해야 하는 기본 규칙은 TarMK가 성능용으로 설계된 반면 MongoMK는 확장성을 위해 사용됩니다. Adobe에서는 TarMK가 AEM 작성자 및 게시 인스턴스 모두에 대해 모든 배포 시나리오에서 고객이 사용하는 기본 지속성 기술로 권장하고 있습니다.

TarMK보다 MongoMK 지속성 백엔드를 선택하는 주된 이유는 인스턴스를 가로로 크기 조절하기 위함입니다. 즉, 두 개 이상의 활성 작성자 인스턴스가 항상 실행되고 MongoDB를 지속성 스토리지 시스템으로 사용할 수 있습니다. 일반적으로 두 개 이상의 작성자 인스턴스를 실행해야 하는 이유는 모든 동시 작성 활동을 지원하는 단일 서버의 CPU 및 메모리 용량이 더 이상 지속되지 않는다는 점입니다.

TarMK와 MongoMK에 대한 자세한 내용은 권장 [배포를 참조하십시오](/help/sites-deploying/recommended-deploys.md#microkernels-which-one-to-use).

### TarMK와 MongoMk 지침 {#tarmk-vs-mongomk-guidelines}

**TarMK의 이점**

* 컨텐츠 관리 애플리케이션을 위해 특별히 구축
* 모든 파일 기반의 백업 툴을 사용하여 파일을 항상 일관되게 백업
* 페일오버 메커니즘을 제공합니다. 자세한 내용은 [콜드](/help/sites-deploying/tarmk-cold-standby.md) 대기 를 참조하십시오.
* 최소한의 운영 오버헤드로 고성능의 안정적인 데이터 스토리지 제공
* TCO 절감(총 소유 비용)

**MongoMK 선택 기준**

* 하루에 연결된 지정된 사용자 수:수천 개 또는 그 이상의
* 동시 사용자 수:수백 개 이상
* 일별 자산 인제션 볼륨:수십만 명 이상
* 일일 페이지 편집 볼륨:수십만 명 이상
* 일일 검색 볼륨:수만 명 이상

### TarMK와 MongoMK 벤치마크 {#tarmk-vs-mongomk-benchmarks}

>[!NOTE]
>
>아래에 표시된 숫자는 기준선으로 1로 표준화되었으며 실제 처리량은 아닙니다.

### 시나리오 1 기술 사양 {#scenario-technical-specifications}

<table>
 <tbody>
  <tr>
   <td><strong> </strong></td>
   <td><strong>작성자 OAK 노드</strong></td>
   <td><strong>MongoDB 노드</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td>서버</td>
   <td>Bare Metal 하드웨어(HP)</td>
   <td>Bare Metal 하드웨어(HP)</td>
   <td> </td>
  </tr>
  <tr>
   <td>운영 체제</td>
   <td>RedHat Linux</td>
   <td>RedHat Linux</td>
   <td> </td>
  </tr>
  <tr>
   <td>CPU/코어</td>
   <td>Intel(R) Xeon(R) CPU E5-2407 @2.40GHz, 8 코어</td>
   <td>Intel(R) Xeon(R) CPU E5-2407 @2.40GHz, 8 코어</td>
   <td> </td>
  </tr>
  <tr>
   <td>RAM</td>
   <td>32GB</td>
   <td>32GB</td>
   <td> </td>
  </tr>
  <tr>
   <td>디스크</td>
   <td>마그네틱 - 1k IOPS 이상</td>
   <td>마그네틱 - 1k IOPS 이상</td>
   <td> </td>
  </tr>
  <tr>
   <td>Java</td>
   <td>Oracle JRE 버전 8</td>
   <td>N/A</td>
   <td> </td>
  </tr>
  <tr>
   <td>JVM Heap16GB</td>
   <td>16GB</td>
   <td>N/A</td>
   <td> </td>
  </tr>
  <tr>
   <td>제품 </td>
   <td>AEM 6.2</td>
   <td>MongoDB 3.2 WiredTiger</td>
   <td> </td>
  </tr>
  <tr>
   <td>노데스토르</td>
   <td>TarMK 또는 MongoMK</td>
   <td>N/A</td>
   <td> </td>
  </tr>
  <tr>
   <td>데이터 저장소</td>
   <td>파일 DS </td>
   <td>N/A</td>
   <td> </td>
  </tr>
  <tr>
   <td>시나리오</td>
   <td><p><br /> 단일 제품:자산 / 실행당 동시 스레드 30개</p> </td>
   <td> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### 시나리오 1 성능 벤치마크 결과 {#scenario-performance-benchmark-results}

![chlimage_1-12](assets/chlimage_1-12a.png)

### 시나리오 2 기술 사양 {#scenario-technical-specifications-1}

>[!NOTE]
>
>MongoDB와 동일한 수의 Author를 하나의 TarMK 시스템과 사용하려면 두 개의 AEM 노드가 있는 클러스터가 필요합니다. 4개의 노드 MongoDB 클러스터는 Author 수의 1.8배를 TarMK 인스턴스 한 개보다 처리할 수 있습니다. 8개의 노드 MongoDB 클러스터는 Author 수의 2.3배를 TarMK 인스턴스 한 개보다 처리할 수 있습니다.

<table>
 <tbody>
  <tr>
   <td><strong> </strong></td>
   <td><strong>작성자 TarMK 노드</strong></td>
   <td><strong>Author MongoMK Node</strong></td>
   <td><strong>MongoDB 노드</strong></td>
  </tr>
  <tr>
   <td>서버</td>
   <td>AWS c3.8xlarge</td>
   <td>AWS c3.8xlarge</td>
   <td>AWS c3.8xlarge</td>
  </tr>
  <tr>
   <td>운영 체제</td>
   <td>RedHat Linux</td>
   <td>RedHat Linux</td>
   <td>RedHat Linux</td>
  </tr>
  <tr>
   <td>CPU/코어</td>
   <td>32</td>
   <td>32</td>
   <td>32</td>
  </tr>
  <tr>
   <td>RAM</td>
   <td>60GB</td>
   <td>60GB</td>
   <td>60GB</td>
  </tr>
  <tr>
   <td>디스크</td>
   <td>SSD - 10k IOPS</td>
   <td>SSD - 10k IOPS</td>
   <td>SSD - 10k IOPS</td>
  </tr>
  <tr>
   <td>Java</td>
   <td>Oracle JRE 버전 8</td>
   <td><br /> Oracle JRE 버전 8</td>
   <td>N/A</td>
  </tr>
  <tr>
   <td>JVM Heap16GB</td>
   <td>30GB</td>
   <td>30GB</td>
   <td>N/A</td>
  </tr>
  <tr>
   <td>제품 </td>
   <td>AEM 6.2</td>
   <td>AEM 6.2</td>
   <td><br /> MongoDB 3.2 WiredTiger</td>
  </tr>
  <tr>
   <td>노데스토르</td>
   <td>TarMK </td>
   <td>MongoMK</td>
   <td><br /> N/A</td>
  </tr>
  <tr>
   <td>데이터 저장소</td>
   <td>파일 DS </td>
   <td><br /> 파일 DS</td>
   <td><br /> N/A</td>
  </tr>
  <tr>
   <td>시나리오</td>
   <td><p><br /> <br /> 세로 사용 사례:Media / 2000 동시 스레드</p> </td>
   <td></td>
   <td></td>
  </tr>
 </tbody>
</table>

### 시나리오 2 성능 벤치마크 결과 {#scenario-performance-benchmark-results-1}

![chlimage_1-13](assets/chlimage_1-13a.png)

### AEM 사이트 및 자산에 대한 아키텍처 확장성 가이드라인 {#architecture-scalability-guidelines-for-aem-sites-and-assets}

![chlimage_1-14](assets/chlimage_1-14a.png)

## 성과 지침 요약 {#summary-of-performance-guidelines}

이 페이지에 제시된 지침은 다음과 같이 요약할 수 있습니다.

* **파일 데이터 저장소가 있는 TarMK는** 대부분의 고객에게 권장되는 아키텍처입니다.

   * 최소 토폴로지:작성자 인스턴스 1개, 게시 인스턴스 2개, 디스패처 2개
   * 파일 데이터 저장소가 공유된 경우 바이너리 없는 복제가 켜짐

* **파일 데이터 저장소가 있는 MongoMK는** 작성자 계층의 수평 확장성을 위한 권장 아키텍처입니다.

   * 최소 토폴로지:작성자 인스턴스 3개, MongoDB 인스턴스 3개, 게시 인스턴스 2개, 디스패처 2개
   * 파일 데이터 저장소가 공유된 경우 바이너리 없는 복제가 켜짐

* **NAS** (Network Attached Storage)가 아닌 로컬 디스크에 Nodestore를 저장해야 합니다.
* Amazon S3 **를**&#x200B;사용하는 경우:

   * Amazon S3 데이터 저장소는 작성자 및 게시 계층 간에 공유됩니다.
   * 바이너리 없는 복제를 설정해야 합니다.
   * Datastore Garbage Collection을 사용하려면 모든 작성자 및 게시 노드에서 먼저 실행한 다음 작성자에서 두 번째 실행이 필요합니다.

* **대부분의 일반적인 검색을 기반으로 하는 기본 색인** 외에 사용자 정의 인덱스를 만들어야 합니다.

   * 사용자 지정 색인에 Lucene 색인을 사용해야 합니다.

* **작업 흐름을 사용자 지정하면 &quot;자산 업데이트&quot; 작업 과정에서 비디오 단계를 제거하거나 사용하지 않는 수신기를 비활성화하는 등 성능을**&#x200B;크게 향상시킬 수 있습니다.

자세한 내용은 권장 배포 [페이지를](/help/sites-deploying/recommended-deploys.md) 참조하십시오.
