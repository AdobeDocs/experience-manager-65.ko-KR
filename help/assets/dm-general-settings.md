---
title: Dynamic Media 일반 설정 구성
description: Dynamic Media에서 일반 설정을 관리하는 방법을 알아봅니다. 여기에 게시 서버 이름과 원본 서버 이름을 설정하고 이미지 덮어쓰기 옵션을 설정할 수 있습니다. 또한 이미지의 언샵 마스킹을 위한 기본 업로드 옵션과 PostScript, Adobe Photoshop, PDF 및 Adobe Illustrator 파일을 처리하는 방법에 대한 업로드 옵션이 있습니다.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User, Admin
mini-toc-levels: 4
hide: true
hidefromtoc: true
exl-id: null
source-git-commit: 26f521868d0b983a05579d0d4c1ef50684b721ee
workflow-type: tm+mt
source-wordcount: '2454'
ht-degree: 4%

---


# Dynamic Media 일반 설정 구성

구성 **[!UICONTROL Dynamic Media 일반 설정]** 다음 경우에만 사용할 수 있습니다.

* Scene7 모드에서 Dynamic Media을 실행하고 있습니다. 자세한 내용은 [Scene7 모드에서 Dynamic Media 활성화](/help/assets/config-dms7.md#enabling-dynamic-media-in-scene-mode)
* 다음 항목이 있습니다. *기존* **[!UICONTROL Dynamic Media 구성]** (in) **[!UICONTROL Cloud Services]**) 내의 아무 곳에나 삽입할 수 있습니다.
* 관리자 권한을 가진 Experience Manager 시스템 관리자입니다.

Dynamic Media 일반 설정은 숙련된 웹 사이트 개발자와 프로그래머가 사용하기 위한 것입니다. Adobe Dynamic Media에서는 이러한 게시 설정을 변경하는 사용자가 Adobe Experience Manager의 Dynamic Media 및 기본 이미징 기술에 익숙할 것을 권장합니다.

계정을 만들 때 Dynamic Media Adobe에서 자동으로 회사에 할당된 서버를 제공합니다. 이러한 서버는 웹 사이트 및 애플리케이션에 대한 URL 문자열을 구성하는 데 사용됩니다. 이러한 URL 호출은 계정에만 적용됩니다.

Dynamic Media 게시 설정 페이지에서는 Dynamic Media Adobe 서버에서 웹 사이트 또는 응용 프로그램으로 자산을 전달하는 방법을 결정하는 기본 설정을 설정합니다. 설정이 지정되지 않은 경우 Adobe Dynamic Media 서버는 Dynamic Media 게시 설정 페이지에 구성된 기본 설정에 따라 자산을 전달합니다.

