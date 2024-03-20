---
title: Dynamic Media - 하이브리드 모드에서 Dynamic Media - S7 모드로 마이그레이션
description: Dynamic Media - 하이브리드 모드의 인스턴스를 Dynamic Media - S7 모드로 마이그레이션하는 방법 알아보기
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User, Admin
feature: Scene7 Mode,Hybrid Mode
exl-id: 07f0803c-4ec4-4745-8214-63370e9d0282
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 52%

---

# Dynamic Media-Hybrid에서 Dynamic Media-Scene7으로 이동 정보 {#about-migrating}

Dynamic Media-Hybrid는 Adobe Experience Manager와 통합한 이전 버전의 Dynamic Media입니다. 하이브리드 버전은 Adobe Experience Manager 6.1에서 처음 도입되었습니다. Adobe은 하이브리드 모드를 계속 지원하지만 기본 모드는 아닙니다. Dynamic Media-Scene7이 기본 모드입니다. 하이브리드 모드는 스마트 자르기 및 파노라마 이미지와 같은 새로운 기능도 지원하지 않지만 Dynamic Media-Scene7은 이를 지원합니다.

Dynamic Media-Hybrid와 Dynamic Media-Scene7의 추가적인 주요 차이점은 다음과 같습니다.

* URL 구조.
* 비디오 처리.
* 이미지 표현물 작성 및 저장.
* 클라우드 구성 및 자격 증명(프로비저닝).

Dynamic Media-Hybrid에서 Dynamic Media-Scene7으로 이동할 때 두 가지 옵션을 사용할 수 있습니다. 첫 번째 옵션은 Experience Manager 시 Dynamic Media-Scene7의 새 인스턴스를 단순히 프로비저닝하는 것입니다. 두 번째 옵션은 Dynamic Media-Hybrid의 기존 인스턴스를 Dynamic Media-Scene7으로 마이그레이션하는 것입니다. 이 옵션은 이동 중에 고려할 단계 및 고려 사항 아래의 표 양식에 요약되어 있습니다.

>[!IMPORTANT]
>
>Adobe은 Dynamic Media-Hybrid 구현을 라이브 프로덕션 인스턴스의 Dynamic Media-Scene7으로 마이그레이션하지 않는 것을 권장합니다.

## 옵션 1 - Experience Manager에서 Dynamic Media-Scene7의 새 인스턴스 프로비저닝 {#provision-new-dms7}

Adobe Experience Manager에서 새로 프로비저닝된 Dynamic Media-Scene7 인스턴스로 새로 고침을 시작해 보십시오. Dynamic Media Cloud Service를 통한 자산 수집 및 처리 외에도 자산 사용, 워크플로우 및 구성 요소에 대한 Adobe 감사를 수행하는 것이 좋습니다. 종종 새로운 기본 기능을 사용하여 사용자 지정 구성 요소 및 워크플로를 바꿀 수 있습니다.

## 옵션 2 - Dynamic Media-Hybrid의 기존 인스턴스를 Dynamic Media-Scene7으로 마이그레이션 {#process-for-migrating}

| 단계 | 작업 | 고려 사항 |
|---|---|---|
| 1 | Dynamic Media-Hybrid 작성자 인스턴스 복제 | 이 마이그레이션 프로세스의 나머지 단계가 성공적으로 완료될 때까지 폴백 목적으로 Dynamic Media-Hybrid 작성자의 기존 인스턴스를 유지합니다. |
| 2 | Dynamic Media-Scene7 모드로 복제된 작성자 인스턴스를 시작합니다. |  |
| 3 | Adobe Experience Manager 클라우드 서비스에서 Dynamic Media-Scene7 자격 증명으로 Dynamic Media를 구성합니다. | Adobe은 Dynamic Media-Scene7 프로비저닝을 승인해야 합니다. 따라서 Adobe에서 지원하지만 제한된 시간 동안만 지원되는 동시 Dynamic MediaM-Hybrid 및 Dynamic Media-Scene7 환경이 있습니다. |
| 4 | 필요에 따라 에셋을 수집할 수 있도록 마이그레이션 번들을 만듭니다.<br>Dynamic Media-Hybrid로 초기 수집 중에 생성된 로컬 PTIFF를 삭제합니다. | 현재 모든 자산을 Dynamic Media-Hybrid 인스턴스에서 사용할 수 있는 경우 해당 복제본에 모든 자산이 이미 포함되어 있습니다. 따라서 번들이 필요하지 않습니다. |
| 5 | 에셋을 Dynamic Media Cloud Service에 동기화할 수 있도록 에셋 업데이트 워크플로를 실행합니다. | Adobe은 압축을 위해 업데이트 워크플로우를 일괄적으로 수행할 것을 권장합니다. |
| 6 | 뷰어, 이미지 및 비디오 사전 설정을 마이그레이션합니다. |  |
| 7 | 각 웹 컨텐츠 관리에서 참조한 자산을 살펴보고 관련 URL을 업데이트합니다. |  |
| 8 | 새로운 Dynamic Media-Scene7 모드를 지원할 모든 사용자 지정 워크플로우를 마이그레이션합니다(수동 업데이트). |  |
| 9 | 웹 컨텐츠 관리 업로드 및 구성을 확인합니다. |  |
| 10 | 확인 후 Dynamic Media-Hybrid 작성자를 비활성화(대체 항목으로 유지)하도록 승인을 받습니다. |  |
| 11 | Dynamic Media-Scene7을 성공적으로 한 달 정도 사용한 후 Dynamic Media-Hybrid 작성자 인스턴스를 삭제합니다. |  |
