---
title: 활성 기능 구성
seo-title: 활성 기능 구성
description: 커뮤니티에서 활성 기능 구성
seo-description: 커뮤니티에서 활성 기능 구성
uuid: 27be3128-1a7d-412e-99a9-6e3b3b0aec1c
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 765a3d9b-4552-403e-872c-fdf684ac271d
translation-type: tm+mt
source-git-commit: ce21755263a2e8a3f0e97acb7f586e32cedde83a
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 1%

---


# 활성 기능 구성 {#configuring-enablement-features}

## 개요 {#overview}

활성 기능은 [활성 커뮤니티](overview.md#enablement-community)를 만드는 기능을 제공합니다.

* 이 기능을 사용하려면 프로덕션 환경에서 사용할 추가 라이선스가 필요합니다.

활성 기능을 사용하려면 다음이 필요합니다.

설치:

* **SCORM**

   SCORM(Sharable Content Object Reference Model)은 e러닝의 표준 및 사양 컬렉션입니다. 또한 SCORM은 컨텐츠가 양도 가능한 ZIP 파일로 패키지되는 방법도 정의합니다.

* **MySQL**

   MySQL은 주로 SCORM 추적 및 지원 데이터 보고 및 비디오 진행 상황을 추적하는 데 사용되는 관계형 데이터베이스입니다. SCORM for enablement 기능 팩을 사용하려면 MySQL JDBC 드라이버가 필요합니다.

* **FFmpeg**

   FFmpeg는 오디오 및 비디오를 변환하고 스트리밍하기 위한 솔루션이며, 설치되면 [비디오 에셋](../../help/sites-authoring/default-components-foundation.md#video)의 적절한 트랜스코딩에 사용됩니다. 활성 커뮤니티의 경우, 작성자 환경에서 업로드된 리소스에 대한 메타데이터를 입수하고 리소스를 나열할 때 표시할 축소판을 생성하는 데 사용됩니다.

설정:

* **커뮤니티 관리자**

   활성 커뮤니티의 경우, `Community Enablement Managers` 사용자 그룹의 구성원만 `Community Site Enablement Manager`의 역할에 할당될 수 있으며, 이 그룹의 권한은 게시 환경의 컨텐츠 생성, 할당 및 멤버 관리를 포함할 수 있습니다.

옵션 구성:

* **Adobe Analytics**

   Adobe Analytics와의 통합은 포괄적인 보고 기능을 추가하고 Analytics에 비디오 하트비트 추가를 지원합니다.

* **Dispatcher**

## 구성 단계 {#configuration-steps}

다음은 역량 강화 커뮤니티에 필요한 단계입니다.

각 단계는 필요한 세부 사항을 제공하는 문서에 연결합니다.

**모든 작성자/게시 인스턴스:**

1. **[MySQL용 JDBC 드라이버 설치](deploy-communities.md#jdbc-driver-for-mysql)**

   웹 콘솔 사용(번들):*http://localhost:4502/system/console/bundles*

   SCORM 패키지를 설치하기 전에 *을(를) 설치합니다.*

1. **[SCORM 패키지 설치](deploy-communities.md#scorm-package)**


   패키지 관리자 사용:*http://localhost:4502/crx/packmgr/*

**모든 서버에서:**

1. **[MySQL, MySQL Workbench 설치](mysql.md)**

1. **[MySQL 데이터베이스 설치](mysql.md#database-setup)**

   작성자 인스턴스에서 다운로드한 SQL 스크립트 실행

   MySQL Workbench 사용

**동일한 서버 호스팅 작성자 인스턴스:**

1. **[FFmpeg 설치](ffmpeg.md)**

**모든 작성자/게시 인스턴스:**

1. **[JDBC 접속 풀 구성](mysql.md#configure-jdbc-connections)**

   웹 콘솔 사용(configMgr):*http://localhost:4502/system/console/configMgr*

1. **[SCORM 엔진 서비스 구성](mysql.md#aem-communities-scormengine-service)**

   웹 콘솔 사용(configMgr):*http://localhost:4502/system/console/configMgr*

1. **[CSRF 필터 구성](mysql.md#adobe-granite-csrf-filter)**

   웹 콘솔 사용(configMgr):*http://localhost:4502/system/console/configMgr*

**작성 인스턴스에서:**

1. (*선택적*) **[Analytics 서비스 구성](analytics.md)**

   도구, 배포, Cloud Services 콘솔 사용:*http://localhost:4502/etc/cloudservices/sitecatalyst.html*

1. **[FFmpeg 구성](ffmpeg.md#configure-ffmpeg-transcoding-service)**

   워크플로우/모델 콘솔 사용

1. **[터널 서비스 사용](deploy-communities.md#tunnel-service-on-author)**

   웹 콘솔 사용(configMgr):*http://localhost:4502/system/console/configMgr*

1. **[커뮤니티 관리자 만들기](users.md#creating-community-members)**

   작성 환경의 경우 클래식-UI 보안 콘솔을 사용하십시오.*http://localhost:4502/useradmin*

   경로 = /home/users/community로 사용자 만들기

   * 다음 그룹에 구성원을 추가합니다.

      * 커뮤니티 활성화 관리자
      * 커뮤니티 관리자

## Dispatcher {#dispatcher}

배포에 [AEM Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html)이(가) 포함되어 있는 경우 지원 기능이 제대로 작동하려면 `clientheader` 및 `filter` 섹션을 수정해야 합니다. [Dispatcher for Communities](dispatcher.md#enablement)을(를) 참조하십시오.
