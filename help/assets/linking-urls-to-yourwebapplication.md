---
title: URL을 웹 애플리케이션에 연결
description: Dynamic Media에서 웹 애플리케이션에 URL을 연결하는 방법
uuid: cf599e66-b1f9-40c0-b572-cea19f2e6793
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: d12e6ea3-aaf4-4672-9679-3c16c76d7d5b
role: Business Practitioner, Administrator
exl-id: d62275f0-02a4-48c9-bfb1-e23d63b618c9
feature: 구성
source-git-commit: 9134130f349c6c7a06ad9658a87f78a86b7dbf9c
workflow-type: tm+mt
source-wordcount: '1275'
ht-degree: 1%

---

# URL을 웹 애플리케이션에 연결 {#linking-urls-to-your-web-application}

웹 사이트 및 애플리케이션이 URL 호출을 통해 Dynamic Media 서비스에 액세스합니다. 자산을 게시하면 Dynamic Media에서 자산을 참조하는 URL 문자열을 활성화합니다. 이러한 URL을 테스트하기 위해 웹 브라우저에 붙여넣을 수 있습니다.

AEM을 WCM으로 사용하지 *않고*&#x200B;인 경우에만 URL에 연결합니다. 연결 대 포함 - 비디오 플레이어를 팝업 또는 모달 창으로 전달하려는 경우 사용됩니다. AEM을 WCM으로 사용하는 경우 [자산을 페이지에 직접 추가합니다.](adding-dynamic-media-assets-to-pages.md)

웹 페이지 및 애플리케이션에 이러한 URL 문자열을 배치하려면 Dynamic Media에서 복사합니다.

>[!NOTE]
>
>URL 문자열은 자산의 동적 변환에만 사용할 수 있습니다. 현재 Dynamic Media 서버가 아닌 DAM에 있는 정적 자산에 사용할 수 없습니다. 정적인 표현물에 대해서는 URL 단추가 표시되지 않습니다.