참조 - [Dynamic Media 설정 및 구성 - Scene7 모드 설정](/help/assets/option-b-config-dms7.md#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings).

>[!NOTE]
>
>Adobe Experience Manager에서 Dynamic Media Classic으로 업그레이드하시겠습니까? Dynamic Media의 일반 설정 및 게시 설정 페이지는 Dynamic Media Classic 계정에서 가져온 값으로 미리 채워집니다. 예외는 **[!UICONTROL 기본 업로드 옵션]** 일반 설정 페이지의 영역. 해당 값은 이미 Experience Manager에 있습니다. 따라서 사용자가 변경한 사항이 **[!UICONTROL 기본 업로드 옵션]**, 5개 탭 모두에 Experience Manager 사용자 인터페이스가 Dynamic Media Classic이 아닌 Dynamic Media에 반영됩니다. 일반 설정 및 게시 설정 페이지의 다른 모든 설정 및 값은 Experience Manager의 Dynamic Media Classic과 Dynamic Media 간에 유지됩니다.

**Dynamic Media 일반 설정을 구성하려면:**

1. Experience Manager 작성자 모드에서 Experience Manager 로고를 선택하여 전역 탐색 콘솔에 액세스합니다.
1. 왼쪽 레일에서 도구 아이콘을 선택한 다음 **[!UICONTROL 자산]** > **[!UICONTROL Dynamic Media 일반 설정]**.
1. 서버 페이지에서 **[!UICONTROL 게시된 서버 이름]** 및 **[!UICONTROL 원본 서버 이름]**&#x200B;그런 다음 다섯 개의 탭을 사용하여 이미지 편집과 Postscript, Photoshop, PDF 및 Illustrator 파일에 대한 기본 업로드 옵션을 구성합니다.

   * [서버](#server-general-setting)
   * [애플리케이션에 업로드](#upload-to-application)
   * [이미지 편집](#image-editing-tab) 탭
   * [PostScript](#postscript-tab) 탭
   * [Photoshop](#photoshop-tab) 탭
   * [PDF](#pdf-tab) 탭
   * [Illustrator](#illustrator-tab) 탭

   ![Dynamic Media 일반 설정 페이지](/help/assets/assets-dm/dm-general-settings.png)
   *Dynamic Media 일반 설정 페이지,**[!UICONTROL 이미지 편집]**탭 선택.*<br><br>

1. 완료되면 페이지의 오른쪽 위 모서리 근처에 있는 를 선택합니다. **[!UICONTROL 저장]**.

## 서버 {#server-general-setting}

계정을 만들 때 Dynamic Media Adobe에서 자동으로 회사에 할당된 서버를 제공합니다. 이러한 서버는 웹 사이트 및 애플리케이션에 대한 URL 문자열을 구성하는 데 사용됩니다. 이러한 URL 호출은 계정에만 적용됩니다.

| 옵션 | 설명 |
| --- | --- |
| **[!UICONTROL 게시된 서버 이름]** | 필수.<br>이름은 를 사용해야 합니다 `https://` 을 가리키도록 업데이트하는 것이 좋습니다.<br>이 서버는 계정과 관련된 시스템에서 생성한 모든 URL 호출에 사용되는 라이브 CDN(Content Delivery Network) 서버입니다. Adobe 기술 지원에서 이 서버 이름을 변경하지 않도록 지시하는 경우가 아니면 변경하지 마십시오. |
| **[!UICONTROL 원본 서버 이름]** | 필수.<br>이 서버는 품질 보증 테스트에만 사용됩니다. Adobe 기술 지원 센터에서 이 서버 이름을 변경하지 마십시오. |

## 애플리케이션에 업로드 {#upload-to-application}

* **[!UICONTROL 이미지 덮어쓰기]**

   Adobe Dynamic Media에서는 두 파일의 이름이 같을 수 없습니다. 각 항목의 Adobe Dynamic Media ID(이미지 이름에서 파일 확장명을 뺀 숫자)는 고유해야 합니다. 이 규칙 때문에 **[!UICONTROL 애플리케이션에 업로드]** 에는 덮어쓰기 가 있습니다. 이 옵션의 정확한 효과는 선택한 지정된 이미지 덮어쓰기 옵션에 따라 다릅니다. 다음 옵션은 교체 이미지를 업로드하는 방법을 지정합니다. 원본 이미지를 바꾸거나 중복 이미지가 되는지 여부. 중복 이미지 이름은 `-1`. 예, `chair.tif` 가 이름이 변경되었습니다. `chair-1.tif`. 이러한 옵션은 원본 폴더와 다른 폴더에 업로드된 이미지나 원래 파일 확장명(예: JPG, TIF 또는 PNG)이 다른 이미지에 영향을 줍니다.

   | 이미지 덮어쓰기 옵션 | 설명 |
   | --- | --- |
   | **[!UICONTROL 동일한 기본 에셋 이름/확장명으로 현재 폴더에 덮어쓰기]** | 새 Dynamic Media 계정에만 적용되는 기본값입니다.<br>이 옵션은 교체에 대한 가장 엄격한 규칙입니다. 교체 이미지를 원본과 동일한 폴더에 업로드하고 교체 이미지의 파일 확장명이 원본과 동일해야 합니다. 이러한 요구 사항을 충족하지 않으면 복제본이 만들어집니다. |
   | **[!UICONTROL 확장명에 상관없이 동일한 기본 이름으로 현재 폴더에 덮어쓰기]** | 교체 이미지를 원본과 동일한 폴더로 업로드해야 하지만 파일 이름 확장명은 원본과 다를 수 있습니다. 예를 들어 chair.tif는 chair.jpg를 대체합니다. |
   | **[!UICONTROL 동일한 기본 에셋 이름/확장명으로 모든 폴더에 덮어쓰기]** | 교체 이미지의 파일 확장명이 원본 이미지와 동일해야 합니다(예: chair.jpg는 chair.tif가 아니라 chair.jpg로 대체해야 함). 그러나 대체 이미지를 원본과 다른 폴더에 업로드할 수 있습니다. 업데이트된 이미지는 새 폴더에 있습니다. 파일을 원래 위치에서 더 이상 찾을 수 없습니다. |
   | **[!UICONTROL 확장명에 상관없이 동일한 기본 에셋 이름으로 모든 폴더에 덮어쓰기]** | 이 옵션은 가장 포괄적인 대체 규칙입니다. 대체 이미지를 원본과 다른 폴더에 업로드하고, 다른 파일 확장자를 가진 파일을 업로드하고, 원래 파일을 바꿀 수 있습니다. 원본 파일이 다른 폴더에 있는 경우 대체 이미지는 업로드된 새 폴더에 있습니다. |

* **[!UICONTROL 자르기 유지]**

   기존 수동 자르기 정의의 보존을 제어합니다.

   참조 - `preserveCrop` in [UploadPostJob](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-upload-post-job.html) 및 [AssetsJob 재처리](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-reprocess-assets-job.html)둘 다 Dynamic Media 뷰어 참조 가이드에 있습니다.

## 기본 업로드 옵션 {#default-upload-options}

### 이미지 편집 탭 {#image-editing-tab}

이 필터를 사용하면 최종 다운샘플링된 이미지에 대해 선명하게 하기 필터 효과를 세밀하게 조정할 수 있습니다. 이 옵션을 사용하면 효과의 강도, 효과의 반경(픽셀 단위 측정) 및 무시되는 대비 임계값을 제어할 수 있습니다.

[언샵 마스크] 효과는 Photoshop의 [언샵 마스크] 필터와 동일한 옵션을 사용합니다. 이름에서 알 수 있듯이 언샵 마스크는 선명하게 하는 필터입니다.

| 언샵 마스크 옵션 | 설명 |
| --- | --- |
| **[!UICONTROL 양]** | 필수.<br>가장자리 픽셀에 적용되는 대비 양을 제어합니다.<br>그것을 효과의 강도로 생각해 보세요. Adobe Dynamic Media의 언샵 마스크 값과 Adobe Photoshop의 금액 값의 주요 차이점은 Photoshop의 크기가 1%~500%라는 것입니다. Adobe Dynamic Media에서 값 범위는 `0.0` to `5.0`. Adobe Dynamic Media의 값 5.0은 Photoshop의 500%와 거의 같습니다. 0.9값은 90%와 같은 값입니다. |
| **[!UICONTROL 반경]** | 필수.<br>효과의 반경을 제어합니다.<br>값 범위는 다음과 같습니다 `0` to `250`. 효과는 이미지의 모든 픽셀에서 실행되며 모든 방향으로 모든 픽셀에서 발산됩니다. 반지름은 픽셀 단위로 측정됩니다. 예를 들어 2000 x 2000 픽셀 이미지와 500 x 500 픽셀 이미지에 대해 비슷한 선명하게 하기 효과를 가져오려면 200 x 2000 픽셀 이미지에 두 픽셀의 반경을 설정합니다. 그런 다음 500 x 500 픽셀 이미지에 한 픽셀의 반경 값을 설정합니다. 픽셀이 많은 이미지에 더 큰 값이 사용됩니다. |
| **[!UICONTROL 임계값]** | 필수.<br>임계값은 언샵 마스크 필터를 적용할 때 무시되는 대비 범위입니다. 이 필터를 사용할 때 이미지에 &quot;노이즈&quot;가 도입되지 않도록 이 효과가 중요합니다. 값 범위는 다음과 같습니다 `0` - `255`: 회색 음영 이미지에 있는 명도 단계 수입니다. `0`= 검정, `128`= 50% 회색 및 `255`= 흰색.<br>임계값 `12` 약간의 변화를 무시하면 피부 색조 밝기가 나타나지만, 속눈썹이 피부에 닿는 것과 같은 대비가 있는 부위에 가장자리 대비를 추가할 수 있습니다.<br>누군가의 얼굴 사진이 있는 경우, [언샵 마스크]는 이미지의 수축 부위에 영향을 줍니다. 예를 들어, 속눈썹과 피부의 접촉은 뚜렷한 대조 영역과 부드러운 피부 자체를 만들어 냅니다. 아무리 매끄러운 피부라도 휘도 값의 미묘한 변화를 나타낸다. 임계값을 사용하지 않는 경우 필터는 스킨 픽셀에서 이러한 미묘한 변경 사항을 적용합니다. 이에 따라, 속눈썹의 대비가 증가하면서 잡음과 바람직하지 않은 효과를 만들어 냄으로써 선명도가 향상된다.<br>이 문제를 방지하기 위해 부드러운 피부와 같이 대비가 크게 변경되지 않는 픽셀을 무시하도록 필터에 알리는 임계값 이 도입되었습니다.<br>앞서 표시된 지퍼 그래픽에서 지퍼 옆에 있는 텍스처를 확인합니다. 임계값이 너무 낮아 노이즈를 억제할 수 없으므로 이미지 소음이 표시됩니다. |
| **[!UICONTROL 모노크롬]** | 선명하게 마스크 이미지 밝기(강도)를 해제하려면 선택합니다.<br>각 색상 구성 요소를 개별적으로 언샵 마스크하려면 선택 취소합니다. |

참조 - [Adobe Dynamic Media 및 이미지 서버에서 이미지 선명하게 하기](/help/assets/assets/sharpening_images.pdf).

### PostScript 탭 {#postscript-tab}

Adobe PostScript® 파일을 래스터화하고 투명한 배경을 유지하고 해상도를 선택한 다음 색상 공간을 선택할 수 있습니다.

Adobe Dynamic Media에서 Adobe PostScript®(EPS) 파일을 사용할 수 있습니다. Adobe Dynamic Media은 이러한 파일을 업로드할 때 이러한 파일을 구성하는 명령을 제공합니다.

PostScript(EPS) 이미지 파일을 업로드할 때 다양한 방법으로 형식을 지정할 수 있습니다. 파일을 래스터화하고 투명한 배경을 유지하고 해상도를 선택한 다음 색상 공간을 선택할 수 있습니다.

| PostScript 옵션 | 설명 |
| --- | --- |
| **[!UICONTROL 처리 중]** | 파일의 벡터 그래픽을 비트맵 형식으로 변환하려면 [래스터화]를 선택합니다. |
| **[!UICONTROL 렌더링된 이미지의 투명 배경 유지]** | 파일의 배경 투명도를 유지합니다. |
| **[!UICONTROL 해상도 (픽셀/인치)]** | 해상도 설정을 결정합니다. 이 설정은 파일에 인치당 표시되는 픽셀 수를 결정합니다. |
| **[!UICONTROL 색상 공간]** | ・ **[!UICONTROL 자동 감지]** - 파일의 색상 공간을 유지합니다.<br>・ **[!UICONTROL 강제 RGB]** - RGB 색상 공간으로 변환<br>・ **[!UICONTROL CMYK로 강제 적용]** - CMYK 색상 공간으로 변환<br>・ **[!UICONTROL 회색 음영으로 강제 적용]** - 회색 음영 색상 공간으로 변환 |

### Photoshop 탭 {#photoshop-tab}

Adobe® Photoshop® 파일에서 템플릿을 만들고, 레이어를 유지 관리하며, 레이어의 이름을 지정하는 방법을 지정하고, 텍스트를 추출하고, 이미지가 템플릿에 고정된 방식을 지정할 수 있습니다.

| Photoshop 옵션 | 설명 |
| --- | --- |
| **[!UICONTROL 레이어 유지]** | PSD의 레이어(있는 경우)를 개별 자산으로 이동합니다. 자산 레이어는 PSD과 계속 연결됩니다. [세부 사항 보기]에서 PSD 파일을 열고 레이어 패널을 선택하여 볼 수 있습니다. PSD 파일에서 레이어 보기 및 편집을 참조하십시오. |
| **[!UICONTROL 템플릿 만들기]** | PSD 파일의 레이어에서 템플릿을 만듭니다. |
| **[!UICONTROL 텍스트 추출]** | 사용자가 뷰어에서 텍스트를 검색할 수 있도록 텍스트를 추출합니다. |
| **[!UICONTROL 레이어를 배경 크기로 확장]** | 분리된 이미지 레이어의 크기를 배경 레이어의 크기로 확장합니다. |
| **[!UICONTROL 레이어 이름 지정]** | 분리된 이미지 레이어의 크기를 배경 레이어의 크기로 확장합니다.<br>・ **[!UICONTROL 레이어 이름]** - PSD 파일에서 레이어 이름 뒤에 이미지의 이름을 지정합니다. 예를 들어 원래 PSD 파일에서 가격 태그라는 레이어가 가격 태그라는 이미지가 됩니다. 그러나 PSD 파일의 레이어 이름이 기본 Photoshop 레이어 이름(배경, 레이어 1, 레이어 2 등)인 경우 해당 이미지의 이름은 PSD 파일의 레이어 번호 뒤에 지정됩니다. <br>・ **[!UICONTROL Photoshop 및 레이어 번호]** - 원본 레이어 이름을 무시하고 PSD 파일에서 레이어 번호 뒤에 이미지의 이름을 지정합니다. 이미지의 이름은 Photoshop 파일 이름과 추가된 레이어 번호로 지정됩니다. 예를 들어, `Spring Ad.psd` 이름이 지정됨 `Spring Ad_2` Photoshop에 기본값이 아닌 이름이 포함되어 있더라도<br>・ **[!UICONTROL Photoshop 및 레이어 이름]** - PSD 파일 뒤에 레이어 이름 또는 레이어 번호를 사용하여 이미지 이름을 지정합니다. PSD 파일의 레이어 이름이 기본 Photoshop 레이어 이름인 경우 레이어 번호가 사용됩니다. 예를 들어 이름이 인 레이어가 있습니다 `Price Tag` PSD 파일에서 `SpringAd` 이름이 지정됨 `Spring Ad_Price Tag`. 기본 이름이 레이어 2인 레이어를 라고 합니다 `Spring Ad_2`. |
| **[!UICONTROL 앵커]** | PSD 파일에서 생성된 계층화된 컴포지션에서 생성된 템플릿에 이미지가 고정되는 방식을 지정합니다. 기본적으로 앵커는 중심입니다. 가운데 앵커는 교체 이미지의 종횡비에 상관없이 교체 이미지가 동일한 공간을 가장 잘 채울 수 있도록 합니다. 템플릿을 참조하고 매개 변수 대체를 사용할 때 이 이미지를 대체하는 다른 측면을 가진 이미지가 동일한 공간을 효과적으로 차지합니다. 템플릿의 할당된 공간을 채우기 위해 응용 프로그램에 교체 이미지가 필요한 경우 다른 설정으로 변경합니다. |

### PDF 탭 {#pdf-tab}

파일을 래스터화하고, 검색어와 링크를 추출하고, 해상도를 설정하고, 색상 공간을 선택하도록 선택할 수 있습니다.

| PDF 옵션 | 설명 |
| --- | --- |
| **[!UICONTROL 처리 중]** | ・ **[!UICONTROL 없음]** - PDF 처리가 완료되지 않았습니다.<br>・ **[!UICONTROL 축소판]** - PDF 파일의 각 페이지를 잘라내어 축소판 이미지로 변환합니다.<br> ・ **[!UICONTROL 래스터화]** - PDF 파일의 페이지를 이동하고 벡터 그래픽을 비트맵 이미지로 변환합니다. eCatalog를 만들려면 이 옵션을 선택합니다. |
| **[!UICONTROL 추출]** | ・ **[!UICONTROL 없음]** - PDF에서 검색어 또는 링크가 추출되지 않습니다.<br>・ **[!UICONTROL 검색어]** - eCatalog 뷰어에서 키워드로 파일을 검색할 수 있도록 PDF 파일에서 검색어를 추출합니다.<br>・ **[!UICONTROL 링크]** - PDF 파일에서 링크를 추출하여 eCatalog 뷰어에서 사용되는 이미지 맵으로 변환합니다.<br>・ **[!UICONTROL 검색 단어 및 링크]** - eCatalog 뷰어에서 사용할 검색어와 링크를 모두 추출합니다. |
| **[!UICONTROL 해상도 (픽셀/인치)]** | 해상도 설정을 결정합니다. 이 설정은 PDF 파일에 인치당 표시되는 픽셀 수를 결정합니다. 기본값은 150입니다. |
| **[!UICONTROL 색상 공간]** | ・ **[!UICONTROL 자동 감지]** - PDF 파일의 색상 공간을 유지합니다.<br>・ **[!UICONTROL 강제 RGB]** - RGB 색상 공간으로 변환<br>・ **[!UICONTROL CMYK로 강제 적용]** - CMYK 색상 공간으로 변환<br>・ **[!UICONTROL 회색 음영으로 강제 적용]** - 회색 음영 색상 공간으로 변환 |

### Illustrator 탭 {#illustrator-tab}

Adobe Illustrator® 파일을 래스터화하고 투명한 배경을 유지하고 해상도를 선택한 다음 색상 공간을 선택할 수 있습니다.

Adobe Dynamic Media에서 Adobe® Illustrator®(AI) 파일을 사용할 수 있습니다. Adobe Dynamic Media은 이러한 파일을 업로드할 때 이러한 파일을 구성하는 명령을 제공합니다.

AI(Illustrator) 이미지 파일을 업로드할 때 다양한 방법으로 형식을 지정할 수 있습니다. 파일을 래스터화하고 투명한 배경을 유지하고 해상도를 선택한 다음 색상 공간을 선택할 수 있습니다. PostScript 및 Illustrator 파일 형식 옵션은 업로드 작업 옵션 상자의 포스트스크립트 옵션 및 Illustrator 옵션 아래의 업로드 화면에서 사용할 수 있습니다.


| Illustrator 옵션 | 설명 |
| --- | --- |
| **[!UICONTROL 처리 중]** | 파일의 벡터 그래픽을 비트맵 형식으로 변환하려면 [래스터화]를 선택합니다. |
| **[!UICONTROL 렌더링된 이미지의 투명 배경 유지]** | 파일의 배경 투명도를 유지합니다. |
| **[!UICONTROL 해상도 (픽셀/인치)]** | 해상도 설정을 결정합니다. 이 설정은 파일에 인치당 표시되는 픽셀 수를 결정합니다. |
| **[!UICONTROL 색상 공간]** | ・ **[!UICONTROL 자동 감지]** - 파일의 색상 공간을 유지합니다.<br>・ **[!UICONTROL 강제 RGB]** - RGB 색상 공간으로 변환<br>・ **[!UICONTROL CMYK로 강제 적용]** - CMYK 색상 공간으로 변환<br>・ **[!UICONTROL 회색 음영으로 강제 적용]** - 회색 음영 색상 공간으로 변환 |
