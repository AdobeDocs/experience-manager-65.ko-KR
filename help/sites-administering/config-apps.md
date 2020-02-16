---
title: AEM Apps 구성
seo-title: AEM Apps 구성
description: AEM Apps 구성 방법을 알아봅니다.
seo-description: AEM Apps 구성 방법을 알아봅니다.
uuid: ab9acd93-da7f-4bb7-8d26-224044899068
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 34f24837-f5e2-41f0-a359-fdb695e1b8f2
translation-type: tm+mt
source-git-commit: 684d2d5f73d571a15c8155e7870134c28dc892b7

---


# AEM Apps 구성{#configuring-for-aem-apps}

Adobe Experience Manager Apps는 OTA(Air)를 통해 애플리케이션의 컨텐츠를 업데이트하는 기능을 제공합니다. 업데이트된 컨텐츠는 게시 인스턴스에 저장됩니다. 장치의 앱이 게시 인스턴스에 연결되도록 하고 업데이트를 확인하려면 게시 인스턴스를 구성하여 빈 레퍼러 헤더를 허용해야 합니다.

## 빈 레퍼러 헤더 구성 {#configuring-empty-referrer-header}

레퍼러 필터 서비스를 구성하려면:

* 다음 위치에서 Apache Felix 콘솔(**구성**)을 엽니다.
* https://&lt;server>:&lt;port_number>/system/console/configMgr
* 관리자로 로그인합니다.
* 구성 **메뉴에서** 다음을 선택합니다.Apache *Sling 레퍼러 필터*
* 비어 있거나 누락된 레퍼러 헤더를 허용하려면 [비어 있는 항목 허용] 필드를 선택합니다.
* Click **Save** to save your changes.

![chlimage_1-58](assets/chlimage_1-58a.png)

자세한 내용은 [OSGI 구성 설정](/help/sites-deploying/osgi-configuration-settings.md) 및 보안 검사 목록 - [교차 사이트 요청 위조](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) 문제를참조하십시오.
