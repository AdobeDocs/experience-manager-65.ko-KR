---
title: Dynamic Media의 비디오
description: 비디오 인코딩, YouTube에 비디오 게시, 비디오 보고서 보기 우수 사례와 같이 Dynamic Media에서 비디오를 사용하여 작업하는 방법을 알아봅니다. 비디오에 자막, 자막 또는 장 마커를 추가하는 방법도 알아봅니다.
mini-toc-levels: 3
uuid: 97f311a3-a227-479a-91bf-fb54ecd1a55d
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 1103b849-0042-4e11-b170-38ee81dd0157
docset: aem65
feature: Asset Management
role: User, Admin
exl-id: 28cf9e39-cab4-4278-b6c9-e84cc31964db
source-git-commit: c704397f08e163a58ee6ac1dbaefc3171298864e
workflow-type: tm+mt
source-wordcount: '8086'
ht-degree: 3%

---

# Dynamic Media의 비디오 {#video}

이 섹션에서는 Dynamic Media에서 비디오 작업을 설명합니다.

## 빠른 시작: 비디오 {#quick-start-videos}

다음 단계별 워크플로우 설명은 Dynamic Media의 응용 비디오 세트를 빠르게 설정 및 실행하는 데 도움이 되도록 설계되었습니다. 각 단계 후에는 자세한 정보를 찾을 수 있는 주제 제목에 대한 상호 참조가 있습니다.

