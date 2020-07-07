---
title: 참조 및 여러 페이지 에셋을 사용하여 복합 자산을 관리합니다 [!DNL Adobe Experience Manager].
description: 디지털 자산에 대한 참조를 만드는 방법을 [!DNL Adobe InDesign], [!DNL Adobe Illustrator], and [!DNL Adobe Photoshop]살펴보십시오. 페이지 뷰어 기능을 사용하여 PDF, INDD, PPT, PPTX 및 AI 파일과 같은 여러 페이지 파일의 개별 하위 자산 페이지를 볼 수 있습니다.
contentOwner: AG
translation-type: tm+mt
source-git-commit: b59f7471ab9f3c5e6eb3365122262b592c8e6244
workflow-type: tm+mt
source-wordcount: '1363'
ht-degree: 0%

---


# 복합 및 여러 페이지 에셋 관리 {#managing-compound-assets}

[!DNL Adobe Experience Manager Assets] 업로드된 파일에 이미 저장소에 있는 자산에 대한 참조가 포함되어 있는지 식별할 수 있습니다. 이 기능은 지원되는 파일 포맷에서만 사용할 수 있습니다. 업로드된 자산에 자산에 대한 참조가 포함되어 있으면, 업로드된 자산과 참조된 자산 사이에 양방향 링크가 만들어집니다. [!DNL Experience Manager]

중복성을 제거할 수 있을 뿐만 아니라 애플리케이션의 에셋을 참조하면 공동 작업을 향상시킬 수 있고 사용자의 효율성과 생산성을 높일 수 있습니다. [!DNL Adobe Creative Cloud]

[!DNL Experience Manager Assets] 는 양방향 참조를 지원합니다. 업로드된 파일의 자산 세부 정보 페이지에서 참조된 자산을 찾을 수 있습니다. 또한 참조된 자산의 자산 세부 정보 페이지에서 참조하는 파일을 볼 수 있습니다.

참조는 참조된 자산의 경로, 문서 ID 및 인스턴스 ID를 기준으로 결정됩니다.

## 디지털 자산을 참조로 추가 [!DNL Adobe Illustrator] {#refai}

파일 내에서 기존 디지털 자산을 참조할 수 [!DNL Adobe Illustrator] 있습니다.

1. Experience Manager 데스크탑 앱 [](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html)을 사용하여 로컬 파일 시스템에서 디지털 자산을 가져옵니다. 참조할 자산의 파일 시스템 위치로 이동합니다.
1. 로컬 폴더의 자산을 [!DNL Illustrator] 파일로 드래그합니다.

