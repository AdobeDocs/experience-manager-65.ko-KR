---
title: 앱 타일 관리
description: 애플리케이션에 대한 세부 정보를 편집할 수 있도록 해 주는 앱 대시보드의 "앱 관리" 타일에 대해 자세히 알아보십시오.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
exl-id: 8bcf70ef-94d2-4958-90b5-bc375b360916
source-git-commit: bf99ad3710638ec823d3b17967e1c750d0405c77
workflow-type: tm+mt
source-wordcount: '1218'
ht-degree: 2%

---

# 앱 타일 관리{#manage-app-tile}

>[!NOTE]
>
>Adobe 단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: React)이 필요한 프로젝트에는 SPA Editor를 사용하는 것이 좋습니다. [자세히 알아보기](/help/sites-developing/spa-overview.md).

다음 **`Manage App`** 앱 대시보드의 타일을 사용하여 애플리케이션에 대한 세부 정보를 편집할 수 있습니다. 세부 정보 페이지를 열려면 다음을 클릭하십시오. **`Manage App`** 타일의 세부 정보 링크입니다. 다음 범위 내에서 **`Manage App`** 페이지에서 PhoneGap Application Configuration(config.xml) 설정을 편집하고 응용 프로그램을 여러 응용 프로그램 저장소에 제출하도록 준비할 수 있습니다.

![chlimage_1-116](assets/chlimage_1-116.png)

## 이해 `Manage App` 타일 {#understanding-the-manage-app-tile}

에서 각 타일로 드릴다운할 수 있습니다. **`Manage App`** 오른쪽 아래 모서리에 있는 &#39;...&#39;를 클릭하여 세부 정보를 보거나 편집할 수 있는 타일을 표시합니다.

### 기본 탭 {#the-basic-tab}

다음을 편집할 수 있습니다. **이름**, **작성자**, **간단한 설명**&#x200B;및 **설명** 앱에 대해 이 탭에서 확인할 수 있습니다.

![chlimage_1-117](assets/chlimage_1-117.png)

### 고급 탭 {#the-advanced-tab}

각 모바일 애플리케이션 플랫폼은 수집된 데이터에 대해 설명하며 각 애플리케이션 스토어를 구체적으로 타겟팅합니다.

표시되는 플랫폼은 PhoneGap config.xml 콘텐츠에 의해 결정됩니다.

```xml
<widget>
<gap:platform name="ios"/>
<gap:platform name="android"/>
</widget>
```

Apple App Store 또는 Google Play 스토어와 같은 각 공급업체 애플리케이션 스토어는 고객에게 애플리케이션 세부 정보를 표시하기 위해 모바일 애플리케이션의 스크린샷을 하나 이상 필요로 합니다. 이러한 스크린샷은 차원 및 콘텐츠에 대한 엄격한 요구 사항을 가질 수 있습니다(기본적으로 애플리케이션을 실제로 표시해야 함). AEM Apps는 지원되는 플랫폼에 대해 이러한 스크린샷을 선택 및 관리하고 각 공급업체의 애플리케이션 스토어에서 요구하는 포트 차원을 볼 수 있도록 지원합니다.

>[!NOTE]
>
>AEM 확인 앱을 사용하면 스크린샷을 AEM의 앱 세부 사항으로 직접 보낼 수 있습니다.
>
>다음을 참조하십시오 [AEM 확인을 위한 모바일 빠른 시작](/help/mobile/phonegap-mobile-quickstart.md) 을 참조하십시오.

![chlimage_1-118](assets/chlimage_1-118.png)

### 메타데이터 {#metadata}

>[!NOTE]
>
>를 잘 알고 있으면 **`Manage App`** 타일, 참조 [앱 메타데이터 편집](/help/mobile/phonegap-editmetadata.md) 메타데이터를 보고 편집합니다.

#### 공통 메타데이터 {#common-metadata}

모든 응용 프로그램에는 응용 프로그램의 다양한 측면을 구성하는 데 도움이 되는 관련 메타데이터가 있어야 합니다. 앱 관리 페이지는 메타데이터 수집과 관련된 두 개의 서로 다른 영역으로 구분됩니다. 플랫폼별 메타데이터 및 일반 메타데이터.

모든 플랫폼에 대한 공통 구성과 메타데이터가 있습니다.

