---
title: 론치 만들기
description: 론치를 만들어 향후 활성화할 수 있도록 기존 웹 페이지의 새 버전 업데이트를 활성화합니다. 론치를 만들 때는 제목과 소스 페이지를 지정합니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
exl-id: 8ab21067-c19a-4faa-8bf0-cd9f21f6df70
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 55%

---

# 론치 만들기{#creating-launches}

론치를 만들어 향후 활성화할 수 있도록 기존 웹 페이지의 새 버전 업데이트를 활성화합니다. 론치를 만들 때에는 제목과 소스 페이지를 지정합니다.

* 제목은 작성자가 액세스하여 작업할 수 있는 **Sidekick**&#x200B;에 표시됩니다.
* 소스 페이지의 하위 페이지는 기본적으로 론치에 포함됩니다. 원할 경우 소스 페이지만 사용할 수 있습니다.
* 기본적으로, [Live Copy](/help/sites-administering/msm.md)는 소스 페이지 변경에 따라 자동으로 론치 페이지를 업데이트합니다. 정적 사본을 만들어 자동 변경을 방지하도록 지정할 수 있습니다.

필요한 경우 **실행 날짜**(및 시간)를 지정하여 실행 페이지를 홍보 및 활성화할 시기를 정의할 수 있습니다. However the **Launch Date** only operates in combination with the **Production Ready** flag (see [Editing a Launch Configuration](/help/sites-classic-ui-authoring/classic-launches-editing.md#editing-a-launch-configuration)); for the actions to actually occur automatically, both must be set.

## 론치 만들기 {#creating-a-launch}

다음 절차에서는 론치를 만듭니다.

1. 웹 사이트 관리 페이지([http://localhost:4502/siteadmin](http://localhost:4502/siteadmin))를 엽니다.
1. **새로 만들기..**&#x200B;를 클릭한 다음 **새 시작...**&#x200B;을 클릭합니다.
1. **시작 만들기** 대화 상자에서 다음 속성에 대한 값을 지정합니다.

   * **론치 제목**: 론치의 이름입니다. 작성자에게 의미가 있는 이름이어야 합니다.
   * **Source 페이지**: 시작을 만들 페이지의 경로입니다. 기본적으로 모든 하위 페이지가 포함됩니다.
   * **하위 페이지 제외**: 하위 페이지가 아닌 원본 페이지에 대해서만 시작을 만들려면 이 옵션을 선택하십시오. 기본적으로 이 옵션은 선택되어 있지 않습니다.
   * **동기화 유지**: 원본 페이지를 변경할 때 시작 페이지의 콘텐츠를 자동으로 업데이트하려면 이 옵션을 선택하십시오. 이 작업은 시작을 [live copy](/help/sites-administering/msm.md)로 만들어 수행됩니다.
   * **론치 날짜**: 론치 카피가 활성화될 날짜 및 시간입니다(**프로덕션 준비** 플래그에 따라 다름). [론치 - 이벤트 순서](/help/sites-authoring/launches.md#launches-the-order-of-events)를 참조하십시오.

   ![chlimage_1-99](assets/chlimage_1-99a.png)

1. **만들기**&#x200B;를 클릭합니다.

## 론치 삭제 {#deleting-a-launch}

론치를 삭제할 수도 있습니다.

1. [론치 콘솔](/help/sites-classic-ui-authoring/classic-launches.md)에서 필요한 론치를 선택합니다.
1. **삭제**&#x200B;를 클릭합니다. 확인 필요:

   ![chlimage_1-100](assets/chlimage_1-100a.png)

   >[!CAUTION]
   >
   >중첩 실행을 삭제할 때는 먼저 낮은 수준을 삭제해야 합니다.
