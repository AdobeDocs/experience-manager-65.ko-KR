---
title: 웹 애플리케이션에 URL 연결
description: Dynamic Media에서 웹 애플리케이션에 URL을 연결하는 방법
uuid: cf599e66-b1f9-40c0-b572-cea19f2e6793
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: d12e6ea3-aaf4-4672-9679-3c16c76d7d5b
role: User, Admin
exl-id: d62275f0-02a4-48c9-bfb1-e23d63b618c9
feature: Configuration
source-git-commit: 78aa7aac838dabc1c4f0329520092e4755541322
workflow-type: tm+mt
source-wordcount: '1279'
ht-degree: 7%

---

# 웹 애플리케이션에 URL 연결 {#linking-urls-to-your-web-application}

웹 사이트 및 애플리케이션이 URL 호출을 통해 Dynamic Media 서비스에 액세스합니다. 자산을 게시하면 Dynamic Media에서 자산을 참조하는 URL 문자열을 활성화합니다. 이러한 URL을 테스트하기 위해 웹 브라우저에 붙여넣을 수 있습니다.

URL은 아래와 같은 경우에만 연결합니다 *not* Experience Manager을 WCM으로 사용. 연결 - 대 포함 - 비디오 플레이어를 팝업 또는 모달 창으로 전달하려는 경우 사용됩니다. Experience Manager을 WCM으로 사용하는 경우, [페이지에서 바로 자산을 추가합니다](adding-dynamic-media-assets-to-pages.md).

웹 페이지 및 애플리케이션에 이러한 URL 문자열을 배치하려면 Dynamic Media에서 복사합니다.

>[!NOTE]
>
>URL 문자열은 자산의 동적 변환에만 사용할 수 있습니다. 현재 Dynamic Media 서버가 아닌 DAM에 있는 정적 자산에 사용할 수 없습니다. 정적인 표현물에 대해서는 URL 단추가 표시되지 않습니다.

참조 - [웹 페이지에 비디오 또는 이미지 뷰어 포함](embed-code.md).

참조 - [웹 애플리케이션에 YouTube URL 연결](video.md).

참조 - [응답형 사이트용으로 최적화된 이미지 제공](responsive-site.md).

