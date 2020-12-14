---
title: Adobe PhoneGap Build Cloud Service 구성
seo-title: Adobe PhoneGap Build Cloud Service 구성
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
workflow-type: tm+mt
source-wordcount: '698'
ht-degree: 1%

---


# Adobe PhoneGap Build Cloud Service {#configure-your-adobe-phonegap-build-cloud-service} 구성

>[!NOTE]
>
>단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: 응답)이 필요한 프로젝트에는 SPA 편집기를 사용하는 것이 좋습니다. [추가 정보](/help/sites-developing/spa-overview.md).

응용 프로그램 대시보드의 **PhoneGap Build 타일**&#x200B;은 Adobe PhoneGap Build 서비스를 통해 PhoneGap 모바일 응용 프로그램을 빌드하고 배포할 수 있는 기능을 제공합니다.

**앱 관리** 타일 내에 정의된 모든 지원 플랫폼은 **PhoneGap Build** 타일로 원격 빌드를 푸시할 때 PhoneGap Build으로 빌드됩니다.

원격 빌드를 [https://build.phonegap.com](https://build.phonegap.com)에 푸시하거나 소스를 다운로드하여 [PhoneGap CLI](https://docs.phonegap.com/references/phonegap-cli/)로 로컬로 빌드할 수 있습니다.

![PhoneGap Build 타일](assets/chlimage_1-60.png)

## Cloud Service {#configuring-the-cloud-service} 구성

PhoneGap Build을 활용하려면 PhoneGap Build 계정 정보로 AEM PhoneGap Build을 구성해야 합니다.

현재 계정이 없는 경우 [https://build.phonegap.com](https://build.phonegap.com)로 이동하여 등록하십시오! Adobe Creative Cloud 멤버십이 있는 경우 최대 25개의 비공개 앱(오픈 소스가 아닌 앱)을 지원할 수 있습니다.

PhoneGap Build 계정이 활성화되었는지 확인했으면 AEM Cloud 관리 콘솔(특히 [PhoneGap Build](http://localhost:4502/etc/cloudservices/phonegap-build.html)(http://localhost:4502/etc/cloudservices/phonegap-build.html)으로 이동합니다.

새 클라우드 서비스 구성을 구성하려면 **Cloud Services 관리** 타일을 사용합니다.

### Cloud Services 관리 타일 사용 {#using-manage-cloud-services-tile}

**PhoneGap Build** 타일을 사용하여 앱 빌드를 시작하기 전에 AEM Mobile 대시보드에서 **Cloud Services 관리** 타일을 사용하여 클라우드 서비스를 구성해야 합니다.

앱에 대한 클라우드 서비스를 구성하려면 아래 단계를 따르십시오.

1. **Cloud Services 관리** 타일의 오른쪽 위 모서리를 클릭합니다.

   ![chlimage_1-61](assets/chlimage_1-61.png)

1. **Cloud Service 추가 또는 편집** 화면에서 **PhoneGap Build** 옵션을 선택합니다.

   **다음**&#x200B;을 클릭합니다.

   ![chlimage_1-62](assets/chlimage_1-62.png)

1. 자격 증명을 입력하여 새 클라우드 구성을 만듭니다.

   확인되면 **제출**&#x200B;을 클릭합니다. 이 구성된 클라우드 구성이 이제 **Cloud Services 관리** 타일에 표시됩니다.

   ![chlimage_1-63](assets/chlimage_1-63.png)

### PhoneGap Build {#building-your-application-with-phonegap-build}을(를) 사용하여 응용 프로그램 만들기

클라우드 서비스를 구성한 후에는 **PhoneGap Build** 타일로 애플리케이션을 구축할 수 있습니다. 오른쪽 위 모서리를 클릭하여 **원격 빌드** 또는 **소스 다운로드** 옵션 중에서 선택합니다.

![chlimage_1-64](assets/chlimage_1-64.png)

Adobe PhoneGap Build에서 원격 빌드를 호출하려면 **원격 빌드**&#x200B;를 클릭합니다.

>[!NOTE]
>
>어떤 이유로든 빌드가 실패하는 경우(아래 빨간색 iOS 아이콘은 플랫폼이 실패했음을 나타남) 아이콘 위로 마우스를 가져가 오류 메시지를 가져올 수 있습니다. 또는 트리플점 &#39;...&#39;을 클릭할 수도 있습니다. 타일 하단에서 바로 https://build.phonegap.com(인증해야 함)으로 이동하여 빌드를 직접 보고 관리할 수 있습니다.

### PhoneGap CLI {#building-your-application-with-phonegap-cli}로 애플리케이션 구축

PhoneGap은 응용 프로그램을 로컬로 빌드하는 명령줄 인터페이스를 제공합니다.

PhoneGap 명령줄 인터페이스(CLI)를 사용하여 컴퓨터에 PhoneGap 애플리케이션을 컴파일합니다. AEM 컨텐츠를 애플리케이션에 포함시키기 위해 AEM은 모바일 애플리케이션의 컨텐츠, 컨텐츠 동기화 구성 및 기타 필수 에셋이 포함된 ZIP 파일을 만듭니다. ZIP 파일을 다운로드하여 빌드에 포함합니다.

PhoneGap의 명령줄 인터페이스를 활용하려면 다음을 포함하도록 로컬 환경을 설정해야 합니다.

1. 플랫폼 SDK(iOS, Android, WindowsPhone, ...) 및,
1. PhoneGap CLI

[여기에서 ](https://docs.phonegap.com/references/phonegap-cli/)을 더 읽을 수 있습니다.

사전 이수 과정을 설치한 후에는 간단한 앱을 만들어 시뮬레이터 또는 장치에서 더 나은 방식으로 실행시키는 간단한 테스트를 터미널 시험버전에서 제공합니다.

```xml
phonegap create myApp
cd myApp
phonegap run ios (or android, ...)
```

>[!NOTE]
>
>추가 —연결된 디바이스에서 실행하지 않으려면 이 줄의 끝에서 에뮬레이션합니다.

위의 작업이 작동하는지 확인했으면 **PhoneGap Build** 타일을 **다운로드 소스**&#x200B;에 사용하십시오. 로컬 시스템에 파일을 저장하고 압축 해제합니다. 완료되면 다음을 수행합니다.

* 저장된 파일(폴더)로 이동합니다.
* &#39;phonegap run ios&#39;(또는 android 등)을 실행합니다.

### 추가 리소스 {#additional-resources}

작성자 및 개발자의 역할 및 책임을 알아보려면 아래 리소스를 참조하십시오.

* [AEM을 사용하여 Adobe PhoneGap Enterprise를 위한 개발](/help/mobile/developing-in-phonegap.md)
* [AEM에서 Adobe PhoneGap Enterprise를 위한 저작](/help/mobile/phonegap.md)
