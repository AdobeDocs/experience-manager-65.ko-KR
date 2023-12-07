---
title: 소프트웨어 아키텍처
description: Adobe Experience Manager용 소프트웨어 아키텍처에 대한 몇 가지 모범 사례에 대해 알아봅니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: cd4f3b4c-5488-4ca7-9c1e-b4c819fda8e8
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 0%

---

# 소프트웨어 아키텍처{#software-architecture}

## 업그레이드 디자인 {#design-for-upgrades}

OOTB 비헤이비어를 확장할 때는 업그레이드를 염두에 두는 것이 중요합니다. 항상 /apps 디렉토리에 사용자 정의를 적용하고 /libs 디렉토리에 있는 해당 노드의 맨 위에 오버레이하거나 sling:resourceSuperType을 사용하여 기본 동작을 확장합니다. 새 AEM 버전을 지원하려면 일부 수정이 필요할 수 있지만, 이 방법을 따를 경우 새 버전이 사용자 정의를 덮어쓰면 안 됩니다.

### 가능한 경우 템플릿 및 구성 요소 재사용 {#reuse-template-and-components-when-possible}

이렇게 하면 사이트에서 더 일관된 모양과 느낌을 유지하고 코드 유지 관리를 단순화할 수 있습니다. 새 템플릿이 필요한 경우 clientlib 포함과 같은 글로벌 요구 사항을 한 곳에서 코딩할 수 있도록 공유 기본 템플릿에서 확장해야 합니다. 새 구성 요소가 필요한 경우 기존 구성 요소에서 확장할 수 있는 기회를 찾습니다.

### 디자인 템플릿 디자인 {#design-template-designs}

페이지의 각 parsys에 포함할 수 있는 구성 요소를 정의하여 사이트 모양/느낌의 일관성을 제어할 수 있습니다. 페이지의 디자인에 대한 액세스를 제한하여 &quot;슈퍼 작성자&quot;는 다른 작성자가 회사 표준을 따르도록 하면서도 개발자의 개입 없이 페이지당 허용된 구성 요소를 수정할 수 있습니다.

### 견고한 아키텍처 개발 {#develop-a-solid-architecture}

SOLID는 다음과 같이 준수해야 하는 5가지 건축 원칙을 설명하는 약어입니다.

* **S**&#x200B;단일 책임 원칙 - 각 모듈, 클래스, 메서드 등에는 하나의 책임만 있어야 합니다.
* **O** pen/Closed Principle - 모듈은 확장을 위해 열고 수정을 위해 닫아야 합니다.
* **L** iskov 대체 원칙 - 유형은 하위 유형으로 대체 가능합니다.
* **I**&#x200B;인터페이스 분리 원칙 - 어떤 클라이언트도 사용하지 않는 방법에 의존하도록 강요되어서는 안 됩니다.
* **D**&#x200B;종속성 반전 원칙 - 높은 수준의 모듈이 낮은 수준의 모듈에 종속되지 않아야 합니다. 두 가지 모두 추상화에 의존해야 합니다. 추상화는 세부 정보에 의존해서는 안 됩니다. 세부 사항은 추상화에 따라 달라야 합니다.

이러한 5가지 원칙의 준수를 위해 노력하는 것은 우려의 분리가 엄격하게 이루어지는 제도로 귀결되어야 한다.

>[!TIP]
>
>SOLID는 객체 지향 프로그래밍에서 일반적으로 사용되는 개념으로 각 요소는 산업문헌에서 널리 논의되고 있다.
>
>이 정보는 인식을 위해 제시된 짧은 요약에 불과하며 이러한 개념에 대해 더 깊이 숙지하도록 권장됩니다.

### 견고성 원칙 준수 {#follow-the-robustness-principle}

강건성 원칙은 보내는 것에는 보수적이어야 하지만 받아들이는 것에는 자유적이어야 한다고 한다. 즉, 서드파티에게 메시지를 보낼 때 사양을 완전히 준수해야 합니다. 그러나 서드파티로부터 메시지를 받을 때는 메시지의 의미가 명확하기만 하면 준수하지 않는 메시지를 수락해야 합니다.

### 자체 모듈에서 스파이크 구현 {#implement-spikes-in-their-own-modules}

스파이크와 테스트 코드는 모든 애자일 소프트웨어 구현의 일부입니다. 그러나 적절한 수준의 감독 없이 프로덕션 코드 베이스에 도달하지 않도록 하려는 경우 따라서 스파이크는 자체 모듈에서 생성하는 것이 좋습니다.

### 자체 모듈에서 데이터 마이그레이션 스크립트 구현 {#implement-data-migration-scripts-in-their-own-module}

데이터 마이그레이션 스크립트는 프로덕션 코드에서 실행되지만 사이트의 초기 시작 시 한 번만 실행됩니다. 따라서 사이트가 활성 상태이면 스크립트는 데드 코드가 됩니다. 마이그레이션 스크립트에 의존하는 구현 코드를 빌드하지 않도록 하려면 자체 모듈에서 구현해야 합니다. 이렇게 하면 실행 후 즉시 이 코드를 제거하고 폐기할 수 있으므로 시스템에서 데드 코드를 제거할 수 있습니다.

### POM 파일에서 게시된 Maven 규칙 준수 {#follow-published-maven-conventions-in-pom-files}

Apache는에 스타일 규칙을 게시했습니다. [https://maven.apache.org/developers/conventions/code.html](https://maven.apache.org/developers/conventions/code.html). 새로운 리소스가 빠르게 올라오기 쉬우므로 이러한 규칙을 따르는 것이 가장 좋습니다.
