---
title: 디지털 자산 컬렉션 관리
description: 컬렉션 만들기, 보기, 삭제, 편집 및 다운로드 등 자산 컬렉션을 관리하는 작업에 대해 학습합니다.
contentOwner: AG
mini-toc-levels: 1
role: Business Practitioner
feature: Collections,Asset Management
translation-type: tm+mt
source-git-commit: aec4530fa93eacd151ca069c2da5d1bc92408e10
workflow-type: tm+mt
source-wordcount: '2185'
ht-degree: 0%

---


# 컬렉션 관리 {#managing-collections}

컬렉션은 [!DNL Adobe Experience Manager Assets] 내의 자산 집합입니다. 컬렉션을 사용하여 사용자 간에 자산을 공유합니다. 이 집합은 검색 결과를 기반으로 하는 정적 컬렉션 또는 동적 컬렉션이 될 수 있습니다.

폴더와 달리 컬렉션은 다른 위치의 자산을 포함할 수 있습니다. 보기, 편집 등 다양한 수준의 권한이 할당된 다양한 사용자와 컬렉션을 공유할 수 있습니다.

여러 컬렉션을 사용자와 공유할 수 있습니다. 각 컬렉션에는 자산에 대한 참조가 포함되어 있습니다. 컬렉션 전체에서 자산의 참조 무결성이 유지됩니다.

컬렉션은 자산을 수집하는 방법에 따라 다음 유형의 컬렉션입니다.

* 자산, 폴더 및 기타 컬렉션의 정적 참조 목록이 포함된 컬렉션입니다.

* 검색 조건을 기반으로 자산을 동적으로 포함하는 스마트 컬렉션입니다.

## 컬렉션 콘솔 {#navigating-the-collections-console} 액세스

**[!UICONTROL 컬렉션]**&#x200B;을 열려면 [!DNL Experience Manager] 인터페이스에서 **[!UICONTROL 자산]** > **[!UICONTROL 컬렉션]**&#x200B;으로 이동합니다.

## 컬렉션 {#creating-a-collection} 만들기

