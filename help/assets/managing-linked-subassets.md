---
title: 참조 및 여러 페이지를 사용하여 복합 에셋 관리
description: 내에서 디지털 에셋에 대한 참조를 만드는 방법을 알아봅니다 [!DNL Adobe InDesign], [!DNL Adobe Illustrator], 및 [!DNL Adobe Photoshop]. 페이지 뷰어 기능을 사용하여 PDF, INDD, PPT, PPTX 및 AI 파일과 같은 다중 페이지 파일의 개별 하위 자산 페이지를 볼 수 있습니다.
contentOwner: AG
role: User, Admin
feature: Asset Management
exl-id: 1ea9d8fe-602c-452b-9a24-4125b705aedf
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '1423'
ht-degree: 0%

---

# 조합 및 다중 페이지 자산 관리 {#managing-compound-assets}

[!DNL Adobe Experience Manager Assets] 은 업로드된 파일에 저장소에 이미 존재하는 에셋에 대한 참조가 포함되어 있는지 식별할 수 있습니다. 이 기능은 지원되는 파일 형식에만 사용할 수 있습니다. 업로드된 에셋에 대한 참조가 포함된 경우 [!DNL Experience Manager] 에셋은 업로드된 에셋과 참조된 에셋 간에 양방향 링크가 만들어집니다.

중복을 제거하는 것 외에도 의 에셋 참조 [!DNL Adobe Creative Cloud] 애플리케이션은 협업을 향상시키고 사용자의 효율성 및 생산성을 향상시킵니다.

[!DNL Experience Manager Assets] 는 양방향 참조를 지원합니다. 업로드된 파일의 에셋 세부 정보 페이지에서 참조된 에셋을 찾을 수 있습니다. 또한 참조된 에셋의 에셋 세부 사항 페이지에서 참조 파일을 볼 수 있습니다.

참조는 참조된 에셋의 경로, 문서 ID 및 인스턴스 ID를 기반으로 해결됩니다.

## [!DNL Adobe Illustrator]: 디지털 에셋을 참조로 추가 {#refai}

내에서 기존 디지털 에셋을 참조할 수 있습니다. [!DNL Adobe Illustrator] 파일.

1. 사용 [[!DNL Experience Manager] 데스크탑 앱](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)로컬 파일 시스템에서 디지털 에셋을 가져옵니다. 참조할 자산의 파일 시스템 위치로 이동합니다.
1. 로컬 폴더에서 로 자산 드래그 [!DNL Illustrator] 파일.

