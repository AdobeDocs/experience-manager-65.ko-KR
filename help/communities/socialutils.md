---
title: SocialUtils 리팩터링
seo-title: SocialUtils 리팩터링
description: 패키지 com.adobe.cq.social.ugcbase.SocialUtils는 AEM 6.1에서 더 이상 사용되지 않습니다
seo-description: 패키지 com.adobe.cq.social.ugcbase.SocialUtils는 AEM 6.1에서 더 이상 사용되지 않습니다
uuid: 54a0d98e-5ead-4c12-850f-8252ea9b3263
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 4ade0d6b-041e-4a2f-98f8-3b8fcae0fb29
exl-id: 0f731ec6-a12e-4098-a1ec-ee4cd4dc1432
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---

# SocialUtils 리팩터링 {#socialutils-refactoring}

## SocialUtils 패키지가 사용되지 않음 {#socialutils-package-deprecated}

패키지 `com.adobe.cq.social.ugcbase.SocialUtils`은 AEM 6.1에서 더 이상 사용되지 않습니다.

다음 표에는 `SocialUtils` 메서드 대신 사용할 메서드가 나와 있습니다.

## SocialResourceUtilities 패키지 {#socialresourceutilities-package}

| com.adobe.cq.social.srp.utilities.api.SocialResourceUtilities의 메서드 |
|---|
| 부울 checkPermission(ResourceResolver, String path, String action) |  |
| SocialResourceProvider getSocialResourceProvider(리소스) |  |
| SocialResourceConfiguration getStorageConfig(리소스) |  |
| 리소스 getUGCRessource(Resource userResource) |  |
| 리소스 getUGCRessource(Resource userResource, ResourceResolverFactory rrrf) | 새 항목 |
| 리소스 getUGCRessource(Resource userResource, ResourceResolverFactory rrrrf, String resourceTypeHint) | 새 항목 |
| 리소스 getUGCRessource(Resource userResource, String resourceTypeHint) |  |
| boolean hasModeratePermissions(리소스 리소스) |  |
| String resourceToACLPath(리소스) |  |
| String resourceToUGCtoragePath(리소스) | string resourceToUGCPath(리소스) 대체 |
| 문자열 UCToResourcePath(리소스) |  |
| 문자열 UCToResourcePath(String ugcPath) | 메서드 서명이 변경되었습니다. |
| String UGCoResourcePath(String ugcPath, ResourceResolver) | 새 항목 |

| `com.adobe.cq.social.`utilities.resource.api.SocialResourceUtilities의 메서드 |
|---|
| SocialResourceProvider getSocialResourceProvider(리소스) | 는 SocialResourceProvider getConfiguredProvider(리소스) 대체 |

## SCFUtifications 패키지 {#scfutilities-package}

| `com.adobe.cq.social.`utilities.scf.api.SCFUtilites의 메서드 |
|---|
| String getAvatar(UserProperties userProperties) |
| String getAvatar(UserProperties userProperties, int size) |
| String getAvatar(UserProperties userProperties, String absoluteDefaultAvatar) |
| String getAvatar(UserProperties userProperties, String absoluteDefaultAvatar, SocialUtils.AVATAR_SIZE) |
| Page getContainingPage(리소스) |
| String getSocialProfileURL(String 사용자 이름, ResourceResolver, Page) |
| UserProperties getUserProperties(ResourceResolver, String userId) |

## 내부용 {#for-internal-use-only}

| 부울 canAddNode(세션, 문자열 경로) |
|---|
| 문자열 createUniqueNameHint(문자열 메시지) |
| 문자열 createUniqueNameHint(문자열 메시지, int numRandomChars) |
| 문자열 generateRandomString(int length) |
| SocialResourceConfiguration getDefaultStorageConfig() |
| Page getPage(문자열 경로, ResourceResolver) |
| String getPagePath(리소스) |
| String getPagePath(문자열 경로) |
| String getResourceTypeForIncludedResource(리소스 구성 요소, String defaultResourceType, String designPropertyName) |
| String getResourceTypeFromDesign(Resource, String styleProperty, String defaultValue) |
| 부울 isResourceOwner(Resource) |
| String mapUGCPath(리소스) |
| String mapUGCPath(String ugcPath, ResourceResolver) |
| boolean mayPost(ResourceResolver, Resource resource) |
| String prepareUserGeneratedContent(ResourceResolver, String path) |

## 더 이상 메서드를 사용할 수 없습니다. {#methods-no-longer-available}

| 노드 createNode(ResourceResolver, String path, String nodeType) |
|---|
| 리소스 getResourceAtPath(ResourceResolver, String path) |
| 리소스 getResourceAtPath(ResourceResolver, String path, String resourceType) |
| 구성 getStorageCloudServiceConfig(리소스) |
| TranslationManager getTranslationManager() |
| TranslationSaveQueue getTranslationSaveQueue() |
| boolean mayAccessUGC(ResourceResolver) |
