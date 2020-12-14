---
title: 구성원 기여도 제한
seo-title: 구성원 기여도 제한
description: 기여도 제한 기능을 사용하면 기여도를 스팸으로부터 보호하기 위해 제한할 수 있습니다
seo-description: 기여도 제한 기능을 사용하면 기여도를 스팸으로부터 보호하기 위해 제한할 수 있습니다
uuid: 99b2a855-3f0d-41a0-9572-517a7f29af9f
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: d855aac2-f34d-402f-9dc3-c7ad494b45f2
translation-type: tm+mt
source-git-commit: d80c6609b5a0ac299b57b1d0c0e8d6210e595b97
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---


# 구성원 기여도 제한 {#member-contribution-limits}

## 개요 {#overview}

기여도 제한 기능은 스팸 방지를 위한 수단으로 커뮤니티 구성원의 기여도를 제한할 수 있는 기능을 제공합니다.

회원이 제한되면 허용된 기여도 수를 초과하는 게시물은 제한을 초과하고 게시물이 거부된다는 경고가 표시됩니다. 그러면 커뮤니티 구성원은 커뮤니티 메시지 센터로 이동하여 해당 제한 사항을 제거할 수 있는 커뮤니티 관리자에게 문의할 수 있습니다.

기여도 제한은 [구성원 콘솔](members.md)에서 개별적으로 활성화하거나 사이트 방문자가 새 구성원이 될 때 자동으로 활성화되도록 구성할 수 있습니다.

구성원 콘솔을 사용하면 커뮤니티 관리자가 구성원에게 대해 언제든지 기여도 제한을 사전에 제거할 수 있으며, 구성원이 이러한 요청을 수행하는 커뮤니티 관리자에게 메시지를 보낼 때 다시 활성 상태로 제거할 수 있습니다.

## AEM Communities 사용자가 생성한 콘텐츠 기여도 제한 구성 {#aem-communities-user-generated-content-contribution-limits-configuration}

이 OSGi 구성:

* 기여도 제한의 특성(기간 내 게시물 수)을 정의합니다.
* 한도에 도달했을 때 회원에게 메시지를 보낼 수 있는 사용자를 식별합니다.
* 제한되지 않아도 되는 도메인을 식별합니다.

이 OSGi 구성에 도달하려면:

* 기본 게시자에서:
* 관리자 권한으로 로그인합니다.
* [웹 콘솔](../../help/sites-deploying/configuring-osgi.md)에 액세스합니다.

   * 예: [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* `AEM Communities User Generated Content Contribution Limits Configuration`을(를) 찾습니다.
* 편집 아이콘을 선택합니다.

![configure-limits](assets/configure-limits.png)

* **[!UICONTROL UGC 기여도 제한 자동 적용]**

   이 확인란을 선택하면 커뮤니티 구성원으로 등록할 때 사용자에게 기여도 제한을 자동으로 설정합니다. 이것은 커뮤니티 구성원의 프로필에 반영되며 [구성원 콘솔](members.md)에서 활성화/비활성화할 수 있습니다. 도메인에서 이메일 주소를 허용 목록에 추가하다 사용하는 새 멤버는 제한되지 않습니다.

   기본값은 선택되어 있지 않습니다.

* **[!UICONTROL UGC 제한]**

   최대 기여도 수입니다.

   기본값은 10개의 게시물입니다.

* **[!UICONTROL UGC 제한 주파수]**

   UGC 제한을 제한하는 기간입니다.

   기본값은 60분입니다.

* **[!UICONTROL 도메인]**

   하나 허용 목록에 추가하다 이상의 이메일 도메인의 목록. + 아이콘을 선택하여 추가 항목을 만듭니다.

   UGC 기여도 허용 목록에 추가하다 제한이 자동으로 적용되는 경우 도메인에 이메일 주소를 사용하는 사용자는 영향을 받지 않습니다. 예를 들어 도메인 `mycompany.com`이(가) 도메인 목록에 추가된 경우 이메일 주소 `me@mycompany.com`이(가) 있는 멤버는 게시로 제한되지 않습니다.

   기본값은 빈 허용 목록에 추가하다입니다.

* **[!UICONTROL 메시지 받는 사람]**

   구성원의 기여도 제한을 수정할 수 있는 하나 이상의 인가할 수 있는 구성원 ID 목록 + 아이콘을 선택하여 추가 항목을 만듭니다.

   멤버는 한도에 도달한 경우에만 지정된 구성원에게 도달할 수 있습니다.

   기본적으로 메시지를 받는 사람이 없습니다.

참고:기본 구성으로 인해 1시간 내에 10개의 게시물이 제한됩니다.
