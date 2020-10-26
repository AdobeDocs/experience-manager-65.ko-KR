---
title: 인쇄 채널 및 웹 채널
seo-title: 인쇄 채널 및 웹 채널
description: 인쇄 채널 템플릿 가져오기 및 웹 채널 템플릿 만들기 및 활성화
seo-description: 인쇄 채널 템플릿 가져오기 및 웹 채널 템플릿 만들기 및 활성화
uuid: 2361b1ee-c789-4a5a-9575-8b62b603da1e
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 96d2b1cc-3252-4cc7-8b06-a897cbef8599
docset: aem65
translation-type: tm+mt
source-git-commit: ce64b148ba96cc64670aaf96c1b201bafa282b98
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 0%

---


# 인쇄 채널 및 웹 채널{#print-channel-and-web-channel}

인터랙티브 커뮤니케이션은인쇄 및 웹 인쇄 채널은 보험료 납부에 대한 독촉장으로 인쇄된 편지와 같은 PDF 및 용지 커뮤니케이션을 만드는 데 사용되고 웹 채널은 웹 사이트에서 신용 카드 명세서와 같은 온라인 경험을 전달하는 데 사용됩니다.

Interactive Communication authors can reuse assets such as document fragments and images to create both print and web version of Interactive Communication.

대화형 통신 [](../../forms/using/create-interactive-communication.md) 만들기를 위한 사전 요구 사항 중 하나는 서버에서 인쇄 및/또는 웹 채널을 위한 템플릿을 사용할 수 있도록 하는 것입니다. 템플릿 작성자가 AEM 자체에서 웹 채널 템플릿을 만드는 동안 인쇄 채널 템플릿 XDP는 Adobe Forms 디자이너에 만들어지고 서버에 업로드됩니다.

## Print channel {#printchannel}

인터랙티브 커뮤니케이션의 인쇄 채널에서는 XFA 양식 템플릿인 XDP를 사용합니다. XDP는 Adobe Forms 디자이너으로 설계되었습니다. 인쇄 채널 템플릿 만들기에 대한 자세한 내용은 [레이아웃 디자인을 참조하십시오](../../forms/using/layout-design-details.md). 인터랙티브 커뮤니케이션에서 인쇄 채널 템플릿을 사용하려면 템플릿을 AEM Forms 서버에 업로드해야 합니다.

### 대화형 통신 인쇄 채널 템플릿 업로드 {#upload-interactive-communication-print-channel-template}

템플릿을 업로드하려면 양식 사용자 그룹의 구성원이어야 합니다. 다음 단계에 따라 인쇄 채널 템플릿(XDP)을 AEM Forms에 업로드합니다.

1. [ **[!UICONTROL Forms]** ] > [ **[!UICONTROL Forms 및 문서]를 선택합니다]**.

1. 만들기 **[!UICONTROL > 파일]** **[!UICONTROL 업로드를]**&#x200B;누릅니다.

   적절한 인쇄 채널 템플릿(XDP)을 찾아 선택하고 열기를 **[!UICONTROL 누릅니다]**.

## Web channel {#web-channel}

템플릿 작성자 및 관리자는 웹 템플릿을 만들고, 편집하고, 활성화할 수 있습니다. 다른 사용자가 웹 템플릿을 작성하도록 허용하려면 해당 사용자에게 권한을 부여해야 합니다. 자세한 내용은 [사용자, 그룹 및 액세스 권한 관리를 참조하십시오](/help/sites-administering/user-group-ac-admin.md).

### 웹 채널 템플릿 작성 {#authoring-web-channel-template}

웹 채널 템플릿을 만들려면 먼저 템플릿 폴더를 만들어야 합니다. 템플릿 폴더 내에 웹 템플릿을 만들면 양식 사용자가 템플릿을 기반으로 대화형 커뮤니케이션의 웹 채널을 만들 수 있도록 템플릿을 활성화해야 합니다.

