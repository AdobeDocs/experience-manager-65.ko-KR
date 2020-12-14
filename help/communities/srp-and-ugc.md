---
title: SRP 및 UGC Essentials
seo-title: SRP 및 UGC Essentials
description: 스토리지 리소스 공급자 및 사용자 생성 컨텐츠 개요
seo-description: 스토리지 리소스 공급자 및 사용자 생성 컨텐츠 개요
uuid: a4ee8725-f554-4fcf-ac1e-34878d6c02f8
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 0763f236-5648-49e9-8a24-dbc8f4c77ee3
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 0%

---


# SRP 및 UGC 필수 {#srp-and-ugc-essentials}

## 소개 {#introduction}

SRP(저장소 리소스 공급자)와 사용자 생성 컨텐트(UGC)와의 관계에 익숙하지 않은 경우 [커뮤니티 컨텐트 저장소](working-with-srp.md) 및 [스토리지 리소스 공급자 개요](srp.md)를 방문하십시오.

설명서의 이 섹션에서는 SRP 및 UGC에 대한 몇 가지 중요한 정보를 제공합니다.

## StorageResourceProvider API {#storageresourceprovider-api}

SocialResourceProvider API(SRP API)는 다양한 Sling 리소스 공급자 API의 확장입니다. 페이지 매김 및 원자적 증가에 대한 지원이 포함되어 있습니다(총계 및 점수 매김에 유용함).

날짜, 도움말, 투표 수 등을 기준으로 정렬할 필요가 있으므로 SCF 구성 요소에 대해 쿼리가 필요합니다. 모든 SRP 옵션에는 버킷에 의존하지 않는 유연한 쿼리 메커니즘이 있습니다.

SRP 저장소 위치는 구성 요소 경로를 통합합니다. 루트 경로는 ASRP, MSRP 또는 JSRP와 같이 선택한 SRP 옵션에 따라 다르므로 SRP API는 항상 UGC에 액세스하는 데 사용해야 합니다.

SRP API는 추상 클래스가 아니라 인터페이스입니다. 새 릴리스로 업그레이드하면 향후 내부 구현에 대한 개선 사항이 보이지 않으므로 사용자 지정 구현을 가볍게 수행해서는 안 됩니다.

SRP API를 사용하는 방법은 SocialResourceUtilities 패키지에 있는 유틸리티와 같이 제공된 유틸리티를 통해 제공됩니다.

AEM 6.0 이전 버전에서 업그레이드하는 경우 오픈 소스 도구를 사용할 수 있는 모든 SRP에 대해 UGC를 마이그레이션해야 합니다. [AEM Communities 6.3으로 업그레이드](upgrade.md)를 참조하십시오.

>[!NOTE]
>
>이전에는 UGC에 액세스하는 유틸리티가 더 이상 존재하지 않는 SocialUtils 패키지에 들어 있었습니다.
>
>대체 유틸리티에 대해서는 [SocialUtils 리팩토링](socialutils.md)을 참조하십시오.

## UGC {#utility-method-to-access-ugc}에 액세스하는 유틸리티 메서드

UGC에 액세스하려면 SRP의 UGC에 액세스하는 데 적합한 경로를 반환하고 SocialUtils 패키지에 있는 더 이상 사용되지 않는 메서드를 대체하는 SocialResourceUtilities 패키지의 메서드를 사용합니다.

다음은 servlet에서 resourceToUGCtoragePath() 메서드를 사용하는 간단한 예입니다.

```java
import com.adobe.cq.social.srp.utilities.api.SocialResourceUtilities;

@Reference
private SocialResourceUtilities socialResourceUtilities;

@Override
protected void doGet(final SlingHttpServletRequest request, final SlingHttpServletResponse response) throws ServletException, IOException {
  String ugcPath = socialResourceUtilities.resourceToUGCStoragePath(request.getResource());
  // rest of servlet
}
```

다른 SocialUtils 교체에는 [SocialUtils 리팩토링](socialutils.md)을 참조하십시오.

코딩 지침을 보려면 [SRP](accessing-ugc-with-srp.md)로 UGC 액세스를 참조하십시오.

