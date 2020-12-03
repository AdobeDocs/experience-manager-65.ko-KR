---
title: 컨텐츠 아키텍처
seo-title: 컨텐츠 아키텍처
description: 컨텐츠 아키텍처에 대한 팁(힌트 - 모든 것이 컨텐츠임)
seo-description: Adobe Experience Manager(AEM)에서 컨텐츠 아키텍처에 대한 팁 (힌트 - 모든 것이 컨텐츠임)
uuid: fef2bf0f-70ec-4621-8479-a62b7e1fbc07
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: ca46b74c-6114-458b-98c0-2a93abffcdc3
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 1%

---


# 컨텐츠 아키텍처{#content-architecture}

## David의 모델 {#follow-david-s-model} 팔로우

데이비드의 모델은 몇 년 전 David Nuescheler에 의해 작성되었지만, 그 아이디어는 오늘 진실입니다. David의 모델의 주요 장점은 다음과 같다.

* 데이터는 먼저, 구조는 나중에. 그럴지도
* 콘텐츠 계층 구조 개선
* 작업 영역은 `clone()`, `merge()` 및 `update()`용입니다.
* 같은 이름의 형제들을 조심해라.
* 참조는 해롭다고 간주된다.
* 파일은 파일입니다.
* ID는 악합니다.

David의 모델은 Jackrabbit wiki 위치 [https://wiki.apache.org/jackrabbit/DavidsModel](https://wiki.apache.org/jackrabbit/DavidsModel)에 있습니다.

### 모든 것이 {#everything-is-content} 컨텐츠입니다.

모든 것은 데이터베이스와 같은 별도의 타사 데이터 소스에 의존하지 않고 저장소에 저장되어야 합니다. 이는 제작된 컨텐츠, 이미지, 코드, 구성 등의 이진 데이터에 적용됩니다. 따라서 한 세트의 API를 사용하여 모든 컨텐츠를 관리하고 복제를 통해 이 컨텐츠의 프로모션을 관리할 수 있습니다. 또한 백업, 로깅 등의 단일 소스를 얻을 수 있습니다.

### &quot;콘텐츠 모델 우선&quot; 디자인 원칙 {#use-the-content-model-first-design-principle} 사용

새로운 기능을 만들 때는 항상 JCR 컨텐츠 구조를 먼저 설계하여 시작한 다음 기본 Sling 서블릿을 사용하여 컨텐츠를 읽고 쓰는 방법을 살펴봅니다. 이를 통해 구현 방식이 즉시 액세스 제어 메커니즘과 잘 작동하는지 확인하고 불필요한 CRUD 스타일 서블릿을 생성하지 않아도 됩니다.

### RESTful {#be-restful}

서비스는 경로 대신 resourceTypes를 기반으로 정의해야 합니다. 따라서 JCR 액세스 컨트롤을 사용하고, REST 원칙을 준수하고, 요청에 제공된 리소스 및 리소스 해결 프로그램을 사용할 수 있습니다. 또한 보안 강화를 위해 클라이언트에서 서버측 구현 세부 정보를 숨긴 반면 클라이언트 측의 URL을 변경하지 않고도 서버 측에서 URL을 렌더링하는 스크립트를 변경할 수 있습니다.

### 새 노드 유형 {#avoid-defining-new-node-types} 정의 안 함

노드 유형은 인프라 레이어에서 낮은 수준에서 작동하며, nt:unstructured, oak:Unstructured, sling:Folder 또는 cq:Page 노드 유형에 지정된 sling:resourceType을 사용하여 대부분의 요구 사항을 충족할 수 있습니다. Node types equate to the schema in the repository and changing node types can be very cost down.

### JCR {#adhere-to-naming-conventions-in-the-jcr}의 명명 규칙 준수

명명 규칙을 준수하면 코드 베이스에 일관성이 추가되어 결함 발생률이 떨어지고 시스템에서 작업하는 개발자의 속도가 향상됩니다. 다음 규칙은 AEM 개발 시 Adobe에서 사용됩니다.

* 노드 이름

   * 모두 소문자
   * 하이픈을 사용한 단어 분리

* 속성 이름

   * 낙타의 경우, 소문자 구분

* 구성 요소(JSP/HTML)

   * 모두 소문자
   * 하이픈을 사용한 단어 분리