웹 채널 템플릿을 작성하려면 다음 단계를 완료하십시오.

1. 아직 Interactive Communication 웹 템플릿이 없는 경우 템플릿 폴더를 만듭니다. 자세한 내용은 페이지 템플릿의 템플릿 폴더 [- 편집 가능을 참조하십시오](/help/sites-developing/page-templates-editable.md).

   1. 도구 **[!UICONTROL 도구]** ![](assets/tools.png) > **[!UICONTROL 구성 브라우저를]**&#x200B;누릅니다.
      * See the [Configuration Browser](/help/sites-administering/configurations.md) documentation for more information.
   1. 구성 브라우저 페이지에서 만들기를 **[!UICONTROL 누릅니다]**.
   1. 구성 만들기 대화 상자에서 폴더의 제목을 지정하고 편집 가능한 템플릿 **[!UICONTROL 을]**&#x200B;선택한 다음 **[!UICONTROL 만들기를 누릅니다]**.

      폴더가 생성되어 구성 브라우저 페이지에 나열됩니다.

1. 해당 템플릿 폴더로 이동하여 웹 템플릿을 만듭니다.

   1. 도구 > 템플릿 **[!UICONTROL > 을 선택하여 해당 템플릿 폴더]** 로 **[!UICONTROL 이동합니다]** **`[Folder]`**.
   1. 만들기를 **[!UICONTROL 누릅니다]**.
   1. [ **[!UICONTROL 대화형 통신 - 웹 채널]** ]을 선택하고 [다음]을 **[!UICONTROL 누릅니다]**.
   1. 템플릿 제목과 설명을 입력한 다음 만들기를 **[!UICONTROL 누릅니다]**.

      템플릿이 만들어지고 대화 상자가 나타납니다.

   1. 열기 **[!UICONTROL 를]** 눌러 템플릿 편집기에서 만든 템플릿을 엽니다.

      템플릿 편집기가 나타납니다.

      ![웹 채널 템플릿](assets/webchanneltemplate.png)

      템플릿을 만들거나 편집할 때 템플릿 작성자가 정의할 수 있는 다양한 측면이 있습니다. 템플릿을 만들거나 편집하는 것은 페이지 작성과 비슷합니다. 자세한 내용은 템플릿 편집 - 페이지 템플릿 만들기에서 템플릿 [작성자를 참조하십시오](/help/sites-authoring/templates.md).

1. 대화형 통신 작성을 위해 이 템플릿을 사용하려면 템플릿을 활성화합니다.

   1. 도구 **[!UICONTROL 도구]** ![](assets/tools.png) > **[!UICONTROL 템플릿을]**&#x200B;누릅니다.
   1. 해당 템플릿으로 이동하여 선택한 다음 **[!UICONTROL 활성화를]** 누르고 경고 메시지에서 **[!UICONTROL 활성화를 탭합니다]**.

      템플릿이 활성화되고 상태는 활성화됨으로 표시됩니다. 이제 새로 만든 웹 채널 템플릿을 사용할 수 있는 대화형 통신을 만들 수 있습니다.

### 웹 채널의 마스터로 채널 인쇄 {#print-channel-as-master-for-web-channel}

작성자는 대화형 통신을 작성하는 동안 이 옵션을 선택하여 인쇄 채널과 동기화된 웹 채널을 만들 수 있습니다. 웹 채널의 마스터로 인쇄 채널을 사용하면 웹 채널의 컨텐츠, 상속 및 데이터 바인딩이 인쇄 채널에서 파생되고 인쇄 채널에서 수행된 변경 사항이 웹 채널에 반영될 수 있습니다. 그러나 대화형 통신 작성자는 필요에 따라 웹 채널의 특정 구성 요소에 대한 상속을 중단할 수 있습니다.

![채널에서 마스터](assets/create_ic_print_master_new.png) ![웹 채널로 인쇄 및 마스터로 인쇄](assets/create_ic_print_master_web_new.png)

