---
title: 다이내믹 미디어의 비디오
description: Dynamic Media에서 비디오를 사용하여 작업하는 방법 학습
uuid: 97f311a3-a227-479a-91bf-fb54ecd1a55d
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 1103b849-0042-4e11-b170-38ee81dd0157
docset: aem65
translation-type: tm+mt
source-git-commit: 4333cfde433d00ddc4cb013b31fe52956791da46
workflow-type: tm+mt
source-wordcount: '11740'
ht-degree: 1%

---


# 다이내믹 미디어의 비디오 {#video}

이 섹션에서는 Dynamic Media에서 비디오를 사용한 작업에 대해 설명합니다.

## 빠른 시작:비디오 {#quick-start-videos}

다음 단계별 작업 과정 설명은 Dynamic Media의 응용 비디오 세트를 빠르게 시작하고 실행하는 데 도움이 되도록 설계되었습니다. 각 단계 후에는 자세한 정보를 찾을 수 있는 주제 제목이 상호 참조됩니다.

>[!NOTE]
>
>Dynamic Media에서 비디오를 사용하여 작업하기 전에 AEM 관리자가 Dynamic Media - Scene7 모드 또는 Dynamic Media - 하이브리드 모드에서 Dynamic Media Cloud Services을 이미 사용하고 구성했는지 확인하십시오.
>
>* Dynamic Media 구성 - Scene7 모드 및 [Dynamic Media 문제 해결 - Scene7 모드의 [Dynamic Media Cloud Services 구성](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services)을 참조하십시오.](/help/assets/troubleshoot-dms7.md)
   >
   >
