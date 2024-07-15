---
title: 대화 상자 편집기
description: 대화 상자 편집기는 대화 상자와 스캐폴드를 쉽게 만들고 편집할 수 있는 그래픽 인터페이스를 제공합니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
exl-id: 57303608-c3e1-4201-8054-1a1798613e2c
solution: Experience Manager, Experience Manager Sites
feature: Developing,Developer Tools
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 0%

---

# 대화 상자 편집기{#dialog-editor}

대화 상자 편집기는 대화 상자와 스캐폴드를 쉽게 만들고 편집할 수 있는 그래픽 인터페이스를 제공합니다.

작동 방식을 보려면 CRXDE Lite으로 이동하여 `/libs/foundation/components/chart`에 대한 탐색기 트리를 열고 `dialog` 노드를 두 번 클릭합니다.

![chlimage_1-247](assets/chlimage_1-247.png)

대화 상자 노드가 **대화 상자 편집기**&#x200B;에서 열립니다.

![screen_shot_2012-02-01at25033pm](assets/screen_shot_2012-02-01at25033pm.png)

## 사용자 인터페이스 개요 {#user-interface-overview}

대화 상자 편집기 인터페이스는 네 개의 창으로 구성됩니다.

* 왼쪽 위 모서리의 **팔레트**&#x200B;입니다. 이 창에는 탭 패널, 텍스트 필드, 선택 목록 및 버튼과 같은 대화 상자를 만드는 데 사용할 수 있는 위젯이 보관됩니다. 원하는 분할선 막대를 클릭하여 팔레트 내에서 다른 범주를 확장할 수 있습니다.
* 왼쪽 아래 모서리에 있는 **구조** 창입니다. 이 창에는 대화 상자 정의를 구성하는 노드의 계층 구조가 표시됩니다. CRXDE Lite 또는 CRX 콘텐츠 탐색기에서 대화 상자 노드를 확장하면 동일한 구조를 볼 수 있습니다.
* 창 중앙의 **render** 창입니다. 이 창에서는 구조 창에 정의된 대화 상자 정의가 실제 대화 상자로 렌더링되는 방법을 보여 줍니다.
* **속성** 창. 이 창은 구조 창에서 강조 표시된 노드의 속성을 보여 줍니다.

### 대화 상자 편집기 사용 {#using-the-dialog-editor}

대화 상자를 작성하기 위해 팔레트에서 요소를 구조 창으로 드래그하여 대화 상자 정의 계층 구조 내의 위치로 놓습니다.

원하는 구조가 완료되면 사용자는 렌더링 창의 맨 위에서 **저장**&#x200B;을 클릭합니다.

>[!CAUTION]
>
>대화 상자 편집기는 간단한 대화 상자를 만들기 위한 것입니다. 더 복잡한 대화 상자 정의를 편집하지 못할 수 있습니다. 대화 상자 편집기에서 대화 상자 구조 편집을 허용하지 않는 경우에는 대화 상자 정의를 수동으로 만들거나 편집하거나 두 가지 모두를 편집해야 합니다. 예를 들어 CRXDE Lite 또는 CRX Content Explorer를 사용하여 노드 구조를 직접 편집하면 됩니다.

### 새 대화 상자 만들기 {#creating-a-new-dialog}

대화 상자를 만들려면 필요한 구성 요소를 선택하고 **만들기..**&#x200B;를 클릭한 다음 **대화 상자 만들기...**&#x200B;를 클릭합니다.

필요한 세부 정보를 입력한 다음 **모두 저장**&#x200B;을 클릭합니다. 이제 편집기로 열도록 대화 상자를 두 번 클릭할 수 있습니다.

### 스캐폴드용 대화 상자 편집기 사용 {#using-the-dialog-editor-for-scaffolds}

스캐폴드는 한 단계로 작성하여 제출할 수 있는 양식이 포함된 특수 페이지입니다. 이렇게 하면 입력한 콘텐츠를 사용하여 페이지를 신속하게 만들 수 있습니다.

스캐폴드를 구성하는 양식은 스캐폴딩 페이지에 다른 양식으로 표시되지만 일반 대화 상자와 마찬가지로 대화 상자 정의에 의해 정의됩니다. 대화 상자 정의를 사용하여 스캐폴드를 정의하므로 대화 상자 편집기를 사용하여 스캐폴드를 디자인할 수 있습니다. 이러한 방식으로 대화 상자 편집기를 사용할 때 렌더링 창에는 대화 상자 정의가 스캐폴드가 아닌 대화 상자 형태로 계속 표시됩니다.

대화 상자 편집기를 사용하여 스캐폴드를 만드는 방법에 대한 자세한 내용은 [스캐폴딩](/help/sites-authoring/scaffolding.md)을 참조하십시오.
