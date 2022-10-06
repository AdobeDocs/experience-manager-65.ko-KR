---
title: 번역 개선 사항
seo-title: Translation Enhancements
description: AEM의 번역 개선 사항.
seo-description: Translation enhancements in AEM.
uuid: 0563603f-327b-48f1-ac14-6777c06734b9
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 42df2db3-4d3c-4954-a03e-221e2f548305
feature: Language Copy
exl-id: 2011a976-d506-4c0b-9980-b8837bdcf5ad
source-git-commit: 1be3d394283493f7c282ea4c3d794458d88e1ac3
workflow-type: tm+mt
source-wordcount: '681'
ht-degree: 34%

---

# 번역 개선 사항{#translation-enhancements}

이 페이지에서는 증분 개선 사항과 AEM 번역 관리 기능에 대한 개선 사항을 제공합니다.

## 번역 프로젝트 자동화 {#translation-project-automation}

번역 실행 자동 홍보 및 삭제, 번역 프로젝트의 반복 실행 예약과 같은 번역 프로젝트 작업 생산성을 향상시키는 옵션이 추가되었습니다.

1. 번역 프로젝트에서 맨 아래에 있는 줄임표를 클릭하거나 탭합니다 **번역 요약** 타일.

   ![screen_shot_2018-04-19at222622](assets/screen_shot_2018-04-19at222622.jpg)

1. 로 전환 **고급** 탭. 맨 아래에서 다음을 선택할 수 있습니다 **번역 실행 자동 홍보**.

   ![screen_shot_2018-04-19at223430](assets/screen_shot_2018-04-19at223430.jpg)

1. 번역된 컨텐츠를 받은 후 번역 실행을 자동으로 홍보하고 삭제해야 하는지 여부를 선택할 수 있습니다.

   ![screen_shot_2018-04-19at224033](assets/screen_shot_2018-04-19at224033.jpg)

1. 번역 프로젝트의 반복 실행을 선택하려면 아래에 드롭다운이 있는 빈도를 선택합니다 **반복 번역**. 반복 프로젝트 실행에서는 지정된 간격으로 번역 작업을 자동으로 만들고 실행합니다.

   ![screen_shot_2018-04-19at223820](assets/screen_shot_2018-04-19at223820.jpg)

## 다국어 번역 프로젝트 {#multilingual-translation-projects}

번역 프로젝트에서 여러 대상 언어를 구성하여 만든 번역 프로젝트의 총 수를 줄일 수 있습니다.

1. 번역 프로젝트에서 맨 아래에 있는 점을 클릭하거나 탭합니다 **번역 요약** 타일.

   ![screen_shot_2018-04-19at222622](assets/screen_shot_2018-04-19at222622.jpg)

1. 로 전환 **고급** 탭. 아래에 여러 언어를 추가할 수 있습니다 **Target 언어**.

   ![screen_shot_2018-04-22at212601](assets/screen_shot_2018-04-22at212601.jpg)

1. 또는 Sites에서 참조 레일을 통해 번역을 시작하는 경우 언어를 추가하고 을(를) 선택합니다 **다국어 번역 프로젝트 만들기**.

   ![screen_shot_2018-04-22at212941](assets/screen_shot_2018-04-22at212941.jpg)

1. 모든 대상 언어에 대한 번역 작업은 프로젝트에서 생성됩니다. 프로젝트 내에서 하나씩 또는 프로젝트 관리자에서 전체적으로 프로젝트를 실행함으로써 한 번에 하나씩 시작할 수 있습니다.

   ![screen_shot_2018-04-22at213854](assets/screen_shot_2018-04-22at213854.jpg)

## 번역 메모리 업데이트 {#translation-memory-updates}

번역된 콘텐츠의 수동 편집 내용을 번역 관리 시스템(TMS)과 다시 동기화하여 번역 메모리를 트레이닝할 수 있습니다.

