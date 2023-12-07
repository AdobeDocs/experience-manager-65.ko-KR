---
title: Adobe Analytics 연결 및 프레임워크 만들기
description: AEM을 SiteCatalyst에 연결하고 프레임워크를 만드는 방법에 대해 알아봅니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: 8262bbf9-a982-479b-a2b5-f8782dd4182d
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1484'
ht-degree: 1%

---

# Adobe Analytics 연결 및 프레임워크 만들기 {#connecting-to-adobe-analytics-and-creating-frameworks}

Adobe Analytics의 AEM 페이지에서 웹 데이터를 추적하려면 Adobe Analytics Cloud 서비스 구성 및 Adobe Analytics 프레임워크를 만듭니다.

* **Adobe Analytics 구성:** Adobe Analytics 계정에 대한 정보. Adobe Analytics 구성을 통해 AEM을 Adobe Analytics에 연결할 수 있습니다. 사용하는 각 계정에 대해 Adobe Analytics 구성을 만듭니다.
* **Adobe Analytics 프레임워크:** Adobe Analytics 보고서 세트 속성과 CQ 변수 간의 매핑 세트입니다. 프레임워크를 사용하여 웹 사이트 데이터가 Adobe Analytics 보고서를 채우는 방법을 구성합니다. 프레임워크는 Adobe Analytics 구성과 연결됩니다. 각 구성에 대해 여러 프레임워크를 만들 수 있습니다.

웹 페이지를 프레임워크에 연결하면 프레임워크는 해당 페이지와 해당 페이지의 하위 항목에 대한 추적을 수행합니다. 그런 다음 Adobe Analytics에서 페이지 보기를 검색하고 사이트 콘솔에 표시할 수 있습니다.

## 사전 요구 사항 {#prerequisites}

### Adobe Analytics 계정 {#adobe-analytics-account}

Adobe Analytics에서 AEM 데이터를 추적하려면 유효한 Adobe Experience Cloud Adobe Analytics 계정이 있어야 합니다.

Adobe Analytics 계정은 다음 작업을 수행해야 합니다.

* 보유 **관리자** 권한
* 할당 대상: **웹 서비스 액세스** 사용자 그룹.

>[!CAUTION]
>
>제공 **관리자** Adobe Analytics 내의 권한이 부족하여 사용자가 AEM에서 Adobe Analytics으로 연결할 수 없습니다. 계정에도 다음이 있어야 합니다. **웹 서비스 액세스** 권한.

![chlimage_1-67](assets/chlimage_1-67.png)

계속하기 전에 자격 증명을 통해 Adobe Analytics에 로그인할 수 있는지 확인하십시오. 다음 중 하나를 통해

