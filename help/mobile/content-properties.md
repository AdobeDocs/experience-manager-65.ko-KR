---
title: 컨텐츠 속성 및 노드
seo-title: 컨텐츠 속성 및 노드
description: 컨텐츠 속성 및 노드에 대해 알려면 이 페이지를 따르십시오.
seo-description: 컨텐츠 속성 및 노드에 대해 알려면 이 페이지를 따르십시오.
uuid: 2dad52c8-5b6c-4b90-8498-62217a9a27fc
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: f5721ddc-df5c-496c-be61-38d1cab63ad4
translation-type: tm+mt
source-git-commit: 50c0bdfc3203410d392e53536bc7cd00245406e5

---


# 컨텐츠 속성 및 노드 {#content-properties-and-nodes}

>[!NOTE]
>
>단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: 응답)이 필요한 프로젝트에 SPA 편집기를 사용하는 것이 좋습니다. [추가 정보](/help/sites-developing/spa-overview.md).

아티클, 배너 및 컬렉션은 AEM에서 cq:Pages로 표시됩니다.

Adobe Experience Manager(AEM) Mobile On-Demand Services 메타데이터 및 통합 지원 속성을 나타내는 다른 몇 개 외에 모든 cq:Page에서 찾은 동일한 공통 속성을 공유합니다.

다음 표에서는 컨텐츠 속성과 노드에 대해 설명합니다.

## 공통 통합 속성 {#common-integration-properties}

| **속성 이름** | **유형** | **기본값 또는 예상 값** | **설명** |
|---|---|---|---|
| dps-id | 문자열 |  | aem Mobile에서 할당되고 AEM에서 저장한 후 AEM Mobile에 업로드하거나 AEM Mobile에서 가져오면 |
| dps-resourceType | 문자열 | dps:Article | dps:Banner | dps:Collection | 엔티티 유형 속성 |
| dps-version | 문자열 |  | AEM Mobile 엔티티 버전(전체 aemm-id 내에 포함) |
| dps-lastSynced | 날짜 |  | aem Mobile에서 AEM으로 마지막 동기화/가져오기 날짜 |
| dps-lastUploaded | 날짜 |  | aem에서 AEM Mobile로 마지막 업로드 날짜 |
| dps-lastUploadedBy | 문자열:userid |  | aem에서 AEM Mobile로 마지막 업로드 요청을 수행한 ID 사용자 |

## 핵심 메타데이터 속성 {#core-metadata-properties}

| 속성 이름 | 유형 | 기본값 또는 예상 값 |
|--- |--- |--- |
| dps-title | 문자열 |  |
| dps-shortTitle | 문자열 |  |
| dps-abstract | 문자열 |  |
| dps-shortAbstract | 문자열 |  |
| dps-department | 문자열 |  |
| dps-category | 문자열 |  |
| dps-keywords | String[] |  |
| dps-internalKeywords | String[] |  |
| dps 중요도 | String[] | {&quot;low&quot;, &quot;normal&quot;, &quot;high&quot;}의 중요도 |

### 기사 {#articles}

| **속성 이름** | **유형** | **기본값 또는 예상 값** |
|---|---|---|
| dps-author | 문자열 |  |
| dps-authorURL | 문자열 |  |
| dps-hideFromBrowsePage | 부울 |  |
| dps-access | 문자열 | {&quot;protected&quot;, &quot;부분 무료&quot;, &quot;무료&quot;}에서 ProtectedAccess |
| **Social** |  |  |
| dps-socialShareURL | 문자열 |  |
| dps-articleText | 문자열 |  |
| dps-url | 문자열 |  |

### 배너 {#banners}

| **속성 이름** | **유형** | **기본값 또는 예상 값** |
|---|---|---|
| dps-tapAction |  | {webLink}에서 TapAction |
| dps-tapActionUrl |  |  |

### 컬렉션 {#collections}

| 속성 이름 | 유형 | 기본값 또는 예상 값 |
|--- |--- |--- |
| dps-productId | 문자열 |  |
| dps-readingPosition | 문자열 | {&quot;reset&quot;,&quot;retain&quot;} |
| dps-horizontalSwipe | 부울 |  |
| dps-allowDownload | 부울 |  |
| dps-openDefault | 문자열 | from {&quot;browsePage&quot;,&quot;contentView&quot;} |
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
| social-share-image |  | jcr:primaryType=nt:unstructured <br> sling:resourceType=foundation/components/image |  |

#### 배너 {#banners-1}

| 노드 이름 | 유형 | 예상 값의 기본값 | 설명 |
|---|---|---|---|
| NA |  |  |  |

#### 컬렉션 {#collections-1}

| 노드 이름 | 유형 | 예상 값의 기본값 | 설명 |
|--- |--- |--- |--- |
| background-image | jcr:primaryType=nt:unstructured <br> sling:resourceType=foundation/components/image |  |  |
