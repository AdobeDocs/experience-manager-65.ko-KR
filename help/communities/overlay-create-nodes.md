---
title: 노드 만들기
seo-title: 노드 만들기
description: 댓글 시스템 오버레이
seo-description: 댓글 시스템 오버레이
uuid: 802ae28b-9989-4c2c-b466-ab76a724efd3
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: cd4f53ee-537b-4f10-a64f-474ba2c44576
exl-id: 3d72cbdf-5eb4-477d-aa61-035a846f7dcb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 6%

---

# 노드 만들기 {#create-nodes}

`/libs`에서 `/apps`에 필요한 최소한의 파일을 복사하고 `/apps`에서 수정하여 주석 시스템을 사용자 정의 버전으로 오버레이합니다.

>[!CAUTION]
>
>/apps 폴더의 내용은 그대로 둔 상태에서 다시 설치하거나 업그레이드하면 /libs 폴더를 삭제하거나 교체할 수 있으므로 /libs 폴더의 내용은 편집되지 않습니다.

작성자 인스턴스에서 [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)를 사용하는 경우, /apps 폴더에 /libs 폴더에 있는 오버레이된 구성 요소의 경로와 동일한 경로를 만듭니다.

복제할 경로는 다음과 같습니다.

* `/libs/social/commons/components/hbs/comments/comment`

경로의 일부 노드는 폴더이고 일부는 구성 요소입니다.

1. [http://localhost:4502/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp) 로 이동합니다.
1. `/apps/social` 만들기(아직 없는 경우)
   * `/apps` 노드 선택
   * **[!UICONTROL 만들기 > 폴더 ..]**
      * 이름 입력: `social`
1. `social` 노드 선택
   * **[!UICONTROL 만들기]**  >  **[!UICONTROL 폴더..]**
      * 이름 입력: `commons`
1. `commons` 노드 선택
   * **[!UICONTROL 만들기 > 폴더...]**
      * 이름 입력: `components`
1. `components` 노드 선택
   * **[!UICONTROL 만들기 > 폴더..]**.
      * 이름 입력: `hbs`
1. `hbs` 노드 선택
   * **[!UICONTROL 만들기]**  >  **[!UICONTROL 구성 요소 만들기..]**
      * 레이블 입력:`comments`
      * 제목 입력:`Comments`
      * 설명 입력:`List of comments without showing avatars`
      * Super Type: `social/commons/components/comments`
      * 그룹 입력:`Communities`
      * **[!UICONTROL 다음]**&#x200B;확인&#x200B;]**까지 클릭하십시오.**[!UICONTROL 
1. `comments` 노드 선택

   * **[!UICONTROL 만들기]**  >  **[!UICONTROL 구성 요소 만들기..]**

      * 레이블 입력:`comment`
      * 제목 입력:`Comment`
      * 설명 입력:`A comment instance without avatars`
      * 수퍼 유형:`social/commons/components/comments/comment`
      * 그룹 입력:`.hidden`
      * **[!UICONTROL 다음]**&#x200B;확인&#x200B;]**까지 클릭하십시오.**[!UICONTROL 
   * **[!UICONTROL 모두 저장]** 선택
1. 기본 `comments.jsp` 삭제
   * 노드 `/apps/social/commons/components/hbs/comments/comments.jsp` 선택
   * **[!UICONTROL 삭제]** 선택
1. 기본 comment.jsp 삭제
   * 노드 `/apps/social/commons/components/hbs/comments/comment/comment.jsp` 선택
   * **[!UICONTROL 삭제]** 선택
   * **[!UICONTROL 모두 저장]** 선택

>[!NOTE]
>
>상속 체인을 보존하기 위해 오버레이 구성 요소의 `Super Type`(속성 `sling:resourceSuperType`)은 오버레이되는 구성 요소의 `Super Type` 값과 동일한 값으로 설정됩니다. 이 경우 다음과 같습니다.
>
>* `social/commons/components/comments`
>* `social/commons/components/comments/comment`


오버레이의 자체 `Type`(속성 `sling:resourceType`)는 /apps에서 찾을 수 없는 컨텐츠를 /libs에서 찾을 수 있도록 상대 자체 참조여야 합니다.
* 이름: `sling:resourceType`
* 유형: `String`
* 값: `social/commons/components/hbs/comments`

1. 녹색 `[+] Add` 을 선택합니다.
   * 이름: `sling:resourceType`
   * 유형: `String`
   * 값: `social/commons/components/hbs/comments/comment`
1. 녹색 `[+] Add` 을 선택합니다.
   * **[!UICONTROL 모두 저장]** 선택

![create-nodes](assets/create-nodes.png)
