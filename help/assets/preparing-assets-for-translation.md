---
title: 번역 자산 준비
description: 언어 루트 폴더를 만들어 번역 자산을 준비하여 다국어 에셋을 지원합니다.
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# 번역 자산 준비 {#preparing-assets-for-translation}

다국어 에셋은 바이너리, 메타데이터 및 여러 언어로 된 태그가 포함된 에셋을 의미합니다. 일반적으로 에셋에 대한 바이너리, 메타데이터 및 태그는 한 언어로 존재하며, 이러한 언어는 다른 언어로 번역되어 다국어 프로젝트에서 사용할 수 있습니다.

AEM(Adobe Experience Manager) 자산에서 다국어 자산은 폴더에 포함되며 각 폴더에는 다른 언어로 된 자산이 포함됩니다.

각 언어 폴더를 언어 복사라고 합니다. 언어 루트라고 하는 언어 사본의 루트 폴더는 언어 사본의 컨텐츠 언어를 식별합니다. 예를 들어 */content/dam/it* is the Italian language root for the Italian language copy. 언어 복사본은 소스 에셋의 번역이 수행될 때 올바른 언어를 타깃팅하도록 [올바르게 구성된 언어 루트를](preparing-assets-for-translation.md#creating-a-language-root) 사용해야 합니다.

자산을 처음 추가하는 언어 사본은 언어 마스터입니다. 언어 마스터는 다른 언어로 번역되는 소스입니다. 샘플 폴더 계층에는 다음과 같은 여러 언어 루트가 포함되어 있습니다.

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

다음 단계를 수행하여 번역을 위해 자산을 준비합니다.

1. 언어 마스터의 언어 루트를 만듭니다. 예를 들어 샘플 폴더 계층 구조에서 영어 사본의 언어 루트는 입니다 `/content/dam/en`. 언어 루트 만들기의 정보에 따라 언어 루트가 올바르게 [구성되었는지 확인합니다](preparing-assets-for-translation.md#creating-a-language-root).

1. 언어 마스터에 에셋 추가
1. 언어 사본이 필요한 각 대상 언어의 언어 루트를 만듭니다.

## 언어 루트 만들기 {#creating-a-language-root}

언어 루트를 만들려면 폴더를 만들고 ISO 언어 코드를 Name 속성 값으로 사용합니다. 언어 루트를 만든 후 언어 루트 내의 모든 수준에서 언어 사본을 만들 수 있습니다.

예를 들어 샘플 계층 구조의 이탈리아어 사본의 루트 페이지는 Name `it` 속성으로 되어 있습니다. 이름 속성은 저장소의 자산 노드의 이름으로 사용되므로 자산의 경로를 결정합니다.(`https://[aem_server]:[port]/assets.html/content/dam/it/`2).

1. 자산 콘솔에서 만들기를 클릭/탭하고 **** 메뉴에서 **[!UICONTROL 폴더를]** 선택합니다.

   ![폴더 만들기](assets/Create-folder.png)

1. 이름 **[!UICONTROL 필드에]** 국가 코드를 의 형식으로 `<language-code>`입력합니다.

   ![폴더에 언어 코드 추가](assets/Add-language-code-in-folder.png)

1. **[!UICONTROL 만들기]**&#x200B;를 클릭하거나 탭합니다. 언어 루트는 자산 콘솔에서 생성됩니다.

## 언어 루트 보기 {#viewing-language-roots}

AEM 인터페이스는 **[!UICONTROL AEM]** 자산 내에 작성된 언어 루트 목록을 표시하는 참조 패널을 제공합니다.

1. 자산 콘솔에서 언어 사본을 만들 언어 마스터를 선택합니다.
1. GlobalNav 아이콘을 클릭하거나 탭하고 참조를 선택하여 **[!UICONTROL 참조]** [!UICONTROL 창을 엽니다] .

   ![chlimage_1-122](assets/chlimage_1-122.png)

1. 참조 창에서 언어 사본을 클릭하거나 **[!UICONTROL 탭합니다]**. 언어 [!UICONTROL 복사] 패널에는 자산의 언어 복사본이 표시됩니다.

   ![chlimage_1-123](assets/chlimage_1-123.png)
