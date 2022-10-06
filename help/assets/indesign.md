---
title: 통합 [!DNL Assets] with [!DNL InDesign Server]
description: 통합 방법 알아보기 [!DNL Adobe Experience Manager Assets] with [!DNL Adobe InDesign Server].
contentOwner: AG
role: Admin
feature: Publishing
exl-id: 5ba020a3-c36c-402b-a11b-d6b0426b03bf
source-git-commit: 67e145e250bbe386168ab2c0f8967f91aa9d8a36
workflow-type: tm+mt
source-wordcount: '1591'
ht-degree: 3%

---

# 통합 [!DNL Adobe Experience Manager Assets] with [!DNL Adobe InDesign Server] {#integrating-aem-assets-with-indesign-server}

[!DNL Adobe Experience Manager Assets] CFP 패키지를:

* 특정 처리 작업의 로드를 분배하는 프록시. 프록시는 [!DNL Experience Manager] 특정 작업을 수행하기 위해 프록시 작업자와 통신하는 인스턴스 및 기타 [!DNL Experience Manager] 결과를 전달하는 인스턴스입니다.
* 특정 작업을 정의하고 관리하는 프록시 작업자
여기에는 다양한 작업이 포함될 수 있습니다. 예를 들어 [!DNL InDesign Server] 를 눌러 파일을 처리합니다.

