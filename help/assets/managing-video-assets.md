---
title: 비디오 에셋 관리
description: 에서 비디오 자산 업로드, 미리 보기, 주석 달기 및 게시 [!DNL Adobe Experience Manager].
contentOwner: AG
role: User
feature: Asset Management
exl-id: 21d3e0bd-5955-470a-8ca2-4d995c17eb4c
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '5499'
ht-degree: 8%

---

# 비디오 에셋 관리 {#manage-video-assets}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기를 클릭하십시오.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/manage-video-assets.html?lang=en) |
| AEM 6.5 | 이 문서 |

비디오 형식은 조직의 디지털 자산에 중요한 부분입니다. [!DNL Adobe Experience Manager] 에서는 비디오 자산이 만들어진 후 비디오 자산의 전체 라이프사이클을 관리하기 위한 성숙한 오퍼링과 기능을 제공합니다.

에서 비디오 자산을 관리하고 편집하는 방법을 알아봅니다 [!DNL Adobe Experience Manager Assets]. 예를 들어, FFmpeg 코드 변환 코딩 등의 비디오 인코딩과 코드 변환이 [!DNL Dynamic Media] 통합.

## 비디오 자산 업로드 및 미리 보기 {#upload-and-preview-video-assets}

[!DNL Adobe Experience Manager Assets] 에서는 확장 MP4를 사용하여 비디오 자산에 대한 미리 보기를 생성합니다. 자산의 형식이 MP4가 아닌 경우, FFmpeg 팩을 설치하여 미리 보기를 생성합니다. FFmpeg는 OGG 및 MP4 유형의 비디오 표현물을 만듭니다. 에서 표현물을 미리 볼 수 있습니다 [!DNL Assets] 사용자 인터페이스.

