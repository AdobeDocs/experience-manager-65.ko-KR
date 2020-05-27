---
title: 스마트 태그 및 검색 관리
description: 부정확한 스마트 태그를 업데이트하거나 제거하여 태그의 연관성을 향상시킬 수 있습니다.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---


# 스마트 태그 및 검색 관리 {#manage-smart-tags-and-searches}

<!--
TBD: This article should be merged into a new, uber article for Smart Tags. Delete this article then. Cloud service article is merged.
-->

브랜드 이미지에 지정되었을 수 있는 부정확한 태그를 제거하여 가장 관련성이 높은 태그만 표시되도록 스마트 태그를 조정할 수 있습니다.

또한 스마트 태그를 중재하면 이미지가 가장 관련성이 높은 태그에 대한 검색 결과에 표시되도록 하여 태그 기반의 이미지 검색을 세분화할 수 있습니다. 기본적으로 관련 없는 이미지가 검색 결과에 표시되지 않을 가능성을 없애줍니다.

이미지에 대한 연관성을 높이기 위해 태그에 더 높은 등급을 지정할 수도 있습니다. 이미지에 대한 태그를 승격하면 특정 태그를 기준으로 검색을 수행할 때 이미지가 검색 결과에 표시될 가능성이 높아집니다.

1. Omnisearch 상자에서 태그를 기반으로 자산을 검색합니다.
1. 검색 결과를 검사하여 검색과 관련이 없는 이미지를 식별합니다.
1. 이미지를 선택하고 도구 모음에서 **[!UICONTROL 태그]** 관리를 클릭합니다.
1. 태그 **[!UICONTROL 관리]** 페이지에서 태그를 검사합니다. 특정 태그를 기준으로 이미지를 검색하지 않으려면 태그를 선택한 다음 도구 모음에서 **[!UICONTROL 삭제를]** 클릭합니다. 또는 레이블 옆에 표시되는 `X` 기호를 클릭합니다.
1. 태그에 높은 등급을 지정하려면 태그를 선택하고 도구 모음에서 **[!UICONTROL 홍보]** 를 클릭합니다. 홍보하는 태그가 **[!UICONTROL 태그]** 섹션으로 이동합니다.
1. 저장 **[!UICONTROL 을]**&#x200B;클릭한 다음 **[!UICONTROL 확인을]** 클릭하여 성공 대화 상자를 닫습니다.
1. 이미지의 속성 페이지로 이동합니다. 홍보한 태그에 높은 연관성이 할당되므로 검색 결과에 더 높은 태그가 나타나도록 합니다.

## 스마트 태그를 사용하여 Experience Manager 검색 결과 이해 {#understandsearch}

기본적으로 Experience Manager 검색은 검색어와 `AND` 절을 결합합니다. 스마트 태그를 사용해도 이 기본 동작은 변경되지 않습니다. 스마트 태그를 사용하면 적용 스마트 태그의 검색어 중 하나를 찾기 위한 추가 `OR` 조항이 추가됩니다. For example, consider searching for `woman running`. 메타데이터에 키워드 `woman` 만 `running` 이 있는 자산은 기본적으로 검색 결과에 나타나지 않습니다. 하지만 스마트 태그를 사용하거나 둘 중 하나 `woman` 로 태그가 `running` 지정된 자산이 이러한 검색 쿼리에 나타납니다. 검색 결과는

* 메타데이터에 `woman` 및 키워드가 있는 `running` 자산입니다.

* 두 키워드 중 하나로 태그가 지정된 스마트 자산.

메타데이터 필드의 모든 검색어와 일치하는 검색 결과가 먼저 표시되고, 그 다음에 스마트 태그의 검색어와 일치하는 검색 결과가 표시됩니다. 위 예에서 검색 결과의 대략적인 표시 순서는 다음과 같습니다.

1. 다양한 메타데이터 필드 `woman running` 에서 일치하는 항목을 찾습니다.
1. 의 일치 `woman running` 를 스마트 태그로 지정합니다.
1. 은 스마트 태그 `woman` 에 있거나 `running` 있는 것과 일치합니다.
