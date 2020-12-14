---
title: 모바일 애플리케이션 작성
seo-title: 모바일 애플리케이션 작성
description: aem mobile Dashboard를 사용하여 모바일 애플리케이션을 제작, 구축 및 배포하고 애플리케이션 메타데이터를 생성, 삭제 및 편집할 수 있습니다. 자세한 내용은 이 페이지를 참조하십시오.
seo-description: aem mobile Dashboard를 사용하여 모바일 애플리케이션을 제작, 구축 및 배포하고 애플리케이션 메타데이터를 생성, 삭제 및 편집할 수 있습니다. 자세한 내용은 이 페이지를 참조하십시오.
uuid: 293b5d29-df7e-42dd-ae64-8c677317e7a5
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
discoiquuid: abfeea65-102d-4800-abeb-304d61afcc13
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1053'
ht-degree: 0%

---


# 모바일 응용 프로그램 작성{#authoring-mobile-applications}

>[!NOTE]
>
>단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: 응답)이 필요한 프로젝트에는 SPA 편집기를 사용하는 것이 좋습니다. [추가 정보](/help/sites-developing/spa-overview.md).

AEM Mobile Dashboard를 사용하면 모바일 애플리케이션을 제작, 구축 및 배포하고 애플리케이션 메타데이터를 생성, 삭제 및 편집할 수 있습니다. 애플리케이션이 라이브되면 라이프사이클 및 사용 지표를 비롯한 애플리케이션 분석을 분석하여 고객 전환율과 브랜드 충성도를 향상시킬 수 있습니다.

AEM Mobile 응용 프로그램을 빌드하려면 [모바일 응용 프로그램 빌드](/help/mobile/building-app-mobile-phonegap.md) 페이지를 참조하십시오.

환경을 설정하고 시작하려면 [AEM PhoneGap Enterprise 사용 관리](/help/mobile/administer-phonegap.md)를 참조하십시오.

## AEM Mobile 앱 카탈로그 {#the-aem-mobile-apps-catalog}

