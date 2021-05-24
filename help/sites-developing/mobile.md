---
title: 모바일 장치용 사이트 만들기
seo-title: 모바일 장치용 사이트 만들기
description: 모바일 사이트를 만드는 것은 템플릿 및 구성 요소를 만드는 작업이 포함되므로 표준 사이트를 만드는 것과 비슷합니다
seo-description: 모바일 사이트를 만드는 것은 템플릿 및 구성 요소를 만드는 작업이 포함되므로 표준 사이트를 만드는 것과 비슷합니다
uuid: 6b19042c-03f1-4e33-970e-475f9fb8c5fb
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
discoiquuid: 0aabfb0a-ef9c-4b06-b698-61cad101c3c1
docset: aem65
legacypath: /content/docs/en/aem/6-0/develop/mobile/mobile
exl-id: 21b2037a-685a-441d-aecd-865884253e03
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '3864'
ht-degree: 1%

---

# 모바일 장치용 사이트 만들기{#creating-sites-for-mobile-devices}

>[!NOTE]
>
>단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: React)이 필요한 프로젝트에 SPA 편집기를 사용하는 것이 좋습니다. [추가 정보](/help/sites-developing/spa-overview.md).

모바일 사이트를 만드는 것은 템플릿 및 구성 요소를 만드는 작업이 포함되므로 표준 사이트를 만드는 것과 비슷합니다. 템플릿 및 구성 요소 만들기에 대한 자세한 내용은 다음 페이지를 참조하십시오.[템플릿](/help/sites-developing/templates.md), [구성 요소](/help/sites-developing/components.md) 및 [AEM Sites 개발 시작](/help/sites-developing/getting-started.md). 가장 큰 차이점은 사이트 내에서 AEM 내장된 모바일 기능을 활성화하는 것입니다. 모바일 페이지 구성 요소를 사용하는 템플릿을 만들어 냅니다.

또한 [반응형 디자인](/help/sites-developing/responsive.md)을 사용하여 여러 화면 크기를 포함하는 단일 사이트를 만드는 것도 고려해야 합니다.

시작하려면 AEM에서 사용할 수 있는 **We.Retail 모바일 데모 사이트**&#x200B;를 살펴보십시오.

모바일 사이트를 만들려면 다음과 같이 진행하십시오.

1. 페이지 구성 요소를 만듭니다.

   * `sling:resourceSuperType` 속성을 `wcm/mobile/components/page` 로 설정합니다.
이렇게 하면 구성 요소가 모바일 페이지 구성 요소에 의존합니다.

   * 프로젝트 특정 논리를 사용하여 `body.jsp` 을 만듭니다.

1. 페이지 템플릿을 만듭니다.

   * `sling:resourceType` 속성을 새로 만든 페이지 구성 요소로 설정합니다.
   * `allowedPaths` 속성을 설정합니다.

1. 사이트에 대한 디자인 페이지를 만듭니다.
1. `/content` 노드 아래에 사이트 루트 페이지를 만듭니다.

   * `cq:allowedTemplates` 속성을 설정합니다.
   * `cq:designPath` 속성을 설정합니다.

1. 사이트 루트 페이지의 페이지 속성에서 **모바일** 탭에서 장치 그룹을 설정합니다.
1. 새 템플릿을 사용하여 사이트 페이지를 만듭니다 .

모바일 페이지 구성 요소( `/libs/wcm/mobile/components/page`):

* **모바일** 탭을 페이지 속성 대화 상자에 추가합니다.
* `head.jsp`을 통해 요청에서 현재 모바일 장치 그룹을 검색하고, 장치 그룹이 발견되면 그룹의 `drawHead()` 메서드를 사용하여 장치 그룹의 연결된 에뮬레이터 init 구성 요소(작성자 모드에서만)와 장치 그룹의 렌더링 CSS를 포함합니다.

>[!NOTE]
>
>모바일 사이트의 루트 페이지는 노드 계층 구조의 수준 1에 있어야 하며 /content 노드 아래에 있는 것이 좋습니다.

## 다중 사이트 관리자 {#creating-a-mobile-site-with-the-multi-site-manager}로 모바일 사이트 만들기

MSM(Multi Site Manager)을 사용하여 표준 사이트에서 모바일 Live Copy를 만듭니다. 표준 사이트는 자동으로 모바일 사이트로 변환됩니다.모바일 사이트에는 모바일 사이트의 모든 기능(예: 에뮬레이터 내의 버전)이 있으며 표준 사이트와 동기화 시 관리할 수 있습니다. 다중 사이트 관리자 페이지에서 [다른 채널용 라이브 카피 만들기](/help/sites-administering/msm.md) 섹션을 참조하십시오.

## 서버측 모바일 API {#server-side-mobile-api}

모바일 클래스가 포함된 Java 패키지는 다음과 같습니다.

