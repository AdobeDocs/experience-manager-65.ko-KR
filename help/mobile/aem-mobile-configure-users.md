---
title: 사용자 및 사용자 그룹 구성
description: 이 페이지를 따라 사용자 역할과 모바일 On-Demand 서비스 앱 작성 및 관리를 지원하도록 사용자 및 그룹을 구성하는 방법을 이해합니다.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-on-demand-services-app
exl-id: 58b7d1b9-a851-442a-9d02-212cad8abbed
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 1%

---

# 사용자 및 사용자 그룹 구성 {#configure-your-users-and-user-groups}

{{ue-over-mobile}}

이 장에서는 사용자 역할과 모바일 앱의 작성 및 관리를 지원하도록 사용자 및 그룹을 구성하는 방법에 대해 설명합니다.

## AEM Mobile 애플리케이션 사용자 및 그룹 관리 {#aem-mobile-application-users-and-group-administration}

### AEM Mobile 애플리케이션 콘텐츠 작성자(앱 작성자 그룹) {#aem-mobile-application-content-authors-app-author-group}

앱 작성자 그룹의 멤버는 페이지, 텍스트, 이미지 및 비디오를 비롯한 AEM 모바일 애플리케이션 콘텐츠를 작성합니다.

#### 그룹 구성 - app-authors {#group-configuration-app-authors}

1. &#39;app-authors&#39;라는 사용자 그룹 만들기:

   사용자 Admin Console([http://localhost:4502/libs/granite/security/content/groupadmin.html](http://localhost:4502/libs/granite/security/content/groupadmin.html))로 이동합니다.

   사용자 그룹 콘솔 내에서 &#39;+&#39; 버튼을 선택하여 그룹을 만듭니다.

   이 그룹의 ID를 &#39;app-authors&#39;로 설정하여 AEM 내의 모바일 애플리케이션 작성에 관련된 특정 유형의 작성자 사용자 그룹임을 나타냅니다.

1. 그룹에 구성원 추가: 작성자

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. 앱 작성자 사용자 그룹을 만들었으므로 이제 [사용자 Admin Console](http://localhost:4502/libs/granite/security/content/useradmin.md)을 통해 개별 팀원을 이 새 그룹에 추가할 수 있습니다.

   ![chlimage_1-168](assets/chlimage_1-168.png)

1. 다음을 AEM의 콘텐츠 작성자 그룹에 추가할 수 있습니다.

   (읽기) 일자

   * /app
   * /etc/clientlibs
   * /etc/designs
   * /etc/cloudservices/dps2015

### AEM Mobile 애플리케이션 관리자 그룹(app-admins 그룹) {#aem-mobile-application-administrators-group-app-admins-group}

app-admins 그룹의 구성원은 app-authors **AND**&#x200B;에 포함된 권한과 동일한 권한으로 응용 프로그램 콘텐츠를 작성할 수 있으며, 다음 작업도 담당합니다.

* 응용 프로그램 스테이징, 게시 및 지우기 ContentSync OTA 업데이트

>[!NOTE]
>
>권한은 AEM 앱 명령 센터에서 일부 사용자 작업의 가용성을 결정합니다.
>
>앱 관리자가 사용할 수 있는 앱 작성자는 일부 옵션을 사용할 수 없습니다.

### 그룹 구성 - app-admins {#group-configuration-app-admins}

1. app-admins라는 그룹을 만듭니다.
1. 새 app-admins 그룹에 다음 그룹을 추가합니다.

   * content-authors
   * 워크플로 사용자

   ![chlimage_1-169](assets/chlimage_1-169.png)

   >[!NOTE]
   >
   >워크플로우 사용자는 PhoneGap Build 서비스를 사용하여 원격 빌드를 수행해야 합니다.

1. [권한 콘솔](http://localhost:4502/useradmin)(으)로 이동하여 cloudservices를 관리할 권한을 추가하십시오.

   * /etc/cloudservices/mobileservices에서 (읽기, 수정, 만들기, 삭제, 복제)

1. 동일한 권한 콘솔에서 앱 콘텐츠 업데이트를 스테이징하고 게시하고 지우는 권한을 추가합니다.

   * /etc/packages/mobileapp에서 (읽기, 수정, 만들기, 삭제, 복제)
   * /var/contentsync에서 (읽기)

   >[!NOTE]
   >
   >패키지 복제는 작성자 인스턴스에서 게시 인스턴스로 앱 업데이트를 게시하는 데 사용됩니다.

   >[!CAUTION]
   >
   >/var/contentsync 액세스가 즉시 거부됩니다.
   >
   >READ 권한을 생략하면 빈 업데이트 패키지가 빌드 및 복제될 수 있습니다.

1. 필요에 따라 이 그룹에 구성원 추가
1. 컨텐츠를 내보내거나 업로드하려면

   * (읽기) /etc/contentsync에서 내보내기 템플릿에 액세스
   * (읽기) on /var to path traversal on reads
   * ContentSync 캐시된 내보내기 컨텐츠를 작성, 읽기 및 정리하려면 /var/contentsync에 (읽기, 쓰기, 수정, 삭제)

### 추가 리소스 {#additional-resources}

AEM Mobile On-demand Services 앱을 만들기 위한 다른 두 가지 역할과 책임에 대해 자세히 알아보려면 다음 리소스를 참조하십시오.

* [AEM Mobile On-demand Services용 AEM 컨텐츠 개발](/help/mobile/aem-mobile-on-demand.md)
* [AEM Mobile On-demand Services 앱용 AEM 컨텐츠 작성](/help/mobile/mobile-apps-ondemand.md)
