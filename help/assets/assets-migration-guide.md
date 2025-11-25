---
title: 일괄 에셋 마이그레이션
description: 자산을  [!DNL Adobe Experience Manager] (으)로 가져오고, 메타데이터를 적용하고, 렌디션을 생성하고, 인스턴스를 게시하도록 활성화하는 방법에 대해 설명합니다.
contentOwner: AG
role: Developer, Admin
feature: Migration,Renditions,Asset Management
exl-id: 184f1645-894a-43c1-85f5-8e0d2d77aa73
solution: Experience Manager, Experience Manager Assets
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '1739'
ht-degree: 6%

---

# 자산을 일괄적으로 마이그레이션하는 방법 {#assets-migration-guide}

자산을 [!DNL Adobe Experience Manager]&#x200B;(으)로 마이그레이션할 때 고려해야 할 단계가 몇 가지 있습니다. 자산 및 메타데이터를 현재 홈에서 추출하는 방법은 구현마다 크게 다르므로 이 문서의 범위를 벗어납니다. 그러나 이 문서에서는 이러한 자산을 [!DNL Experience Manager]&#x200B;(으)로 가져오고, 메타데이터를 적용하고, 렌디션을 생성하고, 인스턴스를 게시하도록 활성화하는 방법에 대해 설명합니다.

## 사전 요구 사항 {#prerequisites}

이 방법론의 단계를 실제로 수행하기 전에 [Assets 성능 조정 팁](performance-tuning-guidelines.md)의 지침을 검토하고 구현하십시오. 최대 동시 작업 구성과 같은 여러 단계를 수행하면 로드 시 서버의 안정성과 성능이 크게 향상됩니다. 파일 데이터 저장소 구성과 같은 다른 단계는 시스템이 에셋으로 로드된 후 수행하기가 훨씬 더 어렵습니다.

