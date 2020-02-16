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
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# SRP 및 UGC Essentials {#srp-and-ugc-essentials}

## 소개 {#introduction}

SRP(Storage Resource Provider) 및 UGC(User-Generated Content)와의 관계에 익숙하지 않은 경우 [Community Content Storage](working-with-srp.md) and [Storage Resource Provider Overview를 참조하십시오](srp.md).

설명서의 이 섹션에서는 SRP 및 UGC에 대한 몇 가지 필수 정보를 제공합니다.

## StorageResourceProvider API {#storageresourceprovider-api}

SocialResourceProvider API(SRP API)는 다양한 Sling 리소스 공급자 API의 확장입니다. 여기에는 페이지 매김 및 원자 증분에 대한 지원이 포함됩니다(총계 및 점수 매기기에 유용함).

SCF 구성 요소에는 날짜, 도움말, 투표 수 등을 기준으로 정렬해야 하므로 쿼리가 필요합니다. 모든 SRP 옵션에는 버킷에 의존하지 않는 유연한 쿼리 메커니즘이 있습니다.

SRP 스토리지 위치에는 구성 요소 경로가 통합되어 있습니다. 루트 경로는 ASRP, MSRP 또는 JSRP와 같이 선택한 SRP 옵션에 따라 다르므로 SRP API는 항상 UGC에 액세스하는 데 사용해야 합니다.

SRP API 파섹 새 릴리스로 업그레이드할 때 향후 내부 구현에 대한 개선 사항의 혜택은 누락되므로 사용자 지정 구현을 가볍게 수행해서는 안 됩니다.

SRP API를 사용하는 방법은 SocialResourceUtilities 패키지에 있는 유틸리티와 같이 제공된 유틸리티를 통해 제공됩니다.

AEM 6.0 이전 버전에서 업그레이드할 때 오픈 소스 도구를 사용할 수 있는 모든 SRP에 대해 UGC를 마이그레이션해야 합니다. See [Upgrading to AEM Communities 6.3](upgrade.md).

>[!NOTE]
>
>이전에는 UGC에 액세스하기 위한 유틸리티가 더 이상 존재하지 않는 SocialUtils 패키지에서 발견되었습니다.
>
>대체 유틸리티에 대해서는 SocialUtils [리팩토링을 참조하십시오](socialutils.md).

## UGC에 액세스하는 유틸리티 메서드 {#utility-method-to-access-ugc}

UGC에 액세스하려면 SRP에서 UGC에 액세스하는 데 적합한 경로를 반환하는 SocialResourceUtilities 패키지의 메서드를 사용하고 SocialUtils 패키지에 있는 더 이상 사용되지 않는 메서드를 대체합니다.

다음은 servlet에서 resourceToUGCStoragePath() 메서드를 사용하는 간단한 예입니다.

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

다른 SocialUtils 교체에 대해서는 SocialUtils [리팩토링을 참조하십시오](socialutils.md).

코딩 지침은 SRP를 [사용하여 UGC 액세스를 참조하십시오](accessing-ugc-with-srp.md).

>[!CAUTION]
>
>resourceToUGCStoragePath() 반환 경로는 *ACL 확인에 [적합하지 않습니다](srp.md#for-access-control-acls).

## ACL에 액세스하는 유틸리티 메서드 {#utility-method-to-access-acls}

ASRP 및 MSRP와 같은 일부 SRP 구현은 ACL 확인을 제공하지 않는 데이터베이스에 커뮤니티 컨텐츠를 저장합니다. 섀도 노드는 로컬 리포지토리에서 ACL을 적용할 수 있는 위치를 제공합니다.

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
>resourceToACLPath()가 반환하는 경로는 *UGC 자체에 [액세스하는 데 적합하지 않습니다](#utility-method-to-access-acls) .

## UGC 관련 스토리지 위치 {#ugc-related-storage-locations}

JSRP 또는 MSRP로 개발할 때 스토리지 위치에 대한 다음 설명은 도움이 될 수 있습니다. JSRP(CRXDE Lite) 및 MSRP(MongoDB 도구)에 대한 UGC에 액세스할[수](../../help/sites-developing/developing-with-crxde-lite.md)있는 UI가 현재 없습니다.

**구성 요소 위치**

회원이 게시 환경에서 UGC에 입장하면 AEM 사이트의 일부로 구성 요소와 상호 작용합니다.

이러한 구성 요소의 예는 커뮤니티 구성 요소 안내서 [사이트에 있는 주석 구성](http://localhost:4502/content/community-components/en/comments.html) [](components-guide.md) 요소입니다. 로컬 저장소의 주석 노드에 대한 경로는 다음과 같습니다.

* 구성 요소 경로 = */content/community-components/en/comments/jcr:content/content/includable/comments*

**그림자 노드 위치**

또한 UGC를 만들면 필요한 ACL이 적용되는 [그림자 노드가](srp.md#about-shadow-nodes-in-jcr) 만들어집니다. 로컬 저장소의 해당 그림자 노드에 대한 경로는 구성 요소 경로에 대한 섀도 노드 루트 경로를 미리 설정한 결과입니다.

* 루트 경로 = /content/usergenerated
* 주석 그림자 노드 = /content/usergenerated/content/community-components/en/comments/jcr:content/content/includable/comments

**UGC 위치**

UGC는 해당 위치 모두에서 생성되며 SRP API를 호출하는 [유틸리티 방법을](#utility-method-to-access-ugc) 사용해야만 합니다.

* 루트 경로 = /content/usergenerated/asi/srp-choice
* JSRP용 UGC 노드 = /content/usergenerated/asi/jcr/content/community-components/en/comments/jcr:content/includable/comments/srzd-let_it_be_

*JSRP의 경우* UGC 노드는 *AEM 인스턴스(작성자 또는 게시)에만* 표시됩니다. 게시 인스턴스에 입력하는 경우 작성자의 중재 콘솔에서 중재가 가능하지 않습니다.

## 관련 정보 {#related-information}

* [스토리지 리소스 공급자 개요](srp.md) - 소개 및 저장소 사용 개요
* [SRP를 사용하여 UGC](accessing-ugc-with-srp.md) 액세스 - 코딩 지침
* [SocialUtils 리팩토링](socialutils.md) - 사용되지 않는 유틸리티 메서드를 현재 SRP 유틸리티 메서드에 매핑

