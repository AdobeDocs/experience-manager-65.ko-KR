---
title: Adobe Enterprise Manager에서 많은 자산 및 컬렉션의 메타데이터를 관리할 수 있습니다.
description: 여러 자산 및 컬렉션의 메타데이터를 동시에 편집하여 일반적인 메타데이터 변경 사항을 신속하게 전파할 수 있습니다.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 23d19d9656d61874cd00a9a2473092be0c53b8f8
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 0%

---


# Manage assets and collections {#managing-multiple-assets-and-collections}

Adobe Enterprise Manager Assets를 사용하면 여러 자산의 메타데이터를 동시에 편집할 수 있으므로 일반적인 메타데이터 변경 사항을 자산에 일괄 적용할 수 있습니다. 여러 컬렉션의 메타데이터를 일괄 편집할 수도 있습니다.

속성 페이지를 사용하여 여러 자산 또는 컬렉션에 대한 메타데이터 변경을 수행합니다.

* 메타데이터 속성을 일반 값으로 변경
* 태그 추가 또는 수정

메타데이터 속성 추가, 수정, 삭제 등 메타데이터 속성 페이지를 사용자 정의하려면 스키마 편집기를 사용합니다.

>[!NOTE]
>
>벌크 편집 방법은 폴더 또는 컬렉션에서 사용할 수 있는 자산에 대해 작동합니다. 여러 폴더에서 사용할 수 있거나 일반적인 기준과 일치하는 자산의 경우 검색 후 메타데이터를 [일괄 업데이트할 수 있습니다](search-assets.md#metadataupdates).

## 여러 자산의 메타데이터 속성 편집 {#editing-metadata-properties-of-multiple-assets}

1. 자산 사용자 인터페이스에서 편집할 자산의 위치로 이동합니다.
1. 공통 속성을 편집할 자산을 선택합니다.
1. 도구 모음에서 **[!UICONTROL 속성]** 아이콘을 클릭하여 선택한 자산에 대한 속성 페이지를 엽니다.

   >[!NOTE]
   >
   >여러 자산을 선택하면 자산에 대해 가장 낮은 공통 상위 양식이 선택됩니다. 즉, 속성 페이지에는 모든 개별 자산의 속성 페이지에서 공통인 메타데이터 필드만 표시됩니다.

1. 다양한 탭에서 선택한 자산에 대한 메타데이터 속성을 수정합니다.
1. 특정 자산에 대한 메타데이터 편집기를 보려면 목록에서 나머지 자산을 선택 취소합니다. 메타데이터 편집기 필드는 특정 자산에 대한 메타데이터로 채워집니다.

   >[!NOTE]
   >
   >* 속성 페이지에서 자산을 선택 취소하여 자산 목록에서 제거할 수 있습니다. 자산 목록에는 기본적으로 모든 자산이 선택되어 있습니다. 목록에서 제거하는 자산에 대한 메타데이터는 업데이트되지 않습니다.
   >* 자산 목록 맨 위에서 **[!UICONTROL 제목]** 근처의 확인란을 선택하여 자산 선택과 목록 지우기 간을 전환합니다.


1. 자산에 대해 다른 메타데이터 스키마를 선택하려면 도구 모음에서 **[!UICONTROL 설정]** 아이콘을 클릭하고 원하는 스키마를 선택합니다.
1. 변경 사항을 저장합니다.
1. 여러 값이 들어 있는 필드에 기존 메타데이터와 함께 새 메타데이터를 추가하려면 추가 모드 **[!UICONTROL 를 선택합니다]**. 이 옵션을 선택하지 않으면 새 메타데이터가 필드에 있는 기존 메타데이터를 대체합니다. 제출을 **[!UICONTROL 클릭합니다]**.

   >[!CAUTION]
   >
   >단일 값 필드의 경우 추가 모드를 선택하더라도 새 메타데이터는 필드의 기존 값에 추가되지 **[!UICONTROL 않습니다]**.

## 일괄 메타데이터 업데이트에 대한 제한 구성 {#configlimit}

DOS와 같은 상황을 방지하기 위해 Enterprise Manager는 Sling 요청에서 지원되는 매개 변수의 수를 제한합니다. 한 번에 많은 자산의 메타데이터를 업데이트할 때 한도에 도달해도 메타데이터가 더 많은 자산에 대해 업데이트되지 않습니다. Enterprise Manager는 로그에 다음 경고를 생성합니다.

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

제한을 변경하려면 **[!UICONTROL 도구]** > **[!UICONTROL 작업]** > **[!UICONTROL 웹 콘솔]** 에 액세스하고 Apache Sapache Request 매개 변수 처리OSGi 구성에 있는 최대 **[!UICONTROL POST 매개 변수의 값을]** Maximum POST 매개 변수 값으로 변경합니다 **** .

>[!MORELIKETHIS]
>
>* [여러 컬렉션의 메타데이터 속성 편집](managing-collections-touch-ui.md#editing-collection-metadata-in-bulk)

