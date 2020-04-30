---
title: 사용자 생성 컨텐츠 태그 지정
seo-title: 사용자 생성 컨텐츠 태그 지정
description: UGC(사용자 생성 콘텐츠)의 태깅은 커뮤니티 구성원이 다른 구성원이 컨텐츠를 검색하는 데 도움이 되는 방법입니다
seo-description: UGC(사용자 생성 콘텐츠)의 태깅은 커뮤니티 구성원이 다른 구성원이 컨텐츠를 검색하는 데 도움이 되는 방법입니다
uuid: ce125d7c-6fc1-44c7-9f67-eca6f599d8e3
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 1cc8ce66-2c03-44e4-9ddd-8d6944d85c99
translation-type: tm+mt
source-git-commit: 77d00c1d6e94b257aa0533ca88b5f9a12dba0054

---


# 사용자 생성 컨텐츠 태그 지정 {#tagging-user-generated-content}

## 개요 {#overview}

UGC(사용자 생성 콘텐츠)에 태그를 지정하는 것은 커뮤니티 구성원이 다른 구성원이 컨텐츠를 검색하는 데 도움이 되는 방법입니다.

일반적으로 태그는 작성 환경의 작성자 및 관리자가 적용합니다. Tagging UGC는 게시 환경의 커뮤니티 구성원이 UGC 태그를 적용할 때 고유합니다.

태그 네임스페이스와 택소노미는 두 애플리케이션 모두에 대해 동일합니다.

## 커뮤니티 기능 {#communities-features}

태그 지정을 허용하도록 구성할 수 있는 AEM Communities 기능은 다음과 같습니다.

* [블로그](blog-feature.md)
* [달력](calendar.md)
* [파일 라이브러리](file-library.md)
* [포럼](forum.md#configuretheaddedforum)
* [질문과 대답](working-with-qna.md)

## 태그 관리 {#administering-tags}

태그 [네임스페이스](../../help/sites-administering/tags.md#tagging-console) 및 택소노미를 만들고 관리하기 위한 태그 관리를 참조하십시오.

개발자 [정보는 태그](tag.md) 필수품을 참조하십시오.

Social [Tag](tagcloud.md) Cloud 구성 요소를 페이지에 추가하려면 적용된 태그를 사용하여 게시된 UGC를 쉽게 검색할 수 있도록 Social Tag Cloud 사용을 참조하십시오.

### 태그 권한 {#tag-permissions}

기본 권한은 게시 환경의 모든 사람이 태그 네임스페이스를 읽을 수 없도록 설정합니다.

태그가 게시 환경에서 UGC에 적용되므로 커뮤니티 구성원이 적용할 태그를 선택할 수 있도록 읽기 권한을 활성화해야 합니다.

태그 [권한 설정을 참조하십시오](../../help/sites-administering/tags.md#setting-tag-permissions).

다음은 관리자가 그룹에 대한 읽기 권한을 적용할 때 CRXDE에 표시되는 `/etc/tag/discussions` `Community Engage Members`방식입니다.

![chlimage_1-74](assets/chlimage_1-74.png)

