---
title: 참조 및 여러 페이지를 사용하여 복합 에셋 관리
description: ' [!DNL Adobe InDesign], [!DNL Adobe Illustrator] 및 [!DNL Adobe Photoshop] 내에서 디지털 자산에 대한 참조를 만드는 방법을 알아봅니다. 페이지 뷰어 기능을 사용하여 PDF, INDD, PPT, PPTX 및 AI 파일과 같은 다중 페이지 파일의 개별 하위 자산 페이지를 볼 수 있습니다.'
contentOwner: AG
role: User, Admin
feature: Asset Management
exl-id: 1ea9d8fe-602c-452b-9a24-4125b705aedf
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1382'
ht-degree: 0%

---

# 조합 및 다중 페이지 자산 관리 {#managing-compound-assets}

[!DNL Adobe Experience Manager Assets]은(는) 업로드된 파일에 저장소에 이미 있는 자산에 대한 참조가 포함되어 있는지 식별할 수 있습니다. 이 기능은 지원되는 파일 형식에만 사용할 수 있습니다. 업로드된 에셋에 [!DNL Experience Manager]개의 에셋에 대한 참조가 포함된 경우 업로드된 에셋과 참조된 에셋 사이에 양방향 링크가 만들어집니다.

중복을 제거하는 것 외에도 [!DNL Adobe Creative Cloud] 응용 프로그램의 자산을 참조하면 공동 작업이 향상되고 사용자의 효율성과 생산성이 향상됩니다.

[!DNL Experience Manager Assets]은(는) 양방향 참조를 지원합니다. 업로드된 파일의 에셋 세부 정보 페이지에서 참조된 에셋을 찾을 수 있습니다. 또한 참조된 에셋의 에셋 세부 사항 페이지에서 참조 파일을 볼 수 있습니다.

참조는 참조된 에셋의 경로, 문서 ID 및 인스턴스 ID를 기반으로 해결됩니다.

## [!DNL Adobe Illustrator]: 디지털 에셋을 참조로 추가 {#refai}

[!DNL Adobe Illustrator] 파일 내에서 기존 디지털 자산을 참조할 수 있습니다.

1. [[!DNL Experience Manager] 데스크톱 앱](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)을 사용하여 로컬 파일 시스템에서 디지털 자산을 가져옵니다. 참조할 자산의 파일 시스템 위치로 이동합니다.
1. 로컬 폴더에서 [!DNL Illustrator] 파일로 자산을 끌어 옵니다.

