---
title: AEM Communities 릴리스 노트
description: Adobe Experience Manager 6.5 Communities와 관련된 릴리스 노트입니다.
translation-type: tm+mt
source-git-commit: 8d60e064ab50f24016c049c8d5d0fceb784c99a3
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 69%

---


# AEM Communities 릴리스 노트 {#aem-communities-release-notes}

6.4 릴리스 이후 AEM Communities에 대한 개선 사항을 확인하십시오. 새로운 기능에 대해 자세히 알아보려면 [AEM 6.5 Communities 사용자 가이드](https://helpx.adobe.com/kr/experience-manager/6-4/communities/user-guide.html)를 참조하십시오.

최신 릴리스를 얻으려면 설명서의 [커뮤니티 배포](https://helpx.adobe.com/in/experience-manager/6-4/help/communities/deploy-communities.html#LatestReleases) 섹션을 참조하십시오.

## 주요 개선 사항 {#major-enhancements}

### 커뮤니티 참여에 대한 개선 {#enhancements-to-community-engagement}

**@Mentions**
supportAEM Communities를 사용하면 이제 등록된 사용자가 사용자 생성 컨텐트에서 다른 등록 멤버에 태그 지정(언급)하여 관심을 유도할 수 있습니다. 그런 다음 태그가 지정된(멘션된) 구성원에게 해당 사용자 생성 컨텐츠에 대한 상세 링크와 정보가 제공됩니다. 그러나 사용자는 웹 및 이메일 알림을 사용/사용 안함으로 설정할 수 있습니다.

![@mentions 지원](assets/at-mentions.png)

커뮤니티 사용자는 자신의 이름, 성 또는 사용자 이름을 검색하지 않아도 누군가가 자신의 관심을 끌었거나 주의를 기울여야 하는지 확인할 수 있습니다. 또한 UGC 작성자는 문제를 가장 잘 처리하고 입력을 추가할 수 있는 등록된 특정 사용자의 응답을 찾을 수 있습니다.

커뮤니티 관리자는 등록된 사용자가 해당 구성 요소의 기능을 사용할 수 있도록 커뮤니티 구성 요소에 대해 **언급 활성화**&#x200B;해야 합니다.

**그룹 메시징**

등록된 커뮤니티 회원은 그룹 구성원에게 동일한 메시지를 개별적으로 보내는 대신 단일 이메일 작성을 통해 대량으로 메시지를 그룹에게 전송할 수 있습니다. [그룹 메시징](/help/communities/configure-messaging.md)을 허용하려면 [Messaging Operations Service](/help/communities/messaging.md#group-messaging)의 인스턴스를 모두 활성화하십시오.

![그룹 메시지](assets/group-messaging.png)

### 대량 조정 개선 {#enhancements-to-bulk-moderation}

벌크 중재의 사용자 지정 필터

[이제 사용자 ](/help/communities/moderation.md#custom-filters) 지정 필터 검색을 개발하여 일괄 중재 UI에 추가할 수 있습니다.

태그를 통한 필터링을 보여 주는 [샘플 프로젝트](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter)를 [Github](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter)에서 확인할 수 있습니다. 이 프로젝트를 기본으로 사용하여 유사한 사용자 지정 필터를 개발할 수 있습니다.

![사용자 지정 필터](assets/custom-tag-filter.png)

**대량 조정에서 목록 보기**

사용자 생성 컨텐츠 항목을 표시하기 위해 대량 조정에 개선된 UI가 있는 새 목록 보기가 제공되었습니다.

![목록 보기의 대량 조정](assets/list-view-moderation.png)

### 사이트 및 그룹 관리에 대한 개선 사항 {#enhancements-to-site-and-group-management}

**작성자 측 사이트 및 그룹 관리자**

AEM 6.5 Communities 이상에서는 서로 다른 커뮤니티 사이트 및 그룹/중첩 그룹의 분산된 관리를 허용합니다. 여러 커뮤니티 사이트 및 중첩 그룹을 호스팅하는 조직은 이제 사이트(및 그룹) 작성 시 작성자 측에서 관리자 역할의 구성원을 선택할 수 있습니다.

![사이트 관리자](assets/site-admin.png)

사이트 관리자는 계층 구조 레벨에서 그룹을 생성하고 기본 관리자가 될 수 있습니다. 이러한 관리자는 나중에 다른 그룹 관리자가 제거할 수 있습니다. 그룹 관리자는 자신의 그룹 G1을 관리하고 G1 아래에 중첩된 하위 그룹을 생성할 수 있습니다.

### 지원 기능 개선 {#enhancements-to-enablement}

**SCORM2017.1 지원**

AEM 6.5 Communities의 지원 기능은 공유 가능한 콘텐츠 개체 참조 모델 [(SCORM) 2017.1](https://rusticisoftware.com/blog/scorm-engine-2017-released/) 엔진을 지원합니다.

* 지원 구성 요소의 키보드 탐색 지원
* AEM Communities의 활성 구성 요소(예: 카탈로그 및 강좌 재생, 할당, 파일 라이브러리)는 키보드 탐색을 지원하여 액세서빌러티를 향상시킵니다.

### 기타 개선 사항 {#other-enhancements}

* 솔루션 7 지원
* AEM 6.5 Communities는 MSRP 및 DSRP를 설정하는 동안 검색 플랫폼의 Apache Solr 7.0 버전을 지원합니다.