웹 페이지에 비디오 또는 이미지 뷰어 포함](embed-code.md)을 참조하십시오.[

또한 [YouTube URL을 웹 애플리케이션에 연결](video.md)을 참조하십시오.

[응답형 사이트용으로 최적화된 이미지 제공](responsive-site.md)도 참조하십시오.

[자산 업로드를 참조하십시오.](manage-assets.md#uploading-assets)

## 자산 {#obtaining-a-url-for-an-asset} URL 가져오기

이미지 사전 설정 또는 뷰어 사전 설정으로 생성된 URL 문자열을 가져올 수 있습니다. URL을 복사하면 클립보드에 로드되므로 웹 사이트 또는 애플리케이션의 페이지에 필요에 따라 붙여넣을 수 있습니다.

>[!NOTE]
>
>선택한 자산을 게시하기 전까지는 URL을 복사할 수 없습니다. 또한 뷰어 사전 설정 또는 이미지 사전 설정도 게시해야 합니다.
>
>[자산 게시](publishing-dynamicmedia-assets.md)를 참조하십시오.
>
>[뷰어 사전 설정 게시](managing-viewer-presets.md#publishing-viewer-presets)를 참조하십시오.
>
>[이미지 사전 설정 게시](managing-image-presets.md#publishing-image-presets)를 참조하십시오.

URL 문자열을 가져오는 방법은 여러 가지가 있습니다. 그러나 아래 단계에서는 사용할 수 있는 한 가지 방법을 보여 줍니다.

**자산의 URL을 가져오려면**

1. 이미지 사전 설정 URL 또는 뷰어 사전 설정 URL이 복사하려는 *게시된* 자산으로 이동하고 자산을 탭하여 엽니다.

   URL은 *다음에*&#x200B;을 복사하는 데에만 사용할 수 있으며, 먼저 *자산을 게시했습니다*. 또한 뷰어 사전 설정 또는 이미지 사전 설정도 게시해야 합니다.

   [자산 게시를 참조하십시오.](publishing-dynamicmedia-assets.md)

   [뷰어 사전 설정 게시](managing-viewer-presets.md#publishing-viewer-presets)를 참조하십시오.

   [이미지 사전 설정 게시](managing-image-presets.md#publishing-image-presets)를 참조하십시오.

1. 선택한 자산에 따라 다음 중 하나를 수행합니다.

   * 이미지를 선택한 경우 드롭다운 메뉴에서 **[!UICONTROL 표현물]**&#x200B;을 누릅니다.

      **[!UICONTROL Dynamic]** 제목 아래에서 사전 설정 이름을 탭하여 오른쪽 프레임에서 해당 변환을 확인합니다. 동적 제목을 보려면 표현물 목록을 스크롤해야 할 수 있습니다.

      왼쪽 레일 하단에서 **[!UICONTROL URL]**&#x200B;을 탭합니다.

      ![chlimage_1-270](assets/chlimage_1-270.png)

   * 스핀 세트, 이미지 세트, 회전 메뉴 세트 또는 비디오를 선택한 경우, 드롭다운 메뉴에서 **[!UICONTROL 뷰어.]**

      왼쪽 레일에서 뷰어 사전 설정 이름을 탭합니다. 세트 또는 비디오의 미리 보기가 별도의 페이지에서 열립니다.

      왼쪽 레일의 하단에서 **[!UICONTROL URL]**&#x200B;을 누릅니다.

      ![chlimage_1-271](assets/chlimage_1-271.png)

1. 텍스트를 선택하고 웹 브라우저에 복사하여 자산을 미리 보거나 웹 컨텐츠 페이지에 추가합니다.

   URL 창을 종료하려면 **[!UICONTROL X]**&#x200B;을 탭하거나 **[!UICONTROL 닫기.]**

## 정적 자산 {#obtaining-a-url-for-a-static-asset} URL 가져오기

Dynamic Media에서는 이미지 및 비디오 이외에 추가적인 자산인 정적 자산 전달을 지원합니다. 전달을 위해 지원되는 정적 자산 형식에는 다음이 포함됩니다.

* 3D 파일
* 애니메이션 GIF
* 오디오 파일
* CSS
* JavaScript (회사가 자체 도메인으로 구성된 경우)
* PDF
* SVG
* XML
* ZIP

**정적 자산의 URL을 가져오려면**

1. 복사할 URL이 있는 *게시된* 정적 자산으로 이동한 후 자산을 탭하여 엽니다.

   URL은 *이후에*&#x200B;을 복사하는 데에만 사용할 수 있으며, 정적 자산을 처음 *게시했습니다*.

   [자산 게시](publishing-dynamicmedia-assets.md)를 참조하십시오.

1. 다음 방법 중 하나를 사용하여 게시된 정적 자산의 URL을 얻습니다.

   * `The URL of the published static is the following:`

      * `https://*<server_name>*/is/content/*<company_name>*/*<static_asset_filename>*.*<extension>*`

         예, `https://aem.com/is/content/adobe/image.gif`.
   * **[!UICONTROL 자산 > 동적 표현물]**&#x200B;을 탭한 다음, 정적 자산의 동적 표현물을 탭하고 URL을 복사합니다.

      복사된 URL을 경로 `is/image/` 대신 `is/content`을 사용하도록 변경합니다.


## 게시된 비디오 표현물에 대한 비디오 URL 가져오기 {#obtaining-a-video-url-for-a-published-video-rendition}

1. AEM에서 **[!UICONTROL 도구 > 배포 > 클라우드 > Cloud Services으로 이동합니다.]**
1. **[!UICONTROL Cloud Services]** 페이지에서 **[!UICONTROL Dynamic Media Cloud Services]** 머리글로 스크롤한 다음 **[!UICONTROL 구성 표시]**&#x200B;를 탭합니다.
1. **[!UICONTROL 사용 가능한 구성]**&#x200B;에서 원하는 구성 이름을 탭합니다.

1. **[!UICONTROL Dynamic Media 클라우드 설정]** 페이지의 **[!UICONTROL 비디오 서비스 URL]**&#x200B;에서 전체 URL 경로를 복사합니다. 복사한 URL 경로가 단계의 후반부에 필요합니다.

   예를 들어 URL 경로는 다음과 유사할 수 있습니다.

   `https://s7athens.macromedia.com:9090/DMGateway/`

   (위 경로는 그림 용도로만 사용됩니다.)복사한 실제 경로가 아닙니다.)

1. **[!UICONTROL 등록 ID]**&#x200B;에서 ID의 마지막 부분에 있는 고객 이름을 복사합니다.

   예를 들어 등록 ID가 `87654321|MyCompany`인 경우 고객 이름은 `MyCompany`입니다.

1. 페이지의 왼쪽 위 모서리 근처에 있는 **[!UICONTROL Cloud Services]**&#x200B;을 탭한 다음 Experience Manager 로고를 탭하고 **[!UICONTROL 일반 > CRXDE Lite으로 이동합니다.]**
1. JCR(Java Content Repository)에서 전체 비디오 변환 경로를 복사합니다.

   예를 들어 비디오의 변환 경로는 다음과 유사할 수 있습니다.

   `/_renditions_/0bd/0bd28743-a616-4fe6-92aa-6eae7c2112f/avs/Momentum_1080-0x720-2600k.mp4`

   (위 경로는 그림 용도로만 사용됩니다.)복사한 실제 경로가 아닙니다.)

1. 복사된 정보를 다음 순서로 정렬하여 전체 URL 경로를 형성합니다.

   `<Video_Service_URL>/public/<Customer_name_from_Registration_ID>/<Video_rendition_path>`

   예를 들어 위의 단계에서 경로 예와 고객 이름 예를 사용하여 전체 경로가 다음과 같이 표시됩니다.

   `https://s7athens.macromedia.com:9090/DMGateway/public/MyCompany/_renditions_/0bd/0bd28743-a616-4fe6-92aa-6eae7c2112ff/avs/Momentum_1080-0x720-2600k.mp4`

   게시된 비디오 표현물에 대한 전체 비디오 URL입니다.

## 응용 스트리밍을 위한 비디오 URL(HLS) {#obtaining-a-video-url-for-adaptive-streaming-hls} 가져오기

1. AEM에서 **[!UICONTROL 도구 > 배포 > 클라우드 > Cloud Services으로 이동합니다.]**
1. **[!UICONTROL Cloud Services]** 페이지에서 **[!UICONTROL Dynamic Media Cloud Services]** 머리글로 스크롤한 다음 **[!UICONTROL 구성 표시]**&#x200B;를 탭합니다.
1. **[!UICONTROL 사용 가능한 구성]**&#x200B;에서 원하는 구성 이름을 탭합니다.
1. **[!UICONTROL Dynamic Media Cloud Services 설정]** 페이지에서 다음을 수행합니다.

   * **[!UICONTROL 비디오 서비스 URL]**&#x200B;에서 전체 URL 경로를 복사합니다. 복사된 URL 경로는 이 단계의 후반부에 필요합니다. 예를 들어 URL 경로는 다음과 유사할 수 있습니다.

   `https://gateway-na.assetsadobe.com/DMGateway/`

   (위 경로는 그림 용도로만 사용됩니다.)복사한 실제 경로가 아닙니다.)

   * **[!UICONTROL 등록 ID]**&#x200B;에서 ID의 마지막 부분에 있는 고객 이름을 복사합니다. 이 단계에서 나중에 복사된 고객 이름이 필요합니다.

      예를 들어 등록 ID가 `87654321|demoCo`이면 복사하는 고객 이름은 `demoCo`입니다.


1. 사용 중인 비디오 게재 프로토콜을 기준으로 각 프로토콜 선택기를 복사합니다. 이 단계의 후반부에 복사된 프로토콜 선택기가 필요합니다.

   | 사용 중인 비디오 게재 프로토콜 | 사용할 프로토콜 선택기 |
   |---|---|
   | HTTP <br> HTTP(비보안 비디오 게재)를 사용하는 경우 이전에 복사한 비디오 서비스 URL 값에서 https를 http로 변경해야 합니다. | `public/` |
   | HTTPS | `public-ssl/` |

1. Dynamic Media에서 처리한 대로 AEM의 전체 비디오 자산 경로를 복사합니다. 이 복사한 비디오 자산 경로가 이 단계의 후반부에 필요합니다.

   예:

   `/content/dam/marketing/MyVideo.mp4`

1. 이전에 복사한 모든 조각을 결합하여 다음 순서로 문자열을 생성합니다.

   &lt;>> &lt;> > &lt;> > &lt;>>`video service URL``protocol selector``customer name``video asset path`

   예를 들어 이러한 단계의 예에서 복사한 정보를 사용하여 문자열이 다음과 같이 표시됩니다.

   `https://gateway-na.assetsadobe.com/DMGateway/public-ssl/demoCo/content/dam/marketing/MyVideo.mp4`

1. 문자열 끝에 `.m3u8` 를 추가하여 URL을 완료합니다. 예를 들어 이전 단계의 문자열에 `.m3u8`을 추가하면 전체 URL 경로가 다음과 같이 나타납니다.

   `https://gateway-na.assetsadobe.com/DMGateway/public-ssl/demoCo/content/dam/marketing/MyVideo.mp4.m3u8`

## HTTP/2를 사용하여 Dynamic Media 자산 {#using-http-to-deliver-your-dynamic-media-assets} 제공

HTTP/2는 브라우저 및 서버의 통신 방식을 향상시키는 업데이트된 새로운 웹 프로토콜입니다. 보다 신속하게 정보를 전송할 수 있고 필요한 처리 능력을 줄일 수 있습니다. 이제 Dynamic Media 자산의 배달이 HTTP/2를 통해 수행될 수 있으므로 로드 시간이 향상됩니다.

Dynamic Media 계정에서 HTTP/2를 사용하는 시작에 대한 자세한 내용은 [HTTP2 컨텐츠 전달](http2.md)을 참조하십시오.
