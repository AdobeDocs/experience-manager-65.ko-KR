---
title: 변형 - 조각 콘텐츠 작성
seo-title: 변형 - 조각 콘텐츠 작성
description: 변형을 사용하면 조각에 대한 컨텐츠를 작성한 다음 목적에 따라 다양한 컨텐츠(필요한 경우)를 만들 수 있습니다.
seo-description: 변형을 사용하면 조각에 대한 컨텐츠를 작성한 다음 목적에 따라 다양한 컨텐츠(필요한 경우)를 만들 수 있습니다.
uuid: 0844f271-79bc-4f76-8031-d388b81d6feb
contentOwner: Alison Heimoz
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: content-fragments
content-type: reference
discoiquuid: 324df1da-78fa-460f-a744-3504259f1d4a
docset: aem65
translation-type: tm+mt
source-git-commit: bccc937c1e1a349ab292a748c3c7b9d0c68b6199
workflow-type: tm+mt
source-wordcount: '1744'
ht-degree: 2%

---


# 변형 - 조각 콘텐츠 작성{#variations-authoring-fragment-content}

[변형](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) 기능은 특정 채널 및/또는 시나리오에서 사용할 마스터 컨텐츠의 사본을 만들고 편집할 수 있으므로 컨텐츠 조각에 대한 중요한 기능입니다.

변형 **탭에서 다음** 작업을 수행할 수 있습니다.

