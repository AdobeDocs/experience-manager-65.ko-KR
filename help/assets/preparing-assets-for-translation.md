---
title: 자산 번역 준비
description: 언어 루트 폴더를 만들어 번역용 에셋을 준비함으로써 다국어 에셋을 지원합니다.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 29cf202b2522b4e624960e8b911f77ec7f291e24
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 3%

---


# 자산 번역 준비 {#preparing-assets-for-translation}

다국어 자산은 이진, 메타데이터 및 태그를 여러 언어로 포함한 자산을 의미합니다. 일반적으로 에셋에 대한 바이너리, 메타데이터 및 태그는 한 언어로 되어 있으며, 이 언어는 다른 언어로 번역되어 다국어 프로젝트에서 사용할 수 있습니다.

Adobe Experience Manager 자산에서 다국어 자산은 폴더에 포함되며 각 폴더에는 다른 언어의 에셋이 포함됩니다.

각 언어 폴더를 언어 복사라고 합니다. 언어 루트라고 하는 언어 사본의 루트 폴더는 언어 사본에 있는 컨텐츠의 언어를 식별합니다. 예를 들어 */content/dam/it* 는 이탈리아어 카피를 위한 이탈리아어 루트입니다. 소스 에셋의 번역이 수행될 때 올바른 언어를 타깃팅하도록 언어 복사본은 [올바르게 구성된 언어 루트를](preparing-assets-for-translation.md#creating-a-language-root) 사용해야 합니다.

자산을 처음 추가하는 언어 사본은 기본 언어입니다. 기본 언어는 다른 언어로 번역되는 소스입니다. 샘플 폴더 계층 구조에는 여러 언어 루트가 포함되어 있습니다.

```
 /content
  /- dam
   |- en
   |- fr
   |- de
   |- es
   |- it
   |- ja
   |- zh
```

다음 단계를 수행하여 자산을 번역할 준비를 합니다.

1. 기본 언어의 언어 루트를 만듭니다. 예를 들어 샘플 폴더 계층 구조에 있는 영어 사본의 언어 루트는 입니다 `/content/dam/en`. 언어 루트 만들기의 정보에 따라 언어 루트 [가 올바르게 구성되었는지 확인합니다](preparing-assets-for-translation.md#creating-a-language-root).

1. 기본 언어로 에셋을 추가합니다.
1. 언어 사본이 필요한 각 대상 언어의 언어 루트를 만듭니다.

## 언어 루트 만들기 {#creating-a-language-root}

언어 루트를 만들려면 폴더를 만들고 이름 속성 값으로 ISO 언어 코드를 사용합니다. 언어 루트를 만든 후 언어 루트 내의 모든 수준에서 언어 사본을 만들 수 있습니다.

예를 들어 샘플 계층의 이탈리아어 언어 사본의 루트 페이지는 이름 속성 `it` 으로 되어 있습니다. Name 속성은 저장소의 자산 노드의 이름으로 사용되므로 자산의 경로를 결정합니다. (`https://[aem_server]:[port]/assets.html/content/dam/it/`).

1. 자산 콘솔에서 **[!UICONTROL 만들기를]** 클릭하고 **[!UICONTROL 메뉴에서]** 폴더를선택합니다.

   ![폴더 만들기](assets/Create-folder.png)

1. 이름 **** 필드에 국가 코드를 의 형식으로 `<language-code>`입력합니다.

   ![폴더에 언어 코드 추가](assets/Add-language-code-in-folder.png)

1. **[!UICONTROL 만들기]**&#x200B;를 클릭합니다. 언어 루트는 자산 콘솔에서 만들어집니다.

## 언어 루트 보기 {#viewing-language-roots}

Experience Manager 인터페이스는 **[!UICONTROL 에셋]** 내에서 생성된 언어 루트 목록을 표시하는 참조 패널을 제공합니다.

1. 자산 콘솔에서 언어 사본을 만들 기본 언어를 선택합니다.
1. 왼쪽 레일에서 **[!UICONTROL 참조]** 옵션을 선택하여 [!UICONTROL 참조] 창을 엽니다.

   ![chlimage_1-122](assets/chlimage_1-122.png)

1. 참조 창에서 언어 사본 **[!UICONTROL 을 클릭합니다]**. 언어 [!UICONTROL 복사] 패널에는 자산의 언어 사본이 표시됩니다.

   ![언어 복사](assets/lang-copy2.png)