파일을 완전히 업로드하려면 [!DNL Experience Manager Assets] Adobe Social이 [!DNL Adobe InDesign] 프록시가 사용됩니다. 프록시 작업자를 사용하여 [!DNL Adobe InDesign Server], 위치 [스크립트](https://www.adobe.com/devnet/indesign/documentation.html#idscripting) 메타데이터를 추출하고 을 위한 다양한 표현물을 생성하기 위해 실행됩니다 [!DNL Experience Manager Assets]. 프록시 작업자는 [!DNL InDesign Server] 그리고 [!DNL Experience Manager] 클라우드 구성의 인스턴스.

>[!NOTE]
>
>[!DNL Adobe InDesign] 는 두 개의 별도 오퍼로 제공됩니다. [Adobe InDesign](https://www.adobe.com/products/indesign.html) 인쇄 및 디지털 배포용 페이지 레이아웃을 디자인하는 데 사용되는 데스크탑 앱입니다. [Adobe InDesign Server](https://www.adobe.com/products/indesignserver.html) 을 사용하면 [!DNL InDesign]. 이 서비스는 인터페이스에 대한 인터페이스를 제공하는 서비스로 작동합니다 [ExtendScript](https://www.adobe.com/devnet/indesign/documentation.html#idscripting) engine.스크립트가 [!DNL ExtendScript]와 유사하며 [!DNL JavaScript]. 에 대한 자세한 정보 [!DNL InDesign] 스크립트 참조 [https://www.adobe.com/devnet/indesign/documentation.html#idscripting](https://www.adobe.com/devnet/indesign/documentation.html#idscripting).

## 추출 작동 방식 {#how-the-extraction-works}

다음 [!DNL Adobe InDesign Server] 와 통합할 수 있습니다. [!DNL Experience Manager Assets] INDD 파일이 [!DNL InDesign] 업로드, 생성된 표현물, 추출된 모든 미디어(예: 비디오) 및 자산으로 저장할 수 있습니다.

>[!NOTE]
>
>이전 버전의 [!DNL Experience Manager] XMP과 축소판 그림을 추출할 수 있었지만 이제 모든 미디어를 추출할 수 있습니다.

1. INDD 파일을에 업로드합니다. [!DNL Experience Manager Assets].
1. 프레임워크는 명령 스크립트를 [!DNL InDesign Server] SOAP를 통해(단순 개체 액세스 프로토콜).
이 명령 스크립트는 다음 작업을 수행합니다.

   * INDD 파일을 검색합니다.
   * 실행 [!DNL InDesign Server] 명령:

      * 구조, 텍스트 및 모든 미디어 파일이 추출됩니다.
      * PDF 및 JPG 표현물이 생성됩니다.
      * HTML 및 IDML 표현물이 생성됩니다.
   * 결과 파일을 다시 [!DNL Experience Manager Assets].

   >[!NOTE]
   >
   >IDML은 모든 내용을 렌더링하는 XML 기반 형식입니다 [!DNL InDesign] 파일. 를 사용하여 압축 패키지로 저장됩니다. [ZIP](https://www.techterms.com/definition/zip) 압축. 자세한 내용은 [InDesign 교환 형식 INX 및 IDML](https://www.peachpit.com/articles/article.aspx?p=1381880&amp;seqNum=8).

   >[!CAUTION]
   >
   >만약 [!DNL InDesign Server] 가 설치되어 있지 않거나 구성되지 않은 경우 INDD 파일을에 업로드할 수 있습니다 [!DNL Experience Manager]. 그러나 생성된 변환은 PNG 및 JPEG으로 제한됩니다. HTML, .idml 또는 페이지 렌디션을 생성할 수 없습니다.

1. 추출 및 변환 생성 후:

   * 구조가 `cq:Page` (표현물 유형).
   * 추출된 텍스트와 파일은 [!DNL Experience Manager Assets].
   * 모든 변환은에 저장됩니다. [!DNL Experience Manager Assets]로 나열된 상태로 남아 있는 문제를 해결했습니다.

## 통합 [!DNL InDesign Server] Experience Manager 사용 {#integrating-the-indesign-server-with-aem}

를 통합하려면 [!DNL InDesign Server] 에서 사용 [!DNL Experience Manager Assets] 프록시를 구성한 후 다음을 수행해야 합니다.

1. [InDesign Server 설치](#installing-the-indesign-server).
1. 필요한 경우 [Experience Manager Assets 워크플로우 구성](#configuring-the-aem-assets-workflow).
기본값이 인스턴스에 적합하지 않은 경우에만 필요합니다.
1. 구성 [InDesign Server의 프록시 작업자](#configuring-the-proxy-worker-for-indesign-server).

### 설치 [!DNL InDesign Server] {#installing-the-indesign-server}

을(를) 설치하고 시작하려면 [!DNL InDesign Server] 에서 사용 [!DNL Experience Manager]:

1. 를 다운로드하여 설치합니다. [!DNL InDesign Server].

1. 필요한 경우 구성을 사용자 지정할 수 있습니다 [!DNL InDesign Server] 인스턴스.

1. 명령줄에서 서버를 시작합니다.

   `<*ids-installation-dir*>/InDesignServer.com -port 8080`

   그러면 포트 8080에서 수신 대기하는 SOAP 플러그인으로 서버가 시작됩니다. 모든 로그 메시지와 출력은 명령 창에 직접 작성됩니다.

   >[!NOTE]
   >
   >출력 메시지를 파일에 저장하려면 리디렉션을 사용하십시오. 예를 들어, Windows에서는
   >`<ids-installation-dir>/InDesignServer.com -port 8080 > ~/temp/INDD-logfile.txt 2>&1`

### 구성 [!DNL Experience Manager Assets] 워크플로우 {#configuring-the-aem-assets-workflow}

[!DNL Experience Manager Assets] 에는 사전 구성된 워크플로우가 있습니다 **[!UICONTROL DAM 자산 업데이트]**&#x200B;에 대해 특별히 적용되는 몇 가지 프로세스 단계가 있습니다 [!DNL InDesign]:

* [미디어 추출](#media-extraction)
* [페이지 추출](#page-extraction)

이 워크플로우는 다양한 작성 인스턴스에서 설정에 맞게 조정할 수 있는 기본값을 사용하여 설정되며, 표준 워크플로우이므로 자세한 내용은 [워크플로우 편집](/help/sites-developing/workflows-models.md#configuring-a-workflow-step)). 기본값(SOAP 포트 포함)을 사용하는 경우 구성이 필요하지 않습니다.

설정 후 업로드 [!DNL InDesign] 파일에 [!DNL Experience Manager Assets] 일반적인 방법에 의해)는 워크플로우를 트리거하여 자산을 처리하고 다양한 표현물을 준비합니다. INDD 파일을에 업로드하여 구성을 테스트합니다 [!DNL Experience Manager Assets] 에서 ID로 만든 다른 표현물이 표시되는지 확인합니다. `<*your_asset*>.indd/Renditions`

#### 미디어 추출 {#media-extraction}

이 단계는 INDD 파일에서 미디어를 추출하는 것을 제어합니다.

To customize, you can edit **[!UICONTROL Arguments]** tab of the **[!UICONTROL Media Extraction]** step.

![미디어 추출 인수 및 스크립트 경로](assets/media_extraction_arguments_scripts.png)

미디어 추출 인수 및 스크립트 경로

* **ExtendScript 라이브러리**: 다른 스크립트에 필요한 간단한 http get/post 메서드 라이브러리입니다.

* **스크립트 확장**: 여기에서 다양한 스크립트 조합을 지정할 수 있습니다. 사용자 고유의 스크립트를 [!DNL InDesign Server]에 스크립트를 저장합니다. `/apps/settings/dam/indesign/scripts`.

<!-- TBD: Hiding this link since ADC is not available anymore. 
For information about [!DNL Adobe InDesign] scripts, see [InDesign developer documentation](https://www.adobe.com/devnet/indesign/documentation.html#idscripting).
-->

>[!CAUTION]
>
>Do not change the ExtendScript library. 이 라이브러리는 Sling과 통신하는 데 필요한 HTTP 기능을 제공합니다. 이 설정은 [!DNL InDesign Server] 여기서 사용할 수 있습니다.

다음 `ThumbnailExport.jsx` 미디어 추출 워크플로우 단계에서 실행하는 스크립트는 JPG 형식으로 축소판 렌디션을 생성합니다. 이 표현물은 [축소판 처리] 워크플로우 단계에서 다음 작업에 필요한 정적 표현물을 생성하는 데 사용됩니다 [!DNL Experience Manager].

다양한 크기로 정적 렌디션을 생성하도록 프로세스 축소판 워크플로우 단계를 구성할 수 있습니다. 기본값이 [!DNL Experience Manager Assets] 인터페이스. 마지막으로, 이미지 미리 보기 변환 삭제 워크플로우 단계에서는 더 이상 필요하지 않으므로 JPG 축소판 렌디션을 제거합니다.

#### 페이지 추출 {#page-extraction}

이렇게 하면 [!DNL Experience Manager] 추출된 요소에서 페이지를 검색합니다. 추출 처리기는 변환(현재 HTML 또는 IDML)에서 데이터를 추출하는 데 사용됩니다. 그런 다음 이 데이터를 사용하여 PageBuilder를 사용하여 페이지를 만듭니다.

To customize, you can edit the **[!UICONTROL Arguments]** tab of the **[!UICONTROL Page Extraction]** step.

![chlimage_1-96](assets/chlimage_1-289.png)

* **페이지 추출 처리기**: 팝업 목록에서 사용할 처리기를 선택합니다. 추출 처리기는 관련된 특정 표현물에서 작동합니다 `RenditionPicker` (자세한 내용은 `ExtractionHandler` API). 표준 [!DNL Experience Manager] 설치 가능한 설치:
   * IDML 내보내기 추출 핸들: 에서 작동합니다. `IDML` MediaExtract 단계에서 생성된 표현물.

* **페이지 이름**: 결과 페이지에 지정할 이름을 지정합니다. 비워 두면 이름이 &quot;page&quot;(또는 &quot;page&quot;가 이미 있는 경우 파생자)입니다.

* **페이지 제목**: 결과 페이지에 지정할 제목을 지정합니다.

* **페이지 루트 경로**: 결과 페이지의 루트 위치에 대한 경로입니다. 비워 두면 자산의 표현물을 포함하는 노드가 사용됩니다.

* **페이지 템플릿**: 결과 페이지를 생성할 때 사용할 템플릿입니다.

* **페이지 디자인**: 결과 페이지를 생성할 때 사용할 페이지 디자인입니다.

### 프록시 작업자 구성 [!DNL InDesign Server] {#configuring-the-proxy-worker-for-indesign-server}

>[!NOTE]
>
>작업자는 프록시 인스턴스에 있습니다.

1. 도구 콘솔에서 를 확장합니다. **[!UICONTROL Cloud Services 구성]** 왼쪽 창에 있습니다. 그런 다음 를 확장합니다. **[!UICONTROL 클라우드 프록시 구성]**.

1. Double-click the **[!UICONTROL IDS worker]** to open for configuration.

1. 클릭 **[!UICONTROL 편집]** 구성 대화 상자를 열고 필수 설정을 정의하려면

   ![proxy_idsworkerconfig](assets/proxy_idsworkerconfig.png)

   * **IDS 풀**
와 통신하는 데 사용할 SOAP 끝점입니다 [!DNL InDesign Server]. 필수 항목을 추가, 제거 및 주문할 수 있습니다.

1. 확인을 클릭하여 저장합니다.

### 일 CQ Link Externalizer 구성 {#configuring-day-cq-link-externalizer}

만약 [!DNL InDesign Server] 및 [!DNL Experience Manager] 다른 호스트에 있거나 이러한 응용 프로그램 중 하나 또는 둘 다 기본 포트에서 작동하지 않는 경우 다음을 구성합니다. [!UICONTROL Day CQ Link Externalizer] 의 호스트 이름, 포트 및 컨텐츠 경로를 설정하려면 [!DNL InDesign Server].

1. 웹 콘솔 액세스 위치: `https://[aem_server]:[port]/system/console/configMgr`.
1. 구성을 찾습니다 **[!UICONTROL Day CQ Link Externalizer]**. 클릭 **[!UICONTROL 편집]** 엽니다.
1. Link Externalizer 설정을 사용하여 [!DNL Experience Manager] 배포 및 [!DNL InDesign Server]. 사용 **[!UICONTROL 도메인]** 필드에 대한 호스트 이름을 지정합니다. [!DNL Adobe InDesign Server]. **저장**&#x200B;을 클릭합니다.

   절대 URL에서 `localhost` 다음 그림과 같이 로컬(작성자) 인스턴스의 호스트 이름과 게시 인스턴스의 호스트 이름 또는 IP 주소입니다.

   ![Link Externalizer 설정](assets/link-externalizer-config.png)

### 에 대한 병렬 작업 처리 사용 [!DNL InDesign Server] {#enabling-parallel-job-processing-for-indesign-server}

이제 ID에 대한 병렬 작업 처리를 활성화할 수 있습니다. 최대 병렬 작업 수 확인(`x`) [!DNL InDesign Server] 처리할 수 있습니다.

* 단일 다중 프로세서 시스템에서 최대 병렬 작업 수(`x`) [!DNL InDesign Server] 처리할 수 있는 프로세서 수는 ID를 실행하는 프로세서 수보다 하나 작습니다.
* 여러 시스템에서 ID를 실행하는 경우 사용 가능한 총 프로세서 수(예: 모든 시스템의 경우)를 계산한 다음 총 시스템 수를 빼야 합니다.

병렬 ID 작업 수를 구성하려면

1. 를 엽니다. **[!UICONTROL 구성]** Felix Console 탭 예: `https://[aem_server]:[port]/system/console/configMgr`.

1. 아래에서 ID 처리 큐를 선택합니다 `Apache Sling Job Queue Configuration`.

1. 설정:

   * **유형** - `Parallel`
   * **최대 병렬 작업 수** - `<*x*>` (위에서 계산됨)

1. 이러한 변경 사항을 저장합니다.
1. Adobe CS6 이상에서 다중 세션 지원을 활성화하려면 다음을 확인하십시오 `enable.multisession.name` 확인란, 아래에 `com.day.cq.dam.ids.impl.IDSJobProcessor.name` 구성.
1. 만들기 [풀 `x` ID 작업자 구성에 SOAP 끝점을 추가하여 ID 작업자](#configuring-the-proxy-worker-for-indesign-server).

   여러 시스템이 실행 중인 경우 [!DNL InDesign Server]를 눌러 각 컴퓨터에 대해 SOAP 엔드포인트(시스템당 프로세서 수 -1)를 추가합니다.

<!-- 
TBD: Make updates to configurations for allow and block list after product updates are done.
-->

>[!NOTE]
>
>작업자 풀을 사용하여 작업할 경우 ID 작업자 차단 목록을 활성화할 수 있습니다.
>
>이렇게 하려면 을(를) 활성화합니다 **[!UICONTROL enable.retry.name]** 확인란, 아래에 `com.day.cq.dam.ids.impl.IDSJobProcessor.name` 구성. ID 작업 검색을 활성화합니다.
>
>또한, `com.day.cq.dam.ids.impl.IDSPoolImpl.name` 구성, 에 양의 값을 설정합니다. `max.errors.to.blacklist` 작업 처리기 목록에서 ID를 제한하기 전에 작업 검색의 수를 결정하는 매개 변수입니다.
>
>기본적으로 구성 가능한(`retry.interval.to.whitelist.name`) ID 작업자의 유효성을 다시 검사한 시간(분). 작업자가 온라인에서 검색되면 차단 목록에서 제거됩니다.

## 지원 활성화 [!DNL InDesign Server] 10.0 이상 {#enabling-support-for-indesign-server-or-later}

대상 [!DNL InDesign Server] 10.0 이상에서는 다음 단계를 수행하여 다중 세션 지원을 활성화합니다.

1. 에서 구성 관리자를 엽니다. [!DNL Experience Manager Assets] 인스턴스 `https://[aem_server]:[port]/system/console/configMgr`.
1. 구성 편집 `com.day.cq.dam.ids.impl.IDSJobProcessor.name`.
1. 을(를) 선택합니다 **[!UICONTROL ids.cc.enable]** 옵션을 선택하고 **[!UICONTROL 저장]**.

>[!NOTE]
>
>대상 [!DNL InDesign Server] 통합 [!DNL Experience Manager Assets]를 채울 때는 통합에 필요한 세션 지원 기능이 단일 코어 시스템에서 지원되지 않으므로 멀티 코어 프로세서를 사용하십시오.

## 구성 [!DNL Experience Manager] 자격 증명 {#configure-aem-credentials}

에 액세스하기 위해 기본 관리자 자격 증명(사용자 이름 및 암호)을 변경할 수 있습니다 [!DNL InDesign Server] 다음 [!DNL Experience Manager] 통합 기능을 중단하지 않고 배포 [!DNL InDesign Server].

1. 이동 `/etc/cloudservices/proxy.html`.
1. 대화 상자에서 새 사용자 이름과 암호를 지정합니다.
1. 자격 증명을 저장합니다.

>[!MORELIKETHIS]
>
>* [Adobe InDesign Server 정보](https://www.adobe.com/products/indesignserver/faq.html)

