---
title: 적응형 양식 자동 저장
description: 이벤트 또는 사전 정의된 시간 간격에 따라 콘텐츠 저장을 자동으로 시작하도록 적응형 양식을 구성할 수 있습니다
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
feature: Adaptive Forms,Foundation Components
exl-id: ff9bf466-228d-40e6-9389-15c1f2ed1d2e
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 7%

---

# 적응형 양식 자동 저장 {#auto-save-an-adaptive-form}

<span class="preview"> [새 적응형 양식 만들기](/help/forms/using/create-an-adaptive-form-core-components.md) 또는 [AEM Sites 페이지에 적응형 양식 추가](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md) 작업을 할 때 현대적이고 확장 가능한 데이터 캡처 [핵심 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ko)를 사용하는 것이 좋습니다. 이러한 구성 요소는 적응형 양식 만들기 작업이 대폭 개선되어 우수한 사용자 경험을 보장할 수 있게 되었음을 나타냅니다. 이 문서에서는 기초 구성 요소를 사용하여 적응형 양식을 작성하는 이전 접근법에 대해 설명합니다. </span>

이벤트 또는 사전 정의된 시간 간격에 따라 콘텐츠 저장을 자동으로 시작하도록 적응형 양식을 구성할 수 있습니다. 기본적으로 적응형 양식의 콘텐츠는 저장 버튼을 누르는 것과 같은 사용자 작업 시 저장됩니다. 자동 저장 옵션은 다음 경우에 유용합니다.

* 익명 및 로그인한 사용자를 위한 콘텐츠 자동 저장
* 사용자 개입 없이 또는 최소한의 양식 콘텐츠 저장
* 사용자 이벤트를 기반으로 양식의 콘텐츠 저장 시작
* 지정된 시간 간격 후 반복적으로 양식 콘텐츠 저장

## 적응형 양식에 대해 자동 저장 활성화 {#enable-autosave-for-an-adaptive-form}

적응형 양식의 경우 자동 저장 옵션이 즉시 활성화되지 않습니다. 적응형 양식의 속성에서 **자동 저장** 섹션에서 자동 저장 옵션을 활성화할 수 있습니다. **자동 저장** 섹션에는 다른 몇 가지 구성 옵션도 있습니다. 적응형 양식에 대해 자동 저장 옵션을 활성화하고 구성하려면 다음 단계를 수행하십시오.

