---
title: AEM Mobile 콘텐츠 개인화
seo-title: AEM Mobile 콘텐츠 개인화
description: AEM 작성자가 Adobe Target을 활용하여 모바일 앱 콘텐츠를 개인화할 수 있는 AEM Mobile 컨텐츠 개인화 기능에 대해 알려면 이 페이지를 따르십시오.
seo-description: AEM 작성자가 Adobe Target을 활용하여 모바일 앱 콘텐츠를 개인화할 수 있는 AEM Mobile 컨텐츠 개인화 기능에 대해 알려면 이 페이지를 따르십시오.
uuid: 9078edd1-8399-485f-8a63-a07e766f7ef9
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: c9c818dc-c5c4-4a96-94fe-9dc9fe75705b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '2701'
ht-degree: 1%

---


# AEM Mobile 콘텐츠 개인화{#aem-mobile-content-personalization}

>[!NOTE]
>
>단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: 응답)이 필요한 프로젝트에는 SPA 편집기를 사용하는 것이 좋습니다. [추가 정보](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>이 문서는 AEM Mobile 참조의 권장 시작점인 [AEM Mobile 시작](/help/mobile/getting-started-aem-mobile.md) 안내서의 일부입니다.

AEM Mobile 콘텐츠 개인화 기능을 사용하면 [AEM 작성자](#author)가 [Adobe Target](https://www.adobe.com/ca/marketing-cloud/testing-targeting.html)을(를) 활용하여 모바일 앱 콘텐츠를 개인화할 수 있습니다. 이를 통해 모바일 애플리케이션 사용자에게 타깃팅된 오퍼를 전달할 수 있습니다. Adobe Experience Manager Mobile은 사용자에게 개인 취향에 맞는 컨텐츠를 제공할 컨텐츠를 제작, 타깃팅 및 전달할 수 있는 기능을 제공합니다.

AEM에서와 마찬가지로 작성자가 이 컨텐츠를 만들기 시작하려면 관리자와 개발자가 먼저 환경을 준비해야 합니다.

[AEM ](#administrator) 관리자는 AEM Mobile과 Adobe Target Cloud Service 간의 연결을 설정해야 합니다.

한편 AEM Mobile [개발자는 타깃팅된 컨텐츠 작성을 용이하게 하기 위해 기존 스크립트를 수정해야 합니다.](#developer)

## 관리자의 경우 {#for-administrators}

컨텐츠 작성자가 모바일 앱에 대한 타깃팅된 컨텐츠를 생성하기 전에 먼저 몇 가지 단계를 수행해야 합니다.사용자 및 그룹에 대한 올바른 권한 집합, 클라우드 서비스 만들기, 활동에 대한 응용 프로그램 구성 및 마지막으로 컨텐츠를 생성하는 등 다양한 작업을 할 수 있습니다.

이 문서는 타게팅을 위해 [AEM Mobile 하이브리드 참조 응용 프로그램](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference)을 구성하는 데 사용되는 프로세스를 안내합니다.

앞으로는 AEM Mobile 하이브리드 참조 애플리케이션이 성공적으로 배포되고 AEM Mobile Dashboard를 통해 액세스할 수 있게 될 것으로 가정합니다.

작성자가 응용 프로그램 내에서 타깃팅된 컨텐츠를 생성하려면 먼저 AEM 인스턴스가 Adobe Target Cloud Service으로 [구성되어야 합니다.](/help/mobile/aem-mobile-configuring-cloud-service.md)

### 권한 {#permissions}

개인화 콘솔에 액세스해야 하는 사용자는 `target-activity-authors` 그룹의 일부여야 합니다.

사용자 및 그룹 설정의 일부로서 target-activity-group을 apps-admins 그룹에 추가해야 합니다. target-activity-authors 그룹을 추가하면 사용자가 개인화 탐색 메뉴 항목을 볼 수 있습니다.

>[!NOTE]
>
>개인화 관리 콘솔에 액세스할 사용자 또는 그룹을 target-activity-authors 그룹에 추가하지 않으면 사용자가 개인화 콘솔을 볼 수 없습니다.

### 클라우드 서비스 {#cloud-services}

모바일 애플리케이션을 위해 타깃팅된 컨텐츠를 작업하려면 다음 2개의 서비스를 구성해야 합니다.Adobe Target 서비스 및 Adobe 모바일 서비스. Adobe Target 서비스는 클라이언트 요청을 처리하고 개인화된 컨텐츠를 반환하기 위한 엔진을 제공합니다. Adobe Mobile Services 서비스는 AMS Cordova 플러그인에서 사용하는 ADBMobileConfig.json 파일을 통해 Adobe 서비스와 모바일 애플리케이션 간의 연결을 제공합니다. AEM Mobile Dashboard에서 두 서비스를 추가하여 애플리케이션을 구성할 수 있습니다.

AEM Mobile Dashboard에서 Cloud Services 관리를 찾아 + 단추를 클릭합니다.

![chlimage_1-38](assets/chlimage_1-38.png)

Cloud Service 추가 마법사에서 &quot;Adobe Target&quot; 클라우드 서비스 카드를 선택하고 다음을 클릭합니다.

![chlimage_1-39](assets/chlimage_1-39.png)

구성 선택 드롭다운에서 새 구성을 만들거나 기존 구성 중에서 선택할 수 있습니다. 새 구성을 만들려면 드롭다운에서 &quot;구성 만들기&quot;를 선택합니다. Target 구성의 제목을 입력합니다. Target 계정과 연결된 클라이언트 코드, 이메일 및 암호를 입력합니다. 이러한 필드에 대한 값을 모를 경우 Adobe Target 지원에 문의하십시오. &quot;확인&quot; 단추를 클릭하여 자격 증명을 확인합니다. 확인되면 [제출] 단추를 클릭하여 클라우드 서비스를 만듭니다.

>[!NOTE]
>
>생성되는 클라우드 서비스는 마법사를 통해 모바일 애플리케이션과 자동으로 연결됩니다. cq:cloudserviceconfigs 속성 값은 apps 그룹 노드의 jcr:content 노드에서 설정됩니다. 하이브리드 앱 샘플의 경우 /etc/cloudservices/testandtarget/adobe-target—aem-apps/framework에 있는 자동으로 생성된 프레임워크 노드를 가리키는 값이 /content/mobileapps/hybrid-reference-app/jcr:content에 설정됩니다. 프레임워크 노드에는 기본적으로 성별 및 연령 두 속성이 설정되어 있습니다. 프레임워크는 AEM 미리 보기에서만 사용되며 장치에 영향을 주지 않습니다.

마법사가 완료되면 Cloud Service 관리 타일에는 Target 클라우드 서비스가 포함되지만 누락된 Adobe Mobile Service 계정에 대한 경고가 포함됩니다.

![chlimage_1-40](assets/chlimage_1-40.png)

### Adobe Mobile Services {#adobe-mobile-services}

Adobe AMS(Mobile Services) 계정을 애플리케이션에 연결해야 할 뿐만 아니라 AMS 서비스는 Target 클라이언트 코드 정보가 포함된 필수 ADBMobileConfig.json 파일을 제공합니다. AMS 계정과의 연결을 만들기 전에 AMS에 대한 권한이 있는 사용자가 AMS 계정을 수정해야 합니다.

### 클라이언트 코드 {#client-code}

AMS 서비스에 로그인하려면 [https://mobilemarketing.adobe.com](https://mobilemarketing.adobe.com/)을 방문하여 모바일 응용 프로그램을 선택하고 설정을 클릭합니다. SDK Target 옵션 필드를 찾아 클라이언트 코드를 필드에 입력하고 저장을 클릭합니다.

![chlimage_1-41](assets/chlimage_1-41.png)

이제 클라이언트 코드가 모바일 애플리케이션과 연결되었으므로 AMS 클라우드 서비스가 Adobe Mobile Dashboard를 통해 구성되면 서비스 설정에 대한 설정이 ADBMobileConfig.json 파일을 통해 전달됩니다.

### Adobe 모바일 서비스 Cloud Service {#adobe-mobile-service-cloud-service}

이제 AMS가 구성되었으므로 이제 Adobe Mobile Dashboard에 모바일 애플리케이션을 연결할 때입니다. AEM Mobile Dashboard에서 Cloud Services 관리를 찾아 + 단추를 클릭합니다.

![chlimage_1-42](assets/chlimage_1-42.png)

Adobe Mobile Services 카드를 선택하고 [다음]을 클릭합니다.

![chlimage_1-43](assets/chlimage_1-43.png)

만들기 또는 선택 마법사 단계에서 Mobile Service 드롭다운을 선택하고 구성 만들기 항목을 선택합니다. 제목, 회사, 사용자 이름, 암호를 입력하고 적절한 데이터 센터를 선택합니다. 이러한 값을 모를 경우 Adobe Mobile Service 관리자에게 문의하여 얻으십시오. 모든 필드가 채워지면 [확인] 단추를 클릭합니다. 확인 프로세스는 AMS로 이동하여 계정에 대한 자격 증명을 확인하며, 확인 작업이 성공적으로 완료되면 드롭다운에서 관련 모바일 응용 프로그램을 선택하는 모바일 응용 프로그램 목록이 채워집니다. 전송 단추를 클릭하여 마법사를 완료합니다. 이 프로세스에서는 구성 데이터 및 응용 프로그램과 연관된 분석을 얻는 데 시간이 다소 걸릴 수 있습니다. 프로세스가 완료되면 모달에서 완료 단추를 클릭하여 Adobe Mobile Dashboard로 돌아갑니다.

Mobile Dashboard로 다시 돌아오면 Cloud Services 관리 타일에 AMS 클라우드 서비스가 포함됩니다. 또한 지표 분석 타일은 라이프사이클 보고서로 채워집니다.

![chlimage_1-44](assets/chlimage_1-44.png)

## 작성자 {#for-authors}

**사전 요구 사항:** 위에서 설명한 바와 같이 작성자가 새로운 타깃팅된 컨텐츠를 생성하기 전에 관리자는 Adobe Target 서비스에 대한 연결을 구성해야 합니다.

관리자가 2개의 클라우드 서비스를 구성했고 개발자가 mobileappoffer 핸들러를 구성했으면 콘텐츠 작성자가 타깃팅된 경험을 생성하기 시작할 수 있습니다.

AEM Mobile 앱 내에서 타깃팅된 컨텐츠를 작성하는 방법은 AEM Sites 작성과 유사한 절차를 따릅니다.

AEM[에서 타깃팅된 컨텐츠 작성에 대한 전체 개요는 여기를 참조하십시오.](/help/sites-authoring/personalization.md)

## 개발자용 {#for-developers}

모바일 애플리케이션을 구축하는 AEM 개발자는 구성 요소를 개발할 때 AEM에서 일반적으로 사용하는 패턴을 지속적으로 따라야 합니다. 콘텐츠 작성자가 타깃팅된 컨텐츠를 만들 수 있도록 필요한 단계를 안내합니다.

### Adobe Target ContentSync 핸들러 {#adobe-target-contentsync-handlers}

AEM 컨텐츠 작성자가 만든 오퍼를 렌더링하여 컨텐츠를 사용자의 장치 컨텐츠로 전달하는 것이 생성됩니다. 대상 오퍼의 렌더링을 처리하기 위해 오퍼를 처리하는 새 컨텐츠 동기화 핸들러가 있습니다. 하이브리드 참조 응용 프로그램을 샘플로 사용하는 en(영어) 컨텐츠 패키지에는 [mobileappoffer](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/aem-package/content-author/src/main/content/jcr_root/content/mobileapps/hybrid-reference-app/en/_jcr_content/pge-app/app-config-dev/targetOffers/.content.xml) 핸들러가 있는 ContentSyncConfig가 들어 있습니다. 다음 단계는 오퍼를 장치에 렌더링하는 데 중요합니다. mobileappoffer 핸들러는 애플리케이션에 사용할 개인화 활동의 경로를 식별하는 경로 속성을 가집니다.

예를 들어 */content/campaigns/hybridref*&#x200B;에 위치한 활동이 있는 경우 이 경로를 복사하여 mobileappoffers 핸들러의 *path* 속성에 붙여 넣습니다.

>[!NOTE]
>
>하이브리드 참조 응용 프로그램의 경우 개발 및 제작용 Mobileprop 핸들러가 두 개 있습니다.

활동 경로가 mobileappoffers 핸들러의 경로 속성에 설정되면 핸들러가 저장됩니다. 이제 처리기가 모바일 장치에 대한 오퍼를 렌더링할 준비가 됩니다.

### 렌더링 모드 {#render-mode}

mobileappoffer 핸들러는 게시 및 개발 설정에 대해 다르게 구성됩니다. 게시 설정의 경우 cq:ContentSyncConfig 노드에 설정된 *publish* 값이 있는 *renderMode*&#x200B;라는 속성이 있습니다. mobileappoffer 핸들러는 renderMode를 참조하며, 게시로 설정된 경우 생성된 mbox id를 수정합니다. 기본적으로 AEM에서 만든 mbox에는 mbox id에 추가된 —author 값이 있습니다. 이것은 활동이 게시되지 않았으며 게시되지 않은 캠페인을 오퍼 해상도에 사용해야 함을 나타냅니다.

Adobe Mobile Dashboard를 통해 컨텐츠를 스테이징할 때 스테이지된 컨텐츠는 프로덕션 준비 컨텐츠로 간주되고 비개발 컨텐츠 동기화 구성을 통해 렌더링됩니다. 이렇게 렌더링하면 —author가 모든 mbox id에서 제거되고 게시된 활동을 Target 서버에서 사용할 수 있을 것으로 예상할 수 있습니다. 스테이지된 컨텐츠를 테스트하기 전에 활동이 게시되었는지 확인합니다.

### 개인화 앱 개발 {#personalization-app-development}

#### 구성 요소 {#components}

모든 컨텐츠의 기본 요소는 일반적으로 HTL 또는 JSP를 사용하는 경우에 따라 기본 AEM 페이지 구성 요소(wcm/foundation/components/page 또는 foundation/components/page) 중 하나를 확장하는 페이지 구성 요소입니다. 이러한 단계의 기간은 wcm/foundation/components/page 구성 요소 사용에 중점을 둡니다. 페이지 구성 요소의 기본 구조는 여러 스크립트로 분류되며, 각 스크립트는 개발자가 필요한 경우 코드를 구성하고 재정의할 수 있도록 하는 특정 목적을 제공합니다. Personalization에 관심 있는 두 개의 스크립트는 head.html 및 body.html입니다. 이 두 스크립트는 Context Hub, Cloud Services 및 모바일 저작을 지원하기 위해 코드를 삽입하는 영역을 제공합니다.

다음은 컨텐츠 타깃팅을 활성화하는 데 사용되는 두 개의 기본 스크립트에 대한 개요입니다.

#### head.html {#head-html}

작성자가 컨텐츠를 타깃팅할 수 있는 기능을 제공하려면 작성자가 편집 모드에서 타깃팅 모드로 컨텍스트를 변경할 수 있도록 타겟 메뉴를 페이지에 추가해야 합니다. 이 기능을 활성화하려면 개발자는 head.html의 위쪽 또는 &lt;title>&lt;/title> 요소에 가까운 다음 코드 조각을 포함하도록 head.html 스크립트를 수정해야 합니다.

```xml
<meta data-sly-test="${!wcmmode.disabled}">
    <div data-sly-call="${clientLib.all @ categories='personalization.kernel'}" data-sly-unwrap></div>
    <div data-sly-resource="${'config' @ resourceType='cq/personalization/components/clientcontext_optimized/config'}" data-sly-unwrap></div>
    <div data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}" data-sly-unwrap></div>
</meta>
```

>[!NOTE]
>
>WCM 모드가 비활성화되지 않은 경우에만 스크립트를 포함해야 합니다. 따라서 WCM 모드가 비활성화된 경우(자세한 내용은 ContentSync 핸들러 섹션 참조) 스크립트가 최종 애플리케이션 코드에 포함되지 않습니다.

작성자에게 타깃팅된 컨텐츠를 미리 볼 수 있는 기능을 제공하려면 편집자가 Adobe Target 클라우드 서비스의 구성을 찾아야 합니다. 아래의 코드 블록에는 두 개의 중요한 스크립트가 추가됩니다. 페이지에 연결된 Target 클라우드 서비스를 찾아 Adobe Target에 전화를 거는 기능을 추가하는 첫 번째 단계입니다. 두 번째는 cq.apps.targeting 카테고리의 추가입니다.

**cq.apps.targeting** 범주는 기본 cq/personalization/component/target 구성 요소를 대체하며 모바일 애플리케이션 소비를 위해 특별히 오퍼를 렌더링하는 mobileapps/components/target 구성 요소를 사용합니다. 자세한 내용은 Target 구성 요소 섹션에서 설명합니다.

이 코드는 head.html에 추가하고 &lt;/head> 요소의 끝 바로 앞에 배치해야 합니다.

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-include="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp" data-sly-unwrap></div>
    <meta data-sly-call="${clientLib.all @ categories='cq.apps.targeting'}" data-sly-unwrap></meta>
</div>
```

>[!NOTE]
>
>코드 블록은 WCM 모드 내에서 래핑되므로 컨텐츠 작성자가 컨텐츠를 만드는 작업을 하는 동안에만 재생됩니다. 클라우드 서비스 스크립트는 생성된 모바일 런타임 코드에 추가되지 않습니다.

#### body.html {#body-html}

내용 작성자가 다른 성격을 테스트할 수 있도록 body.html 스크립트에서 다음 코드 블록을 본문 요소의 첫 번째 자식으로 포함해야 합니다.

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-resource="${'clientcontext' @ resourceType='cq/personalization/components/clientcontext_optimized'}" data-sly-unwrap></div>
</div>
```

필요한 마지막 코드 비트는 body.html의 맨 아래에 있습니다. 이 비트는 연결된 클라우드 서비스를 찾고 적절한 타깃팅 엔진 코드를 삽입합니다.

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-resource="${'cloudservices' @ resourceType='cq/cloudserviceconfigs/components/servicecomponents'}" data-sly-unwrap></div>
</div>
```

### 참조 응용 프로그램 {#reference-application}

head.html 및 body.html의 예는 두 스크립트 내에 스크립트 블록을 배치할 개발자를 보여주는 [AEM Mobile 하이브리드 참조 응용 프로그램](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference)에서 찾을 수 있습니다.

### 콘텐츠 동기화 핸들러 {#content-sync-handlers}

컨텐츠 작성자가 모바일 응용 프로그램용 컨텐츠 작성을 마쳤으면 다음 단계는 소스를 다운로드하고 응용 프로그램을 빌드하거나 게시할 컨텐트를 스테이징하는 것입니다. 개발자가 이러한 작업을 수행하는 데 관여하는 여러 단계가 있습니다. 컨텐츠 렌더링에 도움이 되도록 AEM Mobile은 컨텐츠 동기화 핸들러를 사용하여 컨텐츠를 렌더링하고 패키징합니다. 타깃팅된 컨텐츠를 렌더링하기 위해 개인화 사용 사례에 대해 새로운 컨텐츠 동기화 핸들러가 도입되었습니다. &#39;mobileappoffers&#39; 핸들러는 컨텐츠 작성자가 만든 관련 대상 오퍼를 렌더링하는 방법을 알고 있습니다. mobileappoffer 핸들러는 추상 페이지 업데이트 핸들러를 확장하므로 대부분의 속성이 유사합니다. mobileappoffer 핸들러의 세부 사항에는 다음 속성이 있습니다.

<table>
 <tbody>
  <tr>
   <td><strong>속성</strong></td>
   <td><strong>값</strong></td>
   <td><strong>설명</strong></td>
  </tr>
  <tr>
   <td>다시 쓰기</td>
   <td>+ relativeParentPath<p> - "/"</p> </td>
   <td>rewrite 속성은 컨텐츠 내의 경로를 다시 작성할 방법을 식별합니다.</td>
  </tr>
  <tr>
   <td>includedPageTypes</td>
   <td><p>"cq/personalization/components/teaserpage",</p> <p>"cq/personalization/components/offerproxy"</p> </td>
   <td>includePageTypes 속성은 선택 사항이며 cq/personalization/components/teaserpage 및 cq/personalization/components/offerproxy 리소스 유형이 있는 페이지로 기본 설정됩니다. 이러한 두 리소스 유형은 컨텐츠를 타깃팅할 때 사용되는 기본 리소스 유형입니다. 추가 리소스 유형을 지원해야 하는 경우 includePageTypes 목록에 추가해야 합니다.</td>
  </tr>
  <tr>
   <td>locationRoot</td>
   <td>/content/mobileapps/&lt;app&gt;</td>
   <td>앱의 위치입니다.</td>
  </tr>
  <tr>
   <td>유형</td>
   <td>mobileappoffers</td>
   <td>mobileappoffer인 핸들러의 이름입니다.</td>
  </tr>
  <tr>
   <td>selector</td>
   <td>tandt</td>
   <td>tandt 선택기는 타깃팅된 컨텐츠를 렌더링하는 데 사용됩니다. </td>
  </tr>
  <tr>
   <td>targetRootDirectory</td>
   <td>www</td>
   <td>렌더링된 내용을 유지할 루트 디렉토리.</td>
  </tr>
  <tr>
   <td>includeImages</td>
   <td>true | false</td>
   <td>true이면 오퍼에 포함된 이미지가 렌더링됩니다. 잘못된 이미지를 건너뜁니다.</td>
  </tr>
  <tr>
   <td>includeVideos</td>
   <td>true | false</td>
   <td>true이면 오퍼에 포함된 비디오가 렌더링됩니다. 잘못된 비디오를 건너뜁니다.</td>
  </tr>
  <tr>
   <td>경로</td>
   <td>/content/campaigns/&lt;브랜드&gt;</td>
   <td>오퍼가 참여하는 캠페인의 브랜드를 가리킵니다. 현재 모든 오퍼는 동일한 캠페인에서 가져와야 합니다.</td>
  </tr>
  <tr>
   <td>깊이</td>
   <td>true | false</td>
   <td>true로 설정하면 모든 하위 페이지가 재귀적으로 렌더링됩니다. false로 재귀하지 않으면 </td>
  </tr>
  <tr>
   <td>extension</td>
   <td>html</td>
   <td>렌더링되는 리소스의 확장을 설정합니다. 페이지의 확장명이 .html이 되도록 html로 설정합니다.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>[AEM Mobile 하이브리드 참조 앱](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference)에는 기본 mobileappoffer 핸들러 구성이 있습니다. 샘플의 경로 속성은 캠페인 위치에 따라 다르므로 비어 있습니다. 캠페인 작성자가 캠페인을 만든 후 앱 관리자는 캠페인을 가리키는 경로 속성을 지정하여 캠페인을 핸들러와 연결해야 합니다.

### Target 구성 요소 {#target-component}

모바일 애플리케이션용으로 컨텐츠를 렌더링하는 데 도움이 되도록 AEM Mobile은 mobileapps/components/target 구성 요소를 사용합니다. 모바일 대상 구성 요소는 cq/personalization/components/target 구성 요소를 확장하고 engine_tnt.jsp 스크립트를 무시합니다. 이렇게 engine_tnt.jsp를 재정의하여 AEM Mobile은 모바일 앱 사용 사례에 대해 생성된 HTML을 제어할 수 있습니다. 컨텐츠 작성자가 타깃팅하는 모든 구성 요소에 대해 engine_tnt.jsp에 연결된 mbox가 만들어집니다.

각 mbox에 대해 **cq-targeting** 속성이 추가되어 애플리케이션 개발자가 사용자 지정 코드를 작성하여 사용할 수 있지만 원하는 대로 사용할 수 있습니다. [AEM Mobile 하이브리드 참조 앱](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference)에는 cq-targeting 특성을 사용하는 Angular 지시문의 예가 있습니다. 컨텐츠 교체 시기 및 작업 방식은 모바일 애플리케이션 개발자에게 매우 중요합니다. Adobe 타깃팅 서비스를 호출하는 데 API를 제공하는 AEM /etc/clientlibs/mobileapps/js/mobileapps.js을 통해 제공되는 Mobile SDK가 있습니다. 응용 프로그램 개발자는 응용 프로그램의 디자인에 따라 해당 호출이 언제 수행되어야 하는지 지정하는 것이 중요합니다.

## 다음 소개{#what-s-next}

1. [AEM Mobile 앱 경험 시작](/help/mobile/starting-aem-phonegap-app.md)
1. [앱 콘텐츠 관리](/help/mobile/phonegap-manage-app-content.md)
1. [내 애플리케이션 빌드](/help/mobile/building-app-mobile-phonegap.md)
1. [Adobe Mobile Analytics를 사용하여 앱 성능 추적](/help/mobile/phonegap-intro-to-app-analytics.md)
1. [Adobe Target을 통해 개인화된 앱 경험 제공](/help/mobile/phonegap-aem-mobile-content-personalization.md)
1. [사용자에게 중요 메시지 보내기](/help/mobile/phonegap-push-notifications.md)
