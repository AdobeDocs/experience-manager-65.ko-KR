---
title: 론치 만들기
seo-title: 론치 만들기
description: 론치를 만들어 향후 활성화할 수 있도록 기존 웹 페이지의 새 버전 업데이트를 활성화할 수 있습니다. 론치를 만들 때에는 제목과 소스 페이지를 지정합니다.
seo-description: 론치를 만들어 향후 활성화할 수 있도록 기존 웹 페이지의 새 버전 업데이트를 활성화할 수 있습니다. 론치를 만들 때에는 제목과 소스 페이지를 지정합니다.
uuid: e67608a9-e6c9-42f3-bd1d-63a5fa87ae18
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 48826f03-6731-49c5-a6c5-6e2fb718f912
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
translation-type: tm+mt
source-git-commit: 016c705230dffec052c200b058a36cdbe0520fc4
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 86%

---


# 론치 만들기{#creating-launches}

론치를 만들어 향후 활성화할 수 있도록 기존 웹 페이지의 새 버전 업데이트를 활성화할 수 있습니다. 론치를 만들 때에는 제목과 소스 페이지를 지정합니다:

* 제목은 작성자가 액세스하여 작업할 수 있는 **사이드 킥이**&#x200B;에 나타납니다.
* 소스 페이지의 하위 페이지는 기본적으로 론치에 포함됩니다. 원할 경우 소스 페이지만 사용할 수 있습니다.
* 기본적으로, [Live Copy](/help/sites-administering/msm.md)는 소스 페이지 변경에 따라 자동으로 론치 페이지를 업데이트합니다. 정적 복사본을 만들어 자동 변경을 방지하도록 지정할 수 있습니다.

필요에 따라 **론치 날짜**(및 시간)를 지정하여 론치 페이지가 홍보되고 활성화되는 시기를 정의할 할 수 있습니다. 그러나 **론치 날짜**&#x200B;는 **프로덕션 준비** 플래그와 조합하여 작동합니다([론치 구성 편집](/help/sites-classic-ui-authoring/classic-launches-editing.md#editing-a-launch-configuration) 참조).작업이 실제로 자동으로 수행되도록 하려면 둘 다 설정해야 합니다.

## 론치 만들기 {#creating-a-launch}

다음 절차에서는 론치가 만들어집니다.

1. 웹 사이트 관리 페이지([http://localhost:4502/siteadmin](http://localhost:4502/siteadmin))를 엽니다.
1. **새로 만들기...**&#x200B;를 클릭한 다음, **새 론치...**&#x200B;를 클릭합니다.
1. **론치 만들기** 대화 상자에서, 다음 속성에 대한 값을 지정합니다.

   * **론치 제목**: 론치의 이름입니다. 작성자에게 의미가 있는 이름이어야 합니다.
   * **소스 페이지**: 론치를 만들 페이지 경로. 기본적으로 모든 하위 페이지가 포함되어 있습니다.
   * **하위 페이지 제외**: 이 선택 사항을 선택하면 소스 페이지에 대한 론치만 만들고 하위 페이지에 대해서는 만들지 않습니다. 기본적으로 이 선택 사항은 선택되어 있지 않습니다.
   * ****&#x200B;동기화 유지: 이 옵션을 선택하면, 소스 페이지가 변경될 때 론치 페이지 내용이 자동으로 업데이트됩니다. 이것은 론치를 [Live Copy](/help/sites-administering/msm.md)로 만듦으로써 성취됩니다.
   * **론치 날짜**: 론치 카피가 활성화될 날짜 및 시간입니다(**프로덕션 준비** 플래그에 따라 다름) [론치 - 이벤트 순서](/help/sites-authoring/launches.md#launches-the-order-of-events)를 참조하십시오.

   ![chlimage_1-99](assets/chlimage_1-99a.png)

1. **만들기**&#x200B;를 클릭합니다.

## 론치 삭제 {#deleting-a-launch}

론치를 삭제할 수도 있습니다.

1. [론치 콘솔](/help/sites-classic-ui-authoring/classic-launches.md)에서 필요한 론치를 선택합니다.
1. **삭제**&#x200B;를 클릭합니다. 삭제할 것임을 확인해야 합니다.

   ![chlimage_1-100](assets/chlimage_1-100a.png)

   >[!CAUTION]
   >
   >중첩된 론치를 삭제할 때에는 낮은 수준을 먼저 삭제해야 합니다.

