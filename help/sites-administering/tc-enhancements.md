---
title: 번역 개선 사항
seo-title: 번역 개선 사항
description: AEM의 번역 개선 사항.
seo-description: AEM의 번역 개선 사항.
uuid: 0563603f-327b-48f1-ac14-6777c06734b9
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 42df2db3-4d3c-4954-a03e-221e2f548305
feature: 언어 복사
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 8%

---


# 번역 개선 사항{#translation-enhancements}

이 페이지에서는 AEM 번역 관리 기능에 대한 개선 사항과 개선 사항을 제공합니다.

## 번역 프로젝트 자동화 {#translation-project-automation}

번역 프로젝트를 사용한 생산성 향상 옵션이 추가되었습니다(예: 번역 실행 자동 홍보 및 삭제, 번역 프로젝트의 반복 실행 예약).

1. 번역 프로젝트에서 **번역 요약** 타일 맨 아래에 있는 줄임표를 클릭하거나 탭합니다.

   ![screen_shot_2018-04-19at222622](assets/screen_shot_2018-04-19at222622.jpg)

1. **고급** 탭으로 전환합니다. 아래쪽에서 **번역 자동 승격 시작**&#x200B;을 선택할 수 있습니다.

   ![screen_shot_2018-04-19at223430](assets/screen_shot_2018-04-19at223430.jpg)

1. 번역된 컨텐트를 받은 후 번역 론치가 자동으로 홍보되고 삭제되도록 할지 여부를 선택할 수도 있습니다(선택 사항).

   ![screen_shot_2018-04-19at224033](assets/screen_shot_2018-04-19at224033.jpg)

1. 번역 프로젝트의 반복 실행을 선택하려면 **반복 번역** 드롭다운 아래에 있는 빈도를 선택합니다. 반복 프로젝트를 실행하면 지정된 간격으로 번역 작업이 자동으로 생성되고 실행됩니다.

   ![screen_shot_2018-04-19at223820](assets/screen_shot_2018-04-19at223820.jpg)

## 다국어 번역 프로젝트 {#multilingual-translation-projects}

번역 프로젝트에서 여러 대상 언어를 구성하여 생성된 번역 프로젝트의 총 수를 줄일 수 있습니다.

1. 번역 프로젝트에서 **번역 요약** 타일 아래쪽에 있는 점을 클릭하거나 탭합니다.

   ![screen_shot_2018-04-19at222622](assets/screen_shot_2018-04-19at222622.jpg)

1. **고급** 탭으로 전환합니다. **Target 언어**&#x200B;에서 여러 언어를 추가할 수 있습니다.

   ![screen_shot_2018-04-22at212601](assets/screen_shot_2018-04-22at212601.jpg)

1. 또는 사이트에서 참조 레일을 통해 번역을 시작하는 경우 언어를 추가하고 **다국어 번역 프로젝트 만들기**&#x200B;를 선택합니다.

   ![screen_shot_2018-04-22at212941](assets/screen_shot_2018-04-22at212941.jpg)

1. 모든 대상 언어에 대해 프로젝트에 번역 작업이 생성됩니다. 프로젝트 관리에서 프로젝트를 전체적으로 실행하여 프로젝트 내에서 하나씩 또는 한꺼번에 모두 시작할 수 있습니다.

   ![screen_shot_2018-04-22at213854](assets/screen_shot_2018-04-22at213854.jpg)

## 번역 메모리 업데이트 {#translation-memory-updates}

번역된 컨텐츠의 수동 편집 내용은 TMS(Translation Management System)로 다시 동기화하여 번역 메모리를 교육할 수 있습니다.

1. 사이트 콘솔에서 번역된 페이지의 텍스트 컨텐츠를 업데이트한 후 **번역 메모리 업데이트**&#x200B;를 선택합니다.

   ![screen_shot_2018-04-22at234430](assets/screen_shot_2018-04-22at234430.jpg)

1. 목록 보기에는 편집된 모든 텍스트 구성 요소에 대한 소스 및 번역 내용이 나란히 비교되어 표시됩니다. 번역 메모리에 동기화할 번역 업데이트를 선택하고 **메모리 업데이트**&#x200B;를 선택합니다.

   ![screen_shot_2018-04-22at235024](assets/screen_shot_2018-04-22at235024.jpg)

   >[!NOTE]
   >
   >AEM에서 선택한 문자열을 번역 관리 시스템으로 다시 전송합니다.

## 여러 수준의 언어 사본 {#language-copies-on-multiple-levels}

이제 언어 루트는 언어 사본의 루트로 인식되지만, 예를 들어 지역별로 노드 아래에 그룹화할 수 있습니다.

![screen_shot_2018-04-23at144012](assets/screen_shot_2018-04-23at144012.jpg)

>[!CAUTION]
>
>한 수준만 허용됩니다. 예를 들어, 다음 예제에서는 &quot;es&quot; 페이지에서 언어 사본을 확인할 수 없습니다.
>
>* `/content/we-retail/language-masters/en`
>* `/content/we-retail/language-masters/americas/central-america/es`

>
>
이 `es` 언어 사본은 `en` 노드에서 2단계(아메리카/중앙 아메리카)이므로 검색되지 않습니다.

>[!NOTE]
>
>언어 루트에는 해당 언어의 ISO 코드가 아닌 페이지 이름이 있을 수 있습니다. AEM은 항상 먼저 경로와 이름을 확인하지만 페이지 이름이 언어를 식별하지 않으면 AEM은 페이지의 cq:language 속성을 확인하여 언어 식별을 수행합니다.

## 번역 상태 보고 {#translation-status-reporting}

이제 페이지가 번역되었거나, 번역 중이거나, 아직 번역되지 않았음을 보여주는 속성을 사이트 목록 보기에서 선택할 수 있습니다. 표시하려면 다음을 수행하십시오.

1. 사이트에서 **목록 보기로 전환합니다.**

   ![screen_shot_2018-04-23at130646](assets/screen_shot_2018-04-23at130646.jpg)

1. **설정 보기**&#x200B;를 클릭하거나 탭합니다.

   ![screen_shot_2018-04-23at130844](assets/screen_shot_2018-04-23at130844.jpg)

1. **번역** 아래의 **번역** 확인란을 선택하고 **업데이트**&#x200B;를 탭/클릭합니다.

   ![screen_shot_2018-04-23at130955](assets/screen_shot_2018-04-23at130955.jpg)

이제 페이지의 번역 상태를 보여주는 **Translated** 열이 표시됩니다.

![screen_shot_2018-04-23at133821](assets/screen_shot_2018-04-23at133821.jpg)

