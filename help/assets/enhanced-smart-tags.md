---
title: 향상된 스마트 태그
description: 향상된 스마트 태그
contentOwner: AG
feature: Smart Tags, Search
role: User
exl-id: 5eff4a0f-30b1-4753-ad0b-002656eed972
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1559'
ht-degree: 1%

---

# 스마트 태그 이해, 적용 및 조정 {#enhanced-smart-tags}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/smart-tags.html?lang=en) |
| AEM 6.5 | 이 문서 |

디지털 에셋을 다루는 조직은 에셋 메타데이터에서 분류 제어 어휘를 사용하는 경우가 점점 늘어나고 있습니다. 기본적으로 직원, 파트너 및 고객이 특정 클래스의 디지털 에셋을 참조하고 검색하는 데 일반적으로 사용하는 키워드 목록을 포함합니다. 분류 제어 어휘를 사용하여 자산에 태그를 지정하면 자산을 쉽게 식별하고 검색할 수 있습니다.

자연어 어휘와 비교하여 비즈니스 분류법에 따라 디지털 에셋에 태그를 지정하면 기업의 비즈니스에 맞게 정렬되고 가장 관련성이 높은 에셋이 검색에 표시됩니다.

예를 들어 자동차 제조사가 자동차 이미지에 모델 이름을 태깅해 다양한 모델의 이미지를 검색해 판촉 캠페인을 설계할 때 관련 이미지만 나타나도록 할 수 있다.

스마트 컨텐츠 서비스가 올바른 태그를 적용하려면 분류법을 인식하도록 교육합니다. 서비스를 교육하려면 먼저 이러한 에셋을 가장 잘 설명하는 에셋 및 태그 세트를 큐레이션하십시오. 서비스가 학습하는 데 도움이 되도록 에셋에서 이러한 태그를 적용하고 교육 워크플로우를 실행합니다.

태그가 교육되고 준비되면 이제 서비스는 태그 지정 작업 과정을 통해 자산에 이러한 태그를 적용할 수 있습니다.

배경에서 스마트 컨텐츠 서비스는 Adobe Sensei AI 프레임워크를 사용하여 태그 구조 및 비즈니스 분류법에 대한 이미지 인식 알고리즘을 교육합니다. 그런 다음 이 콘텐츠 인텔리전스를 사용하여 다른 에셋 세트에 관련 태그를 적용합니다.

스마트 컨텐츠 서비스 는에서 호스팅되는 클라우드 서비스입니다. [!DNL Adobe Developer Console]. 에서 사용 [!DNL Adobe Experience Manager], 시스템 관리자는 [!DNL Experience Manager] 배포 [!DNL Adobe Developer Console].

요약하면 스마트 컨텐츠 서비스를 사용하는 주요 단계는 다음과 같습니다.

* 온보딩
* 에셋 및 태그 검토(분류법 정의)
* 스마트 컨텐츠 서비스 교육
* 자동 태깅

![순서도](assets/flowchart.gif)

## 사전 요구 사항 및 지원되는 형식 {#prerequisites}

스마트 컨텐츠 서비스를 사용하기 전에 다음을 확인하여 통합을 만드십시오 [!DNL Adobe Developer Console]:

* 조직에 대한 관리자 권한이 있는 Adobe ID 계정입니다.
* 조직에 대해 스마트 컨텐츠 서비스 서비스를 사용하도록 설정합니다.
* 배포에 Smart Content Services 기본 패키지를 추가하려면 라이선스를 부여합니다. [!DNL Adobe Experience Manager Sites] 기본 패키지 및 [!DNL Assets] 추가 기능.

이 서비스는 다음 MIME 유형의 자산에 스마트 태그를 적용합니다.

* `image/jpeg`
* `image/tiff`
* `image/png`
* `image/bmp`
* `image/gif`
* `image/pjpeg`
* `image/x-portable-anymap`
* `image/x-portable-bitmap`
* `image/x-portable-graymap`
* `image/x-portable-pixmap`
* `image/x-rgb`
* `image/x-xbitmap`
* `image/x-xpixmap`
* `image/x-icon`
* `image/photoshop`
* `image/x-photoshop`
* `image/psd`
* `image/vnd.adobe.photoshop`

