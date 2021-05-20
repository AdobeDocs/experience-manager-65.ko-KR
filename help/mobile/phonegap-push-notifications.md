---
title: 알림 푸시
seo-title: 알림 푸시
description: AEM Mobile 앱에서 푸시 알림을 사용하는 방법에 대해 알려면 이 페이지를 따르십시오.
seo-description: AEM Mobile 앱에서 푸시 알림을 사용하는 방법에 대해 알려면 이 페이지를 따르십시오.
uuid: 0ed8b183-ef81-487f-8f35-934d74ec82af
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: ed8c51d2-5aac-4fe8-89e8-c175d4ea1374
exl-id: 375f2f40-1b98-4e21-adee-cbea274e6a2a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '3291'
ht-degree: 1%

---

# 알림 푸시{#push-notifications}

>[!NOTE]
>
>단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: React)이 필요한 프로젝트에 SPA 편집기를 사용하는 것이 좋습니다. [추가 정보](/help/sites-developing/spa-overview.md).

중요한 알림을 사용하여 AEM Mobile 앱 사용자에게 즉시 알릴 수 있는 것은 모바일 앱과 마케팅 캠페인의 가치에 중요합니다. 여기서는 앱이 푸시 알림을 받을 수 있도록 해야 하는 단계와 AEM Mobile에서 휴대폰에 설치된 앱으로 푸시를 구성하고 전송하는 방법에 대해 설명합니다. 또한 이 섹션에서는 [딥 링크](#deeplinking) 기능을 푸시 알림에 구성하는 방법에 대해 설명합니다.

>[!NOTE]
>
>*푸시 알림이 전달을 보장하지 않습니다.그들은 발표와 더 비슷합니다. 가장 좋은 노력은 모든 사람이 이 플러그인을 수신하지만 보장된 게재 메커니즘이 아님을 확인하는 것입니다. 또한, 푸시 배달 시간은 1초 미만에서 최대 30분까지 달라질 수 있습니다.*

AEM에서 푸시 알림을 사용하려면 몇 가지 다른 기술이 필요합니다. 먼저 푸시 알림 서비스 공급자를 사용하여 알림 및 장치를 관리해야 합니다(AEM에서는 아직 이렇게 하지 않음). 두 공급자는 AEM을 사용하여 즉시 구성됩니다.[Amazon Simple Notification Service](https://aws.amazon.com/sns/)(또는 SNS) 및 [Pushwoosh](https://www.pushwoosh.com/) 둘째, 주어진 모바일 OS에 대한 푸시 기술은 iOS 장치용 Apple의 푸시 알림 서비스(또는 APNS) 와 같은 적절한 서비스를 통과해야 합니다.및 Android 장치용 Google Cloud 메시지(또는 GCM)를 참조하십시오. AEM은 이러한 플랫폼별 서비스와 직접 통신하지 않지만, 이러한 서비스에서 푸시를 실행하려면 알림과 함께 일부 관련 구성 정보를 AEM에서 제공해야 합니다.

설치 및 구성 후에는(아래에 설명된 대로) 다음과 같이 작동합니다.

1. 푸시 알림이 AEM에서 생성되어 서비스 공급자(Amazon SNS 또는 Pushwoosh)에게 전송됩니다.
1. 서비스 공급자가 이 콘텐츠를 수신하여 핵심 공급자(APNS 또는 GCM)에게 보냅니다.
1. 코어 공급자는 알림을 해당 푸시에 등록된 모든 장치에 푸시합니다. 각 장치에 대해 셀룰러 데이터 네트워크 또는 WiFi(현재 장치에서 사용 가능한 것)를 사용합니다.
1. 등록된 앱이 실행되고 있지 않은 경우 장치가 알림을 표시합니다. 알림을 탭하면 앱이 시작되고 앱 내에 알림이 표시됩니다. 애플리케이션이 이미 실행 중인 경우 인앱 알림만 표시됩니다.

이 AEM 릴리스는 iOS 및 Android 모바일 장치를 지원합니다.

## 개요 및 프로시저 {#overview-and-procedure}

AEM Mobile 앱에서 푸시 알림을 사용하려면 다음 높은 수준의 단계를 수행해야 합니다.

일반적으로 AEM 개발자는 다음을 수행합니다.

1. Apple 및 Google 메시징 서비스에 등록
1. 푸시 메시지 서비스에 등록하고 구성합니다
1. 앱에 푸시 지원 추가
1. 테스트 전화 준비

AEM 관리자는 다음을 수행합니다.

1. AEM 앱에서 푸시 구성
1. 앱 빌드 및 배포
1. 푸시 알림 보내기
1. 딥 연결 구성 *(선택 사항)*

### 1단계:Apple 및 Google 메시징 서비스에 등록 {#step-register-with-apple-and-google-messaging-services}

#### Apple 푸시 알림 서비스(APNS) {#using-the-apple-push-notification-service-apns} 사용

Apple 푸시 알림 서비스에 익숙해지려면 Apple 페이지 [여기](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html)로 이동하십시오.

APNS를 사용하려면 Apple의 **Certificate** 파일(.cer 파일), 푸시 **개인 키**(a.p12 파일) 및 **개인 키 암호**&#x200B;가 필요합니다. 방법 지침은 [여기](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ProvisioningDevelopment.html)에서 찾을 수 있습니다.

#### Google Cloud Messaging(GCM) 서비스 사용 {#using-the-google-cloud-messaging-gcm-service}

>[!NOTE]
>
>Google에서 GCM을 Firebase Cloud Messaging(FCM)이라는 유사한 서비스로 대체하고 있습니다. FCM에 대한 자세한 내용을 보려면 [여기](https://developers.google.com/cloud-messaging/faq)를 클릭하십시오.

Google 페이지 [여기](https://developer.android.com/google/gcm/index.html)로 이동하여 Android용 Google Cloud Messaging에 익숙해지십시오.

[여기](https://developer.android.com/google/gcm/gs.html)Google API 프로젝트 만들기&#x200B;**,** GCM 서비스&#x200B;**활성화 및** API 키 가져오기&#x200B;**에 이르는 단계를 따라야 합니다.** Android 장치로 푸시 알림을 전송하려면 **API 키**&#x200B;가 필요합니다. 또한 **프로젝트 번호**&#x200B;를 기록하십시오. 이 이름은 경우에 따라 **GCM 발신자 ID**&#x200B;라고도 합니다.

다음 단계는 GCM API 키를 만드는 다른 방법을 보여줍니다.

1. google에 로그인하고 [Google의 개발자 페이지](https://developers.google.com/mobile/add?platform=android&amp;cntapi=gcm)로 이동합니다.
1. 목록에서 앱을 선택하거나 새 앱을 만듭니다.
1. Android 패키지 이름에서 앱 ID(예:`com.adobe.cq.mobile.weretail.outdoorsapp` (작동하지 않는 경우 &quot;test.test&quot;로 다시 시도하십시오.)
1. **계속 을 클릭하여 서비스 선택 및 구성**
1. 클라우드 메시징 을 선택한 다음 **Google 클라우드 메시지 활성화**&#x200B;를 클릭합니다.
1. 그러면 새 서버 API 키와 (신규 또는 기존) 발신자 ID가 표시됩니다.

>[!NOTE]
>
>서버 API 키를 기록합니다. 이 값은 푸시 공급자의 사이트에 입력됩니다.

### 2단계:푸시 메시지 서비스 등록 및 구성 {#step-register-and-configure-a-push-messaging-service}

AEM은 푸시 알림에 세 가지 서비스 중 하나를 사용하도록 구성되어 있습니다.

* Amazon SNS
* Pushwoosh
* Adobe Mobile Services

*Amazon* SNS와  ** Pushwooshconfigurations를 사용하면 AEM screens 내에서 푸시된 푸시된 푸시된 푸시된 푸시된 푸시된 파일을 보낼 수 있습니다.

*Adobe Mobile* Services 구성에서는 Adobe Analytics 계정을 사용하여 Adobe Mobile Services 내에서 푸시 알림을 구성하고 전송할 수 있습니다(하지만 AMS 푸시 알림을 활성화하려면 이 구성 세트로 앱을 빌드해야 함).

#### Amazon SNS 메시징 서비스 {#using-the-amazon-sns-messaging-service} 사용

>[!NOTE]
>
>*Amazon SNS에 대한 정보와 새 AWS 계정을 만들기 위한 링크는  [여기](https://aws.amazon.com/sns/)에서 찾을 수 있습니다. 1년 동안 무료 계정을 얻을 수 있습니다.*

Amazon SNS를 사용하지 않으려면 이 단계를 건너뛸 수 있습니다.

푸시 알림용 Amazon SNS를 설정하려면 다음 단계를 따르십시오.

1. **Amazon SNS에 등록**

   1. 계정 Id를 기록합니다. 형식은 공백 또는 대시가 없는 12자리여야 합니다(예:&quot;123456789012&quot;.
   1. 이후 단계(Identity Pool Creation)에 따라 &quot;미국-동부&quot; 또는 &quot;eu&quot; 지역에 있는지 확인합니다.
   1. 등록 후 관리 콘솔에 로그인하여 [SNS](https://console.aws.amazon.com/sns/) (푸시 알림 서비스)를 선택합니다. &quot;시작하기&quot;가 나타나면 를 클릭합니다.

1. **액세스 키 및 ID 만들기**

   1. 화면 오른쪽 상단에 있는 로그인 이름을 클릭하고 메뉴에서 보안 자격 증명을 선택합니다.
   1. 액세스 키를 클릭하고 아래 스페이스에서 **새 액세스 키 만들기**&#x200B;를 클릭합니다.
   1. **액세스 키 표시**&#x200B;를 클릭하고, 표시된 액세스 키 ID와 비밀 액세스 키를 복사하여 저장합니다. 키를 다운로드하는 옵션을 선택하면 동일한 값이 들어 있는 csv 파일이 표시됩니다.
   1. 다른 보안 관련 인증서 및 기타 다른 인증서는 이 페이지에서 관리할 수 있습니다.

   >[!NOTE]
   >
   >액세스 키는 여러 앱에 사용할 수 있습니다.

   &quot;AWS Sandbox&quot; 계정을 사용하는 조직의 경우 이 단계는 매우 유사하며 여기에 요약되어 있습니다.

   1. 화면 오른쪽 상단에 있는 로그인 이름을 클릭하고 메뉴에서 내 보안 자격 증명을 선택합니다.
   1. 작업 왼쪽 목록에서 사용자 를 클릭하고 사용자 이름을 선택합니다.
   1. 보안 자격 증명 탭을 클릭합니다.
   1. 여기에서 키가 표시되고 새 키가 만들어집니다. 나중에 사용할 수 있도록 키를 저장합니다.


1. **주제 만들기**

   1. **주제 만들기**&#x200B;를 클릭하고 주제 이름을 선택합니다. 주제 ARN, 주제 소유자, 영역, 표시 이름과 같은 모든 필드를 기록합니다.
   1. **기타 항목 작업** > **주제 정책 편집**&#x200B;을 클릭합니다. **이러한 사용자가 이 주제에 가입할 수 있도록 허용**&#x200B;에서 **모두 를 선택합니다.**
   1. **정책 업데이트**&#x200B;를 클릭합니다.

   >[!NOTE]
   >
   >개발, 테스트, 데모 등과 같은 다양한 시나리오에 대해 여러 주제를 만들 수 있습니다. 나머지 SNS 구성은 그대로 유지될 수 있습니다. 다른 주제를 사용하여 앱을 빌드합니다.해당 주제에 전송되는 푸시 알림은 해당 주제와 함께 빌드된 앱에서만 수신됩니다.

1. **플랫폼 애플리케이션 만들기**

   1. 응용 프로그램, 플랫폼 응용 프로그램 만들기를 차례로 클릭합니다. 이름을 선택하고 플랫폼(iOS용 APNS, Android용 GCM)을 선택합니다. 플랫폼에 따라 다른 필드를 입력해야 합니다.

      1. APNS의 경우 P12 파일, 암호, 인증서 및 개인 키를 모두 입력해야 합니다. 위의 *Apple APNS(Push Notification Service) 사용*&#x200B;단계에서 가져와야 합니다.
      1. GCM의 경우 API 키를 입력해야 합니다. 이 값은 위의 *GCM(Google Cloud Messaging) 서비스 사용*&#x200B;에서 얻었을 것입니다.
   1. 지원할 각 플랫폼에 대해 위의 단계를 한 번 반복합니다. iOS와 Android를 모두 푸시하려면 두 개의 Platform 애플리케이션을 만들어야 합니다.


1. **ID 풀 만들기**

   1. [Cognito](https://console.aws.amazon.com/cognito)를 사용하여 인증되지 않은 사용자의 기본 데이터를 저장하는 자격 증명 풀을 만듭니다. 현재 &quot;미국-동부&quot; 및 &quot;eu&quot; 리전만 Amazon Cognito에서 지원합니다.
   1. 이름을 지정하고 &quot;인증되지 않은 ID에 액세스 활성화&quot; 상자를 선택합니다.
   1. 다음 페이지(&quot;*Your Cognito Id에서 리소스에 액세스해야 함*&quot;)에서 허용을 클릭합니다.
   1. 페이지 오른쪽 상단에서 &quot;*ID 풀 편집&quot;* 링크를 클릭합니다. ID 풀 ID가 표시됩니다. 이 텍스트를 나중에 저장할 수 있습니다.
   1. 동일한 페이지에서 &quot;인증되지 않은 역할&quot; 옆의 드롭다운을 선택하고 Cognito_&lt;풀 이름>UnauthRole 역할이 선택되었는지 확인합니다. 변경 사항을 저장합니다.

1. **액세스 구성**

   1. [Identity and Access Management](https://console.aws.amazon.com/iam/home)에 로그인(IAM)
   1. 역할 선택
   1. 이전 단계에서 생성된 Cognito_&lt;yourIdentityPoolName>Unauth_Role을 클릭합니다. 표시된 &quot;역할 ARN&quot;을 기록합니다.
   1. 아직 열려 있지 않으면 &quot;인라인 정책&quot;을 엽니다. 여기에는 oneClick_Cognito_&lt;yourIdentityPoolName>Unauth_Role_1234567890123 등의 이름이 있는 정책이 표시됩니다.
   1. &quot;정책 편집&quot;을 클릭합니다. 정책 문서의 컨텐츠를 다음 JSON 코드 조각으로 바꿉니다.

   <table>
    <tbody>
     <tr>
     <td><p> </p> <p>{</p> <p> "버전":"2012-10-17",</p> <p> "구문": [</p> <p> {</p> <p> "작업": [</p> <p> "mobileanalytics:PutEvents",</p> <p> "cognito-sync:*",</p> <p> "SNS:CreatePlatformEndpoint",</p> <p> "SNS:가입"</p> <p> ],</p> <p> "효과":"허용",</p> <p> "리소스": [</p> <p> "*"</p> <p> _</p> <p> }</p> <p> _</p> <p>}</p> <p> </p> </td>
     </tr>
    </tbody>
    </table>

   1. **정책 적용**&#x200B;을 클릭합니다.


#### Pushwoosh 메시징 서비스 {#using-the-pushwoosh-messaging-service} 사용

Pushwoosh를 사용하지 않으려면 이 단계를 건너뛸 수 있습니다.

Pushwoosh를 사용하려면

1. **Pushwoosh에 등록**

   1. pushwoosh.com으로 이동하여 새 계정을 만듭니다.

1. **API 액세스 토큰 만들기**

   1. 푸시 사이트, API 액세스 메뉴 항목으로 이동하여 API 액세스 토큰을 생성합니다. 이 내용을 반드시 기록해야 합니다.

1. **새 앱 만들기**

   1. Android 지원의 경우 GCM API 키를 제공해야 합니다.
   1. 앱을 구성할 때 프레임워크로 Cordova를 선택합니다.
   1. iOS 지원의 경우 인증서 파일(.cer), 푸시 인증서(.p12) 및 개인 키 암호를 제공해야 합니다.이는 애플의 APNS 사이트에서 얻어졌어야 했다. 프레임워크에서 Cordova를 선택합니다.
   1. Pushwoosh는 해당 앱의 앱 ID를 &quot;XXXXX-XXXXXXX&quot; 형태로 생성합니다. 여기서 각 X는 16진수 값(0~F)입니다.

>[!NOTE]
>
>*두 번째 앱이 동일한 앱 ID(및 기타 관련 값)를 사용하여 AEM에 구성된 경우:API 액세스 토큰 및 GCM Id)인 경우, AEM의 두 번째 앱을 통해 전송된 모든 푸시 알림은 해당 앱 ID가 있는 다른 앱으로 이동합니다.*

### 3단계:앱 {#step-add-push-support-to-the-app}에 푸시 지원 추가

#### ContentSync 구성 추가 {#add-contentsync-configuration}

notificationsConfig라는 두 개의 컨텐츠 노드(app-config에 하나, app-config-dev에 하나)를 만듭니다.

* /content/`<your app>`/shell/jcr:content/page-app/app-config-dev/notificationsConfig
* /content/`<your app>`/shell/jcr:content/page-app/app-config/notificationsConfig

다음 속성(.content.xml 파일) 사용:
&lt;jcr:root xmlns:jcr=&quot; [https://www.jcp.org/jcr/1.0](https://www.jcp.org/jcr/1.0)&quot; xmlns:nt=&quot; [https://www.jcp.org/jcr/nt/1.0](https://www.jcp.org/jcr/nt/1.0)&quot;
jcr:primaryType=&quot;nt:un구조화되지 않음&quot;
excludeProperties=&quot;[appAPIaccessToken]&quot;
path=&quot;../../../..&quot;
targetRootDirectory=&quot;www&quot;
type=&quot;notificationsconfig&quot;/>

>[!NOTE]
>
>컨텐츠 동기화 처리기는 해당 노드를 찾으며 노드가 없으면 page-notifications-config.json 파일을 쓰지 않습니다.

#### 클라이언트 라이브러리 추가 {#add-client-libraries}

푸시 알림 클라이언트 라이브러리를 다음 단계에 따라 앱에 추가해야 합니다.

CRXDE Lite:

1. */etc/designs/phonegap/&lt;app name>/clientlibsall으로 이동합니다.*
1. 속성 창에서 포함 섹션을 두 번 클릭합니다.
1. 나타나는 대화 상자에서 + 단추를 클릭하여 새 클라이언트 라이브러리를 추가합니다.
1. 새 텍스트 필드에서 &quot;cq.mobile.push&quot;를 추가하고 확인을 클릭합니다.
1. cq.mobile.push.amazon이라는 이름을 한 개 더 추가하고 확인을 클릭합니다.
1. 변경 사항을 저장합니다.

>[!NOTE]
>
>앱의 공간 고려 사항에 대해 푸시 알림이 제거되거나 사용되지 않는 경우, 콘솔 오류 메시지가 표시되지 않도록 앱에서 이러한 clientlibs를 제거합니다.

### 4단계:테스트 전화 준비 {#step-prepare-a-phone-for-testing}

>[!NOTE]
>
>*푸시 알림의 경우 에뮬레이터가 푸시 알림을 받을 수 없으므로 실제 장치에서 테스트해야 합니다.*

#### iOS {#ios}

iOS의 경우 Mac OS 컴퓨터를 사용해야 하며 [iOS 개발자 프로그램](https://developer.apple.com/programs/ios/)에 참여해야 합니다. 일부 기업은 모든 개발자가 사용할 수 있는 기업 라이센스를 보유하고 있습니다.

XCode 8.1을 사용하면 푸시 알림을 사용하기 전에 프로젝트의 기능 탭으로 이동하여 푸시 알림 토글을 켜십시오.

#### Android {#android}

CLI를 사용하여 Android 휴대폰에 앱을 설치하려면 다음을 참조하십시오.**6단계 - 앱**)을 빌드하고 배포합니다. 먼저 휴대폰을 &quot;개발자 모드&quot;로 설정해야 합니다. 이 작업에 대한 자세한 내용은 [장치 내 개발자 옵션 활성화](https://developer.android.com/tools/device.html#developer-device-options) 를 참조하십시오.

### 5단계:AEM 앱에서 푸시 구성 {#step-configure-push-on-aem-apps}

구성된 모바일 장치에 빌드하고 배포하기 전에 사용하도록 결정한 메시징 서비스에 대한 알림 설정을 구성해야 합니다.

1. 푸시 알림에 대한 적절한 권한 부여 그룹을 만듭니다.
1. 적절한 사용자로 AEM에 로그인하고 앱 탭을 클릭합니다.
1. 앱을 클릭합니다.
1. Cloud Services 관리 타일을 찾고 연필을 클릭하여 클라우드 구성을 수정합니다.
1. 알림 구성으로 Amazon SNS 연결, Pushwoosh 연결 또는 Adobe Mobile Services 를 선택합니다.
1. 공급자 속성을 입력하고 제출을 눌러 저장하고 완료 를 클릭합니다. AMS의 경우를 제외하고는 이 단계에서 원격으로 확인되지 않습니다.
1. 이제 Cloud Services 관리 타일에 방금 입력한 구성이 표시됩니다.

### 6단계:앱 {#step-build-and-deploy-the-app} 빌드 및 배포

**참고:** PhoneGap  [](/help/mobile/building-app-mobile-phonegap.md) 애플리케이션 빌드에 대한 지침을 참조하십시오.

PhoneGap를 사용하여 앱을 빌드하고 배포하는 방법에는 두 가지가 있습니다.

**참고:** 푸시 알림 테스트의 경우 푸시 알림은 푸시 공급자(Apple 또는 Google)와 장치 간에 고유한 프로토콜을 사용하기 때문에 에뮬레이터가 충분하지 않습니다. 현재 Mac/PC 하드웨어 및 에뮬레이터는 이를 지원하지 않습니다.

1. *PhoneGap* Builder는 PhoneGap에서 제공하는 서비스로, 서버에서 앱을 빌드하고 이를 장치에 직접 다운로드할 수 있습니다. PhoneGap Build 설정 및 사용 방법에 대해 알아보려면 [PhoneGap Build 설명서](https://build.phonegap.com/)를 참조하십시오.

1. *PhoneGap 명령줄 인터페이스* (CLI)를 사용하면 명령줄에서 풍부한 PhoneGap 명령 세트를 사용하여 앱을 빌드, 디버그 및 배포할 수 있습니다. PhoneGap CLI를 설정하고 사용하는 방법에 대해 알아보려면 [PhoneGap 개발자 설명서](https://docs.phonegap.com/en/edge/guide_cli_index.md.html#The%20Command-Line%20Interface) 를 참조하십시오.

### 7단계:푸시 알림 보내기 {#step-send-a-push-notification}

새 알림을 만들고 전송하려면 다음 단계를 수행합니다.

1. 새 알림 만들기

   * AEM Mobile 앱의 대시보드에서 푸시 알림 타일을 찾습니다.
   * 오른쪽 위의 메뉴에서 &quot;만들기&quot;를 선택합니다. 클라우드 구성이 처음 설정될 때까지 이 단추를 사용할 수 없습니다.
   * 알림 만들기 마법사에서 제목과 메시지를 입력한 다음 &quot;만들기&quot; 단추를 클릭합니다. 이제 알림을 즉시 또는 나중에 보낼 수 있습니다. 편집하고 메시지 및/또는 제목을 변경하거나 저장할 수 있습니다.

1. 알림 보내기

   * 앱 대시보드에서 푸시 알림 타일을 찾습니다.
   * 알림을 선택하거나 오른쪽 하단에 있는 세부 정보 버튼을 클릭합니다(...) 나열됩니다. 이 목록에는 알림을 보낼 준비가 되었는지, 이미 전송되었는지 또는 전송 중에 오류가 발생했는지 여부도 표시됩니다.
   * 한 알림(전용)에 대한 확인란을 선택하고 목록 위에 있는 &quot;알림 보내기&quot; 단추를 클릭합니다. 표시되는 대화 상자에서 알림을 &quot;취소&quot; 또는 &quot;전송&quot;할 수 있습니다.

1. 결과 처리

   * 푸시 알림 서비스(Amazon SNS 또는 Pushwoosh)가 전송 요청을 수신하여 이를 유효한지 확인하고 이를 기본 공급자(APNS 및 GCM)에게 성공적으로 보내면 전송 대화 상자가 메시지가 없는 상태로 닫힙니다. 알림 목록에서 해당 알림의 상태가 전송됨으로 나열됩니다.
   * 푸시 전송이 실패하면 문제를 나타내는 메시지가 대화 상자에 표시됩니다. 알림 목록에서 해당 알림의 상태가 오류로 나열되지만 문제가 수정되면 알림을 다시 전송할 수 있습니다. 오류가 발생하면 서버 오류 로그에 추가 오류 정보가 표시됩니다.
   * 참고: iOS와 Android 푸시 알림 간에는 몇 가지 플랫폼 차이점이 있습니다. 그 중에서:

      * CLI로 빌드하면 Android에 배포된 후 앱이 시작됩니다. iOS에서 수동으로 시작해야 합니다. 푸시 등록 단계는 시작 시 발생하므로 iOS 앱은 시작되지 않지만 Android 앱은 즉시 푸시 알림을 받을 수 있습니다.
      * Android에서 확인 단추 텍스트는 모든 대문자로 표시되지만(및 인앱 알림에 추가된 다른 모든 단추에서) iOS에서는 그렇지 않습니다.

AMS 푸시 알림의 경우 AMS 서버에서 알림을 작성하고 전송해야 합니다. AMS는 AWS 및 Pushwoosh를 통해 AEM 알림에서 제공하는 것 외에도 추가 푸시 알림 기능을 제공합니다.

>[!NOTE]
>
>*푸시 알림이 전달을 보장하지 않습니다.그들은 발표와 더 비슷합니다. 가장 좋은 노력은 모든 사람이 듣도록 하기 위한 것이지만, 그것들은 보장된 배달 메커니즘이 아닙니다. 또한, 푸시 배달 시간은 1초 미만에서 최대 30분까지 달라질 수 있습니다.*

### 푸시 알림과 함께 딥 링크 구성 {#configuring-deep-linking-with-push-notifications}

딥 링크란 무엇입니까? 푸시 알림 컨텍스트에서 앱의 열기 또는 앱 내의 지정된 위치(열려 있는 경우)로 안내할 수 있는 수단입니다.

어떻게 작동합니까? 푸시 알림 작성자는 선택적으로 단추 레이블(즉,&quot;나를 보여!&quot;) 알림 을 선택하고 시각적 경로 브라우저를 통해 알림에 연결할 페이지를 선택합니다. 메시지가 전송되면 인앱 메시지에서 OK 단추가 &quot;해제&quot; 단추로 대체되고 새 단추(&quot;표시!&quot;)가 지정된 경우를 제외하고 푸시가 정상적으로 발생합니다 이 나타납니다. 새 단추를 클릭하면 앱이 앱 내의 지정된 페이지로 이동합니다. 무시 를 클릭하면 메시지가 무시됩니다.

앱이 열려 있지 않으면 음영이 정상적으로 나타납니다. 갓에서 알림에 대해 작업을 수행하면 앱이 열린 다음 푸시 알림에 구성된 내용에 따라 딥 링크 단추를 사용자에게 표시합니다.

알림을 만들고, 선택적 딥 링크에 대한 단추 텍스트와 링크 경로를 추가합니다.

>[!CAUTION]
>
>.대시보드의 푸시 알림 타일에 액세스하려면 아래 단계를 따르십시오.

1. **Cloud Services 관리** 타일의 오른쪽 위 모서리에서 편집을 클릭합니다.

   ![chlimage_1-108](assets/chlimage_1-108.png)

1. **Pushwoosh 연결**&#x200B;을 선택합니다. **다음**&#x200B;을 클릭합니다.

   ![chlimage_1-109](assets/chlimage_1-109.png)

1. 속성의 세부 정보를 입력하고 **제출**&#x200B;을 클릭합니다.

   ![chlimage_1-110](assets/chlimage_1-110.png)

   구성을 제출하면 **푸시 알림** 타일이 대시보드에 표시됩니다.

   ![chlimage_1-111](assets/chlimage_1-111.png)

### 알림 만들기 마법사 {#create-notification-wizard}

대시보드에 **푸시 알림** 타일이 표시되면 알림 만들기 마법사를 사용하여 컨텐츠를 추가합니다.

1. **푸시 알림** 타일의 오른쪽 위 모서리에 있는 추가 기호를 클릭하여 **알림 만들기 마법사**&#x200B;를 엽니다.

   ![chlimage_1-112](assets/chlimage_1-112.png)

1. 링크 경로에서 찾아보기 아이콘을 클릭하면 앱의 컨텐츠 구조가 사용자에게 표시됩니다.

   경로를 선택하면 확인 아이콘을 클릭합니다.

   ![chlimage_1-113](assets/chlimage_1-113.png)

   >[!NOTE]
   >
   >링크 단추 텍스트는 20자로 제한됩니다.
   >
   >최종 사용자에게 최신 버전의 애플리케이션이 없고 연결된 경로를 사용할 수 없는 경우 딥 링크의 작업을 확인하면 사용자가 앱의 기본 페이지로 이동합니다.

1. **알림 만들기 마법사**&#x200B;에 **텍스트 세부 정보**&#x200B;를 입력하고 **만들기**&#x200B;를 클릭합니다.

   ![chlimage_1-114](assets/chlimage_1-114.png)

   **푸시 알림** 타일에서 만든 푸시 알림을 클릭하여 세부 정보를 엽니다.

   속성을 편집하거나, 알림을 보내거나, 알림을 삭제할 수 있습니다.

   ![chlimage_1-115](assets/chlimage_1-115.png)

>[!NOTE]
>
>**추가 정보**:
>
>Pushwoosh 및 Amazon SNS는 6.4 릴리스 이후 지원되지 않으며 패키지 공유에서 추가 기능으로 사용할 수 있습니다.

### 다음 단계 {#the-next-steps}

앱의 푸시 알림에 대한 세부 사항을 이해하면 [AEM Mobile 컨텐츠 개인화](/help/mobile/phonegap-aem-mobile-content-personalization.md)를 참조하십시오.
