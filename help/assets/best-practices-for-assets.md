---
title: 자산에 대한 우수 사례
description: Experience Manager 자산 배포 및 자산 수집, 변환 생성 및 메타데이터 추출에 사용하는 기능에 따라, 다양한 영역에서 모범 사례를 식별하고 이를 준수하여 로드 중인 시스템 안정성과 성능을 크게 향상시킬 수 있습니다.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 76f2df9b1d3e6c2ca7a12cc998d64423d49ebc5b
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 2%

---


# 자산에 대한 우수 사례 {#best-practices-for-assets}

Adobe Experience Manager 자산은 콘텐츠 속도를 높여 비즈니스 목표 달성에 기여하는 고품질의 디지털 마케팅 경험을 전달하는 데 중요한 역할을 합니다. Experience Manager 자산 내에서 많은 양의 자산으로 작업하거나 비디오 및 다이내믹 미디어를 비롯한 다양한 자산을 정기적으로/정기적으로 업로드하는 경우 시스템 효율성을 위해 디지털 자산 관리 경험을 최적화하는 것이 중요합니다.

조직에 자산을 배치한 방법 및 자산 처리, 변환 생성 및 메타데이터 추출과 관련하여 사용하는 기능에 따라, 여러 영역에서 우수 사례를 식별하고 이를 준수함으로써 로드 중인 시스템 안정성과 성능을 크게 향상시킬 수 있습니다.

다음 가이드를 검토한 후 요구 사항에 맞는 엔터프라이즈 에셋 관리 시스템을 구축 및 관리하는 데 필요한 지식과 툴을 사용할 수 있습니다.

* 자산 [성능 조정 가이드](/help/assets/performance-tuning-guidelines.md): 이 안내서에는 구현 중 어느 시점에서나, 실행 후에도 시스템을 최대한 활용할 수 있는 일련의 모범 사례가 포함되어 있습니다.
* 자산 [크기 조정 안내서](/help/assets/assets-sizing-guide.md): 자산 구현에 대한 견적을 작성할 때 자산 저장, CPU, 메모리, IO 및 네트워크 처리량과 관련하여 사용 가능한 충분한 리소스가 있는지 확인해야 합니다. 이러한 항목 중 많은 항목의 크기를 조정하려면 시스템에 로드되는 자산의 수를 이해해야 합니다. 이 안내서에는 자산 배포에 필요한 인프라와 리소스를 측정하기 위한 효율적인 지표와 크기 조정 도구를 결정하는 데 도움이 되는 우수 사례가 포함되어 있습니다.
* 자산 [마이그레이션 안내서](/help/assets/assets-migration-guide.md): 자산을 기존 시스템에서 자산으로 마이그레이션하려면 마이그레이션 프로세스를 간소화하는 몇 가지 단계를 고려해야 합니다. 마이그레이션 가이드는 단계별로 자산을 Experience Manager으로 가져오기 위해 수행하는 작업에 대한 우수 사례를 포함합니다. 여기에는 메타데이터 적용, 변환 생성 및 인스턴스 게시에 에셋 활성화 등이 포함됩니다.
* 자산 [네트워크 고려 사항 문서](/help/assets/assets-network-considerations.md): Experience Manager 배포를 처리할 때 네트워크 토폴로지를 이해하는 것이 네트워크 성능을 이해하고 선택 지점을 식별하며 예상되는 사용자 경험을 설명하는 데 중요합니다. 자산 네트워크 고려 사항 문서에서는 자산 배포를 디자인할 때 네트워크 고려 사항에 대해 설명합니다.
* 자산 [모니터링 안내서](/help/assets/assets-monitoring-best-practices.md): Experience Manager 배포 후 시스템 무결성을 유지하면서 작업의 효율성을 보장하려면 특정 작업과 시스템을 전반적으로 모니터링해야 합니다. 모니터링 안내서에는 시스템의 다양한 측면을 모니터링하기 위한 모범 사례가 포함되어 있습니다.
* [Experience Manager 데스크탑 앱 우수 사례](https://docs.adobe.com/content/help/ko-KR/experience-manager-desktop-app/using/introduction.html): Experience Manager 데스크탑 앱은 데스크탑에 디지털 에셋 관리(DAM) 솔루션을 연결하므로 데스크탑에서 바로 Experience Manager 웹 UI에서 사용할 수 있는 파일을 열 수 있습니다. 데스크탑 앱의 사용이 간편한 워크플로우는 데스크탑 운영 체제에서 제공하는 네트워크 공유 기술을 사용하여 활성화됩니다. 이 안내서에서는 주요 기능 및 Experience Manager 데스크탑 앱 권장 사용에 대해 설명합니다.
* [Experience Manager 및 Creative Cloud 통합 모범 사례](/help/assets/aem-cc-integration-best-practices.md): 다양한 방법으로 Creative Cloud와 Experience Manager 배포를 통합할 수 있습니다. 통합 및 자산 전송 워크플로우를 간소화하기 위한 몇 가지 모범 사례를 통해 효율성을 극대화할 수 있습니다. 이 안내서에는 Adobe Creative Cloud와 에셋 통합에 대한 우수 사례가 포함되어 있습니다.