1. 마운트된 드라이브에 [!DNL Illustrator] 파일을 저장하거나 [저장소에](/help/assets/managing-assets-touch-ui.md#uploading-assets) 업로드할 [!DNL Experience Manager] 수있습니다.

1. 워크플로우가 완료되면 자산의 자산 세부 사항 페이지로 이동합니다. 기존 디지털 자산에 대한 참조는 참조 열 **[!UICONTROL 의 종속성]** 아래에 **[!UICONTROL 나열됩니다]** .

   ![chlimage_1-84](assets/chlimage_1-258.png)

1. 종속성 아래에 나타나는 참조된 자산 **[!UICONTROL 은]** 현재 자산 이외의 파일에서도 참조할 수 있습니다. 자산에 대한 참조 파일 목록을 보려면 종속성 아래의 자산을 **[!UICONTROL 클릭합니다]**.

   ![chlimage_1-85](assets/chlimage_1-259.png)

1. 도구 모음 **[!UICONTROL 에서 속성]** 보기를 클릭합니다. [ [!UICONTROL 속성] ] 페이지에서 **[!UICONTROL 현재 자산을 참조하는 파일 목록이 []** 기본 **]** 탭의 [참조] 열 아래에나타납니다.

   ![자산 세부 정보에서 참조 열의 Experience Manager 자산 참조 보기](assets/asset-references.png)

   *그림: 자산 세부 정보에 있는 자산 참조를 참조하십시오.*

## 디지털 자산을 참조로 추가 [!DNL Adobe InDesign] {#add-aem-assets-as-references-in-adobe-indesign}

파일 내에서 디지털 자산을 참조하려면 [!DNL InDesign] 자산을 [!DNL InDesign] 파일로 드래그하거나 [!DNL InDesign] 파일을 ZIP 보관으로 내보냅니다.

참조된 자산이 이미 있습니다 [!DNL Experience Manager Assets]. InDesign Server를 [구성하여 하위 자산을 추출할 수 있습니다](indesign.md). 파일에 포함된 에셋이 하위 [!DNL InDesign] 자산으로 추출됩니다.

>[!NOTE]
>
>프록시가 [!DNL InDesign Server] 인 경우 파일의 미리 [!DNL InDesign] 보기가 XMP 메타데이터 내에 임베드됩니다. 이 경우 축소판 추출이 명시적으로 필요하지 않습니다. 그러나 프록시가 [!DNL InDesign Server] 되지 않은 경우 [!DNL InDesign] 파일에 대해 축소판을 명시적으로 추출해야 합니다.

### 자산을 드래그하여 참조 만들기 {#create-references-by-dragging-aem-assets}

이 절차는 Adobe Illustrator에서 디지털 자산을 참조로 [추가하는 것과 유사합니다](#refai).

### ZIP 파일을 내보내 자산에 대한 참조 만들기 {#create-references-to-aem-assets-by-exporting-a-zip-file}

1. 워크플로우 모델 [만들기에서](/help/sites-developing/workflows-models.md) 단계를 수행하여 새 워크플로우를 만듭니다.
1. 의 패키지 기능 [!DNL Adobe InDesign] 을 사용하여 문서를 내보냅니다. [!DNL Adobe InDesign] 문서 및 연결된 에셋을 패키지로 내보낼 수 있습니다. 이 경우 내보낸 폴더에는 [!DNL InDesign] 파일의 하위 자산이 들어 있는 링크 폴더가 포함됩니다.
1. ZIP 파일을 만들어 [!DNL Experience Manager] 저장소에 업로드합니다.
1. 워크플로우를 `Unarchiver` 시작합니다.
1. 워크플로우가 완료되면 링크 폴더의 참조는 하위 자산으로 자동 참조됩니다. 참조된 자산 목록을 보려면 자산의 자산 세부 정보 페이지로 이동하고 레일을 [!DNL InDesign] 닫습니다 [](/help/sites-authoring/basic-handling.md#rail-selector).

## 디지털 자산을 참조로 추가 [!DNL Adobe Photoshop] {#refps}

1. 데스크탑 [!DNL Experience Manager] 앱을 사용하여 액세스할 수 [!DNL Experience Manager Assets]있습니다. 로컬 파일 시스템에 에셋을 다운로드하고 표시합니다. 연결 [!UICONTROL 가져오기 기능을] 사용합니다 [!DNL Adobe Photoshop]. 데스크탑 앱에 [에셋 가져오기를 참조하십시오](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#place-assets-in-native-documents).

   ![chlimage_1-87](assets/chlimage_1-261.png)

1. 파일 [!DNL Photoshop] 을 마운트된 드라이브에 저장하거나 [저장소에](/help/assets/managing-assets-touch-ui.md#uploading-assets) 업로드할 [!DNL Experience Manager] 수있습니다.
1. 워크플로우가 완료되면 기존 [!DNL Experience Manager] 자산에 대한 참조가 자산 세부 사항 페이지에 나열됩니다.

   참조된 자산을 보려면 자산 세부 사항 페이지에서 [레일을](/help/sites-authoring/basic-handling.md#rail-selector) 닫습니다.

1. 참조된 자산에는 참조되는 자산의 목록도 들어 있습니다. 참조된 자산 목록을 보려면 자산 세부 사항 페이지로 이동하고 레일을 [닫습니다](/help/sites-authoring/basic-handling.md#rail-selector).

>[!NOTE]
>
>복합 자산 내의 자산은 해당 문서 ID 및 인스턴스 ID를 기준으로 참조할 수도 있습니다. 이 기능은 [!DNL Adobe Illustrator] 및 [!DNL Adobe Photoshop] 버전에서만 사용할 수 있습니다. 다른 경우, 참조는 이전 버전의 경우와 마찬가지로 기본 복합 자산에서 연결된 자산의 상대 경로를 기준으로 수행됩니다 [!DNL Experience Manager].

## 하위 자산 만들기 {#generate-subassets}

PDF 파일, AI 파일, 파일, 파일 등 여러 페이지 형식의 지원되는 에셋의 경우 [!DNL Microsoft PowerPoint] [!DNL Apple Keynote] [!DNL Adobe InDesign] [!DNL Experience Manager] 원본 에셋의 각 개별 페이지에 해당하는 하위 에셋을 생성할 수 있습니다. 이러한 하위 자산은 *상위* 자산에 연결되고 여러 페이지 보기가 더 쉬워집니다. 다른 모든 목적으로 하위 자산은 의 일반 자산처럼 취급됩니다 [!DNL Experience Manager].

하위 자산 생성은 기본적으로 비활성화됩니다. 하위 자산 생성을 활성화하려면 다음 단계를 수행합니다.

1. 관리자로 [!DNL Experience Manager] 로그인합니다. 도구 **[!UICONTROL > 워크플로우]** **** > **[!UICONTROL 모델에 액세스합니다]**.
1. DAM **[!UICONTROL 자산 업데이트]** 워크플로우를 선택하고 편집을 **[!UICONTROL 클릭합니다]**.
1. 사이드 패널 **[!UICONTROL 전환을]** 클릭하고 **[!UICONTROL 하위 자산 만들기]** 단계를 찾습니다. 워크플로우에 단계를 추가합니다. 동기화를 **[!UICONTROL 클릭합니다]**.

하위 자산을 생성하려면 다음 중 하나를 수행합니다.

* 새 자산: DAM 자산 [!UICONTROL 업데이트] 워크플로우는 업로드된 모든 새 자산에 대해 실행됩니다 [!DNL Experience Manager]. 하위 자산은 새 다중 페이지 자산에 대해 자동으로 생성됩니다.
* 기존 다중 페이지 자산: 다음 단계 중 하나를 [!UICONTROL 따라 DAM 자산] 업데이트 워크플로우를 수동으로 실행합니다.

   * 자산을 선택하고 [!UICONTROL 타임라인] 을 클릭하여 왼쪽 패널을 엽니다. 또는 키보드 단축키를 사용합니다 `alt + 3`. 워크플로우 [!UICONTROL 시작]을 클릭하고 [!UICONTROL DAM 자산]업데이트 [!UICONTROL 를 선택한 다음]시작을 [!UICONTROL 클릭하고]Continue를 클릭합니다.
   * 자산을 선택하고 도구 모음에서 [!UICONTROL 만들기] > [!UICONTROL 작업] 흐름을클릭합니다. 팝업 대화 상자에서 [!UICONTROL DAM 자산] 업데이트 워크플로우를 선택하고 [!UICONTROL 시작을]클릭한 다음 [!UICONTROL 진행을 클릭합니다].

Microsoft Word 문서 전용으로, DAM Parse Word 문서 **[!UICONTROL 워크플로우를]** 실행합니다. Microsoft Word 문서의 내용에서 구성 `cq:Page` 요소를 생성합니다. 문서에서 추출한 이미지는 구성 요소에서 `cq:Page` 참조됩니다. 이러한 이미지는 하위 자산 생성을 사용하지 않는 경우에도 추출됩니다.

## View subassets {#viewing-subassets}

하위 자산은 하위 자산이 생성되어 선택된 여러 페이지 자산에 사용할 수 있는 경우에만 표시됩니다. 생성된 하위 자산을 보려면 다중 페이지 자산을 엽니다. 페이지의 왼쪽 위 영역에서 ![옵션을 클릭하여 왼쪽 레일을](assets/do-not-localize/aem_leftrail_contentonly.png) 열고 목록에서 **[!UICONTROL 하위 자산]** 을 클릭합니다. 목록에서 하위 **[!UICONTROL 자산을]** 선택하는 경우. 또는 키보드 단축키를 사용합니다 `alt + 5`.

![여러 페이지 자산에 대한 하위 자산 보기](assets/view_subassets_simulation.gif)

## 여러 페이지 파일의 페이지 보기 {#view-pages-of-a-multi-page-file}

의 페이지 뷰어 기능을 사용하여 PDF, INDD, PPT, PPTX 및 AI 파일과 같은 여러 페이지 파일을 볼 수 있습니다 [!DNL Experience Manager Assets]. 다중 페이지 자산을 열고 페이지의 왼쪽 **[!UICONTROL 위]** 모서리에서 페이지 보기를 클릭합니다. 열리는 페이지 뷰어에는 자산의 페이지와 각 페이지를 탐색하고 확대/축소하는 컨트롤이 표시됩니다.

![여러 페이지 자산의 페이지 보기 및 보기](assets/view_multipage_asset_fmr.gif)

예를 [!DNL InDesign][!DNL InDesign Server]들어, 파일을 만드는 동안 페이지 미리 보기가 저장된 경우 페이지 추출 [!DNL InDesign] [!DNL InDesign Server] 에 필요하지 않습니다.

도구 모음, 왼쪽 레일 및 페이지 뷰어 컨트롤에서 다음 옵션을 사용할 수 있습니다.

* **[!UICONTROL 데스크톱]** 작업을 클릭하여 [!DNL Experience Manager] 데스크탑 앱을 사용하여 특정 하위 자산을 열거나 표시합니다. 데스크톱 앱을 사용하는 경우 [데스크톱 작업](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#desktopactions-v2) 구성 방법을 [!DNL Experience Manager] 참조하십시오.

* **[!UICONTROL 속성]** 옵션을 선택하면 [!UICONTROL 특정 하위 자산의 속성] 페이지가 열립니다.

* **[!UICONTROL 주석]** 옵션을 사용하면 특정 하위 자산에 주석을 달 수 있습니다. 개별 하위 자산에서 사용하는 주석은 상위 자산을 보기 위해 열 때 함께 수집되고 표시됩니다.

* **[!UICONTROL 페이지 개요]** 옵션은 모든 하위 자산을 동시에 표시합니다.

* **[!UICONTROL 옵션(Option)을 클릭하여 왼쪽 레일을]** 연 후 왼쪽 레일의 타임라인 옵션에 파일 ![](assets/do-not-localize/aem_leftrail_contentonly.png) 의 활동 스트림이 표시됩니다.

## 모범 사례 및 제한 사항 {#best-practice-limitation-tips}

* 하위 자산 생성은 모든 Experience Manager 배포에서 매우 많은 리소스를 필요로 할 수 있습니다. 복잡한 자산이 업로드될 때 하위 자산을 생성하는 경우 DAM 자산 업데이트 워크플로우에서 단계를 추가합니다. 주문형 하위 자산을 생성하는 경우 별도의 워크플로우를 만들어 하위 자산을 생성합니다. 전용 워크플로우를 사용하면 DAM 자산 업데이트 워크플로우의 다른 단계를 건너뛰어 계산 리소스를 저장할 수 있습니다.

>[!MORELIKETHIS]
>
>* [Adobe Experience Manager 데스크탑 앱 사용](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html)
>* [Adobe Experience Manager에서 데스크톱 작업 구성](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#desktopactions-v2)
>* [Adobe Photoshop에서 연결된 고급 개체 만들기](https://helpx.adobe.com/photoshop/using/create-smart-objects.html#create-linked-smart-objects)
>* [Adobe InDesign에 그래픽 배치](https://helpx.adobe.com/indesign/using/placing-graphics.html)

