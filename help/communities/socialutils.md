---
title: SocialUtils 리팩토링
seo-title: SocialUtils 리팩토링
description: com.adobe.cq.sosocial.ugcbase.SocialUtils 패키지는 AEM 6.1에서 더 이상 사용되지 않습니다.
seo-description: com.adobe.cq.sosocial.ugcbase.SocialUtils 패키지는 AEM 6.1에서 더 이상 사용되지 않습니다.
uuid: 54a0d98e-5ead-4c12-850f-8252ea9b3263
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 4ade0d6b-041e-4a2f-98f8-3b8fcae0fb29
translation-type: tm+mt
source-git-commit: 1429a099288f038510cb0a194fb55632297ef371
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---


# SocialUtils 리팩토링 {#socialutils-refactoring}

## SocialUtils 패키지 가치 하락 {#socialutils-package-deprecated}

패키지는 AEM 6.1에서 더 이상 사용되지 `com.adobe.cq.social.ugcbase.SocialUtils` 않습니다.

다음 표에는 메서드 대신 사용할 메서드가 `SocialUtils` 나와 있습니다.

## SocialResourceUtilities 패키지  {#socialresourceutilities-package}

| com.adobe.cq.sosocial.srp.utilities.api.SocialResourceUtilities의 메서드 |
|---|
| Boolean checkPermission(ResourceResolver, String path, String action) |  |
| SocialResourceProvider getSocialResourceProvider(리소스) |  |
| SocialResourceConfiguration getStorageConfig(리소스) |  |
| 리소스 getUGCResource(Resource userResource) |  |
| 리소스 getUGCResource(Resource userResource, ResourceResolverFactory rrf) | 새 항목 |
| 리소스 getUGCResource(Resource userResource, ResourceResolverFactory rrf, String resourceTypeHint) | 새 항목 |
| 리소스 getUGCResource(Resource userResource, String resourceTypeHint) |  |
| boolean hasModeratePermissions(리소스) |  |
| 문자열 resourceToACLPath(리소스) |  |
| 문자열 resourceToUGCtoragePath(리소스) | 문자열 resourceToUGCPath(리소스 리소스) 대체 |
| 문자열 UGCoResourcePath(리소스) |  |
| 문자열 UGCoResourcePath(문자열 ugcPath) | 메서드 서명이 변경되었습니다. |
| 문자열 UGCoResourcePath(문자열 ugcPath, ResourceResolver) | 새 항목 |

| utilities.resource.api.SocialResourceUtilities의 `com.adobe.cq.social.`메서드 |
|---|
| SocialResourceProvider getSocialResourceProvider(리소스) | SocialResourceProvider getConfiguredProvider(리소스 리소스) 대체 |

## SCFUtiilities 패키지 {#scfutilities-package}

| utilities.scf.api. `com.adobe.cq.social.`SCFUtilites의 메서드 |
|---|
| 문자열 getAvatar(UserProperties userProperties) |
| String getAvatar(UserProperties userProperties, int size) |
| String getAvatar(UserProperties userProperties, String absoluteDefaultAvatar) |
| String getAvatar(UserProperties userProperties, String absoluteDefaultAvatar, SocialUtils.AVATAR_SIZE) |
| 페이지 getContainingPage(리소스) |
| 문자열 getSocialProfileURL(문자열 사용자 이름, 리소스 확인자, 페이지 페이지) |
| UserProperties getUserProperties(ResourceResolver, String userId) |

## For Internal Use Only {#for-internal-use-only}

| boolean canAddNode(세션, 문자열 경로) |
|---|
| 문자열 createUniqueNameHint(문자열 메시지) |
| 문자열 createUniqueNameHint(문자열 메시지, int numRandomChars) |
| 문자열 generateRandomString(int length) |
| SocialResourceConfiguration getDefaultStorageConfig() |
| 페이지 getPage(문자열 경로, 리소스 확인자) |
| 문자열 getPagePath(리소스) |
| String getPagePath(문자열 경로) |
| String getResourceTypeForIncludedResource(리소스 구성 요소, 문자열 defaultResourceType, String designPropertyName) |
| String getResourceTypeFromDesign(리소스 리소스, 문자열 styleProperty, 문자열 defaultValue) |
| boolean isResourceOwner(리소스) |
| 문자열 mapUGCPath(리소스) |
| 문자열 mapUGCPath(문자열 ugcPath, ResourceResolver) |
| boolean mayPost(ResourceResolver, Resource resource resource) |
| 문자열 prepareUserGeneratedContent(ResourceResolver, String path) |

## 메서드를 더 이상 사용할 수 없음 {#methods-no-longer-available}

| 노드 createNode(ResourceResolver, String path, String nodeType) |
|---|
| 리소스 getResourceAtPath(ResourceResolver, 문자열 경로) |
| 리소스 getResourceAtPath(ResourceResolver, 문자열 경로, 문자열 resourceType) |
| 구성 getStorageCloudServiceConfig(리소스) |
| TranslationManager getTranslationManager() |
| TranslationSaveQueue getTranslationSaveQueue() |
| boolean mayAccessUGC(ResourceResolver) |

