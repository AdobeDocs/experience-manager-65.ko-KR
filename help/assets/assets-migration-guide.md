---
title: Adobe Experience Manager Assets로 자산 일괄 마이그레이션
description: 자산을 AEM으로 가져오고, 메타데이터를 적용하고, 변환을 생성하며, 인스턴스를 게시하도록 활성화하는 방법에 대해 설명합니다.
contentOwner: AG
translation-type: tm+mt
source-git-commit: f24142064b15606a5706fe78bf56866f7f9a40ae

---


# 자산을 일괄 마이그레이션하는 방법 {#assets-migration-guide}

자산을 AEM으로 마이그레이션할 때 고려해야 할 몇 가지 단계가 있습니다. 현재 집에서 자산 및 메타데이터를 추출하는 방법은 구현 간에 다양하므로 이 문서의 범위를 벗어납니다. 그러나 이 문서에서는 이러한 자산을 AEM으로 가져오고, 메타데이터를 적용하고, 변환을 생성하며, 인스턴스를 게시하도록 활성화하는 방법에 대해 설명합니다.

## 전제 조건 {#prerequisites}

이 방법론에 있는 단계를 실제로 수행하기 전에 자산 성능 조정 팁에 [대한 지침을](performance-tuning-guidelines.md)검토하고 구현하십시오. 최대 동시 작업 구성과 같은 많은 단계는 로드 중인 서버의 안정성과 성능을 크게 향상시킵니다. 파일 데이터 저장소 구성과 같은 다른 단계는 시스템이 에셋으로 로드된 후 수행하는 것이 훨씬 더 어렵습니다.

