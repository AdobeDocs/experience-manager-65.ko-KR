---
title: 일괄 에셋 마이그레이션
description: 자산을 [!DNL Adobe Experience Manager]으로 가져오고, 메타데이터를 적용하고, 변환을 생성하고, 인스턴스를 게시하도록 활성화하는 방법에 대해 설명합니다.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5069c2cd26e84866d72a61d36de085dadd556cdd
workflow-type: tm+mt
source-wordcount: '1798'
ht-degree: 0%

---


# 자산을 벌크 {#assets-migration-guide}(으)로 마이그레이션하는 방법

자산을 [!DNL Adobe Experience Manager]으로 마이그레이션할 때 고려해야 할 몇 가지 단계가 있습니다. 현재 집에서 에셋과 메타데이터를 추출하는 방법은 구현 간에 다양하므로 이 문서의 범위를 벗어납니다. 그러나 이 문서에서는 이러한 에셋을 [!DNL Experience Manager]으로 가져오고, 메타데이터를 적용하고, 변환을 생성하며, 인스턴스를 게시하도록 활성화하는 방법에 대해 설명합니다.

## 전제 조건 {#prerequisites}

이 방법론에 있는 단계를 실제로 수행하기 전에 [자산 성능 조정 팁](performance-tuning-guidelines.md)에 대한 지침을 검토 및 구현하십시오. 최대 동시 작업 구성과 같은 많은 단계는 서버의 안정성과 로드 중인 성능을 크게 향상시킵니다. 파일 데이터 저장소 구성과 같은 다른 단계는 시스템이 에셋으로 로드된 후 수행하는 것이 훨씬 더 어렵습니다.

>[!NOTE]
>
>다음 자산 마이그레이션 도구는 [!DNL Experience Manager]의 일부가 아니며 Adobe에서 지원되지 않습니다.
>
>* ACS AEM Tools Tag Maker
>* ACS AEM 도구 CSV 자산 가져오기
>* ACS 커머스 벌크 워크플로우 관리자
>* ACS 커머스 빠른 조치 관리자
>* 합성 워크플로우

