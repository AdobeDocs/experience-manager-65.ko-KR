---
title: 컨텐츠 아키텍처
seo-title: 컨텐츠 아키텍처
description: 컨텐츠 아키텍처 팁(힌트 - 모든 것이 컨텐츠)
seo-description: Adobe Experience Manager(AEM)에서 컨텐츠 아키텍처를 위한 팁입니다. (힌트 - 모든 것이 컨텐츠임)
uuid: fef2bf0f-70ec-4621-8479-a62b7e1fbc07
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: ca46b74c-6114-458b-98c0-2a93abffcdc3
exl-id: bcebbdb4-20b9-4c2d-8a87-013549d686c1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 1%

---

# 컨텐츠 아키텍처{#content-architecture}

## David의 모델 {#follow-david-s-model}을 따르십시오

데이비드의 모델은 몇 년 전 David Nuescheler에 의해 쓰여졌지만, 그 아이디어는 오늘 그대로 적용됩니다. David의 Model의 주요 원칙은 다음과 같습니다.

* 데이터는 먼저, 구조는 나중에 나옵니다. 그럴지도
* 콘텐츠 계층 구조를 만들면 안 됩니다.
* 작업 공간은 `clone()`, `merge()` 및 `update()`용입니다.
* 같은 이름의 형제자매를 주의하라.
* 참고는 해롭다고 여겨진다.
* 파일은 파일입니다.
* ID는 악합니다.

David의 모델은 Jackrabbit Wiki( [https://wiki.apache.org/jackrabbit/DavidsModel](https://wiki.apache.org/jackrabbit/DavidsModel))에 있습니다.

### 모든 내용이 {#everything-is-content} 컨텐츠입니다.

모든 것은 데이터베이스와 같은 별도의 타사 데이터 소스에 의존하지 않고 저장소에 저장되어야 합니다. 이는 작성된 컨텐츠, 이미지, 코드, 구성 등의 이진 데이터에 적용됩니다. 이를 통해 한 세트의 API를 사용하여 모든 콘텐츠를 관리하고 복제를 통해 이 콘텐츠의 프로모션을 관리할 수 있습니다. 또한 백업, 로깅 등의 단일 소스를 얻을 수 있습니다.

### &quot;컨텐츠 모델 우선&quot; 디자인 원칙 {#use-the-content-model-first-design-principle} 사용

새 기능을 작성할 때는 항상 JCR 컨텐츠 구조를 먼저 디자인한 다음 기본 Sling 서블릿을 사용하여 컨텐츠를 읽고 쓰는 것을 고려하십시오. 이렇게 하면 구현이 기본 액세스 제어 메커니즘에서 제대로 작동하는지 확인하고 불필요한 CRUD 스타일 서블릿을 생성하지 않도록 할 수 있습니다.

### RESTful {#be-restful}

서블릿은 경로 대신 resourceTypes를 기반으로 정의해야 합니다. 따라서 JCR 액세스 제어를 사용하고, REST 원칙을 준수하고, 요청에 제공된 리소스 및 리소스 확인자를 사용할 수 있습니다. 또한 보안을 강화하기 위해 클라이언트측에서 서버측 구현 세부 사항을 숨기면서 클라이언트 측에서 URL을 변경할 필요 없이 서버 측에서 URL을 렌더링하는 스크립트를 변경할 수 있습니다.

### 새 노드 유형 {#avoid-defining-new-node-types}을 정의하지 마십시오

노드 유형은 인프라 계층에서 낮은 수준에서 작동하며, 대부분의 요구 사항은 nt:un구조화되지 않음, oak:Unstructured, sling:Folder 또는 cq:Page 노드 유형에 지정된 sling:resourceType을 사용하여 충족할 수 있습니다. 노드 유형은 저장소의 스키마와 같으며 노드 유형을 변경하는 것은 매우 비용이 많이 들 수 있습니다.

### JCR {#adhere-to-naming-conventions-in-the-jcr}에서 이름 지정 규칙을 따릅니다.

명명 규칙을 준수하면 코드 베이스에 일관성이 추가되고, 결함 발생률이 낮아지고 시스템에서 작업하는 개발자의 속도가 빨라집니다. 다음 규칙은 AEM 개발 시 Adobe에서 사용됩니다.

* 노드 이름

   * 모두 소문자
   * 하이픈을 사용한 단어 분리

* 속성 이름

   * 소문자 구분 문자로 시작하는 카멜 케이스

* 구성 요소(JSP/HTML)

   * 모두 소문자
   * 하이픈을 사용한 단어 분리
