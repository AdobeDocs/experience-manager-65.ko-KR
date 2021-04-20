---
title: ' [!DNL Assets]에 대한 우수 사례'
description: 배포 및 구성에 따라 달라지는 모범 사례를 식별하고 준수하여 로드되는 시스템 안정성 및 성능을 향상시킵니다.
contentOwner: AG
feature: Asset Management
role: Architect, Administrator
translation-type: tm+mt
source-git-commit: ebe7042b931869c3b4b7204e3ce7afa52d56f0ef
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 0%

---


# [!DNL Assets] {#best-practices-for-assets}에 대한 우수 사례

[!DNL Adobe Experience Manager Assets] 콘텐츠 제작 속도를 높여 비즈니스 목표 달성에 기여하는 고품질의 디지털 마케팅 경험을 전달하는 데 있어 매우 중요한 역할을 하고 있습니다. [!DNL Experience Manager Assets] 내에서 많은 에셋을 사용하여 작업하거나 비디오 및 Dynamic Media을 비롯한 여러 에셋을 정기적으로/정기적으로 업로드하는 경우 시스템 효율성을 높이기 위해 디지털 에셋 관리 경험을 최적화하는 것이 중요합니다.

조직 및 자산 수집, 변환 생성 및 메타데이터 추출에 사용하는 기능을 배치하여 다양한 영역에서 모범 사례를 식별하고 이에 따라 로드 중인 시스템 안정성과 성능이 크게 향상되었습니다.[!DNL Assets]

다음 가이드를 검토하여 필요에 따라 엔터프라이즈 에셋 관리 시스템을 구축 및 관리할 수 있는 지식과 도구를 갖게 됩니다.

* [자산 성능 조정 안내서](/help/assets/performance-tuning-guidelines.md):이 안내서에는 구현 시, 라이브한 후에도 구현 시 언제든지 따를 수 있는 일련의 모범 사례가 포함되어 있으므로 시스템을 최대한 활용할 수 있습니다.
* [자산 크기 조정 안내서](/help/assets/assets-sizing-guide.md):[!DNL Assets] 구현에 대한 견적을 작성할 때 에셋 스토리지, CPU, 메모리, IO 및 네트워크 처리량에 대해 사용할 수 있는 충분한 리소스가 있는지 확인해야 합니다. 이러한 항목 중 많은 항목의 크기를 조정하려면 시스템에 로드되는 자산 수를 이해해야 합니다. 이 안내서에는 크기 조정 도구와 [!DNL Assets] 배포에 필요한 인프라 및 리소스를 측정하기 위한 효율적인 지표를 결정하는 데 도움이 되는 우수 사례가 포함되어 있습니다.
* [자산 마이그레이션 안내서](/help/assets/assets-migration-guide.md):자산을 기존 시스템에서 자산으로 마이그레이션하려면 마이그레이션 프로세스를 간소화하기 위한 몇 가지 단계를 고려해야 합니다. 마이그레이션 안내서에는 위상 적절한 방식으로 자산을 [!DNL Experience Manager]에 가져오기 위해 수행하는 작업에 대한 우수 사례가 포함되어 있습니다. 여기에는 메타데이터 적용, 변환 생성 및 게시 인스턴스에 자산 활성화 등이 포함됩니다.
* [자산 네트워크 고려 사항 문서](/help/assets/assets-network-considerations.md):[!DNL Experience Manager] 배포를 처리할 때 네트워크 토폴로지를 이해하는 것이 네트워크 성능을 이해하고 선택 지점을 식별하며 예상되는 사용자 경험을 설명하는 데 중요합니다. [!DNL Assets] 네트워크 고려 사항 문서에서는 에셋 배포를 디자인할 때 네트워크 관련 사항을 설명합니다.
* [자산 모니터링 안내서](/help/assets/assets-monitoring-best-practices.md):[!DNL Experience Manager] 배포가 배포된 후에는 일반적으로 특정 작업 및 시스템을 모니터링하여 시스템의 무결성을 유지하고 작업을 효율적으로 수행해야 합니다. 모니터링 안내서에는 시스템의 다양한 측면을 모니터링하기 위한 모범 사례가 포함되어 있습니다.
* [Experience Manager 데스크탑 앱 모범 사례](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html): [!DNL Experience Manager] 데스크탑 앱은 데스크탑에 디지털 에셋 관리(DAM) 솔루션을 연결하여 데스크탑에서 바로  [!DNL Experience Manager] 웹 사용자 인터페이스에서 사용할 수 있는 파일을 열 수 있습니다. 데스크탑 앱의 사용이 간편한 워크플로우는 데스크탑 운영 체제에서 제공하는 네트워크 공유 기술을 사용하여 활성화됩니다. 이 안내서에서는 주요 기능 및 [!DNL Experience Manager] 데스크탑 앱의 권장 사용에 대해 설명합니다.
* [Experience Manager 및 Creative Cloud 통합 우수 사례](/help/assets/aem-cc-integration-best-practices.md):배포 [!DNL Experience Manager] 를 다양한 방법 [!DNL Creative Cloud] 으로 통합할 수 있습니다. 통합 및 자산 전송 워크플로우를 간소화하기 위한 몇 가지 모범 사례를 통해 효율성을 극대화할 수 있습니다. 이 안내서에는 [!DNL Assets]과(와) [!DNL Adobe Creative Cloud]의 통합에 대한 우수 사례가 포함되어 있습니다.
