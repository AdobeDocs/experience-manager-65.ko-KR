---
title: AEM 자산을 Adobe InDesign Server와 통합
description: AEM 자산을 Adobe InDesign Server와 통합하는 방법을 알아봅니다.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 07c1a4102539ba4678c55dee3a4882101e39864f

---


# AEM 자산을 Adobe InDesign Server와 통합 {#integrating-aem-assets-with-indesign-server}

AEM(Adobe Experience Manager) 자산에서는 다음을 사용합니다.

* 특정 처리 작업의 로드를 배포하는 프록시. 프록시는 특정 작업을 수행하기 위해 프록시 작업자와 통신하는 AEM 인스턴스와 다른 AEM 인스턴스를 사용하여 결과를 전달하는 AEM 인스턴스입니다.
* 특정 작업을 정의 및 관리하는 프록시 작업자.
이러한 기능에는 다양한 작업이 포함될 수 있습니다.예를 들어 InDesign Server를 사용하여 파일을 처리할 수 있습니다.

Adobe InDesign으로 만든 파일을 AEM 자산에 완전히 업로드하려면 프록시가 사용됩니다. 이렇게 하면 프록시 작업자가 Adobe InDesign Server와 통신할 수 있습니다. 여기서 [스크립트는](https://www.adobe.com/devnet/indesign/documentation.html#idscripting) 메타데이터를 추출하고 AEM 자산에 대한 다양한 변환을 생성합니다. 프록시 작업자는 클라우드 구성에서 InDesign Server와 AEM 인스턴스 간 양방향 통신을 활성화합니다.

>[!NOTE]
>
>Adobe InDesign은 다음과 같은 두 가지 제품으로 구성되어 있습니다.
>
>* [InDesign](https://www.adobe.com/products/indesign.html)
   >  인쇄 및/또는 디지털 배포를 위한 페이지 레이아웃을 디자인할 수 있습니다.
   >
   >
* [InDesign Server](https://www.adobe.com/products/indesignserver.html)
   >  이 엔진을 사용하면 InDesign을 사용하여 만든 내용을 기반으로 프로그래밍 방식으로 자동화된 문서를 만들 수 있습니다. ExtendScript 엔진에 인터페이스를 제공하는 서비스로 [작동합니다](https://www.adobe.com/devnet/scripting.html) .
   >  스크립트는 javascript와 유사한 ExtendScript로 작성됩니다. InDesign 스크립트에 대한 자세한 내용은 https://www.adobe.com/devnet/indesign/documentation.html#idscripting [을 참조하십시오](https://www.adobe.com/devnet/indesign/documentation.html#idscripting).


## 추출 작동 방식 {#how-the-extraction-works}

Adobe InDesign Server를 AEM Assets와 통합하여 InDesign으로 만든 INDD 파일을 업로드하고, 표현물을 생성하며, 모든 미디어를 추출하여(예: 비디오) 자산으로 저장할 수 있습니다.

>[!NOTE]
>
>이전 버전의 AEM에서 XMP 및 축소판을 추출할 수 있었지만 이제 모든 미디어를 추출할 수 있습니다.

1. INDD 파일을 AEM 자산에 업로드합니다.
1. 프레임워크는 SOAP(Simple Object Access Protocol)를 통해 InDesign Server로 명령 스크립트를 전송합니다.
이 명령 스크립트는 다음을 수행합니다.

   * INDD 파일을 검색합니다.
   * InDesign Server 명령 실행:

      * 구조, 텍스트 및 모든 미디어 파일이 추출됩니다.
      * PDF 및 JPG 변환이 생성됩니다.
      * HTML 및 IDML 변환이 생성됩니다.
   * 결과 파일을 다시 AEM 자산에 게시합니다.
   >[!NOTE]
   >
   >IDML 파섹 ZIP 압축을 사용하여 압축 패키지로 [저장됩니다](https://www.techterms.com/definition/zip) . 자세한 내용은 InDesign Interchange [Formats INX 및 IDML을 참조하십시오](http://www.peachpit.com/articles/article.aspx?p=1381880&seqNum=8).

   >[!CAUTION]
   >
   >InDesign Server가 설치되어 있지 않거나 구성되지 않은 경우에도 INDD 파일을 AEM에 업로드할 수 있습니다. 그러나 생성된 변환은 PNG 및 JPEG로 제한됩니다. HTML, .idml 또는 페이지 변환을 생성할 수 없습니다.

1. 추출 및 변환 생성 후:

   * 구조가 `cq:Page` (변환 유형)에 복제됩니다.
   * 추출된 텍스트와 파일은 AEM 자산에 저장됩니다.
   * 모든 변환은 자산 자체의 AEM 자산에 저장됩니다.

## InDesign Server와 AEM 통합 {#integrating-the-indesign-server-with-aem}

AEM 자산과 함께 사용하기 위해 InDesign Server를 통합하거나 프록시를 구성한 후 다음을 수행해야 합니다.

1. [InDesign Server를 설치합니다](#installing-the-indesign-server).
1. 필요한 경우 AEM 자산 워크플로우를 [구성합니다](#configuring-the-aem-assets-workflow).
기본값이 인스턴스에 적합하지 않은 경우에만 필요합니다.
1. InDesign Server에 대한 [프록시 작업자 구성을 참조하십시오](#configuring-the-proxy-worker-for-indesign-server).

### InDesign Server 설치 {#installing-the-indesign-server}

AEM에서 사용할 InDesign Server를 설치하고 시작하려면 다음을 수행하십시오.

1. Adobe InDesign Server를 다운로드하여 설치합니다.

1. 필요한 경우 InDesign Server 인스턴스의 구성을 사용자 정의할 수 있습니다.

1. 명령줄에서 서버를 시작합니다.

   `<*ids-installation-dir*>/InDesignServer.com -port 8080`

   그러면 포트 8080에서 SOAP 플러그인이 수신 대기하는 상태로 서버가 시작됩니다. 모든 로그 메시지와 출력은 명령 창에 직접 기록됩니다.

   >[!NOTE]
   >
   >출력 메시지를 파일에 저장하려면 리디렉션을 사용합니다.예를 들어 Windows에서 다음을 수행합니다.
   >`<ids-installation-dir>/InDesignServer.com -port 8080 > ~/temp/INDD-logfile.txt 2>&1`

### AEM 자산 구성 워크플로우 {#configuring-the-aem-assets-workflow}

AEM Assets에는 사전 구성된 워크플로우 **[!UICONTROL DAM Update]** Asset이 있으며, 여기에는 InDesign을 위한 몇 가지 프로세스 단계가 있습니다.

* [미디어 추출](#media-extraction)
* [페이지 추출](#page-extraction)

이 워크플로우는 다양한 작성자 인스턴스에서 설정에 맞게 조정할 수 있는 기본값으로 설정되어 있습니다(표준 워크플로우이므로 워크플로우 편집에서 추가 정보를 [사용할 수 있습니다](/help/sites-developing/workflows-models.md#configuring-a-workflow-step)). 기본값(SOAP 포트 포함)을 사용하는 경우 구성이 필요하지 않습니다.

설정 후 AEM 자산에 InDesign 파일을 업로드하면(일반적인 방법 중 하나에서) 자산을 처리하고 다양한 변환을 준비하는 데 필요한 워크플로우가 트리거됩니다. INDD 파일을 AEM Assets에 업로드하여 구성을 테스트하여 IDS에서 만든 다양한 변환이 `<*your_asset*>.indd/Renditions`

#### Media extraction {#media-extraction}

이 단계는 INDD 파일에서 미디어를 추출하는 것을 제어합니다.

사용자 정의하려면 미디어 추출 **[!UICONTROL 단계의]** 인수 탭을 편집할 **[!UICONTROL 수]** 있습니다.

![미디어 추출 인수 및 스크립트 경로](assets/media_extraction_arguments_scripts.png)

미디어 추출 인수 및 스크립트 경로

* **ExtendScript 라이브러리**:이는 다른 스크립트에 필요한 간단한 http get/post 메서드 라이브러리입니다.

* **스크립트 확장**:여기에서 다양한 스크립트 조합을 지정할 수 있습니다. InDesign Server에서 스크립트를 직접 실행하려면 스크립트를 에 저장합니다 `/apps/settings/dam/indesign/scripts`.

Indesign 스크립트에 대한 자세한 내용은 InDesign [개발자 설명서를 참조하십시오](https://www.adobe.com/devnet/indesign/documentation.html#idscripting)

>[!CAUTION]
>
>ExtendScript 라이브러리를 변경하지 마십시오. 이 라이브러리는 Sling과 통신하는 데 필요한 HTTP 기능을 제공합니다. 이 설정은 InDesign Server로 전송할 라이브러리를 지정합니다.

미디어 추출 워크플로우 단계에서 실행되는 `ThumbnailExport.jsx` 스크립트는 .jpg 형식으로 축소판 변환을 생성합니다. 이 변환은 AEM에 필요한 정적 변환을 생성하기 위해 [축소판 처리] 워크플로우 단계에서 사용됩니다.

다른 크기로 정적 변환을 생성하도록 [축소판 처리] 워크플로우 단계를 구성할 수 있습니다. AEM Assets UI에 필수이므로 기본값을 제거하지 않아야 합니다. 마지막으로 이미지 미리 보기 변환 삭제 워크플로우 단계에서는 더 이상 필요하지 않으므로 .jpg 축소판 변환을 제거합니다.

#### Page extraction {#page-extraction}

이렇게 하면 추출된 요소에서 AEM 페이지가 만들어집니다. 추출 핸들러는 변환에서 데이터를 추출하는 데 사용됩니다(현재 HTML 또는 IDML). 그런 다음 이 데이터를 사용하여 PageBuilder를 사용하여 페이지를 만듭니다.

사용자 정의하려면 페이지 추출 **[!UICONTROL 단계의]** 인수 탭을 편집할 **[!UICONTROL 수]** 있습니다.

![chlimage_1-96](assets/chlimage_1-289.png)

* **페이지 추출 처리기**:팝업 목록에서 사용할 처리기를 선택합니다. 추출 핸들러는 관련 API `RenditionPicker` 를 통해 선택한 특정 변환에서 작동합니다 `ExtractionHandler` . 표준 AEM 설치에서는 다음을 사용할 수 있습니다.
   * IDML 내보내기 추출 핸들:MediaExtract 단계에서 생성된 `IDML` 변환에서 작동합니다.

* **페이지 이름**:결과 페이지에 지정할 이름을 지정합니다. 비워 두면 이름이 &quot;page&quot;(또는 &quot;page&quot;가 이미 존재하는 경우 파생됨)가 됩니다.

* **페이지 제목**:결과 페이지에 지정할 제목을 지정합니다.

* **페이지 루트 경로**:결과 페이지의 루트 위치에 대한 경로입니다. 비워 두면 자산의 표현물을 포함하는 노드가 사용됩니다.

* **페이지 템플릿**:결과 페이지를 생성할 때 사용할 템플릿입니다.

* **페이지 디자인**:결과 페이지를 생성할 때 사용할 페이지 디자인입니다.

### InDesign Server용 프록시 작업자 구성 {#configuring-the-proxy-worker-for-indesign-server}

>[!NOTE]
>
>워커는 프록시 인스턴스에 상주합니다.

1. 도구 콘솔의 왼쪽 창에서 **[!UICONTROL 클라우드 서비스]** 구성을 확장합니다. 그런 다음 클라우드 **[!UICONTROL 프록시 구성을 확장합니다]**.

1. IDS **[!UICONTROL 작업자를]** 두 번 클릭하여 구성을 엽니다.

1. 편집을 **[!UICONTROL 클릭하여]** 구성 대화 상자를 열고 필요한 설정을 정의합니다.

   ![proxy_idsworkerconfig](assets/proxy_idsworkerconfig.png)

   * **IDS 풀** InDesign Server와 통신하는 데 사용할 SOAP 끝점입니다. 항목을 추가, 제거 및 주문할 수 있습니다.

1. 확인을 클릭하여 저장합니다.

### 일 CQ 링크 외부라이저 구성 {#configuring-day-cq-link-externalizer}

InDesign 서버와 AEM이 다른 호스트에서 실행되거나 두 응용 프로그램이 모두 기본 포트에서 실행되지 않는 경우 [!UICONTROL InDesign] 서버의 호스트 이름, 포트 및 컨텐츠 경로를 설정하도록 Day CQ Link Externalizer를 구성합니다.

1. 에서 웹 콘솔에 액세스합니다 `https://[aem_server]:[port]/system/console/configMgr`.
1. Day CQ Link **[!UICONTROL Externalizer 구성을]**&#x200B;찾아 편집을 **[!UICONTROL 눌러]** 엽니다.
1. Indesign 서버의 호스트 이름과 컨텍스트 경로를 지정하고 [저장]을 **클릭합니다**.

   ![chlimage_1-97](assets/chlimage_1-290.png)

### InDesign 서버에 대한 병렬 작업 처리 사용 {#enabling-parallel-job-processing-for-indesign-server-s}

이제 ID에 대한 병렬 작업 처리를 활성화할 수 있습니다. InDesign Server에서 처리할 수 있는 최대 병렬 작업(`x`) 수 확인:

* 단일 다중 프로세서 시스템에서 InDesign Server가 처리할 수 있는 최대 병렬 작업(`x`)은 IDS를 실행하는 프로세서 수보다 1개 적습니다.
* 여러 컴퓨터에서 IDS를 실행하는 경우 사용 가능한 프로세서(예: 모든 컴퓨터에서)의 총 수를 계산해야 합니다. 그런 다음 총 시스템 수를 빼야 합니다.

병렬 ID 작업 수를 구성하려면:

1. Felix **[!UICONTROL Console]** 의 구성 탭을 엽니다.예를 들면 다음과 같습니다. `https://[aem_server]:[port]/system/console/configMgr`Adobe

1. 아래에서 IDS 처리 큐를 `Apache Sling Job Queue Configuration`선택합니다.

1. 설정:

   * **유형** - `Parallel`
   * **최대 병렬 작업** - `<*x*>` (위에서 계산됨)

1. 이러한 변경 사항을 저장합니다.
1. Adobe CS6 이상 버전에 대한 다중 세션 지원을 활성화하려면 구성 `enable.multisession.name` 아래의 확인란을 `com.day.cq.dam.ids.impl.IDSJobProcessor.name` 선택하십시오.
1. IDS 작업자 구성에 [`x`](#configuring-the-proxy-worker-for-indesign-server)SOAP 끝점을 추가하여 IDS 작업자 풀을 만듭니다.

   InDesign Server를 실행하는 컴퓨터가 여러 개인 경우 각 컴퓨터에 대해 SOAP 끝점(시스템당 프로세서 수 -1)을 추가합니다.

   >[!NOTE]
   >
   >근로자 풀을 사용하여 작업할 때 ID 근로자의 블랙리스트 사용을 선택할 수 있습니다.
   >
   >
   >이렇게 하려면 IDS 작업 검색을 활성화하는 **[!UICONTROL 구성 아래에서 enable.retry.name]** `com.day.cq.dam.ids.impl.IDSJobProcessor.name` 확인란을 활성화합니다.
   >
   >
   >또한, `com.day.cq.dam.ids.impl.IDSPoolImpl.name` 구성 아래에서 IDS를 작업 처리기 목록에서 제외하기 전에 작업 검색의 수를 결정하는 매개 변수에 대한 양수 값을 `max.errors.to.blacklist` 설정합니다.
   >
   >
   >기본적으로 구성 가능한(retry.interval.to.whitelist.name) 시간(분 단위) 후 IDS 워커의 유효성을 다시 검사해야 합니다. 이 씨가 온라인에서 발견되면 블랙 리스트에서 제거됩니다.

## InDesign Server 10.0 이상 지원 활성화 {#enabling-support-for-indesign-server-or-later}

InDesign Server 10.0 이상의 경우 다음 단계를 수행하여 다중 세션 지원을 활성화합니다.

1. AEM 자산 인스턴스에서 구성 관리자를 엽니다 `https://[aem_server]:[port]/system/console/configMgr`.
1. 구성을 `com.day.cq.dam.ids.impl.IDSJobProcessor.name`편집합니다.
1. ids.cc.en **[!UICONTROL 사용]** 가능 옵션을 선택하고 [저장]을 **[!UICONTROL 클릭합니다]**.

>[!NOTE]
>
>InDesign Server와 AEM Assets를 통합하려면 통합에 필요한 세션 지원 기능이 단일 코어 시스템에서 지원되지 않으므로 멀티코어 프로세서를 사용하십시오.

## AEM 자격 증명 구성 {#configure-aem-credentials}

InDesign 서버와의 통합을 끊지 않고 AEM 인스턴스에서 InDesign 서버에 액세스하기 위한 기본 관리자 자격 증명(사용자 이름 및 암호)을 변경할 수 있습니다.

1. 이동 `/etc/cloudservices/proxy.html`.
1. 대화 상자에서 새 사용자 이름과 암호를 지정합니다.
1. 자격 증명을 저장합니다.

>[!MORELIKETHIS]
>
>* [Adobe InDesign Server 정보](https://www.adobe.com/products/indesignserver/faq.html)

