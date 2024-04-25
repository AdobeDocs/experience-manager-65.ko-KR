---
title: AEM Communities의 사용자 및 UGC 관리 서비스
description: API를 사용하여 생성된 컨텐츠사용자 벌크 삭제 및 벌크 내보내기하고 사용자 계정 비활성화합니다.
contentOwner: mgulati
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
docset: aem65
role: Admin
exl-id: 526ef0fa-3f20-4de4-8bc5-f435c60df0d0
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 2%

---

# AEM Communities의 사용자 및 UGC 관리 서비스 {#user-and-ugc-management-service-in-aem-communities}

>[!IMPORTANT]
>
>GDPR은 아래 섹션에서 예로 사용되지만 다루는 세부 정보는 모든 데이터 보호 및 개인 정보 보호 규정에 적용됩니다. GDPR, CCPA 등과 같은.

AEM Communities은 사용자 프로필을 관리하고 UGC(사용자 생성 컨텐츠)를 대량 관리하기 위한 API를 즉시 표시합니다. UserUgcManagement **서비스를 사용하도록**&#x200B;설정하면 권한 있는 사용자(커뮤니티 관리자 및 중재자)가 사용자 프로필을 비활성화하고 특정 사용자에 대해 UGC를 대량 삭제 또는 대량 내보낼 수 있습니다. 또한 이러한 API를 통해 고객 데이터의 제어자와 프로세서는 유럽 연합의 GDPR(일반 데이터 보호 규정) 및 GDPR에서 영감을 얻은 기타 개인 정보 보호 규정을 준수할 수 있습니다.

자세한 내용은 [Adobe 개인 정보 보호 센터의 GDPR 페이지](https://www.adobe.com/privacy/general-data-protection-regulation.html)를 참조하십시오.

>[!NOTE]
>
>를 구성한 경우 [AEM Communities의 Adobe Analytics](/help/communities/analytics.md) 캡처한 사용자 데이터가 Adobe Analytics 서버로 전송됩니다. Adobe Analytics은 사용자 데이터에 액세스, 내보내기 및 삭제하고 GDPR을 준수할 수 있는 API를 제공합니다. 자세한 내용은 [액세스 및 삭제 요청 제출](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/gdpr-submit-access-delete.html).

이러한 API를 사용하려면 `/services/social/ugcmanagement` UserUgcManagement 서비스를 활성화하여 끝점을 만들었습니다. 이 서비스를 활성화하려면 GitHub.com](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/main/bundles/communities-ugc-management-servlet) 에서 사용 가능한 샘플 서블릿](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/main/bundles/communities-ugc-management-servlet)을 [[설치하십시오. 그런 다음 다음과 유사한 http 요청 사용하여 적절한 매개 변수와 함께 커뮤니티 사이트의 게시 인스턴스 끝점을 히트.

`https://localhost:port/services/social/ugcmanagement?user=<authorizable ID>&operation=<getUgc>`. 그러나 UI(사용자 인터페이스)를 빌드 시스템에서 생성된 컨텐츠프로필 및 사용자 관리 사용자 수 있습니다.

이러한 API를 사용하면 다음 기능을 수행할 수 있습니다.

## 사용자 UGC 검색 {#retrieve-the-ugc-of-a-user}

**getUserUgc(ResourceResolver resourceResolver, String 사용자, OutputStream outputStream)** 는 시스템에서 사용자의 모든 UGC를 내보내는 데 도움이 됩니다.

* **사용자**: 승인 가능한 사용자 ID입니다.
* **outputStream**: 결과는 사용자가 생성한 컨텐츠(json 파일)와 첨부 파일(사용자가 업로드한 이미지 또는 비디오 포함)을 포함하는 zip 파일인 출력 스트림으로 반환됩니다.

예를 들어 weston.mccall@dodgit.com 을 승인 가능 ID로 사용하여 커뮤니티 사이트에 로그인하는 Weston McCall이라는 사용자의 UGC를 내보내려면 다음과 유사한 http GET 요청을 보낼 수 있습니다.

`https://localhost:port/services/social/ugcmanagement?user=weston.mccall@dodgit.com&operation=getUgc`

## 사용자의 UGC 삭제 {#delete-the-ugc-of-a-user}

**deleteUserUgc(ResourceResolver resourceResolver, String user)** 는 시스템에서 사용자의 모든 UGC를 삭제하는 데 도움이 됩니다.

* **사용자**: 승인 가능한 사용자 ID입니다.

예를 들어, http-POST 요청를 통해 승인 가능한 ID가 weston.mccall@dodgit.com 있는 사용자의 UGC 삭제하려면 다음 매개 변수를 사용합니다.

* 사용자 = `weston.mccall@dodgit.com`
* 작업 = `deleteUgc`

### Adobe Analytics에서 삭제 UGC {#delete-ugc-from-adobe-analytics}

Adobe Analytics에서 사용자 데이터를 삭제하려면 API가 Adobe Analytics에서 사용자 데이터를 삭제하지 않으므로 GDPR Analytics 작업 과정](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/an-gdpr-workflow.html);를 팔로우[.

AEM Communities에서 사용하는 Adobe Analytics 변수 매핑의 경우 다음 이미지를 참조하십시오.

![Adobe Analytics에 대한 AEM communities 변수 매핑](assets/analytics-communities-mapping.png)

## 사용자 계정 비활성화 {#disable-a-user-account}

**deleteUserAccount(ResourceResolver resourceResolver, String user)** 는 사용자 계정을 비활성화하는 데 도움이 됩니다.

* **사용자**: 사용자의 승인 가능 ID입니다.

>[!NOTE]
>
>사용자를 비활성화하면 사용자가 서버에 가지고 있는 모든 사용자 생성 컨텐츠가 삭제됩니다.

예를 들어 http-POST 요청를 통해 승인 가능한 ID `weston.mccall@dodgit.com` 가 있는 사용자의 프로필을 삭제하려면 다음 매개 변수를 사용합니다.

* 사용자 = `weston.mccall@dodgit.com`
* 작업 = `deleteUser`

>[!NOTE]
>
>deleteUserAccount() API는 시스템에서 사용자 프로필만 비활성화하고 UGC를 제거합니다. 그러나 시스템에서 사용자 프로필을 삭제하려면 CRXDE Lite **:https://[&lt;server>/crx/de](https://localhost:4502/crx/de)로&lt;/server> 이동하여**&#x200B;사용자 노드 찾아 삭제합니다.
