---
title: 스마트 콘텐츠 서비스 교육 지침
description: Adobe Sensei의 AI 서비스를 트레이닝하여 자산에 스마트 태그 적용
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
contentOwner: AG
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 0%

---


# 스마트 콘텐츠 서비스 교육 지침 {#smart-content-service-training-guidelines}

브랜드 이미지에 효과적으로 태그를 지정할 수 있도록 스마트 콘텐츠 서비스에서는 교육 이미지가 특정 지침을 준수해야 합니다.

## 교육 지침 {#guidelines-for-training}

최상의 결과를 얻으려면 교육 세트의 이미지가 다음 지침을 따라야 합니다.

**수량 및 크기:** 태그당 최소 30개 이미지 긴 면에서 최소 500픽셀입니다.

**일관성**: 태그의 이미지는 시각적으로 유사해야 합니다.

예를 들어 이러한 이미지는 시각적으로 유사하지 않기 때문에 이러한 이미지 `my-party` 에 태그를 모두 교육 목적으로 지정하는 것은 좋지 않습니다.

![트레이닝 지침을 예시하기 위한 실례가 되는 이미지](/help/assets/assets/do-not-localize/coherence.png)

**적용 범위**: 트레이닝에서 이미지에 다양한 이미지가 있어야 합니다. Adobe Experience Manager는 몇 가지 다양한 예제를 제시하여 최적의 환경에 집중할 수 있도록 해야 합니다. 시각적으로 다른 이미지에 동일한 태그를 적용하는 경우 각 종류의 최소 5개의 예를 포함합니다.

예를 들어 태그 *모델 다운 포즈의*&#x200B;경우 태그 지정 중에 서비스에서 유사한 이미지를 보다 정확하게 식별할 수 있도록 아래 강조 표시된 이미지와 유사한 더 많은 교육 이미지를 포함합니다.

![트레이닝 지침을 예시하기 위한 실례가 되는 이미지](/help/assets/assets/do-not-localize/coverage_1.png)

**방해/방해**: 집중을 덜 하는 이미지(두드러진 배경, 주제와 관련된 사물/사람 등 관련 없는 요소)에서 서비스를 더 잘 운행한다.

예를 들어, 태그 *캐주얼*&#x200B;카드의 경우 두 번째 이미지는 올바른 교육 후보가 아닙니다.

![트레이닝 지침을 예시하기 위한 실례가 되는 이미지](/help/assets/assets/do-not-localize/distraction.png)

**완전성:** 이미지가 둘 이상의 태그에 적합하면 교육을 위한 이미지를 포함하기 전에 해당 태그를 모두 추가합니다. 예를 들어, 및 `raincoat` `model-side-view`와 같은 태그의 경우, 교육을 위해 태그를 포함하기 전에 해당 자산에 둘 다 추가합니다.

![트레이닝 지침을 예시하기 위한 실례가 되는 이미지](/help/assets/assets/do-not-localize/completeness.png)

## 제한 사항 {#limitations}

향상된 스마트 태그는 이미지와 태그의 학습 모델을 기반으로 합니다. 이러한 모델이 태그를 식별하는 데 항상 완벽하지는 않습니다. 현재 버전의 스마트 콘텐츠 서비스에는 다음과 같은 제한이 있습니다.

* 이미지의 미묘한 차이를 인식하지 못함 예를 들어, 슬림형 셔츠는 일반 셔츠가 들어 있는 것과 같습니다.
* 이미지의 작은 패턴/부분을 기반으로 태그를 식별할 수 없음 예를 들어 T-셔츠 상의 로고
* 태깅은 Experience Manager가 지원되는 로케일에서 지원됩니다. 언어 목록은 [스마트 콘텐츠 서비스 릴리스 노트를 참조하십시오](https://docs.adobe.com/content/help/en/experience-manager-64/release-notes/smart-content-service-release-notes.html).

스마트 태그가 있는 자산을 검색하려면(일반 또는 고급) 자산 검색(전체 텍스트 검색)을 사용합니다. 스마트 태그에는 별도의 검색 조건자가 없습니다.

>[!NOTE]
>
>태그에서 태그를 교육하고 다른 이미지에 적용할 수 있는 스마트 콘텐츠 서비스의 기능은 교육에 사용하는 이미지의 품질에 따라 달라집니다. 최상의 결과를 얻으려면 시각적으로 유사한 이미지를 사용하여 각 태그에 대한 서비스를 교육하는 것이 좋습니다.
