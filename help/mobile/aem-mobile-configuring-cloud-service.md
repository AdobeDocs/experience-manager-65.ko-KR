---
title: Adobe Target Cloud 서비스 구성
seo-title: Adobe Target Cloud 서비스 구성
description: 이 페이지에서 사용자 및 그룹에 대한 올바른 권한 집합을 가져오고, 클라우드 서비스를 만들고, 활동에 대한 응용 프로그램을 구성하고, 마지막으로 컨텐츠를 생성하는 방법을 알아봅니다.
seo-description: 이 페이지에서 사용자 및 그룹에 대한 올바른 권한 집합을 가져오고, 클라우드 서비스를 만들고, 활동에 대한 응용 프로그램을 구성하고, 마지막으로 컨텐츠를 생성하는 방법을 알아봅니다.
uuid: 569f9c6d-f521-488a-9e51-f43b7a214dd9
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: 8cd6480f-cb4f-40dd-a444-8ba463b78604
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Adobe Target Cloud 서비스 구성 {#configuring-adobe-target-cloud-service}

>[!NOTE]
>
>단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: 응답)이 필요한 프로젝트에 SPA 편집기를 사용하는 것이 좋습니다. [추가 정보](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>이 문서는 AEM Mobile [참조용 권장 시작점인](/help/mobile/getting-started-aem-mobile.md) AEM Mobile 시작하기 안내서의 일부입니다.

컨텐츠 작성자가 모바일 앱에 대한 타깃팅된 컨텐츠를 생성하기 전에 몇 가지 단계를 함께 수행해야 합니다.사용자 및 그룹에 대한 올바른 권한 집합, 클라우드 서비스 만들기, 활동에 대한 응용 프로그램 구성 및 마지막으로 컨텐츠를 생성합니다.

앞으로 AEM Mobile 하이브리드 [참조 애플리케이션이](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) 성공적으로 배포되고 AEM Mobile Dashboard를 통해 액세스할 수 있다고 가정합니다.

## 권한 {#permissions}

개인화 콘솔에 액세스해야 하는 사용자는 `target-activity-authors` 그룹의 일부여야 합니다. 사용자 및 그룹 설정의 일부로 target-activity-group을 apps-admins 그룹에 추가해야 합니다. target-activity-authors 그룹을 추가하면 사용자가 개인화 탐색 메뉴 항목을 볼 수 있습니다.

개인화 관리 콘솔에 액세스할 사용자 또는 그룹을 target-activity-authors 그룹에 추가하지 않으면 사용자가 개인화 콘솔을 볼 수 없습니다.

## 클라우드 서비스 {#cloud-services}

모바일 애플리케이션을 위해 타깃팅된 컨텐츠를 작동하려면 다음 두 가지 서비스를 구성해야 합니다.Adobe Target 서비스 및 Adobe Mobile Services 서비스. Adobe Target 서비스는 클라이언트 요청을 처리하고 개인화된 컨텐츠를 반환하는 엔진을 제공합니다. Adobe Mobile Services 서비스는 AMS Cordova 플러그인이 사용하는 ADBMobileConfig.json 파일을 통해 Adobe 서비스와 모바일 애플리케이션 간의 연결을 제공합니다. AEM Mobile 대시보드에서 두 서비스를 추가하여 애플리케이션을 구성할 수 있습니다.

## Adobe Target Cloud 서비스 {#adobe-target-cloud-service}

AEM Mobile Dashboard에서 클라우드 서비스 관리를 찾아 + 단추를 클릭합니다.

![chlimage_1-8](assets/chlimage_1-8.png)

클라우드 서비스 추가 마법사에서 &quot;Adobe Target&quot; 클라우드 서비스 카드를 선택하고 다음을 클릭합니다.

![chlimage_1-9](assets/chlimage_1-9.png)

구성 선택 드롭다운에서 새 구성을 만들거나 기존 구성 중에서 선택할 수 있습니다. 새 구성을 만들려면 드롭다운에서 &quot;구성 만들기&quot;를 선택합니다. 타겟 구성의 제목을 입력합니다. Target 계정과 관련된 클라이언트 코드, 이메일 및 암호를 입력합니다. 이러한 필드의 값을 모르는 경우 Adobe Target 지원에 문의하십시오. &quot;확인&quot; 단추를 클릭하여 자격 증명을 확인합니다. 확인되면 전송 단추를 클릭하여 클라우드 서비스를 만듭니다.

생성된 클라우드 서비스는 마법사를 통해 모바일 애플리케이션과 자동으로 연결됩니다. cq:cloudserviceconfigs 속성 값은 앱 그룹 노드의 jcr:content 노드에서 설정됩니다. 하이브리드 앱 샘플의 경우 /content/mobileapps/hybrid-reference-app/jcr:content에 설정되고 /etc/cloudservices/testandtarget/adobe-target—aem-apps/framework에 있는 자동으로 생성된 프레임워크 노드를 가리키는 값이 설정됩니다. 프레임워크 노드에는 기본적으로 성별 및 연령별로 설정된 두 개의 속성이 있습니다. 프레임워크는 AEM 미리 보기에서만 사용되며 장치에 영향을 주지 않습니다.

마법사가 완료되면 클라우드 서비스 관리 타일에는 Target 클라우드 서비스가 포함되지만 Adobe Mobile Service 계정이 누락되었다는 경고가 표시됩니다.

![chlimage_1-10](assets/chlimage_1-10.png)

## Adobe Mobile Service {#adobe-mobile-service}

AMS 서비스는 Adobe Mobile Services(AMS) 계정을 응용 프로그램에도 연결해야 합니다. AMS 서비스는 Target 클라이언트 코드 정보를 포함하는 필수 ADBMobileConfig.json 파일을 제공합니다. AMS 계정과 연결을 만들기 전에 AMS에 대한 권한이 있는 사용자가 AMS 계정을 수정해야 합니다.

### 클라이언트 코드 {#client-code}

AMS 서비스에 로그인하려면 https://mobilemarketing.adobe.com [을](https://mobilemarketing.adobe.com/)방문하여 모바일 애플리케이션을 선택하고 설정을 클릭합니다. SDK Target 옵션 필드를 찾아 클라이언트 코드를 필드에 입력하고 저장을 클릭합니다.

![chlimage_1-11](assets/chlimage_1-11.png)

이제 클라이언트 코드가 모바일 애플리케이션과 연결되었으므로 AMS 클라우드 서비스가 Adobe Mobile Dashboard를 통해 구성되면 서비스 설정에 대한 설정이 ADBMobileConfig.json 파일을 통해 전달됩니다.

### Adobe Mobile Service Could Service {#adobe-mobile-service-could-service}

이제 AMS가 구성되었으므로 이제 Adobe Mobile Dashboard에서 모바일 애플리케이션을 연결할 때입니다. AEM Mobile Dashboard에서 클라우드 서비스 관리를 찾아 + 단추를 클릭합니다.

![chlimage_1-12](assets/chlimage_1-12.png)

Adobe Mobile Services 카드를 선택하고 [다음]을 클릭합니다.

![chlimage_1-13](assets/chlimage_1-13.png)

만들기 또는 선택 마법사 단계에서 Mobile Service 드롭다운을 선택하고 구성 만들기 항목을 선택합니다. 제목, 회사, 사용자 이름, 암호를 입력하고 적절한 데이터 센터를 선택합니다. 이러한 값을 모르는 경우 Adobe Mobile Service 관리자에게 문의하여 얻으십시오. 모든 필드가 입력되면 확인 단추를 클릭합니다. 확인 프로세스는 AMS로 이동하여 계정에 대한 자격 증명을 확인하며, 유효성 검사가 성공하면 드롭다운에서 연결된 모바일 응용 프로그램을 선택하는 모바일 응용 프로그램 목록이 채워집니다. 전송 단추를 클릭하여 마법사를 완료합니다. 이 프로세스는 구성 데이터 및 응용 프로그램과 연관된 분석을 얻는 데 시간이 걸릴 수 있습니다. 프로세스가 완료되면 모달에서 완료 단추를 클릭하여 Adobe Mobile Dashboard로 돌아갑니다.

다시 Mobile Dashboard로 돌아가면 클라우드 서비스 관리 타일에는 AMS 클라우드 서비스가 포함됩니다. 지표 분석 타일은 라이프사이클 보고서로 채워집니다.

![chlimage_1-14](assets/chlimage_1-14.png)

## 타겟 컨텐츠 동기화 핸들러 {#target-content-sync-handlers}

AEM 컨텐츠 작성자가 만든 오퍼를 렌더링하여 사용자의 장치 컨텐츠에 컨텐츠를 전달하는 것이 생성됩니다. 대상 오퍼의 렌더링을 처리하기 위해 오퍼를 처리하는 새로운 컨텐츠 동기화 핸들러가 있습니다. 하이브리드 참조 응용 프로그램을 샘플로 사용하는 en(영어) 컨텐츠 패키지에는 ContentSyncConfig와 [mobileappoffers](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/aem-package/content-author/src/main/content/jcr_root/content/mobileapps/hybrid-reference-app/en/_jcr_content/pge-app/app-config-dev/targetOffers/.content.xml) 핸들러가 포함되어 있습니다. 다음 단계는 오퍼를 장치로 렌더링하는 데 중요합니다. mobileappoffers 처리기에는 응용 프로그램에 사용할 개인화 활동의 경로를 식별하는 경로 속성이 있습니다.

예를 들어 */content/campaigns/hybridref에 위치한 활동이* 있는 경우 이 경로를 복사하여 mobileappoffers 처리기의 *path* 속성에 붙여 넣습니다.

하이브리드 참조 응용 프로그램에는 개발 및 제작용 두 개의 모바일 플레이어 핸들러가 있습니다.

활동 경로가 mobileappoffers 핸들러의 경로 속성에 설정되면 처리기가 저장됩니다. 이제 처리기가 모바일 장치에 대한 오퍼를 렌더링할 준비가 됩니다.

### 렌더링 모드 {#render-mode}

mobileappoffers 핸들러는 게시 및 개발 설정에 대해 다르게 구성됩니다. 게시 설정의 경우 cq:ContentSyncConfig 노드에 *게시* 값이 ** 설정된 renderMode라는 속성이 있습니다. mobileappoffers 핸들러는 renderMode를 참조하고, 게시로 설정된 경우, 만들어진 mbox id를 수정합니다. 기본적으로 AEM에서 만든 mbox에는 mbox id에 —author 값이 추가됩니다. 이것은 활동이 게시되지 않았으므로 게시 취소된 캠페인을 오퍼 해상도에 사용해야 함을 나타냅니다.

Adobe Mobile Dashboard를 통해 컨텐츠가 스테이지된 경우 스테이지된 컨텐츠는 프로덕션 준비 컨텐츠로 간주되고 비개발 컨텐츠 동기화 구성을 통해 렌더링됩니다. 이렇게 렌더링하면 —author가 모든 mbox ID에서 제거되고 Target 서버에서 게시된 활동을 사용할 수 있을 것으로 예상됩니다. 스테이지된 컨텐츠를 테스트하기 전에 활동이 게시되었는지 확인합니다.

## 컨텐츠 만들기 {#creating-content}

이제 클라우드 서비스가 만들어졌고 mobileappoffers 핸들러가 구성되었으므로 콘텐츠 작성자는 타깃팅된 경험을 생성하기 시작할 수 있습니다.