이 섹션에서는 콘텐츠 업데이트 서버 URL, 모바일 애플리케이션의 랜딩 페이지, 컴파일을 위한 PhoneGap 버전, 애플리케이션 버전, 이름, 설명 등을 정의합니다.

**앱 버전** 는 애플리케이션의 작업 버전입니다. 일반적인 우수 사례는 3진수 표기법을 사용하고 첫 번째 릴리스 전에 1.0.0 미만에서 시작하는 것입니다.

**PhoneGap 버전** 는 PhoneGap을 사용하여 응용 프로그램을 컴파일할 버전입니다. 가장 좋은 방법은 최신 기능과 버그 수정 사항을 얻을 수 있도록 현재 버전을 최신 상태로 유지하는 것입니다.

**컨텐츠 업데이트 서버 URL** 는 애플리케이션이 ContentSync 업데이트를 호출하는 데 사용하는 URL입니다. Dispatcher URL로 설정하거나 Dispatcher를 사용하지 않는 경우 애플리케이션에 ContentSync 업데이트를 제공하는 데 사용되는 게시 인스턴스 중 하나로 설정해야 합니다.

![chlimage_1-119](assets/chlimage_1-119.png)

>[!NOTE]
>
>필드를 채우는 데이터가 없으면 이 섹션이 비어 있을 수 있습니다.
>
>세부 사항 보기의 맨 위에는 응용 프로그램 버전, PhoneGap 버전 및 업데이트 URL이 표시되며, 이러한 각 값은 [일반 메타데이터] 섹션 내에서 설정할 수 있습니다. 단, 애플리케이션 ID는 편집할 수 없습니다.

#### 플랫폼 메타데이터 {#platform-metadata}

PhoneGap config.xml에 정의된 모든 플랫폼에는 사용자 지정 플랫폼 속성을 포함할 수 있습니다. AEM 개발자는 이러한 속성을 캡처하려면 콘텐츠 구조를 기여해야 합니다. 플랫폼별 속성에 대한 예는 iOS에 대해 제공됩니다.

이제 구성된 모든 플랫폼의 메타데이터가 의 고급 탭에 동시에 표시됩니다. `Manage App` 타일.

>[!NOTE]
>
>CLI 또는 Remote PhoneGap 빌드 중에는 PhoneGap에서 플랫폼 메타데이터 섹션을 사용하지 않습니다. 대신 AEM은 타겟팅된 공급업체의 애플리케이션 스토어에 제출할 때 나중에 사용할 수 있도록 플랫폼에 대한 메타데이터를 캡처하려고 합니다.

AEM에서 인식하지 못하는 플랫폼의 경우, AEM 개발자가 UI를 확장하여 나중에 애플리케이션 제출 프로세스 중에 내보내고 사용할 수 있는 이 메타데이터를 캡처하는 것이 여전히 가능합니다.

#### iOS 메타데이터 {#ios-metadata}

Apple AppStore에서 배포를 위해 애플리케이션을 제출하려면 추가 메타데이터가 필요합니다. iOS 메타데이터 섹션은 Apple의 iTMSTransporter 도구에서 관련 Apple 개발자 계정에 메타데이터를 게시하는 데 사용할 수 있는 필수 정보를 수집하려고 합니다.