* [조각에 사용할 컨텐츠](#authoring-your-content) 입력
* [다양한](#managing-variations) 마스터 **** 컨텐츠 만들기 및 관리

편집 중인 데이터 유형에 따라 다양한 다른 작업을 수행합니다. 예를 들면 다음과 같습니다.

* [조각](#inserting-assets-into-your-fragment) (이미지)에 시각적 자산 삽입
* 편집할 [리치 텍스트](#rich-text), [일반 텍스트](#plain-text) 및 [마크다운](#markdown) 중선택

* [컨텐츠 업로드](#uploading-content)

* [주요 통계](#viewing-key-statistics) 보기(여러 줄 텍스트 정보)
* [텍스트 요약](#summarizing-text)

* [마스터 컨텐츠와 변형 동기화](#synchronizing-with-master)

>[!CAUTION]
>
>조각이 게시 및/또는 참조되면 작성자가 편집을 위해 조각을 다시 열면 AEM에 경고가 표시됩니다. 이것은 조각 변경 사항이 참조된 페이지에도 영향을 준다는 것을 경고하기 위한 것입니다.

## 컨텐츠 작성 {#authoring-your-content}

편집을 위해 컨텐츠 조각을 열면 기본적으로 변형 **** 탭이 열립니다. 여기에서 마스터 또는 변형에 대해 컨텐츠를 작성할 수 있습니다. 다음을 작업을 수행할 수 있습니다.

* 변형 **탭에서 직접** 편집
* 전체 [화면 편집기를](#full-screen-editor) 열고 다음을 수행합니다.

   * 형식 [선택](#formats)
   * 더 많은 편집 옵션 보기( [리치 텍스트](#rich-text) 형식)

   * 다양한 [작업 액세스](#actions)

예:

* 간단한 조각 편집

   단순 조각은 하나의 여러 줄 텍스트 필드로 구성됩니다(전체 화면 편집기에서 시각적 자산을 추가할 수 있음).

   ![cfm-6420-21](assets/cfm-6420-21.png)

* 구조화된 컨텐츠로 조각 편집

   구조화된 조각은 컨텐츠 모델에서 정의된 다양한 데이터 유형의 다양한 필드를 포함합니다. 여러 줄 필드의 경우 [전체 화면 편집기를](#full-screen-editor) 사용할 수 있습니다.

   ![cfm-6420-16](assets/cfm-6420-16.png)

### 전체 화면 편집기 {#full-screen-editor}

여러 줄 텍스트 필드를 편집할 때 전체 화면 편집기를 열 수 있습니다.

![cf-fullscreeneditor-icon](assets/cf-fullscreeneditor-icon.png)

전체 화면 편집기에서는 다음을 제공합니다.

* 다양한 [작업 이용](#actions)
* 서식 [에 따라](#formats)추가 서식 옵션([서식 있는 텍스트](#rich-text))

### 작업 {#actions}

전체 화면 편집기(즉, 여러 줄 텍스트)가 열려 있는 경우에도 다음 작업을 모든 [형식](#formats)에 사용할 수 있습니다.

* 서식 [을](#formats) 선택합니다[(](#rich-text)서식 [](#plain-text) 있는 텍스트 [,](#markdown)일반 텍스트,마크다운).

* [텍스트 통계 표시](#viewing-key-statistics)

* [콘텐트 업로드](#uploading-content)
* [마스터와](#synchronizing-with-master) 동기화(변형 편집 시)
* [텍스트 요약](#summarizing-text)
* [텍스트에 주석](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment) 추가

* [조각](#inserting-assets-into-your-fragment) (이미지)에 시각적 자산 삽입

### 형식 {#formats}

여러 줄 텍스트를 편집하는 옵션은 선택한 형식에 따라 다릅니다.

* [리치 텍스트](#rich-text)
* [일반 텍스트](#plain-text)
* [Markdown](#markdown)

전체 화면 편집기에서 형식을 선택할 수 있습니다.

### 리치 텍스트 {#rich-text}

서식 있는 텍스트 편집 기능을 사용하면

* 굵게
* 기울임체
* 밑줄
* 정렬: 왼쪽, 가운데, 오른쪽
* 글머리 기호 목록
* 번호 매기기 목록
* 들여쓰기: 증가, 감소
* 하이퍼링크 만들기/나누기
* 다음 서식 옵션을 사용할 수 있는 전체 화면 편집기를 엽니다.

   * Word에서 텍스트 붙여넣기
   * 표 삽입
   * 단락 스타일: 단락, 제목 1/2/3
   * [시각적 에셋 삽입](#inserting-assets-into-your-fragment)
   * 검색
   * 찾기/바꾸기
   * 맞춤법 검사기
   * [주석](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)

전체 [화면](#actions) 편집기에서 작업에 액세스할 수도 있습니다.

### 일반 텍스트 {#plain-text}

일반 텍스트를 사용하면 서식을 지정하거나 마크다운 정보를 사용하지 않고도 컨텐츠를 신속하게 입력할 수 있습니다. 전체 화면 편집기를 열어 추가 [작업을 수행할 수도 있습니다](#actions).

>[!CAUTION]
>
>일반 텍스트 **를** 선택하면 서식, 표시 및/또는 리치 텍스트 **또는 마크다운** 에 삽입한 에셋을 잃을 수 **있습니다**.

### Markdown {#markdown}

>[!NOTE]
>
>자세한 내용은 [마크다운](/help/assets/content-fragments/content-fragments-markdown.md) 설명서를 참조하십시오.

이렇게 하면 마크다운을 사용하여 텍스트 서식을 지정할 수 있습니다. 다음을 정의할 수 있습니다.

* 머리글
* 단락 및 줄 바꿈
* 링크
* 이미지
* 따옴표 차단
* 목록
* 강조
* 코드 블록
* 백슬래시 이스케이프

전체 화면 편집기를 열어 추가 [작업을 수행할 수도 있습니다](#actions).

>[!CAUTION]
>
>리치 텍스트 **와** 마크다운 **간을 전환하면 이러한 두 포맷의 처리 방식에 차이가 있을 수 있으므로, 인용문** 블록과 코드 블록 블록에 예기치 않은 효과가 나타날 수 있습니다.

### 주요 통계 보기 {#viewing-key-statistics}

전체 화면 편집기가 열리면 **텍스트 통계** 작업에 텍스트에 대한 다양한 정보가 표시됩니다. 예:

![cfx-6420-22](assets/cfx-6420-22.png)

### 컨텐츠 업로드 {#uploading-content}

컨텐츠 조각 작성 프로세스를 간소화하려면 외부 편집기에서 준비한 텍스트를 업로드하고 조각에 직접 추가할 수 있습니다.

### 텍스트 요약 {#summarizing-text}

텍스트 요약 기능은 사용자가 주요 포인트와 전체 의미를 유지하면서 텍스트의 길이를 사전 정의된 단어 수로 줄이는 데 도움이 되도록 고안되었습니다.

>[!NOTE]
>
>보다 기술적인 수준에서는 특정 알고리즘에 따라 정보 밀도와 고유성 *의* 최고 비율을 제공하는 것으로 문장을 유지하기도 합니다.

>[!CAUTION]
>
>컨텐츠 조각에는 상위 항목으로서 유효한 언어(ISO 코드) 폴더가 있어야 합니다. 사용할 언어 모델을 결정하는 데 사용됩니다.
>
>예를 들어 다음 경로 `en/` 와 같습니다.
>
>`/content/dam/my-brand/en/path-down/my-content-fragment`

>[!CAUTION]
>
>영어로 즉시 이용 가능합니다.
>
>기타 언어는 소프트웨어 배포의 언어 모델 패키지로 사용할 수 있습니다.
>
>* [소프트웨어 배포의 프랑스어(fr)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-fr)
>* [소프트웨어 배포를 통한 독일어(de)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-de)
>* [소프트웨어 배포의 이탈리아어(it)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-it)
>* [소프트웨어 배포의 스페인어(es)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-es)

>



1. 마스터 **또는** 필요한 변형을 선택합니다.
1. 전체 화면 편집기를 엽니다.

1. 도구 **모음에서 텍스트** 요약을 선택합니다.

   ![cf-17](assets/cf-17.png)

1. 대상 단어 수를 지정하고 **시작을 선택합니다**.
1. 원래 텍스트는 제안된 요약과 나란히 표시됩니다.

   * 제거할 문장은 빨간색으로 강조 표시되고, 취소선이 그어져 있습니다.
   * 강조 표시된 문장을 클릭하면 요약된 컨텐츠에 표시됩니다.
   * 강조 표시되지 않은 문장을 클릭하면 제거됩니다.

   ![cfm-6420-23](assets/cfm-6420-23.png)

1. 요약을 **선택하여** 변경 사항을 확인합니다.

### 컨텐츠 조각에 주석 추가 {#annotating-a-content-fragment}

조각에 주석을 다는 방법은 다음과 같습니다.

1. 마스터 **또는** 필요한 변형을 선택합니다.
1. 전체 화면 편집기를 엽니다.
1. 텍스트를 선택합니다. 주석 **** 아이콘을 사용할 수 있게 됩니다.

   ![cfm-6420-24](assets/cfm-6420-24.png)

1. 대화 상자가 열립니다. 주석을 입력할 수 있습니다.

1. 전체 화면 편집기를 닫고 **조각** 저장

### 주석 보기, 편집, 삭제 {#viewing-editing-deleting-annotations}

주석:

* 편집기의 전체 화면과 일반 모드 모두에서 텍스트의 강조 표시로 표시됩니다. 그러면 강조 표시된 텍스트를 클릭하여 주석의 전체 세부 정보를 보고, 편집하고, 삭제할 수 있으며, 그러면 대화 상자가 다시 열립니다.

   >[!NOTE]
   >
   >여러 개의 주석이 하나의 텍스트에 적용된 경우 드롭다운 선택기가 제공됩니다.

* 주석이 적용된 전체 텍스트를 삭제하면 주석도 삭제됩니다.

* 조각 편집기에서 [주석] **탭을 선택하여 나열하거나 삭제할** 수 있습니다.

   ![cfm-6420-25](assets/cfm-6420-25.png)

* 선택한 조각에 대해 [타임라인에서](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments) 보고 삭제할 수 있습니다.

### 조각에 자산 삽입 {#inserting-assets-into-your-fragment}

컨텐츠 조각 작성 프로세스를 간소화하려면 [자산](/help/assets/managing-assets-touch-ui.md) (이미지)을 조각에 직접 추가할 수 있습니다.

포맷하지 않고 조각의 단락 시퀀스에 추가됩니다. 페이지 [에서 조각을 사용/참조할 때 서식을 지정할 수 있습니다](/help/sites-authoring/content-fragments.md).

>[!CAUTION]
>
>참조하는 페이지에서 이러한 자산을 이동하거나 삭제할 수 없습니다. 이 작업은 조각 편집기에서 수행해야 합니다.
>
>그러나 자산(예: 크기)의 서식은 [페이지 편집기에서 수행해야 합니다](/help/sites-authoring/content-fragments.md). 조각 편집기의 자산 표현은 순전히 컨텐츠 흐름을 작성하기 위한 것입니다.

>[!NOTE]
>
>There are various methods of adding [images](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets) to the fragment and/or page.

1. 이미지를 추가할 위치에 커서를 놓습니다.
1. 자산 **삽입** 아이콘을 사용하여 검색 대화 상자를 엽니다.

   ![cf-insertasset-icon](assets/cf-insertasset-icon.png)

1. 대화 상자에서 다음 중 하나를 수행할 수 있습니다.

   * DAM에서 필요한 자산으로 이동
   * DAM에서 자산 검색

   일단 찾으면 축소판을 클릭하여 필요한 자산을 선택합니다.

1. 선택 **을** 사용하여 자산을 현재 위치에서 컨텐츠 조각의 단락 시스템에 추가합니다.

   >[!CAUTION]
   >
   >자산을 추가한 후 형식을 다음으로 변경합니다.
   >
   >* **일반 텍스트**: 조각에서 자산이 완전히 손실됩니다.
   >* **마크다운**: 에셋이 표시되지 않지만 리치 텍스트로 돌아갈 때 **남아 있습니다**.


## 변형 관리 {#managing-variations}

### 변형 만들기 {#creating-a-variation}

변형을 사용하면 **마스터** 컨텐츠를 가져와 목적에 따라 변경할 수 있습니다(필요한 경우).

새 변형을 만들려면:

1. 조각을 열고 사이드 패널이 표시되는지 확인합니다.
1. 사이드 패널 **의** 아이콘 막대에서 변형을 선택합니다.
1. 변형 **만들기를 선택합니다**.
1. 대화 상자가 열리면 새로운 변형에 대한 **제목** 및 **설명** 을 지정합니다.
1. 추가 **를**&#x200B;선택합니다. 조각 **마스터** 가 새 변형에 복사되며, 이 변형은 현재 [편집을 위해 열려 있습니다](#editing-a-variation).

   >[!NOTE]
   >
   >새 변형을 만들 때는 현재 열려 있는 **변형이 아니라 항상** 복사되는 마스터입니다.

### 변형 편집 {#editing-a-variation}

다음 중 하나를 수행한 후에 변형 컨텐츠를 변경할 수 있습니다.

* [변형 만들기](#creating-a-variation).
* 기존 조각을 열고 사이드 패널에서 필요한 변형을 선택합니다.

![cfm-6420-26](assets/cfm-6420-26.png)

### 변형 이름 바꾸기 {#renaming-a-variation}

기존 변형의 이름을 변경하려면

1. 조각을 열고 **사이드** 패널에서 변형을 선택합니다.
1. 필요한 변형을 선택합니다.
1. 작업 **드롭다운** 에서 이름 **변경을** 선택합니다.

1. 결과 대화 상자에서 새 **제목** 및/또는 **설명** 을 입력합니다.

1. 이름 변경 **작업을** 확인합니다.

>[!NOTE]
>
>변형 제목에만 영향을 **줍니다**.

### 변형 삭제 {#deleting-a-variation}

기존 변형을 삭제하려면

1. 조각을 열고 **사이드** 패널에서 변형을 선택합니다.
1. 필요한 변형을 선택합니다.
1. 작업 **드롭다운에서** **삭제를** 선택합니다.

1. 대화 상자에서 **삭제** 작업을 확인합니다.

>[!NOTE]
>
>마스터는 삭제할 수 **없습니다**.

### 마스터와 동기화 {#synchronizing-with-master}

**마스터는 컨텐츠 조각의** 필수 부분이며, 정의에 따라 컨텐츠의 마스터 사본이 포함되어 있는 반면, 변형은 해당 컨텐츠의 개별 업데이트 및 맞춤 버전을 보유합니다. 마스터가 업데이트되면 이러한 변경 내용이 변형과 연관되므로 변경 사항을 해당 변경 내용에 전파해야 합니다.

변형을 편집할 때 변형의 현재 요소를 마스터와 동기화하는 작업에 액세스할 수 있습니다. 이렇게 하면 마스터의 변경 내용을 필요한 변형에 자동으로 복사할 수 있습니다.

>[!CAUTION]
>
>동기화는 *마스터&#x200B;**에서 변형**으로 변경*&#x200B;내용을 복사하는 경우에만 사용할 수 있습니다.
>
>변형의 현재 요소만 동기화됩니다.
>
>동기화는 **여러 줄 텍스트** 데이터 유형에서만 작동합니다.
>
>변경 내용 *에서&#x200B;**마스터로 변경&#x200B;***내용을 전송할 수 없습니다.

1. 조각 편집기에서 컨텐츠 조각을 엽니다. 마스터가 **편집되었는지** 확인합니다.
1. 특정 변형을 선택한 다음, 다음 중 하나에서 적절한 동기화 작업을 선택합니다.

   * 작업 **드롭다운** 선택기 - **현재 요소를 마스터와 동기화**

   * 전체 화면 편집기의 도구 모음 - **마스터와 동기화**

1. 마스터 및 변형이 나란히 표시됩니다.

   * green은 추가된 컨텐츠(변형)를 나타냅니다.
   * red는 제거된 컨텐츠(변수에서)를 나타냅니다.

   ![cfm-6420-27](assets/cfm-6420-27.png)

1. 동기화 **를**&#x200B;선택하면 변형이 업데이트되고 표시됩니다.

