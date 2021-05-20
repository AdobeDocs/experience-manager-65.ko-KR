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
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '2701'
ht-degree: 1%

---


# AEM Mobile 컨텐츠 개인화{#aem-mobile-content-personalization}

>[!NOTE]
>
>단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: React)이 필요한 프로젝트에 SPA 편집기를 사용하는 것이 좋습니다. [추가 정보](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>이 문서는 AEM Mobile 참조의 권장 시작점인 [AEM Mobile 시작하기](/help/mobile/getting-started-aem-mobile.md) 안내서의 일부입니다.

AEM Mobile 컨텐츠 개인화 기능을 사용하면 [AEM 작성자](#author)가 [Adobe Target](https://www.adobe.com/ca/marketing-cloud/testing-targeting.html)을 활용하여 모바일 앱 콘텐츠를 개인화할 수 있습니다. 이를 통해 모바일 애플리케이션 사용자에게 타깃팅된 오퍼를 전달할 수 있습니다. Adobe Experience Manager Mobile은 사용자에게 개인 취향에 맞는 콘텐츠를 제공할 컨텐츠를 만들고, 타깃팅하고, 전달하는 기능을 제공합니다.

AEM에서는 일반적으로 작성자가 이 컨텐츠를 만들려면 먼저 관리자와 개발자가 환경을 준비해야 합니다.

[AEM ](#administrator) 관리자는 AEM Mobile과 Adobe Target Cloud Service 간에 연결을 설정해야 합니다.

한편 AEM Mobile [개발자는 타깃팅된 컨텐츠 작성을 용이하게 하기 위해 기존 스크립트를 수정해야 합니다.](#developer)

## 관리자용 {#for-administrators}

컨텐츠 작성자가 모바일 앱용 타깃팅된 컨텐츠를 생성하기 전에 먼저 서로 협력해야 하는 많은 단계가 있습니다.사용자 및 그룹에 대한 올바른 권한 세트를 가져오고, 클라우드 서비스를 만들고, 활동에 대한 애플리케이션을 구성하고, 마지막으로 컨텐츠를 생성합니다.

이 문서에서는 타깃팅을 위해 [AEM Mobile Hybrid 참조 응용 프로그램](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference)을 구성하는 데 사용되는 프로세스를 안내합니다.

앞으로 AEM Mobile 하이브리드 참조 애플리케이션이 AEM Mobile 대시보드를 통해 성공적으로 배포되고 액세스할 수 있게 됩니다.

작성자가 애플리케이션 내에서 타깃팅된 컨텐츠를 생성하려면 먼저 AEM 인스턴스가 [Adobe Target Cloud Service으로 구성되어 있어야 합니다.](/help/mobile/aem-mobile-configuring-cloud-service.md)

### 권한 {#permissions}

개인화 콘솔에 액세스해야 하는 사용자는 `target-activity-authors` 그룹의 일부여야 합니다.

사용자 및 그룹 설정의 일부로 target-activity-group을 apps-admins 그룹에 추가해야 하는 것이 좋습니다. target-activity-authors 그룹을 추가하면 사용자가 개인화 탐색 메뉴 항목을 볼 수 있습니다.

>[!NOTE]
>
>개인화 Admin Console에 액세스할 사용자 또는 그룹을 target-activity-authors 그룹에 추가하지 않으면 사용자가 개인화 콘솔을 볼 수 없습니다.

### 클라우드 서비스 {#cloud-services}

모바일 애플리케이션에서 타깃팅된 컨텐츠를 작업하려면 다음 두 가지 서비스를 구성해야 합니다.Adobe Target 서비스 및 Adobe Mobile Services 서비스. Adobe Target 서비스는 클라이언트 요청을 처리하고 개인화된 콘텐츠를 반환하는 엔진을 제공합니다. Mobile Services Adobe 서비스는 AMS Cordova 플러그인에서 사용하는 ADBMobileConfig.json 파일을 통해 Adobe 서비스와 모바일 애플리케이션 간의 연결을 제공합니다. AEM Mobile 대시보드에서 두 서비스를 추가하여 애플리케이션을 구성할 수 있습니다.

AEM Mobile 대시보드에서 Cloud Services 관리 을 찾아 + 단추를 클릭합니다.

![chlimage_1-38](assets/chlimage_1-38.png)

Cloud Service 추가 마법사에서 &quot;Adobe Target&quot; 클라우드 서비스 카드를 선택하고 다음을 클릭합니다.

![chlimage_1-39](assets/chlimage_1-39.png)

구성 선택 드롭다운에서 새 구성을 만들거나 기존 구성 중에서 선택할 수 있습니다. 새 구성을 만들려면 드롭다운에서 &quot;구성 만들기&quot;를 선택합니다. Target 구성의 제목을 입력합니다. Target 계정과 연결된 클라이언트 코드, 이메일 및 암호를 입력합니다. 이러한 필드의 값을 모를 경우 Adobe Target 지원에 문의하십시오. 자격 증명을 확인하려면 &quot;확인&quot; 단추를 클릭하십시오. 확인되면 제출 단추를 클릭하여 클라우드 서비스를 만듭니다.

>[!NOTE]
>
>만들어지는 클라우드 서비스는 마법사를 통해 모바일 애플리케이션과 자동으로 연결됩니다. cq:cloudserviceconfigs 속성 값은 apps 그룹 노드의 jcr:content 노드에서 설정됩니다. 하이브리드 앱 샘플의 경우 /content/mobileapps/hybrid-reference-app/jcr:content에 설정되며 /etc/cloudservices/testandtarget/adobe-target—aem-apps/framework에 있는 자동 생성된 프레임워크 노드를 가리키는 값이 있습니다. 프레임워크 노드에는 기본적으로 성별 및 나이에 의해 설정된 두 개의 속성이 있습니다. 프레임워크는 AEM 미리 보기에서만 사용되며 장치에 영향을 주지 않습니다.

마법사가 완료되면 Cloud Service 관리 타일에 Target 클라우드 서비스가 포함되지만, Adobe 모바일 서비스 계정이 누락되었다는 경고가 포함되어 있습니다.

![chlimage_1-40](assets/chlimage_1-40.png)

### Adobe Mobile Services {#adobe-mobile-services}

AMS(Adobe Mobile Services) 계정을 애플리케이션에 연결해야 하므로, AMS 서비스는 Target 클라이언트 코드 정보가 포함된 필수 ADBMobileConfig.json 파일을 제공합니다. AMS 계정과의 연결을 만들려면 먼저 AMS에 대한 권한이 있는 사용자가 AMS 계정을 수정해야 합니다.

### 클라이언트 코드 {#client-code}

AMS 서비스에 로그인하려면 [https://mobilemarketing.adobe.com](https://mobilemarketing.adobe.com/)을(를) 방문하여 모바일 애플리케이션을 선택하고 설정을 클릭합니다. SDK Target 옵션 필드를 찾아 클라이언트 코드를 필드에 배치하고 저장을 클릭합니다.

![chlimage_1-41](assets/chlimage_1-41.png)

클라이언트 코드가 모바일 애플리케이션과 연결되었으므로 이제 AMS 클라우드 서비스가 Mobile Dashboard Adobe을 통해 구성되면 서비스 설정에 대한 설정이 ADBMobileConfig.json 파일을 통해 전달됩니다.

### Adobe 모바일 서비스 Cloud Service {#adobe-mobile-service-cloud-service}

이제 AMS가 구성되었으므로 Adobe 모바일 대시보드에서 모바일 애플리케이션을 연결할 차례입니다. AEM Mobile 대시보드에서 Cloud Services 관리 을 찾아 + 단추를 클릭합니다.

![chlimage_1-42](assets/chlimage_1-42.png)

Adobe Mobile Services 카드를 선택하고 다음 을 클릭합니다.

![chlimage_1-43](assets/chlimage_1-43.png)

만들기 또는 선택 마법사 단계에서 모바일 서비스 드롭다운을 선택하고 구성 만들기 항목을 선택합니다. 제목, 회사, 사용자 이름, 암호를 입력하고 적절한 데이터 센터를 선택합니다. 이러한 값을 모를 경우 Mobile Service 관리자에게 문의하여 얻으십시오. 모든 필드가 입력되면 확인 단추를 클릭합니다. 확인 프로세스는 AMS로 이동하여 계정에 대한 자격 증명을 확인하고, 유효성 검사가 성공하면 드롭다운에서 연결된 모바일 애플리케이션을 선택하는 모바일 애플리케이션 목록이 채워집니다. 전송 단추를 클릭하여 마법사를 완료합니다. 이 프로세스는 구성 데이터 및 애플리케이션과 연관된 분석을 가져오는 데 시간이 좀 걸릴 수 있습니다. 프로세스가 완료되면 모달에서 완료 단추를 클릭하여 Adobe 모바일 대시보드로 돌아갑니다.

모바일 대시보드로 다시 돌아가 Cloud Services 관리 타일에 AMS 클라우드 서비스가 포함됩니다. 또한 분석 지표 타일에 라이프사이클 보고서가 입력된다는 것을 알 수 있습니다.

![chlimage_1-44](assets/chlimage_1-44.png)

## 작성자 {#for-authors}의 경우

**전제 조건:**  위에서 언급한 대로 작성자가 새로운 타깃팅된 컨텐츠를 생성할 수 있으려면 먼저 관리자가 Adobe Target 서비스에 대한 연결을 구성해야 합니다.

관리자가 두 클라우드 서비스를 구성하고 개발자가 mobileappoffers 핸들러를 구성했으면 컨텐츠 작성자가 이제 타깃팅된 경험 생성을 시작할 수 있습니다.

AEM Mobile 앱 내에서 타깃팅된 컨텐츠를 작성하는 절차는 AEM Sites 작성과 유사합니다.

[AEM에서 타깃팅된 컨텐츠 작성](/help/sites-authoring/personalization.md)에 대한 전체 개요는 여기를 참조하십시오

## 개발자용 {#for-developers}

모바일 애플리케이션을 구축하는 AEM 개발자는 구성 요소를 개발할 때 AEM 전체에서 일반적으로 사용되는 패턴을 계속 따라야 합니다. 여기에서는 컨텐츠 작성자가 타깃팅된 컨텐츠를 만들 수 있도록 하는 필요한 단계를 안내합니다.

### Adobe Target ContentSync 처리기 {#adobe-target-contentsync-handlers}

AEM 컨텐츠 작성자가 만든 오퍼를 렌더링하여 사용자의 장치 컨텐츠에 콘텐츠를 전달하는 것은 생성됩니다. 대상 오퍼의 렌더링을 처리하기 위해 오퍼를 처리하는 새 콘텐츠 동기화 처리기가 있습니다. 하이브리드 참조 응용 프로그램을 샘플로 사용하는 경우 en(영어) 컨텐츠 패키지에는 [mobileappoffers](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/aem-package/content-author/src/main/content/jcr_root/content/mobileapps/hybrid-reference-app/en/_jcr_content/pge-app/app-config-dev/targetOffers/.content.xml) 핸들러가 있는 ContentSyncConfig가 포함됩니다. 다음 단계는 오퍼를 장치에 렌더링하는 데 중요합니다. mobileappoffers 처리기에는 애플리케이션에 사용될 개인화 활동의 경로를 식별하는 경로 속성이 있습니다.

예를 들어 */content/campaigns/hybridref*&#x200B;에 있는 활동이 있으면 이 경로를 복사하여 mobileappoffers 처리기의 *path* 속성에 붙여 넣습니다.

>[!NOTE]
>
>하이브리드 참조 응용 프로그램의 경우 개발용 및 프로덕션용 핸들러가 두 개 있습니다.

활동 경로가 mobileappoffers 처리기의 경로 속성에 설정되면 처리기가 저장됩니다. 이제 처리기가 모바일 장치에 대한 오퍼 렌더링을 시작할 준비가 되었습니다.

### 렌더링 모드 {#render-mode}

mobileappoffers 처리기는 게시 및 개발 설정에 대해 다르게 구성됩니다. 게시 설정의 경우 cq:ContentSyncConfig 노드에 설정된 *publish* 값이 있는 *renderMode*&#x200B;라는 속성이 있습니다. mobileappoffers 처리기는 renderMode를 참조하고, 게시로 설정하면 만들어지는 mbox id를 수정합니다. 기본적으로 AEM에서 만든 mbox에는 —author 값이 mbox id에 추가됩니다. 이것은 활동이 게시되지 않았으며 오퍼 해상도에 게시되지 않은 캠페인을 사용해야 함을 식별합니다.

Adobe 모바일 대시보드를 통해 컨텐츠가 스테이징되면 스테이징된 컨텐츠가 프로덕션 준비 컨텐츠로 간주되고 비개발 컨텐츠 동기화 구성을 통해 렌더링됩니다. 이 방법으로 렌더링하면 —author가 모든 mbox ID에서 제거되고 게시된 활동을 Target 서버에서 사용할 수 있을 것으로 예상됩니다. 준비된 콘텐츠를 테스트하기 전에 활동이 게시되었는지 확인하십시오.

### 개인화 앱 개발 {#personalization-app-development}

#### 구성 요소 {#components}

컨텐츠의 기초는 일반적으로 HTL 또는 JSP를 사용하는 경우에 따라 기본 AEM 페이지 구성 요소 wcm/foundation/components/page 또는 foundation/components/page 중 하나를 확장하는 페이지 구성 요소입니다. 이러한 단계의 기간은 wcm/foundation/components/page 구성 요소 사용에 중점을 둡니다. 페이지 구성 요소의 기본 구조는 여러 스크립트로 분류되며, 각 스크립트는 개발자가 필요한 경우 코드를 구성하고 재정의할 수 있도록 하는 특정 목적을 제공합니다. 개인화에 관심이 있는 두 개의 스크립트는 head.html과 body.html입니다. 이 두 스크립트는 Context Hub, Cloud Services 및 모바일 작성을 지원하도록 코드를 삽입할 수 있는 영역을 제공합니다.

다음은 컨텐츠 타깃팅을 활성화하는 데 사용되는 두 개의 기본 스크립트에 대한 개요입니다.

#### head.html {#head-html}

작성자가 컨텐츠를 타깃팅할 수 있는 기능을 제공하려면 작성자가 편집 모드에서 타깃팅 모드로 컨텍스트를 변경할 수 있도록 타겟 메뉴를 페이지에 추가해야 합니다. 이 기능을 사용하려면 개발자가 다음 코드 조각을 head.html의 상단 근처에 포함하거나 &lt;title>&lt;/title> 요소에 최대한 근접하도록 head.html 스크립트를 수정해야 합니다.

```xml
<meta data-sly-test="${!wcmmode.disabled}">
    <div data-sly-call="${clientLib.all @ categories='personalization.kernel'}" data-sly-unwrap></div>
    <div data-sly-resource="${'config' @ resourceType='cq/personalization/components/clientcontext_optimized/config'}" data-sly-unwrap></div>
    <div data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}" data-sly-unwrap></div>
</meta>
```

>[!NOTE]
>
>WCM 모드가 비활성화되지 않은 경우에만 스크립트를 포함해야 하며 WCM 모드가 비활성화된 경우(자세한 내용은 ContentSync 핸들러 의 섹션 참조) 스크립트가 최종 애플리케이션 코드에 포함되지 않습니다.

작성자가 타깃팅된 컨텐츠를 미리 볼 수 있는 기능을 제공하려면 편집기에서 Adobe Target 클라우드 서비스의 구성을 찾아야 합니다. 아래의 코드 블록은 두 개의 중요한 스크립트를 추가합니다. 페이지에서 먼저 관련 Target 클라우드 서비스를 찾아 Adobe Target에 호출하는 기능을 추가합니다. 두 번째는 cq.apps.targeting 카테고리의 추가입니다.

**cq.apps.targeting** 카테고리는 기본 cq/personalization/component/target 구성 요소를 재정의하고 모바일 애플리케이션 소비에 대한 오퍼를 특별히 렌더링하는 mobileapps/components/target 구성 요소를 사용합니다. 자세한 내용은 Target 구성 요소 섹션에서 설명합니다.

코드는 head.html에 추가하고 &lt;/head> 요소의 끝 바로 앞에 배치해야 합니다.

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-include="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp" data-sly-unwrap></div>
    <meta data-sly-call="${clientLib.all @ categories='cq.apps.targeting'}" data-sly-unwrap></meta>
</div>
```

>[!NOTE]
>
>코드 블록은 WCM 모드 내에 래핑되어 비활성화되지 않으므로 컨텐츠 작성자가 컨텐츠를 만드는 작업을 수행하는 동안에만 재생됩니다. 클라우드 서비스 스크립트는 생성된 모바일 런타임 코드에 추가되지 않습니다.

#### body.html {#body-html}

컨텐츠 작성자가 다른 가상 사용자를 테스트할 수 있도록 하려면 body.html 스크립트는 다음 코드 블록을 본문 요소의 첫 번째 하위 요소로 포함해야 합니다.

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-resource="${'clientcontext' @ resourceType='cq/personalization/components/clientcontext_optimized'}" data-sly-unwrap></div>
</div>
```

필요한 마지막 코드 비트는 body.html의 맨 아래에 있습니다. 이 코드 비트는 연결된 클라우드 서비스를 찾고 적절한 타깃팅 엔진 코드를 삽입합니다.

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-resource="${'cloudservices' @ resourceType='cq/cloudserviceconfigs/components/servicecomponents'}" data-sly-unwrap></div>
</div>
```

### 참조 응용 프로그램 {#reference-application}

head.html 및 body.html의 예는 [AEM Mobile Hybrid 참조 애플리케이션](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference)에서 개발자에게 두 스크립트 내에 스크립트 블록을 배치할 위치를 보여주는 를 찾을 수 있습니다.

### 컨텐츠 동기화 처리기 {#content-sync-handlers}

컨텐츠 작성자가 모바일 애플리케이션용 컨텐츠 만들기를 완료하면 다음 단계는 소스를 다운로드하고 애플리케이션을 빌드하거나 게시할 컨텐츠를 스테이징하는 것입니다. 개발자가 이러한 작업을 수행하는 데 관련된 여러 단계가 있습니다. 컨텐츠 렌더링에 도움이 되도록 AEM Mobile은 컨텐츠 동기화 핸들러를 사용하여 컨텐츠를 렌더링하고 패키지화합니다. 타깃팅된 콘텐츠를 렌더링하기 위해 개인화 사용 사례에 대해 새로운 콘텐츠 동기화 핸들러가 도입되었습니다. &#39;mobileappoffers&#39; 처리기는 컨텐츠 작성자가 만든 관련 대상 오퍼를 렌더링하는 방법을 알고 있습니다. mobileappoffers 처리기는 추상 페이지 업데이트 처리기를 확장하므로 대부분의 속성이 유사합니다. mobileappoffers 처리기의 세부 정보에는 다음 속성이 있습니다.

<table>
 <tbody>
  <tr>
   <td><strong>속성</strong></td>
   <td><strong>값</strong></td>
   <td><strong>설명</strong></td>
  </tr>
  <tr>
   <td>rewrite</td>
   <td>+ relativeParentPath<p> - "/"</p> </td>
   <td>rewrite 속성은 컨텐츠 내의 경로를 다시 작성하는 방법을 식별합니다.</td>
  </tr>
  <tr>
   <td>includedPageTypes</td>
   <td><p>"cq/personalization/components/teaserpage",</p> <p>"cq/personalization/components/offerproxy"</p> </td>
   <td>includePageTypes 속성은 선택 사항이며 cq/personalization/components/teaserpage 및 cq/personalization/components/offerproxy의 리소스 유형이 있는 페이지에 기본값 설정됩니다. 이 두 리소스 유형은 컨텐츠를 타깃팅할 때 사용되는 기본 리소스 유형입니다. 추가 리소스 유형을 지원해야 하는 경우 includePageTypes 목록에 추가해야 합니다.</td>
  </tr>
  <tr>
   <td>locationRoot</td>
   <td>/content/mobileapps/&lt;app&gt;</td>
   <td>앱의 위치입니다.</td>
  </tr>
  <tr>
   <td>유형</td>
   <td>mobileappoffers</td>
   <td>mobileappoffer의 핸들러의 이름입니다.</td>
  </tr>
  <tr>
   <td>선택기</td>
   <td>tandt</td>
   <td>제목 선택기는 타깃팅된 컨텐츠를 렌더링하는 데 사용됩니다. </td>
  </tr>
  <tr>
   <td>targetRootDirectory</td>
   <td>www</td>
   <td>렌더링된 컨텐츠를 유지할 루트 디렉토리입니다.</td>
  </tr>
  <tr>
   <td>includeImages</td>
   <td>true | false</td>
   <td>true면 오퍼에 포함된 이미지가 렌더링됩니다. false 이미지를 건너뜁니다.</td>
  </tr>
  <tr>
   <td>includeVideos</td>
   <td>true | false</td>
   <td>true면 오퍼에 포함된 비디오가 렌더링됩니다. false 비디오를 건너뜁니다.</td>
  </tr>
  <tr>
   <td>경로</td>
   <td>/content/campaigns/&lt;brand&gt;</td>
   <td>오퍼가 참여하는 캠페인의 브랜드를 가리킵니다. 현재 모든 오퍼는 동일한 캠페인에서 가져와야 합니다.</td>
  </tr>
  <tr>
   <td>깊이</td>
   <td>true | false</td>
   <td>True가 재귀적으로 모든 하위 페이지를 렌더링하는 경우, false가 재귀하지 않습니다. </td>
  </tr>
  <tr>
   <td>확장</td>
   <td>html</td>
   <td>렌더링되는 리소스의 확장을 설정합니다. 페이지에 .html 확장자가 있도록 html로 설정합니다.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>[AEM Mobile 하이브리드 참조 앱](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference)에 기본 mobileappoffer 처리기의 구성이 있습니다. 샘플의 경로 속성은 캠페인 위치에 따라 달라지므로 비어 있습니다. Campaign 작성자가 Campaign을 만든 후 앱 관리자는 Campaign을 가리키는 경로 속성을 지정하여 Campaign을 처리기와 연결해야 합니다.

### Target 구성 요소 {#target-component}

모바일 애플리케이션용으로 특별히 컨텐츠를 렌더링하는 데 도움이 되도록 AEM Mobile은 mobileapps/components/target 구성 요소를 사용합니다. 모바일 타겟 구성 요소는 cq/personalization/components/target 구성 요소를 확장하고 engine_tnt.jsp 스크립트를 무시합니다. engine_tnt.jsp를 재정의하여 AEM Mobile에서 모바일 앱 사용 사례에 대해 생성된 HTML을 제어할 수 있습니다. 컨텐츠 작성자가 타겟팅하는 모든 구성 요소에 대해 engine_tnt.jsp에 연결된 mbox가 만들어집니다.

각 mbox에 대해 **cq-targeting** 속성이 추가되어 애플리케이션 개발자가 원하는 대로 사용자 지정 코드를 작성하여 사용할 수 있습니다. [AEM Mobile Hybrid 참조 앱](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference)에는 cq-targeting 속성을 사용하는 Angular 지시어의 예가 있습니다. 컨텐츠 교체 시기 및 작성 방법에 대한 개념은 모바일 애플리케이션 개발자에게 매우 중요합니다. Adobe 타깃팅 서비스를 호출하기 위한 API를 제공하는 AEM /etc/clientlibs/mobileapps/js/mobileapps.js 을 통해 전달되는 Mobile SDK가 있습니다. 애플리케이션의 디자인에 따라 해당 호출을 언제 수행해야 하는지 지정하는 것은 애플리케이션 개발자의 책임입니다.

## 다음은 무엇입니까?{#what-s-next}

1. [AEM Mobile 앱 경험 시작](/help/mobile/starting-aem-phonegap-app.md)
1. [내 앱의 콘텐츠 관리](/help/mobile/phonegap-manage-app-content.md)
1. [내 애플리케이션 빌드](/help/mobile/building-app-mobile-phonegap.md)
1. [Adobe Mobile Analytics를 사용하여 내 앱의 성능 추적](/help/mobile/phonegap-intro-to-app-analytics.md)
1. [Adobe Target을 통해 개인화된 앱 경험 제공](/help/mobile/phonegap-aem-mobile-content-personalization.md)
1. [사용자에게 중요한 메시지 보내기](/help/mobile/phonegap-push-notifications.md)
