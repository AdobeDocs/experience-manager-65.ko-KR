---
title: 컨텐츠 속성 및 노드
description: 이 페이지를 따라 콘텐츠 속성 및 노드에 대해 알아보십시오.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: 05c8c846-69cc-4075-9149-33890b3d1e08
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 20%

---

# 컨텐츠 속성 및 노드 {#content-properties-and-nodes}

{{ue-over-mobile}}

문서, 배너 및 컬렉션은 AEM에서 cq:Pages(으)로 표시됩니다.

이 속성은 Adobe Experience Manager(AEM) Mobile On-Demand 서비스 메타데이터 및 통합 지원 속성을 나타내는 아래에 표시된 몇 가지 다른 속성 외에도 모든 cq:Page에서 발견된 동일한 공통 속성을 공유합니다.

다음 표에서는 콘텐츠 속성 및 노드에 대해 설명합니다.

## 일반 통합 속성 {#common-integration-properties}

| **속성 이름** | **유형** | **기본값 또는 예상 값** | **설명** |
|---|---|---|---|
| dps-id | 문자열 |  | AEM Mobile에 업로드하거나 AEM Mobile에서 가져온 후에는 AEM에서 할당하고 AEM Mobile에서 저장합니다. |
| dps-resourceType | 문자열 | dps:Article | `dps:Banner` \| `dps:Collection` \| `entity type property` |
| dps-version | 문자열 |  | AEM Mobile 엔티티 버전(전체 aemm-id에도 포함됨) |
| dps-lastSynced | 날짜 |  | AEM Mobile에서 AEM으로 마지막 동기화/가져오기 날짜 |
| dps-lastUploaded | 날짜 |  | AEM에서 AEM Mobile으로 마지막으로 업로드한 날짜 |
| dps-lastUploadedBy | 문자열:userid |  | AEM에서 AEM Mobile으로의 마지막 업로드 요청을 수행한 id 사용자 |

## 코어 메타데이터 속성 {#core-metadata-properties}

| 속성 이름 | 유형 | 기본값 또는 예상 값 |
|--- |--- |--- |
| dps-title | 문자열 |  |
| dps-shortTitle | 문자열 |  |
| dps-abstract | 문자열 |  |
| dps-shortAbstract | 문자열 |  |
| 디피에스 주 | 문자열 |  |
| dps-category | 문자열 |  |
| dps-키워드 | 문자열[] |  |
| dps-internalKeywords | 문자열[] |  |
| dps 중요도 | 문자열[] | {&quot;low&quot;, &quot;normal&quot;, &quot;high&quot;}의 중요도 |

### 기사 {#articles}

| **속성 이름** | **유형** | **기본값 또는 예상 값** |
|---|---|---|
| dps-author | 문자열 |  |
| dps-authorURL | 문자열 |  |
| dps-hideFromBrowsePage | 부울 |  |
| dps-access | 문자열 | {&quot;protected&quot;, &quot;metered&quot;, &quot;free&quot;}의 ProtectedAccess |
| **소셜** |  |  |
| dps-socialShareURL | 문자열 |  |
| dps-articleText | 문자열 |  |
| dps-url | 문자열 |  |

### 배너 {#banners}

| **속성 이름** | **유형** | **기본값 또는 예상 값** |
|---|---|---|
| dps-tapAction |  | {webLink}에서 TapAction |
| dps-tapActinUrl |  |  |

### 컬렉션 {#collections}

| 속성 이름 | 유형 | 기본값 또는 예상 값 |
|--- |--- |--- |
| dps-productId | 문자열 |  |
| dps-readingPosition | 문자열 | {&quot;reset&quot;,&quot;retain&quot;}에서 |
| dps-horizontalSwipe | 부울 |  |
| dps-allowDownload | 부울 |  |
| dps-openDefault | 문자열 | 출처: {&quot;browsePage&quot;,&quot;contentView&quot;} |
| dps-layout | 문자열 |  |

## 컨텐츠 노드 {#content-nodes}

### 공통 노드 {#common-nodes}

| 노드 이름 | 유형 | 기본값 또는 예상 값 | 설명 |
|--- |--- |--- |--- |
| 이미지 | jcr:primaryType=nt:unstructured <br> sling:resourceType=foundation/components/image |  |  |

### 엔티티 {#entities}

#### 기사 {#articles-1}

| 노드 이름 | 유형 | 예상 값의 기본값 | 설명 |
|--- |--- |--- |--- |
| 소셜 공유 이미지 |  | jcr:primaryType=nt:unstructured <br> sling:resourceType=foundation/components/image |  |

#### 배너 {#banners-1}

| 노드 이름 | 유형 | 예상 값의 기본값 | 설명 |
|---|---|---|---|
| NA |  |  |  |

#### 컬렉션 {#collections-1}

| 노드 이름 | 유형 | 예상 값의 기본값 | 설명 |
|--- |--- |--- |--- |
| background-image | jcr:primaryType=nt:unstructured <br> sling:resourceType=foundation/components/image |  |  |