[AEM Mobile 앱 카탈로그](http://localhost:4502/aem/apps.html/content/phonegap)에는 AEM에서 관리되는 모든 모바일 앱이 표시됩니다.

이 카탈로그를 AEM Mobile의 &quot;랜딩 페이지&quot;로 생각해 보십시오. 여기서 관리자는 템플릿을 기반으로 만들거나 모바일 개발자가 이미 시작한 기존 앱을 업로드하여 새 AEM Mobile 애플리케이션을 시작할 수 있습니다.

앱 카탈로그 랜딩 페이지로 이동하려면 다음 단계를 수행합니다.

1. **내비게이션**&#x200B;을 찾은 다음 **모바일**&#x200B;을 선택합니다.

1. 앱 카탈로그를 열려면 **Apps**&#x200B;를 선택합니다.

![AEM Mobile 앱 카탈로그](assets/chlimage_1-135.png)

## AEM Mobile 앱 대시보드 {#the-aem-mobile-app-dashboard}

카탈로그에서 AEM Mobile 앱을 선택하면 대시보드가 표시됩니다. 여기에서 응용 프로그램을 관리하고, 통계를 보고, 모바일 앱 콘텐츠를 빌드하고 배포 및 관리할 수 있습니다.

AEM Mobile Dashboard의 각 타일로 확장하여 &#39;...&#39;을 클릭하여 세부 사항을 보거나 편집할 수 있습니다. 오른쪽 하단에 있습니다.

![AEM Mobile 애플리케이션 명령 센터](assets/chlimage_1-136.png)

### 앱 관리 타일 {#the-manage-app-tile}

앱 타일 관리에는 애플리케이션 아이콘, 이름, 설명, 지원되는 플랫폼, 업데이트 URL 및 버전 정보를 위한 Call Home이 표시됩니다. 이 타일로 드릴다운하여 PhoneGap 응용 프로그램 구성(config.xml)을 편집 및 유지 관리하고 배포할 수 있도록 응용 프로그램을 다양한 응용 프로그램 스토어에 제출할 수 있습니다.

자세한 내용을 보려면 [여기](/help/mobile/phonegap-app-details-tile.md)를 클릭하십시오.

![chlimage_1-137](assets/chlimage_1-137.png)

### 페이지 컨텐츠 관리 타일 {#the-manage-page-content-tile}

AEM Sites에서와 동일한 방식으로 AEM Mobile에서 컨텐츠를 제작, 업데이트 및 삭제할 수 있습니다. **페이지 컨텐츠 타일 관리**&#x200B;에는 관리되는 컨텐츠 및 마지막으로 수정한 페이지의 수가 표시됩니다. 타일의 각 레코드를 클릭하여 컨텐츠를 드릴다운하여 페이지를 생성, 복사, 이동, 삭제 및 업데이트할 수 있습니다. 콘텐츠가 업데이트되면 **콘텐츠 패키지 관리 타일을 통해 고객에게 콘텐츠 업데이트를 푸시할 수 있습니다.**

![컨텐츠 타일](assets/chlimage_1-138.png)

### 콘텐츠 패키지 관리 타일 {#the-manage-content-packages-tile}

페이지 컨텐츠 관리 타일을 통해 컨텐츠를 추가하거나 수정하면 컨텐츠 릴리스 업데이트를 통해 이러한 변경 사항을 고객에게 전달할 수 있습니다.

콘텐츠 패키지를 사용하면 AEM 앱 제작자는 AEM에서 페이지 컨텐츠를 관리할 수 있고 개발팀은 PhoneGap Shell 애플리케이션(예: 앱 프레임워크 또는 인프라)을 변경한 다음 개발자를 요청하지 않고도 신속하게 고객에게 변경 사항을 전달하여 배포할 수 있습니다.

컨텐츠 패키지는 각 업데이트에 대해 컨텐츠 릴리스 패키지로 간주되는 ZIP 파일을 만듭니다. 이러한 패키지에는 앱을 렌더링하는 동안 생성되는 html 리소스 및 html 페이지가 포함되어 있으며 마지막 업데이트 이후 수정된 파일만 패키지할 수 있는 지능적입니다.

콘텐츠 패키지 타일 관리 타일의 **Type** 열에는 개발자가 관리하는 앱의 프레임워크 또는 인프라 등 애플리케이션 셸 컨텐츠를 나타내는 &#39;App&#39; 또는 컨텐츠 작성자가 관리하는 페이지 컨텐츠를 나타내는 &#39;Content&#39;가 표시됩니다.

콘텐츠는 언어로 표현되거나 앱에서 여러 컨텐츠 릴리스 패키지를 사용하는 앱의 특정 일부로 표현될 수 있습니다. 컨텐츠 번들 방식의 선택은 유연하고 애플리케이션의 컨텐츠 관리 방법에 전적으로 맞게 설계되었습니다.

**수정된** 열은 페이지가 가장 최근에 수정된 시기를 나타냅니다.

**준비 완료** 열은 마지막 컨텐츠 업데이트를 만든 시기를 표시합니다. 새 내용 업데이트를 만들고 변경 사항을 스테이징하려면 타일의 모든 레코드를 열고 새 업데이트를 만듭니다.

**게시된** 열은 마지막 컨텐츠 업데이트가 게시된 시점을 보여주며 고객의 소비를 가능하게 했습니다. 콘텐츠를 게시하려면 먼저 해당 콘텐츠를 단계별로 만든 다음 이 타일로 드릴다운하고 [컨텐츠 릴리스 세부 정보] 콘솔에서 게시하여 업데이트를 게시해야 합니다.

![앱 셸용 콘텐츠 ](assets/chlimage_1-139.png) ![릴리스 TileContentSync 패키지](do-not-localize/chlimage_1-5.png)

이 아이콘은 앱 셸에 대한 콘텐츠 릴리스 패키지를 나타냅니다.

![](do-not-localize/chlimage_1-6.png)

이러한 아이콘은 앱 콘텐츠에 대한 콘텐츠 릴리스 패키지를 나타냅니다.

### PhoneGap Build 타일 {#the-phonegap-build-tile}

**PhoneGap Build 타일**&#x200B;은 [https://build.phonegap.com](https://build.phonegap.com)에 연결하여 원격 버퍼를 작성하고 호스팅합니다. 빌드가 빌드되면 빌드를 다운로드로 사용하거나 QR 코드를 통해 장치에 직접 제공할 수 있습니다.

또는 [PhoneGap CLI](https://docs.phonegap.com/en/3.5.0/guide_cli_index.md.html)를 통해 로컬로 구축할 디바이스 소스를 다운로드할 수 있습니다.

![PhoneGap Build 타일](assets/chlimage_1-140.png)

### 지표 타일 {#the-metrics-tile}

>[!CAUTION]
>
>지표 타일은 클라우드 서비스를 구성한 후에만 표시됩니다.
>
>자세한 내용은 [Adobe Mobile Services Cloud Service 구성](/help/mobile/configure-adobe-mobile-cloud-service.md)을 참조하십시오.

AEM Mobile은 [Adobe Mobile Services SDK](https://www.adobe.com/ca/solutions/digital-marketing/mobile-services/app-sdk.html)(AMS)를 통해 Adobe Analytics과 통합됩니다.

제어 센터 **지표 타일**&#x200B;에 응용 프로그램의 AMS에서 가져온 요약 분석이 표시됩니다. &#39;...&#39;을 클릭하여 분석 대시보드로 드릴다운할 수 있습니다. 오른쪽 하단에 있습니다.

![지표 타일](assets/chlimage_1-141.png)

### 개체 컨텐트 관리 타일 {#the-manage-entity-content-tile}

개체 콘텐츠 관리 타일에서 앱 정의를 추가하고 관리할 수 있습니다. 앱 정의는 앱에 적합한 공간(및 기타 구성)을 식별하는 방법입니다. 이렇게 하면 앱을 다시 컴파일하지 않고도 새 공간을 추가할 수 있습니다. 앱 정의가 업데이트되며 새 공간에 대한 정보가 포함됩니다.

앱 정의를 만들고 관리하려면 [여기](/help/mobile/phonegap-app-definitions.md)를 클릭합니다.

&#39;...&#39;을 클릭하여 엔티티 컨텐트 관리 대시보드로 드릴다운할 수 있습니다. 오른쪽 하단에 있습니다.

![chlimage_1-142](assets/chlimage_1-142.png)

#### 추가 리소스 {#additional-resources}

관리자 및 개발자의 역할 및 책임을 살펴보려면 아래 리소스를 참조하십시오.

* [AEM을 사용하여 Adobe PhoneGap Enterprise를 위한 개발](/help/mobile/developing-in-phonegap.md)
* [AEM에서 Adobe PhoneGap Enterprise용 컨텐츠 관리](/help/mobile/administer-phonegap.md)

