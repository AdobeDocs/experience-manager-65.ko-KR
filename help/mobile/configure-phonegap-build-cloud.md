---
title: Adobe PhoneGap Build Cloud Service 구성
description: 이 페이지를 따라 클라우드 서비스를 구성하고 PhoneGap Build을 사용하여 애플리케이션을 빌드합니다.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
exl-id: d91a00d1-12fa-4c84-a426-49413f61c126
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 1%

---

# Adobe PhoneGap Build Cloud Service 구성 {#configure-your-adobe-phonegap-build-cloud-service}

{{ue-over-mobile}}

응용 프로그램 대시보드의 **PhoneGap Build 타일**&#x200B;을 사용하여 Adobe PhoneGap Build 서비스를 통해 PhoneGap 모바일 응용 프로그램을 빌드하고 배포할 수 있습니다.

**앱 관리** 타일 내에 정의된 모든 지원되는 플랫폼은 **PhoneGap Build** 타일로 원격 빌드를 푸시할 때 PhoneGap Build으로 빌드됩니다.

`https://docs.phonegap.com/references/phonegap-cli/`에서 PhoneGap CLI를 사용하여 원격 빌드를 `https://build.phonegap.com`에 푸시하거나 로컬로 빌드할 소스를 다운로드할 수 있습니다.

![PhoneGap Build 타일](assets/chlimage_1-60.png)

## Cloud Service 구성 {#configuring-the-cloud-service}

PhoneGap Build을 활용하려면 PhoneGap Build Cloud Service 정보로 AEM PhoneGap Build 계정을 구성해야 합니다.

현재 계정이 없는 경우 `https://build.phonegap.com`(으)로 이동하여 등록하십시오! Adobe Creative Cloud 멤버십이 있는 경우 최대 25개의 비공개 앱(비오픈 소스 앱)을 지원할 수 있습니다.

PhoneGap Build 계정이 활성 상태인지 확인한 후 AEM Cloud Management Console, 특히 [PhoneGap Build Cloud Service](http://localhost:4502/etc/cloudservices/phonegap-build.html)(http://localhost:4502/etc/cloudservices/phonegap-build.html)로 이동합니다.

**Cloud Service 관리** 타일을 사용하여 새 클라우드 서비스 구성을 구성하십시오.

### Cloud Service 관리 타일 사용 {#using-manage-cloud-services-tile}

**PhoneGap Build** 타일을 사용하여 앱 빌드를 시작하기 전에 AEM Mobile 대시보드의 **Cloud Service 관리** 타일을 사용하여 클라우드 서비스를 구성해야 합니다.

앱에 대한 클라우드 서비스를 구성하려면 아래 단계를 따르십시오.

1. **Cloud Service 관리** 타일의 오른쪽 상단 모서리를 클릭합니다.

   ![chlimage_1-61](assets/chlimage_1-61.png)

1. **PhoneGap Build 추가 또는 편집** 화면에서 **Cloud Service** 옵션을 선택하십시오.

   **다음**&#x200B;을 클릭합니다.

   ![chlimage_1-62](assets/chlimage_1-62.png)

1. 클라우드 구성을 만들 수 있도록 자격 증명을 입력합니다.

   확인되면 **제출**&#x200B;을 클릭합니다. 구성된 이 클라우드 구성이 이제 **Cloud Service 관리** 타일에 표시됩니다.

   ![chlimage_1-63](assets/chlimage_1-63.png)

### PhoneGap Build을 사용하여 애플리케이션 구축 {#building-your-application-with-phonegap-build}

클라우드 서비스를 구성했으면 **PhoneGap Build** 타일로 응용 프로그램을 빌드할 수 있습니다. 오른쪽 상단을 클릭하면 **원격 빌드** 또는 **Source 다운로드** 옵션 중에서 선택할 수 있습니다.

![chlimage_1-64](assets/chlimage_1-64.png)

Adobe PhoneGap Build으로 원격 빌드를 호출하려면 **원격 빌드**&#x200B;를 클릭합니다.

>[!NOTE]
>
>어떤 이유로든 빌드가 실패하는 경우(아래 빨간색 iOS 아이콘은 플랫폼 실패를 나타냄) 아이콘 위로 마우스를 가져가면 오류 메시지가 표시됩니다. 또는 타일 하단의 트리플 점 &#39;...&#39;을 클릭하여 `https://build.phonegap.com`(인증해야 함)으로 바로 이동하고 빌드를 직접 보고 관리할 수 있습니다.

### PhoneGap CLI를 사용하여 애플리케이션 구축 {#building-your-application-with-phonegap-cli}

PhoneGap에서는 응용 프로그램을 로컬로 빌드할 수 있는 명령줄 인터페이스를 제공합니다.

PhoneGap 명령줄 인터페이스(CLI)를 사용하여 컴퓨터에서 PhoneGap 응용 프로그램을 컴파일합니다. AEM 콘텐츠를 애플리케이션에 포함하기 위해 AEM은 모바일 애플리케이션의 콘텐츠, 콘텐츠 동기화 구성 및 기타 필수 에셋이 포함된 ZIP 파일을 생성합니다. ZIP 파일을 다운로드하여 빌드에 포함합니다.

PhoneGap의 CLI를 활용하려면 다음을 포함하도록 로컬 환경을 설정해야 합니다.

1. Platform SDK(iOS, Android™, WindowsPhone, ...) 및,
1. PhoneGap CLI

자세한 내용은 `https://docs.phonegap.com/references/phonegap-cli/`에서 확인할 수 있습니다.

사전 요구 사항을 설치한 후에는 간단한 앱을 만들어 시뮬레이터에서 실행하거나 장치에서 실행할 수 있도록 터미널에서 다음을 시도해 보십시오.

```xml
phonegap create myApp
cd myApp
phonegap run ios (or android, ...)
```

>[!NOTE]
>
>추가 —연결된 장치에서 실행하지 않으려면 이 줄의 끝에 있는 에뮬레이션을 사용합니다.

위의 기능이 작동하는지 확인한 후에는 **PhoneGap Build** 타일을 사용하여 **Source을 다운로드**&#x200B;하십시오. 파일을 로컬 시스템에 저장하고 압축 해제합니다. 작업이 완료되면:

* 저장된 파일(폴더)로 이동
* phonegap run ios(또는 android 등) 실행

### 추가 리소스 {#additional-resources}

작성자 및 개발자의 역할과 책임에 대해 알아보려면 아래 리소스를 참조하십시오.

* [AEM을 사용하여 Adobe PhoneGap Enterprise용 개발](/help/mobile/developing-in-phonegap.md)
* [AEM에서 Adobe PhoneGap Enterprise용 작성](/help/mobile/phonegap.md)