* [com.day.cq.wcm.mobile.api](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/api/device/capability/package-summary.html)  - MobileConstants를 정의합니다.
* [com.day.cq.wcm.mobile.api.device](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/api/device/package-summary.html)  - Device, DeviceGroup 및 DeviceGroupList를 정의합니다.
* [com.day.cq.wcm.mobile.api.device.capability](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/api/device/capability/package-summary.html)  - DeviceCapability를 정의합니다.
* [com.day.cq.wcm.mobile.api.wurfl](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/workflow/api/package-summary.html)  - WurflQueryEngine을 정의합니다.
* [com.day.cq.wcm.mobile.core](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/core/package-summary.html)  - WCM Mobile을 회전하는 다양한 유틸리티 메서드를 제공하는 MobileUtil을 정의합니다.

### 모바일 구성 요소 {#mobile-components}

**We.Retail 모바일 데모 사이트**&#x200B;에서는 `/libs/foundation/components` 아래에 있는 다음 모바일 구성 요소를 사용합니다.

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
   <td>- image foundation 구성 요소<br /> 기반 - 장치가 가능한 경우 이미지를 렌더링합니다.<br /> </td>
  </tr>
  <tr>
   <td>mobilelist</td>
   <td>모바일</td>
   <td>- list foundation 구성 요소<br /> - list_tem_teaser.jsp를 기반으로 디바이스가 지원 가능한 경우 이미지를 렌더링합니다.<br /> </td>
  </tr>
  <tr>
   <td>mobilelogo</td>
   <td>숨김</td>
   <td>- logo foundation 구성 요소<br /> 기반 - 장치가 가능한 경우 이미지를 렌더링합니다.<br /> </td>
  </tr>
  <tr>
   <td>mobilereference</td>
   <td>모바일</td>
   <td><p>- 참조 foundation 구성 요소와 유사</p> <p>- textimage 구성 요소를 mobiletextimage 1에 매핑하고 이미지 구성 요소를 mobileimage 1에 매핑합니다.</p> </td>
  </tr>
  <tr>
   <td>mobiletextimage</td>
   <td>모바일</td>
   <td>- textimage foundation 구성 요소<br /> 기반 - 장치가 작동할 수 있으면 이미지를 렌더링합니다.</td>
  </tr>
  <tr>
   <td>mobiletopnav</td>
   <td>숨김</td>
   <td><p>- topnav foundation 구성 요소 기반</p> <p>- 텍스트만 렌더링됨</p> </td>
  </tr>
 </tbody>
</table>

#### 모바일 구성 요소 만들기 {#creating-a-mobile-component}

AEM 모바일 프레임워크를 사용하면 요청을 실행하는 장치에 민감한 구성 요소를 개발할 수 있습니다. 다음 코드 샘플은 구성 요소 jsp에서 AEM Mobile API를 사용하는 방법과 특히 다음 방법을 보여 줍니다.

* 요청에서 장치 가져오기:
   `Device device = slingRequest.adaptTo(Device.class);`

* 장치 그룹 가져오기:
   `DeviceGroup deviceGroup = device.getDeviceGroup();`

* 장치 그룹 기능 가져오기:
   `Collection<DeviceCapability> capabilities = deviceGroup.getCapabilities();`

* 장치 속성(WURFL 데이터베이스에서 원시 기능 키/값)을 가져옵니다.
   `Map<String,String> deviceAttributes = device.getAttributes();`

* 장치 사용자 에이전트 가져오기:
   `String userAgent = device.getUserAgent();`

* 현재 페이지에서 장치 그룹 목록(작성자가 사이트에 할당한 장치 그룹)을 가져옵니다.
   `DeviceGroupList deviceGroupList = currentPage.adaptTo(DeviceGroupList.class);`

* 장치 그룹이 이미지를 지원하는지 확인
   `if (deviceGroup.hasCapability(DeviceCapability.CAPABILITY_IMAGES)) {`
...
또는

...   `if MobileUtil.hasCapability(request, DeviceCapability.CAPABILITY_IMAGES) {`
...

>[!NOTE]
>
>jsp에서 `slingRequest`는 `<sling:defineObjects>` 태그 및 `currentPage`를 통해 `<cq:defineObjects>` 태그를 통해 사용할 수 있습니다.

### 에뮬레이터 {#emulators}

에뮬레이터 기반 작성은 작성자가 모바일 클라이언트용 컨텐츠 페이지를 만들 수 있는 수단을 제공합니다. 모바일 컨텐츠 작성은 즉석 WYSIWYG 편집의 동일한 원칙을 따릅니다. 작성자가 모바일 장치에서 페이지 모양을 인식하도록 하기 위해, 모바일 컨텐츠 페이지는 장치 에뮬레이터를 사용하여 편집됩니다.

모바일 장치 에뮬레이터는 일반 에뮬레이터 프레임워크를 기반으로 합니다. 자세한 내용은 [에뮬레이터](/help/sites-developing/emulators.md) 페이지를 참조하십시오.