Apple 관련 메타데이터를 가져오려면에 애플리케이션을 만듭니다. [https://itunesconnect.apple.com](https://itunesconnect.apple.com/). 애플리케이션을 만들 때 Apple은 메타데이터를 확인하고 itunesconnect.apple.com에 업로드하기 위해 Apple iTMSTransporter 도구를 사용하려는 경우 iOS 메타데이터 섹션에 필요한 메타데이터를 생성합니다. 수집할 메타데이터를 가져오려면 iOS 관련 메타데이터를 작성할 필요가 없습니다. iOS과 일반 메타데이터를 병합하는 메타데이터를 내보내고 모든 스크린샷을 언제든지 다운로드할 수 있는 zip 파일로 수집할 수 있습니다.

다운로드한 zip 파일에는 metadata.xml을 검사할 수 있는 itmsp 파일이 포함되어 있습니다. itmsp 파일에는 연결된 모든 스크린샷과 함께 내보낸 메타데이터(metadata.xml 파일 내)가 포함되어 있습니다.

내보내기 기능은 공급업체별 애플리케이션 스토어에 입력하기 위해 애플리케이션 게시자에게 전달할 수 있는 스크린샷과 메타데이터를 편리하게 수집하는 방법을 제공하는 데 사용됩니다.

![chlimage_1-120](assets/chlimage_1-120.png)

#### Android™ 메타데이터 {#android-metadata}

Android™ 플랫폼을 선택할 때 이 시점에서 설정할 수 있는 사용자 지정 메타데이터가 없습니다. 다운로드 버튼을 클릭하면 모든 메타데이터 및 관련 스크린샷이 포함된 속성 파일과 함께 zip 파일이 생성됩니다.

내보내기 기능은 공급업체별 애플리케이션 스토어에 입력하기 위해 애플리케이션 게시자에게 전달할 수 있는 스크린샷과 메타데이터를 편리하게 수집하는 방법을 제공하는 데 사용됩니다.

![chlimage_1-121](assets/chlimage_1-121.png)

### 컨텐츠 업데이트 서버 URL {#content-update-server-url}

AEM Apps의 주요 기능 중 하나는 모바일 애플리케이션이 ContentSync를 통해 새로운 콘텐츠를 요청하도록 하는 기능입니다. 여기서 콘텐츠는 html 리소스, 페이지, 비디오, 이미지, 텍스트 등일 수 있습니다. 콘텐츠 작성자가 콘텐츠를 업데이트한 다음 해당 콘텐츠를 게시하면 서버는 모바일 애플리케이션이 콘텐츠 업데이트를 다운로드할 수 있도록 합니다.

Content Update Server URL 속성은 게시 인스턴스를 가리켜야 하는 URL입니다(직접 또는 Dispatcher 또는 CDN을 통해). URL 형식은 다음과 같습니다.

`https://[hostname]:[port]`

>[!NOTE]
>
>작성자 서버 인스턴스가 여러 게시 서버 인스턴스(AEM의 일반 아키텍처)에 복제하는 경우 각 게시 서버에는 동일한 업데이트 콘텐츠가 있습니다. 그 이유는 업데이트가 작성자에 빌드되고 모든 게시 인스턴스에 복제되기 때문입니다. 기본적으로 로드 밸런싱과 페일오버가 완벽하게 지원됩니다.

### 플러그인 탭 {#the-plugins-tab}

다음 **플러그인** 탭에서는 앱과 연결된 플러그인에 대해 설명합니다. 이 정보는 빌드 중에 적절한 플러그인을 검색하는 데 사용됩니다.

![chlimage_1-122](assets/chlimage_1-122.png)

### 스크린샷 탭 {#the-screenshots-tab}

다음 **스크린샷** 탭에는 다른 플랫폼에서 지원되는 스크린샷 해상도가 표시됩니다.

![chlimage_1-123](assets/chlimage_1-123.png)

>[!NOTE]
>
>스크린샷을 추가하거나 제거하려면 다음을 참조하십시오. [앱 메타데이터 편집](/help/mobile/phonegap-editmetadata.md).

### 인증 탭 {#the-authentication-tab}

다음 **인증** 탭에서는 응용 프로그램과 연결할 OAuth 클라이언트를 선택할 수 있고 개발자가 Adobe Experience Manager의 OAuth 인증을 사용할 수 있습니다.

![chlimage_1-124](assets/chlimage_1-124.png)

### 다음 단계 {#the-next-steps}

응용 프로그램 대시보드의 앱 타일 관리에 대해 알아보았으면 다른 작성 역할에 대한 다음 리소스를 참조하십시오.

* [앱 메타데이터 편집](/help/mobile/phonegap-editmetadata.md)
* [앱 정의](/help/mobile/phonegap-app-definitions.md)
* [앱 만들기 마법사를 사용하여 새 앱 만들기](/help/mobile/phonegap-create-new-app.md)
* [기존 하이브리드 앱 가져오기](/help/mobile/phonegap-adding-content-to-imported-app.md)
* [Content Services](/help/mobile/develop-content-as-a-service.md)

### 기타 리소스 {#additional-resources}

관리자 및 개발자의 역할과 책임에 대해 알아보려면 아래 리소스를 참조하십시오.

* [AEM을 사용하여 Adobe PhoneGap Enterprise용 개발](/help/mobile/developing-in-phonegap.md)
* [AEM을 사용하여 Adobe PhoneGap Enterprise용 컨텐츠 관리](/help/mobile/administer-phonegap.md)
