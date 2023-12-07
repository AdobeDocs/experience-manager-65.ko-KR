---
title: SRP 및 UGC 필수 패키지
description: 저장소 리소스 제공자 및 사용자 생성 컨텐츠 개요
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 8279684f-23dd-4234-bf01-fd2ce74bcb4e
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 0%

---

# SRP 및 UGC 필수 패키지 {#srp-and-ugc-essentials}

## 소개 {#introduction}

SRP(저장소 리소스 제공자) 및 UGC(사용자 생성 컨텐츠)와의 관계가 익숙하지 않은 경우 다음을 방문하십시오. [커뮤니티 콘텐츠 저장소](working-with-srp.md) 및 [저장소 리소스 공급자 개요](srp.md).

설명서의 이 섹션에서는 SRP 및 UGC에 대한 몇 가지 중요한 정보를 제공합니다.

## StorageResourceProvider API {#storageresourceprovider-api}

SocialResourceProvider API(SRP API)는 다양한 Sling 리소스 제공자 API의 확장입니다. 페이지 매김 및 원자 증분에 대한 지원이 포함됩니다(집계 및 점수에 유용함).

날짜, 유용성, 투표 수 등을 기준으로 정렬해야 하므로 SCF 구성 요소에는 쿼리가 필요합니다. 모든 SRP 옵션에는 버킷팅에 의존하지 않는 유연한 쿼리 메커니즘이 있습니다.

SRP 저장소 위치에는 구성 요소 경로가 포함됩니다. 루트 경로가 ASRP, MSRP 또는 JSRP와 같이 선택한 SRP 옵션에 따라 달라지므로 SRP API는 항상 UGC에 액세스하는 데 사용해야 합니다.

SRP API는 추상 클래스가 아니라 인터페이스입니다. 새로운 릴리스로 업그레이드할 때 향후 내부 구현 개선의 이점이 누락되므로 사용자 지정 구현을 가볍게 생각해서는 안 됩니다.

SRP API를 사용하기 위한 수단은 SocialResourceUtilities 패키지에 있는 유틸리티와 같은 제공된 유틸리티를 통해 제공됩니다.

AEM 6.0 또는 이전 버전에서 업그레이드하는 경우 오픈 소스 도구를 사용할 수 있는 모든 SRP에 대해 UGC를 마이그레이션해야 합니다. 다음을 참조하십시오 [AEM Communities 6.3으로 업그레이드](upgrade.md).

>[!NOTE]
>
>지금까지 UGC에 액세스하기 위한 유틸리티는 더 이상 존재하지 않는 SocialUtils 패키지에서 발견되었습니다.
>
>교체 유틸리티에 대해서는 다음을 참조하십시오. [SocialUtils 리팩터링](socialutils.md).

## UGC에 액세스하는 유틸리티 방법 {#utility-method-to-access-ugc}

UGC에 액세스하려면 SRP에서 UGC에 액세스하는 데 적합한 경로를 반환하고 SocialUtils 패키지에 있는 더 이상 사용되지 않는 메서드를 대체하는 SocialResourceUtilities 패키지의 메서드를 사용하십시오.

다음은 서블릿에서 resourceToUGCStoragePath() 메서드를 사용하는 최소한의 예입니다.

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

다른 SocialUtils 대체 요소의 경우 다음을 참조하십시오. [SocialUtils 리팩터링](socialutils.md).

코딩 지침은 다음을 참조하십시오. [SRP를 사용하여 UGC에 액세스](accessing-ugc-with-srp.md).

>[!CAUTION]
>
>resourceToUGCStoragePath() 가 반환하는 경로는 *아님* 다음에 적합 [ACL 검사](srp.md#for-access-control-acls).

## ACL에 액세스하기 위한 유틸리티 메서드 {#utility-method-to-access-acls}

ASRP 및 MSRP와 같은 일부 SRP 구현은 ACL 확인을 제공하지 않는 데이터베이스에 커뮤니티 콘텐츠를 저장합니다. 그림자 노드는 ACL을 적용할 수 있는 로컬 저장소 위치를 제공합니다.

SRP API를 사용하면 모든 SRP 옵션이 모든 CRUD 작업 전에 섀도 위치를 동일하게 확인합니다.

ACL을 확인하려면 리소스의 UGC에 적용된 권한을 확인하는 데 적합한 경로를 반환하는 메서드를 사용합니다.

다음은 서블릿에서 resourceToACLPath() 메서드를 사용하는 간단한 예입니다.

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
>resourceToACLPath()에서 반환된 경로는 다음과 같습니다. *아님* 다음에 적합 [UGC 액세스](#utility-method-to-access-acls) 그 자체.

## UGC 관련 스토리지 위치 {#ugc-related-storage-locations}

저장소 위치에 대한 다음 설명은 JSRP 또는 MSRP를 사용하여 개발할 때 도움이 될 수 있습니다. JSRP( )에 대한 것이므로 현재 ASRP에 저장된 UGC에 액세스할 수 있는 UI가 없습니다.[CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)) 및 MSRP(MongoDB 도구)를 참조하십시오.

**구성 요소 위치**

멤버가 게시 환경에서 UGC에 들어갈 때 AEM 사이트의 일부로 구성 요소와 상호 작용합니다.

이러한 구성 요소의 예로는 [주석 구성 요소](http://localhost:4502/content/community-components/en/comments.html) 다음에 존재함 [커뮤니티 구성 요소 안내서](components-guide.md) 사이트. 로컬 저장소의 주석 노드 경로는 다음과 같습니다.

* 구성 요소 경로 = `/content/community-components/en/comments/jcr:content/content/includable/comments`

**그림자 노드 위치**

UGC를 만들면 [그림자 노드](srp.md#about-shadow-nodes-in-jcr) 필요한 ACL이 적용되는 대상. 로컬 리포지토리에 있는 해당 그림자 노드의 경로는 그림자 노드 루트 경로를 구성 요소 경로에 앞에 추가한 결과입니다.

* 루트 경로 = `/content/usergenerated`
* 댓글 그림자 노드 = `/content/usergenerated/content/community-components/en/comments/jcr:content/content/includable/comments`

**UGC 위치**

UGC는 두 위치 중 어느 곳에서도 만들어지지 않으며 를 통해서만 액세스할 수 있습니다. [효용 방법](#utility-method-to-access-ugc) SRP API를 호출합니다.

* 루트 경로 = `/content/usergenerated/asi/srp-choice`
* JSRP에 대한 UGC 노드 = `/content/usergenerated/asi/jcr/content/community-components/en/comments/jcr:content/content/includable/comments/srzd-let_it_be_`

*주의하십시오.*, JSRP의 경우 UGC 노드는 *전용* 입력된 AEM 인스턴스(작성자 또는 게시)에 있어야 합니다. 게시 인스턴스에 입력하면 작성자의 중재 콘솔에서 중재를 수행할 수 없습니다.

## 관련 정보 {#related-information}

* [저장소 리소스 공급자 개요](srp.md) - 소개 및 저장소 사용 개요.
* [SRP를 사용하여 UGC에 액세스](accessing-ugc-with-srp.md) - 코딩 지침
* [SocialUtils 리팩터링](socialutils.md) - 더 이상 사용되지 않는 유틸리티 메서드를 현재 SRP 유틸리티 메서드에 매핑합니다.
