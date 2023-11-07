---
title: 론치 만들기
description: 론치를 만들어 향후 활성화할 수 있도록 기존 웹 페이지의 새 버전 업데이트를 활성화할 수 있습니다.
uuid: c1a32710-8189-4a2e-bf2f-428ab30d48c8
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 4ec6b408-a165-4617-8d90-e89d8a415bb3
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
exl-id: bc7897da-15f6-4de4-a9fd-9dd84e6c7eed
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1039'
ht-degree: 83%

---

# 론치 만들기{#creating-launches}

론치를 만들어 향후 활성화할 수 있도록 기존 웹 페이지의 새 버전 업데이트를 활성화합니다. 론치를 만들 때에는 제목과 소스 페이지를 지정합니다.

* 제목은 작성자가 액세스하여 작업할 수 있는 [참조](/help/sites-authoring/author-environment-tools.md#references) 레일에 표시됩니다.
* 소스 페이지의 하위 페이지는 기본적으로 론치에 포함됩니다. 원할 경우 소스 페이지만 사용할 수 있습니다.
* 기본적으로, [Live Copy](/help/sites-administering/msm.md)는 소스 페이지 변경에 따라 자동으로 론치 페이지를 업데이트합니다. 정적 사본을 만들어 자동 변경을 방지하도록 지정할 수 있습니다.

필요한 경우 **실행 날짜**(및 시간)를 지정하여 실행 페이지를 홍보 및 활성화할 시기를 정의할 수 있습니다. However the **Launch Date** only operates in combination with the **Production Ready** flag (see [Editing a Launch Configuration](/help/sites-authoring/launches-editing.md#editing-a-launch-configuration)); for the actions to actually occur automatically, both must be set.

## 론치 만들기 {#creating-a-launch}

Sites 또는 론치 콘솔에서 론치를 만들 수 있습니다.

1. **사이트** 또는 **론치** 콘솔을 엽니다.

   >[!NOTE]
   >
   >**Sites** 콘솔을 사용하는 경우 소스 페이지의 위치로 이동하는 것이 일반적이지만, 마법사에서 **론치 소스**&#x200B;를 선택할 때도 소스로 이동할 수 있으므로 필수는 아닙니다.

1. 사용 중인 콘솔에 따라 다음 작업을 수행하십시오.

   * **론치**:

      1. 도구 모음에서 **론치 만들기**&#x200B;를 선택하여 마법사를 엽니다.

   * **사이트**:

      1. 도구 모음에서 **만들기**&#x200B;를 선택하여 선택 상자를 엽니다.
      1. 여기서 **론치 만들기**&#x200B;를 선택하여 마법사를 엽니다.

   >[!NOTE]
   >
   >**사이트** 콘솔에서 **만들기**&#x200B;를 선택하기 전에 [선택 모드](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)를 사용하여 페이지를 선택할 수도 있습니다.
   >
   >이렇게 하면 선택한 페이지가 초기 소스 페이지로 사용됩니다.

1. **소스 선택** 단계에서 **페이지를 추가**&#x200B;해야 합니다. 각각에 대해 경로를 지정하여 여러 페이지를 선택할 수 있습니다.

   * 필요한 위치로 이동합니다.
   * 소스 페이지를 선택하고 확인합니다(확인 표시).

   필요에 따라 반복하십시오.

   ![소스 선택 및 페이지 추가](assets/chlimage_1-225.png)

   >[!NOTE]
   >
   >론치에 페이지 및/또는 분기를 추가하려면 사이트 내에 있어야 합니다(예: 일반적인 최상위 루트 아래).
   >
   >사이트의 최상위 수준 아래에 언어 루트가 있는 경우 론치에 대한 페이지 및 분기는 공통 언어 루트 아래에 있어야 합니다.
   >
   >소스 경로에 상위 또는 하위 페이지가 있는 론치를 만들려고 하면 실패하고 &quot;대상이 :path에 이미 존재함: 페이지에 표시됨&quot; 오류가 반환됩니다.

1. 각 항목에 대해 다음 여부를 지정할 수 있습니다.

   * **하위 페이지 포함**:

      * 하위 페이지를 포함하여 론치를 만들지 아니면 하위 페이지를 포함하지 않고 론치를 만들지 지정합니다. 기본적으로 이 하위 페이지가 포함됩니다.

   **다음**&#x200B;을 선택하여 계속 진행합니다.

   ![페이지 포함 여부 지정](assets/chlimage_1-226.png)

1. 마법사의 **속성** 단계에서 다음을 지정할 수 있습니다.

   * **론치 제목**: 론치의 이름입니다. 작성자에게 의미가 있는 이름이어야 합니다.
   * **기존 콘텐츠 사용**: 론치를 만드는 데 원래 콘텐츠가 사용됩니다.
   * **새 템플릿을 사용하여 페이지 바꾸기**: 자세한 내용은 [새 템플릿을 사용하여 론치 만들기](#create-launch-with-new-template)를 참조하십시오.
   * **소스 페이지의 라이브 데이터 상속**: 이 옵션을 선택하면 소스 페이지를 변경할 때 론치 페이지 콘텐츠가 자동으로 업데이트됩니다. 이 옵션은 론치를 다음으로 만들어 이 작업을 수행합니다. [live copy](/help/sites-administering/msm.md).

     기본적으로 이 옵션은 선택되어 있습니다.

   * **론치 날짜**: 론치 카피가 활성화될 날짜 및 시간입니다(**프로덕션 준비** 플래그에 따라 다름). [론치 - 이벤트 순서](/help/sites-authoring/launches.md#launches-the-order-of-events)를 참조하십시오.

   ![속성 지정](assets/chlimage_1-227.png)

1. **만들기**&#x200B;를 사용하여 프로세스를 완료하고 새 론치를 만듭니다. 확인 대화 상자를 통해 론치를 즉시 열지 여부를 묻게 됩니다.

   **완료**&#x200B;를 사용하여 콘솔로 돌아가면 다음에서 론치를 보고 액세스할 수 있습니다.

   * [****&#x200B;론치 콘솔](/help/sites-authoring/launches.md#the-launches-console)
   * 다음 [**참조** 다음에서 **사이트** 콘솔](/help/sites-authoring/launches.md#launches-in-references-sites-console)

### 새 템플릿을 사용하여 론치 만들기 {#create-launch-with-new-template}

날짜 [론치 만들기](/help/sites-authoring/launches-creating.md#create-launch-with-new-template) 옵션을 사용하여 새 템플릿을 사용할지 여부를 선택할 수 있습니다. **새 템플릿을 사용하여 페이지 바꾸기**

>[!CAUTION]
>
>이 옵션은 **사이트** 콘솔에서 론치를 만들 때만 사용할 수 있습니다. **론치** 콘솔에서 론치를 만들 때는 사용할 수 없습니다.

![새 템플릿을 사용하여 페이지 바꾸기](assets/chlimage_1-228.png)

이 옵션을 선택하면 다음이 수행됩니다.

* 사용 가능한 다른 옵션 업데이트,
* 필요한 템플릿을 선택할 수 있는 새 단계를 포함합니다.

![템플릿 선택](assets/chlimage_1-229.png)

>[!CAUTION]
>
>다른 템플릿을 사용하면 새 페이지가 비어 있습니다. 다른 페이지 구조로 인해 콘텐츠가 복사되지 않습니다.
>
>이 메커니즘을 사용하면 [기존 페이지](/help/sites-authoring/managing-pages.md#creating-a-new-page)의 템플릿을 변경할 수 있습니다. 단, 콘텐츠 손실을 고려해야 합니다.

### 중첩 론치 만들기 {#creating-a-nested-launch}

중첩 론치(론치 내 론치)를 만들면 기존 론치에서 론치를 만들 수 있으므로, 작성자가 각 론치에 대해 동일한 변경을 여러 번 수행하지 않고, 이미 수행된 변경 사항을 활용할 수 있습니다.

>[!NOTE]
>
>[중첩 론치 홍보](/help/sites-authoring/launches-promoting.md#promoting-a-nested-launch)도 참조하십시오.

#### 중첩 론치 만들기 - 론치 콘솔 {#creating-a-nested-launch-launches-console}

**론치** 콘솔에서 중첩 론치를 만드는 것은 다른 형식의 론치를 만드는 것과 기본적으로 동일하지만, 이 경우에는 예외적으로 론치 분기(`/content/launches`)로 이동해야 합니다.

1. **론치** 콘솔에서 **만들기**&#x200B;를 선택합니다.
1. Select **Add Pages**, then navigate to the launches branch by specifying `/content/launches` in the filter. 필요한 론치를 선택하고 **선택**&#x200B;을 사용하여 확인합니다.

   ![시작 선택](assets/chlimage_1-230.png)

1. 다음으로 진행 **다음** 다음을 완료합니다. **속성** 다른 론치와 마찬가지로

   ![속성 지정](assets/chlimage_1-231.png)

#### 중첩 론치 만들기 - Sites 콘솔 {#creating-a-nested-launch-sites-console}

기존 론치를 기준으로 **사이트** 콘솔에서 중첩 실행을 만들려면 다음 작업을 수행하십시오.

1. [참조의 론치(Sites 콘솔)](/help/sites-authoring/launches.md#launches-in-references-sites-console)에 액세스하여 사용 가능한 동작을 표시합니다.
1. **론치 만들기**&#x200B;를 선택하여 마법사를 엽니다. 소스는 이미 선택했으므로 **소스 선택** 단계로 넘어갑니다.

1. **론치 제목** 및 기타 필수 세부 정보를 입력합니다(일반 론치의 경우와 같음).

1. **만들기**&#x200B;를 사용하여 프로세스를 완료하고 새 론치를 만듭니다. 확인 대화 상자를 통해 론치를 즉시 열지 여부를 묻게 됩니다.

   **완료**&#x200B;를 선택하면 **사이트** 콘솔의 **참조** 레일로 돌아가며, 적절한 페이지를 선택하면 새 론치가 표시됩니다.

### 론치 삭제 {#deleting-a-launch}

[론치 콘솔](/help/sites-authoring/launches.md#the-launches-console)에서 론치를 삭제할 수 있습니다.

* 썸네일을 탭/클릭하여 론치를 선택합니다.
* 도구 모음이 표시됩니다. 삭제를 선택합니다.
* 동작을 확인합니다.

>[!CAUTION]
>
>론치를 삭제하면 론치 자체 및 모든 하위 중첩 론치가 제거됩니다.
