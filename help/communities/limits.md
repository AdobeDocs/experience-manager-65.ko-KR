---
title: 구성원 기여도 제한
seo-title: Member Contribution Limits
description: 기여도 제한 기능을 사용하면 스팸으로부터 보호하기 위해 기여도를 제한할 수 있습니다
seo-description: Contribution limits feature lets you limit the contributions to protect against spam
uuid: 99b2a855-3f0d-41a0-9572-517a7f29af9f
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: d855aac2-f34d-402f-9dc3-c7ad494b45f2
role: Admin
exl-id: d00a8eb2-47ce-425a-a312-f043f82912be
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 1%

---

# 구성원 기여도 제한 {#member-contribution-limits}

## 개요 {#overview}

기여도 제한 기능은 스팸을 방지하는 수단으로 커뮤니티 구성원의 기여도를 제한하는 기능을 제공합니다.

회원이 제한될 경우 허용된 기여 수를 초과하는 게시물은 한도를 초과했다는 경고를 받게 되고 게시물이 거부됩니다. 그런 다음 커뮤니티 메시지 센터로 이동하여 필요한 경우 제한을 제거할 수 있는 커뮤니티 관리자에게 문의할 수 있습니다.

기여도 제한은 [구성원 콘솔](members.md) 사이트 방문자가 새 구성원이 될 때 자동으로 활성화되도록 및/또는 구성됩니다.

구성원 콘솔을 사용하면 언제든지 커뮤니티 관리자가 구성원에 대한 기여도 제한을 미리 제거하거나, 구성원이 커뮤니티 관리자에게 그러한 요청을 하는 메시지를 보낼 때 반응적으로 제거할 수 있습니다.

## AEM Communities 사용자 생성 컨텐츠 기여도 제한 구성 {#aem-communities-user-generated-content-contribution-limits-configuration}

이 OSGi 구성은 다음과 같습니다.

* 기여도 제한의 특성(기간 내 게시물 수)을 정의합니다.
* 제한에 도달했을 때 구성원이 메시지를 보낼 수 있는 사용자를 식별합니다.
* 는 제한할 필요가 없는 도메인을 식별합니다.

이 OSGi 구성에 도달하려면:

* 기본 게시자의 경우:
* 관리자 권한으로 로그인합니다.
* 액세스 [웹 콘솔](../../help/sites-deploying/configuring-osgi.md).

   * 예를 들어, [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* 찾기 `AEM Communities User Generated Content Contribution Limits Configuration`.
* 편집 아이콘을 선택합니다.

![제한 구성](assets/configure-limits.png)

* **[!UICONTROL UGC 기여도 제한 자동 적용]**

   선택하면 사용자가 커뮤니티 구성원으로 등록할 때 기여도 제한을 자동으로 설정합니다. 커뮤니티 구성원의 프로필에 반영되며 [구성원 콘솔](members.md). 도메인 허용 목록의 새 구성원은 제한되지 않습니다.

   기본값은 선택 취소되어 있습니다.

* **[!UICONTROL UGC 제한]**

   최대 기여 수.

   기본값은 10개의 게시물입니다.

* **[!UICONTROL UGC 제한 빈도]**

   UGC 제한을 제한하는 기간.

   기본값은 60분입니다.

* **[!UICONTROL 도메인]**

   허용 목록에 추가하다 하나 이상의 이메일 도메인 목록 추가 항목을 만들려면 + 아이콘을 선택합니다.

   도메인의 허용 목록에 추가하다에 이메일 주소가 있는 사용자는 UGC 기여도 제한이 자동으로 적용될 때 영향을 받지 않습니다. 예를 들어 도메인인 경우 `mycompany.com` 도메인 목록에 이 추가된 다음 이메일 주소를 가진 구성원이 추가됩니다 `me@mycompany.com` 은(는) 게시에서 제한되지 않습니다.

   허용 목록에 추가하다 기본값은 빈 차원입니다.

* **[!UICONTROL 메시지 수신자]**

   구성원의 기여도 제한을 수정할 수 있는 승인 가능한 하나 이상의 구성원 ID 목록입니다. 추가 항목을 만들려면 + 아이콘을 선택합니다.

   회원은 한도에 도달했을 때만 지정된 회원에게 연락할 수 있습니다.

   기본값은 메시징 수신자가 없습니다.

참고: 기본 구성으로 인해 1시간 이내에 게시물이 10개로 제한됩니다.
