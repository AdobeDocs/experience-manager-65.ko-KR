---
title: Adobe PhoneGap Build Cloud Service 구성
seo-title: Configure your Adobe PhoneGap Build Cloud Service
description: 클라우드 서비스를 구성하고 PhoneGap Build를 사용하여 애플리케이션을 만들려면 이 페이지를 따르십시오.
seo-description: Follow this page for configuring the cloud services and building your application with PhoneGap build.
uuid: 59aa99c3-1425-4cc5-9839-a57a6a545d45
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 3c84f4ec-d89b-4ad4-802e-ee3e2d49d916
exl-id: d91a00d1-12fa-4c84-a426-49413f61c126
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 1%

---

# Adobe PhoneGap Build Cloud Service 구성 {#configure-your-adobe-phonegap-build-cloud-service}

>[!NOTE]
>
>Adobe 단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: React)이 필요한 프로젝트에는 SPA Editor를 사용하는 것이 좋습니다. [자세히 알아보기](/help/sites-developing/spa-overview.md).

다음 **PhoneGap Build 타일** 애플리케이션 대시보드에서 Adobe PhoneGap Build 서비스를 통해 PhoneGap 모바일 애플리케이션을 빌드하고 배포하는 기능을 제공합니다.

내에 정의된 모든 지원되는 플랫폼 **앱 관리** 타일은 원격 빌드를 푸시할 때 PhoneGap Build으로 빌드됩니다. **PhoneGap Build** 타일.

원격 빌드를 푸시할 수 있습니다. [https://build.phonegap.com](https://build.phonegap.com) 또는 소스를 다운로드하여 로컬로 빌드 [PhoneGap CLI](https://docs.phonegap.com/references/phonegap-cli/).

![PhoneGap Build 타일](assets/chlimage_1-60.png)

## Cloud Service 구성 {#configuring-the-cloud-service}

PhoneGap Build을 활용하려면 PhoneGap Build 계정 정보로 AEM PhoneGap Build Cloud Service을 구성해야 합니다.

현재 계정이 없는 경우 다음으로 이동합니다. [https://build.phonegap.com](https://build.phonegap.com) 등록하십시오! Adobe Creative Cloud 멤버십이 있는 경우 최대 25개의 비공개 앱(비오픈 소스 앱)을 지원할 수 있습니다.

PhoneGap Build 계정이 활성화되어 있는지 확인한 후 AEM Cloud Management Console로 이동합니다. 특히 [PhoneGap Build Cloud Service](http://localhost:4502/etc/cloudservices/phonegap-build.html) (http://localhost:4502/etc/cloudservices/phonegap-build.html).

사용 **Cloud Services 관리** 타일을 사용하여 새 클라우드 서비스 구성을 구성합니다.

### Cloud Services 관리 타일 사용 {#using-manage-cloud-services-tile}

을 사용하여 앱 빌드를 시작하기 전에 **PhoneGap Build** 타일, 다음을 사용하여 클라우드 서비스를 구성해야 합니다. **Cloud Services 관리** AEM Mobile 대시보드에서 타일을 지정합니다.

앱에 대한 클라우드 서비스를 구성하려면 아래 단계를 따르십시오.

1. 의 오른쪽 위 모서리를 클릭합니다. **Cloud Services 관리** 타일.

   ![chlimage_1-61](assets/chlimage_1-61.png)

1. 선택 **PhoneGap Build** 옵션에서 **Cloud Service 추가 또는 편집** 화면.

   **다음**&#x200B;을 클릭합니다.

   ![chlimage_1-62](assets/chlimage_1-62.png)

1. 자격 증명을 입력하여 새 클라우드 구성을 만듭니다.

   확인했으면 다음을 클릭합니다. **제출**. 구성된 이 클라우드 구성은 이제 **Cloud Services 관리** 타일.

   ![chlimage_1-63](assets/chlimage_1-63.png)

### PhoneGap Build을 사용하여 애플리케이션 구축 {#building-your-application-with-phonegap-build}

클라우드 서비스를 구성했으면 를 사용하여 애플리케이션을 빌드할 수 있습니다. **PhoneGap Build** 타일. 오른쪽 상단 모서리에서 을(를) 클릭하여 **원격 빌드** 또는 **소스 다운로드** 옵션.

![chlimage_1-64](assets/chlimage_1-64.png)

Adobe PhoneGap Build으로 원격 빌드를 호출하려면 **원격 빌드**.

>[!NOTE]
>
>어떤 이유로든 빌드가 실패하는 경우(아래 빨간색 iOS 아이콘은 플랫폼 실패를 나타냄) 아이콘 위로 마우스를 가져가면 오류 메시지가 표시됩니다. 또는 타일 하단의 트리플 점 &#39;...&#39;을 클릭하여 https://build.phonegap.com으로 직접 이동하고(인증해야 함) 빌드를 직접 보고 관리할 수 있습니다.

### PhoneGap CLI를 사용하여 애플리케이션 구축 {#building-your-application-with-phonegap-cli}

PhoneGap은 응용 프로그램을 로컬로 빌드하는 명령줄 인터페이스를 제공합니다.

PhoneGap 명령줄 인터페이스(CLI)를 사용하여 컴퓨터에서 PhoneGap 응용 프로그램을 컴파일합니다. AEM 콘텐츠를 애플리케이션에 포함하기 위해 AEM은 모바일 애플리케이션의 콘텐츠, 콘텐츠 동기화 구성 및 기타 필수 에셋이 포함된 ZIP 파일을 생성합니다. ZIP 파일을 다운로드하여 빌드에 포함합니다.

PhoneGap의 명령줄 인터페이스를 활용하려면 다음을 포함하도록 로컬 환경을 설정해야 합니다.

1. Platform SDK(iOS, Android, WindowsPhone, ...) 및,
1. PhoneGap CLI

자세한 내용은 [여기](https://docs.phonegap.com/references/phonegap-cli/).

사전 요구 사항을 설치한 후에는 간단한 앱을 만들어 시뮬레이터에서 실행하거나 장치에서 실행할 수 있도록 터미널에서 다음을 시도해 보십시오.

```xml
phonegap create myApp
cd myApp
phonegap run ios (or android, ...)
```

>[!NOTE]
>
>add - 연결된 디바이스에서 실행하지 않으려면 이 줄의 끝에 있는 에뮬레이션을 수행합니다.

위의 기능이 작동하는지 확인한 후에는 **PhoneGap Build** 타일 대상 **소스 다운로드**. 파일을 로컬 시스템에 저장하고 압축 해제합니다. 작업이 완료되면:

* 저장된 파일(폴더)로 이동
* phonegap run ios(또는 android 등) 실행

### 추가 리소스 {#additional-resources}

작성자 및 개발자의 역할과 책임에 대해 알아보려면 아래 리소스를 참조하십시오.

* [AEM을 사용하여 Adobe PhoneGap Enterprise용 개발](/help/mobile/developing-in-phonegap.md)
* [AEM에서 Adobe PhoneGap Enterprise용 작성](/help/mobile/phonegap.md)
