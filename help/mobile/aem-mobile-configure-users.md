---
title: 사용자 및 사용자 그룹 구성
seo-title: 사용자 및 사용자 그룹 구성
description: 모바일 온디맨드 서비스 앱 제작 및 관리를 지원하도록 사용자 역할 및 사용자 및 그룹을 구성하는 방법에 대해 이해하려면 이 페이지를 따르십시오.
seo-description: 모바일 온디맨드 서비스 앱 제작 및 관리를 지원하도록 사용자 역할 및 사용자 및 그룹을 구성하는 방법에 대해 이해하려면 이 페이지를 따르십시오.
uuid: 461e1725-41dd-4883-92b9-a7e175660401
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-on-demand-services-app
discoiquuid: c3c73e67-7f85-4308-b4cd-1b42d4f3f2d9
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 1%

---


# 사용자 및 사용자 그룹 구성 {#configure-your-users-and-user-groups}

>[!NOTE]
>
>단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: 응답)이 필요한 프로젝트에는 SPA 편집기를 사용하는 것이 좋습니다. [추가 정보](/help/sites-developing/spa-overview.md).

이 장에서는 사용자 역할과 모바일 앱 제작 및 관리를 지원하도록 사용자 및 그룹을 구성하는 방법에 대해 설명합니다.

## AEM Mobile 응용 프로그램 사용자 및 그룹 관리 {#aem-mobile-application-users-and-group-administration}

### AEM Mobile 응용 프로그램 내용 작성자(앱 작성자 그룹) {#aem-mobile-application-content-authors-app-author-group}

앱 작성자 그룹의 구성원은 AEM 모바일 애플리케이션 컨텐츠(예: 페이지, 텍스트, 이미지 및 비디오)를 제작할 책임이 있습니다.

#### 그룹 구성 - app-authors {#group-configuration-app-authors}

1. &#39;app-authors&#39;라는 새 사용자 그룹을 만듭니다.

   사용자 Admin Console으로 이동합니다.[http://localhost:4502/libs/granite/security/content/groupadmin.html](http://localhost:4502/libs/granite/security/content/groupadmin.html)

   사용자 그룹 콘솔 내에서 &#39;+&#39; 단추를 선택하여 그룹을 만듭니다.

   이 그룹의 ID를 &#39;app-authors&#39;로 설정하여 이 그룹이 AEM 내에서 모바일 응용 프로그램을 작성하는 데 사용되는 특정 유형의 작성자 사용자 그룹임을 나타낼 수 있습니다.

1. 그룹에 구성원 추가:작성자

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. 앱 작성자 사용자 그룹을 만들었으므로 이제 [사용자 관리 콘솔](http://localhost:4502/libs/granite/security/content/useradmin.md)을 통해 이 새 그룹에 개별 팀 구성원을 추가할 수 있습니다.

   ![chlimage_1-168](assets/chlimage_1-168.png)

1. 다음은 AEM 컨텐츠 작성자 그룹에 추가할 수 있는 기능입니다.

   (읽기)

   * /app
   * /etc/clientlibs
   * /etc/designs
   * /etc/cloudservices/dps2015

### AEM Mobile 응용 프로그램 관리자 그룹(앱 관리자 그룹) {#aem-mobile-application-administrators-group-app-admins-group}

app-admins 그룹의 구성원은 app-authors **AND**&#x200B;에 포함된 동일한 권한으로 응용 프로그램 콘텐츠를 제작할 수 있으며 다음과 같은 책임도 집니다.

* 애플리케이션 컨텐츠 동기화 업데이트 준비, 게시 및 지우기

>[!NOTE]
>
>권한은 AEM 앱 명령 센터에서 일부 사용자 작업의 가용성을 결정합니다.
>
>앱 관리자에게는 사용 가능한 앱 작성자 옵션이 표시되지 않습니다.

### 그룹 구성 - 앱-관리자 {#group-configuration-app-admins}

1. 앱 관리라는 새 그룹을 만듭니다.
1. 새 app-admins 그룹에 다음 그룹을 추가합니다.

   * content-authors
   * workflow-users

   ![chlimage_1-169](assets/chlimage_1-169.png)

   >[!NOTE]
   >
   >워크플로 사용자는 PhoneGap Build 서비스를 사용하여 원격 빌드를 수행해야 합니다.

1. [권한 콘솔](http://localhost:4502/useradmin)로 이동하고 클라우드 서비스 관리에 권한을 추가합니다.

   * (/etc/cloudservices/mobilesservices의 읽기, 수정, 만들기, 삭제, 복제)

1. 동일한 권한 콘솔에서 앱 컨텐츠 업데이트를 준비, 게시 및 지우십시오.

   * (/etc/packages/mobileapp의 읽기, 수정, 만들기, 삭제, 복제)
   * (읽기) /var/contentsync

   >[!NOTE]
   >
   >패키지 복제는 작성자 인스턴스에서 게시 인스턴스로 앱 업데이트를 게시하는 데 사용됩니다.

   >[!CAUTION]
   >
   >/var/contentsync 액세스가 OOTB가 거부되었습니다.
   >
   >READ 권한을 생략하면 빈 업데이트 패키지가 빌드되고 복제될 수 있습니다.

1. 필요에 따라 이 그룹에 구성원 추가
1. 콘텐트 내보내기 또는 업로드하려면

   * (읽기) 내보내기 템플릿에 액세스하려면 /etc/contentsync에서
   * 읽기 시 경로 순회를 위해 /var에서
   * /var/contentsync에서(읽기, 쓰기, 수정, 삭제) ContentSync 캐시된 내보내기 콘텐츠를 쓰기, 읽기 및 정리할 수 있습니다.

### 추가 리소스 {#additional-resources}

AEM Mobile On-demand Services 앱 만들기에 대한 다른 2가지 역할과 책임에 대한 자세한 내용은 다음 리소스를 참조하십시오.

* [AEM Mobile On-demand Services용 AEM 컨텐츠 개발](/help/mobile/aem-mobile-on-demand.md)
* [AEM Mobile On-demand Services 앱용 AEM 콘텐츠 제작](/help/mobile/mobile-apps-ondemand.md)
