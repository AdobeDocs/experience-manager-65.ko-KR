---
title: Adobe Analytics에 대한 링크 추적 구성
description: SiteCatalyst에 대한 링크 추적을 구성하는 방법에 대해 알아봅니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: 9fa3e531-11b3-4b8d-a87c-a08faf06f5b7
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1615'
ht-degree: 0%

---


# Adobe Analytics에 대한 링크 추적 구성{#configuring-link-tracking-for-adobe-analytics}

사용자가 웹 사이트의 페이지에서 링크를 클릭하면 Adobe Analytics에서 관련 정보를 캡처할 수 있습니다. 예를 들어, 링크 추적을 사용하여 사용자가 사이트와 상호 작용하는 방법을 배우고, 파일 다운로드를 추적하고, 종료 링크를 추적합니다.

## Adobe Analytics 프레임워크에 대한 링크 추적 구성 {#configuring-link-tracking-for-an-adobe-analytics-framework}

1. 사용 **탐색**, 통과 **배포**, **Cloud Service** (으)로 **Adobe Analytics** 섹션.

1. 사용 **구성 표시**&#x200B;필요한 Adobe Analytics 프레임워크를 엽니다.
1. 확장 **링크 추적 구성** 섹션 및 필요에 따라 구성(이 페이지에서는 자세한 내용을 제공합니다.)

   ![Analytics 프레임워크](assets/aa-08.png)

## 파일 다운로드 추적 {#tracking-file-downloads}

연관된 페이지에서 다운로드한 파일이 Adobe Analytics의 다운로드로 자동으로 추적되도록 Adobe Analytics 프레임워크를 구성합니다. 다운로드 추적을 활성화하면 지정한 파일 유형만 추적됩니다.

기본적으로 다음 파일 형식의 다운로드가 추적됩니다.

* exe
* zip
* wav
* mp3
* mov
* 갤런당
* avi
* wmv
* 문서
* pdf
* xls

따라서 예를 들어 PDF 파일에 대해 다운로드 추적을 활성화한 상태에서 사용자가 PDF 파일에 대한 링크를 클릭할 때마다 PDF의 다운로드가 추적됩니다.

프레임워크의 다운로드 추적 속성은 `analytics.sitecatalyst.js` 페이지에 대해 생성된 파일입니다. 다음 코드 샘플은 기본 다운로드 추적 구성을 나타냅니다.

```
s.trackDownloadLinks= true;
s.linkDownloadFileTypes= 'exe,zip,wav,mp3,mov,mpg,avi,wmv,doc,pdf,xls';
```

Adobe Analytics 프레임워크에 대한 다운로드 추적을 활성화하려면 다음을 수행하십시오.

