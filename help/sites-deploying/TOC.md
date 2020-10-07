---
cloud: experience-cloud
product: adobe experience manager
audience: end-user
user-guide-title: AEM 6.5 배포 안내서
breadcrumb-title: Deploying Guide
user-guide-description: Learn more about installing, deploying, and the architecture of Adobe Experience Manager 6.5, including our Adobe Managed Services cloud deployment.
translation-type: tm+mt
source-git-commit: cb07e24b01084f57ad46615cb463ad5a0329c181
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 14%

---


# AEM 6.5 배포 사용 안내서 {#deploying}

+ [배포 사용 안내서](home.md)
+ AEM 플랫폼 소개 {#introduction}
   + [AEM 플랫폼 소개](platform.md)
   + [기술 요구 사항](technical-requirements.md)
   + [AEM 6.5의 스토리지 요소](storage-elements-in-aem-6.md)
   + [AEM with MongoDB](aem-with-mongodb.md)
+ AEM 배포 {#deploying}
   + [배포 및 유지 관리](deploy.md)
   + [권장 배포](recommended-deploys.md)
   + [애플리케이션 서버 설치](application-server-install.md)
   + [사용자 지정 독립형 설치](custom-standalone-install.md)
   + [명령줄 시작 및 중지](command-line-start-and-stop.md)
   + [AEM 6에서 노드 저장소 및 데이터 저장소 구성](data-store-config.md)
   + [개정 정리](revision-cleanup.md)
   + [Oak 쿼리 및 색인](queries-and-indexing.md)
   + [TarMK Cold Standby를 사용하여 AEM을 실행하는 방법](tarmk-cold-standby.md)
   + [AEM 6.5의 RDBMS 지원](rdbms-support-in-aem.md)
   + [Oak-run Jar를 통한 인덱싱](indexing-via-the-oak-run-jar.md)
   + [Oak-run.jar 인덱싱 사용 사례](oak-run-indexing-usecases.md)
   + [Oak 인덱스 문제 해결](troubleshooting-oak-indexes.md)
   + [집계된 사용 통계 수집 선택](opt-in-aggregated-usage-statistics.md)
   + [문제 해결](troubleshooting.md)
+ AEM 구성 {#configuring}
   + [기본 구성 개념](configuring.md)
   + [로깅](configure-logging.md)
   + [OSGi 구성](configuring-osgi.md)
   + [OSGi 구성 설정](osgi-configuration-settings.md)
   + [실행 모드](configure-runmodes.md)
   + [웹 콘솔](web-console.md)
   + [복제](replication.md)
   + [상호 SSL을 사용하여 복제](mssl-replication.md)
   + [복제 문제 해결](troubleshoot-rep.md)
   + [정적 개체 만료](expiration-static-objects.md)
   + [버전 제거](version-purging.md)
   + [AEM 인스턴스 모니터링 및 유지 관리](monitoring-and-maintaining.md)
   + [작업 오프로드](offloading.md)
   + [단일 사인온](single-sign-on.md)
   + [리소스 매핑](resource-mapping.md)
   + [SSL을 통해 HTTP 활성화](/help/sites-administering/ssl-by-default.md)
   + [일관성 및 순회 검사](consistency-check.md)
   + [성능 지침](performance-guidelines.md)
   + [성능 최적화](configuring-performance.md)
   + [자산 성과 가이드](assets-performance-sizing.md)
   + [구성 방법 문서](ht-deploy.md)
   + [웹 콘솔 구성](configuring-web-console.md)
+ Upgrading to AEM 6.5 {#upgrading}
   + [AEM 6.5로 업그레이드](upgrade.md)
   + [업그레이드 계획](upgrade-planning.md)
   + [Pattern Detector를 사용한 업그레이드 복잡성 평가](pattern-detector.md)
   + [AEM 6.5의 이전 버전과의 호환성](backward-compatibility.md)
   + [업그레이드 절차](upgrade-procedure.md)
   + [업그레이드 수행](in-place-upgrade.md)
   + [오프라인 재색인화를 사용하여 업그레이드 중 다운타임 감소](upgrade-offline-reindexing.md)
   + [레이지 컨텐츠 마이그레이션](lazy-content-migration.md)
   + [CRX2Oak 마이그레이션 도구 사용](using-crx2oak.md)
   + [업그레이드 전 유지 관리 작업](pre-upgrade-maintenance-tasks.md)
   + [업그레이드 후 확인 및 문제 해결](post-upgrade-checks-and-troubleshooting.md)
   + [사용자 지정 검색 Forms 업그레이드](upgrading-custom-search-forms.md)
   + [지속적인 업그레이드](sustainable-upgrades.md)
   + [코드 및 사용자 정의 업그레이드](upgrading-code-and-customizations.md)
   + [응용 프로그램 서버 설치 업그레이드 단계](app-server-upgrade.md)
   + [업그레이드 후 제거된 오래된 번들 목록](obsolete-bundles.md)
+ 저장소 재구성 {#restructuring}
   + [AEM 6.5의 저장소 재구성](repository-restructuring.md)
   + [AEM 6.5의 공용 저장소 재구성](all-repository-restructuring-in-aem-6-5.md)
   + [AEM 6.5의 사이트 저장소 재구성](sites-repository-restructuring-in-aem-6-5.md)
   + [AEM 6.5의 자산 저장소 재구성](assets-repository-restructuring-in-aem-6-5.md)
   + [AEM 6.5의 Dynamic Media Repository 재구성](dynamicmedia-repository-restructuring-in-aem-6-5.md)
   + [AEM 6.5의 Forms 리포지토리 구조조정](forms-repository-restructuring-in-aem-6-5.md)
   + [AEM 6.5의 전자 상거래 저장소 구조 조정](ecommerce-repository-restructuring-in-aem-6-5.md)
   + [Repository Recommendations for AEM Communities 6.5](communities-repository-restructuring-in-aem-6-5.md)
+ eCommerce {#ecommerce}
   + [eCommerce 개요](ecommerce.md)
   + [SAP Commerce Cloud](sap-commerce-cloud.md)
   + [Salesforce Commerce Cloud](https://github.com/adobe/commerce-salesforce)
   + [Magento](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html#!AdobeDocs/commerce-cif-documentation/master/integrations/02-AEM-Magento.md)
+ 우수 사례 {#practices}
   + [배포 우수 사례](best-practices.md)
   + [성능 트리](performance-tree.md)
   + [성능 테스트 모범 사례](best-practices-for-performance-testing.md)
   + [쿼리 및 색인 작성 우수 사례](best-practices-for-queries-and-indexing.md)
   + [고객을 위한 유저 인터페이스 Recommendations](ui-recommendations.md)
   + [성능 및 확장성](performance.md)
