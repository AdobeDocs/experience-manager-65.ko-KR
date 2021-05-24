---
title: 소프트웨어 아키텍처
seo-title: 소프트웨어 아키텍처
description: 소프트웨어 아키텍처 모범 사례
seo-description: 소프트웨어 아키텍처 모범 사례
uuid: a557f6ca-c3f1-486e-a45e-6e1f986fab41
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 92971747-1c74-4917-b5a0-7b79b3ae1e68
exl-id: cd4f3b4c-5488-4ca7-9c1e-b4c819fda8e8
source-git-commit: 423e17dadf2e506eb68b37851dde5e68ed950866
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 0%

---

# 소프트웨어 아키텍처{#software-architecture}

## 업그레이드 디자인 {#design-for-upgrades}

OOTB 동작을 확장할 때 업그레이드를 염두에 두어야 합니다. /apps 디렉토리에 사용자 지정 사항을 항상 적용하고 /libs 디렉토리의 해당 노드 위에 오버레이하거나 sling:resourceSuperType을 사용하여 기본 동작을 확장합니다. 새 AEM 버전을 지원하기 위해 일부 수정 사항이 필요할 수 있지만, 이 방법이 따를 경우 새 버전이 사용자 지정 사항을 덮어쓰지 않아야 합니다.

### 가능한 경우 템플릿 및 구성 요소를 다시 사용하십시오 {#reuse-template-and-components-when-possible}

이렇게 하면 사이트에서 더 일관된 모양과 느낌을 유지하고 코드 유지 관리를 간소화할 수 있습니다. 새 템플릿이 필요한 경우 clientlib 포함 과 같은 글로벌 요구 사항을 한 위치에 코딩할 수 있도록 공유 기본 템플릿에서 확장해야 합니다. 새 구성 요소가 필요한 경우 기존 구성 요소에서 확장할 기회를 찾습니다.

### 디자인 템플릿 디자인 {#design-template-designs}

페이지에서 각 parsys에 포함할 수 있는 구성 요소를 정의함으로써 사이트의 모양/느낌의 일관성을 제어할 수 있습니다. 페이지에서 디자인에 대한 액세스를 제한하여 &quot;수퍼 작성자&quot;가 다른 작성자가 회사 표준을 따르도록 하면서도 개발자 개입 없이 페이지당 허용되는 구성 요소를 수정할 수 있도록 할 수 있습니다.

### SOLID 아키텍처 개발 {#develop-a-solid-architecture}

SOLID는 다음과 같이 부착해야 하는 5가지 아키텍처 원칙을 설명하는 약어입니다.

* ****&#x200B;단일 책임 원칙 - 각 모듈, 클래스, 방법 등은 하나의 책임만 가져야 합니다.
* ****&#x200B;오픈/닫힌 원칙 - 모듈은 확장을 위해 개방되고 수정을 위해 닫아야 합니다.
* **** Liskov 대체 원칙 - 유형은 하위 유형에 의해 교체해야 합니다.
* ****&#x200B;인터페이스 격리 원칙 - 클라이언트가 사용하지 않는 방법에 따라 종속되어야 하지 않습니다.
* ****&#x200B;종속성 버전 전환 원칙 - 높은 수준 모듈은 낮은 수준 모듈에 종속되어서는 안 됩니다. 둘 다 추상화에 의존해야 한다. 추상들은 세부 사항에 의존해서는 안 된다. 세부 사항은 추상에 따라 다릅니다.

5원칙을 지키고자 애쓰는 것은 근심분리 제도를 가지게 될 것이다.

>[!TIP]
>
>SOLID는 객체 지향 프로그래밍에서 일반적으로 사용되는 개념이며 각 요소는 업계 문학에서 폭넓게 논의됩니다.
>
>이것은 인식에 대해 제시된 짧은 요약이며 이러한 개념을 보다 깊이 숙지하는 것이 좋습니다.

### 견고성 원칙 {#follow-the-robustness-principle}을 따르십시오

견고성 원칙은 우리가 보내는 것에 대해 보수적이어야 하지만 우리가 받아들이는 것에 대해 자유적이어야 한다는 것입니다. 즉, 제3자에게 메시지를 보낼 때는 규격에 완전히 부합해야 하지만 제3자로부터 메시지를 받을 때는 메시지의 의미가 분명하면 규정을 지키지 않는 메시지를 수락해야 합니다.

### 자체 모듈 {#implement-spikes-in-their-own-modules}에 스파이크 구현

스파이크와 테스트 코드는 모든 Agile 소프트웨어 구현의 필수적인 부분이지만, 적절한 수준의 감독 없이 프로덕션 코드 베이스에 들어가지 않도록 해야 합니다. 따라서 자체 모듈에서 스파이크를 만드는 것이 좋습니다.

### 자체 모듈 {#implement-data-migration-scripts-in-their-own-module}에서 데이터 마이그레이션 스크립트를 구현합니다

데이터 마이그레이션 스크립트는 프로덕션 코드가 있는 동안 일반적으로 사이트를 처음 시작할 때 한 번만 실행됩니다. 따라서 사이트가 라이브되면 이것은 데드 코드가 됩니다. 마이그레이션 스크립트에 의존하는 구현 코드를 빌드하지 않도록 하려면 자체 모듈에서 구현해야 합니다. 또한 실행 직후 이 코드를 제거하고 사용 취소할 수 있으므로 시스템에서 데드 코드를 제거할 수 있습니다.

### POM 파일 {#follow-published-maven-conventions-in-pom-files}에서 게시된 Maven 규칙을 따르십시오

Apache는 [https://maven.apache.org/developers/conventions/code.html](https://maven.apache.org/developers/conventions/code.html)에 스타일 규칙을 게시했습니다. 따라서 새 리소스를 신속하게 찾을 수 있게 되므로 이러한 규칙을 준수하는 것이 가장 좋습니다.
