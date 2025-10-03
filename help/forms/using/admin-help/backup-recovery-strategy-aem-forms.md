---
title: AEM Forms에 대한 백업 및 복구 전략
description: 데이터를 백업하고 AEM Forms 데이터와 동기화 상태를 유지하는 전략을 구현하는 방법을 알아봅니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 01ec6ebc-6d80-4417-9604-c8571aebb57e
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: ht
source-wordcount: '1518'
ht-degree: 100%

---

# AEM Forms에 대한 백업 및 복구 전략{#backup-and-recovery-strategy-for-aem-forms}

AEM Forms 구현 시 다른 데이터베이스에 추가 사용자 정의 데이터를 저장하는 경우 해당 데이터를 백업하고 AEM Forms 데이터와 동기화 상태를 유지하는 전략을 구현하는 것은 사용자의 책임입니다. 또한 애플리케이션은 추가 데이터베이스가 동기화되지 않는 시나리오를 처리할 수 있을 만큼 강력하게 설계되어야 합니다. 일관된 상태를 유지하기 위해 모든 데이터베이스 작업은 트랜잭션 컨텍스트에서 수행하는 것이 좋습니다.

AEM Forms의 사용 방식을 파악한 후 백업해야 할 파일, 백업 빈도, 이용 가능한 백업 시간을 결정합니다.

>[!NOTE]
>
>AEM Forms 구현의 다른 모든 측면과 마찬가지로 백업 및 복구 전략은 프로덕션에서 사용하기 전에 개발 환경 또는 스테이징 환경에서 개발하고 테스트하여 전체 솔루션이 데이터 손실 없이 예상대로 작동하도록 해야 합니다.

AEM(Adobe Experience Manager)은 AEM Forms의 필수적인 부분입니다. 따라서 AEM도 AEM Forms 백업과 동기화하여 백업해야 합니다. 서신 관리 솔루션 및 Forms Manager와 같은 서비스는 AEM Forms의 AEM 부분에 저장된 데이터를 기반으로 하기 때문입니다. 데이터 손실을 방지하려면 GDS 및 AEM(저장소)이 데이터베이스 참조와 상호 관련되도록 AEM Forms 전용 데이터를 백업해야 합니다. 데이터베이스, GDS, AEM 및 콘텐츠 스토리지 루트 디렉터리는 DNS 이름이 원본과 동일한 컴퓨터로 복원해야 합니다.

## 백업 유형 {#types-of-backups}

AEM Forms 백업 전략에는 다음과 같은 두 가지 유형의 백업이 포함됩니다.

**시스템 이미지:** 하드 드라이브나 컴퓨터 전체가 작동을 멈췄을 때 컴퓨터 콘텐츠를 복원하는 데 사용할 수 있는 전체 시스템 백업입니다. 시스템 이미지 백업은 AEM Forms를 프로덕션에 배포하기 전에만 필요합니다. 시스템 이미지 백업 빈도는 회사 내부 정책에 따라 결정됩니다.

**AEM Forms 전용 데이터:** 애플리케이션 데이터는 데이터베이스, 전역 문서 스토리지(GDS), AEM 저장소에 있으며 실시간으로 백업되어야 합니다. GDS는 프로세스 내에서 사용되는 장기 파일을 저장하는 데 사용되는 디렉터리입니다. 이러한 파일에는 PDF, 정책, 양식 템플릿이 포함될 수 있습니다.

>[!NOTE]
>
>콘텐츠 서비스(더 이상 사용되지 않음)가 설치된 경우 콘텐츠 스토리지 루트 디렉터리도 백업하십시오. [콘텐츠 스토리지 루트 디렉터리(콘텐츠 서비스 전용)](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-directory-content-services-only)를 참조하십시오.

데이터베이스는 양식 아티팩트, 서비스 구성, 프로세스 상태, GDS 파일에 대한 데이터베이스 참조를 저장하는 데 사용됩니다. 데이터베이스에서 문서 저장을 활성화한 경우 GDS의 영구 데이터 및 문서도 데이터베이스에 저장됩니다. 다음 방법을 사용하여 데이터베이스를 백업하고 복구할 수 있습니다.

