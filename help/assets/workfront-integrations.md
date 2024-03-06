---
title: '[!DNL Experience Manager Assets] 과 통합 [!DNL Adobe Workfront]'
description: 간 통합 소개 [!DNL Assets] 및 [!DNL Workfront]
role: Admin,Leader,Architect
feature: Integrations
exl-id: 57e2bffe-8094-4557-99c8-7b482681687e
hide: true
source-git-commit: 0aa929021aa724e4ec18d49fea26f8c0b0538bdc
workflow-type: tm+mt
source-wordcount: '1174'
ht-degree: 9%

---

# [!DNL Adobe Experience Manager Assets] 과 통합 [!DNL Adobe Workfront] {#assets-integration-overview}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/integrations/workfront-integrations.html?lang=en) |
| AEM 6.5 | 이 문서 |

[!DNL Adobe Workfront] 는 업무의 전체 라이프사이클을 한 곳에서 관리할 수 있도록 도와주는 작업 관리 애플리케이션입니다. 통합 대상 [!DNL Workfront] 및 [!DNL Adobe Experience Manager Assets] 에서는 작업과 디지털 에셋 관리를 본질적으로 연결하여 콘텐츠 속도와 마켓 출시 속도를 개선할 수 있습니다. Workfront에서 작업을 관리하는 맥락에서 사용자는 필요한 문서 및 이미지에 액세스할 수 있습니다.

