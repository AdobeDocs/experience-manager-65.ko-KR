---
title: AEM Communities의 사용자 및 UGC 관리 서비스
description: API를 사용하여 사용자 생성 콘텐츠를 대량 삭제 및 대량 내보내고 사용자 계정을 비활성화합니다.
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
>아래 섹션에서는 GDPR이 예로 사용되지만, 포함된 세부 사항은 GDPR, CCPA 등과 같은 모든 데이터 보호 및 개인 정보 보호 규정에 적용됩니다.

AEM Communities은 사용자 프로필을 관리하고 UGC(사용자 생성 컨텐츠)를 대량 관리하기 위한 API를 즉시 표시합니다. 사용하도록 설정하면 **UserUgcManagement** 서비스를 통해 권한이 있는 사용자(커뮤니티 관리자 및 중재자)가 사용자 프로필을 사용하지 않도록 설정하고, 특정 사용자에 대한 UGC를 대량 삭제하거나 일괄 내보낼 수 있습니다. 또한 이러한 API를 통해 고객 데이터의 제어자와 프로세서는 유럽 연합의 GDPR(일반 데이터 보호 규정) 및 GDPR에서 영감을 얻은 기타 개인 정보 보호 규정을 준수할 수 있습니다.

자세한 내용은 [Adobe 개인 정보 보호 센터의 GDPR 페이지](https://www.adobe.com/privacy/general-data-protection-regulation.html)를 참조하십시오.

>[!NOTE]
>
>AEM Communities에서 [Adobe Analytics](/help/communities/analytics.md) 사이트를 구성한 경우 캡처한 사용자 데이터가 Adobe Analytics 서버로 전송됩니다. Adobe Analytics은 사용자 데이터에 액세스, 내보내기 및 삭제하고 GDPR을 준수할 수 있는 API를 제공합니다. 자세한 내용은 [액세스 및 삭제 요청 제출](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/gdpr-submit-access-delete.html?lang=ko)을 참조하십시오.

이러한 API를 사용하려면 UserUgcManagement 서비스를 활성화하여 `/services/social/ugcmanagement` 끝점을 사용하도록 설정해야 합니다. 이 서비스를 활성화하려면 [GitHub.com](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/main/bundles/communities-ugc-management-servlet)에서 사용할 수 있는 [샘플 서블릿](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/main/bundles/communities-ugc-management-servlet)을(를) 설치하십시오. 그런 다음 다음과 유사한 http 요청을 사용하여 적절한 매개 변수로 커뮤니티 사이트의 게시 인스턴스에 대한 끝점을 히트합니다.

`https://localhost:port/services/social/ugcmanagement?user=<authorizable ID>&operation=<getUgc>`. 그러나 UI(사용자 인터페이스)를 빌드하여 시스템의 사용자 프로필 및 사용자 생성 콘텐츠를 관리할 수도 있습니다.

이러한 API를 사용하면 다음 기능을 수행할 수 있습니다.

## 사용자의 UGC 검색 {#retrieve-the-ugc-of-a-user}

**getUserUgc(ResourceResolver resourceResolver, String user, OutputStream outputStream)**&#x200B;은(는) 시스템에서 사용자의 모든 UGC를 내보내는 데 도움이 됩니다.

* **user**: 사용자의 승인 가능 ID입니다.
* **outputStream**: 결과가 출력 스트림으로 반환됩니다. 이 파일은 사용자가 생성한 콘텐츠(json 파일)와 첨부 파일(사용자가 업로드한 이미지 또는 비디오 포함)이 포함된 zip 파일입니다.

예를 들어 weston.mccall@dodgit.com 을 승인 가능 ID로 사용하여 커뮤니티 사이트에 로그인하는 Weston McCall이라는 사용자의 UGC를 내보내려면 다음과 유사한 http GET 요청을 보낼 수 있습니다.

`https://localhost:port/services/social/ugcmanagement?user=weston.mccall@dodgit.com&operation=getUgc`

## 사용자의 UGC 삭제 {#delete-the-ugc-of-a-user}

**deleteUserUgc(ResourceResolver resourceResolver, String user)**&#x200B;은(는) 시스템에서 사용자에 대한 모든 UGC를 삭제하는 데 도움이 됩니다.

* **user**: 사용자의 승인 가능 ID입니다.

예를 들어 http POST 요청을 통해 승인 가능한 ID weston.mccall@dodgit.com이 있는 사용자의 UGC를 삭제하려면 다음 매개 변수를 사용하십시오.

* 사용자 = `weston.mccall@dodgit.com`
* 작업 = `deleteUgc`

### Adobe Analytics에서 UGC 삭제 {#delete-ugc-from-adobe-analytics}

API가 Adobe Analytics에서 사용자 데이터를 삭제하지 않으므로 Adobe Analytics에서 사용자 데이터를 삭제하려면 [GDPR Analytics 워크플로](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/an-gdpr-workflow.html?lang=ko)를 따르십시오.

AEM Communities에서 사용하는 Adobe Analytics 변수 매핑의 경우 다음 이미지를 참조하십시오.

Adobe Analytics에 대한 ![AEM 커뮤니티 변수 매핑](assets/analytics-communities-mapping.png)

## 사용자 계정 비활성화 {#disable-a-user-account}

**deleteUserAccount(ResourceResolver resourceResolver, String user)**&#x200B;이(가) 사용자 계정을 사용하지 않도록 설정하는 데 도움이 됩니다.

* **user**: 사용자의 승인 가능 ID입니다.

>[!NOTE]
>
>사용자를 비활성화하면 사용자가 서버에서 보유하는 모든 사용자 생성 컨텐츠가 삭제됩니다.

예를 들어 http POST 요청을 통해 승인 가능한 ID가 `weston.mccall@dodgit.com`인 사용자의 프로필을 삭제하려면 다음 매개 변수를 사용하십시오.

* 사용자 = `weston.mccall@dodgit.com`
* 작업 = `deleteUser`

>[!NOTE]
>
>deleteUserAccount() API는 시스템의 사용자 프로필만 비활성화하고 UGC를 제거합니다. 그러나 시스템에서 사용자 프로필을 삭제하려면 **CRXDE Lite**: [https://&lt;서버>/crx/de](https://localhost:4502/crx/de)(으)로 이동하여 사용자 노드를 찾아 삭제합니다.
