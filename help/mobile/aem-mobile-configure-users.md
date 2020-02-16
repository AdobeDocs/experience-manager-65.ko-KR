---
title: 사용자 및 사용자 그룹 구성
seo-title: 사용자 및 사용자 그룹 구성
description: 이 페이지에서 사용자 역할 및 모바일 온디맨드 서비스 앱의 제작 및 관리를 지원하도록 사용자 및 그룹을 구성하는 방법을 알아보십시오.
seo-description: 이 페이지에서 사용자 역할 및 모바일 온디맨드 서비스 앱의 제작 및 관리를 지원하도록 사용자 및 그룹을 구성하는 방법을 알아보십시오.
uuid: 461e1725-41dd-4883-92b9-a7e175660401
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-on-demand-services-app
discoiquuid: c3c73e67-7f85-4308-b4cd-1b42d4f3f2d9
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 사용자 및 사용자 그룹 구성 {#configure-your-users-and-user-groups}

>[!NOTE]
>
>단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: 응답)이 필요한 프로젝트에 SPA 편집기를 사용하는 것이 좋습니다. [추가 정보](/help/sites-developing/spa-overview.md).

이 장에서는 사용자 역할 및 모바일 앱 제작 및 관리를 지원하도록 사용자 및 그룹을 구성하는 방법에 대해 설명합니다.

## AEM Mobile 응용 프로그램 사용자 및 그룹 관리 {#aem-mobile-application-users-and-group-administration}

### AEM Mobile 애플리케이션 컨텐츠 작성자(앱 작성자 그룹) {#aem-mobile-application-content-authors-app-author-group}

앱 작성자 그룹의 구성원은 페이지, 텍스트, 이미지 및 비디오를 비롯한 AEM 모바일 애플리케이션 컨텐츠를 작성할 책임이 있습니다.

#### 그룹 구성 - 앱 작성자 {#group-configuration-app-authors}

1. &#39;앱 작성자&#39;라는 새 사용자 그룹을 만듭니다.

   사용자 관리 콘솔로 이동합니다. [http://localhost:4502/libs/granite/security/content/groupadmin.html](http://localhost:4502/libs/granite/security/content/groupadmin.html)

   사용자 그룹 콘솔 내에서 &#39;+&#39; 단추를 선택하여 그룹을 만듭니다.

   이 그룹의 ID를 &#39;app-authors&#39;로 설정하여 AEM 내의 모바일 애플리케이션 작성과 관련된 특정 유형의 작성자 사용자 그룹임을 나타냅니다.

1. 그룹에 구성원 추가:작성자

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. 앱 작성자 사용자 그룹을 만들었으므로 이제 사용자 관리 콘솔을 [통해 이 새 그룹에 개별 팀 구성원을 추가할 수](http://localhost:4502/libs/granite/security/content/useradmin.md)있습니다.

   ![chlimage_1-168](assets/chlimage_1-168.png)

1. 다음은 AEM의 컨텐츠 작성자 그룹에 추가할 수 있는 기능입니다.

   (읽기) 켜기

   * /app
   * /etc/clientlibs
   * /etc/designs
   * /etc/cloudservices/dps2015

### AEM Mobile 응용 프로그램 관리자 그룹(앱 관리자 그룹) {#aem-mobile-application-administrators-group-app-admins-group}

앱 관리자 그룹의 구성원은 앱 작성자와 동일한 권한을 가진 애플리케이션 컨텐츠를 작성할 수 있으며 **AND** 역시 다음 작업을 수행할 책임이 있습니다.

* 애플리케이션 컨텐츠 동기화 OTA 업데이트 준비, 게시 및 지우기

>[!NOTE]
>
>권한은 AEM 앱 명령 센터에서 일부 사용자 작업의 가용성을 결정합니다.
>
>앱 관리자에게는 앱 작성자가 사용할 수 있는 일부 옵션이 제공되지 않습니다.

### 그룹 구성 - 앱 관리자 {#group-configuration-app-admins}

1. 앱 관리라는 새 그룹을 만듭니다.
1. 새 앱 관리자 그룹에 다음 그룹을 추가합니다.

   * 컨텐츠 작성자
   * workflow-users
   ![chlimage_1-169](assets/chlimage_1-169.png)

   >[!NOTE]
   >
   >workflow-users is required to remote build with PhoneGap Build service

1. 권한 [콘솔로](http://localhost:4502/useradmin) 이동하고 권한을 추가하여 cloudservices 관리

   * (/etc/cloudservices/mobileserservices에서 읽기, 수정, 만들기, 삭제, 복제)

1. 동일한 권한 콘솔에서 스테이지에 권한을 추가하고 앱 콘텐츠 업데이트를 게시 및 지우십시오.

   * (/etc/packages/mobileapp의 읽기, 수정, 만들기, 삭제, 복제)
   * (읽기) /var/contentsync
   >[!NOTE]
   >
   >패키지 복제는 작성자 인스턴스에서 게시 인스턴스로 앱 업데이트를 게시하는 데 사용됩니다.

   >[!CAUTION]
   >
   >/var/contentsync 액세스가 거부되었습니다.
   >
   >READ 권한을 생략하면 빈 업데이트 패키지가 만들어지고 복제될 수 있습니다.

1. 필요에 따라 이 그룹에 구성원 추가
1. 컨텐츠 내보내기 또는 업로드하기

   * (읽기) 내보내기 템플릿에 액세스하기 위해 /etc/contentsync에서
   * (읽기) /var에서 읽기 시 경로 탐색
   * /var/contentsync에서(읽기, 쓰기, 수정, 삭제)ContentSync 캐시된 내보내기 컨텐츠를 작성, 읽기 및 정리할 수 있습니다.

### 추가 리소스 {#additional-resources}

AEM Mobile 온디맨드 서비스 앱 제작에 대한 다른 두 가지 역할과 책임에 대한 자세한 내용은 다음 리소스를 참조하십시오.

* [AEM Mobile 온디맨드 서비스용 AEM 콘텐츠 개발](/help/mobile/aem-mobile-on-demand.md)
* [AEM Mobile 온디맨드 서비스 앱용 AEM 콘텐츠 제작](/help/mobile/mobile-apps-ondemand.md)
