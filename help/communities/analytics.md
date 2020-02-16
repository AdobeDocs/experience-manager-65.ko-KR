---
title: 커뮤니티 기능에 대한 분석 구성
seo-title: 커뮤니티 기능에 대한 분석 구성
description: 커뮤니티에 대한 분석 구성
seo-description: 커뮤니티에 대한 분석 구성
uuid: 5a083645-9de6-4ecd-a94e-a40143f92edf
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: e6fdaf56-402f-418d-96d8-e46bd3ad1e8c
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# 커뮤니티 기능에 대한 분석 구성{#analytics-configuration-for-communities-features}

## 개요 {#overview}

Adobe Analytics와 Adobe Experience Manager(AEM)는 모두 Adobe Marketing Cloud의 솔루션입니다.

AEM Communities에 대해 Adobe Analytics를 구성할 수 있으므로 구성원이 지원되는 커뮤니티 기능과 상호 작용하면 보고서가 생성되는 이벤트가 Adobe Analytics로 전송됩니다.

예를 들어 활성 커뮤니티 사이트의 구성원이 할당된 비디오 리소스를 보는 경우 리소스 플레이어는 비디오 하트비트 데이터를 포함하여 이벤트를 Analytics로 보냅니다. 커뮤니티 사이트에서 관리자는 비디오 재생과 관련된 다양한 보고서를 볼 수 있습니다.

또한 다음과 같은 경우 분석이 필요합니다.

* 게시 환경에서:

   * 커뮤니티 [트렌드 보고](/help/communities/trends.md)
   * 사이트 방문자가 &quot;가장 많이 본&quot;, &quot;가장 활성&quot;, &quot;가장 좋아함&quot;별로 정렬하도록 허용
   * UGC 목록의 뷰 카운트

* 작성 환경에서:

   * 기여도 데이터를 [멤버 관리 콘솔에서](/help/communities/members.md) 표시(보기, 게시물, 팔로잉, 좋아요)
   * 활성 리소스 [보고서를 위한 트렌드 요약, 비디오 하트비트 및 비디오 디바이스](/help/communities/reports.md)

지원되는 커뮤니티 기능은 다음과 같습니다.

* [역량 강화 리소스](/help/communities/resources.md)
* [포럼](/help/communities/forum.md)
* [QnA](/help/communities/working-with-qna.md)
* [블로그](/help/communities/blog-feature.md)
* [파일 라이브러리](/help/communities/file-library.md)
* [달력](/help/communities/calendar.md)

설명서의 이 섹션에서는 Analytics 보고서 세트와 커뮤니티 기능을 연결하는 방법에 대해 설명합니다. 기본 단계는 다음과 같습니다.

