---
title: 이미지 서버에 대한 Dynamic Media 게시 설정 구성
description: Dynamic Media에서 게시를 설정하는 방법을 알아봅니다.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User, Admin
mini-toc-levels: 4
exl-id: c86e79c4-e887-4ee3-bb54-eeffb34a33c2
source-git-commit: 25fe5e240fd7404cb07375325e1f7b6a32923bfd
workflow-type: tm+mt
source-wordcount: '3494'
ht-degree: 3%

---

# 이미지 서버에 대한 Dynamic Media 게시 설정 구성

Dynamic Media 게시 설정 구성은 다음 경우에만 사용할 수 있습니다.

* Scene7 모드에서 Dynamic Media을 실행하고 있습니다. 자세한 내용은 [Scene7 모드에서 Dynamic Media 활성화](/help/assets/config-dms7.md#enabling-dynamic-media-in-scene-mode).
* 다음 항목이 있습니다. *기존* **[!UICONTROL Dynamic Media 구성]** (in) **[!UICONTROL Cloud Services]**)을 클릭하여 제품에서 사용할 수 있습니다. 자세한 내용은 [Cloud Services에서 Dynamic Media 구성 만들기](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services).
* 관리자 권한을 가진 Experience Manager 시스템 관리자입니다.

Dynamic Media 게시 설정 은 숙련된 웹 사이트 개발자와 프로그래머가 사용하기 위한 것입니다. Adobe Dynamic Media에서는 이러한 게시 설정을 변경하는 사용자가 Adobe Dynamic Media, HTTP 프로토콜 표준 및 규칙, 기본 이미징 기술에 익숙할 것을 권장합니다.

Dynamic Media 게시 설정 페이지에서는 Dynamic Media Adobe 서버에서 웹 사이트 또는 응용 프로그램으로 자산을 전달하는 방법을 결정하는 기본 설정을 설정합니다. 설정이 지정되지 않은 경우 Adobe Dynamic Media 서버는 Dynamic Media 게시 설정 페이지에 구성된 기본 설정에 따라 자산을 전달합니다.

