---
title: 번역 우수 사례
seo-title: 번역 우수 사례
description: 번역 프로젝트를 시작하고 실행하는 데 도움이 되는 Adobe 엔지니어링 및 컨설팅 팀이 컴파일한 우수 사례를 찾아보십시오.
seo-description: 번역 프로젝트를 시작하고 실행하는 데 도움이 되는 Adobe 엔지니어링 및 컨설팅 팀이 컴파일한 우수 사례를 찾아보십시오.
uuid: 3bac1d73-9696-4c9b-8bdd-6f00fac40cf7
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features, best-practices
content-type: reference
discoiquuid: 1554010e-a1d1-4edf-b28f-9eead8f83b4a
feature: 언어 복사
exl-id: 01a81c4b-cb30-4f7e-b281-7194ebb5fc70
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 0%

---

# 번역 우수 사례{#translation-best-practices}

## 일반 {#general}

글로벌 웹 환경을 만들거나 확장하는 것은 복잡한 과정일 수 있지만 AEM을 잘 이해하고 계획하면 노력을 단순화하고 글로벌 비즈니스 목표를 지원할 수 있습니다.

* **첫 번째** 사이트를 구현하기 전에 글로벌 확장을 계획합니다. 사이트가 짧은 시간에 구현되었을 때 글로벌 커버리지에 대한 기존 사이트를 적용하는 것은 일반적으로 시작 시 글로벌 확장을 계획하는 것보다 어렵습니다.

   * 조직의 현지화 성숙도 상태를 평가합니다. 전역 확장을 지원할 **tools**, **processes** 및 **resources**&#x200B;가 있는지 확인합니다.
   * **전역 규정** 및 **지역 언어 환경 설정**&#x200B;을 알아 두십시오. 변화하는 글로벌 비즈니스 환경을 수용할 수 있는 유연한 컨텐츠 구조 및 프로세스를 설계합니다.

* 글로벌 비즈니스를 지원하고 MSM 및 사용자 권한과 같은 AEM 메커니즘을 사용하여 선택한 모델을 적용하는 **거버넌스** 모델을 결정합니다. 예를 들어 컨텐츠가 중앙 작성 및 지역/국가에 &quot;푸시&quot; 또는 &quot;풀&quot;되는지 여부를 결정합니다. 지리적 위치에서 잠금이 해제되고 변경할 수 있는 콘텐츠를 결정합니다. 번역 시작 및 관리를 담당하는 사람을 결정합니다.
* 리소스가 허용되면 필요한 도구, 프로세스 및 공급업체 관계에 대한 전문 지식을 개발할 수 있는 중앙 팀의 번역 활동을 관리하는 것이 가장 좋습니다.
* **글로벌 구조 및**&#x200B;프로세스를 계획,  ****   **** 프로토타이핑 및 테스트하여 해당 조직이 비즈니스를 지원하고 지역의 이해 관계자의 필요한 지원을 받을 수 있도록 합니다.

## 사이트 구조 {#site-structure}

