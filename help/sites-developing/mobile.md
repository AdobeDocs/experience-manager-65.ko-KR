---
title: 모바일 장치용 사이트 만들기
description: 모바일 사이트를 만드는 것은 템플릿 및 구성 요소를 만드는 작업도 포함하므로 표준 사이트를 만드는 것과 비슷합니다
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
docset: aem65
legacypath: /content/docs/en/aem/6-0/develop/mobile/mobile
exl-id: 21b2037a-685a-441d-aecd-865884253e03
source-git-commit: 69346a710708ee659ee97e9fdc193c8ea2658fe6
workflow-type: tm+mt
source-wordcount: '3787'
ht-degree: 1%

---

# 모바일 장치용 사이트 만들기{#creating-sites-for-mobile-devices}

>[!NOTE]
>
>Adobe 단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: React)이 필요한 프로젝트에는 SPA Editor를 사용하는 것이 좋습니다. [자세히 알아보기](/help/sites-developing/spa-overview.md).

모바일 사이트를 만드는 것은 템플릿 및 구성 요소를 만드는 작업도 포함하므로 표준 사이트를 만드는 것과 비슷합니다. 템플릿 및 구성 요소 만들기에 대한 자세한 내용은 다음 페이지를 참조하십시오. [템플릿](/help/sites-developing/templates.md), [구성 요소](/help/sites-developing/components.md), 및 [AEM Sites 개발 시작](/help/sites-developing/getting-started.md). 주요 차이점은 사이트 내에서 Adobe Experience Manager(AEM) 내장 모바일 기능을 활성화하는 것입니다. 모바일 페이지 구성 요소에 의존하는 템플릿을 만들어 이를 수행할 수 있습니다.

사용 고려 [반응형 디자인](/help/sites-developing/responsive.md), 여러 화면 크기를 수용하는 단일 사이트 생성.

시작하려면 다음을 살펴보십시오. **We.Retail 모바일 데모 사이트** AEM에서 사용할 수 있습니다.

모바일 사이트를 만들려면 다음과 같이 진행하십시오.

1. 페이지 구성 요소를 만듭니다.

   * 설정 `sling:resourceSuperType` 다음으로 속성: `wcm/mobile/components/page`
이러한 방식으로 구성 요소는 모바일 페이지 구성 요소를 사용합니다.

   * 만들기 `body.jsp` 프로젝트별 논리를 사용하는 경우입니다.

1. 페이지 템플릿 만들기:

   * 설정 `sling:resourceType` 속성을 새로 만든 페이지 구성 요소에 매핑합니다.
   * 설정 `allowedPaths` 속성.

1. 사이트에 대한 디자인 페이지를 만듭니다.
1. 아래 사이트 루트 페이지를 만듭니다. `/content` 노드:

   * 설정 `cq:allowedTemplates` 속성.
   * 설정 `cq:designPath` 속성.

1. 사이트 루트 페이지의 페이지 속성에서 **모바일** 탭.
1. 새 템플릿을 사용하여 사이트 페이지를 만듭니다.

모바일 페이지 구성 요소( `/libs/wcm/mobile/components/page`):

* 를 추가합니다. **모바일** 탭으로 이동하여 페이지 속성 대화 상자를 표시합니다.
* 를 통해 `head.jsp`, 요청에서 현재 모바일 장치 그룹을 검색하고 장치 그룹이 발견되면 그룹의 `drawHead()` 장치 그룹의 연결된 에뮬레이터 초기화 구성 요소(작성자 모드에서만)와 장치 그룹의 렌더링 CSS를 포함하는 방법입니다.

>[!NOTE]
>
>모바일 사이트의 루트 페이지는 노드 계층의 레벨 1에 있어야 하며 /content 노드 아래에 있는 것이 좋습니다.

## 다중 사이트 관리자를 사용하여 모바일 사이트 생성 {#creating-a-mobile-site-with-the-multi-site-manager}

MSM(Multi Site Manager)을 사용하여 표준 사이트에서 모바일 라이브 카피를 만듭니다. 표준 사이트는 자동으로 모바일 사이트로 변환됩니다. 모바일 사이트에는 모바일 사이트의 모든 기능(예: 에뮬레이터 내의 버전)이 있으며 표준 사이트와 동기화하여 관리할 수 있습니다. 섹션을 참조하십시오 [다른 채널을 위한 라이브 카피 만들기](/help/sites-administering/msm.md) 다중 사이트 관리자 페이지에서 참조할 수 있습니다.

## 서버측 모바일 API {#server-side-mobile-api}

모바일 클래스가 포함된 Java™ 패키지는 다음과 같습니다.

* [com.day.cq.wcm.mobile.api](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/mobile/api/device/capability/package-summary.html) - MobileConstant를 정의합니다.
* [com.day.cq.wcm.mobile.api.device](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/mobile/api/device/package-summary.html) - Device, DeviceGroup 및 DeviceGroupList를 정의합니다.
* [com.day.cq.wcm.mobile.api.device.capability](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/mobile/api/device/capability/package-summary.html) - DeviceCapability를 정의합니다.
* [com.day.cq.wcm.mobile.api.wurfl](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/workflow/api/package-summary.html) - WurflQueryEngine을 정의합니다.
* [com.day.cq.wcm.mobile.core](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/mobile/core/package-summary.html) - WCM Mobile을 중심으로 순환하는 다양한 유틸리티 메서드를 제공하는 MobileUtil을 정의합니다.

