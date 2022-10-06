---
title: 참조 및 여러 페이지로 복합 자산 관리
description: 내에서 디지털 자산에 대한 참조를 만드는 방법을 알아봅니다 [!DNL Adobe InDesign], [!DNL Adobe Illustrator], 및 [!DNL Adobe Photoshop]. 페이지 뷰어 기능을 사용하여 PDF, INDD, PPT, PPTX 및 AI 파일과 같은 다중 페이지 파일의 개별 하위 자산 페이지를 볼 수 있습니다.
contentOwner: AG
role: User, Admin
feature: Asset Management
exl-id: 1ea9d8fe-602c-452b-9a24-4125b705aedf
source-git-commit: 79d8b5896f5f8eb7a22dccea81acf0656d435f2b
workflow-type: tm+mt
source-wordcount: '1424'
ht-degree: 0%

---

# 조합 및 다중 페이지 자산 관리 {#managing-compound-assets}

[!DNL Adobe Experience Manager Assets] 업로드된 파일에 리포지토리에 이미 있는 자산에 대한 참조가 포함되어 있는지 식별할 수 있습니다. 이 기능은 지원되는 파일 형식에만 사용할 수 있습니다. 업로드된 자산에 [!DNL Experience Manager] 자산인 경우 업로드된 자산과 참조된 자산 사이에 양방향 링크가 만들어집니다.

중복성을 제거하고 의 자산을 참조합니다. [!DNL Adobe Creative Cloud] 응용 프로그램은 공동 작업을 향상시키고 사용자의 효율성 및 생산성을 높입니다.

[!DNL Experience Manager Assets] 는 양방향 참조를 지원합니다. 업로드된 파일의 자산 세부 정보 페이지에서 참조된 자산을 찾을 수 있습니다. 또한 참조된 자산의 자산 세부 사항 페이지에서 참조하는 파일을 볼 수 있습니다.

참조는 참조된 자산의 경로, 문서 ID 및 인스턴스 ID를 기반으로 해결됩니다.

## [!DNL Adobe Illustrator]: 디지털 자산을 참조로 추가 {#refai}

내에서 기존 디지털 자산을 참조할 수 있습니다 [!DNL Adobe Illustrator] 파일.

1. 사용 [[!DNL Experience Manager] 데스크탑 앱](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)로컬 파일 시스템에서 디지털 자산을 가져옵니다. 참조할 자산의 파일 시스템 위치로 이동합니다.
1. 로컬 폴더의 자산을 [!DNL Illustrator] 파일.

