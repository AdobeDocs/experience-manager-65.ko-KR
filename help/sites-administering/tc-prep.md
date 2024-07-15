---
title: 번역을 위한 콘텐츠 준비
description: Adobe Experience Manager에서 번역할 콘텐츠를 준비하는 방법을 알아봅니다.
contentOwner: Guillaume Carlino
feature: Language Copy
exl-id: 81978733-89a6-4436-bcf1-4bde962ed54f
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: eae057caed533ef16bb541b4ad41b8edd7aaa1c7
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 45%

---

# 번역을 위한 콘텐츠 준비{#preparing-content-for-translation}

일반적으로 다국어 웹 사이트는 여러 언어로 일정량의 콘텐츠를 제공합니다. 사이트는 하나의 언어로 작성된 다음 다른 언어로 번역됩니다. 일반적으로 다국어 사이트는 페이지 분기로 구성되며, 각 분기에는 서로 다른 언어로 된 사이트 페이지가 포함됩니다.

샘플 Geometrixx 데모 사이트는 여러 언어 분기를 포함하며, 다음 구조를 사용합니다.

```xml
/content
    |- geometrixx
             |- en
             |- fr
             |- de
             |- es
             |- it
             |- ja
             |- zh
```

각각의 사이트 언어 분기를 언어 사본이라고 합니다. 언어 루트라고도 하는 언어 사본의 루트 페이지는 언어 사본에 있는 콘텐츠의 언어를 식별합니다. 예를 들어 `/content/geometrixx/fr`은 프랑스어 언어 사본의 언어 루트입니다. 언어 사본은 원본 사이트의 번역을 수행할 때 올바른 언어가 타겟팅되도록 [올바르게 구성된 언어 루트](/help/sites-administering/tc-prep.md#creating-a-language-root)를 사용해야 합니다.

처음 사이트 콘텐츠를 작성하는 언어 사본은 언어 마스터입니다. 언어 마스터는 다른 언어로 번역되는 소스입니다.

다음 단계를 사용하여 사이트 번역을 준비하십시오.

1. 언어 마스터의 언어 루트를 만듭니다. 예를 들어 영어 Geometrixx 데모 사이트의 언어 루트는 /content/geometrixx/en입니다. 언어 루트는 [언어 루트 만들기](/help/sites-administering/tc-prep.md#creating-a-language-root)에 기재된 정보에 따라 올바르게 구성되어야 합니다.
1. 언어 마스터의 콘텐츠를 작성합니다.
1. 사이트에 대한 각 언어 사본의 언어 루트를 만듭니다. 예를 들어 Geometrixx 샘플 사이트의 프랑스어 언어 사본은 /content/geometrixx/fr입니다.

번역을 위한 콘텐츠를 준비한 다음에는 언어 사본 및 관련 번역 프로젝트에서 누락된 페이지를 자동으로 만들 수 있습니다. ([번역 프로젝트 만들기](/help/sites-administering/tc-manage.md)를 참조하십시오.) AEM 콘텐츠 번역 프로세스의 개요를 확인하려면 [다국어 웹 사이트를 위한 콘텐츠 번역](/help/sites-administering/translation.md)을 살펴보십시오.

## 언어 루트 만들기 {#creating-a-language-root}

언어 루트를 콘텐츠의 언어를 식별하는 언어 사본의 루트 페이지로 만듭니다. 언어 루트를 만든 다음에는 언어 사본이 포함된 번역 프로젝트를 만들 수 있습니다.

언어 루트를 만들려면 페이지를 만들고 ISO 언어 코드를 이름 속성 값으로 사용합니다. 언어 코드는 다음 형식 중 하나여야 합니다.

* `<language-code>`지원되는 언어 코드는 ISO-639-1에서 정의된 두 자리 코드입니다(예: `en`).

* `<language-code>_<country-code>` 또는 `<language-code>-<country-code>`지원되는 국가 코드는 ISO 3166에서 정의된 소문자 또는 대문자 두 자리 코드입니다(예: `en_US`, `en_us`, `en_GB`, `en-gb`).

전역 사이트에 대해 선택한 구조에 따라 두 형식 중 하나를 사용할 수 있습니다. 예를 들어 Geometrixx 사이트의 프랑스어 언어 사본의 루트 페이지에는 이름 속성으로 `fr`이(가) 있습니다. 이름 속성은 저장소의 페이지 노드 이름으로 사용되므로 페이지 경로를 결정합니다. (http://localhost:4502/content/geometrixx/fr.html)

다음 절차에서는 터치에 적합한 UI를 사용하여 웹 사이트의 언어 사본을 만듭니다. 클래식 UI를 사용하는 지침은 [클래식 UI를 사용하여 언어 루트 만들기](/help/sites-administering/tc-lroot-classic.md)를 참조하십시오.

1. 사이트로 이동합니다.
1. 언어 사본을 만들 사이트를 클릭합니다.

   예를 들어 Geometrixx Outdoors 사이트의 언어 사본을 만들려면 Geometrixx Outdoors 사이트 를 클릭합니다.

1. 만들기를 클릭한 다음 페이지 만들기를 클릭합니다.

   ![chlimage_1-21](assets/chlimage_1-21a.png)

1. 페이지 템플릿을 선택하고 다음 을 클릭합니다.
1. 이름 필드에 국가 코드를 `<language-code>` 또는 `<language-code>_<country-code>` 형식으로 입력합니다(예: `en`, `en_US`, `en_us`, `en_GB`, `en_gb`). 페이지 제목을 입력합니다.

   ![chlimage_1-22](assets/chlimage_1-22a.png)

1. 만들기 를 클릭합니다. 확인 대화 상자에서 사이트 콘솔로 돌아가려면 **완료**&#x200B;를 클릭하고 언어 사본을 열려면 **열기**&#x200B;를 클릭합니다.

## 언어 루트 상태 보기 {#seeing-the-status-of-language-roots}

터치에 적합한 UI는 생성된 언어 루트 목록을 표시하는 참조 패널을 제공합니다.

![chlimage_1-23](assets/chlimage_1-23a.png)

다음 절차에서는 터치에 적합한 UI를 사용하여 페이지의 참조 패널을 엽니다.

1. 사이트 콘솔에서 사이트의 페이지를 선택한 다음 **참조**&#x200B;을 클릭합니다.

   ![chlimage_1-24](assets/chlimage_1-24a.png)

1. 참조 패널에서 **언어 사본**&#x200B;을 클릭합니다. 언어 사본 패널에는 웹 사이트의 언어 사본이 표시됩니다.