* **스냅샷 백업** 모드는 AEM Forms 시스템이 무기한 또는 지정된 시간(분) 동안 백업 모드에 있으며 그 이후에는 백업 모드가 더 이상 활성화되지 않음을 나타냅니다. 스냅샷 백업 모드를 시작하거나 종료하려면 다음 옵션 중 하나를 사용할 수 있습니다. 복구 시나리오 후에는 스냅샷 백업 모드를 활성화해서는 안 됩니다.

   * 관리 콘솔의 백업 설정 페이지를 사용합니다. 스냅샷 모드를 시작하려면 안전 백업 모드에서 작동 확인란을 선택합니다. 스냅샷 모드를 종료하려면 확인란을 선택 취소합니다.
   * LCBackupMode 스크립트를 사용합니다([데이터베이스, GDS 및 콘텐츠 스토리지 루트 디렉터리 백업](/help/forms/using/admin-help/backing-aem-forms-data.md#back-up-the-database-gds-aem-repository-and-content-storage-root-directories) 참조). 스냅샷 백업 모드를 종료하려면 스크립트 인수에서 `continuousCoverage` 매개변수를 `false`로 설정하거나 `leaveContinuousCoverage` 옵션을 사용합니다.
   * 제공된 백업/복구 API를 사용합니다. <!-- Fix broken link(see AEM forms API Reference section on AEM Forms Help and Tutorials page).-->

* **롤링 백업** 모드는 시스템이 항상 백업 모드에 있으며 이전 세션이 해제되자마자 새로운 백업 모드 세션이 시작됨을 나타냅니다. 롤링 백업 모드에는 시간 초과가 연결되어 있지 않습니다. LCBackupMode 스크립트 또는 API가 호출되어 롤링 백업 모드가 종료되면 새로운 롤링 백업 모드 세션이 시작됩니다. 이 모드는 연속 백업을 지원하면서도 오래되고 불필요한 문서를 GDS 디렉터리에서 정리할 수 있도록 해준다는 점에서 유용합니다. 백업 및 복구 페이지에서는 롤링 백업 모드가 지원되지 않습니다. 복구 시나리오 후에도 롤링 백업 모드가 계속 활성화되어 있습니다. LCBackupMode 스크립트에서 `leaveContinuousCoverage` 옵션을 사용하여 연속 백업 모드(롤링 백업 모드)를 종료할 수 있습니다.

>[!NOTE]
>
>롤링 백업 모드를 종료하는 즉시 새로운 백업 모드 세션이 시작됩니다. 롤링 백업 모드를 완전히 비활성화하려면 스크립트에서 기존 롤링 백업 세션을 덮어쓰는 `leaveContinuousCoverage` 옵션을 사용하십시오. 스냅샷 백업 모드에서는 평소처럼 백업 모드를 종료할 수 있습니다.

데이터 손실을 방지하려면 GDS 및 콘텐츠 스토리지 루트 디렉터리 문서가 데이터베이스 참조와 상호 관련되도록 AEM Forms 전용 데이터를 백업해야 합니다.

>[!NOTE]
>
>GDS가 데이터베이스가 아닌 파일 시스템에 저장되어 있는 경우 GDS 백업 전에 데이터베이스 백업을 수행합니다.

## 백업 및 복구에 대한 특별 고려 사항 {#special-considerations-for-backup-and-recovery}

다음과 같은 변경 사항으로 인해 AEM Forms를 다른 환경으로 복구해야 하는 경우 다음 지침을 따르십시오.

* AEM Forms 서버의 IP 주소, 호스트 이름 또는 포트 변경
* 드라이브 문자 또는 디렉터리 경로 변경
* 다른 데이터베이스 호스트, 포트 또는 이름으로 변경

일반적으로 이러한 복구 시나리오는 애플리케이션 서버, 데이터베이스 서버 또는 Forms 서버를 호스팅하는 서버의 하드웨어 장애로 인해 발생합니다. 이 섹션에 설명된 AEM Forms 전용 구성 외에도 AEM Forms 서버의 호스트 이름이나 IP 주소가 변경되면 로드 밸런서 및 방화벽과 같은 AEM Forms 배포의 다른 부분에 대해서도 필요한 변경 작업을 수행해야 합니다.

### 변경할 수 없는 대상 {#what-cannot-be-changed}

백업에서 AEM Forms를 복구할 때 데이터베이스 서버와 기타 여러 매개변수를 변경할 수 있지만 애플리케이션 서버 유형이나 데이터베이스 유형은 변경할 수 없습니다. 예를 들어 AEM Forms 백업을 복구하는 경우 애플리케이션 서버를 JBoss에서 WebLogic으로 변경하거나 데이터베이스를 Oracle에서 DB2로 변경할 수 없습니다. 또한 복구된 AEM Forms는 글꼴 디렉터리와 같은 동일한 파일 시스템 경로를 사용해야 합니다.

### 복구 후 다시 시작 {#restarting-after-a-recovery}

복구 후 Forms 서버를 다시 시작하기 전에 다음 작업을 수행하십시오.

1. 유지 관리 모드에서 시스템을 시작합니다.
1. 다음 작업을 수행하여 유지 관리 모드에서 Form Manager가 AEM Forms와 동기화되도록 합니다.

   1. https://&lt;*server*>:&lt;*port*>/lc/fm으로 이동하여 관리자/암호 자격 증명을 사용하여 로그인합니다.
   1. 오른쪽 상단 모서리에 있는 사용자 이름(이 경우 슈퍼 관리자)을 클릭합니다.
   1. **관리자 옵션**&#x200B;을 클릭합니다.
   1. **시작**&#x200B;을 클릭하여 저장소에서 자산을 동기화합니다.

1. 클러스터링된 환경에서는 기본 노드(AEM 기준)가 보조 노드보다 먼저 실행되어야 합니다.
1. 시스템의 정상 작동이 검증될 때까지 웹, SOAP, EJB 프로세스 개시자와 같은 내부 또는 외부 소스에서 어떠한 프로세스도 시작되지 않도록 합니다.

기본 AEM Forms 데이터베이스가 이동하거나 변경된 경우 애플리케이션 서버와 관련된 설치 안내서를 검토하여 AEM Forms 데이터 소스 IDP_DS 및 EDC_DS에 대한 데이터베이스 연결 정보를 업데이트하는 방법에 대한 정보를 확인합니다.

>[!NOTE]
> 
> SDK를 다시 시작하려면 &#39;Ctrl + C&#39; 명령을 사용하는 것이 좋습니다. 예를 들어 Java 프로세스를 중지하는 것과 같은 다른 방법을 사용하여 AEM SDK를 다시 시작하면 AEM 개발 환경에서 불일치가 발생할 수 있습니다.

### AEM Forms 호스트 이름 또는 IP 주소 변경 {#changing-the-aem-forms-hostname-or-ip-address}

클러스터에서 UDP 대신 TCP 캐싱을 사용하는 경우 캐시 검색기 구성을 업데이트해야 합니다. 애플리케이션 서버와 관련된 구성 안내서에서 &#39;캐싱 검색기 구성(TCP만 사용하는 캐싱)&#39;을 참조하십시오.

### AEM Forms 노드 파일 시스템 경로 변경 {#changing-the-aem-forms-node-file-system-paths}

독립 실행형 노드의 파일 시스템 경로를 변경하는 경우 환경 설정, 기타 시스템 구성, 사용자 정의 애플리케이션, 배포된 AEM Forms 애플리케이션에서 해당 참조를 업데이트해야 합니다. 반면에 클러스터의 경우 모든 노드가 동일한 파일 시스템 경로 구성을 사용해야 합니다. 전역 문서 스토리지(GDS) 루트 디렉터리를 설정하고 해당 디렉터리가 복구된 데이터베이스와 동기화되는 복구된 GDS 사본을 가리키도록 합니다. GDS 경로를 설정하는 작업은 GDS에 애플리케이션 서버가 다시 시작되더라도 유지되어야 하는 데이터가 포함될 수 있으므로 중요합니다.

클러스터링된 환경에서 저장소의 파일 시스템 경로 구성은 백업 전과 복구 후에 모든 클러스터 노드에서 동일해야 합니다.

파일 시스템 경로를 변경한 후 `[*aem-forms root]*\sdk\misc\Foundation\SetGDSCommandline` 폴더의 `LCSetGDS` 스크립트를 사용하여 GDS 경로를 설정합니다. 자세한 내용은 같은 폴더에 있는 `ReadMe.txt` 파일을 참조하십시오. 기존 GDS 디렉터리 경로를 사용할 수 없는 경우 AEM Forms를 시작하기 전에 `LCSetGDS` 스크립트를 사용하여 GDS에 대한 새 경로를 설정해야 합니다.

>[!NOTE]
>
>이러한 상황에서만 해당 스크립트를 사용하여 GDS 위치를 변경해야 합니다. AEM Forms가 실행되는 동안 GDS 위치를 변경하려면 관리 콘솔을 사용하십시오. ([일반 AEM Forms 설정 구성](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)을 참조하십시오*.)*

GDS 경로를 설정한 후 유지 관리 모드에서 Forms 서버를 시작하고 관리 콘솔을 사용하여 새 노드의 나머지 파일 시스템 경로를 업데이트합니다. 모든 필수 구성이 업데이트되었는지 확인한 후 AEM Forms를 다시 시작하고 테스트합니다.
