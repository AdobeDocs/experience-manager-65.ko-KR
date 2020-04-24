---
title: 노드 만들기
seo-title: 노드 만들기
description: 주석 시스템 오버레이
seo-description: 주석 시스템 오버레이
uuid: 802ae28b-9989-4c2c-b466-ab76a724efd3
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: cd4f53ee-537b-4f10-a64f-474ba2c44576
translation-type: tm+mt
source-git-commit: 48afa2146d0dcbab4beaa1044645c269b49fd7ff

---


# 노드 만들기 {#create-nodes}

필요한 최소한의 파일 수를 복사하여 에서 수정하여 주석 시스템을 사용자 정의 `/libs` 버전으로 `/apps` 오버레이합니다 `/apps`.

>[!CAUTION]
>
>다시 설치하거나 업그레이드하면 /apps 폴더의 내용이 그대로 유지되지만 /libs 폴더를 삭제하거나 대체할 수 있으므로 /libs 폴더의 내용은 편집되지 않습니다.


작성자 [인스턴스에서 CRXDE](../../help/sites-developing/developing-with-crxde-lite.md) Lite를 사용하면 먼저 /apps 폴더에 /libs 폴더의 오버레이된 구성 요소 경로와 동일한 경로를 만듭니다.

복제할 경로는 다음과 같습니다.

* `/libs/social/commons/components/hbs/comments/comment`

경로에 있는 일부 노드는 폴더이고 일부는 구성 요소입니다.

1. http://localhost:4502/crx/de/index.jsp으로 [이동](http://localhost:4502/crx/de/index.jsp)
1. 만들기 `/apps/social` (없는 경우)
   * 노드 `/apps` 선택
   * **[!UICONTROL 만들기 > 폴더 ...]**
      * 이름 입력: `social`
1. 노드 `social` 선택
   * **[!UICONTROL 만들기]** > **[!UICONTROL 폴더...]**
      * 이름 입력: `commons`
1. 노드 `commons` 선택
   * **[!UICONTROL 만들기 > 폴더...]**
      * 이름 입력: `components`
1. 노드 `components` 선택
   * **[!UICONTROL 만들기 > 폴더..]**.
      * 이름 입력: `hbs`
1. 노드 `hbs` 선택
   * **[!UICONTROL 만들기]** > **[!UICONTROL 구성 요소 만들기...]**
      * 레이블 입력: `comments`
      * Enter Title: `Comments`
      * Enter Description: `List of comments without showing avatars`
      * Super Type: `social/commons/components/comments`
      * 그룹 입력: `Communities`
      * [ **[!UICONTROL 확인]** ]을 클릭할 때까지 **[!UICONTROL 다음을 클릭합니다]**
1. 노드 `comments` 선택

   * **[!UICONTROL 만들기 > 구성 요소 만들기...]**

      * 레이블 입력: `comment`
      * Enter Title: `Comment`
      * Enter Description: `A comment instance without avatars`
      * Super Type: `social/commons/components/comments/comment`
      * 그룹 입력: `.hidden`
      * [ **[!UICONTROL 확인]** ]을 클릭할 때까지 **[!UICONTROL 다음을 클릭합니다]**
   * 모두 **[!UICONTROL 저장을 선택합니다.]**
1. 기본값 삭제 `comments.jsp`
   * 노드 선택 `/apps/social/commons/components/hbs/comments/comments.jsp`
   * 삭제 **[!UICONTROL 선택]**
1. 기본 comment.jsp 삭제
   * select node `/apps/social/commons/components/hbs/comments/comment/comment.jsp`
   * 삭제 **[!UICONTROL 선택]**
   * 모두 **[!UICONTROL 저장을 선택합니다.]**

>[!NOTE]
>
>상속 체인을 보존하기 위해 오버레이 구성 요소의 `Super Type` (속성 `sling:resourceSuperType`)가 겹쳐지는 구성 요소의 `Super Type` 값과 같은 값으로 설정됩니다. 이 경우:
>
>* `social/commons/components/comments`
>* `social/commons/components/comments/comment`
>



오버레이의 자체 `Type`(속성 `sling:resourceType`)는 상대 자체 참조여야 합니다. 따라서 /apps에서 찾을 수 없는 모든 컨텐츠가 /libs에서 검색됩니다.
* 이름: `sling:resourceType`
* 유형: `String`
* 값: `social/commons/components/hbs/comments`

1. 녹색 선택 `[+] Add`
   * 이름: `sling:resourceType`
   * 유형: `String`
   * 값: `social/commons/components/hbs/comments/comment`
1. 녹색 선택 `[+] Add`
   * 모두 **[!UICONTROL 저장을 선택합니다.]**

![chlimage_1-4](assets/chlimage_1-4.png)

