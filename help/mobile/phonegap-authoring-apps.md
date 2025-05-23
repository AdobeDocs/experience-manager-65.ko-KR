---
title: 모바일 애플리케이션 작성
description: AEM Mobile Dashboard를 사용하면 모바일 애플리케이션을 생성, 빌드 및 배포하고 애플리케이션 메타데이터를 생성, 삭제 및 편집할 수 있습니다. 자세한 내용은 이 페이지를 참조하십시오.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
exl-id: 073daff7-0c1d-4715-bfd4-3e2336e4cb88
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '982'
ht-degree: 0%

---

# 모바일 애플리케이션 작성{#authoring-mobile-applications}

{{ue-over-mobile}}

AEM Mobile Dashboard를 사용하면 모바일 애플리케이션을 생성, 빌드 및 배포하고 애플리케이션 메타데이터를 생성, 삭제 및 편집할 수 있습니다. 애플리케이션이 실행되면 라이프사이클 및 사용 지표를 포함한 애플리케이션 분석을 분석하여 고객 전환 및 브랜드 충성도를 향상시킬 수 있습니다.

AEM Mobile 응용 프로그램을 빌드하려면 [모바일 응용 프로그램 빌드](/help/mobile/building-app-mobile-phonegap.md) 페이지를 참조하십시오.

환경을 설정하고 시작하려면 [AEM PhoneGap Enterprise 사용을 위한 AEM 관리](/help/mobile/administer-phonegap.md)를 참조하십시오.

## AEM Mobile 앱 카탈로그 {#the-aem-mobile-apps-catalog}