### 모바일 구성 요소 {#mobile-components}

다음 **We.Retail 모바일 데모 사이트** 는 아래에 있는 다음 모바일 구성 요소를 사용합니다. `/libs/foundation/components`:

<table>
 <tbody>
  <tr>
   <td>이름</td>
   <td>그룹</td>
   <td>특성</td>
  </tr>
  <tr>
   <td>mobilefooter</td>
   <td>숨김</td>
   <td>- 바닥글</td>
  </tr>
  <tr>
   <td>mobileimage</td>
   <td>모바일</td>
   <td>- 이미지 기초 구성 요소 기반<br /> - 장치가 가능한 경우 이미지를 렌더링합니다.<br /> </td>
  </tr>
  <tr>
   <td>mobilelist</td>
   <td>모바일</td>
   <td>- list foundation 구성 요소를 기반으로 함<br /> - listitem_teaser.jsp는 디바이스가 가능한 경우 이미지를 렌더링합니다.<br /> </td>
  </tr>
  <tr>
   <td>mobilelogo</td>
   <td>숨김</td>
   <td>- 로고 기초 구성 요소를 기반으로 함<br /> - 장치가 가능한 경우 이미지를 렌더링합니다.<br /> </td>
  </tr>
  <tr>
   <td>mobilereference</td>
   <td>모바일</td>
   <td><p>- 참조 기초 구성 요소와 유사</p> <p>- textimage 구성 요소를 mobiletextimage 구성 요소에 매핑하고 이미지 구성 요소를 mobileimage 구성 요소에 매핑합니다.</p> </td>
  </tr>
  <tr>
   <td>mobiletextimage</td>
   <td>모바일</td>
   <td>- textimage 기초 구성 요소 기반<br /> - 장치가 가능한 경우 이미지를 렌더링합니다.</td>
  </tr>
  <tr>
   <td>mobiletopnav</td>
   <td>숨김</td>
   <td><p>- topnav foundation 구성 요소 기반</p> <p>- 텍스트만 렌더링</p> </td>
  </tr>
 </tbody>
</table>

#### 모바일 구성 요소 만들기 {#creating-a-mobile-component}

AEM 모바일 프레임워크를 사용하면 요청을 실행하는 장치에 민감한 구성 요소를 개발할 수 있습니다. 다음 코드 샘플은 구성 요소 jsp에서 AEM 모바일 API를 사용하는 방법을 보여 주며 특히 다음 방법을 보여 줍니다.

* 요청에서 장치 가져오기:
  `Device device = slingRequest.adaptTo(Device.class);`

* 장치 그룹 가져오기:
  `DeviceGroup deviceGroup = device.getDeviceGroup();`

* 장치 그룹 기능 가져오기:
  `Collection<DeviceCapability> capabilities = deviceGroup.getCapabilities();`

* 디바이스 속성(WURFL 데이터베이스의 원시 기능 키/값) 가져오기:
  `Map<String,String> deviceAttributes = device.getAttributes();`

* 장치 사용자 에이전트 가져오기:
  `String userAgent = device.getUserAgent();`

* 현재 페이지에서 장치 그룹 목록(작성자가 사이트에 할당한 장치 그룹)을 가져옵니다.
  `DeviceGroupList deviceGroupList = currentPage.adaptTo(DeviceGroupList.class);`

* 장치 그룹이 이미지를 지원하는지 확인
  `if (deviceGroup.hasCapability(DeviceCapability.CAPABILITY_IMAGES)) {`
...
또는
  `if MobileUtil.hasCapability(request, DeviceCapability.CAPABILITY_IMAGES) {`
...

>[!NOTE]
>
>jsp의 경우, `slingRequest` 를 통해 사용할 수 있습니다. `<sling:defineObjects>` 태그 및 `currentPage` 다음을 통해 `<cq:defineObjects>` 태그에 가깝게 배치하십시오.

### 에뮬레이터 {#emulators}

에뮬레이터 기반 작성은 작성자가 모바일 클라이언트용 콘텐츠 페이지를 만들 수 있는 방법을 제공합니다. 모바일 컨텐츠 작성은 동일한 원본 위치 WYSIWYG 편집 원칙을 따릅니다. 작성자가 모바일 디바이스에서 페이지 모양을 인지할 수 있도록 디바이스 에뮬레이터를 사용하여 모바일 콘텐츠 페이지를 편집합니다.

모바일 장치 에뮬레이터는 일반 에뮬레이터 프레임워크를 기반으로 합니다. 자세한 내용은 [에뮬레이터](/help/sites-developing/emulators.md).

디바이스 에뮬레이터는 모바일 디바이스를 페이지에 표시하는 반면 일반적인 편집(parsys, components)은 디바이스의 화면 내에서 발생합니다. 장치 에뮬레이터는 사이트에 대해 구성된 장치 그룹에 따라 다릅니다. 여러 에뮬레이터를 장치 그룹에 할당할 수 있습니다. 그런 다음 콘텐츠 페이지에서 모든 에뮬레이터를 사용할 수 있습니다. 기본적으로 사이트에 할당된 첫 번째 장치 그룹에 할당된 첫 번째 에뮬레이터가 표시됩니다. 에뮬레이터는 Sidekick 상단의 에뮬레이터 회전 메뉴 또는 페이지의 편집 단추를 통해 전환할 수 있습니다.

