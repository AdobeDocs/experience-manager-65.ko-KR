---
title: Adobe Search&Promote와 통합
seo-title: Adobe Search&Promote와 통합
description: Adobe Search&Promote와 통합하는 방법을 살펴보십시오.
seo-description: Adobe Search&Promote와 통합하는 방법을 살펴보십시오.
uuid: 7e9384d9-9e4f-4e00-a1c9-35547de6ceb8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: aca444f6-418a-4c01-ae19-663b4e04fab9
docset: aem65
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd

---


# Integrating with Adobe Search&amp;Promote{#integrating-with-adobe-search-promote}

웹 사이트에서 Adobe Search&amp;Promote 서비스를 호출하려면 다음 작업을 수행하십시오.

1. 클라우드의 URL을 지정합니다.
1. Search&amp;Promote 서비스에 대한 연결을 구성합니다.
1. Search&amp;Promote 구성 요소를 사이드킥에 추가합니다.
1. 구성 요소를 사용하여 컨텐츠를 작성합니다. (웹 [페이지에 Search&amp;Promote 기능 추가를 참조하십시오](/help/sites-authoring/search-and-promote.md).)
1. 페이지에 배너를 추가합니다. 배너 이미지는 Search&amp;Promote 데이터에 민감합니다.
1. Search&amp;Promote 서비스가 사용할 사이트 맵을 생성합니다.

>[!NOTE]
>
>사용자 지정 프록시 구성과 함께 Search&amp;Promote를 사용하는 경우, AEM의 일부 기능이 3.x API를 사용하고 있고 일부 다른 API는 4.x API를 사용하고 있으므로 HTTP 클라이언트 프록시 구성을 모두 구성해야 합니다.
>
>* 3.x는 https://localhost:4502/system/console/configMgr/com.day.commons.httpclient로 구성되어 [있습니다.](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* 4.x는 https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator로 구성되어 [있습니다.](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>



## Search&amp;Promote 서비스 URL 변경 {#changing-the-search-promote-service-url}

Search&amp;Promote 서비스에 대해 구성된 기본 URL은 `https://searchandpromote.omniture.com/px/`입니다. 다른 서비스를 사용하려면 OSGi 콘솔을 사용하여 다른 URL을 지정합니다.

