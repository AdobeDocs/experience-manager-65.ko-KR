---
title: 페이지에 워크플로우 적용
seo-title: 페이지에 워크플로우 적용
description: 작성 시 워크플로우를 호출하여 페이지에서 작업을 수행할 수 있습니다. 또한 둘 이상의 워크플로우를 적용할 수도 있습니다.
seo-description: 작성 시 워크플로우를 호출하여 페이지에서 작업을 수행할 수 있습니다. 또한 둘 이상의 워크플로우를 적용할 수도 있습니다.
uuid: 652d9a23-907d-43ad-9eef-7ab1d07918cd
contentOwner: Alison Heimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 6472dc94-96e0-4286-8f86-d85726cc843c
docset: aem65
translation-type: tm+mt
source-git-commit: 611743cc4144f99968845093b3903fe7df8bf9d9
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 85%

---


# 페이지에 워크플로우 적용{#applying-workflows-to-pages}

작성 시 워크플로우를 호출하여 페이지에서 작업을 수행할 수 있습니다.또한 두 개 이상의 워크플로우를 적용할 수도 있습니다.

워크플로우를 적용할 때에는 다음 정보를 지정합니다.

* 적용할 워크플로우.
 모든 워크플로우(AEM 관리자가 지정한 액세스 권한이 있는 워크플로우)를 적용할 수 있습니다.
* 원할 경우, 사용자의 받은 편지함에서 워크플로우 인스턴스를 식별하는 데 도움이 되는 제목.
* 워크플로우 페이로드. 하나 이상의 페이지일 수 있습니다.

워크플로우는 다음 위치에서 시작될 수 있습니다.