**에뮬레이터 만들기**

에뮬레이터를 만들려면 다음을 참조하십시오 [사용자 지정 모바일 에뮬레이터 만들기](/help/sites-developing/emulators.md) 를 참조하십시오.

**모바일 에뮬레이터의 주요 특성**

* 장치 그룹은 하나 이상의 에뮬레이터로 구성됩니다. 예를 들어, /etc/mobile/groups/touch와 같은 장치 그룹 구성 페이지에는 `emulators` 아래 속성 `jcr:content` 노드.
참고: 동일한 에뮬레이터가 여러 장치 그룹에 속할 수 있지만 그다지 적절하지 않습니다.

* 장치 그룹의 구성 대화 상자를 통해 `emulators` 속성은 원하는 에뮬레이터의 경로로 설정됩니다. 예: `/libs/wcm/mobile/components/emulators/iPhone4`.

* 에뮬레이터 구성 요소(예: `/libs/wcm/mobile/components/emulators/iPhone4`) 기본 모바일 에뮬레이터 구성 요소를 확장합니다( `/libs/wcm/mobile/components/emulators/base`).

* 기본 모바일 에뮬레이터를 확장하는 모든 구성 요소는 장치 그룹을 구성할 때 선택할 수 있습니다. 따라서 사용자 지정 에뮬레이터를 쉽게 만들거나 확장할 수 있습니다.
* 편집 모드의 요청 시, 에뮬레이터 구현은 페이지를 렌더링하는 데 사용됩니다.
* 페이지의 템플릿이 모바일 페이지 구성 요소에 있으면 에뮬레이터 기능은 (를 통해) 페이지에 자동으로 통합됩니다. `head.jsp` ( 모바일 페이지 구성 요소).

### 장치 그룹 {#device-groups}

