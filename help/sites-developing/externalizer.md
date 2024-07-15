---
title: URL 표면화
description: 외부화는 프로그래밍 방식으로 리소스 경로를 외부 및 절대 URL로 변환할 수 있는 OSGI 서비스입니다
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
docset: aem65
exl-id: 971d6c25-1fbe-4c07-944e-be6b97a59922
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 0%

---

# URL 표면화{#externalizing-urls}

Adobe Experience Manager(AEM)에서 **외부화**&#x200B;은(는) 미리 구성된 DNS를 사용하여 경로를 접두사로 추가하여 리소스 경로(예: `/path/to/my/page`)를 외부 및 절대 URL(예: `https://www.mycompany.com/path/to/my/page`)로 프로그래밍 방식으로 변환할 수 있는 OSGI 서비스입니다.

인스턴스가 웹 레이어 뒤에서 실행 중인 경우 외부로 표시되는 URL을 알 수 없고 경우에 따라 링크가 요청 범위 외부에서 만들어져야 하므로 이 서비스는 이러한 외부 URL을 구성하고 빌드할 수 있는 중앙 위치를 제공합니다.

이 페이지에서는 **외부화** 서비스를 구성하는 방법과 사용 방법을 설명합니다. 자세한 내용은 [Javadocs](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/Externalizer.html)을 참조하세요.

## 외부화 서비스 구성 {#configuring-the-externalizer-service}

**외부화** 서비스를 사용하면 프로그래밍 방식으로 리소스 경로를 접두사로 사용하는 여러 도메인을 중앙에서 정의할 수 있습니다. 각 도메인은 도메인을 프로그래밍 방식으로 참조하는 데 사용하는 고유한 이름으로 식별됩니다.

**외부화** 서비스에 대한 도메인 매핑을 정의하려면 다음을 수행하십시오.

1. **도구**, **웹 콘솔**&#x200B;을 통해 구성 관리자로 이동하거나 다음을 입력합니다.

   `https://<host>:<port>/system/console/configMgr`

1. **일 CQ 링크 외부화**&#x200B;를 클릭하여 구성 대화 상자를 엽니다.

   >[!NOTE]
   >
   >구성에 대한 직접 링크는 `https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl`입니다.

   ![aem-externalizer-01](assets/aem-externalizer-01.png)

1. **도메인** 매핑 정의: 매핑은 코드에서 도메인, 스페이스 및 도메인을 참조하는 데 사용할 수 있는 고유한 이름으로 구성됩니다.

   `<unique-name> [scheme://]server[:port][/contextpath]`

   위치:

   * **스키마**&#x200B;은(는) http 또는 https이지만 ftp일 수도 있습니다.

      * 원하는 경우 https를 사용하여 https 링크를 적용합니다
      * URL의 외부화를 요청할 때 클라이언트 코드가 스키마를 재정의하지 않는 경우에 사용됩니다.

   * **server**&#x200B;은(는) 호스트 이름입니다(도메인 이름 또는 ip 주소일 수 있음).
   * **port**(선택 사항)은 포트 번호입니다.
   * **contextpath**(선택 사항)은 AEM이 다른 컨텍스트 경로 아래에 웹 앱으로 설치된 경우에만 설정됩니다.

   예를 들어`production https://my.production.instance`

   다음 매핑 이름은 사전 정의되어 있으며 AEM이 이 이름을 사용하므로 설정해야 합니다.

   * `local` - 로컬 인스턴스
   * `author` - 제작 시스템 DNS
   * `publish` - 공개 웹 사이트 DNS

   >[!NOTE]
   >
   >사용자 지정 구성을 사용하면 `production`, `staging`과(와) 같은 범주 또는 `my-internal-webservice`과(와) 같은 외부 비 AEM 시스템을 추가할 수 있습니다. 이러한 URL을 프로젝트의 코드 베이스에 있는 여러 위치에서 하드코딩하지 않는 것이 유용합니다.

1. 변경 내용을 저장하려면 **저장**&#x200B;을 클릭하세요.

>[!NOTE]
>
>Adobe은 [저장소에 구성을 추가](/help/sites-deploying/configuring.md#addinganewconfigurationtotherepository)할 것을 권장합니다.

### Externalizer 서비스 사용 {#using-the-externalizer-service}

이 섹션에서는 **Externalizer** 서비스를 사용하는 방법에 대한 몇 가지 예를 보여 줍니다.

1. **JSP에서 Externalizer 서비스를 가져오려면:**

   ```java
   Externalizer externalizer = resourceResolver.adaptTo(Externalizer.class);
   ```

1. **&#39;게시&#39; 도메인을 사용하여 경로를 외부화하려면:**

   ```java
   String myExternalizedUrl = externalizer.publishLink(resolver, "/my/page") + ".html";
   ```

   도메인 매핑 가정:

   * `publish https://www.website.com`

   `myExternalizedUrl`은(는) 다음 값으로 끝납니다.

   * `https://www.website.com/contextpath/my/page.html`

1. **&#39;작성자&#39; 도메인이 있는 경로를 외부화하려면:**

   ```java
   String myExternalizedUrl = externalizer.authorLink(resolver, "/my/page") + ".html";
   ```

   도메인 매핑 가정:

   * `author https://author.website.com`

   `myExternalizedUrl`은(는) 다음 값으로 끝납니다.

   * `https://author.website.com/contextpath/my/page.html`

1. **경로를 &#39;로컬&#39; 도메인으로 외부화하려면:**

   ```java
   String myExternalizedUrl = externalizer.externalLink(resolver, Externalizer.LOCAL, "/my/page") + ".html";
   ```

   도메인 매핑 가정:

   * `local https://publish-3.internal`

   `myExternalizedUrl`은(는) 다음 값으로 끝납니다.

   * `https://publish-3.internal/contextpath/my/page.html`

1. [Javadocs](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/Externalizer.html)에서 더 많은 예제를 찾을 수 있습니다.
