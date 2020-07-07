---
title: 자산 템플릿 [!DNL Adobe Experience Manager Assets].
description: 자산 템플릿 [!DNL Adobe Experience Manager Assets] 과 자산 템플릿을 사용하여 마케팅 자료를 만드는 방법에 대해 알아봅니다.
contentOwner: AG
translation-type: tm+mt
source-git-commit: b59f7471ab9f3c5e6eb3365122262b592c8e6244
workflow-type: tm+mt
source-wordcount: '1553'
ht-degree: 1%

---


# 자산 템플릿 {#asset-templates}

에셋 템플릿은 디지털 및 인쇄 미디어를 위해 시각적으로 풍부한 컨텐츠를 신속하게 재활용할 수 있는 특수 에셋 클래스입니다. 자산 템플릿에는 고정 메시징 섹션과 편집 가능한 섹션이 포함되어 있습니다. 고정 메시징 섹션에는 브랜드 로고 및 편집에 사용할 수 없는 저작권 정보와 같은 독점 컨텐츠가 포함될 수 있습니다. 편집 가능한 섹션에는 메시지를 사용자 지정하기 위해 편집할 수 있는 필드에 시각적 컨텐츠와 텍스트 컨텐츠가 포함될 수 있습니다.

글로벌 사이니지를 보호하면서 제한된 편집 작업을 유연하게 수행할 수 있는 자산 템플릿은 다양한 기능을 위한 컨텐츠 가공물로 빠른 컨텐츠 적응과 배포를 위한 기본 요소에 이상적입니다. 컨텐츠를 재활용하면 인쇄 및 디지털 채널을 관리하는 데 소요되는 비용을 절감하고 이러한 채널에서 전체적이고 일관된 경험을 전달할 수 있습니다.

마케터는 템플릿을 저장 및 관리하고 하나의 기본 템플릿을 사용하여 개인화된 여러 인쇄 경험 [!DNL Experience Manager Assets] 을 손쉽게 만들 수 있습니다. 브로셔, 전단지, 엽서, 명함 등 다양한 유형의 마케팅 자료를 만들어 고객에게 마케팅 메시지를 전달할 수 있습니다. 또한 기존 또는 새로운 인쇄 출력에서 여러 페이지의 인쇄 출력을 취합할 수 있습니다. 무엇보다도 디지털 경험과 인쇄 경험을 동시에 손쉽게 전달하여 사용자에게 일관된 통합 경험을 제공할 수 있습니다.

에셋 템플릿은 대부분 [!DNL Adobe InDesign] 파일이지만 뛰어난 객체 [!DNL Adobe InDesign] 를 만드는 데 있어 숙련도는 문제가 아닙니다. 카탈로그 제작 시 [!DNL Adobe InDesign] 템플릿 필드를 제품 필드와 매핑할 필요는 없습니다. 웹 인터페이스에서 직접 WYSIWYG 모드에서 템플릿을 편집할 수 있습니다. 그러나 편집 변경 사항 [!DNL Adobe InDesign] 을 처리하려면 먼저 [!DNL Experience Manager Assets] 와 통합되도록 구성해야 합니다 [!DNL Adobe InDesign Server].

웹 인터페이스에서 템플릿 [!DNL Adobe InDesign] 을 편집할 수 있으므로 크리에이티브 및 마케팅 담당자 간의 공동 작업을 향상시킬 수 있습니다. 콘텐츠 제작 속도가 향상되어 마케팅 자료 출시 시간을 단축할 수 있습니다.

자산 템플릿으로 다음을 수행할 수 있습니다.

* 웹 인터페이스에서 편집 가능한 템플릿 필드를 수정합니다.
* 글꼴 크기, 스타일, 태그 수준 문자 등 텍스트의 기본 스타일을 제어할 수 있습니다.
* 컨텐츠 선택기를 사용하여 템플릿 내의 이미지를 변경합니다.
* 템플릿 편집 내용을 미리 볼 수 있습니다.
* 여러 템플릿 파일을 병합하여 여러 페이지로 된 아티팩트를 만들 수 있습니다.

담보물 템플릿을 선택하면 편집할 수 있는 템플릿 [!DNL Experience Manager Assets] 사본이 만들어집니다. 원본 템플릿은 그대로 유지되므로 글로벌 사이니지는 그대로 유지되고 브랜드 일관성을 유지하기 위해 다시 사용할 수 있습니다.

