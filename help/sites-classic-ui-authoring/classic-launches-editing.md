---
title: 론치 편집
seo-title: 론치 편집
description: 페이지(또는 페이지 세트)에 대한 론치가 만들어지면 페이지의 론치 카피에서 컨텐츠를 편집할 수 있습니다.
seo-description: 페이지(또는 페이지 세트)에 대한 론치가 만들어지면 페이지의 론치 카피에서 컨텐츠를 편집할 수 있습니다.
uuid: 3a310eeb-553d-4d2b-98b5-c5bc523b2aca
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 666b967a-e94b-4f94-a676-00adf150580f
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 100%

---


# 론치 편집{#editing-launches}

## 론치 편집 페이지 {#editing-launch-pages}

페이지(또는 페이지 세트)에 대한 론치가 만들어지면 페이지의 론치 카피에서 컨텐츠를 편집할 수 있습니다.

1. 편집할 페이지를 엽니다.
1. 사이드 킥에서 **버전 관리** 탭을 선택한 다음, **론치** 그룹을 확장합니다. 현재 편집하고 있는 론치의 제목에서는 굵은 글꼴을 사용합니다.

   ![chlimage_1-13](assets/chlimage_1-13.jpeg)

1. 작업할 론치를 선택한 다음 **전환**&#x200B;을 클릭합니다.
1. 편집을 시작합니다.

   >[!NOTE]
   >
   >사이드 킥의 **페이지** 탭을 사용하여 다른 작업 중에서 **하위 페이지 만들기**&#x200B;와 같은 작업을 수행할 수 있습니다.

## 론치 구성 편집 {#editing-a-launch-configuration}

론치를 만든 후 론치 이름과 론치 날짜를 변경할 수 있습니다. 이미지를 지정하여 론치와 연결할 수도 있습니다.

1. 론치 관리 페이지([http://localhost:4502/libs/launches/content/admin.html](http://localhost:4502/libs/launches/content/admin.html))를 엽니다.

1. 필요한 론치를 선택하고 **편집**&#x200B;을 클릭하여 대화 상자를 엽니다.

   * **일반** 탭에서 다음 내용을 편집할 수 있습니다.

      * **제목**
      * **활성 날짜**: 론치 날짜와 같습니다.
      * **프로덕션 준비**

      이 필드들의 목적과 상호 작용에 대해 알려면 [론치 - 이벤트 순서](/help/sites-authoring/launches.md#launches-the-order-of-events)를 참조하십시오.

   * **이미지** 탭에서 이미지 파일을 업로드할 수 있습니다.


1. **저장**&#x200B;을 클릭합니다.

## 페이지의 론치 상태 찾기 {#discovering-the-launch-status-of-a-page}

페이지의 론치를 편집할 때 론치에 대한 정보는 사이드 킥의 **버전 관리** 탭 하단에 표시됩니다.

* 론치 이름입니다.
* 마지막 변경 사항 이후의 시간입니다.
* 마지막 변경 작업을 수행한 사용자입니다.
* **프로덕션 준비** 플래그의 상태(주황색=설정되지 않음, 녹색=설정됨).

![chlimage_1-186](assets/chlimage_1-186.png)