1. [암호화 키를](#replicate-the-crypto-key) 복제하여 모든 AEM 인스턴스에서 암호화/암호 해독이 올바르게 수행되도록 합니다.
1. Adobe Analytics [보고서 세트 준비](#adobe-analytics-report-suite-for-video-reporting)
1. AEM Analytics [클라우드 서비스](#aem-analytics-cloud-service-configuration) 및 [프레임워크 만들기](#aem-analytics-framework-configuration)

1. [커뮤니티 사이트에](#enable-analytics-for-a-community-site) 대한 분석 활성화
1. [**AEM **](#verify-analytics-to-aem-variable-mapping)변수 매핑에 대한 분석 확인
1. 기본 [게시자 식별](#primary-publisher)
1. [커뮤니티 사이트](#publish-community-site-and-analytics-cloud-service) 게시
1. Adobe Analytics에서 커뮤니티 사이트로 보고서 데이터 [](#obtaining-reports-from-analytics) 가져오기 구성

## 전제 조건 {#prerequisites}

Analytics for Communities 기능을 구성하려면 계정 담당자와 협력하여 Adobe Analytics 계정 및 [보고서 세트를](#adobe-analytics-report-suite-for-video-reporting)설정해야 합니다. 설정된 후에는 다음 정보를 사용할 수 있습니다.

* 회사 이름Adobe Analytics 계정과 연결된 회사
* 사용자 이름 Analytics 계정을 관리할 수 있는 사용자의 로그인 사용자 이름(웹 서비스 액세스 권한 포함)

* 암호 인증된 사용자의 로그인 암호
* Analytics 데이터 센터 계정의 Analytics 데이터 센터의 URL
* 보고서 세트 사용할 Analytics 보고서 세트의 이름

## 비디오 보고를 위한 Adobe Analytics 보고서 세트 {#adobe-analytics-report-suite-for-video-reporting}

Adobe Marketing Cloud의 보고서 [세트 관리자를](https://marketing.adobe.com/resources/help/en_US/reference/new_report_suite.html)사용하여 커뮤니티 사이트에서 커뮤니티 기능에 대한 보고서를 제공하도록 Analytics 보고서 세트를 구성할 수 있습니다.

회사 이름과 [사용자 이름으로](https://marketing.adobe.com/resources/help/en_US/analytics/getting-started/analytics-navigation.html) Adobe Marketing Cloud에 [](/help/communities/analytics.md#prerequisites)로그인하면 새 보고서 세트 또는 기존 보고서 세트를 구성할 수 있습니다.

* [11 전환 변수](https://marketing.adobe.com/resources/help/en_US/reference/conversion_var_admin.html) (eVar)

   * **`evar1`** - 사용 **`evar11`**

   * 기존 eVar를 재사용하거나(이름 변경) 커뮤니티 기능에 사용할 새 eVar를 만들 수 있습니다.

* [7 성공 이벤트](https://marketing.adobe.com/resources/help/en_US/reference/success_event.html) (이벤트)

   * **`event1`** - 사용 **`event7`**

   * 유형 **`Counter`**

      * 아님 **`Counter (no subrelations)`**
   * 기존 이벤트를 재사용하거나(이름 변경) 커뮤니티 기능에 사용할 새 이벤트를 만들 수 있습니다.


* [비디오 관리](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/video_analytics_config.html)

   * 비디오 보고 콘솔

      * 활성화 `Video Core`
      * 저장 선택
   * 비디오 코어 측정 콘솔

      * select `Use Solution Variables`
      * 저장 선택


새 보고서 세트를 ****&#x200B;사용하는 경우 새 보고서 세트에는 4개의 evar 및 6개의 이벤트 변수만 있고, Communities에는 11개의 evar 및 7개의 이벤트 변수가 필요합니다.

기존 보고서 세트를 **사용하는 경우 커뮤니티 사이트에 대한 Analytics 프레임워크를 활성화하기 전에 변수 매핑을**[](#modifying-analytics-variable-mapping) 수정해야 할 수 있습니다. 커뮤니티 전용 변수에 대한 우려 사항은 계정 담당자에게 문의하십시오.

>[!CAUTION]
>
>**If using a existing report suite that already uses variables within**
>
>* **`evar1`** through **`evar11`**
   >
   >
* **`event1`** through **`event7`**
>
>
**그런 다음 커뮤니티 사이트를 게시하기 전에** Analytics가 커뮤니티 사이트에 대해 활성화되었을 때 Analytics 변수에 자동으로 매핑되는 AEM 변수를 이동하여 기존 매핑을 복원하는 것이 중요합니다.
>
>기존 매핑을 복원하고 AEM 변수를 다른 Analytics 변수로 이동하려면 Analytics 변수 매핑 [수정에 대한 섹션을 참조하십시오](#modifying-analytics-variable-mapping).
>
>이렇게 하지 않으면 복구할 수 없는 데이터 손실이 발생할 수 있습니다.

### 비디오 하트비트 분석 {#video-heartbeat-analytics}

비디오 하트비트 분석에 라이센스가 부여되면 `Marketing Cloud Org Id` 가 할당됩니다.

비디오 보고를 [위해 Analytics 보고서 세트를](#adobe-analytics-report-suite-for-video-reporting)구성한 후 비디오 하트비트 보고를 활성화하려면:

* analytics 클라우드 [서비스 만들기](#aem-analytics-cloud-service-configuration)
* 커뮤니티 [사이트에 대한 분석 활성화](#enable-analytics-for-a-community-site)
* 커뮤니티 사이트에 `Marketing Cloud Org Id` 연결

커뮤니티 사이트 속성을 `Marketing Cloud Org Id`[수정하여](/help/communities/sites-console.md#enablement) [커뮤니티 사이트 생성](/help/communities/sites-console.md#modifying-site-properties) 시 또는 나중에 입력할수 있습니다. [](#aem-analytics-cloud-service-configuration)

![chlimage_1-177](assets/chlimage_1-177.png)

비디오 하트비트 분석이 활성화되면 비디오 플레이어에 대한 JavaScript(JS) 코드는 비디오 하트비트 라이브러리 코드(JS라고도 함)를 인스턴스화하여 10초마다(구성할 수 없음) 비디오 추적 서버로 비디오 상태 업데이트를 전송하는 모든 논리를 처리하고 결국 비디오 세션의 누적 보고서를 기본 Analytics 서버로 보냅니다.

활성화하지 않으면 비디오 하트비트 코드가 인스턴스화되지 않고 비디오 진행 및 다시 시작 위치 추적만 보고를 위해 SRP에 유지됩니다.

## AEM Analytics Cloud 서비스 구성 {#aem-analytics-cloud-service-configuration}

작성자 인스턴스의 표준 UI를 사용하여 Adobe Analytics를 AEM 커뮤니티 사이트와 통합하는 새 Analytics 통합을 만들려면:

* 전역 탐색에서 다음을 수행합니다.도구, **배포, 클라우드 서비스**
* 아래로 스크롤하여 **Adobe Analytics**
* 지금 **구성 또는 구성** **표시를 선택합니다.**

![chlimage_1-178](assets/chlimage_1-178.png)

### 구성 만들기 대화 상자 {#create-configuration-dialog}

* 사용 가능한 구성 옆에 **[있는]** + **아이콘을 선택하여** 새 구성 만들기

구성 만들기 대화 상자에서 입력할 값은 구성을 식별합니다.

![chlimage_1-179](assets/chlimage_1-179.png)

* **제목**(필수) 구성에 대한 표시 제목입니다.
예를 들어 역량 강화 *커뮤니티 분석을 입력합니다.*

* **이름**(선택 사항) 지정하지 않으면 이름이 기본적으로 제목에서 파생된 유효한 노드 이름으로 지정됩니다.
예를 들어 *커뮤니티에 입장합니다.*

* *템플릿*&#x200B;선택 `Adobe Analytics Configuration`

* **만들기**&#x200B;를 선택합니다

   * 구성 페이지를 실행하고 `Analytics Settings` 대화 상자 열기

### Analytics 설정 대화 상자 {#analytics-settings-dialog}

새 Analytics 구성을 처음 만들면 구성이 표시되고 Analytics 설정 항목에 대한 새 대화 상자가 표시됩니다. 이 대화 상자를 사용하려면 [전제 조건 계정 정보를](#prerequisites) 계정 담당자로부터 받아야 합니다.

![chlimage_1-180](assets/chlimage_1-180.png)

* **Adobe** Analytics 계정과 연결된 회사

* **사용자 이름** Analytics 계정을 관리할 수 있는 사용자의 로그인 사용자 이름

* **인증된**&#x200B;사용자의 로그인 암호

* **데이터 센터는**&#x200B;보고서 세트를 호스팅하는 Analytics 데이터 센터를 선택합니다

* **페이지에**&#x200B;추적 태그를 추가하지 않음(선택 취소됨)

* **AppMeasurement를**&#x200B;기본값으로 사용(선택 취소)

* **매일 밤 페이지 노출 횟수를 가져오지 않음(작성자)**&#x200B;은 기본값으로 남음(선택 취소됨)

* **페이지 노출 횟수를 매일 밤 가져오지 않음(게시)**&#x200B;은 기본값으로 남음(선택 취소됨)

설정을 저장하려면

* analytics **에 연결 선택**

   * 성공하지 못하면

      * 항목에 선행 공백이 포함되어 있지 않은지 확인
      * 다른 데이터 센터 사용
      * 계정 담당자에게 문의

* 확인 **선택**

![chlimage_1-181](assets/chlimage_1-181.png)

### 프레임워크 만들기 {#create-framework}

Adobe Analytics에 대한 기본 연결을 성공적으로 구성한 후에는 커뮤니티 사이트에 대한 프레임워크를 만들거나 편집해야 합니다. 이 프레임워크의 목적은 AEM(Communities Feature) 변수를 Analytics(보고서 세트) 변수에 매핑하는 것입니다.

* 사용 가능한 프레임워크 옆에 `[+]` 있는 **** 아이콘을 선택하여 새 프레임워크를 만듭니다.

![chlimage_1-182](assets/chlimage_1-182.png)

* **Title**(필수) 프레임워크의 표시 제목예를 들어, Enablement *Community Framework를 입력합니다*

* **이름**(선택 사항) 지정하지 않으면 이름이 기본적으로 제목에서 파생된 유효한 노드 이름으로 지정됩니다.
예를 들어 *커뮤니티에 입장합니다.*

* *템플릿*&#x200B;선택 `Adobe Analytics Framework`

* **만들기**&#x200B;를 선택합니다

Analytics 프레임워크를 만들면 구성에 대한 프레임워크가 열립니다.

## AEM Analytics 프레임워크 구성 {#aem-analytics-framework-configuration}

프레임워크의 목적은 AEM 변수를 Analytics 변수(eVar 및 이벤트)에 매핑하는 것입니다. 매핑에 사용할 수 있는 Analytics 변수는 보고서 세트에 [정의됩니다](#adobe-analytics-report-suite-for-video-reporting).

![chlimage_1-183](assets/chlimage_1-183.png)

### 보고서 세트 선택 {#select-report-suite}

비디오 보고를 위해 설정된 보고서 세트를 선택합니다.

보고서 세트가 아직 만들어지지 않았거나 제대로 설정되지 않은 경우 이전 섹션을 참조하십시오.비디오[보고를 위한 Adobe Analytics 보고서 세트](#adobe-analytics-report-suite-for-video-reporting)

사이드 킥은 필요하지 않으며 보고서 세트 설정에 대한 액세스를 방해하지 않도록 최소화할 수 있습니다.

#### &#39;항목 추가&#39;를 선택하기 전과 후 보고서 세트 대화 상자 {#report-suites-dialog-before-and-after-selecting-add-item}

![chlimage_1-184](assets/chlimage_1-184.png)

1. 항목 **+ 추가를 선택합니다.**
두 개의 드롭다운 상자가 나타납니다.

1. 회사 `Report suite.`계정과 연결된 보고서 세트를 선택할 수 있습니다.

1. 대화 상자가 열리면 **Yes **를 선택합니다.

   ```
   Load default server settings?
    Do you want to load the default server settings and overwrite current values in the Server section?
   ```

1. 선택 `Run Mode`
1. Select **publish**

![chlimage_1-185](assets/chlimage_1-185.png)

Analytics 클라우드 서비스 및 프레임워크가 이제 완료되었습니다. 매핑은 이 Analytics 서비스를 활성화한 상태로 커뮤니티 사이트를 만든 후에 정의됩니다.

## 커뮤니티 사이트에 대한 분석 활성화 {#enable-analytics-for-a-community-site}

### 새 커뮤니티 사이트 활성화 {#enable-for-new-community-site}

새 커뮤니티 사이트를 [만드는 동안 Analytics 클라우드 서비스를 추가하려면](/help/communities/sites-console.md):

* 3단계의 ANALYTICS 탭에서 [다음을 수행합니다](/help/communities/sites-console.md#analytics).
   * 분석 **활성화** 확인란을 선택합니다.
   * 드롭다운 상자에서 프레임워크를 선택합니다.

* 원할 경우, Analytics 프레임워크 구성으로 돌아가 변수 매핑을 조정합니다.

### 기존 커뮤니티 사이트 활성화 {#enable-for-existing-community-site}

Analytics 클라우드 서비스를 [기존 커뮤니티 사이트에](/help/communities/sites-console.md#modifying-site-properties)추가하려면:

* 커뮤니티, **사이트 콘솔로** 이동합니다.
* 커뮤니티 사이트의 사이트 편집 아이콘을 선택합니다.
* 설정을 선택합니다.
* 분석 섹션에서 다음을 수행합니다.
   * Analytics **활성화** 확인란을 선택합니다.
   * 드롭다운 상자에서 프레임워크를 선택합니다.

* 원할 경우, Analytics 프레임워크 구성으로 돌아가 변수 매핑을 조정합니다.

### 사용자 지정 사이트 활성화 {#enable-for-customized-sites}

Analytics 추적 및 가져오기가 커뮤니티 사이트에 대해 제대로 작동하려면 `scf-js-site-title` 클래스와 href 특성이 있는 페이지 요소가 있어야 합니다. 이러한 요소는 커뮤니티 사이트에 대한 수정되지 않은 `sitepage.hbs` 스크립트와 같이 페이지에 하나만 있어야 합니다. 의 값이 `siteUrl` 추출되어 *사이트 경로로* Adobe Analytics로 전송됩니다.

```xml
# present in default sitepage.hbs
# only one scf-js-site-title class should be included
# this example sets it to be hidden as it serves no visual purpose
<div
    class="navbar-brand scf-js-site-title"
    href="{{siteUrl}}.html"
    style="visibility: hidden;"
>
</div>
```

스크립트를 오버레이하는 **사용자 지정 커뮤니티 사이트의** 경우 `sitepage.hbs` 요소가 있는지 확인합니다. 이 `siteUrl`변수는 클라이언트에 제공하기 전에 서버에서 렌더링될 때 설정됩니다.

커뮤니티 구성 요소를 포함하지만 **사이트 만들기 마법사로** 만들지 않은 일반 AEM 사이트의 [](/help/communities/sites-console.md)경우 요소를 추가해야 합니다. href 값은 사이트의 경로여야 합니다. 예를 들어 사이트 경로가 인 경우 `/content/my/company/en`다음을 사용합니다.

```xml
<div
    class="navbar-brand scf-js-site-title"
    href="/content/my/company/en.html"
    style="visibility: hidden;"
>
</div>
```

## Analytics for Communities 기능 {#analytics-for-communities-features}

Analytics는 여러 커뮤니티 기능에 자동으로 사용됩니다.

작성 환경의 OSGi [구성은](/help/sites-deploying/configuring-osgi.md)Analytics용으로 구현된 구성 요소 목록을 `AEM Communities Analytics Component Configuration`제공합니다. 변수의 자동 매핑은 나열된 구성 요소에 의해 결정됩니다.

Analytics에 대해 구현된 새 사용자 지정 구성 요소가 만들어진 경우 이 구성 요소 목록에 추가해야 합니다.

### 구성 요소 구성 {#component-configuration}

![chlimage_1-186](assets/chlimage_1-186.png)

>[!NOTE]
>
>저널 구성 요소는 블로그 기능을 구현하는 데 사용됩니다.

### AEM 변수에 Analytics 매핑 {#mapped-analytics-to-aem-variables}

Analytics가 활성화되고 클라우드 구성 프레임워크가 선택된 상태에서 커뮤니티 사이트가 저장되면 AEM 변수는 각각 evar1 및 event1로 시작하여 Analytics eVar 및 이벤트에 자동으로 매핑되고 1로 증가합니다.

evar1 - evar11 및 event1에서 event7까지의 변수 중 하나를 매핑한 기존 보고서 세트를 사용하는 경우 AEM 변수를 [다시 매핑하고](#modifying-analytics-variable-mapping) 원래 매핑을 복원해야 합니다.

다음은 [시작하기 자습서](/help/communities/getting-started-enablement.md)다음에 나오는 기본 매핑의 예입니다.

![chlimage_1-187](assets/chlimage_1-187.png)

#### 각 이벤트와 함께 전송된 eVar 맵 {#map-of-evars-sent-with-each-event}

<table>
 <tbody>
  <tr>
   <td><strong> </strong></td>
   <td><strong>지원<br /> 리소스<br /> 유형</strong></td>
   <td><strong>사이트<br /> 제목</strong></td>
   <td><strong>함수<br /> 유형</strong></td>
   <td><strong>그룹<br /> 제목</strong></td>
   <td><strong>Group<br /> Path</strong></td>
   <td><strong>UGC<br /> 유형</strong></td>
   <td><strong>UGC<br /> 제목</strong></td>
   <td><strong>사용자<br /> (구성원)</strong></td>
   <td><strong>UGC<br /> 경로</strong></td>
   <td><strong>사이트<br /> 경로</strong></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><strong>eVar1</strong></td>
   <td><strong>eVar2</strong></td>
   <td><strong>eVar3</strong></td>
   <td><strong>eVar4</strong></td>
   <td><strong>eVar5</strong></td>
   <td><strong>eVar6</strong></td>
   <td><strong>eVar7</strong></td>
   <td><strong>eVar8</strong></td>
   <td><strong>eVar9</strong></td>
   <td><strong>eVar10</strong></td>
  </tr>
  <tr>
   <td><strong>event1<br /> 리소스 재생</strong></td>
   <td><em>가.</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>자.</em></td>
   <td><em>-</em></td>
  </tr>
  <tr>
   <td><strong>event2<br /> SCFView</strong></td>
   <td><em>가.</em></td>
   <td><em>나.</em></td>
   <td><em>다.</em></td>
   <td><em>(d)</em></td>
   <td><em>(e)</em></td>
   <td><em>(f)</em></td>
   <td><em>(g)</em></td>
   <td><em>(h)</em></td>
   <td><em>자.</em></td>
   <td><em>차.</em></td>
  </tr>
  <tr>
   <td><strong>event3<br /> SCFCreate(Post)</strong></td>
   <td><em>-</em></td>
   <td><em>나.</em></td>
   <td><em>다.</em></td>
   <td><em>(d)</em></td>
   <td><em>(e)</em></td>
   <td><em>(f)</em></td>
   <td><em>(g)</em></td>
   <td><em>(h)</em></td>
   <td><em>자.</em></td>
   <td><em>차.</em></td>
  </tr>
  <tr>
   <td><strong>event4<br /> SCFFollow</strong></td>
   <td><em>-</em></td>
   <td><em>나.</em></td>
   <td><em>다.</em></td>
   <td><em>(d)</em></td>
   <td><em>(e)</em></td>
   <td><em>(f)</em></td>
   <td><em>(g)</em></td>
   <td><em>(h)</em></td>
   <td><em>자.</em></td>
   <td><em>차.</em></td>
  </tr>
  <tr>
   <td><strong>event5<br /> SCFVoteUp</strong></td>
   <td><em>-</em></td>
   <td><em>나.</em></td>
   <td><em>다.</em></td>
   <td><em>(d)</em></td>
   <td><em>(e)</em></td>
   <td><em>(f)</em></td>
   <td><em>(g)</em></td>
   <td><em>(h)</em></td>
   <td><em>자.</em></td>
   <td><em>차.</em></td>
  </tr>
  <tr>
   <td><strong>event6<br /> SCFVoteDown</strong></td>
   <td><em>-</em></td>
   <td><em>나.</em></td>
   <td><em>다.</em></td>
   <td><em>(d)</em></td>
   <td><em>(e)</em></td>
   <td><em>(f)</em></td>
   <td><em>(g)</em></td>
   <td><em>(h)</em></td>
   <td><em>자.</em></td>
   <td><em>차.</em></td>
  </tr>
  <tr>
   <td><strong>event7<br /> SCFRate</strong></td>
   <td><em>-</em></td>
   <td><em>나.</em></td>
   <td><em>다.</em></td>
   <td><em>(d)</em></td>
   <td><em>(e)</em></td>
   <td><em>(f)</em></td>
   <td><em>(g)</em></td>
   <td><em>(h)</em></td>
   <td><em>자.</em></td>
   <td><em>차.</em></td>
  </tr>
 </tbody>
</table>

**eVar 값에 대한 예:**

* *(a)[MIME 유형](https://www.iana.org/assignments/media-types)*:video/mp4
* *(b)[커뮤니티 사이트 제목](/help/communities/sites-console.md#step13asitetemplate)*:Geometrixx Communities
* *(c)[커뮤니티 기능 이름](/help/communities/functions.md)*:포럼
* *(d)[커뮤니티 그룹 이름](/help/communities/creating-groups.md#creating-a-new-group)*:하이킹
* *(e) 커뮤니티 그룹 콘텐츠의*&#x200B;경로:/content/sites/communities/en/groups/hiking
* *(f)[UGC 구성 요소 리소스유형](/help/communities/essentials.md)*:social/forum/components/hbs/topic
* *(g) UGC 구성 요소 제목*:하이킹 주제
* *(h) 로그인(authorizableId)*:aaron.mcdonald@mailinator.com
* *(i) UGC에 대한 SRP 경로*:/content/usergenerated/asi/.../forum/jmtz-topic3또는 *팔로우할*&#x200B;구성 요소의 경로:/content/sites/communities/en/jcr:content/content/primary/forum

* *(j) 커뮤니티 사이트 컨텐츠의*&#x200B;경로:/content/sites/community/en

### Analytics 변수 매핑 수정 {#modifying-analytics-variable-mapping}

Analytics가 커뮤니티 사이트에 대해 활성화된 후 프레임워크 구성에서 Analytics eVar 및 이벤트를 AEM 변수에 매핑하는 것이 표시됩니다.

Analytics가 활성화되고 커뮤니티 사이트가 게시되기 전에 왼쪽 레일에서 원하는 Analytics evar 또는 이벤트를 드래그하여 매핑 테이블의 관련 행으로 놓아 프레임워크에서 매핑을 변경할 수 있습니다.

중복 매핑을 방지하려면, 마우스를 행에서 해당 이벤트나 이벤트를 제거하고 Analytics 변수 요소의 오른쪽에 나타나는 &quot;X&quot;를 선택하여 대체된 Analytics evar 또는 이벤트를 제거해야 합니다.

Communities eVar 및 이벤트가 보고서 세트에 이미 존재했던 매핑을 덮어쓰는 경우 데이터 손실을 방지하려면 Communities 기능에 대한 AEM 변수를 다른 Analytics eVar 또는 이벤트에 할당하고 원래 매핑을 복원합니다.

>[!CAUTION]
>
>Analytics를 사용하여 커뮤니티 사이트를 [게시하기](#publishing-the-community-site) 전에 다시 매핑해야 합니다. 그렇지 않으면 데이터가 손실될 위험이 있습니다.

#### 1단계 예:Analytics evar14를 매핑 테이블로 끌기 {#example-step-dragging-analytics-evar-into-mapping-table}

![chlimage_1-188](assets/chlimage_1-188.png)

#### 2단계 예:바뀐 evar11을 제거하려면 &#39;x&#39; 선택 {#example-step-selecting-x-to-remove-replaced-evar}

![chlimage_1-189](assets/chlimage_1-189.png)

#### 3단계 예:Analytics evar14에 다시 매핑된 AEM var eventdata.siteId {#example-step-aem-var-eventdata-siteid-remapped-to-analytics-evar}

![chlimage_1-190](assets/chlimage_1-190.png)

## 커뮤니티 사이트 게시 {#publishing-the-community-site}

### AEM 변수 매핑에 대한 분석 확인 {#verify-analytics-to-aem-variable-mapping}

Analytics 클라우드 서비스 및 프레임워크를 게시하는 커뮤니티 사이트를 게시하기 전에 변수 매핑을 확인하는 것이 좋습니다.

섹션 참조:

* [AEM 변수에 Analytics 매핑](#mapped-analytics-to-aem-variables)
* [Analytics 변수 매핑 수정](#modifying-analytics-variable-mapping)

>[!CAUTION]
>
>**If using a existing report suite that already uses variables within**
>
>* **`evar1`** through **`evar11`**
   >
   >
* **`event1`** through **`event7`**
>
>
**그런 다음 커뮤니티 사이트를 게시하기 전에** 기존 매핑을 복원하고 자동으로 매핑되는(커뮤니티 사이트에 대해 Analytics가 활성화된 경우) 커뮤니티 AEM 변수를 다른 Analytics 변수로 이동하는 것이 중요합니다. 이 다시 매핑은 모든 커뮤니티 구성 요소에서 일관되어야 합니다.
>
>이렇게 하지 않으면 복구할 수 없는 데이터 손실이 발생할 수 있습니다.

### 기본 게시자 {#primary-publisher}

선택한 배포가 [게시 팜인](/help/communities/topologies.md#tarmk-publish-farm)경우 SRP에 쓸 보고서 데이터를 위해 Adobe Analytics를 폴링하는 기본 게시자로 AEM 게시 인스턴스 하나가 식별되어야 [합니다](/help/communities/working-with-srp.md).

기본적으로 OSGi `AEM Communities Publisher Configuration` 구성은 게시 인스턴스를 기본 게시자로 식별합니다. 이렇게 하면 게시 팜의 모든 게시 인스턴스가 기본으로 자체적으로 식별됩니다.

따라서 모든 보조 게시 인스턴스의 구성을 편집하여 기본 게시자 **확인란을 선택 취소해야** 합니다.

특정 지침은 커뮤니티 배포의 기본 게시자 섹션을 [참조하십시오](/help/communities/deploy-communities.md#primary-publisher).

>[!CAUTION]
>
>주 게시자를 구성하여 여러 게시 인스턴스의 폴링을 방지해야 합니다.

### 암호화 키 복제 {#replicate-the-crypto-key}

Adobe Analytics 자격 증명은 암호화됩니다. 작성자와 발행자 간에 암호화된 분석 자격 증명을 복제하거나 전송하기 위해 모든 AEM 인스턴스는 동일한 마스터 암호화 키를 공유해야 합니다.

이렇게 하려면 암호화 키 [복제의 지침을 따르십시오](/help/communities/deploy-communities.md#replicate-the-crypto-key).

### 커뮤니티 사이트 및 Analytics 클라우드 서비스 게시 {#publish-community-site-and-analytics-cloud-service}

Analytics 클라우드 서비스가 커뮤니티 사이트에 대해 활성화되고 필요한 경우 AEM 변수에 대한 Analytics [매핑이 조정되면](#mapped-analytics-to-aem-variables), 커뮤니티 사이트를 [](/help/communities/sites-console.md#publishing-the-site)게시하여 게시 환경에 구성을 복제해야 합니다.

## Analytics에서 보고서 얻기 {#obtaining-reports-from-analytics}

### 보고서 관리 {#report-management}

작성자 및 기본 게시자의 [OSGi 구성은](/help/sites-deploying/configuring-osgi.md)Analytics `AEM Communities Analytics Report Management`를 쿼리하는 데 사용됩니다.

작성자의 경우 쿼리는 실시간 보고서용입니다.

기본 게시자에서 쿼리는 보고서 가져오기의 분석 데이터 가져오기 준비에 대한 정보를 제공하는 데 사용됩니다.

쿼리 간격의 기본값은 10초입니다.

### 보고서 가져오기 {#report-importer}

Analytics가 활성화된 커뮤니티 사이트가 게시되면 기본 게시자의 [OSGi 구성이](/help/sites-deploying/configuring-osgi.md)CRXDE에 개별적으로 구성되지 않은 구성에 대한 기본 폴링 간격을 `AEM Communities Analytics Report Importer`설정하도록 구성할 수 있습니다.

폴링 간격은 Adobe Analytics에 대한 SRP로 가져오고 저장할 데이터의 요청 빈도를 [제어합니다](/help/communities/working-with-srp.md).

데이터가 &quot;빅데이터&quot;로 분류될 수 있는 경우 설문 조사가 빈번하면 커뮤니티 사이트에 큰 부하가 발생할 수 있습니다.

기본 폴링 가져오기 **간격이** 12시간으로 설정되어 있습니다.

![chlimage_1-191](assets/chlimage_1-191.png)

### 구성 요소 보고서 사용자 지정 {#component-report-customization}

현재, 추적할 지표를 사용자 정의하기 위해 해당 지표에 대한 보고서를 생성할 기간을 정의하는 노드가 저장소에 생성됩니다.

포럼 주제는 현재 이 사용자 지정 예제의 유일한 예입니다.

* 기본 게시자에서 관리 권한으로 로그인합니다.
* CRXDE [Lite로 이동합니다](/help/sites-developing/developing-with-crxde-lite.md). 예: https://localhost:4503/crx/de [를 참조하십시오](https://localhost:4503/crx/de).

* 언어 루트의 jcr:content 노드 아래에 있습니다(예: Analytics 보고를 위해 구성된 구성 요소로 `/content/sites/engage/en/jcr:content),`이동).
예, **`analytics/reportConfigs/social_forum_components_hbs_topic`**

* 생성된 기간을 확인합니다.

   * `last30Days`
   * `last90Days`
   * `thisYear`

* Notice the `total`node.

   * **`interval`**속성을 수정하면 보고서 가져오기 간격이 무시됩니다.
   * 값은 초 단위이며 4시간(14400초)으로 설정됩니다.

![chlimage_1-192](assets/chlimage_1-192.png)

## Analytics에서 사용자 데이터 관리 {#manage-user-data-in-analytics}

Adobe Analytics는 사용자 데이터에 액세스, 내보내기 및 삭제할 수 있는 API를 제공합니다. 자세한 내용은 액세스 제출 [및 요청 삭제를 참조하십시오](https://marketing.adobe.com/resources/help/en_US/analytics/gdpr/gdpr_submit_access_delete.html).

## 리소스 {#resources}

* Adobe Marketing Cloud:Analytics [도움말 및 참조](https://marketing.adobe.com/resources/help/en_US/reference/)
* AEM:Adobe [Analytics와 통합](/help/sites-administering/adobeanalytics.md)
* AEM:외부 [제공업체를 통한 분석](/help/sites-administering/external-providers.md)