1. 탑재된 드라이브에 [!DNL Illustrator] 파일을 저장하거나 [!DNL Experience Manager] 저장소에 [업로드](/help/assets/manage-assets.md#uploading-assets)하십시오.

1. 워크플로우가 완료되면 에셋에 대한 에셋 세부 사항 페이지로 이동합니다. 기존 디지털 자산에 대한 참조는 **[!UICONTROL 참조]** 열의 **[!UICONTROL 종속성]** 아래에 나열됩니다.

   ![chlimage_1-84](assets/chlimage_1-258.png)

1. **[!UICONTROL 종속성]** 아래에 나타나는 참조된 자산은 현재 파일이 아닌 파일에서도 참조할 수 있습니다. 에셋에 대한 참조 파일 목록을 보려면 **[!UICONTROL 종속성]**&#x200B;에서 에셋을 클릭하십시오.

   ![chlimage_1-85](assets/chlimage_1-259.png)

1. 도구 모음에서 **[!UICONTROL 속성 보기]**&#x200B;를 클릭합니다. [!UICONTROL 속성] 페이지에서 현재 자산을 참조하는 파일 목록은 **[!UICONTROL 기본]** 탭의 **[!UICONTROL 참조]** 열 아래에 나타납니다.

   ![자산 세부 정보의 참조 열에서 Experience Manager Assets 참조 보기](assets/asset-references.png)

   *그림: 에셋 세부 정보의 에셋 참조.*

## [!DNL Adobe InDesign]: 디지털 에셋을 참조로 추가 {#add-aem-assets-as-references-in-adobe-indesign}

[!DNL InDesign] 파일 내에서 디지털 자산을 참조하려면 자산을 [!DNL InDesign] 파일로 끌어 놓거나 [!DNL InDesign] 파일을 ZIP 아카이브로 내보내십시오.

참조된 자산이 [!DNL Experience Manager Assets]에 이미 있습니다. [InDesign Server 구성](indesign.md)을 통해 하위 자산을 추출할 수 있습니다. [!DNL InDesign] 파일에 포함된 자산이 하위 자산으로 추출됩니다.

>[!NOTE]
>
>[!DNL InDesign Server]이(가) 프록시되는 경우 [!DNL InDesign] 파일의 미리 보기가 XMP 메타데이터 내에 포함되어 있습니다. 이 경우 썸네일 추출이 명시적으로 필요하지 않습니다. 그러나 [!DNL InDesign Server]이(가) 프록시되지 않으면 [!DNL InDesign] 파일에 대해 썸네일을 명시적으로 추출해야 합니다.

INDD 파일이 업로드되면 저장소에 `xmpMM:InstanceID` 및 `xmpMM:DocumentID` 속성이 있는 자산을 쿼리하여 참조를 가져옵니다.

### 에셋을 끌어 참조 만들기 {#create-references-by-dragging-aem-assets}

이 절차는 [Adobe Illustrator에서 참조로 디지털 에셋을 추가](#refai)하는 것과 유사합니다.

### ZIP 파일을 내보내어 에셋에 대한 참조 만들기 {#create-references-to-aem-assets-by-exporting-a-zip-file}

1. [워크플로 모델 만들기](/help/sites-developing/workflows-models.md)의 단계를 수행하여 워크플로를 만듭니다.
1. [!DNL Adobe InDesign]의 [패키지 기능](https://helpx.adobe.com/indesign/how-to/indesign-package-files-for-handoff.html)을(를) 사용하여 문서를 내보냅니다. [!DNL Adobe InDesign]에서 문서 및 연결된 자산을 패키지로 내보낼 수 있습니다. 이 경우 내보낸 폴더에 [!DNL InDesign] 파일의 하위 자산이 포함된 `Links` 폴더가 있습니다. `Links` 폴더가 INDD 파일과 같은 폴더에 있습니다.
1. ZIP 파일을 만들어 [!DNL Experience Manager] 리포지토리에 업로드합니다.
1. `Unarchiver` 워크플로를 시작합니다.
1. 워크플로우가 완료되면 링크 폴더의 참조가 자동으로 하위 자산으로 참조됩니다. 참조된 자산 목록을 보려면 [!DNL InDesign] 자산의 자산 세부 정보 페이지로 이동하여 [레일](/help/sites-authoring/basic-handling.md#rail-selector)을 닫으십시오.

## [!DNL Adobe Photoshop]: 디지털 에셋을 참조로 추가 {#refps}

1. [!DNL Experience Manager] 데스크톱 앱을 사용하여 [!DNL Experience Manager Assets]에 액세스하세요. 로컬 파일 시스템에서 에셋을 다운로드하고 표시합니다. [!DNL Adobe Photoshop]에서 [!UICONTROL 연결 배치] 기능을 사용하십시오. [데스크톱 앱에 자산 배치](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#place-assets-in-native-documents)를 참조하십시오.

1. 탑재된 드라이브에 [!DNL Photoshop] 파일을 저장하거나 [!DNL Experience Manager] 저장소에 [업로드](/help/assets/manage-assets.md#uploading-assets)하십시오.
1. 워크플로우가 완료되면 기존 [!DNL Experience Manager]개의 자산에 대한 참조가 자산 세부 정보 페이지에 나열됩니다.

   참조된 자산을 보려면 자산 세부 정보 페이지에서 [레일](/help/sites-authoring/basic-handling.md#rail-selector)을 닫으십시오.

1. 참조된 에셋에는 에셋이 참조되는 에셋 목록도 포함됩니다. 참조된 자산 목록을 보려면 자산 세부 정보 페이지로 이동하여 [레일](/help/sites-authoring/basic-handling.md#rail-selector)을 닫으십시오.

>[!NOTE]
>
>복합 에셋 내의 에셋은 문서 ID 및 인스턴스 ID를 기반으로 참조할 수도 있습니다. 이 기능은 [!DNL Adobe Illustrator] 및 [!DNL Adobe Photoshop] 버전에서만 사용할 수 있습니다. 다른 항목의 경우, 참조는 이전 버전의 [!DNL Experience Manager]에서 수행한 대로 기본 복합 에셋에 연결된 에셋의 상대 경로를 기반으로 수행됩니다.

## 하위 자산 만들기 {#generate-subassets}

다중 페이지 형식의 지원되는 에셋(PDF 파일, AI 파일, [!DNL Microsoft PowerPoint] 및 [!DNL Apple Keynote] 파일, [!DNL Adobe InDesign] 파일)에 대해 [!DNL Experience Manager]은(는) 원본 에셋의 각 개별 페이지에 해당하는 하위 에셋을 생성할 수 있습니다. 이러한 하위 자산은 *상위* 자산에 연결되어 여러 페이지를 쉽게 볼 수 있습니다. 다른 모든 용도로 하위 자산은 [!DNL Experience Manager]에서 일반 자산처럼 처리됩니다.

하위 자산 생성은 기본적으로 비활성화되어 있습니다. 하위 자산 생성을 활성화하려면 다음 단계를 수행합니다.

1. [!DNL Experience Manager]에 관리자로 로그인합니다. **[!UICONTROL 도구]** > **[!UICONTROL 워크플로]** > **[!UICONTROL 모델]**&#x200B;에 액세스합니다.
1. **[!UICONTROL DAM 자산 업데이트]** 워크플로우를 선택하고 **[!UICONTROL 편집]**&#x200B;을 클릭합니다.
1. **[!UICONTROL 사이드 패널 전환]**&#x200B;을 클릭하고 **[!UICONTROL 하위 자산 만들기]** 단계를 찾습니다. 워크플로우에 단계를 추가합니다. **[!UICONTROL 동기화]**&#x200B;를 클릭합니다.

하위 자산을 생성하려면 다음 중 하나를 수행합니다.

* 새 자산: [!DNL Experience Manager]에 업로드된 새 자산에 대해 [!UICONTROL DAM Assets 업데이트] 워크플로우가 실행됩니다. 새 다중 페이지 자산에 대해 하위 자산이 자동으로 생성됩니다.
* 기존 다중 페이지 자산: 다음 단계 중 하나에 따라 [!UICONTROL DAM Assets 업데이트] 워크플로우를 수동으로 실행합니다.

   * 자산을 선택하고 [!UICONTROL 타임라인]을 클릭하여 왼쪽 패널을 엽니다. 또는 키보드 단축키 `alt + 3`을(를) 사용합니다. [!UICONTROL 워크플로 시작]을 클릭하고 [!UICONTROL DAM 자산 업데이트]를 선택하고 [!UICONTROL 시작]을 클릭한 다음 [!UICONTROL 계속]을 클릭합니다.
   * 자산을 선택하고 도구 모음에서 [!UICONTROL 만들기] > [!UICONTROL 워크플로]를 클릭합니다. 팝업 대화 상자에서 [!UICONTROL DAM 자산 업데이트] 워크플로우를 선택하고 [!UICONTROL 시작]을 클릭한 다음 [!UICONTROL 계속]을 클릭합니다.

특히 Microsoft Word 문서의 경우 **[!UICONTROL DAM Word 문서 구문 분석]** 워크플로우를 실행하십시오. Microsoft Word 문서의 콘텐츠에서 `cq:Page` 구성 요소를 생성합니다. 문서에서 추출된 이미지가 `cq:Page` 구성 요소에서 참조됩니다. 이러한 이미지는 하위 에셋 생성이 비활성화된 경우에도 추출됩니다.

>[!NOTE]
>
>[!UICONTROL 프로세스 인수]의 [!UICONTROL 하위 자산 만들기 프로세스 - 단계 속성]에서 [!DNL Experience Manager]이(가) 생성하는 하위 자산의 수를 지정할 수 있습니다. 기본값은 5입니다. 모든 하위 에셋을 생성하려면 필드를 비워 둡니다. 필드에 음수가 있으면 하위 에셋이 생성되지 않습니다.

## 하위 자산 보기 {#viewing-subassets}

하위 에셋은 하위 에셋이 생성되고 선택한 다중 페이지 에셋에 사용할 수 있는 경우에만 표시됩니다. 생성된 하위 자산을 보려면 다중 페이지 자산을 엽니다. 페이지의 왼쪽 상단 영역에서 ![왼쪽 레일을 여는 옵션](assets/do-not-localize/aem_leftrail_contentonly.png)을 클릭하고 목록에서 **[!UICONTROL 하위 자산]**&#x200B;을 클릭합니다. 목록에서 **[!UICONTROL 하위 자산]**&#x200B;을(를) 선택하는 경우. 또는 키보드 단축키 `alt + 5`을(를) 사용합니다.

![다중 페이지 자산에 대한 하위 자산 보기](assets/view_subassets_simulation.gif)

## 다중 페이지 파일의 페이지 보기 {#view-pages-of-a-multi-page-file}

[!DNL Experience Manager Assets]의 페이지 뷰어 기능을 사용하여 PDF, INDD, PPT, PPTX 및 AI 파일과 같은 다중 페이지 파일을 볼 수 있습니다. 다중 페이지 자산을 열고 페이지의 왼쪽 상단에서 **[!UICONTROL 페이지 보기]**&#x200B;를 클릭합니다. 열리는 페이지 뷰어에는 에셋의 페이지와 각 페이지를 탐색하고 확대/축소할 수 있는 컨트롤이 표시됩니다.

![다중 페이지 자산의 페이지 보기](assets/view_multipage_asset_fmr.gif)

[!DNL InDesign]의 경우 [!DNL InDesign Server]을(를) 사용하여 페이지를 추출할 수 있습니다. [!DNL InDesign] 파일을 만드는 동안 페이지의 미리 보기를 저장하면 페이지 추출에 [!DNL InDesign Server]이(가) 필요하지 않습니다.

다음 옵션은 도구 모음, 왼쪽 레일 및 페이지 뷰어 컨트롤에서 사용할 수 있습니다.

* [!DNL Experience Manager] 데스크톱 앱을 사용하여 특정 하위 자산을 열거나 표시하는 **[!UICONTROL 데스크톱 작업]**. [!DNL Experience Manager] 데스크톱 앱을 사용하는 경우 [데스크톱 작업을 구성하는 방법](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#desktopactions-v2)을 참조하세요.

* **[!UICONTROL 속성]** 옵션을 사용하면 특정 하위 자산의 [!UICONTROL 속성] 페이지가 열립니다.

* **[!UICONTROL 주석]** 옵션을 사용하면 특정 하위 자산에 주석을 달 수 있습니다. 별도의 하위 에셋에서 사용하는 주석은 상위 에셋을 열어 볼 때 함께 수집되어 표시됩니다.

* **[!UICONTROL 페이지 개요]** 옵션은 모든 하위 자산을 동시에 표시합니다.

* ![왼쪽 레일을 여는 옵션](assets/do-not-localize/aem_leftrail_contentonly.png)을 클릭하면 왼쪽 레일의 **[!UICONTROL 타임라인]** 옵션이 파일에 대한 활동 스트림을 표시합니다.

## 모범 사례 및 제한 사항 {#best-practice-limitation-tips}

* 하위 자산 생성은 [!DNL Experience Manager] 배포에서 리소스를 많이 사용할 수 있습니다. 복잡한 에셋이 업로드될 때 하위 에셋을 생성하는 경우 DAM 에셋 업데이트 워크플로에서 단계를 추가합니다. 온디맨드로 하위 에셋을 생성하는 경우 별도의 워크플로우를 만들어 하위 에셋을 생성합니다. 전용 워크플로우를 사용하면 DAM 자산 업데이트 워크플로우의 다른 단계를 건너뛰고 계산 리소스를 저장할 수 있습니다.

>[!MORELIKETHIS]
>
>* [Adobe Experience Manager 데스크톱 앱 사용](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)
>* [Adobe Experience Manager에서 데스크톱 작업 구성](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#desktopactions-v2)
>* [Adobe Photoshop에서 연결된 스마트 개체 만들기](https://helpx.adobe.com/photoshop/using/create-smart-objects.html#create-linked-smart-objects)
>* [Adobe InDesign에 그래픽 배치](https://helpx.adobe.com/indesign/using/placing-graphics.html)
