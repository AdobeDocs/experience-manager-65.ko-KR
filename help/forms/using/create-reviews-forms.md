---
title: 양식에서 자산에 대한 검토 만들기 및 관리
seo-title: Creating and managing reviews for assets in forms
description: 검토는 한 명 이상의 검토자가 양식에서 사용할 수 있는 에셋에 댓글을 달 수 있는 메커니즘입니다.
seo-description: A Review is a mechanism that allows one or more reviewers to comment on an asset that is available in a form.
uuid: 45c7ff56-3fa8-4a0f-8597-05404e547282
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: d8c1c507-a6c4-44f5-be01-ee902bc28410
docset: aem65
feature: Adaptive Forms
exl-id: 9ca4fcd6-3eb0-4fc1-a09c-e4ad532bbed0
source-git-commit: 4edfc51227607b4fb3ee4b97443d2040015b6a65
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 0%

---

# 양식에서 자산에 대한 검토 만들기 및 관리{#creating-and-managing-reviews-for-assets-in-forms}

## 리뷰 {#review}

검토는 한 명 이상의 검토자가 양식에서 사용할 수 있는 에셋에 댓글을 달 수 있는 메커니즘입니다.

## 리뷰 설정 {#setting-up-a-review}

1. Forms 탭으로 이동하여 양식을 선택합니다.
1. 에셋에 진행 중인 검토가 없는 경우 검토 시작 ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png) 아이콘이 작업 표시줄에 나타납니다. Start Review 를 클릭합니다. ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png) 아이콘.
1. 다음 정보를 입력합니다.

   * 검토 이름: 필수, 영숫자, 하이픈 또는 밑줄을 포함할 수 있습니다.
   * 검토 설명: 선택사항, 검토 목적/콘텐츠에 대한 설명.
   * 검토 기한: 선택적, 검토 종료 일자. 기한이 지나면 작업이 &#39;기한 초과&#39;로 표시됩니다.
   * 검토자: 최소 1명은 필수입니다. 콤보 상자를 사용하여 검토자를 추가합니다. 이름을 입력하면 일치하는 모든 이름이 나열됩니다. 이름을 선택하고 추가를 누릅니다.

1. 나머지 세부 정보를 모두 입력한 다음 시작을 클릭합니다.

### 검토를 설정할 때 발생하는 작업 {#actions-that-occur-when-a-review-is-set-up}

이 섹션에서는 검토를 만들거나 설정할 때 수행되는 작업을 설명합니다.

1. 새 검토 작업이 생성되고 검토 개시자에게 할당됩니다.
1. 모든 검토자에게 검토 작업이 할당됩니다. 작업이 알림 섹션에 표시됩니다. 검토자는 알림을 클릭하거나 받은 편지함으로 이동하여 작업을 볼 수 있습니다. 검토자가 클릭하여 검토 작업을 열고 양식을 보고 주석 추가를 시작할 수 있습니다.

   ![검토자 알림 경고](assets/noti.png)

   검토자 알림 경고

1. 설명 상자는 에셋의 개시자와 검토자가 사용할 수 있습니다. 다른 사용자는 댓글을 볼 수 있지만 댓글을 쓸 수 없습니다.

## 검토 관리 {#managing-a-review}

>[!NOTE]
>
>진행 중인 검토만 수정할 수 있습니다. 완료된 검토는 수정할 수 없습니다.

1. Forms 탭으로 이동하여 양식을 선택합니다.

1. 에셋에 검토 진행 중인 경우 사용자가 검토 개시자인 경우 검토 관리 ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png) 아이콘이 작업 표시줄에 나타납니다. 검토 개시자만 검토를 관리(업데이트/종료)할 수 있습니다.

   Manage Review 클릭 ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png)아이콘.

   개시자가 아닌 사용자의 경우 검토 관리 아이콘이 비활성화됩니다.

1. 정보를 표시하는 화면이 나타납니다.

   * **이름 검토**: 편집할 수 없습니다.

   * **설명 검토**: 편집에 사용할 수 있습니다.

   * **검토 기한**: 편집에 사용할 수 있습니다. 기한을 현재 날짜 및 시간 이후의 모든 날짜 및 시간으로 수정할 수 있습니다.

   * **검토자**: 편집에 사용할 수 있습니다. 검토자를 추가하거나 제거할 수 있습니다. 작업이 지연되는 경우 현재 날짜를 넘어 기한을 연장한 후에만 검토자를 추가할 수 있습니다.

1. 검토를 종료하려면 종료를 누릅니다.

### 검토를 수정할 때 발생하는 작업 {#actions-that-occur-when-a-review-is-modified}

이 섹션에서는 검토 종료/수정 시 발생하는 사항에 대해 설명합니다.

1. 검토 설명이 수정되면 검토자와 개시자의 해당 작업이 업데이트됩니다.
1. 검토 기한을 수정하면 검토자에 대한 해당 작업이 새 날짜로 업데이트됩니다.

1. 검토자가 제거된 경우:

   ![검토자 제거](assets/removeduser.png)

   검토자 제거

   1. 완료되지 않은 경우 할당된 작업이 종료됩니다.
   1. 검토자가 더 이상 에셋에 댓글을 달 수 없습니다.

1. 검토자가 추가되면:

   ![검토자 추가](assets/addedreviewer.png)

   검토자 추가

   1. 검토 작업이 생성되고 새로 추가된 검토자에게 할당됩니다.
   1. 새로 추가된 검토자는 에셋에 대한 주석을 추가할 수 있습니다.

1. 검토 종료 시:

   1. **검토자**: 각 검토자에 대해 검토와 관련된 완료되지 않은 작업이 종료됩니다. 검토자의 알림 섹션에 작업이 더 이상 &#39;보류 중&#39;으로 표시되지 않습니다.
   1. **개시자**: 검토 개시자에게 할당된 작업이 완료된 것으로 표시됩니다. 작업이 검토 개시자의 알림 섹션에서 제거됩니다.
   1. **모두**: 리뷰가 이전 리뷰 섹션에 표시됩니다. 더 이상 댓글을 추가할 수 없습니다.