1. 속성의 자동 저장 섹션에 액세스하려면 구성 요소를 선택한 다음 ![필드 수준](assets/field-level.png) > **[!UICONTROL 적응형 양식 컨테이너]**&#x200B;를 선택하고 ![cmpr](assets/cmppr.png)을 선택합니다.
1. **[!UICONTROL 자동 저장]** 섹션에서 자동 저장 옵션을 **[!UICONTROL 활성화]**&#x200B;합니다.
1. **[!UICONTROL 적응형 양식 이벤트]** 상자에서 1 또는 TRUE를 지정하여 양식을 브라우저에 로드할 때 자동으로 양식 저장을 시작합니다. 이벤트에 대해 트리거되고 true를 반환하면 양식의 콘텐츠 저장을 시작하는 조건식을 지정할 수도 있습니다.
1. [트리거]를 지정합니다. 자동 저장은 구성에 따라 트리거됩니다. 옵션은 다음과 같습니다.

   * **[!UICONTROL 시간 기준:]** 특정 시간 간격을 기준으로 콘텐츠 저장을 시작하려면 옵션을 선택하십시오.
   * **[!UICONTROL 이벤트 기반:]** 이벤트가 트리거될 때 콘텐츠 저장을 시작하려면 옵션을 선택하십시오.

   트리거를 선택하면 전략 구성 상자가 활성화됩니다. 전략 구성 상자를 사용하면 다음 작업을 수행할 수 있습니다.

   * **[!UICONTROL 시간 기반]** 트리거를 선택하는 경우 시간 간격을 지정하십시오.
   * **[!UICONTROL 이벤트 기반]** 트리거를 선택하는 경우 이벤트 이름을 지정하십시오.

   사용자 지정 전략을 만들어 목록에 추가할 수도 있습니다. 자세한 내용은 [양식을 자동으로 저장하는 사용자 지정 전략 구현](/help/forms/using/auto-save-an-adaptive-form.md#p-implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms-p)을 참조하십시오.

1. (시간 기반 자동 저장만 해당) 다음 단계를 수행하여 시간 기반 자동 저장에 대한 옵션을 구성합니다.

   1. **[!UICONTROL 이 간격에 자동 저장]** 상자에서 시간 간격을 초 단위로 지정합니다. 간격 상자에 지정된 초 수가 경과하면 양식이 반복적으로 저장됩니다.

1. (이벤트 기반 자동 저장만 해당) 다음 단계를 수행하여 이벤트 기반 자동 저장에 대한 옵션을 구성합니다.

   1. **이 이벤트 후 자동 저장** 상자에서 [GuideBridge](https://helpx.adobe.com/kr/aem-forms/6/javascript-api/GuideBridge.html) 이벤트를 지정합니다. 표현식이 TRUE로 평가될 때마다 양식이 저장됩니다.

1. (선택 사항) 익명 사용자에 대한 콘텐츠를 자동으로 저장하려면 **익명 사용자에 대한 자동 저장 사용** 옵션을 선택하고 **[!UICONTROL 확인]**&#x200B;을 클릭합니다.

   >[!NOTE]
   >
   >익명 사용자에 대해 자동 저장 옵션이 작동하려면 모든 사용자가 양식을 미리 보고, 확인하고, 서명할 수 있도록 Forms 일반 구성 서비스를 구성해야 합니다.
   >
   >서비스를 구성하려면 `https://server:port/system/console/configMgr`의 AEM Web Console 구성으로 이동하여 **[!UICONTROL Forms 일반 구성 서비스]**&#x200B;를 편집하여 **[!UICONTROL 허용]** 필드에서 **[!UICONTROL 모든 사용자]** 옵션을 선택한 다음 구성을 저장합니다.

## 적응형 양식에 대해 자동 저장을 활성화하기 위한 사용자 지정 전략 구현 {#implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms}

사용자 지정 이벤트를 구현하여 자동 저장 기능을 트리거할 수 있습니다. 사용자 지정 이벤트를 만들고 구현하려면 다음 단계를 수행하십시오.

1. 클라이언트 라이브러리 및 클라이언트 라이브러리 폴더를 만듭니다. 자세한 단계는 [클라이언트측 라이브러리 사용 문서](/help/sites-developing/clientlibs.md)를 참조하십시오.

   예를 들어 다음 스크립트는 사용자 지정 `emailFocusChange`이벤트를 사용하여 자동 저장 기능을 트리거합니다.

   ```javascript
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
   >클라이언트 라이브러리 폴더를 만드는 동안 범주 속성이 정의됩니다. 범주 속성에 할당된 값을 바로 사용할 수 있습니다.

1. 작성자 모드에서 적응형 양식을 엽니다.

1. 편집 모드에서 구성 요소를 선택한 다음 ![필드 수준](assets/field-level.png) > **[!UICONTROL 적응형 양식 컨테이너]**&#x200B;를 선택하고 ![cmpr](assets/cmppr.png)을 선택합니다.
1. 속성에서 **[!UICONTROL 기본]** 섹션을 엽니다. **[!UICONTROL 클라이언트 라이브러리 범주]** 상자에 클라이언트 라이브러리 폴더를 만드는 동안 정의된 범주 속성 값을 입력합니다.
1. 자동 저장 섹션을 엽니다. **[!UICONTROL 이 이벤트 후 자동 저장]** 상자에서 클라이언트 라이브러리에 이미 정의된 사용자 지정 이벤트를 지정합니다. **[!UICONTROL 확인]**&#x200B;을 클릭합니다.
