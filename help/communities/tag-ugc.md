---
title: 사용자 생성 컨텐츠에 태깅
seo-title: Tagging User Generated Content
description: UGC(사용자 생성 컨텐츠)의 태깅은 커뮤니티 구성원이 컨텐츠를 검색하는 데 도움이 되는 방법입니다
seo-description: Tagging of user generated content (UGC) is how community members can help other members search for content
uuid: ce125d7c-6fc1-44c7-9f67-eca6f599d8e3
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 1cc8ce66-2c03-44e4-9ddd-8d6944d85c99
role: Admin
exl-id: 1ecb41e5-c959-4380-a5c7-df9fc3a7703a
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 3%

---

# 사용자 생성 컨텐츠에 태깅 {#tagging-user-generated-content}

## 개요 {#overview}

UGC(사용자 생성 컨텐츠)의 태깅은 커뮤니티 구성원이 컨텐츠를 검색하는 데 도움이 되는 수단입니다.

일반적으로 태그는 작성 환경의 작성자 및 관리자가 적용합니다. UGC 태그는 게시 환경에서 커뮤니티 멤버가 적용하는 경우 UGC 태그가 고유합니다.

태그 네임스페이스와 분류법은 두 애플리케이션 모두에 대해 동일합니다.

## 커뮤니티 기능 {#communities-features}

태깅을 허용하도록 구성할 수 있는 AEM Communities 기능은 다음과 같습니다.

* [블로그](blog-feature.md)
* [달력](calendar.md)
* [파일 라이브러리](file-library.md)
* [포럼](forum.md#configuretheaddedforum)
* [질문과 대답](working-with-qna.md)

## 태그 관리 {#administering-tags}

자세한 내용은 [태그 관리](../../help/sites-administering/tags.md#tagging-console) 태그 네임스페이스 및 분류 체계를 만들고 관리하기 위해

자세한 내용은 [태그 핵심 사항](tag.md) 개발자 정보.

자세한 내용은 [Social Tag Cloud 사용](tagcloud.md) 적용된 태그를 사용하여 게시된 UGC를 쉽게 검색할 수 있도록 페이지에 소셜 태그 클라우드 구성 요소를 추가하는 방법을 설명합니다.

### 태그 권한 {#tag-permissions}

기본 권한은 게시 환경의 모든 사용자가 태그 네임스페이스를 읽을 수 있도록 설정되어 있습니다.

태그는 게시 환경에서 UGC에 적용되므로 커뮤니티 구성원이 적용할 태그를 선택할 수 있도록 읽기 권한을 활성화해야 합니다.

자세한 내용은 [태그 권한 설정](../../help/sites-administering/tags.md#setting-tag-permissions).

다음은 관리자가 읽기 권한을 적용할 때 CRXDE에 표시되는 방식입니다 `/etc/tag/discussions` 그룹 `Community Engage Members`.

![태그 권한](assets/tag-permissions.png)
