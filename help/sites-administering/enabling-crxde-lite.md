---
title: AEM에서 CRXDE Lite 활성화
description: Adobe Experience Manager에서 CRXDE Lite을 활성화하는 방법을 알아봅니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
exl-id: bf51def2-1dd4-4bd3-b989-685058f0ead8
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: a3587d248569982a8f9b137602ba95dd40c47012
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 0%

---

# AEM에서 CRXDE Lite 활성화{#enabling-crxde-lite-in-aem}

AEM 설치가 최대한 안전하도록 보안 검사 목록에서 프로덕션 환경에서 [WebDAV를 사용하지 않도록 설정](/help/sites-administering/security-checklist.md#disable-webdav)합니다.

그러나 CRXDE Lite은 `org.apache.sling.jcr.davex` 번들이 제대로 작동하는지에 따라 다르므로 WebDAV를 사용하지 않도록 설정하면 CRXDE Lite도 효과적으로 사용하지 않도록 설정됩니다.

이 경우 `https://serveraddress:4502/crx/de/index.jsp`을(를) 검색하면 빈 루트 노드가 표시되고 CRXDE Lite 리소스에 대한 모든 HTTP 요청이 실패합니다.

```xml
404 Resource at '/crx/server/crx.default/jcr:root/.1.json' not found: No resource found
```

이 권장 사항은 공격 표면을 최대한 줄이기 위한 것이지만, 시스템 관리자는 때때로 프로덕션 인스턴스의 콘텐츠를 검색하거나 문제를 디버깅하기 위해 CRXDE Lite에 액세스해야 할 수도 있습니다.

[OSGi 설정](#enabling-crxde-lite-osgi) 또는 [cURL 명령](#enabling-crxde-lite-curl)을 사용하여 CRXDE Lite을 활성화할 수 있습니다.

>[!WARNING]
>
>이 메서드의 작동 방식에 약간의 차이가 있으므로 ***either*** OSGI ***or*** cURL을 사용해야 합니다.
>
>두 메서드는 서로 바꿀 수 있는 ***not***&#x200B;입니다.

## OSGI로 CRXDE Lite 활성화 {#enabling-crxde-lite-osgi}

비활성화된 경우 아래 절차에 따라 CRXDE Lite을 켤 수 있습니다.

1. `http://localhost:4502/system/console/components`의 OSGi 구성 요소 콘솔로 이동합니다.
1. 다음 구성 요소를 검색합니다.

   * `org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet`

1. 옆에 있는 렌치 아이콘을 클릭하여 구성 옵션을 확인합니다.

   ![chlimage_1-80](assets/chlimage_1-80a.png)

1. 다음 구성을 만듭니다.

   * **루트 경로:** `/crx/server`
   * **절대 URI 사용** 아래의 상자를 선택합니다.

1. CRXDE Lite 사용을 마치면 WebDAV를 다시 비활성화해야 합니다.

## cURL을 사용하여 CRXDE Lite 활성화 {#enabling-crxde-lite-curl}

다음 두 명령을 모두 실행하여 cURL을 통해 CRXDE Lite을 활성화할 수도 있습니다.

* `create-absolute-uri` 사용:

  ```shell
  curl -u admin:admin 'http://localhost:4502/system/console/configMgr/org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet' --data-raw 'apply=true&action=ajaxConfigManager&%24location=&dav.create-absolute-uri=true&propertylist=dav.create-absolute-uri'
  ```

* `alias` 정의:

  ```shell
  curl -u admin:admin 'http://localhost:4502/system/console/configMgr/org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet' --data-raw 'apply=true&action=ajaxConfigManager&%24location=&alias=/crx/server&propertylist=alias'
  ```

## 기타 리소스 {#other-resources}

AEM 6 보안 기능에 대한 자세한 내용은 다음 페이지를 참조하십시오.

* [AEM Security 검사 목록](/help/sites-administering/security-checklist.md)
* [프로덕션 준비 모드에서 AEM 실행](/help/sites-administering/production-ready.md)
