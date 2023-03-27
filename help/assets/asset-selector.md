---
title: 자산 선택기
description: 자산 선택기를 사용하여 Adobe Experience Manager Assets 내에서 자산에 대한 메타데이터를 검색, 필터링, 탐색 및 가져오는 방법을 알아봅니다. 자산 선택기 인터페이스를 사용자 지정하는 방법도 알아봅니다.
contentOwner: Adobe
feature: Asset Management,Metadata,Search
role: User
exl-id: 4b518ac0-5b8b-4d61-ac31-269aa1f5abe4
source-git-commit: 0c6c269e9f0cbdcc0c5e3b925ef09b9923cbb2b3
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 1%

---

# 자산 선택기 {#asset-selector}

>[!NOTE]
>
>자산 선택기가 호출되었습니다 [자산 선택기](https://helpx.adobe.com/experience-manager/6-2/assets/using/asset-picker.html) 이전 버전의 [!DNL Experience Manager].

자산 선택기에서 자산을 탐색, 검색 및 필터링할 수 있습니다 [!DNL Adobe Experience Manager] 자산. 자산 선택기를 사용하여 선택한 자산의 메타데이터를 가져올 수도 있습니다. 자산 선택기 인터페이스를 사용자 지정하기 위해 지원되는 요청 매개 변수로 시작할 수 있습니다. 이러한 매개 변수는 특정 시나리오에 대한 자산 선택기의 컨텍스트를 설정합니다.

현재 요청 매개 변수를 전달할 수 있습니다 `assettype` (*이미지/비디오/텍스트*) 및 선택 `mode` (*단일/다중*)를 자산 선택기의 컨텍스트 정보로서, 선택 영역 전체에서 그대로 유지됩니다.

자산 선택기에서 HTML 5을 사용합니다 **Window.postMessage** 선택한 자산의 데이터를 수신자에게 보내는 메시지입니다.

자산 선택기는 Granite의 기초 선택기 어휘를 기반으로 합니다. 기본적으로 자산 선택기는 검색 모드에서 작동합니다. 그러나 Omnisearch 경험을 사용하여 필터를 적용하여 특정 자산에 대한 검색을 개선할 수 있습니다.

자산 선택기(`https://[AEM_server]:[port]/aem/assetpicker.html`).

## 컨텍스트 매개 변수 {#contextual-parameters}

URL에 다음 요청 매개 변수를 전달하여 특정 컨텍스트에서 자산 선택기를 시작할 수 있습니다.

| 이름 | 값 | 예 | 용도 |
|---|---|---|---|
| 리소스 접미사(B) | 폴더 경로는 URL에 리소스 접미사로 사용됩니다.`http://localhost:4502/aem/`<br>`assetpicker.html/<folder_path>` | 예를 들어 폴더를 선택한 특정 폴더가 있는 자산 선택기를 시작하려면 `/content/dam/we-retail/en/activities` 선택한 경우 URL은 다음과 같은 형식이어야 합니다. `http://localhost:4502/aem/assetpicker.html`<br>`/content/dam/we-retail/en/activities?assettype=images` | 자산 선택기를 시작할 때 특정 폴더를 선택해야 하는 경우 이 폴더를 리소스 접미사로 전달합니다. |
| 모드 | 단일, 다중 | `http://localhost:4502/aem/assetpicker.html`<br>`?mode=multiple` <br> `http://localhost:4502/aem/assetpicker.html`<br>`?mode=single` | 여러 모드에서 자산 선택기를 사용하여 여러 자산을 동시에 선택할 수 있습니다. |
| 사용할 수 없게 됩니다 | true, false | `http://localhost:4502/aem/assetpicker.html`<br>`?dialog=true` | 이러한 매개 변수를 사용하여 자산 선택기를 Granite 대화 상자로 엽니다. 이 옵션은 Granite Path Field를 통해 자산 선택기를 시작하고 pickerSrc URL로 구성하는 경우에만 적용할 수 있습니다. |
| 루트 | `<folder_path>` | `http://localhost:4502/aem/`<br>`assetpicker.html?assettype=images`<br>`&root=/content/dam/we-retail/en/activities` | 이 옵션을 사용하여 자산 선택기의 루트 폴더를 지정합니다. 이 경우 자산 선택기를 사용하여 루트 폴더 아래에 하위 자산(직접/간접)만 선택할 수 있습니다. |
| 보기 모드 | 검색 |  | 자산 유형 및 MIME 유형 매개 변수와 함께 검색 모드에서 자산 선택기를 실행하려면 |
| 자산 유형(S) | 이미지, 문서, 멀티미디어, 아카이브 | <ul><li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=images`</li> <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=documents`</li> <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=multimedia`</li> <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=archives`</li> | 전달된 값에 따라 자산 유형을 필터링하려면 이 옵션을 사용합니다. |
| mime 유형 | mime 유형(`/jcr:content/metadata/dc:format`)( 와일드카드가 지원됨) | <ul><li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&mimetype=image/png`</li>  <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&?mimetype=*png`</li>  <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&mimetype=*presentation`</li>  <li>`http://localhost:4502/aem/assetpicker?viewmode=search&mimetype=*presentation&mimetype=*png`</li></ul> | MIME 유형에 따라 자산을 필터링하려면 이 함수를 사용하십시오 |

## 자산 선택기 사용 {#using-the-asset-selector}

1. 자산 선택기 인터페이스에 액세스하려면 다음 위치로 이동하십시오. `https://[AEM_server]:[port]/aem/assetpicker`.
1. 원하는 폴더로 이동하고 하나 이상의 자산을 선택합니다.

   ![chlimage_1-441](assets/chlimage_1-441.png)

   또는 OmniSearch 상자에서 원하는 자산을 검색한 다음 선택할 수 있습니다.

   ![chlimage_1-442](assets/chlimage_1-442.png)

   OmniSearch 상자를 사용하여 자산을 검색하는 경우, **[!UICONTROL 필터]** 창을 사용하여 검색을 세분화할 수 있습니다.

   ![chlimage_1-443](assets/chlimage_1-443.png)

1. 탭/클릭 **[!UICONTROL 선택]** 를 클릭합니다.
