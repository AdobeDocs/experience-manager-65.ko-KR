---
title: 컨텐츠 아키텍처
seo-title: 컨텐츠 아키텍처
description: 컨텐츠 아키텍처에 대한 팁(힌트 - 모든 것이 컨텐츠임)
seo-description: AEM(Adobe Experience Manager)에서 컨텐츠 아키텍처에 대한 팁 (힌트 - 모든 것이 컨텐츠임)
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

데이비드의 모델은 몇 년 전 David Nuescheler에 의해 작성되었지만, 그 아이디어는 오늘 그대로 실현됩니다. David의 모델의 주요 특징은 다음과 같다.

* 데이터는 먼저, 구조는 나중에. 그럴지도
* 콘텐츠 계층 구조 개선
* 작업 영역은 `clone()`, `merge()` 및 `update()`용입니다.
* 같은 이름을 가진 형제들을 조심하라.
* 참조는 해롭다고 간주됩니다.
* 파일은 파일입니다.
* ID는 악합니다.

데이비드의 모델은 [https://wiki.apache.org/jackrabbit/DavidsModel](https://wiki.apache.org/jackrabbit/DavidsModel)의 Jackrabbit wiki에서 찾을 수 있습니다.

### 모든 것이 {#everything-is-content} 컨텐츠입니다.

모든 것은 데이터베이스와 같은 별도의 제3자 데이터 소스에 의존하지 않고 저장소에 저장해야 합니다. 이는 제작된 컨텐츠, 이미지, 코드, 구성 등의 이진 데이터에 적용됩니다. 이를 통해 하나의 API 세트를 사용하여 모든 컨텐츠를 관리하고 복제를 통해 이 컨텐츠의 프로모션을 관리할 수 있습니다. 또한 백업, 로깅 등의 단일 소스를 얻을 수 있습니다.

### &quot;콘텐츠 모델 우선&quot; 디자인 원칙 {#use-the-content-model-first-design-principle} 사용

새 기능을 만들 때는 항상 JCR 컨텐츠 구조를 먼저 디자인하고 기본 Sling 서블릿을 사용하여 컨텐츠를 읽고 쓰는 방법을 살펴봅니다. 이렇게 하면 구현 방식이 즉시 액세스 제어 메커니즘과 제대로 작동하는지 확인하고 불필요한 CRUD 스타일 서블릿을 생성하지 않아도 됩니다.

### RESTful {#be-restful}

서비스는 경로 대신 resourceTypes를 기반으로 정의해야 합니다. 따라서 JCR 액세스 컨트롤을 사용하고, REST 원칙을 준수하고, 요청에 제공된 리소스 및 리소스 해결 프로그램을 사용할 수 있습니다. 또한 보안 강화를 위해 클라이언트에서 서버측 구현 세부 정보를 숨겨 클라이언트측에서 URL을 변경하지 않고도 서버 측에서 URL을 렌더링하는 스크립트를 변경할 수 있습니다.

### 새 노드 유형 {#avoid-defining-new-node-types} 정의 방지

노드 유형은 인프라 레이어에서 낮은 수준에서 작동하며, nt:unstructured, oak:Unstructured, sling:Folder 또는 cq:Page 노드 유형에 할당된 sling:resourceType을 사용하여 대부분의 요구 사항을 충족할 수 있습니다. 노드 유형은 저장소의 스키마와 동일하며 노드 유형을 변경하는 데는 비용이 많이 들 수 있습니다.

### JCR {#adhere-to-naming-conventions-in-the-jcr}의 명명 규칙 준수

이름 지정 규칙을 준수하면 코드 베이스에 일관성이 추가되고 결함 발생률이 낮아지고 시스템에서 작업하는 개발자의 속도가 향상됩니다. AEM 개발 시 Adobe에서 다음 규칙을 사용합니다.

* 노드 이름

   * 모두 소문자
   * 하이픈을 사용한 단어 분리

* 속성 이름

   * 소문자 구분 문자로 시작하는 낙타 사건

* 구성 요소(JSP/HTML)

   * 모두 소문자
   * 하이픈을 사용한 단어 분리

