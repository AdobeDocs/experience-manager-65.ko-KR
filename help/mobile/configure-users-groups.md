---
title: 사용자 및 사용자 그룹 구성
description: 이 페이지를 따라 사용자 역할과 모바일 앱의 작성 및 관리를 지원하도록 사용자 및 그룹을 구성하는 방법을 이해합니다.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
exl-id: 9f814204-8cd4-4ba9-9e25-3ff1b25c1955
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 1%

---

# 사용자 및 사용자 그룹 구성 {#configure-your-users-and-user-groups}

{{ue-over-mobile}}

이 장에서는 사용자 역할과 모바일 앱의 작성 및 관리를 지원하도록 사용자 및 그룹을 구성하는 방법에 대해 설명합니다.

## AEM Mobile 애플리케이션 사용자 및 그룹 관리 {#aem-mobile-application-users-and-group-administration}

AEM 앱에 대한 권한 모델을 구성하고 관리하는 데 도움이 되도록 다음 두 개의 그룹을 사용할 수 있습니다.

* 앱 관리자용 앱 관리자
* 앱 작성자용 app-authors

### AEM Mobile 애플리케이션 콘텐츠 작성자(앱 작성자 그룹) {#aem-mobile-application-content-authors-app-author-group}

앱 작성자 그룹의 멤버는 페이지, 텍스트, 이미지 및 비디오를 비롯한 AEM 모바일 애플리케이션 콘텐츠를 작성합니다.

#### 그룹 구성 - app-authors {#group-configuration-app-authors}

1. &#39;app-authors&#39;라는 사용자 그룹 만들기:

   사용자 Admin Console([http://localhost:4502/libs/granite/security/content/groupadmin.html](http://localhost:4502/libs/granite/security/content/groupadmin.html))로 이동합니다.

   사용자 그룹 콘솔 내에서 &#39;+&#39; 버튼을 선택하여 그룹을 만듭니다.

   이 그룹의 ID를 &#39;app-authors&#39;로 설정하여 AEM 내의 모바일 애플리케이션 작성에 관련된 특정 유형의 작성자 사용자 그룹임을 나타냅니다.

1. 그룹에 구성원 추가: 작성자

   ![chlimage_1-18](assets/chlimage_1-18.png)

   Authors 그룹에 앱 작성자 추가

1. 앱 작성자 사용자 그룹을 만들었으므로 이제 [사용자 Admin Console](http://localhost:4502/libs/granite/security/content/useradmin.md)을 통해 개별 팀원을 이 새 그룹에 추가할 수 있습니다.

   ![chlimage_1-19](assets/chlimage_1-19.png)

   사용자 그룹 편집

1. [권한 콘솔](http://localhost:4502/useradmin)(으)로 이동하여 cloudservices를 관리할 권한을 추가하십시오.

   * (읽기) on /etc/cloudservices

   >[!NOTE]
   >
   >앱 작성자는 /content/phonegap에서 콘텐츠를 만드는 기능을 상속받도록 AEM에서 기본 콘텐츠 작성자(작성자) 그룹을 확장합니다

### AEM Mobile 애플리케이션 관리자 그룹(app-admins 그룹) {#aem-mobile-application-administrators-group-app-admins-group}

app-admins 그룹의 구성원은 app-authors **AND**&#x200B;에 포함된 권한과 동일한 권한으로 응용 프로그램 콘텐츠를 작성할 수 있으며, 다음 작업도 담당합니다.

* AEM에서 PhoneGap Build 및 Adobe Mobile Services 클라우드 서비스 구성
* 응용 프로그램 컨텐츠 동기화 OTA 업데이트 준비, 게시 및 지우기

>[!NOTE]
>
>권한은 AEM 앱 명령 센터에서 일부 사용자 작업의 가용성을 결정합니다.
>
>앱 관리자가 사용할 수 있는 앱 작성자는 일부 옵션을 사용할 수 없습니다.

#### 그룹 구성 - app-admins {#group-configuration-app-admins}

1. app-admins라는 그룹을 만듭니다.
1. 새 app-admins 그룹에 다음 그룹을 추가합니다.

   * content-authors
   * 워크플로 사용자

   ![chlimage_1-20](assets/chlimage_1-20.png)

1. [권한 콘솔](http://localhost:4502/useradmin)(으)로 이동하여 cloudservices를 관리할 권한을 추가하십시오.

   * /etc/cloudservices/mobileservices에서 (읽기, 수정, 만들기, 삭제, 복제)
   * /etc/cloudservices/phonegap-build에서 (읽기, 수정, 만들기, 삭제, 복제)

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

## 대시보드 타일 권한 {#dashboard-tile-permissions}

대시보드 타일은 사용자가 보유한 권한에 따라 다른 작업을 노출할 수 있습니다. 다음은 각 타일에 사용할 수 있는 작업을 설명합니다.

이러한 권한 외에도 현재 앱이 구성된 방식에 따라 작업을 표시하거나 숨길 수 있습니다. 예를 들어 PhoneGap 클라우드 구성이 앱에 할당되지 않은 경우 &#39;원격 빌드&#39; 작업을 노출하는 지점이 없습니다. 다음은 &#39;**구성 조건**&#39; 섹션 아래에 나와 있습니다.

### 앱 타일 관리 {#manage-app-tile}

타일에는 현재 권한이 필요한 작업이 없지만 응용 프로그램에 대한 세부 정보 페이지에는 다음 작업이 있습니다.

* 앱 작성자 및 앱 관리자에 대한 *편집*(UI 트리거 - jcr:write - on /content/phonegap/{suffix})
* 앱 작성자 및 앱 관리자용 *다운로드*(UI 트리거 - /content/phonegap/{suffix})

아래 이미지는 앱에 대한 다운로드 및 편집 옵션을 보여 줍니다.

![chlimage_1-21](assets/chlimage_1-21.png)