이 서비스는 다음 MIME 유형의 에셋 렌디션에 스마트 태그를 적용합니다.

* `image/jpeg`
* `image/pjpeg`
* `image/png`

## 온보딩 {#onboarding}

스마트 컨텐츠 서비스 를 의 추가 기능으로 구입할 수 있습니다. [!DNL Experience Manager]. 구입하고 나면 링크를 통해 조직의 관리자에게 이메일이 전송됩니다. [!DNL Adobe I/O].

관리자는 링크를 따라 스마트 컨텐츠 서비스를 와 통합할 수 있습니다 [!DNL Experience Manager]. 서비스를 와 통합하려면 [!DNL Experience Manager Assets], 참조 [스마트 태그 구성](config-smart-tagging.md).

관리자가 서비스를 구성하고 사용자를에 추가하면 온보딩 프로세스가 완료됩니다. [!DNL Experience Manager].

## 에셋 및 태그 검토 {#reviewing-assets-and-tags}

온보딩한 후 가장 먼저 비즈니스 컨텍스트에서 이러한 이미지를 가장 잘 설명하는 태그 세트를 식별해야 합니다.

그런 다음 이미지를 검토하여 특정 비즈니스 요구 사항에 가장 적합한 이미지 세트를 식별합니다. 조정된 세트의 자산이 [스마트 컨텐츠 서비스 교육 지침](/help/assets/config-smart-tagging.md#training-the-smart-content-service).

에셋을 폴더에 추가하고 속성 페이지에서 각 에셋에 태그를 적용합니다. 그런 다음 이 폴더에서 교육 워크플로우를 실행합니다. 조정된 에셋 세트를 사용하면 Smart Content Service에서 분류 정의 를 사용하여 더 많은 에셋을 효과적으로 교육할 수 있습니다.

>[!NOTE]
>
>1. 훈련은 돌이킬 수 없는 과정이다. Adobe은 태그에 대한 스마트 컨텐츠 서비스를 교육하기 전에 조정된 자산 세트의 태그를 검토할 것을 권장합니다.
>1. 태그 교육 전에 다음을 참조하십시오. [스마트 컨텐츠 서비스 교육 지침](/help/assets/config-smart-tagging.md#training-the-smart-content-service).
>1. 스마트 컨텐츠 서비스를 처음 교육할 때 Adobe은 두 개 이상의 서로 다른 태그에 대해 교육하는 것을 권장합니다.

## 이해 [!DNL Experience Manager] 스마트 태그를 사용한 검색 결과 {#understandsearch}

기본적으로, [!DNL Experience Manager] 검색어에 검색어를 결합한 다음 `AND` 절. 스마트 태그를 사용해도 이 기본 동작은 변경되지 않습니다. 스마트 태그를 사용하면 추가 기능이 추가됩니다 `OR` 절을 사용하여 스마트 태그와 관련된 검색어를 찾을 수 있습니다. 예를 들어 다음 항목을 검색하는 것이 좋습니다. `woman running`. 자산이 있는 경우 `woman` 또는 `running` 메타데이터의 키워드는 기본적으로 검색 결과에 표시되지 않습니다. 그러나 다음 중 하나로 태그가 지정된 에셋 `woman` 또는 `running` 스마트 태그를 사용하면 이러한 검색 쿼리에 표시됩니다. 그래서 검색 결과는

* 자산 포함 `woman` 및 `running` 메타데이터 키워드.

* 키워드 중 하나로 스마트 태그가 지정된 에셋입니다.

메타데이터 필드의 모든 검색어와 일치하는 검색 결과가 먼저 표시되고, 스마트 태그의 검색어와 일치하는 검색 결과가 표시됩니다. 위의 예에서 검색 결과가 표시되는 대략적인 순서는 다음과 같습니다.

1. 의 일치 `woman running` 을 참조하십시오.
1. 의 일치 `woman running` 스마트 태그에서 사용됩니다.
1. 의 일치 `woman` 또는 `running` 스마트 태그에서 사용됩니다.

>[!CAUTION]
>
>Lucene 색인화가 다음 항목에서 수행되면 [!DNL Adobe Experience Manager], 스마트 태그를 기반으로 한 검색이 예상대로 작동하지 않습니다.

## 자산에 자동으로 태그 지정 {#tagging-assets-automatically}

스마트 컨텐츠 서비스에 대한 교육을 마친 후에는 태그 지정 워크플로우를 트리거하여 다른 유사한 자산 세트에 적절한 태그를 자동으로 적용할 수 있습니다.

태그 지정 워크플로는 정기적으로 또는 필요할 때마다 실행할 수 있습니다.

>[!NOTE]
>
>태깅 워크플로우는 에셋과 폴더 모두에서 실행됩니다.

### 주기적 태그 지정 {#periodic-tagging}

스마트 컨텐츠 서비스에서 폴더 내의 자산에 정기적으로 태그를 지정할 수 있습니다. 에셋 폴더의 속성 페이지를 열고 을 선택합니다. **[!UICONTROL 스마트 태그 활성화]** 다음 아래에 **[!UICONTROL 세부 사항]** 을 탭하고 변경 내용을 저장합니다.

폴더에 대해 이 옵션을 선택하면 Smart Content Service가 자동으로 폴더 내 자산에 태그를 지정합니다. 태깅 워크플로우는 기본적으로 매일 오전 12시에 실행됩니다.

### 온디맨드 태깅 {#on-demand-tagging}

워크플로우 콘솔 또는 타임라인에서 태깅 워크플로우를 트리거하여 자산에 즉시 태깅할 수 있습니다.

>[!NOTE]
>
>타임라인에서 태깅 워크플로우를 실행하는 경우 한 번에 최대 15개의 에셋에 태그를 적용할 수 있습니다.

#### 워크플로우 콘솔에서 자산에 태그 지정 {#tagging-assets-from-the-workflow-console}

1. 위치 [!DNL Experience Manager] 인터페이스, 이동 **[!UICONTROL 도구]** > **[!UICONTROL 워크플로]** > **[!UICONTROL 모델]**.
1. 다음에서 **[!UICONTROL 워크플로 모델]** 페이지에서 **[!UICONTROL DAM 스마트 태그 자산]** 워크플로우를 클릭한 다음 **[!UICONTROL 워크플로우 시작]** 을 클릭합니다.

   ![dam_smart_tag_workflow](assets/dam_smart_tag_workflow.png)

1. 다음에서 **[!UICONTROL 워크플로우 실행]** 대화 상자에서 태그를 자동으로 적용할 자산이 포함된 페이로드 폴더를 찾습니다.
1. 워크플로우의 제목과 선택적 설명을 지정합니다. 클릭 **[!UICONTROL 실행]**.

   ![tagging_dialog](assets/tagging_dialog.png)

   스마트 컨텐츠 서비스에서 자산에 태그를 제대로 지정했는지 확인하려면 자산 폴더로 이동하여 태그를 검토하십시오.

#### 타임라인에서 에셋에 태그 지정 {#tagging-assets-from-the-timeline}

1. 다음에서 [!DNL Assets] 사용자 인터페이스에서 스마트 태그를 적용할 에셋 또는 특정 에셋이 포함된 폴더를 선택합니다.
1. 왼쪽 상단 모서리에서 을(를) 엽니다. **[!UICONTROL 타임라인]**.
1. 왼쪽 사이드바 아래쪽에서 작업을 열고 를 클릭합니다. **[!UICONTROL 워크플로우 시작]**.

   ![start_workflow](assets/start_workflow.png)

1. 다음 항목 선택 **[!UICONTROL DAM 스마트 태그 자산]** 워크플로우를 참조하고 워크플로우의 제목을 지정합니다.
1. 클릭 **[!UICONTROL 시작]**. 워크플로는 에셋에 태그를 적용합니다. 스마트 컨텐츠 서비스에서 자산에 태그를 제대로 지정했는지 확인하려면 자산 폴더로 이동하여 태그를 검토하십시오.

>[!NOTE]
>
>이후 태그 지정 주기에서는 수정된 자산만 새로 교육된 태그로 다시 태그 지정됩니다. 하지만 태깅 워크플로우의 마지막 태깅 주기와 현재 태깅 주기 사이의 간격이 24시간을 초과하는 경우 변경되지 않은 에셋에도 태깅됩니다. 주기적 태그 지정 워크플로의 경우, 시간 간격이 6개월을 초과하면 변경되지 않은 자산에 태그가 지정됩니다.

## 적용된 스마트 태그 조정 또는 중재 {#manage-smart-tags}

스마트 태그를 조정하여 가장 관련성이 높은 태그만 표시되도록 브랜드 이미지에 할당된 부정확한 태그를 제거할 수 있습니다.

스마트 태그를 중재하면 가장 관련성이 높은 태그에 대한 검색 결과에 이미지가 나타나도록 하여 이미지에 대한 태그 기반 검색을 구체화하는 데도 도움이 됩니다. 기본적으로 관련 없는 이미지가 검색 결과에 나타날 가능성을 제거하는 데 도움이 됩니다.

태그에 더 높은 등급을 할당하여 이미지에 대한 관련성을 높일 수도 있습니다. 이미지에 대한 태그를 프로모션하면 특정 태그가 검색될 때 이미지가 검색 결과에 나타날 가능성이 높아집니다.

1. 검색 상자에서 태그를 키워드로 사용하여 에셋을 검색합니다.
1. 검색과 관련이 없는 이미지를 식별하려면 검색 결과를 검토하십시오.
1. 이미지를 선택하고 **[!UICONTROL 태그 관리]** 을 클릭합니다.
1. 다음에서 **[!UICONTROL 태그 관리]** 페이지, 태그를 검토합니다. 특정 태그를 기준으로 이미지를 검색하지 않으려면 태그를 선택한 다음 를 클릭합니다 **[!UICONTROL 삭제]** 을 클릭합니다. 또는 를 클릭합니다 `x` 태그 옆에 표시되는 기호입니다.
1. 선택적으로 태그에 더 높은 등급을 지정하려면 태그를 선택하고 을 클릭합니다. **[!UICONTROL 홍보]** 을 클릭합니다. 프로모션한 태그가 로 이동됩니다. **[!UICONTROL 태그]** 섹션.
1. 클릭 **[!UICONTROL 저장]** 그런 다음 을 클릭합니다. **[!UICONTROL 확인]**
1. 다음 위치로 이동 **[!UICONTROL 속성]** 이미지를 위한 페이지입니다. 프로모션한 태그에 더 많은 관련성이 할당되고 검색 결과 앞에 표시되는지 확인합니다.

## 팁 및 제한 사항 {#tips-best-practices-limitations}

* 모델을 교육하려면 가장 적절한 이미지를 사용하십시오. 교육을 되돌리거나 교육 모델을 제거할 수 없습니다. 태그 지정 정확도는 현재 교육에 따라 다르므로 주의해서 수행합니다.
* 스마트 컨텐츠 서비스의 사용은 연간 최대 200만 개의 태그가 지정된 이미지로 제한됩니다. 처리되고 태그된 임의의 복제 이미지들은 각각 태그된 이미지로서 카운팅된다.
* 타임라인에서 태깅 워크플로우를 실행하는 경우 한 번에 최대 15개의 에셋에 태그를 적용할 수 있습니다.
* 스마트 태그는 PNG 및 JPG 이미지 형식에서만 작동합니다. 따라서 이러한 두 형식으로 만들어진 렌디션이 있는 지원되는 에셋에는 스마트 태그가 지정됩니다.
