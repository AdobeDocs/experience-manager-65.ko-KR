---
title: SocialUtils 리팩터링
description: 패키지 com.adobe.cq.social.ugcbase.SocialUtils는 AEM 6.1에서 더 이상 사용되지 않습니다
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 0f731ec6-a12e-4098-a1ec-ee4cd4dc1432
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 1%

---

# SocialUtils 리팩터링 {#socialutils-refactoring}

## SocialUtils 패키지 사용 안 함 {#socialutils-package-deprecated}

패키지 `com.adobe.cq.social.ugcbase.SocialUtils` AEM 6.1에서 더 이상 사용되지 않습니다.

다음 표에는 대신 사용할 메서드가 나열되어 있습니다 `SocialUtils` 메서드를 사용합니다.

## SocialResourceUtility 패키지  {#socialresourceutilities-package}

| com.adobe.cq.social.srp.utilities.api.SocialResourceUtilities의 메서드 |
|---|
| 부울 checkPermission(ResourceResolver, 문자열 경로, 문자열 작업) |  |
| SocialResourceProvider getSocialResourceProvider(리소스 리소스 리소스) |  |
| SocialResourceConfiguration getStorageConfig(리소스 리소스) |  |
| 리소스 getUGCResource(리소스 사용자 리소스) |  |
| 리소스 getUGCResource(Resource userResource, ResourceResolverFactory rrf) | 새 항목 |
| 리소스 getUGCResource(Resource userResource, ResourceResolverFactory rrf, String resourceTypeHint) | 새 항목 |
| 리소스 getUGCResource(리소스 사용자 리소스, 문자열 리소스 유형 힌트) |  |
| boolean hasModeratePermissions(리소스 리소스) |  |
| 문자열 resourceToACLPath(리소스 리소스) |  |
| 문자열 resourceToUGCStoragePath(Resource resource) | 문자열 resourceToUGCPath(리소스 리소스)를 대체합니다. |
| 문자열 UGCoResourcePath(리소스 리소스) |  |
| 문자열 UGCoResourcePath(문자열 ugcPath) | 메서드 시그니처가 변경됨 |
| 문자열 UGCoResourcePath(문자열 ugcPath, ResourceResolver) | 새 항목 |

| 의 메서드 `com.adobe.cq.social.`utilities.resource.api.SocialResourceUtilities |
|---|
| SocialResourceProvider getSocialResourceProvider(리소스 리소스 리소스) | 는 SocialResourceProvider getConfiguredProvider(리소스 리소스)를 대체합니다. |

## SCFUtilities 패키지 {#scfutilities-package}

| 의 메서드 `com.adobe.cq.social.`utilities.scf.api.SCFUtilites |
|---|
| 문자열 getAvatar(UserProperties userProperties) |
| 문자열 getAvatar(UserProperties userProperties, int size) |
| 문자열 getAvatar(UserProperties userProperties, String absoluteDefaultAvatar) |
| 문자열 getAvatar(UserProperties userProperties, String absoluteDefaultAvatar, SocialUtils.AVATAR_SIZE) |
| Page getContainingPage(Resource resource) |
| 문자열 getSocialProfileURL(문자열 사용자 이름, ResourceResolver, 페이지 페이지 페이지) |
| UserProperties getUserProperties(ResourceResolver, String userId) |

## 내부 전용 {#for-internal-use-only}

| 부울 canAddNode(세션 세션, 문자열 경로) |
|---|
| String createUniqueNameHint(문자열 메시지) |
| String createUniqueNameHint(String message, int numRandomChars) |
| 문자열 generateRandomString(int length) |
| SocialResourceConfiguration getDefaultStorageConfig() |
| 페이지 getPage(문자열 경로, ResourceResolver) |
| 문자열 getPagePath(리소스 리소스) |
| String getPagePath(문자열 경로) |
| String getResourceTypeForIncludedResource(Resource 구성 요소, String defaultResourceType, String designPropertyName) |
| String getResourceTypeFromDesign(Resource resource, String styleProperty, String defaultValue) |
| 부울 isResourceOwner(리소스 리소스) |
| 문자열 mapUGCPath(리소스 리소스) |
| 문자열 mapUGCath(문자열 ugcPath, ResourceResolver) |
| 부울 mayPost(ResourceResolver, Resource resource) |
| 문자열 prepareUserGeneratedContent(ResourceResolver, 문자열 경로) |

## 메서드를 더 이상 사용할 수 없음 {#methods-no-longer-available}

| 노드 createNode(ResourceResolver, 문자열 경로, 문자열 nodeType) |
|---|
| 리소스 getResourceAtPath(ResourceResolver, 문자열 경로) |
| 리소스 getResourceAtPath(ResourceResolver, 문자열 경로, 문자열 리소스 유형) |
| 구성 getStorageCloudServiceConfig(리소스 리소스 리소스) |
| TranslationManager getTranslationManager() |
| TranslationSaveQueue getTranslationSaveQueue() |
| 부울 mayAccessUGC(ResourceResolver) |