1. 저장 [!DNL Illustrator] 파일을 마운트된 드라이브에 저장하거나 [업로드](/help/assets/manage-assets.md#uploading-assets) (으)로 [!DNL Experience Manager] 리포지토리.

1. 워크플로우가 완료되면 에셋에 대한 에셋 세부 사항 페이지로 이동합니다. 기존 디지털 자산에 대한 참조는 아래에 나열되어 있습니다. **[!UICONTROL 종속성]** 다음에서 **[!UICONTROL 참조]** 열.

   ![chlimage_1-84](assets/chlimage_1-258.png)

1. 아래에 표시되는 참조된 에셋 **[!UICONTROL 종속성]** 현재 파일이 아닌 다른 파일에서도 참조할 수 있습니다. 에셋에 대한 참조 파일 목록을 보려면 아래에서 에셋을 클릭합니다 **[!UICONTROL 종속성]**.

   ![chlimage_1-85](assets/chlimage_1-259.png)

1. 클릭 **[!UICONTROL 속성 보기]** 을 클릭합니다. 다음에서 [!UICONTROL 속성] 페이지의 현재 에셋을 참조하는 파일 목록은 **[!UICONTROL 참조]** 열의 **[!UICONTROL 기본]** 탭.

   ![에셋 세부 정보의 참조 열에서 Experience Manager Assets 참조 보기](assets/asset-references.png)

   *그림: 에셋 세부 정보의 에셋 참조*

## [!DNL Adobe InDesign]: 디지털 에셋을 참조로 추가 {#add-aem-assets-as-references-in-adobe-indesign}

내에서 디지털 에셋을 참조하려면 [!DNL InDesign] 파일, 자산을 다음으로 드래그 [!DNL InDesign] 파일 또는 내보내기 [!DNL InDesign] 파일을 ZIP 아카이브로 만듭니다.

참조된 자산이에 이미 있음 [!DNL Experience Manager Assets]. 다음을 수행하여 하위 자산을 추출할 수 있습니다. [InDesign Server 구성](indesign.md). 에 임베드된 에셋 [!DNL InDesign] 파일이 하위 자산으로 추출됩니다.

>[!NOTE]
>
>다음과 같은 경우 [!DNL InDesign Server] 프록시화됨, [!DNL InDesign] 파일은 XMP 메타데이터 내에 미리보기가 임베드되어 있습니다. 이 경우 썸네일 추출이 명시적으로 필요하지 않습니다. 그러나 [!DNL InDesign Server] 은(는) 프록시가 아닙니다. 다음에 대한 썸네일을 명시적으로 추출해야 합니다. [!DNL InDesign] 파일.

INDD 파일이 업로드되면 다음 자산을 쿼리하여 참조를 가져옵니다. `xmpMM:InstanceID` 및 `xmpMM:DocumentID` 저장소의 속성입니다.

### 에셋을 끌어 참조 만들기 {#create-references-by-dragging-aem-assets}

이 절차는 다음과 유사합니다. [Adobe Illustrator에서 디지털 에셋을 참조로 추가](#refai).

### ZIP 파일을 내보내어 에셋에 대한 참조 만들기 {#create-references-to-aem-assets-by-exporting-a-zip-file}

1. 의 단계를 수행합니다. [워크플로우 모델 만들기](/help/sites-developing/workflows-models.md) 새 워크플로를 만듭니다.
1. 사용 [패키지 기능](https://helpx.adobe.com/indesign/how-to/indesign-package-files-for-handoff.html) / [!DNL Adobe InDesign] 문서를 내보냅니다. [!DNL Adobe InDesign] 는 문서 및 연결된 에셋을 패키지로 내보낼 수 있습니다. 이 경우 내보낸 폴더에는 `Links` 폴더에 하위 에셋이 포함된 폴더 [!DNL InDesign] 파일. 다음 `Links` 폴더는 INDD 파일과 동일한 폴더에 있습니다.
1. ZIP 파일을 만들어 [!DNL Experience Manager] 리포지토리.
1. 시작 `Unarchiver` 워크플로입니다.
1. 워크플로우가 완료되면 링크 폴더의 참조가 자동으로 하위 자산으로 참조됩니다. 참조된 에셋 목록을 보려면 의 에셋 세부 정보 페이지로 이동합니다. [!DNL InDesign] 에셋 및 닫기 [레일](/help/sites-authoring/basic-handling.md#rail-selector).

## [!DNL Adobe Photoshop]: 디지털 에셋을 참조로 추가 {#refps}

1. 사용 [!DNL Experience Manager] 액세스할 데스크탑 앱 [!DNL Experience Manager Assets]. 로컬 파일 시스템에서 에셋을 다운로드하고 표시합니다. 사용 [!UICONTROL 연결 배치] 의 기능 [!DNL Adobe Photoshop]. 다음을 참조하십시오 [데스크탑 앱에 자산 배치](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#place-assets-in-native-documents).

1. 저장 위치 [!DNL Photoshop] 파일을 마운트된 드라이브에 저장하거나 [업로드](/help/assets/manage-assets.md#uploading-assets) (으)로 [!DNL Experience Manager] 리포지토리.
1. 워크플로우가 완료된 후 기존 을 참조합니다. [!DNL Experience Manager] 에셋은 에셋 세부 사항 페이지에 나열됩니다.

   참조된 자산을 보려면 를 닫습니다. [레일](/help/sites-authoring/basic-handling.md#rail-selector) (자산 세부 사항 페이지에서)

1. 참조된 에셋에는 에셋이 참조되는 에셋 목록도 포함됩니다. 참조된 에셋 목록을 보려면 에셋 세부 사항 페이지로 이동하여 [레일](/help/sites-authoring/basic-handling.md#rail-selector).

>[!NOTE]
>
>복합 에셋 내의 에셋은 문서 ID 및 인스턴스 ID를 기반으로 참조할 수도 있습니다. 이 기능은 다음에서 사용할 수 있습니다. [!DNL Adobe Illustrator] 및 [!DNL Adobe Photoshop] 버전만 해당됩니다. 다른 항목의 경우, 의 이전 버전에서 수행한 대로 기본 조합 에셋에서 연결된 에셋의 상대 경로를 기반으로 참조가 수행됩니다. [!DNL Experience Manager].

## 하위 자산 만들기 {#generate-subassets}

PDF 파일, AI 파일 등 다중 페이지 형식의 지원되는 에셋의 경우 [!DNL Microsoft PowerPoint] 및 [!DNL Apple Keynote] 파일 및 [!DNL Adobe InDesign] 파일 — [!DNL Experience Manager] 은 원본 에셋의 각 개별 페이지에 해당하는 하위 에셋을 생성할 수 있습니다. 이러한 하위 자산은 *상위* 에셋 및 다중 페이지 보기를 용이하게 합니다. 다른 모든 용도로 하위 에셋은에서 일반 에셋처럼 처리됩니다. [!DNL Experience Manager].

하위 자산 생성은 기본적으로 비활성화되어 있습니다. 하위 자산 생성을 활성화하려면 다음 단계를 수행합니다.

1. 에 로그인 [!DNL Experience Manager] 관리자입니다. 액세스 **[!UICONTROL 도구]** > **[!UICONTROL 워크플로]** > **[!UICONTROL 모델]**.
1. 선택 **[!UICONTROL DAM 자산 업데이트]** 워크플로우 및 클릭 **[!UICONTROL 편집]**.
1. 클릭 **[!UICONTROL 사이드 패널 전환]** 및 를 찾습니다. **[!UICONTROL 하위 자산 만들기]** 단계. 워크플로우에 단계를 추가합니다. **[!UICONTROL 동기화]**&#x200B;를 클릭합니다.

하위 자산을 생성하려면 다음 중 하나를 수행합니다.

* 새 에셋: [!UICONTROL DAM 자산 업데이트] 워크플로는에 업로드된 새 에셋에 대해 실행됩니다. [!DNL Experience Manager]. 새 다중 페이지 자산에 대해 하위 자산이 자동으로 생성됩니다.
* 기존 다중 페이지 에셋: [!UICONTROL DAM 자산 업데이트] 다음 단계 중 하나를 수행하는 워크플로:

   * 에셋을 선택하고 [!UICONTROL 타임라인] 왼쪽 패널을 엽니다. 또는 키보드 단축키를 사용합니다 `alt + 3`. 클릭 [!UICONTROL 워크플로우 시작], 선택 [!UICONTROL DAM 자산 업데이트], 클릭 [!UICONTROL 시작], 및 클릭 [!UICONTROL 진행].
   * 에셋을 선택하고 [!UICONTROL 만들기] > [!UICONTROL 워크플로] 을 클릭합니다. 팝업 대화 상자에서 다음을 선택합니다. [!UICONTROL DAM 자산 업데이트] 워크플로우, 클릭 [!UICONTROL 시작], 및 클릭 [!UICONTROL 진행].

특히 Microsoft Word 문서의 경우 **[!UICONTROL DAM Word 문서 구문 분석]** 워크플로입니다. 다음을 생성합니다. `cq:Page` Microsoft Word 문서 컨텐츠의 구성 요소입니다. 문서에서 추출된 이미지는 `cq:Page` 구성 요소. 이러한 이미지는 하위 에셋 생성이 비활성화된 경우에도 추출됩니다.

>[!NOTE]
>
>다음에서 [!UICONTROL 하위 자산 만들기 프로세스 - 단계 속성] 위치: [!UICONTROL 프로세스 인수], 다음과 같은 하위 에셋의 수를 지정할 수 있습니다 [!DNL Experience Manager] 를 생성합니다. 기본값은 5입니다. 모든 하위 에셋을 생성하려면 필드를 비워 둡니다. 필드에 음수가 있으면 하위 에셋이 생성되지 않습니다.

## 하위 자산 보기 {#viewing-subassets}

하위 에셋은 하위 에셋이 생성되고 선택한 다중 페이지 에셋에 사용할 수 있는 경우에만 표시됩니다. 생성된 하위 자산을 보려면 다중 페이지 자산을 엽니다. 페이지의 왼쪽 상단 영역에서 을(를) 클릭합니다. ![왼쪽 레일 열기 옵션](assets/do-not-localize/aem_leftrail_contentonly.png) 및 클릭 **[!UICONTROL 하위 자산]** 목록에서 삭제할 수 있습니다. 다음을 선택할 때 **[!UICONTROL 하위 자산]** 목록에서 삭제할 수 있습니다. 또는 키보드 단축키를 사용합니다 `alt + 5`.

![다중 페이지 자산에 대한 하위 자산 보기](assets/view_subassets_simulation.gif)

## 다중 페이지 파일의 페이지 보기 {#view-pages-of-a-multi-page-file}

의 페이지 뷰어 기능을 사용하여 PDF, INDD, PPT, PPTX 및 AI 파일과 같은 다중 페이지 파일을 볼 수 있습니다. [!DNL Experience Manager Assets]. 다중 페이지 자산을 열고 을 클릭합니다. **[!UICONTROL 페이지 보기]** 페이지의 왼쪽 상단 모서리에서 열리는 페이지 뷰어에는 에셋의 페이지와 각 페이지를 탐색하고 확대/축소할 수 있는 컨트롤이 표시됩니다.

![다중 페이지 자산의 페이지 보기 및 보기](assets/view_multipage_asset_fmr.gif)

대상 [!DNL InDesign]를 사용하여 페이지를 추출할 수 있습니다 [!DNL InDesign Server]. 다음 기간 동안 페이지 미리보기가 저장된 경우 [!DNL InDesign] 파일 생성, [!DNL InDesign Server] 은 페이지 추출에 필요하지 않습니다.

다음 옵션은 도구 모음, 왼쪽 레일 및 페이지 뷰어 컨트롤에서 사용할 수 있습니다.

* **[!UICONTROL 데스크탑 작업]** 을 사용하여 특정 하위 에셋을 열거나 표시하려면 [!DNL Experience Manager] 데스크탑 앱입니다. 방법 보기 [데스크탑 작업 구성](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#desktopactions-v2) 을 사용하는 경우 [!DNL Experience Manager] 데스크탑 앱입니다.

* **[!UICONTROL 속성]** 옵션을 선택하면 [!UICONTROL 속성] 특정 하위 에셋의 페이지입니다.

* **[!UICONTROL 주석]** 옵션을 사용하면 특정 하위 에셋에 주석을 달 수 있습니다. 별도의 하위 에셋에서 사용하는 주석은 상위 에셋을 열어 볼 때 함께 수집되어 표시됩니다.

* **[!UICONTROL 페이지 개요]** 옵션은 모든 하위 자산을 동시에 표시합니다.

* **[!UICONTROL 타임라인]** 을(를) 클릭한 후 왼쪽 레일에서 옵션 ![왼쪽 레일 열기 옵션](assets/do-not-localize/aem_leftrail_contentonly.png) 파일에 대한 활동 스트림을 표시합니다.

## 모범 사례 및 제한 사항 {#best-practice-limitation-tips}

* 하위 에셋 생성은 모든 항목에서 리소스 집약적일 수 있습니다. [!DNL Experience Manager] 배포. 복잡한 에셋이 업로드될 때 하위 에셋을 생성하는 경우 DAM 에셋 업데이트 워크플로에서 단계를 추가합니다. 온디맨드로 하위 에셋을 생성하는 경우 별도의 워크플로우를 만들어 하위 에셋을 생성합니다. 전용 워크플로우를 사용하면 DAM 자산 업데이트 워크플로우의 다른 단계를 건너뛰고 계산 리소스를 저장할 수 있습니다.

>[!MORELIKETHIS]
>
>* [Adobe Experience Manager 데스크탑 앱 사용](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)
>* [Adobe Experience Manager에서 데스크탑 작업 구성](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#desktopactions-v2)
>* [Adobe Photoshop에서 연결된 스마트 오브젝트 만들기](https://helpx.adobe.com/photoshop/using/create-smart-objects.html#create-linked-smart-objects)
>* [Adobe InDesign에 그래픽 배치](https://helpx.adobe.com/indesign/using/placing-graphics.html)
