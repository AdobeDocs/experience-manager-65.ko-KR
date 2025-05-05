---
title: Dynamic Media 일반 설정 구성
description: Dynamic Media에서 일반 설정을 관리하는 방법을 알아봅니다. 여기에서 게시 서버 이름과 원본 서버 이름을 설정하고 이미지 덮어쓰기 옵션을 설정할 수 있습니다. 또한 이미지의 언샵 마스킹을 위한 기본 업로드 옵션과 PostScript, Adobe Photoshop, PDF 및 Adobe Illustrator 파일을 처리하는 방법에 대한 업로드 옵션이 있습니다.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User, Admin
mini-toc-levels: 4
exl-id: 55cc7c57-87a0-4bfb-b226-36d01d36849a
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '2506'
ht-degree: 0%

---

# Dynamic Media 일반 설정 구성

**[!UICONTROL Dynamic Media 일반 설정]** 구성은 다음 경우에만 사용할 수 있습니다.

* Scene7 모드에서 Dynamic Media을 실행하고 있습니다. [Scene7 모드에서 Dynamic Media 사용](/help/assets/config-dms7.md#enabling-dynamic-media-in-scene-mode)을 참조하십시오.
* Adobe Experience Manager 6.5.11 이상에 *기존* **[!UICONTROL Dynamic Media 구성]**(**[!UICONTROL Cloud Service]**&#x200B;에서)이 있습니다. [Cloud Service에서 Dynamic Media 구성 만들기](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services)를 참조하십시오.
* 관리자 권한이 있는 Experience Manager 시스템 관리자입니다.

Dynamic Media 일반 설정 은 숙련된 웹 사이트 개발자와 프로그래머가 사용할 수 있도록 설계되었습니다. Adobe Dynamic Media은 이러한 게시 설정을 변경하는 사용자에게 Adobe Experience Manager의 Dynamic Media 및 기본 이미징 기술을 잘 익힐 것을 권장합니다.

계정 생성 시 Dynamic Media Adobe은 회사에 할당된 서버를 자동으로 제공합니다. 이러한 서버는 웹 사이트 및 응용 프로그램의 URL 문자열을 구성하는 데 사용됩니다. 이러한 URL 호출은 계정에만 해당됩니다.

Dynamic Media Publish 설정 페이지는 Adobe Dynamic Media 서버에서 웹 사이트 또는 애플리케이션으로 에셋을 전달하는 방법을 결정하는 기본 설정을 구성합니다. 설정을 지정하지 않으면 Adobe Dynamic Media 서버는 Dynamic Media Publish 설정 페이지에서 구성한 기본 설정에 따라 자산을 전달합니다.

추가 선택적 구성 작업은 [옵션 - Dynamic Media 설정 및 구성 - Scene7 모드 설정](/help/assets/config-dms7.md#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings)을 참조하십시오.

>[!NOTE]
>
>Adobe Experience Manager에서 Dynamic Media Classic에서 Dynamic Media으로 업그레이드하시겠습니까? Dynamic Media의 일반 설정 페이지 및 [Publish 설정](/help/assets/dm-publish-settings.md) 페이지는 Dynamic Media Classic 계정에서 가져온 값으로 미리 채워집니다. 일반 설정 페이지의 **[!UICONTROL 기본 업로드 옵션]** 영역에 나열된 모든 값은 예외입니다. 해당 값은 이미 Experience Manager 상태입니다. 따라서 Experience Manager 사용자 인터페이스를 통해 **[!UICONTROL 기본 업로드 옵션]**&#x200B;의 5개 탭에서 변경한 내용은 Dynamic Media Classic이 아닌 Dynamic Media에 반영됩니다. 일반 설정 페이지 및 [Publish 설정](/help/assets/dm-publish-settings.md) 페이지의 다른 모든 설정 및 값은 Experience Manager 시 Dynamic Media Classic과 Dynamic Media 간에 유지 관리됩니다.

**Dynamic Media 일반 설정을 구성하려면:**

1. Experience Manager 작성자 모드에서 Experience Manager 로고를 선택하여 전역 탐색 콘솔에 액세스합니다.
1. 왼쪽 레일에서 도구 아이콘을 선택한 다음 **[!UICONTROL Assets]** > **[!UICONTROL Dynamic Media 일반 설정]**(으)로 이동합니다.
1. 서버 페이지에서 **[!UICONTROL 게시된 서버 이름]** 및 **[!UICONTROL 원본 서버 이름]**&#x200B;을 설정한 다음 다섯 개의 탭을 사용하여 이미지 편집과 Postscript, Photoshop, PDF 및 Illustrator 파일에 대한 기본 업로드 옵션을 구성합니다.

   * [서버](#server-general-setting)
   * [애플리케이션에 업로드](#upload-to-application)
   * [이미지 편집](#image-editing-tab) 탭
   * [PostScript](#postscript-tab) 탭
   * [Photoshop](#photoshop-tab) 탭
   * [PDF](#pdf-tab) 탭
   * [Illustrator](#illustrator-tab) 탭

   ![Dynamic Media 일반 설정 페이지](/help/assets/assets-dm/dm-general-settings.png)
   *Dynamic Media 일반 설정 페이지(**[!UICONTROL 이미지 편집]**&#x200B;탭 선택)*<br><br>

1. 완료되면 페이지의 오른쪽 상단 근처에서 **[!UICONTROL 저장]**&#x200B;을 선택합니다.

## 서버 {#server-general-setting}

계정 생성 시 Dynamic Media Adobe은 회사에 할당된 서버를 자동으로 제공합니다. 이러한 서버는 웹 사이트 및 응용 프로그램의 URL 문자열을 구성하는 데 사용됩니다. 이러한 URL 호출은 계정에만 해당됩니다.

| 옵션 | 설명 |
| --- | --- |
| **[!UICONTROL 게시된 서버 이름]** | 필수.<br>이름은 경로에 `https://`을(를) 사용해야 합니다.<br>이 서버는 사용자 계정과 관련된 모든 시스템 생성 URL 호출에 사용되는 Live CDN(Content Deliver Network) 서버입니다. Adobe 기술 지원부에서 지시하지 않는 한 이 서버 이름을 변경하지 마십시오. |
| **[!UICONTROL 원본 서버 이름]** | 필수.<br>이 서버는 품질 보증 테스트에만 사용됩니다. Adobe 기술 지원부에서 지시하지 않는 한 이 서버 이름을 변경하지 마십시오. |

## 애플리케이션에 업로드 {#upload-to-application}

* **[!UICONTROL 이미지 덮어쓰기]**

  Adobe Dynamic Media에서는 두 파일의 이름이 동일하지 않습니다. 각 항목의 Adobe Dynamic Media ID(이미지 이름에서 파일 이름 확장자를 뺀 값)는 고유해야 합니다. 이 규칙 때문에 **[!UICONTROL 응용 프로그램에 업로드]**&#x200B;에 덮어쓰기가 있습니다. 이 옵션의 정확한 효과는 선택한 지정된 이미지 덮어쓰기 옵션에 따라 달라집니다. 이러한 옵션은 대체 이미지를 업로드하는 방법을 지정합니다. 즉, 원본 이미지를 바꾸는지 아니면 중복 이미지가 되는지의 여부를 지정합니다. 중복 이미지의 이름이 `-1`(으)로 바뀝니다. 예를 들어 `chair.tif`의 이름이 `chair-1.tif`(으)로 바뀝니다. 이러한 옵션은 원본과 다른 폴더에 업로드된 이미지 또는 원본과 다른 파일 확장자(예: JPG, TIF 또는 PNG)를 갖는 이미지에 영향을 줍니다.

  >[!NOTE]
  >
  >Experience Manager과 일관성을 유지하려면 [이미지 덮어쓰기] 옵션 **[!UICONTROL 같은 기본 이름/확장명으로 현재 폴더에 덮어쓰기]**&#x200B;를 선택하십시오.

  | 이미지 덮어쓰기 옵션 | 설명 |
  | --- | --- |
  | **[!UICONTROL 같은 기본 이름/확장명으로 현재 폴더에 덮어쓰기]** | 새 Dynamic Media 계정에만 *기본값*.<br>이 옵션은 교체에 가장 엄격한 규칙입니다. 대체 이미지를 원본과 동일한 폴더에 업로드하고 대체 이미지의 파일 이름 확장명이 원본과 동일해야 합니다. 이러한 요구 사항이 충족되지 않으면 복제본이 생성됩니다.<br>*Experience Manager과 일관성을 유지하려면 이 옵션을 선택하십시오*. |
  | **[!UICONTROL 확장명에 상관없이 같은 기본 이름으로 현재 폴더에 덮어쓰기]** | 대체 이미지를 원본과 동일한 폴더에 업로드해야 하지만, 파일 이름 확장명이 원본과 다를 수 있습니다. 예를 들어 chair.tif는 chair.jpg를 대체합니다. |
  | **[!UICONTROL 같은 기본 에셋 이름/확장명으로 모든 폴더에 덮어쓰기]** | 대체 이미지의 파일 이름 확장명이 원본 이미지와 동일해야 합니다(예: chair.jpg는 chair.tif가 아닌 chair.jpg를 대체해야 함). 그러나 대체 이미지를 원본과 다른 폴더에 업로드할 수 있습니다. 업데이트된 이미지가 새 폴더에 있습니다. 파일은 원래 위치에서 더 이상 찾을 수 없습니다. |
  | **[!UICONTROL 확장명에 상관없이 같은 기본 자산 이름으로 모든 폴더에 덮어쓰기]** | 이 옵션은 가장 포괄적인 대체 규칙입니다. 대체 이미지를 원본이 아닌 다른 폴더에 업로드하고, 파일 확장명이 다른 파일을 업로드하고, 원본 파일을 바꿀 수 있습니다. 원본 파일이 다른 폴더에 있는 경우 대체 이미지는 업로드된 새 폴더에 있습니다. |

* **[!UICONTROL 자르기 유지]**

  기존 수동 자르기 정의의 유지를 제어합니다.

  Dynamic Media 뷰어 참조 가이드의 [UploadPostJob](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-upload-post-job.html) 및 [ReprocessAssetsJob](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-reprocess-assets-job.html)에서도 `preserveCrop`을(를) 참조하십시오.

## 기본 업로드 옵션 {#default-upload-options}

### 이미지 편집 탭 {#image-editing-tab}

이 필터를 사용하면 최종 다운샘플링된 이미지에서 선명하게 하기 필터 효과를 미세 조정할 수 있습니다. 효과의 강도, 효과의 반경(픽셀 단위 측정) 및 무시되는 대비 임계값을 제어하는 데 도움이 됩니다.

[언샵 마스크] 효과는 Photoshop의 [언샵 마스크] 필터와 동일한 옵션을 사용합니다. 언샵 마스크는 이름과는 달리 선명하게 하기 필터입니다.

| [언샵 마스크] 옵션 | 설명 |
| --- | --- |
| **[!UICONTROL 금액]** | 필수.<br>가장자리 픽셀에 적용되는 대비의 양을 제어합니다.<br>효과의 강도로 생각하십시오. Adobe Dynamic Media의 언샵 마스크 금액 값과 Adobe Photoshop의 금액 값의 주요 차이점은 Photoshop의 금액 범위가 1%~500%라는 것입니다. 반면 Adobe Dynamic Media에서는 값 범위가 `0.0`에서 `5.0`까지입니다. Adobe Dynamic Media의 값 5.0은 Photoshop의 500%에 해당하는 대략적인 값이며, 값 0.9는 90%에 해당하는 대략적인 값입니다. |
| **[!UICONTROL 반경]** | 필수.<br>효과의 반경을 제어합니다.<br>값 범위는 `0`에서 `250`까지입니다. 이 효과는 이미지의 모든 픽셀에서 실행되며 모든 픽셀에서 모든 방향으로 방사됩니다. 반경은 픽셀 단위로 측정됩니다. 예를 들어, 2000 x 2000 픽셀 이미지와 500 x 500 픽셀 이미지에 대해 유사한 선명하게 하기 위해 2000 x 2000 픽셀 이미지에 대해 두 픽셀의 반경을 설정합니다. 그런 다음 500 x 500 픽셀 이미지에서 한 픽셀의 반경 값을 설정합니다. 더 많은 픽셀이 있는 이미지에는 더 큰 값이 사용됩니다. |
| **[!UICONTROL 임계값]** | 필수.<br>임계값은 [언샵 마스크] 필터를 적용할 때 무시되는 대비 범위입니다. 이 필터를 사용할 때 이미지에 &quot;노이즈&quot;가 삽입되지 않도록 이 효과가 중요합니다. 값 범위는 회색 음영 이미지의 밝기 단계 수인 `0` - `255`입니다. `0`=검정, `128`=50% 회색 및 `255`=흰색.<br>작은 변화를 무시하는 임계값 `12`은(는) 피부 색조 밝기로 노이즈를 추가하지 않지만 속눈썹이 피부와 만나는 곳과 같은 대비되는 영역에 가장자리 대비를 추가합니다.<br>다른 사람의 얼굴 사진이 있는 경우 [언샵 마스크]는 이미지의 대비되는 부분에 영향을 줍니다. 예를 들어, 속눈썹과 피부가 만나 뚜렷한 대조 영역을 만들고 매끄러운 피부 그 자체입니다. 가장 매끄러운 피부도 밝기 값에 미묘한 변화를 보인다. 임계값을 사용하지 않는 경우에는 필터가 스킨 픽셀에서 이러한 미묘한 변화를 강조합니다. 차례로, 시끄럽고 바람직하지 않은 효과가 만들어지면서 속눈썹의 조영 증대가 이루어져 선명도를 향상시킨다.<br>이 문제를 방지하기 위해 필터에 부드러운 피부처럼 대비가 크게 변경되지 않는 픽셀을 무시하도록 하는 임계값이 도입되었습니다.<br>앞에 표시된 지퍼 그래픽에서 지퍼 옆에 있는 질감을 확인합니다. 문턱값이 너무 낮아서 노이즈를 억제하지 못하기 때문에 화상 노이즈가 나타난다. |
| **[!UICONTROL 흑백]** | 이미지 밝기(강도)를 언샵 마스크하려면 선택합니다.<br>각 색상 구성 요소를 개별적으로 선택 해제하려면 선택을 취소합니다. |

[Adobe Dynamic Media 및 이미지 서버에서 이미지 선명하게 하기](/help/assets/assets/sharpening_images.pdf)도 참조하세요.

### PostScript 탭 {#postscript-tab}

Adobe PostScript® 파일을 래스터화하고 투명한 배경을 유지하며 해상도를 선택하고 색상 공간을 선택할 수 있습니다.

Dynamic Media Adobe에서 Adobe PostScript® (EPS) 파일을 사용할 수 있습니다. Adobe Dynamic Media은 이러한 파일을 업로드할 때 구성하기 위한 명령을 제공합니다.

PostScript(EPS) 이미지 파일을 업로드할 때 다양한 방법으로 형식을 지정할 수 있습니다. 파일을 래스터화하고 투명 배경을 유지하며 해상도를 선택하고 색상 공간을 선택할 수 있습니다.

| PostScript 옵션 | 설명 |
| --- | --- |
| **[!UICONTROL 처리 중]** | [래스터화]를 선택하여 파일의 벡터 그래픽을 비트맵 형식으로 변환합니다. |
| **[!UICONTROL 렌더링된 이미지에서 투명 배경 유지]** | 파일의 배경 투명도를 유지합니다. |
| **[!UICONTROL 해상도(픽셀/인치)]** | 해상도 설정을 결정합니다. 이 설정은 파일의 인치당 표시되는 픽셀 수를 결정합니다. |
| **[!UICONTROL 색상 공간]** | · **[!UICONTROL 자동으로 감지]** - 파일의 색상 공간을 유지합니다.<br>· **[!UICONTROL RGB으로 적용]** - RGB 색상 공간으로 변환합니다.<br>· **[!UICONTROL CMYK로 강제 적용]** - CMYK 색상 공간으로 변환합니다.<br>· **[!UICONTROL 회색으로 강제 적용]** - 회색조 색상 공간으로 변환합니다. |

### Photoshop 탭 {#photoshop-tab}

Adobe® Photoshop® 파일에서 템플릿을 만들고, 레이어를 유지하고, 레이어 이름 지정 방법을 지정하고, 텍스트를 추출하고, 이미지가 템플릿에 고정되는 방법을 지정할 수 있습니다.

| Photoshop 옵션 | 설명 |
| --- | --- |
| **[!UICONTROL 레이어 유지]** | PSD의 레이어(있는 경우)를 개별 에셋으로 분할합니다. 에셋 레이어는 PSD과 연결된 상태로 유지됩니다. 세부 사항 보기의 PSD 파일을 열고 레이어 패널을 선택하여 해당 파일을 볼 수 있습니다. PSD 파일에서 레이어 보기 및 편집을 참조하십시오. |
| **[!UICONTROL 템플릿 만들기]** | PSD 파일의 레이어로 템플릿을 만듭니다. |
| **[!UICONTROL 텍스트 추출]** | 사용자가 뷰어에서 텍스트를 검색할 수 있도록 텍스트를 추출합니다. |
| **[!UICONTROL 레이어를 배경 크기로 확장]** | 리핑된 이미지 레이어의 크기를 배경 레이어의 크기로 확장합니다. |
| **[!UICONTROL 레이어 이름 지정]** | 리핑된 이미지 레이어의 크기를 배경 레이어의 크기로 확장합니다.<br>· **[!UICONTROL 레이어 이름]** - PSD 파일에서 레이어 이름 뒤에 이미지 이름을 지정합니다. 예를 들어 원본 PSD 파일에서 Price Tag 라는 이름의 레이어는 Price Tag 라는 이미지가 됩니다. 그러나 PSD 파일의 레이어 이름이 기본 Photoshop 레이어 이름(배경, 레이어 1, 레이어 2 등)이면 PSD 파일에서 해당 레이어 번호의 이름을 따서 이미지 이름이 지정됩니다. <br>· **[!UICONTROL Photoshop 및 레이어 번호]** - 원래 레이어 이름을 무시하고 PSD 파일에서 레이어 번호 뒤에 이미지 이름을 지정합니다. 이미지 이름은 Photoshop 파일 이름과 추가된 레이어 번호로 지정됩니다. 예를 들어, 이름이 `Spring Ad.psd`인 파일의 두 번째 레이어는 Photoshop에 기본이 아닌 이름이 있더라도 이름이 `Spring Ad_2`입니다.<br>· **[!UICONTROL Photoshop 및 레이어 이름]** - PSD 파일 뒤에 레이어 이름 또는 레이어 번호가 붙은 이미지 이름을 지정합니다. PSD 파일의 레이어 이름이 기본 Photoshop 레이어 이름인 경우 레이어 번호가 사용됩니다. 예를 들어 PSD 파일 `SpringAd`에 있는 `Price Tag` 레이어의 이름은 `Spring Ad_Price Tag`입니다. 기본 이름이 Layer 2인 레이어를 `Spring Ad_2`이라고 합니다. |
| **[!UICONTROL 앵커]** | PSD 파일에서 생성된 레이어 컴포지션에서 생성된 템플릿에서 이미지가 고정되는 방식을 지정합니다. 기본적으로 앵커는 가운데입니다. 가운데 앵커를 사용하면 대체 이미지의 종횡비에 관계없이 대체 이미지가 동일한 공간을 가장 잘 채울 수 있습니다. 템플릿을 참조하고 매개 변수 대체를 사용할 때 이 이미지를 대체하는 다른 양상의 이미지가 동일한 공간을 효과적으로 차지합니다. 템플릿에서 할당된 공간을 채우기 위해 응용 프로그램에 교체 이미지가 필요한 경우 다른 설정으로 변경합니다. |

### PDF 탭 {#pdf-tab}

파일을 래스터화하고, 검색어와 링크를 추출하고, 해상도를 설정하고, 색상 공간을 선택할 수 있습니다.

| PDF 옵션 | 설명 |
| --- | --- |
| **[!UICONTROL 처리 중]** | · **[!UICONTROL 없음]** - PDF 처리가 완료되지 않았습니다.<br>· **[!UICONTROL 축소판]** - PDF 파일의 각 페이지를 잘라내어 축소판 이미지로 변환합니다.<br> · **[!UICONTROL 래스터화]** - PDF 파일의 페이지를 분리하고 벡터 그래픽을 비트맵 이미지로 변환합니다. eCatalog를 만들려면 이 옵션을 선택합니다. |
| **[!UICONTROL 추출]** | · **[!UICONTROL 없음]** - PDF에서 추출된 검색어 또는 링크가 없습니다.<br>· **[!UICONTROL 검색어]** - eCatalog 뷰어에서 키워드로 파일을 검색할 수 있도록 PDF 파일에서 검색어를 추출합니다.<br>· **[!UICONTROL 링크]** - PDF 파일에서 링크를 추출하여 eCatalog 뷰어에서 사용되는 이미지 맵으로 변환합니다.<br>· **[!UICONTROL 검색어 및 링크]** - eCatalog 뷰어에서 사용할 검색어와 링크를 모두 추출합니다. |
| **[!UICONTROL 해상도(픽셀/인치)]** | 해상도 설정을 결정합니다. 이 설정은 PDF 파일에서 인치당 표시되는 픽셀 수를 결정합니다. 기본값은 150입니다. |
| **[!UICONTROL 색상 공간]** | · **[!UICONTROL 자동으로 감지]** - PDF 파일의 색상 공간을 유지합니다.<br>· **[!UICONTROL RGB으로 적용]** - RGB 색상 공간으로 변환합니다.<br>· **[!UICONTROL CMYK로 강제 적용]** - CMYK 색상 공간으로 변환합니다.<br>· **[!UICONTROL 회색으로 강제 적용]** - 회색조 색상 공간으로 변환합니다. |

### Illustrator 탭 {#illustrator-tab}

Adobe Illustrator® 파일을 래스터화하고 투명한 배경을 유지하며 해상도를 선택하고 색상 공간을 선택할 수 있습니다.

Dynamic Media Adobe에서 Adobe® Illustrator® (AI) 파일을 사용할 수 있습니다. Adobe Dynamic Media은 이러한 파일을 업로드할 때 구성하기 위한 명령을 제공합니다.

Illustrator(AI) 이미지 파일을 업로드할 때 다양한 방법으로 형식을 지정할 수 있습니다. 파일을 래스터화하고 투명 배경을 유지하며 해상도를 선택하고 색상 공간을 선택할 수 있습니다. PostScript 및 Illustrator 파일 형식 지정 옵션은 업로드 작업 옵션 상자의 PostScript 옵션 및 Illustrator 옵션 아래에 있는 업로드 화면에서 사용할 수 있습니다.


| Illustrator 옵션 | 설명 |
| --- | --- |
| **[!UICONTROL 처리 중]** | [래스터화]를 선택하여 파일의 벡터 그래픽을 비트맵 형식으로 변환합니다. |
| **[!UICONTROL 렌더링된 이미지에서 투명 배경 유지]** | 파일의 배경 투명도를 유지합니다. |
| **[!UICONTROL 해상도(픽셀/인치)]** | 해상도 설정을 결정합니다. 이 설정은 파일의 인치당 표시되는 픽셀 수를 결정합니다. |
| **[!UICONTROL 색상 공간]** | · **[!UICONTROL 자동으로 감지]** - 파일의 색상 공간을 유지합니다.<br>· **[!UICONTROL RGB으로 적용]** - RGB 색상 공간으로 변환합니다.<br>· **[!UICONTROL CMYK로 강제 적용]** - CMYK 색상 공간으로 변환합니다.<br>· **[!UICONTROL 회색으로 강제 적용]** - 회색조 색상 공간으로 변환합니다. |
