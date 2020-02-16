---
title: 적응형 양식 자동 저장
seo-title: 적응형 양식 자동 저장
description: 이벤트 또는 사전 정의된 시간 간격에 따라 컨텐츠 저장을 자동으로 시작하도록 적응형 양식을 구성할 수 있습니다
seo-description: 이벤트 또는 사전 정의된 시간 간격에 따라 컨텐츠 저장을 자동으로 시작하도록 적응형 양식을 구성할 수 있습니다
uuid: 0fe9a389-269b-438a-9489-d9d1d09558a1
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: d519ac4e-6d29-4a69-874e-792acabe87ff
translation-type: tm+mt
source-git-commit: 3eaace94bc0499aaebfcd389d4dc97b97c7d9160

---


# 적응형 양식 자동 저장 {#auto-save-an-adaptive-form}

이벤트 또는 사전 정의된 시간 간격에 따라 컨텐츠 저장을 자동으로 시작하도록 적응형 양식을 구성할 수 있습니다. 기본적으로 응용 양식의 내용은 저장 단추 누르기와 같은 사용자 작업에 저장됩니다. 자동 저장 옵션은 다음 경우에 유용합니다.

* 익명 사용자와 로그인한 사용자를 위해 컨텐츠를 자동으로 저장
* 사용자의 개입 없이도 양식 컨텐츠 저장
* 사용자 이벤트에 따라 양식의 내용 저장 시작
* 지정된 시간 간격 후에 양식의 내용 반복 저장

## 적응형 양식에 대해 자동 저장 사용 {#enable-autosave-for-an-adaptive-form}

적응형 양식의 경우 자동 저장 옵션은 즉시 사용할 수 없습니다. 적응형 양식의 속성에 있는 자동 **저장** 섹션에서 자동 저장 옵션을 활성화할 수 있습니다. 자동 **저장** 섹션은 다른 구성 옵션도 제공합니다. 적응형 양식에 대해 자동 저장 옵션을 활성화하고 구성하려면 다음 단계를 수행하십시오.

1. 속성의 자동 저장 섹션에 액세스하려면 구성 요소를 선택한 다음 ![필드 수준](assets/field-level.png) > 적응형 양식 **[!UICONTROL 컨테이너를]**&#x200B;탭한 ![다음](assets/cmppr.png)cmppr을탭합니다.
1. 자동 **[!UICONTROL 저장]** 섹션에서 **[!UICONTROL 자동]** 저장 옵션을 활성화합니다.
1. [응용 **[!UICONTROL 양식 이벤트]** ] 상자에서 1이나 TRUE를 지정하여 양식을 브라우저에 로드할 때 자동으로 양식 저장을 시작합니다. 이벤트에 대한 조건부 표현식을 지정할 수도 있습니다. 이 표현식은 트리거되고 true가 반환되면 양식의 내용 저장을 시작합니다.
1. 트리거를 지정합니다. 자동 저장은 구성에 따라 트리거됩니다. 옵션은 다음과 같습니다.

   * **** 시간 기반:특정 시간 간격에 따라 컨텐츠 저장을 시작하는 옵션을 선택합니다.
   * **** 이벤트 기반:이벤트가 트리거될 때 컨텐츠 저장을 시작하는 옵션을 선택합니다.
   트리거를 선택하면 전략 구성 상자가 활성화됩니다. 전략 구성 상자를 사용하여 다음을 수행할 수 있습니다.

   * 시간 기반 **** 트리거를 선택하는 경우 시간 간격을 지정합니다.
   * 이벤트 기반 **** 트리거를 선택하는 경우 이벤트 이름을 지정합니다.
   사용자 지정 전략을 만들어 목록에 추가할 수도 있습니다. 자세한 내용은 [사용자 지정 전략을 구현하여 양식을](/help/forms/using/auto-save-an-adaptive-form.md#p-implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms-p)자동 저장을 참조하십시오.

1. (시간 기반 자동 저장만 해당) 다음 단계를 수행하여 시간 기반 자동 저장에 대한 옵션을 구성합니다.

   1. 이 **[!UICONTROL 간격]** 자동 저장 상자에서 시간 간격(초)을 지정합니다. 간격 상자에 지정된 시간(초)이 경과하면 양식이 반복적으로 저장됩니다.

1. (이벤트 기반 자동 저장만 해당) 다음 단계를 수행하여 이벤트 기반 자동 저장에 대한 옵션을 구성합니다.

   1. 이 **이벤트** 후 자동 저장 상자에서 GuideBridge [이벤트를 지정합니다](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html) . 표현식이 TRUE로 평가될 때마다 양식이 저장됩니다.

1. (선택 사항) 익명 사용자를 위해 컨텐츠를 자동으로 저장하려면 익명 사용자를 **위해** 자동 저장 활성화 옵션을 선택하고 확인을 **[!UICONTROL 클릭합니다]**.

   >[!NOTE]
   >
   >자동 저장 옵션이 익명의 사용자에게 작동하려면 모든 사용자가 양식을 미리 보고, 확인하고, 서명할 수 있도록 Forms Common Configuration Service를 구성해야 합니다.
   >
   >서비스를 구성하려면 에서 AEM Web Console 구성으로 이동한 `https://[server]:[host]/system/console/configMgr` 후 **[!UICONTROL Forms Common Configuration Service를]** 편집하여 허용 **[!UICONTROL 필드에서]** 모든 사용자 **[!UICONTROL 옵션을]** 선택하고구성을 저장합니다.

## 사용자 지정 전략을 구현하여 적응형 양식에 대한 자동 저장 활성화 {#implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms}

사용자 지정 이벤트를 구현하여 자동 저장 기능을 트리거할 수 있습니다. 다음 단계를 수행하여 사용자 지정 이벤트를 만들고 구현합니다.

1. 클라이언트 라이브러리 및 클라이언트 라이브러리 폴더를 만듭니다. 자세한 내용은 클라이언트측 라이브러리 [사용 문서를](/help/sites-developing/clientlibs.md)참조하십시오.

   예를 들어 다음 스크립트는 사용자 지정 `emailFocusChange`이벤트를 사용하여 자동 저장 기능을 트리거합니다.

   ```
   window.addEventListener("bridgeInitializeStart", function (){
       guideBridge.connect(function () { guideBridge.on("elementFocusChanged", function (event,data) {
           if(data.target.name === 'Email') {
               guideBridge.trigger("emailFocusChange");
           }
       });
      });
   });
   ```

   >[!NOTE]
   >
   >category 속성은 클라이언트 라이브러리 폴더를 만드는 동안 정의됩니다. 카테고리 속성에 할당된 값을 가까이 유지할 수 있습니다.

1. 작성 모드에서 응용 양식을 엽니다.

1. 편집 모드에서 구성 요소를 선택한 다음 ![필드 수준](assets/field-level.png) > 적응형 양식 **[!UICONTROL 컨테이너를]**&#x200B;탭한 다음 ![cmppr](assets/cmppr.png)을누릅니다.
1. 속성에서 기본 **[!UICONTROL 섹션을 엽니다]** . [ **[!UICONTROL 클라이언트 라이브러리]** 범주] 상자에 클라이언트 라이브러리 폴더를 만들 때 정의된 category 속성의 값을 입력합니다.
1. 자동 저장 섹션을 엽니다. 이 **[!UICONTROL 이벤트]** 후 자동 저장 상자에서 클라이언트 라이브러리에 이미 정의된 사용자 지정 이벤트를 지정합니다. **[!UICONTROL 확인]**&#x200B;을 클릭합니다.