[정적 참조](#creating-a-collection-with-static-references) 또는 [검색 조건 기반 필터](#creating-a-smart-collection)를 기준으로 컬렉션을 만들 수 있습니다. 라이트박스에서 컬렉션을 만들 수도 있습니다.

### 정적 참조 {#creating-a-collection-with-static-references}을(를) 사용하여 컬렉션 만들기

정적 참조를 사용하여 컬렉션을 만들 수 있습니다. 예를 들어 자산, 폴더, 컬렉션, 스핀 세트 및 이미지 세트에 대한 참조가 있는 컬렉션을 만들 수 있습니다.

1. **[!UICONTROL 컬렉션]** 콘솔로 이동합니다.
1. 도구 모음에서 **[!UICONTROL 만들기]**&#x200B;를 클릭합니다.
1. **[!UICONTROL 컬렉션 만들기]** 페이지에서 컬렉션에 대한 제목과 선택적 설명을 입력합니다.
1. 구성원을 컬렉션에 추가하고 적절한 권한을 할당합니다. 또는 모든 사용자가 컬렉션에 액세스할 수 있도록 하려면 **[!UICONTROL 공개 컬렉션]**&#x200B;을 선택합니다.

   >[!NOTE]
   >
   >구성원이 다른 사용자와 컬렉션을 공유할 수 있도록 하려면 `home/users` 경로에서 `dam-users` 그룹 읽기 권한을 제공합니다. 사용자가 팝업 목록에서 컬렉션을 볼 수 있도록 `/content/dam/collections` 위치의 사용자에게 권한을 부여합니다. 또는 사용자를 `dam-users` 그룹의 일부로 만듭니다.

1. (선택 사항) 컬렉션의 축소판 이미지를 추가합니다.
1. **[!UICONTROL 만들기]**&#x200B;를 클릭한 다음 **[!UICONTROL 확인]**&#x200B;을 클릭하여 대화 상자를 닫습니다. 지정된 제목과 속성이 있는 컬렉션이 컬렉션 콘솔에서 열립니다.

   >[!NOTE]
   >
   >[!DNL Experience Manager Assets] 자산 폴더에 대한 검토 작업을 만드는 방법과 유사한 방법으로 컬렉션에 대한 검토 작업을 만들 수 있습니다.

   컬렉션에 자산을 추가하려면 [!DNL Assets] 사용자 인터페이스로 이동합니다. 자세한 내용은 [컬렉션에 자산 추가](#adding-assets-to-a-collection)를 참조하십시오.

### dropzone {#create-collections-using-dropzone}을(를) 사용하여 컬렉션 만들기

[!DNL Assets] 사용자 인터페이스에서 컬렉션으로 자산을 드래그할 수 있습니다. 컬렉션의 복사본을 만들고 자산을 거기에서 드래그할 수도 있습니다.

1. [!DNL Assets] 사용자 인터페이스에서 컬렉션에 추가할 자산을 선택합니다.
1. 자산을 **[!UICONTROL 컬렉션에 놓기]** 영역으로 드래그합니다. 또는 도구 모음에서 **[!UICONTROL 컬렉션]**&#x200B;을 클릭합니다.

   ![drop_in_collection](assets/drop_in_collection.png)

1. **[!UICONTROL 컬렉션에 추가]** 페이지의 도구 모음에서 **[!UICONTROL 컬렉션 만들기]**&#x200B;를 클릭합니다.

   기존 컬렉션에 자산을 추가하려면 페이지에서 자산을 선택하고 **[!UICONTROL 추가]**&#x200B;를 클릭합니다. 기본적으로 가장 최근에 업데이트된 컬렉션이 선택됩니다.

1. **[!UICONTROL 새 컬렉션 만들기]** 대화 상자에서 컬렉션 이름을 지정합니다. 모든 사용자가 컬렉션에 액세스할 수 있게 하려면 **[!UICONTROL 공개 컬렉션]**&#x200B;을 선택합니다.
1. 컬렉션을 만들려면 **[!UICONTROL 계속]**&#x200B;을 클릭합니다.

### 스마트 컬렉션 {#creating-a-smart-collection} 만들기

스마트 컬렉션은 검색 기준을 사용하여 자산을 동적으로 채웁니다. 폴더나 파일이나 폴더가 아닌 파일만 사용하여 스마트 컬렉션을 만들 수 있습니다.

스마트 컬렉션을 만들려면 다음 단계를 수행합니다.

1. [!DNL Assets] 사용자 인터페이스로 이동하고 검색을 클릭합니다.

1. Omnisearch 상자에 검색 키워드를 입력하고 `Enter`을 선택합니다. [필터] 패널을 열고 검색 필터를 적용합니다.

1. **[!UICONTROL 파일 및 폴더]** 목록에서 **[!UICONTROL 파일]**&#x200B;을 선택합니다.

   ![files_option](assets/files_option.png)

1. **[!UICONTROL 스마트 컬렉션 저장]**&#x200B;을 클릭합니다.

1. 컬렉션 이름을 지정합니다. 뷰어 역할이 있는 DAM 사용자 그룹을 스마트 컬렉션에 추가하려면 **[!UICONTROL 공개]**&#x200B;을 선택합니다.

   ![save_collection](assets/save_collection.png)

   >[!NOTE]
   >
   >**[!UICONTROL 공개]**&#x200B;를 선택하면 스마트 컬렉션을 만든 후 소유자 역할을 가진 모든 사람이 스마트 컬렉션을 사용할 수 있습니다. **[!UICONTROL 공개]** 옵션을 취소하면 DAM 사용자 그룹이 더 이상 스마트 컬렉션과 연결되지 않습니다.

1. 스마트 컬렉션을 만들려면 **[!UICONTROL 저장]**&#x200B;을 클릭한 다음 메시지 상자를 닫고 프로세스를 완료합니다.

   새 스마트 컬렉션은 **[!UICONTROL 저장된 검색]** 목록에도 추가됩니다.

   ![collection_listing](assets/collection_listing.png)

   **[!UICONTROL 스마트 선택 만들기]** 옵션의 레이블이 **[!UICONTROL 스마트 선택 편집]**&#x200B;으로 변경됩니다. 스마트 컬렉션의 설정을 편집하려면 **[!UICONTROL 파일 및 폴더]** 목록에서 **[!UICONTROL 파일]**&#x200B;을 선택합니다. **[!UICONTROL 스마트 선택 편집]** ![스마트 컬렉션 편집](assets/do-not-localize/edit-smart-collection.png) 옵션을 클릭합니다.

## 컬렉션 {#adding-assets-to-a-collection}에 에셋 추가

참조된 자산 또는 폴더 목록이 포함된 자산을 컬렉션에 추가할 수 있습니다. 스마트 컬렉션은 검색 쿼리를 사용하여 자산을 채웁니다. 따라서 자산 및 폴더에 대한 정적 참조는 적용되지 않습니다.

1. [!DNL A]사용자 인터페이스에서 자산을 선택하고 도구 모음에서 **[!UICONTROL 컬렉션에 추가]** ![컬렉션에 추가](assets/do-not-localize/add-to-collection.png)를 클릭합니다.
또는 인터페이스의 **[!UICONTROL 컬렉션에 놓기]** 영역으로 자산을 드래그할 수 있습니다. 영역 레이블이 **[!UICONTROL Drop to Add]**&#x200B;로 변경되면 자산을 추가합니다.

1. **[!UICONTROL 컬렉션에 추가]** 페이지에서 자산을 추가할 컬렉션을 선택합니다.

1. **[!UICONTROL 추가]**&#x200B;를 클릭한 다음 확인 메시지를 닫습니다. 자산이 컬렉션에 추가됩니다.

## 스마트 컬렉션 편집 {#editing-a-smart-collection}

스마트 컬렉션은 [저장된 검색](#saved-searches)의 검색 매개 변수를 수정하여 컨텐츠를 변경할 수 있도록 검색을 저장하여 작성합니다.

1. [!DNL Assets] 사용자 인터페이스의 도구 모음에서 검색 옵션 ![검색 옵션](assets/do-not-localize/search_icon.png)을 클릭합니다.
1. Omnisearch 상자에 커서를 두고 `Return` 키를 선택합니다.
1. [!DNL Experience Manager] 인터페이스에서 [필터] 패널을 엽니다.
1. **[!UICONTROL 저장된 검색]** 목록에서 수정할 스마트 컬렉션을 선택합니다. 검색 패널에는 저장된 검색에 대해 구성된 필터가 표시됩니다.

   ![select_smart_collection](assets/select_smart_collection.png)

1. **[!UICONTROL 파일 및 폴더]** 목록에서 **[!UICONTROL 파일]**&#x200B;을 선택합니다.
1. 필요에 따라 필터를 하나 이상 수정합니다. **[!UICONTROL 스마트 컬렉션 편집]**&#x200B;을 클릭합니다.

   스마트 컬렉션의 이름을 편집할 수도 있습니다.

   ![edit_smart_collectiondialog](assets/edit_smart_collectiondialog.png)

1. **[!UICONTROL 저장]**&#x200B;을 클릭합니다. **[!UICONTROL 스마트 컬렉션 편집]** 대화 상자가 나타납니다.
1. 원본 스마트 컬렉션을 편집된 컬렉션으로 바꾸려면 **[!UICONTROL 덮어쓰기]**&#x200B;를 클릭합니다. 또는 **[!UICONTROL 다른 이름으로 저장을 선택하여 편집한 컬렉션을 별도로 저장합니다.]**
1. 확인 대화 상자에서 **[!UICONTROL 저장]**&#x200B;을 클릭하여 프로세스를 완료합니다.

## 컬렉션 메타데이터 보기 및 편집 {#view-edit-collection-metadata}

컬렉션 메타데이터는 추가되는 모든 태그를 포함하여 컬렉션에 대한 데이터로 구성됩니다.

1. [!UICONTROL 컬렉션] 콘솔에서 컬렉션을 선택하고 도구 모음에서 **[!UICONTROL 속성]**&#x200B;을 클릭합니다.
1. **[!UICONTROL 컬렉션 메타데이터]** 페이지에서 **[!UICONTROL 기본]** 및 **[!UICONTROL 고급]** 탭의 컬렉션 메타데이터를 봅니다.
1. 필요에 따라 메타데이터를 수정합니다. 변경 내용을 저장하려면 도구 모음에서 **[!UICONTROL 저장 및 닫기]**&#x200B;를 클릭합니다.

## 여러 컬렉션의 메타데이터를 일괄 {#editing-collection-metadata-in-bulk} 편집

여러 컬렉션의 메타데이터를 동시에 편집할 수 있습니다. 이 기능은 여러 컬렉션의 일반 메타데이터를 빠르게 복제하는 데 도움이 됩니다.

1. 컬렉션 콘솔에서 두 개 이상의 컬렉션을 선택합니다.
1. 도구 모음에서 **[!UICONTROL 속성]**&#x200B;을 클릭합니다.
1. **[!UICONTROL 컬렉션 메타데이터]** 페이지에서 필요에 따라 **[!UICONTROL 기본]** 및 **[!UICONTROL 고급]** 탭 아래의 메타데이터를 편집합니다.
1. 특정 컬렉션에 대한 메타데이터 속성을 보려면 컬렉션 목록에서 나머지 컬렉션 선택을 취소합니다. 메타데이터 편집기 필드는 특정 컬렉션에 대한 메타데이터로 채워집니다.

   >[!NOTE]
   >
   >* [!UICONTROL 속성] 페이지에서 선택한 항목을 취소하여 컬렉션 목록에서 컬렉션을 제거할 수 있습니다. 컬렉션 목록에는 기본적으로 선택된 모든 컬렉션이 있습니다. [!DNL Experience Manager] 에서 제거하는 컬렉션의 메타데이터를 업데이트하지 않습니다.
   >* 목록 맨 위에서 **[!UICONTROL 제목]** 옆의 확인란을 선택하여 컬렉션을 선택하고 목록을 지우는 간을 전환합니다.


1. 도구 모음에서 **[!UICONTROL 저장 및 닫기]**&#x200B;를 클릭한 다음 확인 대화 상자를 닫습니다.
1. 기존 메타데이터에 새 메타데이터를 추가하려면 **[!UICONTROL 추가 모드]**&#x200B;를 선택합니다. 이 옵션을 선택하지 않으면 새 메타데이터가 필드에 있는 기존 메타데이터를 대체합니다. **[!UICONTROL 제출]**&#x200B;을 클릭합니다.

   >[!NOTE]
   >
   >선택한 컬렉션에 대해 추가하는 메타데이터는 이러한 컬렉션에 대한 이전 메타데이터를 덮어씁니다. 여러 값을 포함할 수 있는 필드의 기존 메타데이터에 새 값을 추가하려면 [!UICONTROL 추가 모드]를 사용합니다. 단일 값 필드는 항상 덮어쓰여집니다. [!UICONTROL 태그] 필드에 추가하는 모든 태그는 메타데이터의 기존 태그 목록에 추가됩니다.

메타데이터 속성 추가, 수정, 삭제를 포함하여 메타데이터 [!UICONTROL 속성] 페이지를 사용자 정의하려면 스키마 편집기를 사용합니다.

>[!TIP]
>
>벌크 편집 방법은 컬렉션에서 사용할 수 있는 자산에 대해 작동합니다. 폴더 간에 사용할 수 있거나 일반적인 기준과 일치하는 자산의 경우 [검색 후 메타데이터를 일괄 업데이트하는 것이 가능합니다.](/help/assets/search-assets.md#metadataupdates)

## 컬렉션 검색 {#searching-collections}

컬렉션 콘솔에서 컬렉션을 검색할 수 있습니다. Omnisearch 상자에서 키워드를 사용하여 검색할 때 [!DNL Assets]은 컬렉션 이름, 메타데이터 및 컬렉션에 추가된 태그를 검색합니다.

최상위 수준에서 컬렉션을 검색하면 개별 컬렉션만 검색 결과에 반환됩니다. [!DNL Assets] 또는 컬렉션 내의 폴더가 제외됩니다. 다른 모든 경우(예: 개별 컬렉션 내 또는 폴더 계층 구조) 모든 관련 자산, 폴더 및 컬렉션이 반환됩니다.

## 컬렉션 내에서 검색 {#searching-within-collections}

컬렉션 콘솔에서 컬렉션을 클릭하여 엽니다.

컬렉션 내에서 [!DNL Experience Manager] 검색은 보고 있는 컬렉션 내의 자산(및 해당 태그 및 메타데이터)으로 제한됩니다. 폴더 내에서 검색하면 현재 폴더 내의 일치하는 모든 자산 및 하위 폴더가 반환됩니다. 컬렉션 내에서 검색할 때 컬렉션의 직접 멤버인 일치하는 자산, 폴더 및 기타 컬렉션만 반환됩니다.

## 컬렉션 설정 편집 {#editing-collection-settings}

제목 및 설명과 같은 컬렉션 설정을 편집하거나 컬렉션에 구성원을 추가할 수 있습니다.

1. 컬렉션을 선택하고 도구 모음에서 **[!UICONTROL 설정]**&#x200B;을 클릭합니다. 또는 컬렉션 축소판에서 **[!UICONTROL 설정]** 빠른 작업을 사용합니다.
1. **[!UICONTROL 컬렉션 설정]** 페이지에서 컬렉션 설정을 수정합니다. 예를 들어 [컬렉션 추가](#creating-a-collection)에서 설명한 대로 컬렉션 제목, 설명, 멤버 및 권한을 수정합니다.

1. 변경 내용을 저장하려면 **[!UICONTROL 저장]**&#x200B;을 클릭합니다.

## 컬렉션 {#deleting-a-collection} 삭제

1. 컬렉션 콘솔에서 하나 이상의 컬렉션을 선택하고 도구 모음에서 삭제를 클릭합니다.

1. 대화 상자에서 **[!UICONTROL 삭제]**&#x200B;를 클릭하여 삭제 작업을 확인합니다.

   >[!NOTE]
   >
   >[저장된 검색 삭제](#saved-searches)를 통해 스마트 컬렉션을 삭제할 수도 있습니다.

## 컬렉션 다운로드 {#downloading-a-collection}

컬렉션을 다운로드할 때 폴더 및 하위 컬렉션을 비롯한 컬렉션 내의 자산 계층 전체가 다운로드됩니다.

1. 컬렉션 콘솔에서 다운로드할 컬렉션을 하나 이상 선택합니다.
1. 도구 모음에서 **[!UICONTROL 다운로드]**&#x200B;를 클릭합니다.
1. **[!UICONTROL 다운로드]** 대화 상자에서 **[!UICONTROL 다운로드]**&#x200B;를 클릭합니다. 컬렉션 내의 자산 표현물을 다운로드하려면 **[!UICONTROL 표현물]**&#x200B;을 선택합니다. 컬렉션 소유자에게 이메일 알림을 보내려면 **[!UICONTROL 이메일]** 옵션을 선택합니다.

   다운로드할 컬렉션을 선택하면 컬렉션 아래의 전체 폴더 계층 구조가 다운로드됩니다. 개별 폴더에 다운로드한 각 컬렉션(상위 컬렉션 아래에 중첩된 하위 컬렉션에 있는 에셋 포함)을 포함하려면 **[!UICONTROL 각 에셋에 대해 별도의 폴더 만들기]**&#x200B;를 선택합니다.

## 중첩된 컬렉션 만들기 {#creating-nested-collections}

다른 컬렉션에 컬렉션을 추가하여 중첩된 컬렉션을 만들 수 있습니다.

1. 컬렉션 콘솔에서 원하는 컬렉션 또는 컬렉션 그룹을 선택하고 도구 모음에서 **[!UICONTROL 컬렉션]**&#x200B;을 클릭합니다.

1. **[!UICONTROL 컬렉션에 추가]** 페이지에서 컬렉션을 추가할 컬렉션을 선택합니다.

   >[!NOTE]
   >
   >가장 최근에 업데이트된 컬렉션은 기본적으로 **[!UICONTROL 컬렉션에 추가]** 페이지에서 선택됩니다.

1. **[!UICONTROL 추가]**&#x200B;를 클릭합니다. 컬렉션이 **[!UICONTROL 대상 선택]** 페이지에서 대상 컬렉션에 추가되었음을 확인하는 메시지가 표시됩니다. 메시지를 닫고 프로세스를 완료합니다.

>[!NOTE]
>
>스마트 컬렉션은 중첩될 수 없습니다. 즉, 스마트 컬렉션은 다른 컬렉션을 포함할 수 없습니다.

## 저장된 검색 {#saved-searches}

[!DNL Assets] 사용자 인터페이스에서 특정 규칙, 검색 조건 또는 사용자 지정 검색 패싯을 기반으로 자산을 검색 또는 필터링할 수 있습니다. 이러한 검색 결과를 **[!UICONTROL 저장된 검색]**&#x200B;으로 저장하는 경우 [필터] 패널의 **[!UICONTROL 저장된 검색]** 목록에서 나중에 액세스할 수 있습니다. 저장된 검색을 만들면 스마트 컬렉션도 생성됩니다.

![saved_searches_list](assets/saved_searches_list.png)

스마트 컬렉션을 만들 때 저장된 검색이 생성됩니다. 스마트 컬렉션은 **[!UICONTROL 저장된 검색]** 목록에 자동으로 추가됩니다. 컬렉션에 대한 [!UICONTROL 저장한 검색 결과] 쿼리는 CRXDE의 상대 위치 `/content/dam/collections/`에 있는 `dam:query` 속성에 저장됩니다. 저장할 수 있는 검색과 목록에 표시된 저장된 검색에는 제한이 없습니다.

>[!NOTE]
>
>정적 컬렉션을 공유하는 것과 같은 방법으로 스마트 컬렉션을 공유할 수 있습니다.

저장된 검색을 편집하는 것은 스마트 컬렉션 편집과 동일합니다. 자세한 내용은 [스마트 컬렉션 편집](#editing-a-smart-collection)을 참조하십시오.

저장된 검색을 삭제하려면 다음 단계를 수행합니다.

1. [!DNL Assets] 사용자 인터페이스에서 ![검색 옵션](assets/do-not-localize/search_icon.png)을 클릭합니다.
1. Omnisearch 필드에 커서를 두고 `Return` 키를 선택합니다.
1. [!DNL Experience Manager] 인터페이스에서 [필터] 패널을 엽니다.
1. 삭제할 스마트 컬렉션 옆의 **[!UICONTROL 저장된 검색]** 목록에서 **[!UICONTROL 삭제]**&#x200B;를 클릭합니다.

   ![select_smart_collection](assets/select_smart_collection.png)

1. 대화 상자에서 **[!UICONTROL 삭제]**&#x200B;를 클릭하여 저장된 검색을 삭제합니다.

## 컬렉션 {#running-a-workflow-on-a-collection}에서 워크플로우 실행

컬렉션 내의 자산에 대한 워크플로우를 실행할 수 있습니다. 컬렉션에 중첩된 컬렉션이 포함된 경우 중첩된 컬렉션 내의 자산에서도 워크플로우가 실행됩니다. 그러나 컬렉션과 중첩된 컬렉션에 중복 에셋이 포함되어 있는 경우 해당 에셋에 대해 워크플로우는 한 번만 실행됩니다.

1. **[!UICONTROL 자산]** > **[!UICONTROL 컬렉션]**&#x200B;을 엽니다. 특정 컬렉션에서 워크플로우를 실행하려면 선택합니다.
1. **[!UICONTROL 타임라인]** 레일을 엽니다. ![Chevrup](assets/do-not-localize/chevron-up-icon.png)을 클릭하고 **[!UICONTROL 워크플로우 시작]**&#x200B;을 클릭합니다.
1. **[!UICONTROL 워크플로우 시작]** 섹션의 목록에서 워크플로우 모델을 선택합니다. 예를 들어 **[!UICONTROL DAM 자산 업데이트]** 모델을 선택합니다.
1. 워크플로우의 제목을 입력하고 **[!UICONTROL 시작]**&#x200B;을 클릭합니다.
1. 대화 상자에서 **[!UICONTROL 계속]**&#x200B;을 클릭합니다. 워크플로우는 선택한 컬렉션의 모든 자산을 처리합니다.

>[!MORELIKETHIS]
>
>* [Experience Manager 자산 이메일 알림 구성](/help/sites-administering/notification.md#assetsconfig)
>* [컬렉션에 대한 검토 작업 만들기](bulk-approval.md)

