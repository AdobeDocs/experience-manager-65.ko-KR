---
title: ' [!DNL Assets]에 대한 우수 사례'
description: 배포 및 구성에 따라 달라지는 우수 사례를 식별하고 준수하여 로드 중인 시스템 안정성 및 성능을 향상시킵니다.
contentOwner: AG
feature: 자산 관리
role: Architect, Administrator
exl-id: 6b50f1b3-9c1c-47c8-a43e-6f40c42a41cc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 0%

---

# [!DNL Assets] {#best-practices-for-assets}에 대한 우수 사례

[!DNL Adobe Experience Manager Assets] 는 컨텐츠 속도를 높여 비즈니스 목표 달성에 기여하는 고품질 디지털 마케팅 경험을 제공하는데 중요한 부분입니다. [!DNL Experience Manager Assets] 내에서 자산을 대량으로 사용하거나 비디오 및 Dynamic Media을 포함한 다양한 자산을 정기적으로/정기적으로 업로드하는 경우 시스템 효율성을 위해 디지털 자산 관리 경험을 최적화해야 합니다.

조직에 대해 [!DNL Assets]을 배치한 방법과 자산 수집, 표현물 생성 및 메타데이터 추출에 사용하는 기능에 따라 다양한 영역에서 우수 사례를 식별하고 준수하면 로드 중인 시스템 안정성 및 성능이 크게 향상됩니다.

다음 안내서를 검토한 후 사용자의 요구 사항에 맞는 엔터프라이즈 자산 관리 시스템을 구축하고 관리할 수 있는 지식과 도구가 제공됩니다.

* [자산 성능 조정 가이드](/help/assets/performance-tuning-guidelines.md):이 안내서에는 시스템을 최대한 활용할 수 있도록 구현 중 어느 시점에서든 따를 수 있는 모범 사례 세트가 포함되어 있습니다.
* [자산 크기 조정 가이드](/help/assets/assets-sizing-guide.md):[!DNL Assets] 구현에 대한 추정치를 작성할 때 자산 저장, CPU, 메모리, 입출력 및 네트워크 처리량 측면에서 사용 가능한 리소스가 충분한지 확인하는 것이 중요합니다. 이러한 항목 중 많은 항목의 크기를 조정하려면 시스템에 로드되는 자산의 수를 이해해야 합니다. 이 안내서에는 [!DNL Assets] 배포에 필요한 인프라 및 리소스를 추정하는 효율적인 지표를 결정하는 데 도움이 되는 모범 사례가 포함되어 있습니다.
* [자산 마이그레이션 안내서](/help/assets/assets-migration-guide.md):자산을 기존 시스템에서 Assets로 마이그레이션하려면 마이그레이션 프로세스를 간소화하기 위해 몇 가지 단계를 고려해야 합니다. 마이그레이션 안내서에는 단계를 기준으로 자산을 [!DNL Experience Manager]에 가져오기 위해 수행하는 작업에 대한 우수 사례가 포함되어 있습니다. 여기에는 메타데이터 적용, 변환 생성 및 자산 게시 인스턴스가 포함됩니다.
* [자산 네트워크 고려 사항 문서](/help/assets/assets-network-considerations.md):[!DNL Experience Manager] 배포를 처리할 때는 네트워크 성능을 이해하고 선택점을 식별하며 예상 사용자 경험을 설명하는 데 네트워크 토폴로지를 이해하는 것이 중요합니다. [!DNL Assets] 네트워크 고려 사항 문서에서는 자산 배포를 디자인할 때 네트워크 고려 사항에 대해 설명합니다.
* [자산 모니터링 안내서](/help/assets/assets-monitoring-best-practices.md):[!DNL Experience Manager] 배포가 배포되면 일반적으로 특정 작업 및 시스템을 모니터링하여 시스템의 무결성과 작업 효율성을 확인해야 합니다. 모니터링 안내서에는 시스템의 다양한 측면을 모니터링하기 위한 모범 사례가 포함되어 있습니다.
* [Experience Manager 데스크탑 앱 모범 사례](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html): [!DNL Experience Manager] 데스크탑 앱은 DAM(디지털 자산 관리) 솔루션을 데스크탑에 연결하여 데스크탑에서 바로  [!DNL Experience Manager] 웹 사용자 인터페이스에서 사용할 수 있는 파일을 열 수 있습니다. 데스크탑 앱의 사용하기 쉬운 워크플로우는 데스크탑 운영 체제에서 제공하는 네트워크 공유 기술을 사용하여 활성화됩니다. 이 안내서에서는 주요 기능 및 [!DNL Experience Manager] 데스크탑 앱의 권장 사용에 대해 설명합니다.
* [Experience Manager 및 Creative Cloud 통합 우수 사례](/help/assets/aem-cc-integration-best-practices.md):여러 가지 방법으로 배포 [!DNL Experience Manager] 를  [!DNL Creative Cloud] 와 통합할 수 있습니다. 통합 및 자산 전송 워크플로우를 간소화하는 몇 가지 모범 사례를 따르면 최대 효율성을 달성할 수 있습니다. 이 안내서에는 [!DNL Assets]과 [!DNL Adobe Creative Cloud]을 통합하는 방법에 대한 우수 사례가 포함되어 있습니다.