1. 사이트 콘솔에서 번역된 페이지에서 텍스트 컨텐츠를 업데이트한 후 을 선택합니다 **번역 메모리 업데이트**.

   ![screen_shot_2018-04-22at234430](assets/screen_shot_2018-04-22at234430.jpg)

1. 편집된 모든 텍스트 구성 요소에 대해 소스와 번역의 병렬 비교가 목록 보기에 표시됩니다. 번역 메모리와 동기화해야 하는 번역 업데이트를 선택하고 **메모리 업데이트**.

   ![screen_shot_2018-04-22at235024](assets/screen_shot_2018-04-22at235024.jpg)

AEM은 구성된 TMS의 번역 메모리에 기존 문자열의 번역을 업데이트합니다.

* 이 작업은 구성된 TMS의 번역 메모리에 기존 문자열의 번역을 업데이트합니다.
* 이는 새로운 번역 작업을 생성하지 않습니다.
* 이는 AEM 번역 API를 통해 TMS로 번역을 다시 전달합니다(아래 참조).

이 기능을 사용하려면 다음 작업을 수행하십시오.

* TMS를 AEM과 사용할 수 있도록 구성해야 합니다.
* 커넥터가 방법 [`storeTranslation`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/granite/translation/api/TranslationService.html)를 구현해야 합니다.
   * 이 방법에 포함되는 코드는 번역 메모리 업데이트 요청에 발생하는 일을 결정합니다.
   * 이 방법의 구현을 통해 AEM 번역 프레임워크는 문자열 값 쌍(원본 번역과 업데이트된 번역)을 TMS로 다시 전달합니다.

독점 번역 메모리를 사용하는 경우 번역 메모리 업데이트가 이전되어 사용자 정의 대상으로 전달될 수 있습니다.

## 여러 수준의 언어 사본 {#language-copies-on-multiple-levels}

이제 언어 루트는 노드 아래에 그룹화할 수 있습니다. 예를 들어, 영역별로 그룹화할 수 있지만 언어 사본의 루트로 인식될 수 있습니다.

![screen_shot_2018-04-23at144012](assets/screen_shot_2018-04-23at144012.jpg)

>[!CAUTION]
>
>하나의 수준만 허용됩니다. 예를 들어 다음 단계에서는 &quot;es&quot; 페이지가 언어 사본으로 확인되지 않습니다.
>
>* `/content/we-retail/language-masters/en`
>* `/content/we-retail/language-masters/americas/central-america/es`
>
>이 `es` 언어 사본은 2수준(미국/중앙 아메리카)에서 멀리 있으므로 검색되지 않습니다 `en` 노드 아래에 있어야 합니다.

>[!NOTE]
>
>언어 루트는 언어의 ISO 코드가 아닌 모든 페이지 이름을 가질 수 있습니다. AEM은 항상 경로와 이름을 먼저 확인하지만 페이지 이름이 언어를 식별하지 않으면 AEM에서는 페이지의 cq:language 속성을 통해 언어 식별을 확인합니다.

## 번역 상태 보고 {#translation-status-reporting}

이제 사이트 목록 보기에서 페이지를 번역했는지, 번역했는지, 아니면 아직 번역되지 않았는지 여부를 보여주는 속성을 선택할 수 있습니다. 표시하려면 다음을 수행하십시오.

1. Sites에서 로 전환합니다. **목록 보기.**

   ![screen_shot_2018-04-23at130646](assets/screen_shot_2018-04-23at130646.jpg)

1. 클릭 또는 탭 **설정 보기**.

   ![screen_shot_2018-04-23at130844](assets/screen_shot_2018-04-23at130844.jpg)

1. 확인 **번역됨** 확인란 아래의 **번역** 탭/클릭 **업데이트**.

   ![screen_shot_2018-04-23at130955](assets/screen_shot_2018-04-23at130955.jpg)

이제 **번역됨** 열의 페이지 번역 상태를 보여 줍니다.

![screen_shot_2018-04-23at133821](assets/screen_shot_2018-04-23at133821.jpg)
