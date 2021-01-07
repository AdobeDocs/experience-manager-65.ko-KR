---
title: ' [!DNL Assets] 과(와) 통합 [!DNL InDesign Server]'
description: ' [!DNL Adobe Experience Manager Assets] 과(와) [!DNL Adobe InDesign Server]을(를) 통합하는 방법을 알아봅니다.'
contentOwner: AG
translation-type: tm+mt
source-git-commit: a31fa2712e541dfdc7a5b08ee9b33782f190f00b
workflow-type: tm+mt
source-wordcount: '1578'
ht-degree: 1%

---


# [!DNL Adobe Experience Manager Assets]과 [!DNL Adobe InDesign Server] {#integrating-aem-assets-with-indesign-server} 통합

[!DNL Adobe Experience Manager Assets] CFP 패키지를:

* 특정 처리 작업의 로드를 배포하는 프록시입니다. 프록시는 특정 작업을 수행하기 위해 프록시 워커와 통신하는 [!DNL Experience Manager] 인스턴스와 그 결과를 전달하는 다른 [!DNL Experience Manager] 인스턴스입니다.
* 특정 작업을 정의하고 관리하는 프록시 워커입니다.
다양한 작업을 다룹니다.예를 들어 [!DNL InDesign Server]을 사용하여 파일을 처리합니다.

