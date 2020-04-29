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
source-git-commit: 3296db289b2e2f4ca0d1981597ada6ca1310bd46

---


# SocialUtils 리팩토링 {#socialutils-refactoring}

## SocialUtils 패키지 가치 하락 {#socialutils-package-deprecated}

패키지는 `com.adobe.cq.social.ugcbase.SocialUtils` AEM 6.1에서 더 이상 사용되지 않습니다.

다음 표에는 SocialUtils 메서드 대신 사용할 메서드가 나와 있습니다.

## SocialResourceUtilities 패키지 {#socialresourceutilities-package}

| com.adobe.cq.sosocial.srp.utilities.api.SocialResourceUtilities의 메서드 |
|---|
| Boolean checkPermission(ResourceResolver, String path, String action) |  |
| SocialResourceProvider getSocialResourceProvider(리소스) |  |
| SocialResourceConfiguration getStorageConfig(리소스 리소스) |  |
| 리소스 getUGCResource(Resource userResource) |  |
| 리소스 getUGCResource(Resource userResource, ResourceResolverFactory rf) | 새 항목 |
| 리소스 getUGCResource(Resource userResource, ResourceResolverFactory rf, String resourceTypeHint) | 새 항목 |
| 리소스 getUGCResource(리소스 사용자 리소스, 문자열 리소스 유형 힌트) |  |
| boolean hasModeratePermissions(리소스 리소스) |  |
| String resourceToACLPath(리소스) |  |
| String resourceToUGCStoragePath(리소스) | string resourceToUGCPath(리소스 리소스) 대체 |
| 문자열 UGCToResourcePath(리소스) |  |
| String UGCToResourcePath(String ugcPath) | 메서드 서명이 변경되었습니다. |
| String UGCToResourcePath(String ugcPath, ResourceResolver) | 새 항목 |

| utilities.resource.api.SocialResourceUtilities의 `com.adobe.cq.social.`메서드 |
|---|
| SocialResourceProvider getSocialResourceProvider(리소스) | socialResourceProvider getConfiguredProvider(리소스 리소스) 대체 |

## SCFUtiilities 패키지 {#scfutilities-package}

| utilities.scf.api. `com.adobe.cq.social.`SCFUtilites의 메서드 |
|---|
| String getAvatar(UserProperties userProperties) |
| String getAvatar(UserProperties userProperties, int size) |
| String getAvatar(UserProperties userProperties, String absoluteDefaultAvatar) |
| String getAvatar(UserProperties userProperties, String absoluteDefaultAvatar, SocialUtils.AVATAR_SIZE) |
| 페이지 getContainingPage(리소스 리소스) |
| String getSocialProfileURL(문자열 사용자 이름, ResourceResolver 해결 프로그램, 페이지 페이지) |
| UserProperties getUserProperties(ResourceResolver, String userId) |

## For Internal Use Only {#for-internal-use-only}

| boolean canAddNode(세션 세션, 문자열 경로) |
|---|
| 문자열 createUniqueNameHint(문자열 메시지) |
| 문자열 createUniqueNameHint(문자열 메시지, int numRandomChars) |
| 문자열 generateRandomString(int length) |
| SocialResourceConfiguration getDefaultStorageConfig() |
| 페이지 getPage(문자열 경로, 리소스 해결 프로그램) |
| String getPagePath(리소스 리소스) |
| String getPagePath(문자열 경로) |
| String getResourceTypeForIncludedResource(Resource 구성 요소, String defaultResourceType, String designPropertyName) |
| String getResourceTypeFromDesign(리소스, 문자열 styleProperty, 문자열 defaultValue) |
| boolean isResourceOwner(리소스 리소스) |
| 문자열 mapUGCPath(리소스) |
| String mapUGCPath(String ugcPath, ResourceResolver) |
| boolean mayPost(ResourceResolver, Resource 리소스) |
| String prepareUserGeneratedContent(ResourceResolver, String 경로) |

## 더 이상 사용할 수 없는 메서드 {#methods-no-longer-available}

| 노드 createNode(ResourceResolver, String path, String nodeType) |
|---|
| 리소스 getResourceAtPath(ResourceResolver, String 경로) |
| Resource getResourceAtPath(ResourceResolver, String path, String resourceType) |
| 구성 getStorageCloudServiceConfig(리소스 리소스) |
| TranslationManager getTranslationManager() |
| TranslationSaveQueue getTranslationSaveQueue() |
| boolean mayAccessUGC(ResourceResolver) |

