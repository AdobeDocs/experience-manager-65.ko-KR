---
title: 다이내믹 미디어 - 하이브리드 모드에서 다이내믹 미디어로 마이그레이션 - S7 모드
description: 다이내믹 미디어 - 하이브리드 모드 - 다이내믹 미디어로 마이그레이션 - S7 모드
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
translation-type: tm+mt
source-git-commit: 7aba1f3b492a07fe502f95535a94c8054a044eb5

---


# Dynamic Media-Hybrid에서 Dynamic Media-Scene7으로 이동 정보 {#about-migrating}

Dynamic Media-Hybrid는 Adobe Experience Manager와 이전 버전의 Dynamic Media 통합입니다. 하이브리드 버전은 AEM(Adobe Experience Manager) 6.1에서 처음 도입되었습니다.Adobe는 하이브리드 모드를 계속 지원하지만 기본 모드는 아닙니다(Dynamic Media-Scene7이 기본 모드임). 또한 스마트 자르기 및 파노라마 이미지와 같은 새로운 기능을 지원하지 않습니다. 반면 Dynamic Media-Scene7은 그렇지 않습니다.

Dynamic Media-Hybrid와 Dynamic Media-Scene7의 추가적인 주요 차이점은 다음과 같습니다.

* URL 구조.
* 비디오 통합
* 이미지 표현물의 작성 및 저장.
* 클라우드 구성 및 자격 증명(프로비저닝).

Dynamic Media-Hybrid에서 Dynamic Media-Scene7으로 이동할 때 두 가지 옵션을 사용할 수 있습니다. 첫 번째 옵션은 AEM에서 Dynamic Media-Scene7의 새 인스턴스를 간단하게 제공하는 것입니다. 두 번째 옵션은 Dynamic Media-Hybrid의 기존 인스턴스를 Dynamic Media-Scene7으로 마이그레이션하는 것입니다. 이 옵션은 아래 표의 윤곽선을 표시합니다. 이동 중에 수행할 단계 및 고려 사항입니다.

>[!IMPORTANT]
>
>Dynamic Media-Hybrid 구현은 라이브 프로덕션 인스턴스에서 Dynamic Media-Scene7으로 마이그레이션하지 않는 것이 좋습니다.

## 옵션 1 - AEM 파섹 {#provision-new-dms7}

Adobe Experience Manager에서 새롭게 제공된 Dynamic Media-Scene7 인스턴스로 시작하는 것이 좋습니다. Dynamic Media Cloud Service를 통해 에셋을 수집 및 처리할 수 있을 뿐만 아니라 에셋 사용, 워크플로우 및 구성 요소에 대한 Adobe 감사를 수행하는 것이 좋습니다. 대부분의 경우 사용자 정의 구성 요소 및 워크플로우는 최신 기본 기능으로 대체할 수 있습니다.

## 옵션 2 - Dynamic Media-Hybrid의 기존 인스턴스를 Dynamic Media-Scene7으로 마이그레이션 {#process-for-migrating}

| 단계 | 작업 | 고려 사항 |
|---|---|---|
| 1 | Dynamic Media-Hybrid 작성자 인스턴스 복제 | 이 마이그레이션 프로세스의 나머지 단계가 성공적으로 완료될 때까지 대체 목적으로 기존 Dynamic Media-Hybrid 작성자 인스턴스를 유지해야 합니다. |
| 2 | Dynamic Media-Scene7 모드에서 복제된 작성자 인스턴스를 시작합니다. |  |
| 3 | Adobe Experience Manager Cloud Services에서 Dynamic Media-Scene7 자격 증명을 사용하여 Dynamic Media를 구성합니다. | Adobe는 Dynamic Media-Scene7 제공을 승인해야 합니다. 제한된 기간 동안 지원되는 동시 Dynamic MediaM-Hybrid 및 Dynamic Media-Scene7 환경이 있습니다. |
| 4 | 필요에 따라 에셋을 인제스트할 마이그레이션 번들 만들기<br>Dynamic Media-Hybrid로 초기 통합 중에 생성된 로컬 PTIFF를 삭제합니다. | 현재 모든 자산을 Dynamic Media-Hybrid 인스턴스에서 사용할 수 있는 경우 해당 복제의 모든 에셋이 이미 포함됩니다. 따라서 번들은 필요하지 않습니다. |
| 5 | 자산 업데이트 워크플로우를 실행하여 자산을 Dynamic Media Cloud Service에 동기화합니다. | Adobe에서는 비교를 위해 업데이트 워크플로우를 일괄적으로 수행하는 것이 좋습니다. |
| 6 | 뷰어, 이미지 및 비디오 사전 설정을 마이그레이션합니다. |  |
| 7 | 각 웹 컨텐츠 관리 참조 에셋을 살펴보고 관련 URL을 업데이트합니다. |  |
| 8 | 모든 사용자 정의 워크플로우를 마이그레이션하여 새로운 Dynamic Media-Scene7 모드를 지원합니다(수동 업데이트). |  |
| 9 | 웹 컨텐츠 관리 업로드 및 구성을 확인합니다. |  |
| 10 | 확인 후 Dynamic Media-Hybrid Author 비활성화(폴백으로 유지)에 대한 승인을 받습니다. |  |
| 11 | Dynamic Media-Scene7을 성공적으로 한 달 정도 사용한 후 Dynamic Media-Hybrid 작성자 인스턴스를 삭제합니다. |  |
