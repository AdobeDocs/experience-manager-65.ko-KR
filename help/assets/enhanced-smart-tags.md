---
title: 향상된 스마트 태그
description: 향상된 스마트 태그
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '1536'
ht-degree: 1%

---


# 향상된 스마트 태그 {#enhanced-smart-tags}

## 향상된 스마트 태그 개요 {#overview-of-enhanced-smart-tags}

디지털 자산을 처리하는 조직은 자산 메타데이터에 분류 제어 용어를 점점 더 사용하고 있습니다. 기본적으로 직원, 파트너 및 고객이 특정 클래스의 디지털 자산을 참조하고 검색하는 데 일반적으로 사용하는 키워드 목록이 포함되어 있습니다. 분류 제어 어휘를 사용하여 자산에 태그를 지정하면 태그 기반 검색으로 쉽게 식별하고 검색할 수 있습니다.

자연어 어휘와 비교하여 비즈니스 분류법에 따라 디지털 자산에 태그를 지정하여 회사의 비즈니스와 연계할 수 있고 검색에서 가장 관련성이 높은 자산이 표시되도록 할 수 있습니다.

예를 들어 자동차 제조업체는 자동차 이미지에 모델 이름을 태그로 지정할 수 있으므로 다양한 모델의 이미지를 검색하여 프로모션 캠페인을 디자인할 때만 관련 이미지만 나타납니다.

Smart Content Service가 올바른 태그를 적용하려면 분류 방식을 인식하도록 훈련해야 합니다. 서비스를 교육하려면 먼저 이러한 자산을 가장 잘 설명하는 자산 및 태그 집합을 조정하십시오. 자산에 이러한 태그를 적용하고 교육 워크플로우를 실행하여 서비스 학습에 도움이 됩니다.

태그가 교육되고 준비되면, 서비스는 태그 지정 워크플로우를 통해 이러한 태그를 자산에 적용할 수 있습니다.

백그라운드에서 Smart Content Service는 Adobe Sensei AI 프레임워크를 사용하여 태그 구조 및 비즈니스 분류법에 대한 이미지 인식 알고리즘을 교육합니다. 그런 다음 이 컨텐츠 인텔리전스를 사용하여 다른 자산 세트에 관련 태그를 적용합니다.

스마트 콘텐츠 서비스는 Adobe I/O에서 호스팅되는 클라우드 서비스입니다. 시스템 관리자 [!DNL Adobe Experience Manager][!DNL Experience Manager] 는 배포를 Adobe I/O와 통합해야 합니다.

다음은 스마트 콘텐츠 서비스를 사용하는 주요 단계입니다.

* 온보딩
* 자산 및 태그 검토(분류 정의)
* 스마트 콘텐츠 서비스 교육
* 자동 태그 지정

![순서도](assets/flowchart.gif)

## 전제 조건 {#prerequisites}

스마트 콘텐츠 서비스를 사용하려면 먼저 Adobe I/O에 통합을 만들려면 다음을 확인하십시오.

* 조직에 대한 관리자 권한이 부여된 Adobe ID 계정이 있습니다.
* 조직에서 스마트 콘텐츠 서비스 서비스를 사용할 수 있습니다.

## 온보딩 {#onboarding}

The Smart Content Service is available for purchase as an add-on to [!DNL Experience Manager]. 구입하면 Adobe I/O에 대한 링크가 포함된 이메일이 조직의 관리자에게 전송됩니다.

관리자는 링크를 따라 Smart Content Service를 통합할 수 있습니다 [!DNL Experience Manager]. 서비스를 통합하려면 스마트 태그 구성 [!DNL Experience Manager Assets]을 [참조하십시오](config-smart-tagging.md).

온보딩 프로세스는 관리자가 서비스를 구성하고 사용자를 [!DNL Experience Manager]