>[!CAUTION]
>
>경로 resourceToUGCStoragePath()가 반환하는 경로는 [ACL 검사](srp.md#for-access-control-acls)에 적합하지 않은 *입니다.*

## ACL {#utility-method-to-access-acls}에 액세스하는 유틸리티 메서드

ASRP 및 MSRP와 같은 일부 SRP 구현은 ACL 확인을 제공하지 않는 데이터베이스에 커뮤니티 콘텐츠를 저장합니다. 그림자 노드는 로컬 저장소의 ACL을 적용할 수 있는 위치를 제공합니다.

SRP API를 사용하는 모든 SRP 옵션은 모든 CRUD 작업 전에 그림자 위치를 동일하게 확인합니다.

ACL을 확인하려면 리소스의 UGC에 적용된 권한을 확인하는 데 적합한 경로를 반환하는 메서드를 사용합니다.

다음은 servlet에서 resourceToACLPath() 메서드를 사용하는 간단한 예입니다.

```java
import com.adobe.cq.social.srp.utilities.api.SocialResourceUtilities;

@Reference
private SocialResourceUtilities socialResourceUtilities;

@Override
protected void doGet(final SlingHttpServletRequest request, final SlingHttpServletResponse response) throws ServletException, IOException {
  String aclPath = socialResourceUtilities.resourceToACLPath(request.getResource());
  // rest of servlet
}
```

>[!CAUTION]
>
>resourceToACLPath()가 반환하는 경로는 UGC](#utility-method-to-access-acls) 자체에 액세스하는 데 적합한 *이(가) 아닌*&#x200B;입니다.[

## UGC 관련 저장소 위치 {#ugc-related-storage-locations}

JSRP 또는 MSRP를 사용하여 개발할 때 스토리지 위치에 대한 다음 설명은 도움이 될 수 있습니다. JSRP([CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)) 및 MSRP(MongoDB 도구)에 대한 UGC에 액세스할 수 있는 UI가 현재 없습니다.

**구성 요소 위치**

멤버가 게시 환경에서 UGC에 입장하면 AEM 사이트의 일부로 구성 요소와 상호 작용합니다.

이러한 구성 요소의 예는 [커뮤니티 구성 요소 안내서](components-guide.md) 사이트에 있는 [주석 구성 요소](http://localhost:4502/content/community-components/en/comments.html)입니다. 로컬 저장소의 주석 노드의 경로는 다음과 같습니다.

* 구성 요소 경로 = `/content/community-components/en/comments/jcr:content/content/includable/comments`

**그림자 노드 위치**

UGC를 만들면 필요한 ACL이 적용되는 [그림자 노드](srp.md#about-shadow-nodes-in-jcr)도 만들어집니다. 로컬 저장소의 해당 그림자 노드에 대한 경로는 구성 요소 경로에 대한 그림자 노드 루트 경로를 미리 설정한 결과입니다.

* 루트 경로 = `/content/usergenerated`
* 주석 그림자 노드 = `/content/usergenerated/content/community-components/en/comments/jcr:content/content/includable/comments`

**UGC 위치**

UGC는 두 위치 모두에서 생성되며 SRP API를 호출하는 [유틸리티 메서드](#utility-method-to-access-ugc)를 사용해야만 합니다.

* 루트 경로 = `/content/usergenerated/asi/srp-choice`
* JSRP용 UGC 노드 = `/content/usergenerated/asi/jcr/content/community-components/en/comments/jcr:content/content/includable/comments/srzd-let_it_be_`

*JSRP의 경우* UGC 노드는  ** 입력된 AEM 인스턴스(작성자 또는 게시)에만 있습니다. 게시 인스턴스에 입력하는 경우 작성자의 중재 콘솔에서 중재를 사용할 수 없습니다.

## 관련 정보 {#related-information}

* [스토리지 자원 공급자 개요](srp.md)  - 소개 및 저장소 사용 개요.
* [SRP](accessing-ugc-with-srp.md) - 코딩 가이드라인을 사용하여 UGC 액세스
* [SocialUtils 리팩토링](socialutils.md)  - 사용되지 않는 유틸리티 메서드를 현재 SRP 유틸리티 메서드에 매핑합니다.
