---
title: 자산 템플릿
description: ' [!DNL Adobe Experience Manager Assets] 의 자산 템플릿과 자산 템플릿을 사용하여 마케팅 자료를 만드는 방법에 대해 알아봅니다.'
contentOwner: AG
role: User
feature: Asset Management,Developer Tools
exl-id: 12c92aad-3a1d-486e-a830-31de2fc6d07b
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1576'
ht-degree: 1%

---

# 자산 템플릿 {#asset-templates}

에셋 템플릿은 디지털 및 인쇄 미디어용 시각적으로 풍부한 콘텐츠를 신속하게 재활용할 수 있는 특별한 에셋 클래스입니다. 에셋 템플릿에는 고정 메시징 섹션과 편집 가능 섹션의 두 부분이 포함되어 있습니다. 고정 메시징 섹션에는 편집할 수 없는 브랜드 로고 및 저작권 정보와 같은 독점 콘텐츠가 포함될 수 있습니다. 편집 가능 섹션에는 메시징을 사용자 지정하기 위해 편집할 수 있는 필드에 시각적 및 텍스트 콘텐츠가 포함될 수 있습니다.

글로벌 사이니지의 보안을 유지하면서 제한적인 편집 작업을 할 수 있는 유연성은 자산 템플릿을 다양한 기능의 콘텐츠 아티팩트로 빠른 콘텐츠 적응 및 배포에 이상적인 빌딩 블록으로 만듭니다. 컨텐츠 재활용 기능은 인쇄 및 디지털 채널 관리 비용을 절감하고, 이러한 채널 전반에 걸쳐 총체적이고 일관된 환경을 제공하는 데 도움이 됩니다.

마케터는 [!DNL Experience Manager Assets] 내에서 템플릿을 저장하고 관리할 수 있으며, 단일 기본 템플릿을 사용하여 간편하게 여러 개인 맞춤화된 인쇄 경험을 만들 수 있습니다. 브로셔, 전단지, 엽서, 명함 등 다양한 유형의 마케팅 자료를 만들어 고객에게 마케팅 메시지를 전달할 수 있습니다. 기존 또는 새 인쇄 출력에서 다중 페이지 인쇄 출력을 조합할 수도 있습니다. 무엇보다도 디지털 및 인쇄 환경을 동시에 쉽게 제공하여 사용자에게 일관되고 통합된 환경을 제공할 수 있습니다.

자산 템플릿이 대부분 [!DNL Adobe InDesign]개 파일이지만 [!DNL Adobe InDesign]의 숙련도는 Stellar 아티팩트를 만드는 데 걸림돌이 되지 않습니다. [!DNL Adobe InDesign] 템플릿의 필드를 카탈로그를 만들 때 필요한 제품 필드와 매핑할 필요가 없습니다. 웹 인터페이스에서 직접 WYSIWYG 모드로 템플릿을 편집할 수 있습니다. 그러나 [!DNL Adobe InDesign]이(가) 편집 변경 내용을 처리하려면 먼저 [!DNL Experience Manager Assets]을(를) [!DNL Adobe InDesign Server]과(와) 통합하도록 구성해야 합니다.

웹 인터페이스에서 [!DNL Adobe InDesign] 템플릿을 편집하는 기능은 크리에이티브 및 마케팅 담당자 간의 공동 작업을 강화하는 데 도움이 됩니다. 콘텐츠 속도가 증가하면 마케팅 자료의 마켓 출시 시간이 단축됩니다.

에셋 템플릿으로 다음을 수행할 수 있습니다.

* 웹 인터페이스에서 편집 가능한 템플릿 필드를 수정합니다.
* 태그 수준에서 글꼴 크기, 스타일 및 문자 등 텍스트의 기본 스타일을 제어합니다.
* 콘텐츠 선택기를 사용하여 템플릿 내에서 이미지를 변경합니다.
* 템플릿 편집 내용을 미리 봅니다.
* 여러 템플릿 파일을 병합하여 다중 페이지 아티팩트를 만들 수 있습니다.

담보에 사용할 템플릿을 선택하면 [!DNL Experience Manager Assets]에서 편집할 수 있는 템플릿 복사본을 만듭니다. 원본 템플릿은 그대로 유지되므로 글로벌 사이니지가 그대로 유지되고 브랜드 일관성을 유지하는 데 다시 사용할 수 있습니다.