[AEM Mobile 앱 카탈로그](http://localhost:4502/aem/apps.html/content/phonegap)는 AEM에서 관리되는 모든 모바일 앱을 표시합니다.

이 카탈로그를 관리자가 템플릿을 기반으로 만들거나 모바일 개발자가 이미 시작한 기존 앱을 업로드하여 새 AEM Mobile 애플리케이션을 시작할 수 있는 AEM Mobile의 &quot;랜딩 페이지&quot;로 생각해 보십시오.

다음 단계에 따라 앱 카탈로그 랜딩 페이지로 이동합니다.

1. **탐색**(으)로 이동한 다음 **모바일**&#x200B;을 선택합니다.

1. 앱 카탈로그를 열려면 **앱**&#x200B;을 선택하십시오.

![AEM Mobile 앱 카탈로그](assets/chlimage_1-135.png)

## AEM Mobile 앱 대시보드 {#the-aem-mobile-app-dashboard}

카탈로그에서 AEM Mobile 앱을 선택하면 해당 대시보드가 표시됩니다. 여기에서 애플리케이션을 관리하고, 통계를 보고, 모바일 앱 콘텐츠를 빌드하고, 배포하고, 관리할 수 있습니다.

오른쪽 아래 모서리에 있는 &#39;...&#39;를 클릭하여 AEM Mobile 대시보드의 각 타일을 확장하여 세부 정보를 보거나 편집할 수 있습니다.

![AEM Mobile 응용 프로그램 명령 센터](assets/chlimage_1-136.png)

### 앱 관리 타일 {#the-manage-app-tile}

앱 관리 타일에는 애플리케이션 아이콘, 이름, 설명, 지원되는 플랫폼, 업데이트 URL 및 버전 정보에 대한 콜 홈이 표시됩니다. 이 타일로 드릴다운하여 PhoneGap 응용 프로그램 구성(config.xml)을 편집하고 유지 관리하며 응용 프로그램을 다양한 응용 프로그램 저장소에 제출하여 배포하도록 준비할 수 있습니다.

자세한 내용을 보려면 [여기](/help/mobile/phonegap-app-details-tile.md)를 클릭하십시오.

![chlimage_1-137](assets/chlimage_1-137.png)

### 페이지 콘텐츠 관리 타일 {#the-manage-page-content-tile}

AEM Sites 내에서 동일한 작업을 수행하는 것과 거의 동일한 방식으로 AEM Mobile에서 컨텐츠를 만들고, 업데이트하고, 삭제할 수 있습니다. **페이지 콘텐츠 관리 타일**&#x200B;은 관리되는 콘텐츠와 마지막으로 수정한 콘텐츠의 페이지 수를 표시합니다. 타일에서 각 레코드를 클릭하여 페이지를 만들고, 복사하고, 이동하고, 삭제하고, 업데이트하기 위해 콘텐츠를 드릴인할 수 있습니다. 콘텐츠가 업데이트되면 **콘텐츠 패키지 관리 타일을 통해 고객에게 콘텐츠 업데이트를 푸시할 수 있습니다.**

![콘텐츠 타일](assets/chlimage_1-138.png)

### 콘텐츠 패키지 관리 타일 {#the-manage-content-packages-tile}

페이지 콘텐츠 관리 타일을 통해 콘텐츠를 추가하거나 수정한 후에는 콘텐츠 릴리스 업데이트를 통해 이러한 변경 사항을 고객에게 푸시할 수 있습니다.

콘텐츠 패키지를 사용하면 AEM 앱 작성자가 AEM에서 페이지 콘텐츠를 관리하고 개발 팀이 PhoneGap Shell 애플리케이션(즉, 앱 프레임워크 또는 인프라)을 변경한 다음 개발자가 다양한 스토어에 배포용으로 다시 제출하도록 등록할 필요 없이 이러한 변경 사항을 고객에게 신속하게 푸시할 수 있습니다.

콘텐츠 패키지는 각 업데이트에 대해 콘텐츠 릴리스 패키지로 간주되는 ZIP 파일을 만듭니다. 이러한 패키지에는 앱을 렌더링하는 동안 생성된 html 리소스 및 html 페이지가 포함되어 있으며 지능적으로 마지막 업데이트 이후 수정된 파일만 패키징할 수 있습니다.

콘텐츠 패키지 관리 타일의 **Type** 열에는 개발자가 관리하는 앱의 프레임워크나 인프라와 같은 응용 프로그램 셸 콘텐츠를 나타내는 &#39;App&#39; 또는 콘텐츠 작성자가 관리하는 페이지 콘텐츠를 나타내는 &#39;Content&#39;가 표시됩니다.

콘텐츠는 언어로 또는 앱에서 여러 콘텐츠 릴리스 패키지를 사용하는 앱의 특정 부분으로 표시될 수 있습니다. 컨텐츠 번들 방식을 유연하게 선택할 수 있으며, 애플리케이션에 대한 컨텐츠 관리 방식을 완벽하게 선택할 수 있습니다.

**수정됨** 열은 페이지가 가장 최근에 수정된 시기를 나타냅니다.

**스테이징된** 열은 마지막으로 콘텐츠 업데이트를 만든 시기를 표시합니다. 콘텐츠 업데이트를 만들고 변경 사항을 스테이징하려면 타일의 레코드를 열고 업데이트를 만듭니다.

**게시됨** 열은 마지막 콘텐츠 업데이트가 게시되어 고객이 사용할 수 있게 된 시기를 표시합니다. 콘텐츠를 게시하려면 먼저 해당 콘텐츠를 스테이징한 다음 이 타일로 드릴다운하고 콘텐츠 릴리스 세부 정보 콘솔에서 게시하여 업데이트를 게시해야 합니다.

![콘텐츠 릴리스 타일](assets/chlimage_1-139.png) ![앱 셸에 대한 ContentSync 패키지](do-not-localize/chlimage_1-5.png)

이 아이콘은 앱 셸의 콘텐츠 릴리스 패키지를 나타냅니다

![두 개의 사각형으로 겹치는 패키지 기호로 표시된 콘텐츠 릴리스 패키지 아이콘](do-not-localize/chlimage_1-6.png)

이러한 아이콘은 앱 컨텐츠에 대한 컨텐츠 릴리스 패키지를 나타냅니다

### PhoneGap Build 타일 {#the-phonegap-build-tile}

**PhoneGap Build 타일**&#x200B;이 `https://build.phonegap.com`과(와) 연결하여 원격 빌드를 빌드하고 호스팅합니다. 빌드가 빌드되면 다운로드로 사용하거나 QR 코드를 통해 디바이스에 직접 사용할 수 있습니다.

또는 PhoneGap CLI(`https://docs.phonegap.com/en/3.5.0/guide_cli_index.md.html`)를 통해 로컬로 빌드할 장치 원본을 다운로드할 수 있습니다.

![PhoneGap Build 타일](assets/chlimage_1-140.png)

### 지표 타일 {#the-metrics-tile}

>[!CAUTION]
>
>지표 타일은 클라우드 서비스를 구성한 후에만 표시됩니다.
>
>자세한 내용은 [Adobe Mobile Services Cloud Service 구성](/help/mobile/configure-adobe-mobile-cloud-service.md)을 참조하십시오.

AEM Mobile은 [Adobe Mobile Services SDK](https://experienceleague.adobe.com/docs/mobile.html?lang=ko)(AMS)를 통해 Adobe Analytics과 통합됩니다.

컨트롤 센터 **지표 타일**&#x200B;은 응용 프로그램에 대해 AMS에서 가져온 요약 분석을 표시합니다. 오른쪽 하단에 있는 &#39;...&#39;를 클릭하여 분석 대시보드로 드릴다운할 수 있습니다.

![지표 타일](assets/chlimage_1-141.png)

### 엔티티 컨텐츠 관리 타일 {#the-manage-entity-content-tile}

엔티티 컨텐츠 관리 타일을 사용하여 앱 정의를 추가하고 관리할 수 있습니다. 앱 정의는 앱에 적합한 공간(및 기타 구성)을 식별하는 방법입니다. 이렇게 하면 앱을 다시 컴파일하지 않고도 새 공간을 추가할 수 있습니다. 앱 정의가 업데이트되고, 여기에 새 스페이스에 대한 정보가 포함됩니다.

앱 정의를 만들고 관리하려면 [여기](/help/mobile/phonegap-app-definitions.md)를 클릭하세요.

오른쪽 하단에 있는 &#39;...&#39;를 클릭하여 엔티티 컨텐츠 관리 대시보드로 드릴다운할 수 있습니다.

![chlimage_1-142](assets/chlimage_1-142.png)

#### 추가 리소스 {#additional-resources}

관리자 및 개발자의 역할과 책임에 대해 알아보려면 아래 리소스를 참조하십시오.

* [AEM을 사용하여 Adobe PhoneGap Enterprise용 개발](/help/mobile/developing-in-phonegap.md)
* [AEM을 사용하여 Adobe PhoneGap Enterprise용 컨텐츠 관리](/help/mobile/administer-phonegap.md)