* [사이트 콘솔](#starting-a-workflow-from-the-sites-console).
* [페이지 편집 시 페이지 정보](#starting-a-workflow-from-the-page-editor)

>[!NOTE]
>
>참고 항목:
>
>* [워크플로우를 DAM 자산에 적용하는 방법](/help/assets/assets-workflow.md)
>* [프로젝트 워크플로우 작업](/help/sites-authoring/projects-with-workflows.md).

>



>[!NOTE]
>
>AEM 관리자는 [몇 가지 다른 방법](/help/sites-administering/workflows-starting.md)을 사용하여 워크플로우를 시작할 수 있습니다.

## 사이트 콘솔에서 워크플로우 시작 {#starting-a-workflow-from-the-sites-console}

다음 중 하나에서 워크플로우를 시작할 수 있습니다.

* [[사이트] 도구 모음의 만들기 선택 사항](#starting-a-workflow-from-the-sites-toolbar)
* [사이트 콘솔의 타임라인 레일](#starting-a-workflow-from-the-timeline)

두 경우 모두 다음을 수행해야 합니다.

* [워크플로우 만들기 마법사에서 워크플로우 세부 사항 지정](#specifying-workflow-details-in-the-create-workflow-wizard)

### 사이트 도구 모음에서 워크플로우 시작  {#starting-a-workflow-from-the-sites-toolbar}

**사이트** 콘솔의 도구 모음에서 워크플로우를 시작할 수 있습니다.

1. 필요한 페이지로 이동하여 선택합니다.

1. 이제 도구 모음의 **만들기** 옵션에서 **워크플로우**&#x200B;를 선택할 수 있습니다.

   ![screen_shot_2019-03-06at121237pm](assets/screen_shot_2019-03-06at121237pm.png)

1. **워크플로우 만들기** 마법사는 [워크플로우 세부 사항을 지정](#specifying-workflow-details-in-the-create-workflow-wizard)하는 데 도움이 됩니다.

### 타임라인에서 워크플로우 시작  {#starting-a-workflow-from-the-timeline}

**타임라인**&#x200B;에서는 선택한 리소스에 적용할 워크플로우를 시작할 수 있습니다.

1. [리소스를 ](/help/sites-authoring/basic-handling.md#viewingandselectingyourresources) 선택하고  [타임라인](/help/sites-authoring/basic-handling.md#timeline) 을 엽니다(또는 타임라인을 연 다음 리소스를 선택합니다.).
1. 주석 필드 옆에 있는 화살촉 모양을 사용하여 **워크플로우 시작**&#x200B;을 표시할 수 있습니다.

   ![screen-shot_2019-03-05at120026](assets/screen-shot_2019-03-05at120026.png)

1. **워크플로우 만들기** 마법사는 [워크플로우 세부 사항을 지정](#specifying-workflow-details-in-the-create-workflow-wizard)하는 데 도움이 됩니다.

### 워크플로우 만들기 마법사에서 워크플로우 세부 사항 지정  {#specifying-workflow-details-in-the-create-workflow-wizard}

**워크플로우 만들기** 마법사는 워크플로우를 선택하고 필요한 세부 사항을 지정하는 데 도움이 됩니다.

다음 중 하나에서 **워크플로우 만들기** 마법사를 여십시오.

* [[사이트] 도구 모음의 만들기 선택 사항](#starting-a-workflow-from-the-sites-toolbar)
* [사이트 콘솔의 타임라인 레일](#starting-a-workflow-from-the-timeline)

세부 사항을 지정할 수 있습니다.

1. **속성** 단계에서는 워크플로우의 기본 선택 사항이 정의됩니다.

   * **워크플로우 모델**
   * **워크플로우 제목**

      * 나중 단계에서 식별할 수 있도록 이 인스턴스의 제목을 지정할 수 있습니다.

   워크플로우 모델에 따라 다음 선택 사항도 사용할 수 있습니다. 이 선택 사항을 사용하면 워크플로우가 완료된 후에도 페이로드로 만들어진 패키지를 유지할 수 있습니다.

   * **워크플로우 패키지 유지**
   * **패키지 제목**

      * 식별할 수 있도록 패키지의 제목을 지정할 수 있습니다.
   >[!NOTE]
   >
   >[여러 리소스 지원](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support)을 위한 워크플로우를 구성하고 여러 리소스를 선택하면 **워크플로우 패키지 유지** 선택 사항을 사용할 수 있습니다.

   완료되면 **다음**&#x200B;을 사용하여 계속 진행하십시오.

   ![wf-52](assets/wf-52.png)

1. **범위** 단계에서 다음 내용을 선택할 수 있습니다.

   * **컨텐츠** 추가에서  [경로 탐색](/help/sites-authoring/author-environment-tools.md#path-browser) 을 열고 추가 리소스를 선택합니다.브라우저에서는 선택을 클릭/ **** 탭하여 워크플로우 인스턴스에 컨텐츠를 추가합니다.

   * 추가 작업을 보기 위한 기존 리소스:

      * **하위 포함** - 해당 리소스의 하위 항목이 워크플로우에 포함되도록 지정합니다.
 대화 상자가 열려서 다음 내용에 따라 선택 내용을 개선할 수 있습니다.

         * 바로 아래 하위만 포함.
         * 수정된 페이지만 포함.
         * 이미 게시된 페이지만 포함.

         지정된 모든 하위 항목이 워크플로우가 적용될 리소스 목록에 추가됩니다.

      * **선택 제거** - 워크플로우에서 해당 리소스를 제거합니다.

   ![wf-53](assets/wf-53.png)

   >[!NOTE]
   >
   >리소스를 더 추가하려는 경우 **뒤로**&#x200B;를 사용하여 **속성** 단계에서 **워크플로우 패키지 유지**&#x200B;에 대한 설정을 조정할 수 있습니다.

1. **만들기**&#x200B;를 사용하여 마법사를 닫고 워크플로 인스턴스를 만듭니다. 알림은 사이트 콘솔에 표시됩니다.

## 페이지 편집기에서 워크플로우 시작  {#starting-a-workflow-from-the-page-editor}

페이지를 편집할 때 도구 모음에서 **페이지 정보**&#x200B;를 선택할 수 있습니다. 드롭다운 메뉴에는 **워크플로우에서 시작** 선택 사항이 있습니다. 이 선택 사항을 선택하면 필요한 경우 제목과 함께 필요한 워크플로를 지정할 수 있는 대화 상자가 열립니다.

![wf-54](assets/wf-54.png)