1. OSGi 콘솔을 열고 구성 탭을 클릭합니다. ([https://localhost:4502/system/console/configMgr.](https://localhost:4502/system/console/configMgr))
1. Day CQ Search&amp;Promote Configuration 항목을 클릭합니다.
1. [원격 서버 URI] 상자에 URL을 입력하고 [저장]을 클릭합니다.

## Search&amp;Promote에 대한 연결 구성 {#configuring-the-connection-to-search-promote}

웹 페이지가 서비스와 상호 작용할 수 있도록 Search&amp;Promote에 대한 하나 이상의 연결을 구성합니다. 연결하려면 Search&amp;Promote 계정의 멤버 ID와 계정 번호가 필요합니다.

1. 도구 **아이콘 >** 배포에서 **클라우드**&#x200B;서비스를 **선택합니다**.

   그러면 클라우드 서비스 대시보드로 이동합니다. 로컬 컴퓨터에서 대시보드의 URL은 다음과 같이 표시됩니다.

   [https://localhost:4502/libs/cq/core/content/tools/cloudservices.html](https://localhost:4502/libs/cq/core/content/tools/cloudservices.html)

1. 클라우드 서비스 페이지에서 Adobe Search&amp;Promote 링크 또는 Search&amp;Promote 아이콘을 클릭합니다.

1. 처음으로 Adobe Search&amp;Promote를 구성하는 경우 지금 구성을 클릭하여 **구성** 만들기 패널을 엽니다.

   Search&amp;Promote에 대한 자세한 내용을 보려면 **자세한 내용을**&#x200B;클릭하십시오.

   ![](assets/chlimage_1-59.png)

1. 페이지 **작성자가** 인식할 수 있는 제목을 입력하고 고유한 이름을 **입력한 다음**&#x200B;만들기를 **클릭합니다**.

   The **Edit Component** window opens.

   또한 새로 만든 구성은 클라우드 서비스 **대시보드** Adobe Search&amp;Promote 목록 **항목의 사용 가능한 구성** 아래에 표시됩니다.

   ![](assets/chlimage_1-60.png)

1. 구성 요소 편집 대화 상자의 필드에 **다음을** 추가합니다.

   * **구성원 ID**
   * **계정 번호**
   >[!NOTE]
   >
   >이 정보를 **직접 얻으려면** 먼저
   >
   >[https://searchandpromote.omniture.com/center/](https://searchandpromote.omniture.com/center/)
   >
   >
   >유효한 Search&amp;Promote 자격 증명 사용(이메일/암호).
   >그런 다음 브라우저의 주소 표시줄에 있는 URL을 확인해야 합니다. 이 URL은 다음과 같습니다.
   >[](https://searchandpromote.omniture.com/px/home/?sp_id=XXXXXXXX-spYYYYYYYY)
   >
   >[https://searchandpromote.omniture.com/px/home/?sp_id=XXXXXXXX-spYYYYYYYY](https://searchandpromote.omniture.com/px/home/?sp_id=XXXXXXXX-spYYYYYYYY)
   >
   >**위치:**
   >
   >    * **XXXXXXXX는** 귀하의** 회원 ID에 해당합니다**
   >    * **spYYYYYY는** 계정 **번호와 일치함**


1. Click **Connect To Search&amp;Promote**.

   연결 성공 메시지가 나타나면 확인을 **클릭합니다**.

   연결 후 단추 텍스트가** Search&amp;Promote에 다시 연결**로 변경됩니다.

1. **확인**&#x200B;을 클릭합니다. 방금 만든 구성에 대해 [Search&amp;Promote 설정] 페이지가 나타납니다.

## 데이터 센터 구성 {#configuring-the-data-center}

Search&amp;Promote 계정이 아시아 또는 유럽에 있는 경우 기본 데이터 센터를 변경하여 올바른 데이터 센터를 가리켜야 합니다(기본 데이터 센터는 북미 계정).

데이터 센터를 구성하려면:

1. 웹 콘솔의 `https://localhost:4502/system/console/configMgr/com.day.cq.searchpromote.impl.SearchPromoteServiceImpl`

   ![](assets/chlimage_1-61.png)

1. 서버 위치에 따라 URI를 다음 중 하나로 변경합니다.

   * 북미: [https://center.atomz.com/px/](https://center.atomz.com/px/)
   * EMEA: [https://center.lon5.atomz.com/px/](https://center.lon5.atomz.com/px/)
   * APAC: [https://center.sin2.atomz.com/px/](https://center.sin2.atomz.com/px/)

1. **저장**&#x200B;을 클릭합니다.

## 사이드 킥에 Search&amp;Promote 구성 요소 추가 {#adding-search-promote-components-to-sidekick}

디자인 모드에서 **par** 구성 요소를 편집하여 사이드 킥에서 Search&amp;Promote 구성 요소를 허용합니다. (See the [Components](/help/sites-developing/components.md#addinganewcomponenttotheparagraphsystemdesignmode) documentation for more information.)

구성 요소 사용에 대한 자세한 내용은 웹 페이지에 [Search&amp;Promote 기능 추가를 참조하십시오](/help/sites-authoring/search-and-promote.md).

## 페이지에서 사용하는 Search&amp;Promote 서비스 지정 {#specifying-the-search-promote-service-that-your-pages-use}

특정 Search&amp;Promote 서비스를 사용하도록 웹 페이지를 구성합니다. Search&amp;Promote 구성 요소는 호스트 페이지의 서비스를 자동으로 사용합니다.

페이지에 대한 Search&amp;Promote 속성을 구성하면 모든 하위 페이지가 설정을 상속합니다. 필요한 경우 상속된 설정을 무시하도록 하위 페이지를 구성할 수 있습니다.

>[!NOTE]
>
>서비스 연결을 이미 구성해야 합니다. ( [Search&amp;Promote에 대한 연결 구성을 참조하십시오](#connection).)

1. 페이지 **속성** 대화 상자를 엽니다. 예를 들어** 웹 사이트** 페이지에서 페이지를 마우스 오른쪽 단추로 클릭하고 속성을 **클릭합니다**.
1. 클라우드 서비스 **탭을** 클릭합니다.
1. 상위 페이지에서 클라우드 서비스 구성의 상속을 비활성화하려면 상속 경로 옆에 있는 자물쇠 아이콘을 클릭합니다.

   ![](assets/sandpinheritpadlock.png)

1. 서비스 **추가를**&#x200B;클릭하고 Adobe **Search&amp;Promote를**&#x200B;선택한 다음 확인을 **클릭합니다**.
1. Search&amp;Promote 계정에 대한 연결 구성을 선택한 다음 확인을 **클릭합니다**.

## Product Feed {#product-feed}

Search&amp;Promote 통합을 통해 다음 작업을 수행할 수 있습니다.

* 기본 저장소 구조 및 상거래 플랫폼과는 별도로 eCommerce API를 사용합니다.
* search&amp;Promote의 색인 커넥터 기능을 활용하여 제품 피드를 XML 형식으로 제공합니다.
* search&amp;Promote의 원격 제어 기능을 활용하여 제품 피드의 on-demand 또는 예약된 요청을 수행할 수 있습니다.
* 클라우드 서비스 구성으로 구성된 다양한 Search&amp;Promote 계정에 대한 피드 생성.

자세한 내용은 제품 [피드를 참조하십시오](/help/sites-administering/product-feed.md).
