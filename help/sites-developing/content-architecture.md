---
title: 컨텐츠 아키텍처
seo-title: Content Architecture
description: 콘텐츠 아키텍처를 위한 팁(힌트 - 모든 것이 콘텐츠임)
seo-description: Tips for architecting your content in Adobe Experience Manager (AEM). (hint - everything is content)
uuid: fef2bf0f-70ec-4621-8479-a62b7e1fbc07
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: ca46b74c-6114-458b-98c0-2a93abffcdc3
exl-id: bcebbdb4-20b9-4c2d-8a87-013549d686c1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 0%

---

# 컨텐츠 아키텍처{#content-architecture}

## David의 모델 팔로우 {#follow-david-s-model}

David&#39;s Model은 수년 전 David Nuescheler에 의해 쓰여졌으나, 오늘날에도 그 개념들이 참이다. David&#39;s Model의 주요 개념은 다음과 같습니다.

* 데이터는 먼저 가져오고, 구조는 나중에 가져옵니다. 그럴지도.
* 콘텐츠 계층 구조를 구동하십시오. 그렇게 되지 않도록 하십시오.
* 작업 공간은 다음과 같습니다. `clone()`, `merge()`, 및 `update()`.
* 같은 이름의 형제 자매를 조심하십시오.
* 참고문헌은 유해한 것으로 간주된다.
* 파일은 파일입니다.
* ID는 사악합니다.

David의 모델은 Jackrabbit wiki의 [https://wiki.apache.org/jackrabbit/DavidsModel](https://wiki.apache.org/jackrabbit/DavidsModel).

### 모든 내용이 콘텐츠입니다. {#everything-is-content}

데이터베이스와 같은 별도의 타사 데이터 소스에 의존하지 않고 모든 것을 저장소에 저장해야 합니다. 이는 작성된 콘텐츠, 이미지, 코드, 구성 등과 같은 바이너리 데이터에 적용됩니다. 이를 통해 하나의 API 세트를 사용하여 모든 콘텐츠를 관리하고 복제를 통해 이 콘텐츠의 프로모션을 관리할 수 있습니다. 또한 백업, 로깅 등의 단일 소스도 확보할 수 있습니다.

### &quot;콘텐츠 모델 우선&quot; 설계 원칙 사용 {#use-the-content-model-first-design-principle}

새 기능을 빌드할 때는 항상 먼저 JCR 콘텐츠 구조를 디자인한 다음 기본 Sling 서블릿을 사용하여 콘텐츠를 읽고 쓰는 과정을 살펴봅니다. 이렇게 하면 구현이 즉시 사용 가능한 액세스 제어 메커니즘과 잘 작동하는지 확인하고 불필요한 CRUD 스타일 서블릿을 생성하지 않도록 할 수 있습니다.

### 마음을 편히 가지세요 {#be-restful}

서블릿은 경로 대신 resourceTypes를 기반으로 정의해야 합니다. 이렇게 하면 JCR 액세스 제어를 사용하고, REST 원칙을 준수하고, 요청에서 제공되는 리소스 및 리소스 확인자를 사용할 수 있습니다. 또한 클라이언트측의 URL을 변경할 필요 없이 서버측의 URL을 렌더링하는 스크립트를 변경할 수 있도록 해주며, 추가 보안을 위해 클라이언트측의 서버측 구현 세부 정보를 숨길 수 있습니다.

### 새 노드 유형을 정의하지 마십시오 {#avoid-defining-new-node-types}

노드 유형은 인프라 레이어에서 낮은 수준에서 작동하며 대부분의 요구 사항은 nt:unstructured, oak:Unstructured, sling:Folder 또는 cq:Page 노드 유형에 할당된 sling:resourceType 을 사용하여 충족할 수 있습니다. 노드 유형은 저장소의 스키마와 동일하며, 노드 유형을 변경하는 것은 비용이 매우 많이 들 수 있습니다.

### JCR의 명명 규칙 준수 {#adhere-to-naming-conventions-in-the-jcr}

명명 규칙을 준수하면 코드 베이스에 일관성이 추가되어 결함 발생률이 낮아지고 시스템에서 작업하는 개발자의 속도가 빨라집니다. Adobe은 AEM 개발 시 다음 규칙을 사용합니다.

* 노드 이름

   * 모든 소문자
   * 하이픈을 사용한 단어 분리

* 속성 이름

   * 카멜 대/소문자, 소문자로 시작

* 구성 요소(JSP/HTML)

   * 모든 소문자
   * 하이픈을 사용한 단어 분리
