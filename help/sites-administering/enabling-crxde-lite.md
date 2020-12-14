---
title: AEM에서 CRXDE Lite 활성화
seo-title: AEM에서 CRXDE Lite 활성화
description: AEM에서 CRXDE Lite을 활성화하는 방법을 알아봅니다.
seo-description: AEM에서 CRXDE Lite을 활성화하는 방법을 알아봅니다.
uuid: d7a3db67-6384-463b-9aa9-f08ecc6c99c6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 72df3ece-badf-466b-8f9a-0ec985d87741
translation-type: tm+mt
source-git-commit: a833a34bbeb938c72cdb851a46b2ffd97aee9f6d
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 1%

---


# AEM{#enabling-crxde-lite-in-aem}에서 CRXDE Lite 활성화

AEM 설치가 가능한 한 안전한지 확인하려면 프로덕션 환경에서 [WebDAV](/help/sites-administering/security-checklist.md#disable-webdav)를 비활성화하는 것이 좋습니다.

그러나 CRXDE Lite은 `org.apache.sling.jcr.davex` 번들이 제대로 작동하기 위해 종속되므로 WebDAV를 비활성화하면 CRXDE Lite도 효과적으로 비활성화할 수 있습니다.

이 경우 `https://serveraddress:4502/crx/de/index.jsp`으로 이동하면 빈 루트 노드가 표시되고 CRXDE Lite 리소스에 대한 모든 HTTP 요청이 실패합니다.

```xml
404 Resource at '/crx/server/crx.default/jcr:root/.1.json' not found: No resource found
```

이 권장 사항은 공격 표면을 최대한 줄이기 위한 것이지만 시스템 관리자는 컨텐트를 검색하거나 프로덕션 인스턴스에서 문제를 디버그하기 위해 경우에 따라 CRXDE Lite에 액세스해야 할 수 있습니다.

비활성화된 경우 아래 절차에 따라 CRXDE Lite을 활성화할 수 있습니다.

1. `http://localhost:4502/system/console/components`의 OSGi 구성 요소 콘솔로 이동합니다.
1. 다음 구성 요소를 검색합니다.

   * `org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet`

1. 구성 옵션을 보려면 옆에 있는 공구 모양 아이콘을 클릭합니다.

   ![chlimage_1-80](assets/chlimage_1-80a.png)

1. 다음 구성을 만듭니다.

   * **루트 경로:** `/crx/server`
   * **절대 URI 사용** 아래의 상자에 확인 표시를 합니다.

1. CRXDE Lite 사용을 마치면 WebDAV를 다시 비활성화해야 합니다.

다음 명령을 실행하여 cURL을 통한 CRXDE Lite을 활성화할 수도 있습니다.

```shell
curl -u admin:admin -F "jcr:primaryType=sling:OsgiConfig" -F "alias=/crx/server" -F "dav.create-absolute-uri=true" -F "dav.create-absolute-uri@TypeHint=Boolean" http://localhost:4502/apps/system/config/org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet
```

## 기타 리소스 {#other-resources}

AEM 6 보안 기능에 대한 자세한 내용은 다음 페이지를 참조하십시오.

* [AEM 보안 검사 목록](/help/sites-administering/security-checklist.md)
* [프로덕션 준비 모드에서 AEM 실행](/help/sites-administering/production-ready.md)