상위 폴더 내에서 업데이트된 파일을 INDD, PDF 또는 JPG 형식으로 내보낼 수 있습니다. 이러한 형식의 출력을 로컬 파일 시스템에 다운로드할 수도 있습니다.

## 자료 조각 만들기 {#creating-a-collateral}

예정된 캠페인에 대한 브로셔, 전단지 및 광고와 같은 디지털 인쇄 가능한 자료를 만들고 전 세계 아울렛 매장과 공유하는 시나리오를 생각해 보십시오. 템플릿을 기반으로 자료를 만들면 여러 채널에 통합된 고객 경험을 제공할 수 있습니다. 디자이너는 [!DNL InDesign]과(와) 같은 크리에이티브 솔루션을 사용하여 캠페인 템플릿(단일 페이지 또는 다중 페이지)을 만들고 이 템플릿을 [!DNL Experience Manager Assets]에 업로드할 수 있습니다. 자료 조각을 만들기 전에 하나 이상의 INDD 템플릿을 [!DNL Experience Manager]에 업로드하고 미리 사용할 수 있도록 하십시오.

1. [!DNL Experience Manager] 인터페이스에서 [!UICONTROL Assets]을(를) 선택합니다.

1. 옵션에서 **[!UICONTROL 템플릿]**&#x200B;을 선택합니다.

   ![chlimage_1-101](assets/chlimage_1-306.png)

1. **[!UICONTROL 만들기]**&#x200B;를 선택한 다음 메뉴에서 만들려는 보충 자료를 선택하십시오. 예를 들어 **[!UICONTROL 브로셔]**&#x200B;를 선택합니다.

   ![chlimage_1-102](assets/chlimage_1-307.png)

1. 하나 이상의 INDD 템플릿을 [!DNL Experience Manager]에 업로드하고 미리 사용할 수 있습니다. 브로셔의 템플릿을 선택하고 **[!UICONTROL 다음]**&#x200B;을(를) 클릭합니다.
1. 브로셔의 이름과 선택적 설명을 지정합니다.

   ![chlimage_1-104](assets/chlimage_1-309.png)

1. (선택 사항) **[!UICONTROL 태그]**&#x200B;를 클릭하고 브로셔에 사용할 태그를 하나 이상 선택합니다. 선택을 확인하려면 **[!UICONTROL 확인]**&#x200B;을 클릭하세요.
1. **[!UICONTROL 만들기]**&#x200B;를 클릭합니다. 대화 상자에서 새 브로셔가 생성되었음을 확인합니다. 브로셔를 편집 모드로 열려면 **[!UICONTROL 열기]**&#x200B;를 클릭하십시오.

   <!--![chlimage_1-106](assets/.png) -->

   또는 대화 상자를 닫고 시작한 템플릿 페이지의 폴더로 이동하여 작성한 브로셔를 확인합니다. 자료 유형이 카드 보기의 썸네일에 나타납니다. 예를 들어 이 경우 [!UICONTROL 브로셔]라는 단어가 썸네일에 표시됩니다.

   ![chlimage_1-107](assets/chlimage_1-312.png)

## 자료 조각 편집 {#editing-a-collateral}

자료 조각을 만든 후 바로 편집할 수 있습니다. 또는 [!UICONTROL 템플릿] 페이지 또는 에셋 페이지에서 엽니다.