모바일 장치 그룹은 장치 기능에 따라 모바일 장치의 세그먼테이션을 제공합니다. 장치 그룹은 작성자 인스턴스의 에뮬레이터 기반 작성과 게시 인스턴스의 올바른 컨텐츠 렌더링에 필요한 정보를 제공합니다. 작성자가 모바일 페이지에 컨텐츠를 추가하고 게시하면 게시 인스턴스에서 페이지를 요청할 수 있습니다. 여기서 에뮬레이터 편집 보기 대신 구성된 장치 그룹 중 하나를 사용하여 컨텐츠 페이지가 렌더링됩니다. 장치 그룹의 선택은 다음을 기반으로 수행됩니다. [모바일 디바이스 감지](#devicedetection). 그러면, 매칭 디바이스 그룹은 필요한 스타일링 정보를 제공한다.

장치 그룹은 아래 컨텐츠 페이지로 정의됩니다 `/etc/mobile/devices` 및 사용 **모바일 장치 그룹** 템플릿. 장치 그룹 템플릿은 컨텐츠 페이지 형식의 장치 그룹 정의에 대한 구성 템플릿 역할을 합니다. 주요 특징은 다음과 같습니다.

* 위치: `/libs/wcm/mobile/templates/devicegroup`
* 허용된 경로: `/etc/mobile/groups/*`
* 페이지 구성 요소: `wcm/mobile/components/devicegroup`

#### 사이트에 장치 그룹 할당 {#assigning-device-groups-to-your-site}

모바일 사이트를 만들 때 장치 그룹을 사이트에 할당해야 합니다. AEM은 장치의 HTML 및 JavaScript 렌더링 기능에 따라 세 개의 장치 그룹을 제공합니다.

* **기능** 휴대폰, Sony Ericsson W800과 같은 기능 장치의 경우 기본 HTML은 지원되지만 이미지 및 JavaScript는 지원되지 않습니다.
* **스마트** 기본 HTML 및 이미지를 지원하지만 JavaScript는 지원하지 않는 BlackBerry®와 같은 장치의 경우.

* **터치** 휴대폰: HTML, 이미지, JavaScript 및 장치 회전을 완전히 지원하는 iPad과 같은 장치입니다.

에뮬레이터는 장치 그룹과 연결될 수 있으므로( 섹션 참조) [장치 그룹 만들기](#creating-a-device-group)) 장치 그룹을 사이트에 할당하면 작성자가 장치 그룹과 연결된 에뮬레이터 중에서 선택하여 페이지를 편집할 수 있습니다.

장치 그룹을 사이트에 할당하려면 다음 작업을 수행하십시오.

1. 브라우저에서 **Siteadmin** 콘솔.
1. 아래에서 모바일 사이트의 루트 페이지를 엽니다. **웹 사이트**.
1. 페이지 속성을 엽니다.
1. 다음 항목 선택 **모바일** 탭:

   * 장치 그룹을 정의합니다.
   * **확인**&#x200B;을 클릭합니다.

>[!NOTE]
>
>사이트에 대해 장치 그룹이 정의되면 사이트의 모든 페이지에 상속됩니다.

#### 장치 그룹 필터 {#device-group-filters}

장치 그룹 필터는 장치가 그룹에 속하는지 여부를 결정하는 기능 기반 기준을 정의합니다. 장치 그룹을 만들 때 장치 평가에 사용할 필터를 선택할 수 있습니다.

AEM이 장치에서 HTTP 요청을 받는 런타임에 그룹과 연결된 각 필터는 장치 기능을 특정 기준과 비교합니다. 장치에 필터가 필요로 하는 모든 기능이 있는 경우 장치가 그룹에 속하는 것으로 간주됩니다. 기능은 WURFL™ 데이터베이스에서 검색됩니다.

장치 그룹은 기능 감지를 위해 0개 이상의 필터를 사용할 수 있습니다. 또한 필터를 여러 장치 그룹과 함께 사용할 수 있습니다. AEM은 디바이스에 그룹에 대해 선택된 기능이 있는지 여부를 결정하는 기본 필터를 제공합니다.

* CSS
* JPG 및 PNG 이미지
* JavaScript
* 장치 회전

장치 그룹에서 필터를 사용하지 않는 경우 그룹에 대해 구성된 선택된 기능은 장치에 필요한 유일한 기능입니다.

자세한 내용은 [장치 그룹 필터 만들기](/help/sites-developing/groupfilters.md).

#### 장치 그룹 만들기 {#creating-a-device-group}

AEM이 설치하는 그룹이 요구 사항을 충족하지 않을 때 장치 그룹을 만듭니다.

1. 브라우저에서 **도구** 콘솔.
1. 아래 페이지 만들기 **도구** > **모바일** > **장치 그룹**. 다음에서 **페이지 만들기** 대화 상자:

   * 다음으로: **제목**, 입력 `Special Phones`.

   * 다음으로: **이름**, 입력 `special`.

   * 다음 항목 선택 **모바일 장치 그룹 템플릿**.
   * **만들기**&#x200B;를 클릭합니다.

1. CRXDE에서 **static.css** 아래에 장치 그룹의 스타일이 들어 있는 파일 `/etc/mobile/groups/special` 노드.

1. 를 엽니다. **특수 전화** 페이지를 가리키도록 업데이트하는 중입니다.
1. 장치 그룹을 구성하려면 **편집** 옆에 있는 단추 **설정**.
다음에서 **일반** 탭:

   * **제목**: 모바일 장치 그룹의 이름입니다.
   * **설명**: 그룹에 대한 설명.
   * **User-Agent**: 장치가 일치하는 사용자 에이전트 문자열입니다. 이 변수는 선택 사항이며 정규 표현식이 될 수 있습니다. 예: `BlackBerryZ10`
   * **기능**: 그룹이 이미지, CSS, JavaScript 또는 장치 회전을 처리할 수 있는지 여부를 정의합니다.
   * **최소 화면 너비**&#x200B;및&#x200B;**높이**
   * **에뮬레이터 사용 안 함**: 콘텐츠를 편집하는 동안 에뮬레이터를 활성화/비활성화합니다.

   다음에서 **에뮬레이터** 탭:

   * **에뮬레이터**: 이 장치 그룹에 지정된 에뮬레이터를 선택합니다.

   다음에서 **필터** 탭:

   * 필터를 추가하려면 항목 추가 를 클릭하고 드롭다운 목록에서 필터를 선택합니다.
   * 필터는 표시되는 순서대로 평가됩니다. 장치가 필터의 기준을 충족하지 않으면 목록의 후속 필터가 평가되지 않습니다.

1. 확인을 클릭합니다.

모바일 장치 그룹 구성 대화 상자는 다음과 같습니다.

![screen_shot_2012-02-01at22043pm](assets/screen_shot_2012-02-01at22043pm.png)

#### 장치 그룹당 사용자 지정 CSS {#custom-css-per-device-group}

앞에서 설명한 대로 사용자 지정 CSS를 디자인 페이지의 CSS와 마찬가지로 장치 그룹 페이지와 연결할 수 있습니다. 이 CSS는 작성 및 게시에 대한 페이지 콘텐츠의 장치 그룹별 렌더링에 영향을 주는 데 사용됩니다. 그런 다음 이 CSS가 자동으로 포함됩니다.

* 작성자 인스턴스의 페이지에서 이 장치 그룹에 사용되는 모든 에뮬레이터에 대해 다음을 수행합니다.
* 게시 인스턴스의 페이지에서 요청의 사용자 에이전트가 이 특정 장치 그룹의 모바일 장치와 일치하는 경우.

## 서버측 장치 감지 {#server-side-device-detection}

필터 및 장치 사양의 라이브러리를 사용하여 HTTP 요청을 수행하는 장치의 기능을 결정합니다.

### 장치 그룹 필터 개발 {#develop-device-group-filters}

장치 그룹 필터를 만들어 장치 기능 요구 사항 집합을 정의합니다. 필요한 장치 기능 그룹을 타깃팅하는 데 필요한 만큼 필터를 만듭니다.

필터 조합을 사용하여 기능 그룹을 정의할 수 있도록 필터를 디자인합니다. 일반적으로 서로 다른 장치 그룹의 기능이 겹칩니다. 따라서 여러 장치 그룹 정의가 있는 일부 필터를 사용할 수 있습니다.

필터를 만든 후 그룹 구성에서 사용할 수 있습니다.

자세한 내용을 보려면 [장치 그룹 필터 만들기](/help/sites-developing/groupfilters.md).

### WURFL™ 데이터베이스 사용 {#using-the-wurfl-database}

AEM은 의 잘린 버전을 사용합니다. [WURFL](https://wurfl.sourceforge.net/)™을 사용하여 디바이스의 사용자 에이전트를 기반으로 화면 해상도 또는 JavaScript 지원과 같은 디바이스 기능을 쿼리합니다.

WURFL™ 데이터베이스의 XML 코드는 아래 노드로 표시됩니다 `/var/mobile/devicespecs` 구문 분석 `wurfl.xml`파일 위치: `/libs/wcm/mobile/devicespecs/wurfl.xml.` 노드로의 확장은 `cq-mobile-core` 번들이 시작되었습니다.

디바이스 기능은 노드 속성으로 저장되며, 노드는 디바이스 모델을 나타냅니다. 쿼리를 사용하여 장치 또는 사용자 에이전트의 기능을 검색할 수 있습니다.

WURFL™ 데이터베이스가 발전함에 따라 데이터베이스를 사용자 정의하거나 교체해야 할 수 있습니다. 모바일 장치 데이터베이스를 업데이트하려면 다음 옵션이 필요합니다.

* 이 사용을 허용하는 라이센스가 있는 경우 파일을 최신 버전으로 바꾸십시오. 다른 WURFL 데이터베이스 설치를 참조하십시오.
* AEM에서 사용할 수 있는 버전을 사용하고 사용자 에이전트 문자열과 일치하고 기존 WURFL™ 디바이스를 가리키는 regexp를 구성합니다. 다음을 참조하십시오 [정규 표현식 기반 사용자-에이전트 일치 추가](#adding-a-regexp-based-user-agent-matching).

#### WURFL™ 기능에 대한 사용자 에이전트 매핑 테스트 {#testing-the-mapping-of-a-user-agent-to-wurfl-capabilities}

장치가 모바일 사이트에 액세스하면 AEM이 장치를 감지하여 기능에 따라 장치 그룹에 매핑하고 장치 그룹에 해당하는 페이지 보기를 보냅니다. 매칭하는 디바이스 그룹은 필요한 스타일링 정보를 제공한다. 매핑은 모바일 사용자 에이전트 테스트 페이지에서 테스트할 수 있습니다.

`https://localhost:4502/etc/mobile/useragent-test.html`

#### 다른 WURFL™ 데이터베이스 설치 {#installing-a-different-wurfl-database}

AEM과 함께 설치되는 잘린 WURFL™ 데이터베이스는 2011년 8월 30일 이전에 릴리스됩니다. WURFL 버전이 2011년 8월 30일 이후에 릴리스된 경우 사용이 라이센스를 준수하는지 확인하십시오.

WURFL™ 데이터베이스를 설치하려면:

1. CRXDE Lite에서 다음 폴더를 만듭니다. `/apps/wcm/mobile/devicespecs`
1. 폴더에 WURFL™ 파일을 복사합니다.
1. 파일 이름을 로 변경합니다. `wurfl.xml`.

AEM은 다음을 자동으로 구문 분석합니다 `wurfl.xml` 아래 노드 파일 및 업데이트 `/var/mobile/devicespecs`.

>[!NOTE]
>
>전체 WURFL™ 데이터베이스가 활성화된 경우 구문 분석과 활성화가 몇 분 정도 소요될 수 있습니다. 진행 상황 정보를 보려면 로그를 볼 수 있습니다.

#### 정규 표현식 기반 사용자-에이전트 일치 추가 {#adding-a-regexp-based-user-agent-matching}

/apps/wcm/mobile/devicesecs/wurfl/regexp 아래에 사용자 에이전트를 정규식으로 추가하여 기존 WURFL™ 장치 유형을 가리킵니다.

1. 위치 **CRXDE Lite**, /apps/wcm/mobile/devicesecs/regexp 아래에 노드를 만듭니다. 예: `apple_ipad_ver1`.
1. 노드에 다음 속성을 추가합니다.

   * **regexp**: 사용자 에이전트를 정의하는 정규 표현식(예: ).&#42;모질라&#42;iPad.&#42;AppleWebkit.&#42;Safari.&#42;
   * **deviceId**: wurfl.xml에 정의된 디바이스 ID(예: ) `apple_ipad_ver1`

위의 구성은 사용자 에이전트가 제공된 정규 표현식과 일치하는 장치가 apple_ipad_ver1 WURFL™ 장치 ID(있는 경우)에 매핑되도록 합니다.

## 클라이언트측 디바이스 감지 {#client-side-device-detection}

이 섹션에서는 AEM의 장치 클라이언트측 감지를 사용하여 페이지 렌더링을 최적화하거나 클라이언트에 대체 웹 사이트 버전을 제공하는 방법에 대해 설명합니다.

AEM은 다음을 기반으로 장치 클라이언트측 감지 지원 `BrowserMap`. `BrowserMap` AEM에서 클라이언트 라이브러리로 제공됩니다. `/etc/clientlibs/browsermap`.

`BrowserMap` 은 고객에게 대체 웹 사이트를 제공하는 데 사용할 수 있는 세 가지 전략을 제공하며, 이 전략은 다음 순서로 사용됩니다.

1. [대체 링크](#providing-alternate-links)
1. [장치 그룹별 URL](#definingdevicegroupspecificurl)
1. [선택기 기반 URL](#defining-selector-based-urls)

>[!NOTE]
>
클라이언트 라이브러리 통합에 대한 자세한 내용은 [클라이언트측 HTML 라이브러리 사용](/help/sites-developing/clientlibs.md).

### 대체 링크 제공 {#providing-alternate-links}

다음 `PageVariantsProvider` OSGi 서비스는 동일한 패밀리에 속하는 사이트에 대한 대체 링크를 생성할 수 있습니다. 서비스에서 고려할 사이트를 구성하려면 `cq:siteVariant` 노드를 다음에 추가해야 함 `jcr:content` 사이트 루트의 노드입니다.

다음 `cq:siteVariant` 노드에는 다음 속성이 있어야 합니다.

* `cq:childNodesMapTo` - 하위 노드가 매핑될 링크 요소의 속성을 결정합니다. 루트 노드의 하위 노드가 전역 웹 사이트의 언어 변형에 대한 루트를 나타내도록 웹 사이트의 콘텐츠를 구성하는 것이 좋습니다(예: `/content/mysite/en`, `/content/mysite/de`). 이 경우 의 값은 `cq:childNodesMapTo` 다음이어야 함: `hreflang`;
* `cq:variantDomain` - 다음을 나타냅니다. `Externalizer` 도메인은 페이지 변형 절대 URL을 생성하는 데 사용됩니다. 이 값이 설정되지 않은 경우 페이지 변형은 상대 링크를 사용하여 생성됩니다.
* `cq:variantFamily` - 이 사이트가 속한 웹 사이트 제품군을 나타냅니다. 동일한 웹 사이트의 여러 디바이스별 표시가 동일한 제품군에 속해야 합니다.
* `media` - link 요소의 media 속성 값을 저장합니다. 이름을 사용하는 것이 좋습니다. `BrowserMap` 등록됨 `DeviceGroups`, 따라서 `BrowserMap` 라이브러리는 웹 사이트의 올바른 변형으로 클라이언트를 자동으로 전달할 수 있습니다.

#### PageVariantsProvider 및 Externalizer {#pagevariantsprovider-and-externalizer}

값: `cq:variantDomain` 의 속성 `cq:siteVariant` 노드가 비어 있지 않습니다. `PageVariantsProvider` 서비스는 이 값을 의 구성된 도메인으로 사용하여 절대 링크를 생성합니다. `Externalizer` 서비스. 다음을 구성해야 합니다. `Externalizer` 설정을 반영하는 서비스.

>[!NOTE]
>
AEM을 사용하여 작업할 때 이러한 서비스에 대한 구성 설정을 관리하는 방법에는 몇 가지가 있습니다. 다음을 참조하십시오. [OSGi 구성](/help/sites-deploying/configuring-osgi.md) 를 참조하십시오.

### 장치 그룹별 URL 정의 {#defining-a-device-group-specific-url}

대체 링크를 사용하지 않으려면 각각에 대해 글로벌 URL을 구성할 수 있습니다 `DeviceGroup`. Adobe은 를 임베드하는 고유한 클라이언트 라이브러리를 만들 것을 권장합니다. `browsermap.standard` 클라이언트 라이브러리이지만 장치 그룹을 재정의합니다.

BrowserMap은 장치 그룹 정의를 재정의할 수 있는 방식으로 디자인되었습니다. `BrowserMap` 사용자 지정된 클라이언트 라이브러리의 객체입니다.

>[!NOTE]
>
자세한 내용은 [사용자 지정된 브라우저 맵](#creatingacustomisedbrowsermap).

### 선택기 기반 URL 정의 {#defining-selector-based-urls}

이전 메커니즘 중 대체 사이트를 나타내는 데 사용된 메커니즘이 없는 경우 `BrowserMap`을 클릭한 다음 의 이름을 사용할 선택기 `DeviceGroups` 이(가)에 추가됩니다. `URL`s. 이 경우 요청을 처리할 고유한 서블릿을 제공해야 합니다.

예를 들어 디바이스 찾아보기 `www.example.com/index.html` 다음으로 식별됨 `smartphone` BrowserMap에 의해 전달됩니다. `www.example.com/index.smartphone.html.`

### 페이지에서 BrowserMap 사용 {#using-browsermap-on-your-pages}

페이지에서 표준 BrowserMap 클라이언트 라이브러리를 사용하려면 다음을 포함해야 합니다 `/libs/wcm/core/browsermap/browsermap.jsp` 를 사용하는 파일 `cq:include`페이지의 `head` 섹션.

```xml
<cq:include script="/libs/wcm/core/browsermap/browsermap.jsp" />
```

추가 외 `BrowserMap` 의 클라이언트 라이브러리 `JSP` 파일, 다음을 추가해야 함: `cq:deviceIdentificationMode` 문자열 속성이 로 설정됨 `client-side` (으)로 `jcr:content` 웹 사이트의 루트 아래에 있는 노드입니다.

### BrowserMap의 기본 동작 재정의 {#overriding-browsermap-s-default-behaviour}

사용자 지정하려는 경우 `BrowserMap` - 재정의하여 `DeviceGroups` 또는 더 많은 Probe를 추가하는 경우 를 포함할 고유한 클라이언트측 라이브러리를 만들어야 합니다. `browsermap.standard`클라이언트측 라이브러리입니다.

또한 을 수동으로 호출해야 합니다. `BrowserMap.forwardRequest()` 의 메서드 `JavaScript` 코드.

>[!NOTE]
>
클라이언트 라이브러리 통합에 대한 자세한 내용은 [클라이언트측 HTML 라이브러리 사용](/help/sites-developing/clientlibs.md).

맞춤화된 항목을 만들면 `BrowserMap` 클라이언트 라이브러리와 Adobe은 다음 접근 방식을 제안합니다.

1. 만들기 `browsermap.jsp` 응용 프로그램의 파일

   ```xml
   <%@include file="/libs/foundation/global.jsp" %>
   <%@ taglib prefix="c" uri="https://java.sun.com/jsp/jstl/core" %>
   <%@ page import="
       com.day.cq.wcm.api.variants.PageVariant,
       com.day.cq.wcm.api.variants.PageVariantsProvider,
       com.day.cq.wcm.api.devicedetection.DeviceIdentificationMode,
       com.day.cq.wcm.api.WCMMode"
   %>
   <%
       final PageVariantsProvider p = sling.getService(PageVariantsProvider.class);
       if(p == null) {
           throw new IllegalStateException("Missing PageVariantsProvider service");
       }
       for(PageVariant v : p.getVariants(currentPage, slingRequest)) {
           final String curVar = v.getAttributes().get("data-current-variant");
           String media = v.getAttributes().get("media");
           if (media != null) {
               media = media.replaceAll(" ", "");
           }
   %>
       <link
           rel="alternate"
           data-cq-role="site.variant"
           title="<%= xssAPI.encodeForHTMLAttr(v.getTitle()) %>"
           hreflang="<%= xssAPI.encodeForHTMLAttr(v.getAttributes().get("hreflang")) %>"
           media="<%= xssAPI.encodeForHTMLAttr(media) %>"
           href="<%= xssAPI.getValidHref(v.getURL()) %>"
           <% if(curVar != null) { %> data-current-variant="<%= curVar %>"<% } %>
       />
   <%
       }
       Boolean browserMapEnabled = true;
       final DeviceIdentificationMode dim = sling.getService(DeviceIdentificationMode.class);
       String[] selectors  = slingRequest.getRequestPathInfo().getSelectors();
       boolean isPortletRequest = false;
       for (int i = 0; i < selectors.length; i++) {
           if ("portlet".equals(selectors[i])) {
               isPortletRequest = true;
               break;
           }
       }
       if (isPortletRequest) {
           log.debug("Request was made by a portlet container - BrowserMap will not be embedded");
       } else {
           final WCMMode wcmMode = WCMMode.fromRequest(slingRequest);
           boolean shouldIncludeClientLib = false;
           if (WCMMode.EDIT != wcmMode && WCMMode.PREVIEW != wcmMode && WCMMode.DESIGN != wcmMode) {
               if (dim != null) {
                   final String mode = dim.getDeviceIdentificationModeForPage(currentPage);
                   shouldIncludeClientLib = DeviceIdentificationMode.CLIENT_SIDE.equals(mode);
                   if (shouldIncludeClientLib) {
                       browserMapEnabled = (Boolean) request.getAttribute("browsermap.enabled");
                       if (browserMapEnabled == null) {
                           browserMapEnabled = true;
                       }
                   }
               }
           }
   %>
           <c:if test="<%= !browserMapEnabled %>">
               <meta name="browsermap.enabled" content="false">
           </c:if>
           <c:if test="<%= shouldIncludeClientLib %>">
               <meta name="viewport" content="width=device-width, initial-scale=1.0">
               <cq:includeClientLib categories="browsermap.custom"/>
           </c:if>
   <%
       }
   %>
   ```

1. 포함 `broswermap.jsp` head 섹션에 있는 파일입니다.

   ```xml
   <cq:include script="browsermap.jsp" />
   ```

### 특정 페이지에서 BrowserMap 제외 {#excluding-browsermap-from-certain-pages}

클라이언트 검색이 필요하지 않은 일부 페이지에서 BrowserMap 라이브러리를 제외하려면 요청 속성을 추가할 수 있습니다.

```xml
<%
request.setAttribute("browsermap.enabled", false);
%>
```

이렇게 하면 다음이 수행됩니다. `/libs/wcm/core/browsermap/browsermap.jsp` 메타 태그를 페이지에 추가하는 스크립트 `BrowserMap` 검색을 수행하지 않으려면 다음을 수행합니다.

```xml
<meta name="browsermap.enabled" content="false">
```

### 웹 사이트의 특정 버전 테스트 {#testing-a-specific-version-of-a-web-site}

일반적으로 BrowserMap 스크립트는 항상 방문자를 가장 적합한 웹 사이트 버전으로 리디렉션하며, 일반적으로 필요한 경우 데스크탑 또는 모바일 사이트로 리디렉션합니다.

를 추가하여 모든 요청의 장치가 웹 사이트의 특정 버전을 테스트하도록 강제할 수 있습니다. `device` 매개 변수를 URL에 추가합니다. 다음 URL은 Geometrixx Outdoors 웹 사이트의 모바일 버전을 렌더링합니다.

`https://localhost:4502/content/geometrixx-outdoors/en.html?wcmmode=disabled&device=smartphone`

>[!NOTE]
>
다음 `wcmmode` 매개 변수가 로 설정되어 있습니다. `disabled` 게시 인스턴스의 비헤이비어를 시뮬레이션합니다.

오버라이드 디바이스 값은 쿠키에 저장되므로 을 추가하지 않고도 웹 사이트를 검색할 수 있습니다. `device` 매개 변수 `URL`.

따라서 동일한 을 호출해야 합니다 `URL` (으)로 `device` 을 로 설정 `browser` 웹 사이트의 데스크탑 버전으로 돌아갑니다.

>[!NOTE]
>
BrowserMap은 오버라이딩 장치 값을 `BMAP_device`. 이 쿠키를 삭제하면 CQ가 현재 장치(예: 데스크탑 또는 모바일)에 따라 적절한 웹 사이트 버전을 제공합니다.

## 모바일 요청 처리 {#mobile-request-processing}

AEM은 터치 장치 그룹에 속하는 모바일 장치에서 발행한 요청을 다음과 같이 처리합니다.

1. iPad은 AEM 게시 인스턴스로 요청을 보냅니다(예: ). `https://localhost:4503/content/geometrixx_mobile/en/products.html`
1. AEM은 요청된 페이지의 사이트가 모바일 사이트인지 여부를 결정합니다(첫 번째 수준 페이지인지 여부를 확인하여) `/content/geometrixx_mobile` 모바일 페이지 구성 요소를 확장합니다). 해당되는 경우:
1. AEM은 요청 헤더의 사용자 에이전트를 기반으로 장치 기능을 조회합니다.
1. AEM은 장치 기능을 장치 그룹에 매핑하고 를 설정합니다. `touch` 디바이스 그룹 선택기로 사용됩니다.
1. AEM이 요청을으로 리디렉션합니다. `https://localhost:4503/content/geometrixx_mobile/en/products.touch.html.`
1. AEM이 iPad에 응답을 보냅니다.

   * `products.touch.html` 는 일반적인 방식으로 렌더링되며 캐시할 수 있습니다.
   * 렌더링 구성 요소는 선택기를 사용하여 프레젠테이션을 조정합니다.
   * AEM은 페이지의 모든 내부 링크에 모바일 선택기를 자동으로 추가합니다.

### 통계 {#statistics}

모바일 장치에서 AEM 서버에 대해 수행한 요청 수에 대한 몇 가지 통계를 가져올 수 있습니다. 요청 수는 다음과 같이 분류할 수 있습니다.

* 장치 그룹 및 장치당
* 년, 월 및 일

통계를 보려면 다음과 같이 하십시오.

1. 로 이동 **도구** 콘솔.
1. 를 엽니다. **장치 통계** 아래 페이지 **도구** > **모바일**.
1. 링크를 눌러 특정 연도, 월 또는 일에 대한 통계를 확인합니다.

다음 **통계** 페이지는 다음과 같습니다.

![screen_shot_2012-02-01at24353pm](assets/screen_shot_2012-02-01at24353pm.png)

>[!NOTE]
>
다음 **통계** 모바일 장치가 AEM에 처음 액세스하고 검색되면 페이지가 만들어집니다. 그 전에는 사용이 불가능합니다

통계에서 항목을 생성해야 하는 경우 다음과 같이 진행할 수 있습니다.

1. 모바일 디바이스 또는 에뮬레이터(예: Firefox의 https://chrispederick.com/work/user-agent-switcher/)를 사용합니다.
1. 작성 모드를 비활성화하여 작성자 인스턴스의 모바일 페이지를 요청합니다. 예를 들면 다음과 같습니다.
   `https://localhost:4502/content/geometrixx_mobile/en/products.html?wcmmode=disabled`

다음 **통계** 이제 페이지를 사용할 수 있습니다.

### 친구에게 링크 보내기 링크에 대한 페이지 캐싱 지원 {#supporting-page-caching-for-send-link-to-a-friend-links}

장치 그룹에 대해 렌더링되는 페이지는 장치 그룹 선택기에 의해 페이지 URL에서 구별되므로 모바일 페이지는 Dispatcher에서 캐시할 수 있습니다 `/content/mobilepage.touch.html`. 선택기가 없는 모바일 페이지에 대한 요청은 캐시되지 않습니다. 이 경우 디바이스 감지가 작동하고 최종적으로 일치하는 디바이스 그룹(또는 해당 문제에 대한 &quot;nomatch&quot;)으로 리디렉션됩니다. 장치 그룹 선택기로 렌더링된 모바일 페이지는 링크 재작성기에 의해 처리되며, 링크 재작성기는 페이지 내의 모든 링크를 장치 그룹 선택기를 포함하도록 재작성하여 이미 자격이 있는 페이지를 클릭할 때마다 장치 감지를 다시 수행하지 않도록 합니다.

따라서 다음과 같은 시나리오가 발생할 수 있습니다.

사용자 Alice가 (으)로 리디렉션됨 `coolpage.feature.html`에 있는 다른 클라이언트로 액세스하는 친구 Bob에게 해당 URL을 보냅니다. `touch` 장치 그룹.

If `coolpage.feature.html` 는 프론트엔드 캐시에서 제공되며, AEM은 요청을 분석하여 모바일 선택기가 새 사용자 에이전트와 일치하지 않으며 Bob이 잘못된 표현을 가져오는지 확인할 수 없습니다.

이 문제를 해결하려면 페이지에 간단한 선택 UI를 포함할 수 있습니다. 이 UI에서 최종 사용자는 AEM에서 선택한 장치 그룹을 무시할 수 있습니다. 위의 예에서 페이지의 링크(또는 아이콘)는 최종 사용자가 `coolpage.touch.html` 만약 그들이 그들의 장치가 그것을 위해 충분하다고 생각한다면.
