---
title: ' [!DNL InDesign Server]과(와)  [!DNL Assets]  통합'
description: ' [!DNL Adobe Experience Manager Assets] 을(를)  [!DNL Adobe InDesign Server]과(와) 통합하는 방법을 알아봅니다.'
contentOwner: AG
role: Admin
feature: Publishing
exl-id: 5ba020a3-c36c-402b-a11b-d6b0426b03bf
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1555'
ht-degree: 2%

---

# [!DNL Adobe Experience Manager Assets]과(와) [!DNL Adobe InDesign Server] 통합 {#integrating-aem-assets-with-indesign-server}

[!DNL Adobe Experience Manager Assets] 사용:

* 특정 처리 작업의 로드를 분산하는 프록시입니다. 프록시는 프록시 작업자와 통신하여 특정 작업을 수행하고 다른 [!DNL Experience Manager] 인스턴스를 통해 결과를 제공하는 [!DNL Experience Manager] 인스턴스입니다.
* 특정 작업을 정의하고 관리하는 프록시 작업자입니다.
예를 들어 [!DNL InDesign Server]을(를) 사용하여 파일을 처리하는 등 다양한 작업을 처리할 수 있습니다.

[!DNL Adobe InDesign](으)로 만든 파일을 [!DNL Experience Manager Assets]에 완전히 업로드하려면 프록시가 사용됩니다. 프록시 작업자를 사용하여 [!DNL Adobe InDesign Server]과(와) 통신합니다. [스크립트](https://www.adobe.com/devnet/indesign/documentation.html#idscripting)을(를) 실행하여 메타데이터를 추출하고 [!DNL Experience Manager Assets]에 대한 다양한 변환을 생성합니다. 프록시 작업자를 사용하면 클라우드 구성에서 [!DNL InDesign Server]과(와) [!DNL Experience Manager] 인스턴스 간의 양방향 통신을 사용할 수 있습니다.

>[!NOTE]
>
>[!DNL Adobe InDesign]은(는) 두 개의 개별 오퍼로 제공됩니다. 인쇄 및 디지털 배포를 위해 페이지 레이아웃을 디자인하는 데 사용되는 [Adobe InDesign](https://www.adobe.com/products/indesign.html) 데스크톱 앱입니다. [Adobe InDesign Server](https://www.adobe.com/products/indesignserver.html)을(를) 사용하면 [!DNL InDesign](으)로 만든 내용을 기반으로 자동화된 문서를 프로그래밍 방식으로 만들 수 있습니다. 해당 [ExtendScript](https://www.adobe.com/devnet/indesign/documentation.html#idscripting) 엔진에 대한 인터페이스를 제공하는 서비스로 작동합니다. 스크립트는 [!DNL JavaScript]과(와) 유사한 [!DNL ExtendScript]에 작성됩니다. [!DNL InDesign] 스크립트에 대한 자세한 내용은 [https://www.adobe.com/devnet/indesign/documentation.html#idscripting](https://www.adobe.com/devnet/indesign/documentation.html#idscripting)을(를) 참조하십시오.

## 추출 작동 방식 {#how-the-extraction-works}

[!DNL Adobe InDesign Server]을(를) [!DNL Experience Manager Assets]과(와) 통합하여 [!DNL InDesign](으)로 만든 INDD 파일을 업로드하고, 렌디션을 생성하고, 모든 미디어(예: 비디오)를 추출하여 에셋으로 저장할 수 있습니다.

>[!NOTE]
>
>이전 버전의 [!DNL Experience Manager]에서 XMP과 썸네일을 추출할 수 있었습니다. 이제 모든 미디어를 추출할 수 있습니다.

1. INDD 파일을 [!DNL Experience Manager Assets]에 업로드합니다.
1. 프레임워크는 SOAP(Simple Object Access Protocol)을 통해 [!DNL InDesign Server]에 명령 스크립트를 보냅니다.
이 명령 스크립트는 다음을 수행합니다.

   * INDD 파일을 검색합니다.
   * [!DNL InDesign Server]개 명령 실행:

      * 구조, 텍스트 및 모든 미디어 파일이 추출됩니다.
      * PDF 및 JPG 렌디션이 생성됩니다.
      * HTML 및 IDML 렌디션이 생성됩니다.

   * 결과 파일을 다시 [!DNL Experience Manager Assets](으)로 Post.

   >[!NOTE]
   >
   >IDML은 [!DNL InDesign] 파일의 모든 내용을 렌더링하는 XML 기반 형식입니다. [ZIP](https://www.techterms.com/definition/zip) 압축을 사용하여 압축된 패키지로 저장됩니다. 자세한 내용은 [InDesign 교환 형식 INX 및 IDML](https://www.peachpit.com/articles/article.aspx?p=1381880&amp;seqNum=8)을 참조하세요.

   >[!CAUTION]
   >
   >[!DNL InDesign Server]이(가) 설치되지 않았거나 구성되지 않은 경우에도 INDD 파일을 [!DNL Experience Manager]에 업로드할 수 있습니다. 그러나 생성된 렌디션은 PNG 및 JPEG으로 제한됩니다. HTML, .idml 또는 페이지 표현물을 생성할 수 없습니다.

1. 추출 및 렌디션 생성 후:

   * 구조가 `cq:Page`(렌디션 유형)에 복제됩니다.
   * 추출된 텍스트와 파일이 [!DNL Experience Manager Assets]에 저장되어 있습니다.
   * 모든 렌디션은 에셋 자체의 [!DNL Experience Manager Assets]에 저장됩니다.

## [!DNL InDesign Server]을(를) Experience Manager과 통합 {#integrating-the-indesign-server-with-aem}

[!DNL Experience Manager Assets]에서 사용할 [!DNL InDesign Server]을(를) 통합하고 프록시를 구성한 후 다음을 수행해야 합니다.

1. [InDesign Server 설치](#installing-the-indesign-server).
1. 필요한 경우 [Experience Manager Assets 워크플로를 구성](#configuring-the-aem-assets-workflow)합니다.
기본값이 인스턴스에 적합하지 않은 경우에만 필요합니다.
1. ](#configuring-the-proxy-worker-for-indesign-server) InDesign Server에 대해 [프록시 작업자를 구성하십시오.

### [!DNL InDesign Server] 설치 {#installing-the-indesign-server}

[!DNL Experience Manager]에 사용할 [!DNL InDesign Server]을(를) 설치하고 시작하려면 다음을 수행하십시오.

1. [!DNL InDesign Server]을(를) 다운로드하여 설치하십시오.

1. 필요한 경우 [!DNL InDesign Server] 인스턴스의 구성을 사용자 지정할 수 있습니다.

1. 명령줄에서 서버를 시작합니다.

   `<*ids-installation-dir*>/InDesignServer.com -port 8080`

   이렇게 하면 포트 8080에서 수신하는 SOAP 플러그인으로 서버가 시작됩니다. 모든 로그 메시지와 출력은 명령 창에 직접 기록됩니다.

   >[!NOTE]
   >
   >출력 메시지를 파일에 저장하려면 리디렉션을 사용합니다(예: Windows에서).
   >`<ids-installation-dir>/InDesignServer.com -port 8080 > ~/temp/INDD-logfile.txt 2>&1`

### [!DNL Experience Manager Assets] 워크플로 구성 {#configuring-the-aem-assets-workflow}

[!DNL Experience Manager Assets]에 [!DNL InDesign]에 대해 여러 프로세스 단계가 있는 미리 구성된 워크플로우 **[!UICONTROL DAM 자산 업데이트]**&#x200B;가 있습니다.

* [미디어 추출](#media-extraction)
* [페이지 추출](#page-extraction)

이 워크플로는 다양한 작성자 인스턴스의 설정에 맞게 조정할 수 있는 기본값으로 설정됩니다(표준 워크플로이므로 [워크플로 편집](/help/sites-developing/workflows-models.md#configuring-a-workflow-step)에서 추가 정보를 사용할 수 있음). 기본값(SOAP 포트 포함)을 사용하는 경우 구성이 필요하지 않습니다.

설정 후 일반적인 방법으로 [!DNL InDesign]개의 파일을 [!DNL Experience Manager Assets]에 업로드하면 워크플로우가 트리거되어 자산을 처리하고 다양한 렌디션을 준비합니다. INDD 파일을 [!DNL Experience Manager Assets]에 업로드하여 구성을 테스트하여 `<*your_asset*>.indd/Renditions` 아래 ID로 만든 다른 변환이 표시되는지 확인합니다.

#### 미디어 추출 {#media-extraction}

이 단계는 INDD 파일에서 미디어 추출을 제어합니다.

To customize, you can edit **[!UICONTROL Arguments]** tab of the **[!UICONTROL Media Extraction]** step.

![미디어 추출 인수 및 스크립트 경로](assets/media_extraction_arguments_scripts.png)

미디어 추출 인수 및 스크립트 경로

* **ExtendScript 라이브러리**: 다른 스크립트에 필요한 간단한 http get/post 메서드 라이브러리입니다.

* **스크립트 확장**: 여기에서 다른 스크립트 조합을 지정할 수 있습니다. [!DNL InDesign Server]에서 고유한 스크립트를 실행하려면 `/apps/settings/dam/indesign/scripts`에 스크립트를 저장하십시오.

<!-- TBD: Hiding this link since ADC is not available anymore. 
For information about [!DNL Adobe InDesign] scripts, see [InDesign developer documentation](https://www.adobe.com/devnet/indesign/documentation.html#idscripting).
-->

>[!CAUTION]
>
>ExtendScript 라이브러리를 변경하지 마십시오. 이 라이브러리는 Sling과 통신하는 데 필요한 HTTP 기능을 제공합니다. 이 설정은 [!DNL InDesign Server]에서 사용하기 위해 전송할 라이브러리를 지정합니다.

미디어 추출 워크플로 단계에서 실행되는 `ThumbnailExport.jsx` 스크립트는 JPG 형식의 썸네일 렌디션을 생성합니다. 이 렌디션은 프로세스 썸네일 워크플로 단계에서 [!DNL Experience Manager]에 필요한 정적 렌디션을 생성하는 데 사용됩니다.

프로세스 축소판 워크플로 단계를 구성하여 다양한 크기의 정적 렌디션을 생성할 수 있습니다. 기본값은 [!DNL Experience Manager Assets] 인터페이스에 필요하므로 제거하지 마십시오. 마지막으로, 이미지 미리 보기 렌디션 삭제 워크플로 단계에서는 더 이상 필요하지 않으므로 JPG 썸네일 렌디션을 제거합니다.

#### 페이지 추출 {#page-extraction}

이렇게 하면 추출된 요소에서 [!DNL Experience Manager] 페이지가 만들어집니다. 추출 핸들러는 렌디션(현재 HTML 또는 IDML)에서 데이터를 추출하는 데 사용됩니다. 그런 다음 PageBuilder를 사용하여 페이지를 만드는 데 이 데이터를 사용합니다.

To customize, you can edit the **[!UICONTROL Arguments]** tab of the **[!UICONTROL Page Extraction]** step.

![chlimage_1-96](assets/chlimage_1-289.png)

* **페이지 추출 처리기**: 팝업 목록에서 사용할 처리기를 선택하십시오. 추출 처리기는 관련 `RenditionPicker`에 의해 선택된 특정 렌디션에 대해 작동합니다(`ExtractionHandler` API 참조). 표준 [!DNL Experience Manager] 설치에서는 다음 항목을 사용할 수 있습니다.
   * IDML 내보내기 추출 핸들: MediaExtract 단계에서 생성된 `IDML` 렌디션에서 작동합니다.

* **페이지 이름**: 결과 페이지에 지정할 이름을 지정합니다. 비워 두면 이름은 &quot;page&quot;(또는 &quot;page&quot;가 이미 있으면 파생)입니다.

* **페이지 제목**: 결과 페이지에 지정할 제목을 지정합니다.

* **페이지 루트 경로**: 결과 페이지의 루트 위치에 대한 경로입니다. 비워 두면 에셋의 렌디션이 포함된 노드가 사용됩니다.

* **페이지 템플릿**: 결과 페이지를 생성할 때 사용할 템플릿입니다.

* **페이지 디자인**: 결과 페이지를 생성할 때 사용할 페이지 디자인입니다.

### [!DNL InDesign Server]에 대한 프록시 작업자 구성 {#configuring-the-proxy-worker-for-indesign-server}

>[!NOTE]
>
>작업자는 프록시 인스턴스에 상주합니다.

1. 도구 콘솔에서 왼쪽 창의 **[!UICONTROL Cloud Service 구성]**&#x200B;을 확장합니다. 그런 다음 **[!UICONTROL 클라우드 프록시 구성]**&#x200B;을 확장합니다.

1. Double-click the **[!UICONTROL IDS worker]** to open for configuration.

1. **[!UICONTROL 편집]**&#x200B;을 클릭하여 구성 대화 상자를 열고 필요한 설정을 정의합니다.

   ![proxy_idsworkerconfig](assets/proxy_idsworkerconfig.png)

   * **IDS 풀**
[!DNL InDesign Server]과(와) 통신하는 데 사용할 SOAP 끝점입니다. 항목을 추가, 제거 및 주문해야 합니다.

1. 확인 을 클릭하여 저장합니다.

### 일별 CQ 링크 외부화 구성 {#configuring-day-cq-link-externalizer}

[!DNL InDesign Server] 및 [!DNL Experience Manager]이(가) 다른 호스트에 있거나 이러한 응용 프로그램 중 하나 또는 둘 다 기본 포트에서 작동하지 않는 경우 [!UICONTROL 일 CQ 링크 외부화]을(를) 구성하여 [!DNL InDesign Server]에 대한 호스트 이름, 포트 및 콘텐츠 경로를 설정합니다.

1. `https://[aem_server]:[port]/system/console/configMgr`에서 웹 콘솔에 액세스합니다.
1. **[!UICONTROL 일 CQ 링크 외부화]** 구성을 찾습니다. 열려면 **[!UICONTROL 편집]**&#x200B;을 클릭하세요.
1. 링크 외부화 설정은 [!DNL Experience Manager] 배포 및 [!DNL InDesign Server]에 대한 절대 URL을 만드는 데 도움이 됩니다. **[!UICONTROL 도메인]** 필드를 사용하여 [!DNL Adobe InDesign Server]에 대한 호스트 이름을 지정하십시오. **저장**&#x200B;을 클릭합니다.

   절대 URL에서 다음 그림과 같이 로컬(작성자) 인스턴스의 호스트 이름으로 `localhost`을(를) 사용하고 게시 인스턴스의 호스트 이름 또는 IP 주소를 사용하십시오.

   ![링크 외부화 설정](assets/link-externalizer-config.png)

### [!DNL InDesign Server]에 대해 병렬 작업 처리 사용 {#enabling-parallel-job-processing-for-indesign-server}

이제 ID에 대해 병렬 작업 처리를 활성화할 수 있습니다. [!DNL InDesign Server]에서 처리할 수 있는 최대 병렬 작업 수(`x`)를 결정합니다.

* 단일 다중 프로세서 컴퓨터에서 [!DNL InDesign Server]이(가) 처리할 수 있는 최대 병렬 작업 수(`x`)는 ID를 실행하는 프로세서 수보다 한 개 적습니다.
* 여러 시스템에서 ID를 실행하는 경우 사용 가능한 총 프로세서 수(즉, 모든 시스템에서)를 계산한 다음 총 시스템 수를 빼야 합니다.

병렬 ID 작업 수를 구성하려면 다음을 수행합니다.

1. Felix 콘솔의 **[!UICONTROL 구성]** 탭을 엽니다(예: `https://[aem_server]:[port]/system/console/configMgr`).

1. `Apache Sling Job Queue Configuration`에서 IDS 처리 큐를 선택하십시오.

1. 설정:

   * **유형** - `Parallel`
   * **최대 병렬 작업** - `<*x*>`(위에서 계산됨)

1. 이러한 변경 사항을 저장합니다.
1. Adobe CS6 이상에 대한 다중 세션 지원을 사용하도록 설정하려면 `com.day.cq.dam.ids.impl.IDSJobProcessor.name` 구성에서 `enable.multisession.name` 확인란을 선택하십시오.
1. IDS 작업자 구성에 SOAP 끝점을 추가하여 `x` IDS 작업자의 [풀을 만듭니다](#configuring-the-proxy-worker-for-indesign-server).

   [!DNL InDesign Server]을(를) 실행하는 컴퓨터가 여러 개 있는 경우 각 컴퓨터에 대해 SOAP 끝점(컴퓨터당 프로세서 수 -1)을 추가하십시오.

<!-- 
TBD: Make updates to configurations for allow and block list after product updates are done.
-->

>[!NOTE]
>
>작업자 풀로 작업할 때 IDS 작업자 차단 목록을 활성화할 수 있습니다.
>
>이렇게 하려면 `com.day.cq.dam.ids.impl.IDSJobProcessor.name` 구성 아래에서 IDS 작업 재검색을 활성화하는 **[!UICONTROL enable.retry.name]** 확인란을 활성화하십시오.
>
>또한 `com.day.cq.dam.ids.impl.IDSPoolImpl.name` 구성 아래에서 작업 처리기 목록에서 ID를 금지하기 전에 작업 재시도 횟수를 결정하는 `max.errors.to.blacklist` 매개 변수에 양의 값을 설정하십시오.
>
>기본적으로 구성 가능한(`retry.interval.to.whitelist.name`) 시간(분)이 지나면 IDS 작업자의 유효성을 다시 검사합니다. 작업자가 온라인에서 발견되는 경우 해당 작업자는 차단 목록에서 제거됩니다.

## [!DNL InDesign Server] 10.0 이상에 대한 지원 사용 {#enabling-support-for-indesign-server-or-later}

[!DNL InDesign Server] 10.0 이상의 경우 다음 단계를 수행하여 다중 세션 지원을 사용하도록 설정하십시오.

1. [!DNL Experience Manager Assets] 인스턴스 `https://[aem_server]:[port]/system/console/configMgr`에서 구성 관리자를 엽니다.
1. 구성 `com.day.cq.dam.ids.impl.IDSJobProcessor.name`을(를) 편집합니다.
1. **[!UICONTROL ids.cc.enable]** 옵션을 선택하고 **[!UICONTROL 저장]**&#x200B;을 클릭합니다.

>[!NOTE]
>
>[!DNL Experience Manager Assets]과(와) [!DNL InDesign Server] 통합의 경우 통합에 필요한 세션 지원 기능이 단일 코어 시스템에서 지원되지 않으므로 멀티 코어 프로세서를 사용하십시오.

## [!DNL Experience Manager] 자격 증명 구성 {#configure-aem-credentials}

[!DNL InDesign Server]과의 통합을 중단하지 않고 [!DNL Experience Manager] 배포에서 [!DNL InDesign Server]에 액세스하기 위한 기본 관리자 자격 증명(사용자 이름 및 암호)을 변경할 수 있습니다.

1. `/etc/cloudservices/proxy.html`로 이동합니다.
1. 대화 상자에서 새 사용자 이름과 암호를 지정합니다.
1. 자격 증명을 저장합니다.

>[!MORELIKETHIS]
>
>* [Adobe InDesign Server 정보](https://www.adobe.com/products/indesignserver/faq.html)
