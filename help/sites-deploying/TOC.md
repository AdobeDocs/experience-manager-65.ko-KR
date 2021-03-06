---
cloud: Experience Cloud
product: adobe experience manager
solution: Experience Manager, Experience Manager Sites
audience: end-user
user-guide-title: AEM 6.5 Deploying 안내서
breadcrumb-title: Deploying 안내서
user-guide-description: Adobe Managed Services 클라우드 배포를 포함하여 Adobe Experience Manager 6.5의 설치, 배포 및 아키텍처에 대해 자세히 알아봅니다.
feature: Deploying
role: Architect
source-git-commit: f29612ee633d2a62144b770f3c225fc82b9174f8
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 20%

---


# AEM 6.5 배포 사용 안내서 {#deploying}

+ [배포 사용 안내서](home.md)
+ AEM Platform 소개 {#introduction}
   + [AEM Platform 소개](platform.md)
   + [기술 요구 사항](technical-requirements.md)
   + [AEM 6.5의 저장소 요소](storage-elements-in-aem-6.md)
   + [AEM과 MongoDB](aem-with-mongodb.md)
+ AEM 배포 {#deploying}
   + [배포 및 유지 관리](deploy.md)
   + [권장 배포](recommended-deploys.md)
   + [애플리케이션 서버 설치](application-server-install.md)
   + [사용자 지정 독립형 설치](custom-standalone-install.md)
   + [명령줄 시작 및 중지](command-line-start-and-stop.md)
   + [AEM 6에서 노드 저장소 및 데이터 저장소 구성](data-store-config.md)
   + [개정 정리](revision-cleanup.md)
   + [Oak 쿼리 및 색인 지정](queries-and-indexing.md)
   + [TarMK Cold Standby를 사용하여 AEM을 실행하는 방법](tarmk-cold-standby.md)
   + [AEM 6.5의 RDBMS 지원](rdbms-support-in-aem.md)
   + [Oak-run Jar를 통한 색인 지정](indexing-via-the-oak-run-jar.md)
   + [Oak-run.jar 색인 지정 사용 사례](oak-run-indexing-usecases.md)
   + [Oak 색인 문제 해결](troubleshooting-oak-indexes.md)
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
   + [버전 삭제](version-purging.md)
   + [AEM 인스턴스 모니터링 및 유지 관리](monitoring-and-maintaining.md)
   + [작업 오프로딩](offloading.md)
   + [단일 사인온](single-sign-on.md)
   + [리소스 매핑](resource-mapping.md)
   + [SSL을 통해 HTTP 활성화](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/ssl-by-default.html)
   + [일관성 및 순회 검사](consistency-check.md)
   + [성능 지침](performance-guidelines.md)
   + [성능 최적화](configuring-performance.md)
   + [Assets 성능 안내서](assets-performance-sizing.md)
   + [구성 방법 문서](ht-deploy.md)
   + [웹 콘솔 구성](configuring-web-console.md)
+ AEM 6.5로 업그레이드 {#upgrading}
   + [AEM 6.5로 업그레이드](upgrade.md)
   + [업그레이드 계획](upgrade-planning.md)
   + [패턴 탐지기를 사용한 업그레이드 복잡성 평가](pattern-detector.md)
   + [AEM 6.5의 이전 버전과의 호환성](backward-compatibility.md)
   + [업그레이드 프로시저](upgrade-procedure.md)
   + [즉석 업그레이드 수행](in-place-upgrade.md)
   + [오프라인 재색인화를 사용하여 업그레이드 중 다운타임 감소](upgrade-offline-reindexing.md)
   + [레이지 컨텐츠 마이그레이션](lazy-content-migration.md)
   + [CRX2Oak 마이그레이션 도구 사용](using-crx2oak.md)
   + [업그레이드 전 유지 관리 작업](pre-upgrade-maintenance-tasks.md)
   + [업그레이드 후 확인 및 문제 해결](post-upgrade-checks-and-troubleshooting.md)
   + [사용자 지정 검색 Forms 업그레이드](upgrading-custom-search-forms.md)
   + [지속 가능한 업그레이드](sustainable-upgrades.md)
   + [코드 및 사용자 지정 업그레이드](upgrading-code-and-customizations.md)
   + [응용 프로그램 서버 설치에 대한 업그레이드 단계](app-server-upgrade.md)
   + [업그레이드 후 제거된 오래된 번들 목록](obsolete-bundles.md)
+ 저장소 재구성 {#restructuring}
   + [AEM 6.5의 저장소 구조 변경](repository-restructuring.md)
   + [AEM 6.5의 공통 저장소 구조 변경](all-repository-restructuring-in-aem-6-5.md)
   + [AEM 6.5의 사이트 저장소 구조 변경](sites-repository-restructuring-in-aem-6-5.md)
   + [AEM 6.5의 Assets 저장소 구조 변경](assets-repository-restructuring-in-aem-6-5.md)
   + [AEM 6.5의 Dynamic Media 저장소 구조 변경](dynamicmedia-repository-restructuring-in-aem-6-5.md)
   + [AEM 6.5의 Forms 저장소 구조 변경](forms-repository-restructuring-in-aem-6-5.md)
   + [AEM 6.5의 E-Commerce Repository 구조 변경](ecommerce-repository-restructuring-in-aem-6-5.md)
   + [6.5에서 AEM Communities에 대한 저장소 구조 변경](communities-repository-restructuring-in-aem-6-5.md)
+ 우수 사례 {#practices}
   + [배포 우수 사례](best-practices.md)
   + [성능 트리](performance-tree.md)
   + [성능 테스트 우수 사례](best-practices-for-performance-testing.md)
   + [쿼리 및 색인 생성에 대한 우수 사례](best-practices-for-queries-and-indexing.md)
   + [고객을 위한 사용자 인터페이스 Recommendations](ui-recommendations.md)
   + [성능 및 확장성](performance.md)