1. [Adobe Analytics 프레임워크를 열고 링크 추적 구성 섹션을 확장합니다.](#configuring-link-tracking-for-an-adobe-analytics-framework).
1. 사용 **다운로드 추적**.
1. 다음에서 **다운로드 파일 유형** 상자에 추적할 파일 유형의 파일 확장자를 입력합니다.

## 외부 링크 추적 {#tracking-external-links}

페이지에서 외부 링크(종료 링크) 클릭을 추적할 수 있습니다.

Adobe Analytics 프레임워크에 대한 외부 링크를 추적하려면 다음 작업을 수행하십시오.

1. [Adobe Analytics 프레임워크를 열고 를 확장합니다. **링크 추적 구성** 섹션](#configuring-link-tracking-for-an-adobe-analytics-framework).
1. 요구 사항에 따라 다음 속성을 구성합니다.

외부 링크를 클릭할 때 추적할 속성:

* **외부 추적**
외부 링크 추적을 활성화합니다.

* **외부 필터**
(선택 사항) 링크 대상의 외부 URL과 일치하는 필터를 정의합니다. 링크 대상이 필터와 일치하면 링크가 추적됩니다. 외부 필터는 페이지에서 일부 외부 링크만 추적하는 데 유용합니다.

  추적할 외부 링크를 지정하려면 링크 대상의 URL의 전체 또는 일부를 입력합니다. 여러 필터는 쉼표로 구분하십시오. 문자열 리터럴을 작은 따옴표로 묶습니다. 값 없음(기본값) `''`를 두 개의 작은 따옴표로 묶으면 모든 외부 링크가 추적됩니다.

* **내부 필터**
내부 링크의 URL과 일치하는 필터를 정의합니다. 링크가 이 필터와 일치하는 URL을 타겟팅하면 링크가 추적되지 않습니다. 기본값은 현재 창 주소에 대한 URL의 호스트 이름을 반환하는 javascript 명령입니다.

  추적되지 않는 내부 링크를 지정하려면 링크 대상의 내부 URL의 전부 또는 일부를 입력합니다. 여러 필터는 쉼표로 구분하십시오. 문자열 리터럴을 작은 따옴표로 묶습니다.

  기본값은 입니다. `'javascript:,'+window.location.hostname`

* **쿼리 문자열 남기기**
내부 및 외부 필터와의 일치 항목을 평가할 때 URL 매개 변수를 포함합니다.

  외부 및 내부 필터에 대해 링크 대상 URL을 평가할 때 URL 매개 변수를 포함하려면 활성화합니다.

외부 링크 추적 속성은 `analytics.sitecatalyst.js` 페이지에 대해 생성된 파일입니다. 다음 예제 코드는 다음 구성으로 외부 링크 추적을 활성화하는 프레임워크와 연결된 페이지에 대해 생성됩니다.

* 외부 필터: `'google.com'`
* 내부 필터는 기본값입니다. `'javascript:,'+window.location.hostname`
* 필터에 대해 링크 대상을 평가할 때 쿼리 문자열이 포함되지 않습니다.

```
s.trackExternalLinks= false;
s.linkExternalFilters= 'google.com';
s.linkInternalFilters= 'javascript:,'+window.location.hostname;
s.linkLeaveQueryString= false;
```

## 링크 클릭으로 변수 데이터 보내기 {#sending-variable-data-with-link-clicks}

사용자가 링크를 클릭할 때 이벤트 및 변수 데이터를 Adobe Analytics으로 보내도록 AEM을 구성할 수 있습니다. 다음 **링크 추적 구성** 속성을 사용하면 링크 클릭이 발생할 때 추적할 Adobe Analytics 이벤트 및 변수를 지정할 수 있습니다.

프레임워크 매핑은 이벤트 및 변수 값을 결정합니다. 링크를 클릭할 때 추적하려는 데이터를 저장하는 컨텐츠 구성 요소의 변수에 Adobe Analytics 변수를 매핑할 수 있습니다.

링크 클릭으로 변수 데이터를 보내려면 다음을 수행하십시오.

1. [Adobe Analytics 프레임워크를 열고 링크 추적 구성 섹션을 확장합니다.](#configuring-link-tracking-for-an-adobe-analytics-framework).
1. 요구 사항에 따라 다음 속성을 구성합니다.

링크 클릭으로 변수 데이터를 전송하기 위한 속성:

* **링크 추적 이벤트**
링크 클릭 수를 계산하는 데 사용할 Adobe Analytics 이벤트 변수를 입력합니다.

  여러 변수 이름은 쉼표로 구분하십시오.

  기본값 `None` 은(는) 이벤트 추적을 발생시키지 않습니다.

* **링크 추적 변수**
링크를 클릭할 때 Adobe Analytics으로 보낼 Adobe Analytics 변수를 입력합니다. 여러 변수 이름은 쉼표로 구분하십시오.

  기본값 `None` 은(는) 변수 데이터를 전송하지 않습니다.

전송할 이벤트 및 변수를 지정하면 구성이 `analytics.sitecatalyst.js` 페이지에 대해 생성된 파일입니다. 다음 예제 코드는 프레임워크가 `event10` 이벤트 및 `prop4` 속성:

```
s.linkTrackEvents= 'event10';
s.linkTrackVars= 'prop4';
```

## 링크 추적 구성 예 {#example-link-tracking-configuration}

Adobe Analytics 통합의 링크 추적 동작을 살펴보려면 다음 절차를 수행하십시오. 다음 절차에 따라 다음 결과가 표시됩니다. [Adobe Marketing Cloud 디버거](https://experienceleague.adobe.com/docs/debugger/using/experience-cloud-debugger.html).

### 일반 구성 {#general-configuration}

다음 예에서는 추적 및 디버거의 컨텍스트에서 매핑이 작동하는 방식을 보여 줍니다.

1. 웹 페이지와 연결된 프레임워크를 엽니다.
1. 드래그 **페이지** 구성 요소를 프레임워크의 매핑 영역에 추가합니다. 다음 **페이지** 구성 요소가 다음에 속함 **일반** Sidekick의 구성 요소 그룹

   >[!NOTE]
   >
   >실제 시나리오에서 사용해야 하는 구성 요소는 (전혀 없는 경우)에서 상속된 구성 요소에 따라 다릅니다.
   >
   >그렇지 않은 경우 자체 구성 요소가 여기에 노출되어 있어야 합니다(페이지 구성 요소에서 분석 하위 노드를 정의함으로써).

   왼쪽 사이드 패널에서 Analytics(SiteCatalyst) 변수를 끌어 다음 표에 따라 매핑을 구성합니다.

<table>
 <tbody>
  <tr>
   <th>CQ 변수<br /> </th>
   <th>변수 브라우저의 항목<br /> </th>
   <th>Adobe Analytics 변수</th>
  </tr>
  <tr>
   <td>pagedata.title</td>
   <td>사용자 지정 eVar 1(eVar1)</td>
   <td>eVar</td>
  </tr>
  <tr>
   <td>eventdata.events.pageView</td>
   <td>사용자 지정 1 (event1)</td>
   <td>event1</td>
  </tr>
 </tbody>
</table>

1. 검색 구성 요소를 프레임워크의 매핑 영역으로 드래그합니다. 검색 구성 요소는 Sidekick의 일반 구성 요소 그룹에 속합니다. 왼쪽 사이드 패널에서 Analytics(SiteCatalyst) 변수를 끌어 다음 표에 따라 매핑을 구성합니다.

<table>
 <tbody>
  <tr>
   <th>CQ 변수<br /> </th>
   <th>변수 브라우저의 항목</th>
   <th>Adobe Analytics 변수</th>
  </tr>
  <tr>
   <td>eventdata.keyword</td>
   <td>사용자 지정 eVar 2 (eVar2)</td>
   <td>eVar</td>
  </tr>
  <tr>
   <td>eventdata.results</td>
   <td>사용자 지정 eVar 3(eVar 3)</td>
   <td>eVar</td>
  </tr>
  <tr>
   <td>eventdata.events.search</td>
   <td>사용자 지정 2 (event2)</td>
   <td>event2</td>
  </tr>
 </tbody>
</table>

### 외부 링크 추적 구성 {#configure-external-link-tracking}

1. 프레임워크에서 **링크 추적 구성** 영역입니다.
1. 선택 취소 **다운로드 추적**.

1. 선택 **외부 추적**.
1. 선택 취소 **쿼리 문자열 남기기**.
1. 다음에 대한 다음 값 사용 **외부 필터** 외부 URL로 식별할 목록:

   `'yahoo.com'`

1. 에 다음 값 추가 **링크 추적 이벤트** 필드:

   ```
       event1,event2
   ```

1. 에 다음 값 추가 **링크 추적 변수** 필드:

   ```
       eVar1,eVar2
   ```

1. 프레임워크와 연결된 페이지에서 **텍스트** 구성 요소. 내부 **텍스트** 구성 요소에서 다음 주소를 가리키는 하이퍼링크를 추가합니다.

   `https://search.yahoo.com/?p=this`

1. 다음으로 전환 **미리 보기 모드** 링크를 클릭합니다.

Adobe Marketing Cloud Debugger에서 볼 때 수행된 호출은 다음과 같이 표시됩니다.

![Adobe Marketing Cloud 디버거](assets/aa-leavequerysearch-blank.png)

>[!NOTE]
>
>URL에 쿼리 문자열이 포함되어 있지 않습니다. `?p=this`

### URL 매개 변수 포함 {#include-the-url-parameter}

1. 프레임워크에서 를 확장합니다. **링크 추적 구성** 영역입니다.
1. 사용 **쿼리 문자열 남기기**.
1. 페이지 미리보기를 다시 로드하고 링크를 클릭합니다.

Adobe Marketing Cloud Debugger에 표시되는 호출 세부 사항은 다음 예와 유사합니다.

![Adobe Marketing Cloud Debugger 다시 시작](assets/aa-leavequerysearch-active.png)

>[!NOTE]
>
>이번에는 URL에 쿼리 문자열이 포함되어 있습니다. `?p=this`

## 임시 링크 추적 {#ad-hoc-link-tracking}

임시 링크 추적을 사용하면 콘텐츠 작성자가 구성 요소에 대한 링크 추적을 구성할 수 있습니다. 구성 요소의 구성은 **링크 추적 구성** 프레임워크와 연결된 페이지에서 **텍스트** URL의 링크 추적을 위해 구성 요소를 구성할 수 있습니다.

임시 링크 추적을 사용하면 다운로드 링크, 외부 링크, 이벤트 및 변수 데이터를 추적할 수 있습니다.

임시 링크 추적을 활성화하려면 다음 작업을 수행해야 합니다.

* [을(를) 포함하는 페이지 연결 **텍스트** 프레임워크가 포함된 구성 요소](/help/sites-administering/adobeanalytics-connect.md#associating-a-page-with-a-adobe-analytics-framework).
* [임시 링크 추적을 활성화하도록 Adobe Analytics 프레임워크 구성](#enabling-ad-hoc-link-tracking).
* [텍스트 구성 요소에 대한 링크 추적 구성](#configuring-link-tracking-for-a-text-component).

### 임시 링크 추적 활성화 {#enabling-ad-hoc-link-tracking}

임시 링크 추적을 활성화하도록 Adobe Analytics 프레임워크를 구성합니다.

1. Adobe Analytics 프레임워크를 열고 를 확장합니다. **링크 추적 구성** 섹션.

1. 사용 **임시 링크 추적**.

   >[!NOTE]
   >
   >모든 사용자 유형이 이 확인란에 액세스할 수 있는 것은 아닙니다. 액세스하려면 사이트 관리자에게 문의하십시오.

>[!NOTE]
>
>XSS Antisamy 구성이 이제 경로 아래의 SLING에 있습니다. **/libs/sling/xss.config.xml** 임시 연결이 작동하려면 및에 다음 규칙을 추가해야 합니다.

#### 앵커 태그 규칙 확장 {#anchor-tag-rule-extension}

```xml
<attribute name="onclick">
    <literal-list>
        <literal value="CQ_Analytics.Sitecatalyst.customTrack(this)"/>
    </literal-list>
</attribute>
<attribute name="adhocenable">
    <literal-list>
        <literal value="true"/>
        <literal value="false"/>
    </literal-list>
</attribute>
<attribute name="adhocevents">
    <regexp-list>
        <regexp name="anything"/>
    </regexp-list>
</attribute>
<attribute name="adhocevars">
    <regexp-list>
        <regexp name="anything"/>
    </regexp-list>
</attribute>
```

### 텍스트 구성 요소에 대한 링크 추적 구성 {#configuring-link-tracking-for-a-text-component}

다음에 대한 임시 링크 추적을 구성하기 전에 **텍스트** 구성 요소 자체, 다음 구성이 이미 구현되었을 것입니다.

* 다음 [Adobe Analytics 프레임워크는 임시 링크 추적을 활성화하도록 구성되어 있습니다.](#enabling-ad-hoc-link-tracking).
* 다음 [이 포함된 페이지 **텍스트** 구성 요소가 프레임워크와 연계되어 있습니다.](/help/sites-administering/adobeanalytics-connect.md#associating-a-page-with-a-adobe-analytics-framework).

다음 절차에 따라 다음에 대한 링크 추적을 구성합니다 **텍스트** 구성 요소:

1. 페이지를 편집 모드로 열고 **텍스트** 구성 요소.

1. 하이퍼텍스트로 사용할 텍스트를 선택하고 하이퍼링크 단추를 클릭합니다.

   ![링크 아이콘](do-not-localize/chlimage_1.png)

1. 링크 대상 상자에 대상 URL을 추가한 다음 링크 추적 영역을 확장합니다.

   >[!NOTE]
   >
   >사용자 지정 링크 추적은 링크/링크 해제 작업(Analytics 아이콘) 옆에 별도의 작업으로 표시됩니다.
   >
   >RTE에서 유효한 링크를 선택한 경우에만 활성화됩니다.

   ![링크 추적 활성화](assets/aa-17.png)

1. 사용 **사용자 지정 링크 추적** Adobe Analytics 프레임워크의 링크 추적 구성을 재정의하고 현재 링크에 대한 링크 추적을 활성화합니다.

1. Adobe Analytics (선택 사항) 링크 클릭으로 이벤트를 추적하려면 **Adobe Analytics 변수 포함** 필드. 여러 이벤트 이름(예: 쉼표)은 쉼표로 구분하십시오

   `event1, event22`

1. Adobe Analytics (선택 사항) 링크 클릭으로 변수 데이터를 추적하려면 **Adobe Analytics 변수 포함** 필드. 다음 형식 중 하나를 사용합니다.

   * *`<Variable-name>`*: *`<Dynamic Value>`*
   * *`<Variable-name>`*: *`'CONSTANT'`*

   다음 예제는 각 형식을 보여 줍니다.

   * `eVar10:pagedata.title`
   * `prop1: 'Aubergine'`

   여러 값은 쉼표로 구분하십시오.

1. 선택 **확인**.
