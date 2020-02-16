---
title: 소프트웨어 아키텍처
seo-title: 소프트웨어 아키텍처
description: 소프트웨어 설계 모범 사례
seo-description: 소프트웨어 설계 모범 사례
uuid: a557f6ca-c3f1-486e-a45e-6e1f986fab41
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 92971747-1c74-4917-b5a0-7b79b3ae1e68
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 소프트웨어 아키텍처{#software-architecture}

## 업그레이드 디자인 {#design-for-upgrades}

OOTB 비헤이비어를 확장할 때 업그레이드를 염두에 두어야 합니다. 항상 /apps 디렉토리에 사용자 지정을 적용하고 /libs 디렉토리의 해당 노드 위에 오버레이를 적용하거나 sling:resourceSuperType을 사용하여 기본 비헤이비어를 확장합니다. 새 AEM 버전을 지원하기 위해 일부 수정이 필요할 수 있지만, 이 방법이 수행되는 경우 새 버전이 사용자 지정을 덮어쓰지 않아야 합니다.

### 가능한 경우 템플릿 및 구성 요소 재사용 {#reuse-template-and-components-when-possible}

이렇게 하면 사이트가 보다 일관된 모양과 느낌을 유지하고 코드 유지 관리를 간소화할 수 있습니다. 새 템플릿이 필요한 경우 clientlib 포함과 같은 글로벌 요구 사항을 한 곳에 코딩할 수 있도록 공유 기본 템플릿에서 확장해야 합니다. 새 구성 요소가 필요하면 기존 구성 요소에서 확장할 수 있는 기회를 찾습니다.

### 템플릿 디자인 디자인 {#design-template-designs}

페이지의 각 parsys에 포함할 수 있는 구성 요소를 정의하여 사이트의 모양과 느낌의 일관성을 제어할 수 있습니다. 페이지의 디자인에 대한 액세스를 제한함으로써 다른 작성자가 회사 표준을 따르도록 하면서 개발자 개입 없이 페이지당 허용되는 구성 요소를 수정할 수 있습니다.

### SOLID 아키텍처 개발 {#develop-a-solid-architecture}

SOLID는 다음과 같이 준수해야 하는 5가지 건축 원칙을 설명하는 약어입니다.

* **단일**&#x200B;책임 원칙 - 각 모듈, 클래스, 방법 등은 한 가지 일만 해야 합니다.
* **개방식**/폐쇄적 원칙 - 모듈은 연장용으로 열려 있으며 수정을 위해 닫아야 합니다.
* **Liskov**&#x200B;대체 원칙 - 유형은 하위 유형에 의해 대체되어야 합니다.
* **인터페이스 분리**&#x200B;원칙 - 클라이언트가 사용하지 않는 방법에 의존하지 않아야 합니다.
* **종속성**&#x200B;전환 원칙 - 상위 수준 모듈은 하위 수준 모듈에 의존하지 않아야 합니다. 둘 다 추상화에 의존해야 한다. 추상적인 요소는 세부 사항에 의존해서는 안 됩니다. 세부 사항은 추상적인 요소에 따라 달라야 합니다.

이 5원칙을 따르기 위해 애쓰는 것은 근심을 엄격하게 분리하는 제도가 되어야 한다.

### 견고함 원칙 준수 {#follow-the-robustness-principle}

강건함 원칙은 우리가 보내는 것에 대해 보수적이어야 하지만 우리가 받아들이는 것에 대해 자유주의를 가져야 한다고 말합니다. 즉, 제3자에게 메시지를 보낼 때 사양은 완벽하게 준수해야 하지만 제3자로부터 메시지를 받을 때 메시지의 의미가 분명하다면 부적합 메시지를 수락해야 합니다.

### 자체 모듈에 스파이크 구현 {#implement-spikes-in-their-own-modules}

스파이크 및 테스트 코드는 Agile 소프트웨어 구현의 필수 요소이지만, Adobe는 해당 수준의 감독 없이는 프로덕션 코드 베이스로 들어가지 않도록 해야 합니다. 따라서 자체 모듈에서 스파이크를 만드는 것이 좋습니다.

### 자체 모듈에서 데이터 마이그레이션 스크립트 구현 {#implement-data-migration-scripts-in-their-own-module}

프로덕션 코드 동안 데이터 마이그레이션 스크립트는 일반적으로 사이트를 처음 실행할 때 한 번만 실행됩니다. 따라서 사이트가 라이브되는 즉시 이 코드는 코드가 되지 않습니다. 마이그레이션 스크립트에 의존하는 구현 코드를 구축하지 않도록 하려면 자체 모듈에서 구현해야 합니다. 또한 실행 후 즉시 이 코드를 제거하고 사용 중지하여 시스템에서 사용 불가능한 코드를 제거할 수 있습니다.

### POM 파일에서 게시된 Maven 규칙 팔로우 {#follow-published-maven-conventions-in-pom-files}

Apache가 https://maven.apache.org/developers/conventions/code.html에 스타일 규칙을 [게시했습니다](https://maven.apache.org/developers/conventions/code.html). 이러한 규칙을 따르는 것이 가장 좋습니다. 따라서 새로운 리소스가 빠르게 개발될 수 있습니다.
