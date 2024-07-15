---
title: 번역을 위한 자산 준비
description: 언어 루트 폴더를 만들어 다국어 자산을 지원하도록 번역을 위한 자산을 준비합니다.
contentOwner: AG
role: User, Admin
feature: Projects
exl-id: eee768e3-3eb4-46fa-b9ae-9ef8764a3a94
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 1%

---

# 번역을 위한 자산 준비 {#preparing-assets-for-translation}

다국어 에셋은 여러 언어로 된 바이너리, 메타데이터 및 태그가 있는 에셋을 의미합니다. 일반적으로 에셋의 바이너리, 메타데이터 및 태그는 한 언어로 된 후 다국어 프로젝트에서 사용할 수 있도록 다른 언어로 번역됩니다.

[!DNL Adobe Experience Manager Assets]에서 다국어 자산은 폴더에 포함되어 있으며 각 폴더에는 다른 언어의 자산이 포함되어 있습니다.

각 언어 폴더를 언어 사본이라고 합니다. 언어 루트라고도 하는 언어 사본의 루트 폴더는 언어 사본에 있는 콘텐츠의 언어를 식별합니다. 예를 들어 */content/dam/it*&#x200B;은(는) 이탈리아어 사본의 이탈리아어 루트입니다. 언어 사본은 원본 에셋의 번역을 수행할 때 올바른 언어가 타겟팅되도록 [올바르게 구성된 언어 루트](preparing-assets-for-translation.md#creating-a-language-root)를 사용해야 합니다.

자산을 처음 추가하는 언어 사본은 기본 언어입니다. 기본 언어는 다른 언어로 번역되는 소스입니다. 샘플 폴더 계층에는 여러 언어 루트가 포함됩니다.

```shell
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

에셋을 번역할 준비를 하려면 다음 단계를 수행하십시오.

1. 기본 언어의 언어 루트를 만듭니다. 예를 들어 샘플 폴더 계층 구조에서 영어 사본의 언어 루트는 `/content/dam/en`입니다. 언어 루트가 [언어 루트 만들기](preparing-assets-for-translation.md#creating-a-language-root)의 정보에 따라 올바르게 구성되었는지 확인하십시오.

1. 기본 언어에 자산을 추가합니다.
1. 언어 사본이 필요한 각 대상 언어의 언어 루트를 만듭니다.

## 언어 루트 만들기 {#creating-a-language-root}

언어 루트를 만들려면 폴더를 만들고 ISO 언어 코드를 이름 속성 값으로 사용합니다. 언어 루트를 만든 후에는 언어 루트 내의 모든 수준에서 언어 사본을 만들 수 있습니다.

예를 들어 샘플 계층 구조의 이탈리아어 언어 사본의 루트 페이지에는 이름 속성으로 `it`이(가) 있습니다. 이름 속성은 저장소의 자산 노드 이름으로 사용되므로 자산 경로를 결정합니다. (`https://[aem_server]:[port]/assets.html/content/dam/it/`).

1. [!DNL Assets] 콘솔에서 **[!UICONTROL 만들기]**&#x200B;를 클릭하고 메뉴에서 **[!UICONTROL 폴더]**&#x200B;를 선택합니다.

   ![폴더 만들기](assets/Create-folder.png)

1. **[!UICONTROL 이름]** 필드에 국가 코드를 `<language-code>` 형식으로 입력하십시오.

   ![폴더에 언어 코드 추가](assets/Add-language-code-in-folder.png)

1. **[!UICONTROL 만들기]**&#x200B;를 클릭합니다. 언어 루트가 [!DNL Assets] 콘솔에 만들어집니다.

## 언어 루트 보기 {#viewing-language-roots}

[!DNL Experience Manager] 인터페이스는 [!DNL Assets] 내에 만들어진 언어 루트 목록을 표시하는 **[!UICONTROL 참조]** 패널을 제공합니다.

1. [!DNL Assets] 콘솔에서 언어 사본을 만들 기본 언어를 선택합니다.
1. 왼쪽 레일에서 **[!UICONTROL 참조]** 옵션을 선택하여 [!UICONTROL 참조] 창을 엽니다.

   ![chlimage_1-122](assets/chlimage_1-122.png)

1. 참조 창에서 **[!UICONTROL 언어 사본]**&#x200B;을 클릭합니다. [!UICONTROL 언어 사본] 패널에 자산의 언어 사본이 표시됩니다.

   ![언어 사본](assets/lang-copy2.png)
