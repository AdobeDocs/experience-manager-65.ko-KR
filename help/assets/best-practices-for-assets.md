---
title: 에 대한 우수 사례 [!DNL Assets]
description: 배포 및 구성에 따라 달라지는 모범 사례를 식별하고 준수하여 로드 중 시스템 안정성과 성능을 향상시킵니다.
contentOwner: AG
feature: Asset Management
role: Architect, Admin
exl-id: 6b50f1b3-9c1c-47c8-a43e-6f40c42a41cc
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 1%

---

# 에 대한 우수 사례 [!DNL Assets] {#best-practices-for-assets}

[!DNL Adobe Experience Manager Assets] 는 콘텐츠 속도를 높여 비즈니스 목표 달성에 기여하는 고품질 디지털 마케팅 경험을 제공하는 데 있어 중요한 부분입니다. 내에서 많은 에셋으로 작업하는 경우 [!DNL Experience Manager Assets] 또는 비디오 및 Dynamic Media을 비롯한 수많은 에셋을 정기적으로/정기적으로 업로드하여 디지털 에셋 관리 환경을 최적화하는 것은 시스템 효율성을 위해 매우 중요합니다.

위치 지정 방법에 따라 [!DNL Assets] 조직 및 에셋 수집, 렌디션 생성 및 메타데이터 추출에 사용하는 기능을 위해 다양한 영역에서 모범 사례를 식별하고 준수하면 로드 중 시스템 안정성과 성능이 크게 향상됩니다.

다음 안내서를 검토한 후 요구 사항에 맞는 엔터프라이즈 자산 관리 시스템을 구축하고 관리할 수 있는 지식과 도구를 갖추게 됩니다.

* 다음 [자산 성능 조정 가이드](/help/assets/performance-tuning-guidelines.md): 이 안내서에는 시스템을 최대한 활용할 수 있도록 라이브 후에도 구현의 모든 시점에서 따를 수 있는 모범 사례 세트가 포함되어 있습니다.
* 다음 [자산 크기 조정 안내서](/help/assets/assets-sizing-guide.md): 다음에 대한 예상 값을 작성할 때: [!DNL Assets] 구현에서는 자산 저장소, CPU, 메모리, IO 및 네트워크 처리량 측면에서 사용 가능한 리소스가 충분히 있는지 확인하는 것이 중요합니다. 이러한 항목의 수를 조정하려면 시스템에 로드되는 에셋의 수를 이해해야 합니다. 이 안내서에는 배포에 필요한 인프라 및 리소스 추정을 위한 효율적인 지표를 결정하는 데 도움이 되는 모범 사례가 포함되어 있습니다 [!DNL Assets] 크기 조정 도구를 사용할 수 있습니다.
* 다음 [자산 마이그레이션 안내서](/help/assets/assets-migration-guide.md): 기존 시스템에서 에셋으로 에셋을 마이그레이션하려면 마이그레이션 프로세스를 간소화하는 몇 가지 단계를 고려해야 합니다. 마이그레이션 안내서에는 자산을 로 가져오기 위해 수행하는 작업에 대한 모범 사례가 포함되어 있습니다 [!DNL Experience Manager] 단계적인 방식으로. 여기에는 메타데이터 적용, 렌디션 생성 및 게시 인스턴스에 대한 에셋 활성화가 포함됩니다.
* 다음 [자산 네트워크 고려 사항 문서](/help/assets/assets-network-considerations.md): 처리 시 [!DNL Experience Manager] 배포, 네트워크 토폴로지 이해는 네트워크 성능을 이해하고, 콜포인트를 식별하며, 예상되는 사용자 경험을 설명하는 데 중요합니다. 다음 [!DNL Assets] 네트워크 고려 사항 문서에서는 자산 배포를 디자인할 때의 네트워크 고려 사항에 대해 설명합니다.
* 다음 [에셋 모니터링 안내서](/help/assets/assets-monitoring-best-practices.md): 다음 이후 [!DNL Experience Manager] 배포가 배포되면 일반적으로 특정 작업과 시스템을 모니터링하여 시스템의 무결성과 운영의 효율성을 보장해야 합니다. 모니터링 안내서에는 시스템의 다양한 측면을 모니터링하기 위한 모범 사례가 포함되어 있습니다.
* [Experience Manager 데스크탑 앱 우수 사례](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html): [!DNL Experience Manager] 데스크탑 앱은 DAM(디지털 자산 관리) 솔루션을 데스크탑과 연결하여 [!DNL Experience Manager] 데스크탑에서 직접 웹 사용자 인터페이스. 데스크탑 앱의 사용하기 쉬운 워크플로는 데스크탑 운영 체제에서 제공하는 네트워크 공유 기술을 사용하여 활성화됩니다. 이 안내서에서는 주요 기능 및 권장 사용 방법에 대해 설명합니다. [!DNL Experience Manager] 데스크탑 앱입니다.
* [Experience Manager 및 Creative Cloud 통합 우수 사례](/help/assets/aem-cc-integration-best-practices.md): 다음을 통합할 수 있습니다. [!DNL Experience Manager] 배포 [!DNL Creative Cloud] 다양한 방식으로. 통합 및 자산 전송 워크플로우를 간소화하는 몇 가지 모범 사례를 따라 최대의 효율성을 달성하는 데 도움이 됩니다. 이 안내서에는 통합에 대한 모범 사례가 포함되어 있습니다 [!DNL Assets] 포함 [!DNL Adobe Creative Cloud].
