---
title: 노드 만들기
description: /libs에서 필요한 최소 수의 파일을 복사하고 /apps에서 편집하여 사용자 지정 버전으로 주석 시스템을 오버레이하는 방법에 대해 알아봅니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 3d72cbdf-5eb4-477d-aa61-035a846f7dcb
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 1%

---

# 노드 만들기 {#create-nodes}

필요한 최소 수의 파일을 `/libs`에서 `/apps`(으)로 복사하고 `/apps`에서 수정하여 사용자 지정 버전으로 주석 시스템을 오버레이합니다.

>[!CAUTION]
>
>/apps 폴더의 내용은 그대로 두고 다시 설치하거나 업그레이드하면 /libs 폴더가 삭제되거나 대체될 수 있으므로 /libs 폴더의 내용은 편집되지 않습니다.

작성자 인스턴스에서 [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)을(를) 사용하여 /libs 폴더에 있는 오버레이된 구성 요소의 경로와 동일한 경로를 /apps 폴더에 만듭니다.

복제되는 경로는 다음과 같습니다.

* `/libs/social/commons/components/hbs/comments/comment`

경로의 일부 노드는 폴더이고 일부는 구성 요소입니다.

1. [http://localhost:4502/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp)(으)로 이동
1. `/apps/social` 만들기(아직 없는 경우)
   * `/apps` 노드 선택
   * **[!UICONTROL 만들기 > 폴더]**
      * 이름 입력: `social`
1. `social` 노드 선택
   * **[!UICONTROL 만들기]** > **[!UICONTROL 폴더]**
      * 이름 입력: `commons`
1. `commons` 노드 선택
   * **[!UICONTROL 만들기 > 폴더]**
      * 이름 입력: `components`
1. `components` 노드 선택
   * **[!UICONTROL 만들기 > 폴더]**.
      * 이름 입력: `hbs`
1. `hbs` 노드 선택
   * **[!UICONTROL 만들기]** > **[!UICONTROL 구성 요소 만들기]**
      * 레이블 입력: `comments`
      * 제목 입력: `Comments`
      * 설명 입력: `List of comments without showing avatars`
      * 상위 유형: `social/commons/components/comments`
      * 그룹 입력: `Communities`
      * **[!UICONTROL 확인]**&#x200B;까지 **[!UICONTROL 다음]**&#x200B;을 클릭하세요.
1. `comments` 노드 선택

   * **[!UICONTROL 만들기]** > **[!UICONTROL 구성 요소 만들기]**

      * 레이블 입력: `comment`
      * 제목 입력: `Comment`
      * 설명 입력: `A comment instance without avatars`
      * 상위 유형: `social/commons/components/comments/comment`
      * 그룹 입력: `.hidden`
      * **[!UICONTROL 확인]**&#x200B;까지 **[!UICONTROL 다음]**&#x200B;을 클릭하세요.
   * **[!UICONTROL 모두 저장]** 선택
1. 기본 `comments.jsp` 삭제
   * `/apps/social/commons/components/hbs/comments/comments.jsp` 노드 선택
   * **[!UICONTROL 삭제]** 선택
1. 기본 comment.jsp 삭제
   * `/apps/social/commons/components/hbs/comments/comment/comment.jsp` 노드 선택
   * **[!UICONTROL 삭제]** 선택
   * **[!UICONTROL 모두 저장]** 선택

>[!NOTE]
>
>상속 체인을 유지하기 위해 오버레이 구성 요소의 `Super Type`(속성 `sling:resourceSuperType`)이(가) 오버레이되는 구성 요소의 `Super Type`과(와) 동일한 값으로 설정됩니다. 이 경우 다음과 같습니다.
>
>* `social/commons/components/comments`
>* `social/commons/components/comments/comment`

오버레이의 자체 `Type`(속성 `sling:resourceType`)은(는) 상대 자체 참조여야 /apps에서 찾을 수 없는 모든 콘텐츠를 /libs에서 찾을 수 있습니다.
* 이름: `sling:resourceType`
* 유형: `String`
* 값: `social/commons/components/hbs/comments`

1. 녹색 `[+] Add` 선택
   * 이름: `sling:resourceType`
   * 유형: `String`
   * 값: `social/commons/components/hbs/comments/comment`
1. 녹색 `[+] Add` 선택
   * **[!UICONTROL 모두 저장]** 선택

![노드 만들기](assets/create-nodes.png)
