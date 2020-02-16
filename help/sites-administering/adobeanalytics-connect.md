---
title: Adobe Analytics에 연결 및 프레임워크 만들기
seo-title: Adobe Analytics에 연결 및 프레임워크 만들기
description: AEM을 SiteCatalyst에 연결하고 프레임워크를 만드는 방법에 대해 알아봅니다.
seo-description: AEM을 SiteCatalyst에 연결하고 프레임워크를 만드는 방법에 대해 알아봅니다.
uuid: 3820dd24-4193-42ea-aef2-4669ebfeaa9d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 6b545a51-3677-4ea1-ac7e-2d01ba19283e
docset: aem65
translation-type: tm+mt
source-git-commit: 4b965d8f7814816126601f6366c1ba313e404538

---


# Adobe Analytics에 연결 및 프레임워크 만들기 {#connecting-to-adobe-analytics-and-creating-frameworks}

Adobe Analytics에서 AEM 페이지에서 웹 데이터를 추적하려면 Adobe Analytics 클라우드 서비스 구성 및 Adobe Analytics 프레임워크를 만드십시오.

* **** Adobe Analytics 구성:Adobe Analytics 계정에 대한 정보입니다. Adobe Analytics 구성을 사용하면 AEM이 Adobe Analytics에 연결할 수 있습니다. 사용하는 각 계정에 대해 Adobe Analytics 구성을 만듭니다.
* **** Adobe Analytics Framework:Adobe Analytics 보고서 세트 속성과 CQ 변수 간의 매핑 집합. 프레임워크를 사용하여 웹 사이트 데이터가 Adobe Analytics 보고서를 채우는 방법을 구성합니다. 프레임워크는 Adobe Analytics 구성과 연결됩니다. 각 구성에 대해 여러 프레임워크를 만들 수 있습니다.

웹 페이지를 프레임워크와 연결할 때 프레임워크는 해당 페이지 및 해당 페이지의 하위 멤버에 대한 추적을 수행합니다. 그런 다음 Adobe Analytics에서 페이지 보기를 검색하여 사이트 콘솔에 표시할 수 있습니다.

## 전제 조건 {#prerequisites}

### Adobe Analytics Account {#adobe-analytics-account}

Adobe Analytics에서 AEM 데이터를 추적하려면 유효한 Adobe Marketing Cloud Adobe Analytics 계정이 있어야 합니다.

Adobe Analytics 계정은 다음 작업을 수행해야 합니다.

* 관리자 **권한** 있음
* 웹 서비스 액세스 **사용자 그룹에** 할당됩니다.

>[!CAUTION]
>
>Adobe **Analytics** 내에서 관리자 권한을 제공한다고 해서 사용자가 AEM에서 Adobe Analytics로 연결할 수 있는 것은 아닙니다. 계정에는 웹 서비스 **액세스 권한도 있어야** 합니다.

![chlimage_1-67](assets/chlimage_1-67.png)

계속하기 전에 자격 증명으로 Adobe Analytics에 로그인할 수 있는지 확인하십시오. 다음 중 하나를 통해:

