---
title: 노드 만들기
seo-title: Create Nodes
description: 댓글 시스템 오버레이
seo-description: Overlay the comments system
uuid: 802ae28b-9989-4c2c-b466-ab76a724efd3
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: cd4f53ee-537b-4f10-a64f-474ba2c44576
exl-id: 3d72cbdf-5eb4-477d-aa61-035a846f7dcb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 9%

---

# 노드 만들기 {#create-nodes}

에 필요한 최소 수의 파일을 복사하여 사용자 지정 버전으로 주석 시스템을 오버레이합니다. `/libs` 대상 `/apps` 및 수정 `/apps`.

>[!CAUTION]
>
>/apps 폴더의 내용은 그대로 두고 다시 설치하거나 업그레이드하면 /libs 폴더가 삭제되거나 대체될 수 있으므로 /libs 폴더의 내용은 편집되지 않습니다.

사용 [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) 작성자 인스턴스에서 /libs 폴더에 있는 오버레이된 구성 요소에 대한 경로와 동일한 경로를 /apps 폴더에 만들어 시작합니다.

복제되는 경로는 다음과 같습니다.

* `/libs/social/commons/components/hbs/comments/comment`

경로의 일부 노드는 폴더이고 일부는 구성 요소입니다.

1. 다음으로 이동 [http://localhost:4502/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp)
1. 만들기 `/apps/social` (아직 존재하지 않는 경우)
   * 선택 `/apps` 노드
   * **[!UICONTROL 만들기 > 폴더 ...]**
      * 이름 입력: `social`
1. 선택 `social` 노드
   * **[!UICONTROL 만들기]** > **[!UICONTROL 폴더...]**
      * 이름 입력: `commons`
1. 선택 `commons` 노드
   * **[!UICONTROL 만들기 > 폴더...]**
      * 이름 입력: `components`
1. 선택 `components` 노드
   * **[!UICONTROL 만들기 > 폴더..]**.
      * 이름 입력: `hbs`
1. 선택 `hbs` 노드
   * **[!UICONTROL 만들기]** > **[!UICONTROL 구성 요소 만들기...]**
      * 레이블 입력: `comments`
      * 제목 입력: `Comments`
      * 설명 입력: `List of comments without showing avatars`
      * Super Type: `social/commons/components/comments`
      * 그룹 입력: `Communities`
      * 클릭 **[!UICONTROL 다음]** 종료 시간 **[!UICONTROL 확인]**
1. 선택 `comments` 노드

   * **[!UICONTROL 만들기]** > **[!UICONTROL 구성 요소 만들기...]**

      * 레이블 입력: `comment`
      * 제목 입력: `Comment`
      * 설명 입력: `A comment instance without avatars`
      * Super Type: `social/commons/components/comments/comment`
      * 그룹 입력: `.hidden`
      * 클릭 **[!UICONTROL 다음]** 종료 시간 **[!UICONTROL 확인]**
   * 선택 **[!UICONTROL 모두 저장]**
1. 기본값 삭제 `comments.jsp`
   * 노드 선택 `/apps/social/commons/components/hbs/comments/comments.jsp`
   * **[!UICONTROL 삭제]**&#x200B;를 선택합니다
1. 기본 comment.jsp 삭제
   * 노드 선택 `/apps/social/commons/components/hbs/comments/comment/comment.jsp`
   * **[!UICONTROL 삭제]**&#x200B;를 선택합니다
   * 선택 **[!UICONTROL 모두 저장]**

>[!NOTE]
>
>상속 체인을 유지하기 위해 `Super Type` (속성) `sling:resourceSuperType`오버레이 구성 요소의 )가 와 동일한 값으로 설정되어 있습니다. `Super Type` 오버레이되는 구성 요소의 경우:
>
>* `social/commons/components/comments`
>* `social/commons/components/comments/comment`


오버레이의 자체 `Type`(속성) `sling:resourceType`)는 /apps에 없는 모든 콘텐츠를 /libs에서 검색하도록 상대 자체 참조여야 합니다.
* 이름: `sling:resourceType`
* 유형: `String`
* 값: `social/commons/components/hbs/comments`

1. 녹색 선택 `[+] Add`
   * 이름: `sling:resourceType`
   * 유형: `String`
   * 값: `social/commons/components/hbs/comments/comment`
1. 녹색 선택 `[+] Add`
   * 선택 **[!UICONTROL 모두 저장]**

![노드 만들기](assets/create-nodes.png)