참조 - [선택 사항 - Dynamic Media 설정 및 구성 - Scene7 모드 설정](/help/assets/config-dms7.md#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings) 추가 선택적 구성 작업

>[!NOTE]
>
>Adobe Experience Manager에서 Dynamic Media Classic으로 업그레이드하시겠습니까? 다음 [일반 설정](/help/assets/dm-general-settings.md) Dynamic Media의 페이지 및 게시 설정 페이지는 Dynamic Media Classic 계정에서 가져온 값으로 미리 채워집니다. 예외는 **[!UICONTROL 기본 업로드 옵션]** 일반 설정 페이지의 영역. 해당 값은 이미 Experience Manager에 있습니다. 따라서 사용자가 변경한 사항이 **[!UICONTROL 기본 업로드 옵션]**, 5개의 탭 중 Experience Manager 사용자 인터페이스를 통해 Dynamic Media Classic이 아닌 Dynamic Media에 반영됩니다. 의 기타 모든 설정 및 값 [일반 설정](/help/assets/dm-general-settings.md) 페이지와 게시 설정 페이지는 Experience Manager의 Dynamic Media Classic과 Dynamic Media 간에 유지됩니다.

**Dynamic Media 게시 설정 이미지 서버를 구성하려면:**

1. Experience Manager 작성자 모드에서 Experience Manager 로고를 선택하여 전역 탐색 콘솔에 액세스합니다.
1. 왼쪽 레일에서 도구 아이콘을 선택한 다음 **[!UICONTROL 자산]** > **[!UICONTROL Dynamic Media 게시 설정]**.
1. 이미지 서버 페이지에서 이미지 서버 - 게시 컨텍스트를 설정한 다음 5개의 탭을 사용하여 기본 게시 설정을 구성합니다.

   * [이미지 서버](#image-server)
   * [보안](#security-tab) 탭
   * [카탈로그 관리](#catalog-management-tab) 탭
   * [요청 속성](#request-attributes-tab) 탭
   * [공통 축소판 속성](#common-thumbnail-attributes-tab) 탭
   * [색상 관리 속성](#color-management-attributes-tab) 탭

   ![Dynamic Media 게시 설정 페이지](/help/assets/assets-dm/dm-publish-setup.png)
   *Dynamic Media 게시 설정 페이지,**[!UICONTROL 요청 속성]**탭 선택.*<br><br>

1. 완료되면 페이지의 오른쪽 위 모서리 근처에 있는 를 선택합니다. **[!UICONTROL 저장]**.

## 이미지 서버 {#image-server}

이미지 서버 페이지는 이미지 서버에서 이미지를 전달하는 기본 설정을 설정합니다. 설정은 5개의 카테고리에서 사용할 수 있습니다

| 컨텍스트 게시 | 설명 |
| --- | --- |
| 이미지 제공 | 게시 설정의 컨텍스트를 지정합니다. |
| 이미지 제공 테스트 | 게시 설정을 테스트할 컨텍스트를 지정합니다.<br>새 Dynamic Media 계정에만 적용되는 경우 기본값은 기본값입니다 **[!UICONTROL 클라이언트 주소]** 필드가 `127.0.0.1` 자동.<br>자세한 내용은 [자산을 공개하기 전에 테스트](#test-assets-before-making-public). |

### 보안 탭 {#security-tab}

**[!UICONTROL 클라이언트 주소]** - 하나 이상의 IP 주소 또는 IP 주소 범위를 지정할 수 있습니다. 지정하면 목록에 없는 IP 주소의 클라이언트에서 생성된 이 이미지 카탈로그에 대한 요청이 거부됩니다. 이 규칙은 이미지 전달과 렌더링된 이미지 모두에 적용됩니다.

![보안 탭&#x200B;](/help/assets/assets-dm/dm-ipallowlist.png)<br>*IP &quot;허용&quot; 필드를 표시하는 보안 탭입니다.*

### 카탈로그 관리 탭 {#catalog-management-tab}

**[!UICONTROL 규칙 세트 정의 파일 경로]** - 이미지 카탈로그에 대한 규칙 세트 정의를 포함하는 파일을 지정합니다.

참조 - [RuleSetFile](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-rulesetfile.html) 매개 변수( Dynamic Media 뷰어 참조 안내서)를 참조하십시오.

>[!NOTE]
>
>Dynamic Media Classic 계정에 이미 **[!UICONTROL 규칙 세트 정의 파일 경로]** 선택(아래에 설정된 대로) **[!UICONTROL 설정]** > **[!UICONTROL 애플리케이션]** > **[!UICONTROL 게시 설정]**, 아래에 **[!UICONTROL 카탈로그 관리]** 그룹), Experience Manager의 Dynamic Media 계정이 Dynamic Media Classic에서 파일을 가져옵니다. 그런 다음 파일을 열 때 파일이 저장되고 이 필드에서 사용할 수 있게 됩니다 **[!UICONTROL Dynamic Media 게시 설정]** 페이지를 처음 표시합니다.

### 요청 속성 탭 {#request-attributes-tab}

이러한 설정은 이미지의 기본 모양과 관련이 있습니다.

| 설정 | 설명 |
| --- | --- |
| **[!UICONTROL 응답 이미지 크기 제한]** | 필수.<br>새 Dynamic Media 계정만 사용하는 경우 기본 크기 제한이 자동으로 너비로 설정됩니다. `3000` 및 높이: `3000` 둘 다 **[!UICONTROL 이미지 제공]** 및 **[!UICONTROL 테스트 이미지 제공]**.<br>클라이언트에 반환되는 최대 회신 이미지 너비와 높이를 지정합니다. 요청 시 폭이나 높이 또는 둘 다 이 설정보다 큰 회신 이미지가 발생하면 서버에서 오류를 반환합니다.<br>참조 - [MaxPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-maxpix.html) 매개 변수( Dynamic Media 뷰어 참조 안내서)를 참조하십시오. |
| **[!UICONTROL 난독화 모드 요청]** | base64 인코딩이 유효한 요청에 적용되도록 하려면 활성화합니다.<br>참조 - [RequestObfusation](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-requestobfuscation.html) 매개 변수( Dynamic Media 뷰어 참조 안내서)를 참조하십시오. |
| **[!UICONTROL 잠금 모드 요청]** | 요청에 단순 해시 잠금이 포함되도록 하려면 활성화합니다.<br>참조 - [RequestLock](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-requestlock.html) 매개 변수( Dynamic Media 뷰어 참조 안내서)를 참조하십시오. |
| **[!UICONTROL 기본 요청 특성]** |  |
| **[!UICONTROL 기본 이미지 파일 접미사]** | 필수.<br>경로에 파일 접미사를 포함하지 않는 경우 카탈로그 경로 및 MaskPath 필드 값에 추가되는 기본 데이터 파일 확장입니다.<br>참조 - [DefaultExt](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultext.html) 매개 변수( Dynamic Media 뷰어 참조 안내서)를 참조하십시오. |
| **[!UICONTROL 기본 글꼴 이름]** | 텍스트 레이어 요청에서 글꼴을 제공하지 않을 경우 사용할 글꼴을 지정합니다. 지정하면 이 이미지 카탈로그의 글꼴 맵이나 기본 카탈로그의 글꼴 맵에 유효한 글꼴 이름 값이어야 합니다.<br>참조 - [DefaultFont](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultfont.html) 매개 변수( Dynamic Media 뷰어 참조 안내서)를 참조하십시오. |
| **[!UICONTROL 기본 이미지]** | 요청한 이미지를 찾을 수 없는 요청에 응답하여 반환할 기본 이미지를 제공합니다.<br>참조 - [DefaultImage](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-defaultimage.html) 매개 변수( Dynamic Media 뷰어 참조 안내서)를 참조하십시오.<br>**참고**: Dynamic Media Classic 계정에 이미 **[!UICONTROL 기본 이미지]** 선택(아래에 설정된 대로) **[!UICONTROL 설정]** > **[!UICONTROL 애플리케이션]** > **[!UICONTROL 게시 설정]**, 아래에 **[!UICONTROL 기본 요청 속성]** 그룹), Experience Manager의 Dynamic Media 계정이 Dynamic Media Classic에서 파일을 가져옵니다. 그런 다음 파일이 저장되고 을 열 때 이 필드에서 사용할 수 있게 됩니다 **[!UICONTROL Dynamic Media 게시 설정]** 페이지를 처음 표시합니다. |
| **[!UICONTROL 기본 이미지 모드]** | 슬라이더 상자(오른쪽 슬라이더)가 활성화되면 **[!UICONTROL 기본 이미지]** 소스 이미지에서 누락된 각 레이어를 기본 이미지로 바꾸고 컴포지션을 평소대로 반환합니다. 슬라이더 상자가 비활성화되면(왼쪽의 슬라이더) 누락된 이미지가 여러 레이어 중 하나에 불과하더라도 기본 이미지가 전체 합성 이미지를 대체합니다.<br>참조 - [DefaultImageMode](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultimagemode.html) 매개 변수( Dynamic Media 뷰어 참조 안내서)를 참조하십시오. |
| **[!UICONTROL 기본 보기 크기]** | 필수.<br>새 Dynamic Media 계정만 사용하는 경우 기본 보기 크기가 자동으로 너비로 설정됩니다. `1280` 및 높이: `1280` 둘 다 **[!UICONTROL 이미지 제공]** 및 **[!UICONTROL 테스트 이미지 제공]**.<br>요청이 을 사용하여 보기 크기를 명시적으로 지정하지 않는 경우 서버는 이 너비와 높이보다 크지 않은 회신 이미지를 제한합니다 `wid=`, `hei=`, 또는 `scl=`.<br>참조 - [DefaultPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultpix.html) 매개 변수( Dynamic Media 뷰어 참조 안내서)를 참조하십시오. |
| **[!UICONTROL 기본 썸네일 크기]** | 필수.<br>속성 대신 사용됩니다. **[!UICONTROL 기본 보기 크기]** 축소판 요청(`req=tmb`). 서버는 축소판 요청(`req=tmb`)에서 을 사용하여 크기를 명시적으로 지정하지 않습니다 `wid=`, `hei=`, 또는 `scl=`.<br>참조 - [DefaultThumbPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultthumbpix.html) 매개 변수( Dynamic Media 뷰어 참조 안내서)를 참조하십시오. |
| **[!UICONTROL 기본 배경색]** | 실제 이미지 데이터를 포함하지 않는 회신 이미지의 영역을 채우는 데 사용되는 RGB 값을 지정합니다.<br>참조 - [BkgColor](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-bkgcolor.html) 매개 변수( Dynamic Media 뷰어 참조 안내서)를 참조하십시오. |
| **[!UICONTROL JPEG 인코딩 특성]** |  |
| **[!UICONTROL 품질]** | <br>JPEG 회신 이미지의 기본 속성을 지정합니다.<br>새 Dynamic Media 계정에만 적용되는 경우, **[!UICONTROL 품질]** 기본값은 자동으로 `80` 둘 다 **[!UICONTROL 이미지 제공]** 및 **[!UICONTROL 테스트 이미지 제공]**.<br>이 필드는 1 - 100 범위에 정의됩니다.<br>참조 - [JpegQuality](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-jpegquality.html) 매개 변수( Dynamic Media 뷰어 참조 안내서)를 참조하십시오. |
| **[!UICONTROL 채도 다운샘플링]** | JPEG 인코더에 사용되는 색상 변색 다운샘플링을 활성화하거나 비활성화합니다. |
| **[!UICONTROL 기본 리샘플링 모드]** | 이미지 데이터 크기 조절에 사용할 기본 리샘플링 및 보간 속성을 지정합니다. 다음 경우에 사용 `resMode` 이 요청에 지정되지 않았습니다.<br>새 Dynamic Media 계정만 사용하는 경우 기본 재샘플링 모드가 자동으로 `Sharp2` 둘 다 **[!UICONTROL 이미지 제공]** 및 **[!UICONTROL 테스트 이미지 제공]**.<br>참조 - [ResMode](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-resmode.html) 매개 변수( Dynamic Media 뷰어 참조 안내서)를 참조하십시오. |

### 공통 축소판 속성 탭 {#common-thumbnail-attributes-tab}

이러한 설정은 축소판 이미지의 기본 모양과 정렬에 적용됩니다.

| 설정 | 설명 |
| --- | --- |
| **[!UICONTROL 썸네일용 기본 배경색]** | 실제 이미지 데이터가 포함되지 않은 출력 축소판 이미지의 영역을 채우는 데 사용되는 RGB 값을 지정합니다. 축소판 요청에만 사용됩니다(`req=tmb`) 및 **[!UICONTROL 기본 축소판 그림 유형]** 설정이 **[!UICONTROL Fit]** 또는 **[!UICONTROL 텍스처]**.<br>참조 - [ThumbBkgColor](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbbkgcolor.html) 매개 변수( Dynamic Media 뷰어 참조 안내서)를 참조하십시오. |
| **[!UICONTROL 수평 정렬]** | 지정된 회신 이미지 사각형에서 축소판 이미지의 가로 정렬을 지정합니다. `wid=` 및 `hei=` 값.<br>축소판 요청에만 사용됩니다(`req=tmb`) 및 **[!UICONTROL 기본 축소판 그림 유형]** 설정이 **[!UICONTROL Fit]**.<br>다음 세 가지 수평 정렬 중에서 선택할 수 있습니다. **[!UICONTROL 가운데 정렬]**, **[!UICONTROL 왼쪽 정렬]**, 및 **[!UICONTROL 오른쪽 정렬]**.<br>참조 - [ThumbHorizAlign](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbhorizalign.html) 매개 변수( Dynamic Media 뷰어 참조 안내서)를 참조하십시오. |
| **[!UICONTROL 수직 정렬]** | 지정된 회신 이미지 사각형에서 축소판 이미지의 세로 정렬을 지정합니다. `wid=` 및 `hei=` 값. 축소판 요청에만 사용됩니다(`req=tmb`) 및 **[!UICONTROL 기본 축소판 그림 유형]** 설정이 **[!UICONTROL Fit]**.<br>다음 세 가지 세로 정렬 중에서 선택할 수 있습니다. **[!UICONTROL 위쪽 정렬]**, **[!UICONTROL 가운데 정렬]**, 및 **[!UICONTROL 아래쪽 정렬]**.<br>참조 - [ThumbVertAlign](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbvertalign.html) 매개 변수( Dynamic Media 뷰어 참조 안내서)를 참조하십시오. |
| **[!UICONTROL 기본 캐시 사용 시간]** | 특정 카탈로그 레코드에 유효한 카탈로그 만료 값이 없는 경우 기본 만료 간격을 시간 단위로 제공합니다. 을 로 설정합니다. `-1` 만료되지 않은 것으로 표시합니다. <br>참조 - [만료](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-expiration.html) 매개 변수( Dynamic Media 뷰어 참조 안내서)를 참조하십시오. |
| **[!UICONTROL 기본 썸네일 유형]** | 특정 카탈로그 레코드에 올바른 카탈로그 ThumbType 값이 없는 경우 축소판 유형에 대한 기본값을 제공합니다. 축소판 요청에만 사용됩니다(`req=tmb`).<br>다음 세 가지 축소판 유형을 선택할 수 있습니다. **[!UICONTROL 자르기]**, **[!UICONTROL Fit]**, 및 **[!UICONTROL 텍스처]**.<br>참조 - [ThumbType](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbtype.html) 매개 변수( Dynamic Media 뷰어 참조 안내서)를 참조하십시오. |
| **[!UICONTROL 기본 썸네일 해상도]** | 특정 카탈로그 레코드에 유효한 카탈로그 ThumbRes 값이 없는 경우 축소판 개체 해상도의 기본값을 제공합니다. 축소판 요청에만 사용됩니다(`req=tmb`) 및 **[!UICONTROL 기본 축소판 그림 유형]** 설정이 **[!UICONTROL 텍스처]**.<br>참조 - [ThumbRes](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbres.html) 매개 변수( Dynamic Media 뷰어 참조 안내서)를 참조하십시오. |

### 색상 관리 속성 탭 {#color-management-attributes-tab}

이러한 설정은 이미지에 사용되는 ICC 색상 프로파일을 결정합니다.

**색상 변환 렌더링 의도**
색상 변환 렌더링 의도를 사용하면 작업 프로필의 기본 렌더링 의도를 재정의하여 소스 색상의 조정 방법을 결정할 수 있습니다. 다음 경우에 사용됩니다.

1. 기본 ICC 프로파일 중 하나는 색상 변환의 대상 색상 공간입니다.
1. 출력 장치(프린터 또는 모니터)는 이 프로파일을 나타냅니다.
1. 지정한 렌더링 의도가 이 프로필에 대해 유효합니다.

다른 렌더링 의도마다 소스 색상의 조정 방식을 결정하는 다양한 규칙이 사용됩니다.

참조 - [IccRenderIntent](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccrenderintent.html) 매개 변수( Dynamic Media 뷰어 참조 안내서)를 참조하십시오.

>[!NOTE]
>
>일반적으로 업계 표준을 충족하기 위해 Adobe에서 테스트한 선택한 색상 설정에 기본 렌더링 의도를 사용하는 것이 가장 좋습니다. 예를 들어, 북미 또는 유럽에 대한 색상 설정을 선택하는 경우 기본 색상 변환 렌더링 목적은 입니다 **[!UICONTROL 상대 색각]**. 일본에 대한 색상 설정을 선택하는 경우 기본 색상 변환 렌더링 의도는 다음과 같습니다 **[!UICONTROL 지각]**.

| 설정 | 특성 |
| --- | --- |
| **[!UICONTROL CMYK 기본 색상 공간]** | CMYK 데이터의 작업 프로필로 사용할 ICC 색상 프로파일의 이름을 지정합니다. If **[!UICONTROL 지정되지 않음]** 이 선택되면 CMYK 소스 이미지가 포함된 경우 이 이미지 카탈로그에 대해 색상 관리가 비활성화됩니다. 모든 CMYK 작업 영역은 장치에 종속됩니다. 즉, 실제 잉크 및 용지 조합을 기반으로 합니다. CMYK 작업 공간 Adobe 공급 장치는 표준 상용 인쇄 조건을 기반으로 합니다.<br> 참조 - [IccProfileCMYK](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilecmyk.html) 매개 변수( Dynamic Media 뷰어 참조 안내서)를 참조하십시오. |
| **[!UICONTROL 회색 음영 기본 색상 공간]** | 회색 스케일 데이터의 작업 프로필로 사용할 ICC 색상 프로파일의 이름을 지정합니다. If **[!UICONTROL 지정되지 않음]** 이 선택되면 회색 크기 소스 이미지가 포함된 경우 이 이미지 카탈로그에 대해 색상 관리를 사용할 수 없습니다.<br>참조 - [IccProfileGray](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilegray.html) 매개 변수( Dynamic Media 뷰어 참조 안내서)를 참조하십시오. |
| **[!UICONTROL RGB 기본 색상 공간]** | RGB 데이터의 작업 프로필로 사용할 ICC 색상 프로파일의 이름을 지정합니다. If **[!UICONTROL 지정되지 않음]** 을 선택하면 RGB 소스 이미지가 포함된 경우 이 이미지 카탈로그에 대해 색상 관리를 사용할 수 없습니다. 일반적으로 선택하는 것이 가장 좋습니다 **[!UICONTROL Adobe RGB]** 또는 **[!UICONTROL sRGB]**&#x200B;특정 장치(예: 모니터 프로필)에 대한 프로필이 아닌, **[!UICONTROL sRGB]** 웹 또는 모바일 장치용 이미지를 준비할 때는 웹 이미지를 보는 데 사용되는 표준 모니터의 색상 공간을 정의하므로 이 옵션을 사용하는 것이 좋습니다. **[!UICONTROL sRGB]** 또한 소비자 수준의 디지털 카메라의 이미지를 사용하여 작업할 때는 대부분의 카메라에서 sRGB를 기본 색상 공간으로 사용하기 때문에 유용합니다.<br>참조 - [IccProfileRBG](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilergb.html) 매개 변수( Dynamic Media 뷰어 참조 안내서)를 참조하십시오. |
| **[!UICONTROL 색상 변환 렌더링 의도]** | **[!UICONTROL 지각]** - 색상 값 자체가 바뀔 수 있어도 인간의 눈으로 자연으로 인식되도록 색상 간의 시각 관계를 유지하는 것을 목표로 합니다. 이 의도는 색상 영역 이외의 색상이 많은 사진 이미지에 적합합니다. 이 설정은 일본 인쇄 업계의 표준 렌더링 의도입니다. |
|  | **[!UICONTROL 상대 색각]** - 소스 색상 공간의 극단적 강조 표시를 대상 색상 공간의 강조 표시와 비교하고 그에 따라 모든 색상을 이동합니다. 색상 영역 밖의 색상은 대상 색상 공간에서 재현성이 가장 가까운 색상으로 바뀝니다. 상대 색상은 이미지의 원래 색상을 [지각]보다 더 많이 유지합니다. 이 설정은 북미 및 유럽에서 인쇄하기 위한 표준 렌더링 의도입니다. |
|  | **[!UICONTROL 채도]** - 색상 정확성을 희생하여 이미지에 선명한 색상을 생성하려고 합니다. 이 렌더링 의도는 그래프 또는 차트와 같은 비즈니스 그래픽에 적합하며, 색상 간의 정확한 관계보다 밝은 포화 색상이 더 중요합니다. |
|  | **[!UICONTROL 절대 색각]** - 대상 색상 영역 내에 있는 색상을 그대로 유지합니다. 색상 영역 외의 색상은 클리핑됩니다. 대상 흰색 점으로 색상 스케일링을 수행하지 않습니다. 이러한 목적은 색상 간의 관계를 보존하지 않고 색상 정확도를 유지하기 위한 것이며 특정 장치의 출력을 시뮬레이션하는 데 적합합니다. 이 의도는 종이 색상이 인쇄된 색상에 미치는 영향을 미리 보는 데 유용합니다. |

## 자산을 공개하기 전에 테스트 {#test-assets-before-making-public}

Secure Testing 을 사용하면 안전한 테스트 환경을 정의하고 구성 가능한 IP 주소 및 범위 세트를 기반으로 강력한 B2B 솔루션을 구축할 수 있습니다. 이 기능을 사용하면 Adobe Dynamic Media 배포를 컨텐츠 관리 및 비즈니스 시스템의 아키텍처와 일치시킬 수 있습니다.

보안 테스트를 통해 게시되지 않은 컨텐츠로 웹 사이트의 스테이징 버전을 미리 볼 수 있습니다.

원할 경우 다음과 같은 이유로 자산을 공개적으로 사용할 수 있도록 하지 않고 스테이징 환경을 만드십시오.

* 공개 실행 전(웹 사이트 스테이징) 웹 사이트를 미리 봅니다.
* B2B 웹 애플리케이션에 가격을 표시하는 eCatalogs와 같이 제한된 액세스가 필요한 자산을 제공합니다.
* 제품 정보 관리 시스템, 고객 서비스 애플리케이션, 교육 사이트 등의 일부로 방화벽 뒤에 자산을 사용합니다.

>[!NOTE]
>
>보안 테스트는 Adobe Dynamic Media Classic 액세스에 영향을 주지 않습니다. Adobe Dynamic Media Classic 보안은 일관되게 유지되며 Adobe Dynamic Media Classic 및 관련 웹 서비스에 액세스하기 위한 일반적인 자격 증명이 필요합니다.

### 보안 테스트 작동 방식 {#how-test-assets-works}

대부분의 기업들은 방화벽 뒤에 인터넷을 사용한다. 특정 경로를 통해 또는 일반적으로 제한된 범위의 공용 IP 주소를 통해 인터넷에 액세스할 수 있습니다.

기업 네트워크에서 다음과 같은 웹 사이트를 사용하여 공개 IP 주소를 파악할 수 있습니다 [https://www.whatismyip.com](https://www.whatismyip.com/) 또는 기업 IT 조직에서 이 정보를 요청합니다.

보안 테스트를 통해 Dynamic Media Adobe은 스테이징 환경 또는 내부 애플리케이션을 위한 전용 이미지 서버를 설정합니다. 이 서버에 대한 모든 요청은 원본 IP 주소를 확인합니다. 수신 요청이 승인된 IP 주소 목록에 없으면 오류 응답이 반환됩니다. Dynamic Media 회사 Adobe 관리자는 회사의 보안 테스트 환경에 대해 승인된 IP 주소 목록을 구성합니다.

원래 요청의 위치를 확인해야 하므로 Secure Testing 서비스의 트래픽이 공용 Dynamic Media Image Server 트래픽과 같은 컨텐츠 배포 네트워크를 통해 라우팅되지 않습니다. Secure Testing Service에 대한 요청은 공용 Dynamic Media 이미지 서버와 비교하여 약간 더 높은 지연을 갖습니다.

게시되지 않은 자산은 게시하지 않고도 Secure Testing Services에서 즉시 사용할 수 있습니다. 이러한 방식으로 자산이 공개 이미지 서버에 게시되기 전에 미리 보기를 실행할 수 있습니다.

>[!NOTE]
>
>Secure Testing Services는 내부 게시 컨텍스트에서 구성된 카탈로그 서버를 사용합니다. 따라서 회사가 Secure Testing에 게시하도록 구성되어 있는 경우, Adobe Dynamic Media의 업로드된 모든 자산을 Secure Testing 서비스에서 즉시 사용할 수 있게 됩니다. 이 기능은 자산이 업로드 시 게시하도록 표시되는지 여부에 관계없이 적용됩니다.

Secure Testing Services는 현재 다음과 같은 자산 유형 및 기능을 지원합니다.

* 이미지.
* 비네팅(서버 요청 렌더링).
* Render Server 요청(지원되지만 고객이 명시적으로 요청해야 함).
* 이미지 세트, eCatalog, render set 및 미디어 세트를 포함한 집합입니다.
* 표준 Adobe Dynamic Media 리치 미디어 뷰어입니다.
* Adobe Dynamic Media OnDemand JSP 페이지.
* PDF 파일 및 점진적으로 제공되는 비디오와 같은 정적 콘텐츠.
* HTTP 비디오 스트리밍.
* 점진적 비디오 스트리밍.

다음 자산 유형 및 기능은 현재 지원되지 않습니다.

* Adobe Dynamic Media Classic 정보 또는 eCatalog 검색
* RTMP 비디오 스트리밍
* Web-to-print
* UGC(사용자 생성 컨텐츠) 서비스

   >[!IMPORTANT]
   >
   >2023년 5월 1일부터 Dynamic Media의 UGC 자산은 업로드한 날부터 최대 60일 동안 사용할 수 있습니다. 60일 후 자산이 제거됩니다.

   >[!NOTE]
   >
   >Adobe Dynamic Media의 신규 또는 기존 UGC 벡터 이미지 자산에 대한 지원은 2021년 9월 30일에 종료되었습니다.

### Secure Testing 서비스 테스트 {#test-secure-testing-service}

Secure Testing 서비스가 예상대로 작동하는지 확인하려면 다음을 수행하십시오.

#### 계정 준비

1. Adobe 고객 지원 센터에 문의하여 계정에서 보안 테스트를 사용하도록 요청하십시오.
1. Adobe Experience Manager에서 **[!UICONTROL 도구]** > **[!UICONTROL 자산]** > **[!UICONTROL Dynamic Media 게시 설정]**.
1. 이미지 서버 페이지의 **[!UICONTROL 게시 컨텍스트]** 드롭다운 목록에서 **[!UICONTROL 테스트 이미지 제공]**.
1. 을(를) 선택합니다 **[!UICONTROL 보안]** 탭.
1. 대상 **[!UICONTROL 클라이언트 주소]** 필터, 선택 **[!UICONTROL 추가]**.
1. 에서 **[!UICONTROL IP 주소]** 필드에 IP 주소를 입력합니다.
1. 에서 **[!UICONTROL 마스크]** 필드에 네트 마스크를 입력합니다.

   >[!NOTE]
   >
   >두 개 이상의 IP 주소와 네트 마스크를 추가하면 *모두* 자산 호출을 위한 IP 주소 및 모든 가 표시됩니다.

1. 다음 중 하나를 수행하십시오.

   * IP 주소를 더 추가하려면 이전 3단계를 반복합니다.
   * 다음 단계로 진행합니다.

1. 이미지 서버 페이지의 오른쪽 위 모서리에서 을(를) 선택합니다 **[!UICONTROL 저장]**.
1. 원하는 이미지를 Adobe Dynamic Media 계정에 업로드합니다.

<!--    See [Upload files](uploading-files.md#uploading_files). -->

1. 일부 이미지가 게시용으로 표시되어 있고 다른 이미지가 표시되지 않았는지 확인한 다음 게시 작업을 제출하십시오.

<!--    See [Publish files](publishing-files.md#publishing_files). -->

1. 다음 위치로 이동하여 Secure Testing 서비스의 이름을 확인합니다. **[!UICONTROL 도구]** > **[!UICONTROL 자산]** > **[!UICONTROL Dynamic Media 일반 설정]**.
1. 설정 **[!UICONTROL 서버]** 페이지의 오른쪽에 있는 서버 이름을 찾습니다. **[!UICONTROL 게시된 서버 이름]**.

서버 이름이 없거나 서버 URL이 작동하지 않는 경우 Adobe 지원 센터에 문의하십시오.

#### 웹 사이트 변형 준비

게시된 자산과 게시 취소된 자산을 연결하는 웹 사이트의 두 가지 변형이 필요합니다.

* 공개 버전 - 기존 Adobe Dynamic Media URL 구문을 사용하여 자산을 연결합니다.
* 스테이징 버전 - 동일한 구문을 사용하지만 보안 테스트 사이트 이름과 함께 자산을 연결합니다.

#### 테스트 실행

다음 테스트를 수행합니다.

1. 회사 네트워크 내에서 자산이 표시되는지 확인합니다.

   이전에 정의한 IP 주소 범위로 식별된 회사 네트워크 내에서 웹 사이트의 스테이징 버전은 게시용으로 표시되었는지 여부에 관계없이 모든 이미지를 표시합니다. 따라서 미리 보기 승인 또는 제품 출시 전에 이미지를 실수로 사용할 수 있도록 만들지 않고 테스트할 수 있습니다.

   사이트의 공개 버전에 Adobe Dynamic Media에서 이전에 경험했듯이 게시된 자산이 표시되는지 확인합니다.

1. 회사 네트워크 외부에서 게시되지 않은 자산(즉, 게시용으로 표시되지 않은 자산)이 타사 액세스로부터 보호되는지 확인합니다.

   외부(예: 홈 컴퓨터 또는 4G/5G 연결)에서 네트워크에 액세스한 다음 사이트의 공개 버전에 게시된 모든 자산이 표시되지만 게시되지 않은 컨텐츠는 표시되지 않는지 확인합니다.

   승인되지 않은 IP 주소에서 Secure Testing 서비스에 액세스하고 있으므로 스테이징 버전에서 자산이 표시되지 않는지 확인합니다.