업데이트된 파일을 INDD, PDF 또는 JPG 포맷으로 상위 폴더 내에서 내보낼 수 있습니다. 이러한 형식의 출력을 로컬 파일 시스템으로 다운로드할 수도 있습니다.

## 자료 만들기 {#creating-a-collateral}

향후 캠페인을 위한 브로셔, 전단지 및 광고와 같은 디지털 인쇄 가능한 자료를 만들고 아울렛 매장과 전 세계에 공유하는 시나리오를 생각해 보십시오. 템플릿을 기반으로 한 마케팅 자료를 만들어 다양한 채널에서 일관된 고객 경험을 제공할 수 있습니다. 디자이너는 템플릿을 업로드하고 같은 크리에이티브 솔루션을 사용하여 캠페인 템플릿(단일 페이지 또는 여러 페이지)을 만들 수 [!DNL InDesign] [!DNL Experience Manager Assets] 있습니다. 자료를 만들기 전에 하나 이상의 INDD 템플릿을 업로드하여 미리 사용할 수 있도록 [!DNL Experience Manager] 하십시오.

1. 인터페이스에서 자산 [!DNL Experience Manager] 을 클릭합니다 .

1. 옵션에서 템플릿을 **[!UICONTROL 선택합니다]**.

   ![chlimage_1-101](assets/chlimage_1-306.png)

1. 만들기 **[!UICONTROL 를]**&#x200B;클릭한 다음 메뉴에서 만들 자료를 선택합니다. 예를 들어 브로셔를 **[!UICONTROL 선택합니다]**.

   ![chlimage_1-102](assets/chlimage_1-307.png)

1. 하나 이상의 INDD 템플릿을 업로드하여 미리 사용할 수 [!DNL Experience Manager] 있도록 합니다. 브로셔에 사용할 템플릿을 선택하고 다음을 **[!UICONTROL 클릭합니다]**.

   ![chlimage_1-103](assets/chlimage_1-308.png)

1. 브로셔에 대한 이름과 선택적 설명을 지정합니다.

   ![chlimage_1-104](assets/chlimage_1-309.png)

1. (선택 사항) **[!UICONTROL 태그를]** 클릭하고 브로셔에 대해 하나 이상의 태그를 선택합니다. 확인을 **[!UICONTROL 클릭하여]** 선택을 확인합니다.

   ![chlimage_1-105](assets/chlimage_1-310.png)

1. **[!UICONTROL 만들기]**&#x200B;를 클릭합니다. 새 브로셔가 만들어지는지 확인하는 대화 상자가 나타납니다. 열기 **[!UICONTROL 를]** 클릭하여 브로셔를 편집 모드로 엽니다.

   <!--![chlimage_1-106](assets/.png) -->

   또는 대화 상자를 닫고 시작했던 템플릿 페이지의 폴더로 이동하여 만든 브로셔를 확인합니다. 자료 유형이 카드 보기에서 축소판에 나타납니다. 예를 들어 이 경우 축소판에 브로셔 [!UICONTROL 라는] 단어가 표시됩니다.

   ![chlimage_1-107](assets/chlimage_1-312.png)

## 자료 편집 {#editing-a-collateral}

자료를 만든 후 바로 편집할 수 있습니다. 또는 템플릿 [!UICONTROL 페이지] 또는 자산 페이지에서 엽니다.

