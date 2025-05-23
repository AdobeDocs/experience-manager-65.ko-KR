---
title: 자산 선택기
description: 에셋 선택기를 사용하여 Adobe Experience Manager Assets 내의 에셋에 대한 메타데이터를 검색, 필터링, 검색 및 가져오는 방법을 알아봅니다. 자산 선택기 인터페이스를 사용자 지정하는 방법도 알아봅니다.
contentOwner: Adobe
feature: Asset Management,Metadata,Search
role: User
hide: true
exl-id: c84ce84a-1e52-48fd-a16c-38c7769df9af
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 2%

---

# 자산 선택기 {#asset-selector}

>[!NOTE]
>
>[!DNL Experience Manager] 이전 버전에서 [자산 선택기](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/asset-selector.html?lang=ko)을(를) [자산 선택기](https://helpx.adobe.com/kr/experience-manager/6-2/assets/using/asset-picker.html)이라고 했습니다.

에셋 선택기를 사용하여 [!DNL Adobe Experience Manager] Assets에서 에셋을 검색 및 필터링할 수 있습니다. 에셋 선택기를 사용하여 선택한 에셋의 메타데이터를 가져올 수도 있습니다. 자산 선택기 인터페이스를 사용자 지정하려면 지원되는 요청 매개 변수와 함께 자산 선택기 인터페이스를 시작할 수 있습니다. 이러한 매개 변수는 특정 시나리오에 대한 에셋 선택기의 컨텍스트를 설정합니다.

현재 선택 전체에서 그대로 유지되는 자산 선택기에 대한 컨텍스트 정보로 요청 매개 변수 `assettype`(*이미지/비디오/텍스트*) 및 선택 `mode`(*단일/다중*)을 전달할 수 있습니다.

에셋 선택기는 HTML5 **Window.postMessage** 메시지를 사용하여 선택한 에셋에 대한 데이터를 받는 사람에게 보냅니다.

에셋 선택기는 Granite의 기초 선택기 어휘를 기반으로 합니다. 기본적으로 에셋 선택기는 검색 모드에서 작동합니다. 그러나 Omnisearch 경험을 사용하여 필터를 적용하여 특정 에셋에 대한 검색을 구체화할 수 있습니다.

CQ 컨테이너의 일부인지 여부에 관계없이 모든 웹 페이지를 자산 선택기(`https://[AEM_server]:[port]/aem/assetpicker.html`)와 통합할 수 있습니다.

## 컨텍스트 매개 변수 {#contextual-parameters}

URL에 다음 요청 매개 변수를 전달하여 특정 컨텍스트에서 자산 선택기를 실행할 수 있습니다.

| 이름 | 값 | 예 | 용도 |
|---|---|---|---|
| 리소스 접미사(B) | URL의 리소스 접미사 폴더 경로: `http://localhost:4502/aem/`<br>`assetpicker.html/<folder_path>` | 특정 폴더가 선택된 상태로 에셋 선택기를 시작하려면(예: `/content/dam/we-retail/en/activities` 폴더가 선택된 상태로) URL의 형식이 `http://localhost:4502/aem/assetpicker.html`<br>`/content/dam/we-retail/en/activities?assettype=images`이어야 합니다. | 자산 선택기를 시작할 때 특정 폴더를 선택해야 하는 경우 리소스 접미사로 전달합니다. |
| 모드 | 단일, 다중 | `http://localhost:4502/aem/assetpicker.html`<br>`?mode=multiple` <br> `http://localhost:4502/aem/assetpicker.html`<br>`?mode=single` | 다중 모드에서는 에셋 선택기를 사용하여 여러 에셋을 동시에 선택할 수 있습니다. |
| 대화 상자 | true, false | `http://localhost:4502/aem/assetpicker.html`<br>`?dialog=true` | 이러한 매개 변수를 사용하여 자산 선택기를 [Granite] 대화 상자로 엽니다. 이 옵션은 Granite 경로 필드를 통해 자산 선택기를 시작하고 pickerSrc URL로 구성하는 경우에만 적용할 수 있습니다. |
| 루트 | `<folder_path>` | `http://localhost:4502/aem/`<br>`assetpicker.html?assettype=images`<br>`&root=/content/dam/we-retail/en/activities` | 이 옵션을 사용하여 자산 선택기의 루트 폴더를 지정합니다. 이 경우 에셋 선택기를 사용하면 루트 폴더 아래에서 하위 에셋(직접/간접)만 선택할 수 있습니다. |
| 보기 모드 | 검색 |  | assettype 및 mimetype 매개 변수와 함께 검색 모드에서 자산 선택기를 시작합니다. |
| assettype(S) | 이미지, 문서, 멀티미디어, 아카이브 | <ul><li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=images`</li> <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=documents`</li> <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=multimedia`</li> <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=archives`</li> | 전달된 값을 기반으로 자산 유형을 필터링하려면 이 옵션을 사용합니다. |
| mimetype | 자산의 mimetype(`/jcr:content/metadata/dc:format`)(와일드카드도 지원됨) | <ul><li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&mimetype=image/png`</li>  <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&?mimetype=*png`</li>  <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&mimetype=*presentation`</li>  <li>`http://localhost:4502/aem/assetpicker?viewmode=search&mimetype=*presentation&mimetype=*png`</li></ul> | MIME 유형을 기반으로 자산을 필터링하는 데 사용합니다. |

## 자산 선택기 사용 {#using-the-asset-selector}

1. 자산 선택기 인터페이스에 액세스하려면 `https://[AEM_server]:[port]/aem/assetpicker`(으)로 이동하십시오.
1. 원하는 폴더로 이동하고 하나 이상의 에셋을 선택합니다.

   ![chlimage_1-441](assets/chlimage_1-441.png)

   또는 OmniSearch 상자에서 원하는 에셋을 검색한 다음 선택할 수 있습니다.

   ![chlimage_1-442](assets/chlimage_1-442.png)

   OmniSearch 상자를 사용하여 자산을 검색하는 경우 **[!UICONTROL 필터]** 창에서 다양한 필터를 선택하여 검색을 구체화할 수 있습니다.

   ![chlimage_1-443](assets/chlimage_1-443.png)

1. 도구 모음에서 **[!UICONTROL 선택]**&#x200B;을 클릭합니다.

>[!MORELIKETHIS]
>
>* AEM as a Cloud Service의 [Micro-Frontend 자산 선택기](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/asset-selector.html?lang=ko)
