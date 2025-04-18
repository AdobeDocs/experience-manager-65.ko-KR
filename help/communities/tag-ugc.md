---
title: 사용자 생성 컨텐츠 태깅
description: UGC(사용자 생성 컨텐츠) 태깅은 커뮤니티 구성원이 다른 구성원의 컨텐츠 검색을 지원하는 방법입니다
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 1ecb41e5-c959-4380-a5c7-df9fc3a7703a
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 4%

---

# 사용자 생성 컨텐츠 태깅 {#tagging-user-generated-content}

## 개요 {#overview}

UGC(사용자 생성 컨텐츠) 태깅은 커뮤니티 구성원이 다른 구성원의 컨텐츠 검색을 도울 수 있는 방법입니다.

일반적으로 태그는 작성 환경에서 작성자 및 관리자에 의해 적용됩니다. UGC 태그 지정은 게시 환경의 커뮤니티 구성원에 의해 UGC 태그가 적용된다는 점에서 독특합니다.

태그 네임스페이스 및 분류는 두 애플리케이션에서 동일합니다.

## 커뮤니티 기능 {#communities-features}

태깅을 허용하도록 구성할 수 있는 AEM Communities 기능은 다음과 같습니다.

* [블로그](blog-feature.md)
* [달력](calendar.md)
* [파일 라이브러리](file-library.md)
* [포럼](forum.md#configuretheaddedforum)
* [질문과 대답](working-with-qna.md)

## 태그 관리 {#administering-tags}

태그 네임스페이스 및 분류법을 만들고 관리하려면 [태그 관리](../../help/sites-administering/tags.md#tagging-console)를 참조하십시오.

개발자 정보는 [Tag Essentials](tag.md)을(를) 참조하십시오.

적용된 태그를 사용하여 게시된 UGC를 쉽게 검색할 수 있도록 페이지에 소셜 태그 클라우드 구성 요소를 추가하려면 [소셜 태그 클라우드 사용](tagcloud.md)을 참조하십시오.

### 태그 권한 {#tag-permissions}

기본 권한은 게시 환경의 모든 사용자가 태그 네임스페이스를 읽을 수 없도록 설정됩니다.

태그는 게시 환경의 UGC에 적용되므로 커뮤니티 구성원이 적용할 태그를 선택할 수 있으려면 읽기 권한이 활성화되어 있어야 합니다.

[태그 권한 설정](../../help/sites-administering/tags.md#setting-tag-permissions)을 참조하세요.

다음은 관리자가 `Community Engage Members` 그룹의 `/etc/tag/discussions`에 대한 읽기 권한을 적용할 때 CRXDE에 표시되는 방식입니다.

![tag-permissions](assets/tag-permissions.png)