1. 디지털 자산 폴더 또는 하위 폴더에서 디지털 자산을 추가할 위치로 이동합니다.
1. 자산을 업로드하려면 **[!UICONTROL 만들기]** 도구 모음에서 **[!UICONTROL 파일]**. 또는 사용자 인터페이스에서 파일을 드래그합니다. 자세한 내용은 [자산 업로드](manage-assets.md#uploading-assets) 자세한 내용
1. 카드 보기에서 비디오를 미리 보려면 **[!UICONTROL 재생]** ![재생 옵션](assets/do-not-localize/play.png) 옵션 을 클릭합니다. 카드 보기에서만 비디오를 일시 중지하거나 재생할 수 있습니다. 다음 [!UICONTROL 재생] 및 [!UICONTROL 일시 정지] 목록 보기에서는 옵션을 사용할 수 없습니다.

1. 자산 세부 사항 페이지에서 비디오를 미리 보려면 **[!UICONTROL 편집]** 카드 위에 비디오는 브라우저의 기본 비디오 플레이어에서 재생됩니다. 비디오를 전체 화면으로 재생, 일시 정지, 볼륨 제어 및 확대/축소할 수 있습니다.

   ![비디오 재생 제어](assets/video-playback-controls.png)

## 2GB보다 큰 자산을 업로드하도록 구성 {#configuration-to-upload-assets-that-are-larger-than-gb}

기본적으로 [!DNL Assets] 에서는 파일 크기 제한으로 인해 2GB보다 큰 자산을 업로드할 수 없습니다. 그러나 CRXDE Lite으로 이동하여 아래에 노드를 만들어 이 제한을 덮어쓸 수 있습니다 `/apps` 디렉토리. 노드에는 동일한 노드 이름, 디렉토리 구조 및 이와 비교할 수 있는 노드 속성이 있어야 합니다.

추가 [!DNL Assets] 구성, 다음 구성을 변경하여 큰 자산을 업로드하십시오.

* 토큰 만료 시간을 늘립니다. 자세한 내용은 [!UICONTROL Adobe Granite CSRF 서블릿] 웹 콘솔에서 `https://[aem_server]:[port]/system/console/configMgr`. 자세한 내용은 [CSRF 보호](/help/sites-developing/csrf-protection.md).
* 를 늘립니다 `receiveTimeout` 참조하십시오. 자세한 내용은 [Experience Manager Dispatcher 구성](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#renders-options).

>[!NOTE]
>
>다음 [!DNL Experience Manager] 클래식 사용자 인터페이스에는 2GB 파일 크기 제한이 없습니다. 또한 큰 비디오에 대한 종단 간 워크플로우는 완전히 지원되지 않습니다.

더 높은 파일 크기 제한을 구성하려면 `/apps` 디렉토리.

1. in [!DNL Experience Manager]를 클릭합니다. **[!UICONTROL 도구]** > **[!UICONTROL 일반]** > **[!UICONTROL CRXDE Lite]**.
1. CRXDE Lite에서 `/libs/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`. 디렉토리 창을 보려면 `>>`.
1. 도구 모음에서 **[!UICONTROL 오버레이 노드]**. Alternatively, select **[!UICONTROL Overlay Node]** from the context menu.
1. 에서 **[!UICONTROL 오버레이 노드]** 대화 상자 **[!UICONTROL 확인]**.

   ![오버레이 노드](assets/overlay-node-path.png)

1. 브라우저를 새로 고칩니다. 오버레이 노드 `/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload` 이 선택되어 있습니다.
1. 에서 **[!UICONTROL 속성]** 탭에서 적절한 값(바이트)을 입력하여 크기 제한을 원하는 크기로 늘립니다. 예를 들어 크기 제한을 30GB로 늘리려면 를 입력합니다. `32212254720` 값.

1. 도구 모음에서 **[!UICONTROL 모두 저장]**.
1. in [!DNL Experience Manager]를 클릭합니다. **[!UICONTROL 도구]** > **[!UICONTROL 작업]** > **[!UICONTROL 웹 콘솔]**.
1. 설정 [!DNL Adobe Experience Manager] [!UICONTROL 웹 콘솔 번들] 페이지의 테이블의 이름 열 아래에서 를 찾은 다음 **[!UICONTROL Adobe Granite Workflow 외부 프로세스 작업 처리기]**.
1. 설정 [!UICONTROL Adobe Granite Workflow 외부 프로세스 작업 처리기] 페이지에서 두 시간 모두에 대한 초 수를 설정합니다. **[!UICONTROL 기본 시간 초과]** 및 **[!UICONTROL 최대 시간 초과]** 필드 대상 `18000` (5시간). **[!UICONTROL 저장]**&#x200B;을 클릭합니다.
1. in [!DNL Experience Manager]를 클릭합니다. **[!UICONTROL 도구]** > **[!UICONTROL 워크플로우]** > **[!UICONTROL 모델]**.
1. 워크플로우 모델 페이지에서 을 선택합니다 **[!UICONTROL Dynamic Media 인코딩 비디오]**&#x200B;를 클릭한 다음 **[!UICONTROL 편집]**.
1. 워크플로우 페이지에서 **[!UICONTROL Dynamic Media 비디오 서비스 프로세스]** 구성 요소.
1. In the [!UICONTROL Step Properties] dialog box, under the **[!UICONTROL Common]** tab, expand **Advanced Settings**.
1. 에서 **[!UICONTROL 시간 초과]** 필드, 값 지정 `18000`를 클릭한 다음 **[!UICONTROL 확인]** 로 돌아가기 **[!UICONTROL Dynamic Media 인코딩 비디오]** 워크플로우 페이지.
1. 페이지 상단 근처에 있는 [!UICONTROL Dynamic Media 인코딩 비디오] 페이지 제목 **[!UICONTROL 저장]**.

## 비디오 자산 게시 {#publish-video-assets}

게시 후 비디오 자산을 웹 페이지에 URL로 포함하거나 자산을 직접 포함할 수 있습니다. 자세한 내용은 [Dynamic Media 자산 게시](/help/assets/publishing-dynamicmedia-assets.md).

## YouTube에 비디오 게시 {#publishing-videos-to-youtube}

온-프레미스 Experience Manager 비디오 자산을 이전에 만든 YouTube 채널에 직접 게시할 수 있습니다.

비디오 자산을 YouTube에 게시하려면 태그가 있는 Experience Manager Assets을 설정합니다. 이러한 태그를 YouTube 채널과 연관시킵니다. 비디오 자산의 태그가 YouTube 채널의 태그와 일치하면 비디오가 YouTube에 게시됩니다. YouTube에 게시는 연결된 태그가 사용되는 한 비디오의 일반 게시와 함께 발생합니다.

YouTube은 자체 인코딩을 수행합니다. 따라서 Experience Manager에 업로드된 원본 비디오 파일은 Dynamic Media의 인코딩이 만들어진 비디오 변환 대신 YouTube에 게시됩니다. Dynamic Media을 사용하여 비디오를 처리할 필요는 없지만 재생에 뷰어 사전 설정이 필요한 경우 처리할 필요가 있습니다.

비디오 처리 프로필을 건너뛰고 YouTube에 바로 게시할 경우 Experience Manager 자산의 비디오 자산이 볼 수 있는 축소판을 가져오지 않음을 의미합니다. 즉, `dynamicmedia` 또는 `dynamicmedia_scene7` 인코딩되지 않은 비디오 실행 모드가 Dynamic Media 자산 유형에서 작동하지 않습니다.

YouTube 서버에 비디오 자산을 게시하려면 YouTube을 사용하여 안전하고 안전한 서버 간 인증을 위해 다음 작업을 완료해야 합니다.

1. [Google Cloud 설정 구성](#configuring-google-cloud-settings)
1. [YouTube 채널 만들기](#creating-a-youtube-channel)
1. [게시할 태그 추가](#adding-tags-for-publishing)
1. [YouTube 게시 복제 에이전트 활성화](#enabling-the-youtube-publish-replication-agent)
1. [Experience Manager에서 YouTube 설정](#setting-up-youtube-in-aem)
1. [(선택 사항) 업로드된 비디오에 대한 기본 YouTube 속성 설정을 자동화합니다](#optional-automating-the-setting-of-default-youtube-properties-for-your-uploaded-videos)
1. [YouTube 채널에 비디오 게시](#publishing-videos-to-your-youtube-channel)
1. [(선택 사항) YouTube에서 게시된 비디오를 확인합니다](/help/assets/video.md#optional-verifying-the-published-video-on-youtube)
1. [웹 애플리케이션에 YouTube URL 연결](#linking-youtube-urls-to-your-web-application)

다음을 수행할 수도 있습니다 [YouTube에서 제거할 비디오 게시 취소](#unpublishing-videos-to-remove-them-from-youtube).

### Google Cloud 설정 구성 {#configuring-google-cloud-settings}

YouTube에 게시하려면 Google 계정이 필요합니다. GMAIL 계정이 있는 경우 이미 Google 계정이 있습니다. Google 계정이 없는 경우 쉽게 만들 수 있습니다. 비디오 자산을 YouTube에 게시하려면 자격 증명이 필요하므로 계정이 필요합니다. 계정을 이미 만든 경우 이 작업을 건너뛰고 바로 다음 작업을 진행합니다 [YouTube 채널 만들기](#creating-a-youtube-channel).

Google Cloud와 YouTube에 사용된 Google 계정에 사용된 계정이 동일할 필요가 없습니다.

Google은 사용자 인터페이스를 주기적으로 변경합니다. 따라서 YouTube에 비디오를 게시하는 단계는 아래에 설명된 것과 약간 다를 수 있습니다. 이 주의 사항은 비디오가 업로드되었는지를 확인하려고 할 때도 YouTube에 적용됩니다.

>[!NOTE]
>
>다음 단계는 이 작성 시 정확했습니다. 그러나 Google은 사전 통지 없이 정기적으로 웹 사이트를 업데이트합니다. 따라서 이러한 단계는 약간 다를 수 있습니다.

Google Cloud 설정을 구성하려면:

1. Google 계정을 만듭니다.
   [https://accounts.google.com/SignUp?service=mail](https://accounts.google.com/SignUp?service=mail)

   이미 Google 계정이 있는 경우 다음 단계로 건너뜁니다.

1. 이동 [https://cloud.google.com/](https://cloud.google.com/).
1. On the Google Cloud page, near the upper-right corner, click **[!UICONTROL Console]**.

   필요한 경우 **[!UICONTROL 로그인]** Google 계정 자격 증명을 사용하여 확인 **[!UICONTROL 콘솔]** 선택 사항입니다.

1. 대시보드 페이지의 오른쪽 **[!UICONTROL Google Cloud Platform]**&#x200B;프로젝트 드롭다운 목록을 클릭하여 프로젝트 선택 대화 상자를 엽니다.
1. 프로젝트 선택 대화 상자에서 **[!UICONTROL 새 프로젝트]**.

   ![6_5_googleaccount-newproject](assets/6_5_googleaccount-newproject.png)

1. 새 프로젝트 대화 상자의 프로젝트 이름 필드에 새 프로젝트의 이름을 입력합니다.

   프로젝트 ID는 프로젝트 이름을 기반으로 합니다. 따라서 프로젝트 이름을 신중하게 선택합니다. 만든 후에는 변경할 수 없습니다. 또한 나중에 Experience Manager에서 YouTube을 설정할 때 동일한 프로젝트 ID를 다시 입력해야 합니다. 그것을 적는 것을 고려해 보십시오.

1. **[!UICONTROL 만들기]**&#x200B;를 클릭합니다.

1. 다음 중 하나를 수행합니다.

   * 프로젝트의 대시보드의 시작하기 카드에서 **[!UICONTROL API 탐색 및 활성화]**.
   * 프로젝트의 대시보드의 API 카드에서 를 누릅니다 **[!UICONTROL API 개요로 이동]**.

   ![6_5_googleaccount-apis-enable2](assets/6_5_googleaccount-apis-enable2.png)

1. API 및 서비스 페이지의 상단 근처에 있는 **[!UICONTROL API 및 서비스 활성화]**.
1. API 라이브러리 페이지의 왼쪽에 있는 **[!UICONTROL 카테고리]**, 탭 **[!UICONTROL YouTube]**. 페이지 오른쪽에서 **[!UICONTROL YouTube 데이터 API]**.
1. YouTube Data API v3 페이지에서 **[!UICONTROL 활성화]**.

   ![6_5_googleaccount-apis-enable3](assets/6_5_googleaccount-apis-enable3.png)

1. API를 사용하려면 자격 증명이 필요합니다. 필요한 경우 **[!UICONTROL 자격 증명 만들기]**.

   ![6_5_googleaccount-apis-createcreatecredentials](assets/6_5_googleaccount-apis-createcredentials.png)

1. 설정 **[!UICONTROL 프로젝트에 자격 증명 추가]** 페이지, 1단계에서 다음을 수행합니다.

   * 에서 **[!UICONTROL 어떤 API를 사용하고 있습니까?]** 드롭다운 목록에서 **[!UICONTROL YouTube 데이터 API v3]**.

   * 에서 **[!UICONTROL API는 어디에서 호출합니까?]** 드롭다운 목록에서 **[!UICONTROL 웹 서버(예: node.js, Tomcat)]**

   * 에서 **[!UICONTROL 어떤 데이터에 액세스하고 있습니까?]** 드롭다운 목록에서 **[!UICONTROL 사용자 데이터]**.

   ![6_5_googleaccount-apis-createcredentials2](assets/6_5_googleaccount-apis-createcredentials2.png)

1. 탭 **[!UICONTROL 어떤 자격 증명이 필요합니까?]**
1. On the **[!UICONTROL Add credentials to your project]** page, step 2, under the **[!UICONTROL Create an OAuth 2.0 client ID]** heading, in the Name field, enter a unique name if desired. Or, you can use the default name specified by Google.
1. 아래에 **[!UICONTROL 인증된 JavaScript 원본]** 텍스트 필드에 다음 경로를 입력하고 경로에 고유한 도메인과 포트 번호를 바꾼 다음 키를 누릅니다 **[!UICONTROL Enter 키]** 목록에 경로를 추가하려면 다음을 수행합니다.

   `https://<servername.domain>:<port_number>`

   예, `https://1a2b3c.mycompany.com:4321`

   **참고**: 위의 경로 예는 데모용으로만 사용됩니다.

   ![6_5_googleaccount-apis-createcredentials-oauth](assets/6_5_googleaccount-apis-createcredentials-oauth.png)

1. 아래에 **[!UICONTROL 허가된 리디렉션 URI]** 텍스트 필드에 다음 경로를 입력하고 경로에 고유한 도메인과 포트 번호를 바꾼 다음 키를 누릅니다 **[!UICONTROL Enter 키]** 목록에 경로를 추가하려면 다음을 수행합니다.

   `https://<servername.domain>:<port_number>/etc/cloudservices/youtube.youtubecredentialcallback.json`

   예, `https://1a2b3c.mycompany.com:4321/etc/cloudservices/youtube.youtubecredentialcallback.json`

   **참고**: 위의 경로 예는 데모용으로만 사용됩니다.

1. 클릭 **[!UICONTROL OAuth 클라이언트 ID 만들기]**.
1. On the **[!UICONTROL Add credentials to your project]** page, step 3, under the **[!UICONTROL Set up the OAuth 2.0 consent screen]** heading, select the Gmail email address that you are currently using.

   ![6_5_googleaccount-apis-createcredentials-consenscreen](assets/6_5_googleaccount-apis-createcredentials-consentscreen.png)

1. 아래에 **[!UICONTROL 사용자에게 표시되는 제품 이름]** 제목 텍스트 필드에 동의 화면에 표시할 내용을 입력합니다.

   Experience Manager 관리자가 YouTube을 인증할 때 동의 화면이 표시됩니다. Experience Manager은 YouTube에 권한을 요청하십시오.

1. **[!UICONTROL 계속]**&#x200B;을 클릭합니다.
1. On the Add credentials to your project page, step 4, under the **[!UICONTROL Download credentials]** heading, tap **[!UICONTROL Download]**.

   ![6_5_googleaccount-apis-createcredentials-downloadcredentials](assets/6_5_googleaccount-apis-createcredentials-downloadcredentials.png)

1. 를 저장합니다 `client_id.json` 파일.

   나중에 Adobe Experience Manager에서 YouTube을 설정할 때 이 다운로드한 json 파일이 필요합니다.

1. 클릭 **[!UICONTROL 완료]**.

   Google 계정에서 로그아웃합니다. 이제 YouTube 채널을 만듭니다.

### YouTube 채널 만들기 {#creating-a-youtube-channel}

YouTube에 비디오를 게시하려면 하나 이상의 채널이 있어야 합니다. YouTube 채널을 이미 만든 경우 이 작업을 건너뛰고 로 이동할 수 있습니다. [게시할 태그 추가](/help/assets/video.md#adding-tags-for-publishing).

>[!WARNING]
>
>YouTube에서 이미 하나 이상의 채널을 설정했는지 확인하십시오 *이전* Experience Manager의 YouTube 설정에서 채널을 추가합니다( [Experience Manager에서 YouTube 설정](#setting-up-youtube-in-aem) 아래에 표시됩니다. 하나 이상의 채널을 설정하지 않으면 존재하지 않는 채널에 대한 경고가 표시되지 않습니다. 그러나 채널을 추가할 때는 Google 인증이 계속 발생하지만 비디오가 전송되는 채널을 선택할 수 있는 옵션이 없습니다.

**YouTube 채널을 만들려면:**

1. 이동 [https://www.youtube.com](https://www.youtube.com/) Google 계정 자격 증명을 사용하여 로그인합니다.
1. YouTube 페이지의 오른쪽 위 모서리에서 프로필 사진(단색 원 내에 문자로 표시될 수 있음)을 클릭한 다음 을 클릭합니다 **[!UICONTROL YouTube 설정]** (라운드 톱니바퀴 아이콘).
1. 개요 페이지의 추가 기능 제목 아래에서 **[!UICONTROL 내 채널을 모두 보거나 채널을 만듭니다]**.
1. 채널 페이지에서 **[!UICONTROL 새 채널 만들기]**.
1. 브랜드 계정 페이지의 브랜드 계정 이름 필드에 비디오 자산을 게시하려는 위치에 비즈니스 이름 또는 다른 채널 이름을 입력한 다음 을 클릭합니다 **[!UICONTROL 만들기]**.

   Experience Manager에서 YouTube을 설정할 때 다시 입력해야 하므로 여기에 입력하는 이름을 기억하십시오.

1. (선택 사항) 필요한 경우 채널을 더 추가합니다.

   이제 게시할 태그를 추가합니다.

### 게시할 태그 추가 {#adding-tags-for-publishing}

비디오를 YouTube에 게시하려면 Experience Manager은 태그를 하나 이상의 YouTube 채널에 연결합니다. 게시할 태그를 추가하려면 [태그 관리](/help/sites-administering/tags.md).

또는 Experience Manager에서 기본 태그를 사용하려는 경우 이 작업을 건너뛰고 로 이동할 수 있습니다. [YouTube 게시 복제 에이전트 활성화](#enabling-the-youtube-publish-replication-agent).

### YouTube 게시 복제 에이전트 활성화 {#enabling-the-youtube-publish-replication-agent}

YouTube 게시 복제 에이전트를 활성화한 후 Google Cloud 계정에 대한 연결을 테스트하려면 을(를) 탭합니다 **[!UICONTROL 연결 테스트]**. 브라우저 탭에 연결 결과가 표시됩니다. YouTube 채널을 추가한 경우 목록의 일부가 테스트의 일부로 표시됩니다.

1. Experience Manager의 왼쪽 위 모서리에서 Experience Manager 로고를 클릭한 다음 왼쪽 레일에서 를 클릭합니다 **[!UICONTROL 도구]** > **[!UICONTROL 배포]** > **[!UICONTROL 복제]** > **[!UICONTROL 작성자의 에이전트]**.
1. 작성자 에이전트 페이지에서 **[!UICONTROL YouTube 게시]**.
1. 도구 모음에서 설정 오른쪽의 **[!UICONTROL 편집]**.
1. 을(를) 선택합니다 **[!UICONTROL 활성화됨]** 복제 에이전트를 설정할 수 있도록 확인란을 선택합니다.
1. **[!UICONTROL 확인]**&#x200B;을 클릭합니다.

   이제 Experience Manager에서 YouTube을 설정합니다.

### Experience Manager에서 YouTube 설정 {#setting-up-youtube-in-aem}

Experience Manager 6.4부터 Experience Manager에서 YouTube 게시를 설정하는 새로운 터치 사용자 인터페이스 방법이 도입되었습니다. 사용 중인 Experience Manager의 설치된 인스턴스에 따라 다음 중 하나를 수행합니다.

* 6.4 이전 Experience Manager에서 YouTube을 구성하려면 다음을 참조하십시오 [6.4 이전 Experience Manager에서 YouTube 설정](/help/assets/video.md#setting-up-youtube-in-aem-before).
* Experience Manager 6.4 이상에서 YouTube을 구성하려면 다음을 참조하십시오 [Experience Manager 6.4 이상에서 YouTube 설정](#setting-up-youtube-in-aem-and-later).

#### Experience Manager 6.4 이상에서 YouTube 설정 {#setting-up-youtube-in-aem-and-later}

1. 관리자로 Dynamic Media 인스턴스에 로그인해야 합니다.
1. 왼쪽 위 모서리에서 Experience Manager 로고를 탭한 다음, 왼쪽 레일에서 를 탭합니다 **[!UICONTROL 도구]**(망치 아이콘) > **[!UICONTROL Cloud Services]** > **[!UICONTROL YouTube 게시 구성]**.
1. 탭 **[!UICONTROL 글로벌]** (선택하지 마십시오.)

1. 글로벌 페이지의 오른쪽 위 모서리 근처에 있는 **[!UICONTROL 만들기]**.
1. On the Create YouTube Configuration page, under Google Cloud Platform Settings, in the **[!UICONTROL Application Name]** field, enter the Google Project ID.

   처음에 Google Cloud 설정을 구성할 때 프로젝트 ID를 지정했습니다.
YouTube 구성 만들기 페이지를 열어 둡니다. 잠시 후에, 당신은 그것에 대해 돌아올 것입니다.

   ![6_5_youtubepublish-createyoutubeconfiguration](assets/6_5_youtubepublish-createyoutubeconfiguration.png)

1. 일반 텍스트 편집기를 사용하여 작업에서 이전에 다운로드하여 저장한 JSON 파일을 엽니다 [Google Cloud 설정 구성](/help/assets/video.md#configuring-google-cloud-settings).
1. 전체 JSON 텍스트를 선택하고 복사합니다.
1. Return to the YouTube Account Settings dialog box. In the **[!UICONTROL JSON Config]** field, paste the JSON text.
1. 페이지의 오른쪽 위 모서리 근처에 있는 탭하기 **[!UICONTROL 저장]**.

   이제 Experience Manager에서 YouTube 채널을 설정합니다.

1. 탭 **[!UICONTROL 채널 추가]**.
1. 채널 이름 필드에 작업에서 만든 채널의 이름을 입력합니다 **[!UICONTROL YouTube에 하나 이상의 채널 추가]** 더 일찍

   원하는 경우 설명을 선택적으로 추가할 수 있습니다.

1. 탭 **[!UICONTROL 추가]**.
1. YouTube/Google 인증이 표시됩니다. Google Cloud 계정에 아직 로그인하지 않은 경우 이 단계를 건너뜁니다.

   * Google 프로젝트 ID 및 위의 JSON 텍스트와 연결된 Google 사용자 이름 및 암호를 입력합니다.
   * 계정에 두 개 이상의 항목이 표시되는 채널 수에 따라 다릅니다. 채널을 선택합니다. 전자 메일 주소를 선택하지 마십시오; 채널이 아닙니다.
   * 다음 페이지에서 **[!UICONTROL 수락]** 이 채널에 대한 액세스를 허용합니다.

1. 탭 **[!UICONTROL 허용]**.

   이제 게시할 태그를 설정합니다.

1. **[!UICONTROL 게시할 태그 설정]** - Cloud Services > YouTube 페이지에서 연필 아이콘을 탭하여 사용할 태그 목록을 편집합니다.
1. Experience Manager에 사용 가능한 태그 목록을 표시할 수 있도록 드롭다운 목록 아이콘(위/아래 캐럿)을 누릅니다.
1. 태그를 추가할 수 있도록 하나 이상의 태그를 탭합니다.

   추가한 태그를 삭제하려면 태그를 선택하고 **[!UICONTROL X]**.

1. 원하는 태그를 추가했으면 을 누릅니다 **[!UICONTROL 저장]**.

   이제 비디오를 YouTube 채널에 게시합니다.

#### 6.4 이전 Experience Manager에서 YouTube 설정 {#setting-up-youtube-in-aem-before}

1. 관리자로 Dynamic Media 인스턴스에 로그인해야 합니다.

1. 왼쪽 위 모서리에서 Experience Manager 로고를 탭한 다음, 왼쪽 레일에서 를 탭합니다 **[!UICONTROL 도구]** (망치 아이콘) > **[!UICONTROL 배포]** > **[!UICONTROL Cloud Services]**.
1. 타사 서비스 제목 아래에 있는 YouTube에서 **[!UICONTROL 지금 구성]**.
1. 구성 만들기 대화 상자의 각 필드에 제목(필수)과 이름(선택 사항)을 입력합니다.
1. 탭 **[!UICONTROL 만들기]**.
1. In the YouTube Account Settings dialog box, in the **[!UICONTROL Application Name]** field, enter the Google Project ID.

   처음에 프로젝트 ID를 지정한 경우 [구성된 Google Cloud 설정](/help/assets/video.md#configuring-google-cloud-settings) 더 일찍
YouTube 계정 설정 대화 상자를 열어 둡니다. 곧 다시 돌아올 겁니다.

1. 일반 텍스트 편집기를 사용하여 Google Cloud 설정 구성 작업에서 이전에 다운로드하여 저장한 JSON 파일을 엽니다.
1. 전체 JSON 텍스트를 선택하고 복사합니다.
1. Return to the YouTube Account Settings dialog box. In the **[!UICONTROL JSON Config]** field, paste the JSON text.
1. 탭 **[!UICONTROL 확인]**.

   이제 Experience Manager에서 YouTube 채널을 설정합니다.

1. To the right of **[!UICONTROL Available Channels]**, tap **+** (plus sign icon).
1. In the YouTube Channel Settings dialog box, in the Title field, enter the name of the channel that you created in the task **[!UICONTROL Adding one or more channels to YouTube]** earlier.

   원하는 경우 설명을 선택적으로 추가할 수 있습니다.

1. 탭 **[!UICONTROL 확인]**.
1. YouTube/Google 인증이 표시됩니다. Google Cloud 계정에 아직 로그인하지 않은 경우 이 단계를 건너뜁니다.

   * Google 프로젝트 ID 및 위의 JSON 텍스트와 연결된 Google 사용자 이름 및 암호를 입력합니다.
   * 계정에 두 개 이상의 항목이 표시되는 채널 수에 따라 다릅니다. 채널을 선택합니다. 전자 메일 주소를 선택하지 마십시오; 채널이 아닙니다.
   * 다음 페이지에서 **[!UICONTROL 수락]** 이 채널에 대한 액세스를 허용합니다.

1. 탭 **[!UICONTROL 허용]**.

   이제 게시할 태그를 설정합니다.

1. **[!UICONTROL 게시할 태그 설정]** - Cloud Services > YouTube 페이지에서 연필 아이콘을 탭하여 사용할 태그 목록을 편집합니다.
1. Experience Manager에 사용 가능한 태그 목록을 표시할 수 있도록 드롭다운 목록 아이콘(위/아래 캐럿)을 누릅니다.
1. 태그를 추가할 수 있도록 하나 이상의 태그를 탭합니다.

   추가한 태그를 삭제하려면 태그를 선택하고 **X**.

1. 원하는 태그를 추가했으면 을 누릅니다 **[!UICONTROL 확인]**.

   이제 비디오를 YouTube 채널에 게시합니다.

### (선택 사항) 업로드된 비디오에 대한 기본 YouTube 속성 설정을 자동화합니다 {#optional-automating-the-setting-of-default-youtube-properties-for-your-uploaded-videos}

선택적으로 Experience Manager에서 메타데이터 처리 프로필을 만들어 비디오 업로드 시 YouTube 속성 설정을 자동화할 수 있습니다.

To create the metadata processing profile, you are first going to copy values from the **[!UICONTROL Field Label]**, **[!UICONTROL Map to property]**, and **[!UICONTROL Choices]** fields, all found in Metadata Schemas for video. Then, you build your YouTube video metadata processing profile by adding those values to it.

업로드한 비디오에 대한 기본 YouTube 속성 설정을 자동화하는 방법은 다음과 같습니다.

1. 왼쪽 위 모서리에서 Experience Manager 로고를 탭한 다음, 왼쪽 레일에서 를 클릭합니다 **[!UICONTROL 도구]** (망치 아이콘) > **[!UICONTROL 자산]** > **[!UICONTROL 메타데이터 스키마]**.
1. 클릭 **[!UICONTROL 기본]**. (선택 상자에 &quot;기본값&quot; 왼쪽에 선택 표시를 추가하지 마십시오.)
1. 설정 **[!UICONTROL 기본]** 페이지의 왼쪽에 있는 상자를 선택합니다. **[!UICONTROL 비디오]**&#x200B;를 탭한 다음, **[!UICONTROL 편집]**.
1. 메타데이터 스키마 편집기 페이지에서 **[!UICONTROL 고급]** 탭.
1. Under the YouTube Publishing heading, click **[!UICONTROL YouTube Category]**.
1. 페이지 오른쪽의 아래에서 **[!UICONTROL 설정]** 탭에서 다음을 수행합니다.

   * 에서 **[!UICONTROL 속성에 매핑]** 텍스트 필드에서 값을 선택하고 복사합니다.
복사한 값을 열려 있는 텍스트 편집기에 붙여넣습니다. 메타데이터 처리 프로필을 만들 때 나중에 이 값이 필요합니다. 텍스트 편집기를 열어 둡니다.

   * 아래 **[!UICONTROL 선택 사항]**을(를) 선택하고 사용할 기본값(예: 사용자 및 블로그 또는 과학 및 기술)을 복사합니다.
복사한 값을 열려 있는 텍스트 편집기에 붙여넣습니다. 메타데이터 처리 프로필을 만들 때 나중에 이 값이 필요합니다. 텍스트 편집기를 열어 둡니다.

1. YouTube 게시 제목 아래에서 **[!UICONTROL YouTube 개인 정보]**.
1. 페이지 오른쪽의 아래에서 **[!UICONTROL 설정]** 탭에서 다음을 수행합니다.

   * 에서 **[!UICONTROL 속성에 매핑]** 텍스트 필드에서 값을 선택하고 복사합니다.
복사한 값을 열려 있는 텍스트 편집기에 붙여넣습니다. 메타데이터 처리 프로필을 만들 때 나중에 이 값이 필요합니다. 텍스트 편집기를 열어 둡니다.

   * 아래 **[!UICONTROL 선택 사항]**을(를) 선택하고 사용할 기본값을 복사합니다. 선택 사항은 두 쌍으로 그룹화됩니다. 쌍의 맨 아래 필드는 공용, 비상장 또는 개인 등의 복사할 기본값입니다.
복사한 값을 열려 있는 텍스트 편집기에 붙여넣습니다. 메타데이터 처리 프로필을 만들 때 나중에 이 값이 필요합니다. 텍스트 편집기를 열어 둡니다.

1. [메타데이터 스키마 편집기] 페이지의 오른쪽 위 모서리 근처에 있는 **[!UICONTROL 취소]**.
1. Experience Manager의 왼쪽 위 모서리에서 Experience Manager 로고를 탭한 다음 왼쪽 레일에서 를 클릭합니다 **[!UICONTROL 도구]** (망치 아이콘) > **[!UICONTROL 자산]** > **[!UICONTROL 메타데이터 프로필]**.

1. 페이지의 오른쪽 위 모서리 근처에 있는 메타데이터 프로필 페이지에서 을 클릭합니다. **[!UICONTROL 만들기]**.
1. In the Add Metadata Profile dialog box, in the **[!UICONTROL Profile title]** text field, enter the name `YouTube Video` then click **[!UICONTROL Create]**.
1. 메타데이터 프로필 편집기 페이지에서 **[!UICONTROL 고급]** 탭.
1. 다음을 수행하여 복사된 YouTube 게시 값을 프로필에 추가합니다.

   * 페이지 오른쪽에서 **[!UICONTROL 양식 작성]** 탭.
   * (선택 사항) 레이블이 지정된 구성 요소를 드래그합니다. **[!UICONTROL 섹션 헤더]** 왼쪽에 놓고 양식 영역에 놓습니다.
   * (선택 사항) **[!UICONTROL 필드 레이블]** 를 클릭하여 구성 요소를 선택합니다.
   * (선택 사항) 페이지의 오른쪽의 설정 탭의 필드 레이블 텍스트 필드에 를 입력합니다 `YouTube Publishing`.
   * 을(를) 클릭합니다. **[!UICONTROL 양식 작성]** 탭을 클릭한 다음 레이블이 지정된 구성 요소를 드래그합니다. **[!UICONTROL 다중 값 텍스트]** 아래에 놓고 **[!UICONTROL YouTube 게시]** 만든 제목.

   * 클릭 **[!UICONTROL 필드 레이블]** 따라서 구성 요소가 선택됩니다.
   * 페이지 오른쪽의 설정 탭에서 이전에 복사한 YouTube 게시 값(필드 레이블 값 및 속성 값에 매핑)을 양식의 해당 필드에 붙여 넣습니다. 선택 사항 값을 기본값 필드에 붙여넣습니다.

1. 다음을 수행하여 복사된 YouTube 개인 정보 보호 값을 프로필에 추가합니다.

   * 페이지 오른쪽에서 **[!UICONTROL 양식 작성]** 탭.
   * (선택 사항) 레이블이 지정된 구성 요소를 드래그합니다. **[!UICONTROL 섹션 헤더]** 왼쪽에 놓고 양식 영역에 놓습니다.
   * (선택 사항) **[!UICONTROL 필드 레이블]** 를 클릭하여 구성 요소를 선택합니다.
   * (선택 사항) 페이지의 오른쪽의 설정 탭의 필드 레이블 텍스트 필드에 를 입력합니다 `YouTube Privacy`.
   * 을(를) 클릭합니다. **[!UICONTROL 양식 작성]** 탭을 클릭한 다음 레이블이 지정된 구성 요소를 드래그합니다. **[!UICONTROL 다중 값 텍스트]** 아래에 놓고 **[!UICONTROL YouTube 개인 정보]** 만든 제목.

   * 클릭 **[!UICONTROL 필드 레이블]** 따라서 구성 요소가 선택됩니다.
   * 페이지 오른쪽의 설정 탭에서 이전에 복사한 YouTube 게시 값(필드 레이블 값 및 속성 값에 매핑)을 양식의 해당 필드에 붙여 넣습니다. 선택 사항 값을 기본값 필드에 붙여넣습니다.

1. Near the upper-right corner of the page, click **[!UICONTROL Save]**.
1. 비디오를 업로드할 폴더에 YouTube 게시 메타데이터 프로필을 적용합니다. 메타데이터 프로필과 비디오 프로필 세트가 모두 있어야 합니다.

   See [Metadata Profiles](/help/assets/metadata-config.md#metadata-profiles) and [Video Profiles](/help/assets/video-profiles.md).

### YouTube 채널에 비디오 게시 {#publishing-videos-to-your-youtube-channel}

이제 이전에 비디오 자산에 추가한 태그를 연결합니다. 이 프로세스를 통해 Experience Manager은 YouTube 채널에 게시할 자산을 알 수 있습니다.

>[!NOTE]
>
>Dynamic Media - Scene7 모드에서 실행할 때 게시가 즉시 YouTube에 자동으로 게시되지 않습니다. Dynamic Media - Scene7 모드가 설정되면, 다음 두 가지 게시 옵션 중에서 선택할 수 있습니다. **[!UICONTROL 즉시]** 또는 **[!UICONTROL 활성화 시]**.
>
>**[!UICONTROL 즉시 게시]** 은(는) 업로드된 자산이 IPS와 동기화된 후 게재 시스템에 자동으로 게시됨을 의미합니다. Dynamic Media에게 이는 사실이지만 YouTube에게는 그렇지 않습니다. YouTube에 게시하려면 Experience Manager 작성자를 통해 게시해야 합니다.

>[!NOTE]
>
>YouTube에서 컨텐츠를 게시하기 위해 Experience Manager은 **[!UICONTROL YouTube에 게시]** 작업 과정: 진행 상황을 모니터링하고 실패 정보를 볼 수 있습니다.
>
>자세한 내용은 [비디오 인코딩 및 YouTube 게시 진행 모니터링](#monitoring-video-encoding-and-youtube-publishing-progress).
>
>자세한 진행 정보를 보려면 복제 중인 YouTube 로그를 모니터링할 수 있습니다. 그러나 이러한 모니터링에는 관리자 액세스 권한이 필요합니다.

**비디오를 YouTube 채널에 게시하려면:**

1. Experience Manager에서 YouTube 채널에 게시할 비디오 자산으로 이동합니다.
1. 비디오 자산(응용 비디오 세트)을 선택합니다.
1. 도구 모음에서 **[!UICONTROL 속성]**.
1. 기본 탭의 메타데이터 머리글에서 **[!UICONTROL 선택 대화 상자 열기]** 태그 필드의 오른쪽에 있습니다.
1. 태그 선택 페이지에서 사용할 태그로 이동한 다음, 태그를 하나 이상 선택합니다.

   태그는 YouTube 채널과 연결되어 있어야 합니다.

1. 페이지의 오른쪽 위 모서리에서 **[!UICONTROL 선택]**.
1. 비디오 속성 페이지의 오른쪽 위 모서리에서 을(를) 클릭합니다 **[!UICONTROL 저장 후 닫기]**.
1. 도구 모음에서 **[!UICONTROL 빠른 게시]**.

   참조 - [Experience Manager Sites에서 게시 관리 사용](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/page-authoring/publication-management-feature-video-use.html).

   YouTube 채널에서 게시된 비디오를 선택적으로 확인할 수 있습니다.

### (선택 사항) YouTube에서 게시된 비디오를 확인합니다 {#optional-verifying-the-published-video-on-youtube}

선택적으로 YouTube 게시(또는 게시 취소)의 진행 상황을 모니터링할 수 있습니다.

자세한 내용은 [비디오 인코딩 및 YouTube 게시 진행 모니터링](#monitoring-video-encoding-and-youtube-publishing-progress).

게시 시간은 기본 소스 비디오의 형식, 파일 크기 및 업로드 트래픽이 포함된 여러 요인에 따라 크게 달라질 수 있습니다. 게시 프로세스는 몇 분에서 몇 시간 정도 걸릴 수 있습니다. 또한 고해상도 포맷이 훨씬 느리게 렌더링됩니다. 예를 들어 720p와 1080p는 480p보다 오래 걸립니다.

8시간 후에도 상태 메시지가 계속 표시되면 **[!UICONTROL 업로드됨(처리 중입니다. 잠시 기다려 주십시오.)]**&#x200B;의 웹 사이트에서 비디오를 제거하고 다시 업로드해 보십시오.

### 웹 애플리케이션에 YouTube URL 연결 {#linking-youtube-urls-to-your-web-application}

비디오를 게시한 후 Dynamic Media에서 생성한 YouTube URL 문자열을 가져올 수 있습니다. YouTube URL을 복사하면 클립보드에 로드되므로 웹 사이트 또는 애플리케이션의 페이지에 필요에 따라 붙여넣을 수 있습니다.

>[!NOTE]
>
>YouTube URL은 비디오 자산을 YouTube에 게시하기 전까지 복사할 수 없습니다.

**YouTube URL을 웹 애플리케이션에 연결하려면**

1. 로 이동합니다 *YouTube 게시됨* 복사할 URL이 있는 비디오 자산을 선택한 다음 선택합니다.

   YouTube URL은 복사에만 사용할 수 있습니다 *after* 먼저 *게시됨* 비디오 자산을 YouTube에 추가합니다.

1. 도구 모음에서 **[!UICONTROL 속성]**.
1. 을(를) 클릭합니다. **[!UICONTROL 고급]** 탭.
1. YouTube 게시 제목 아래의 YouTube URL 목록에서 URL 텍스트를 선택하고 웹 브라우저에 복사하여 자산을 미리 보거나 웹 컨텐츠 페이지에 추가합니다.

### YouTube에서 제거할 수 있도록 비디오 게시 취소 {#unpublishing-videos-to-remove-them-from-youtube}

Experience Manager에서 비디오 자산 게시를 취소하면 비디오가 YouTube에서 제거됩니다.

>[!CAUTION]
>
>YouTube 내에서 직접 비디오를 제거하는 경우, Experience Manager은 이를 인식하지 못하고 비디오가 YouTube에 아직 게시되어 있는 것처럼 계속 동작합니다. 항상 Experience Manager 방식으로 YouTube에서 비디오 자산 게시를 취소합니다.

>[!NOTE]
>
>YouTube에서 컨텐츠를 제거하려면 Experience Manager은 **[!UICONTROL YouTube에서 게시 취소]** 작업 과정: 진행 상황을 모니터링하고 실패 정보를 볼 수 있습니다.
>
>자세한 내용은 [비디오 인코딩 및 YouTube 게시 진행 모니터링](#monitoring-video-encoding-and-youtube-publishing-progress).

**YouTube에서 제거할 비디오 게시를 취소하려면,**

1. YouTube 채널에서 게시를 취소하려는 비디오 자산으로 이동합니다.
1. 자산 선택 모드에서 하나 이상의 게시된 비디오 자산을 선택합니다.
1. 도구 모음에서 **[!UICONTROL 게시 관리]**. 세 점 아이콘()을 누릅니다. . ) 도구 모음에서 **[!UICONTROL 게시 관리]** 엽니다.
1. 게시 관리 페이지에서 **[!UICONTROL 게시 취소]**.
1. 페이지의 오른쪽 위 모서리에서 을(를) 탭합니다. **[!UICONTROL 다음]**.
1. 페이지의 오른쪽 위 모서리에서 을(를) 탭합니다. **[!UICONTROL 게시 취소]**.

## 비디오 인코딩 및 YouTube 게시 진행 모니터링 {#monitoring-video-encoding-and-youtube-publishing-progress}

비디오 인코딩이 적용된 폴더에 새 비디오를 업로드하거나 YouTube에 비디오를 게시하면 비디오 인코딩/Youtube 게시 진행 방식을 모니터링할 수 있습니다. 실제 YouTube 게시 진행 상태는 로그 방식으로만 사용할 수 있습니다. 그러나 실패 또는 성공은 다음 절차에 설명된 추가 방법으로 나열되어 있습니다. 또한 YouTube 게시 워크플로우 또는 비디오 인코딩이 완료되거나 중단되면 이메일 알림을 받게 됩니다.

### 진행 상태 모니터링 {#monitoring-progress}

1. 자산 폴더에서 비디오 인코딩 진행 상태 보기:

   * 카드 보기에서 자산에 비디오 인코딩 진행 상태가 백분율로 표시됩니다. 오류가 있으면 이 정보가 자산에도 표시됩니다.

   ![chlimage_1-429](assets/chlimage_1-429.png)

   * 목록 보기에서 비디오 인코딩 진행 상태는 **[!UICONTROL 처리 상태]** 열. If there is an error, this message displays in that same column.

   ![chlimage_1-430](assets/chlimage_1-430.png)

   This column does not display by default. To enable the column, select **[!UICONTROL View Settings]** from the views drop-down menu, and add the **[!UICONTROL Processing Status]** column and tap or click **[!UICONTROL Update]**.

   ![chlimage_1-431](assets/chlimage_1-431.png)

1. 자산 세부 정보에서 진행 상황을 봅니다. 자산을 탭하거나 클릭하면, 드롭다운 메뉴를 열고 를 선택합니다 **[!UICONTROL 타임라인]**. 인코딩 또는 YouTube 게시과 같은 워크플로우 활동으로 범위를 좁히려면 **[!UICONTROL 워크플로우]**.

   ![chlimage_1-432](assets/chlimage_1-432.png)

   인코딩과 같은 모든 워크플로우 정보가 타임라인에 표시됩니다. YouTube 게시의 경우 워크플로우 타임라인에는 YouTube 채널의 이름과 YouTube 비디오 URL도 포함되어 있습니다. 또한 게시가 완료된 후 워크플로우 타임라인에 오류 알림이 표시됩니다.

   >[!NOTE]
   >
   >의 여러 워크플로우 구성으로 인해 실패/오류 메시지를 최종적으로 기록하는 데 시간이 오래 걸릴 수 있습니다 **[!UICONTROL 다시 시도]**, **[!UICONTROL 다시 시도 지연]**, 및 **[!UICONTROL timeout]** 변환 전: [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr), 예:
   >
   >    * Apache Sling 작업 큐 구성
   >    * Adobe Granite Workflow 외부 프로세스 작업 처리기
   >    * Granite 워크플로우 시간 초과 큐

   >
   >을 조정할 수 있습니다 **[!UICONTROL 다시 시도]**, **[!UICONTROL 다시 시도 지연]**, 및 **[!UICONTROL timeout]** 이러한 구성의 속성.

1. For workflows in progress, see Workflow Instances available from **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Instances]**.

   >[!NOTE]
   >
   >에 액세스하려면 관리 권한이 필요합니다 **[!UICONTROL 도구]** 메뉴 아래의 제품에서 사용할 수 있습니다.

   ![chlimage_1-433](assets/chlimage_1-433.png)

   인스턴스를 선택하고 을(를) 누릅니다 **[!UICONTROL 기록 열기]**.

   ![chlimage_1-434](assets/chlimage_1-434.png)

   워크플로우 인스턴스 영역에서 워크플로우를 일시 중단, 종료 또는 변경할 수도 있습니다. 자세한 내용은 [워크플로우 관리](/help/sites-administering/workflows-administering.md) 추가 정보.

1. For failed jobs, see Workflow Failures available from **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Failures]**. The **[!UICONTROL Workflow Failure]** lists all failed workflow activities.

   >[!NOTE]
   >
   >에 액세스하려면 관리 권한이 필요합니다 **[!UICONTROL 도구]** 메뉴 아래의 제품에서 사용할 수 있습니다.

   ![chlimage_1-435](assets/chlimage_1-435.png)

   >[!NOTE]
   >
   >의 여러 워크플로우 구성으로 인해 오류 메시지가 최종적으로 기록되는 데 시간이 오래 걸릴 수 있습니다 **[!UICONTROL 다시 시도]**, **[!UICONTROL 다시 시도 지연]**, 및 **[!UICONTROL timeout]** 변환 전: [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr), 예:
   >
   >
   >
   >    * Apache Sling 작업 큐 구성
   >    * Adobe Granite Workflow 외부 프로세스 작업 처리기
   >    * Granite 워크플로우 시간 초과 큐

   >
   >
   >을 조정할 수 있습니다 **[!UICONTROL 다시 시도]**, **[!UICONTROL 다시 시도 지연]**, 및 **[!UICONTROL timeout]** 이러한 구성의 속성.

1. For completed workflows, see Workflow Archive available from **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Archive]**. The **[!UICONTROL Workflow Archive]** lists all completed workflow activities.

   >[!NOTE]
   >
   >에 액세스하려면 관리 권한이 필요합니다 **[!UICONTROL 도구]** 메뉴 아래의 제품에서 사용할 수 있습니다.

   ![chlimage_1-436](assets/chlimage_1-436.png)

1. 중단되거나 실패한 워크플로우 작업에 대한 이메일 알림을 받게 됩니다. 관리자가 이러한 이메일 알림을 구성할 수 있습니다. 자세한 내용은 [이메일 알림 구성](#configuring-e-mail-notifications).

#### 전자 메일 알림 구성 {#configuring-e-mail-notifications}

>[!NOTE]
>
>에 액세스하려면 관리 권한이 필요합니다 **[!UICONTROL 도구]** 메뉴 아래의 제품에서 사용할 수 있습니다.

알림을 구성하는 방법은 인코딩 작업 또는 YouTube 게시 작업에 대한 알림을 원하는 지에 따라 다릅니다.

* 인코딩 작업의 경우 의 모든 Experience Manager 워크플로우 이메일 알림에 대한 구성 페이지에 액세스할 수 있습니다 **[!UICONTROL 도구]** > **[!UICONTROL 작업]** > **[!UICONTROL 웹 콘솔]** 그리고 **[!UICONTROL Day CQ Workflow Email Notification Service]**. 자세한 내용은 [Experience Manager에서 이메일 알림 구성](/help/sites-administering/notification.md). 확인란을 선택하거나 취소할 수 있습니다 **[!UICONTROL 중단 시 알림]** 또는 **[!UICONTROL 완료 시 알림]** 따라서,

* YouTube 게시 작업의 경우 다음을 수행합니다.

1. Experience Manager에서 **[!UICONTROL 도구]** > **[!UICONTROL 워크플로우]** > **[!UICONTROL 모델]**.
1. 워크플로우 모델 페이지에서 을 선택합니다 **[!UICONTROL YouTube에 게시]**&#x200B;를 탭한 다음, **[!UICONTROL 편집]** 클릭합니다.
1. YouTube에 게시 워크플로우 페이지의 오른쪽 위 모서리 근처에 있는 **[!UICONTROL 편집]**.
1. YouTube 업로드 구성 요소에서 마우스 포인터를 놓은 다음 한 번 탭하여 인라인 도구 모음을 표시합니다.

   ![6_5_publishtoyoutubeworkflow](assets/6_5_publishtoyoutubeworkflow.png)

1. 인라인 도구 모음에서 구성 아이콘(공구모양)을 누릅니다. 을(를) 클릭합니다. **[!UICONTROL 인수]** 탭.

   ![6_5_publishtoyoutubeworkflow-configurationicon](assets/6_5_publishtoyoutubeworkflow-configurationicon.png)

1. YouTube 업로드 프로세스 - 단계 속성 대화 상자에서 **[!UICONTROL 인수]** 탭.

   ![6_5_publishtoyoutubeworkflow-arguments-tab](assets/6_5_publishtoyoutubeworkflow-arguments-tab.png)

1. 다음 확인란을 선택하거나 취소할 수 있습니다.

   * 게시 시작
   * 게시 실패
   * 게시 완료 - 채널 및 URL에 대한 정보를 포함합니다

   확인란을 지우는 것은 YouTube 게시 워크플로우에서 지정된 이메일 알림을 받지 않음을 의미합니다.

   >[!NOTE]
   >
   >이러한 이메일은 YouTube에만 해당되며 일반 워크플로우 이메일 알림 외에도 제공됩니다. 그 결과, 두 세트의 이메일 알림 즉, **[!UICONTROL Day CQ Workflow Email Notification Service]** 구성 설정에 따라 YouTube에만 적용되는 구성 및 세트를 선택할 수 있습니다.

1. 완료되면 대화 상자의 오른쪽 위 모서리 근처에 있는 **[!UICONTROL 완료]** 아이콘(확인 표시).
1. YouTube에 게시 워크플로우 페이지의 오른쪽 상단 모서리에서 을(를) 탭합니다. **[!UICONTROL 동기화]**.

## 비디오 자산에 주석 달기 {#annotate-video-assets}

1. 에서 [!DNL Assets] 콘솔, 선택 **[!UICONTROL 편집]** 자산 카드의 자산 세부 사항 페이지를 표시합니다.
1. 비디오를 재생하려면 **[!UICONTROL 미리 보기]**.
1. 비디오에 주석을 달려면 **[!UICONTROL 주석 달기]**. 비디오에서 특정 시간(프레임)에 주석이 추가됩니다. 캔버스에 주석을 달 때 그림을 그리고 드로잉에 주석을 포함할 수 있습니다. 주석이 자동으로 저장됩니다. 주석 마법사를 종료하려면 **[!UICONTROL 닫기]**.

   ![비디오 프레임에 그리기 및 주석 달기](assets/annotate-video.png)

1. Seek to a specific point in the video, specify the time in seconds in the **text** field and click **Jump**. For example, to skip the first 20 seconds of video, enter 20 in the text field.

   ![비디오에서 지정된 초 단위로 건너뛸 시간을 찾습니다](assets/seek-in-video.png)

1. 타임라인에서 보려면 주석을 클릭합니다. 타임라인에서 주석을 삭제하려면 **[!UICONTROL 삭제]**.

   ![타임라인에서 주석 및 세부 정보 보기](assets/timeline-view-annotation.png)

>[!MORELIKETHIS]
>
>* [Experience Manager Assets에서 디지털 자산 관리](/help/assets/manage-assets.md)
>* [Experience Manager Assets에서 컬렉션 관리](/help/assets/manage-collections.md)
>* [Dynamic Media 비디오 설명서](/help/assets/video.md).

