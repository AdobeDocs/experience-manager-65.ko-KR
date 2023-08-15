---
title: 대화 상자 편집기
seo-title: Dialog Editor
description: 대화 상자 편집기는 대화 상자와 스캐폴드를 쉽게 만들고 편집할 수 있는 그래픽 인터페이스를 제공합니다
seo-description: The dialog editor provides a graphical interface for easily creating and editing dialog boxes and scaffolds
uuid: 64d3fb12-8638-441b-8595-c590d48f3072
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: b7ac457d-3689-4f5d-9ceb-ff6a9944e7eb
exl-id: 57303608-c3e1-4201-8054-1a1798613e2c
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 1%

---

# 대화 상자 편집기{#dialog-editor}

대화 상자 편집기는 대화 상자와 스캐폴드를 쉽게 만들고 편집할 수 있는 그래픽 인터페이스를 제공합니다.

작동 방식을 확인하려면 CRXDE Lite 로 이동하여 `/libs/foundation/components/chart` 노드를 두 번 클릭합니다. `dialog`:

![chlimage_1-247](assets/chlimage_1-247.png)

대화 상자 노드가 **대화 상자 편집기**:

![screen_shot_2012-02-01at25033pm](assets/screen_shot_2012-02-01at25033pm.png)

## 사용자 인터페이스 개요 {#user-interface-overview}

대화 상자 편집기 인터페이스는 네 개의 창으로 구성됩니다.

* 다음 **팔레트**&#x200B;왼쪽 상단 모서리에서 을 참조하십시오. 이 창에는 탭 패널, 텍스트 필드, 선택 목록 및 버튼과 같은 대화 상자를 만드는 데 사용할 수 있는 위젯이 보관됩니다. 원하는 분할선 표시줄을 클릭하여 팔레트 내에서 다른 범주를 확장할 수 있습니다.
* 다음 **구조** 왼쪽 아래 모서리에 있는 창입니다. 이 창에는 대화 상자 정의를 구성하는 노드의 계층 구조가 표시됩니다. CRXDE Lite 또는 CRX 콘텐츠 탐색기에서 대화 상자 노드를 확장하면 동일한 구조를 볼 수 있습니다.
* 다음 **렌더링** 창, 창 가운데 이 창에서는 구조 창에 정의된 대화 상자 정의가 실제 대화 상자로 렌더링되는 방법을 보여 줍니다.
* 다음 **속성** 창. 이 창은 구조 창에서 현재 강조 표시된 노드의 속성을 보여 줍니다.

### 대화 상자 편집기 사용 {#using-the-dialog-editor}

대화 상자를 작성하기 위해 팔레트에서 요소를 구조 창으로 드래그하여 대화 상자 정의 계층 구조 내의 위치로 놓습니다.

원하는 구조가 완료되면 사용자는 **저장**&#x200B;렌더링 창의 맨 위에 있습니다.

>[!CAUTION]
>
>대화 상자 편집기는 비교적 간단한 대화 상자를 만들기 위한 것이며 더 복잡한 대화 상자 정의를 편집하지 못할 수 있습니다. 대화 상자 편집기에서 대화 상자 구조 편집을 허용하지 않는 경우 CRXDE Lite 또는 CRX 콘텐츠 탐색기 등을 사용하여 노드 구조를 직접 편집하여 대화 상자 정의를 수동으로 생성 및/또는 편집해야 합니다.

### 새 대화 상자 만들기 {#creating-a-new-dialog}

새 대화 상자를 만들려면 필요한 구성 요소를 선택하고 **만들기...** 그런 다음 **대화 상자 만들기...**.

필요한 세부 정보를 입력한 다음 **모두 저장** - 이제 대화 상자를 두 번 클릭하여 편집기로 열 수 있습니다.

### 스캐폴드용 대화 상자 편집기 사용 {#using-the-dialog-editor-for-scaffolds}

스캐폴드는 한 단계로 작성하여 제출할 수 있는 양식이 포함된 특수 페이지입니다. 이렇게 하면 입력한 콘텐츠를 사용하여 페이지를 신속하게 만들 수 있습니다.

스캐폴드를 구성하는 양식은 스캐폴딩 페이지에 다른 양식으로 표시되지만 일반 대화 상자와 마찬가지로 대화 상자 정의에 의해 정의됩니다. 대화 상자 정의를 사용하여 스캐폴드를 정의하므로 대화 상자 편집기를 사용하여 스캐폴드를 디자인할 수 있습니다. 이러한 방식으로 대화 상자 편집기를 사용할 때 렌더링 창은 대화 상자 정의를 스캐폴드가 아닌 대화 상자 형태로 계속 표시합니다.

다음을 참조하십시오 [스캐폴딩](/help/sites-authoring/scaffolding.md) 대화 상자 편집기를 사용하여 스캐폴드를 만드는 방법에 대한 자세한 내용을 보려면 를 클릭하십시오.