>[!NOTE]
>
>다음 자산 마이그레이션 도구는 [!DNL Experience Manager]에 속하지 않으며 Adobe에서 지원되지 않습니다.
>
>* ACS AEM Tools Tag Maker
>* ACS AEM 도구 CSV 자산 가져오기
>* ACS Commons Bulk Workflow Manager
>* ACS Commons 빠른 작업 관리자
>* 합성 워크플로우
>
>This software are open source and covered by the [Apache v2 License](https://adobe-consulting-services.github.io/pages/license.html). To ask a question or report an issue, visit the respective [GitHub Issues for ACS AEM Tools](https://github.com/Adobe-Consulting-Services/acs-aem-commons/issues) and [ACS AEM Commons](https://github.com/Adobe-Consulting-Services/acs-aem-tools/issues).

## [!DNL Experience Manager]&#x200B;(으)로 마이그레이션 {#migrating-to-aem}

자산을 [!DNL Experience Manager]&#x200B;(으)로 마이그레이션하려면 몇 가지 단계가 필요하며, 이를 단계별 프로세스로 간주해야 합니다. 마이그레이션 단계는 다음과 같습니다.

1. 워크플로우를 비활성화합니다.
1. 태그를 로드합니다.
1. 에셋을 수집합니다.
1. 렌디션 처리.
1. 에셋을 활성화합니다.
1. 워크플로우를 활성화합니다.

![chlimage_1-223](assets/chlimage_1-223.png)

### 워크플로우 비활성화 {#disabling-workflows}

마이그레이션을 시작하기 전에 [!UICONTROL DAM 자산 업데이트] 워크플로에 대한 시작 관리자를 비활성화하십시오. 모든 자산을 시스템으로 수집한 다음 워크플로우를 일괄적으로 실행하는 것이 가장 좋습니다. 마이그레이션이 수행되는 동안 이미 라이브하는 경우 이러한 활동이 업무 외 시간에 실행되도록 예약할 수 있습니다.

### 태그 로드 {#loading-tags}

이미지에 적용할 태그 분류가 이미 준비되었을 수 있습니다. CSV 자산 가져오기 및 메타데이터 프로필에 대한 [!DNL Experience Manager] 지원과 같은 도구는 자산에 태그를 적용하는 프로세스를 자동화할 수 있지만 태그를 시스템으로 로드해야 합니다. [ACS AEM 도구 태그 메이커](https://adobe-consulting-services.github.io/acs-aem-tools/features/tag-maker/index.html) 기능을 사용하면 시스템에 로드되는 Microsoft Excel 스프레드시트를 사용하여 태그를 채울 수 있습니다.

### 에셋 수집 {#ingesting-assets}

자산이 시스템으로 흡수될 때 성능과 안정성은 중요한 관심사이다. 많은 양의 데이터를 시스템에 로드하기 때문에 시스템이 제대로 작동하는지 확인하여 필요한 시간을 최소화하고 시스템 오버로드를 방지해야 합니다. 그러면 시스템 충돌이 발생할 수 있으며, 특히 이미 운영 중인 시스템에서 그러할 수 있습니다.

에셋을 시스템으로 로드하는 방법에는 HTTP를 사용하는 푸시 기반 접근 방식과 JCR API를 사용하는 풀 기반 접근 방식이 있습니다.

#### HTTP를 통해 보내기 {#pushing-through-http}

Adobe의 Managed Services 팀은 Glutton이라는 도구를 사용하여 데이터를 고객 환경에 로드합니다. Glutton은 [!DNL Experience Manager] 배포의 한 디렉터리에서 다른 디렉터리로 모든 자산을 로드하는 작은 Java 응용 프로그램입니다. Glutton 대신 Perl 스크립트와 같은 도구를 사용하여 에셋을 저장소에 게시할 수도 있습니다.

https를 통해 푸시하는 접근 방식을 사용하는 데에는 두 가지 주요 단점이 있습니다.

1. 자산은 HTTP를 통해 서버로 전송해야 합니다. 이 작업에는 상당한 오버헤드가 필요하고 시간이 많이 소요되므로 마이그레이션을 수행하는 데 걸리는 시간이 길어집니다.
1. 자산에 적용해야 하는 태그 및 사용자 지정 메타데이터가 있는 경우, 이 접근 방식에서는 자산을 가져온 후 이 메타데이터를 자산에 적용하기 위해 실행해야 하는 두 번째 사용자 지정 프로세스가 필요합니다.

에셋을 수집하는 또 다른 방법은 로컬 파일 시스템에서 에셋을 가져오는 것입니다. 그러나 외부 드라이브 또는 네트워크 공유를 서버에 마운트하여 가져오기 기반 접근 방식을 수행할 수 없는 경우에는 HTTP를 통해 자산을 게시하는 것이 가장 좋습니다.

#### 로컬 파일 시스템에서 가져오기 {#pulling-from-the-local-filesystem}

[ACS AEM 도구 CSV 자산 가져오기](https://adobe-consulting-services.github.io/acs-aem-tools/features/csv-asset-importer/index.html)는 자산 가져오기를 위해 파일 시스템의 자산과 CSV 파일의 자산 메타데이터를 가져옵니다. Experience Manager Asset Manager API를 사용하여 에셋을 시스템으로 가져오고 구성된 메타데이터 속성을 적용합니다. 에셋은 네트워크 파일 마운트 또는 외부 드라이브를 통해 서버에 마운트되는 것이 가장 좋습니다.

네트워크를 통해 에셋을 전송할 필요가 없으므로 전체 성능이 크게 향상되며 일반적으로 이 방법은 에셋을 저장소에 로드하는 가장 효율적인 방법으로 간주됩니다. 또한 이 도구는 메타데이터 수집을 지원하므로 별도의 도구를 통해 메타데이터를 적용하는 두 번째 단계를 만들지 않고 모든 에셋과 메타데이터를 한 단계로 가져올 수 있습니다.

### 렌디션 처리 {#processing-renditions}

시스템에 에셋을 로드한 후 [!UICONTROL DAM 에셋 업데이트] 워크플로우를 통해 에셋을 처리하여 메타데이터를 추출하고 렌디션을 생성해야 합니다. 이 단계를 수행하기 전에 필요에 맞게 [!UICONTROL DAM 자산 업데이트] 워크플로우를 복제하고 수정해야 합니다. 기본 워크플로에는 Dynamic Media PTIFF 생성 또는 [!DNL InDesign Server] 통합과 같이 사용자에게 필요하지 않은 많은 단계가 포함되어 있습니다.

필요에 따라 워크플로우를 구성한 후에는 두 가지 실행 옵션이 있습니다.

1. 가장 간단한 방법은 [ACS Commons의 벌크 워크플로 관리자](https://adobe-consulting-services.github.io/acs-aem-commons/features/bulk-workflow-manager.html)입니다. 이 도구를 사용하면 쿼리를 실행하고 워크플로우를 통해 쿼리 결과를 처리할 수 있습니다. 배치 크기를 설정하는 옵션도 있습니다.
1. You can use the [ACS Commons Fast Action Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/fast-action-manager.html) in concert with [Synthetic Workflows](https://adobe-consulting-services.github.io/acs-aem-commons/features/synthetic-workflow.html). 이 방법을 사용하면 서버 리소스 사용을 최적화하는 동시에 [!DNL Experience Manager] 워크플로 엔진의 오버헤드를 제거할 수 있습니다. Additionally, the Fast Action Manager further boosts performance by dynamically monitoring server resources and throttling the load placed on the system. Example scripts have been provided on the ACS Commons feature page.

### 에셋 활성화 {#activating-assets}

게시 계층이 있는 배포의 경우 게시 팜에 자산을 활성화해야 합니다. Adobe에서는 둘 이상의 게시 인스턴스를 실행하는 것이 좋지만 모든 자산을 단일 게시 인스턴스로 복제한 다음 해당 인스턴스를 복제하는 것이 가장 효율적입니다. 많은 수의 에셋을 활성화할 때 트리 활성화를 트리거한 후 개입해야 할 수 있습니다. 이유는 다음과 같습니다. 활성화를 실행하면 항목이 Sling 작업/이벤트 큐에 추가됩니다. 이 큐의 크기가 약 40,000개의 항목을 초과하기 시작하면 처리 속도가 크게 느려집니다. 이 큐의 크기가 100,000개 항목을 초과하면 시스템 안정성이 저하되기 시작합니다.

이 문제를 해결하려면 [빠른 작업 관리자](https://adobe-consulting-services.github.io/acs-aem-commons/features/fast-action-manager.html)를 사용하여 자산 복제를 관리할 수 있습니다. 이 기능은 Sling 대기열을 사용하지 않고 작동하여 오버헤드를 줄이는 동시에 워크로드를 조정하여 서버가 오버로드되지 않도록 합니다. FAM을 사용하여 복제를 관리하는 예는 기능의 설명서 페이지에 나와 있습니다.

Other options for getting assets to the publish farm include using [vlt-rcp](https://jackrabbit.apache.org/filevault/rcp.html) or [oak-run](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run), which are provided as tools as part of Jackrabbit. 또 다른 옵션은 vlt보다 성능이 빠르다고 주장하는 [!DNL Experience Manager]Grabbit[이라는 &#x200B;](https://github.com/TWCable/grabbit) 인프라에 대해 오픈 소스 도구를 사용하는 것입니다.

이러한 접근 방식의 경우, 작성자 인스턴스의 자산이 활성화된 것으로 표시되지 않는다는 점에 주의해야 합니다. 이러한 에셋에 올바른 활성화 상태로 플래그를 지정하려면 에셋을 활성화됨으로 표시하는 스크립트도 실행해야 합니다.

>[!NOTE]
>
>Adobe은 Grabbit을 유지 또는 지원하지 않습니다.

### 복제 게시 {#cloning-publish}

에셋이 활성화되면 게시 인스턴스를 복제하여 배포에 필요한 만큼 복사본을 만들 수 있습니다. 서버 복제는 매우 간단하지만 몇 가지 중요한 단계를 기억해야 합니다. 게시 복제:

1. 소스 인스턴스 및 데이터 저장소를 백업합니다.
1. 인스턴스 및 데이터 저장소의 백업을 대상 위치로 복원합니다. 다음 단계는 모두 이 새 인스턴스를 참조합니다.
1. `crx-quickstart/launchpad/felix`에 대해 `sling.id` 아래의 파일 시스템 검색을 수행합니다. Delete this file.
1. 데이터 저장소의 루트 경로에서 `repository-XXX`개 파일을 찾아 삭제합니다.
1. 새 환경에서 데이터 저장소의 위치를 가리키도록 `crx-quickstart/install/org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config` 및 `crx-quickstart/launchpad/config/org/apache/jackrabbit/oak/plugins/blob/datastore/FileDataStore.config`을(를) 편집합니다.
1. 환경을 시작합니다.
1. 작성자의 복제 에이전트 구성을 업데이트하여 올바른 게시 인스턴스 또는 새 인스턴스의 Dispatcher 플러시 에이전트를 가리키도록 하여 새 환경에 대한 올바른 Dispatcher를 지정합니다.

### 워크플로우 활성화 {#enabling-workflows}

마이그레이션을 완료하면 [!UICONTROL DAM 자산 업데이트] 워크플로우에 대한 런처를 다시 사용하도록 설정하여 지속적인 시스템 사용을 위한 렌디션 생성 및 메타데이터 추출을 지원해야 합니다.

## [!DNL Experience Manager]개 배포 간 마이그레이션 {#migrating-between-aem-instances}

거의 일반적이지는 않지만 대량의 데이터를 한 [!DNL Experience Manager] 배포에서 다른 배포로 마이그레이션해야 하는 경우가 있습니다. 예를 들어 [!DNL Experience Manager] 업그레이드를 수행하거나 하드웨어를 업그레이드하거나 AMS 마이그레이션과 같은 새 데이터 센터로 마이그레이션하는 경우가 있습니다.

이 경우 에셋은 이미 메타데이터로 채워지고 변환은 이미 생성됩니다. 한 인스턴스에서 다른 인스턴스로 자산을 이동하는 데 집중할 수 있습니다. [!DNL Experience Manager] 배포 간에 마이그레이션할 때 다음 단계를 수행합니다.

1. 워크플로 비활성화: 에셋과 함께 렌디션을 마이그레이션하고 있으므로 [!UICONTROL DAM 에셋 업데이트] 워크플로에 대한 워크플로 시작 관리자를 비활성화해야 합니다.

1. 태그 마이그레이션: 원본 [!DNL Experience Manager] 배포에 이미 태그가 로드되었으므로 콘텐츠 패키지에 태그를 빌드하고 대상 인스턴스에 패키지를 설치할 수 있습니다.

1. 자산 마이그레이션: 자산을 한 [!DNL Experience Manager] 배포에서 다른 배포로 이동하는 데 권장되는 두 가지 도구가 있습니다.

   * **자격 증명 모음 원격 복사본** 또는 vlt rcp를 사용하면 네트워크에서 vlt를 사용할 수 있습니다. 소스 및 대상 디렉토리를 지정할 수 있으며 vlt는 한 인스턴스에서 모든 저장소 데이터를 다운로드하고 다른 인스턴스로 로드합니다. Vlt rcp는 [https://jackrabbit.apache.org/filevault/rcp.html](https://jackrabbit.apache.org/filevault/rcp.html)에 설명되어 있습니다.
   * **Grabbit**&#x200B;은(는) Time Warner Cable에서 [!DNL Experience Manager] 구현을 위해 개발한 오픈 소스 콘텐츠 동기화 도구입니다. 지속적인 데이터 스트림을 사용하므로 vlt rcp에 비해 지연 시간이 짧고 vlt rcp보다 2~10배 빠른 속도 개선을 주장합니다. Grabbit은 또한 델타 컨텐츠 동기화만 지원하므로 초기 마이그레이션 과정이 완료된 후 변경 사항을 동기화할 수 있습니다.

1. 에셋 활성화: [(으)로의 초기 마이그레이션에 대해 문서화된 &#x200B;](#activating-assets)에셋 활성화[!DNL Experience Manager]에 대한 지침을 따르십시오.

1. 복제 게시: 새로운 마이그레이션과 마찬가지로 단일 게시 인스턴스를 로드하고 복제하는 것이 두 노드에서 콘텐츠를 활성화하는 것보다 효율적입니다. [게시 복제](#cloning-publish)를 참조하십시오.

1. 워크플로우 사용: 마이그레이션을 완료한 후 [!UICONTROL DAM 자산 업데이트] 워크플로우에 대한 런처를 다시 사용하도록 설정하여 지속적인 시스템 사용을 위한 렌디션 생성 및 메타데이터 추출을 지원합니다.