[!DNL Adobe InDesign]로 만든 파일을 [!DNL Experience Manager Assets]에 완전히 업로드하려면 프록시가 사용됩니다. 이렇게 하면 프록시 워커에서 [!DNL Adobe InDesign Server]과 통신합니다. 여기서 [scripts](https://www.adobe.com/devnet/indesign/documentation.html#idscripting)는 메타데이터를 추출하고 [!DNL Experience Manager Assets]에 대한 다양한 변환을 생성할 수 있습니다. 프록시 워커는 클라우드 구성에서 [!DNL InDesign Server]과 [!DNL Experience Manager] 인스턴스 사이의 양방향 통신을 활성화합니다.

>[!NOTE]
>
>[!DNL Adobe InDesign] 는 두 개의 별도 서비스로 제공됩니다. [인쇄 ](https://www.adobe.com/products/indesign.html) 및 디지털 배포를 위한 페이지 레이아웃을 디자인하는 데 사용되는 Adobe InDesign 데스크탑 앱 [Adobe InDesign ](https://www.adobe.com/products/indesignserver.html) Server를 사용하면 제작한 컨텐츠를 바탕으로 프로그래밍 방식으로 자동화된 문서를 만들 수 있습니다 [!DNL InDesign]. 이 스크립트는 [ExtendScript](https://www.adobe.com/devnet/scripting.html) 엔진에 인터페이스를 제공하는 서비스로 작동합니다. 스크립트는 [!DNL ExtendScript]에 기록되며 [!DNL JavaScript]와 유사합니다. [!DNL InDesign] 스크립트에 대한 자세한 내용은 [https://www.adobe.com/devnet/indesign/documentation.html#idscripting](https://www.adobe.com/devnet/indesign/documentation.html#idscripting)을(를) 참조하십시오.

## 압축 풀기의 작동 방식 {#how-the-extraction-works}

[!DNL Adobe InDesign Server]을(를) [!DNL Experience Manager Assets]과 통합하여 [!DNL InDesign]로 만든 INDD 파일을 업로드하고, 생성된 표현물을 생성할 수 있으며, 추출된 모든 미디어(예: 비디오)를 추출하여 자산으로 저장할 수 있습니다.

>[!NOTE]
>
>이전 버전의 [!DNL Experience Manager]에서 XMP 및 축소판을 추출할 수 있었지만 이제 모든 미디어를 추출할 수 있습니다.

1. INDD 파일을 [!DNL Experience Manager Assets]에 업로드합니다.
1. 프레임워크는 SOAP(Simple Object Access Protocol)를 통해 명령 스크립트를 [!DNL InDesign Server]으로 보냅니다.
이 명령 스크립트는 다음을 수행합니다.

   * INDD 파일을 검색합니다.
   * [!DNL InDesign Server] 명령 실행:

      * 구조, 텍스트 및 모든 미디어 파일이 추출됩니다.
      * PDF 및 JPG 변환이 생성됩니다.
      * HTML 및 IDML 변환이 생성됩니다.
   * 결과 파일을 다시 [!DNL Experience Manager Assets]에 게시합니다.

   >[!NOTE]
   >
   >IDML은 [!DNL InDesign] 파일의 모든 내용을 렌더링하는 XML 기반 형식입니다. [ZIP](https://www.techterms.com/definition/zip) 압축을 사용하여 압축 패키지로 저장됩니다. 자세한 내용은 [InDesign 교환 형식 INX 및 IDML](https://www.peachpit.com/articles/article.aspx?p=1381880&amp;seqNum=8)을 참조하십시오.

   >[!CAUTION]
   >
   >[!DNL InDesign Server]이(가) 설치되어 있지 않거나 구성되지 않은 경우에도 INDD 파일을 [!DNL Experience Manager]에 업로드할 수 있습니다. 그러나 생성된 변환은 PNG 및 JPEG로 제한됩니다. HTML, .idml 또는 페이지 변환을 생성할 수 없습니다.

1. 추출 및 변환 생성 후:

   * 구조가 `cq:Page`(변환 유형)에 복제됩니다.
   * 추출된 텍스트와 파일은 [!DNL Experience Manager Assets]에 저장됩니다.
   * 모든 변환은 자산 자체의 [!DNL Experience Manager Assets]에 저장됩니다.

## [!DNL InDesign Server]을(를) Experience Manager {#integrating-the-indesign-server-with-aem}과 통합

[!DNL Experience Manager Assets]에 사용할 [!DNL InDesign Server]을 통합하고 프록시를 구성한 후 다음을 수행해야 합니다.

1. [InDesign Server을 설치합니다](#installing-the-indesign-server).
1. 필요한 경우 [Experience Manager 자산 작업 과정](#configuring-the-aem-assets-workflow)을 구성합니다.
기본값이 인스턴스에 적합하지 않은 경우에만 필요합니다.
1. InDesign Server](#configuring-the-proxy-worker-for-indesign-server)에 대한 [프록시 작업자를 구성합니다.

### [!DNL InDesign Server] {#installing-the-indesign-server} 설치

[!DNL Experience Manager]에 사용할 [!DNL InDesign Server]을(를) 설치하고 시작하려면 다음을 수행합니다.

1. [!DNL InDesign Server]을(를) 다운로드하고 설치합니다.

1. 필요한 경우 [!DNL InDesign Server] 인스턴스의 구성을 사용자 정의할 수 있습니다.

1. 명령줄에서 서버를 시작합니다.

   `<*ids-installation-dir*>/InDesignServer.com -port 8080`

   그러면 포트 8080에서 SOAP 플러그인 수신 대기 상태로 서버가 시작됩니다. 모든 로그 메시지와 출력이 명령 창에 직접 기록됩니다.

   >[!NOTE]
   >
   >출력 메시지를 파일에 저장하려면 리디렉션;예를 들어 Windows의 경우:
   >`<ids-installation-dir>/InDesignServer.com -port 8080 > ~/temp/INDD-logfile.txt 2>&1`

### [!DNL Experience Manager Assets] 워크플로 {#configuring-the-aem-assets-workflow} 구성

[!DNL Experience Manager Assets] 에는 특별히 다음을 위한 몇 가지 프로세스 단계가  **[!UICONTROL 있는 사전 구성된 워크플로우]** DAM 자산 업데이트 [!DNL InDesign]가 있습니다.

* [미디어 추출](#media-extraction)
* [페이지 추출](#page-extraction)

이 워크플로우는 다양한 작성자 인스턴스에서 설정에 맞게 조정할 수 있는 기본값을 사용하여 설정합니다(표준 워크플로우이므로, 자세한 내용은 [워크플로우 편집](/help/sites-developing/workflows-models.md#configuring-a-workflow-step)) 아래에서 확인할 수 있습니다. 기본값(SOAP 포트 포함)을 사용하는 경우 구성이 필요하지 않습니다.

설정 후 [!DNL InDesign] 파일을 [!DNL Experience Manager Assets](일반적인 방법 중 하나)에 업로드하면 워크플로우를 트리거하여 자산을 처리하고 다양한 변환을 준비합니다. INDD 파일을 [!DNL Experience Manager Assets]에 업로드하여 구성을 테스트하고 `<*your_asset*>.indd/Renditions` 아래에 IDS로 만든 다른 변환이 표시되는지 확인합니다.

#### 미디어 추출 {#media-extraction}

이 단계는 INDD 파일에서 미디어를 추출하는 작업을 제어합니다.

사용자 정의하려면 **[!UICONTROL 미디어 추출]** 단계의 **[!UICONTROL 인수]** 탭을 편집할 수 있습니다.

![미디어 추출 인수 및 스크립트 경로](assets/media_extraction_arguments_scripts.png)

미디어 추출 인수 및 스크립트 경로

* **ExtendScript 라이브러리**:다른 스크립트에서 요구하는 간단한 http get/post 메서드 라이브러리입니다.

* **스크립트 확장**:여기에서 다양한 스크립트 조합을 지정할 수 있습니다. [!DNL InDesign Server]에서 자신만의 스크립트를 실행하려면 스크립트를 `/apps/settings/dam/indesign/scripts`에 저장합니다.

[!DNL Adobe InDesign] 스크립트에 대한 자세한 내용은 [InDesign 개발자 설명서](https://www.adobe.com/devnet/indesign/documentation.html#idscripting)를 참조하십시오.

>[!CAUTION]
>
>ExtendScript 라이브러리를 변경하지 마십시오. 이 라이브러리는 Sling과 통신하는 데 필요한 HTTP 기능을 제공합니다. 이 설정은 사용할 라이브러리를 [!DNL InDesign Server]으로 지정합니다.

미디어 추출 워크플로우 단계에서 실행하는 `ThumbnailExport.jsx` 스크립트는 JPG 형식으로 축소판 변환을 생성합니다. 이 변환은 [!DNL Experience Manager]에 필요한 정적 변환을 생성하는 [프로세스 축소판] 작업 과정 단계에서 사용합니다.

[축소판 처리] 워크플로우 단계를 구성하여 다른 크기로 정적 변환을 생성할 수 있습니다. 기본값은 [!DNL Experience Manager Assets] 인터페이스에 필요하므로 제거하지 않아야 합니다. 마지막으로, 이미지 미리 보기 변환 삭제 워크플로우 단계에서는 JPG 축소판 변환이 더 이상 필요하지 않으므로 제거합니다.

#### 페이지 추출 {#page-extraction}

추출된 요소에서 [!DNL Experience Manager] 페이지가 만들어집니다. 추출 핸들러는 변환(현재 HTML 또는 IDML)에서 데이터를 추출하는 데 사용됩니다. 그런 다음 이 데이터를 사용하여 PageBuilder를 사용하여 페이지를 만듭니다.

사용자 정의하려면 **[!UICONTROL 페이지 추출]** 단계의 **[!UICONTROL 인수]** 탭을 편집할 수 있습니다.

![chlimage_1-96](assets/chlimage_1-289.png)

* **페이지 추출 처리기**:팝업 목록에서 사용할 핸들러를 선택합니다. 추출 핸들러는 관련 `RenditionPicker`에 의해 선택된 특정 변환에서 작동합니다( `ExtractionHandler` API 참조). 표준 [!DNL Experience Manager] 설치에서는 다음을 사용할 수 있습니다.
   * IDML 내보내기 추출 핸들:MediaExtract 단계에서 생성된 `IDML` 변환에서 작동합니다.

* **페이지 이름**:결과 페이지에 할당할 이름을 지정합니다. 비워 두면 이름이 &quot;page&quot;(또는 &quot;page&quot;가 이미 있는 경우 파생)입니다.

* **페이지 제목**:결과 페이지에 할당할 제목을 지정합니다.

* **페이지 루트 경로**:결과 페이지의 루트 위치에 대한 경로입니다. 비워 두면 자산의 표현물을 보유한 노드가 사용됩니다.

* **페이지 템플릿**:결과 페이지를 생성할 때 사용할 템플릿입니다.

* **페이지 디자인**:결과 페이지를 생성할 때 사용할 페이지 디자인입니다.

### [!DNL InDesign Server] {#configuring-the-proxy-worker-for-indesign-server}에 대한 프록시 작업자 구성

>[!NOTE]
>
>워커는 프록시 인스턴스에 상주합니다.

1. 도구 콘솔의 왼쪽 창에서 **[!UICONTROL Cloud Services 구성]**&#x200B;을 확장합니다. 그런 다음 **[!UICONTROL 클라우드 프록시 구성]**&#x200B;을 확장합니다.

1. **[!UICONTROL IDS 작업자]**&#x200B;를 두 번 클릭하여 구성을 엽니다.

1. **[!UICONTROL 편집]**&#x200B;을 클릭하여 구성 대화 상자를 열고 필요한 설정을 정의합니다.

   ![proxy_idsworkerconfig](assets/proxy_idsworkerconfig.png)

   * **IDS**
풀과 통신하는 데 사용할 SOAP 끝점입니다 [!DNL InDesign Server]. 항목을 추가, 제거 및 주문할 수 있습니다.

1. 확인을 클릭하여 저장합니다.

### 일 CQ 링크 외부라이저 구성 {#configuring-day-cq-link-externalizer}

[!DNL InDesign Server] 및 [!DNL Experience Manager]이(가) 다른 호스트에 있거나 이러한 응용 프로그램 중 하나 또는 둘 다 기본 포트에서 작동하지 않는 경우 [!UICONTROL Day CQ Link Externalizer]를 구성하여 [!DNL InDesign Server]의 호스트 이름, 포트 및 컨텐트 경로를 설정합니다.

1. `https://[aem_server]:[port]/system/console/configMgr`에서 웹 콘솔에 액세스합니다.
1. **[!UICONTROL 일 CQ 링크 외부라이저]** 구성을 찾습니다. **[!UICONTROL 편집]**&#x200B;을 클릭하여 엽니다.
1. 링크 외부라이저 설정을 사용하면 [!DNL Experience Manager] 배포 및 [!DNL InDesign Server]에 대한 절대 URL을 만들 수 있습니다. **[!UICONTROL 도메인]** 필드를 사용하여 호스트 이름과 [!DNL Adobe InDesign Server]의 컨텍스트 경로를 지정합니다. **저장**&#x200B;을 클릭합니다.

   ![링크 외부라이저 설정](assets/link-externalizer-config.png)

### [!DNL InDesign Server] {#enabling-parallel-job-processing-for-indesign-server}에 대한 병렬 작업 처리 사용

이제 ID에 대해 병렬 작업 처리를 활성화할 수 있습니다. 처리할 수 있는 최대 병렬 작업 수(`x`)를 결정합니다. [!DNL InDesign Server]

* 단일 다중 프로세서 컴퓨터에서 [!DNL InDesign Server]에서 처리할 수 있는 최대 병렬 작업 수(`x`)는 IDS를 실행하는 프로세서 수보다 하나 작습니다.
* 여러 컴퓨터에서 ID를 실행하는 경우 사용 가능한 총 프로세서 수(예: 모든 컴퓨터에서)를 계산한 다음 총 시스템 수를 빼야 합니다.

병렬 ID 작업 수를 구성하려면:

1. Felix Console의 **[!UICONTROL 구성]** 탭을 엽니다.예를 들면 다음과 같습니다.`https://[aem_server]:[port]/system/console/configMgr`.

1. `Apache Sling Job Queue Configuration` 아래에서 IDS 처리 큐를 선택합니다.

1. 설정:

   * **유형** - `Parallel`
   * **최대 병렬 작업**  -  `<*x*>` (위에 계산됨)

1. 이러한 변경 내용을 저장합니다.
1. Adobe CS6 이상 버전에 대한 다중 세션 지원을 활성화하려면 `com.day.cq.dam.ids.impl.IDSJobProcessor.name` 구성 아래의 `enable.multisession.name` 확인란을 선택합니다.
1. IDS Worker 구성](#configuring-the-proxy-worker-for-indesign-server)에 SOAP 끝점을 추가하여 [ IDS 워커 풀을 만듭니다.`x`

   [!DNL InDesign Server]을(를) 실행하는 컴퓨터가 여러 개인 경우 각 컴퓨터에 대해 SOAP 끝점(컴퓨터 -1당 프로세서 수)을 추가하십시오.

<!-- 
TBD: Make updates to configurations for allow and block list after product updates are done.
-->

>[!NOTE]
>
>직원 풀을 사용할 때 ID 근로자의 차단 목록을 활성화할 수 있습니다.
>
>이렇게 하려면 IDS 작업 검색을 활성화하는 `com.day.cq.dam.ids.impl.IDSJobProcessor.name` 구성 아래의 **[!UICONTROL enable.retry.name]** 확인란을 활성화합니다.
>
>또한 `com.day.cq.dam.ids.impl.IDSPoolImpl.name` 구성에서 작업 핸들러 목록에서 ID를 제외하기 전에 작업 검색의 수를 결정하는 `max.errors.to.blacklist` 매개 변수에 대해 양의 값을 설정합니다.
>
>기본적으로 구성 가능한(`retry.interval.to.whitelist.name`) 시간(분) 후 IDS 워커의 유효성을 다시 검사해야 합니다. 워커가 온라인에서 검색되면 차단 목록에서 제거됩니다.

## [!DNL InDesign Server] 10.0 이상 {#enabling-support-for-indesign-server-or-later} 지원 활성화

[!DNL InDesign Server] 10.0 이상의 경우 다음 단계를 수행하여 멀티 세션 지원을 활성화합니다.

1. [!DNL Experience Manager Assets] 인스턴스 `https://[aem_server]:[port]/system/console/configMgr`에서 구성 관리자를 엽니다.
1. `com.day.cq.dam.ids.impl.IDSJobProcessor.name` 구성을 편집합니다.
1. **[!UICONTROL ids.cc.enable]** 옵션을 선택하고 **[!UICONTROL 저장]**&#x200B;을 클릭합니다.

>[!NOTE]
>
>[!DNL Experience Manager Assets]과의 [!DNL InDesign Server] 통합의 경우 통합에 필요한 세션 지원 기능이 단일 코어 시스템에서 지원되지 않으므로 멀티 코어 프로세서를 사용하십시오.

## [!DNL Experience Manager] 자격 증명 {#configure-aem-credentials} 구성

[!DNL InDesign Server]와의 통합을 끊지 않고 [!DNL Experience Manager] 배포에서 [!DNL InDesign Server]에 액세스하기 위한 기본 관리자 자격 증명(사용자 이름 및 암호)을 변경할 수 있습니다.

1. 이동 `/etc/cloudservices/proxy.html`.
1. 대화 상자에서 새 사용자 이름과 암호를 지정합니다.
1. 자격 증명을 저장합니다.

>[!MORELIKETHIS]
>
>* [Adobe InDesign Server 정보](https://www.adobe.com/products/indesignserver/faq.html)