장치 에뮬레이터는 페이지에 모바일 장치를 표시하는 반면, 일반적인 편집(parsys, 구성 요소)은 장치의 화면 내에서 발생합니다. 장치 에뮬레이터는 사이트에 대해 구성된 장치 그룹에 따라 다릅니다. 여러 에뮬레이터를 장치 그룹에 할당할 수 있습니다. 그러면 컨텐츠 페이지에서 모든 에뮬레이터를 사용할 수 있습니다. 기본적으로 사이트에 할당된 첫 번째 장치 그룹에 할당된 첫 번째 에뮬레이터가 표시됩니다. 에뮬레이터는 페이지 맨 위에 있는 에뮬레이터 회전판을 통해 또는 사이드 킥의 편집 단추를 통해 전환할 수 있습니다.

**에뮬레이터 만들기**

에뮬레이터를 만들려면 일반 에뮬레이터 페이지에서 [사용자 지정 모바일 에뮬레이터 만들기](/help/sites-developing/emulators.md) 섹션을 참조하십시오.

**모바일 에뮬레이터의 주요 특성**

* 장치 그룹은 다음 중 하나의 에뮬레이터로 구성됩니다.장치 그룹 구성 페이지(예:/etc/mobile/groups/touch에는 `jcr:content` 노드 아래에 `emulators` 속성이 포함되어 있습니다.
참고:동일한 에뮬레이터가 여러 장치 그룹에 속할 수는 있지만, 이것은 그다지 의미가 없습니다.

* 장치 그룹의 구성 대화 상자를 통해 `emulators` 속성은 원하는 에뮬레이터의 경로로 설정됩니다. 예: `/libs/wcm/mobile/components/emulators/iPhone4`.

* 에뮬레이터 구성 요소(예:`/libs/wcm/mobile/components/emulators/iPhone4`)가 기본 모바일 에뮬레이터 구성 요소를 확장합니다( `/libs/wcm/mobile/components/emulators/base`).

* 장치 그룹을 구성할 때 기본 모바일 에뮬레이터를 확장하는 모든 구성 요소를 선택할 수 있습니다. 따라서 사용자 정의 에뮬레이터를 쉽게 만들거나 확장할 수 있습니다.
* 편집 모드에서 요청 시 에뮬레이터 구현을 사용하여 페이지를 렌더링합니다.
* 페이지의 템플릿이 모바일 페이지 구성 요소를 사용하는 경우 에뮬레이터 기능은 모바일 페이지 구성 요소의 `head.jsp`을 통해 페이지에 자동으로 통합됩니다.

### 장치 그룹 {#device-groups}

모바일 장치 그룹은 장치 기능을 기반으로 모바일 장치의 세그멘테이션을 제공합니다. 장치 그룹은 작성 인스턴스에서 에뮬레이터 기반 작성을 수행하고 게시 인스턴스에서 올바른 컨텐츠 렌더링을 위해 필요한 정보를 제공합니다.작성자가 모바일 페이지에 콘텐츠를 추가하고 게시하면 게시 인스턴스에서 페이지를 요청할 수 있습니다. 거기에서 에뮬레이터 편집 보기 대신 구성된 장치 그룹 중 하나를 사용하여 컨텐츠 페이지가 렌더링됩니다. 장치 그룹 선택은 [모바일 장치 탐지](#devicedetection)에 따라 발생합니다. 그러면 일치하는 장치 그룹이 필요한 스타일 정보를 제공합니다.

장치 그룹은 `/etc/mobile/devices` 아래의 컨텐츠 페이지로 정의되며, **모바일 장치 그룹** 템플릿을 사용합니다. 장치 그룹 템플릿은 컨텐츠 페이지 형태로 장치 그룹 정의에 대한 구성 템플릿으로 사용됩니다. 주요 특징은 다음과 같습니다.

* 위치: `/libs/wcm/mobile/templates/devicegroup`
* 허용되는 경로:`/etc/mobile/groups/*`
* 페이지 구성 요소:`wcm/mobile/components/devicegroup`

#### 사이트에 장치 그룹 할당 {#assigning-device-groups-to-your-site}

모바일 사이트를 만들 때 사이트에 장치 그룹을 할당해야 합니다. AEM은 장치의 HTML 및 JavaScript 렌더링 기능에 따라 세 개의 장치 그룹을 제공합니다.

* **** 기본 HTML을 지원하지만 이미지 및 JavaScript에 대한 지원은 없는 Sony Ericsson W800과 같은 기능 장치용 기능 전화.
* **** 스마트폰, 기본 HTML 및 이미지를 지원하는 Blackberry와 같은 장치의 경우 JavaScript는 지원되지 않습니다.

* **** HTML, 이미지, JavaScript 및 장치 회전을 완벽하게 지원하는 iPad와 같은 장치용 터치폰.

에뮬레이터는 장치 그룹과 연결할 수 있으므로([장치 그룹 만들기](#creating-a-device-group) 섹션 참조), 작성자가 사이트에 장치 그룹을 할당하면 장치 그룹과 연결된 에뮬레이터 중에서 선택하여 페이지를 편집할 수 있습니다.

사이트에 장치 그룹을 할당하려면

1. 브라우저에서 **Siteadmin** 콘솔로 이동합니다.
1. 모바일 사이트의 루트 페이지를 **웹 사이트** 아래에서 엽니다.
1. 페이지 속성을 엽니다.
1. **모바일** 탭을 선택합니다.

   * 장치 그룹을 정의합니다.
   * **확인**&#x200B;을 클릭합니다.

>[!NOTE]
>
>사이트에 대해 장치 그룹이 정의되면 사이트의 모든 페이지에서 해당 장치 그룹이 상속됩니다.

#### 장치 그룹 필터 {#device-group-filters}

장치 그룹 필터는 장치가 그룹에 속하는지 여부를 판별하는 기능 기반 기준을 정의합니다. 장치 그룹을 만들 때 장치 평가에 사용할 필터를 선택할 수 있습니다.

AEM이 장치로부터 HTTP 요청을 받는 런타임 시, 그룹과 연관된 각 필터는 장치 기능을 특정 기준과 비교합니다. 장치에 필터에 필요한 모든 기능이 있으면 해당 장치가 그룹에 속하는 것으로 간주됩니다. 기능은 WURFL™ 데이터베이스에서 검색됩니다.

장치 그룹은 기능 검색에 0개 이상의 필터를 사용할 수 있습니다. 또한 필터를 여러 장치 그룹과 함께 사용할 수 있습니다. AEM은 장치에 그룹에 대해 선택된 기능이 있는지 여부를 결정하는 기본 필터를 제공합니다.

* CSS
* JPG 및 PNG 이미지
* JavaScript
* 장치 회전

장치 그룹이 필터를 사용하지 않는 경우, 그룹에 대해 구성된 선택한 기능이 장치에 필요한 유일한 기능입니다.

자세한 내용은 [장치 그룹 필터 만들기](/help/sites-developing/groupfilters.md)를 참조하십시오.

#### 장치 그룹 {#creating-a-device-group} 만들기

AEM이 설치하는 그룹이 요구 사항을 충족하지 못할 경우 장치 그룹을 만듭니다.

1. 브라우저에서 **도구** 콘솔로 이동합니다.
1. **도구** > **모바일** > **장치 그룹** 아래에 새 페이지를 만듭니다. **페이지 만들기** 대화 상자에서 다음을 수행합니다.

   * **제목** (으)로 `Special Phones`를 입력합니다.

   * **이름**(으)로 `special`를 입력합니다.

   * **모바일 장치 그룹 템플릿**&#x200B;을 선택합니다.
   * **만들기**&#x200B;를 클릭합니다.

1. CRXDE에서 `/etc/mobile/groups/special` 노드 아래에 장치 그룹의 스타일이 들어 있는 **static.css** 파일을 추가합니다.

1. **특수 전화** 페이지를 엽니다.
1. 장치 그룹을 구성하려면 **설정** 옆의 **편집** 단추를 클릭합니다.
**일반** 탭에서 다음을 수행합니다.

   * **제목**:모바일 장치 그룹의 이름입니다.
   * **설명**:그룹에 대한 설명입니다.
   * **User-Agent**:장치가 일치하는 사용자 에이전트 문자열입니다. 선택 사항이며 정규 표현식이 될 수 있습니다. 예: `BlackBerryZ10`
   * **기능**:그룹이 이미지, CSS, JavaScript 또는 장치 순환을 처리할 수 있는지 여부를 정의합니다.
   * **최소 화면 너비****및 높이**
   * **에뮬레이터 사용 안 함**:컨텐츠 편집 중에 에뮬레이터를 활성화/비활성화합니다.

   **에뮬레이터** 탭에서 다음을 수행합니다.

   * **에뮬레이터**:이 장치 그룹에 할당된 에뮬레이터를 선택합니다.

   **필터** 탭에서 다음을 수행합니다.

   * 필터를 추가하려면 항목 추가 를 클릭하고 드롭다운 목록에서 필터를 선택합니다.
   * 필터는 표시된 순서대로 평가됩니다. 장치가 필터 기준을 충족하지 않으면 목록의 후속 필터가 평가되지 않습니다.



1. 확인을 클릭합니다.

모바일 장치 그룹 구성 대화 상자의 모양은 다음과 같습니다.

![screen_shot_2012-02-01at22043pm](assets/screen_shot_2012-02-01at22043pm.png)

#### 장치 그룹당 사용자 지정 CSS {#custom-css-per-device-group}

앞에서 설명한 바와 같이, 디자인 페이지의 CSS와 마찬가지로 사용자 지정 CSS를 장치 그룹 페이지와 연결할 수 있습니다.이 CSS는 페이지 컨텐츠의 작성자와 게시 시 장치 그룹별 렌더링에 영향을 주는 데 사용됩니다.그러면 이 CSS가 자동으로 포함됩니다.

* 이 장치 그룹에서 사용하는 모든 에뮬레이터에 대한 작성자 인스턴스의 페이지에 있습니다.
* 요청의 사용자 에이전트가 이 특정 장치 그룹의 모바일 장치와 일치하는 경우 게시 인스턴스의 페이지에 있습니다.

## 서버측 장치 탐지 {#server-side-device-detection}

필터 및 장치 사양 라이브러리를 사용하여 HTTP 요청을 수행하는 장치의 기능을 결정합니다.

### 장치 그룹 필터 개발 {#develop-device-group-filters}

장치 그룹 필터를 만들어 장치 기능 요구 사항 집합을 정의합니다. 필요한 장치 기능 그룹을 타깃팅하는 데 필요한 만큼 필터를 만듭니다.

필터를 디자인하여 필터 조합을 사용하여 기능 그룹을 정의할 수 있습니다. 일반적으로 서로 다른 장치 그룹의 기능이 겹칩니다. 따라서 여러 장치 그룹 정의가 있는 일부 필터를 사용할 수 있습니다.

필터를 만든 후 그룹 구성에서 사용할 수 있습니다.

자세한 내용을 보려면 [장치 그룹 필터 만들기](/help/sites-developing/groupfilters.md)로 이동하십시오.

### WURFL™ 데이터베이스 {#using-the-wurfl-database} 사용

AEM에서는 잘린 버전의 [WURFL](https://wurfl.sourceforge.net/)™ 데이터베이스를 사용하여 장치의 사용자 에이전트를 기반으로 화면 해상도 또는 javascript 지원과 같은 장치 기능을 쿼리합니다.

WURFL™ 데이터베이스의 XML 코드는 `/libs/wcm/mobile/devicespecs/wurfl.xml.`에서 `wurfl.xml`파일을 구문 분석하여 `/var/mobile/devicespecs` 아래의 노드로 표시됩니다. 노드에 대한 확장은 `cq-mobile-core` 번들이 처음 시작될 때 발생합니다.

장치 기능은 노드 속성으로 저장되고 노드는 장치 모델을 나타냅니다. 쿼리를 사용하여 장치 또는 사용자 에이전트의 기능을 검색할 수 있습니다.

WURFL™ 데이터베이스가 진화하고 있으므로 사용자 정의하거나 바꿔야 할 수 있습니다. 모바일 장치 데이터베이스를 업데이트하려면 다음 옵션이 있습니다.

* 이 사용을 허용하는 라이센스가 있는 경우 파일을 최신 버전으로 바꾸십시오. 다른 WURFL 데이터베이스 설치를 참조하십시오.
* AEM에서 사용할 수 있는 버전을 사용하고 사용자-에이전트 문자열과 일치하고 기존 WURFL™ 장치를 가리키는 regexp를 구성합니다. [regexp 기반 사용자 에이전트 일치 추가](#adding-a-regexp-based-user-agent-matching)를 참조하십시오.

#### 사용자-에이전트의 WURFL™ 기능에 매핑 {#testing-the-mapping-of-a-user-agent-to-wurfl-capabilities} 테스트

장치가 모바일 사이트에 액세스하면 AEM에서 장치를 감지하여 기능에 따라 장치 그룹에 매핑하고 장치 그룹에 해당하는 페이지 보기를 보냅니다. 일치하는 장치 그룹은 필요한 스타일 정보를 제공합니다. 매핑은 모바일 사용자 에이전트 테스트 페이지에서 테스트할 수 있습니다.

`https://localhost:4502/etc/mobile/useragent-test.html`

#### 다른 WURFL™ 데이터베이스 설치 {#installing-a-different-wurfl-database}

AEM과 함께 설치된 잘린 WURFL™ 데이터베이스는 사전 날짜를 갖는 릴리스입니다
2011년 8월 30일 WURFL 버전이 2011년 8월 30일 이후에 릴리스된 경우, 사용이 라이센스를 준수하는지 확인하십시오.

WURFL™ 데이터베이스를 설치하려면

1. CRXDE Lite에서 다음 폴더를 만듭니다.`/apps/wcm/mobile/devicespecs`
1. WURFL™ 파일을 폴더에 복사합니다.
1. 파일 이름을 `wurfl.xml`로 변경합니다.

AEM은 자동으로 `wurfl.xml` 파일을 구문 분석하고 `/var/mobile/devicespecs` 아래의 노드를 업데이트합니다.

>[!NOTE]
>
>전체 WURFL™ 데이터베이스를 사용하는 경우 구문 분석 및 활성화는 몇 분 정도 걸릴 수 있습니다. 로그에서 진행 정보를 확인할 수 있습니다.

#### regexp 기반 사용자-에이전트 일치 추가 {#adding-a-regexp-based-user-agent-matching}

기존 WURFL™ 장치 유형을 가리키도록 사용자 에이전트를 /apps/wcm/mobile/devicespecs/wurfl/regexp 아래의 정규 표현식으로 추가합니다.

1. **CRXDE Lite**&#x200B;에서 /apps/wcm/mobile/devicespecs/regexp 아래에 노드를 만듭니다(예: apple_ipad_ver1).
1. 노드에 다음 속성을 추가합니다.

   * **regexp**:사용자 에이전트를 정의하는 정규 표현식(예:.*Mozilla.*iPad.*AppleWebKit.*Safari.*
   * **deviceId**:wurfl.xml에 정의된 장치 ID(예:apple_ipad_ver1

위의 구성으로 인해 User-Agent가 제공된 정규 표현식과 일치하는 장치가 apple_ipad_ver1 WURFL™ 장치 ID가 있는 경우 매핑됩니다.

## 클라이언트측 장치 탐지 {#client-side-device-detection}

이 섹션에서는 페이지 렌더링을 최적화하거나 클라이언트에 대체 웹 사이트 버전을 제공하기 위해 AEM의 장치 클라이언트측 검색을 사용하는 방법에 대해 설명합니다.

AEM은 `BrowserMap`을 기반으로 장치 클라이언트측 감지를 지원합니다. `BrowserMap` 는 아래의 클라이언트 라이브러리로 AEM에 제공됩니다  `/etc/clientlibs/browsermap`.

`BrowserMap` 는 클라이언트에 대체 웹 사이트를 제공하는 데 사용할 수 있는 세 가지 전략을 제공하며, 이 전략은 다음 순서로 사용됩니다.

1. [대체 링크](#providing-alternate-links)
1. [장치 그룹별 URL](#definingdevicegroupspecificurl)
1. [선택기 기반 URL](#defining-selector-based-urls)

>[!NOTE]
>
>클라이언트 라이브러리 통합에 대한 자세한 내용은 [클라이언트측 HTML 라이브러리 사용](/help/sites-developing/clientlibs.md) 섹션을 참조하십시오.

### 대체 링크 제공 {#providing-alternate-links}

`PageVariantsProvider` OSGi 서비스는 동일한 패밀리에 속하는 사이트에 대한 대체 링크를 생성할 수 있습니다. 서비스에서 고려할 사이트를 구성하려면 `cq:siteVariant` 노드를 사이트 루트에서 `jcr:content` 노드에 추가해야 합니다.

`cq:siteVariant` 노드에는 다음 속성이 있어야 합니다.

* `cq:childNodesMapTo` - 자식 노드가 매핑될 링크 요소의 속성을 결정합니다.루트 노드의 하위 항목이 글로벌 웹 사이트의 언어 변형에 대한 루트(예: `/content/mysite/en`,  `/content/mysite/de`). 여기서 의 값은  `cq:childNodesMapTo`   `hreflang`.
* `cq:variantDomain` - 페이지  `Externalizer` 변형 절대 URL을 생성하는 데 사용할 도메인을 나타냅니다.이 값이 설정되지 않으면 페이지 변형이 상대 링크를 사용하여 생성됩니다.
* `cq:variantFamily` - 이 사이트가 속한 웹 사이트 제품군을 나타냅니다.동일한 웹 사이트의 여러 장치 특정 표현 기능은 동일한 패밀리에 속해야 합니다.
* `media` - 링크 요소의 미디어 속성 값을 저장합니다.라이브러리는 자동으로 클라이언트를 웹 사이트의 올바른  `BrowserMap` 변형에  `DeviceGroups`전달할 수 있도록  `BrowserMap` 등록된 이름을 사용하는 것이 좋습니다.

#### PageVariantsProvider 및 Externalizer {#pagevariantsprovider-and-externalizer}

`cq:siteVariant` 노드의 `cq:variantDomain` 속성 값이 비어 있지 않으면 `PageVariantsProvider` 서비스는 `Externalizer` 서비스에 대해 구성된 도메인으로 이 값을 사용하여 절대 링크를 생성합니다. 설정을 반영하도록 `Externalizer` 서비스를 구성해야 합니다.

>[!NOTE]
>
>AEM을 사용하여 작업하는 경우 이러한 서비스에 대한 구성 설정을 관리하는 방법에는 몇 가지가 있습니다.자세한 내용 및 권장 방법은 [OSGi](/help/sites-deploying/configuring-osgi.md) 구성 을 참조하십시오.

### 장치 그룹 특정 URL 정의 {#defining-a-device-group-specific-url}

대체 링크를 사용하지 않으려면 각 `DeviceGroup`에 대한 글로벌 URL을 구성할 수 있습니다. `browsermap.standard` 클라이언트 라이브러리를 포함하고 장치 그룹을 다시 정의하는 클라이언트 라이브러리를 만드는 것이 좋습니다.

BrowserMap은 사용자 지정된 클라이언트 라이브러리의 `BrowserMap` 개체에 동일한 이름의 새 장치 그룹을 만들고 추가하여 장치 그룹 정의를 덮어쓸 수 있도록 설계되었습니다.

>[!NOTE]
>
>자세한 내용은 [사용자 지정된 BrowserMap](#creatingacustomisedbrowsermap) 섹션을 참조하십시오.

### 선택기 기반 URL 정의 {#defining-selector-based-urls}

`BrowserMap`에 대한 대체 사이트를 나타내기 위해 이전 메커니즘을 사용하지 않은 경우 `DeviceGroups` 이름을 사용할 선택기가 `URL`s에 추가됩니다. 이 경우 요청을 처리할 자체 서블릿을 제공해야 합니다.

예를 들어, BrowserMap에서 `smartphone`로 식별된 `www.example.com/index.html`을 검색하는 장치가 `www.example.com/index.smartphone.html.`에 전달됩니다

### 페이지에서 BrowserMap 사용 {#using-browsermap-on-your-pages}

페이지에서 표준 BrowserMap 클라이언트 라이브러리를 사용하려면 페이지의 `head` 섹션에 `cq:include`태그를 사용하여 `/libs/wcm/core/browsermap/browsermap.jsp` 파일을 포함해야 합니다.

```xml
<cq:include script="/libs/wcm/core/browsermap/browsermap.jsp" />
```

`BrowserMap` 클라이언트 라이브러리를 `JSP` 파일에 추가하는 것 외에, 웹 사이트의 루트 아래에 `jcr:content` 노드에 `cq:deviceIdentificationMode` 문자열 속성을 추가해야 합니다.`client-side`

### BrowserMap의 기본 동작 {#overriding-browsermap-s-default-behaviour} 재정의

`BrowserMap` 을(를) 사용자 정의하거나 `DeviceGroups` 프로브를 더 추가하려면 `browsermap.standard`클라이언트측 라이브러리를 포함하는 고유한 클라이언트측 라이브러리를 만들어야 합니다.

또한 `JavaScript` 코드에서 `BrowserMap.forwardRequest()` 메서드를 수동으로 호출해야 합니다.

>[!NOTE]
>
>클라이언트 라이브러리 통합에 대한 자세한 내용은 [클라이언트측 HTML 라이브러리 사용](/help/sites-developing/clientlibs.md) 섹션을 참조하십시오.

사용자 지정된 `BrowserMap` 클라이언트 라이브러리를 만들면 다음 방법을 권장합니다.

1. 응용 프로그램에서 `browsermap.jsp` 파일을 만듭니다

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

1. 헤드 섹션에 `broswermap.jsp` 파일을 포함하십시오.

   ```xml
   <cq:include script="browsermap.jsp" />
   ```

### 특정 페이지에서 BrowserMap 제외 {#excluding-browsermap-from-certain-pages}

클라이언트 감지가 필요하지 않은 일부 페이지에서 BrowserMap 라이브러리를 제외하려면 요청 속성을 추가할 수 있습니다.

```xml
<%
request.setAttribute("browsermap.enabled", false);
%>
```

이렇게 하면 `/libs/wcm/core/browsermap/browsermap.jsp` 스크립트가 `BrowserMap` 이 검색을 수행하지 않도록 하는 메타 태그를 페이지에 추가합니다.

```xml
<meta name="browsermap.enabled" content="false">
```

### 웹 사이트의 특정 버전 테스트 {#testing-a-specific-version-of-a-web-site}

일반적으로 BrowserMap 스크립트는 항상 방문자를 항상 가장 적합한 웹 사이트 버전으로 리디렉션하며 일반적으로 필요할 때 방문자를 데스크탑 또는 모바일 사이트로 리디렉션합니다.

URL에 `device` 매개 변수를 추가하여 특정 버전의 웹 사이트를 테스트하기 위해 어떤 요청이든 해당 장치가 강제 적용할 수 있습니다. 다음 URL은 Geometrixx Outdoors 웹 사이트의 모바일 버전을 렌더링합니다.

`https://localhost:4502/content/geometrixx-outdoors/en.html?wcmmode=disabled&device=smartphone`

>[!NOTE]
>
>게시 인스턴스의 동작을 시뮬레이션하기 위해 `wcmmode` 매개 변수가 `disabled` 로 설정되어 있습니다.

전반적인 장치 값은 쿠키에 저장되므로 각 `URL`에 `device` 매개 변수를 추가하지 않고 웹 사이트를 검색할 수 있습니다.

따라서 웹 사이트의 데스크탑 버전으로 돌아가려면 `device` 를 `browser`로 설정한 동일한 `URL`을 호출해야 합니다.

>[!NOTE]
>
>BrowserMap은 잘못된 장치 값을 `BMAP_device` 쿠키에 저장합니다. 이 쿠키를 삭제하면 CQ에서 현재 장치(예: 데스크탑 또는 모바일)에 따라 적절한 버전의 웹 사이트가 제공됩니다.

## 모바일 요청 처리 {#mobile-request-processing}

AEM은 터치 장치 그룹에 속하는 모바일 장치에서 발생한 요청을 다음과 같이 처리합니다.

1. iPad에서 AEM 게시 인스턴스에 요청을 보냅니다(예: ).`https://localhost:4503/content/geometrixx_mobile/en/products.html`
1. AEM은 요청한 페이지의 사이트가 모바일 사이트인지 여부를 결정합니다(첫 번째 수준 페이지 `/content/geometrixx_mobile`이 모바일 페이지 구성 요소를 확장하는지 여부를 확인하여). 예:
1. AEM은 요청 헤더에서 사용자-에이전트를 기반으로 장치 기능을 조회합니다.
1. AEM은 장치 기능을 장치 그룹에 매핑하고 `touch` 을 장치 그룹 선택기로 설정합니다.
1. AEM이 요청을 `https://localhost:4503/content/geometrixx_mobile/en/products.touch.html.`(으)로 리디렉션합니다.
1. AEM에서 iPad로 응답을 전송합니다.

   * `products.touch.html` 는 일반적인 방법으로 렌더링되며, 분리할 수 있습니다.
   * 렌더링 구성 요소는 선택기를 사용하여 프레젠테이션을 조정합니다.
   * AEM은 자동으로 모바일 선택기를 페이지의 모든 내부 링크에 추가합니다.

### 통계 {#statistics}

모바일 장치별로 AEM 서버에 수행된 요청 수에 대한 통계를 확인할 수 있습니다. 요청 수를 분류할 수 있습니다.

* 장치 그룹 및 장치당
* 연간

통계를 보려면

1. **도구** 콘솔로 이동합니다.
1. **장치 통계** 페이지를 **도구** > **모바일** 아래에 엽니다.
1. 특정 연도, 월 또는 일에 대한 통계를 보려면 링크를 클릭합니다.

**통계** 페이지는 다음과 같습니다.

![screen_shot_2012-02-01at24353pm](assets/screen_shot_2012-02-01at24353pm.png)

>[!NOTE]
>
>**통계** 페이지는 모바일 장치가 AEM에 처음 액세스하고 감지될 때 생성됩니다. 그 전에는 사용할 수 없습니다.

통계에서 항목을 생성해야 하는 경우 다음과 같이 진행할 수 있습니다.

1. 모바일 장치나 에뮬레이터(예: Firefox의 경우 https://chrispederick.com/work/user-agent-switcher/)을 사용합니다.
1. 작성 모드를 비활성화하여 작성자 인스턴스에서 모바일 페이지를 요청합니다(예:
   `https://localhost:4502/content/geometrixx_mobile/en/products.html?wcmmode=disabled`

이제 **통계** 페이지를 사용할 수 있습니다.

### &quot;친구에게 링크 보내기&quot;에 대한 페이지 캐싱 지원 링크 {#supporting-page-caching-for-send-link-to-a-friend-links}

장치 그룹에 대해 렌더링되는 페이지는 장치 그룹 선택기에 의해 페이지 URL에서 식별되므로 모바일 페이지는 일반적으로 Dispatcher에서 사용할 수 있습니다(예: `/content/mobilepage.touch.html`). 선택기가 없는 모바일 페이지에 대한 요청은 캐시되지 않습니다. 이 경우 장치 감지가 작동하여 일치하는 장치 그룹(또는 해당 문제에 대한 &quot;nomatch&quot;)으로 최종 리디렉션됩니다. 장치 그룹 선택기로 렌더링된 모바일 페이지는 링크 재기록기에 의해 처리되며, 이는 페이지 내의 모든 링크를 장치 그룹 선택기도 포함하도록 다시 기록하므로, 이미 자격이 있는 페이지에서 클릭할 때마다 장치 검색을 다시 수행하지 못합니다.

따라서 다음 시나리오가 발생할 수 있습니다.

사용자 Alice는 `coolpage.feature.html`으로 리디렉션되고 `touch` 장치 그룹에 속한 다른 클라이언트를 사용하여 해당 URL에 액세스하는 친구 Bob에게 해당 URL을 보냅니다.

프런트엔드 캐시에서 `coolpage.feature.html` 가 제공되는 경우 AEM이 모바일 선택기가 새 사용자-에이전트와 일치하지 않음을 확인하기 위한 요청을 분석할 수 없고 Bob이 잘못된 표현을 가져옵니다.

이를 해결하기 위해 페이지에 간단한 선택 UI를 포함할 수 있습니다. 이 UI는 최종 사용자가 AEM에서 선택한 장치 그룹을 재정의할 수 있습니다. 위의 예에서, 최종 사용자는 페이지의 링크(또는 아이콘)가 해당 장치가 충분하다고 판단되면 `coolpage.touch.html`로 전환할 수 있습니다.