다음 [!DNL Workfront for Experience Manager enhanced connector] 엔드 투 엔드 워크플로우를 통해 향상된 비즈니스 프로세스를 구현하고 개인화된 엔드 투 엔드 클라이언트 경험과 중앙 스토리지를 제공합니다. Adobe은 표준 커넥터와 두 솔루션을 통합할 수 있는 향상된 커넥터를 제공합니다. 비교에 대해서는 아래의 지원되는 기능 을 참조하십시오. [의 새로운 기능 [!DNL enhanced connector]](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

[!DNL Workfront for Experience Manage enhanced connector] 를 통해 조직은 다음과 같은 작업을 수행할 수 있습니다.

* Workfront에서 연결된 Experience Manager 폴더를 자동으로 만들고 Workfront Portfolio, 프로그램 및 프로젝트를 기반으로 폴더를 구성합니다.
* Workfront 프로젝트 메타데이터를 연결된 Experience Manager 폴더와 동기화합니다.
* 새 버전으로 Experience Manager 메타데이터 업데이트.
* Experience Manager 워크플로우를 사용하여 구성 가능한 조건에 따라 Workfront 개체 상태를 설정합니다.
* Experience Manager 게시 환경 또는 Brand Portal에 자산을 게시합니다.

플랫폼 지원 및 [향상된 커넥터에 대한 사전 요구 사항](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>* Adobe을 사용하려면 [!DNL Adobe Workfront for Experience Manager enhanced connector] 인증된 파트너를 통해서만 또는 [!DNL Adobe Professional Services]. 공인 파트너 없이 구축 및 구성된 경우 또는 [!DNL Adobe Professional Services], Adobe에서 지원되지 않습니다.
>
>* Adobe은 다음에 대한 업데이트를 릴리스할 수 있습니다. [!DNL Adobe Workfront] 및 [!DNL Adobe Experience Manager] 따라서 이 커넥터가 이중화됩니다. 이 경우 고객은 이 커넥터를 사용하지 않도록 전환해야 할 수 있습니다.
>
>* Adobe은 향상된 커넥터 버전 1.7.4 이상을 지원합니다. 이전 프리릴리스 및 사용자 지정 버전은 지원되지 않습니다. 향상된 커넥터 버전을 확인하려면 `digital.hoodoo` 의 왼쪽 창에서 사용할 수 있는 그룹 [패키지 관리자](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en).
>
>* 다음을 참조하십시오 [Workfront for Experience Manager Assets 강화 커넥터에 대한 파트너 인증 시험](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). 시험에 대한 자세한 내용은 [시험 안내서](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).

## 간의 다양한 통합 비교 [!DNL Assets] 및 [!DNL Workfront] {#feature-parity-matrix}

다음은 다양한 유형의 통합을 통해 사용할 수 있는 기능에 대한 세부 정보입니다 [!DNL Assets] 및 [!DNL Workfront].

| 기능 | 설명 | [!DNL Workfront] 및 [!DNL Assets Essentials] *커넥터 없음(기본 제공)* | [!DNL Workfront for Experience Manager enhanced connector] *커넥터 필요* | Workfront 및 [!DNL Experience Manager as a Cloud Service] *커넥터 없음(기본 제공)* |
|----|----|----|-----|-----|
| 배포 메서드 | 다음에 적합 [!DNL Assets] 제공. | Assets Essentials | Adobe Managed Services, On-Premise | Cloud Service |
| **일반** |
| 에서 디지털 파일 보내기 [!DNL Workfront] 끝 [!DNL Assets] | WF 문서의 최신 버전은 문서의 새 버전으로 연결된 AEM Assets에 업로드할 수 있습니다. | ✓ | ✓ | ✓ |
| 수동으로 AEM 폴더에 Workfront 개체 연결 | 기존 AEM 폴더는 Workfront 폴더로 연결되고 하위 자산은 새 Workfront 문서로 연결됩니다. | ✓ | ✓ | ✓ |
| 링크 [!DNL Assets] Workfront 개체로 | AEM의 기존 에셋을 새 Workfront 문서에 연결하거나 기존 문서의 새 버전으로 연결할 수 있습니다. | ✓ | ✓ | ✓ |
| 연결된 폴더에 추가된 에셋은 자동으로 AEM으로 전송됩니다. | 연결된 폴더에 문서가 추가되면 연결된 에셋이 자동으로 새 에셋으로 AEM Assets에 업로드됩니다. | ✓ | ✓ | ✓ |
| Workfront 내에서 연결된 AEM Assets 다운로드 | 에셋이 Workfront에 연결되면 에셋의 바이트를 다운로드할 수 있습니다. | ✓ | ✓ | ✓ |
| Workfront 내에서 AEM Assets 검색 | Workfront의 AEM Assets 선택기를 사용하여 에셋을 전체 텍스트 검색할 수 있습니다. | ✓ | ✓ | ✓ |
| Workfront 내에서 AEM 폴더 검색 | Workfront의 AEM Assets 선택기를 사용하여 폴더를 전체 텍스트 검색할 수 있습니다. | ✓ | ✓ | ✓ |
| Workfront 내에서 AEM 폴더 계층 구조 보기 및 탐색 | Workfront의 AEM Assets 선택기를 사용하면 AEM에서 설정된 사용자와 관련된 액세스 제어 및 권한에 의해 제한된 AEM Assets 계층 구조를 검색할 수 있습니다. | ✓ | ✓ | ✓ |
| AEM 타임라인에서 자산 버전 추적 | Workfront과 AEM 간 문서 버전 내역 유지 | ✓ | ✓ | ✓ |
| Workfront의 AEM Assets에서 자산 연결 해제 | AEM에서 연결된 기존 에셋은 연결된 Workfront 문서에서 연결 해제할 수 있습니다. AEM 내의 원본 에셋은 삭제되지 않습니다. | ✓ | ✓ | ✓ |
| Workfront에서 AEM Assets에 새 버전 에셋 추가 | Workfront의 문서에 새로 추가된 버전이 있으면 사용자는 새 버전을 AEM으로 전송하여 기존 버전을 바꿀 수 있습니다. | ✓ | ✓ | ✓ |
| AEM에 직접 사용자 클릭 시 Workfront에 연결된 에셋 | Workfront 내에서 연결된 자산을 미리 보기 위해 AEM으로 이동합니다. | ✓ | ✓ | 예정 |
| Workfront에서 연결된 AEM 폴더 자동 생성 | 프로젝트 상태를 사용하여 Workfront에서 연결된 AEM 폴더를 자동으로 만듭니다. Workfront Portfolio, 프로그램 및 프로젝트를 기반으로 AEM 폴더를 자동으로 구성합니다. | 아니요 | ✓ | 아니요 |
| Workfront에서 AEM 저장소로 직접 이동합니다. | 사용자가 Workfront 내에 구성된 사용 가능한 AEM 저장소로 이동할 수 있도록 허용합니다. | ✓ | 아니요 | ✓ |
| Workfront에서 연결된 AEM 폴더 만들기 | 문서 탭에서 사용할 수 있는 옵션을 사용하여 Workfront에서 연결된 AEM 폴더를 수동으로 만듭니다. | ✓ | 아니요 | ✓ |
| 댓글 동기화 중 | 에서 에셋에 대한 주석을 자동으로 동기화 [!DNL Workfront] 끝 [!DNL Assets] | 아니요 | ✓ | 아니요 |
| 단일 AEM 환경에 연결하는 여러 Workfront 환경 지원 | 여러 Workfront 환경의 사용자는 단일 AEM 환경에 연결할 수 있습니다. | ✓ | 아니요 | ✓ |
| 단일 Workfront 환경에 연결하는 여러 AEM 환경 지원 | 단일 Workfront 환경 내의 사용자는 여러 AEM 환경 간에 에셋을 전송하거나 연결할 수 있습니다. | ✓ | ✓ | ✓ |
| **메타데이터** |
| Workfront 에셋 메타데이터를 AEM Assets에 매핑 | Workfront 개체 및 사용자 지정 양식 속성이 AEM 에셋 메타데이터 속성에 매핑될 수 있습니다. 값은 초기 업로드/링크에서 푸시됩니다. | ✓ | ✓ | ✓ |
| Workfront에서 자동으로 문서 사용자 지정 Forms 만들기 | AEM 워크플로우를 사용하여 Workfront 문서, 작업 및 문제에 사용자 정의 양식을 첨부합니다. | 아니요 | ✓ | 아니요 |
| AEM Assets과 Workfront 간 메타데이터의 양방향 자동 업데이트 | AEM Assets과 Workfront 간에 메타데이터를 자동으로 업데이트합니다. 에셋은 처음에 Workfront에서 AEM으로 푸시해야 하며 양방향 메타데이터 업데이트가 제대로 작동하려면 Workfront 에셋 메타데이터를 AEM assets에 매핑해야 합니다. | 아니요 | ✓ | 아니요 |
| AEM에 매핑된 메타데이터에 대한 Workfront의 실시간 보기 | Workfront 문서 세부 정보 및 문서 요약 패널에서 AEM에 대해 업데이트된 매핑된 메타데이터를 봅니다. | ✓ | 아니요 | ✓ |
| 업데이트된 Workfront 메타데이터를 AEM에 실시간으로 푸시 | 에셋 또는 에셋의 새 버전을 다시 푸시하지 않고 매핑된 Workfront 메타데이터를 AEM으로 자동으로 업데이트합니다. | ✓ | 아니요 | ✓ |
| Workfront 메타데이터를 AEM Assets 폴더에 매핑 | Workfront 프로젝트 메타데이터를 연결된 AEM 폴더와 동기화합니다. | 아니요 | ✓ | ✓ |
| 새 버전으로 AEM 메타데이터 업데이트 | AEM의 구성을 통해 Workfront에서 새로 버전이 지정된 에셋이 해당 메타데이터에 대한 변경 사항을 푸시하는지 여부를 확인할 수 있습니다. | 아니요 | ✓ | 아니요 |
| Workfront에서 사용자 지정 Forms의 변경 사항에 대한 AEM 메타데이터 자동 업데이트 | AEM을 사용하면 Workfront의 문서 양식에 대한 업데이트를 구독할 수 있습니다. 따라서 Workfront 문서 사용자 정의 양식 메타데이터에 대한 모든 업데이트는 매핑된 AEM 메타데이터 필드의 값을 편집합니다. | 아니요 | ✓ | 아니요 |
| **워크플로우(기본 제공)** |
| 연결된 자산에 대한 새 증명 버전 만들기 | Workfront에서 자산을 연결할 때 증명을 자동으로 생성할 수 있습니다. | 아니요 | 사용자 정의 | 아니요 |
| Workfront 개체의 상태 설정 | AEM 워크플로우를 사용하여 구성 가능한 조건에 따라 Workfront 객체 상태 설정 | 아니요 | ✓ | 예정 |
| AEM 게시 환경 또는 Brand Portal에 자산 게시 | Workfront 사용자에게 연결된 자산을 AEM 게시 환경 또는 Brand Portal에 자동으로 게시하는 옵션을 제공합니다. | 아니요 | ✓ | 예정 |