참조 - [자산 업로드](manage-assets.md#uploading-assets).

## 자산의 URL 가져오기 {#obtaining-a-url-for-an-asset}

이미지 사전 설정 또는 뷰어 사전 설정으로 생성된 URL 문자열을 가져올 수 있습니다. URL을 복사하면 클립보드에 로드되므로 웹 사이트 또는 애플리케이션의 페이지에 필요에 따라 붙여넣을 수 있습니다.

>[!NOTE]
>
>선택한 자산을 게시하기 전까지는 URL을 복사할 수 없습니다. 또한 뷰어 사전 설정 또는 이미지 사전 설정도 게시해야 합니다.
>
>자세한 내용은 [자산 게시](publishing-dynamicmedia-assets.md).
>
>자세한 내용은 [뷰어 사전 설정 게시](managing-viewer-presets.md#publishing-viewer-presets).
>
>자세한 내용은 [이미지 사전 설정 게시](managing-image-presets.md#publishing-image-presets).

URL 문자열을 가져오는 방법은 여러 가지가 있습니다. 그러나 아래 단계에서는 사용할 수 있는 한 가지 방법을 보여 줍니다.

**자산의 URL을 가져오려면 다음을 수행하십시오.**

1. 로 이동합니다 *게시됨* 복사할 이미지 사전 설정 URL 또는 뷰어 사전 설정 URL의 자산을 선택하고, 자산을 선택하여 엽니다.

   Remember that URLs are only available to copy *after* you have first *published* the assets. In addition, the viewer preset or image preset must also be published.

   자세한 내용은 [자산 게시](publishing-dynamicmedia-assets.md).

   자세한 내용은 [뷰어 사전 설정 게시](managing-viewer-presets.md#publishing-viewer-presets).

   자세한 내용은 [이미지 사전 설정 게시](managing-image-presets.md#publishing-image-presets).

1. 선택한 자산에 따라 다음 중 하나를 수행합니다.

   * 이미지를 선택한 경우, 드롭다운 메뉴에서 **[!UICONTROL 표현물]**.

      아래에 **[!UICONTROL 동적]** 제목, 오른쪽 프레임에서 해당 변환을 보려면 사전 설정된 이름을 선택합니다. 필요한 경우 표현물 목록을 스크롤하여 동적 제목을 확인합니다.

      왼쪽 레일 하단에서 을 선택합니다. **[!UICONTROL URL]**.

      ![chlimage_1-270](assets/chlimage_1-270.png)

   * 스핀 세트, 이미지 세트, 회전 메뉴 세트 또는 비디오를 선택한 경우, 드롭다운 메뉴에서 을 선택합니다 **[!UICONTROL 뷰어]**.

      왼쪽 레일에서 뷰어 사전 설정 이름을 선택합니다. 세트 또는 비디오의 미리 보기가 별도의 페이지에서 열립니다.

      왼쪽 레일의 하단에서 을 선택합니다 **[!UICONTROL URL]**.

      ![chlimage_1-271](assets/chlimage_1-271.png)

1. 자산을 미리 보거나 웹 컨텐츠 페이지에 추가할 수 있도록 텍스트를 선택하여 웹 브라우저에 복사합니다.

   URL 창을 종료하려면 **[!UICONTROL X]** 또는 **[!UICONTROL 닫기]**.

## 정적 자산의 URL 가져오기 {#obtaining-a-url-for-a-static-asset}

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

**정적 자산의 URL을 가져오려면 다음을 수행하십시오.**

1. 로 이동합니다 *게시됨* 복사할 URL이 있는 정적 자산과, 자산을 선택하여 엽니다.

   URL은 복사에만 사용할 수 있습니다 *after* 먼저 *게시됨* 정적 자산입니다.

   자세한 내용은 [자산 게시](publishing-dynamicmedia-assets.md).

1. 다음 방법 중 하나를 사용하여 게시된 정적 자산의 URL을 얻습니다.

   * `The URL of the published static is the following:`

      * `https://*<server_name>*/is/content/*<company_name>*/*<static_asset_filename>*.*<extension>*`

         (예: `https://aem.com/is/content/adobe/image.gif`)
   * 선택 **[!UICONTROL 자산]** > **[!UICONTROL 동적 표현물]**&#x200B;그런 다음 정적 자산의 동적 렌디션을 선택하고 URL을 복사합니다.

      복사된 URL을 사용하여 변경합니다 `is/content` 대신 경로에서 `is/image/`.


## 게시된 비디오 표현물에 대한 비디오 URL 가져오기 {#obtaining-a-video-url-for-a-published-video-rendition}

1. Experience Manager에서 **[!UICONTROL 도구]** > **[!UICONTROL 배포]** > **[!UICONTROL 클라우드]** > **[!UICONTROL Cloud Services]**.
1. 설정 **[!UICONTROL Cloud Services]** 페이지에서 아래로 스크롤하여 **[!UICONTROL Dynamic Media Cloud Services]** 제목을 선택한 후 **[!UICONTROL 구성 표시]**.
1. 아래 **[!UICONTROL 사용 가능한 구성]**&#x200B;를 클릭하고 원하는 구성 이름을 선택합니다.

1. 설정 **[!UICONTROL Dynamic Media Cloud 설정]** 페이지, 아래의 **[!UICONTROL 비디오 서비스 URL]**&#x200B;를 전체 URL 경로 아래에 복사합니다. 복사한 URL 경로를 단계의 후반부에 입력해야 합니다.

   예를 들어 URL 경로는 다음과 유사할 수 있습니다.

   `https://s7athens.macromedia.com:9090/DMGateway/`

   (위의 경로는 예만 해당됩니다. 복사한 실제 경로가 아닙니다.)

1. Under **[!UICONTROL Registration ID]**, copy the customer name found in the last part of the ID.

   예를 들어 등록 ID가 `87654321|MyCompany`, 고객 이름은 `MyCompany`.

1. 페이지의 왼쪽 위 모서리 근처에 있는 를 선택합니다. **[!UICONTROL Cloud Services]**&#x200B;로 이동한 다음 Experience Manager 로고를 선택하고 **[!UICONTROL 일반]** > **[!UICONTROL CRXDE Lite]**.
1. JCR(Java™ Content Repository)에서 전체 비디오 표현물 경로를 복사합니다.

   예를 들어 비디오의 변환 경로는 다음과 유사할 수 있습니다.

   `/_renditions_/0bd/0bd28743-a616-4fe6-92aa-6eae7c2112f/avs/Momentum_1080-0x720-2600k.mp4`

   (위의 경로는 예만 해당됩니다. 복사한 실제 경로가 아닙니다.)

1. 복사한 정보를 전체 URL 경로를 형성하도록 다음 순서로 배열합니다.

   `<Video_Service_URL>/public/<Customer_name_from_Registration_ID>/<Video_rendition_path>`

   예를 들어 위의 단계에서 경로 예와 고객 이름 예를 사용하여 전체 경로가 다음과 같이 표시됩니다.

   `https://s7athens.macromedia.com:9090/DMGateway/public/MyCompany/_renditions_/0bd/0bd28743-a616-4fe6-92aa-6eae7c2112ff/avs/Momentum_1080-0x720-2600k.mp4`

   이 예는 게시된 비디오 표현물을 위한 전체 비디오 URL입니다.

## 응용 비트율 스트리밍(DASH 또는 HLS)을 위한 비디오 URL 가져오기 {#obtaining-a-video-url-for-adaptive-streaming-hls}

1. Experience Manager에서 **[!UICONTROL 도구]** > **[!UICONTROL 배포]** > **[!UICONTROL 클라우드]** > **[!UICONTROL Cloud Services]**.
1. 설정 **[!UICONTROL Cloud Services]** 페이지에서 아래로 스크롤하여 **[!UICONTROL Dynamic Media Cloud Services]** 제목을 선택한 후 **[!UICONTROL 구성 표시]**.
1. 아래 **[!UICONTROL 사용 가능한 구성]**&#x200B;를 클릭하고 원하는 구성 이름을 선택합니다.
1. 설정 **[!UICONTROL Dynamic Media Cloud Services 설정]** 페이지에서 다음을 수행합니다.

   * 아래 **[!UICONTROL 비디오 서비스 URL]**&#x200B;를 눌러 전체 URL 경로를 복사합니다. 복사된 URL 경로는 이 단계의 후반부에 필요합니다. 예를 들어 URL 경로는 다음과 유사할 수 있습니다.

   `https://gateway-na.assetsadobe.com/DMGateway/`

   (위의 경로는 예만 해당됩니다. 복사한 실제 경로가 아닙니다.)

   * Under **[!UICONTROL Registration ID]**, copy the customer name found in the last part of the ID. You need the copied customer name later in these steps.

      예를 들어 등록 ID가 `87654321|demoCo`, 복사한 고객 이름은 `demoCo`.


1. 사용 중인 비디오 게재 프로토콜을 기준으로 각 프로토콜 선택기를 복사합니다. 이 단계의 후반부에 복사된 프로토콜 선택기가 필요합니다.

   | 사용 중인 비디오 게재 프로토콜 | 사용할 프로토콜 선택기 |
   |---|---|
   | HTTP <br> HTTP(비보안 비디오 게재)를 사용하는 경우 이전에 복사한 비디오 서비스 URL 값에서 https를 http로 변경해야 합니다. | `public/` |
   | HTTPS | `public-ssl/` |

1. Dynamic Media에서 처리한 대로 Experience Manager의 전체 비디오 자산 경로를 복사합니다. 이 복사한 비디오 자산 경로가 이 단계의 후반부에 필요합니다.

   예:

   `/content/dam/marketing/MyVideo.mp4`

1. 이전에 복사한 모든 조각을 결합하여 다음 순서로 문자열을 생성합니다.

   &lt; `video service URL`>&lt; `protocol selector`>&lt; `customer name`>&lt; `video asset path`>

   예를 들어 이러한 단계의 예에서 복사한 정보를 사용하여 문자열이 다음과 같이 표시됩니다.

   `https://gateway-na.assetsadobe.com/DMGateway/public-ssl/demoCo/content/dam/marketing/MyVideo.mp4`

1. 를 추가하여 URL을 완료합니다 `.m3u8` 를 클릭합니다. 예를 들어, `.m3u8` 이전 단계의 문자열에 다음과 같이 전체 URL 경로가 표시됩니다.

   `https://gateway-na.assetsadobe.com/DMGateway/public-ssl/demoCo/content/dam/marketing/MyVideo.mp4.m3u8`

## HTTP/2를 사용하여 Dynamic Media 자산을 전달합니다 {#using-http-to-deliver-your-dynamic-media-assets}

HTTP/2는 브라우저 및 서버의 통신 방식을 향상시키는 업데이트된 새로운 웹 프로토콜입니다. 보다 신속하게 정보를 전송할 수 있고 필요한 처리 능력을 줄일 수 있습니다. 이제 Dynamic Media 자산의 배달이 HTTP/2를 통해 수행될 수 있으므로 로드 시간이 향상됩니다.

자세한 내용은 [컨텐츠의 HTTP2 전달](http2.md) Dynamic Media 계정으로 HTTP/2 사용을 시작하는 방법에 대한 전체 세부 사항을 살펴보십시오.
