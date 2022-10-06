---
title: 채널 및 웹 채널 인쇄
seo-title: Print channel and web channel
description: 인쇄 채널 템플릿 가져오기 및 웹 채널 템플릿 만들기 및 활성화
seo-description: Importing print channel templates and creating and enabling web channel templates
uuid: 2361b1ee-c789-4a5a-9575-8b62b603da1e
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 96d2b1cc-3252-4cc7-8b06-a897cbef8599
docset: aem65
feature: Interactive Communication
exl-id: cd7dbdac-dc76-4a1f-b850-0a9f47ae08de
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 0%

---

# 채널 및 웹 채널 인쇄{#print-channel-and-web-channel}

대화형 커뮤니케이션은 다음 두 가지 채널을 통해 전달될 수 있습니다. 인쇄 및 웹 인쇄 채널은 보험료 지불을 미리 알림하기 위해 인쇄된 편지와 같은 PDF 및 용지 커뮤니케이션을 만드는 데 사용되는 반면, 웹 채널은 웹 사이트의 신용 카드 명세서와 같은 온라인 경험을 전달하는 데 사용됩니다.

Interactive Communication 작성자는 문서 조각이나 이미지와 같은 자산을 재사용하여 Interactive Communication의 인쇄 및 웹 버전을 모두 만들 수 있습니다.

을 위한 사전 요구 사항 중 하나 [대화형 통신 만들기](../../forms/using/create-interactive-communication.md) 는 서버에서 인쇄 및/또는 웹 채널을 위한 템플릿을 사용할 수 있도록 합니다. 템플릿 작성자가 AEM 자체에서 웹 채널 템플릿을 만드는 동안 인쇄 채널 템플릿 XDP는 Adobe Forms 디자이너에서 만들어지고 서버에 업로드됩니다.

## 인쇄 채널 {#printchannel}

대화형 커뮤니케이션의 인쇄 채널은 XFA 양식 서식 파일인 XDP를 사용합니다. XDP는 Adobe Forms 디자이너에 디자인되었습니다. 인쇄 채널 템플릿 만들기에 대한 자세한 내용은 [레이아웃 디자인](../../forms/using/layout-design-details.md). Interactive Communication에서 인쇄 채널 템플릿을 사용하려면 템플릿을 AEM Forms 서버에 업로드해야 합니다.

### 대화형 통신 인쇄 채널 템플릿 업로드 {#upload-interactive-communication-print-channel-template}

템플릿을 업로드하려면 forms-user 그룹의 구성원이어야 합니다. 다음 단계를 사용하여 인쇄 채널 템플릿(XDP)을 AEM Forms에 업로드합니다.

1. 선택 **[!UICONTROL Forms]** > **[!UICONTROL Forms 및 문서]**.

1. 탭 **[!UICONTROL 만들기]** > **[!UICONTROL 파일 업로드]**.

   적절한 XDP(인쇄 채널 템플릿)를 탐색하고 선택하고 를 누릅니다 **[!UICONTROL 열기]**.

## 웹 채널 {#web-channel}

템플릿 작성자 및 관리자는 웹 템플릿을 만들고, 편집하고, 활성화할 수 있습니다. 다른 사용자가 웹 템플릿을 작성할 수 있도록 하려면 사용자에게 권한을 제공해야 합니다. 자세한 내용은 [사용자, 그룹 및 액세스 권한 관리](/help/sites-administering/user-group-ac-admin.md).

### 웹 채널 템플릿 작성 {#authoring-web-channel-template}

웹 채널 템플릿을 만들려면 먼저 템플릿 폴더를 만들어야 합니다. 템플릿 폴더 내에 웹 템플릿을 만들면 양식 사용자가 템플릿을 기반으로 대화형 커뮤니케이션의 웹 채널을 만들 수 있도록 템플릿을 활성화해야 합니다.

웹 채널 템플릿을 작성하려면 다음 단계를 완료하십시오.

1. Interactive Communication 웹 템플릿이 아직 없는 경우 해당 템플릿을 유지할 템플릿 폴더를 만듭니다. 자세한 내용은 템플릿 폴더 를 참조하십시오. [페이지 템플릿 - 편집 가능](/help/sites-developing/page-templates-editable.md).

   1. 탭 **[!UICONTROL 도구]** ![도구](assets/tools.png) > **[!UICONTROL 구성 브라우저]**.
      * 자세한 내용은 [구성 브라우저](/help/sites-administering/configurations.md) 설명서 를 참조하십시오.
   1. Configuration Browser 페이지에서 **[!UICONTROL 만들기]**.
   1. 구성 만들기 대화 상자에서 폴더의 제목을 지정하고 **[!UICONTROL 편집 가능한 템플릿]**, 탭 **[!UICONTROL 만들기]**.

      폴더가 생성되고 구성 브라우저 페이지에 나열됩니다.

1. 해당 템플릿 폴더로 이동하고 웹 템플릿을 만듭니다.

   1. 을(를) 선택하여 해당 템플릿 폴더로 이동합니다 **[!UICONTROL 도구]** > **[!UICONTROL 템플릿]** > **`[Folder]`**.
   1. 탭 **[!UICONTROL 만들기]**.
   1. 선택 **[!UICONTROL 대화형 통신 - 웹 채널]** 탭 **[!UICONTROL 다음]**.
   1. 템플릿 제목 및 설명을 입력한 다음 **[!UICONTROL 만들기]**.

      템플릿이 만들어지고 대화 상자가 나타납니다.

   1. 탭 **[!UICONTROL 열기]** 템플릿 편집기에서 만든 템플릿을 열려면 다음을 수행하십시오.

      템플릿 편집기가 나타납니다.

      ![웹 채널 템플릿](assets/webchanneltemplate.png)

      템플릿을 만들거나 편집할 때 템플릿 작성자가 정의할 수 있는 다양한 측면이 있습니다. 템플릿을 만들거나 편집하는 것은 페이지 작성과 유사합니다. 자세한 내용은 의 템플릿 편집 - 템플릿 작성자 를 참조하십시오. [페이지 템플릿 만들기](/help/sites-authoring/templates.md).

1. 대화형 통신 작성을 위해 이 템플릿을 사용하려면 템플릿을 활성화합니다.

   1. 탭 **[!UICONTROL 도구]** ![도구](assets/tools.png) > **[!UICONTROL 템플릿]**.
   1. 해당 템플릿으로 이동하여 선택한 다음 탭합니다 **[!UICONTROL 활성화]** 경고 메시지에서 **[!UICONTROL 활성화]**.

      템플릿이 활성화되고 해당 상태가 사용으로 표시됩니다. 이제 새로 만든 웹 채널 템플릿을 사용할 수 있는 대화형 통신 만들기를 진행할 수 있습니다.

### 웹 채널용 마스터로 채널 인쇄 {#print-channel-as-master-for-web-channel}

대화형 커뮤니케이션을 작성하는 동안 작성자가 이 옵션을 선택하여 인쇄 채널과 동기화되는 웹 채널을 만들 수 있습니다. 인쇄 채널을 웹 채널용 마스터로 사용하면 웹 채널의 컨텐츠, 상속 및 데이터 바인딩이 인쇄 채널에서 파생되고 인쇄 채널에서 수행된 변경 사항이 웹 채널에 반영될 수 있습니다. 그러나 대화형 통신 작성자는 필요에 따라 웹 채널의 특정 구성 요소에 대한 상속을 중단할 수 있습니다.

![채널을 마스터로 인쇄](assets/create_ic_print_master_new.png) ![인쇄 채널을 마스터로 사용하는 웹 채널](assets/create_ic_print_master_web_new.png)
