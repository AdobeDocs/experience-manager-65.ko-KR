---
title: Facebook 및 Twitter로 소셜 로그인
seo-title: Facebook 및 Twitter로 소셜 로그인
description: 소셜 로그인을 사용하면 사이트 방문자가 Facebook 또는 Twitter 계정으로 로그인할 수 있습니다.
seo-description: 소셜 로그인을 사용하면 사이트 방문자가 Facebook 또는 Twitter 계정으로 로그인할 수 있습니다.
uuid: f70e346e-0d8c-41a0-a100-206a420088dc
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: c0a71870-8f95-40c8-9ffd-b7af49723288
translation-type: tm+mt
source-git-commit: 42606e76742fe7698c4c186208e515ed22adc5a4
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Facebook 및 Twitter로 소셜 로그인 {#social-login-with-facebook-and-twitter}

소셜 로그인은 사이트 방문자에게 Facebook 또는 Twitter 계정으로 로그인하는 옵션을 제공하는 기능입니다. 따라서 AEM 멤버 프로필에 허용되는 Facebook 또는 Twitter 데이터를 포함합니다.

![socialloginweretail](assets/socialloginweretail.png)

## 소셜 로그인 개요 {#social-login-overview}

소셜 로그인을 포함하려면 사용자 지정 Facebook 및 Twitter 애플리케이션을 *만들어야* 합니다.

소매 샘플에서는 샘플 Facebook 및 Twitter 앱과 클라우드 서비스를 제공하지만 [프로덕션 웹 사이트에서는 이용할 수 없습니다](../../help/sites-administering/production-ready.md).

필요한 단계는 다음과 같습니다.

1. [모든 AEM 게시 인스턴스에서](#adobe-granite-oauth-authentication-handler) OAuth 인증을 활성화합니다.

   OAuth를 사용하지 않으면 로그인 시도가 실패합니다.

1. **소셜 앱 및 클라우드 서비스 만들기** .

   * Facebook 로그인을 지원하려면:

      * Facebook [앱](#create-a-facebook-app)만들기
      * Facebook [Connect 클라우드 서비스를 만들고 게시합니다](#create-a-facebook-connect-cloud-service).
   * Twitter에서 로그인을 지원하려면:

      * Twitter [앱](#create-a-twitter-app)만들기
      * Twitter [Connect 클라우드 서비스를 만들고 게시합니다](#create-a-twitter-connect-cloud-service).


1. [**커뮤니티 사이트에** 소셜 로그인](#enable-social-login) 기능을 활성화합니다.

두 가지 기본 개념이 있습니다.

1. **범위** (권한)는 앱이 요청할 수 있는 데이터를 지정합니다.

   * 기본적으로 Facebook 및 Twitter [Adobe [화강암 OAuth 애플리케이션 및 공급자](#adobe-granite-oauth-application-and-provider) 인스턴스]에는 해당 범위 내에 기본 앱 권한이 포함됩니다.

1. **필드** (매개 변수)는 URL 매개 변수를 사용하여 요청한 실제 데이터를 지정합니다.

   * 이 필드는 [AEM Communities Facebook OAuth 공급자](#aem-communities-facebook-oauth-provider) 및 [AEM Communities Twitter OAuth 제공자에 지정됩니다](#aem-communities-twitter-oauth-provider).
   * 기본 필드는 대부분의 사용 사례에는 충분하지만 수정할 수 있습니다.

## Facebook 로그인 {#facebook-login}

### Facebook API 버전 {#facebook-api-version}

Facebook 그래프 API가 버전 1.0일 때 소셜 로그인 및 소매 Facebook 샘플이 개발되었습니다. AEM 6.4 GA 및 AEM 6.3 SP1 소셜 로그인이 최신 Facebook 그래프 API 2.5 버전에서 작동하도록 업데이트되었습니다.

>[!NOTE]
>
>이전 AEM 버전의 경우 로그에서 예외가 발생하면 **이**&#x200B;버전에서 토큰을 추출할 수 없으면 해당 AEM 릴리스에 대한 최신 CFP로 업그레이드하십시오.


Facebook 그래프 API 버전 정보는 [Facebook API 변경 로그를 참조하십시오](https://developers.facebook.com/docs/apps/changelog).

### Facebook 앱 만들기 {#create-a-facebook-app}

Facebook 소셜 로그인을 사용하려면 올바르게 구성된 Facebook 애플리케이션이 필요합니다.

Facebook 애플리케이션을 만들려면 https://developers.facebook.com/apps/에서 Facebook의 지침을 [따릅니다](https://developers.facebook.com/apps/). 지침에 대한 변경 사항은 다음 정보에 반영되지 않습니다.

일반적으로 Facebook API v2.7의 경우:

* *새 Facebook 앱 추가*
   * 플랫폼 *의 경우 웹 사이트*:
      * 사이트 *URL에*&#x200B;대해 `  https://<server>:<port>.`
      * 표시 *이름*&#x200B;에 Facebook Connect 서비스의 제목으로 사용할 제목을 입력합니다.
      * 카테고리 *의 경우*&#x200B;페이지용 *앱*&#x200B;선택을 권장합니다.
      * *제품 추가: Facebook 로그인*
      * 유효한 *OAuth 리디렉션 URI에*&#x200B;대해 `  https://<server>:<port>.`

>[!NOTE]
>
>개발을 위해 http://localhost:4503이 작동합니다.


응용 프로그램이 만들어지면 **[!UICONTROL 앱 ID]** 및 **[!UICONTROL 앱 암호]** 설정을 찾습니다. 이 정보는 [Facebook 클라우드 서비스를 구성하는 데 필요합니다](#createafacebookcloudservice).

### Facebook Connect Cloud Service 만들기 {#create-a-facebook-connect-cloud-service}

클라우드 서비스 구성을 만들어 인스턴스화된 [ [Adobe [OAuth 응용 프로그램 및 공급자](#adobe-granite-oauth-application-and-provider) ] 인스턴스는 Facebook 응용 프로그램 및 새 사용자가 추가된 멤버 그룹을 식별합니다.

1. AEM 작성자 인스턴스에서 관리자 권한으로 로그인합니다.
1. 전역 탐색에서 **[!UICONTROL 도구]** > Cloud Services **[!UICONTROL >]** Facebook **[!UICONTROL Social 로그인 구성을 선택합니다]**.
1. 구성 **[!UICONTROL 컨텍스트 경로를 선택합니다]**.

   **[!UICONTROL 컨텍스트 경로는]** 커뮤니티 사이트를 만들고 편집하는 동안 선택한 클라우드 구성 경로와 동일해야 합니다.

1. 컨텍스트 경로가 클라우드 서비스를 만들 수 있는지 확인합니다.
1. 도구 **[!UICONTROL >]** 일반 ******[!UICONTROL >]**&#x200B;구성 브라우저로 이동합니다. 컨텍스트를 선택하고 속성을 편집합니다. 아직 활성화되지 않은 경우 클라우드 구성을 활성화합니다.

   ![config-properties](assets/config-propertiespng.png)

1. **Facebook 클라우드 서비스 구성 만들기/** 편집을 참조하십시오.

   ![fbsocialloginconfigpng](assets/fbsocialloginconfigpng.png)

   * **[!UICONTROL 제목]** (*필수*) Facebook 앱을 식별하는 표시 제목을 입력합니다. Facebook 앱에 대해 *표시 이름과* 동일한 이름을 사용하는 것이 좋습니다.
   * **[!UICONTROL 앱 ID/API 키]** (*필수****) Facebook 앱에*** 대한 앱 ID를입력합니다. 대화 상자에서 만든 [Adobe [OAuth 응용 프로그램 및 공급자](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#AdobeGraniteOAuthApplicationandProvider) 인스턴스]를 식별합니다.
   * **[!UICONTROL 앱 암호]** (*필수****)*** Facebook 앱에 대한앱암호를 입력합니다.
   * **[!UICONTROL 사용자]** 만들기 이 확인란을 선택하면 Facebook 계정으로 로그인하면 AEM 사용자 항목이 만들어지고 선택한 사용자 그룹에 구성원으로 추가됩니다.  기본값이 선택됨(적극 권장)
   * **[!UICONTROL 마스크 사용자 ID]**:선택 해제한 상태로 둡니다.
   * **[!UICONTROL 범위 이메일]**:사용자의 이메일 ID를 Facebook에서 가져와야 합니다.
   * **[!UICONTROL 사용자 그룹에]** 추가를 선택하여 사용자를 추가할 커뮤니티 사이트에 대해 하나 이상의 [구성원 그룹을](https://helpx.adobe.com/experience-manager/6-3/communities/using/users.html) 선택합니다.

   >[!NOTE]
   >
   >그룹은 언제든지 추가하거나 제거할 수 있습니다. 그러나 기존 사용자의 멤버십은 영향을 받지 않습니다. 자동 멤버십은 이 필드 업데이트 이후 만들어지는 새 사용자에게만 적용됩니다. 익명 사용자가 비활성화된 사이트의 경우, 폐쇄된 커뮤니티 사이트에 대한 해당 커뮤니티 구성원 그룹에 사용자를 추가하도록 선택합니다.

   * Select **[!UICONTROL SAVE]**.
   * **[!UICONTROL 게시]**.




그 결과는 추가 범위(권한)를 추가하지 않는 한 더 이상 수정할 필요가 없는 [Adobe [OAuth 응용 프로그램 및 공급자](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#adobe-granite-oauth-application-and-provider) 인스턴스입니다. 기본 범위는 Facebook 로그인에 대한 표준 권한입니다. 추가 범위를 원하는 경우 OSGI 구성을 직접 편집해야 합니다. 시스템/콘솔을 통해 직접 수정하는 경우 터치 UI에서 클라우드 서비스 구성을 편집하지 않아도 덮어쓰지 않습니다.

### AEM Communities Facebook OAuth 공급자 {#aem-communities-facebook-oauth-provider}

AEM Communities 공급자가 [ [Adobe [Granite OAuth 응용 프로그램 및 공급자] 인스턴스를](#adobe-granite-oauth-application-and-provider) 확장합니다.

이 공급자를 편집하려면 다음이 필요합니다.

* 사용자 업데이트 허용
* 범위 [내에 필드 추가](#adobe-granite-oauth-application-and-provider)

   * 기본적으로 허용되는 모든 필드가 포함된 것은 아닙니다.

편집이 필요한 경우 각 AEM 게시 인스턴스에서 다음을 수행합니다.

1. 관리자 권한으로 로그인합니다.
1. 웹 [콘솔로 이동합니다](../../help/sites-deploying/configuring-osgi.md). 예: http://localhost:4503/system/console/configMgr.
1. AEM Communities Facebook OAuth 공급자를 찾습니다.
1. 편집할 연필 아이콘을 선택합니다.

   ![fboauthprov_png](assets/fboauthprov_png.png)

   * **[!UICONTROL OAuth 공급자 ID]**

      (*필수*) 기본값은 *soco -facebook*&#x200B;입니다. 편집하지 마십시오.

   * **[!UICONTROL Cloud Service 구성]**

      Default value is `/etc/  cloudservices /  facebookconnect`. 편집하지 마십시오.

   * **[!UICONTROL OAuth 공급자 서비스 구성]**

      Default value is `/apps/social/facebookprovider/config/`. 편집하지 마십시오.

   * **[!UICONTROL 태그 사용]**

      편집하지 마십시오.

   * **[!UICONTROL 사용자 경로]**

      사용자 데이터가 저장되는 저장소의 위치입니다. 커뮤니티 사이트에서 구성원이 다른 사람의 프로필을 볼 수 있는 권한을 보장하기 위해 경로는 기본 */홈/사용자/커뮤니티여야 합니다*.

   * **[!UICONTROL 필드 활성화]**

      이 확인란을 선택하면 나열된 필드가 사용자 인증 및 정보를 위해 Facebook 요청에 지정됩니다. 기본값은 선택 취소입니다.

   * **[!UICONTROL 필드]**

      필드가 활성화되어 있으면 Facebook 그래프 API를 호출할 때 다음 필드가 포함됩니다. 클라우드 서비스 구성에 정의된 범위 내에서 필드를 허용해야 합니다. 추가 필드에는 Facebook의 승인이 필요할 수 있습니다. Facebook 설명서의 Facebook 로그인 권한 섹션을 참조하십시오. 매개 변수로 추가된 기본 필드는 다음과 같습니다.

      * id
      * 이름
      * first_name
      * last_name
      * link
      * 로케일
      * 사진
      * timezone
      * updated_time
      * 확인됨
      * 이메일

   필드가 추가되거나 변경된 경우 해당 기본 동기화 처리기 구성을 업데이트하여 매핑을 수정하십시오.

   * **[!UICONTROL 사용자 업데이트]**

      이 확인란을 선택하면 프로필 변경 사항이나 요청된 추가 데이터를 반영하도록 각 로그인 시 저장소의 사용자 데이터를 새로 고칩니다. 기본값은 선택 취소입니다.


#### 다음 단계 {#next-steps}

다음 단계는 Facebook과 Twitter 모두에 동일합니다.

* [클라우드 서비스 구성 게시](#publishcloudservices)
* [커뮤니티 사이트 활성화](#enable-social-login)

## Twitter 로그인 {#twitter-login}

### Twitter 앱 만들기 {#create-a-twitter-app}

Twitter 소셜 로그인을 활성화하려면 구성된 Twitter 애플리케이션이 필요합니다.

최신 지침에 따라 https://apps.twitter.com에서 새 Twitter 응용 프로그램을 [만듭니다](https://apps.twitter.com/).

일반적으로:

1. 웹 사이트 사용자에게 Twitter *애플리케이션을* 식별할 이름을 입력합니다.
1. Enter a *Description*.
1. 웹 *사이트* - 를 입력합니다 `https://<server>`.
1. 콜백 *URL의 경우* - 를 `https://server`입력합니다.

   >[!NOTE]
   >
   >포트를 지정할 필요는 없습니다.
   >
   >개발을 위해 https://127.0.0.1/이 작동합니다.

1. 애플리케이션이 만들어지면 **[!UICONTROL 소비자(API) 키]** 및 **[!UICONTROL 소비자(API) 암호를 찾습니다]**. 이 정보는 [Twitter 클라우드 서비스를 구성하는 데 필요합니다](#createatwittercloudservice).

#### 권한 {#permissions}

Twitter 애플리케이션 관리의 권한 섹션에서 다음을 수행합니다.

* **[!UICONTROL 액세스]**:선택합니다 `Read only`.

   * 다른 옵션은 지원되지 않습니다.

* **[!UICONTROL 추가 권한]**:원하는 경우 선택합니다 `Request email addresses from users`.

   * 선택하지 않으면 AEM의 사용자 프로필에 이메일 주소가 포함되지 않습니다.
   * Twitter의 지침에 따라 수행해야 할 추가 단계가 나와 있습니다.

소셜 로그인에 대한 REST 요청은 계정 *[GET/자격 증명 확인에만 있습니다](https://dev.twitter.com/rest/reference/get/account/verify_credentials)*.

### Twitter Connect Cloud Service 만들기 {#create-a-twitter-connect-cloud-service}

클라우드 서비스 구성을 만들어 인스턴스화된 [ [Adobe [OAuth 응용 프로그램 및 공급자](#adobe-granite-oauth-application-and-provider) ] 인스턴스는 Twitter 응용 프로그램과 새 사용자가 추가된 멤버 그룹을 식별합니다.

1. 작성자 인스턴스에서 관리자 권한으로 로그인합니다.
1. 전역 탐색에서 **[!UICONTROL 도구]** > Cloud Services **[!UICONTROL >]** Twitter 소셜 로그인 구성을 선택합니다 ****.
1. 컨텍스트 **[!UICONTROL 경로]** 구성을 선택합니다.

   컨텍스트 경로는 커뮤니티 사이트를 만들고 편집하는 동안 선택한 클라우드 구성 경로와 동일해야 합니다.

1. 컨텍스트 경로가 클라우드 서비스를 만들 수 있는지 확인합니다.
1. 도구 **[!UICONTROL >]** 일반 ******[!UICONTROL >]**&#x200B;구성 브라우저로 이동합니다. 컨텍스트를 선택하고 속성을 편집합니다. 아직 활성화되지 않은 경우 클라우드 구성을 활성화합니다.

   ![twitterconfigpropping](assets/twitterconfigproppng.png)

1. Twitter 클라우드 서비스 구성 만들기/편집을 참조하십시오.

   ![twittersocialloginpng](assets/twittersocialloginpng.png)

   * **[!UICONTROL 제목]**

      (*필수*) Twitter 앱을 식별하는 표시 제목을 입력합니다. Twitter 앱에 대해 *표시 이름과* 동일한 이름을 사용하는 것이 좋습니다.

   * **[!UICONTROL 소비자 키]**

      (*필수***) Twitter 앱용** 소비자(API) 키를입력합니다. 대화 상자에서 만든 [Adobe [OAuth 응용 프로그램 및 공급자](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#AdobeGraniteOAuthApplicationandProvider) 인스턴스]를 식별합니다.

   * **[!UICONTROL 소비자 암호]**

      (*필수****) Twitter 앱용*** 소비자(API) 암호를입력합니다.

   * **[!UICONTROL 사용자 만들기]**

      이 확인란을 선택하면 Twitter 계정으로 로그인하여 AEM 사용자 항목을 만들고 선택한 사용자 그룹에 구성원으로 추가합니다. 기본값이 선택됨(적극 권장)

   * **[!UICONTROL 사용자 ID 마스크]**

      선택 해제한 상태로 둡니다.

   * **[!UICONTROL 사용자 그룹에 추가]**

      사용자 그룹 추가를 선택하여 사용자를 추가할 커뮤니티 사이트에 대해 하나 이상의 [구성원 그룹을](https://helpx.adobe.com/experience-manager/6-3/communities/using/users.html) 선택합니다.
   >[!NOTE]
   >
   >그룹은 언제든지 추가하거나 제거할 수 있습니다. 그러나 기존 사용자의 멤버십은 영향을 받지 않습니다. 자동 멤버십은 이 필드 업데이트 이후 만들어지는 새 사용자에게만 적용됩니다. 익명 사용자가 비활성화된 사이트의 경우 해당 폐쇄된 커뮤니티 사이트에 대한 해당 커뮤니티 구성원 그룹에 사용자를 추가합니다.

1. 저장 **[!UICONTROL 및 게시]** 를 **[!UICONTROL 선택합니다]**.

그 결과 추가 수정이 필요하지 않은 [ [Adobe [OAuth 응용 프로그램 및 공급자](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#adobe-granite-oauth-application-and-provider) 인스턴스]가 됩니다. 기본 범위는 Twitter 로그인에 대한 표준 권한입니다.

### AEM Communities Twitter OAuth Provider {#aem-communities-twitter-oauth-provider}

AEM Communities 구성은 [ [Adobe [Granite OAuth 응용 프로그램 및 Provider] 인스턴스를](#adobe-granite-oauth-application-and-provider) 확장합니다. 이 공급자는 사용자 업데이트를 허용하기 위해 편집이 필요합니다.

편집이 필요한 경우 각 AEM 게시 인스턴스에서 다음을 수행합니다.

1. 관리자 권한으로 로그인합니다.
1. 웹 [콘솔로 이동합니다](../../help/sites-deploying/configuring-osgi.md).

   예: http://localhost:4503/system/console/configMgr.

1. AEM Communities Twitter OAuth 공급자를 찾습니다.
1. 편집할 연필 아이콘을 선택합니다.

   ![twitteroauth_png](assets/twitteroauth_png.png)

   * **[!UICONTROL OAuth 공급자 ID]**

   (*필수*) 기본값은 *soco -twitter입니다*. 편집하지 마십시오.

   * **[!UICONTROL Cloud Service 구성]**

      The default value is *conf.* 편집하지 마십시오.

   * **[!UICONTROL OAuth 공급자 서비스 구성]**

      The default value is `/apps/social/twitterprovider/config/`. 편집하지 마십시오.

   * **[!UICONTROL 사용자 경로]**

      사용자 데이터가 저장되는 저장소의 위치입니다. 커뮤니티 사이트에서 구성원이 다른 사람의 프로필을 볼 수 있는 권한을 보장하기 위해 경로가 기본이어야 합니다 `/home/users/community`.

   * **[!UICONTROL 매개 변수]** 편집 안 함
   * **[!UICONTROL URL 매개]** 변수가 편집되지 않음
   * **[!UICONTROL 사용자 업데이트]**

      이 확인란을 선택하면 프로필 변경 사항이나 요청된 추가 데이터를 반영하도록 각 로그인 시 저장소의 사용자 데이터를 새로 고칩니다. 기본값은 선택 취소입니다.


#### 다음 단계 {#next-steps-1}

다음 단계는 Facebook과 Twitter 모두에 동일합니다.

* [클라우드 서비스 구성 게시](#publishcloudservices)
* [커뮤니티 사이트 활성화](#enable-social-login)

## 소셜 로그인 활성화 {#enable-social-login}

### AEM Communities 사이트 콘솔 {#aem-communities-sites-console}

클라우드 서비스가 구성되면 커뮤니티 사이트 [생성](https://helpx.adobe.com/experience-manager/6-3/communities/using/sites-console.html#USERMANAGEMENT) 또는 [관리](https://helpx.adobe.com/experience-manager/6-3/communities/using/sites-console.html#SiteCreation) 중에 사용자 관리 [설정 하위 패널을 사용하여 커뮤니티 사이트에 대한 관련 소셜 로그인 설정이 활성화될 수 있습니다](https://helpx.adobe.com/experience-manager/6-3/communities/using/sites-console.html#ModifyingSiteProperties).

1. 소셜 로그인 구성을 저장한 사이트 구성 컨텍스트를 선택합니다.

1. 일반 탭에서 클라우드 구성을 설정합니다.

   ![managessites_png](assets/managesites_png.png)

1. 설정 탭에서 **[!UICONTROL 소셜 로그인]** 및 저장을 활성화합니다.

   ![usermgmt_png](assets/usermgmt_png.png)

## 소셜 로그인 테스트 {#test-social-login}

* 모든 게시 인스턴스에서 [ [Adobe [OAuth 인증 처리기](#adobe-granite-oauth-authentication-handler) ]가 활성화되어 있는지 확인합니다.
* 클라우드 서비스가 게시되었는지 확인합니다.
* 커뮤니티 사이트가 게시되었는지 확인합니다.
* 브라우저에서 게시된 사이트를 실행합니다.
예: http://localhost:4503/content/sites/engage/en.html
* 로그인 **[!UICONTROL 을 선택합니다]**.
* Facebook **[!UICONTROL 으로 로그인]** 또는 Twitter로 **[!UICONTROL 로그인을 선택합니다]**.
* Facebook 또는 Twitter에 아직 로그인하지 않은 경우 해당 자격 증명으로 로그인합니다.
* Facebook 또는 Twitter 앱에서 표시되는 대화 상자에 따라 권한을 부여해야 할 수 있습니다.
* 페이지 상단의 도구 모음이 성공적인 로그인을 반영하도록 업데이트됩니다.
* 프로필 **[!UICONTROL 선택]**:프로필 페이지에는 사용자의 아바타 이미지, 이름 및 성이 표시됩니다. 또한 허용된 필드/매개 변수에 따라 Facebook 또는 Twitter 프로필의 정보도 표시합니다.

## AEM 플랫폼 OAuth 구성 {#aem-platform-oauth-configurations}

### Adobe Granite OAuth 인증 처리기 {#adobe-granite-oauth-authentication-handler}

이 `Adobe Granite OAuth Authentication Handler` 는 기본적으로 활성화되지 않으며 모든 AEM 게시 인스턴스에서 활성화되어야 ***합니다.***

게시 시 인증 핸들러를 활성화하려면 OSGi 구성을 열고 저장하면 됩니다.

* 관리자 권한으로 로그인합니다.
* 웹 [콘솔로 이동합니다](../../help/sites-deploying/configuring-osgi.md).
예: http://localhost:4503/system/console/configMgr
* 위치 `Adobe Granite OAuth Authentication Handler`확인
* 편집할 구성을 열려면 선택합니다.
* **[!UICONTROL 저장]**&#x200B;을 선택합니다.

![chlimage_1-489](assets/chlimage_1-489.png)

>[!CAUTION]
>
>인증 핸들러를 Granite OAuth 응용 프로그램 및 공급자의 Facebook 또는 Twitter 인스턴스와 *혼동하지 않도록 주의하십시오*.


![chlimage_1-490](assets/chlimage_1-490.png)

### Adobe Granite OAuth 응용 프로그램 및 공급자 {#adobe-granite-oauth-application-and-provider}

Facebook 또는 Twitter에 대한 클라우드 서비스가 만들어지면 인스턴스 `Adobe Granite OAuth Authentication Handler` 가 만들어집니다.

Facebook 또는 Twitter 앱에 대해 생성된 인스턴스를 찾으려면 다음을 수행하십시오.

1. 관리자 권한으로 로그인합니다.
1. 웹 [콘솔로 이동합니다](../../help/sites-deploying/configuring-osgi.md).

   예: http://localhost:4503/system/console/configMgr.

1. [MOCK] Locate Adobe Granite OAuth Application and Provider.

   * 클라이언트 ID가 **[!UICONTROL 앱 ID와]** 일치하는 인스턴스를 **[!UICONTROL 찾습니다]**.

      ![chlimage_1-491](assets/chlimage_1-491.png)

      다음 속성을 제외하고 구성의 다른 속성은 변경하지 않은 상태로 둡니다.

   * **[!UICONTROL 구성 ID]**

      (*필수*) OAuth 구성 ID는 고유해야 합니다. 클라우드 서비스가 만들어지면 자동으로 생성됩니다.

   * **[!UICONTROL 클라이언트 ID]**

      (*필수*) 클라우드 서비스를 만들 때 제공된 응용 프로그램 ID입니다.

   * **[!UICONTROL 클라이언트 암호]**

      (*필수*) 클라우드 서비스가 생성될 때 제공된 응용 프로그램 암호입니다.

   * **[!UICONTROL 범위]**

      (*선택*&#x200B;사항) 제공자로부터 허용된 내용에 대한 추가 범위를 요청할 수 있습니다. 기본 범위에서는 소셜 인증 및 프로필 데이터를 제공하는 데 필요한 권한을 다룹니다.

   * **[!UICONTROL 공급자 ID]**

      (*필수*) 클라우드 서비스를 만들 때 AEM Communities의 공급자 ID가 설정됩니다. 편집하지 마십시오. Facebook Connect의 경우 값은 *soco -facebook입니다*. Twitter Connect의 경우 값은 *soco-twitter입니다*.

   * **[!UICONTROL 그룹]**

      (*권장*) 만들어진 사용자가 추가된 하나 이상의 구성원 그룹이 있습니다. AEM Communities의 경우 커뮤니티 사이트의 구성원 그룹을 나열하는 것이 좋습니다.

   * **[!UICONTROL 콜백 URL]**

      (*선택*&#x200B;사항) 클라이언트를 다시 리디렉션하도록 OAuth 공급자로 구성된 URL. 원본 요청의 호스트를 사용하려면 상대 url을 사용합니다. 원래 요청된 URL을 대신 사용하려면 비워 두십시오. 접미사 &quot;/callback/j_security_check&quot;가 이 url에 자동으로 추가됩니다.
   >[!NOTE]
   >
   >콜백의 도메인은 공급자에게 등록되어야 합니다(Facebook 또는 Twitter).

각 OAuth 인증 핸들러 구성에 대해 인스턴스에 두 개의 추가 구성이 있습니다.

* Apache Jackrabbit Oak 기본 동기화 처리기(org.apache.jackrabbit.oak.security.authentication.external.impl.DefaultSyncHandler) - 편집할 필요가 없지만 Facebook 필드가 CQ 사용자 프로필 노드에 매핑되는 방법을 사용자 필드 매핑을 볼 수 있습니다. 또한 &#39;Sync 처리기 이름&#39;이 OAuth 공급자 구성의 구성 ID와 일치하는지 확인합니다.
* Apache Jackrabbit Oak 외부 로그인 모듈(org.apache.jackrabbit.oak.security.authentication.external.impl.ExternalLoginModuleFactory) - 편집할 필요가 없지만, &#39;ID 공급자 이름&#39; 및 &#39;Sync 처리기 이름&#39;이 각각 해당 OAuth 및 동기화 처리기 구성을 가리키는 것을 알 수 있습니다.

자세한 내용은 Apache [Oak 외부 로그인 모듈로 인증을 참조하십시오](https://jackrabbit.apache.org/oak/docs/security/authentication/externalloginmodule.html).

## OAuth 사용자 트래버스 성능 {#oauth-user-traversal-performance}

수십만 명의 사용자가 Facebook 또는 Twitter 로그인을 사용하여 등록하는 커뮤니티 사이트의 경우 사이트 방문자가 소셜 로그인을 사용할 때 수행되는 쿼리의 통과적 성능을 다음 Oak 색인을 추가하여 향상시킬 수 있습니다.

로그에 트래픽 경고가 표시되면 이 인덱스를 추가하는 것이 좋습니다.

작성자 인스턴스에서 관리자 권한으로 로그인됨:

1. 전역 탐색에서:도구, **CRX/[DE Lite를 선택합니다](../../help/sites-developing/developing-with-crxde-lite.md).**
1. ntBaseLucene 사본에 ntBaseLucene-oauth라는 이름의 인덱스를 만듭니다.

   * Under node `/oak:index`
   * 노드 선택 `ntBaseLucene`
   * 복사 **[!UICONTROL 선택]**
   * 선택 `/oak:index`
   * 붙여넣기 **[!UICONTROL 선택]**
   * ntBaseLucene의 복사본 이름을 `ntBaseLucene-oauth`

1. 노드 ntBaseLucene-oauth의 속성을 수정합니다.

   * **[!UICONTROL indexPath]**: `/oak:index/ntBaseLucene-oauth`
   * **[!UICONTROL 이름]**: `oauthid-123****`
   * **[!UICONTROL 다시 색인]**: `true`
   * **[!UICONTROL reindexCount]**: `1`

1. /oak:index/ntBaseLucene-oauth/indexRules/nt:base/properties:

   * cqTags를 제외한 모든 하위 노드를 삭제합니다.
   * cqTags의 이름을 `oauthid-123****`
   * 노드의 속성 수정 `oauthid-123****`

      * **[!UICONTROL 이름]**: `oauthid-123****`
   * 모두 **[!UICONTROL 저장을 선택합니다]**.


* 이름 **의** 경우, Facebook `oauthid-123`ID *또는 Twitter ID Consumer(API)와* 함께 ***123*** 이 ****** **** [](social-login.md#adobe-granite-oauth-application-and-provider) 있습니다. 키API는 [GRANITE DOMAINuth 응용 프로그램 및 Provider]에 있는 Twitter 응용 프로그램 ID의 값입니다.

   ![chlimage_1-492](assets/chlimage_1-492.png)

자세한 내용 및 도구는 [Oak 쿼리 및 색인을 참조하십시오](../../help/sites-deploying/queries-and-indexing.md).

## Dispatcher Configuration {#dispatcher-configuration}

커뮤니티에 [대한 발송자 구성을 참조하십시오](dispatcher.md).
