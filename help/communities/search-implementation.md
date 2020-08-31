---
title: Search Essentials
seo-title: Search Essentials
description: 커뮤니티에서 검색
seo-description: 커뮤니티에서 검색
uuid: 5f35a033-2069-499e-9cdb-db25781312f0
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 300aa9f3-596f-42bc-8d46-e535f2bc4379
translation-type: tm+mt
source-git-commit: 9a4ae73c08657195da2741cccdb196bd7f7142c9
workflow-type: tm+mt
source-wordcount: '1189'
ht-degree: 4%

---


# Search Essentials {#search-essentials}

## 개요 {#overview}

이 검색 기능은 AEM Communities의 필수적인 기능입니다. AEM Communities은 [AEM 플랫폼 검색](../../help/sites-deploying/queries-and-indexing.md) 기능 외에도 UGC(사용자 생성 컨텐츠 [)를 검색할 수 있도록](#ugc-search-api) UGC 검색 API를제공합니다. UGC는 다른 AEM 컨텐츠 및 사용자 데이터와 별도로 입력되어 저장될 때 고유한 속성을 갖습니다.

Communities에서 일반적으로 검색된 두 가지 사항은 다음과 같습니다.

* 커뮤니티 회원이 게시한 컨텐츠

   * AEM Communities의 UGC 검색 API를 사용합니다.

* 사용자 및 사용자 그룹(사용자 데이터)

   * AEM 플랫폼 검색 기능을 사용합니다.

이 설명서 섹션은 UGC를 생성하거나 관리하는 사용자 정의 구성 요소를 만드는 개발자에게 유용합니다.

## 보안 및 그림자 노드 {#security-and-shadow-nodes}

사용자 지정 구성 요소의 경우 [SocialResourceUtilities 메서드를 사용해야](socialutils.md#socialresourceutilities-package) 합니다. UGC를 만들고 검색하는 유틸리티 메서드는 필요한 [그림자 노드를](srp.md#about-shadow-nodes-in-jcr) 설정하고 멤버에 요청에 대한 올바른 권한이 있는지 확인합니다.

SRP 유틸리티를 통해 관리하지 않는 것은 중재와 관련된 속성입니다.

UGC 및 [ACL](srp-and-ugc.md) 그림자 노드에 액세스하는 데 사용되는 유틸리티 방법에 대한 자세한 내용은 SRP 및 UGC Essentials를 참조하십시오.

## UGC 검색 API {#ugc-search-api}

UGC [공용 스토어는](working-with-srp.md) 다양한 SRP(Storage Resource Provider) 중 한 곳에서 제공되며 각 SRP에는 서로 다른 기본 쿼리 언어가 있을 수 있습니다. 따라서 선택한 SRP에 관계없이 사용자 지정 코드는 선택한 SRP에 적합한 쿼리 언어를 호출하는 [UGC API 패키지](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/ugc/api/package-summary.html) (*com.adobe.cq.sosocial.ugc.api*)의 메서드를 사용해야 합니다.

### ASRP 검색 {#asrp-searches}

ASRP의 [경우](asrp.md)UGC는 Adobe 클라우드에 저장됩니다. UGC는 CRX에 표시되지 않지만 [작성자 및 게시 환경 모두에서 중재를](moderate-ugc.md) 사용할 수 있습니다. UGC [검색 API의](#ugc-search-api) 사용은 다른 SRP와 동일한 ASRP에서 작동합니다.

현재 ASRP 검색을 관리하기 위한 도구가 없습니다.

검색 가능한 사용자 지정 속성을 만들 때는 [이름 지정 요구 사항을 준수해야 합니다](#naming-of-custom-properties).

### MSRP 검색 {#msrp-searches}

MSRP의 [경우](msrp.md)UGC는 검색용으로 Solr를 사용하도록 구성된 MongoDB에 저장됩니다. UGC는 CRX에 표시되지 않지만 [중재는](moderate-ugc.md) 작성 환경과 게시 환경 모두에서 사용할 수 있습니다.

MSRP 및 솔루션 관련:

* AEM 플랫폼용 임베디드 솔러는 MSRP에 사용되지 않습니다.
* AEM 플랫폼용 원격 솔루션을 사용하는 경우 MSRP와 공유할 수 있지만 다른 컬렉션을 사용해야 합니다.
* 솔러는 표준 검색 또는 MLS(다국어 검색)용으로 구성할 수 있습니다.
* 구성에 대한 자세한 내용은 [MSRP용](msrp.md#solr-configuration) 솔루션 구성을 참조하십시오.

사용자 지정 검색 기능은 [UGC 검색 API를 사용해야 합니다](#ugc-search-api).

검색 가능한 사용자 지정 속성을 만들 때는 [이름 지정 요구 사항을 준수해야 합니다](#naming-of-custom-properties).

### JSRP 검색 {#jsrp-searches}

JSRP의 [경우](jsrp.md)UGC는 [Oak에](../../help/sites-deploying/platform.md) 저장되고 입력된 AEM 작성자 또는 게시 인스턴스의 보관소에만 표시됩니다.

UGC는 일반적으로 게시 환경에 입력되기 때문에 다중 게시자 프로덕션 시스템의 경우, [게시 팜이 아니라 게시 클러스터를](topologies.md)구성해야 하므로 입력한 컨텐츠가 모든 게시자에서 볼 수 있습니다.

JSRP의 경우 게시 환경에 입력된 UGC는 작성 환경에서 보이지 않습니다. 따라서 모든 [중재](moderate-ugc.md) 작업은 게시 환경에서 수행됩니다.

사용자 지정 검색 기능은 [UGC 검색 API를 사용해야 합니다](#ugc-search-api).

#### Oak 인덱싱 {#oak-indexing}

AEM 플랫폼 검색에 대해 Oak 색인은 자동으로 만들어지지 않지만 AEM 6.2에서는 UGC 검색 결과를 표시할 때 성능을 향상시키고 페이지 매김을 지원하기 위해 AEM Communities이 추가되었습니다.

사용자 지정 속성이 사용 중이고 검색이 느린 경우 사용자 지정 속성을 더 성능으로 만들려면 추가 색인을 만들어야 합니다. 이식성을 유지하려면 검색 가능한 사용자 정의 속성을 만들 때 [이름 지정 요구](#naming-of-custom-properties) 사항을 따르십시오.

기존 색인을 수정하거나 사용자 정의 색인을 만들려면 [Oak 쿼리 및 색인을 참조하십시오](../../help/sites-deploying/queries-and-indexing.md).

Oak [색인 관리자는](https://adobe-consulting-services.github.io/acs-aem-commons/features/oak-index-manager.html) ACS AEM Commons에서 사용할 수 있습니다. 다음과 같은 이점을 제공합니다.

* 기존 색인의 보기.
* 다시 색인 작성 기능

CRXDE Lite에서 기존 Oak 색인을 보려면 [위치](../../help/sites-developing/developing-with-crxde-lite.md):

* `/oak:index/socialLucene`

![social-lucene](assets/social-lucene.png)

## 인덱싱된 검색 속성 {#indexed-search-properties}

### 기본 검색 속성 {#default-search-properties}

다음은 다양한 커뮤니티 기능에 사용되는 검색 가능한 속성 중 일부입니다.

| **속성** | **데이터 유형** |
|---|---|
| isFlagged | *부울* |
| isSpam | *부울* |
| read | *부울* |
| 영향력 | *부울* |
| 첨부 파일 | *부울* |
| 감정 | *긴* |
| 플래그 | *부울* |
| 추가됨 | *날짜* |
| modifiedDate | *날짜* |
| 상태 | *String* |
| userIdentifier | *String* |
| 답글 | *긴* |
| jcr:title | *String* |
| jcr:description | *String* |
| sling:resourceType | *String* |
| allowThreadedReply | *부울* |
| isDraft | *부울* |
| publishDate | *날짜* |
| publishJobId | *String* |
| 답변됨 | *부울* |
| 답변한 사람 | *부울* |
| 태그 | *String* |
| cq:태그 | *String* |
| author_display_name | *String* |
| location_t | *String* |
| parentPath | *String* |
| parentTitle | *String* |

### 사용자 지정 속성 이름 지정 {#naming-of-custom-properties}

사용자 지정 속성을 추가할 때 [UGC 검색 API로 만든 정렬 및 검색에 이러한 속성을 표시하려면 속성 이름에 접미사를](#ugc-search-api)추가해야 ** 합니다.

접미사는 스키마를 사용하는 쿼리 언어용입니다.

* 검색 가능한 속성을 식별합니다.
* 데이터 유형을 식별합니다.

솔러는 스키마를 사용하는 쿼리 언어의 예입니다.

| **접미사** | **데이터 유형** |
|---|---|
| _b | *부울* |
| _dt | *달력* |
| _d | *더블* |
| _tl | *긴* |
| _s | *String* |
| _t | *텍스트* |

**메모:**

* *텍스트는* 토큰화된 문자열이고 *문자열은* 그렇지 않습니다. 퍼지( *유사)* 검색에 텍스트 사용

* 다중값 유형의 경우 접미사에 &#39;s&#39;를 추가합니다. 예:

   * `viewDate_dt`:단일 날짜 속성
   * `viewDates_dts`:날짜 목록 속성

## 필터 {#filters}

주석 시스템을 포함하는 구성 요소는 [끝점에 필터 매개 변수 추가를](essentials-comments.md) 지원합니다.

AND 및 OR 로직용 필터 구문은 다음과 같이 표현됩니다(URL로 인코딩되기 전에 표시됨).

* OR을 지정하려면 쉼표로 구분된 값이 있는 하나의 필터 매개 변수를 사용합니다.

   * `filter=name eq 'Jennifer',name eq 'Jen'`

* AND를 지정하고 여러 필터 매개 변수를 사용하려면:

   * `filter = name eq 'Jackson'&filter=message eq 'testing'`

검색 구성 요소의 기본 구현 [은](search.md) 커뮤니티 구성 요소 안내서의 검색 결과 페이지를 여는 URL에서 볼 수 있는 것처럼 이 구문을 [사용합니다](components-guide.md). 실험해 보려면 http://localhost:4503/content/community-components/en/search.html으로 [이동합니다](http://localhost:4503/content/community-components/en/search.html).

필터 연산자는 다음과 같습니다.

| EQ | 같음 |
|---|---|
| NE | 같지 않음 |
| LT | 보다 작음 |
| LTE | 작거나 같음 |
| GE | 보다 큼 |
| GTE | 크거나 같음 |
| LIKE | 유사 일치 |

URL은 구성 요소가 배치된 페이지가 아니라 커뮤니티 구성 요소(리소스)를 참조해야 합니다.

* 정답:포럼 구성 요소
   * `/content/community-components/en/forum/jcr:content/content/forum.social.json`
* 틀림:포럼 페이지
   * `/content/community-components/en/forum.social.json`

## SRP 도구 {#srp-tools}

다음과 같은 Adobe Marketing Cloud GitHub 프로젝트가 있습니다.

[AEM Communities SRP 도구](https://github.com/Adobe-Marketing-Cloud/aem-communities-srp-tools)

이 저장소에는 SRP의 데이터 관리 도구가 포함되어 있습니다.

현재 SRP에서 모든 UGC를 삭제할 수 있는 기능을 제공하는 서블릿이 하나 있습니다.

예를 들어 ASRP에서 모든 UGC를 삭제하려면 다음을 수행하십시오.

```shell
curl -X POST http://localhost:4502/services/social/srp/cleanup?path=/content/usergenerated/asi/cloud -uadmin:admin
```

## 문제 해결 {#troubleshooting}

### 솔루션 쿼리 {#solr-query}

솔루션 쿼리 문제를 해결하는 데 도움이 되도록 하려면

`com.adobe.cq.social.srp.impl.SocialSolrConnector`.

실제 솔루션 쿼리는 디버그 로그에 URL로 인코딩됩니다.

솔루션 쿼리: `sort=timestamp+desc&bl=en&pl=en&start=0&rows=10 &q=%2Btitle_t:(hello)+%2Bprovider_id:\/content/usergenerated/asi/mongo/content/+%2Bresource_type_s:&df=provider_id&trf=verbatim&fq={!cost%3D100}report_suite:mongo`

매개 변수의 값 `q` 은 쿼리입니다. URL 인코딩이 디코딩되면 추가 디버깅을 위해 쿼리를 Solr Admin Query 툴로 전달할 수 있습니다.

## 관련 리소스 {#related-resources}

* [커뮤니티 콘텐츠 저장소](working-with-srp.md) - UGC 공용 저장소에 대해 사용할 수 있는 SRP에 대해 설명합니다.
* [스토리지 리소스 공급자 개요](srp.md) - 소개 및 저장소 사용 개요
* [SRP를 사용하여 UGC](accessing-ugc-with-srp.md) 액세스 - 코딩 가이드라인.
* [SocialUtils 리팩토링](socialutils.md) - SocialUtils를 대체하는 SRP에 대한 유틸리티 메서드입니다.
* [검색 및 검색 결과 구성 요소](search.md) - 템플릿에 UGC 검색 기능 추가

