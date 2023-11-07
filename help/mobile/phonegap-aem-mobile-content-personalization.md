---
title: Adobe Experience Manager Mobile 콘텐츠 개인화
description: AEM 작성자가 Adobe Target을 사용하여 모바일 앱 컨텐츠를 개인화할 수 있는 AEM(Adobe 경험 관리) 모바일 컨텐츠 개인화 기능에 대해 알려면 이 페이지를 따르십시오.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: 70d7ee0d-2f6d-4f97-a6e2-b02d84a0ca42
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '2607'
ht-degree: 1%

---

# AEM Mobile 콘텐츠 개인화{#aem-mobile-content-personalization}

>[!NOTE]
>
>Adobe 단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: React)이 필요한 프로젝트에는 SPA Editor를 사용하는 것이 좋습니다. [자세히 알아보기](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>이 문서는 [AEM Mobile 시작하기](/help/mobile/getting-started-aem-mobile.md) AEM Mobile 참조에 대한 권장 시작점인 안내서입니다.

AEM Mobile 콘텐츠 개인화 기능을 통해 다음과 같은 작업을 수행할 수 있습니다 [AEM 작성자](#author) 을 사용하여 모바일 앱 컨텐츠를 개인화하려면 [Adobe Target](https://business.adobe.com/products/target/adobe-target.html). 이렇게 하면 모바일 애플리케이션 사용자에게 타깃팅된 오퍼를 전달할 수 있습니다. Adobe Experience Manager Mobile은 사용자에게 고유한 개인 취향에 맞는 콘텐츠를 제공할 콘텐츠를 만들고, 타깃팅하고, 전달하는 기능을 제공합니다.

AEM에서 작성자가 이 콘텐츠를 만들려면 먼저 관리자와 개발자가 환경을 준비해야 합니다.

[AEM 관리자](#administrator) AEM Mobile과 Adobe Target Cloud Service 간 연결을 설정하는 데 필요합니다.

한편, AEM Mobile [개발자](#developer) 타겟팅된 콘텐츠를 쉽게 작성할 수 있도록 기존 스크립트를 편집해야 합니다.

## 관리자용 {#for-administrators}

콘텐츠 작성자가 모바일 앱에 대한 타겟팅된 콘텐츠를 생성하기 전에 수행해야 하는 몇 가지 단계가 있습니다. 사용자 및 그룹에 적합한 권한 세트를 가져오고, 클라우드 서비스를 만들고, 활동용 애플리케이션을 구성하고, 마지막으로 콘텐츠를 생성합니다.

이 문서에서는 을 구성하는 데 사용되는 프로세스를 안내합니다. [AEM Mobile 하이브리드 참조 애플리케이션](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) 타깃팅용.

앞으로 AEM Mobile 하이브리드 참조 애플리케이션이 AEM Mobile 대시보드를 통해 성공적으로 배포되고 액세스할 수 있다고 가정합니다.

작성자가 애플리케이션 내에서 타겟팅된 콘텐츠를 생성하려면 먼저 AEM 인스턴스가 다음과 같아야 합니다. [Adobe Target Cloud Service으로 구성됩니다.](/help/mobile/aem-mobile-configuring-cloud-service.md)

### 권한 {#permissions}

개인화 콘솔에 액세스해야 하는 사용자는 `target-activity-authors` 그룹입니다.

사용자 및 그룹 설정의 일부로 target-activity-group을 apps-admins 그룹에 추가하는 것이 좋습니다. target-activity-authors 그룹을 추가하면 사용자는 개인화 탐색 메뉴 항목을 볼 수 있습니다.

>[!NOTE]
>
>개인화 Admin Console에 액세스할 수 있는 사용자 또는 그룹을 target-activity-authors 그룹에 추가하지 않으면 사용자가 개인화 콘솔을 볼 수 없습니다.

### 클라우드 서비스 {#cloud-services}

모바일 애플리케이션에서 작동하는 타겟팅된 콘텐츠를 가져오려면 Adobe Target 서비스와 Adobe Mobile Services 서비스의 두 가지 서비스를 구성해야 합니다. Adobe Target 서비스는 클라이언트 요청을 처리하고 개인화된 콘텐츠를 반환하기 위한 엔진을 제공합니다. Adobe Mobile Services 서비스는 AMS Cordova 플러그인이 사용하는 ADBMobileConfig.json 파일을 통해 Adobe 서비스와 모바일 애플리케이션 간의 연결을 제공합니다. AEM Mobile 대시보드에서 두 서비스를 추가하여 애플리케이션을 구성할 수 있습니다.

AEM Mobile 대시보드에서 관리 Cloud Service을 찾아 + 단추를 클릭합니다.

![chlimage_1-38](assets/chlimage_1-38.png)

Cloud Service 추가 마법사에서 &quot;Adobe Target&quot; 클라우드 서비스 카드를 선택하고 다음을 클릭합니다.

![chlimage_1-39](assets/chlimage_1-39.png)

구성 선택 드롭다운에서 구성을 만들거나 기존 구성에서 선택할 수 있습니다. 구성을 만들려면 드롭다운에서 &quot;구성 만들기&quot;를 선택합니다. Target 구성의 제목을 입력합니다. Target 계정과 연결된 클라이언트 코드, 이메일 및 암호를 입력합니다. 이러한 필드의 값을 모를 경우 Adobe Target 지원 센터에 문의하십시오. 자격 증명의 유효성을 검사하려면 &quot;확인&quot; 단추를 클릭하십시오. 확인되면 제출 단추를 클릭하여 클라우드 서비스를 만듭니다.

>[!NOTE]
>
>만들어지는 클라우드 서비스는 마법사를 통해 모바일 애플리케이션과 자동으로 연결됩니다. cq:cloudserviceconfigs 속성 값은 앱 그룹 노드의 jcr:content 노드에서 설정됩니다. 하이브리드 앱 샘플의 경우 /etc/cloudservices/testandtarget/adobe-target—aem-apps/framework에서 자동으로 생성된 프레임워크 노드를 가리키는 값으로 /content/mobileapps/hybrid-reference-app/jcr:content에 설정됩니다. 프레임워크 노드에는 기본적으로 성별 및 연령의 두 가지 속성이 설정되어 있습니다. 프레임워크는 AEM 미리보기에서만 사용되며 장치에는 영향을 주지 않습니다.

마법사 완료 후 Cloud Service 관리 타일에는 Target 클라우드 서비스가 포함됩니다. 하지만 여기에는 누락된 Adobe Mobile Service 계정에 대한 경고가 포함되어 있습니다.

![chlimage_1-40](assets/chlimage_1-40.png)

### Adobe Mobile Services {#adobe-mobile-services}

AMS(Adobe 모바일 서비스) 계정을 응용 프로그램에 연결해야 합니다. 또한 AMS 서비스는 Target 클라이언트 코드 정보가 포함된 필수 ADBMobileConfig.json 파일을 제공합니다. AMS 계정과의 연결을 만들기 전에 AMS에 대한 권한이 있는 사용자가 AMS 계정을 수정해야 합니다.

### 클라이언트 코드 {#client-code}

AMS 서비스에 로그인하려면 다음을 방문하십시오. [https://mobilemarketing.adobe.com](https://mobilemarketing.adobe.com/)모바일 애플리케이션을 선택하고 설정을 클릭합니다. SDK Target 옵션 필드를 찾아 필드에 클라이언트 코드를 넣은 다음 저장 을 클릭합니다.

![chlimage_1-41](assets/chlimage_1-41.png)

클라이언트 코드가 모바일 애플리케이션과 연결되었으므로 AMS 클라우드 서비스가 Adobe 모바일 대시보드를 통해 구성되면 서비스 설정에 대한 설정이 ADBMobileConfig.json 파일을 통해 전달됩니다.

### Adobe Mobile Service Cloud Service {#adobe-mobile-service-cloud-service}

이제 AMS가 구성되었으므로 Adobe 모바일 대시보드에서 모바일 애플리케이션을 연결할 차례입니다. AEM Mobile 대시보드에서 관리 Cloud Service을 찾아 + 단추를 클릭합니다.

![chlimage_1-42](assets/chlimage_1-42.png)

Mobile Services Adobe 카드를 선택하고 다음 을 클릭합니다.

![chlimage_1-43](assets/chlimage_1-43.png)

만들기 또는 선택 마법사 단계에서 Mobile Service 드롭다운을 선택하고 구성 만들기 항목을 선택합니다. 제목, 회사, 사용자 이름, 암호를 입력하고 적절한 데이터 센터를 선택합니다. 이러한 값을 모를 경우 Adobe Mobile Service 관리자에게 문의하여 값을 받으십시오. 모든 필드가 채워지면 **확인**. 확인 프로세스는 AMS로 이동하여 계정에 대한 자격 증명을 확인하고, 유효성 검사에 성공하면 드롭다운에서 연결된 모바일 애플리케이션을 선택할 수 있는 모바일 애플리케이션 목록이 채워집니다. 클릭 **제출** 을 클릭하여 마법사를 완료합니다. 프로세스는 구성 데이터 및 애플리케이션과의 임의의 연관된 분석을 획득하는 데 약간의 시간이 걸릴 수 있다. 프로세스가 완료되면 다음을 클릭합니다. **완료** Adobe 모바일 대시보드로 돌아갑니다 .

모바일 대시보드로 돌아가면 Cloud Service 관리 타일에 AMS 클라우드 서비스가 포함됩니다. 또한 지표 분석 타일은 라이프사이클 보고서로 채워집니다.

![chlimage_1-44](assets/chlimage_1-44.png)

## 작성자용 {#for-authors}

**전제 조건:** 위에서 언급했듯이 작성자가 새로운 타겟팅된 콘텐츠를 생성하려면 관리자가 Adobe Target 서비스에 대한 연결을 구성해야 합니다.

관리자가 두 개의 클라우드 서비스를 구성하고 개발자가 mobileappoffers 핸들러를 구성하면 콘텐츠 작성자는 이제 타깃팅된 경험을 생성할 수 있습니다.

AEM Mobile 앱 내에서 타깃팅된 컨텐츠를 작성하는 작업은 AEM Sites 작성과 유사한 절차를 따릅니다.

에 대한 전체 개요는 여기 를 참조하십시오. [AEM에서 타깃팅된 컨텐츠 작성](/help/sites-authoring/personalization.md)

## 개발자용 {#for-developers}

모바일 애플리케이션을 구축하는 AEM 개발자는 구성 요소를 개발할 때 AEM 전체에서 일반적으로 사용되는 패턴을 계속 따라야 합니다. 여기에서 Adobe은 콘텐츠 작성자가 타깃팅된 콘텐츠를 만들 수 있도록 하는 데 필요한 단계를 안내합니다.

### Adobe Target ContentSync 핸들러 {#adobe-target-contentsync-handlers}

컨텐츠를 사용자의 장치에 전달하기 위해 컨텐츠는 AEM 컨텐츠 작성자가 만든 오퍼를 렌더링하여 생성됩니다. 대상 오퍼의 렌더링을 처리하기 위해 오퍼를 처리하는 새로운 콘텐츠 동기화 핸들러가 있습니다. 하이브리드 참조 응용 프로그램을 샘플로 사용하는 en(영어) 콘텐츠 패키지에는 [mobileappoffers](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/aem-package/content-author/src/main/content/jcr_root/content/mobileapps/hybrid-reference-app/en/_jcr_content/pge-app/app-config-dev/targetOffers/.content.xml) 핸들러입니다. 다음 단계는 장치에 오퍼를 렌더링하는 데 중요합니다. mobileappoffers 핸들러에는 애플리케이션에 사용할 개인화 활동의 경로를 식별하는 경로 속성이 있습니다.

예를 들어 다음 위치에 활동이 있는 경우 */content/campaigns/hybridref*, 이 경로를 복사한 다음 값에 붙여넣습니다. *경로* mobileappoffers 처리기의 속성입니다.

>[!NOTE]
>
>하이브리드 참조 애플리케이션의 경우 두 개의 mobileappoffers 핸들러가 있으며 하나는 개발용이고 하나는 제작용입니다.

mobileappoffers 처리기의 path 속성에 활동 경로가 설정되면 처리기를 저장합니다. 이제 핸들러가 모바일 장치에 대한 오퍼 렌더링을 시작할 준비가 되었습니다.

### 렌더링 모드 {#render-mode}

mobileappoffers 처리기는 게시 및 개발 설정에 대해 다르게 구성됩니다. 게시 설정의 경우 라는 속성이 있습니다. *renderMode* (값: *게시* cq:ContentSyncConfig 노드에 설정합니다. mobileappoffers 처리기가 renderMode를 참조하고 게시로 설정된 경우 만들어지는 mbox id를 편집합니다. 기본적으로 AEM에서 만드는 mbox에는 mbox id에 —author 값이 추가됩니다. 이는 활동이 게시되지 않았으며 오퍼 확인에 게시되지 않은 캠페인을 사용해야 함을 나타냅니다.

Adobe Mobile Dashboard를 통해 콘텐츠를 스테이징하면 스테이징된 콘텐츠는 프로덕션 준비 콘텐츠로 간주되고 비개발 콘텐츠 동기화 구성을 통해 렌더링됩니다. 이 방법으로 렌더링하면 —author가 모든 mbox id에서 제거되고 게시된 활동을 Target 서버에서 사용할 수 있게 됩니다. 스테이징된 콘텐츠를 테스트하기 전에 활동이 이미 게시되었는지 확인하십시오.

### 개인화 앱 개발 {#personalization-app-development}

#### 구성 요소 {#components}

콘텐츠의 기반은 일반적으로 HTL 또는 JSP를 사용하는 경우에 따라 기본 AEM 페이지 구성 요소 wcm/foundation/components/page 또는 foundation/components/page 중 하나를 확장하는 페이지 구성 요소입니다. 이 단계의 기간은 wcm/foundation/components/page 구성 요소 사용에 중점을 둡니다. 페이지 구성 요소의 기본 구조는 여러 스크립트로 나뉘며, 각 스크립트는 개발자가 필요한 경우 코드를 구성하고 재정의할 수 있는 특정 목적을 제공합니다. 개인화에 관심 있는 두 가지 스크립트는 head.html과 body.html입니다. 이 두 스크립트는 Context Hub, Cloud Service 및 모바일 작성을 지원하기 위해 코드를 삽입할 수 있는 영역을 제공합니다.

다음은 콘텐츠 타겟팅을 활성화하는 데 사용되는 두 가지 기본 스크립트에 대한 개요입니다.

#### head.html {#head-html}

작성자에게 콘텐츠를 타깃팅하는 기능을 제공하려면 작성자가 컨텍스트를 편집 모드에서 타깃팅 모드로 변경할 수 있도록 타겟 메뉴를 페이지에 추가해야 합니다. 이 기능을 활성화하려면 개발자가 head.html의 상단에 다음 코드 조각을 포함하거나 &lt;title>&lt;/title> 요소를 가능한 한 추가합니다.

```xml
<meta data-sly-test="${!wcmmode.disabled}">
    <div data-sly-call="${clientLib.all @ categories='personalization.kernel'}" data-sly-unwrap></div>
    <div data-sly-resource="${'config' @ resourceType='cq/personalization/components/clientcontext_optimized/config'}" data-sly-unwrap></div>
    <div data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}" data-sly-unwrap></div>
</meta>
```

>[!NOTE]
>
>WCM 모드가 비활성화된 경우에만 스크립트를 포함하십시오. 따라서 WCM 모드가 비활성화된 경우(자세한 내용은 ContentSync 처리기 섹션 참조) 스크립트는 최종 응용 프로그램 코드에 포함되지 않습니다.

작성자가 타겟팅된 콘텐츠를 미리 볼 수 있는 기능을 제공하려면 편집기에서 Adobe Target 클라우드 서비스의 구성을 찾을 수 있어야 합니다. 아래의 코드 블록은 두 개의 중요한 스크립트를 추가합니다. 첫 번째 추가 기능은 페이지가 연결된 Target 클라우드 서비스를 찾고 Adobe Target을 호출하는 기능입니다. 두 번째는 cq.apps.targeting 카테고리의 추가입니다.

다음 **cq.apps.targeting** 카테고리는 기본 cq/personalization/component/target 구성 요소를 재정의하고 모바일 애플리케이션 이용에 대한 오퍼를 렌더링하는 mobileapps/components/target 구성 요소를 사용합니다. 이에 대한 자세한 내용은 타겟 구성 요소 섹션에 자세히 설명되어 있습니다.

코드는 head.html에 추가하고 의 끝 바로 앞에 배치해야 합니다. &lt;/head> 요소를 생성하지 않습니다.

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-include="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp" data-sly-unwrap></div>
    <meta data-sly-call="${clientLib.all @ categories='cq.apps.targeting'}" data-sly-unwrap></meta>
</div>
```

>[!NOTE]
>
>코드 블록은 비활성화되지 않고 WCM 모드 내에서 래핑되므로 콘텐츠 작성자가 콘텐츠를 만드는 작업 중에만 재생됩니다. 클라우드 서비스 스크립트는 생성된 모바일 런타임 코드에 추가되지 않습니다.

#### body.html {#body-html}

콘텐츠 작성자에게 다양한 가상 사용자를 테스트할 수 있는 기능을 제공하려면 body.html 스크립트에 body 요소의 첫 번째 하위 항목으로 다음 코드 블록이 포함되어야 합니다.

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-resource="${'clientcontext' @ resourceType='cq/personalization/components/clientcontext_optimized'}" data-sly-unwrap></div>
</div>
```

필요한 마지막 코드 비트는 body.html의 맨 아래에 있습니다. 이 코드 비트는 연결된 클라우드 서비스를 찾아 적절한 타깃팅 엔진 코드를 주입합니다.

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-resource="${'cloudservices' @ resourceType='cq/cloudserviceconfigs/components/servicecomponents'}" data-sly-unwrap></div>
</div>
```

### 참조 애플리케이션 {#reference-application}

head.html 및 body.html의 예는 [AEM Mobile 하이브리드 참조 애플리케이션](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) 개발자에게 두 스크립트 내에서 스크립트 블록을 배치할 위치를 보여 줍니다.

### 콘텐츠 동기화 핸들러 {#content-sync-handlers}

콘텐츠 작성자가 모바일 애플리케이션용 콘텐츠 작성을 마치면 다음 단계는 소스를 다운로드하고 애플리케이션을 빌드하거나 게시할 콘텐츠를 스테이징하는 것입니다. 이를 실현하기 위해 개발자가 관여하는 몇 가지 단계가 있습니다. 컨텐츠 렌더링에 도움이 되도록 AEM Mobile은 컨텐츠 동기화 핸들러를 사용하여 컨텐츠를 렌더링하고 패키징합니다. 맞춤화 사용 사례에서 타겟팅된 콘텐츠를 렌더링하기 위한 새로운 콘텐츠 동기화 핸들러가 도입되었습니다. &#39;mobileappoffers&#39; 처리기는 콘텐츠 작성자가 만든 연결된 대상 오퍼를 렌더링하는 방법을 알고 있습니다. mobileappoffers 처리기는 추상 페이지 업데이트 처리기를 확장하므로 대부분의 속성이 유사합니다. mobileappoffers 처리기의 세부 정보에는 다음 속성이 있습니다.

<table>
 <tbody>
  <tr>
   <td><strong>속성</strong></td>
   <td><strong>값</strong></td>
   <td><strong>설명</strong></td>
  </tr>
  <tr>
   <td>다시 작성</td>
   <td>+ relativeParentPath<p> - "/"</p> </td>
   <td>재작성 속성은 콘텐츠 내의 경로를 재작성하는 방법을 식별합니다.</td>
  </tr>
  <tr>
   <td>includedPageTypes</td>
   <td><p>"cq/personalization/components/teaserpage",</p> <p>"cq/personalization/components/offerproxy"</p> </td>
   <td>includePageTypes 속성은 선택 사항이며 cq/personalization/components/teaserpage 리소스 유형과 cq/personalization/components/offerproxy 리소스 유형이 있는 페이지에 기본값을 설정합니다. 이 두 리소스 유형은 콘텐츠를 타깃팅할 때 사용되는 기본 리소스 유형입니다. 추가 리소스 유형을 지원해야 하는 경우 includePageTypes 목록에 추가합니다.</td>
  </tr>
  <tr>
   <td>locationRoot</td>
   <td>/content/mobileapps/&lt;app&gt;</td>
   <td>앱의 위치입니다.</td>
  </tr>
  <tr>
   <td>유형</td>
   <td>mobileappoffers</td>
   <td>mobileappoffers인 처리기의 이름입니다.</td>
  </tr>
  <tr>
   <td>선택기</td>
   <td>탄트</td>
   <td>대상 콘텐츠를 렌더링하는 데 사용되는 문트 선택기입니다. </td>
  </tr>
  <tr>
   <td>대상 루트 디렉터리</td>
   <td>www</td>
   <td>렌더링된 콘텐츠를 유지할 루트 디렉터리입니다.</td>
  </tr>
  <tr>
   <td>includeImages</td>
   <td>true | false</td>
   <td>true인 경우 오퍼에 포함된 모든 이미지가 렌더링됩니다. false인 경우 이미지를 건너뜁니다.</td>
  </tr>
  <tr>
   <td>includeVideos</td>
   <td>true | false</td>
   <td>true인 경우 오퍼에 포함된 모든 비디오가 렌더링됩니다. false인 경우 비디오를 건너뜁니다.</td>
  </tr>
  <tr>
   <td>path</td>
   <td>/content/campaigns/&lt;brand&gt;</td>
   <td>오퍼가 참여하는 캠페인의 브랜드를 가리킵니다. 현재 모든 오퍼는 동일한 캠페인에서 가져와야 합니다.</td>
  </tr>
  <tr>
   <td>깊이</td>
   <td>true | false</td>
   <td>true이면 모든 하위 페이지를 재귀적으로 렌더링하고, false이면 재귀하지 않습니다. </td>
  </tr>
  <tr>
   <td>확장</td>
   <td>html</td>
   <td>렌더링되는 리소스의 확장을 설정합니다. 페이지의 확장자가 .html이 되도록 html로 설정합니다.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>다음 [AEM Mobile 하이브리드 참조 앱](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) 에는 기본 mobileappoffer 처리기 구성이 있습니다. 샘플의 경로 속성은 캠페인 위치에 따라 달라지므로 비어 있습니다. Campaign 작성자가 Campaign을 만든 후 앱 관리자는 Campaign을 가리키는 경로 속성을 지정하여 Campaign을 핸들러와 연결해야 합니다.

### 타겟 구성 요소 {#target-component}

AEM Mobile에서는 모바일 애플리케이션용으로 콘텐츠를 렌더링할 수 있도록 mobileapps/components/target 구성 요소를 사용합니다. 모바일 타겟 구성 요소는 cq/personalization/components/target 구성 요소를 확장하고 engine_tnt.jsp 스크립트를 무시합니다. engine_tnt.jsp를 재정의하여 AEM Mobile이 모바일 앱 사용 사례에 대해 생성된 HTML을 제어할 수 있도록 합니다. 콘텐츠 작성자가 타겟팅하는 모든 구성 요소에 대해 관련 mbox가 engine_tnt.jsp에 의해 생성됩니다.

각 mbox에 대해 의 속성 **cq-targeting** 애플리케이션 개발자가 원하는 대로 사용하고 사용할 사용자 지정 코드를 작성할 수 있도록 가 추가되었습니다. 다음 [AEM Mobile 하이브리드 참조 앱](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) 에는 cq-targeting 속성을 사용하는 Angular 지시문의 예제가 있습니다. 콘텐츠 교체의 개념, 시기 및 방법은 모바일 애플리케이션 개발자가 결정합니다. Adobe 타깃팅 서비스를 호출하기 위한 API를 제공하는 AEM /etc/clientlibs/mobileapps/js/mobileapps.js 를 통해 제공되는 Mobile SDK가 있습니다. 응용 프로그램의 디자인에 따라 호출이 언제 수행되어야 하는지 지정하는 것은 응용 프로그램 개발자의 책임입니다.

## 다음 단계? {#what-s-next}

1. [내 AEM Mobile 앱 경험 시작](/help/mobile/starting-aem-phonegap-app.md)
1. [내 앱 콘텐츠 관리](/help/mobile/phonegap-manage-app-content.md)
1. [내 애플리케이션 빌드](/help/mobile/building-app-mobile-phonegap.md)
1. [Adobe Mobile Analytics로 앱 성능 추적](/help/mobile/phonegap-intro-to-app-analytics.md)
1. [Adobe Target을 통해 개인화된 앱 경험 제공](/help/mobile/phonegap-aem-mobile-content-personalization.md)
1. [내 사용자에게 중요한 메시지 보내기](/help/mobile/phonegap-push-notifications.md)