* 사이트 구조를 디자인할 때 먼저 콘텐츠를 살펴보고 언어 컨텐츠가 작성되는 위치와 위치를 결정합니다. 이 위치는 사이트의 최상위 수준이어야 합니다.
* 가장 좋은 방법은 최상위 작성과 국가 사이트 간에 3개 수준 이하의 **언어 기반 구조**&#x200B;입니다.
* **W3C 표준**&#x200B;을 따르는 언어/국가 사이트 이름 지정 규칙을 사용합니다.
* 지역 및 국가별로 콘텐츠가 배포되는 방식을 결정합니다. 언어를 공유하는 국가를 고려해 보십시오. 번역된 컨텐츠를 검토 및 수정한 다음 해당 언어를 공유하는 국가 사이트에 푸시하거나 가져올 수 있는 활성화되지 않은 페이지 레이어인 언어 마스터를 만드는 것이 좋습니다.
* 언어 마스터를 만드는 방법에는 두 가지가 있습니다.언어 사본 사용 및 MSM/live copy 사용.

   * 언어 복사 접근 방식은 AEM 기본 번역 통합 프레임워크에서 사용하는 방법이므로 가장 쉽게 시작할 수 있는 방법입니다. 프레임워크는 기본 언어(예: 영어) 마스터에서 언어 마스터로 컨텐츠 변경 사항을 처음부터 쉽게 전파하고 변환할 수 있도록 하는 사용자 인터페이스를 제공합니다. 그러나 프로젝트가 증가함에 따라 워크플로우 자동화는 증가된 페이지 및/또는 언어 수의 번역을 관리하는 데 점점 더 필요합니다.
   * MSM/live copy 접근 방식은 사이트가 더 크고 복잡한 고급 사용 사례를 위한 대안이 될 수 있습니다. 처음부터 영어 마스터와 언어 마스터의 복잡한 상속 관계를 처리하고 기존 번역을 덮어쓰는 위험을 줄이려면 강력한 거버넌스 및 워크플로우 자동화가 필요합니다. 일부 번역 커넥터의 도움을 받아 이 처리를 수행할 수 있습니다. 자세한 내용은 [MSM 및 다국어 사이트](/help/sites-administering/msm-best-practices.md#msm-and-multilingual-websites)를 참조하십시오.

* 마스터 언어에 전역 변형이 있는 경우, MSM을 사용하여 변환에 사용할 글로벌 마스터에서 Live Copy를 만드는 옵션이 있습니다. 예를 들어, 미국 영어 마스터에서 전역 작성이 수행되는 경우 국제 영어 마스터를 Live Copy로 만들고 다른 언어로 번역하는 기준을 만듭니다.
* MSM을 사용하여 번역된 언어 마스터에서 국가 사이트를 만들고 동일한 언어를 공유하는 사이트에 콘텐츠를 롤아웃합니다. 예를 들어, 프랑스어 마스터는 프랑스, 벨기에 및 스위스 사이트로 롤아웃될 수 있습니다.
* 구현을 시작하기 전에 먼저 계획, 프로토타입 및 테스트를 수행하십시오.

## 번역 프로세스 및 메서드 {#translation-processes-and-methods}

* 번역 및 관련 로컬라이제이션 활동에 대한 전문 지식을 가진 **로컬라이제이션 서비스 공급자(LSP)**&#x200B;에 참여하십시오. LSP는 효율성을 향상시키고 번역 비용을 절감하기 위해 다양한 리소스와 기술을 제공하여 글로벌 비즈니스 규모에 맞게 확장할 수 있도록 지원합니다.

   * 일부 LSP는 서비스 및 기술 제공업체입니다. 또한 많은 LSP가 번역 플랫폼에 참여할 수 있도록 허용하는 독립 실행형 기술 공급업체도 있습니다.
   * **AEM Translation Framework**&#x200B;에서는 기계 및 인간 번역 모두를 위한 다양한 번역 기술 공급자와의 통합을 지원합니다.
   * AEM 시스템](/help/sites-administering/translation.md)에서 [LSP 커넥터를 통합하여 컨텐츠 번역을 자동화하는 방법 또는 테스트를 위한 번역 프로젝트를 수동으로 작성, 내보내기 및 가져오는 방법과 LSP 또는 번역 기술 공급자가 없는 경우에 대해 알아봅니다.

* 컨텐츠에 가장 적합한 **번역 방법**&#x200B;을 선택합니다.

   * **사용자** 번역은 메시지 및 품질 기대치가 높고 마케팅 페이지와 같은 사이트에서 일정 시간 컨텐츠가 실행되는 컨텐츠에 가장 적합합니다.
   * **게시 시간이** 중요하거나, 품질 기대치가 완화되거나, 인간 번역 비용이 너무 많이 드는 경우 대량 번역 시 좋은 선택이 될 수 있습니다. 지원 기술 자료 및 사용자가 생성한 컨텐츠는 일반적으로 기계로 번역됩니다.

* 로컬라이제이션 서비스 공급자, Adobe 컨설팅 및 시스템 통합자의 전문 지식을 활용하여 다국어 사이트 구조를 계획, 프로토타입 및 테스트할 수 있습니다.