1. 편집할 자료를 열려면 다음 중 하나를 수행합니다.

   * [자료 만들기](/help/assets/asset-templates.md#creating-a-collateral)의 7단계에서 만든 자료(이 경우 브로셔)를 엽니다.
   * 템플릿 페이지에서 보충 자료를 만든 폴더로 이동한 다음 보충 자료의 썸네일에서 [!UICONTROL 편집] 빠른 작업을 클릭합니다.
   * 담보에 대한 자산 페이지의 도구 모음에서 **[!UICONTROL 편집]**&#x200B;을 클릭합니다.
   * 자료를 선택하고 도구 모음에서 **[!UICONTROL 편집]**&#x200B;을 클릭합니다.

   <!--![chlimage_1-108](assets/chlimage_1-313.png) -->

   에셋 파인더 및 텍스트 편집기는 페이지 왼쪽에 표시됩니다. 텍스트 편집기는 기본적으로 열려 있습니다.

   텍스트 편집기를 사용하여 텍스트 필드에 표시할 텍스트를 수정합니다. 태그 수준에서 글꼴 크기, 스타일, 색상 및 문자를 수정할 수 있습니다.

   에셋 파인더를 사용하려면 [!DNL Experience Manager Assets] 내에서 이미지를 검색하거나 검색하고 템플릿의 편집 가능한 이미지를 원하는 이미지로 바꿀 수 있습니다.

   ![chlimage_1-109](assets/chlimage_1-314.png)

   편집 가능한 이미지가 오른쪽에 표시됩니다. [!DNL Experience Manager Assets]에서 필드를 편집할 수 있으려면 템플릿의 해당 필드에 [!DNL InDesign]에서 태그를 지정해야 합니다. 즉, [!DNL InDesign]에서 편집 가능으로 표시해야 합니다.

   >[!NOTE]
   >
   >[!DNL Experience Manager Assets]이(가) [!DNL InDesign] 템플릿에서 데이터를 추출하고 편집할 수 있도록 하려면 [!DNL Experience Manager] 배포가 [!DNL InDesign Server]과(와) 통합되어야 합니다. 자세한 내용은 [Experience Manager Assets과 InDesign Server 통합](/help/assets/indesign.md)을 참조하세요.

1. 편집 가능한 필드의 텍스트를 수정하려면 편집 가능한 필드 목록에서 텍스트 필드를 클릭하고 필드의 텍스트를 편집합니다.

   ![chlimage_1-111](assets/chlimage_1-316.png)

   제공된 옵션을 사용하여 글꼴 스타일, 색상 및 크기와 같은 텍스트 속성을 편집할 수 있습니다.

1. 텍스트 변경 내용을 미리 볼 수 있도록 **[!UICONTROL 미리 보기]**&#x200B;를 선택하십시오.

1. 이미지를 바꾸려면 **[!UICONTROL 자산 파인더]** ![chlimage_1-113](assets/chlimage_1-318.png)을(를) 선택하십시오.

1. 편집 가능한 필드 목록에서 이미지 필드를 선택한 다음 에셋 선택기에서 원하는 이미지를 편집 가능한 필드로 드래그합니다.

   ![chlimage_1-114](assets/chlimage_1-319.png)

   키워드, 태그 및 게시 상태를 기반으로 이미지를 검색할 수도 있습니다. [!DNL Experience Manager Assets] 저장소를 탐색하고 원하는 이미지의 위치로 이동할 수 있습니다.

   ![chlimage_1-115](assets/chlimage_1-320.png)

1. 이미지를 미리 볼 수 있도록 **[!UICONTROL 미리 보기]**&#x200B;를 선택하십시오.
1. 여러 페이지로 구성된 자료의 특정 페이지를 편집하려면 맨 아래에 있는 페이지 탐색기를 사용하십시오.

1. 모든 변경 내용을 미리 볼 수 있도록 도구 모음에서 **[!UICONTROL 미리 보기]**&#x200B;를 선택합니다. 보조 부분의 편집 변경 내용을 저장하려면 **[!UICONTROL 완료]**&#x200B;를 선택하십시오.

   >[!NOTE]
   >
   >자료 내의 편집 가능한 이미지 필드에 누락된 아이콘이 없는 경우에만 미리 보기 및 완료 옵션이 활성화됩니다. 담보에 누락된 아이콘이 있는 이유는 [!DNL Experience Manager]이(가) [!DNL InDesign] 템플릿의 이미지를 확인할 수 없기 때문입니다. 일반적으로 [!DNL Experience Manager]은(는) 다음과 같은 경우 이미지를 확인할 수 없습니다.
   >
   >* 기본 [!DNL InDesign] 템플릿에 이미지가 포함되지 않았습니다.
   >* 이미지는 로컬 파일 시스템에서 연결됩니다.
   >
   >[!DNL Experience Manager]이(가) 이미지를 확인하도록 하려면 다음을 수행하십시오.
   >
   >* [!DNL InDesign]개의 템플릿을 만드는 동안 이미지를 포함합니다([링크 및 포함된 그래픽 정보](https://helpx.adobe.com/kr/indesign/using/graphics-links.html) 참조).
   >* 로컬 파일 시스템에 [!DNL Experience Manager]을(를) 탑재한 다음 누락된 아이콘을 [!DNL Experience Manager]의 기존 자산에 매핑합니다.
   >
   >[!DNL InDesign] 문서 작업에 대한 자세한 내용은 [Experience Manager에서 InDesign 문서 작업 모범 사례](https://helpx.adobe.com/experience-manager/kb/best-practices-idd-docs-aem.html)를 참조하세요.

1. 브로셔에 대한 PDF 렌디션을 생성하려면 대화 상자에서 Acrobat 옵션을 선택한 다음 **[!UICONTROL 계속]**&#x200B;을 클릭합니다.
1. 자료 조각은 시작한 폴더에 생성됩니다. 렌디션을 보려면 자료를 열고 GlobalNav 목록에서 **[!UICONTROL 렌디션]**&#x200B;을 선택하십시오.

   ![chlimage_1-118](assets/chlimage_1-323.png)

1. PDF 파일을 다운로드할 수 있도록 렌디션 목록에서 PDF 렌디션을 선택합니다. PDF 파일을 열어 자료를 검토하십시오.

   ![chlimage_1-119](assets/chlimage_1-324.png)

## 자료 병합 {#merge-collateral}

1. [!DNL Experience Manager] 인터페이스의 탐색 페이지에서 [!UICONTROL Assets]을(를) 선택합니다.

1. 옵션에서 **[!UICONTROL 템플릿]**&#x200B;을 선택합니다.

1. **[!UICONTROL 만들기]**&#x200B;를 선택한 다음 메뉴에서 **[!UICONTROL 병합]**&#x200B;을 선택합니다.

   ![chlimage_1-120](assets/chlimage_1-325.png)

1. [!UICONTROL 템플릿 병합] 페이지에서 **[!UICONTROL 병합]** ![자산 추가](assets/do-not-localize/assets_add_icon.png)를 선택합니다.

1. 병합할 자료 조각의 위치로 이동하고 병합할 자료의 썸네일을 선택하여 선택합니다.

   ![chlimage_1-122](assets/chlimage_1-327.png)

   Omnisearch 상자에서 템플릿을 검색할 수도 있습니다.

   [!DNL Experience Manager Assets] 리포지토리 또는 컬렉션을 탐색하고 원하는 템플릿의 위치로 이동한 다음 병합할 템플릿을 선택할 수 있습니다.

   다양한 필터를 적용하여 원하는 템플릿을 검색할 수 있습니다. 예를 들어 파일 유형 또는 태그를 기반으로 템플릿을 검색할 수 있습니다.

1. 도구 모음에서 **[!UICONTROL 다음]**&#x200B;을 선택합니다.
1. **[!UICONTROL 미리 보기 및 순서 바꾸기]** 화면에서 필요한 경우 템플릿을 다시 정렬하고 병합할 템플릿 선택을 미리 봅니다. 도구 모음에서 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

   ![chlimage_1-126](assets/chlimage_1-331.png)

1. [!UICONTROL 템플릿 구성] 화면에서 담보의 이름을 지정하십시오. 필요한 경우 적합하다고 판단되는 태그를 지정합니다. 출력을 PDF 형식으로 내보내려면 **[!UICONTROL Acrobat(.PDF)]**&#x200B;을(를) 선택합니다. 기본적으로 자료는 JPG 및 [!DNL InDesign] 형식으로 내보내집니다. 다중 페이지 자료의 표시 축소판을 변경하려면 **[!UICONTROL 축소판 변경]**&#x200B;을 클릭하십시오.

   ![chlimage_1-127](assets/chlimage_1-332.png)

1. **[!UICONTROL 저장]**&#x200B;을 선택한 다음 **[!UICONTROL 확인]**&#x200B;을 선택하여 대화 상자를 닫습니다. 다중 페이지 자료가 시작한 폴더에 만들어집니다.

   >[!NOTE]
   >
   >병합된 자료 조각은 나중에 편집하거나 다른 자료 조각을 만드는 데 사용할 수 없습니다.

## 우수 사례 및 제한 사항 {#best-practices-limitations-tips}

* [!DNL Experience Manager]의 [!DNL InDesign] 편집기는 태그 수준에서 작동하며 단일 태그의 모든 텍스트는 단일 엔터티로 간주됩니다. 편집할 때 텍스트 서식과 스타일을 유지하려면 각 단락(또는 스타일이 다른 텍스트)에 개별적으로 태그를 지정합니다.
