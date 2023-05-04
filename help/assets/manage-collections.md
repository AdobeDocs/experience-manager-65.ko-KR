---
title: 디지털 자산 컬렉션 관리
description: 컬렉션 만들기, 보기, 삭제, 편집 및 다운로드와 같은 자산 컬렉션을 관리하는 작업을 알아봅니다.
contentOwner: AG
mini-toc-levels: 1
role: User
feature: Collections,Asset Management
exl-id: 2117b2de-8024-4aa8-9ce0-68a156928356
source-git-commit: 3d713021ac410ca2925a282c5dfca98ed4e483ee
workflow-type: tm+mt
source-wordcount: '2203'
ht-degree: 14%

---

# 컬렉션 관리 {#managing-collections}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기를 클릭하십시오.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/manage-collections.html?lang=en) |
| AEM 6.5 | 이 문서 |

컬렉션은 내의 자산 세트입니다 [!DNL Adobe Experience Manager Assets]. 컬렉션을 사용하여 사용자 간에 에셋을 공유합니다. 이 집합은 검색 결과를 기반으로 하는 정적 컬렉션 또는 동적 컬렉션일 수 있습니다.

폴더와 달리 컬렉션에는 서로 다른 위치의 에셋이 포함될 수 있습니다. 보기, 편집 등을 포함하여 서로 다른 수준의 권한이 할당된 다양한 사용자와 컬렉션을 공유할 수 있습니다.

사용자와 여러 컬렉션을 공유할 수 있습니다. 각 컬렉션에는 에셋에 대한 참조가 포함되어 있습니다. 에셋의 참조 무결성은 컬렉션에 간에 유지됩니다.

컬렉션은 자산을 수집하는 방식에 따라 다음 유형입니다.

* 자산, 폴더 및 기타 컬렉션의 정적 참조 목록을 포함하는 컬렉션입니다.

* 검색 기준에 따라 자산을 동적으로 포함하는 스마트 컬렉션입니다.

## 컬렉션 콘솔 액세스 {#navigating-the-collections-console}

를 열려면 **[!UICONTROL 컬렉션]**&#x200B;에서 [!DNL Experience Manager] 인터페이스, **[!UICONTROL 자산]** > **[!UICONTROL 컬렉션]**.

## 컬렉션 생성 {#creating-a-collection}

