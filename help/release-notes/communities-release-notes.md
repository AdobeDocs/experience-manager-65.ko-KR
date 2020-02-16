---
title: AEM Communities 릴리스 노트
description: Adobe Experience Manager 6.5 Communities와 관련된 릴리스 노트입니다.
uuid: 1b436959-581c-4b34-b2df-cccc5727da59
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: c3505807-1550-491a-8619-e87839afca4f
docset: aem65
translation-type: tm+mt
source-git-commit: 57bad4e74b2dfd9e389643bfe58ef25564c5c545

---


# AEM Communities 릴리스 노트{#aem-communities-release-notes}

6.4 릴리스 이후 AEM Communities에 대한 개선 사항을 확인하십시오. To learn about the new features in greater detail, see [AEM 6.5 Communities User Guide](https://helpx.adobe.com/experience-manager/6-4/communities/user-guide.html).

To obtain the latest release, see the [Deploying Communities](https://helpx.adobe.com/in/experience-manager/6-4/help/communities/deploy-communities.html#LatestReleases) section of the documentation.

## 주요 개선 사항 {#major-enhancements}

### 커뮤니티 참여에 대한 개선 {#enhancements-to-community-engagement}

**@언급 지원** AEM Communities를 통해 등록된 사용자가 사용자 생성 컨텐츠에서 다른 등록된 구성원에게 태그를 지정하여 관심을 유도할 수 있습니다. 그런 다음 태그가 지정된(멘션된) 구성원에게 해당 사용자 생성 컨텐츠에 대한 상세 링크와 정보가 제공됩니다. 그러나 사용자는 웹 및 이메일 알림을 비활성화/활성화할 수 있습니다.

![@mentions 지원](assets/at-mentions.png)

커뮤니티 사용자는 자신의 이름, 성 또는 사용자 이름을 검색하지 않아도 누군가가 자신의 관심을 끌었거나 주의를 기울여야 하는지 확인할 수 있습니다. 또한 UGC 작성자는 문제를 가장 잘 처리하고 입력을 추가할 수 있는 등록된 특정 사용자의 응답을 찾을 수 있습니다.

커뮤니티 관리자는 등록된 사용자가 해당 구성 요소에서 기능을 사용할 수 있도록 하려면 **커뮤니티 구성 요소에서 언급을 활성화해야 합니다.

**그룹 메시징**

등록된 커뮤니티 회원은 그룹 구성원에게 동일한 메시지를 개별적으로 보내는 대신 단일 이메일 작성을 통해 대량으로 메시지를 그룹에게 전송할 수 있습니다. To allow [group messaging](/help/communities/configure-messaging.md), enable both the instances of [Messaging Operations Service](/help/communities/messaging.md#group-messaging).

![그룹 메시지](assets/group-messaging.png)

### Bulk Moderation 개선 {#enhancements-to-bulk-moderation}

벌크 중재의 사용자 지정 필터

[이제 사용자 정의 필터를](/help/communities/moderation.md#custom-filters) 개발 및 일괄 중재 UI에 추가할 수 있습니다.

태그를 통한 필터링을 보여 주는 [샘플 프로젝트](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter)를 [Github](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter)에서 확인할 수 있습니다. 이 프로젝트를 기본으로 사용하여 유사한 사용자 지정 필터를 개발할 수 있습니다.

![사용자 지정 필터](assets/custom-tag-filter.png)

**Bulk Moderation에서 목록 보기**

사용자 생성 컨텐츠 항목을 표시하기 위해 bulk moderation에 개선된 UI가 있는 새 목록 보기가 제공되었습니다.

![목록 보기의 Bulk moderation](assets/list-view-moderation.png)

### 사이트 및 그룹 관리에 대한 개선 사항 {#enhancements-to-site-and-group-management}

**작성자 측 사이트 및 그룹 관리자**

AEM 6.5 Communities 이상에서는 서로 다른 커뮤니티 사이트 및 그룹/중첩 그룹의 분산된 관리를 허용합니다. 여러 커뮤니티 사이트 및 중첩 그룹을 호스팅하는 조직은 이제 사이트(및 그룹) 작성 시 작성자 측에서 관리자 역할의 구성원을 선택할 수 있습니다.

![사이트 관리자](assets/site-admin.png)

사이트 관리자는 계층 구조 레벨에서 그룹을 생성하고 기본 관리자가 될 수 있습니다. 이러한 관리자는 나중에 다른 그룹 관리자가 제거할 수 있습니다. 그룹 관리자는 자신의 그룹 G1을 관리하고 G1 아래에 중첩된 하위 그룹을 생성할 수 있습니다.

### 지원 기능 개선 {#enhancements-to-enablement}

**SCORM2017.1 지원**

The enablement functionality of AEM 6.5 Communities support Shareable Content Object Reference Model [(SCORM) 2017.1](https://rusticisoftware.com/blog/scorm-engine-2017-released/) engine.

**AEM Communities의 지원 구성 요소**지원 구성 요소(예: 카탈로그 및 강좌 재생, 할당, 파일 라이브러리)는 키보드 탐색을 지원하여 액세서빌러티를 향상시킵니다.

### 기타 개선 사항 {#other-enhancements}

* **Solr 7 지원**AEM 6.5 Communities는 MSRP 및 DSRP를 설정하는 동안 검색 플랫폼의 Apache Solr 7.0 버전을 지원합니다.