* [https://marketing.adobe.com](https://marketing.adobe.com)

* [https://sc.omniture.com/login/](https://sc.omniture.com/login/)

### Adobe Analytics 데이터 센터를 사용하도록 AEM 구성 {#configuring-aem-to-use-your-adobe-analytics-data-centers}

Adobe Analytics [데이터 센터는](https://developer.omniture.com/en_US/content_page/concepts-terminology/c-how-is-data-stored) Adobe Analytics 보고서 세트와 관련된 데이터를 수집, 처리 및 저장합니다. Adobe Analytics 보고서 세트를 호스팅하는 데이터 센터를 사용하도록 AEM을 구성해야 합니다. 다음 표에는 사용 가능한 데이터 센터와 해당 URL이 나와 있습니다.

| 데이터 센터 | URL |
|---|---|
| 산 호세 | https://api.omniture.com/admin/1.4/rest/ |
| 달라스 | https://api2.omniture.com/admin/1.4/rest/ |
| 런던 | https://api3.omniture.com/admin/1.4/rest/ |
| 싱가포르 | https://api4.omniture.com/admin/1.4/rest/ |
| 오리건 | https://api5.omniture.com/admin/1.4/rest/ |

AEM 파섹

웹 콘솔을 [사용하여 OSGi 번들](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) Adobe AEM Analytics HTTP **클라이언트를 구성합니다**. AEM **페이지에서** 데이터를 수집하는 보고서 세트를 호스팅하는 데이터 센터의 데이터 센터 URL을 추가합니다.

![aa-07](assets/aa-07.png)

1. 웹 브라우저에서 웹 콘솔을 엽니다. ([https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr))
1. 콘솔에 액세스할 자격 증명을 입력합니다.

   >[!NOTE]
   >
   >이 콘솔에 액세스할 수 있는지 확인하려면 사이트 관리자에게 문의하십시오.

1. Adobe AEM Analytics HTTP **Client라는 구성 항목을 선택합니다**.
1. 데이터 센터의 URL을 추가하려면 데이터 센터 URL 목록 옆에 있는 + **단추를** 누르고 상자에 URL을 입력합니다.

1. 목록에서 URL을 제거하려면 URL 옆에 있는 - 단추를 클릭합니다.
1. [저장]을 클릭합니다.

## Configuring the Connection to Adobe Analytics {#configuring-the-connection-to-adobe-analytics}

>[!CAUTION]
>
>Adobe Analytics API의 보안 변경 사항으로 인해, AEM 내에 포함된 Activity Map 버전을 더는 사용할 수 없습니다.
>
>The [ActivityMap plugin provided by Adobe Analytics](https://docs.adobe.com/content/help/en/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html) should now be used.

## Configuring for the Activity Map {#configuring-for-the-activity-map}

>[!CAUTION]
>
>Adobe Analytics API의 보안 변경 사항으로 인해, AEM 내에 포함된 Activity Map 버전을 더는 사용할 수 없습니다.
>
>The [ActivityMap plugin provided by Adobe Analytics](https://docs.adobe.com/content/help/en/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html) should now be used.

## Adobe Analytics 프레임워크 만들기 {#creating-a-adobe-analytics-framework}

사용 중인 보고서 세트 ID(RSID)의 경우 보고서 세트에 데이터를 기여하는 서버 인스턴스(작성자, 게시 또는 둘 다)를 제어할 수 있습니다.

* **모두**:작성자와 게시 인스턴스의 정보가 보고서 세트를 채웁니다.
* **작성자**:작성자 인스턴스의 정보만 보고서 세트를 채웁니다.
* **게시**:게시 인스턴스의 정보만 보고서 세트를 채웁니다.

>[!NOTE]
>
>서버 인스턴스 유형을 선택하더라도 Adobe Analytics에 대한 호출은 제한되지 않으며 RSID를 포함하는 호출만 제어합니다.
>
>예를 들어, 프레임워크는 *다이웨소매* 보고서 세트를 사용하도록 구성되었으며 작성자는 선택한 서버 인스턴스입니다. 페이지가 프레임워크와 함께 게시되더라도 Adobe Analytics에 대한 호출은 여전히 수행되지만, 이러한 호출에는 RSID가 포함되지 않습니다. 작성자 인스턴스의 호출에만 RSID가 포함됩니다.

1. 도구 **, 클라우드**&#x200B;서비스 **를**&#x200B;선택한 **다음** Legacy Cloud **Services**&#x200B;를선택합니다.
1. Adobe Analytics **로 스크롤하고** 사용 가능한 구성 **옆에 있는** [+] **를**&#x200B;클릭합니다.
1. Adobe Analytics 구성 옆에 있는 **[+]** 링크를 클릭합니다.

1. 프레임워크 **만들기** 대화 상자에서 다음을 수행합니다.

   * 제목을 **지정합니다**.
   * 원할 경우, 저장소에 **프레임워크**&#x200B;세부 사항을 저장하는 노드에 대해 이름을 지정할 수 있습니다.
   * Adobe **Analytics Framework 선택**
   만들기를 **클릭합니다**.

   편집을 위해 프레임워크가 열립니다.

1. 사이드 **창의** [보고서 세트] 섹션(기본 패널의 오른쪽)에서 [항목 추가] **를 클릭합니다**. 그런 다음 드롭다운을 사용하여 프레임워크와 상호 작용할 보고서 세트 ID(예: `geometrixxauth`)를 선택합니다.

   >[!NOTE]
   >
   >왼쪽의 컨텐츠 파인더는 보고서 세트 ID를 선택하면 Adobe Analytics 변수(SiteCatalyst 변수)로 채워집니다.

1. 그런 다음 **보고서 세트** ID 옆에 있는 실행 모드 드롭다운을 사용하여 정보를 보고서 세트로 전송할 서버 인스턴스를 선택합니다.

   ![aa-framework-01](assets/aa-framework-01.png)

1. 사이트의 게시 인스턴스에서 프레임워크를 사용할 수 있게 하려면 사이드 킥의 **페이지** 탭에서 프레임워크 **활성화를 클릭합니다.**

### Adobe Analytics에 대한 서버 설정 구성 {#configuring-server-settings-for-adobe-analytics}

프레임워크 시스템을 사용하면 각 Adobe Analytics 프레임워크 내에서 서버 설정을 변경할 수 있습니다.

>[!CAUTION]
>
>이러한 설정은 데이터의 전송 위치와 방법을 결정하므로 이러한 설정을 *변경하지* 않고 Adobe Analytics 담당자가 직접 설정해야 합니다.

먼저 패널을 엽니다. 서버 옆에 있는 아래쪽 화살표를 **누릅니다**.

![server_001](assets/server_001.png)

* **서버 추적**

   * Adobe Analytics 호출을 전송하는 데 사용되는 URL을 포함합니다.

      * cname - 기본값은 Adobe Analytics 계정의 회사 *이름입니다.*
      * d1 - 정보가 전송될 데이터 센터에 해당합니다(d1, d2 또는 d3 가능).
      * sc.omtrdc.net - 도메인 이름

* **보안 추적 서버**

   * 추적 서버와 동일한 세그먼트
   * 보안 페이지에서 데이터를 전송하는 데 사용됩니다(https://).

* **방문자 네임스페이스**

   * 네임스페이스는 추적 URL의 첫 번째 부분을 결정합니다.
   * 예를 들어, 네임스페이스를 CNAME으로 **변경하면** Adobe Analytics에 대한 호출이 **기본값이 아닌 CNAME.d1.omtrdc.net** 처럼 보입니다.

## Adobe Analytics 프레임워크와 페이지 연결 {#associating-a-page-with-a-adobe-analytics-framework}

페이지가 Adobe Analytics 프레임워크와 연결되면 페이지가 로드되면 페이지가 Adobe Analytics로 데이터를 전송합니다. 페이지가 채우는 변수는 프레임워크의 Adobe Analytics 변수에서 매핑되고 검색됩니다. 예를 들어 페이지 보기는 Adobe Analytics에서 검색됩니다.

페이지의 하위 항목은 프레임워크와의 연결을 상속합니다. 예를 들어 사이트의 루트 페이지를 프레임워크와 연결하면 사이트의 모든 페이지가 프레임워크와 연결됩니다.

1. 사이트 **콘솔에서** 추적으로 설정할 페이지를 선택합니다.
1. 콘솔 **[또는 페이지](/help/sites-authoring/editing-page-properties.md)**편집기에서 직접 페이지 속성을 엽니다.
1. ** 클라우드 서비스* 탭을 엽니다.

1. 구성 **추가** 드롭다운을 사용하여 사용 가능한 **옵션에서 Adobe** Analytics를 선택합니다. 상속이 있는 경우 선택기를 사용할 수 있게 되기 전에 상속을 비활성화해야 합니다.

1. Adobe Analytics의 **드롭다운 선택기가** 사용 가능한 옵션에 추가됩니다. 이 구성 요소를 사용하여 필요한 프레임워크 구성을 선택합니다.

1. 저장 **및 닫기를 선택합니다**.
1. **[페이지를 게시하여](/help/sites-authoring/publishing-pages.md)**페이지와 연결된 구성/파일을 활성화합니다.
1. 최종 단계는 게시 인스턴스의 페이지를 방문하여 검색 구성 요소를 사용하여 키워드(예: 가지)를 검색하는 **것입니다** .
1. 그런 다음 적절한 도구를 사용하여 Adobe Analytics에 대한 호출을 확인할 수 있습니다.예: [Adobe Marketing Cloud Debugger](https://marketing.adobe.com/resources/help/en_US/sc/implement/debugger_install.html).
1. 제공된 예제를 사용하여 호출에는 eVar7에 입력된 값(즉, eggplant)이 포함되어야 하며 이벤트 목록에는 event3이 포함되어야 합니다.

### 페이지 조회수 {#page-views}

페이지가 Adobe Analytics 프레임워크와 연결되면 사이트 콘솔의 목록 보기에 페이지 보기 수를 표시할 수 있습니다.

자세한 [내용은 페이지](/help/sites-authoring/page-analytics-using.md) 분석 데이터 보기를 참조하십시오.

### 가져오기 간격 구성 {#configuring-the-import-interval}

Adobe AEM Managed Polling **구성 서비스의 적절한 인스턴스를 구성합니다** .

* **투표 간격**:서비스가 Adobe Analytics에서 페이지 보기 데이터를 검색하는 간격(초)입니다.
기본 간격은 43200000ms(12시간)입니다.

* **활성화**:서비스를 활성화하거나 비활성화합니다. 기본적으로 서비스가 활성화됩니다.

이 OSGi 서비스를 구성하려면 웹 [콘솔](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) 또는 저장소의 [osgiConfig 노드](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) (서비스 PID는 `com.day.cq.polling.importer.impl.ManagedPollConfigImpl`)를사용할 수 있습니다.

## Adobe Analytics 구성 및/또는 프레임워크 편집 {#editing-adobe-analytics-configurations-and-or-frameworks}

Adobe Analytics 구성 또는 프레임워크를 만들 때처럼 (기존) 클라우드 서비스 **화면으로** 이동합니다. 구성 **표시를**&#x200B;선택한 다음 업데이트할 특정 구성에 대한 링크를 클릭합니다.

Adobe Analytics 구성을 편집할 때 구성 페이지 **자체에서** 편집 단추를 눌러 구성 요소 편집 **대화 상자를 열어야** 합니다.

## Adobe Analytics 프레임워크 삭제 {#deleting-adobe-analytics-frameworks}

Adobe Analytics 프레임워크를 삭제하려면 먼저 [열어 편집합니다](#editing-adobe-analytics-configurations-and-or-frameworks).

그런 다음 **사이드킥의** 페이지 **탭에서** 프레임워크 삭제를 선택합니다.

