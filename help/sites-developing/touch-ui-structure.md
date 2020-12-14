---
title: AEM 터치 지원 UI의 구조
seo-title: AEM 터치 지원 UI의 구조
description: 터치에 적합한 UI는 AEM에 구현되어 있으며 몇 가지 기본 원칙을 가지고 있으며 몇 가지 주요 요소로 구성됩니다
seo-description: 터치에 적합한 UI는 AEM에 구현되어 있으며 몇 가지 기본 원칙을 가지고 있으며 몇 가지 주요 요소로 구성됩니다
uuid: 9a255238-1adc-4a40-9c37-30cb53ffb26c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 55dba890-4847-4986-b272-33480bc1d573
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 5%

---


# AEM 터치 지원 UI의 구조{#structure-of-the-aem-touch-enabled-ui}

AEM 터치 지원 UI에는 몇 가지 기본 원칙이 있으며 다음과 같은 몇 가지 주요 요소가 있습니다.

## 콘솔 {#consoles}

### 기본 레이아웃 및 크기 조정 {#basic-layout-and-resizing}

2가지 스타일 Adobe을 만드는 대신 모든 화면과 장치에 맞는 하나의 스타일을 사용하기로 결정한 UI는 모바일 및 데스크톱 장치 모두를 위한 것입니다.

모든 모듈은 동일한 기본 레이아웃을 사용합니다. AEM에서는 다음과 같이 볼 수 있습니다.

![chlimage_1-142](assets/chlimage_1-142.png)

레이아웃은 반응형 디자인 스타일을 준수하며 사용 중인 장치/창의 크기에 맞게 자동으로 조정됩니다.

예를 들어 해상도가 1024px(모바일 장치) 아래로 내려가면 디스플레이가 그에 따라 조정됩니다.

![chlimage_1-143](assets/chlimage_1-143.png)

### 헤더 막대 {#header-bar}

![chlimage_1-144](assets/chlimage_1-144.png)

헤더 막대는 다음을 포함한 글로벌 요소를 보여줍니다.

* 로고 및 현재 사용 중인 특정 제품/솔루션;aem의 경우 전역 탐색 링크도 구성됩니다
* 검색
* 도움말 리소스에 액세스하기 위한 아이콘
* 다른 솔루션에 액세스하기 위한 아이콘
* 대기 중인 알림 또는 받은 편지함 항목의 표시기(및 액세스)
* 프로필 관리 링크와 함께 사용자 아이콘

### 도구 모음 {#toolbar}

이것은 아래 페이지의 보기 또는 자산을 제어하는 것과 관련된 위치 및 표면 도구에 상황에 맞는 것입니다. 도구 모음은 제품별로 다르지만 요소에 공통성이 있습니다.

어떤 위치에서든 도구 모음에는 현재 사용 가능한 작업이 표시됩니다.

![chlimage_1-145](assets/chlimage_1-145.png)

또한 리소스가 현재 선택되어 있는지 여부에 따라 달라집니다.

![chlimage_1-146](assets/chlimage_1-146.png)

### 왼쪽 레일 {#left-rail}

필요에 따라 왼쪽 레일을 열거나 숨길 수 있습니다.

* **타임라인**
* **참조**
* **필터**

기본값은 **컨텐츠 전용**(레일 숨김)입니다.

![chlimage_1-147](assets/chlimage_1-147.png)

## 페이지 작성 {#page-authoring}

페이지를 작성할 때 구조적 영역은 다음과 같습니다.

### 내용 프레임 {#content-frame}

페이지 컨텐츠가 컨텐츠 프레임에서 렌더링됩니다. 컨텐츠 프레임은 편집기와 완전히 독립적입니다. CSS 또는 javascript로 인해 충돌이 발생하지 않도록 할 수 있습니다.

내용 프레임은 창 오른쪽 섹션의 도구 모음 아래에 있습니다.

![chlimage_1-148](assets/chlimage_1-148.png)

### 편집기 프레임 {#editor-frame}

편집기 프레임은 편집 기능을 인식합니다.

편집기 프레임은 모든 *페이지 작성 요소*&#x200B;에 대한 컨테이너(추상)입니다. 컨텐츠 프레임 위에 있으며 다음을 포함합니다.

* 상단 도구 모음
* 사이드 패널
* 모든 오버레이
* 기타 페이지 제작 요소예를 들어, 구성 요소 도구 모음

