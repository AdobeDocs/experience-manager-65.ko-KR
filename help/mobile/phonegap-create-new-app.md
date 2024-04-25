---
title: 만들기 마법사를 사용하여 AEM Mobile 앱 만들기
description: AEM Mobile 앱은 페이지 구조 및 속성을 정의하는 블루프린트를 기반으로 합니다. 이 페이지를 따라 앱 템플릿을 기반으로 앱을 만드는 방법에 대해 알아보십시오.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
exl-id: be093025-b19f-4499-a7b5-aae5ab74f966
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 2%

---

# 만들기 마법사를 사용하여 AEM Mobile 앱 만들기{#creating-a-new-aem-mobile-app-using-create-wizard}

>[!NOTE]
>
>Adobe 단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: React)이 필요한 프로젝트에는 SPA Editor를 사용하는 것이 좋습니다. [자세히 알아보기](/help/sites-developing/spa-overview.md).

AEM Mobile 앱은 페이지 구조 및 속성을 정의하는 블루프린트를 기반으로 합니다. 다음 애플리케이션 속성을 구성할 수 있습니다.

* **제목:** 애플리케이션 제목입니다.
* **대상 경로:** 저장소에서 응용 프로그램이 저장되는 위치입니다. 앱 이름을 기반으로 경로를 만들려면 기본값을 둡니다.

* **이름:** 기본값은 공백 문자가 제거된 Title 속성 값입니다. 이 이름은 AEM 내에서 응용 프로그램을 참조하는 데 사용됩니다(예: 응용 프로그램을 나타내는 저장소 노드).
* **설명:** 애플리케이션에 대한 설명.
* **서버 URL:** OTA(Over-the-Air) 콘텐츠를 애플리케이션에 제공하는 URL입니다. 기본값은 응용 프로그램을 만드는 데 사용되는 인스턴스의 게시 서버 URL입니다(외부화 서비스에서 가져옴). 참고: 이는 인증이 필요한 작성자가 아닌 게시 서버 인스턴스여야 합니다.

애플리케이션 썸네일로 사용할 이미지 파일을 제공하고, 사용할 PhoneGap Build 구성을 선택하고, 사용할 Mobile App Analytics 구성을 선택할 수도 있습니다. 이 이미지는 Experience Manager의 모바일 앱 콘솔 내에서 모바일 애플리케이션을 나타내는 축소판으로만 사용됩니다.

Adobe 클라우드 서비스를 빌드하고 Mobile Services SDK 플러그인을 앱에 통합하기 위한 추가(및 선택 사항) 탭이 있습니다.

* 빌드: 구성 관리 를 클릭하고 여기에서 build.phonegap.com 빌드 서비스를 설정합니다. 그런 다음 드롭다운에서 새로 만든 PhoneGap Build 클라우드 서비스를 선택할 수 있습니다.
* Analytics: 구성 관리 를 클릭하고 다음을 설정합니다. [Adobe Mobile Services SDK](https://experienceleague.adobe.com/docs/mobile-services/using/home.html) 클라우드 서비스. 그런 다음 드롭다운에서 모바일 앱에 통합할 새로 만든 모바일 서비스를 선택할 수 있습니다.

## 앱 템플릿 사용 {#using-app-templates}

앱 템플릿은 개발자가 만든 기존 디자인을 AEM 내에서 새 앱을 만드는 데 사용하는 간편한 방법을 제공합니다.

앱 템플릿이란 무엇입니까? 앱의 기준선이나 기반을 나타내는 페이지 템플릿과 구성 요소의 컬렉션으로 생각하십시오.
다른 앱의 템플릿을 기반으로 앱을 만들 때 앱이 만들어진 원본 앱을 나타내는 시작점이 있는 앱을 받게 됩니다.

이 기능을 사용하려면 기존 모바일 앱 템플릿(또는 앱 템플릿이 설치된 앱)이 있어야 합니다.

최신 AEM 앱 샘플 패키지에는 앱 템플릿과 함께 업데이트된 버전의 Geometrixx 앱이 포함되어 있습니다. 또는 다음을 설치할 수 있습니다. [StarterKit](https://github.com/Adobe-Marketing-Cloud-Apps/aem-phonegap-starter-kit) 템플릿도 제공합니다.

앱 템플릿을 기반으로 앱을 만드는 절차:

1. AEM Mobile 앱 카탈로그로 이동합니다. &lt;*server-url*>aem/apps.html/content/mobileapps
1. 선택 **만들기** 을(를) 선택한 다음 **앱** 아래와 같이

![chlimage_1-158](assets/chlimage_1-158.png)

AEM 개발자가 사용할 수 있는 앱 템플릿을 선택합니다. 다음을 참조하십시오 [AEM Mobile 앱 구조](/help/mobile/phonegap-structure-an-app.md) 개발자 지원.

![chlimage_1-159](assets/chlimage_1-159.png)

필요에 따라 썸네일 이미지 변경을 포함하여 새 앱의 세부 정보를 입력합니다. 이러한 값은 나중에 **앱 관리** 타일.

![chlimage_1-160](assets/chlimage_1-160.png)

## 다음 단계 {#the-next-steps}

다른 작성 역할에 대한 자세한 내용은 다음 리소스를 참조하십시오.

* [앱 관리 타일](/help/mobile/phonegap-app-details-tile.md)
* [앱 메타데이터 편집](/help/mobile/phonegap-editmetadata.md)
* [앱 정의](/help/mobile/phonegap-app-definitions.md)
* [기존 하이브리드 앱 가져오기](/help/mobile/phonegap-adding-content-to-imported-app.md)
* [Content Services](/help/mobile/develop-content-as-a-service.md)

## 추가 리소스 {#additional-resources}

관리자 및 개발자의 역할과 책임에 대해 알아보려면 아래 리소스를 참조하십시오.

* [AEM을 사용하여 Adobe PhoneGap Enterprise용 개발](/help/mobile/developing-in-phonegap.md)
* [AEM을 사용하여 Adobe PhoneGap Enterprise용 컨텐츠 관리](/help/mobile/administer-phonegap.md)
