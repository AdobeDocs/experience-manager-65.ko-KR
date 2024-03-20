---
title: 인쇄 채널 및 웹 채널
description: 인쇄 채널 템플릿 가져오기 및 웹 채널 템플릿 만들기 및 활성화
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Interactive Communication
exl-id: cd7dbdac-dc76-4a1f-b850-0a9f47ae08de
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 0%

---

# 인쇄 채널 및 웹 채널{#print-channel-and-web-channel}

대화형 커뮤니케이션은 인쇄와 웹의 두 가지 채널을 통해 전달될 수 있습니다. 인쇄 채널은 PDF 및 보험료 납부를 위한 미리 알림으로 인쇄된 서신과 같은 종이 통신을 만드는 데 사용되며, 웹 채널은 웹 사이트의 신용 카드 명세서와 같은 온라인 경험을 전달하는 데 사용됩니다.

대화형 통신 작성자는 문서 단편 및 이미지와 같은 자산을 재사용하여 대화형 통신의 인쇄 및 웹 버전을 모두 만들 수 있습니다.

에 대한 사전 요구 사항 중 하나 [대화형 통신 만들기](../../forms/using/create-interactive-communication.md) 인쇄 및/또는 웹 채널용 템플릿을 서버에서 사용할 수 있도록 하는 것입니다. 템플릿 작성자가 AEM 자체에서 웹 채널 템플릿을 만드는 동안 인쇄 채널 템플릿 XDP는 Adobe Forms Designer에서 만들어지고 서버에 업로드됩니다.

## 인쇄 채널 {#printchannel}

대화형 통신의 인쇄 채널은 XFA 양식 템플릿 XDP를 사용합니다. XDP는 Adobe Forms Designer에서 설계되었습니다. 인쇄 채널 템플릿 만들기에 대한 자세한 내용은 [레이아웃 디자인](../../forms/using/layout-design-details.md). 대화형 통신에서 인쇄 채널 템플릿을 사용하려면 템플릿을 AEM Forms 서버에 업로드해야 합니다.

### 대화형 통신 인쇄 채널 템플릿 업로드 {#upload-interactive-communication-print-channel-template}

템플릿을 업로드하려면 양식 사용자 그룹의 멤버여야 합니다. 다음 단계를 사용하여 인쇄 채널 템플릿(XDP)을 AEM Forms에 업로드합니다.

1. 선택 **[!UICONTROL Forms]** > **[!UICONTROL Forms 및 문서]**.

1. 선택 **[!UICONTROL 만들기]** > **[!UICONTROL 파일 업로드]**.

   해당 인쇄 채널 템플릿(XDP)으로 이동하여 선택한 다음 를 선택합니다 **[!UICONTROL 열기]**.

## 웹 채널 {#web-channel}

템플릿 작성자 및 관리자는 웹 템플릿을 만들고 편집하고 활성화할 수 있습니다. 다른 사용자가 웹 템플릿을 작성할 수 있도록 하려면 해당 사용자에게 권한을 부여해야 합니다. 자세한 내용은 [사용자, 그룹 및 액세스 권한 관리](/help/sites-administering/user-group-ac-admin.md).

### 웹 채널 템플릿 작성 {#authoring-web-channel-template}

웹 채널 템플릿을 만들려면 먼저 템플릿 폴더를 만들어야 합니다. 템플릿 폴더 내에 웹 템플릿을 만든 후에는 양식 사용자가 템플릿을 기반으로 대화형 통신의 웹 채널을 만들 수 있도록 템플릿을 활성화해야 합니다.

웹 채널 템플릿을 작성하려면 다음 단계를 완료하십시오.

1. 대화형 통신 웹 템플릿이 없는 경우 템플릿 폴더를 만들어 유지합니다. 자세한 내용은 의 템플릿 폴더 를 참조하십시오. [페이지 템플릿 - 편집 가능](/help/sites-developing/page-templates-editable.md).

   1. 선택 **[!UICONTROL 도구]** ![도구](assets/tools.png) > **[!UICONTROL 구성 브라우저]**.
      * 다음을 참조하십시오. [구성 브라우저](/help/sites-administering/configurations.md) 설명서 를 참조하십시오.
   1. Configuration Browser 페이지에서 **[!UICONTROL 만들기]**.
   1. 구성 만들기 대화 상자에서 폴더의 제목을 지정하고 을 선택합니다 **[!UICONTROL 편집 가능한 템플릿]**, 및 선택 **[!UICONTROL 만들기]**.

      폴더가 생성되고 [구성 브라우저] 페이지에 나열됩니다.

1. 해당 템플릿 폴더로 이동하여 웹 템플릿을 만듭니다.

   1. 을 선택하여 해당 템플릿 폴더로 이동합니다. **[!UICONTROL 도구]** > **[!UICONTROL 템플릿]** > **`[Folder]`**.
   1. **[!UICONTROL 만들기]**&#x200B;를 선택합니다.
   1. 선택 **[!UICONTROL 대화형 통신 - 웹 채널]** 및 선택 **[!UICONTROL 다음]**.
   1. 템플릿 제목과 설명을 입력한 다음 을 선택합니다. **[!UICONTROL 만들기]**.

      템플릿이 생성되고 대화 상자가 나타납니다.

   1. 선택 **[!UICONTROL 열기]** 템플릿 편집기에서 만든 템플릿을 엽니다.

      템플릿 편집기 가 나타납니다.

      ![webchanneltemplate](assets/webchanneltemplate.png)

      템플릿을 만들거나 편집할 때 템플릿 작성자가 정의할 수 있는 다양한 측면이 있습니다. 템플릿을 만들거나 편집하는 것은 페이지 작성과 유사합니다. 자세한 내용은 템플릿 편집 - 템플릿 작성자 를 참조하십시오. [페이지 템플릿 만들기](/help/sites-authoring/templates.md).

1. 대화형 통신 만들기에 이 템플릿을 사용할 수 있도록 하려면 템플릿을 활성화합니다.

   1. 선택 **[!UICONTROL 도구]** ![도구](assets/tools.png) > **[!UICONTROL 템플릿]**.
   1. 해당 템플릿으로 이동하여 선택한 다음 를 선택합니다 **[!UICONTROL 사용]** 경고 메시지에서 다음을 선택합니다. **[!UICONTROL 사용]**.

      템플릿이 활성화되고 상태가 활성화됨으로 표시됩니다. 이제 새로 만든 웹 채널 템플릿을 사용할 수 있는 대화형 통신을 만들 수 있습니다.

### 웹 채널용 마스터로 인쇄 채널 {#print-channel-as-master-for-web-channel}

작성자는 대화형 통신을 작성하는 동안 이 옵션을 선택하여 인쇄 채널과 동기화된 웹 채널을 만들 수 있습니다. 인쇄 채널을 웹 채널에 대한 마스터로 사용하면 웹 채널의 콘텐츠, 상속 및 데이터 바인딩이 인쇄 채널에서 파생되고 인쇄 채널에서 수행된 변경 사항이 웹 채널에 반영될 수 있습니다. 그러나 대화형 통신 작성자는 필요에 따라 웹 채널에서 특정 구성 요소의 상속을 중단할 수 있습니다.

![채널을 마스터로 인쇄](assets/create_ic_print_master_new.png) ![인쇄 채널을 마스터로 사용하는 웹 채널](assets/create_ic_print_master_web_new.png)