>[!NOTE]
>
>6.3 이전 버전을 사용하고 있고 자산에 대한 태그 지정 서비스가 필요한 경우 [!DNL Experience Manager] 스마트 태그를 참조하십시오 [](https://helpx.adobe.com/experience-manager/6-3/assets/using/touch-ui-smart-tags.html). 스마트 태그는 최신 AI 기능을 사용하지 않으므로 향상된 스마트 태그 지정 서비스보다 정확도가 떨어집니다.

## 자산 및 태그 검토 {#reviewing-assets-and-tags}

온보드 환경을 구현한 후에는 먼저 비즈니스 컨텍스트에서 이러한 이미지를 가장 잘 설명하는 태그 세트를 식별합니다.

그런 다음 이미지를 검토하여 특정 비즈니스 요구 사항에 맞게 제품을 가장 잘 나타내는 이미지 세트를 확인합니다. 선별된 세트의 에셋이 [스마트 콘텐츠 서비스 교육 지침을 준수하는지 확인합니다](smart-tags-training-guidelines.md).

자산을 폴더에 추가하고 속성 페이지에서 각 자산에 태그를 적용합니다. 그런 다음 이 폴더에서 교육 워크플로우를 실행합니다. 선별된 자산 집합을 통해 Smart Content Service는 분류 정의를 사용하여 더 많은 자산을 효과적으로 교육할 수 있습니다.

>[!NOTE]
>
>1. 훈련은 취소할 수 없는 과정이다. Adobe은 태그에서 스마트 컨텐츠 서비스를 교육하기 전에 선별된 자산 세트의 태그를 검토할 것을 권장합니다.
>1. 태그에 대한 교육을 시작하기 전에 [스마트 콘텐츠 서비스 교육 지침을](smart-tags-training-guidelines.md) 읽어 보십시오.
>1. 스마트 콘텐츠 서비스를 처음 교육할 때 두 개 이상의 개별 태그로 교육하는 것이 좋습니다.


## 스마트 콘텐츠 서비스 트레이닝 {#training-the-smart-content-service}

Smart Content Service가 비즈니스 분류 방식을 인식하려면 비즈니스와 관련이 있는 태그를 이미 포함하는 자산 세트에서 실행합니다. 교육 후 서비스는 유사한 자산 세트에 동일한 분류법을 적용할 수 있습니다.

관련 태그를 적용할 수 있도록 서비스를 여러 번 교육할 수 있습니다. 각 교육 주기 후에 태그 지정 워크플로우를 실행하고 자산에 태그가 적절하게 지정되어 있는지 확인합니다.

정기적으로 또는 요구 사항에 따라 스마트 콘텐츠 서비스를 교육할 수 있습니다.

>[!NOTE]
>
>교육 워크플로우는 폴더에서만 실행됩니다.

### 정기적인 교육 {#periodic-training}

Smart Content Service가 폴더 내의 자산 및 관련 태그를 정기적으로 교육하도록 설정할 수 있습니다. 자산 폴더의 [!UICONTROL 속성] 페이지 **[!UICONTROL 를 열고]** 세부 **[!UICONTROL 사항]** 탭 아래에서 스마트 태그활성화를 선택한다음 변경 사항을저장합니다.

![enable_smart_tags](assets/enable_smart_tags.png)

폴더에 대해 이 옵션을 선택하면 교육 워크플로우가 자동으로 [!DNL Experience Manager] 실행되어 폴더 자산 및 해당 태그에서 스마트 콘텐츠 서비스를 훈련합니다. 기본적으로 교육 워크플로우는 매주 토요일 오전 12시 30분에 실행됩니다.

### 주문형 트레이닝 {#on-demand-training}

Workflow 콘솔에서 필요할 때마다 스마트 콘텐츠 서비스를 교육할 수 있습니다.

1. In [!DNL Experience Manager] interface, go to **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
1. [워크플로우 **[!UICONTROL 모델]** ] 페이지에서 **[!UICONTROL 스마트 태그 교육]** 작업 과정을 선택한 다음 도구 모음에서 **[!UICONTROL 워크플로우]** 시작을클릭합니다.
1. [워크플로우 **[!UICONTROL 실행]** ] 대화 상자에서 서비스 교육을 위해 태그가 지정된 에셋이 포함된 페이로드 폴더를 찾습니다.
1. 워크플로우의 제목을 지정하고 주석을 추가합니다. 그런 다음 실행을 **[!UICONTROL 클릭합니다]**. 교육 목적으로 자산 및 태그가 제출됩니다.

   ![workflow_dialog](assets/workflow_dialog.png)

>[!NOTE]
>
>교육 목적으로 폴더의 자산이 처리되면 수정된 자산만 이후 교육 주기에 처리됩니다.

### 교육 보고서 보기 {#viewing-training-reports}

스마트 콘텐츠 서비스가 교육 자산의 태그에 대해 교육되었는지 확인하려면 보고서 콘솔에서 교육 워크플로우 보고서를 검토하십시오.

1. 인터페이스에서 [!DNL Experience Manager] 도구 **[!UICONTROL >]** 자산 **[!UICONTROL > 보고서]** 로 **[!UICONTROL 이동합니다]**.
1. 자산 **[!UICONTROL 보고서]** 페이지에서 만들기를 **[!UICONTROL 클릭합니다]**.
1. 스마트 **[!UICONTROL 태그 교육]** 보고서를 선택한 다음 도구 모음에서 **[!UICONTROL 다음]** 을 클릭합니다.
1. 보고서의 제목과 설명을 지정합니다. 보고서 **[!UICONTROL 예약]**&#x200B;아래에서 **[!UICONTROL 지금]** 옵션을 선택된 상태로 두십시오. 나중에 보고서를 예약하려면 **[!UICONTROL 나중에를]** 선택하고 날짜 및 시간을 지정합니다. 그런 다음 도구 **[!UICONTROL 모음에서]** 만들기를 클릭합니다.
1. 자산 **[!UICONTROL 보고서]** 페이지에서 생성한 보고서를 선택합니다. 보고서를 보려면 도구 모음에서 **[!UICONTROL 보기]** 를 클릭합니다.
1. 보고서의 세부 사항을 검토하십시오.

   이 보고서에는 교육된 태그의 교육 상태가 표시됩니다. [ **[!UICONTROL 교육 상태]** ] 열의 녹색 색상은 스마트 콘텐츠 서비스가 태그용으로 교육되었음을 나타냅니다. 노란색 색상은 서비스가 특정 태그에 대해 완전히 교육되지 않음을 나타냅니다. 이 경우 특정 태그로 이미지를 더 추가하고 교육 워크플로우를 실행하여 태그에서 서비스를 완전히 교육합니다.

   이 보고서에 태그가 없으면 이러한 태그에 대해 교육 워크플로우를 다시 실행하십시오.

1. 보고서를 다운로드하려면 목록에서 선택하고 도구 모음에서 **[!UICONTROL 다운로드를]** 클릭합니다. 이 보고서는 Microsoft Excel 스프레드시트로 다운로드됩니다.

## 에셋에 자동으로 태그 지정 {#tagging-assets-automatically}

스마트 콘텐츠 서비스를 교육한 후 유사한 다른 자산 세트에 적절한 태그를 자동으로 적용하도록 태그 지정 워크플로우를 트리거할 수 있습니다.

정기적으로 또는 필요할 때마다 태그 지정 워크플로우를 실행할 수 있습니다.

>[!NOTE]
>
>태그 지정 워크플로우는 자산과 폴더 모두에서 실행됩니다.

### 주기적 태그 지정 {#periodic-tagging}

Smart Content Service가 폴더 내의 에셋에 정기적으로 태그를 지정할 수 있도록 설정할 수 있습니다. 자산 폴더의 속성 페이지를 열고 **[!UICONTROL 세부 사항]** 탭 아래에서 스마트 태그 **[!UICONTROL 활성화를]** 선택한다음 변경 사항을 저장합니다.

폴더에 대해 이 옵션을 선택하면 Smart Content Service가 폴더 내의 자산에 자동으로 태그를 지정합니다. 기본적으로 태그 지정 워크플로우는 매일 오전 12:00에 실행됩니다.

### On-Demand 태깅 {#on-demand-tagging}

다음과 같이 태그 지정 워크플로우를 트리거하여 자산에 즉시 태그를 지정할 수 있습니다.

* 워크플로우 콘솔
* 타임라인

>[!NOTE]
>
>타임라인에서 태그 지정 워크플로우를 실행하는 경우 한 번에 최대 15개의 자산에 태그를 적용할 수 있습니다.

#### 워크플로우 콘솔에서 자산 태그 지정 {#tagging-assets-from-the-workflow-console}

1. In [!DNL Experience Manager] interface, go to **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
1. 워크플로우 **[!UICONTROL 모델]** 페이지에서 **[!UICONTROL DAM 스마트 태그 자산]** 워크플로우를 선택한 다음 도구 모음에서 **[!UICONTROL 워크플로우]** 시작을클릭합니다.

   ![dam_smart_tag_workflow](assets/dam_smart_tag_workflow.png)

1. 워크플로우 **[!UICONTROL 실행]** 대화 상자에서 태그를 자동으로 적용할 자산이 들어 있는 페이로드 폴더를 찾습니다.
1. 워크플로우의 제목과 선택적 주석을 지정합니다. 실행을 **[!UICONTROL 클릭합니다]**.

   ![tagging_dialog](assets/tagging_dialog.png)

   자산 폴더로 이동하고 태그를 검토하여 Smart Content Service가 에셋에 제대로 태그를 지정했는지 확인합니다. 자세한 내용은 스마트 태그 [관리를 참조하십시오](managing-smart-tags.md).

#### 타임라인에서 에셋에 태그 지정 {#tagging-assets-from-the-timeline}

1. 사용자 [!DNL Assets] 인터페이스에서 스마트 태그를 적용할 자산 또는 특정 자산이 들어 있는 폴더를 선택합니다.
1. 왼쪽 위 모서리에서 **[!UICONTROL 타임라인을 엽니다]**.
1. 왼쪽 사이드바 아래쪽에서 작업을 열고 [워크플로우 **[!UICONTROL 시작]을 클릭합니다]**.

   ![start_workflow](assets/start_workflow.png)

1. DAM **[!UICONTROL 스마트 태그 자산]** 워크플로우를 선택하고 워크플로우의 제목을 지정합니다.
1. 시작을 **[!UICONTROL 클릭합니다]**. 워크플로우는 자산에 태그를 적용합니다. 자산 폴더로 이동하고 태그를 검토하여 Smart Content Service가 에셋에 제대로 태그를 지정했는지 확인합니다. 자세한 내용은 스마트 태그 [관리를 참조하십시오](managing-smart-tags.md).

>[!NOTE]
>
>후속 태그 지정 주기 동안 새로 훈련된 태그로 수정된 자산만 다시 태그됩니다. 하지만 태그 지정 워크플로우에 대한 마지막 태그 지정 주기와 현재 태그 지정 주기 사이의 간격이 24시간이 넘는 경우에도 변경되지 않은 자산에 태그됩니다. 주기적인 태그 지정 워크플로우의 경우, 시간 간격이 6개월이 되면 변경되지 않은 자산에 태그가 지정됩니다.
