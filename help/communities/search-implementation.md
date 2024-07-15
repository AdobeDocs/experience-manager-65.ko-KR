---
title: Essentials 검색
description: AEM Communities의 필수 기능인 검색 기능에 대해 알아봅니다. 커뮤니티는 사용자 생성 콘텐츠에 대한 검색 API도 제공합니다.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 8af5ee58-19d7-47b6-b45d-e88006703a5d
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1158'
ht-degree: 3%

---

# Essentials 검색 {#search-essentials}

## 개요 {#overview}

검색 기능은 Adobe Experience Manager(AEM) 커뮤니티의 필수 기능입니다. [AEM 플랫폼 검색](../../help/sites-deploying/queries-and-indexing.md) 기능 외에도 AEM Communities에서는 UGC(사용자 생성 콘텐츠)를 검색하기 위한 [UGC 검색 API](#ugc-search-api)를 제공합니다. UGC는 다른 AEM 콘텐츠 및 사용자 데이터와 별도로 입력 및 저장되므로 고유한 속성을 갖습니다.

Communities에서 일반적으로 검색되는 두 가지 사항은 다음과 같습니다.

* 커뮤니티 회원이 게시한 컨텐츠

   * AEM Communities의 UGC 검색 API를 사용합니다.

* 사용자 및 사용자 그룹(사용자 데이터)

   * AEM platform 검색 기능을 사용합니다.

설명서의 이 섹션은 UGC를 만들거나 관리하는 사용자 지정 구성 요소를 만드는 개발자의 관심사입니다.

## 보안 및 섀도우 노드 {#security-and-shadow-nodes}

사용자 지정 구성 요소의 경우 [SocialResourceUtilities](socialutils.md#socialresourceutilities-package) 메서드를 사용해야 합니다. UGC를 만들고 검색하는 유틸리티 메서드는 필요한 [섀도 노드](srp.md#about-shadow-nodes-in-jcr)를 설정하고 구성원에게 요청에 대한 올바른 권한이 있는지 확인합니다.

SRP 유틸리티를 통해 관리되지 않는 것은 중재와 관련된 속성입니다.

UGC 및 ACL 섀도 노드에 액세스하는 데 사용되는 유틸리티 메서드에 대한 자세한 내용은 [SRP 및 UGC 필수 패키지](srp-and-ugc.md)를 참조하십시오.

## UGC 검색 API {#ugc-search-api}

[UGC 공용 저장소](working-with-srp.md)은(는) 다양한 SRP(저장소 리소스 공급자) 중 하나에서 제공하며, 각 SRP는 서로 다른 기본 쿼리 언어를 가지고 있습니다. 따라서 선택한 SRP에 관계없이 사용자 지정 코드에서는 선택한 SRP에 적합한 쿼리 언어를 호출하는 [UGC API 패키지](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/ugc/api/package-summary.html)(*com.adobe.cq.social.ugc.api*)의 메서드를 사용해야 합니다.

### ASRP 검색 {#asrp-searches}

[ASRP](asrp.md)의 경우 UGC가 Adobe 클라우드에 저장됩니다. UGC가 CRX에 표시되지 않지만 [중재](moderate-ugc.md)는 작성자와 Publish 환경 모두에서 사용할 수 있습니다. [UGC 검색 API](#ugc-search-api)를 사용하면 다른 SRP와 동일한 ASRP에 사용할 수 있습니다.

ASRP 검색 관리를 위한 도구가 현재 없습니다.

검색 가능한 사용자 지정 속성을 만들 때는 [이름 지정 요구 사항](#naming-of-custom-properties)을 준수해야 합니다.

### MSRP 검색 {#msrp-searches}

[MSRP](msrp.md)의 경우 UGC는 Solr을 사용하여 검색하도록 구성된 MongoDB에 저장됩니다. UGC가 CRX에 표시되지 않지만 [중재](moderate-ugc.md)는 작성자와 Publish 환경 모두에서 사용할 수 있습니다.

MSRP 및 Solr 관련 사항:

* AEM 플랫폼용 내장 Solr은 MSRP에 사용되지 않습니다.
* AEM 플랫폼용 원격 Solr을 사용하는 경우 MSRP와 공유할 수 있지만 서로 다른 컬렉션을 사용해야 합니다.
* Solr은 표준 검색 또는 다국어 검색(MLS)에 대해 구성될 수 있다.
* 구성에 대한 자세한 내용은 MSRP에 대한 [Solr 구성](msrp.md#solr-configuration)을 참조하십시오.

사용자 지정 검색 기능은 [UGC 검색 API](#ugc-search-api)를 사용해야 합니다.

검색 가능한 사용자 지정 속성을 만들 때는 [이름 지정 요구 사항](#naming-of-custom-properties)을 준수해야 합니다.

### JSRP 검색 {#jsrp-searches}

[JSRP](jsrp.md)의 경우 UGC는 [Oak](../../help/sites-deploying/platform.md)에 저장되며 입력된 AEM 작성자 또는 Publish 인스턴스의 저장소에서만 볼 수 있습니다.

UGC는 일반적으로 Publish 환경에 입력되므로 다중 게시자 프로덕션 시스템의 경우 입력한 콘텐츠가 모든 게시자에서 표시되도록 게시 팜이 아닌 [게시 클러스터](topologies.md)를 구성해야 합니다.

JSRP의 경우 Publish 환경에 입력된 UGC는 작성 환경에 표시되지 않습니다. 따라서 모든 [중재](moderate-ugc.md) 작업은 Publish 환경에서 수행됩니다.

사용자 지정 검색 기능은 [UGC 검색 API](#ugc-search-api)를 사용해야 합니다.

#### Oak 색인화 {#oak-indexing}

AEM 6.2부터 AEM 플랫폼 검색에 대해 Oak 색인이 자동으로 만들어지지 않지만, AEM Communities에 추가된 색인은 성능을 개선하고 UGC 검색 결과를 표시할 때 페이지 매김을 지원합니다.

사용자 지정 속성이 사용 중이고 검색 속도가 느린 경우 사용자 지정 속성에 대한 추가 색인을 만들어야 성능이 향상됩니다. 이식성을 유지하려면 검색 가능한 사용자 지정 속성을 만들 때 [이름 지정 요구 사항](#naming-of-custom-properties)을 준수하십시오.

기존 색인을 수정하거나 사용자 지정 색인을 만들려면 [Oak 쿼리 및 색인화](../../help/sites-deploying/queries-and-indexing.md)를 참조하세요.

[Oak 색인 관리자](https://adobe-consulting-services.github.io/acs-aem-commons/features/oak-index-manager.html)는 ACS AEM Commons에서 사용할 수 있습니다. 다음을 제공합니다.

* 기존 인덱스 보기.
* 리인덱싱을 시작할 수 있습니다.

[CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)에서 기존 Oak 색인을 보려면 다음 위치를 지정하십시오.

* `/oak:index/socialLucene`

![social-lucene](assets/social-lucene.png)

## 인덱싱된 검색 속성 {#indexed-search-properties}

### 기본 검색 속성 {#default-search-properties}

다음은 다양한 Communities 기능에 사용되는 검색 가능한 속성 중 일부입니다.

| **속성** | **데이터 형식** |
|---|---|
| 플래그 지정됨 | *부울* |
| isSpam | *부울* |
| 읽기 | *부울* |
| 영향 | *부울* |
| 첨부 파일 | *부울* |
| 감정 | *길게* |
| 플래그 지정됨 | *부울* |
| 추가됨 | *날짜* |
| modifiedDate | *날짜* |
| 시/도 | *문자열* |
| userIdentifier | *문자열* |
| 답글 | *길게* |
| jcr:title | *문자열* |
| jcr:description | *문자열* |
| sling:resourceType | *문자열* |
| allowThreadReply | *부울* |
| 초안 | *부울* |
| publishDate | *날짜* |
| publishJobId | *문자열* |
| 답변됨 | *부울* |
| chosenanted | *부울* |
| 태그 | *문자열* |
| cq:Tag | *문자열* |
| author_display_name | *문자열* |
| location_t | *문자열* |
| parentPath | *문자열* |
| parentTitle | *문자열* |

### 사용자 지정 속성 이름 지정 {#naming-of-custom-properties}

사용자 지정 속성을 추가할 때 해당 속성이 [UGC 검색 API](#ugc-search-api)로 만들어진 정렬 및 검색에 표시되도록 하려면 속성 이름에 접미사를 추가하는 것이 *필수*&#x200B;입니다.

접미사는 스키마를 사용하는 쿼리 언어용입니다.

* 속성을 검색 가능한 것으로 식별합니다.
* 데이터 유형을 식별합니다.

Solr은 스키마를 사용하는 쿼리 언어의 예입니다.

| **접미사** | **데이터 형식** |
|---|---|
| _b | *부울* |
| _dt | *일정* |
| _d | *이중* |
| _tl | *길게* |
| _s | *문자열* |
| _t | *텍스트* |

**메모:**

* *Text*&#x200B;은(는) 토큰화된 문자열이고 *String*&#x200B;은(는) 토큰화되지 않았습니다. 유사(유사) 검색을 위해 *텍스트*&#x200B;을(를) 사용합니다.

* 다중 값 형식의 경우 접미사에 &#39;s&#39;를 추가하십시오. 예를 들면 다음과 같습니다.

   * `viewDate_dt`: 단일 날짜 속성
   * `viewDates_dts`: 날짜 속성 목록

## 필터 {#filters}

[댓글 시스템](essentials-comments.md)을 포함하는 구성 요소는 끝점과 함께 필터 매개 변수를 지원합니다.

AND 및 OR 논리에 대한 필터 구문은 다음과 같이 표현됩니다(URL로 인코딩되기 전에 표시됨).

* OR을 지정하려면 쉼표로 구분된 값으로 하나의 필터 매개 변수를 사용합니다.

   * `filter=name eq 'Jennifer',name eq 'Jen'`

* 여러 필터 매개 변수를 지정하고 사용하려면 다음을 수행합니다.

   * `filter = name eq 'Jackson'&filter=message eq 'testing'`

[검색 구성 요소](search.md)의 기본 구현에서는 [커뮤니티 구성 요소 안내서](components-guide.md)에서 검색 결과 페이지를 여는 URL에 표시되는 것과 같이 이 구문을 사용합니다. 실험하려면 [http://localhost:4503/content/community-components/en/search.html](http://localhost:4503/content/community-components/en/search.html)(으)로 이동하세요.

필터 연산자는 다음과 같습니다.

| EQ | 같음 |
|---|---|
| NE | 같지 않음 |
| LT | 보다 작음 |
| LTE | 보다 작거나 같음 |
| GE | 보다 큼 |
| GTE | 크거나 같음 |
| 좋아요 | 유사 일치 |

URL은 구성 요소가 배치된 페이지가 아니라 Communities 구성 요소(리소스)를 참조해야 합니다.

* 수정: 포럼 구성 요소
   * `/content/community-components/en/forum/jcr:content/content/forum.social.json`
* 잘못됨: 포럼 페이지
   * `/content/community-components/en/forum.social.json`

## SRP 도구 {#srp-tools}

다음을 포함하는 Adobe Experience Cloud GitHub 프로젝트가 있습니다.

[AEM Communities SRP 도구](https://github.com/Adobe-Marketing-Cloud/aem-communities-srp-tools)

이 저장소에는 SRP에서 데이터를 관리하기 위한 도구가 들어 있습니다.

현재 모든 SRP에서 모든 UGC를 삭제할 수 있는 서블릿이 한 개 있습니다.

예를 들어 ASRP에서 모든 UGC를 삭제하려면 다음을 수행하십시오.

```shell
curl -X POST http://localhost:4502/services/social/srp/cleanup?path=/content/usergenerated/asi/cloud -uadmin:admin
```

## 문제 해결 {#troubleshooting}

### Solr 쿼리 {#solr-query}

Solr 쿼리의 문제를 해결하려면 다음에 대한 DEBUG 로깅을 활성화합니다.

`com.adobe.cq.social.srp.impl.SocialSolrConnector`

실제 Solr 쿼리는 디버그 로그에 인코딩된 URL로 표시됩니다.

Solr 쿼리: `sort=timestamp+desc&bl=en&pl=en&start=0&rows=10 &q=%2Btitle_t:(hello)+%2Bprovider_id:\/content/usergenerated/asi/mongo/content/+%2Bresource_type_s:&df=provider_id&trf=verbatim&fq={!cost%3D100}report_suite:mongo`

`q` 매개 변수의 값은 쿼리입니다. URL 인코딩이 디코딩되면 추가적인 디버깅을 위해 Solr Admin Query 도구로 쿼리를 전달할 수 있습니다.

## 관련 리소스 {#related-resources}

* [커뮤니티 콘텐츠 저장소](working-with-srp.md) - UGC 공용 저장소에 사용 가능한 SRP 선택 사항에 대해 설명합니다.
* [저장소 리소스 공급자 개요](srp.md) - 소개 및 저장소 사용 개요.
* [SRP를 사용하여 UGC에 액세스](accessing-ugc-with-srp.md) - 코딩 지침.
* [SocialUtils 리팩터링](socialutils.md) - SocialUtils를 대체하는 SRP용 유틸리티 메서드입니다.
* [검색 및 검색 결과 구성 요소](search.md) - 템플릿에 UGC 검색 기능을 추가하는 중입니다.