1. 를 저장합니다 [!DNL Illustrator] 마운트된 드라이브에 파일을 추가하거나 [업로드](/help/assets/manage-assets.md#uploading-assets) 변환 후 [!DNL Experience Manager] 저장소.

1. 워크플로우가 완료되면 자산의 자산 세부 사항 페이지로 이동합니다. 기존 디지털 자산에 대한 참조가 아래에 나열됩니다 **[!UICONTROL 종속성]** 에서 **[!UICONTROL 참조]** 열.

   ![chlimage_1-84](assets/chlimage_1-258.png)

1. 아래에 표시되는 참조된 자산 **[!UICONTROL 종속성]** 현재 파일 이외의 다른 파일에서도 참조할 수 있습니다. 자산에 대한 참조 파일 목록을 보려면 아래의 자산을 클릭합니다 **[!UICONTROL 종속성]**.

   ![chlimage_1-85](assets/chlimage_1-259.png)

1. 클릭 **[!UICONTROL 속성 보기]** 를 클릭합니다. 에서 [!UICONTROL 속성] 페이지에서 현재 자산을 참조하는 파일 목록이 **[!UICONTROL 참조]** 열 **[!UICONTROL 기본]** 탭.

   ![자산 세부 정보의 참조 열에서 Experience Manager Assets 참조 보기](assets/asset-references.png)

   *그림: 자산 세부 사항의 자산 참조.*

## [!DNL Adobe InDesign]: 디지털 자산을 참조로 추가 {#add-aem-assets-as-references-in-adobe-indesign}

내에서 디지털 자산을 참조하려면 [!DNL InDesign] 파일에서 자산을 [!DNL InDesign] 파일 또는 내보내기 [!DNL InDesign] 파일로 저장합니다.

참조된 자산이 이미 있습니다. [!DNL Experience Manager Assets]. 다음 방법으로 하위 자산을 추출할 수 있습니다 [InDesign Server 구성](indesign.md). 에 포함된 자산 [!DNL InDesign] 파일은 하위 자산으로 추출됩니다.

>[!NOTE]
>
>만약 [!DNL InDesign Server] 는 프록시되고, [!DNL InDesign] 파일의 미리 보기는 XMP 메타데이터 내에 포함됩니다. 이 경우 축소판 추출이 명시적으로 필요하지 않습니다. 그러나 [!DNL InDesign Server] 프록시되지 않은 경우 축소판을 명시적으로 추출해야 합니다. [!DNL InDesign] 파일.

INDD 파일이 업로드되면 `xmpMM:InstanceID` 및 `xmpMM:DocumentID` 저장소의 속성입니다.

### 자산을 끌어 참조 만들기 {#create-references-by-dragging-aem-assets}

이 절차는 다음과 유사합니다 [Adobe Illustrator에서 참조로 디지털 자산 추가](#refai).

### ZIP 파일을 내보내어 자산에 대한 참조를 만듭니다 {#create-references-to-aem-assets-by-exporting-a-zip-file}

1. 다음 단계를 수행하십시오. [워크플로우 모델 만들기](/help/sites-developing/workflows-models.md) 새 워크플로우를 만들려면 다음을 수행하십시오.
1. 를 사용하십시오 [패키지 기능](https://helpx.adobe.com/indesign/how-to/indesign-package-files-for-handoff.html) 의 [!DNL Adobe InDesign] 문서를 내보내려면 [!DNL Adobe InDesign] 문서 및 연결된 자산을 패키지로 내보낼 수 있습니다. 이 경우 내보낸 폴더에는 `Links` 하위 자산을 포함하는 폴더 [!DNL InDesign] 파일. 다음 `Links` 폴더가 INDD 파일과 동일한 폴더에 있습니다.
1. ZIP 파일을 만든 다음 [!DNL Experience Manager] 저장소.
1. 시작 `Unarchiver` 워크플로우.
1. 워크플로우가 완료되면 링크 폴더의 참조가 자동으로 하위 자산으로 참조됩니다. 참조된 자산 목록을 보려면 페이지의 자산 세부 사항 페이지로 이동합니다 [!DNL InDesign] 자산 및 닫기 [레일](/help/sites-authoring/basic-handling.md#rail-selector).

## [!DNL Adobe Photoshop]: 디지털 자산을 참조로 추가 {#refps}

1. 사용 [!DNL Experience Manager] 데스크탑 앱 액세스 [!DNL Experience Manager Assets]. 로컬 파일 시스템에 자산을 다운로드하여 표시합니다. 을(를) 사용하여 [!UICONTROL 연결 배치] 기능 [!DNL Adobe Photoshop]. 자세한 내용은 [데스크탑 앱에서 자산 배치](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#place-assets-in-native-documents).

1. 저장 위치 [!DNL Photoshop] 마운트된 드라이브 또는 [업로드](/help/assets/manage-assets.md#uploading-assets) 변환 후 [!DNL Experience Manager] 저장소.
1. 워크플로우가 완료되면 기존 [!DNL Experience Manager] 자산이 자산 세부 사항 페이지에 나열됩니다.

   참조된 자산을 보려면 [레일](/help/sites-authoring/basic-handling.md#rail-selector) 를 입력합니다.

1. 참조된 자산에는 참조된 자산 목록도 포함되어 있습니다. 참조된 자산 목록을 보려면 자산 세부 사항 페이지로 이동하여 를 닫습니다 [레일](/help/sites-authoring/basic-handling.md#rail-selector).

>[!NOTE]
>
>조합 자산 내의 자산은 문서 ID 및 인스턴스 ID를 기반으로 참조할 수도 있습니다. 이 기능은 [!DNL Adobe Illustrator] 및 [!DNL Adobe Photoshop] 버전 전용. 다른 경우와 마찬가지로, 참조는 이전 버전의 와 같이 기본 조합 자산에서 연결된 자산의 상대 경로를 기반으로 수행됩니다 [!DNL Experience Manager].

## 하위 자산 만들기 {#generate-subassets}

다중 페이지 형식을 사용하는 지원되는 자산의 경우 - PDF 파일, AI 파일, [!DNL Microsoft PowerPoint] 및 [!DNL Apple Keynote] 파일 및 [!DNL Adobe InDesign] 파일 — [!DNL Experience Manager] 은 원래 자산의 각 개별 페이지에 해당하는 하위 자산을 생성할 수 있습니다. 이러한 하위 자산은 *상위* 자산 및 여러 페이지 보기를 지원합니다. 다른 모든 목적으로 하위 자산은 의 일반 자산처럼 처리됩니다 [!DNL Experience Manager].

하위 자산 생성은 기본적으로 비활성화됩니다. 하위 자산 생성을 활성화하려면 다음 단계를 수행하십시오.

1. 에 로그인합니다. [!DNL Experience Manager] 관리자로. 액세스 **[!UICONTROL 도구]** > **[!UICONTROL 워크플로우]** > **[!UICONTROL 모델]**.
1. 선택 **[!UICONTROL DAM 자산 업데이트]** 워크플로우 및 **[!UICONTROL 편집]**.
1. 클릭 **[!UICONTROL 사이드 패널 전환]** 그리고 **[!UICONTROL 하위 자산 만들기]** 단계. 워크플로우를 추가합니다. **[!UICONTROL 동기화]**&#x200B;를 클릭합니다.

하위 자산을 생성하려면 다음 중 하나를 수행합니다.

* 새 자산: 다음 [!UICONTROL DAM 자산 업데이트] 워크플로우는에 업로드된 모든 새 자산에 대해 실행됩니다 [!DNL Experience Manager]. 새 다중 페이지 자산에 대해 하위 자산이 자동으로 생성됩니다.
* 기존 다중 페이지 자산: 수동으로 [!UICONTROL DAM 자산 업데이트] 다음 단계 중 하나를 수행하는 워크플로우입니다.

   * 자산을 선택하고 을(를) 클릭합니다 [!UICONTROL 타임라인] 왼쪽 패널을 열려면 다음을 수행하십시오. 또는 키보드 단축키를 사용합니다 `alt + 3`. 클릭 [!UICONTROL 워크플로우 시작], 선택 [!UICONTROL DAM 자산 업데이트]를 클릭합니다. [!UICONTROL 시작]를 클릭하고 [!UICONTROL 계속].
   * 자산을 선택하고 을(를) 클릭합니다 [!UICONTROL 만들기] > [!UICONTROL 워크플로우] 를 클릭합니다. 팝업 대화 상자에서 다음을 선택합니다 [!UICONTROL DAM 자산 업데이트] 워크플로우, [!UICONTROL 시작]를 클릭하고 [!UICONTROL 계속].

Microsoft Word 문서 특히 의 경우 **[!UICONTROL DAM Parse Word 문서]** 워크플로우. 이 변수는 `cq:Page` Microsoft Word 문서의 내용에 포함된 구성 요소입니다. 문서에서 추출한 이미지는 `cq:Page` 구성 요소. 이러한 이미지는 하위 자산 생성이 비활성화된 경우에도 추출됩니다.

>[!NOTE]
>
>에서 [!UICONTROL 하위 자산 생성 프로세스 - 단계 속성] in [!UICONTROL 프로세스 인수]를 지정하는 하위 자산의 수를 지정할 수 있습니다 [!DNL Experience Manager] 생성합니다. 기본값은 5입니다. 모든 하위 자산을 생성하려면 필드를 비워 둡니다. 필드에 음수가 있으면 하위 자산이 생성되지 않습니다.

## 하위 자산 보기 {#viewing-subassets}

하위 자산은 하위 자산이 생성되고 선택한 다중 페이지 자산에 사용할 수 있는 경우에만 표시됩니다. 생성된 하위 자산을 보려면 다중 페이지 자산을 엽니다. 페이지의 왼쪽 위 영역에서 ![왼쪽 레일을 여는 옵션](assets/do-not-localize/aem_leftrail_contentonly.png) 을(를) 클릭합니다. **[!UICONTROL 하위 자산]** 참조하십시오. 선택 시 **[!UICONTROL 하위 자산]** 참조하십시오. 또는 키보드 단축키를 사용합니다 `alt + 5`.

![다중 페이지 자산에 대한 하위 자산 보기](assets/view_subassets_simulation.gif)

## 다중 페이지 파일의 페이지 보기 {#view-pages-of-a-multi-page-file}

다음 의 페이지 뷰어 기능을 사용하여 PDF, INDD, PPT, PPTX 및 AI 파일과 같은 다중 페이지 파일을 볼 수 있습니다 [!DNL Experience Manager Assets]. 다중 페이지 자산을 열고 클릭 **[!UICONTROL 페이지 보기]** 페이지의 왼쪽 위 모서리에서 을(를) 클릭합니다. 열리는 페이지 뷰어 에는 자산의 페이지와 각 페이지를 탐색하고 확대/축소하는 컨트롤이 표시됩니다.

![다중 페이지 자산의 페이지를 보고 확인합니다](assets/view_multipage_asset_fmr.gif)

대상 [!DNL InDesign]를 사용하여 페이지를 추출할 수 있습니다. [!DNL InDesign Server]. 페이지의 미리 보기가 [!DNL InDesign] 파일을 만든 다음 [!DNL InDesign Server] 은 페이지 추출에 필요하지 않습니다.

다음 옵션은 도구 모음, 왼쪽 레일 및 페이지 뷰어 컨트롤에서 사용할 수 있습니다.

* **[!UICONTROL 데스크톱 작업]** 를 사용하여 특정 하위 자산을 열거나 표시하려면 [!DNL Experience Manager] 데스크탑 앱. 방법 보기 [데스크톱 작업 구성](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#desktopactions-v2) 사용 중인 [!DNL Experience Manager] 데스크탑 앱.

* **[!UICONTROL 속성]** 옵션이 열립니다 [!UICONTROL 속성] 특정 하위 자산의 페이지입니다.

* **[!UICONTROL 주석 달기]** 옵션을 사용하면 특정 하위 자산에 주석을 달 수 있습니다. 상위 자산을 열어 볼 때 별도의 하위 자산에서 사용하는 주석이 수집되어 함께 표시됩니다.

* **[!UICONTROL 페이지 개요]** 옵션을 선택하면 모든 하위 자산이 동시에 표시됩니다.

* **[!UICONTROL 타임라인]** 클릭 후 왼쪽 레일에서 옵션 ![왼쪽 레일을 여는 옵션](assets/do-not-localize/aem_leftrail_contentonly.png) 파일에 대한 활동 스트림을 표시합니다.

## 우수 사례 및 제한 사항 {#best-practice-limitation-tips}

* 하위 자산 생성은 모든 항목에 매우 많은 리소스를 사용할 수 있습니다 [!DNL Experience Manager] 배포. 복잡한 자산을 업로드할 때 하위 자산을 생성하는 경우 DAM 자산 업데이트 워크플로우에서 단계를 추가합니다. 주문형 하위 자산을 생성하는 경우 별도의 워크플로우를 만들어 하위 자산을 생성합니다. 전용 워크플로우를 사용하면 DAM 자산 업데이트 워크플로우의 다른 단계를 건너뛰고 계산 리소스를 저장할 수 있습니다.

>[!MORELIKETHIS]
>
>* [Adobe Experience Manager 데스크탑 앱 사용](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)
>* [Adobe Experience Manager에서 데스크톱 작업 구성](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#desktopactions-v2)
>* [Adobe Photoshop에서 연결된 스마트 개체 만들기](https://helpx.adobe.com/photoshop/using/create-smart-objects.html#create-linked-smart-objects)
>* [Adobe InDesign에서 그래픽 배치](https://helpx.adobe.com/indesign/using/placing-graphics.html)

