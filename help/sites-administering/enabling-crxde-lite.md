---
title: AEM에서 CRXDE Lite 활성화
seo-title: Enabling CRXDE Lite in AEM
description: AEM에서 CRXDE Lite을 활성화하는 방법을 알아봅니다.
seo-description: Learn how to enable CRXDE Lite in AEM.
uuid: d7a3db67-6384-463b-9aa9-f08ecc6c99c6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 72df3ece-badf-466b-8f9a-0ec985d87741
exl-id: bf51def2-1dd4-4bd3-b989-685058f0ead8
source-git-commit: a4183bb9d72763ebea3b464c77fce978c723e053
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 1%

---

# AEM에서 CRXDE Lite 활성화{#enabling-crxde-lite-in-aem}

AEM 설치가 가능한 한 안전하도록 보안 체크리스트에서는 다음을 권장합니다 [webdav 비활성화](/help/sites-administering/security-checklist.md#disable-webdav) 프로덕션 환경에서.

그러나 CRXDE Lite은 다음에 따라 다릅니다. `org.apache.sling.jcr.davex` 번들이 제대로 작동하므로 WebDAV를 비활성화하면 CRXDE Lite도 효과적으로 비활성화됩니다.

이 경우 찾아보기 `https://serveraddress:4502/crx/de/index.jsp` 은 빈 루트 노드를 표시하며 CRXDE Lite 리소스에 대한 모든 HTTP 요청이 실패합니다.

```xml
404 Resource at '/crx/server/crx.default/jcr:root/.1.json' not found: No resource found
```

이 권장 사항은 공격 표면을 최대한 줄이기 위한 것이지만, 시스템 관리자는 때때로 프로덕션 인스턴스의 문제를 검색하거나 디버깅하기 위해 CRXDE Lite에 액세스해야 할 수도 있습니다.

다음 중 하나를 사용하여 CRXDE Lite을 활성화할 수 있습니다. [OSGi 설정](#enabling-crxde-lite-osgi) 또는 [cURL 명령](#enabling-crxde-lite-curl).

>[!WARNING]
>
>이러한 방법의 작동 방식에 약간의 차이가 있으므로 다음을 사용해야 합니다. ***다음 중 하나*** OSGI ***또는*** cURL.
>
>두 가지 방법은 다음과 같습니다. ***아님*** 호환됩니다.

## OSGI로 CRXDE Lite 활성화 {#enabling-crxde-lite-osgi}

비활성화된 경우 아래 절차에 따라 CRXDE Lite을 켤 수 있습니다.

1. 의 OSGi 구성 요소 콘솔로 이동합니다. `http://localhost:4502/system/console/components`
1. 다음 구성 요소를 검색합니다.

   * `org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet`

1. 구성 옵션을 보려면 옆에 있는 렌치 아이콘을 클릭합니다.

   ![chlimage_1-80](assets/chlimage_1-80a.png)

1. 다음 구성을 만듭니다.

   * **루트 경로:** `/crx/server`
   * 아래 상자를 선택합니다. **절대 URI 사용**.

1. CRXDE Lite 사용을 마치면 WebDAV를 다시 비활성화해야 합니다.

## cURL을 사용하여 CRXDE Lite 활성화 {#enabling-crxde-lite-curl}

다음 명령을 실행하여 cURL을 통해 CRXDE Lite을 활성화할 수도 있습니다.

```shell
curl -u admin:admin -F "jcr:primaryType=sling:OsgiConfig" -F "alias=/crx/server" -F "dav.create-absolute-uri=true" -F "dav.create-absolute-uri@TypeHint=Boolean" http://localhost:4502/apps/system/config/org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet
```

## 기타 리소스 {#other-resources}

AEM 6 보안 기능에 대한 자세한 내용은 다음 페이지를 참조하십시오.

* [AEM Security 검사 목록](/help/sites-administering/security-checklist.md)
* [프로덕션 준비 모드에서 AEM 실행](/help/sites-administering/production-ready.md)
