---
title: URL 표면화
seo-title: URL 표면화
description: Externalizer는 리소스 경로를 프로그래밍 방식으로 외부 및 절대 URL로 변환할 수 있는 OSGI 서비스입니다
seo-description: Externalizer는 리소스 경로를 프로그래밍 방식으로 외부 및 절대 URL로 변환할 수 있는 OSGI 서비스입니다
uuid: 65bcc352-fc8c-4aa0-82fb-1321a035602d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 938469ad-f466-42f4-8b6f-bfc060ae2785
docset: aem65
exl-id: 971d6c25-1fbe-4c07-944e-be6b97a59922
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 1%

---

# URL 표면화{#externalizing-urls}

AEM에서 **Externalizer**&#x200B;는 프로그래밍 방식으로 리소스 경로(예: )를 변환할 수 있는 OSGI 서비스입니다.`/path/to/my/page`)를 미리 구성된 DNS로 경로를 접두사로 사용하여 외부 및 절대 URL(예: `https://www.mycompany.com/path/to/my/page`)에 추가합니다.

인스턴스가 웹 레이어 뒤에서 실행 중인 경우 외부에서 볼 수 있는 URL을 알 수 없고, 경우에 따라 요청 범위 외부에서 링크를 만들어야 하기 때문에 이 서비스는 이러한 외부 URL을 구성하고 빌드할 수 있는 중앙 위치를 제공합니다.

이 페이지에서는 **Externalizer** 서비스를 구성하는 방법과 이 서비스를 사용하는 방법을 설명합니다. 자세한 내용은 [Javadocs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html)를 참조하십시오.

## Externalizer 서비스 {#configuring-the-externalizer-service} 구성

**Externalizer** 서비스를 사용하면 프로그래밍 방식으로 리소스 경로를 접두사로 지정하는 데 사용할 수 있는 여러 도메인을 중앙에서 정의할 수 있습니다. 각 도메인은 프로그래밍 방식으로 도메인을 참조하는 데 사용되는 고유한 이름으로 식별됩니다.

**Externalizer** 서비스에 대한 도메인 매핑을 정의하려면

1. **도구**&#x200B;를 통해 구성 관리자로 이동한 다음 **웹 콘솔**&#x200B;을 통해 이동하거나, 다음을 입력합니다.

   `https://<host>:<port>/system/console/configMgr`

1. **Day CQ Link Externalizer**&#x200B;를 클릭하여 구성 대화 상자를 엽니다.

   >[!NOTE]
   >
   >구성에 대한 직접 링크는 `https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl`입니다.

   ![aem-externalizer-01](assets/aem-externalizer-01.png)

1. **도메인** 매핑을 정의합니다.매핑은 코드 내에서 도메인, 공간 및 도메인을 참조하는 데 사용할 수 있는 고유한 이름으로 구성됩니다.

   `<unique-name> [scheme://]server[:port][/contextpath]`

   위치:

   * **** 스키마는 일반적으로 http 또는 https이지만 ftp 등일 수 있습니다.

      * 원할 경우 https를 사용하여 https 링크 적용
      * URL의 외부화를 요청할 때 클라이언트 코드가 스키마를 재정의하지 않는 경우 사용됩니다.
   * **** server는 호스트 이름입니다(도메인 이름 또는 ip 주소일 수 있음).
   * **port** (선택 사항)는 포트 번호입니다.
   * **contextpath** (선택 사항)는 AEM이 다른 컨텍스트 경로 아래에 웹 앱으로 설치된 경우에만 설정됩니다.

   예를 들어,`production https://my.production.instance`

   다음 매핑 이름은 사전 정의되어 있으며, AEM이 매핑 이름을 사용함에 따라 항상 설정되어야 합니다.

   * `local` - 로컬 인스턴스
   * `author` - 작성 시스템 DNS
   * `publish` - 공개 웹 사이트 DNS

   >[!NOTE]
   >
   >사용자 지정 구성을 사용하면 `production`, `staging` 등의 새 카테고리 또는 `my-internal-webservice` 등의 외부 비 AEM 시스템도 추가할 수 있습니다. 이러한 URL을 프로젝트의 코드 베이스에 있는 서로 다른 위치에 하드코딩하지 않는 것이 유용합니다.

1. **저장**&#x200B;을 클릭하여 변경 내용을 저장합니다.

>[!NOTE]
>
>Adobe은 [구성을 저장소](/help/sites-deploying/configuring.md#addinganewconfigurationtotherepository)에 추가할 것을 권장합니다.

### Externalizer 서비스 {#using-the-externalizer-service} 사용

이 섹션에서는 **Externalizer** 서비스를 사용하는 방법에 대한 몇 가지 예를 보여줍니다.

1. **JSP에서 Externalizer 서비스를 가져오려면 다음을 수행하십시오.**

   ```java
   Externalizer externalizer = resourceResolver.adaptTo(Externalizer.class);
   ```

1. **&#39;publish&#39; 도메인으로 경로를 구체화하려면**

   ```java
   String myExternalizedUrl = externalizer.publishLink(resolver, "/my/page") + ".html";
   ```

   도메인 매핑이 다음과 같다고 가정합니다.

   * `publish https://www.website.com`

   `myExternalizedUrl` 다음으로 끝남 값:

   * `https://www.website.com/contextpath/my/page.html`


1. **&#39;author&#39; 도메인으로 경로를 표면화하려면**

   ```java
   String myExternalizedUrl = externalizer.authorLink(resolver, "/my/page") + ".html";
   ```

   도메인 매핑이 다음과 같다고 가정합니다.

   * `author https://author.website.com`

   `myExternalizedUrl` 다음으로 끝남 값:

   * `https://author.website.com/contextpath/my/page.html`


1. **&#39;local&#39; 도메인으로 경로를 표면화하려면**

   ```java
   String myExternalizedUrl = externalizer.externalLink(resolver, Externalizer.LOCAL, "/my/page") + ".html";
   ```

   도메인 매핑이 다음과 같다고 가정합니다.

   * `local https://publish-3.internal`

   `myExternalizedUrl` 다음으로 끝남 값:

   * `https://publish-3.internal/contextpath/my/page.html`


1. [Javadocs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html)에서 더 많은 예를 찾을 수 있습니다.
