---
title: AEM Mobile 설정
description: 이 페이지를 따라 AEM Mobile을 설정하여 사용자가 Adobe Experience Manager(AEM) 내에서 콘텐츠를 만들고 관리할 수 있도록 합니다. 이 페이지에서는 AEM 인스턴스와 클라우드 기반 AEM Mobile On-demand Services 계정 및 프로젝트의 통합에 대한 정보를 제공합니다.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-on-demand-services-app
exl-id: 0ead982d-2315-4947-b762-596aa2aa42a1
source-git-commit: 99808cb38c5d376ccb7fb550c5212138890cec11
workflow-type: tm+mt
source-wordcount: '928'
ht-degree: 2%

---

# AEM Mobile 설정{#aem-mobile-setup}

>[!NOTE]
>
>Adobe 단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: React)이 필요한 프로젝트에는 SPA Editor를 사용하는 것이 좋습니다. [자세히 알아보기](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>AEM 6.2 또는 6.3에서 AEM 6.5로 마이그레이션하는 기존 AEM(Adobe Experience Manager) 모바일 앱 고객은 패키지 공유에서 패키지를 다운로드하여 AEM Mobile 앱을 계속 사용할 수 있습니다. 그러나 AEM 6.5의 새 설치는 AEM Mobile 앱 기능을 지원하지 않습니다.

AEM을 사용하여 AEM Mobile 앱용 콘텐츠를 생성하려면 AEM 인스턴스를 클라우드 기반 AEM Mobile On-demand Services 계정 및 프로젝트와 통합해야 합니다.

다음 단계에 따라 AEM Mobile을 설정하고 사용자가 AEM 내에서 콘텐츠를 만들고 관리할 수 있도록 합니다.

## AEM Mobile 프로비저닝 {#aem-mobile-provisioning}

AEM Mobile 설정을 시작하려면 다음을 수행해야 합니다.

* **API 키 요청**: 주문형 서비스 API에 액세스하려면 API 키를 요청해야 합니다. API 키를 요청하려면 다음을 수행하십시오. [PDF 양식](https://helpx.adobe.com/digital-publishing-solution/help/aem-mobile-end-of-life-faq.html). 완료된 양식을 Adobe Developer 지원 팀에 보내기: [wwds@adobe.com](mailto:wwds@adobe.com)

* **장치 ID 및 장치 토큰 생성**: API 키를 받으면 장치 ID 및 장치 토큰을 생성할 수 있습니다. 다음으로 이동 `https://aex.aemmobile.adobe.com` 다음을 수행합니다.

   * API 키 제공
   * 다음 권한으로 AEM Mobile 프로젝트에 추가한 Adobe ID으로 로그인합니다(프로젝트를 만들려면 아래 단계 참조)

      * 관리 > 프로젝트 및 사용자 관리
      * 컨텐츠 > 컨텐츠 추가 및 편집, 컨텐츠 삭제, 컨텐츠 보기, 컨텐츠 게시

모든 조건이 충족되면 장치 ID 및 장치 토큰이 생성됩니다.

>[!NOTE]
>
>필요한 Adobe ID에게 AEM Mobile 프로젝트에 대한 액세스 권한이 부여되어야 합니다. 다음을 참조하십시오 [AEM Mobile용 계정 관리](https://helpx.adobe.com/digital-publishing-solution/help/aem-mobile-end-of-life-faq.html) 온라인 도움말에서 참조할 수 있습니다.

## AEM Mobile에 대한 프로젝트 만들기 {#creating-projects-for-aem-mobile}

프로젝트를 만들 때 타겟팅하는 플랫폼(iOS, Android™, Windows 및 Desktop Web Viewer)에 대한 설정을 지정합니다. 지정하는 프로젝트 설정 중 대부분은 앱의 동작에 영향을 줍니다.

프로젝트를 만들려면 기본 관리자 역할이 있는 Adobe ID을 사용하여 온디맨드 서비스 포털에 로그인해야 합니다. 프로젝트를 편집하려면 기본 관리자 역할이나 **프로젝트 및 사용자 관리** 권한.

>[!NOTE]
>
>AEM Mobile에서 프로젝트 만들기에 대한 자세한 내용을 보려면 [여기](https://helpx.adobe.com/digital-publishing-solution/help/creating-projects.html).

## AEM Mobile 커넥터 구성 {#configuring-an-aem-mobile-connector}

AEM 설정에는 커넥터 구성에 대한 다음 단계가 포함됩니다. AEM Mobile 커넥터 구성이 완료되면 사용자는 사용자 그룹 및 권한을 설정할 수 있습니다.

AEM Mobile 온디맨드 커넥터는 AEM Mobile 관리 콘텐츠를 Adobe Experience Manager Mobile의 온디맨드 서비스와 바인딩하는 데 사용됩니다. 이를 통해 콘텐츠 작성자는 AEM 도구를 사용하여 모바일 애플리케이션용 자료를 만들고 관리하는 동시에 AEM Mobile의 온디맨드 서비스를 사용하여 모바일 콘텐츠를 손쉽게 배포할 수 있습니다.

>[!NOTE]
>
>AEM 인스턴스를 설정하는 1회성 단계입니다.

### AEM Mobile On-demand Services 클라이언트 구성 {#configuring-aem-mobile-on-demand-services-client}

AEM Mobile 통합이 올바르게 작동하도록 구성 단계를 완료합니다.

1. OSGI 서비스 구성으로 이동

   1. AEM > 도구 > 작업 > 웹 콘솔
   1. 스크롤 또는 검색 ***Experience Manager Mobile On-demand Services 클라이언트(Adobe Digital Publishing Solution 클라이언트임)***

1. 편집 ***Experience Manager Mobile On-demand Services 클라이언트***

   1. **(필수)** 필수 필드를 입력하십시오.

      1. 클라이언트 ID.
      1. 클라이언트 암호.

   1. **(선택 사항)** 기존 값을 편집합니다.

1. 변경 사항을 저장합니다.
1. 다음은 구성의 예입니다.

![chlimage_1-53](assets/chlimage_1-53.png)

### AEM Mobile On-demand Services CloudService 구성 {#configuring-aem-mobile-on-demand-services-cloudservice}

1. Cloud Service으로 이동합니다.

   1. AEM > 도구 > 배포> [CloudServices](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html). 스크롤 또는 검색 ***Adobe Experience Manager Mobile 온디맨드 서비스***

1. 선택 ***지금 구성*** 또는 ***구성 표시*** 구성 추가 아이콘을 선택합니다.

1. 구성 만들기

   1. 제목 및 이름 입력
   1. 장치 ID 입력
   1. 장치 토큰 입력
   1. 선택 ***장치 구성 테스트*** 입력한 값의 유효성을 검사할 수 있음
   1. 확인 선택

## AEM Mobile 사용자 역할 추가 및 권한 할당 {#adding-aem-mobile-user-roles-and-assigning-permissions}

프로젝트를 만든 후 역할을 만들고 사용자에게 액세스 권한을 부여해야 합니다. 기본 관리자만 역할을 만들고 편집할 수 있습니다. 역할을 만들 때는 해당 권한이 할당된 사용자에 대해 기능(또는 권한)을 활성화합니다. 예를 들어 앱 빌드에 대한 권한을 포함하는 역할과 콘텐츠를 만들고 게시하기 위한 권한을 포함하는 역할을 만들 수 있습니다.

AEM Mobile 앱 개발에서는 세 가지 역할이 있습니다.

* 관리자
* 개발자
* 작성자

앱 빌드 또는 콘텐츠 만들기 및 게시와 같이 다양한 권한으로 역할을 만드는 방법에 대한 자세한 내용을 보려면 다음을 클릭하십시오. [사용자 역할 만들기 및 액세스 권한 부여](https://helpx.adobe.com/digital-publishing-solution/help/account-admin-dps.html) AEM Mobile 도움말에서 참조할 수 있습니다.

>[!NOTE]
>
>앱 콘텐츠를 관리하려면 개발자, 콘텐츠 작성자 및 관리자의 공동 노력이 필요합니다. 작성자는 앱 개발자가 생성한 템플릿과 구성 요소를 기반으로 하는 페이지를 조작합니다. 마지막으로 관리자는 업데이트된 앱 컨텐츠를 전략적으로 게시합니다. AEM 그룹 및 권한을 설정하면 App Dashboard 또는 Control Center에서 해당 역할이 정의됩니다.
>
>다음을 참조하십시오 [AEM Mobile 대시보드](/help/mobile/mobile-apps-ondemand-application-dashboard.md).

앱 빌드나 콘텐츠 만들기 및 게시와 같이 다른 권한으로 역할 만들기를 완료하면 을 참조하십시오. [**사용자 및 사용자 그룹 구성**](/help/mobile/aem-mobile-configure-users.md). 이렇게 하면 모바일 앱의 작성 및 관리를 지원하도록 사용자 및 그룹을 구성하는 데 도움이 될 수 있습니다.

### 추가 리소스 {#additional-resources}

AEM Mobile On-demand Services 앱을 만들기 위한 다른 두 가지 역할과 책임에 대해 자세히 알아보려면 다음 리소스를 참조하십시오.

* [AEM Mobile On-demand Services용 AEM 컨텐츠 개발](/help/mobile/aem-mobile-on-demand.md)
* [AEM Mobile On-demand Services 앱용 AEM 컨텐츠 작성](/help/mobile/mobile-apps-ondemand.md)

>[!NOTE]
>
>찾아보기 페이지 및 문서를 포함하여 앱 컨텐츠를 미리 보려면 다음을 참조하십시오. [Preflight로 미리 보기](/help/mobile/aem-mobile-manage-ondemand-services.md).
