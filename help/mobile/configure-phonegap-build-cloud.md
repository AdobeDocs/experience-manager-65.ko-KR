---
title: Adobe PhoneGap Build Cloud 서비스 구성
seo-title: Adobe PhoneGap Build Cloud 서비스 구성
description: 클라우드 서비스를 구성하고 PhoneGap 빌드로 애플리케이션을 빌드하려면 이 페이지를 따르십시오.
seo-description: 클라우드 서비스를 구성하고 PhoneGap 빌드로 애플리케이션을 빌드하려면 이 페이지를 따르십시오.
uuid: 59aa99c3-1425-4cc5-9839-a57a6a545d45
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 3c84f4ec-d89b-4ad4-802e-ee3e2d49d916
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Adobe PhoneGap Build Cloud 서비스 구성 {#configure-your-adobe-phonegap-build-cloud-service}

>[!NOTE]
>
>단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: 응답)이 필요한 프로젝트에 SPA 편집기를 사용하는 것이 좋습니다. [추가 정보](/help/sites-developing/spa-overview.md).

애플리케이션 **대시보드의 PhoneGap** 빌드 타일은 Adobe PhoneGap Build Service를 통해 PhoneGap 모바일 애플리케이션을 빌드하고 배포할 수 있는 기능을 제공합니다.

PhoneGap Build **Tile을** 사용하여 원격 빌드를 푸시할 때 앱 관리 타일에 정의된 **모든 지원** 플랫폼이 PhoneGap Build로빌드됩니다.

원격 빌드를 https://build.phonegap.com으로 푸시하거나 [소스를](https://build.phonegap.com) 다운로드하여 PhoneGap CLI를 통해 로컬에 구축할 [수 있습니다](https://docs.phonegap.com/references/phonegap-cli/).

![PhoneGap 빌드 타일](assets/chlimage_1-60.png)

## 클라우드 서비스 구성 {#configuring-the-cloud-service}

PhoneGap Build를 활용하려면 PhoneGap Build 계정 정보와 함께 AEM PhoneGap Build Cloud 서비스를 구성해야 합니다.

현재 계정이 없는 경우 https://build.phonegap.com으로 이동하여 [등록하십시오](https://build.phonegap.com) ! Adobe Creative Cloud 멤버십이 있는 경우 최대 25개의 비공개 앱(오픈 소스 앱 아님)을 지원할 수 있습니다.

PhoneGap Build 계정이 활성화되었는지 확인했으면 AEM Cloud 관리 콘솔, 특히 PhoneGap Build [Cloud 서비스](http://localhost:4502/etc/cloudservices/phonegap-build.html) (http://localhost:4502/etc/cloudservices/phonegap-build.html)로 이동합니다.

클라우드 서비스 **관리** 타일을 사용하여 새 클라우드 서비스 구성을 구성합니다.

### 클라우드 서비스 관리 타일 사용 {#using-manage-cloud-services-tile}

PhoneGap Build **타일을 사용하여 앱을** 빌드하기 전에 AEM Mobile 대시보드의 클라우드 서비스 **관리 타일을 사용하여** 클라우드 서비스를 구성해야 합니다.

앱에 대한 클라우드 서비스를 구성하려면 아래 단계를 따르십시오.

1. 클라우드 서비스 관리 타일의 오른쪽 상단 **모서리에서 을** 클릭합니다.

   ![chlimage_1-61](assets/chlimage_1-61.png)

1. 클라우드 서비스 **추가** 또는 편집 **화면에서 PhoneGap Build 옵션을** 선택합니다.

   **다음**&#x200B;을 클릭합니다.

   ![chlimage_1-62](assets/chlimage_1-62.png)

1. 자격 증명을 입력하여 새 클라우드 구성을 만듭니다.

   확인되면 제출을 **클릭합니다**. 이제 이 구성된 클라우드 구성이 클라우드 서비스 관리 **타일에 표시됩니다** .

   ![chlimage_1-63](assets/chlimage_1-63.png)

### PhoneGap Build를 사용하여 애플리케이션 제작 {#building-your-application-with-phonegap-build}

클라우드 서비스를 구성한 후에는 PhoneGap Build **타일로 애플리케이션을 구축할 수** 있습니다. 오른쪽 위 모서리에서 을 클릭하여 원격 빌드 또는 **다운로드 소스** 옵션 중에서 **선택합니다** .

![chlimage_1-64](assets/chlimage_1-64.png)

Adobe PhoneGap Build를 사용하여 원격 빌드를 호출하려면 원격 **빌드를 클릭합니다**.

>[!NOTE]
>
>어떤 이유로든 빌드가 실패하는 경우(아래 빨간색 iOS 아이콘은 플랫폼이 실패했음을 나타냅니다) 아이콘 위로 마우스를 가져가면 오류 메시지가 표시됩니다. 또는 삼중 점 &#39;...&#39;을 클릭할 수도 있습니다. 타일 하단에서 바로 https://build.phonegap.com(인증해야 함)으로 이동하여 빌드를 직접 보고 관리할 수 있습니다.

### PhoneGap CLI를 사용하여 애플리케이션 구축 {#building-your-application-with-phonegap-cli}

PhoneGap은 응용 프로그램을 로컬로 빌드하는 명령줄 인터페이스를 제공합니다.

PhoneGap 명령줄 인터페이스(CLI)를 사용하여 컴퓨터에서 PhoneGap 애플리케이션을 컴파일합니다. AEM 콘텐츠를 애플리케이션에 포함시키기 위해 AEM은 모바일 응용 프로그램의 콘텐츠, 콘텐츠 동기화 구성 및 기타 필요한 에셋이 포함된 ZIP 파일을 만듭니다. ZIP 파일을 다운로드하여 빌드에 포함합니다.

PhoneGap의 명령줄 인터페이스를 활용하려면 다음을 포함하도록 로컬 환경을 설정해야 합니다.

1. 플랫폼 SDK(iOS, Android, WindowsPhone, ...) 및,
1. PhoneGap CLI

자세한 내용은 [여기에서](https://docs.phonegap.com/references/phonegap-cli/)확인하시기 바랍니다.

사전 이수 과정을 설치한 후에는 간단한 앱을 만들어 시뮬레이터 또는 디바이스에서 더 나은 버전으로 설정하여 간단한 테스트를 실시하십시오.

```xml
phonegap create myApp
cd myApp
phonegap run ios (or android, ...)
```

>[!NOTE]
>
>add —emulate at the end of this line if you don&#39;t want to run it on your connected device.

위의 기능이 작동하는지 확인했으면 PhoneGap **빌드 타일을** 사용하여 소스를 **다운로드하십시오**. 로컬 시스템에 파일을 저장하고 압축 해제합니다. 완료되면 다음을 수행합니다.

* 저장된 파일(폴더)로 이동합니다.
* &#39;phonegap run ios&#39;(또는 android 등) 실행

### 추가 리소스 {#additional-resources}

작성자 및 개발자의 역할과 책임에 대한 자세한 내용은 아래 리소스를 참조하십시오.

* [AEM을 사용한 Adobe PhoneGap Enterprise 개발](/help/mobile/developing-in-phonegap.md)
* [AEM 파섹](/help/mobile/phonegap.md)
