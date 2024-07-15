---
title: 양식에서 리뷰 생성 및 관리
description: 검토는 한 명 이상의 검토자가 양식에 주석을 달 수 있는 메커니즘입니다.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
docset: aem65
feature: Foundation Components
exl-id: 9ca4fcd6-3eb0-4fc1-a09c-e4ad532bbed0
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 8a77756e8ba771c8de9950c2323bef8f23cc59b4
workflow-type: tm+mt
source-wordcount: '701'
ht-degree: 9%

---

# 양식에 대한 리뷰 생성 및 관리{#creating-and-managing-reviews-to-forms}

<span class="preview"> [새 적응형 양식 만들기](/help/forms/using/create-an-adaptive-form-core-components.md) 또는 [AEM Sites 페이지에 적응형 양식 추가](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md) 작업을 할 때 현대적이고 확장 가능한 데이터 캡처 [핵심 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)를 사용하는 것이 좋습니다. 이러한 구성 요소는 적응형 양식 만들기 작업이 대폭 개선되어 우수한 사용자 경험을 보장할 수 있게 되었음을 나타냅니다. 이 문서에서는 기초 구성 요소를 사용하여 적응형 양식을 작성하는 이전 접근법에 대해 설명합니다. </span>

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-reviews-forms.html) |
| AEM 6.5 | 이 문서 |

## 검토 {#review}

검토는 한 명 이상의 검토자가 양식에 주석을 달 수 있도록 하는 메커니즘입니다.

## 리뷰 설정 {#setting-up-a-review}

1. 양식 브라우저로 이동하고 검토할 양식을 선택합니다.
1. 양식에 진행 중인 검토가 없으면 **검토 시작** ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png) 아이콘이 작업 표시줄에 나타납니다. **검토 시작** ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png) 아이콘을 클릭합니다.
1. 다음 정보를 입력합니다.

   * **제목**: 필수 항목이며, 영숫자, 하이픈 및 밑줄을 포함할 수 있습니다.
   * **설명**: 검토용 목적/콘텐츠에 대한 선택적 설명입니다.
   * **기한**: 선택적, 검토 종료 날짜입니다. 기한이 지나면 작업이 &#39;기한 초과&#39;로 표시됩니다.
   * **검토자 이름**: 최소 하나의 이름은 필수입니다. 콤보 상자를 사용하여 검토자를 추가하고 일치하는 모든 이름의 이름 목록을 입력하십시오. 이름을 선택하고 **추가**&#x200B;를 클릭하십시오. **검토자** 탭의 다음 섹션에 모든 검토자의 이름이 표시됩니다.

1. 검토를 시작하려면 **시작**&#x200B;을 클릭하세요.

   >[!NOTE]
   >
   >* 관리자는 양식 사용자와 관련된 모든 그룹에 액세스할 수 있습니다.
   >* [서비스 사용자] 그룹을 선택하여 검토할 수 없습니다.

### 검토를 설정할 때 발생하는 작업 {#actions-that-occur-when-a-review-is-set-up}

이 섹션에서는 검토를 만들거나 설정할 때 수행되는 작업을 설명합니다.

1. 새 검토 작업이 생성되고 선택한 검토자에게 할당됩니다.
1. 모든 검토자에게 검토 작업이 할당됩니다. 작업이 알림 섹션에 표시됩니다. 검토자는 알림을 클릭하거나 받은 편지함으로 이동하여 작업을 볼 수 있습니다. 검토자가 클릭하여 검토 작업을 열고 양식을 보고 주석 추가를 시작할 수 있습니다.

   ![검토자 알림 경고](assets/review-notification-img.png)

   검토자 알림 경고

1. 설명 상자는 양식 검토자가 사용할 수 있습니다. 다른 사용자는 설명을 읽을 수 있지만 자신의 설명을 추가할 수는 없습니다.

## 검토 관리 {#managing-a-review}

>[!NOTE]
>
>* 진행 중인 검토만 수정할 수 있습니다.
>* 완료된 검토는 수정할 수 없습니다.

1. 양식 탭으로 이동하여 양식을 선택합니다.

1. 검토 중인 양식에 검토 개시자가 있는 경우 **검토 관리** ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png) 아이콘이 작업 표시줄에 나타납니다. 검토 개시자만 검토를 관리(업데이트/종료)할 수 있습니다.

   **검토 관리** ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png)아이콘을 클릭합니다.

   개시자가 아닌 사용자의 경우 검토 관리 아이콘이 비활성화됩니다.

1. 이제 정보를 표시하는 화면이 나타납니다.

   * **검토 이름**: 편집할 수 없습니다.

   * **설명 검토**: 편집할 수 있습니다.

   * **검토 기한**: 편집할 수 있습니다. 기한을 현재 날짜 및 시간 이후의 모든 날짜 및 시간으로 수정할 수 있습니다.

   * **검토자**: 편집 가능. 검토자를 추가하거나 제거할 수 있습니다. 작업이 지연되는 경우 현재 날짜를 넘어 기한을 연장한 후에만 검토자를 추가할 수 있습니다.

1. 검토를 종료하려면 **종료**&#x200B;를 클릭하십시오.

### 검토를 수정할 때 발생하는 작업 {#actions-that-occur-when-a-review-is-modified}

이 섹션에서는 **업데이트/종료 검토**&#x200B;에서 수행되는 작업에 대해 설명합니다.

1. 검토 설명이 수정되면 검토자와 개시자의 해당 작업이 업데이트됩니다.
1. 검토 기한을 수정하면 검토자에 대한 해당 작업이 새 날짜로 업데이트됩니다.

1. 검토자가 제거된 경우:

   ![검토자 제거](assets/removeduser.png)

   검토자 제거

   1. 완료되지 않은 경우 할당된 작업이 종료됩니다.
   1. 검토자가 더 이상 양식에 주석을 달 수 없습니다.

1. 검토자가 추가되면:

   ![검토자 추가](assets/addedreviewer.png)

   검토자 추가

   1. 검토 작업이 생성되고 새로 추가된 검토자에게 할당됩니다.
   1. 새로 추가된 검토자는 양식에 대한 주석을 추가할 수 있습니다.

1. 검토 종료 시:

   1. **검토자**: 각 검토자에 대해 검토와 관련된 불완전한 작업이 종료됩니다. 검토자의 알림 섹션에 작업이 더 이상 &#39;보류 중&#39;으로 표시되지 않습니다.
   1. **개시자**: 검토 개시자에게 할당된 작업이 완료된 것으로 표시됩니다. 작업이 검토 개시자의 알림 섹션에서 제거됩니다.
   1. **모두**: 리뷰가 이전 리뷰 섹션에 표시됩니다. 더 이상 댓글을 추가할 수 없습니다.

   ![검토 완료](assets/review-complete-imgg.png)