>
>
이 소프트웨어는 오픈 소스이며 [Apache v2 License](https://adobe-consulting-services.github.io/pages/license.html)에 의해 보호를 받습니다. 질문하거나 문제를 보고하려면 ACS AEM 도구](https://github.com/Adobe-Consulting-Services/acs-aem-commons/issues) 및 [ACS AEM Commons](https://github.com/Adobe-Consulting-Services/acs-aem-tools/issues)에 대한 해당 [GitHub 문제를 방문하십시오.

## [!DNL Experience Manager] (으)로 마이그레이션{#migrating-to-aem}

자산을 [!DNL Experience Manager]으로 마이그레이션하려면 여러 단계가 필요하며 단계적 프로세스로 확인해야 합니다. 마이그레이션 단계는 다음과 같습니다.

1. 워크플로우 비활성화
1. 태그를 로드합니다.
1. 에셋을 인제스트합니다.
1. 변환을 처리합니다.
1. 자산 활성화
1. 워크플로우 활성화

![chlimage_1-223](assets/chlimage_1-223.png)

### 워크플로 사용 안 함 {#disabling-workflows}

마이그레이션을 시작하기 전에 [!UICONTROL DAM 자산 업데이트] 워크플로우에 대해 방사포를 비활성화합니다. 모든 자산을 시스템에 인제스트한 다음 워크플로우를 일괄적으로 실행하는 것이 가장 좋습니다. 마이그레이션이 진행되는 동안 이미 라이브된 경우 이러한 활동이 비시간에 실행되도록 예약할 수 있습니다.

### {#loading-tags} 태그 로드

이미지에 적용할 태그 분류가 이미 있을 수 있습니다. CSV 자산 가져오기 도구 및 메타데이터 프로필에 대한 [!DNL Experience Manager] 지원과 같은 도구를 사용하여 자산에 태그를 적용하는 프로세스를 자동화할 수 있지만, 태그를 시스템에 로드해야 합니다. [ACS AEM Tools Tag Maker](https://adobe-consulting-services.github.io/acs-aem-tools/features/tag-maker/index.html) 기능을 사용하면 시스템에 로드된 Microsoft Excel 스프레드시트를 사용하여 태그를 채울 수 있습니다.

### 자산 {#ingesting-assets} 인제스트

에셋을 시스템에 인제스트할 때 성능과 안정성을 중요하게 생각합니다. 많은 양의 데이터를 시스템에 로드하고 있으므로 시스템이 필요한 시간을 최소화하며 시스템 과부하 발생을 방지할 수 있을 뿐만 아니라 시스템이 제대로 작동하는지 확인해야 합니다. 특히 이미 운영 중인 시스템에서 시스템 충돌을 야기할 수 있습니다.

시스템에 자산을 로드하는 방법은 두 가지가 있습니다.HTTP를 사용한 푸시 기반 접근 방식 또는 JCR API를 사용한 풀 기반 접근 방식

#### HTTP {#pushing-through-http}를 통해 전송

Adobe Managed Services 팀은 글루튼이라는 도구를 사용하여 고객 환경에 데이터를 로드합니다. Logton은 하나의 디렉토리에서 [!DNL Experience Manager] 배포의 다른 디렉토리로 모든 자산을 로드하는 작은 Java 애플리케이션입니다. Logton 대신 Perl 스크립트와 같은 도구를 사용하여 에셋을 저장소에 게시할 수도 있습니다.

https를 통해 푸싱하는 접근 방식을 사용하는 두 가지 주요 단면이 있습니다.

1. 자산은 HTTP를 통해 서버로 전송되어야 합니다. 따라서 오버헤드가 너무 심하며 시간이 많이 소요되므로 마이그레이션을 수행하는 데 걸리는 시간이 길어집니다.
1. 자산에 적용해야 하는 태그와 사용자 지정 메타데이터가 있는 경우 이 방법을 사용하려면 자산을 가져온 후 이 메타데이터를 자산에 적용하려면 실행해야 하는 두 번째 사용자 지정 프로세스가 필요합니다.

에셋을 인제스트하는 또 다른 방법은 로컬 파일 시스템에서 에셋을 가져오는 것입니다. 그러나 가져오기 기반 접근 방식을 수행하기 위해 서버에 마운트된 외부 드라이브 또는 네트워크 공유를 가져올 수 없는 경우 HTTP를 통해 에셋을 게시하는 것이 가장 좋습니다.

#### 로컬 파일 시스템 {#pulling-from-the-local-filesystem}에서 가져오기

[ACS AEM Tools CSV Asset Importer](https://adobe-consulting-services.github.io/acs-aem-tools/features/csv-asset-importer/index.html)는 자산을 가져오기 위해 파일 시스템 및 자산 메타데이터에서 자산을 가져옵니다. Experience Manager 자산 관리자 API는 자산을 시스템으로 가져오고 구성된 메타데이터 속성을 적용하는 데 사용됩니다. 에셋은 네트워크 파일 마운트 또는 외부 드라이브를 통해 서버에 마운트되는 것이 좋습니다.

자산을 네트워크를 통해 전송할 필요가 없기 때문에 전반적인 성능이 크게 향상되고 일반적으로 이 방법이 저장소에 자산을 로드하는 가장 효율적인 방법으로 간주됩니다. 또한 이 툴은 메타데이터 질문을 지원하므로 모든 에셋과 메타데이터를 한 번에 가져올 수 있습니다. 또한 별도의 툴을 통해 메타데이터를 적용하는 두 번째 단계를 만드는 대신

### 변환 처리 {#processing-renditions}

자산을 시스템에 로드한 후, 메타데이터를 추출하고 변환을 생성하려면 [!UICONTROL DAM 자산 업데이트] 워크플로우를 통해 자산을 처리해야 합니다. 이 단계를 수행하기 전에 요구 사항에 맞게 [!UICONTROL DAM 자산 업데이트] 워크플로우를 복제하고 수정해야 합니다. 즉시 사용 가능한 워크플로우에는 Scene7 PTIFF 생성 또는 [!DNL InDesign Server] 통합 등 사용자에게 필요하지 않은 여러 단계가 포함되어 있습니다.

필요에 따라 워크플로우를 구성한 후에는 두 가지 옵션을 사용하여 워크플로우를 실행합니다.

1. 가장 간단한 방법은 [ACS 공유자의 벌크 워크플로우 관리자](https://adobe-consulting-services.github.io/acs-aem-commons/features/bulk-workflow-manager.html)입니다. 이 도구를 사용하여 쿼리를 실행하고 워크플로우를 통해 쿼리 결과를 처리할 수 있습니다. 일괄 처리 크기를 설정하는 옵션도 있습니다.
1. [Synthetic Workflows](https://adobe-consulting-services.github.io/acs-aem-commons/features/synthetic-workflow.html)와 함께 [ACS Commons Fast Action Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/fast-action-manager.html)를 사용할 수 있습니다. 이러한 접근 방식은 서버 리소스 사용을 최적화하는 동시에 [!DNL Experience Manager] 워크플로우 엔진의 오버헤드를 제거할 수 있습니다. 또한 Fast Action Manager는 서버 리소스를 동적으로 모니터링하고 시스템에 배치된 로드를 조절하여 성능을 더욱 향상시킵니다. 예제 스크립트는 ACS Commons 기능 페이지에 제공되었습니다.

### 자산 {#activating-assets} 활성화

게시 계층이 있는 배포의 경우 게시 팜에서 자산을 활성화해야 합니다. Adobe은 단일 게시 인스턴스 이상을 실행하는 것이 좋지만, 모든 자산을 단일 게시 인스턴스에 복제한 다음 해당 인스턴스를 복제하는 것이 가장 효율적입니다. 대량의 자산을 활성화할 때 트리 활성화를 트리거한 후 개입해야 할 수 있습니다. 그 이유는 다음과 같습니다.활성화가 시작될 때 항목이 Sling 작업/이벤트 대기열에 추가됩니다. 이 큐의 크기가 약 40,000개 항목을 초과할 경우 처리 속도가 크게 느려집니다. 이 큐의 크기가 100,000개 항목을 초과하면 시스템 안정성이 손상되기 시작합니다.

이 문제를 해결하려면 [빠른 작업 관리자](https://adobe-consulting-services.github.io/acs-aem-commons/features/fast-action-manager.html)를 사용하여 자산 복제를 관리할 수 있습니다. 이는 Sling 대기열을 사용하지 않고 오버헤드를 낮추고 작업 로드를 조절하여 서버의 오버로드가 되지 않도록 합니다. FAM을 사용하여 복제를 관리하는 예는 기능의 설명서 페이지에 나와 있습니다.

게시 팜에 에셋을 가져오기 위한 다른 옵션에는 Jackrabbit의 일부로 제공되는 [vlt-rcp](https://jackrabbit.apache.org/filevault/rcp.html) 또는 [oak-run](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run)을 사용하는 옵션이 있습니다. 또 다른 옵션은 vlt보다 더 빠른 성능을 발휘한다고 주장하는 [!DNL Experience Manager]Grabbit[라는 인프라에 대해 오픈 소스 도구를 사용하는 것입니다.](https://github.com/TWCable/grabbit)

이러한 접근 방식에서 주의해야 할 점은 작성자 인스턴스의 에셋이 활성화된 것으로 표시되지 않는다는 것입니다. 이러한 자산에 대한 플래그를 올바른 활성화 상태로 처리하려면 자산을 활성화한 것으로 표시하는 스크립트도 실행해야 합니다.

>[!NOTE]
>
>Adobe은 Grabbit를 유지 관리하거나 지원하지 않습니다.

### 복제 게시 {#cloning-publish}

자산이 활성화되면 게시 인스턴스를 복제하여 배포에 필요한 만큼의 사본을 만들 수 있습니다. 서버 복제는 매우 간단하지만 기억해야 할 몇 가지 중요한 단계가 있습니다. 게시를 복제하려면

1. 소스 인스턴스와 데이터 저장소를 백업합니다.
1. 인스턴스 및 데이터 저장소의 백업을 대상 위치로 복원합니다. 다음 단계는 모두 이 새 인스턴스를 참조합니다.
1. `sling.id`에 대해 `crx-quickstart/launchpad/felix` 아래에서 파일 시스템 검색을 수행합니다. 이 파일을 삭제합니다.
1. 데이터 저장소의 루트 경로 아래에서 `repository-XXX` 파일을 찾아 삭제합니다.
1. 새 환경의 데이터 저장소 위치를 가리키도록 `crx-quickstart/install/org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config` 및 `crx-quickstart/launchpad/config/org/apache/jackrabbit/oak/plugins/blob/datastore/FileDataStore.config`을 편집합니다.
1. 환경을 시작합니다.
1. 새 인스턴스의 올바른 게시 인스턴스 또는 발송자 플러쉬 에이전트를 가리키도록 작성자의 복제 에이전트 구성을 업데이트하여 새 환경에 대한 올바른 디스패처를 가리킵니다.

### 워크플로 사용 {#enabling-workflows}

마이그레이션이 완료되면, 지속적인 시스템 사용을 위해 변환 생성 및 메타데이터 추출을 지원하기 위해 [!UICONTROL DAM Update Asset] 워크플로우의 방사선을 다시 사용하도록 설정해야 합니다.

## [!DNL Experience Manager] 배포 간에 마이그레이션 {#migrating-between-aem-instances}

거의 일반적이지 않지만, 대량의 데이터를 한 [!DNL Experience Manager] 배포에서 다른 데이터로 마이그레이션해야 하는 경우가 있습니다.예를 들어 [!DNL Experience Manager] 업그레이드를 수행하거나, 하드웨어를 업그레이드하거나, AMS 마이그레이션과 같은 새로운 데이터 센터로 마이그레이션합니다.

이 경우 자산이 이미 메타데이터로 채워지고 변환이 이미 생성됩니다. 한 인스턴스에서 다른 인스턴스로 자산을 이동하는 것에 간단하게 집중할 수 있습니다. [!DNL Experience Manager] 배포 간에 마이그레이션할 때 다음 단계를 수행합니다.

1. 워크플로우 비활성화:Adobe 자산과 함께 변환을 마이그레이션하고 있으므로 [!UICONTROL DAM 자산 업데이트] 워크플로우에 대한 워크플로우 릴리스를 비활성화할 수 있습니다.

1. 태그 마이그레이션:소스 [!DNL Experience Manager] 배포에 이미 태그가 로드되어 있으므로 콘텐츠 패키지에서 태그를 빌드하고 대상 인스턴스에 패키지를 설치할 수 있습니다.

1. 자산 마이그레이션:한 [!DNL Experience Manager] 배포에서 다른 배포로 자산을 이동하는 데 권장되는 두 가지 도구가 있습니다.

   * **Vault Remote** Copy 또는 vlt rcp를 사용하면 네트워크를 통해 vlt를 사용할 수 있습니다. 소스 및 대상 디렉토리를 지정하고 vlt가 한 인스턴스에서 모든 저장소 데이터를 다운로드하고 다른 인스턴스로 로드할 수 있습니다. Vlt rcp는 [https://jackrabbit.apache.org/filevault/rcp.html](https://jackrabbit.apache.org/filevault/rcp.html)에 기록되어 있습니다.
   * **Grabbbitis** 는 Time Warner Cable에서 구현하기 위해 개발한 오픈 소스 컨텐츠 동기화  [!DNL Experience Manager] 툴입니다. vlt rcp에 비해 연속 데이터 스트림을 사용하기 때문에 지연 시간이 더 적고 vlt rcp에 비해 2-10배 빠른 속도 개선 효과를 제공합니다. 또한 Grabbit는 델타 컨텐츠 동기화만 지원하므로 초기 마이그레이션 전달이 완료된 후 변경 사항을 동기화할 수 있습니다.

1. 자산 활성화:[!DNL Experience Manager]로의 초기 마이그레이션에 대해 문서화된 [자산](#activating-assets)을 활성화하기 위한 지침을 따르십시오.

1. 복제 게시:새 마이그레이션과 마찬가지로 단일 게시 인스턴스를 로드하고 복제하는 것이 두 노드에서 컨텐츠를 활성화하는 것보다 더 효율적입니다. [게시 복제를 참조하십시오.](#cloning-publish)

1. 워크플로우 활성화:마이그레이션을 완료한 후, 지속적인 시스템 사용을 위해 변환 생성 및 메타데이터 추출을 지원하기 위해 [!UICONTROL DAM Update Asset] 워크플로우에 대한 방사포를 다시 활성화합니다.