* Dynamic Media 구성 - 하이브리드 모드에서 Dynamic Media Cloud Services 구성](/help/assets/config-dynamic.md#configuring-dynamic-media-cloud-services)을 참조하십시오.[

>



1. **다음을 수행하여 Dynamic Media** 비디오를 업로드합니다.

   * 고유한 비디오 인코딩 프로필을 만듭니다. 또는 Dynamic Media과 함께 제공되는 사전 정의된 _응용 비디오 인코딩_ 프로필을 사용하면 됩니다.

      * [비디오 인코딩 프로필 만들기](/help/assets/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming).
      * [비디오 인코딩 우수 사례](#best-practices-for-encoding-videos)에 대해 자세히 알아보십시오.
   * 기본 소스 비디오를 업로드할 하나 이상의 폴더에 비디오 처리 프로필을 연결합니다.

      * [폴더에 비디오 프로필 적용](/help/assets/video-profiles.md#applying-a-video-profile-to-folders).
      * 처리 프로필 사용](/help/assets/organize-assets.md)에 대한 디지털 자산을 구성하기 위한 모범 사례에 대해 자세히 알아보십시오.[
      * [디지털 자산 구성](/help/assets/organize-assets.md)에 대해 자세히 알아보십시오.
   * 기본 소스 비디오를 폴더에 업로드합니다. 각각 최대 15GB의 비디오 파일을 업로드할 수 있습니다. 폴더에 비디오를 추가하면 폴더에 할당된 비디오 처리 프로필에 따라 인코딩됩니다.

      * [비디오를 업로드합니다](/help/assets/managing-video-assets.md#upload-and-preview-video-assets).
      * [지원되는 입력 파일 형식](/help/assets/assets-formats.md#supported-multimedia-formats)에 대해 자세히 알아보십시오.
   * 에셋 또는 워크플로우 보기에서 [비디오 인코딩이 어떻게 진행되는지 모니터링합니다.](#monitoring-video-encoding-and-youtube-publishing-progress)




1. **다음 중** 하나를 수행하여 Dynamic Media 비디오를 관리합니다.

   * 비디오 에셋 구성, 검색 및 검색

      * [디지털 ](/help/assets/organize-assets.md)
자산 구성처리 프로필 사용을  [위한 디지털 자산을 구성하기 위한 모범 사례에 대한 자세한 내용](organize-assets.md)

      * [비디오 자산 ](search-assets.md#custompredicates) 검색 또는  [자산 검색](/help/assets/search-assets.md)
   * 비디오 에셋 미리 보기 및 게시

      * 관련 축소판과 함께 비디오의 소스 비디오 및 인코딩된 표현물을 봅니다.
         [비디오 ](managing-video-assets.md#upload-and-preview-video-assets) 미리 보기 또는  [자산 미리 보기](previewing-assets.md)
         [비디오 변환 보기](video-renditions.md)
         [비디오 변환 관리](manage-assets.md#managing-renditions)

      * [뷰어 사전 설정 관리](managing-viewer-presets.md)
      * [자산 게시](publishing-dynamicmedia-assets.md)
   * 비디오 메타데이터를 사용한 작업

      * 프레임 속도, 오디오 및 비디오 비트 전송률, 코덱과 같은 인코딩된 비디오 변환의 속성을 볼 수 있습니다.
         [비디오 변환 속성 보기](video-renditions.md)

      * 제목, 설명 및 태그, 사용자 정의 메타데이터 필드 등의 비디오 속성을 편집합니다.
         [비디오 속성 편집](manage-assets.md#editing-properties)

      * [디지털 자산에 대한 메타데이터 관리](metadata.md)
      * [메타데이터 스키마](metadata-schemas.md)
   * 비디오를 검토, 승인 및 주석을 달고 버전 제어 기능 유지

      * [비디오에 ](managing-video-assets.md#annotate-video-assets) 주석 달기 또는  [자산에 주석 달기](manage-assets.md#annotating)

      * [버전 만들기](manage-assets.md#asset-versioning)
      * [자산에 워크플로우 적용 ](assets-workflow.md) 또는 자산 [에서 워크플로우 시작을 참조하십시오.](manage-assets.md#starting-a-workflow-on-an-asset)

      * [폴더 에셋 검토](bulk-approval.md)
      * [프로젝트](../sites-authoring/projects.md)




1. **다음** 중 하나를 수행하여 Dynamic Media 비디오를 게시합니다.

   * 웹 컨텐츠 관리 시스템으로 Adobe Experience Manager을 사용하는 경우 웹 페이지에 직접 비디오를 추가할 수 있습니다.

      * [웹 페이지에 비디오 추가](adding-dynamic-media-assets-to-pages.md).
   * 타사 웹 컨텐츠 관리 시스템을 사용하는 경우 비디오를 웹 페이지에 링크하거나 포함할 수 있습니다.

      * URL을 사용하여 비디오 통합:
         [URL을 웹 애플리케이션에 연결](linking-urls-to-yourwebapplication.md).

      * 웹 페이지의 포함 코드를 사용하여 비디오 통합:
         [웹 페이지에 비디오 뷰어를 포함합니다](embed-code.md).
   * [YouTube에 비디오 게시를 참조하십시오](#publishing-videos-to-youtube).
   * [비디오 보고서](#viewing-video-reports) 생성

   * [비디오에 캡션 추가](#adding-captions-to-video).



## Dynamic Media {#working-with-video-in-dynamic-media}에서 비디오 작업

Dynamic Media의 비디오는 데스크탑, iOS, Android, Blackberry 및 Windows 모바일 디바이스를 비롯한 다양한 화면에서 스트리밍할 수 있는 고품질 적응형 비디오를 손쉽게 제작할 수 있는 엔드 투 엔드 솔루션입니다. 응용 비디오 세트는 다른 비트율 및 형식(예: 400kbps, 800kbps 및 1000kbps)으로 인코딩된 동일한 비디오 버전을 그룹화합니다. 데스크탑 컴퓨터 또는 모바일 장치에서 사용 가능한 대역폭을 감지합니다.

예를 들어 iOS 모바일 장치에서 3G, 4G 또는 Wi-Fi와 같은 대역폭을 감지합니다. 그런 다음 응용 비디오 집합 내의 다양한 비디오 비트 전송률 중에서 올바른 인코딩된 비디오를 자동으로 선택합니다. 비디오는 데스크톱, 모바일 장치 또는 태블릿으로 스트리밍됩니다.

또한 데스크탑 또는 모바일 디바이스에서 네트워크 상태가 변경되면 비디오 품질이 자동으로 동적으로 전환됩니다. 또한 고객이 데스크탑의 전체 화면 모드로 전환하면 응용 비디오 세트가 더 나은 해상도를 사용하여 응답하여 고객의 보기 환경을 개선합니다. 응용 비디오 세트를 사용하면 여러 화면 및 장치에서 Dynamic Media 비디오를 재생하는 고객에게 최상의 재생 방법을 제공합니다.

비디오 플레이어에서 재생할 인코딩된 비디오를 결정하거나 재생 중에 선택할 인코딩된 비디오를 결정하는 데 사용하는 로직은 다음 알고리즘을 기반으로 합니다.

1. 비디오 플레이어는 플레이어 자체에서 &quot;초기 비트 전송률&quot;에 설정된 값에 가장 가까운 비트 전송률을 기반으로 초기 비디오 조각을 로드합니다.
1. 다음 기준을 사용하여 대역폭 속도 변경 사항을 기반으로 비디오 플레이어를 전환합니다.

   1. 플레이어는 낮은 대역폭 스트림을 선택하거나 예상 대역폭과 동일한 높은 대역폭 스트림을 선택합니다.
   1. 플레이어는 사용 가능한 대역폭의 80%만 고려합니다. 그러나, 이 제품이 전환되고 있다면, 과대 평가하고 즉시 다시 되돌아가지 않도록 70%만이 더 보수적입니다.

알고리즘에 대한 자세한 기술 정보는 [https://android.googlesource.com/platform/frameworks/av/+/master/media/libstagefright/httplive/LiveSession.cpp](https://android.googlesource.com/platform/frameworks/av/+/master/media/libstagefright/httplive/LiveSession.cpp)을 참조하십시오.

단일 비디오 및 응용 비디오 세트를 관리하는 경우 다음 기능이 지원됩니다.

* 지원되는 다양한 비디오 포맷 및 오디오 포맷의 비디오를 업로드하고 여러 화면에서 재생할 수 있는 MP4 H.264 포맷으로 비디오를 인코딩할 수 있습니다. 사전 정의된 응용 비디오 사전 설정, 단일 비디오 인코딩 사전 설정을 사용하거나 자체 인코딩을 사용자 정의하여 비디오의 품질과 크기를 제어할 수 있습니다.

   * 응용 비디오 세트가 생성되면 MP4 비디오가 포함됩니다.
   * **참고**:응용 비디오 기본 집합에/소스 비디오가 추가되지 않습니다.

* 모든 HTML5 비디오 뷰어에서 비디오 캡션 지정
* 비디오 에셋을 효율적으로 관리할 수 있는 완벽한 메타데이터 지원을 통해 비디오를 구성, 검색 및 검색할 수 있습니다.
* 응용 비디오 세트를 웹뿐만 아니라 iPhone, iPad, Android, Blackberry 및 Windows 폰을 비롯한 데스크톱 및 모바일 장치에 제공합니다.

적응형 비디오 스트리밍은 다양한 iOS 플랫폼에서 지원됩니다. [Dynamic Media 뷰어 참조 안내서](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/c-html5-video-reference.html#video)를 참조하십시오.

Dynamic Media은 MP4 H.264 비디오에 대한 모바일 비디오 재생을 지원합니다. 다음 위치에서 이 비디오 형식을 지원하는 Blackberry 장치를 찾을 수 있습니다.[Blackberry](https://support.blackberry.com/kb/articleDetail?ArticleNumber=000005482)에서 지원되는 비디오 형식.

다음 위치에서 이 비디오 형식을 지원하는 Windows 장치를 찾을 수 있습니다.[Windows Phone에서 지원되는 비디오 형식](https://msdn.microsoft.com/library/windows/apps/ff462087%28v=vs.105%29.aspx)

* 다음을 포함한 Dynamic Media 비디오 뷰어 사전 설정을 사용하여 비디오를 재생합니다.

   * 단일 비디오 뷰어.
   * 비디오와 이미지 컨텐츠를 모두 결합하는 혼합 미디어 뷰어.

* 브랜딩 요구 사항에 맞게 비디오 플레이어를 구성할 수 있습니다.
* 간단한 URL 또는 포함 코드를 사용하여 웹 사이트, 모바일 사이트 또는 모바일 애플리케이션에 비디오를 통합할 수 있습니다.

<!-- See [Dynamic video playback](https://s7d9.scene7.com/s7/uvideo.jsp?asset=GeoRetail/Mop_AVS&config=GeoRetail/Universal_Video1&stageSize=640,480) sample. -->

AEM Assets 및 Dynamic Media Classic용 [뷰어](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/c-html5-s7-aem-asset-viewers.html#viewers-aem-assets-dmc) 및 AEM 에셋에만 대한 [뷰어를 참조하십시오](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/c-html5-aem-asset-viewers.html#viewers-for-aem-assets-only).

## 모범 사례:HTML5 비디오 뷰어 사용 {#best-practice-using-the-html-video-viewer}

Dynamic Media HTML5 비디오 뷰어 사전 설정은 강력한 비디오 플레이어입니다. 적응형 스트리밍 전달 부족, 데스크탑 브라우저 전달 범위 제한과 같은 모바일 디바이스와 관련된 HTML5 비디오 재생과 관련된 많은 일반적인 문제를 방지하는 데 이러한 효과를 사용할 수 있습니다.

플레이어의 디자인 측면에서는 표준 웹 개발 도구를 사용하여 비디오 플레이어의 모든 기능을 디자인할 수 있습니다. 예를 들어 HTML5 및 CSS를 사용하여 버튼, 컨트롤 및 사용자 정의 포스터 이미지 배경을 디자인하여 원하는 모양으로 고객에게 다가갈 수 있습니다.

뷰어의 재생 측에서 브라우저의 비디오 기능을 자동으로 감지합니다. 응용 비디오 스트리밍이라고도 하는 HLS(HTTP Live Streaming)를 사용하여 비디오를 제공합니다. 또는 이러한 전달 방법이 없으면 HTML5 점진적 기능이 대신 사용됩니다.

HTML5 및 CSS를 사용하여 재생 구성 요소를 디자인하고 내장된 재생을 제공하며 브라우저 기능에 따라 적응형 및 점진적 스트리밍을 사용하는 기능을 단일 플레이어로 통합함으로써 리치 미디어 컨텐츠의 범위를 데스크탑 및 모바일 사용자 모두로 확대하고 간소화된 비디오 경험을 제공할 수 있습니다.

[HTML5 뷰어 정보](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/c-html5-aem-asset-viewers.html#viewers-for-aem-assets-only)도 참조하십시오.

### HTML5 비디오 뷰어 {#playback-of-video-on-desktop-computers-and-mobile-devices-using-the-html-video-viewer}를 사용하여 데스크톱 컴퓨터와 모바일 장치에서 비디오 재생

데스크탑 및 모바일 적응형 비디오 스트리밍의 경우 비트 전송률 전환에 사용되는 비디오는 적응형 비디오 세트의 모든 MP4 비디오를 기반으로 합니다.

비디오 재생은 HLS 또는 점진적 비디오 다운로드를 사용하여 수행됩니다. 6.0, 6.1 및 6.2와 같은 이전 버전의 AEM에서는 비디오가 HTTP를 통해 스트리밍되었습니다.

그러나 AEM 6.3 이상에서 비디오는 이제 HTTPS(즉, HLS)를 통해 스트리밍됩니다. DM 게이트웨이 서비스 URL은 항상 HTTPS를 사용하기 때문입니다. 이 기본 동작에는 고객에게 영향을 주지 않습니다. 즉, 브라우저에서 지원되지 않는 한 비디오 스트리밍은 항상 HTTPS를 통해 발생합니다. (다음 표 참조). 따라서

* HTTPS 비디오 스트리밍이 있는 HTTPS 웹 사이트를 사용하는 경우 스트리밍이 좋습니다.
* HTTPS 비디오 스트리밍이 있는 HTTP 웹 사이트가 있는 경우 스트리밍은 양호하며 웹 브라우저에서 혼합 컨텐츠 문제가 발생하지 않습니다.

HLS는 네트워크 대역폭 용량에 따라 재생을 자동으로 조정하는 응용 비디오 스트리밍을 위한 Apple 표준입니다. 또한 고객이 비디오의 나머지 부분 다운로드를 기다릴 필요 없이 비디오의 모든 부분을 &quot;검색&quot;할 수 있습니다.

점진적 비디오는 사용자의 데스크탑 시스템 또는 모바일 장치에 로컬로 비디오를 다운로드 및 저장하여 전달됩니다.

다음 표에서는 Dynamic Media Video Viewer를 사용하는 데스크톱 컴퓨터와 모바일 장치에서 비디오의 장치, 브라우저 및 재생 방법에 대해 설명합니다.

<table>
 <tbody>
  <tr>
   <td><strong>장치</strong></td>
   <td><strong>브라우저</strong></td>
   <td><strong>비디오 재생 모드</strong></td>
  </tr>
  <tr>
   <td>데스크톱</td>
   <td>Internet Explorer 9 및 10</td>
   <td>점진적 다운로드.</td>
  </tr>
  <tr>
   <td>데스크톱</td>
   <td>Internet Explorer 11+</td>
   <td>Windows 8 및 Windows 10의 경우 - HLS가 요청될 때마다 HTTPS를 강제로 사용하십시오. 알려진 제한 사항:HLS의 HTTP는 이 브라우저/운영 체제 조합<br /> <br /> Windows 7의 경우 - 점진적 다운로드에서 작동하지 않습니다. HTTP와 HTTPS 프로토콜을 선택할 때 표준 로직을 사용합니다.</td>
  </tr>
  <tr>
   <td>데스크톱</td>
   <td>Firefox 23-44</td>
   <td>점진적 다운로드.</td>
  </tr>
  <tr>
   <td>데스크톱</td>
   <td>Firefox 45 이상</td>
   <td>HLS</td>
  </tr>
  <tr>
   <td>데스크톱</td>
   <td>Chrome</td>
   <td>HLS</td>
  </tr>
  <tr>
   <td>데스크톱</td>
   <td>Safari(Mac)</td>
   <td>HLS</td>
  </tr>
  <tr>
   <td>모바일</td>
   <td>Chrome(Android 6 또는 이전 버전)</td>
   <td>점진적 다운로드.</td>
  </tr>
  <tr>
   <td>모바일</td>
   <td>Chrome(Android 7 이상)</td>
   <td>HLS</td>
  </tr>
  <tr>
   <td>모바일</td>
   <td>Android(기본 브라우저)</td>
   <td>점진적 다운로드.</td>
  </tr>
  <tr>
   <td>모바일</td>
   <td>Safari(iOS)</td>
   <td>HLS</td>
  </tr>
  <tr>
   <td>모바일</td>
   <td>Chrome(iOS)</td>
   <td>HLS</td>
  </tr>
  <tr>
   <td>모바일</td>
   <td>Blackberry</td>
   <td>HLS</td>
  </tr>
 </tbody>
</table>

## Dynamic Media 비디오 솔루션 아키텍처 {#architecture-of-dynamic-media-video-solution}

다음 그래픽은 DMGateway(Dynamic Media 하이브리드 모드)를 통해 업로드 및 인코딩되고 공개 소비에 사용할 수 있는 비디오의 전체 제작 워크플로우를 보여줍니다.

![chlimage_1-427](assets/chlimage_1-427.png)

## 비디오 {#hybrid-publishing-architecture-for-videos} 하이브리드 게시 아키텍처

![chlimage_1-428](assets/chlimage_1-428.png)

## 비디오 인코딩 우수 사례 {#best-practices-for-encoding-videos}

동적 미디어를 활성화하고 비디오 클라우드 서비스를 설정한 경우 **Dynamic Media 비디오 인코딩** 워크플로우는 비디오를 인코딩합니다. 이 워크플로우는 워크플로우 프로세스 내역 및 실패 정보를 캡처합니다. [비디오 인코딩 및 YouTube 게시 진행 모니터링](#monitoring-video-encoding-and-youtube-publishing-progress)을 참조하십시오. 다이내믹 미디어를 활성화하고 비디오 클라우드 서비스를 설정한 경우 비디오를 업로드할 때 **[!UICONTROL Dynamic Media 비디오 인코딩]** 워크플로우가 자동으로 적용됩니다. 동적 미디어를 사용하지 않는 경우 **[!UICONTROL DAM 자산 업데이트]** 워크플로우가 적용됩니다.

다음은 소스 비디오 파일을 인코딩하기 위한 우수 사례 팁입니다.

비디오 인코딩에 대한 자세한 내용은 다음을 참조하십시오.

* [스트리밍 101:기본 사항 — 코덱스, 대역폭, 데이터 비율 및 해상도](https://www.adobe.com/go/learn_s7_streaming101_en).
* [비디오 인코딩 기본](https://www.adobe.com/go/learn_s7_encoding_en) 사항.

### 소스 비디오 파일 {#source-video-files}

비디오 파일을 인코딩할 때는 최상의 품질을 제공하는 소스 비디오 파일을 사용합니다. 이러한 파일은 이미 압축되어 있으므로 이전에 인코딩된 비디오 파일을 사용하지 마십시오. 추가로 인코딩하면 하위 품질의 비디오가 만들어집니다.

다음 표는 소스 비디오 파일을 인코딩하기 전에 사용해야 하는 권장 크기, 종횡비 및 최소 비트 전송률에 대해 설명합니다.

| 크기 | 종횡비 | 최소 비트 전송률 |
|--- |--- |--- |
| 1024 X 768 | 4:3 | 대부분의 비디오에 대해 4500kbps. |
| 1280 X 720 | 16:9 | 3000 - 6000kbps(비디오의 동작 양에 따라 다름) |
| 1920 X 1080 | 16:9 | 6000 - 8000kbps(비디오의 동작 양에 따라 다름) |

### 파일의 메타데이터 {#obtaining-a-file-s-metadata} 얻기

비디오 편집 도구를 사용하거나 메타데이터를 얻기 위해 디자인된 응용 프로그램을 사용하여 파일의 메타데이터를 볼 수 있습니다. 다음은 제3자 응용 프로그램인 MediaInfo를 사용하여 비디오 파일의 메타데이터를 가져오는 방법에 대한 지침입니다.

1. 이 웹 페이지로 이동:[https://mediainfo.sourceforge.net/en/Download](https://mediainfo.sourceforge.net/en/Download).
1. GUI 버전용 설치 프로그램을 선택하여 다운로드하고 설치 지침을 따릅니다.
1. 설치 후 비디오 파일(Windows 전용)을 마우스 오른쪽 단추로 클릭하고 MediaInfo를 선택하거나 MediaInfo를 열고 비디오 파일을 응용 프로그램으로 드래그합니다. 폭, 높이, fps 등 비디오 파일과 연관된 모든 메타데이터가 표시됩니다.

### 종횡비 {#aspect-ratio}

기본 소스 비디오 파일에 대한 비디오 인코딩 사전 설정을 선택하거나 만들 때는 사전 설정이 기본 소스 비디오 파일과 동일한 종횡비를 가지고 있는지 확인합니다. 종횡비는 비디오의 높이에 대한 폭입니다.

비디오 파일의 종횡비를 결정하려면 파일의 메타데이터를 가져와 파일의 폭과 높이를 확인합니다(위의 파일 메타데이터 얻기를 참조하십시오). 다음 공식을 사용하여 종횡비를 결정하십시오.

너비/높이 = 종횡비

다음 표에서는 공식 결과가 일반적인 종횡비 선택 사항으로 변환되는 방법을 설명합니다.

| 공식 결과 | 종횡비 |
|--- |--- |
| 1.33 | 4:3 |
| 0.75 | 3:4 |
| 1.78 | 16:9 |
| 0.56 | 9:16 |

예를 들어 1440 너비 x 1080 높이의 비디오의 종횡비는 1440/1080 또는 1.33입니다. 이 경우 비디오 파일을 인코딩하기 위해 4:3 종횡비로 비디오 인코딩 사전 설정을 선택합니다.

### 비트율 {#bitrate}

비트 전송률은 비디오 재생 1초를 구성하기 위해 인코딩된 데이터의 양입니다. 비트 전송률은 초당 킬로비트(Kbps)로 측정됩니다.

>[!NOTE]
>
>모든 코덱은 손실 압축을 사용하기 때문에 비트 전송률이 비디오 품질에서 가장 중요한 요소입니다. 손실 압축을 사용하면 비디오 파일을 압축할수록 품질이 더 낮아집니다. 이러한 이유로 다른 모든 특성(해상도, 프레임 속도 및 코덱은)이 동일하며 비트 전송률이 낮을수록 압축된 파일의 품질이 낮아집니다.

비트 전송률 인코딩을 선택할 때 다음 두 가지 유형을 선택할 수 있습니다.

* **[!UICONTROL 상수 비트 전송률 인코딩]** (CBR) - CBR 인코딩 시 인코딩 과정 동안 비트 전송률 또는 초당 비트 수가 동일하게 유지됩니다. CBR 인코딩은 전체 비디오에 대한 설정 데이터 속도를 유지합니다. 또한 CBR 인코딩은 품질로 미디어 파일을 최적화하지는 않지만 저장 공간에 저장할 수 있습니다.
비디오 전체에 걸쳐 비슷한 모션 레벨이 포함된 비디오의 경우 CBR을 사용합니다. CBR은 비디오 컨텐츠를 스트리밍하는 데 가장 일반적으로 사용됩니다. [사용자 정의 추가 비디오 인코딩 매개 변수 사용](/help/assets/video-profiles.md#using-custom-added-video-encoding-parameters)을 참조하십시오.

* **[!UICONTROL 가변 비트 전송률 인코딩]** (VBR) - VBR 인코딩은 압축기에 필요한 데이터를 기반으로 데이터 속도를 낮추고 사용자가 설정한 상한으로 조정합니다. 즉, VBR 인코딩 과정 중에 미디어 파일의 비트 전송률이 미디어 파일 비트 전송률에 따라 동적으로 증가하거나 감소합니다.
VBR은 인코딩하는 데 시간이 오래 걸리지만 가장 유리한 결과를 얻을 수 있습니다.미디어 파일의 품질이 우수합니다. VBR은 비디오 컨텐츠의 http 점진적 전달에 가장 일반적으로 사용됩니다.

VBR과 CRB는 언제 사용해야 합니까?
VBR 대 CBR을 선택하는 경우에는 미디어 파일에 VBR을 사용하는 것이 좋습니다. VBR은 경쟁력 있는 비트 전송률로 고품질의 파일을 제공합니다. VBR을 사용하는 경우 2패스 인코딩을 사용하고 최대 비트 전송률을 대상 비디오 비트 전송률의 1.5배로 설정합니다.

비디오 인코딩 사전 설정을 선택하는 경우 대상 최종 사용자의 연결 속도를 고려합니다. 해당 속도의 80%인 데이터 속도의 사전 설정을 선택합니다. 예를 들어 대상 최종 사용자의 연결 속도가 1000Kbps인 경우 최상의 사전 설정은 비디오 데이터 속도가 800Kbps인 사전 설정입니다.

이 표에서는 일반적인 연결 속도의 데이터 속도를 설명합니다.

| 속도(Kbps) | 연결 유형 |
|--- |--- |
| 256년 | 전화 접속 연결. |
| 800 | 일반적인 모바일 연결. 이 연결의 경우 3G 경험에 대해 400 ~ 최대 800 범위의 데이터 전송률을 타깃팅합니다. |
| 2000년 | 일반적인 광대역 데스크탑 연결. 이 연결의 경우 대부분의 대상이 평균 1200-1500Kbps인 800-2000Kbps 범위의 데이터 전송률을 타깃팅합니다. |
| 5000 | 일반 고광대역 연결. 대부분의 소비자는 이 속도로 비디오를 전달할 수 없으므로 이 상한 범위의 인코딩을 권장하지 않습니다. |

### 해상도 {#resolution}

**Resolution ** 비디오 파일의 높이 및 너비(픽셀 단위)를 설명합니다. 대부분의 소스 비디오는 고해상도(예: 1920 x 1080)에 저장됩니다. 스트리밍을 위해 소스 비디오는 더 작은 해상도(640 x 480 이하)로 압축됩니다.

해상도와 데이터 전송률은 비디오 품질을 결정하는 두 가지 통합 연결 요소입니다. 동일한 비디오 품질을 유지하려면 비디오 파일의 픽셀 수가 많을수록 해상도가 높아지므로 데이터 속도는 높아야 합니다. 예를 들어 320 x 240 해상도의 프레임당 픽셀 수와 640 x 480 해상도 비디오 파일을 생각해 보십시오.

| 해상도 | 프레임당 픽셀 수 |
|--- |--- |
| 320 x 240 | 76,800 |
| 640 x 480 | 307,200 |

640 x 480 파일은 프레임당 4배 더 많은 픽셀을 가집니다. 이러한 두 가지 예제 해상도에 대해 동일한 데이터 속도를 얻으려면 640 x 480 파일에 압축의 4배를 적용하여 비디오 품질을 줄일 수 있습니다. 따라서 비디오 데이터 속도인 250Kbps를 사용하면 320 x 240 해상도로 고음질의 보기를 만들 수 있지만 640 x 480 해상도는 아닙니다.

일반적으로 데이터 속도가 빠를수록 비디오가 좋아지며 해상도가 높을수록 보기 품질을 유지하는 데 필요한 데이터 비율이 높아집니다(해상도가 낮을수록).

해상도와 데이터 전송률이 연결되어 있으므로 비디오를 인코딩할 때 두 가지 옵션이 있습니다.

* 데이터 전송률을 선택한 다음 선택한 데이터 전송률에 맞는 최고 해상도로 인코딩할 수 있습니다.
* 해상도를 선택한 다음 선택한 해상도에서 고품질 비디오를 얻는 데 필요한 데이터 속도로 인코딩합니다.

기본 소스 비디오 파일에 대한 비디오 인코딩 사전 설정을 선택하거나 만들 때 이 표를 사용하여 올바른 해상도를 타게팅합니다.

| 해상도 | 높이(픽셀) | 화면 크기 |
|--- |--- |--- |
| 240p | 240년 | 작은 화면 |
| 300p | 300 | 일반적으로 모바일 장치용 작은 화면 |
| 360p | 360 | 작은 화면 |
| 480p | 480 | 중간 화면 |
| 720p | 720년 | 대형 화면 |
| 1080p | 1080년 | HD 대형 화면 |

### Fps(초당 프레임 수) {#fps-frames-per-second}

미국 및 일본에서는 대부분의 비디오가 29.97fps로 촬영됩니다.유럽에서 대부분의 비디오는 25fps로 촬영됩니다. 영화는 24fps로 촬영됩니다.

기본 소스 비디오 파일의 fps 속도와 일치하는 비디오 인코딩 사전 설정을 선택합니다. 예를 들어 기본 소스 비디오가 25fps인 경우 25fps의 인코딩 사전 설정을 선택합니다. 기본적으로 모든 사용자 정의 인코딩은 기본 소스 비디오 파일의 fps를 사용합니다. 따라서 비디오 인코딩 사전 설정을 만들 때 fps 설정을 명시적으로 지정할 필요가 없습니다.

### 비디오 인코딩 차원 {#video-encoding-dimensions}

최적의 결과를 얻으려면 소스 비디오가 인코딩된 모든 비디오의 전체 배수인 인코딩 크기를 선택합니다.

이 비율을 계산하려면 소스 너비를 인코딩된 너비로 나누어 너비 비율을 얻습니다. 그런 다음 소스 높이를 인코딩된 높이로 나누어 높이 비율을 얻습니다.

결과 비율이 정수 단위인 경우 비디오가 최적으로 조절됨을 의미합니다. 결과 비율이 정수가 아닌 경우, 화면에 남아 있는 픽셀 가공물을 남겨 두면 비디오 품질에 영향을 줍니다. 이 효과는 비디오에 텍스트가 있을 때 가장 잘 나타납니다.

예를 들어 소스 비디오가 1920 x 1080이라고 가정합니다. 다음 표에서 3개의 인코딩된 비디오는 사용할 최적의 인코딩 설정을 제공합니다.

| 비디오 유형 | 너비 x 높이 | 폭 비율 | 높이 비율 |
|--- |--- |--- |--- |
| 소스 | 1920x1080 | 1 | 3 |
| 인코딩됨 | 960 x 540 | 2 | 2 |
| 인코딩됨 | 640 x 360 | 3 | 3 |
| 인코딩됨 | 480 x 270 | 4 | 4 |

### 인코딩된 비디오 파일 형식 {#encoded-video-file-format}

Dynamic Media에서는 MP4 H.264 비디오 인코딩 사전 설정을 사용하는 것이 좋습니다. MP4 파일은 H.264 비디오 코덱을 사용하기 때문에 고품질 비디오를 제공하지만 압축된 파일 크기로 제공합니다.

## YouTube {#publishing-videos-to-youtube}에 비디오 게시

사내 AEM 비디오 자산을 이전에 만든 YouTube 채널에 직접 게시할 수 있습니다.

비디오 자산을 YouTube에 게시하려면 태그가 있는 AEM Assets을 설정합니다. 이러한 태그를 YouTube 채널과 연결합니다. 비디오 자산의 태그가 YouTube 채널의 태그와 일치하는 경우 비디오가 YouTube에 게시됩니다. YouTube에 게시는 연결된 태그가 사용되는 한 정상적인 비디오 게시와 함께 발생합니다.

YouTube는 자체 인코딩을 수행합니다. 따라서 AEM에 업로드된 원본 비디오 파일은 Dynamic Media의 인코딩이 만들어진 비디오 변환 대신 YouTube에 게시됩니다. Dynamic Media을 사용하여 비디오를 처리할 필요는 없지만 재생에 뷰어 사전 설정이 필요한 경우 비디오를 처리할 필요가 있습니다.

비디오 처리 프로필을 무시하고 YouTube에 직접 게시하는 경우 간단히 AEM Asset의 비디오 에셋에 볼 수 있는 축소판이 없을 수 있습니다. 또한 다이내믹 미디어 또는 dynamicmedia_scene7 실행 모드에서 실행되는 경우 인코딩되지 않은 비디오는 Dynamic Media 에셋 유형에서 작동하지 않습니다.

YouTube 서버에 비디오 에셋을 게시하려면 YouTube를 통해 안전하고 보안이 적용된 서버 간 인증을 보장하기 위해 다음 작업을 완료해야 합니다.

1. [Google 클라우드 설정 구성](#configuring-google-cloud-settings)
1. [YouTube 채널 만들기](#creating-a-youtube-channel)
1. [게시용 태그 추가](#adding-tags-for-publishing)
1. [YouTube 게시 복제 에이전트 활성화](#enabling-the-youtube-publish-replication-agent)
1. [AEM에서 YouTube 설정](#setting-up-youtube-in-aem)
1. [(선택 사항) 업로드된 비디오에 대한 기본 YouTube 속성 설정을 자동화합니다.](#optional-automating-the-setting-of-default-youtube-properties-for-your-uploaded-videos)
1. [YouTube 채널에 비디오 게시](#publishing-videos-to-your-youtube-channel)
1. [(선택 사항) 게시된 비디오를 YouTube에서 확인](/help/assets/video.md#optional-verifying-the-published-video-on-youtube)
1. [YouTube URL을 웹 응용 프로그램에 연결](#linking-youtube-urls-to-your-web-application)

[비디오를 게시 취소하여 YouTube](#unpublishing-videos-to-remove-them-from-youtube)에서 제거할 수도 있습니다.

### Google 클라우드 설정 구성 중 {#configuring-google-cloud-settings}

YouTube에 게시하려면 Google 계정이 필요합니다. GMAIL 계정이 있는 경우 이미 Google 계정을 가지고 있습니다.Google 계정이 없는 경우 계정을 쉽게 만들 수 있습니다. YouTube에 비디오 자산을 게시하려면 자격 증명이 필요하므로 계정이 필요합니다. 이미 만든 계정이 있는 경우 이 작업을 건너뛰고 [Creating a YouTube 채널](#creating-a-youtube-channel)으로 바로 진행합니다.

Google Cloud와 YouTube에 사용되는 Google 계정과 같은 계정이 같을 필요는 없습니다.

Google은 사용자 인터페이스를 주기적으로 변경합니다. 따라서 비디오를 YouTube에 게시하는 단계는 아래 문서화된 것과 약간 다를 수 있습니다. 이 경고는 비디오가 업로드되었는지 확인하려고 할 때 YouTube에도 적용됩니다.

>[!NOTE]
>
>다음 단계는 이 글을 쓸 때 정확했다. 하지만 Google은 사전 통지 없이 정기적으로 웹 사이트를 업데이트합니다. 따라서 이러한 단계는 약간 다를 수 있습니다.

Google 클라우드 설정을 구성하려면:

1. 새 Google 계정을 만듭니다.
   [https://accounts.google.com/SignUp?service=mail](https://accounts.google.com/SignUp?service=mail)

   이미 Google 계정이 있는 경우 다음 단계로 건너뜁니다.

1. [https://cloud.google.com/](https://cloud.google.com/)로 이동합니다.
1. 오른쪽 위 모서리 근처에 있는 Google Cloud 페이지에서 **[!UICONTROL 콘솔을 클릭합니다.]**

   필요한 경우 **[!UICONTROL 콘솔]** 옵션을 보려면 Google 계정 자격 증명을 사용하여 **[!UICONTROL 에 로그인해야 할 수 있습니다.]**

1. 대시보드 페이지의 **[!UICONTROL Google 클라우드 플랫폼]** 오른쪽에 있는 프로젝트 드롭다운 목록을 클릭하여 프로젝트 선택 대화 상자를 엽니다.
1. 프로젝트 선택 대화 상자에서 **[!UICONTROL 새 프로젝트를 누릅니다.]**

   ![6_5_googleaccount-newproject](assets/6_5_googleaccount-newproject.png)

1. 새 프로젝트 대화 상자의 프로젝트 이름 필드에 새 프로젝트의 이름을 입력합니다.

   프로젝트 ID는 프로젝트 이름을 기반으로 합니다. 따라서 프로젝트 이름을 신중하게 선택합니다.만든 후에는 변경할 수 없습니다. 또한 나중에 AEM에서 YouTube를 설정할 때 동일한 프로젝트 ID를 다시 입력해야 합니다.그것을 적으셔도 좋습니다

1. **[!UICONTROL 만들기를 클릭합니다.]**

1. 다음 중 하나를 수행합니다.

   * 프로젝트의 대시보드의 시작하기 카드에서 **[!UICONTROL 탐색 및 API를 활성화합니다.]**
   * 프로젝트의 대시보드의 API 카드에서 **[!UICONTROL API로 이동을 누릅니다.]**

   ![6_5_googleaccount-api-enable2](assets/6_5_googleaccount-apis-enable2.png)

1. API 및 서비스 페이지의 상단 근처에 있는 **[!UICONTROL API 및 서비스 활성화를 탭합니다.]**
1. API 라이브러리 페이지의 왼쪽의 **[!UICONTROL 범주]** 아래에서 **[!UICONTROL YouTube를 탭합니다.]** 페이지 오른쪽에서  **[!UICONTROL YouTube 데이터 API를 누릅니다.]**
1. YouTube 데이터 API v3 페이지에서 **[!UICONTROL 활성화를 탭합니다.]**

   ![6_5_googleaccount-api-enable3](assets/6_5_googleaccount-apis-enable3.png)

1. API를 사용하려면 자격 증명이 필요할 수 있습니다. 필요한 경우 **[!UICONTROL 자격 증명 만들기를 클릭합니다.]**

   ![6_5_googleaccount-api-createcredentials](assets/6_5_googleaccount-apis-createcredentials.png)

1. **[!UICONTROL 프로젝트]** 페이지에 자격 증명을 추가하려면 1단계에서 다음을 수행합니다.

   * **[!UICONTROL 어떤 API를 사용하고 있습니까?]** 드롭다운 목록에서  **[!UICONTROL YouTube 데이터 API v3을 선택합니다.]**

   * **[!UICONTROL API를 어디에서 호출합니까?]** 드롭다운 목록에서  **[!UICONTROL 웹 서버(예: node.js, Tomcat)를 선택합니다.]**

   * **[!UICONTROL 어떤 데이터에 액세스하시겠습니까?]** 드롭다운 목록에서  **[!UICONTROL 사용자 데이터를 누릅니다.]**

   ![6_5_googleaccount-api-createcredentials2](assets/6_5_googleaccount-apis-createcredentials2.png)

1. **[!UICONTROL 필요한 자격 증명을 탭합니다.]**
1. **[!UICONTROL 프로젝트]** 페이지에 자격 증명 추가, 2단계의 **[!UICONTROL OAuth 2.0 클라이언트 ID 만들기]** 머리글 아래의 이름 필드에 원하는 경우 고유한 이름을 입력합니다. 또는 Google에서 지정한 기본 이름을 사용할 수 있습니다.
1. **[!UICONTROL Authorized Javascript 원본]** 머리글 아래의 텍스트 필드에 다음 경로를 입력하고 경로에 자신의 도메인과 포트 번호를 대체한 다음 **[!UICONTROL Enter]**&#x200B;를 눌러 목록에 경로를 추가합니다.

   `https://<servername.domain>:<port_number>`

   예, `https://1a2b3c.mycompany.com:4321`

   **참고**:위의 경로 예는 그림 용도로만 사용할 수 있습니다.

   ![6_5_googleaccount-apis-createcredentials-oauth](assets/6_5_googleaccount-apis-createcredentials-oauth.png)

1. **[!UICONTROL 인증된 리디렉션 URI]** 머리글 아래의 텍스트 필드에 다음 경로를 입력하고 경로에 사용자 자신의 도메인과 포트 번호를 대체한 다음 **[!UICONTROL Enter]**&#x200B;를 눌러 목록에 경로를 추가합니다.

   `https://<servername.domain>:<port_number>/etc/cloudservices/youtube.youtubecredentialcallback.json`

   예, `https://1a2b3c.mycompany.com:4321/etc/cloudservices/youtube.youtubecredentialcallback.json`

   **참고**:위의 경로 예는 그림 용도로만 사용할 수 있습니다.

1. **[!UICONTROL OAuth 클라이언트 ID 만들기를 클릭합니다.]**
1. **[!UICONTROL 프로젝트]** 페이지에 자격 증명 추가, 3단계의 **[!UICONTROL OAuth 2.0 동의 화면 설정]** 머리글 아래에서 현재 사용 중인 Gmail 이메일 주소를 선택합니다.

   ![6_5_googleaccount-apis-createcredentials-consententscreen](assets/6_5_googleaccount-apis-createcredentials-consentscreen.png)

1. **[!UICONTROL 사용자에게 표시되는 제품 이름]** 머리글의 텍스트 필드에 동의 화면에 표시할 항목을 입력합니다.

   AEM 관리자가 YouTube에 인증할 때 동의 화면이 표시됩니다.AEM은 허가를 위해 YouTube에 연락합니다.

1. **[!UICONTROL 계속을 클릭합니다.]**
1. 프로젝트 페이지에 자격 증명 추가 페이지의 4단계에서 **[!UICONTROL 자격 증명 다운로드]** 머리글 아래에서 **[!UICONTROL 다운로드를 탭합니다.]**

   ![6_5_googleaccount-api-createcredentials-downloadcredentials](assets/6_5_googleaccount-apis-createcredentials-downloadcredentials.png)

1. `client_id.json` 파일을 저장합니다.

   나중에 Adobe Experience Manager에서 YouTube를 설정할 때 다운로드한 json 파일이 필요합니다.

1. **[!UICONTROL 완료를 클릭합니다.]**

   Google 계정에서 로그아웃합니다. 이제 YouTube 채널을 만듭니다.

### YouTube 채널 {#creating-a-youtube-channel} 만들기

YouTube에 비디오를 게시하려면 하나 이상의 채널이 있어야 합니다. YouTube 채널을 이미 만든 경우 이 작업을 건너뛰고 [게시용 태그 추가](/help/assets/video.md#adding-tags-for-publishing)로 이동할 수 있습니다.

>[!CAUTION]
>
>AEM의 YouTube 설정 아래에 채널을 추가하기 전에 YouTube *에 채널을 하나 이상 설정해야 합니다(아래 AEM](#setting-up-youtube-in-aem)에서 YouTube 설정 참조).*[ 이렇게 하지 않으면 기존 채널이 없다는 경고가 표시되지 않습니다. 그러나 채널을 추가할 때도 Google 인증이 계속 수행되지만 비디오를 전송할 채널을 선택할 수 있는 옵션은 없습니다.

YouTube 채널을 만들려면:

1. [https://www.youtube.com](https://www.youtube.com/)로 이동하여 Google 계정 자격 증명을 사용하여 로그인합니다.
1. YouTube 페이지의 오른쪽 위 모서리에서 프로필 사진(단색 원 내에 문자로 나타날 수도 있음)을 클릭한 다음 **[!UICONTROL YouTube 설정]** (원형 톱니바퀴 아이콘)을 클릭합니다.
1. 개요 페이지의 추가 기능 머리글 아래에서 **[!UICONTROL 내 채널을 모두 보거나 새 채널을 만듭니다.]**
1. 채널 페이지에서 **[!UICONTROL 새 채널 만들기를 클릭합니다.]**
1. 브랜드 계정 페이지의 브랜드 계정 이름 필드에 비디오 자산을 게시할 위치를 선택하는 회사 이름이나 다른 채널 이름을 입력한 다음 **[!UICONTROL 만들기를 클릭합니다.]**

   AEM에서 YouTube를 설정할 때 다시 입력해야 하기 때문에 여기에 입력한 이름을 기억하십시오.

1. (선택 사항) 필요한 경우 채널을 더 추가합니다.

   이제 게시용 태그를 추가합니다.

### {#adding-tags-for-publishing} 게시를 위한 태그 추가

비디오를 YouTube에 게시하려면 AEM에서 하나 이상의 YouTube 채널에 태그를 연결합니다. 게시할 태그를 추가하려면 [태그 관리](/help/sites-administering/tags.md)를 참조하십시오.

또는 AEM에서 기본 태그를 사용하려는 경우 이 작업을 건너뛰고 [Enabling the YouTube 게시 복제 에이전트](#enabling-the-youtube-publish-replication-agent)로 이동할 수 있습니다.

### YouTube 게시 복제 에이전트 {#enabling-the-youtube-publish-replication-agent} 활성화

YouTube 게시 복제 에이전트를 활성화한 후 Google 클라우드 계정에 대한 연결을 테스트하려면 **[!UICONTROL 연결 테스트를 누릅니다.]** 브라우저 탭에 연결 결과가 표시됩니다. YouTube 채널을 추가한 경우 해당 채널의 목록이 테스트의 일부로 표시됩니다.

1. AEM의 왼쪽 위 모서리에서 AEM 로고를 클릭하고 왼쪽 레일에서 **[!UICONTROL 도구]** > **[!UICONTROL 배포]** > **[!UICONTROL 복제]** > **[!UICONTROL 작성자의 에이전트를 클릭합니다.]**
1. 작성자 에이전트 페이지에서 **[!UICONTROL YouTube 게시(youtube)를 클릭합니다.]**
1. 도구 모음에서 설정 오른쪽에서 **[!UICONTROL 편집을 클릭합니다.]**
1. 복제 에이전트를 켜려면 **[!UICONTROL 활성화됨]** 확인란을 선택합니다.
1. **[!UICONTROL 확인]**&#x200B;을 클릭합니다.

   이제 AEM에서 YouTube를 설정할 수 있습니다.

### AEM {#setting-up-youtube-in-aem}에서 YouTube 설정

AEM 6.4부터 AEM에서 YouTube 게시를 설정하는 새로운 터치 사용자 인터페이스 방법이 도입되었습니다. 사용 중인 AEM의 설치된 인스턴스를 기준으로 다음 중 하나를 수행합니다.

* 6.4 이전에 AEM에서 YouTube를 구성하려면 6.4](/help/assets/video.md#setting-up-youtube-in-aem-before) 이전에 [AEM에서 YouTube 설정을 참조하십시오.
* AEM 6.4 이상에서 YouTube를 구성하려면 AEM 6.4 이상에서 [YouTube 설정](#setting-up-youtube-in-aem-and-later)을 참조하십시오.

#### AEM 6.4 이상에서 YouTube 설정 {#setting-up-youtube-in-aem-and-later}

1. Dynamic Media 인스턴스에 관리자로 로그인해야 합니다.
1. AEM의 왼쪽 위 모서리에서 AEM 로고를 누른 다음 왼쪽 레일에서 **[!UICONTROL 도구]**(망치 아이콘) > **[!UICONTROL Cloud Services]** > **[!UICONTROL YouTube 게시 구성을 누릅니다.]**
1. **[!UICONTROL global]**&#x200B;을(를) 누릅니다(선택하지 않음).

1. 글로벌 페이지의 오른쪽 위 모서리 근처에 있는 **[!UICONTROL 만들기를 탭합니다.]**
1. YouTube 구성 만들기 페이지의 Google 클라우드 플랫폼 설정 아래의 **[!UICONTROL 응용 프로그램 이름]** 필드에 Google 프로젝트 ID를 입력합니다.

   처음에 Google 클라우드 설정을 처음 구성할 때 프로젝트 ID를 지정했습니다.
YouTube 구성 만들기 페이지를 열어 둡니다.잠시 후에 다시 돌아오실 겁니다

   ![6_5_youtubepublish-createyoutubeconfiguration](assets/6_5_youtubepublish-createyoutubeconfiguration.png)

1. 일반 텍스트 편집기를 사용하여 [Google 클라우드 설정 구성](/help/assets/video.md#configuring-google-cloud-settings) 작업에서 이전에 다운로드하고 저장한 JSON 파일을 엽니다.
1. 전체 JSON 텍스트를 선택하고 복사합니다.
1. YouTube 계정 설정 대화 상자로 돌아갑니다. **[!UICONTROL JSON 구성]** 필드에 JSON 텍스트를 붙여 넣습니다.
1. 페이지의 오른쪽 위 모서리 근처에 있는 **[!UICONTROL 저장을 탭합니다.]**

   이제 AEM에서 YouTube 채널을 설정합니다.

1. **[!UICONTROL 채널 추가를 누릅니다.]**
1. 채널 이름 필드에 **[!UICONTROL YouTube]** 이전 버전에 하나 이상의 채널을 추가하는 작업에서 만든 채널의 이름을 입력합니다.

   원할 경우 선택적으로 설명을 추가할 수 있습니다.

1. **[!UICONTROL 추가]**&#x200B;를 탭합니다.
1. YouTube/Google 인증이 표시됩니다. Google Cloud 계정에 아직 로그인하지 않은 경우 이 단계를 건너뜁니다.

   * Google 프로젝트 ID와 연관된 Google 사용자 이름 및 암호와 위의 JSON 텍스트를 입력합니다.
   * 계정에 있는 채널 수에 따라 2개 이상의 항목이 표시됩니다. 채널을 선택합니다. 이메일 주소를 선택하지 마십시오.채널이 아닙니다.
   * 다음 페이지에서 **[!UICONTROL 수락]**&#x200B;을 눌러 이 채널에 대한 액세스를 허용합니다.

1. **[!UICONTROL Allow.]**&#x200B;을 탭합니다.

   이제 게시용 태그를 설정합니다.

1. **[!UICONTROL 게시할]**  태그 설정 - Cloud Services > YouTube 페이지에서 연필 아이콘을 눌러 사용할 태그 목록을 편집합니다.
1. 드롭다운 목록 아이콘(위/아래 삽입 기호)을 눌러 AEM에서 사용 가능한 태그 목록을 표시합니다.
1. 태그를 하나 이상 눌러 추가합니다.

   추가한 태그를 삭제하려면 태그를 선택하고 **[!UICONTROL X.]**

1. 원하는 태그 추가가 완료되면 **[!UICONTROL 저장을 탭합니다.]**

   이제 비디오를 YouTube 채널에 게시합니다.

#### 6.4 이전 AEM에서 YouTube 설정 {#setting-up-youtube-in-aem-before}

1. Dynamic Media 인스턴스에 관리자로 로그인해야 합니다.

1. AEM의 왼쪽 위 모서리에서 AEM 로고를 누른 다음 왼쪽 레일에서 **[!UICONTROL 도구]**(망치 아이콘) > **[!UICONTROL 배포]** > **[!UICONTROL Cloud Services을 누릅니다.]**
1. 제3자 서비스 머리글 아래의 YouTube에서 **[!UICONTROL 지금 구성을 탭합니다.]**
1. 구성 만들기 대화 상자의 각 필드에 제목(필수)과 이름(선택 사항)을 입력합니다.
1. **[!UICONTROL 만들기를 누릅니다.]**
1. YouTube 계정 설정 대화 상자의 **[!UICONTROL 응용 프로그램 이름]** 필드에 Google 프로젝트 ID를 입력합니다.

   처음에 [Google 클라우드 설정](/help/assets/video.md#configuring-google-cloud-settings) 이전 버전을 구성할 때 프로젝트 ID를 지정했습니다.
YouTube 계정 설정 대화 상자를 열어 둡니다.잠시 후에 다시 돌아오실 겁니다

1. 일반 텍스트 편집기를 사용하여 이전에 다운로드하고 저장한 JSON 파일을 Google 클라우드 설정 구성 작업에서 엽니다.
1. 전체 JSON 텍스트를 선택하고 복사합니다.
1. YouTube 계정 설정 대화 상자로 돌아갑니다. **[!UICONTROL JSON 구성]** 필드에 JSON 텍스트를 붙여 넣습니다.
1. **[!UICONTROL 확인을 누릅니다.]**

   이제 AEM에서 YouTube 채널을 설정합니다.

1. **[!UICONTROL 사용 가능한 채널]**&#x200B;의 오른쪽에서 **+**(더하기 기호 아이콘)을 누릅니다.
1. [YouTube 채널 설정] 대화 상자의 [제목] 필드에 **[!UICONTROL YouTube]** 이전 버전에 하나 이상의 채널을 추가하는 작업에서 만든 채널의 이름을 입력합니다.

   원할 경우 선택적으로 설명을 추가할 수 있습니다.

1. **[!UICONTROL 확인을 누릅니다.]**
1. YouTube/Google 인증이 표시됩니다. Google Cloud 계정에 아직 로그인하지 않은 경우 이 단계를 건너뜁니다.

   * Google 프로젝트 ID와 연관된 Google 사용자 이름 및 암호와 위의 JSON 텍스트를 입력합니다.
   * 계정에 있는 채널 수에 따라 2개 이상의 항목이 표시됩니다. 채널을 선택합니다. 이메일 주소를 선택하지 마십시오.채널이 아닙니다.
   * 다음 페이지에서 **[!UICONTROL 수락]**&#x200B;을 눌러 이 채널에 대한 액세스를 허용합니다.

1. **[!UICONTROL Allow.]**&#x200B;을 탭합니다.

   이제 게시용 태그를 설정합니다.

1. **[!UICONTROL 게시할]**  태그 설정 - Cloud Services > YouTube 페이지에서 연필 아이콘을 눌러 사용할 태그 목록을 편집합니다.
1. 드롭다운 목록 아이콘(위/아래 삽입 기호)을 눌러 AEM에서 사용 가능한 태그 목록을 표시합니다.
1. 태그를 하나 이상 눌러 추가합니다.

   추가한 태그를 삭제하려면 태그를 선택하고 **X**&#x200B;을 누릅니다.

1. 원하는 태그 추가가 완료되면 **[!UICONTROL 확인을 누릅니다.]**

   이제 비디오를 YouTube 채널에 게시합니다.

### (선택 사항) 업로드한 비디오에 대한 기본 YouTube 속성 설정을 자동화합니다 {#optional-automating-the-setting-of-default-youtube-properties-for-your-uploaded-videos}

선택적으로 비디오를 업로드할 때 YouTube 속성 설정을 자동화할 수 있습니다. AEM에서 메타데이터 처리 프로필을 만들어 이를 완수합니다.

메타데이터 처리 프로필을 만들려면 먼저 **[!UICONTROL 필드 레이블]**, **[!UICONTROL 속성]**&#x200B;에 매핑 및 **[!UICONTROL Choices]** 필드에서 비디오를 위한 메타데이터 스키마에 있는 값을 복사합니다. 그런 다음 해당 값을 YouTube 비디오 메타데이터 처리 프로필에 추가하여 프로필을 만듭니다.

업로드된 비디오에 대한 기본 YouTube 속성 설정을 자동화하려면:

1. AEM의 왼쪽 위 모서리에서 AEM 로고를 클릭하고 왼쪽 레일에서 **[!UICONTROL 도구]**(망치 아이콘) > **[!UICONTROL 자산]** > **[!UICONTROL 메타데이터 스키마를 클릭합니다.]**
1. **[!UICONTROL 기본값을 클릭합니다.]** (선택 상자의 왼쪽에 &quot;기본값&quot;을 선택하지 마십시오.)
1. **[!UICONTROL 기본]** 페이지에서 **[!UICONTROL video]**&#x200B;의 왼쪽에 있는 상자를 선택한 다음 **[!UICONTROL 편집을 클릭합니다.]**
1. 메타데이터 스키마 편집기 페이지에서 **[!UICONTROL 고급]** 탭을 클릭합니다.
1. YouTube 게시 머리글에서 **[!UICONTROL YouTube 카테고리.]**
1. 페이지 오른쪽의 **[!UICONTROL 설정]** 탭에서 다음을 수행합니다.

   * **[!UICONTROL 속성에 매핑]** 텍스트 필드에서 값을 선택하고 복사합니다.
복사한 값을 열려 있는 텍스트 편집기에 붙여넣습니다. 나중에 메타데이터 처리 프로필을 만들 때 이 값이 필요합니다. 텍스트 편집기를 엽니다.

   * **[!UICONTROL 선택 항목]**에서 사용할 기본값(예: 사람 및 블로그, 과학 및 기술)을 선택하고 복사합니다.
복사한 값을 열려 있는 텍스트 편집기에 붙여넣습니다. 나중에 메타데이터 처리 프로필을 만들 때 이 값이 필요합니다. 텍스트 편집기를 엽니다.

1. YouTube 게시 머리글에서 **[!UICONTROL YouTube 개인 정보 보호.]**
1. 페이지 오른쪽의 **[!UICONTROL 설정]** 탭에서 다음을 수행합니다.

   * **[!UICONTROL 속성에 매핑]** 텍스트 필드에서 값을 선택하고 복사합니다.
복사한 값을 열려 있는 텍스트 편집기에 붙여넣습니다. 나중에 메타데이터 처리 프로필을 만들 때 이 값이 필요합니다. 텍스트 편집기를 엽니다.

   * **[!UICONTROL 선택 항목]**에서 사용할 기본값을 선택하고 복사합니다. 선택 항목은 두 쌍으로 그룹화됩니다. 쌍의 맨 아래 필드는 복사하려는 기본값(예: public, 목록에 없음 또는 private)입니다.
복사한 값을 열려 있는 텍스트 편집기에 붙여넣습니다. 나중에 메타데이터 처리 프로필을 만들 때 이 값이 필요합니다. 텍스트 편집기를 엽니다.

1. 메타데이터 스키마 편집기 페이지의 오른쪽 위 모서리 근처에 있는 **[!UICONTROL 취소.]**
1. AEM의 왼쪽 위 모서리에서 AEM 로고를 누른 다음 왼쪽 레일에서 **[!UICONTROL 도구]**(망치 아이콘) > **[!UICONTROL 자산]** > **[!UICONTROL 메타데이터 프로필을 클릭합니다.]**

1. 페이지의 오른쪽 위 모서리 근처에 있는 메타데이터 프로필 페이지에서 **[!UICONTROL 만들기를 클릭합니다.]**
1. 메타데이터 프로필 추가 대화 상자의 **[!UICONTROL 프로필 제목]** 텍스트 필드에 이름 `YouTube Video`을 입력한 다음 **[!UICONTROL 만들기.]**
1. 메타데이터 프로필 편집기 페이지에서 **[!UICONTROL 고급]** 탭을 클릭합니다.
1. 다음을 수행하여 복사한 YouTube 게시 값을 프로필에 추가합니다.

   * 페이지 오른쪽에서 **[!UICONTROL 양식 작성]** 탭을 클릭합니다.
   * (선택 사항) **[!UICONTROL 섹션 헤더]**&#x200B;라는 레이블이 지정된 구성 요소를 왼쪽으로 드래그하여 양식 영역에 놓습니다.
   * (선택 사항) **[!UICONTROL 필드 레이블]**&#x200B;을 클릭하여 구성 요소를 선택합니다.
   * (선택 사항) 페이지 오른쪽의 설정 탭의 필드 레이블 텍스트 필드에 `YouTube Publishing`을 입력합니다.
   * **[!UICONTROL 빌드 양식]** 탭을 클릭한 다음 **[!UICONTROL 복수 값 텍스트]**&#x200B;라는 구성 요소를 드래그하여 방금 만든 **[!UICONTROL YouTube 게시]** 머리글 아래에 놓습니다.

   * **[!UICONTROL 필드 레이블]**&#x200B;을 클릭하여 구성 요소를 선택합니다.
   * 페이지 오른쪽의 설정 탭에서 이전에 복사한 YouTube 게시 값(필드 레이블 값 및 속성 값에 매핑)을 양식의 각 필드에 붙여 넣습니다. 선택 항목 값을 기본값 필드에 붙여 넣습니다.

1. 다음을 수행하여 복사한 YouTube 개인 정보 값을 프로필에 추가합니다.

   * 페이지 오른쪽에서 **[!UICONTROL 양식 작성]** 탭을 클릭합니다.
   * (선택 사항) **[!UICONTROL 섹션 헤더]**&#x200B;라는 레이블이 지정된 구성 요소를 왼쪽으로 드래그하여 양식 영역에 놓습니다.
   * (선택 사항) **[!UICONTROL 필드 레이블]**&#x200B;을 클릭하여 구성 요소를 선택합니다.
   * (선택 사항) 페이지 오른쪽의 설정 탭의 필드 레이블 텍스트 필드에 `YouTube Privacy`을 입력합니다.
   * **[!UICONTROL 빌드 양식]** 탭을 클릭한 다음 **[!UICONTROL 복수 값 텍스트]**&#x200B;라는 구성 요소를 드래그하여 방금 만든 **[!UICONTROL YouTube 개인 정보 보호]** 머리글 아래에 놓습니다.

   * **[!UICONTROL 필드 레이블]**&#x200B;을 클릭하여 구성 요소를 선택합니다.
   * 페이지 오른쪽의 설정 탭에서 이전에 복사한 YouTube 게시 값(필드 레이블 값 및 속성 값에 매핑)을 양식의 각 필드에 붙여 넣습니다. 선택 항목 값을 기본값 필드에 붙여 넣습니다.

1. 페이지의 오른쪽 위 모서리 근처에 있는 **[!UICONTROL 저장을 클릭합니다.]**
1. 비디오를 업로드할 폴더에 YouTube 게시 메타데이터 프로필을 적용합니다. 메타데이터 프로필과 비디오 프로필 세트를 모두 설정해야 합니다.

   [메타데이터 프로필](/help/assets/metadata-config.md#metadata-profiles) 및 [비디오 프로필](/help/assets/video-profiles.md)을 참조하십시오.

### YouTube 채널 {#publishing-videos-to-your-youtube-channel}에 비디오 게시

비디오 자산에 이전에 추가한 태그를 연결합니다. 이 프로세스를 통해 AEM에서 YouTube 채널에 게시할 자산을 알 수 있습니다.

>[!NOTE]
>
>Dynamic Media - Scene7 모드에서 실행 중인 경우 즉시 게시가 YouTube에 자동으로 게시되지 않습니다. Dynamic Media - Scene7 모드가 설정되면 다음 두 가지 게시 옵션 중에서 선택할 수 있습니다.**[!UICONTROL 즉시]** 또는 **[!UICONTROL 활성화 시.]**
>
>**[!UICONTROL 즉시 게시]** 는 업로드된 자산(IPS와 동기화된 후)이 배달 시스템에 자동으로 게시됨을 의미합니다. Dynamic Media의 경우에는 그렇지만 YouTube에서는 그렇지 않습니다. YouTube에 게시하려면 AEM 작성자 방식으로 게시해야 합니다.

>[!NOTE]
>
>YouTube에서 콘텐츠를 게시하기 위해 AEM에서는 진행 상황을 모니터링하고 실패 정보를 볼 수 있도록 **[!UICONTROL Publish to YouTube]** 작업 과정을 사용합니다.
>
>[비디오 인코딩 및 YouTube 게시 진행 모니터링](#monitoring-video-encoding-and-youtube-publishing-progress)을 참조하십시오.
>
>자세한 진행 정보를 보려면 복제 아래의 YouTube 로그를 모니터링할 수 있습니다. 그러나 이러한 모니터링에는 관리자 액세스가 필요합니다.

비디오를 YouTube 채널에 게시하려면:

1. AEM에서 YouTube 채널에 게시할 비디오 자산으로 이동합니다.
1. 비디오 자산(응용 비디오 세트)을 선택합니다.
1. 도구 모음에서 **[!UICONTROL 속성을 클릭합니다.]**
1. 기본 탭의 메타데이터 머리글에서 태그 필드 오른쪽에 있는 **[!UICONTROL 선택 대화 상자 열기]**&#x200B;를 클릭합니다.
1. 태그 선택 페이지에서 사용할 태그로 이동한 다음 하나 이상의 태그를 선택합니다.

   태그가 YouTube 채널과 연결되어 있어야 합니다.

1. 페이지의 오른쪽 위 모서리에서 **[!UICONTROL 선택을 클릭합니다.]**
1. 비디오 속성 페이지의 오른쪽 위 모서리에서 **[!UICONTROL 저장 및 닫기.]**
1. 도구 모음에서 **[!UICONTROL 빠른 게시.]**

   AEM Sites](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/page-authoring/publication-management-feature-video-use.html)에서 게시 관리 사용을 참조하십시오.[

   YouTube 채널에서 게시된 비디오를 선택적으로 확인할 수 있습니다.

### (선택 사항) 게시된 비디오를 YouTube {#optional-verifying-the-published-video-on-youtube}에서 확인

선택적으로 YouTube 게시(또는 게시 취소)의 진행 상태를 모니터링할 수 있습니다.

[비디오 인코딩 및 YouTube 게시 진행 모니터링](#monitoring-video-encoding-and-youtube-publishing-progress)을 참조하십시오.

게시 시간은 기본 소스 비디오 형식, 파일 크기 및 업로드 트래픽을 포함하는 다양한 요소에 따라 크게 다를 수 있습니다. 게시 프로세스는 몇 분에서 몇 시간 정도 걸릴 수 있습니다. 또한 고해상도 포맷은 훨씬 더 느리게 렌더링됩니다. 예를 들어 720p 및 1080p는 480p보다 표시되는 데 훨씬 오래 걸립니다.

**[!UICONTROL 업로드됨(처리 중)]**&#x200B;이라는 상태 메시지가 계속 나타나면 8시간 후 사이트에서 비디오를 제거하고 다시 업로드해 보십시오.

### YouTube URL을 웹 응용 프로그램 {#linking-youtube-urls-to-your-web-application}에 연결

비디오를 게시한 후 Dynamic Media에서 생성한 YouTube URL 문자열을 얻을 수 있습니다. YouTube URL을 복사하면 클립보드에 배치되므로 필요에 따라 웹 사이트 또는 애플리케이션의 페이지에 붙여넣을 수 있습니다.

>[!NOTE]
>
>YouTube URL은 비디오 자산을 YouTube에 게시하기 전까지 복사할 수 없습니다.

YouTube URL을 웹 애플리케이션에 연결하려면:

1. 복사할 URL이 있는 *YouTube 게시된* 비디오 자산으로 이동한 다음 선택합니다.

   YouTube URL은 *after*&#x200B;을(를) 복사하여 *게시된*&#x200B;만 YouTube에 사용할 수 있습니다.

1. 도구 모음에서 **[!UICONTROL 속성을 클릭합니다.]**
1. **[!UICONTROL 고급]** 탭을 클릭합니다.
1. YouTube 게시 머리글의 YouTube URL 목록에서 URL 텍스트를 선택하고 웹 브라우저에 복사하여 자산을 미리 보거나 웹 컨텐츠 페이지에 추가합니다.

### 비디오를 게시 취소하여 YouTube {#unpublishing-videos-to-remove-them-from-youtube}에서 제거

AEM에서 비디오 에셋을 게시 취소하면 비디오가 YouTube에서 제거됩니다.

>[!CAUTION]
>
>YouTube에서 바로 비디오를 제거하면 AEM은 이를 인식하지 못하고 비디오가 YouTube에 아직 게시된 것처럼 계속 동작합니다. 항상 AEM을 통해 YouTube에서 비디오 에셋을 게시 취소합니다.

>[!NOTE]
>
>YouTube에서 콘텐츠를 제거하려면 진행 상황을 모니터링하고 오류 정보를 볼 수 있는 **[!UICONTROL YouTube에서 게시 취소]** 작업 과정을 사용합니다.
>
>[비디오 인코딩 및 YouTube 게시 진행 모니터링](#monitoring-video-encoding-and-youtube-publishing-progress)을 참조하십시오.

YouTube에서 제거할 비디오를 게시 취소하려면 다음을 수행하십시오.

1. YouTube 채널에서 게시를 취소할 비디오 자산으로 이동합니다.
1. 자산 선택 모드에서 게시된 비디오 자산을 하나 이상 선택합니다.
1. 도구 모음에서 **[!UICONTROL 게시 관리를 클릭합니다.]** 세 개의 점 아이콘(.)을 눌러야 할 수도 있습니다...) 도구 모음에서 **[!UICONTROL 게시 관리.]**
1. 게시 관리 페이지에서 **[!UICONTROL 게시 취소를 누릅니다.]**
1. 페이지의 오른쪽 위 모서리에서 **[!UICONTROL 다음.]**
1. 페이지의 오른쪽 위 모서리에서 **[!UICONTROL 게시 취소를 누릅니다.]**

## 비디오 인코딩 및 YouTube 게시 진행 모니터링 {#monitoring-video-encoding-and-youtube-publishing-progress}

비디오 인코딩이 적용된 폴더에 새 비디오를 업로드하거나 Youtube에 비디오를 게시하면 다양한 방법으로 비디오 인코딩/Youtube 게시 진행(또는 실패)을 모니터링할 수 있습니다. 실제 YouTube 게시 진행 상태는 로그를 통해서만 사용할 수 있지만 실패하거나 성공했는지 여부는 다음 절차에 설명된 추가 방법으로 나열되어 있습니다. 또한 YouTube 게시 워크플로우 또는 비디오 인코딩이 완료되거나 중단되면 이메일 알림을 받을 수 있습니다.

### 진행률 모니터링 {#monitoring-progress}

진행 상태를 모니터링하려면(인코딩 실패/YouTube 게시 포함):

1. 에셋 폴더에서 비디오 인코딩 진행 상황 보기:

   * 카드 보기에서는 비디오 인코딩 진행 상태가 백분율로 자산에 표시됩니다. 오류가 있는 경우 이 정보도 자산에 표시됩니다.

   ![chlimage_1-429](assets/chlimage_1-429.png)

   * 목록 보기에서는 비디오 인코딩 진행 상태가 **[!UICONTROL 처리 상태]** 열에 표시됩니다. 오류가 있으면 이 메시지가 동일한 열에 표시됩니다.

   ![chlimage_1-430](assets/chlimage_1-430.png)

   이 열은 기본적으로 표시되지 않습니다. 열을 활성화하려면 보기 드롭다운 메뉴에서 **[!UICONTROL 설정 보기]**&#x200B;를 선택하고 **[!UICONTROL 처리 상태]** 열을 추가한 다음 **[!UICONTROL 업데이트]**&#x200B;를 탭하거나 클릭합니다.

   ![chlimage_1-431](assets/chlimage_1-431.png)

1. 자산 세부 사항에서 진행 상황을 봅니다. 자산을 탭하거나 클릭하면 드롭다운 메뉴를 열고 **[!UICONTROL 타임라인을 선택합니다.]** 인코딩 또는 YouTube 게시와 같은 워크플로우 활동으로 범위를 좁히려면 워크플로우를  **[!UICONTROL 선택합니다.]**

   ![chlimage_1-432](assets/chlimage_1-432.png)

   인코딩 등 모든 워크플로우 정보가 타임라인에 표시됩니다. YouTube 게시를 위한 워크플로우 타임라인에는 YouTube 채널 이름과 YouTube 비디오 URL도 포함되어 있습니다. 또한 게시가 완료된 후 워크플로우 타임라인에 오류 알림이 표시됩니다.

   >[!NOTE]
   >
   >다음과 같이 [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)에서 **[!UICONTROL retries]**, **[!UICONTROL 재시도 지연]** 및 **[!UICONTROL 시간 초과]**&#x200B;에 대한 여러 워크플로우 구성이 있기 때문에 실패/오류 메시지가 최종적으로 기록되는 데 시간이 오래 걸릴 수 있습니다.
   >
   >    * Apache Sling 작업 큐 구성
   >    * Adobe Granite Workflow 외부 프로세스 작업 핸들러
   >    * Granite Workflow 시간 초과 큐

   >
   >이러한 구성에서 **[!UICONTROL 재시도]**, **[!UICONTROL 재시도 지연]** 및 **[!UICONTROL 시간 초과]** 속성을 조정할 수 있습니다.

1. 진행 중인 워크플로우의 경우 **[!UICONTROL 도구]** > **[!UICONTROL 워크플로]** > **[!UICONTROL 인스턴스에서 사용할 수 있는 워크플로 인스턴스를 참조하십시오.]**

   >[!NOTE]
   >
   >**[!UICONTROL 도구]** 메뉴에 액세스하려면 관리 권한이 필요할 수 있습니다.

   ![chlimage_1-433](assets/chlimage_1-433.png)

   인스턴스를 선택하고 **[!UICONTROL 작업 내역 열기]**&#x200B;를 탭하거나 클릭합니다.

   ![chlimage_1-434](assets/chlimage_1-434.png)

   워크플로우 인스턴스 영역에서 워크플로우를 일시 중단하거나 종료하거나 이름을 변경할 수도 있습니다. 자세한 내용은 [워크플로우 관리](/help/sites-administering/workflows-administering.md)를 참조하십시오.

1. 실패한 작업의 경우 **[!UICONTROL 도구]** > **[!UICONTROL 워크플로]** > **[!UICONTROL 실패에서 사용할 수 있는 워크플로 오류를 참조하십시오.]** 워크플로우  **[!UICONTROL 실패]** 는 모든 실패한 워크플로우 활동을 나타냅니다.

   >[!NOTE]
   >
   >**[!UICONTROL 도구]** 메뉴에 액세스하려면 관리 권한이 필요할 수 있습니다.

   ![chlimage_1-435](assets/chlimage_1-435.png)

   >[!NOTE]
   >
   >다음 예와 같이 [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)에서 **[!UICONTROL 재시도]**, **[!UICONTROL 재시도 지연]** 및 **[!UICONTROL 시간 초과]**&#x200B;에 대한 여러 워크플로우 구성이 있기 때문에 오류 메시지가 최종적으로 기록되는 데 시간이 오래 걸릴 수 있습니다.
   >
   >
   >
   >    * Apache Sling 작업 큐 구성
   >    * Adobe Granite Workflow 외부 프로세스 작업 핸들러
   >    * Granite Workflow 시간 초과 큐

   >
   >
   >이러한 구성에서 **[!UICONTROL 재시도]**, **[!UICONTROL 재시도 지연]** 및 **[!UICONTROL 시간 초과]** 속성을 조정할 수 있습니다.

1. 완료된 워크플로우의 경우 **[!UICONTROL 도구]** > **[!UICONTROL 워크플로]** > **[!UICONTROL 보관에서 사용할 수 있는 워크플로 아카이브를 참조하십시오.]** 워크플로우  **[!UICONTROL 아카이브]** 기록 목록 완료된 워크플로우 활동

   >[!NOTE]
   >
   >**[!UICONTROL 도구]** 메뉴에 액세스하려면 관리 권한이 필요할 수 있습니다.

   ![chlimage_1-436](assets/chlimage_1-436.png)

1. 워크플로우 중단 또는 실패에 대한 이메일 알림을 받을 수 있습니다. 이러한 이메일 알림은 관리자가 구성할 수 있습니다. [이메일 알림 구성](#configuring-e-mail-notifications)을 참조하십시오.

#### 전자 메일 알림 구성 {#configuring-e-mail-notifications}

>[!NOTE]
>
>**[!UICONTROL 도구]** 메뉴에 액세스하려면 관리 권한이 필요할 수 있습니다.

알림을 구성하는 방법은 인코딩 작업 또는 YouTube 게시 작업에 대한 알림을 원하는지 여부에 따라 다릅니다.

* 인코딩 작업의 경우 **[!UICONTROL 도구]** > **[!UICONTROL 작업]** > **[!UICONTROL 웹 콘솔]**&#x200B;에서 모든 AEM 워크플로우 이메일 알림에 대한 구성 페이지에 액세스하고 **[!UICONTROL 일 CQ 워크플로우 이메일 알림 서비스를 검색하여 액세스할 수 있습니다.]** AEM [에서 이메일 알림 구성을 참조하십시오](/help/sites-administering/notification.md). **[!UICONTROL 중단 시 알림]** 또는 **[!UICONTROL 완료 시 알림]**&#x200B;에 대한 확인란을 선택하거나 선택 취소할 수 있습니다.

* YouTube 게시 작업의 경우 다음을 수행합니다.

1. AEM에서 **[!UICONTROL 도구]** > **[!UICONTROL 워크플로]** > **[!UICONTROL 모델을 누릅니다.]**
1. 워크플로우 모델 페이지에서 **[!UICONTROL YouTube에 게시]**&#x200B;를 선택한 다음 도구 모음에서 **[!UICONTROL 편집]**&#x200B;을 탭합니다.
1. YouTube에 게시 워크플로우 페이지의 오른쪽 위 모서리 근처에 있는 **[!UICONTROL 편집을 탭합니다.]**
1. YouTube 업로드 구성 요소에 마우스 포인터를 올려 놓은 다음 한 번 눌러 인라인 도구 모음을 표시합니다.

   ![6_5_publishtoyoutubeworkflow](assets/6_5_publishtoyoutubeworkflow.png)

1. 인라인 도구 모음에서 구성 아이콘(렌치)을 누릅니다. **[!UICONTROL 인수]** 탭을 클릭합니다.

   ![6_5_publishtoyoutubeworkflow-configurationicon](assets/6_5_publishtoyoutubeworkflow-configurationicon.png)

1. YouTube 업로드 프로세스 - 단계 속성 대화 상자에서 **[!UICONTROL 인수]** 탭을 누릅니다.

   ![6_5_publishtoyoutubeworkflow-arguments-tab](assets/6_5_publishtoyoutubeworkflow-arguments-tab.png)

1. 다음 확인란을 선택하거나 취소할 수 있습니다.

   * 게시 시작
   * 게시 실패
   * 게시 완료 - 채널 및 URL에 대한 정보 포함

   확인란을 지우면 YouTube 게시 워크플로우에서 지정된 이메일 알림을 받지 못함을 의미합니다.

   >[!NOTE]
   >
   >이러한 이메일은 YouTube에만 해당되며 일반적인 워크플로 이메일 알림에도 추가됩니다. 그 결과, 2개의 이메일 알림 세트(CQ Workflow Email Notification Service ]**일 CQ Workflow에서 사용할 수 있는 일반 알림 및 구성 설정에 따라 YouTube에만 적용되는 알림)를 받을 수 있습니다.**[!UICONTROL 

1. 완료되면 대화 상자의 오른쪽 위 모서리 근처에 있는 **[!UICONTROL 완료]** 아이콘(확인 표시)을 누릅니다.
1. YouTube에 게시 워크플로우 페이지의 오른쪽 위 모서리 근처에 있는 **[!UICONTROL 동기화를 탭합니다.]**

## 비디오 보고서 보기 {#viewing-video-reports}

>[!NOTE]
>
>비디오 보고서는 Dynamic Media - 하이브리드 모드를 실행할 때만 사용할 수 있습니다.

비디오 보고서에는 지정된 기간 동안 게시된 *개별 및 집계 비디오가 예상대로 수행되고 있음을 모니터하는 데 도움이 되는 몇 가지 집계 지표가 표시됩니다. 다음 주요 지표 데이터는 전체 웹 사이트에서 게시된 모든 비디오에 대해 집계됩니다.

* 비디오 시작
* 완료율
* 비디오 평균 시간
* 비디오 총 시간
* 방문당 비디오

전체 비디오 시작을 기준으로 웹 사이트에서 가장 많이 본 비디오를 추적할 수 있도록 모든 *게시된* 비디오의 표도 나열됩니다.

목록에서 비디오 이름을 누르면 라인 차트 형식으로 비디오의 대상 유지(드롭다운) 보고서가 표시됩니다. 차트에는 비디오 재생 중 지정된 시간의 뷰 수가 표시됩니다. 비디오를 재생하면 세로 막대가 플레이어의 시간 표시기와 동기화되는 상태로 추적됩니다. 라인 차트 데이터의 드롭은 대상이 관심 없는 위치에서 이탈하는 위치를 나타냅니다.

비디오가 Adobe Experience Manager Dynamic Media 외부에서 인코딩된 경우 대상 유지(드롭다운) 차트와 테이블의 재생 백분율 데이터를 사용할 수 없습니다.

[Dynamic Media Cloud Services 구성](/help/assets/config-dynamic.md)을 참조하십시오.

>[!NOTE]
>
>추적 및 보고 데이터는 Dynamic Media의 자체 비디오 플레이어 및 관련 비디오 플레이어 사전 설정의 사용만을 기반으로 합니다. 따라서 다른 비디오 플레이어를 통해 재생되는 비디오를 추적하고 보고할 수 없습니다.

기본적으로 비디오 보고서를 처음 입력할 때 보고서에는 현재 월의 첫 번째 부분에서 시작하여 현재 월의 날짜로 끝나는 비디오 데이터가 표시됩니다. 그러나 고유한 날짜 범위를 지정하여 기본 날짜 범위를 재정의할 수 있습니다. 다음에 비디오 보고서를 입력하면 지정한 날짜 범위가 사용됩니다.

비디오 보고서가 제대로 작동하려면 Dynamic Media Cloud Services이 구성되면 보고서 세트 ID가 자동으로 생성됩니다. 동시에 보고서 세트 ID는 자산을 미리 볼 때 URL 복사 기능에 사용할 수 있도록 게시 서버로 푸시됩니다. 그러나 게시 서버가 이미 설정되어 있어야 합니다. 게시 서버가 설정되어 있지 않으면 여전히 게시하여 비디오 보고서를 볼 수 있지만, Dynamic Media 클라우드 구성으로 돌아가서 **[!UICONTROL 확인을 탭해야 합니다.]**

비디오 보고서를 보려면:

1. AEM의 왼쪽 위 모서리에서 AEM 로고를 누른 다음 왼쪽 레일에서 **[!UICONTROL 도구]**(망치 아이콘) > **[!UICONTROL 자산]** > **[!UICONTROL 비디오 보고서.]**
1. 비디오 보고서 페이지에서 다음 중 하나를 수행합니다.

   * 오른쪽 위 모서리 근처에 있는 **비디오 보고서 새로 고침** 아이콘을 탭합니다.
보고서의 종료 날짜가 현재 날짜인 경우에만 새로 고침을 사용해야 합니다. 이렇게 하면 마지막으로 보고서를 실행한 이후 발생한 비디오 추적이 표시됩니다.

   * 오른쪽 위 모서리 근처에 있는 **날짜 선택기** 아이콘을 탭합니다.
비디오 데이터를 저장할 시작 및 종료 날짜 범위를 지정한 다음 **[!UICONTROL 보고서 실행을 누릅니다.]**

   상위 지표 그룹 상자는 사이트에서 게시된 모든 *게시된* 비디오에 대한 다양한 집계 측정을 식별합니다.

1. 상위 게시된 비디오를 나열하는 표에서 비디오 이름을 눌러 비디오를 재생하고 비디오의 대상자 유지(드롭다운) 보고서를 확인합니다.

### Dynamic Media HTML5 뷰어 SDK {#viewing-video-reports-based-on-a-video-viewer-that-you-created-using-the-scene-hmtl-viewer-sdk}를 사용하여 만든 비디오 뷰어를 기반으로 비디오 보고서 보기

Dynamic Media에서 제공하는 기본 비디오 뷰어를 사용하거나 기본 비디오 뷰어를 기반으로 사용자 정의 뷰어 사전 설정을 만든 경우 비디오 보고서를 보는 데 추가 단계가 필요하지 않습니다. 그러나 HTML5 뷰어 SDK API를 기반으로 자체 비디오 뷰어를 만든 경우, 다음 단계를 사용하여 비디오 뷰어가 추적 이벤트를 Dynamic Media 비디오 보고서로 전송하도록 하십시오.

[Adobe Dynamic Media 뷰어 참조 안내서](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/home.html) 및 [HTML5 뷰어 SDK API](https://s7d1.scene7.com/s7sdk/3.10/docs/jsdoc/index.html)를 사용하여 고유한 비디오 뷰어를 만듭니다.

HTML5 뷰어 SDK API를 사용하여 만든 비디오 뷰어를 기반으로 비디오 보고서를 보려면:

1. 게시된 비디오 자산으로 이동합니다.
1. 자산 페이지의 왼쪽 위 모서리 근처에 있는 드롭다운 목록에서 **[!UICONTROL 뷰어]**&#x200B;를 선택합니다.
1. 비디오 뷰어 사전 설정을 선택하고 포함 코드를 복사합니다.
1. 포함 코드에서 다음 행을 찾습니다.

   `videoViewer.setParam("config2", "<value>");`

   `config2` 매개 변수는 HTML5 뷰어에서 추적을 활성화합니다. 또한 비디오 보고 및 고객별 Adobe Analytics 구성에 대한 구성 정보가 포함된 회사별 사전 설정입니다.

   config2 매개 변수의 올바른 값은 **[!UICONTROL 포함 코드]** 및 **[!UICONTROL URL]** 복사 함수에 모두 있습니다. 복사 **[!UICONTROL URL]** 명령의 URL에서 찾을 매개 변수는 `&config2=<value>`입니다. 이 값은 거의 항상 `companypreset`이지만, 경우에 따라 `companypreset-1`, `companypreset-2` 등이 될 수도 있습니다.

1. 사용자 정의 비디오 뷰어 코드에서 다음을 수행하여 뷰어 페이지에 AppMeasurementBridge .jsp를 추가합니다.

   * 먼저 `&preset` 매개 변수가 필요한지 확인합니다.

      `config2` 매개 변수가 `companypreset`이면 *에 `&preset=parameter`가 필요하지 않은*&#x200B;입니다.

      `config2`이(가) 다른 경우 사전 설정 매개 변수를 `config2` 매개 변수와 동일하게 설정합니다. 예를 들어 `config2=companypreset-2`인 경우 AppMeasurmentBridge.jsp URL에 `&param2=companypreset-2`을 추가합니다.

   * 그런 다음 AppMeasurementBridge.jsp 스크립트를 추가합니다.

      `<script language="javascript" type="text/javascript" src="https://s7d1.scene7.com/s7viewers/AppMeasurementBridge.jsp?company=robindallas&preset=companypreset-2"></script>`

1. 다음을 수행하여 TrackingManager 구성 요소를 만듭니다.

   * `s7sdk.Util.init();`을(를) 호출한 후 다음을 추가하여 이벤트를 추적할 TrackingManager 인스턴스를 만듭니다.

      `var trackingManager = new s7sdk.TrackingManager();`

   * 다음을 수행하여 구성 요소를 TrackingManager에 연결합니다.

      `s7sdk.Event.SDK_READY` 이벤트 핸들러에서 추적할 구성 요소를 TrackingManager에 연결합니다.

      예를 들어 구성 요소가 `videoPlayer`인 경우

      `trackingManager.attach(videoPlayer);`

      를 클릭하여 trackingManager에 구성 요소를 첨부합니다. 한 페이지에서 여러 뷰어를 추적하려면 여러 추적 관리자 구성 요소를 사용합니다.

   * 다음을 추가하여 AppMeasurementBridge 개체를 만듭니다.

      ```
      var appMeasurementBridge = new AppMeasurementBridge(); appMeasurementBridge.setVideoPlayer(videoPlayer);
      ```

   * 다음을 추가하여 추적 함수를 추가합니다.

      ```
      trackingManager.setCallback(appMeasurementBridge.track, 
       appMeasurementBridge);
      ```
   appMeasurementBridge 객체에는 내장 추적 함수가 있습니다. 그러나 여러 추적 시스템 또는 기타 기능을 지원하기 위해 자체 코드를 제공할 수 있습니다.

<!--    For more information, see *Using the TrackingManager Component* in the *Scene7 HTML5 Viewer SDK User Guide* available for download from [Adobe Developer Connection](https://help.adobe.com/en_US/scene7/using/WSef8d5860223939e2-43dedf7012b792fc1d5-8000.html). -->

## 비디오 {#adding-captions-to-video}에 캡션 추가

단일 비디오 또는 적응형 비디오 집합에 캡션을 추가하여 비디오의 범위를 글로벌 마켓까지 확장할 수 있습니다. 캡션을 추가하면 오디오를 더빙할 필요가 없거나 기본 스피커를 사용하여 각각의 다른 언어에 대한 오디오를 다시 기록할 필요가 없습니다. 비디오가 기록된 언어로 재생됩니다. 다른 언어의 사람들이 오디오 부분을 계속 이해할 수 있도록 외국어 자막이 표시됩니다.

자막은 청각 장애나 청각 장애인이 사용할 수 있도록 자막을 사용하여 접근성을 향상시킵니다.

>[!NOTE]
>
>사용하는 비디오 플레이어는 캡션 표시를 지원해야 합니다.

Dynamic Media에는 캡션 파일을 JSON(JavaScript 개체 표기법) 형식으로 변환하는 기능이 있습니다. 이러한 전환은 JSON 텍스트를 숨김이지만 비디오 전체 스크립트로 웹 페이지에 포함할 수 있음을 의미합니다. 그런 다음 검색 엔진을 통해 컨텐츠를 크롤링하고 색인화하여 비디오를 보다 손쉽게 검색할 수 있게 하고 비디오 컨텐츠에 대한 추가 세부 정보를 고객에게 제공할 수 있습니다.

URL에서 JSON 함수 사용에 대한 자세한 내용은 *Dynamic Media 이미지 제공 및 렌더링 API 도움말*&#x200B;의 [정적(이미지가 아님) 컨텐츠 제공](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/c-serving-static-nonimage-contents.html#image-serving-api)을 참조하십시오.

**비디오에 캡션 또는 자막을 추가하려면 다음을 수행하십시오**.

1. 제3자 응용 프로그램 또는 서비스를 사용하여 비디오 캡션/자막 파일을 만듭니다.

   만드는 파일이 WebVTT(웹 비디오 텍스트 트랙) 표준을 따르는지 확인합니다. 캡션 파일 이름 확장명은 .vtt입니다. WebVTT 캡션 표준에 대한 자세한 내용을 살펴볼 수 있습니다.

   [WebVTT 참조:웹 비디오 텍스트 트랙 형식](https://dev.w3.org/html5/webvtt/)입니다.

   Dynamic Media 외부에서 캡션/자막 파일을 작성하는 데 사용할 수 있는 무료 및 프리미엄 툴과 서비스가 있습니다. 예를 들어 스타일이 없는 간단한 비디오 캡션 파일을 만들려면 다음 무료 온라인 캡션 제작 및 편집 도구를 사용할 수 있습니다.

   [WebVTT 캡션 작성기](https://testdrive-archive.azurewebsites.net/Graphics/CaptionMaker/Default.html)

   최상의 결과를 얻으려면 Internet Explorer 9 이상, Google Chrome 또는 Safari에서 도구를 사용하십시오.

   도구의 **[!UICONTROL 비디오 파일]** URL 입력 필드에서 비디오 파일의 복사한 URL을 붙여 넣은 다음 **[!UICONTROL 로드]**&#x200B;를 클릭합니다. 비디오 파일 자체에 URL을 가져온 다음 비디오 파일의 **[!UICONTROL URL 입력 필드에 붙여 넣을 수 있는 [에셋](/help/assets/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-an-asset)에 대한 URL 얻기를 참조하십시오.]** 그러면 Internet Explorer, Chrome 또는 Safari에서 비디오를 기본적으로 재생할 수 있습니다.

   이제 사이트에서 화면의 지침에 따라 WebVTT 파일을 작성하고 저장합니다. 완료되면 캡션 파일 내용을 복사하여 일반 텍스트 편집기에 붙여 넣은 다음 .vtt 파일 이름 확장자로 저장합니다.

   >[!NOTE]
   >
   >여러 언어로 된 비디오 자막을 전체적으로 지원하려면 WebVTT 표준을 사용하여 지원할 각 언어에 대한 .vtt 파일과 호출을 별도로 만들어야 합니다.

   일반적으로 캡션 VTT 파일의 이름을 비디오 파일과 동일하게 지정하고 -EN, -FR 또는 -DE 등의 언어 로캘에 추가하려고 합니다. 기존 웹 컨텐츠 관리 시스템을 사용하여 비디오 URL의 생성을 자동화하는 데 도움이 됩니다.

1. AEM에서 WebVTT 캡션 파일을 DAM에 업로드합니다.
1. 업로드한 캡션 파일과 연결할 *게시된* 비디오 자산으로 이동합니다.

   URL은 *after* 다음에 *게시된*&#x200B;만 복사할 수 있습니다.

   [자산 게시를 참조하십시오.](/help/assets/publishing-dynamicmedia-assets.md)

1. 다음 중 하나를 수행하십시오.

   * 팝업 비디오 뷰어 환경의 경우 **[!UICONTROL URL을 누릅니다.]** [URL] 대화 상자에서 URL을 선택하여 클립보드로 복사한 다음 URL을 지나 간단한 텍스트 편집기로 복사합니다. 다음 구문과 함께 비디오의 복사된 URL을 추가합니다.

      `&caption=<server_path>/is/content/<path_to_caption.vtt_file,1>`

      캡션 경로의 끝에 있는 `,1`을 참고하십시오. 경로에서 .vtt 파일 이름 확장자 바로 뒤에는 각각 `,1` 또는 `,0`로 설정하여 비디오 플레이어 막대에서 닫힌 캡션 단추를 활성화(켜기) 또는 비활성화(끄기)하는 옵션이 있습니다.

   * 포함된 비디오 뷰어 환경의 경우 **[!UICONTROL 포함 코드를 누릅니다.]** 포함 코드 대화 상자에서 포함 코드를 선택하여 클립보드에 복사한 다음 코드를 간단한 텍스트 편집기에 붙여넣습니다. 다음 구문을 사용하여 복사한 포함 코드를 추가합니다.

      `videoViewer.setParam("caption","<path_to_caption.vtt_file,1>");`

      캡션 경로의 끝에 있는 `,1`을 참고하십시오. 경로에서 .vtt 파일 이름 확장자 바로 뒤에는 각각 `,1` 또는 `,0`로 설정하여 비디오 플레이어 막대에서 닫힌 캡션 단추를 활성화(켜기) 또는 비활성화(끄기)하는 옵션이 있습니다.

## 비디오 {#adding-chapter-markers-to-video}에 장 마커 추가

장 마커를 단일 비디오 또는 응용 비디오 집합에 추가하여 긴 형식의 비디오를 보다 쉽게 보고 탐색할 수 있습니다. 사용자가 비디오를 재생하면 비디오 타임라인에서 장 마커(비디오 스크러버라고도 함)를 클릭하여 관심 영역으로 손쉽게 이동하거나 새로운 컨텐츠, 데모, 자습서 등으로 바로 이동할 수 있습니다.

>[!NOTE]
>
>사용되는 비디오 플레이어는 장 마커 사용을 지원해야 합니다. Dynamic Media 비디오 플레이어는 장(chapter) 마커를 지원하지만 제3자 비디오 플레이어를 사용하는 경우에는 지원하지 않을 수 있습니다.

원하는 경우 비디오 뷰어 사전 설정을 사용하는 대신 장을 사용하여 자신만의 사용자 정의 비디오 뷰어를 만들고 브랜딩할 수 있습니다. 장 탐색을 사용하여 자신의 HTML5 뷰어를 만드는 방법에 대한 지침은 Adobe HTML5 뷰어 SDK API에서 `s7sdk.video.VideoPlayer` 및 `s7sdk.video.VideoScrubber` 클래스의 &quot;수정자를 사용하여 비헤이비어 사용자 정의&quot; 머리글을 참조하십시오. [HTML5 뷰어 SDK API]((https://s7d1.scene7.com/s7sdk/3.10/docs/jsdoc/index.html)) 설명서를 참조하십시오.

<!-- If desired, you can create and brand your own custom video viewer with chapters instead of using a video viewer preset. For instructions on creating your own HTML5 viewer with chapter navigation, in the Adobe Scene7 Viewer SDK for HTML5 guide, reference the heading “Customizing Behavior Using Modifiers” under the classes `s7sdk.video.VideoPlayer` and `s7sdk.video.VideoScrubber`. The Adobe Scene7 Viewer SDK is available as a download from [Adobe Developer Connection](https://help.adobe.com/en_US/scene7/using/WSef8d5860223939e2-43dedf7012b792fc1d5-8000.html). -->

캡션을 만드는 것과 동일한 방식으로 비디오의 장 목록을 만듭니다. 즉, WebVTT 파일을 만듭니다. 그러나 이 파일은 사용 중인 WebVTT 캡션 파일과는 별도로 사용해야 합니다.캡션과 장을 하나의 WebVTT 파일로 결합할 수는 없습니다.

다음 샘플을 장 탐색을 사용하여 WebVTT 파일을 만드는 데 사용하는 형식의 예로 사용할 수 있습니다.

### 비디오 장 탐색 {#webvtt-file-with-video-chapter-navigation}이(가) 있는 WebVTT 파일

```xml
WEBVTT
Chapter 1
00:00.000 --> 01:04.364
The bicycle store behind it all.
Chapter 2
01:04.364 --> 02:00.944
Creative Cloud.
Chapter 3
02:00.944 --> 03:02.937
Ease of management for a working solution.
Chapter 4
03:02.937 --> 03:35.000
Cost-efficient access to rapidly evolving technology.
```

위의 예에서 `Chapter 1`은 큐 식별자이며 선택 사항입니다. `00:00:000 --> 01:04:364`의 큐 시간은 장 시작 시간과 종료 시간을 `00:00:000` 형식으로 지정합니다. 마지막 3자리 숫자는 밀리초 단위이며 원하는 경우 `000`으로 남을 수 있습니다. `The bicycle store behind it all`의 장 제목은 장 내용의 실제 설명입니다. 사용자가 비디오 타임라인에서 시각적 큐 포인트 위로 마우스 포인터를 가져갈 때 비디오 플레이어에서 큐 식별자, 시작 큐 시간 및 장 제목이 모두 팝업에 표시됩니다.

HTML5 비디오 뷰어를 사용하고 있으므로 만드는 장 파일은 WebVTT(Web Video Text Tracks) 표준을 따라야 합니다. 장 파일 이름 확장자는 .vtt입니다. WebVTT 캡션 표준에 대한 자세한 내용을 살펴볼 수 있습니다.

[WebVTT 참조:웹 비디오 텍스트 트랙 형식](https://dev.w3.org/html5/webvtt/)

**비디오에 장 마커를 추가하려면:**

1. 장 제목 텍스트의 문자 변환에 문제가 발생하지 않도록 UTF8 인코딩으로 .vtt 파일을 저장합니다.

   일반적으로 장 VTT 파일의 이름을 비디오 파일과 동일한 이름으로 지정하고 장에 추가하려고 합니다. 기존 웹 컨텐츠 관리 시스템을 사용하여 비디오 URL의 생성을 자동화하는 데 도움이 됩니다.
1. AEM에서 WebVTT 장 파일을 업로드합니다.

   [자산 업로드](/help/assets/manage-assets.md#uploading-assets)를 참조하십시오.

1. 다음 중 하나를 수행하십시오.

   <table>
     <tbody>
      <tr>
       <td>팝업 비디오 뷰어 환경의 경우</td>
       <td>
       <ol>
       <li>업로드한 장 파일과 연결할 <i>게시된 </i>비디오 자산으로 이동합니다. URL은 <i>after</i> 다음에 <i>게시된</i>만 복사할 수 있습니다. <a href="/help/assets/publishing-dynamicmedia-assets.md">자산 게시를 참조하십시오.</a></li>
       <li>드롭다운 메뉴에서 <strong>뷰어</strong>를 클릭하거나 탭합니다.</li>
       <li>왼쪽 레일에서 비디오 뷰어 사전 설정 이름을 탭하거나 클릭합니다. 비디오의 미리 보기가 별도의 페이지에 열립니다.</li>
       <li>왼쪽 레일의 맨 아래에서 <strong>URL</strong>을 클릭합니다.</li>
       <li>URL 대화 상자에서 URL을 선택하여 클립보드에 복사한 다음 URL을 지나 간단한 텍스트 편집기로 복사합니다.</li>
       <li>비디오의 복사된 URL을 다음 구문과 함께 추가하여 복사한 URL을 장 파일에 연결합니다.<br /> <br /> <code>&navigation=<<i>full_copied_URL_path_to_chapter_file</i>.vtt></code><br /> </li>
       </ol> </td>
      </tr>
      <tr>
       <td>포함된 비디오 뷰어 환경의 경우<br /> </td>
       <td>
       <ol>
       <li>업로드한 장 파일과 연결할 <i>게시된 </i>비디오 자산으로 이동합니다. URL은 <i>after</i> 다음에 <i>게시된</i>만 복사할 수 있습니다. <a href="/help/assets/publishing-dynamicmedia-assets.md">자산 게시를 참조하십시오.</a></li>
       <li>드롭다운 메뉴에서 <strong>뷰어</strong>를 클릭하거나 탭합니다.</li>
       <li>왼쪽 레일에서 비디오 뷰어 사전 설정 이름을 탭하거나 클릭합니다. 비디오의 미리 보기가 별도의 페이지에 열립니다.</li>
       <li>왼쪽 레일의 맨 아래에서 <strong>포함</strong>을 클릭합니다.</li>
       <li>포함 코드 대화 상자에서 전체 코드를 선택하여 클립보드에 복사한 다음 간단한 텍스트 편집기에 붙여넣습니다.</li>
       <li>비디오의 포함 코드를 다음 구문과 함께 추가하여 복사한 URL과 장 파일에 연결합니다.<br /> <br /> <code>videoViewer.setParam("navigation","&lt;<i>full_copied_URL_path_to_chapter_file</i>.vtt&gt;"</code></li>
       </ol> </td>
      </tr>
     </tbody>
   </table>

## Dynamic Media의 비디오 축소판 정보 - Scene7 모드 {#about-video-thumbnails-in-dynamic-media-scene-mode}

비디오 축소판은 비디오 프레임 크기를 축소하거나 고객에게 비디오를 나타내는 이미지 에셋입니다. 이 축소판은 고객이 비디오를 클릭하도록 권장하기 위해 사용해야 합니다.

AEM의 모든 비디오에는 연결된 축소판이 있어야 합니다.축소판을 대체하지 않으면 삭제할 수 없습니다. 기본적으로 비디오를 AEM에 업로드할 때 첫 번째 프레임이 축소판으로 사용됩니다. 하지만 예를 들어 브랜딩 또는 시각적 검색을 위해 축소판을 사용자 정의할 수 있습니다. 비디오 축소판을 사용자 정의할 때 사용할 프레임에서 비디오를 재생하고 일시 정지하거나 디지털 자산 관리자에서 이미 업로드한 이미지 에셋과 *게시된*&#x200B;을(를) 선택할 수 있습니다.

비디오에서 선택한 사용자 정의 비디오 축소판 이미지는 DAM에 별도의 에셋으로 추출되어 저장되지 않습니다. 그러나 기존 이미지 자산에서 선택하는 사용자 지정 비디오 축소판은 JCR에 저장됩니다. 선택한 자산의 경로는 다음 예제 경로와 같이 비디오 자산의 노드 아래에 저장됩니다.

`/content/dam/*<folder_name*>/<*video_name*>/jcr:content/manualThumbnail`

비디오 축소판을 사용자 정의하는 기능은 비디오가 있는 폴더에 비디오 프로필을 적용한 후에만 사용할 수 있습니다.

자세한 내용은 [Dynamic Media의 비디오 축소판 정보 - 하이브리드 모드](#about-video-thumbnails-in-dynamic-media-hybrid-mode)를 참조하십시오.

### 사용자 정의 비디오 축소판 {#adding-a-custom-video-thumbnail} 추가

이러한 단계는 &quot;Dynamicmedia_Scene7&quot; 모드에서 실행되는 Dynamic Media에만 적용됩니다.

**사용자 정의 비디오 축소판 추가**,

1. 다음을 이미 수행했는지 확인하십시오.

   * 비디오 에셋에 사용할 폴더를 만들었습니다.
   * [폴더에 비디오 프로필을 적용했습니다](/help/assets/video-profiles.md#applying-a-video-profile-to-folders).

   * [비디오를 폴더에 업로드했습니다](/help/assets/managing-video-assets.md#upload-and-preview-video-assets).

1. 축소판 이미지를 변경할 업로드된 비디오 자산으로 이동합니다.
1. 자산 선택 모드에서 **[!UICONTROL 목록 보기]** 또는 **[!UICONTROL 카드 보기]**&#x200B;에서 비디오 자산을 탭합니다.
1. 도구 모음에서 **[!UICONTROL 속성]** 아이콘(&quot;i&quot;가 포함된 원)을 누릅니다.
1. 비디오의 속성 페이지에서 **[!UICONTROL 축소판 변경을 누릅니다.]**
1. 축소판 변경 페이지에서 다음 중 하나를 수행합니다.

   * 비디오의 프레임을 새 축소판으로 사용하려면:

      * 도구 모음에서 **[!UICONTROL 비디오의 프레임 선택을 누릅니다.]**
      * 재생 버튼을 누른 다음 비디오의 새로운 축소판으로 캡처할 프레임에 있는 일시 정지 버튼을 누릅니다.
   * 이미지 에셋을 새 축소판으로 사용하려면:

      * 도구 모음에서 **[!UICONTROL 자산에서 축소판 선택을 누릅니다.]**
      * **[!UICONTROL 축소판 선택을 누릅니다.]**
      * 사용할 이전에 업로드되고 게시된 이미지 자산으로 이동합니다. 비디오의 축소판 이미지 역할을 위해 에셋 크기가 자동으로 조정됩니다.
      * 이미지 자산을 선택한 다음 **[!UICONTROL 선택을 누릅니다.]**


1. 축소판 변경 페이지에서 **[!UICONTROL 변경 내용 저장을 탭합니다.]**
1. 비디오의 속성 페이지의 오른쪽 위 모서리에서 **[!UICONTROL 저장 및 닫기.]**

## Dynamic Media의 비디오 축소판 정보 - 하이브리드 모드 {#about-video-thumbnails-in-dynamic-media-hybrid-mode}

Dynamic Media에서 자동으로 생성한 10개의 축소판 이미지 중 하나를 선택하여 비디오에 추가할 수 있습니다. 비디오 에셋이 AEM Sites, AEM Mobile 또는 AEM Screens의 작성 환경에서 Dynamic Media 구성 요소와 함께 사용될 경우 비디오 플레이어에 선택한 축소판이 표시됩니다. 축소판은 전체 비디오의 컨텐츠를 가장 잘 나타내는 정적 사진 역할을 하며 사용자가 [재생] 단추를 클릭하도록 합니다.

비디오의 총 시간을 기반으로 Dynamic Media은 10개의 축소판 이미지를 비디오에 1%, 11%, 21%, 31%, 41%, 51%, 61%, 71%, 81% 및 91%로 캡처합니다. 10개의 축소판은 지속되므로 나중에 다른 축소판을 선택하더라도 시리즈를 다시 생성할 필요가 없습니다. 10개의 축소판 이미지를 미리 본 다음 비디오에 사용할 이미지를 선택합니다. 기본값으로 변경하려면 CRXDE Lite을 사용하여 축소판 이미지가 생성되는 시간 간격을 구성할 수 있습니다. 예를 들어 비디오에서 간격을 일정하게 두고 4개의 축소판 이미지만 생성하려는 경우 간격 시간을 24%, 49%, 74% 및 99%로 구성할 수 있습니다.

가장 좋은 방법은 비디오를 업로드한 후 언제든지 비디오 축소판을 추가할 수 있지만 웹 사이트에 비디오를 게시하기 전에 추가합니다.

원하는 경우 Dynamic Media에서 생성된 축소판을 사용하는 대신 사용자 정의 축소판을 업로드하여 비디오를 나타낼 수 있습니다. 예를 들어 비디오의 제목, 시선을 사로잡는 열기 이미지 또는 비디오에서 캡처한 매우 특정 이미지가 있는 사용자 정의 축소판 이미지를 만들 수 있습니다. 업로드하는 사용자 정의 비디오 축소판 이미지는 최대 해상도 1280 x 720픽셀(최소 폭 640픽셀)이며 2MB보다 크지 않아야 합니다.

Dynamic Media - Scene7 모드](/help/assets/video.md#about-video-thumbnails-in-dynamic-media-scene-mode)의 비디오 축소판 정보를 참조하십시오.[

### 비디오 축소판 {#adding-a-video-thumbnail} 추가

이러한 단계는 하이브리드 모드에서 실행되는 Dynamic Media에만 적용됩니다.

T **비디오 축소판 추가**,

1. 비디오 축소판을 추가할 업로드된 비디오 자산으로 이동합니다.
1. 자산 선택 모드에서 목록 보기 또는 카드 보기에서 비디오 자산을 탭합니다.
1. 도구 모음에서 **[!UICONTROL 속성 보기]** 아이콘(&quot;i&quot;가 포함된 원)을 누릅니다.
1. 비디오의 속성 페이지에서 **[!UICONTROL 축소판 변경을 누릅니다.]**
1. 축소판 변경 페이지의 도구 모음에서 **[!UICONTROL 프레임 선택을 누릅니다.]**

   Dynamic Media은 사용자가 지정한 기본 시간 간격 또는 시간 간격에 따라 비디오에서 축소판 이미지를 생성합니다.

1. 생성된 축소판 이미지를 미리 본 다음 비디오에 추가할 이미지를 선택합니다.
1. **[!UICONTROL 변경 내용 저장을 탭합니다.]**

   선택한 축소판을 사용하도록 비디오의 축소판 이미지가 업데이트됩니다. 나중에 축소판 이미지를 변경하기로 결정한 경우 **[!UICONTROL 축소판 변경]** 페이지로 돌아가서 새 이미지를 선택할 수 있습니다.

   새 기본 시간 간격을 구성했거나 기존 비디오를 대체할 새 비디오를 업로드한 경우 Dynamic Media에서 축소판을 다시 생성하도록 해야 합니다.

   [비디오 축소판이 생성되는 기본 시간 간격 구성을 참조하십시오](#configuring-the-default-time-interval-that-video-thumbnails-are-generated).

#### 비디오 축소판이 생성되는 기본 시간 간격 구성 {#configuring-the-default-time-interval-that-video-thumbnails-are-generated}

새 기본 시간 간격을 구성하고 저장할 때 변경 내용은 나중에 업로드하는 비디오에만 자동으로 적용됩니다. 이전에 업로드한 비디오에 새 기본값이 자동으로 적용되지 않습니다. 기존 비디오의 경우 축소판을 다시 생성해야 합니다.

[비디오 축소판 추가](#adding-a-video-thumbnail)를 참조하십시오.

**비디오 축소판이 생성되는 기본 시간 간격을 구성하려면**

1. AEM에서 **[!UICONTROL 도구]** > **[!UICONTROL 일반]** > **[!UICONTROL CRXDE Lite을 탭합니다.]**

1. CRXDE Lite 페이지의 왼쪽에 있는 디렉토리 패널에서 `o etc/dam/imageserver/configuration/jcr:content/settings.`으로 이동합니다.

   디렉토리 패널이 보이지 않으면 [홈] 탭의 왼쪽에 있는 >> 아이콘을 탭해야 할 수 있습니다.

1. 오른쪽 아래 패널의 속성 탭에서 `thumbnailtime`을 두 번 누릅니다.
1. [축소판 편집] 대화 상자에서 텍스트 필드를 사용하여 간격 값을 백분율로 입력합니다.

   * 더하기 기호(+) 아이콘을 눌러 하나 이상의 간격 값 필드를 추가합니다. 아이콘을 보려면 대화 상자 아래쪽으로 스크롤해야 할 수도 있습니다.
   * 간격 값 필드의 오른쪽에 있는 빼기 기호(-) 아이콘을 눌러 목록에서 삭제합니다.
   * 위쪽 화살표 아이콘과 아래쪽 화살표 아이콘을 눌러 간격 값의 순서를 변경합니다.

1. **[!UICONTROL 확인]**&#x200B;을 눌러 속성 탭으로 돌아갑니다.
1. CRXDE Lite 페이지의 왼쪽 위 모서리 근처에 있는 **[!UICONTROL 모두 저장]**&#x200B;을 탭한 다음 왼쪽 위 모서리의 뒤로 홈 아이콘을 눌러 AEM으로 돌아갑니다.

   [비디오 축소판 추가를 참조하십시오.](#adding-a-video-thumbnail)

### 사용자 정의 비디오 축소판 {#adding-a-custom-video-thumbnail-1} 추가

이러한 단계는 하이브리드 모드에서 실행되는 Dynamic Media에만 적용됩니다.

**사용자 정의 비디오 축소판 추가**,

1. 사용자 정의 비디오 축소판을 추가할 업로드된 비디오 자산으로 이동합니다.
1. 자산 선택 모드에서 목록 보기 또는 카드 보기에서 비디오 자산을 탭합니다.
1. 도구 모음에서 **[!UICONTROL 속성 보기]** 아이콘(&quot;i&quot;가 포함된 원)을 누릅니다.
1. 비디오의 속성 페이지에서 **[!UICONTROL 축소판 변경을 누릅니다.]**
1. 축소판 변경 페이지의 도구 모음에서 **[!UICONTROL 새 축소판 업로드를 누릅니다.]**
1. 사용할 축소판 이미지를 탐색하고 선택한 다음 **[!UICONTROL 열기]**&#x200B;를 눌러 AEM에 이미지를 업로드합니다. 업로드를 수행한 후 반드시 이미지를 게시해야 합니다.
1. 이미지를 업로드하고 게시한 후 축소판 변경 페이지에서 **[!UICONTROL 변경 내용 저장을 탭합니다.]**

   사용자 정의 축소판이 비디오에 추가됩니다.

