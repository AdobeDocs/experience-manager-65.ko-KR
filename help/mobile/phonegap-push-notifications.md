---
title: 알림 푸시
description: 이 페이지를 따라 Adobe Experience Manager Mobile 앱에서 푸시 알림을 사용하는 방법에 대해 알아보십시오.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: 375f2f40-1b98-4e21-adee-cbea274e6a2a
source-git-commit: 9d497413d0ca72f22712581cf7eda1413eb8d643
workflow-type: tm+mt
source-wordcount: '3156'
ht-degree: 1%

---

# 알림 푸시{#push-notifications}

>[!NOTE]
>
>Adobe 단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: React)이 필요한 프로젝트에는 SPA Editor를 사용하는 것이 좋습니다. [자세히 알아보기](/help/sites-developing/spa-overview.md).

중요한 알림을 통해 Adobe Experience Manager(AEM) 모바일 앱 사용자에게 즉시 알릴 수 있는 것은 모바일 앱과 해당 마케팅 캠페인의 가치에 매우 중요합니다. 여기에서는 앱이 푸시 알림을 수신할 수 있도록 하기 위해 수행해야 하는 단계에 대해 설명합니다. 또한 AEM Mobile에서 휴대폰에 설치된 앱으로 푸시를 구성하고 전송하는 방법에 대해 알아봅니다. 또한 이 섹션에서는 [딥링크](#deeplinking) 푸시 알림에 대한 기능입니다.

>[!NOTE]
>
>*푸시 알림은 전달이 보장되지 않습니다. 알림과 더 비슷합니다. 모든 사람이 이를 받을 수 있지만 보장된 전달 메커니즘이 아니라는 것을 확인하기 위해 최선의 노력을 기울입니다. 또한 푸시를 전달하는 시간은 1초 미만에서 최대 30분까지 다양할 수 있습니다.*

AEM에서 푸시 알림을 사용하려면 몇 가지 다른 기술이 필요합니다. 먼저 푸시 알림 서비스 공급자를 사용하여 알림 및 장치를 관리해야 합니다(AEM에서는 아직 이 작업을 수행하지 않음). 두 공급자는 AEM으로 즉시 구성됩니다. [Amazon Simple Notification Service](https://aws.amazon.com/sns/) (또는 SNS) 및 [Pushwoosh](https://www.pushwoosh.com/). 둘째, 지정된 모바일 OS에 대한 푸시 기술은 적절한 서비스(Apple 장치의 경우 iOS 푸시 알림 서비스(또는 APNS), Android™ 장치의 경우 Google 클라우드 메시징(또는 GCM))을 거쳐야 합니다. AEM이 이러한 플랫폼별 서비스와 직접 통신하지는 않지만, 푸시를 실행하려면 AEM에서 이러한 서비스에 대한 알림과 함께 일부 관련 구성 정보를 제공해야 합니다.

설치 및 구성(아래에 설명)되면 다음과 같이 작동합니다.

1. 푸시 알림이 AEM에서 만들어지고 서비스 공급자(Amazon SNS 또는 Pushwoosh)에게 전송됩니다.
1. 서비스 제공자는 이를 수신하여 핵심 제공자(APNS 또는 GCM)에게 전송한다.
1. 코어 공급자는 해당 푸시에 대해 등록된 모든 장치에 알림을 푸시합니다. 각 장치의 경우 장치에서 사용할 수 있는 셀룰러 데이터 네트워크 또는 WiFi를 사용합니다.
1. 이 알림은 등록된 앱이 실행되고 있지 않을 경우 디바이스에 표시됩니다. 알림을 탭한 사용자는 앱을 시작하고 앱 내에 알림을 표시합니다. 애플리케이션이 이미 실행 중인 경우 인앱 알림만 표시됩니다.

이 AEM 릴리스는 iOS 및 Android™ 모바일 장치를 지원합니다.

## 개요 및 절차 {#overview-and-procedure}

AEM Mobile 앱에서 푸시 알림을 사용하려면 다음과 같은 높은 수준의 단계를 수행해야 합니다.

일반적으로 Experience Manager 개발자는 다음을 수행합니다.

1. Apple 및 Google 메시징 서비스에 등록
1. 푸시 메시지 서비스에 등록 및 구성
1. 앱에 푸시 지원 추가
1. 테스트를 위한 전화 준비

Experience Manager 관리자가 다음을 수행하는 동안:

1. AEM 앱에서 푸시 구성
1. 앱 빌드 및 배포
1. 푸시 알림 보내기
1. 딥링크 구성 *(선택 사항)*

### 1단계: Apple 및 Google 메시징 서비스에 등록 {#step-register-with-apple-and-google-messaging-services}

#### Apple 푸시 알림 서비스(APNS) 사용 {#using-the-apple-push-notification-service-apns}

Apple 페이지로 이동 [여기](https://developer.apple.com/documentation/usernotifications#//apple_ref/doc/uid/TP40008194-CH8-SW1) Apple 푸시 알림 서비스에 익숙해지려면 다음을 수행하십시오.

APNs를 사용하려면 **인증서** 파일(.cer 파일), 푸시 **개인 키** (a .p12 file) 및 **개인 키 암호** Apple에서. 이 작업을 수행하는 방법에 대한 지침은 다음을 참조하십시오 [여기](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/).

#### Google 클라우드 메시징(GCM) 서비스 사용 {#using-the-google-cloud-messaging-gcm-service}

>[!NOTE]
>
>Google은 GCM을 FCM(Firebase Cloud Messaging)이라는 유사한 서비스로 대체하고 있습니다. FCM에 대한 자세한 내용을 보려면 [여기](https://firebase.google.com/docs/cloud-messaging/).

Google 페이지로 이동 [여기](https://developer.android.com/google/gcm/index.html) android™용 Google Cloud Messaging에 익숙해질 수 있습니다.

[다음 단계를 따르십시오](https://developer.android.com/google/gcm/gs.html) 끝 **Google API 프로젝트 만들기**, **GCM 서비스 활성화**, 및 **API 키 가져오기**. 다음이 필요합니다. **API 키** android™ 장치로 푸시 알림을 보냅니다. 또한 다음을 레코딩하십시오. **프로젝트 번호**, 또는 라고도 함 **GCM 발신자 Id**.

다음 단계는 GCM API 키를 만드는 다른 방법을 보여 줍니다.

1. Google에 로그인하고 [Google 개발자 페이지](https://developers.google.com/mobile/add?platform=android&amp;cntapi=gcm).
1. 목록에서 앱을 선택하거나 앱을 만듭니다.
1. Android™ 패키지 이름 아래에 앱 ID, 즉 `com.adobe.cq.mobile.weretail.outdoorsapp`. (작동하지 않는 경우 &quot;test.test&quot;로 다시 시도하십시오.)
1. 클릭 **서비스 선택 및 구성 계속**
1. 클라우드 메시징 을 선택하고 **Google 클라우드 메시징 활성화**.
1. 그러면 새 서버 API 키 및 (신규 또는 기존) 발신자 ID가 표시됩니다.

>[!NOTE]
>
>서버 API 키를 기록합니다. 이 값은 푸시 공급자의 사이트에 입력됩니다.

### 2단계: 푸시 메시지 서비스 등록 및 구성 {#step-register-and-configure-a-push-messaging-service}

AEM은 푸시 알림에 다음 세 가지 서비스 중 하나를 사용하도록 구성되어 있습니다.

* Amazon SNS
* Pushwoosh
* Adobe Mobile Services

*AMAZON SNS* 및 *Pushwoosh* 구성을 사용하면 AEM 화면 내에서 푸시된 을 보낼 수 있습니다.

*Adobe Mobile Services* 구성을 사용하면 Adobe Analytics 계정을 사용하여 Adobe Mobile Services 내에서 푸시 알림을 구성하고 전송할 수 있습니다(하지만 AMS 푸시 알림을 활성화하려면 이 구성을 설정하여 앱을 빌드해야 함).

#### Amazon SNS 메시징 서비스 사용 {#using-the-amazon-sns-messaging-service}

>[!NOTE]
>
>*Amazon SNS에 대한 정보 및 AWS 계정을 만드는 링크를 찾을 수 있습니다 [여기](https://aws.amazon.com/sns/). 1년 동안 무료 통장을 받을 수 있습니다.*

Amazon SNS를 사용하지 않으려면 이 단계를 건너뛸 수 있습니다.

푸시 알림용 Amazon SNS를 설정하려면 다음 단계를 따르십시오.

1. **Amazon SNS에 등록**

   1. 계정 ID를 기록합니다. 형식은 공백이나 대시가 없는 12자리, 즉 &quot;123456789012&quot;이어야 합니다.
   1. 이후 단계(ID 풀 생성)에서는 이러한 영역 중 하나가 필요하므로 &quot;미국 동부&quot; 또는 &quot;유럽 연합&quot; 영역에 있는지 확인합니다.
   1. 등록 후 관리 콘솔에 로그인하고 다음을 선택합니다. [SNS](https://console.aws.amazon.com/sns/) (푸시 알림 서비스). 표시되는 경우 &quot;시작하기&quot;를 클릭합니다.

1. **액세스 키 및 ID 만들기**

   1. 화면 오른쪽 상단에 있는 로그인 이름을 클릭하고 메뉴에서 보안 자격 증명을 선택합니다.
   1. 액세스 키를 클릭하고 아래 공간에서 **새 액세스 키 만들기**.
   1. 클릭 **액세스 키 표시**&#x200B;을 클릭하고, 표시된 액세스 키 ID 및 비밀 액세스 키를 복사하여 저장합니다. 키를 다운로드하는 옵션을 선택하면 동일한 값이 포함된 csv 파일이 제공됩니다.
   1. 다른 보안 관련 인증서 및 기타 인증서는 이 페이지에서 관리할 수 있습니다.

   >[!NOTE]
   >
   >액세스 키는 여러 앱에 사용할 수 있습니다.

   AWS Sandbox 계정을 사용하는 조직의 경우, 단계는 유사하며 여기에 요약되어 있습니다.

   1. 화면 오른쪽 상단에 있는 로그인 이름을 클릭하고 메뉴에서 내 보안 자격 증명을 선택합니다.
   1. 작업 왼쪽 목록에서 사용자 를 클릭하고 사용자 이름을 선택합니다.
   1. 보안 자격 증명 탭을 클릭합니다.
   1. 여기에서 키를 보고 새 키를 만듭니다. 나중에 사용할 수 있도록 키를 저장합니다.

1. **주제 만들기**

   1. 클릭 **주제 만들기** 주제 이름을 선택합니다. 항목 ARN, 항목 소유자, 영역, 표시 이름 등 모든 필드를 기록합니다.
   1. 클릭 **기타 주제 작업** > **주제 정책 편집**. 아래 **이 사용자가 이 주제에 가입하도록 허용**, 선택 **여러분**
   1. 클릭 **정책 업데이트**.

   >[!NOTE]
   >
   >개발, 테스트 및 데모와 같은 다양한 시나리오에 대해 여러 주제를 만들 수 있습니다. 나머지 SNS 구성은 동일하게 유지될 수 있습니다. 다른 주제로 앱을 빌드합니다. 해당 주제로 전송된 푸시 알림은 해당 주제로 빌드된 앱에서만 수신됩니다.

1. **플랫폼 애플리케이션 만들기**

   1. 응용 프로그램, 플랫폼 응용 프로그램 생성 순으로 누릅니다. 이름을 선택하고 플랫폼(iOS용 APNS, Android™용 GCM)을 선택합니다. 플랫폼에 따라 다릅니다. 다른 필드는 입력해야 합니다.

      1. APNS의 경우 P12 파일, 암호, 인증서 및 개인 키를 모두 입력해야 합니다. 이러한 함수는 단계에서 가져와야 합니다. *Apple 푸시 알림 서비스(APNS) 사용* 위.
      1. GCM의 경우 API 키를 입력해야 합니다. 이 값은 단계에서 가져와야 합니다. *Google 클라우드 메시징(GCM) 서비스 사용* 위.

   1. 지원하는 각 플랫폼에 대해 위 단계를 한 번 반복합니다. iOS과 Android™을 모두 푸시하려면 두 개의 Platform 애플리케이션을 만들어야 합니다.

1. **ID 풀 만들기**

   1. 사용 [코그니토](https://console.aws.amazon.com/cognito) 인증되지 않은 사용자의 기본 데이터를 저장하는 ID 풀을 만듭니다. 참고로, 현재 Amazon Cognito에서는 &quot;us-east&quot; 및 &quot;eu&quot; 지역만 지원됩니다.
   1. 이름을 지정하고 &quot;인증되지 않은 ID에 대한 액세스 활성화&quot; 상자를 선택합니다.
   1. 다음 페이지에서(&quot;*귀하의 Cognito ID는 귀하의 리소스에 대한 액세스 권한이 필요합니다.*&quot;) 허용 을 클릭합니다.
   1. 페이지 오른쪽 상단에서 &quot; 링크를 클릭합니다.*ID 풀 편집&quot;*. ID 풀 ID가 표시됩니다. 나중에 이 텍스트를 저장하십시오.
   1. 같은 페이지에서 &quot;인증되지 않은 역할&quot; 옆에 있는 드롭다운을 선택하고 Cognito_ 역할이 있는지 확인합니다&lt;pool name=&quot;&quot;>UnauthRole이 선택되었습니다. 변경 사항을 저장합니다.

1. **액세스 구성**

   1. 에 로그인 [ID 및 액세스 관리](https://console.aws.amazon.com/iam/home) (IAM)
   1. 역할을 선택합니다.
   1. 이전 단계에서 생성된 Cognito_ 라는 역할을 클릭합니다.&lt;youridentitypoolname>Unauth_Role. 표시된 &quot;역할 ARN&quot;을 기록합니다.
   1. 아직 열리지 않은 경우 &quot;인라인 정책&quot;을 엽니다. oneClick_Cognito_와 같은 이름의 정책이 표시됩니다.&lt;youridentitypoolname>Unauth_Role_1234567890123.
   1. &quot;정책 편집&quot;을 클릭합니다. 정책 문서의 콘텐츠를 다음 JSON 조각으로 바꾸기:

   <table>
    <tbody>
     <tr>
     <td><p> </p> <p>{</p> <p> "버전": "2012-10-17",</p> <p> "문": [</p> <p> {</p> <p> "작업": [</p> <p> "mobileanalytics:PutEvents",</p> <p> "cognito-sync:*",</p> <p> "SNS:CreatePlatformEndpoint",</p> <p> "SNS:Subscribe"</p> <p> ],</p> <p> "효과": "허용",</p> <p> "리소스": [</p> <p> "*"</p> <p> ]</p> <p> }</p> <p> ]</p> <p>}</p> <p> </p> </td>
     </tr>
    </tbody>
    </table>

   1. 클릭 **정책 적용**.

#### Pushwoosh 메시징 서비스 사용 {#using-the-pushwoosh-messaging-service}

Pushwoosh를 사용하지 않으려면 이 단계를 건너뛸 수 있습니다.

Pushwoosh를 사용하려면:

1. **Pushwoosh에 등록**

   1. pushwoosh.com으로 이동하여 계정을 만듭니다.

1. **API 액세스 토큰 만들기**

   1. Pushwoosh 사이트에서 API 액세스 메뉴 항목으로 이동하여 API 액세스 토큰을 생성합니다. 이 토큰을 안전하게 기록하십시오.

1. **앱 만들기**

   1. Android™ 지원의 경우 GCM API 키를 제공해야 합니다.
   1. 앱을 구성할 때 프레임워크로 Cordova를 선택합니다.
   1. iOS 지원의 경우 인증서 파일(.cer), 푸시 인증서(.p12) 및 개인 키 암호를 제공해야 합니다. 이러한 암호는 Apple의 APNS 사이트에서 가져와야 합니다. [프레임워크]에서 [Cordova]를 선택합니다.
   1. Pushwoosh는 해당 앱에 대한 앱 ID를 &quot;XXXXX-XXXXX&quot; 형식으로 생성합니다. 여기서 각 X는 16진수 값(0 - F)입니다.

>[!NOTE]
>
>*두 번째 앱이 동일한 앱 ID(및 기타 관련 값: API 액세스 토큰 및 GCM ID)로 AEM에 구성된 경우 AEM에서 두 번째 앱을 통해 전송된 푸시 알림은 해당 앱 ID가 있는 다른 앱으로 이동합니다.*

### 3단계: 앱에 푸시 지원 추가 {#step-add-push-support-to-the-app}

#### ContentSync 구성 추가 {#add-contentsync-configuration}

notificationsConfig라는 두 개의 콘텐츠 노드(app-config와 app-config-dev에 각각 하나씩)를 만듭니다.

* /content/`<your app>`/shell/jcr:content/pge-app/app-config-dev/notificationsConfig
* /content/`<your app>`/shell/jcr:content/pge-app/app-config/notificationsConfig

다음 속성(.content.xml 파일) 사용:
&lt;jcr:root xmlns:jcr=&quot; &lt;span id=&quot; translate=&quot;no&quot; />https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/1.0/index.html](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/1.0/index.html)&quot; xmlns:nt=&quot; [https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/1.0/index.html](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/1.0/index.html)&quot; jcr:primaryType=&quot;nt:unstructured&quot; excludeProperties=&quot;[appAPIAccessToken]&quot; path=&quot;../../../...&quot;
[
targetRootDirectory=&quot;www&quot; type=&quot;notificationsconfig&quot;/>

>[!NOTE]
>
>콘텐츠 동기화 핸들러가 해당 노드를 찾고, 없는 경우 pge-notifications-config.json 파일을 작성하지 않습니다.

#### 클라이언트 라이브러리 추가 {#add-client-libraries}

푸시 알림 클라이언트 라이브러리는 다음 단계에 따라 앱에 추가해야 합니다.

CRXDE Lite:

1. 다음으로 이동 */etc/designs/phonegap/&lt;app name=&quot;&quot;>/clientlibsall.*
1. 속성 창에서 포함 섹션을 두 번 클릭합니다.
1. 표시되는 대화 상자에서 + 단추를 클릭하여 클라이언트 라이브러리를 추가합니다.
1. 새 텍스트 필드에 &quot;cq.mobile.push&quot;를 추가하고 [확인]을 클릭합니다.
1. cq.mobile.push.amazon이라는 것을 한 개 더 추가하고 확인 을 클릭합니다.
1. 변경 사항을 저장합니다.

>[!NOTE]
>
>푸시 알림이 앱에서의 공간 고려 사항에 대해 제거되거나 사용되지 않는 경우 및 콘솔 오류 메시지를 방지하려면 앱에서 이러한 clientlib을 제거합니다.

### 4단계: 테스트를 위한 전화 준비 {#step-prepare-a-phone-for-testing}

>[!NOTE]
>
>*푸시 알림의 경우 에뮬레이터가 푸시 알림을 받을 수 없으므로 실제 디바이스에서 테스트해야 합니다.*

#### IOS {#ios}

iOS의 경우 macOS 컴퓨터를 사용하고 [iOS 개발자 프로그램](https://developer.apple.com/programs/ios/). 일부 기업은 모든 개발자가 사용할 수 있는 기업 라이선스를 보유하고 있습니다.

XCode 8.1에서 푸시 알림을 사용하기 전에 프로젝트의 기능 탭으로 이동하여 푸시 알림 토글을 켜야 합니다.

#### Android™ {#android}

CLI를 사용하여 Android™ 휴대폰에 앱을 설치하려면 다음을 참조하십시오. **6단계 - 앱 빌드 및 배포**) 먼저 휴대폰을 &quot;개발자 모드&quot;로 설정해야 합니다. 다음을 참조하십시오 [온디바이스 개발자 옵션 활성화](https://developer.android.com/tools/device.html#developer-device-options) 자세한 내용은 을 참조하십시오.

### 5단계: AEM 앱에서 푸시 구성 {#step-configure-push-on-aem-apps}

구성된 모바일 장치를 빌드하고 배포하기 전에 사용하기로 한 메시징 서비스에 대한 알림 설정을 구성해야 합니다.

1. 푸시 알림에 적절한 인증 그룹을 만듭니다.
1. 적절한 사용자로 AEM에 로그인하고 앱 탭을 클릭합니다.
1. 앱을 클릭합니다.
1. Cloud Service 관리 타일을 찾아 연필을 클릭하여 클라우드 구성을 수정합니다.
1. 알림 구성으로 Amazon SNS Connection, Pushwoosh Connection 또는 Adobe Mobile Services 를 선택합니다.
1. 공급자 등록 정보를 입력하고 제출을 눌러 저장한 다음 완료를 누릅니다. 이 단계에서는 AMS가 있는 경우를 제외하고 원격으로 확인되지 않습니다.
1. 이제 Cloud Service 관리 타일에 방금 입력한 구성이 표시됩니다.

### 6단계: 앱 빌드 및 배포 {#step-build-and-deploy-the-app}

**참고:** 지침 보기 [여기](/help/mobile/building-app-mobile-phonegap.md) PhoneGap 응용 프로그램을 빌드하는 중입니다.

PhoneGap을 사용하여 앱을 빌드하고 배포하는 방법에는 두 가지가 있습니다.

**참고:** 푸시 알림 테스트의 경우 푸시 알림은 푸시 공급자(Apple 또는 Google)와 디바이스 간에 고유한 프로토콜을 사용하기 때문에 에뮬레이터로 충분하지 않습니다. 현재 Mac/PC 하드웨어 및 에뮬레이터는 이 기능을 지원하지 않습니다.

1. *PhoneGap Build* 는 PhoneGap에서 제공하는 서비스로, 서버에 앱을 빌드하고 이를 장치로 직접 다운로드할 수 있습니다. 다음 PhoneGap Build 설명서를 참조하십시오. `https://build.phonegap.com/` PhoneGap Build 설정 및 사용 방법을 알아봅니다.

1. *PhoneGap 명령줄 인터페이스* (CLI)를 사용하면 명령줄에서 다양한 PhoneGap 명령 집합을 사용하여 앱을 빌드하고 디버깅하고 배포할 수 있습니다. PhoneGap 개발자 설명서 를 참조하십시오(`https://docs.phonegap.com/en/edge/guide_cli_index.md.html#The%20Command-Line%20Interface`) PhoneGap CLI를 설정하고 사용하는 방법을 알아봅니다.

### 7단계: 푸시 알림 보내기 {#step-send-a-push-notification}

알림을 만들고 보내려면 다음 단계를 수행합니다.

1. 알림 만들기

   * AEM Mobile 앱의 대시보드에서 푸시 알림 타일을 찾습니다.
   * 오른쪽 위의 메뉴에서 &quot;만들기&quot;를 선택합니다. 이 단추는 클라우드 구성이 처음 설정될 때까지 사용할 수 없습니다.
   * 알림 만들기 마법사에서 제목과 메시지를 입력한 다음 &quot;만들기&quot; 버튼을 클릭합니다. 이제 알림을 즉시 또는 나중에 전송할 준비가 되었습니다. 이를 편집하고 메시지 및/또는 제목을 변경 및 저장할 수 있습니다.

1. 알림 보내기

   * 앱 대시보드에서 푸시 알림 타일을 찾습니다.
   * 알림을 선택하거나 오른쪽 하단에 있는 세부 정보 버튼을 클릭합니다(. . .) 알림의 목록을 표시합니다. 이 목록은 알림을 전송할 준비가 되었는지, 이미 전송되었는지 또는 전송 중 오류가 발생했는지 여부도 표시합니다.
   * 한 개의 알림에 대한 확인란을 선택하고 목록 위에 있는 &quot;알림 보내기&quot; 버튼을 클릭합니다. 표시되는 대화 상자에서 알림을 &quot;취소&quot; 또는 &quot;전송&quot;할 기회가 한 번 있습니다.

1. 결과 처리

   * 푸시 알림 서비스(Amazon SNS 또는 Pushwoosh)가 전송 요청을 수신하고 유효한 것으로 확인한 후 기본 공급자(APNS 및 GCM)에게 전송하면 전송 대화 상자가 메시지 없이 닫힙니다. 알림 목록에 해당 알림의 상태가 전송됨으로 나열됩니다.
   * 푸시 전송이 실패하면 대화 상자에 문제를 나타내는 메시지가 표시됩니다. 알림 목록에는 해당 알림의 상태가 오류로 표시되지만 문제가 해결되면 알림을 다시 전송할 수 있습니다. 오류가 있는 경우 서버 오류 로그에 추가 오류 정보가 표시됩니다.
   * iOS과 Android™ 푸시 알림 사이에는 몇 가지 플랫폼 차이가 있습니다. 그 중 하나는:

      * Android™에서 앱을 배포한 후 CLI를 사용하여 빌드하면 앱이 시작됩니다. iOS에서는 수동으로 시작해야 합니다. 푸시 등록 단계는 시작 시 발생하므로 Android™ 앱은 푸시 알림을 즉시 수신할 수 있지만(이미 시작되고 등록되었기 때문) iOS 앱은 그럴 수 없습니다.
      * Android™에서는 확인 단추 텍스트가 모두 대문자로 표시되고(인앱 알림에 추가된 다른 모든 단추에서는) iOS에서는 그렇지 않습니다.

AMS 푸시 알림의 경우 AMS 서버에서 알림을 구성하고 전송해야 합니다. AMS는 AWS 및 Pushwoosh를 사용하여 AEM 알림에서 제공하는 기능 이상의 추가 푸시 알림 기능을 제공합니다.

>[!NOTE]
>
>*푸시 알림은 전달이 보장되지 않습니다. 알림과 더 비슷합니다. 모든 사람이 듣지만 배달 메커니즘이 보장되지 않도록 최선을 다합니다. 또한 푸시를 전달하는 시간은 1초 미만에서 최대 30분까지 다양할 수 있습니다.*

### 푸시 알림으로 딥링크 구성 {#configuring-deep-linking-with-push-notifications}

딥링크란 무엇입니까? 푸시 알림의 컨텍스트에서, 앱을 열거나 앱 내의 지정된 위치로 안내(열려 있는 경우)할 수 있도록 하는 수단입니다.

어떻게 작동합니까? 푸시 알림의 작성자는 선택적으로 버튼 레이블(즉, &quot;표시!&quot;)을 추가합니다. 을 누르고 시각적 경로 브라우저를 통해 알림에 연결할 페이지를 선택합니다. 전송 시 인앱 메시지에서 확인 단추가 &quot;해제&quot; 단추와 새 단추(&quot;표시!&quot;)로 바뀌는 것을 제외하고 푸시가 정상적으로 발생합니다. 도 표시됩니다. 새 버튼을 클릭하면 앱이 앱 내의 지정된 페이지로 이동합니다. 닫기 를 클릭하면 메시지가 지워집니다.

앱이 열려 있지 않으면 음영이 정상적으로 표시됩니다. 음영에 있는 알림에 대해 작업을 수행하면 앱이 열린 다음 푸시 알림에 구성된 내용을 기반으로 사용자에게 딥링크 버튼이 표시됩니다.

알림을 만들고, 버튼 텍스트 및 선택적 딥링크에 대한 링크 경로를 추가합니다.

>[!CAUTION]
>
>대시보드의 푸시 알림 타일에 액세스하려면 아래 단계를 따르십시오.

1. 의 오른쪽 위 모서리에 있는 편집 을 클릭합니다. **Cloud Service 관리** 타일.

   ![chlimage_1-108](assets/chlimage_1-108.png)

1. 다음 항목 선택 **Pushwoosh 연결**. **다음**&#x200B;을 클릭합니다.

   ![chlimage_1-109](assets/chlimage_1-109.png)

1. 속성의 세부 정보를 입력하고 를 클릭합니다 **제출**.

   ![chlimage_1-110](assets/chlimage_1-110.png)

   구성을 제출하면 **푸시 알림** 타일이 대시보드에 표시됩니다.

   ![chlimage_1-111](assets/chlimage_1-111.png)

### 알림 만들기 마법사 {#create-notification-wizard}

한 번 **푸시 알림** 타일이 대시보드에 표시되면 알림 만들기 마법사를 사용하여 컨텐츠를 추가합니다.

1. 의 오른쪽 위 모서리에 있는 추가 기호를 클릭합니다. **푸시 알림** 타일을 사용하여 열기 **알림 만들기 마법사**.

   ![chlimage_1-112](assets/chlimage_1-112.png)

1. 링크 경로에서 찾아보기 아이콘을 클릭하면 앱의 콘텐츠 구조가 사용자에게 표시됩니다.

   경로를 선택한 후 확인 아이콘을 클릭합니다.

   ![chlimage_1-113](assets/chlimage_1-113.png)

   >[!NOTE]
   >
   >링크 단추 텍스트는 20자로 제한됩니다.
   >
   >최종 사용자에게 최신 버전의 애플리케이션이 없고 연결된 경로를 사용할 수 없는 경우, 딥 링크 작업을 확인하면 사용자가 앱의 기본 페이지로 이동합니다.

1. 다음을 입력합니다. **텍스트 세부 사항** 다음에서 **알림 만들기 마법사** 및 클릭 **만들기**.

   ![chlimage_1-114](assets/chlimage_1-114.png)

   에서 만든 푸시 알림을 클릭하여 세부 정보를 엽니다. **푸시 알림** 타일.

   속성을 편집하거나, 알림을 보내거나, 알림을 삭제할 수 있습니다.

   ![chlimage_1-115](assets/chlimage_1-115.png)

>[!NOTE]
>
>**추가 정보**:
>
>Pushwoosh 및 Amazon SNS는 6.4 릴리스 이후부터 지원되지 않으며 패키지 공유에서 추가 기능으로 사용할 수 있습니다.

### 다음 단계 {#the-next-steps}

앱의 푸시 알림에 대한 자세한 내용을 이해하면 을 참조하십시오. [AEM Mobile 콘텐츠 개인화](/help/mobile/phonegap-aem-mobile-content-personalization.md).