>[!IMPORTANT]
>
>Dynamic Media에서 비디오를 사용하기 전에 Adobe Experience Manager 관리자가 Dynamic Media - Scene7 모드 또는 Dynamic Media - 하이브리드 모드에서 Dynamic Media Cloud Services을 이미 활성화 및 구성했는지 확인하십시오.
>
>* 자세한 내용은 [Dynamic Media Cloud Services 구성](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services) Dynamic Media 구성 - Scene7 모드 및 [Dynamic Media 문제 해결 - Scene7 모드](/help/assets/troubleshoot-dms7.md).
>
>* 자세한 내용은 [Dynamic Media Cloud Services 구성](/help/assets/config-dynamic.md#configuring-dynamic-media-cloud-services) Dynamic Media 구성 - 하이브리드 모드에서 을 참조하십시오.
>
>현재 Dynamic Media에서 알려진 비디오 재생 문제 *Experience Manager 6.5.9.0에서만*:
>
>* 게시된 비디오가 업데이트되면 게재의 변경 사항을 반영하려면 다시 게시해야 합니다.
>


1. **Dynamic Media 비디오 업로드** 다음을 수행하십시오.

   * 자신만의 비디오 인코딩 프로필을 만듭니다. 또는 사전 정의된 _응용 비디오 인코딩_ Dynamic Media과 함께 제공되는 프로필입니다.

      * [비디오 인코딩 프로필 만들기](/help/assets/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming).
      * 추가 정보 [비디오 인코딩에 대한 우수 사례](#best-practices-for-encoding-videos).
   * 비디오 처리 프로필을 기본 소스 비디오를 업로드할 하나 이상의 폴더에 연결합니다.

      * [폴더에 비디오 프로필 적용](/help/assets/video-profiles.md#applying-a-video-profile-to-folders).
      * 추가 정보 [처리 프로필 사용을 위한 디지털 자산을 구성하는 우수 사례](/help/assets/organize-assets.md).
      * 추가 정보 [디지털 자산 구성](/help/assets/organize-assets.md).
   * 기본 소스 비디오를 폴더에 업로드합니다. 폴더에 비디오를 추가하면 폴더에 할당한 비디오 처리 프로필에 따라 인코딩됩니다.

      * Dynamic Media은 주로 최대 30분 길이의 짧은 비디오와 25x 25보다 큰 최소 해상도를 지원합니다.
      * 각각 최대 15GB의 비디오 파일을 업로드할 수 있습니다.
      * [비디오 업로드](/help/assets/managing-video-assets.md#upload-and-preview-video-assets).
      * 추가 정보 [지원되는 입력 파일 형식](/help/assets/assets-formats.md#supported-multimedia-formats).
   * 모니터링 방법 [비디오 인코딩이 진행 중입니다.](#monitoring-video-encoding-and-youtube-publishing-progress) 자산 또는 워크플로우 보기에서 선택합니다.




1. **Dynamic Media 비디오 관리** 다음을 수행하여 다음을 수행합니다.

   * 비디오 자산 구성, 탐색 및 검색

      * [디지털 자산 구성](/help/assets/organize-assets.md)
추가 정보 [처리 프로필 사용을 위한 디지털 자산을 구성하는 우수 사례](organize-assets.md)

      * [비디오 자산 검색](search-assets.md#custompredicates) 또는 [자산 검색](/help/assets/search-assets.md)
   * 비디오 자산 미리 보기 및 게시

      * 관련 축소판과 함께 비디오의 소스 비디오 및 인코딩된 표현물을 봅니다.
         [비디오 미리 보기](managing-video-assets.md#upload-and-preview-video-assets) 또는 [자산 미리 보기](previewing-assets.md)
         [비디오 표현물 보기](video-renditions.md)
         [비디오 표현물 관리](manage-assets.md#managing-renditions)

      * [뷰어 사전 설정 관리](managing-viewer-presets.md)
      * [자산 게시](publishing-dynamicmedia-assets.md)
   * 비디오 메타데이터 작업

      * 프레임 속도, 오디오 및 비디오 비트율, 코덱과 같은 인코딩된 비디오 표현물의 속성을 봅니다.
         [비디오 표현물 속성 보기](video-renditions.md)

      * 제목, 설명 및 태그, 사용자 지정 메타데이터 필드와 같은 비디오의 속성을 편집합니다.
         [비디오 속성 편집](manage-assets.md#editing-properties)

      * [디지털 자산에 대한 메타데이터 관리](metadata.md)
      * [메타데이터 스키마](metadata-schemas.md)
   * 비디오 검토, 승인 및 주석 달기, 전체 버전 제어 유지

      * [비디오에 주석 달기](managing-video-assets.md#annotate-video-assets) 또는 [자산에 주석 달기](manage-assets.md#annotating)

      * [버전 만들기](manage-assets.md#asset-versioning)
      * [자산에 워크플로우 적용](assets-workflow.md) 또는 [자산에서 워크플로우 시작](manage-assets.md#starting-a-workflow-on-an-asset)

      * [폴더 자산 검토](bulk-approval.md)
      * [프로젝트](../sites-authoring/projects.md)




1. **Dynamic Media 비디오 게시** 다음 중 하나를 수행하여 다음을 수행합니다.

   * Adobe Experience Manager을 웹 컨텐츠 관리 시스템으로 사용하는 경우 웹 페이지에 비디오를 직접 추가할 수 있습니다.

      * [웹 페이지에 비디오 추가](adding-dynamic-media-assets-to-pages.md).
   * 타사 웹 컨텐츠 관리 시스템을 사용하는 경우 웹 페이지에 비디오를 링크하거나 포함할 수 있습니다.

      * URL을 사용하여 비디오 통합:
         [웹 애플리케이션에 URL 연결](linking-urls-to-yourwebapplication.md).

      * 웹 페이지에서 포함 코드를 사용하여 비디오 통합:
         [웹 페이지에 비디오 뷰어 포함](embed-code.md).
   * [비디오 보고서 생성](#viewing-video-reports).

   * [비디오에 캡션 추가](#adding-captions-to-video).



## Dynamic Media에서 비디오를 사용한 작업 {#working-with-video-in-dynamic-media}

Dynamic Media의 비디오는 데스크탑, iOS, Android™, BlackBerry® 및 Windows 모바일 장치를 포함하여 여러 화면에서 스트리밍을 위한 고품질 적응형 비디오를 쉽게 게시할 수 있도록 하는 종단 간 솔루션입니다. 응용 비디오 세트는 다른 비트율 및 형식(예: 400kbps, 800kbps 및 1000kbps)으로 인코딩된 동일한 비디오 버전을 그룹화합니다. 데스크탑 컴퓨터 또는 모바일 장치가 사용 가능한 대역폭을 감지합니다.

예를 들어 iOS 모바일 장치에서 3G, 4G 또는 Wi-Fi와 같은 대역폭을 감지합니다. 그런 다음 응용 비디오 세트 내의 다양한 비디오 비트 전송률 중에서 올바른 인코딩된 비디오를 자동으로 선택합니다. 비디오는 데스크탑, 모바일 장치 또는 태블릿으로 스트리밍됩니다.

또한 데스크탑 또는 모바일 장치에서 네트워크 조건이 변경되면 자동으로 비디오 품질이 전환됩니다. 또한 고객이 데스크탑에서 전체 화면 모드로 전환하면 더 나은 해상도를 사용하여 응용 비디오 세트가 응답하여 고객의 보기 환경을 향상시킵니다. 응용 비디오 세트 사용은 고객이 여러 화면 및 장치에서 Dynamic Media 비디오를 재생할 수 있는 최상의 재생 기능을 제공합니다.

비디오 플레이어에서 재생할 인코딩된 비디오 또는 재생 중에 선택할 인코딩된 비디오를 결정하는 데 사용하는 로직은 다음 알고리즘을 기반으로 합니다.

1. 비디오 플레이어는 플레이어 자체에서 &quot;초기 비트율&quot;에 대해 설정된 값에 가장 가까운 비트율을 기반으로 초기 비디오 조각을 로드합니다.
1. 비디오 플레이어는 다음 기준을 사용하여 대역폭 속도 변경 사항을 기반으로 전환합니다.

   1. 플레이어가 예상 대역폭보다 작거나 같은 가장 높은 대역폭 스트림을 선택합니다.
   1. 플레이어는 사용 가능한 대역폭의 80%만 고려합니다. 그러나, 만약 그것이 전환하고 있다면, 그것은 단지 70%에서 더 보수적인데, 그것은 과대평가하고 즉시 다시 돌아서는 것을 피한다.

알고리즘에 대한 자세한 기술 정보는 [https://android.googlesource.com/platform/frameworks/av/+/master/media/libstagefright/httplive/LiveSession.cpp](https://android.googlesource.com/platform/frameworks/av/+/master/media/libstagefright/httplive/LiveSession.cpp)

단일 비디오 및 응용 비디오 세트를 관리하는 경우 다음과 같이 지원됩니다.

* 다양한 비디오 형식 및 오디오 포맷에서 비디오를 업로드하고 여러 화면에서 재생되도록 비디오를 MP4 H.264 형식으로 인코딩합니다. 사전 정의된 응용 비디오 사전 설정, 단일 비디오 인코딩 사전 설정을 사용하거나 자체 인코딩을 사용자 지정하여 비디오의 품질과 크기를 제어할 수 있습니다.

   * 응용 비디오 세트가 생성되면 MP4 비디오가 포함됩니다.
   * **참고**: 기본/소스 비디오가 응용 비디오 세트에 추가되지 않습니다.

* 모든 HTML 5 비디오 뷰어의 비디오 캡션.
* 비디오 자산을 효율적으로 관리하기 위해 전체 메타데이터 지원을 사용하여 비디오를 구성, 탐색 및 검색할 수 있습니다.
* iPhone, iPad, Android™, BlackBerry® 및 Windows 휴대폰을 비롯한 모바일 장치, 웹, 데스크탑 및 모바일 장치에 응용 비디오 세트를 제공합니다.

응용 비디오 스트리밍은 다양한 iOS 플랫폼에서 지원됩니다. 자세한 내용은 [Dynamic Media 뷰어 참조 안내서](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/c-html5-video-reference.html#video).

Dynamic Media은 MP4 H.264 비디오용 모바일 비디오 재생을 지원합니다. 다음 위치에서 이 비디오 형식을 지원하는 BlackBerry® 장치를 찾을 수 있습니다. [BlackBerry®에서 지원되는 비디오 형식](https://support.blackberry.com/kb/articleDetail?ArticleNumber=000005482).

다음 위치에서 이 비디오 형식을 지원하는 Windows 장치를 찾을 수 있습니다. [Windows Phone 8용 지원되는 미디어 코덱입니다](https://learn.microsoft.com/en-us/windows/uwp/audio-video-camera/supported-codecs)



* 다음을 포함하여 Dynamic Media 비디오 뷰어 사전 설정을 사용하여 비디오를 재생합니다.

   * 단일 비디오 뷰어입니다.
   * 비디오와 이미지 컨텐츠를 모두 결합하는 혼합 미디어 뷰어입니다.

* 브랜딩 요구 사항을 충족하도록 비디오 플레이어를 구성합니다.
* 간단한 URL 또는 포함 코드와 함께 웹 사이트, 모바일 사이트 또는 모바일 애플리케이션에 비디오를 통합합니다.

<!-- See [Dynamic video playback](https://s7d9.scene7.com/s7/uvideo.jsp?asset=GeoRetail/Mop_AVS&config=GeoRetail/Universal_Video1&stageSize=640,480) sample. -->

참조 - [Experience Manager Assets 및 Dynamic Media Classic용 뷰어](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/c-html5-s7-aem-asset-viewers.html#viewers-aem-assets-dmc) 및 [Experience Manager 자산에만 대한 뷰어](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/c-html5-aem-asset-viewers.html#viewers-for-aem-assets-only).

## 우수 사례: HTML 5 비디오 뷰어 사용 {#best-practice-using-the-html-video-viewer}

Dynamic Media HTML5 비디오 뷰어 사전 설정은 강력한 비디오 플레이어입니다. HTML5 비디오 재생과 관련된 많은 일반적인 문제를 방지하기 위해 이 매개 변수를 사용할 수 있습니다. 또한 적응형 비트율 스트리밍 게재 부족 및 제한된 데스크탑 브라우저 도달과 같은 모바일 장치와 관련된 문제가 있습니다.

플레이어의 디자인 측면에서는 표준 웹 개발 도구를 사용하여 비디오 플레이어의 기능을 디자인할 수 있습니다. 예를 들어 HTML5 및 CSS를 사용하여 단추, 컨트롤 및 사용자 지정 포스터 이미지 배경을 디자인하여 고객에게 맞춤형 모양을 만들어 줄 수 있습니다.

뷰어의 재생 측에서 브라우저의 비디오 기능을 자동으로 감지합니다. 그런 다음 적응형 비트율 스트리밍이라고도 하는 HLS(HTTP Live Streaming) 또는 DASH(HTTP를 통한 동적 적응형 스트리밍)를 사용하여 비디오를 제공합니다. 또는 이러한 배달 방법이 없으면 HTML 5 프로그레시브가 대신 사용됩니다.

를 단일 플레이어에 결합하여 다음을 수행합니다.

* HTML 5 및 CSS를 사용하여 재생 구성 요소를 디자인하는 기능
* 포함된 재생 있음
* 브라우저의 기능에 따라 적응형 및 점진적 스트리밍을 사용합니다

리치 미디어 콘텐츠의 범위를 데스크탑 및 모바일 사용자 모두로 확장하고 간소화된 비디오 경험을 제공할 수 있습니다.

참조 - [HTML5 뷰어 정보](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/c-html5-aem-asset-viewers.html#viewers-for-aem-assets-only).

### HTML 5 비디오 뷰어를 사용하여 데스크탑 컴퓨터 및 모바일 장치에서 비디오 재생 {#playback-of-video-on-desktop-computers-and-mobile-devices-using-the-html-video-viewer}

데스크탑 및 모바일 적응형 비디오 스트리밍의 경우 비트율 전환에 사용되는 비디오는 응용 비디오 세트의 모든 MP4 비디오를 기반으로 합니다.

비디오 재생은 DASH 또는 HLS 또는 점진적 비디오 다운로드를 사용하여 발생합니다. 6.0, 6.1 및 6.2와 같은 이전 버전의 Experience Manager에서는 비디오가 HTTP를 통해 스트리밍되었습니다.

Experience Manager 6.3 이상에서는 DM 게이트웨이 서비스 URL이 항상 HTTPS를 사용하므로 비디오가 HTTPS(즉, DASH 또는 HLS)를 통해 스트리밍됩니다. 이 기본 동작에는 고객이 영향을 주지 않습니다. 즉, 비디오 스트리밍은 브라우저가 지원하지 않는 한 항상 HTTPS를 통해 발생합니다. (다음 표를 참조하십시오.) 따라서,

* HTTPS 비디오 스트리밍이 있는 HTTPS 웹 사이트가 있는 경우 스트리밍이 좋습니다.
* HTTPS 비디오 스트리밍이 있는 HTTP 웹 사이트가 있는 경우 스트리밍이 문제가 해결되고 웹 브라우저에서 혼합 콘텐츠 문제가 발생하지 않습니다.

DASH는 국제 표준이며 HLS는 Apple 표준입니다. 둘 다 응용 비디오 스트리밍에 사용됩니다. 또한 두 기술 모두 네트워크 대역폭 용량에 따라 재생을 자동으로 조정합니다. 또한 고객이 나머지 비디오가 다운로드될 때까지 기다릴 필요 없이 비디오의 모든 지점을 &quot;찾기&quot;할 수 있습니다.

점진적 비디오는 사용자의 데스크탑 시스템 또는 모바일 장치에 로컬로 비디오를 다운로드하여 저장하여 전달됩니다.

다음 표에서는 Dynamic Media Video Viewer를 사용하는 데스크톱 컴퓨터 및 모바일 장치에서 비디오의 장치, 브라우저 및 재생 방법에 대해 설명합니다.

<table>
 <tbody>
  <tr>
   <td><strong>장치</strong></td>
   <td><strong>브라우저</strong></td>
   <td><strong>비디오 재생 모드</strong></td>
  </tr>
  <tr>
   <td>데스크탑</td>
   <td>Internet Explorer 9 및 10</td>
   <td>점진적 다운로드.</td>
  </tr>
  <tr>
   <td>데스크탑</td>
   <td>Internet Explorer 11+</td>
   <td>Windows 8 및 Windows 10의 경우 - DASH* 또는 HLS가 요청될 때마다 HTTPS를 강제로 사용합니다. 알려진 제한 사항: DASH* 또는 HLS의 HTTP가 이 브라우저/운영 체제 조합에서 작동하지 않습니다<br /> <br /> Windows 7 - Progressive 다운로드의 경우. HTTP 및 HTTPS 프로토콜을 선택하는 표준 로직을 사용합니다.</td>
  </tr>
  <tr>
   <td>데스크탑</td>
   <td>Firefox 23-44</td>
   <td>점진적 다운로드.</td>
  </tr>
  <tr>
   <td>데스크탑</td>
   <td>Firefox 45 이상</td>
   <td>DASH* 또는 HLS 응용 비트율 스트리밍입니다.</td>
  </tr>
  <tr>
   <td>데스크탑</td>
   <td>Chrome</td>
   <td>DASH* 또는 HLS 응용 비트율 스트리밍입니다.</td>
  </tr>
  <tr>
   <td>데스크탑</td>
   <td>Safari(Mac)</td>
   <td>HLS 적응형 비트율 스트리밍.</td>
  </tr>
  <tr>
   <td>모바일</td>
   <td>Chrome(Android™ 6 이하)</td>
   <td>점진적 다운로드.</td>
  </tr>
  <tr>
   <td>모바일</td>
   <td>Chrome(Android™ 7 이상)</td>
   <td>DASH* 또는 HLS 응용 비트율 스트리밍입니다.</td>
  </tr>
  <tr>
   <td>모바일</td>
   <td>Android™(기본 브라우저)</td>
   <td>점진적 다운로드.</td>
  </tr>
  <tr>
   <td>모바일</td>
   <td>Safari(iOS)</td>
   <td>HLS 적응형 비트율 스트리밍.</td>
  </tr>
  <tr>
   <td>모바일</td>
   <td>Chrome(iOS)</td>
   <td>HLS 적응형 비트율 스트리밍.</td>
  </tr>
  <tr>
   <td>모바일</td>
   <td>BlackBerry®</td>
   <td>DASH* 또는 HLS 응용 비트율 스트리밍입니다./td&gt;
  </tr>
 </tbody>
</table>

>[!IMPORTANT]
>
>*비디오에 DASH를 사용하려면 먼저 계정에 대한 Adobe 기술 지원 팀에서 DASH를 활성화해야 합니다. 자세한 내용은 [계정에서 DASH 사용](#enable-dash).

## Dynamic Media 비디오 솔루션 아키텍처 {#architecture-of-dynamic-media-video-solution}

다음 그래픽은 DMGateway(Dynamic Media Hybrid 모드)를 통해 업로드 및 인코딩되고 공개 소비에 사용할 수 있는 비디오의 전체 작성 워크플로우를 보여줍니다.

![chlimage_1-427](assets/chlimage_1-427.png)

## 비디오용 하이브리드 게시 아키텍처 {#hybrid-publishing-architecture-for-videos}

![chlimage_1-428](assets/chlimage_1-428.png)

## 비디오 인코딩 우수 사례 {#best-practices-for-encoding-videos}

다음 **Dynamic Media 인코딩 비디오** Dynamic Media을 활성화하고 video cloud 서비스를 설정한 경우 워크플로우가 비디오를 인코딩합니다. This workflow captures workflow process history and failure information. Dynamic Media을 활성화하고 비디오 클라우드 서비스를 설정한 경우, **[!UICONTROL Dynamic Media 인코딩 비디오]** 워크플로우는 비디오를 업로드할 때 자동으로 적용됩니다. (Dynamic Media을 사용하지 않는 경우, **[!UICONTROL DAM 자산 업데이트]** 워크플로우가 적용됩니다.)

<!-- DEAD The following are best-practice tips for encoding source video files.

For advice about video encoding, see [Video Encoding Basics](https://www.adobe.com/go/learn_s7_encoding_en).

* [Streaming 101: The Basics — Codecs, Bandwidth, Data Rate, and Resolution](https://www.adobe.com/go/learn_s7_streaming101_en). -->

### 소스 비디오 파일 {#source-video-files}

비디오 파일을 인코딩할 때 가능한 가장 높은 품질의 소스 비디오 파일을 사용하십시오. 이전에 인코딩된 비디오 파일은 이미 압축되었으므로 해당 파일을 사용하지 마십시오. 또한 인코딩을 통해 하위 품질의 비디오가 생성됩니다.

* Dynamic Media은 주로 최대 30분 길이의 짧은 비디오와 25x 25보다 큰 최소 해상도를 지원합니다.
* 각각 최대 15GB의 기본 소스 비디오 파일을 업로드할 수 있습니다.

다음 표에서는 소스 비디오 파일을 인코딩하기 전에 사용해야 하는 권장 크기, 종횡비 및 최소 비트 전송률에 대해 설명합니다.

| 크기 | 종횡비 | 최소 비트 전송률 |
|--- |--- |--- |
| 1024 X 768 | 4:3 | 대부분의 비디오에는 4500kbps입니다. |
| 1280 X 720 | 16:9 | 3000 - 6000kbps(비디오의 동작 양에 따라 다름) |
| 1920 X 1080 | 16:9 | 6000 - 8000kbps(비디오의 동작 양에 따라 다름) |

### 파일의 메타데이터 가져오기 {#obtaining-a-file-s-metadata}

비디오 편집 도구를 사용하여 파일의 메타데이터를 보거나 메타데이터를 얻기 위해 디자인된 응용 프로그램을 사용하여 파일의 메타데이터를 가져올 수 있습니다. 다음은 타사 응용 프로그램인 MediaInfo를 사용하여 비디오 파일의 메타데이터를 가져오는 방법에 대한 지침입니다.

1. 이동 [MediaInfo 다운로드](https://mediaarea.net/en/MediaInfo/Download).
1. GUI 버전에 대한 설치 프로그램을 선택하여 다운로드하고 설치 지침을 따르십시오.
1. 설치 후 비디오 파일(Windows만 해당)을 마우스 오른쪽 단추로 클릭하고 MediaInfo를 선택하거나 MediaInfo를 열고 비디오 파일을 응용 프로그램으로 드래그합니다. 너비, 높이, fps 등 비디오 파일과 관련된 모든 메타데이터가 표시됩니다.

### 종횡비 {#aspect-ratio}

기본 소스 비디오 파일에 대한 비디오 인코딩 사전 설정을 선택하거나 만들 때는 사전 설정이 기본 소스 비디오 파일과 동일한 종횡비인지 확인하십시오. 종횡비는 비디오 높이에 대한 너비의 비율입니다.

비디오 파일의 종횡비를 결정하려면 파일의 메타데이터를 가져와서 파일의 폭과 높이를 확인합니다(위의 파일 메타데이터 가져오기 참조). 다음 공식을 사용하여 종횡비를 확인합니다.

너비/높이 = 종횡비

다음 표에서는 공식 결과가 일반적인 종횡비 선택 사항으로 변환되는 방법을 설명합니다.

| 수식 결과 | 종횡비 |
|--- |--- |
| 1.33 | 4:3 |
| 0.75 | 3:4 |
| 1.78 | 16:9 |
| 0.56 | 9:16 |

예를 들어, 1440 너비 x 1080 높이의 비디오에는 1440/1080 또는 1.33의 종횡비가 있습니다. 이 경우 4:3 종횡비가 있는 비디오 인코딩 사전 설정을 선택하여 비디오 파일을 인코딩합니다.

### 비트율 {#bitrate}

비트율은 비디오 재생 1초를 구성하기 위해 인코딩된 데이터의 양입니다. 비트율은 초당 킬로비트(Kbps)로 측정됩니다.

>[!NOTE]
>
>모든 코덱에서는 손실 압축을 사용하므로 비디오 품질에서 비트율이 가장 중요합니다. 손실 압축을 사용하면 비디오 파일을 압축할수록 품질이 더 저하됩니다. 따라서 다른 모든 특성(해상도, 프레임 속도 및 코덱은)은 비트율이 낮을수록 압축 파일의 품질이 낮습니다.

비트율 인코딩을 선택할 때 두 가지 유형을 선택할 수 있습니다.

* **[!UICONTROL 상수 비트율 인코딩]** (CBR) - CBR 인코딩 중에 비트율 또는 초당 비트 수가 인코딩 프로세스 전체에서 동일하게 유지됩니다. CBR 인코딩은 전체 비디오에서 설정에 설정된 데이터 속도를 유지합니다. 또한 CBR 인코딩은 품질을 위해 미디어 파일을 최적화하지는 않지만 저장 공간에 저장합니다.
비디오가 전체 비디오 전체에서 유사한 동작 수준을 포함하는 경우 CBR을 사용합니다. CBR은 비디오 컨텐츠를 스트리밍하는 데 가장 일반적으로 사용됩니다. 참조 - [사용자가 추가한 비디오 인코딩 매개 변수 사용](/help/assets/video-profiles.md#using-custom-added-video-encoding-parameters).

* **[!UICONTROL 변수 비트율 인코딩]** (VBR) - VBR 인코딩은 압축기에 필요한 데이터를 기반으로 사용자가 설정한 상한과 데이터 속도를 조절합니다. 이 기능은 VBR 인코딩 프로세스 중에 미디어 파일의 비트율이 미디어 파일 비트율 요구 사항에 따라 동적으로 증가 또는 감소함을 의미합니다.
VBR은 인코딩하는 데 더 오래 걸리지만 가장 유리한 결과를 생성합니다. 미디어 파일의 품질이 우수합니다. VBR은 비디오 컨텐츠의 http 점진적 게재에 가장 일반적으로 사용됩니다.

VBR 대 CRB는 언제 사용합니까?
VBR과 CBR을 선택할 때는 미디어 파일에 VBR을 사용하는 것이 좋습니다. VBR은 경쟁적 비트율로 고품질의 파일을 제공합니다. VBR을 사용하는 경우 2단계 인코딩에 사용하고 최대 비트율을 대상 비디오 비트율의 1.5배로 설정하십시오.

비디오 인코딩 사전 설정을 선택하는 경우 대상 최종 사용자의 연결 속도를 기억하십시오. 해당 속도의 80%인 데이터 비율이 있는 사전 설정을 선택합니다. 예를 들어 대상 최종 사용자의 연결 속도가 1000Kbps인 경우 가장 좋은 사전 설정은 비디오 데이터 속도가 800Kbps인 사전 설정입니다.

이 표에서는 일반적인 연결 속도의 데이터 속도를 설명합니다.

| 속도(Kbps) | 연결 유형 |
|--- |--- |
| 256 | 전화 접속 연결입니다. |
| 800 | 일반적인 모바일 연결. 이 연결의 경우 3G 경험에 대해 400~최대 800 범위의 데이터 전송률을 타깃팅하십시오. |
| 2000 | 일반 광대역 데스크탑 연결. 이 연결의 경우 평균 1200-1500Kbps로 800-2000Kbps 범위의 데이터 속도를 타깃팅합니다. |
| 5000 | 일반적인 고속 광대역 연결 대부분의 소비자는 이 속도로 비디오를 전달할 수 없으므로 이 상위 범위의 인코딩을 사용하지 않는 것이 좋습니다. |

### 해결 {#resolution}

**해결 방법** 비디오 파일의 높이 및 너비를 픽셀 단위로 설명합니다. 대부분의 소스 비디오는 고해상도(예: 1920 x 1080)로 저장됩니다. 스트리밍을 위해 소스 비디오는 더 작은 해상도(640 x 480 이하)로 압축됩니다.

해상도 및 데이터 전송률은 비디오 품질을 결정하는 두 가지 통합 연결 요소입니다. 동일한 비디오 품질을 유지하려면 비디오 파일의 픽셀 수가 많을수록 해상도가 높을수록 데이터 속도가 빨라야 합니다. 예를 들어, 320 x 240 해상도와 640 x 480 해상도 비디오 파일에서 프레임당 픽셀 수를 고려해 보십시오.

| 해결 | 프레임당 픽셀 수 |
|--- |--- |
| 320 x 240 | 76,800 |
| 640 x 480 | 307,200 |

640 x 480 파일은 프레임당 4배 더 많은 픽셀을 가지고 있습니다. 이러한 두 가지 예제 해상도에 대해 동일한 데이터 속도를 구현하려면 640 x 480 파일에 4배 압축을 적용하여 비디오 품질을 줄일 수 있습니다. 따라서, 비디오 데이터 속도가 250Kbps이면 320 x 240 해상도로 고품질로 볼 수 있지만, 640 x 480 해상도에서는 볼 수 없습니다.

일반적으로 데이터 속도가 높을수록 비디오가 더 잘 보이고 해상도가 높을수록 보기 품질이 유지되어야 하는 데이터 비율이 높습니다(해상도가 낮은 것과 비교하여).

해상도와 데이터 전송률이 연결되어 있으므로 비디오를 인코딩할 때 두 가지 옵션이 있습니다.

* 데이터 비율을 선택한 다음 선택한 데이터 전송률에 적합한 최고 해상도로 인코딩하십시오.
* 해상도를 선택한 다음 선택한 해상도로 고품질의 비디오를 구현하는 데 필요한 데이터 속도로 인코딩하십시오.

기본 소스 비디오 파일에 대한 비디오 인코딩 사전 설정을 선택(또는 생성)할 때 이 표를 사용하여 올바른 해상도를 타깃팅하십시오.

| 해결 | 높이(픽셀) | 화면 크기 |
|--- |--- |--- |
| 240p | 240 | 작은 화면 |
| 300p | 300 | 일반적으로 모바일 장치용 작은 화면 |
| 360p | 360 | 작은 화면 |
| 480p | 480 | 미디어 화면 |
| 720p | 720 | 대형 화면 |
| 1080p | 1080 | HD 대형 화면 |

### Fps(초당 프레임 수) {#fps-frames-per-second}

미국 및 일본에서는 대부분의 비디오가 초당 29.97프레임(fps)으로 촬영됩니다. 유럽에서는 대부분의 비디오가 25fps로 촬영됩니다. 필름은 24fps로 촬영됩니다.

기본 소스 비디오 파일의 fps 속도와 일치하는 비디오 인코딩 사전 설정을 선택합니다. 예를 들어 기본 소스 비디오가 25fps인 경우 25fps로 인코딩 사전 설정을 선택합니다. 기본적으로 모든 사용자 지정 인코딩은 기본 소스 비디오 파일의 fps를 사용합니다. 따라서 비디오 인코딩 사전 설정을 만들 때 fps 설정을 명시적으로 지정할 필요가 없습니다.

### 비디오 인코딩 차원 {#video-encoding-dimensions}

최적의 결과를 얻으려면 인코딩 차원을 선택하면 소스 비디오가 인코딩된 모든 비디오의 전체 배수입니다.

이 비율을 계산하려면 소스 너비를 인코딩된 너비로 나누어 너비 비율을 가져옵니다. 그런 다음 소스 높이를 인코딩된 높이로 나눈 뒤 높이 비율을 얻습니다.

결과 비율이 전체 정수인 경우 비디오 크기가 최적으로 조절됩니다. 결과 비율이 정수가 아닌 경우, 나머지 픽셀 가공물을 화면에 남겨 두면 비디오 품질에 영향을 줍니다. 이 효과는 비디오에 텍스트가 있을 때 가장 잘 보입니다.

예를 들어 소스 비디오가 1920 x 1080이라고 가정합니다. 다음 표에서 세 개의 인코딩된 비디오는 사용할 최적의 인코딩 설정을 제공합니다.

| 비디오 유형 | 너비 x 높이 | 폭 비율 | 높이 비율 |
|--- |--- |--- |--- |
| 소스 | 1920x1080 | 1 | 1 |
| 인코딩됨 | 960 x 540 | 2 | 2 |
| 인코딩됨 | 640 x 360 | 3 | 3 |
| 인코딩됨 | 480 x 270 | 4 | 4 |

### 인코딩된 비디오 파일 형식 {#encoded-video-file-format}

Dynamic Media에서는 MP4 H.264 비디오 인코딩 사전 설정을 사용하는 것이 좋습니다. MP4 파일은 H.264 비디오 코덱을 사용하기 때문에 고품질의 비디오를 제공하지만 압축된 파일 크기로 제공합니다.

### 계정에서 DASH 사용 {#enable-dash}

DASH(Digital Adaptive Streaming over HTTP)는 비디오 스트리밍을 위한 국제 표준이며, 다양한 비디오 뷰어에서 광범위하게 채택됩니다. 계정에 DASH가 활성화되면 응용 비디오 스트리밍을 위한 DASH 또는 HLS에서 선택할 수 있는 옵션이 제공됩니다. 또는 플레이어 간에 자동 전환을 선택할 수 있습니다. **[!UICONTROL 자동]** 뷰어 사전 설정에서 재생 유형으로 선택됩니다.

계정에서 DASH를 활성화하면 다음과 같은 주요 이점이 있습니다.

* 적응형 비트율 스트리밍을 위한 DASH 스트림 비디오를 패키지화합니다. 이 방법을 사용하면 전달 효율성이 향상됩니다. 적응형 스트리밍을 통해 고객에게 최상의 시청 경험을 제공합니다.
* Dynamic Media 플레이어에서 최적화된 스트리밍은 HLS와 DASH 스트리밍 간에 전환되므로 최상의 서비스 품질을 보장합니다. Safari 브라우저를 사용하면 비디오 플레이어가 HLS로 자동 전환됩니다.
* 비디오 뷰어 사전 설정을 편집하여 선호하는 스트리밍 방법(HLS 또는 DASH)을 구성할 수 있습니다.
* 최적화된 비디오 인코딩을 통해 DASH 기능을 활성화하는 동안 추가 스토리지를 사용하지 않습니다. HLS 및 DASH 모두에 대해 하나의 비디오 코드 세트가 생성되어 비디오 저장 비용을 최적화합니다.
* 고객이 보다 쉽게 비디오를 게재할 수 있도록 지원합니다.
* API를 통해 스트리밍 URL도 가져옵니다.

   >[!IMPORTANT]
   >
   >현재 계정의 DASH 활성화는 아시아 태평양 및 북아메리카에서만 사용할 수 있습니다. 곧 유럽-중동-아프리카에 도착합니다.

계정에서 DASH를 활성화하려면 다음 두 단계가 필요합니다.

* DASH를 사용하도록 Dynamic Media 구성 을 직접 수행할 수 있습니다.
* DASH를 사용하도록 Experience Manager 6.5를 구성하되, 이 작업은 사용자가 만들고 제출하는 Adobe 고객 지원 사례를 통해 수행됩니다.

**계정에서 DASH를 사용하려면**

1. **Dynamic Media 구성** - Experience Manager 6.5의 Dynamic Media에서 [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
1. 검색 대상 **AEM Assets Dynamic Media Video Advanced Streaming** 기능 플래그.
1. DASH를 활성화(켜기)하려면 확인란을 선택합니다.
1. **[!UICONTROL 저장]**&#x200B;을 선택합니다.
1. **Experience Manager 6.5 구성** - [Admin Console을 사용하여 새 지원 사례 만들기를 시작합니다](https://helpx.adobe.com/kr/enterprise/using/support-for-experience-cloud.html).
1. 다음 정보를 제공하는지 확인하면서 지원 사례를 만들려면 지침을 따르십시오.

   * 기본 연락처 이름, 이메일, 전화
   * Dynamic Media 계정 이름입니다.
   * Experience Manager 6.5에서 DASH를 활성화하도록 지정합니다.

1. Adobe 고객 지원에서는 요청을 제출하는 순서에 따라 DASH 고객 대기 목록에 사용자를 추가합니다.
1. Adobe이 요청을 처리할 준비가 되면 고객 지원에서 DASH 활성화를 위한 대상 날짜를 조정하고 설정할 수 있도록 사용자에게 연락합니다.
1. 고객 지원 센터에서 완료 후 알림을 받습니다.
1. 만들기 [비디오 뷰어 사전 설정](/help/assets/managing-viewer-presets.md#creating-a-new-viewer-preset) 평소대로요

## 비디오 보고서 보기 {#viewing-video-reports}

>[!NOTE]
>
>비디오 보고서는 Dynamic Media - 하이브리드 모드를 실행하는 경우에만 사용할 수 있습니다.

비디오 보고서에는 특정 시간 동안 몇 개의 집계 지표가 표시되어 해당 지표를 모니터링할 수 있습니다 *게시됨* 개별 및 집계 비디오가 예상대로 작동하는지 확인합니다. 다음 상위 지표 데이터는 전체 웹 사이트에서 게시된 모든 비디오에 대해 집계됩니다.

* 비디오 시작
* 완료율
* 비디오의 평균 시간
* 비디오의 총 시간
* 방문당 비디오 수

테이블 *게시됨* 비디오도 나열되므로 총 비디오 시작을 기반으로 웹 사이트에서 가장 많이 본 비디오를 추적할 수 있습니다.

목록에서 비디오 이름을 탭하면 비디오의 대상 유지(드롭다운) 보고서가 라인 차트 형태로 표시됩니다. 차트는 비디오 재생 중 지정된 시간 동안의 보기 수를 표시합니다. 비디오를 재생하면 세로 막대가 플레이어의 시간 표시기와 동기식으로 추적합니다. 라인 차트 데이터의 드롭은 대상이 관심 영역에서 이탈하는 위치를 나타냅니다.

비디오가 Adobe Experience Manager Dynamic Media 외부에 인코딩된 경우 대상 유지(드롭다운) 차트와 테이블의 재생 비율 데이터를 사용할 수 없습니다.

참조 - [Dynamic Media Cloud Services 구성](/help/assets/config-dynamic.md).

>[!NOTE]
>
>추적 및 보고 데이터는 Dynamic Media의 자체 비디오 플레이어 및 관련 비디오 플레이어 사전 설정의 사용만을 기반으로 합니다. 따라서 다른 비디오 플레이어로 재생되는 비디오를 추적하고 보고할 수 없습니다.

기본적으로 비디오 보고서를 처음 입력할 때 이 보고서는 현재 달 1일에 시작하여 현재 월의 날짜로 끝나는 비디오 데이터를 표시합니다. 그러나 고유한 날짜 범위를 지정하여 기본 날짜 범위를 무시할 수 있습니다. 다음에 비디오 보고서를 입력할 때 지정한 날짜 범위가 사용됩니다.

비디오 보고서가 올바르게 작동하려면 Dynamic Media Cloud Services이 구성되면 보고서 세트 ID가 자동으로 생성됩니다. 동시에 보고서 세트 ID가 게시 서버로 푸시되어 자산을 미리 볼 때 URL 복사 기능에 사용할 수 있습니다. 그러나 이 기능을 사용하려면 게시 서버가 이미 설정되어 있어야 합니다. 게시 서버가 설정되지 않은 경우에는 여전히 게시하여 비디오 보고서를 볼 수 있습니다. 그러나 Dynamic Media Cloud 구성으로 돌아가 다음을 탭해야 합니다 **[!UICONTROL 확인]**.

**비디오 보고서를 보려면 다음을 수행하십시오.**

1. Experience Manager의 왼쪽 위 모서리에서 Experience Manager 로고를 탭한 다음 왼쪽 레일에서 를 탭합니다 **[!UICONTROL 도구]** (망치 아이콘) > **[!UICONTROL 자산]** > **[!UICONTROL 비디오 보고서]**.
1. 비디오 보고서 페이지에서 다음 중 하나를 수행합니다.

   * 오른쪽 위 모서리 근처에 있는 **비디오 보고서 새로 고침** 아이콘.
보고서의 종료 날짜가 현재 날짜인 경우에만 새로 고침을 사용합니다. 이렇게 하면 보고서를 마지막으로 실행한 이후 발생한 비디오 추적이 표시됩니다.

   * 오른쪽 위 모서리 근처에 있는 **날짜 선택기** 아이콘.
비디오 데이터를 저장할 시작 날짜 및 종료 날짜 범위를 지정한 다음 탭합니다 **[!UICONTROL 보고서 실행]**.

   상위 지표 그룹 상자는 모든 지표에 대한 다양한 집계 측정을 식별합니다 *게시됨* 사이트 전체에서 비디오를 업로드합니다.

1. 게시된 상위 비디오를 나열하는 테이블에서 비디오 이름을 탭하여 비디오를 재생하고 비디오의 대상 유지(드롭다운) 보고서를 볼 수 있습니다.

### Dynamic Media HTML5 Viewer SDK를 사용하여 만든 비디오 뷰어를 기반으로 비디오 보고서를 봅니다 {#viewing-video-reports-based-on-a-video-viewer-that-you-created-using-the-scene-hmtl-viewer-sdk}

Dynamic Media에서 제공하는 기본 비디오 뷰어를 사용하거나 기본 비디오 뷰어를 기반으로 사용자 지정 뷰어 사전 설정을 만든 경우 비디오 보고서를 보는 데 추가 단계가 필요하지 않습니다. 그러나 HTML5 Viewer SDK API를 기반으로 자체 비디오 뷰어를 만든 경우 다음 단계를 사용하여 비디오 뷰어가 추적 이벤트를 Dynamic Media 비디오 보고서에 전송하는지 확인합니다.

를 사용하십시오 [Adobe Dynamic Media 뷰어 참조 안내서](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources.html) 그리고 [HTML5 뷰어 SDK API](https://s7d1.scene7.com/s7sdk/3.10/docs/jsdoc/index.html) 자신의 비디오 뷰어를 만들 수 있습니다.

**Dynamic Media HTML5 Viewer SDK를 사용하여 만든 비디오 뷰어를 기반으로 한 비디오 보고서를 보려면 다음을 수행하십시오.**

1. 게시된 비디오 자산으로 이동합니다.
1. Near the upper-left corner of the asset&#39;s page, from the drop-down list, select **[!UICONTROL Viewers]**.
1. 비디오 뷰어 사전 설정을 선택하고 포함 코드를 복사합니다.
1. 포함 코드에서 다음을 사용하여 줄을 찾습니다.

   `videoViewer.setParam("config2", "<value>");`

   다음 `config2` 매개 변수를 사용하면 HTML5 뷰어에서 추적을 사용할 수 있습니다. 또한 비디오 보고 및 고객별 Adobe Analytics 구성에 대한 구성 정보가 포함된 회사별 사전 설정입니다.

   The correct value for the config2 parameter is found in both the **[!UICONTROL Embed Code]** and in the copy **[!UICONTROL URL]** function. In the URL from the copy **[!UICONTROL URL]** command, the parameter to look for is `&config2=<value>` . The value is almost always `companypreset`, but in some instances it can also be `companypreset-1`, `companypreset-2`, and so forth.

1. 사용자 지정 비디오 뷰어 코드에서 다음을 수행하여 뷰어 페이지에 AppMeasurementBridge.jsp를 추가합니다.

   * 먼저, `&preset` 매개 변수.

      만약 `config2` 매개 변수: `companypreset`, 다음을 수행합니다. *not* 필요 `&preset=parameter`.

      If `config2` 이 아니면 사전 설정 매개 변수를 와 동일하게 설정합니다. `config2` 매개 변수. 예를 들어 `config2=companypreset-2`, 추가 `&param2=companypreset-2` at.js 또는 AppMeasurementBridge.jsp URL로 마이그레이션

   * 그런 다음 AppMeasurementBridge.jsp 스크립트를 추가합니다.

      `<script language="javascript" type="text/javascript" src="https://s7d1.scene7.com/s7viewers/AppMeasurementBridge.jsp?company=robindallas&preset=companypreset-2"></script>`

1. 다음을 수행하여 TrackingManager 구성 요소를 만듭니다.

   * 전화한 후 `s7sdk.Util.init();`를 채울 때 다음을 추가하여 이벤트를 추적할 TrackingManager 인스턴스를 만듭니다.

      `var trackingManager = new s7sdk.TrackingManager();`

   * 다음을 수행하여 구성 요소를 TrackingManager에 연결합니다.

      에서 `s7sdk.Event.SDK_READY` 이벤트 처리기에서 추적할 구성 요소를 TrackingManager에 연결합니다.

      예를 들어, 구성 요소가 `videoPlayer`, 추가

      `trackingManager.attach(videoPlayer);`

      trackingManager에 구성 요소를 첨부하기 위해 페이지에서 여러 뷰어를 추적하려면 여러 추적 관리자 구성 요소를 사용합니다.

   * 다음을 추가하여 AppMeasurementBridge 개체를 만듭니다.

      ```
      var appMeasurementBridge = new AppMeasurementBridge(); appMeasurementBridge.setVideoPlayer(videoPlayer);
      ```

   * 다음을 추가하여 추적 함수를 추가합니다.

      ```
      trackingManager.setCallback(appMeasurementBridge.track, 
       appMeasurementBridge);
      ```
   appMeasurementBridge 개체에는 내장된 추적 함수가 있습니다. 그러나 여러 추적 시스템 또는 기타 기능을 지원하도록 자체 코드를 제공할 수 있습니다.

<!--    For more information, see *Using the TrackingManager Component* in the *Scene7 HTML5 Viewer SDK User Guide* available for download from [Adobe Developer Connection](https://help.adobe.com/en_US/scene7/using/WSef8d5860223939e2-43dedf7012b792fc1d5-8000.html). -->

## 비디오에 자막 또는 자막 추가 {#adding-captions-to-video}

단일 비디오나 응용 비디오 세트에 자막을 추가하여 비디오의 범위를 글로벌 마켓플레이스로 확장할 수 있습니다. 자막을 추가하면 오디오를 더하거나 각 다른 언어에 대해 오디오를 다시 녹음하기 위해 기본 스피커를 사용할 필요가 없습니다. 비디오는 녹음된 언어로 재생됩니다. 외국어 자막이 나타나므로 다른 언어를 사용하는 사람들이 오디오 부분을 계속 이해할 수 있습니다.

또한 자막은 청각 장애나 청각 장애가 있는 사람이 더 쉽게 액세스할 수 있도록 해줍니다.

>[!NOTE]
>
>사용하는 비디오 플레이어는 캡션 표시를 지원해야 합니다.

참조 - [Dynamic Media의 접근성](/help/assets/accessibility-dm.md).

Dynamic Media은 캡션 파일을 JSON(JavaScript 개체 표기법) 형식으로 변환합니다. 이 전환은 JSON 텍스트를 비디오의 숨겨진 완전한 텍스트 로 웹 페이지에 포함할 수 있음을 의미합니다. 그런 다음 검색 엔진은 컨텐츠를 크롤링하고 색인화하여 비디오를 보다 손쉽게 검색할 수 있게 만들고 고객에게 비디오 컨텐츠에 대한 추가 세부 사항을 제공할 수 있습니다.

자세한 내용은 [정적(비이미지) 콘텐츠 제공](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/c-serving-static-nonimage-contents.html#image-serving-api) 에서 *Dynamic Media 이미지 제공 및 렌더링 API 도움말* 를 참조하십시오.

**비디오에 캡션 또는 자막을 추가하려면**

1. 타사 응용 프로그램 또는 서비스를 사용하여 비디오 캡션/자막 파일을 만듭니다.

   만드는 파일이 WebVTT(Web Video Text Tracks) 표준을 따르는지 확인합니다. 캡션 파일 이름 확장명은 .vtt입니다. WebVTT 캡션 표준에 대한 자세한 정보를 확인할 수 있습니다.

   자세한 내용은 [WebVTT: 웹 비디오 텍스트 트랙 형식](https://w3c.github.io/webvtt/).

   Dynamic Media 외부에서 캡션/자막 파일을 작성하는 데 사용할 수 있는 무료 및 프리미엄 도구와 서비스가 모두 있습니다. 예를 들어 스타일이 없는 간단한 비디오 캡션 파일을 만들려면 다음과 같은 무료 온라인 캡션 작성 및 편집 도구를 사용할 수 있습니다.

   [WebVTT 캡션 작성기](https://testdrive-archive.azurewebsites.net/Graphics/CaptionMaker/Default.html)

   최상의 결과를 얻으려면 Internet Explorer 9 이상, Google Chrome 또는 Safari에서 도구를 사용하십시오.

   도구에서 **[!UICONTROL 비디오 파일의 URL 입력]** 필드에서 복사한 비디오 파일의 URL을 붙여넣은 다음 **[!UICONTROL 로드]**. 자세한 내용은 [자산의 URL 가져오기](/help/assets/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-an-asset) 비디오 파일 자체에 URL을 붙여 넣을 수 있습니다. **[!UICONTROL 비디오 파일 필드의 URL 입력]**. Internet Explorer, Chrome, or Safari can then natively play back the video.

   이제 사이트에서 화면의 지침에 따라 WebVTT 파일을 작성하고 저장합니다. 완료되면 캡션 파일 내용을 복사하여 일반 텍스트 편집기에 붙여넣은 다음 `.vtt` 파일 이름 확장명을 사용합니다.

   >[!NOTE]
   >
   >여러 언어로 비디오 자막을 글로벌 지원하려면 WebVTT 표준을 사용하려면 지원할 각 언어에 대해 별도의 .vtt 파일과 호출을 만들어야 합니다.

   일반적으로 캡션 VTT 파일의 이름을 비디오 파일과 같은 이름으로 지정하고 -EN, -FR 또는 -DE와 같은 언어 로케일에 추가하려고 합니다. 이렇게 하면 기존 웹 컨텐츠 관리 시스템을 사용하여 비디오 URL의 생성을 자동화하는 데 도움이 됩니다.

1. Experience Manager에서 WebVTT 캡션 파일을 DAM에 업로드합니다.
1. 로 이동합니다 *게시됨* 업로드한 캡션 파일과 연결할 비디오 자산입니다.

   Remember that URLs are only available to copy *after* you have first *published* the assets.

   자세한 내용은 [자산 게시](/help/assets/publishing-dynamicmedia-assets.md).

1. 다음 중 하나를 수행하십시오.

   * 팝업 비디오 뷰어 환경의 경우 **[!UICONTROL URL]**. URL 대화 상자에서 URL을 선택하여 클립보드에 복사한 다음 URL을 단순 텍스트 편집기에 복사합니다. 비디오의 복사된 URL을 다음 구문과 함께 추가합니다.

      `&caption=<server_path>/is/content/<path_to_caption.vtt_file,1>`

      참고 사항 `,1` 캡션 경로의 끝입니다. 바로 다음 `.vtt` 파일 이름 확장명을 경로에 사용하면 비디오 플레이어 모음에서 닫힌 캡션 단추를 활성화(켜기) 또는 비활성화(끄기)할 수 있습니다 `,1` 또는 `,0`각각 입니다.

   * 포함된 비디오 뷰어 환경의 경우 **[!UICONTROL 포함 코드]**. 포함 코드 대화 상자에서 를 선택하고 포함 코드를 클립보드에 복사한 다음 단순 텍스트 편집기에 붙여넣습니다. 복사된 포함 코드를 다음 구문과 함께 추가합니다.

      `videoViewer.setParam("caption","<path_to_caption.vtt_file,1>");`

      참고 사항 `,1` 캡션 경로의 끝입니다. 바로 다음 `.vtt` 파일 이름 확장명을 경로에 사용하면 비디오 플레이어 모음에서 닫힌 캡션 단추를 활성화(켜기) 또는 비활성화(끄기)할 수 있습니다 `,1` 또는 `,0`각각 입니다.

## 비디오에 장 마커 추가 {#adding-chapter-markers-to-video}

장 마커를 단일 비디오나 응용 비디오 세트에 추가하여 긴 양식 비디오를 더 쉽게 보고 탐색할 수 있습니다. 사용자가 비디오를 재생하면 비디오 타임라인에서 장 마커(비디오 스크러버라고도 함)를 클릭하여 관심 영역으로 쉽게 이동할 수 있습니다. 또는 새로운 컨텐츠, 데모 및 자습서로 바로 이동할 수 있습니다.

>[!NOTE]
>
>사용되는 비디오 플레이어는 장 마커 사용을 지원해야 합니다. Dynamic Media 비디오 플레이어는 장 마커를 지원하지만 타사 비디오 플레이어를 사용하지 않을 수 있습니다.

원할 경우 비디오 뷰어 사전 설정을 사용하는 대신 장을 사용하여 자신만의 사용자 지정 비디오 뷰어를 만들고 브랜드화할 수 있습니다. 장 탐색을 사용하여 고유한 HTML5 뷰어를 만드는 방법에 대한 지침은 Adobe HTML5 Viewer SDK API에서 클래스 아래의 &quot;Customizing Behavior Using Modifiers&quot; 제목을 참조하십시오 `s7sdk.video.VideoPlayer` 및 `s7sdk.video.VideoScrubber`. 자세한 내용은 [HTML5 뷰어 SDK API](https://s7d1.scene7.com/s7sdk/3.10/docs/jsdoc/index.html) 설명서.

<!-- If desired, you can create and brand your own custom video viewer with chapters instead of using a video viewer preset. For instructions on creating your own HTML5 viewer with chapter navigation, in the Adobe Scene7 Viewer SDK for HTML5 guide, reference the heading "Customizing Behavior Using Modifiers" under the classes `s7sdk.video.VideoPlayer` and `s7sdk.video.VideoScrubber`. The Adobe Scene7 Viewer SDK is available as a download from [Adobe Developer Connection](https://help.adobe.com/en_US/scene7/using/WSef8d5860223939e2-43dedf7012b792fc1d5-8000.html). -->

캡션을 만드는 것과 거의 동일한 방식으로 비디오에 대한 장 목록을 만듭니다. 즉, WebVTT 파일을 만듭니다. 그러나 이 파일은 또한 사용 중인 WebVTT 캡션 파일과 구분해야 합니다. 캡션과 장을 하나의 WebVTT 파일에 결합할 수 없습니다.

다음 샘플을 사용하여 장 탐색 기능을 사용하여 WebVTT 파일을 만들 수 있습니다.

### 비디오 장 탐색 기능이 있는 WebVTT 파일 {#webvtt-file-with-video-chapter-navigation}

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

위의 예에서 `Chapter 1` 는 큐 식별자이며, 선택 사항입니다. 의 큐 시간 `00:00:000 --> 01:04:364` 장의 시작 시간과 종료 시간을 지정합니다. `00:00:000` 형식 지정 마지막 세 자리는 밀리초이며 그대로 둘 수 있습니다 `000`를 설정하는 것이 좋습니다. 의 장 제목 `The bicycle store behind it all` 는 장의 내용에 대한 실제 설명입니다. 사용자가 비디오 타임라인의 시각적 큐 포인트 위에 마우스 포인터를 놓으면 큐 식별자, 시작 큐 시간 및 장 제목이 모두 비디오 플레이어 팝업에 나타납니다.

HTML5 비디오 뷰어를 사용하고 있으므로 만드는 장 파일이 WebVTT(Web Video Text Tracks) 표준을 따르는지 확인합니다. 장 파일 확장명은 다음과 같습니다. `.vtt`. WebVTT 캡션 표준에 대한 자세한 정보를 확인할 수 있습니다.

자세한 내용은 [WebVTT: 웹 비디오 텍스트 트랙 형식](https://w3c.github.io/webvtt/)

**비디오 장 탐색 추가**

1. 를 저장합니다 `.vtt` 제목 텍스트에서 문자 표현물과 관련된 문제를 방지하려면 UTF8 인코딩으로 파일을 사용하십시오.

   일반적으로 VTT 장의 이름을 비디오 파일과 같은 이름으로 지정하고 장에 추가하려고 합니다. 이렇게 하면 기존 웹 컨텐츠 관리 시스템을 사용하여 비디오 URL의 생성을 자동화하는 데 도움이 됩니다.
1. Experience Manager에서 WebVTT 장 파일을 업로드합니다.

   자세한 내용은 [자산 업로드](/help/assets/manage-assets.md#uploading-assets).

1. 다음 중 하나를 수행하십시오.

   <table>
     <tbody>
      <tr>
       <td>팝업 비디오 뷰어 경험의 경우</td>
       <td>
       <ol>
       <li>로 이동합니다 <i>게시됨 </i>업로드한 장 파일과 연결할 비디오 자산입니다. Remember that URLs are only available to copy <i>after</i> you have first <i>published</i> the assets. 자세한 내용은 <a href="/help/assets/publishing-dynamicmedia-assets.md">자산 게시.</a></li>
       <li>드롭다운 메뉴에서 을(를) 클릭하거나 탭합니다 <strong>뷰어</strong>.</li>
       <li>왼쪽 레일에서 비디오 뷰어 사전 설정 이름을 탭하거나 클릭합니다. 비디오 미리 보기가 별도의 페이지에 열립니다.</li>
       <li>왼쪽 레일의 하단에서 을 클릭합니다. <strong>URL</strong>.</li>
       <li>URL 대화 상자에서 URL을 선택하여 클립보드에 복사한 다음 URL을 단순 텍스트 편집기에 복사합니다.</li>
       <li>복사한 비디오의 URL을 다음 구문과 함께 추가하면 복사한 URL과 장 파일에 연결할 수 있습니다.<br /> <br /> <code>&navigation=<<i>full_copied_URL_path_to_chapter_file</i>.vtt></code><br /> </li>
       </ol> </td>
      </tr>
      <tr>
       <td>포함된 비디오 뷰어 경험의 경우<br /> </td>
       <td>
       <ol>
       <li>로 이동합니다 <i>게시됨 </i>업로드한 장 파일과 연결할 비디오 자산입니다. Remember that URLs are only available to copy <i>after</i> you have first <i>published</i> the assets. 자세한 내용은 <a href="/help/assets/publishing-dynamicmedia-assets.md">자산 게시.</a></li>
       <li>드롭다운 메뉴에서 을(를) 클릭하거나 탭합니다 <strong>뷰어</strong>.</li>
       <li>왼쪽 레일에서 비디오 뷰어 사전 설정 이름을 탭하거나 클릭합니다. 비디오 미리 보기가 별도의 페이지에 열립니다.</li>
       <li>왼쪽 레일의 하단에서 을 클릭합니다. <strong>포함</strong>.</li>
       <li>포함 코드 대화 상자에서 를 선택하고 전체 코드를 클립보드에 복사한 다음 단순 텍스트 편집기에 붙여넣습니다.</li>
       <li>비디오의 포함 코드를 다음 구문과 추가하므로 복사한 URL과 장 파일에 연결할 수 있습니다.<br /> <br /> <code>videoViewer.setParam("navigation","&lt;<i>full_copied_URL_path_to_chapter_file</i>.vtt&gt;"</code></li>
       </ol> </td>
      </tr>
     </tbody>
   </table>

## Dynamic Media - Scene7 모드의 비디오 축소판 정보 {#about-video-thumbnails-in-dynamic-media-scene-mode}

비디오 축소판은 고객에게 비디오를 나타내는 이미지 자산 또는 비디오 프레임의 축소된 버전입니다. 축소판은 고객이 비디오를 클릭하도록 권장하는 데 사용됩니다.

Experience Manager의 모든 비디오에는 연결된 축소판이 있어야 합니다. 축소판을 바꾸지 않으면 삭제할 수 없습니다. 기본적으로 비디오를 Experience Manager에 업로드할 때 첫 번째 프레임이 축소판으로 사용됩니다. 그러나 브랜딩 용도나 시각적 검색 등을 위해 축소판을 사용자 지정할 수 있습니다. 비디오 축소판을 사용자 지정할 때 비디오를 재생하고 사용할 프레임에서 일시 정지할 수 있습니다. 또는 이미 업로드한 이미지 자산을 선택할 수 있습니다 *게시됨* 참조하십시오.

비디오에서 선택하는 사용자 지정 비디오 축소판 이미지는 추출되지 않고 DAM에 별도의 개별 자산으로 저장됩니다. 그러나 기존 이미지 자산에서 선택하는 사용자 지정 비디오 축소판은 JCR에 저장됩니다. 선택한 자산의 경로는 다음 예제 경로에서 과 같이 비디오 자산의 노드 아래에 저장됩니다.

`/content/dam/*<folder_name*>/<*video_name*>/jcr:content/manualThumbnail`

비디오 축소판을 사용자 지정하는 기능은 비디오가 있는 폴더에 비디오 프로필을 적용한 후에만 사용할 수 있습니다.

참조 - [Dynamic Media - 하이브리드 모드의 비디오 축소판 정보](#about-video-thumbnails-in-dynamic-media-hybrid-mode).

### 사용자 지정 비디오 축소판 추가 {#adding-a-custom-video-thumbnail}

이 단계는 &quot;Dynamic Media_Scene7&quot; 모드에서 실행되는 Dynamic Media에만 적용됩니다.

**사용자 지정 비디오 축소판을 추가하려면:**

1. 다음을 이미 수행했는지 확인하십시오.

   * 비디오 자산에 대한 폴더를 만들었습니다.
   * [폴더에 비디오 프로필 적용](/help/assets/video-profiles.md#applying-a-video-profile-to-folders).

   * [비디오를 폴더에 업로드했습니다](/help/assets/managing-video-assets.md#upload-and-preview-video-assets).

1. 축소판 이미지를 변경할 업로드된 비디오 자산으로 이동합니다.
1. 자산 선택 모드에서 **[!UICONTROL 목록 보기]** 또는 **[!UICONTROL 카드 보기]**&#x200B;를 눌러 비디오 자산을 탭합니다.
1. 도구 모음에서 **[!UICONTROL 속성]** 아이콘(안에 &quot;i&quot;가 있는 원).
1. 비디오의 속성 페이지에서 **[!UICONTROL 축소판 변경]**.
1. 축소판 그림 변경 페이지에서 다음 중 하나를 수행합니다.

   * 비디오의 프레임을 새 축소판으로 사용하려면

      * 도구 모음에서 **[!UICONTROL 비디오에서 프레임 선택]**.
      * 재생 단추를 누른 다음 비디오의 새 축소판으로 캡처할 프레임에서 일시 중지 단추를 누릅니다.
   * 이미지 자산을 새 축소판으로 사용하려면

      * 도구 모음에서 **[!UICONTROL 자산에서 축소판 선택]**.
      * 탭 **[!UICONTROL 축소판 선택]**.
      * 사용하려는 이전에 업로드 및 게시된 이미지 자산으로 이동합니다. 비디오의 축소판 이미지로 사용할 수 있도록 자산 크기가 자동으로 조정됩니다.
      * 이미지 자산을 선택한 다음 **[!UICONTROL 선택]**.


1. Change Thumbnail 페이지에서 **[!UICONTROL 변경 내용 저장]**.
1. 비디오의 속성 페이지의 오른쪽 위 모서리에서 을(를) 탭합니다 **[!UICONTROL 저장 및 닫기]**.

## Dynamic Media - 하이브리드 모드의 비디오 축소판 정보 {#about-video-thumbnails-in-dynamic-media-hybrid-mode}

Dynamic Media에서 자동으로 생성된 10개의 축소판 이미지 중 하나를 선택하여 비디오에 추가할 수 있습니다. Experience Manager Sites, Experience Manager 모바일 또는 Experience Manager Screens의 작성 환경에서 비디오 자산이 Dynamic Media 구성 요소와 함께 사용되는 경우 비디오 플레이어에 선택한 축소판이 표시됩니다. 축소판은 전체 비디오의 내용을 가장 잘 나타내는 정적 그림 역할을 하며 사용자가 재생 단추를 클릭하도록 합니다.

Dynamic Media은 비디오의 총 시간을 기반으로 10개의(기본값) 축소판 이미지를 캡처합니다. 이 영상은 1%, 11%, 21%, 31%, 41%, 51%, 61%, 71%, 81%, 91%로 녹화된 것이다. 열 축소판은 지속됩니다. 즉, 나중에 다른 축소판을 선택하더라도 시리즈를 다시 생성할 필요가 없습니다. 10개의 축소판 이미지를 미리 보고 비디오에 사용할 이미지를 선택합니다. 기본값으로 변경하려면 CRXDE Lite을 사용하여 축소판 이미지가 생성되는 시간 간격을 구성할 수 있습니다. 예를 들어 비디오에서 균일하게 배치된 네 개의 축소판 이미지만 생성하려는 경우 간격 시간을 24%, 49%, 74% 및 99%로 구성할 수 있습니다.

가장 좋은 방법은 비디오를 업로드한 후 언제든지 웹 사이트에 비디오를 게시하기 전에 비디오 축소판을 추가할 수 있는 것입니다.

Dynamic Media에서 생성된 축소판을 사용하는 대신 사용자 정의 축소판을 업로드하여 비디오를 나타낼 수 있습니다. 예를 들어 비디오의 제목, 눈길을 끄는 개방형 이미지 또는 비디오에서 캡처한 특정 이미지가 있는 사용자 정의 축소판 이미지를 만들 수 있습니다. 업로드하는 사용자 정의 비디오 축소판 이미지는 최대 해상도가 1280 x 720픽셀(최소 너비 640픽셀)이며 2MB보다 크지 않아야 합니다.

참조 - [Dynamic Media - Scene7 모드의 비디오 축소판 정보](/help/assets/video.md#about-video-thumbnails-in-dynamic-media-scene-mode).

### 비디오 축소판 추가 {#adding-a-video-thumbnail}

이러한 단계는 하이브리드 모드에서 실행되는 Dynamic Media에만 적용됩니다.

**비디오 축소판을 추가하려면**

1. 비디오 축소판을 추가할 업로드된 비디오 자산으로 이동합니다.
1. 목록 보기 또는 카드 보기에서 자산 선택 모드에서 비디오 자산을 탭합니다.
1. 도구 모음에서 **[!UICONTROL 속성 보기]** 아이콘(안에 &quot;i&quot;가 있는 원).
1. 비디오의 속성 페이지에서 **[!UICONTROL 축소판 변경]**.
1. Change Thumbnail 페이지의 도구 모음에서 **[!UICONTROL 프레임 선택]**.

   Dynamic Media은 사용자 지정한 기본 시간 간격이나 시간 간격에 따라 비디오에서 축소판 이미지를 생성합니다.

1. 생성된 축소판 이미지를 미리 보고 비디오에 추가할 이미지를 선택합니다.
1. 탭 **[!UICONTROL 변경 내용 저장]**.

   선택한 축소판을 사용하도록 비디오의 축소판 이미지가 업데이트됩니다. 나중에 축소판 이미지를 변경하기로 결정한 경우 **[!UICONTROL 축소판 변경]** 페이지를 열고 새 페이지를 선택합니다.

   새 기본 시간 간격을 구성했거나 기존 비디오를 바꾸기 위해 새 비디오를 업로드한 경우 Dynamic Media에서 미리 보기를 다시 생성하도록 합니다.

   자세한 내용은 [비디오 축소판이 생성되는 기본 시간 간격을 구성합니다](#configuring-the-default-time-interval-that-video-thumbnails-are-generated).

#### 비디오 축소판이 생성되는 기본 시간 간격을 구성합니다 {#configuring-the-default-time-interval-that-video-thumbnails-are-generated}

새로운 기본 시간 간격을 구성하고 저장하면 나중에 업로드하는 비디오에만 변경 사항이 자동으로 적용됩니다. 이전에 업로드한 비디오에는 새 기본값이 자동으로 적용되지 않습니다. 기존 비디오의 경우 축소판을 다시 생성해야 합니다.

자세한 내용은 [비디오 축소판 추가](#adding-a-video-thumbnail).

**비디오 축소판이 생성되는 기본 시간 간격을 구성하려면 다음을 수행합니다.**

1. Experience Manager에서 **[!UICONTROL 도구]** > **[!UICONTROL 일반]** > **[!UICONTROL CRXDE Lite]**.

1. CRXDE Lite 페이지의 왼쪽 디렉토리 패널에서 `o etc/dam/imageserver/configuration/jcr:content/settings.`

   디렉토리 패널이 표시되지 않으면 홈 탭 왼쪽의 > 아이콘을 누릅니다.

1. 오른쪽 아래 패널의 속성 탭에서 두 번 탭합니다 `thumbnailtime`.
1. 에서 **[!UICONTROL 축소판 표시 시간 편집]** 대화 상자에서 간격 값을 백분율로 입력하려면 텍스트 필드를 사용합니다.

   * 하나 이상의 간격 값 필드를 추가하려면 더하기 기호(+) 아이콘을 누릅니다. 필요한 경우 대화 상자 아래쪽으로 스크롤하여 아이콘을 확인합니다.
   * 목록에서 삭제하려면 간격 값 필드 오른쪽에 있는 빼기 기호(-) 아이콘을 누릅니다.
   * 간격 값을 다시 정렬하려면 위쪽 화살표 아이콘과 아래쪽 화살표 아이콘을 누릅니다.

1. 탭 **[!UICONTROL 확인]** 속성 탭으로 돌아갑니다.
1. CRXDE Lite 페이지의 왼쪽 위 모서리 근처에 있는 **[!UICONTROL 모두 저장]**&#x200B;그런 다음 왼쪽 위 모서리에 있는 뒤로 홈 아이콘을 탭하여 Experience Manager으로 돌아갑니다.

   자세한 내용은 [비디오 축소판 추가](#adding-a-video-thumbnail).

### 사용자 지정 비디오 축소판 추가 {#adding-a-custom-video-thumbnail-1}

이러한 단계는 하이브리드 모드에서 실행되는 Dynamic Media에만 적용됩니다.

**사용자 지정 비디오 축소판을 추가하려면:**

1. 사용자 지정 비디오 축소판을 추가할 업로드된 비디오 자산으로 이동합니다.
1. 목록 보기 또는 카드 보기에서 자산 선택 모드에서 비디오 자산을 탭합니다.
1. 도구 모음에서 **[!UICONTROL 속성 보기]** 아이콘(안에 &quot;i&quot;가 있는 원).
1. 비디오의 속성 페이지에서 **[!UICONTROL 축소판 변경]**.
1. Change Thumbnail 페이지의 도구 모음에서 **[!UICONTROL 새 축소판 업로드]**.
1. 사용할 축소판 이미지로 이동하여 선택한 다음 **[!UICONTROL 열기]** Experience Manager에 이미지 업로드를 시작합니다. 업로드 후에 이미지를 게시합니다.
1. 이미지를 업로드하고 게시한 후 축소판 그림 변경 페이지에서 **[!UICONTROL 변경 내용 저장]**.

   사용자 정의 축소판이 비디오에 추가됩니다.

## Dynamic Media 자산에 대한 Dynamic Media URL 변경 {#manifest-urls}

Dynamic Media에 처리된 비디오는 기본 제공 뷰어 및 매니페스트 URL에 직접 액세스하여 사용자 지정 뷰어를 통해 재생함으로써 사용할 수 있습니다. 다음은 비디오의 매니페스트 URL을 가져오기 위한 API입니다.

### getVideoManifestURI API 정보

다음 `getVideoManifestURI`API는 c를 통해 노출됩니다`q-scene7-api:com.day.cq.dam.scene7.api` 및 를 사용하여 다음 매니페스트 URL을 생성할 수 있습니다.

```java
/**   
* Returns the manifest url for videos 
* @param resource video resource 
* @param manifestType type of video streaming manifest being requested 
* @param onlyIfPublished return a manifest only if the video is published 
* @return the manifest url for videos 
* 
* @throws Exception 
*/
@Nullable 
String getVideoManifestURI(Resource resource, ManifestType manifestType, boolean onlyIfPublished) throws Exception;
```

#### getVideoManifestURI API 매개 변수

이 API는 다음 세 가지 매개 변수를 사용합니다.

| 매개변수 | 설명 |
| --- | --- |
| `resource` | Dynamic Media이 수집한 비디오에 해당하는 리소스입니다. |
| `manifestType` | 다음 중 하나일 수 있습니다 `ManifestType.DASH` 또는 `ManifestType.HLS` |
| `onlyIfPublished` | 매니페스트 URI가 게시되어 게재 계층에서 사용할 수 있는 경우에만 매니페스트 URI가 생성되는 경우 true로 설정합니다. |

위의 메서드를 사용하여 비디오에 대한 매니페스트 URL을 가져오려면 다음을 추가하십시오 [비디오 인코딩 프로필](/help/assets/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming) 를 &quot;비디오 업로드&quot; 폴더로 업로드합니다. Dynamic Media은 폴더에 할당된 비디오 인코딩 파일에 있는 인코딩을 기반으로 이러한 비디오를 처리합니다. 이제 업로드된 비디오의 매니페스트 URL을 가져오기 위해 위의 API를 호출할 수 있습니다.

### 오류 시나리오

오류가 있으면 API가 null을 반환합니다. 예외가 Experience Manager 오류 로그에 기록됩니다. 이러한 모든 로그된 오류는 `Could not generate Video Manifest URI`. 다음 시나리오에서는 이러한 오류가 발생할 수 있습니다.

* An `IllegalArgumentException` 다음 중 하나에 대해 기록됩니다.

   * 다음 `resource` 전달된 매개 변수가 null입니다.
   * 다음 `resource` 전달된 매개 변수가 비디오가 아닙니다.
   * 다음 `manifestType` 전달된 매개 변수가 null입니다.
   * 다음 `onlyIfPublished` 매개 변수가 true로 전달되지만 비디오가 게시되지 않습니다.
   * Dynamic Media에서 가져온 응용 비디오 세트를 사용하여 비디오를 수집하지 않았습니다.

* `IOException` Dynamic Media에 연결하는 데 문제가 있으면 기록됩니다.
* `UnsupportedOperationException` 은 `manifestType` 전달된 매개 변수 `ManifestType.DASH`인 경우 문제가 발생합니다.

다음은 에 작성된 서블릿을 사용하는 위의 API의 예입니다 *HTTPWhiteBoard* 사양. 코드 구문에 사용할 각 탭을 선택합니다.

>[!BEGINTABS]

>[!TAB pom.xml에 종속성 추가]

+++**pom.xml에 종속성 추가**

```java
dependency> 
     <groupId>com.day.cq.dam</groupId> 
     <artifactId>cq-scene7-api</artifactId> 
     <version>5.12.64</version> 
     <scope>provided</scope> 
</dependency> 
```

+++

>[!TAB 샘플 서블릿]

+++**샘플 서블릿**

```java
@Component
        service = Servlet.class 
) 
@HttpWhiteboardServletPattern(value = ManifestServlet.SERVLET_PATTERN) 
@HttpWhiteboardContextSelect(value = Constants.SERVLET_CONTEXT_SELECTOR) 
public class ManifestServlet extends HttpServlet { 

   private static final Logger LOGGER = LoggerFactory.getLogger(ManifestServlet.class); 

   private final ObjectMapper objectMapper; 

    @Reference 
    private Scene7Service scene7Service; 

   public static final String SERVLET_PATTERN = Constants.VIDEO_API_PREFIX + "/manifestUrl"; 

   public ManifestServlet() {
         this.objectMapper = new ObjectMapper(); 
         objectMapper.setSerializationInclusion(JsonInclude.Include.NON_NULL); 
   }

   @Override 

   protected void doGet(HttpServletRequest request, HttpServletResponse response) throws IOException {
        final ResourceResolver resolver = getResourceResolver(request); 
        String assetPath = request.getParameter("assetPath"); 
        String manifest = request.getParameter("manifestType"); 
        String onlyIfPublished = request.getParameter("onlyIfPublished"); 
        Resource resource = resolver.getResource(assetPath); 
        response.setCharacterEncoding(StandardCharsets.UTF_8.toString()); 
        response.setContentType("application/json"); 
        if(resource == null) { 
            LOGGER.info("could not retrieve the resource from JCR"); 
            error("could not retrieve the resource from JCR", response); 
            return; 
        }

        String manifestUri = null; 

        try{ 
            ManifestType manifestType =  ManifestType.DASH; 
            if(manifest != null) { 
                manifestType = ManifestType.valueOf(manifest); 
            } 
            manifestUri = scene7Service.getVideoManifestURI(resource, manifestType, onlyIfPublished != null); 
            objectMapper.writeValue(response.getWriter(), new ManifestUrl(manifestUri)); 
            response.setContentType("application/json"); 
        } catch (Exception e) { 
            LOGGER.error(e.getMessage(), e); 
            error(String.format("Unable to get the manifest url for %s. %s", assetPath, e.getMessage()), response); 
        } 
    } 

    private ResourceResolver getResourceResolver(HttpServletRequest request) { 
        Object rr = request.getAttribute(AuthenticationSupport.REQUEST_ATTRIBUTE_RESOLVER); 
        if (!(rr instanceof ResourceResolver)) { 
            throw new IllegalStateException( 
                    "The request does not seem to have been created via Apache Sling's authentication mechanism."); 
        } else { 
            return (ResourceResolver) rr; 
        } 
    } 

    private void error(String errorMessage, HttpServletResponse response) throws IOException { 
        ManifestUrl errorManifest = new ManifestUrl(null); 
        errorManifest.setErrorMessage(errorMessage); 
        response.setStatus(HttpServletResponse.SC_INTERNAL_SERVER_ERROR); 
        objectMapper.writeValue(response.getWriter(), errorManifest); 
    } 
} 
```

+++

>[!TAB 서블릿에 대한 응답 클래스]

+++**서블릿에 대한 응답 클래스**

```java
public class ManifestUrl extends VideoResponse { 
     String manifestUrl; 
     public ManifestUrl(String manifestUrl) { 
         this.manifestUrl = manifestUrl; 
     } 
     public String getManifestUrl() { 
         return manifestUrl; 
     } 
} 

public abstract class VideoResponse { 
     String errorString; 

     public String getErrorString() { 
         return errorString; 
     } 

     public void setErrorMessage(String errorString) { 
         this.errorString = errorString; 
     } 
} 
```

+++

>[!TAB 서블릿에서 참조되는 상수 파일]

+++**서블릿에서 참조되는 상수 파일**

```java
public final class Constants { 

     private Constants() { 
     } 

     public static final String VIDEO_API_PREFIX = "/dynamicmedia/video"; 
     public static final String SERVLET_CONTEXT_SELECTOR = "(" + HttpWhiteboardConstants.HTTP_WHITEBOARD_CONTEXT_NAME + "=" + 
             DMSampleApiHttpContext.CONTEXT_NAME + ")"; 

 } 
```

+++

>[!TAB ServletContext]

+++**ServletContext**

를 사용하여 위의 서블릿 마운트 `servletContext`. 다음은 의 예입니다 `servletContext`.

```java
public class DMSampleApiHttpContext extends ServletContextHelper { 

 public static final String CONTEXT_NAME = "com.adobe.dmSample"; 
 public static final String CONTEXT_PATH = "/dmSample"; 

 private final MimeTypeService mimeTypeService; 

 private final AuthenticationSupport authenticationSupport; 

 /** 
  * Constructs a new context that will use the given dependencies. 
  * 
  * @param mimeTypeService Used when providing mime type of requests. 
  * @param authenticationSupport Used to authenticate requests with sling. 
  */ 
 @Activate 
 public DMSampleApiHttpContext(@Reference final MimeTypeService mimeTypeService, 
                               @Reference final AuthenticationSupport authenticationSupport) { 
     this.mimeTypeService = mimeTypeService; 
     this.authenticationSupport = authenticationSupport; 
 } 

 // ---------- HttpContext interface ---------------------------------------- 
 /** 
  * Returns the MIME type as resolved by the <code>MimeTypeService</code> or 
  * <code>null</code> if the service is not available. 
  */ 
 @Override 
 public String getMimeType(String name) { 
     MimeTypeService mtservice = mimeTypeService; 
     if (mtservice != null) { 
         return mtservice.getMimeType(name); 
     } 
     return null; 
 } 

 /** 
  * Returns the real context path that is used to mount this context. 
  * @param req servlet request 
  * @return the context path 
  */ 
 public static String getRealContextPath(HttpServletRequest req) { 
     final String path = req.getContextPath(); 
     if (path.equals(CONTEXT_PATH)) { 
         return ""; 
     } 
     return path.substring(CONTEXT_PATH.length()); 
 } 

 /** 
  * Returns a request wrapper that transforms the context path back to the original one 
  * @param req request 
  * @return the request wrapper 
  */ 
 public static HttpServletRequest createContextPathAdapterRequest(HttpServletRequest req) { 
     return new HttpServletRequestWrapper(req) { 

         @Override 
         public String getContextPath() { 
             return getRealContextPath((HttpServletRequest) getRequest()); 
         } 

     }; 

 } 

 /** 
  * Always returns <code>null</code> because resources are all provided 
  * through individual endpoint implementations. 
  */ 
 @Override 
 public URL getResource(String name) { 
     return null; 
 } 

 /** 
  * Tries to authenticate the request using the 
  * <code>SlingAuthenticator</code>. If the authenticator or the Repository 
  * is missing this method returns <code>false</code> and sends a 503/SERVICE 
  * UNAVAILABLE status back to the client. 
  */ 
 @Override 
 public boolean handleSecurity(HttpServletRequest request, 
                               HttpServletResponse response) throws IOException { 

     final AuthenticationSupport authenticator = this.authenticationSupport; 
     if (authenticator != null) { 
         return authenticator.handleSecurity(createContextPathAdapterRequest(request), response); 
     } 

     // send 503/SERVICE UNAVAILABLE, flush to ensure delivery 
     response.sendError(HttpServletResponse.SC_SERVICE_UNAVAILABLE, 
             "AuthenticationSupport service missing. Cannot authenticate request."); 
     response.flushBuffer(); 

     // terminate this request now 
     return false; 
 } 
}
```

+++

>[!ENDTABS]

### 샘플 서블릿 사용

을 수행하여 서블릿을 호출합니다 `GET` 작업 `/dmSample/dynamicmedia/video/manifestUrl`. 다음 쿼리 매개 변수가 전달됩니다.

| 쿼리 매개 변수 | 설명 |
| --- | --- |
| `assetPath` | 필수. 비디오에 사용할 경로입니다 `manifestUrl` 가 생성됩니다. |
| `manifestType` | 선택 사항. 매개 변수는 DASH 또는 HLS일 수 있습니다. 전달되지 않으면 기본값이 DASH로 설정됩니다. |
| `onlyIfPublished` | 선택 사항. 전달된 경우 `manifestUrl` 가 반환되는 것은 비디오가 게시되는 경우에만 해당됩니다. |

이 예에서 다음 설정을 가정해 보겠습니다.

* 회사가 `samplecompany`.
* 작성 인스턴스는 `http://sample-aem-author.com`.
* 폴더 `/content/dam/video-example` 에는 비디오 인코딩 프로필이 적용되어 있습니다.
* 비디오 `scenery.mp4` 폴더에 업로드됩니다 `/content/dam/video-example`.

다음과 같은 방법으로 서블릿을 호출할 수 있습니다.

| 유형 | 설명 |
| :--- | --- |
| HLS | `http://sample-aem-author.com/dmSample/dynamicmedia/video/manifestUrl?manifestType=HLS&assetPath=/content/dam/video-example/scenery.mp4`<br><br>DASH 전달이 활성화된 경우:<br>`{"manifestUrl":"https://s7d1.scene7.com/is/content/samplecompany/scenery-AVS.m3u8?packagedStreaming=true"}`<br><br>DASH 전달이 비활성화된 경우:<br>`{"manifestUrl":"https://s7d1.scene7.com/is/content/samplecompany/scenery-AVS.m3u8"}` |
| 대시 | `http://sample-aem-author.com/dmSample/dynamicmedia/video/manifestUrl?manifestType=DASH&assetPath=/content/dam/video-example/scenery.mp4`<br><br>DASH 전달이 활성화된 경우:<br>`{"manifestUrl":"https://s7d1.scene7.com/is/content/samplecompany/scenery-AVS.mpd"}`<br><br>DASH 전달이 비활성화된 경우:<br>`{}` |
| 오류: 자산 경로가 잘못되었습니다. | `http://sample-aem-author.com/dmSample/dynamicmedia/video/manifestUrl?manifestType=DASH&assetPath=/content/dam/video-example/scennnnnnery.mp4`<br><br>`{"errorString":"could not retrieve the resource from JCR"}` |