>[!NOTE]
>
>다음 에셋 마이그레이션 도구는 AEM의 일부가 아니며 Adobe에서 지원되지 않습니다.
>
>* ACS AEM Tools Tag Maker
>* ACS AEM 도구 CSV 자산 가져오기
>* ACS 커머스 벌크 워크플로우 관리자
>* ACS Commons Fast Action Manager
>* 합성 워크플로우
>
>
이 소프트웨어는 오픈 소스이며 Apache v2 [라이센스의 적용을 받습니다](https://adobe-consulting-services.github.io/pages/license.html). 질문하거나 문제를 보고하려면 ACS AEM 도구 및 ACS AEM [Commons에 대한 해당 GitHub](https://github.com/Adobe-Consulting-Services/acs-aem-commons/issues) 문제를 [참조하십시오](https://github.com/Adobe-Consulting-Services/acs-aem-tools/issues).

## AEM으로 마이그레이션 {#migrating-to-aem}

자산을 AEM으로 마이그레이션하려면 몇 가지 단계가 필요하며 단계적인 프로세스로 봐야 합니다. 마이그레이션 단계는 다음과 같습니다.

1. 워크플로우 비활성화
1. 태그를 로드합니다.
1. 에셋 인제스트
1. 변환을 처리합니다.
1. 자산 활성화
1. 워크플로우 활성화

![chlimage_1-223](assets/chlimage_1-223.png)

### 워크플로우 비활성화 {#disabling-workflows}

마이그레이션을 시작하기 전에 DAM 자산 업데이트 [!UICONTROL 워크플로우에 대해 런처를 비활성화하십시오] . 모든 자산을 시스템에 인제스트한 다음 워크플로우를 일괄로 실행하는 것이 가장 좋습니다. 마이그레이션이 진행되는 동안 이미 라이브한 경우 이러한 활동이 비시간대로 실행되도록 예약할 수 있습니다.

### 태그 로드 {#loading-tags}

이미지에 적용할 태그 분류법이 이미 있을 수 있습니다. CSV Asset Importer 및 Experience Manager의 메타데이터 프로필 지원과 같은 도구를 사용하여 자산에 태그를 적용하는 프로세스를 자동화할 수 있지만, 태그를 시스템에 로드해야 합니다. ACS [AEM Tools Tag](https://adobe-consulting-services.github.io/acs-aem-tools/features/tag-maker/index.html) Maker 기능을 사용하면 시스템에 로드된 Microsoft Excel 스프레드시트를 사용하여 태그를 채울 수 있습니다.

### 에셋 인제스트 {#ingesting-assets}

에셋을 시스템에 인제스트할 때 성능과 안정성은 중요한 문제입니다. 많은 양의 데이터를 시스템에 로드하고 있으므로 시스템이 필요한 시간을 최소화하고 시스템 과부하를 방지할 수 있을 뿐만 아니라 시스템이 제대로 작동하는지 확인해야 합니다. 이는 특히 이미 운영 중인 시스템에서 시스템 충돌을 야기할 수 있습니다.

시스템에 자산을 로드하는 방법은 두 가지가 있습니다.http를 사용하는 푸시 기반 접근 방식 또는 JCR API를 사용하는 풀 기반 접근 방식

#### HTTP를 통해 보내기 {#pushing-through-http}

Adobe의 Managed Services 팀은 Logton이라는 도구를 사용하여 고객 환경에 데이터를 로드합니다. Logton은 한 디렉토리에서 AEM 인스턴스의 다른 디렉토리로 모든 자산을 로드하는 작은 Java 애플리케이션입니다. Logton 대신 Perl 스크립트와 같은 도구를 사용하여 에셋을 저장소에 게시할 수도 있습니다.

https를 통해 푸싱하는 접근 방식을 사용하는 데는 두 가지 주요 단점이 있습니다.

1. HTTP를 통해 서버에 자산을 전송해야 합니다. 따라서 오버헤드가 너무 많이 필요하고 시간이 많이 소요되므로 마이그레이션 수행에 소요되는 시간이 길어집니다.
1. 자산에 적용해야 하는 태그와 사용자 지정 메타데이터가 있는 경우, 이 방법을 사용하려면 두 번째 사용자 지정 프로세스를 실행해야 하며, 이 메타데이터를 가져온 후 자산에 적용하려면 실행해야 합니다.

에셋을 인제스트하는 또 다른 방법은 로컬 파일 시스템에서 에셋을 가져오는 것입니다. 그러나 가져오기 기반 접근 방식을 수행하기 위해 외부 드라이브 또는 네트워크 공유를 서버에 마운트할 수 없는 경우 HTTP를 통해 에셋을 게시하는 것이 가장 좋습니다.

#### 로컬 파일 시스템에서 가져오기 {#pulling-from-the-local-filesystem}

ACS [AEM Tools CSV Asset](https://adobe-consulting-services.github.io/acs-aem-tools/features/csv-asset-importer/index.html) Importer는 파일 시스템에서 자산을 가져오고 CSV 파일에서 자산 메타데이터를 가져옵니다. AEM Asset Manager API는 자산을 시스템으로 가져오고 구성된 메타데이터 속성을 적용하는 데 사용됩니다. 에셋은 네트워크 파일 마운트 또는 외부 드라이브를 통해 서버에 마운트하는 것이 좋습니다.

자산을 네트워크를 통해 전송할 필요가 없기 때문에 전반적인 성능이 크게 향상되고 일반적으로 이 방법은 에셋을 저장소로 로드하는 가장 효율적인 방법입니다. 또한 이 툴은 메타데이터 질문을 지원하므로 모든 자산과 메타데이터를 한 번에 가져올 수 있습니다. 두 번째 단계를 만들어 별도의 툴을 통해 메타데이터를 적용할 수도 있습니다.

### 변환 처리 {#processing-renditions}

자산을 시스템에 로드한 후 DAM 자산 업데이트 [!UICONTROL 워크플로우를 통해] 메타데이터를 추출하고 변환을 생성해야 합니다. 이 단계를 수행하기 전에 필요에 맞게 DAM 자산 [!UICONTROL 업데이트] 워크플로우를 복제하고 수정해야 합니다. 기본 작업 과정에는 Scene7 PTIFF 생성 또는 InDesign 서버 통합과 같이 사용자에게 필요하지 않은 여러 단계가 포함되어 있습니다.

필요에 따라 워크플로우를 구성한 후에는 두 가지 옵션을 사용하여 워크플로우를 실행합니다.

1. 가장 간단한 방법은 ACS [Commons의 벌크 워크플로우 관리자입니다](https://adobe-consulting-services.github.io/acs-aem-commons/features/bulk-workflow-manager.html). 이 도구를 사용하여 쿼리를 실행하고 워크플로우를 통해 쿼리 결과를 처리할 수 있습니다. 일괄 처리 크기를 설정하는 옵션도 있습니다.
1. ACS Commons Fast [Action Manager를](https://adobe-consulting-services.github.io/acs-aem-commons/features/fast-action-manager.html) Synthetic Workflows와 함께 사용할 [수 있습니다](https://adobe-consulting-services.github.io/acs-aem-commons/features/synthetic-workflow.html). 이 방법은 보다 많이 사용되지만 서버 리소스 사용을 최적화하는 동안 AEM 워크플로우 엔진의 오버헤드를 제거할 수 있습니다. 또한 Fast Action Manager는 서버 리소스를 동적으로 모니터링하고 시스템에 배치된 로드를 조절하여 성능을 더욱 향상시켜 줍니다. 예제 스크립트는 ACS Commons 기능 페이지에 제공되었습니다.

### 자산 활성화 {#activating-assets}

게시 계층이 있는 배포의 경우 게시 팜에서 자산을 활성화해야 합니다. Adobe에서는 단일 게시 인스턴스 이상을 실행하는 것이 좋지만, 모든 자산을 단일 게시 인스턴스에 복제한 다음 해당 인스턴스를 복제하는 것이 가장 효율적입니다. 대량의 자산을 활성화할 때 트리 활성화를 트리거한 후 개입해야 할 수 있습니다. 그 이유는 다음과 같습니다.활성화를 시작하면 항목이 Sling 작업/이벤트 대기열에 추가됩니다. 이 큐의 크기가 약 40,000개 항목을 초과할 때 처리 속도가 크게 느려집니다. 이 큐의 크기가 100,000개 항목을 초과하면 시스템 안정성이 떨어지기 시작합니다.

이 문제를 해결하려면 빠른 작업 관리자를 사용하여 [자산](https://adobe-consulting-services.github.io/acs-aem-commons/features/fast-action-manager.html) 복제를 관리할 수 있습니다. 이는 Sling 대기열을 사용하지 않고 오버헤드를 줄이고 작업 로드를 조절하여 서버가 오버로드되지 않도록 합니다. FAM을 사용하여 복제를 관리하는 예는 기능의 설명서 페이지에 나와 있습니다.

게시 팜에 에셋을 가져오기 위한 다른 옵션으로는 Jackrabbit의 일부로 제공되는 [vlt-rcp](https://jackrabbit.apache.org/filevault/rcp.html) 또는 [oak-run](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run)사용등이 있습니다. 또 다른 옵션은 Grabbit라는 AEM 인프라에 대해 [오픈 소스](https://github.com/TWCable/grabbit)도구를 사용하는 것입니다. 이 도구는 VLT보다 성능이 빠릅니다.

이러한 접근 방식에서 주의해야 할 점은 작성자 인스턴스의 에셋이 활성화된 것으로 표시되지 않는다는 것입니다. 이러한 자산의 플래그를 올바른 활성화 상태로 처리하려면 스크립트를 실행하여 자산을 활성화됨으로 표시해야 합니다.

>[!NOTE]
>
>Adobe는 Grabbit를 유지 관리하거나 지원하지 않습니다.

### 복제 게시 {#cloning-publish}

자산이 활성화되면 게시 인스턴스를 복제하여 배포에 필요한 만큼의 사본을 만들 수 있습니다. 서버 복제는 매우 간단하지만 기억해야 할 몇 가지 중요한 단계가 있습니다. 게시를 복제하려면

1. 소스 인스턴스와 데이터 저장소를 백업합니다.
1. 인스턴스 및 데이터 저장소의 백업을 대상 위치로 복원합니다. 다음 단계는 모두 이 새 인스턴스를 참조합니다.
1. 에서 파일 시스템 검색을 `crx-quickstart/launchpad/felix` 수행합니다 `sling.id`. 이 파일을 삭제합니다.
1. 데이터 저장소의 루트 경로 아래에서 모든 `repository-XXX` 파일을 찾아 삭제합니다.
1. 새 환경에서 데이터 저장소의 위치를 `crx-quickstart/install/org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config` 편집하고 `crx-quickstart/launchpad/config/org/apache/jackrabbit/oak/plugins/blob/datastore/FileDataStore.config` 지정합니다.
1. 환경을 시작합니다.
1. 작성자의 복제 에이전트 구성을 업데이트하여 새 인스턴스의 올바른 게시 인스턴스 또는 발송자 플러시 에이전트를 가리키도록 합니다.

### 워크플로우 활성화 {#enabling-workflows}

마이그레이션이 완료되면 DAM Update Asset [!UICONTROL 워크플로우의] 방사선을 다시 활성화하여 지속적인 시스템 사용을 위해 변환 생성 및 메타데이터 추출을 지원해야 합니다.

## AEM 배포 간 마이그레이션 {#migrating-between-aem-instances}

일반적이지는 않지만 경우에 따라 대량의 데이터를 한 AEM 인스턴스에서 다른 AEM 인스턴스로 마이그레이션해야 합니다.예를 들어 AEM 업그레이드를 수행할 때 하드웨어를 업그레이드하거나 AMS 마이그레이션과 같은 새 데이터 센터로 마이그레이션합니다.

이 경우 자산은 이미 메타데이터로 채워지고 표현물은 이미 생성됩니다. 한 인스턴스에서 다른 인스턴스로 에셋을 이동하는 데 집중할 수 있습니다. AEM 인스턴스 간에 마이그레이션할 때 다음 단계를 수행합니다.

1. 워크플로우 비활성화:Adobe 자산과 함께 변환을 마이그레이션하기 때문에 DAM 자산 업데이트 [!UICONTROL 워크플로우에 대한 워크플로우 런처를 비활성화하려고] 합니다.

1. 태그 마이그레이션:소스 AEM 인스턴스에 이미 태그가 로드되어 있으므로 콘텐츠 패키지에서 태그를 빌드하고 대상 인스턴스에 패키지를 설치할 수 있습니다.

1. 자산 마이그레이션:한 AEM 인스턴스에서 다른 AEM 인스턴스로 자산을 이동하는 데 권장되는 두 가지 도구가 있습니다.

   * **저장소 원격 복사** 또는 vlt rcp를 사용하면 네트워크를 통해 vlt를 사용할 수 있습니다. 소스 및 대상 디렉토리를 지정하고 Vlt가 한 인스턴스에서 모든 저장소 데이터를 다운로드하고 다른 인스턴스로 로드할 수 있습니다. Vlt rcp는 https://jackrabbit.apache.org/filevault/rcp.html에 [있습니다.](https://jackrabbit.apache.org/filevault/rcp.html)
   * **Grabbit** 는 AEM 구현을 위해 Time Warner Cable에서 개발한 오픈 소스 컨텐츠 동기화 도구입니다. vlt rcp에 비해 연속 데이터 스트림을 사용하기 때문에 지연 시간이 더 적고 vlt rcp에 비해 2-10배 빠른 속도 개선 효과가 있다고 주장합니다. 또한 Grabbit는 델타 컨텐츠 동기화만 지원하므로 초기 마이그레이션 전달이 완료된 후 변경 사항을 동기화할 수 있습니다.

1. 자산 활성화:AEM으로의 초기 마이그레이션에 대해 문서화된 자산 [](#activating-assets) 활성화에 대한 지침을 따르십시오.

1. 복제 게시:새 마이그레이션과 마찬가지로, 단일 게시 인스턴스를 로드하고 복제하는 것이 두 노드에서 컨텐츠를 활성화하는 것보다 더 효율적입니다. 게시 [복제를 참조하십시오.](#cloning-publish)

1. 워크플로우 활성화:마이그레이션을 완료한 후 DAM 자산 업데이트 [!UICONTROL 워크플로우용] 런처를 다시 활성화하여 지속적인 시스템 사용을 위해 변환 생성 및 메타데이터 추출을 지원합니다.
