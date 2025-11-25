---
title: ' [!DNL Assets]에 대한 모범 사례'
description: 배포 및 구성에 따라 달라지는 모범 사례를 식별하고 준수하여 로드 중 시스템 안정성과 성능을 향상시킵니다.
contentOwner: AG
feature: Asset Management
role: Developer, Admin
exl-id: 6b50f1b3-9c1c-47c8-a43e-6f40c42a41cc
solution: Experience Manager, Experience Manager Assets
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 0%

---

# [!DNL Assets]에 대한 모범 사례 {#best-practices-for-assets}

[!DNL Adobe Experience Manager Assets]은(는) 콘텐츠 속도를 높여 비즈니스 목표 달성에 기여하는 고품질 디지털 마케팅 경험을 제공하는 데 있어 중요한 부분입니다. [!DNL Experience Manager Assets] 내에서 많은 자산을 사용하여 작업하거나 비디오 및 Dynamic Media를 포함하여 많은 자산을 정기적으로/정기적으로 업로드하는 경우 시스템 효율성을 위해 디지털 자산 관리 환경을 최적화하는 것이 중요합니다.

조직에 대해 [!DNL Assets]을(를) 배치한 방법과 자산 수집, 렌디션 생성 및 메타데이터 추출에 사용하는 기능에 따라 다양한 영역에서 모범 사례를 식별하고 준수하면 로드 중인 시스템의 안정성과 성능이 크게 향상됩니다.

다음 안내서를 검토한 후 요구 사항에 맞는 엔터프라이즈 자산 관리 시스템을 구축하고 관리할 수 있는 지식과 도구를 갖추게 됩니다.

* [Assets 성능 조정 가이드](/help/assets/performance-tuning-guidelines.md): 이 안내서에는 시스템을 최대한 활용할 수 있도록 실행 후에도 구현의 모든 시점에서 따를 수 있는 모범 사례 집합이 포함되어 있습니다.
* [Assets 크기 조정 가이드](/help/assets/assets-sizing-guide.md): [!DNL Assets] 구현에 대한 예상 값을 작성할 때 에셋 저장소, CPU, 메모리, IO 및 네트워크 처리량 측면에서 사용 가능한 리소스가 충분한지 확인하는 것이 중요합니다. 이러한 항목의 수를 조정하려면 시스템에 로드되는 에셋의 수를 이해해야 합니다. 이 안내서에는 [!DNL Assets] 및 크기 조정 도구를 배포하는 데 필요한 인프라 및 리소스 추정에 대한 효율적인 지표를 결정하는 데 도움이 되는 모범 사례가 포함되어 있습니다.
* [Assets 마이그레이션 안내서](/help/assets/assets-migration-guide.md): 기존 시스템에서 Assets으로 자산을 마이그레이션하려면 마이그레이션 프로세스를 간소화하는 여러 단계를 고려해야 합니다. 마이그레이션 안내서에는 단계별로 자산을 [!DNL Experience Manager]&#x200B;(으)로 가져오기 위해 수행하는 작업에 대한 모범 사례가 포함되어 있습니다. 여기에는 메타데이터 적용, 렌디션 생성 및 게시 인스턴스에 대한 에셋 활성화가 포함됩니다.
* [Assets 네트워크 고려 사항 문서](/help/assets/assets-network-considerations.md): [!DNL Experience Manager] 배포를 처리할 때 네트워크 성능을 이해하고, 가늠점을 식별하며, 예상되는 사용자 경험을 설명하는 데 네트워크 토폴로지를 이해하는 것이 중요합니다. [!DNL Assets] 네트워크 고려 사항 문서에서 자산 배포를 디자인할 때의 네트워크 고려 사항을 설명합니다.
* [Assets 모니터링 안내서](/help/assets/assets-monitoring-best-practices.md): [!DNL Experience Manager] 배포가 배포된 후 일반적으로 특정 작업과 시스템을 모니터링하여 시스템 무결성과 작업의 효율성을 보장해야 합니다. 모니터링 안내서에는 시스템의 다양한 측면을 모니터링하기 위한 모범 사례가 포함되어 있습니다.
* [Experience Manager 데스크톱 앱 모범 사례](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html): [!DNL Experience Manager] 데스크톱 앱은 데스크톱에서 직접 [!DNL Experience Manager] 웹 사용자 인터페이스에서 사용할 수 있는 파일을 열 수 있도록 DAM(디지털 자산 관리) 솔루션을 데스크톱과 연결합니다. 데스크탑 앱의 사용하기 쉬운 워크플로는 데스크탑 운영 체제에서 제공하는 네트워크 공유 기술을 사용하여 활성화됩니다. 이 안내서에서는 [!DNL Experience Manager] 데스크톱 앱의 주요 기능 및 권장 사용에 대해 설명합니다.
* [Experience Manager 및 Creative Cloud 통합 모범 사례](/help/assets/aem-cc-integration-best-practices.md): [!DNL Experience Manager] 배포를 [!DNL Creative Cloud]과(와) 다양한 방법으로 통합할 수 있습니다. 통합 및 자산 전송 워크플로우를 간소화하는 몇 가지 모범 사례를 따라 최대의 효율성을 달성하는 데 도움이 됩니다. 이 안내서에는 [!DNL Assets]과(와) [!DNL Adobe Creative Cloud]의 통합에 대한 모범 사례가 포함되어 있습니다.