![chlimage_1-149](assets/chlimage_1-149.png)

### 사이드 패널 {#side-panel}

여기에는 자산 및 구성 요소를 선택할 수 있는 두 개의 기본 탭이 포함되어 있습니다.여기에서 드래그하여 페이지로 놓을 수 있습니다.

사이드 패널은 기본적으로 숨겨집니다. 이 옵션을 선택하면 왼쪽에 표시되고, 창 크기가 1024px 미만인 경우 전체 창을 덮기 위해 옆으로 밀면 됩니다.예를 들어 모바일 장치에서의 경우처럼).

![chlimage_1-150](assets/chlimage_1-150.png)

### 사이드 패널 - 자산 {#side-panel-assets}

자산 탭의 자산 범위에서 선택할 수 있습니다. 특정 용어에 대해 필터링하거나 그룹을 선택할 수도 있습니다.

![chlimage_1-151](assets/chlimage_1-151.png)

### 사이드 패널 - 자산 그룹 {#side-panel-asset-groups}

자산 탭에 특정 자산 그룹을 선택하는 데 사용할 수 있는 드롭다운이 있습니다.

![chlimage_1-152](assets/chlimage_1-152.png)

### 사이드 패널 - 구성 요소 {#side-panel-components}

구성 요소 탭에서 구성 요소 범위에서 선택할 수 있습니다. 특정 용어에 대해 필터링하거나 그룹을 선택할 수도 있습니다.

![chlimage_1-153](assets/chlimage_1-153.png)

### 오버레이 {#overlays}

이러한 오버레이는 컨텐츠 프레임을 오버레이하고 [레이어](#layer)에서 사용하여 구성 요소 및 해당 컨텐츠와 상호 작용(완전히 투명하게)하는 방법에 대한 메커니즘을 실현합니다.

오버레이는 컨텐츠 프레임에 해당 구성 요소를 오버레이하지만 다른 모든 페이지 제작 요소와 함께 편집기 프레임에 라이브됩니다.

![chlimage_1-154](assets/chlimage_1-154.png)

### 레이어 {#layer}

레이어는 활성화할 수 있는 기능의 독립적인 번들입니다.

* 페이지의 다른 보기 제공
* 페이지를 조작하거나 인터랙션할 수 있도록 허용

레이어는 개별 구성 요소에 대한 특정 작업이 아닌 전체 페이지에 대해 정교한 기능을 제공합니다.

AEM에는 페이지 작성을 위해 이미 구현된 여러 레이어가 포함되어 있습니다.예를 들어 편집, 미리 보기, 주석 달기 등이 있습니다.

>[!NOTE]
>
>레이어는 사용자의 페이지 컨텐츠 보기 및 상호 작용에 영향을 주는 강력한 개념입니다. 자체 레이어를 개발할 때는 레이어를 종료한 후 레이어를 깔끔하게 정리해야 합니다.

### 레이어 전환기 {#layer-switcher}

레이어 전환기를 사용하면 사용할 레이어를 선택할 수 있습니다. 닫으면 현재 사용 중인 레이어를 나타냅니다.

레이어 전환기는 도구 모음(창 상단, 편집기 프레임 내)에서 드롭다운으로 사용할 수 있습니다.

![chlimage_1-155](assets/chlimage_1-155.png)

### 구성 요소 도구 모음 {#component-toolbar}

구성 요소의 각 인스턴스는 클릭할 때(한 번 또는 느리게 두 번 클릭) 해당 도구 모음이 표시됩니다. 도구 모음에는 페이지의 구성 요소 인스턴스(편집 가능)에 사용할 수 있는 특정 작업(예: 복사, 붙여넣기, 편집기)이 포함되어 있습니다.

사용 가능한 공간에 따라 구성 요소 도구 모음은 해당 구성 요소의 상단 또는 하단 오른쪽 모서리에 배치됩니다.

![chlimage_1-156](assets/chlimage_1-156.png)

## 추가 정보 {#further-information}

터치 지원 UI에 대한 개념에 대한 자세한 내용은 [AEM 터치 지원 UI의 개념](/help/sites-developing/touch-ui-concepts.md) 아티클을 계속 참조하십시오.

자세한 기술 정보는 터치가 활성화된 페이지 편집기에 대해 [JS 설명서 세트](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/jsdoc/ui-touch/editor-core/index.html)를 참조하십시오.

