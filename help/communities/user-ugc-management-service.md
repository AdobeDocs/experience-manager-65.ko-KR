---
title: AEM Communities의 사용자 및 UGC 관리 서비스
seo-title: AEM Communities의 사용자 및 UGC 관리 서비스
description: API를 사용하여 사용자 생성 콘텐츠를 벌크 삭제 및 일괄 내보내고 사용자 계정을 비활성화할 수 있습니다.
seo-description: API를 사용하여 사용자 생성 콘텐츠를 벌크 삭제 및 일괄 내보내고 사용자 계정을 비활성화할 수 있습니다.
uuid: 91180659-617d-4f6c-9a07-e680770d0d8f
contentOwner: mgulati
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
discoiquuid: d305821d-1371-4e4a-8b28-8eee8fafa43b
docset: aem65
translation-type: tm+mt
source-git-commit: 2bcd098ae901070d5e50cd89d06c854884b4e461

---


# AEM Communities의 사용자 및 UGC 관리 서비스 {#user-and-ugc-management-service-in-aem-communities}

>[!IMPORTANT]
>
>GDPR은 아래 섹션에 소개되어 있지만, 자세한 내용은 모든 데이터 보호 및 개인 정보 보호 규정에 적용됩니다.(예: GDPR, CCPA 등)


AEM Communities는 사용자 프로필을 관리하고 UGC(사용자 생성 콘텐츠)를 일괄 관리하기 위해 즉시 API를 표시합니다. UserUgcManagement **서비스가 활성화되면** 권한 있는 사용자(커뮤니티 관리자 및 중재자)는 사용자 프로필을 비활성화하고 특정 사용자에 대해 UGC를 벌크 삭제 또는 벌크 내보낼 수 있습니다. 또한 이러한 API를 통해 고객 데이터의 관리자 및 프로세서는 유럽 연합의 개인 정보 보호 규정(GDPR) 및 기타 GDPR에 따른 개인 정보 보호 규정을 준수할 수 있습니다.

자세한 내용은 Adobe 개인 정보 [보호 센터에서 GDPR 페이지를 참조하십시오](https://www.adobe.com/privacy/general-data-protection-regulation.html).

>[!NOTE]
>
>AEM Communities [사이트에서 Adobe Analytics를](/help/communities/analytics.md) 구성한 경우 캡처한 사용자 데이터가 Adobe Analytics 서버로 전송됩니다. Adobe Analytics는 사용자 데이터에 액세스, 내보내기 및 삭제와 GDPR을 준수하는 API를 제공합니다. 자세한 내용은 액세스 제출 [및 요청 삭제를 참조하십시오](https://marketing.adobe.com/resources/help/en_US/analytics/gdpr/gdpr_submit_access_delete.html).


이러한 API를 사용하려면 UserUgcManagement 서비스를 활성화하여 `/services/social/ugcmanagement` 종단점을 활성화해야 합니다. 이 서비스를 활성화하려면 GitHub.com에서 사용할 수 있는 [샘플](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-ugc-management-servlet) 서블릿을 [설치합니다](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-ugc-management-servlet). 그런 다음 http 요청을 사용하여 적절한 매개 변수를 사용하여 커뮤니티 사이트의 게시 인스턴스에 대한 끝점을 다음과 같이 히트:

`https://localhost:port/services/social/ugcmanagement?user=<authorizable ID>&operation=<getUgc>`. 그러나 UI(사용자 인터페이스)를 만들어 사용자 프로필 및 사용자 생성 콘텐츠를 시스템에서 관리할 수도 있습니다.

이러한 API를 사용하면 다음 기능을 수행할 수 있습니다.

## 사용자의 UGC 검색 {#retrieve-the-ugc-of-a-user}

**getUserUgc(ResourceResolver resourceResolver, String user, OutputStream outputStream)** 는 시스템에서 사용자의 모든 UGC를 내보내는 데 도움이 됩니다.

* **사용자**:사용자의 승인 가능 ID.
* **outputStream**:결과는 사용자가 생성한 컨텐츠(json 파일)와 첨부 파일(사용자가 업로드한 이미지 또는 비디오 포함)을 포함하는 zip 파일인 출력 스트림으로 반환됩니다.

예를 들어 weston.mccall@dodgit.com을 승인 가능 ID로 사용하여 커뮤니티 사이트에 로그인하는 Weston McCall이라는 사용자의 UGC를 내보내려면 다음과 유사한 http GET 요청을 보낼 수 있습니다.

`https://localhost:port/services/social/ugcmanagement?user=weston.mccall@dodgit.com&operation=getUgc`

## 사용자의 UGC 삭제 {#delete-the-ugc-of-a-user}

**deleteUserUgc(ResourceResolver resourceResolver, String user)** 는 시스템에서 사용자에 대한 모든 UGC를 삭제하는 데 도움이 됩니다.

* **사용자**:사용자의 승인 가능 ID입니다.

예를 들어 권한 부여 ID가 weston.mccall@dodgit.com인 사용자의 UGC를 http-POST 요청을 통해 삭제하려면 다음 매개 변수를 사용하십시오.

* 사용자 = `weston.mccall@dodgit.com`
* 작업 = `deleteUgc`

### Adobe Analytics에서 UGC 삭제 {#delete-ugc-from-adobe-analytics}

Adobe Analytics에서 사용자 데이터를 삭제하려면 GDPR [Analytics 워크플로우를](https://marketing.adobe.com/resources/help/en_US/analytics/gdpr/an_gdpr_workflow.html)따르십시오.as the API does not delete user data from Adobe Analytics.

AEM Communities에서 사용되는 Adobe Analytics 변수 매핑은 다음 이미지를 참조하십시오.

![Adobe Analytics에 대한 AEM 커뮤니티 변수 매핑](assets/analytics-communities-mapping.png)

## 사용자 계정 비활성화 {#disable-a-user-account}

**deleteUserAccount(ResourceResolver resourceResolver, String 사용자)** - 사용자 계정을 비활성화하는 데 도움이 됩니다.

* **사용자**:사용자의 승인 가능 ID입니다.

>[!NOTE]
>
>사용자를 비활성화하면 사용자가 서버에 가지고 있는 모든 사용자 생성 컨텐츠가 삭제됩니다.


예를 들어 http-POST 요청을 `weston.mccall@dodgit.com` 통해 승인 가능 ID가 있는 사용자의 프로필을 삭제하려면 다음 매개 변수를 사용합니다.

* 사용자 = `weston.mccall@dodgit.com`
* 작업 = `deleteUser`

>[!NOTE]
>
>deleteUserAccount() API는 시스템에서 사용자 프로필만 비활성화하고 UGC를 제거합니다. 그러나 시스템에서 사용자 프로필을 삭제하려면 CRXDE Lite로 **이동합니다**.https:// [&lt;server>/crx/de](https://localhost:4502/crx/de), 사용자 노드를 찾아 삭제합니다.