다음 중 한 방법으로 컬렉션을 만들 수 있습니다 [정적 참조](#creating-a-collection-with-static-references) 또는 [검색 기준 기반 필터](#creating-a-smart-collection). Lightbox에서 컬렉션을 만들 수도 있습니다.

### 정적 참조를 사용하여 컬렉션 만들기 {#creating-a-collection-with-static-references}

정적 참조와 함께 컬렉션을 만들 수 있습니다. 예를 들어 자산, 폴더, 컬렉션, 스핀 세트 및 이미지 세트에 대한 참조가 있는 컬렉션입니다.

1. 로 이동합니다 **[!UICONTROL 컬렉션]** 콘솔.
1. 도구 모음에서 **[!UICONTROL 만들기]**.
1. 에서 **[!UICONTROL 컬렉션 만들기]** 페이지에서 컬렉션에 대한 제목과 선택적 설명을 입력합니다.
1. Add members to the collection and assign appropriate permissions. Alternatively, select **[!UICONTROL Public Collection]** to allow all users to access the collection.

   >[!NOTE]
   >
   >구성원이 다른 사용자와 컬렉션을 공유할 수 있도록 하려면 `dam-users` 경로에서 읽기 권한 그룹 `home/users`. 사용자를에 대한 권한 부여 `/content/dam/collections` 사용자가 팝업 목록에서 컬렉션을 볼 수 있는 위치입니다. 또는 사용자를 `dam-users` 그룹에 속해 있어야 합니다.

1. (선택 사항) 컬렉션에 대한 축소판 이미지를 추가합니다.
1. 클릭 **[!UICONTROL 만들기]**&#x200B;를 클릭한 다음 **[!UICONTROL 확인]** 을 클릭하여 대화 상자를 닫습니다. A collection with the specified title and properties is opened in the Collections console.

   >[!NOTE]
   >
   >[!DNL Experience Manager Assets] 자산 폴더에 대한 검토 작업을 만드는 방법과 유사한 방식으로 컬렉션에 대한 검토 작업을 만들 수 있습니다.

   컬렉션에 자산을 추가하려면 [!DNL Assets] 사용자 인터페이스. 자세한 내용은 [컬렉션에 자산 추가](#adding-assets-to-a-collection).

### 드롭존을 사용하여 컬렉션 만들기 {#create-collections-using-dropzone}

에서 자산을 드래그할 수 있습니다 [!DNL Assets] 컬렉션에 대한 사용자 인터페이스. 컬렉션의 사본을 만들고 자산을 여기에 드래그할 수도 있습니다.

1. 에서 [!DNL Assets] 사용자 인터페이스에서 컬렉션에 추가할 자산을 선택합니다.
1. 자산을 로 드래그합니다. **[!UICONTROL 컬렉션에 놓기]** 영역. 또는 **[!UICONTROL 대상 컬렉션]** 를 클릭합니다.

   ![drop_in_collection](assets/drop_in_collection.png)

1. 에서 **[!UICONTROL 컬렉션에 추가]** 페이지를 클릭한 다음 **[!UICONTROL 컬렉션 만들기]** 를 클릭합니다.

   기존 컬렉션에 자산을 추가하려면 페이지에서 해당 자산을 선택하고 **[!UICONTROL 추가]**. By default, the most recently updated collection is selected.

1. In the **[!UICONTROL Create New Collection]** dialog, specify a name for the collection. If you want the collection to be accessible to all users, select **[!UICONTROL Public Collection]**.
1. 클릭 **[!UICONTROL 계속]** 컬렉션을 만들려면

### 스마트 컬렉션 만들기 {#creating-a-smart-collection}

Smart Collection에서는 검색 기준을 사용하여 자산을 동적으로 채웁니다. 폴더나 파일 및 폴더가 아니라 파일만 사용하여 Smart Collection을 만들 수 있습니다.

스마트 컬렉션을 만들려면 다음 단계를 수행합니다.

1. 로 이동합니다 [!DNL Assets] 사용자 인터페이스를 사용하고 검색을 클릭합니다.

1. Omnisearch 상자에 검색 키워드를 입력하고 을 선택합니다 `Enter`. 필터 패널을 열고 검색 필터를 적용합니다.

1. 에서 **[!UICONTROL 파일 및 폴더]** 목록, 선택 **[!UICONTROL 파일]**.

   ![files_option](assets/files_option.png)

1. 클릭 **[!UICONTROL 스마트 컬렉션 저장]**.

1. 컬렉션 이름을 지정합니다. 선택 **[!UICONTROL 공용]** 뷰어 역할을 가진 DAM 사용자 그룹을 스마트 컬렉션에 추가

   ![save_collection](assets/save_collection.png)

   >[!NOTE]
   >
   >선택하는 경우 **[!UICONTROL 공용]**&#x200B;를 만들면 스마트 컬렉션을 만든 후에 소유자 역할을 가진 모든 사람이 스마트 컬렉션을 사용할 수 있습니다. 취소 **[!UICONTROL 공용]** 옵션을 선택하면 DAM 사용자 그룹이 더 이상 스마트 컬렉션과 연결되지 않습니다.

1. 클릭 **[!UICONTROL 저장]** 스마트 컬렉션을 만들려면, 메시지 상자를 닫고 프로세스를 완료합니다.

   The new smart collection is also added to the **[!UICONTROL Saved Searches]** list.

   ![collection_listing](assets/collection_listing.png)

   의 레이블 **[!UICONTROL 스마트 선택 만들기]** 옵션 변경 **[!UICONTROL 스마트 선택 편집]**. To edit the settings of the smart collection, select **[!UICONTROL Files]** from the **[!UICONTROL Files &amp; Folders]** list. 을(를) 클릭합니다. **[!UICONTROL 스마트 선택 편집]** ![스마트 컬렉션 편집](assets/do-not-localize/edit-smart-collection.png) 선택 사항입니다.

## 컬렉션에 에셋 추가 {#adding-assets-to-a-collection}

참조된 자산 또는 폴더 목록을 포함하는 컬렉션에 자산을 추가할 수 있습니다. 스마트 컬렉션은 검색 쿼리를 사용하여 자산을 채웁니다. 따라서 자산 및 폴더에 대한 정적 참조는 적용할 수 없습니다.

1. 에서 [!DNL A]ssets 사용자 인터페이스를 선택하고 자산을 선택한 다음 **[!UICONTROL 대상 컬렉션]** ![컬렉션에 추가](assets/do-not-localize/add-to-collection.png) 를 클릭합니다.
또는 자산을 로 드래그할 수 있습니다 **[!UICONTROL 컬렉션에 놓기]** 인터페이스 영역입니다. 영역의 레이블이 로 변경될 때 자산을 추가합니다 **[!UICONTROL 추가할 드롭]**.

1. 에서 **[!UICONTROL 컬렉션에 추가]** 페이지에서 자산을 추가할 컬렉션을 선택합니다.

1. 클릭 **[!UICONTROL 추가]**&#x200B;를 클릭한 다음 확인 메시지를 닫습니다. 자산이 컬렉션에 추가됩니다.

## 스마트 컬렉션 편집 {#editing-a-smart-collection}

스마트 컬렉션은 검색을 저장하여 작성되므로, [저장된 검색](#saved-searches).

1. 에서 [!DNL Assets] 사용자 인터페이스에서 검색 옵션을 클릭합니다. ![검색 옵션](assets/do-not-localize/search_icon.png) 를 클릭합니다.
1. Omnisearch 상자에 커서를 놓고 `Return` 키.
1. 에서 [!DNL Experience Manager] 인터페이스에서 [필터] 패널을 엽니다.
1. From the **[!UICONTROL Saved Searches]** list, select the smart collection you want to modify. The Search panel displays the filters configured for the saved search.

   ![select_smart_collection](assets/select_smart_collection.png)

1. 에서 **[!UICONTROL 파일 및 폴더]** 목록, 선택 **[!UICONTROL 파일]**.
1. 필요에 따라 하나 이상의 필터를 수정합니다. **[!UICONTROL 스마트 컬렉션 편집]**&#x200B;을 클릭합니다.

   스마트 컬렉션의 이름을 편집할 수도 있습니다.

   ![edit_smart_collectiondialog](assets/edit_smart_collectiondialog.png)

1. **[!UICONTROL 저장]**&#x200B;을 클릭합니다. 다음 **[!UICONTROL 스마트 컬렉션 편집]** 대화 상자가 나타납니다.
1. 클릭 **[!UICONTROL 덮어쓰기]** 원본 스마트 컬렉션을 편집된 컬렉션으로 대체하려면 또는 을 선택합니다 **[!UICONTROL 다른 이름으로 저장]** 편집한 컬렉션을 별도로 저장하려면
1. 확인 대화 상자에서 **[!UICONTROL 저장]** 프로세스를 완료합니다.

## 컬렉션 메타데이터 보기 및 편집 {#view-edit-collection-metadata}

컬렉션 메타데이터는 추가된 태그를 포함하여 컬렉션에 대한 데이터를 포함합니다.

1. 에서 [!UICONTROL 컬렉션] 콘솔에서 컬렉션을 선택하고 **[!UICONTROL 속성]** 를 클릭합니다.
1. In the **[!UICONTROL Collection Metadata]** page, view the collection metadata from the **[!UICONTROL Basic]** and **[!UICONTROL Advanced]** tabs.
1. 필요에 따라 메타데이터를 수정합니다. 변경 사항을 저장하려면 **[!UICONTROL 저장 및 닫기]** 를 클릭합니다.

## 여러 컬렉션의 메타데이터 일괄적으로 편집 {#editing-collection-metadata-in-bulk}

여러 컬렉션의 메타데이터를 동시에 편집할 수 있습니다. 이 기능을 사용하면 여러 컬렉션에서 공통 메타데이터를 빠르게 복제할 수 있습니다.

1. 컬렉션 콘솔에서 컬렉션을 두 개 이상 선택합니다.
1. 도구 모음에서 **[!UICONTROL 속성]**.
1. In the **[!UICONTROL Collection Metadata]** page, edit the metadata under the **[!UICONTROL Basic]** and **[!UICONTROL Advanced]** tabs, as necessary.
1. 특정 컬렉션에 대한 메타데이터 속성을 보려면 컬렉션 목록에서 나머지 컬렉션 선택을 취소합니다. 메타데이터 편집기 필드는 특정 컬렉션의 메타데이터로 채워집니다.

   >[!NOTE]
   >
   >* 에서 [!UICONTROL 속성] 페이지에서 선택한 항목을 취소하여 컬렉션 목록에서 컬렉션을 제거할 수 있습니다. 컬렉션 목록에는 기본적으로 선택된 모든 컬렉션이 있습니다. [!DNL Experience Manager] 제거할 컬렉션의 메타데이터는 업데이트하지 않습니다.
   >* 목록의 맨 위에서 가까운 확인란을 선택합니다 **[!UICONTROL 제목]** 컬렉션 선택 및 목록 지우기 간을 전환하려면.


1. 클릭 **[!UICONTROL 저장 및 닫기]** 도구 모음에서 확인 대화 상자를 닫습니다.
1. 기존 메타데이터에 새 메타데이터를 추가하려면 을 선택합니다 **[!UICONTROL 추가 모드]**. If you do not select this option, the new metadata replaces the existing metadata in the fields. 클릭 **[!UICONTROL 제출]**.

   >[!NOTE]
   >
   >선택한 컬렉션에 대해 추가하는 메타데이터는 이러한 컬렉션에 대한 이전 메타데이터를 덮어씁니다. 를 사용하십시오 [!UICONTROL 추가 모드] 여러 값을 포함할 수 있는 필드에서 기존 메타데이터에 새 값을 추가하려면 단일 값 필드를 항상 덮어씁니다. 에 추가하는 모든 태그 [!UICONTROL 태그] 필드가 메타데이터의 기존 태그 목록에 추가됩니다.

메타데이터를 사용자 지정하는 방법 [!UICONTROL 속성] 페이지에서 메타데이터 속성 추가, 수정, 삭제를 비롯한 스키마 편집기를 사용합니다.

>[!TIP]
>
>벌크 편집 방법은 컬렉션에서 사용할 수 있는 자산에 대해 작동합니다. 여러 폴더 간에 사용할 수 있거나 공통 기준과 일치하는 자산의 경우 다음을 수행할 수 있습니다 [검색 후 메타데이터 대량 업데이트](/help/assets/search-assets.md#metadataupdates).

## 컬렉션 검색 {#searching-collections}

컬렉션 콘솔에서 컬렉션을 검색할 수 있습니다. Omnisearch 상자에서 키워드로 검색할 경우, [!DNL Assets] 컬렉션 이름, 메타데이터 및 컬렉션에 추가된 태그를 검색합니다.

최상위 수준에서 컬렉션을 검색하는 경우 개별 컬렉션만 검색 결과에 반환됩니다. [!DNL Assets] 또는 컬렉션 내의 폴더는 제외됩니다. 다른 모든 경우(예: 개별 컬렉션 내 또는 폴더 계층 구조) 모든 관련 자산, 폴더 및 컬렉션이 반환됩니다.

## 컬렉션 내에서 검색 {#searching-within-collections}

컬렉션 콘솔에서 컬렉션을 클릭하여 엽니다.

컬렉션 내에서, [!DNL Experience Manager] 검색 기능은 보고 있는 컬렉션 내의 자산(및 해당 태그 및 메타데이터)으로 제한됩니다. 폴더 내에서 검색하면 현재 폴더 내에서 일치하는 모든 자산 및 하위 폴더가 반환됩니다. 컬렉션 내에서 검색할 때 컬렉션의 직접 멤버인 일치하는 자산, 폴더 및 기타 컬렉션만 반환됩니다.

## 컬렉션 설정 편집 {#editing-collection-settings}

제목 및 설명과 같은 컬렉션 설정을 편집하거나 컬렉션에 구성원을 추가할 수 있습니다.

1. 컬렉션을 선택하고 **[!UICONTROL 설정]** 클릭합니다. 또는 **[!UICONTROL 설정]** 컬렉션 축소판에서의 빠른 작업.
1. Modify the collection settings in the **[!UICONTROL Collection Settings]** page. 예를 들어, 에 설명된 대로 컬렉션 제목, 설명, 멤버 및 권한을 수정합니다 [컬렉션 추가](#creating-a-collection).

1. 변경 사항을 저장하려면 **[!UICONTROL 저장]**.

## 컬렉션 삭제 {#deleting-a-collection}

1. 컬렉션 콘솔에서 컬렉션을 한 개 이상 선택하고 도구 모음에서 삭제 를 클릭합니다.

1. 대화 상자에서 **[!UICONTROL 삭제]** 를 클릭하여 삭제 작업을 확인합니다.

   >[!NOTE]
   >
   >다음 방법으로 스마트 컬렉션을 삭제할 수도 있습니다. [저장된 검색 삭제](#saved-searches).

## 컬렉션 다운로드 {#downloading-a-collection}

컬렉션을 다운로드하면 폴더 및 하위 컬렉션을 포함하여 컬렉션 내의 자산의 전체 계층 구조가 다운로드됩니다.

1. 컬렉션 콘솔에서 다운로드할 컬렉션을 하나 이상 선택합니다.
1. 도구 모음에서 **[!UICONTROL 다운로드]**.
1. 에서 **[!UICONTROL 다운로드]** 대화 상자 **[!UICONTROL 다운로드]**. 컬렉션 내에서 자산의 표현물을 다운로드하려면 를 선택합니다 **[!UICONTROL 표현물]**. 을(를) 선택합니다 **[!UICONTROL 이메일]** 컬렉션 소유자에게 이메일 알림을 보내는 옵션.

   다운로드할 컬렉션을 선택하면 컬렉션 아래의 전체 폴더 계층 구조가 다운로드됩니다. 개별 폴더에 다운로드한 각 컬렉션(상위 컬렉션 아래에 중첩된 하위 컬렉션의 자산 포함)을 포함하려면 를 선택합니다 **[!UICONTROL 각 자산에 대해 별도의 폴더를 만듭니다]**.

## 중첩된 컬렉션 만들기 {#creating-nested-collections}

다른 컬렉션에 컬렉션을 추가하여 중첩된 컬렉션을 만들 수 있습니다.

1. 컬렉션 콘솔에서 원하는 컬렉션이나 컬렉션 그룹을 선택하고 **[!UICONTROL 대상 컬렉션]** 클릭합니다.

1. 에서 **[!UICONTROL 컬렉션에 추가]** 페이지에서 컬렉션을 추가할 컬렉션을 선택합니다.

   >[!NOTE]
   >
   >가장 최근에 업데이트된 컬렉션은 기본적으로 **[!UICONTROL 컬렉션에 추가]** 페이지.

1. 클릭 **[!UICONTROL 추가]**. 컬렉션이 **[!UICONTROL 대상 선택]** 페이지. 메시지를 닫고 프로세스를 완료합니다.

>[!NOTE]
>
>스마트 컬렉션은 중첩할 수 없습니다. 즉, 스마트 컬렉션에는 다른 컬렉션이 포함될 수 없습니다.

## 저장된 검색 {#saved-searches}

에서 [!DNL Assets] 사용자 인터페이스에서는 특정 규칙, 검색 기준 또는 사용자 지정 검색 패싯을 기반으로 자산을 검색하거나 필터링할 수 있습니다. If you save these as **[!UICONTROL Saved Searches]**, you can access them later from the **[!UICONTROL Saved Searches]** list in the Filter panel. Creating a saved search also creates a smart collection.

![saves_searches_list](assets/saved_searches_list.png)

Saved searches are created when you create a smart collection. Smart collections are automatically added to the **[!UICONTROL Saved Searches]** list. 다음 [!UICONTROL 저장된 검색] 컬렉션에 대한 쿼리가 `dam:query` 상대 위치의 CRXDE에 있는 속성 `/content/dam/collections/`. 저장 및 목록에 표시된 저장된 검색에서 저장할 수 있는 검색에는 제한이 없습니다.

>[!NOTE]
>
>정적 컬렉션을 공유하는 것과 동일한 방법으로 스마트 컬렉션을 공유할 수 있습니다.

저장된 검색을 편집하는 것은 스마트 컬렉션을 편집하는 것과 같습니다. 자세한 내용은 [스마트 컬렉션 편집](#editing-a-smart-collection).

저장된 검색을 삭제하려면 다음 단계를 수행합니다.

1. 에서 [!DNL Assets] 사용자 인터페이스, 검색 클릭 ![검색 옵션](assets/do-not-localize/search_icon.png).
1. Omnisearch 필드에 커서를 두고 `Return` 키.
1. 에서 [!DNL Experience Manager] 인터페이스에서 [필터] 패널을 엽니다.
1. 에서 **[!UICONTROL 저장된 검색]** 목록, **[!UICONTROL 삭제]** 삭제할 스마트 컬렉션 옆에 있습니다.

   ![select_smart_collection](assets/select_smart_collection.png)

1. 대화 상자에서 **[!UICONTROL 삭제]** 저장된 검색을 삭제합니다.

## 컬렉션에서 워크플로우 실행 {#running-a-workflow-on-a-collection}

컬렉션 내의 자산에 대한 워크플로우를 실행할 수 있습니다. 컬렉션에 중첩된 컬렉션이 포함되어 있으면 중첩된 컬렉션 내의 자산에서도 워크플로우가 실행됩니다. 그러나 컬렉션과 중첩된 컬렉션에 중복 자산이 포함되어 있는 경우 워크플로우는 해당 자산에 대해 한 번만 실행됩니다.

1. 열기 **[!UICONTROL 자산]** > **[!UICONTROL 컬렉션]**. 특정 컬렉션에서 워크플로우를 실행하려면 선택합니다.
1. 열기 **[!UICONTROL 타임라인]** 레일. 클릭 ![V자 위로](assets/do-not-localize/chevron-up-icon.png) 을(를) 클릭합니다. **[!UICONTROL 워크플로우 시작]**.
1. In the **[!UICONTROL Start Workflow]** section, select a workflow model from the list. For example, select the **[!UICONTROL DAM Update Asset]** model.
1. 워크플로우의 제목을 입력하고 **[!UICONTROL 시작]**.
1. 대화 상자에서 **[!UICONTROL 계속]**. 워크플로우는 선택한 컬렉션의 모든 자산을 처리합니다.

>[!MORELIKETHIS]
>
>* [Experience Manager Assets 이메일 알림 구성](/help/sites-administering/notification.md#assetsconfig)
>* [컬렉션에 대한 검토 작업 만들기](bulk-approval.md)