1. 편집할 자료를 열려면 다음 중 하나를 수행합니다.

   * 자료 제작의 7단계에서 만든 자료(이 경우 브로셔)를 [엽니다](/help/assets/asset-templates.md#creating-a-collateral).
   * 템플릿 페이지에서 담보물을 만든 폴더로 이동하고 [!UICONTROL 담보물 축소판에서 빠른 편집] 작업을 클릭합니다.
   * 자료의 자산 페이지에서 도구 모음에서 **[!UICONTROL 편집을]** 클릭합니다.
   * 자료를 선택하고 도구 모음에서 **[!UICONTROL 편집]** 을 클릭합니다.
   <!--![chlimage_1-108](assets/chlimage_1-313.png) -->

   자산 파인더와 텍스트 편집기가 페이지 왼쪽에 표시됩니다. 텍스트 편집기는 기본적으로 열려 있습니다.

   텍스트 편집기를 사용하여 텍스트 필드에 표시할 텍스트를 수정할 수 있습니다. 글꼴 크기, 스타일, 색상 및 문자를 태그 수준에서 수정할 수 있습니다.

   자산 파인더를 사용하여 내에서 이미지를 찾거나 검색하고 템플릿의 편집 가능한 이미지를 원하는 이미지 [!DNL Experience Manager Assets] 로 바꿀 수 있습니다.

   ![chlimage_1-109](assets/chlimage_1-314.png)

   편집 가능한 파일은 오른쪽에 표시됩니다. 에서 필드를 편집하려면 템플릿의 해당 필드 [!DNL Experience Manager Assets]에 태그가 지정되어 있어야 합니다 [!DNL InDesign]. 즉, 편집할 수 있는 것으로 표시되어야 합니다 [!DNL InDesign].

   ![chlimage_1-110](assets/chlimage_1-315.png)

   >[!NOTE]
   >
   >인스턴스에서 템플릿 [!DNL Experience Manager] 의 데이터를 추출하고 [!DNL InDesign Server] 편집할 수 있도록 하려면 인스턴스와 [!DNL Experience Manager Assets] [!DNL InDesign] 통합되어야 합니다. 자세한 내용은 Experience Manager 에셋을 InDesign Server와 [통합을 참조하십시오](/help/assets/indesign.md).

1. 편집 가능한 필드의 텍스트를 수정하려면 편집 가능한 필드 목록에서 텍스트 필드를 클릭하고 필드의 텍스트를 편집합니다.

   ![chlimage_1-111](assets/chlimage_1-316.png)

   제공된 옵션을 사용하여 글꼴 스타일, 색상 및 크기 등의 텍스트 속성을 편집할 수 있습니다.

1. 미리 **[!UICONTROL 보기를]** 클릭하여 텍스트 변경 내용을 미리 봅니다.

   ![chlimage_1-112](assets/chlimage_1-317.png)

1. 이미지를 교체하려면 **[!UICONTROL 자산 파인더를 클릭합니다]**.

   ![chlimage_1-113](assets/chlimage_1-318.png)

1. 편집 가능한 필드 목록에서 이미지 필드를 선택한 다음 자산 선택기에서 원하는 이미지를 편집 가능한 필드로 드래그합니다.

   ![chlimage_1-114](assets/chlimage_1-319.png)

   키워드, 태그 및 게시 상태를 기반으로 하여 이미지를 검색할 수도 있습니다. 저장소를 [!DNL Experience Manager Assets] 탐색하고 원하는 이미지의 위치로 이동할 수 있습니다.

   ![chlimage_1-115](assets/chlimage_1-320.png)

1. 미리 **[!UICONTROL 보기를]** 클릭하여 이미지를 미리 봅니다.

   ![chlimage_1-116](assets/chlimage_1-321.png)

1. 다중 페이지 담보에서 특정 페이지를 편집하려면 하단에 있는 페이지 탐색기를 사용합니다.

   ![chlimage_1-117](assets/chlimage_1-322.png)

1. 도구 모음 **[!UICONTROL 에서 미리]** 보기를 클릭하여 모든 변경 사항을 미리 봅니다. 완료를 **[!UICONTROL 클릭하여]** 마케팅 자료에 대한 편집 변경 내용을 저장합니다.

   >[!NOTE]
   >
   >미리 보기 및 완료 옵션은 담보물 내의 편집 가능한 이미지 필드에 누락된 아이콘이 없는 경우에만 활성화됩니다. 자료에 아이콘이 없는 경우 템플릿에서 이미지를 확인할 [!DNL Experience Manager] 수 없기 [!DNL InDesign] 때문입니다. 일반적으로 다음 경우 이미지 [!DNL Experience Manager] 를 해결할 수 없습니다.
   >
   >* 이미지는 기본 [!DNL InDesign] 템플릿에 포함되지 않습니다.
   >* 이미지는 로컬 파일 시스템에서 연결됩니다.
   >
   >이미지 [!DNL Experience Manager] 를 해결하려면 다음을 수행합니다.
   >
   >* 템플릿을 만드는 동안 이미지 [!DNL InDesign] 포함(링크 및 포함된 그래픽 [정보 참조](https://helpx.adobe.com/indesign/using/graphics-links.html)).
   >* 로컬 파일 시스템 [!DNL Experience Manager] 에 마운트한 다음 누락된 아이콘을 기존 에셋에 매핑합니다 [!DNL Experience Manager].
   >
   >문서 작업에 대한 자세한 내용은 Experience Manager에서 InDesign 문서를 사용하여 작업하는 [!DNL InDesign] 모범 사례를 참조하십시오 [](https://helpx.adobe.com/experience-manager/kb/best-practices-idd-docs-aem.html).

1. 브로셔에 대한 PDF 변환을 생성하려면 대화 상자에서 Acrobat 옵션을 선택한 다음 **[!UICONTROL 계속을 클릭합니다]**.
1. 이 자료는 사용자가 시작한 폴더에 만들어집니다. 변환을 보려면, 자료를 열고 전역 탐색 목록에서 **[!UICONTROL 표현물]** 을 선택합니다.

   ![chlimage_1-118](assets/chlimage_1-323.png)

1. 변환 목록에서 PDF 변환을 클릭하여 PDF 파일을 다운로드합니다. PDF 파일을 열어 자료를 검토합니다.

   ![chlimage_1-119](assets/chlimage_1-324.png)

## 자료 병합 {#merge-collateral}

1. 인터페이스에서 탐색 [!DNL Experience Manager] 페이지의 자산  을 클릭합니다.

1. 옵션에서 템플릿을 **[!UICONTROL 선택합니다]**.

1. 만들기 **[!UICONTROL 를]** 클릭하고 **[!UICONTROL 메뉴에서 병합]** 선택

   ![chlimage_1-120](assets/chlimage_1-325.png)

1. 템플릿 [!UICONTROL 병합] 페이지에서 **[!UICONTROL 병합을 클릭합니다]**.

   ![chlimage_1-121](assets/chlimage_1-326.png)

1. 병합할 자료의 위치로 이동하고 병합할 자료의 축소판을 클릭하여 선택합니다.

   ![chlimage_1-122](assets/chlimage_1-327.png)

   Omnisearch 상자에서 템플릿을 검색할 수도 있습니다.

   ![chlimage_1-123](assets/chlimage_1-328.png)

   저장소 또는 컬렉션을 [!DNL Experience Manager Assets] 탐색하고 원하는 템플릿의 위치로 이동한 다음 병합할 위치를 선택할 수 있습니다.

   ![chlimage_1-124](assets/chlimage_1-329.png)

   다양한 필터를 적용하여 원하는 템플릿을 검색할 수 있습니다. 예를 들어 파일 유형이나 태그를 기준으로 템플릿을 검색할 수 있습니다.

   ![chlimage_1-125](assets/chlimage_1-330.png)

1. 도구 모음 **[!UICONTROL 에서]** 다음을 클릭합니다.
1. 미리 **[!UICONTROL 보기 및 순서]** 변경 화면에서 필요한 경우 템플릿을 다시 정렬하고 병합할 템플릿 선택을 미리 봅니다. 그런 다음 도구 모음 **[!UICONTROL 에서 [다음]** ]을 클릭합니다.

   ![chlimage_1-126](assets/chlimage_1-331.png)

1. 템플릿 [!UICONTROL 구성] 화면에서 담보물 이름을 지정합니다. 원하는 경우, 적절하다고 생각하는 태그를 지정합니다. PDF 형식으로 출력을 내보내려면 **[!UICONTROL Acrobat(.PDF)을 선택합니다]**. 기본적으로 자료는 JPG 및 [!DNL InDesign] 형식으로 내보내집니다. 여러 페이지로 구성된 자료에 대한 표시 축소판을 변경하려면 축소판 **[!UICONTROL 변경을 클릭합니다]**.

   ![chlimage_1-127](assets/chlimage_1-332.png)

1. 저장 **[!UICONTROL 을]** 클릭한 다음 대화 **[!UICONTROL 상자에서]** 확인을 클릭하여 대화 상자를 닫습니다. 여러 페이지로 구성된 담보가 시작된 폴더에 만들어집니다.

   >[!NOTE]
   >
   >나중에 병합된 자료를 편집하거나 다른 자료를 만들 수 없습니다.

## 모범 사례 및 제한 사항 {#best-practices-limitations-tips}

* 의 [!DNL InDesign] 편집기는 [!DNL Experience Manager] 태그 수준에서 작동하며 단일 태그 아래의 모든 텍스트는 단일 엔티티로 간주됩니다. 편집 시 텍스트 서식 및 스타일을 유지하려면 각 단락(또는 스타일이 다른 텍스트)에 개별적으로 태그를 지정합니다.