* [Adobe Experience Cloud 로그인](https://experience.adobe.com/#/@login/home)

* [Adobe Analytics 로그인](https://sc.omniture.com/login/)

### Adobe Analytics 데이터 센터를 사용하도록 AEM 구성 {#configuring-aem-to-use-your-adobe-analytics-data-centers}

Adobe Analytics [데이터 센터](https://experienceleague.adobe.com/docs/analytics/analyze/reports-analytics/reporting-interface/overview-data-collection.html?lang=en) Adobe Analytics 보고서 세트와 연결된 데이터를 수집, 처리 및 저장합니다. Adobe Analytics 보고서 세트를 호스팅하는 데이터 센터를 사용하도록 AEM을 구성합니다. 데이터 센터는 계약에 언급되어 있습니다. 이 정보는 조직의 관리자에게 문의하십시오.

필요한 경우 다음을 사용하여 올바른 데이터 센터로 라우팅합니다. `https://api.omniture.com/`.

조직에서 특정 데이터 센터에서 데이터를 수집하거나 검색해야 하는 경우 다음을 사용하십시오.

| 데이터 센터 | URL |
|---|---|
| 런던 | `https://api3.omniture.com/` |
| 싱가포르 | `https://api4.omniture.com/` |
| 오리건 | `https://api5.omniture.com/` |

사용 [OSGi 번들을 구성하는 웹 콘솔](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) **Adobe AEM Analytics HTTP 클라이언트**. 추가 **데이터 센터 URL** AEM 페이지가 데이터를 수집하는 보고서 세트를 호스팅하는 데이터 센터용입니다.

![aa-7](assets/aa-07.png)

1. 웹 브라우저에서 웹 콘솔을 엽니다. ([https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr))
1. 콘솔에 액세스하려면 자격 증명을 입력합니다.

   >[!NOTE]
   >
   >이 콘솔에 대한 액세스 권한이 있는지 확인하려면 사이트 관리자에게 문의하십시오.

1. 이름이 인 구성 항목 선택 **Adobe AEM Analytics HTTP 클라이언트**.
1. 데이터 센터의 URL을 추가하려면 **데이터 센터 URL** 을 나열하고 상자에 URL을 입력합니다.

1. 목록에서 URL을 제거하려면 URL 옆에 있는 - 버튼을 클릭합니다.
1. 저장을 클릭합니다.

## Adobe Analytics에 연결 구성 {#configuring-the-connection-to-adobe-analytics}

>[!CAUTION]
>
>Adobe Analytics API의 보안 변경 사항으로 인해 AEM 내에 포함된 Activity Map 버전을 더 이상 사용할 수 없습니다.
>
>다음 [Adobe Analytics에서 제공하는 ActivityMap 플러그인](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html) 이제 를 사용해야 합니다.

## Activity Map 구성 {#configuring-for-the-activity-map}

>[!CAUTION]
>
>Adobe Analytics API의 보안 변경 사항으로 인해 AEM 내에 포함된 Activity Map 버전을 더 이상 사용할 수 없습니다.
>
>다음 [Adobe Analytics에서 제공하는 ActivityMap 플러그인](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html) 이제 를 사용해야 합니다.

## Adobe Analytics 프레임워크 만들기 {#creating-a-adobe-analytics-framework}

사용 중인 보고서 세트 ID(RSID)의 경우, 보고서 세트에 데이터를 기여하는 서버 인스턴스(작성자, 게시 또는 둘 다)를 제어할 수 있습니다.

* **모두**: 작성자와 게시 인스턴스의 정보가 보고서 세트를 채웁니다.
* **작성자**: 작성자 인스턴스의 정보만 보고서 세트를 채웁니다.
* **게시**: 게시 인스턴스의 정보만 보고서 세트를 채웁니다.

>[!NOTE]
>
>서버 인스턴스 유형을 선택해도 Adobe Analytics에 대한 호출은 제한되지 않으며 RSID를 포함하는 호출만 제어합니다.
>
>예를 들어 프레임워크는 *디버레테일* 보고서 세트 및 작성자가 선택한 서버 인스턴스입니다. 페이지가 프레임워크와 함께 게시되면 호출은 여전히 Adobe Analytics에 수행되지만 이러한 호출에는 RSID가 포함되지 않습니다. 작성자 인스턴스의 호출만 RSID를 포함합니다.

1. 사용 **탐색**, 선택 **도구**, **Cloud Service**, 그런 다음 **이전 Cloud Service**.
1. 다음으로 스크롤 **Adobe Analytics** 및 선택 **구성 표시**.
1. 다음을 클릭합니다. **[+]** Adobe Analytics 구성 옆에 있는 링크입니다.

1. 다음에서 **프레임워크 만들기** 대화 상자:

   * **제목**&#x200B;을 지정합니다.
   * 필요한 경우 다음을 지정할 수 있습니다. **이름**&#x200B;저장소에 프레임워크 세부 사항을 저장하는 노드용입니다.
   * 선택 **Adobe Analytics 프레임워크**

   및 클릭 **만들기**.

   편집할 프레임워크가 열립니다.

1. 다음에서 **보고서 세트** 측면 pod의 섹션(주 패널의 오른쪽)에서 **항목 추가**. 그런 다음 드롭다운을 사용하여 보고서 세트 ID를 선택합니다(예: `geometrixxauth`) 프레임워크와 상호 작용합니다.

   >[!NOTE]
   >
   >왼쪽의 컨텐츠 파인더는 보고서 세트 ID를 선택하면 Adobe Analytics 변수 (SiteCatalyst 변수)로 채워집니다.

1. 보고서 세트에 정보를 보낼 서버 인스턴스를 선택하려면 **실행 모드** 드롭다운(보고서 세트 ID 옆).

   ![aa-framework-01](assets/aa-framework-01.png)

1. 사이트의 게시 인스턴스에서 프레임워크를 사용하려면 **페이지** 사이드 킥의 탭, 클릭 **프레임워크를 활성화합니다.**

### Adobe Analytics에 대한 서버 설정 구성 {#configuring-server-settings-for-adobe-analytics}

프레임워크 시스템을 사용하면 각 Adobe Analytics 프레임워크 내에서 서버 설정을 변경할 수 있습니다.

>[!CAUTION]
>
>이러한 설정은 데이터가 전송되는 위치와 방법을 결정하므로 반드시 수행해야 합니다 *이 설정을 변경하지 마십시오.* Adobe Analytics 담당자가 대신 설정하도록 하십시오.

패널을 열어 시작하십시오. 옆에 있는 아래쪽 화살표를 누릅니다 **서버**:

![server_001](assets/server_001.png)

* **추적 서버**

   * Adobe Analytics 호출을 전송하는 데 사용되는 URL을 포함합니다.

      * `cname` - 기본값은 Adobe Analytics 계정의 *회사 이름*
      * `d1` - 정보가 전송되는 데이터 센터에 해당합니다(다음 중 하나). `d1`, `d2`, 또는 `d3`)
      * `sc.omtrdc.net` - 도메인 이름

* **보안 추적 서버**

   * 추적 서버와 동일한 세그먼트 있음
   * 보안 페이지에서 데이터를 전송하는 데 사용됩니다(`https://`)

* **방문자 네임스페이스**

   * 네임스페이스는 추적 URL의 첫 번째 부분을 결정합니다.
   * 예를 들어 네임스페이스를 **CNAME** 은 Adobe Analytics에 대한 호출이 **CNAME.d1.omtrdc.net** 기본 값 대신 사용합니다.

## 페이지를 Adobe Analytics 프레임워크와 연결 {#associating-a-page-with-a-adobe-analytics-framework}

페이지가 Adobe Analytics 프레임워크와 연결되면 페이지가 로드될 때 Adobe Analytics에 데이터를 전송합니다. 페이지가 채우는 변수는 프레임워크의 Adobe Analytics 변수에서 매핑되고 검색됩니다. 예를 들어 페이지 보기는 Adobe Analytics에서 검색됩니다.

페이지의 하위 항목은 프레임워크와의 연결을 상속합니다. 예를 들어 사이트의 루트 페이지를 프레임워크에 연결하면 사이트의 모든 페이지가 프레임워크에 연결됩니다.

1. 다음에서 **사이트** 콘솔을 누르고 추적을 설정할 페이지를 선택합니다.
1. 를 엽니다. **[페이지 속성](/help/sites-authoring/editing-page-properties.md)**&#x200B;콘솔에서 직접 가져오거나 페이지 편집기에서 가져옵니다.
1. ** Cloud Service** 탭을 엽니다.

1. 사용 **구성 추가** 선택 드롭다운 **Adobe Analytics** 사용 가능한 옵션에서 상속이 있는 경우 선택기를 사용하려면 먼저 상속을 비활성화하십시오.

1. 에 대한 드롭다운 선택기 **Adobe Analytics** 는 사용 가능한 옵션에 추가됩니다. 필요한 프레임워크 구성을 선택합니다.

1. **저장 후 닫기**&#x200B;를 선택합니다.
1. 페이지 및 연결된 구성/파일을 활성화하려면 **[게시](/help/sites-authoring/publishing-pages.md)** 페이지.
1. 마지막 단계는 게시 인스턴스의 페이지를 방문하여 를 사용하여 키워드(예: 가지)를 검색하는 것입니다. **검색** 구성 요소.
1. 그런 다음 적절한 도구를 사용하여 Adobe Analytics에 대한 호출을 확인할 수 있습니다. 예: [Adobe Experience Cloud 디버거](https://experienceleague.adobe.com/docs/experience-platform/debugger/home.html).
1. 제공된 예를 사용하면 호출에는 event7에 입력한 값(즉, 가지)이 포함되어야 하며 eVar 목록에는 event3이 있어야 합니다.

### 페이지 조회수 {#page-views}

페이지가 Adobe Analytics 프레임워크와 연결된 경우 사이트 콘솔의 목록 보기에 페이지 보기 수가 표시될 수 있습니다.

다음을 참조하십시오 [페이지 분석 데이터 보기](/help/sites-authoring/page-analytics-using.md) 을 참조하십시오.

### 가져오기 간격 구성 {#configuring-the-import-interval}

의 적절한 인스턴스 구성 **Adobe AEM Analytics Report Sling Importer** 서비스:

* **가져오기 시도 횟수**: 대기 중인 보고서 가져오기 시도 횟수입니다.
기본값은 `6`입니다.

* **가져오기 지연**: 대기 중인 보고서 가져오기 시도 사이의 시간(밀리초)
기본값은 입니다 `10000`. 밀리초 단위이므로 10초입니다.

* **가져오기 빈도**: A `cron` Analytics 보고서를 가져오는 빈도를 결정하는 표현식입니다.
기본값은 입니다 `0 0 0/12 * * ?`: 매시간 12회 페치에 해당합니다.

이 OSGi 서비스를 구성하려면 다음을 사용할 수 있습니다. [웹 콘솔](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) 또는 [저장소의 osgiConfig 노드](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) (서비스 PID: `com.day.cq.analytics.sitecatalyst.impl.importer.ReportImporterScheduler`).

## Adobe Analytics 구성 및/또는 프레임워크 편집 {#editing-adobe-analytics-configurations-and-or-frameworks}

Adobe Analytics 구성 또는 프레임워크를 만들 때와 마찬가지로 (기존)으로 이동합니다. **Cloud Service** 화면. 선택 **구성 표시**&#x200B;을 클릭한 다음 업데이트할 특정 구성에 대한 링크를 클릭합니다.

Adobe Analytics 구성을 편집할 때 **편집** 구성 페이지 자체에서 을 열 때 **구성 요소 편집** 대화 상자.

## Adobe Analytics 프레임워크 삭제 {#deleting-adobe-analytics-frameworks}

Adobe Analytics 프레임워크를 삭제하려면 먼저 [편집을 위해 열기](#editing-adobe-analytics-configurations-and-or-frameworks).

그런 다음 을 선택합니다 **프레임워크 삭제** 다음에서 **페이지** 사이드 킥의 탭
