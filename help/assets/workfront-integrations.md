---
title: '`[!DNL Experience Manager Assets] 통합 [!DNL Adobe Workfront]`'
description: 통합 소개 [!DNL Assets] 및 [!DNL Workfront]
role: Admin,Leader,Architect
feature: Integrations
exl-id: 57e2bffe-8094-4557-99c8-7b482681687e
source-git-commit: d83242c8fa6a8cd627a6db24f3c45fcaeae45b2b
workflow-type: tm+mt
source-wordcount: '1170'
ht-degree: 5%

---

# [!DNL Adobe Experience Manager Assets] 통합 [!DNL Adobe Workfront] {#assets-integration-overview}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기를 클릭하십시오.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/integrations/workfront-integrations.html?lang=en) |
| AEM 6.5 | 이 문서 |
| AEM 6.4 | [여기를 클릭하십시오.](https://experienceleague.adobe.com/docs/experience-manager-64/assets/integrations/workfront-integrations.html?lang=en) |

[!DNL Adobe Workfront]는 업무의 전체 라이프사이클을 한 곳에서 관리할 수 있도록 도와주는 작업 관리 애플리케이션입니다. 통합 [!DNL Workfront] 및 [!DNL Adobe Experience Manager Assets] 작업 및 디지털 자산 관리를 동적으로 연결하여 컨텐츠 속도 및 출시 시간을 향상시킬 수 있습니다. Workfront에서 작업을 관리하는 컨텍스트 내에서 사용자는 필요한 문서 및 이미지에 액세스할 수 있습니다.

다음 [!DNL Workfront for Experience Manager enhanced connector] 종단 간 워크플로우를 통해 비즈니스 프로세스를 향상시키고 개인화된 종단 간 클라이언트 경험과 중앙 스토리지를 제공합니다. Adobe은 두 솔루션을 통합하는 표준 커넥터와 향상된 커넥터를 제공합니다. 비교에 대해서는 아래의 지원되는 기능을 참조하고 를 참조하십시오 [의 새로운 기능 [!DNL enhanced connector]](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

[!DNL Workfront for Experience Manage enhanced connector] 조직을 사용하여 다음을 수행할 수 있습니다.

* Workfront에서 연결된 Experience Manager 폴더를 자동으로 만들고 Workfront Portfolio, 프로그램 및 프로젝트를 기반으로 폴더를 구성합니다.
* Workfront 프로젝트 메타데이터를 연결된 Experience Manager 폴더와 동기화합니다.
* Experience Manager 메타데이터 업데이트와 새 버전.
* Experience Manager 워크플로우를 사용하여 구성 가능한 조건을 기반으로 Workfront 개체 상태를 설정합니다.
* 자산을 Experience Manager 게시 환경 또는 Brand Portal에 게시합니다.

플랫폼 지원 및 [향상된 커넥터를 위한 사전 요구 사항](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>* Adobe을 사용하려면 [!DNL Adobe Workfront for Experience Manager enhanced connector] 인증된 파트너를 통해 [!DNL Adobe Professional Services]. 인증된 파트너 또는 [!DNL Adobe Professional Services]Adobe에서 지원하지 않습니다.
>
>* Adobe은 [!DNL Adobe Workfront] 및 [!DNL Adobe Experience Manager] 이렇게 하면 커넥터가 이중화됩니다. 이러한 경우 고객은 이 커넥터를 사용하는 상태에서 전환해야 할 수 있습니다.
>
>* Adobe은 향상된 커넥터 버전 1.7.4 이상을 지원합니다. 이전 사전 릴리스 및 사용자 지정 버전은 지원되지 않습니다. 향상된 커넥터 버전을 확인하려면 `digital.hoodoo` 의 왼쪽 창에서 사용할 수 있는 그룹 [패키지 관리자](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=ko-KR).
>
>* 자세한 내용은 [Experience Manager Assets Enhanced Connector용 Workfront의 파트너 인증 시험](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). 시험에 대한 자세한 내용은 [시험 안내서](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).


## 서로 다른 통합 비교 [!DNL Assets] 및 [!DNL Workfront] {#feature-parity-matrix}

다음은 다양한 유형의 통합을 통해 사용할 수 있는 기능에 대한 세부 사항입니다 [!DNL Assets] 및 [!DNL Workfront].

| 기능 | 설명 | [!DNL Workfront] 및 [!DNL Assets Essentials] *커넥터 없음(OOTB)* | [!DNL Workfront for Experience Manager enhanced connector] *커넥터 필요* | Workfront 및 [!DNL Experience Manager as a Cloud Service] *커넥터 없음(OOTB)* |
|----|----|----|-----|-----|
| 배포 메서드 | 적합한 [!DNL Assets] 제공 | Assets Essentials | Adobe Managed Services, 온-프레미스 | 클라우드 서비스 |
| **일반** |
| 에서 디지털 파일 보내기 [!DNL Workfront] to [!DNL Assets] | 최신 버전의 WF 문서를 AEM Assets에 업로드하여 새로운 버전의 문서로 연결할 수 있습니다. | ✓ | ✓ | ✓ |
| 수동으로 AEM 폴더를 Workfront 개체에 연결 | 기존 AEM 폴더를 Workfront 폴더로 연결할 수 있으며 하위 자산이 새 Workfront 문서로 연결됩니다. | ✓ | ✓ | ✓ |
| 링크 [!DNL Assets] Workfront 개체 | AEM의 기존 자산은 새 Workfront 문서에 연결되거나 기존 문서의 새 버전으로 연결할 수 있습니다. | ✓ | ✓ | ✓ |
| 연결된 폴더에 추가된 자산은 자동으로 AEM으로 전송됩니다 | 문서가 연결된 폴더에 추가되면 연결된 자산이 자동으로 AEM Assets에 새 자산으로 업로드됩니다. | ✓ | ✓ | ✓ |
| Workfront 내에서 연결된 AEM Assets 다운로드 | 자산이 Workfront에 연결되어 있으면 사용자는 자산의 바이트를 다운로드할 수 있습니다. | ✓ | ✓ | ✓ |
| Workfront 내에서 AEM Assets 검색 | Workfront의 AEM Assets 선택기를 사용하면 자산을 전체 텍스트 검색으로 검색할 수 있습니다. | ✓ | ✓ | ✓ |
| Workfront 내에서 AEM 폴더 검색 | Workfront의 AEM Assets 선택기에서 폴더를 전체 텍스트 검색할 수 있습니다. | ✓ | ✓ | ✓ |
| Workfront 내에서 AEM 폴더 계층 구조 보기 및 탐색 | Workfront의 AEM Assets 선택기를 사용하면 AEM에 설정된 사용자의 연결된 액세스 제어 및 권한에 의해 제한된 AEM Assets 계층 구조를 검색할 수 있습니다. | ✓ | ✓ | ✓ |
| AEM 타임라인에서 자산 버전 추적 | Workfront과 AEM 간에 문서 버전 기록을 유지합니다. | ✓ | ✓ | ✓ |
| Workfront에서 AEM Assets에서 자산 연결 해제 | AEM의 기존 연결된 자산은 연결된 Workfront 문서에서 연결을 해제할 수 있습니다. 이렇게 해도 AEM 내의 원래 자산은 삭제되지 않습니다. | ✓ | ✓ | ✓ |
| Workfront에서 AEM Assets에 새로 버전이 지정된 자산 추가 | Workfront의 문서에 새로 추가된 버전이 추가되면 사용자는 새 버전을 AEM으로 보내 기존 버전을 바꿀 수 있습니다. | ✓ | ✓ | ✓ |
| AEM에 직접 사용자를 클릭할 때 Workfront에 연결된 자산 | 사용자는 Workfront 내에서 연결된 자산을 미리 보기 위해 AEM으로 이동됩니다. | ✓ | ✓ | 예정된 날짜 |
| Workfront에서 연결된 AEM 폴더를 자동으로 만들기 | 프로젝트 상태를 사용하여 Workfront에서 연결된 AEM 폴더를 자동으로 만듭니다. Workfront Portfolio, 프로그램 및 프로젝트를 기반으로 AEM 폴더를 자동으로 구성합니다. | 아니요 | ✓ | 아니요 |
| Workfront에서 AEM 리포지토리로 직접 이동합니다. | Workfront 내에 구성된 사용 가능한 AEM 리포지토리로 이동할 수 있습니다. | ✓ | 아니요 | ✓ |
| Workfront에서 연결된 AEM 폴더 만들기 | 문서 탭에서 사용할 수 있는 옵션을 사용하여 Workfront에서 연결된 AEM 폴더를 수동으로 만듭니다. | ✓ | 아니요 | ✓ |
| 주석 동기화 | 다음에서 자산에 대한 주석을 자동으로 동기화 [!DNL Workfront] to [!DNL Assets] | 아니요 | ✓ | 아니요 |
| 단일 AEM 환경에 연결하는 여러 Workfront 환경 지원 | 여러 Workfront 환경의 사용자가 단일 AEM 환경에 연결할 수 있습니다. | ✓ | 아니요 | ✓ |
| 단일 Workfront 환경에 연결하는 여러 AEM 환경 지원 | 단일 Workfront 환경 내의 사용자는 여러 AEM 환경 간에 자산을 전송하거나 연결할 수 있습니다. | ✓ | ✓ | ✓ |
| **메타데이터** |
| AEM Assets에 Workfront 자산 메타데이터 매핑 | Workfront 개체 및 사용자 지정 양식 속성은 AEM 자산 메타데이터 속성에 매핑될 수 있습니다. 초기 업로드/링크 시 값이 푸시됩니다. | ✓ | ✓ | ✓ |
| Workfront에서 문서 사용자 지정 Forms 자동 만들기 | AEM 워크플로우를 사용하여 Workfront 문서, 작업 및 문제에 사용자 지정 양식을 첨부합니다. | 아니요 | ✓ | 아니요 |
| AEM Assets과 Workfront 간 메타데이터의 양방향 자동 업데이트 | AEM Assets과 Workfront 간의 메타데이터를 자동으로 업데이트합니다. 자산은 처음에 Workfront에서 AEM으로 푸시되어야 하며, 양방향 메타데이터 업데이트가 제대로 작동하려면 Workfront 자산 메타데이터가 AEM 자산에 매핑되어야 합니다. | 아니요 | ✓ | 아니요 |
| AEM에 매핑된 메타데이터를 위한 Workfront의 실시간 보기 | Workfront 문서 세부 사항 및 문서 요약 패널에서 AEM에 업데이트된 매핑된 메타데이터를 봅니다. | ✓ | 아니요 | ✓ |
| 업데이트된 Workfront 메타데이터를 AEM에 대한 실시간 푸시 | 자산이나 자산의 새 버전을 삭제하지 않고 매핑된 Workfront 메타데이터를 AEM에 자동으로 업데이트합니다. | ✓ | 아니요 | ✓ |
| AEM Assets 폴더에 Workfront 메타데이터 매핑 | Workfront 프로젝트 메타데이터를 연결된 AEM 폴더와 동기화합니다. | 아니요 | ✓ | ✓ |
| 새 버전으로 AEM 메타데이터 업데이트 | AEM에서 구성을 수행하여 Workfront의 새로 버전이 지정된 자산도 메타데이터의 변경 사항을 사용하여 푸시하는지 여부를 결정할 수 있습니다. | 아니요 | ✓ | 아니요 |
| Workfront에서 사용자 지정 Forms 변경 시 AEM 메타데이터 자동 업데이트 | AEM에서는 Workfront에서 문서 양식 업데이트를 구독할 수 있습니다. 따라서 Workfront 문서 사용자 지정 양식 메타데이터에 대한 모든 업데이트는 매핑된 AEM 메타데이터 필드의 값을 수정합니다. | 아니요 | ✓ | 아니요 |
| **워크플로우(기본 제공)** |
| 연결된 자산에 새 증명 버전 만들기 | Workfront에서 자산을 연결하면 증명을 자동으로 생성할 수 있습니다. | 아니요 | 사용자 정의 | 아니요 |
| Workfront 개체에 상태 설정 | AEM 워크플로우를 사용하여 구성 가능한 조건을 기반으로 Workfront 개체 상태 설정 | 아니요 | ✓ | 예정된 날짜 |
| AEM 게시 환경 또는 Brand Portal에 자산 게시 | Workfront 사용자에게 연결된 자산을 AEM 게시 환경 또는 Brand Portal에 자동으로 게시할 수 있는 옵션을 제공합니다. | 아니요 | ✓ | 예정된 날짜 |
