---
title: Facebook 및 Twitter를 사용한 소셜 로그인
seo-title: Facebook 및 Twitter를 사용한 소셜 로그인
description: Social 로그인을 사용하면 사이트 방문자가 Facebook 또는 Twitter 계정으로 로그인할 수 있습니다.
seo-description: Social 로그인을 사용하면 사이트 방문자가 Facebook 또는 Twitter 계정으로 로그인할 수 있습니다.
uuid: f70e346e-0d8c-41a0-a100-206a420088dc
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: c0a71870-8f95-40c8-9ffd-b7af49723288
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Facebook 및 Twitter를 사용한 소셜 로그인 {#social-login-with-facebook-and-twitter}

Social 로그인은 사이트 방문자에게 Facebook 또는 Twitter 계정으로 로그인하는 옵션을 제공하는 기능입니다. 따라서 AEM 멤버 프로필에 허용되는 Facebook 또는 Twitter 데이터를 포함합니다.

![socialloginweretail](assets/socialloginweretail.png)

## 소셜 로그인 개요 {#social-login-overview}

소셜 로그인을 포함하려면 *필수 *로 사용자 정의 Facebook 및 Twitter 애플리케이션을 만듭니다.

Adobe 소매 샘플에서는 샘플 Facebook 및 Twitter 앱과 클라우드 서비스를 제공하지만 [프로덕션 웹 사이트에서는](../../help/sites-administering/production-ready.md)제공되지 않습니다.

필요한 단계는 다음과 같습니다.

1. [모든 AEM 게시 인스턴스에서 OAuth 인증을](#adobe-granite-oauth-authentication-handler) 활성화합니다.

   OAuth를 사용하지 않으면 로그인 시도가 실패합니다.

1. **소셜 앱** 및 클라우드 서비스 만들기

   * Facebook에서 로그인을 지원하려면:

      * Facebook [앱을](#create-a-facebook-app)만듭니다.
      * Facebook Connect 클라우드 [서비스를](#create-a-facebook-connect-cloud-service)만들고 게시합니다.
   * Twitter로 로그인을 지원하려면:

      * Twitter [앱을](#create-a-twitter-app)만듭니다.
      * Twitter Connect 클라우드 [서비스를](#create-a-twitter-connect-cloud-service)만들고 게시합니다.


1. [**커뮤니티 사이트에 대한 소셜 로그인을&#x200B;**활성화합니다](#enable-social-login).

두 가지 기본 개념이 있습니다.

1. **범위** (권한)는 앱이 요청할 수 있는 데이터를 지정합니다.

   * Facebook 및 Twitter [Adobe Granite OAuth 애플리케이션 및](#adobe-granite-oauth-application-and-provider) Provider 인스턴스는 기본적으로 범위 내에 기본 앱 권한을 포함합니다.

1. **필드** (매개 변수)는 URL 매개 변수를 사용하여 요청한 실제 데이터를 지정합니다.

   * 이러한 필드는 AEM Communities Facebook [OAuth 공급자](#aem-communities-facebook-oauth-provider) 및 AEM Communities [Twitter OAuth 공급자에 지정됩니다](#aem-communities-twitter-oauth-provider).
   * 기본 필드는 대부분의 사용 사례에서 충분하지만 수정할 수 있습니다.

## Facebook 로그인 {#facebook-login}

### Facebook API 버전 {#facebook-api-version}

Facebook 그래프 API가 버전 1.0일 때 소셜 로그인 및 소매 Facebook 샘플이 개발되었습니다.AEM 6.4 GA 및 AEM 6.3 SP1 소셜 로그인이 최신 Facebook 그래프 API 2.5 버전에서 작동하도록 업데이트되었습니다.

>[!NOTE]
>
>이전 AEM 버전의 경우 로그에서 예외가 발생하면 **이 버전에서 토큰을 추출할 수 없는 경우 **해당 AEM 릴리스에 대한 최신 CFP로 업그레이드하십시오.

Facebook 그래프 API 버전 정보는 Facebook API [변경 로그를 참조하십시오](https://developers.facebook.com/docs/apps/changelog).

### Facebook 앱 만들기 {#create-a-facebook-app}

Facebook 소셜 로그인을 활성화하려면 적절하게 구성된 Facebook 애플리케이션이 필요합니다.

Facebook 애플리케이션을 만들려면 https://developers.facebook.com/apps/에서 Facebook의 지침을 [따르십시오](https://developers.facebook.com/apps/). 지침에 대한 변경 사항은 다음 정보에 반영되지 않습니다.

일반적으로 Facebook API v2.7의 경우:

* *새 Facebook 앱 추가:*
   * 플랫폼의 *경우*&#x200B;웹 사이트를 선택합니다.
      * 사이트 *URL의*&#x200B;경우 `  https://<server>:<port>.`
   * 표시 *이름에* Facebook Connect 서비스의 제목으로 사용할 제목을 입력합니다.
   * 카테고리의 *경우*&#x200B;페이지용 *앱을 선택하는 것이 좋지만,* 무엇이든 될 수 있습니다.
   * *제품 추가: Facebook 로그인*
      * 유효한 *OAuth 리디렉션 URI의*&#x200B;경우 `  https://<server>:<port>.`

>[!NOTE]
>
>개발을 위해 http://localhost:4503이 작동합니다.

애플리케이션이 만들어지면 앱 ID 및 **[!UICONTROL 앱]** 암호 **[!UICONTROL 설정을]** 찾습니다. 이 정보는 Facebook 클라우드 서비스를 구성하는 데 [필요합니다](#createafacebookcloudservice).

### Facebook Connect Cloud 서비스 만들기 {#create-a-facebook-connect-cloud-service}

클라우드 서비스 [구성을](https://chl-author.corp.adobe.com/content/help/en/experience-manager/6-4/communities/using/social-login.html#AdobeGraniteOAuthApplicationandProvider) 만들어 인스턴스화된 Adobe Granite OAuth 응용 프로그램 및 Provider 인스턴스는 Facebook 응용 프로그램과 새 사용자가 추가되는 멤버 그룹을 식별합니다.

1. AEM 작성자 인스턴스에서 관리자 권한으로 로그인합니다.
1. 글로벌 탐색에서 도구 > 클라우드 **[!UICONTROL 서비스 > Facebook Social 로그인 구성을]**&#x200B;선택합니다.
1. 구성 **[!UICONTROL 컨텍스트 경로를]**&#x200B;선택합니다.

   **[!UICONTROL 컨텍스트 경로는]** 커뮤니티 사이트를 만들거나 편집할 때 선택한 클라우드 구성 경로와 같아야 합니다.

1. 컨텍스트 경로에서 클라우드 서비스를 만들 수 있는지 확인합니다.
1. 도구 > **[!UICONTROL 일반 > 구성 브라우저로 이동합니다]**. 컨텍스트를 선택하고 속성을 편집합니다. 아직 활성화되지 않은 경우 클라우드 구성을 활성화합니다.

   ![config-propertisping](assets/config-propertiespng.png)

1. Facebook 클라우드 서비스 구성 만들기/편집을 참조하십시오.

   ![fbsocialloginconfigpng](assets/fbsocialloginconfigpng.png)

   * **[!UICONTROL 제목]** (*필수*) Facebook 앱을 식별하는 표시 제목을 입력합니다. Facebook 앱의 표시 이름으로 입력한 동일한 *이름을 사용하는* 것이 좋습니다.
   * **[!UICONTROL 앱 ID/API 키]** (*필수*) Facebook ***앱용 앱*** ID를입력합니다. 대화 상자에서 [만든 Adobe Granite OAuth 응용 프로그램 및](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#AdobeGraniteOAuthApplicationandProvider) 공급자 인스턴스를 식별합니다.
   * **[!UICONTROL 앱 암호]** (*필수*)Facebook ***앱용 앱*** 암호를 입력합니다.
   * **[!UICONTROL 사용자]** 만들기 이 확인란을 선택하면 Facebook 계정으로 로그인하여 AEM 사용자 항목을 만들고 선택한 사용자 그룹에 멤버로 추가합니다.  기본값은 선택됨(적극 권장).
   * **[!UICONTROL 마스크 사용자 ID]**:선택 해제한 상태로 둡니다.
   * **[!UICONTROL 범위 이메일]**:사용자의 이메일 ID를 Facebook에서 가져와야 합니다.
   * **[!UICONTROL 사용자 그룹에]** 추가를 선택하여 사용자가 추가될 커뮤니티 사이트에 대해 하나 이상의 [구성원 그룹을](https://helpx.adobe.com/experience-manager/6-3/communities/using/users.html) 선택합니다.
   >[!NOTE]
   >
   >그룹은 언제든지 추가하거나 제거할 수 있습니다. 그러나 기존 사용자의 멤버십은 영향을 받지 않습니다. 자동 멤버십은 이 필드 업데이트를 게시하는 새 사용자에게만 적용됩니다. 익명 사용자가 비활성화된 사이트의 경우 해당 폐쇄된 커뮤니티 사이트에 대한 해당 커뮤니티 구성원 그룹에 사용자를 추가하도록 선택합니다.

   * Select **[!UICONTROL SAVE]**.
   * **[!UICONTROL 게시]**.



그 결과 Adobe Granite [OAuth 응용 프로그램 및](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#adobe-granite-oauth-application-and-provider) Provider 인스턴스가 생성되며, 이 인스턴스는 추가 범위(권한)를 추가하지 않는 한 더 이상 수정할 필요가 없습니다. 기본 범위는 Facebook 로그인에 대한 표준 권한입니다. 추가 범위를 원하는 경우 OSGI 구성을 직접 편집해야 합니다. 시스템/콘솔을 통해 직접 수정하는 경우 덮어쓰지 않도록 터치 UI에서 클라우드 서비스 구성을 편집하지 마십시오.

### AEM Communities Facebook OAuth 공급자 {#aem-communities-facebook-oauth-provider}

AEM Communities 공급자는 Adobe Granite OAuth 응용 [프로그램 및 공급자 인스턴스를 확장합니다](#adobe-granite-oauth-application-and-provider) .

이 공급자를 편집하려면 다음이 필요합니다.

* 사용자 업데이트 허용
* 범위 [내에 필드 추가](#adobe-granite-oauth-application-and-provider)

   * 기본적으로 허용되는 모든 필드가 포함된 것은 아닙니다.

편집이 필요한 경우 각 AEM 게시 인스턴스에서 다음을 수행합니다.

1. 관리자 권한으로 로그인합니다.
1. 웹 콘솔로 [이동합니다](../../help/sites-deploying/configuring-osgi.md). 예: http://localhost:4503/system/console/configMgr.
1. AEM Communities Facebook OAuth 공급자를 찾습니다.
1. 편집할 연필 아이콘을 선택합니다.

   ![fboauthprov_png](assets/fboauthprov_png.png)

   * **[!UICONTROL OAuth 공급자 ID]**

      (*필수*) 기본값은 *soco-facebook*&#x200B;입니다. 편집하지 마십시오.

   * **[!UICONTROL 클라우드 서비스 구성]**

      기본값은 */etc/cloudservices/facebook connect입니다*. 편집하지 마십시오.

   * **[!UICONTROL OAuth 공급자 서비스 구성]**

      기본값은 */apps/social/facebook공급자/config/입니다*. 편집하지 마십시오.

   * **[!UICONTROL 태그 사용]**

      편집하지 마십시오.

   * **[!UICONTROL 사용자 경로]**

      사용자 데이터가 저장되는 보관소의 위치입니다. 커뮤니티 사이트의 경우 구성원이 다른 사람의 프로필을 볼 수 있는 권한을 보장하려면 해당 경로가 기본 */홈/사용자/커뮤니티여야*&#x200B;합니다.

   * **[!UICONTROL 필드 활성화]**

      이 확인란을 선택하면 나열된 필드가 사용자 인증 및 정보를 위해 Facebook에 대한 요청에 지정됩니다. 기본값은 선택 취소입니다.

   * **[!UICONTROL 필드]**

      필드가 활성화되면 Facebook 그래프 API를 호출할 때 다음 필드가 포함됩니다. 클라우드 서비스 구성에 정의된 범위 내에서 필드를 허용해야 합니다. 추가 필드에는 Facebook의 승인이 필요할 수 있습니다. Facebook 설명서의 Facebook 로그인 권한 섹션을 참조하십시오. 매개 변수로 추가된 기본 필드는 다음과 같습니다.

      * id
      * 이름
      * first_name
      * last_name
      * link
      * 로케일
      * 그림
      * timezone
      * updated_time
      * 확인됨
      * 이메일
   필드가 추가되거나 변경된 경우 해당 기본 동기화 처리기 구성을 업데이트하여 매핑을 수정합니다.

   * **[!UICONTROL 사용자 업데이트]**&#x200B;이 확인란을 선택하면 프로필 변경 사항이나 요청된 추가 데이터를 반영하도록 각 로그인 시 저장소의 사용자 데이터를 새로 고칩니다. 기본값은 선택 취소입니다.


#### 다음 단계 {#next-steps}

다음 단계는 Facebook과 Twitter 모두에 대해 동일합니다.

* [클라우드 서비스 구성 게시](#publishcloudservices)
* [커뮤니티 사이트 활성화](#enable-social-login)

## Twitter 로그인 {#twitter-login}

### Twitter 앱 만들기 {#create-a-twitter-app}

Twitter 소셜 로그인을 활성화하려면 구성된 Twitter 애플리케이션이 필요합니다.

최신 지침에 따라 https://apps.twitter.com에서 새 Twitter 응용 프로그램을 [만듭니다](https://apps.twitter.com/).

일반적으로:

1. 웹 *사이트* 사용자에게 Twitter 애플리케이션을 식별할 이름을 입력합니다.
1. *설명* 입력.
1. 웹 *사이트의* 경우 - https://&lt;server>/를 입력합니다.
1. 콜백 *URL의* 경우 - https://&lt;server>/를 입력합니다.

   >[!NOTE]
   >
   >포트를 지정할 필요는 없습니다.
   >
   >개발을 위해 https://127.0.0.1/이 작동합니다.

1. 애플리케이션이 만들어지면 소비자(API) **[!UICONTROL 키와 소비자]** (API) **[!UICONTROL 암호를 찾습니다]**. 이 정보는 Twitter 클라우드 서비스를 구성하는 데 [필요합니다](#createatwittercloudservice).

#### 권한 {#permissions}

Twitter 애플리케이션 관리의 권한 섹션에서 다음을 수행합니다.

* **[!UICONTROL 액세스]**:을 `Read only`선택합니다.

   * 다른 옵션은 지원되지 않습니다.

* **[!UICONTROL 추가 권한]**:원하는 경우 `Request email addresses from users`선택합니다.

   * 선택하지 않으면 AEM의 사용자 프로필에 이메일 주소가 포함되지 않습니다.
   * Twitter의 지침에 따라 수행해야 할 추가 단계가 표시됩니다.

소셜 로그인에 대해 수행된 REST 요청은 GET *[account/verify credentials](https://dev.twitter.com/rest/reference/get/account/verify_credentials)*뿐입니다.

### Twitter Connect Cloud 서비스 만들기 {#create-a-twitter-connect-cloud-service}

클라우드 서비스 [구성을](#adobe-granite-oauth-application-and-provider) 만들어 인스턴스화된 Adobe Granite OAuth 응용 프로그램 및 공급자 인스턴스는 Twitter 응용 프로그램과 새 사용자가 추가되는 멤버 그룹을 식별합니다.

1. 작성자 인스턴스에서 관리자 권한으로 로그인합니다.
1. 글로벌 탐색에서 도구 > 클라우드 **[!UICONTROL 서비스 > Twitter Social 로그인 구성을]**&#x200B;선택합니다.
1. 컨텍스트 **[!UICONTROL 경로]** 구성을 선택합니다.

   컨텍스트 경로는 커뮤니티 사이트를 만들거나 편집할 때 선택한 클라우드 구성 경로와 같아야 합니다.

1. 컨텍스트 경로에서 클라우드 서비스를 만들 수 있는지 확인합니다.
1. 도구 > **[!UICONTROL 일반 > 구성 브라우저로 이동합니다]**. 컨텍스트를 선택하고 속성을 편집합니다. 아직 활성화되지 않은 경우 클라우드 구성을 활성화합니다.

   ![twitterconfigpropping](assets/twitterconfigproppng.png)

1. Twitter 클라우드 서비스 구성 만들기/편집을 참조하십시오.

   ![twittersocialloginpng](assets/twittersocialloginpng.png)

   * **[!UICONTROL 제목]** (*필수*) Twitter 앱을 식별하는 표시 제목을 입력합니다. Twitter 앱의 표시 이름으로 입력한 동일한 *이름을 사용하는* 것이 좋습니다.

   * **[!UICONTROL 소비자 키]** (*필수*) Twitter **앱용 API** 키를 입력합니다. 대화 상자에서 [만든 Adobe Granite OAuth 응용 프로그램 및](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#AdobeGraniteOAuthApplicationandProvider) 공급자 인스턴스를 식별합니다.

   * **[!UICONTROL 소비자 암호]** (*필수*)Twitter ***앱용 Consumer(API)*** 암호를 입력합니다.

   * **[!UICONTROL 사용자]** 만들기 이 확인란을 선택하면 Twitter 계정으로 로그인하여 AEM 사용자 항목을 만들고 선택한 사용자 그룹에 멤버로 추가합니다. 기본값은 선택됨(적극 권장).

   * **[!UICONTROL 마스크 사용자 ID]** 선택 해제

   * **[!UICONTROL 사용자 그룹에]** 추가를 선택하여 사용자가 추가될 커뮤니티 사이트에 대해 하나 이상의 [구성원 그룹을](https://helpx.adobe.com/experience-manager/6-3/communities/using/users.html) 선택합니다.
   >[!NOTE]
   >
   >그룹은 언제든지 추가하거나 제거할 수 있습니다. 그러나 기존 사용자의 멤버십은 영향을 받지 않습니다. 자동 멤버십은 이 필드 업데이트를 게시하는 새 사용자에게만 적용됩니다. 익명 사용자가 비활성화된 사이트의 경우 해당 폐쇄된 커뮤니티 사이트에 대한 해당 커뮤니티 구성원 그룹에 사용자를 추가합니다.

1. 저장 **[!UICONTROL 및]** 게시를 **[!UICONTROL 선택합니다]**.

그 결과 Adobe [Granite OAuth 응용 프로그램 및](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#adobe-granite-oauth-application-and-provider) Provider 인스턴스로 추가 수정이 필요하지 않습니다. 기본 범위는 Twitter 로그인에 대한 표준 권한입니다.

### AEM Communities Twitter OAuth 공급자 {#aem-communities-twitter-oauth-provider}

AEM Communities 구성은 Adobe Granite OAuth [응용 프로그램 및 공급자 인스턴스를 확장합니다](#adobe-granite-oauth-application-and-provider) . 이 공급자는 사용자 업데이트를 허용하기 위해 편집이 필요합니다.

편집이 필요한 경우 각 AEM 게시 인스턴스에서 다음을 수행합니다.

1. 관리자 권한으로 로그인합니다.
1. 웹 콘솔로 [이동합니다](../../help/sites-deploying/configuring-osgi.md).

   예: http://localhost:4503/system/console/configMgr.

1. AEM Communities Twitter OAuth 공급자를 찾습니다.
1. 편집할 연필 아이콘을 선택합니다.

   ![twitter_auth_png](assets/twitteroauth_png.png)

   * **[!UICONTROL OAuth 공급자 ID]** (*필수*)

      기본값은 soco-twitter *입니다*. 편집하지 마십시오.

   * **[!UICONTROL 클라우드 서비스 구성]**

      기본값은 *conf입니다.* 편집하지 마십시오.

   * **[!UICONTROL OAuth 공급자 서비스 구성]**

      기본값은 */apps/social/twitterprovider/config/입니다*. 편집하지 마십시오.

   * **[!UICONTROL 사용자 경로]**

      사용자 데이터가 저장되는 보관소의 위치입니다. 커뮤니티 사이트의 경우 구성원이 다른 사람의 프로필을 볼 수 있는 권한을 보장하려면 해당 경로가 기본 */홈/사용자/커뮤니티여야*&#x200B;합니다.

   * **[!UICONTROL 매개 변수]** 사용 안 함
   * **[!UICONTROL URL 매개]** 변수가 편집되지 않음
   * **[!UICONTROL 사용자 업데이트]**

      이 확인란을 선택하면 각 로그인 시 저장소의 사용자 데이터를 새로 고쳐 프로필 변경 사항이나 요청된 추가 데이터를 반영합니다. 기본값은 선택 취소입니다.

#### 다음 단계 {#next-steps-1}

다음 단계는 Facebook과 Twitter 모두에 대해 동일합니다.

* [클라우드 서비스 구성 게시](#publishcloudservices)
* [커뮤니티 사이트 활성화](#enable-social-login)

## 소셜 로그인 활성화 {#enable-social-login}

### AEM Communities 사이트 콘솔 {#aem-communities-sites-console}

클라우드 서비스가 구성되면 커뮤니티 사이트 [생성](https://helpx.adobe.com/experience-manager/6-3/communities/using/sites-console.html#USERMANAGEMENT) 또는 [관리](https://helpx.adobe.com/experience-manager/6-3/communities/using/sites-console.html#SiteCreation) 중에 사용자 관리 설정 하위 패널을 사용하여 커뮤니티 사이트에 대한 관련 소셜 로그인 설정이 활성화될 [수 있습니다](https://helpx.adobe.com/experience-manager/6-3/communities/using/sites-console.html#ModifyingSiteProperties).

1. 소셜 로그인 구성을 저장한 사이트 구성 컨텍스트를 선택합니다.

1. 일반 탭에서 클라우드 구성을 설정합니다.

   ![managessites_png](assets/managesites_png.png)

1. 설정 탭에서 소셜 로그인 **[!UICONTROL 및 저장을]** 활성화합니다.

   ![usermgmt_png](assets/usermgmt_png.png)

## 소셜 로그인 테스트 {#test-social-login}

* 모든 [게시 인스턴스에서 Adobe Granite](#adobe-granite-oauth-authentication-handler) OAuth 인증 처리기가 활성화되어 있는지 확인
* 클라우드 서비스가 게시되었는지 확인
* 커뮤니티 사이트가 게시되었는지 확인
* 브라우저에서 게시된 사이트 실행예: http://localhost:4503/content/sites/engage/en.html
* 로그인 **[!UICONTROL 선택]**
* Facebook **[!UICONTROL 으로 로그인 또는 Twitter로]** **[!UICONTROL 로그인 선택]**
* Facebook 또는 Twitter에 아직 로그인하지 않은 경우 해당 자격 증명으로 로그인합니다
* Facebook 또는 Twitter 앱에서 표시되는 대화 상자에 따라 권한을 부여해야 할 수 있습니다
* 페이지 상단의 도구 모음이 성공적인 로그인을 반영하도록 업데이트되었습니다.
* 프로필 **[!UICONTROL 선택]**:프로필 페이지에는 사용자의 아바타 이미지, 이름 및 성이 표시됩니다. 또한 허용된 필드/매개 변수에 따라 Facebook 또는 Twitter 프로필의 정보도 표시됩니다.

## AEM Platform OAuth 구성 {#aem-platform-oauth-configurations}

### Adobe Granite OAuth 인증 처리기 {#adobe-granite-oauth-authentication-handler}

이 `Adobe Granite OAuth Authentication Handler` 옵션은 기본적으로 활성화되지 않으며 모든 AEM 게시 인스턴스에서 활성화되어야 ***합니다.***

게시 시 인증 처리기를 활성화하려면 OSGi 구성을 열고 저장하면 됩니다.

* 관리자 권한으로 로그인
* 웹 콘솔로 이동합니다. [예](../../help/sites-deploying/configuring-osgi.md): http://localhost:4503/system/console/configMgr
* 찾기 `Adobe Granite OAuth Authentication Handler`
* 편집할 구성을 열려면 선택합니다.
* **[!UICONTROL 저장]**&#x200B;을 선택합니다

![chlimage_1-489](assets/chlimage_1-489.png)

>[!CAUTION]
>
>Adobe Granite OAuth 응용 프로그램 및 공급자의 Facebook 또는 Twitter 인스턴스와 인증 *처리기를 혼동하지 않도록 주의하십시오*.

![chlimage_1-490](assets/chlimage_1-490.png)

### Adobe Granite OA 파섹 {#adobe-granite-oauth-application-and-provider}

Facebook 또는 Twitter에 대한 클라우드 서비스가 만들어지면 인스턴스가 `Adobe Granite OAuth Authentication Handler` 생성됩니다.

Facebook 또는 Twitter 앱에 대해 생성된 인스턴스를 찾으려면 다음을 수행하십시오.

1. 관리자 권한으로 로그인합니다.
1. 웹 콘솔로 [이동합니다](../../help/sites-deploying/configuring-osgi.md).

   예: http://localhost:4503/system/console/configMgr.

1. Adobe Granite OAuth 응용 프로그램 및 공급자를 찾습니다.

   * 클라이언트 ID가 앱 **[!UICONTROL ID와]** 일치하는 인스턴스를 **[!UICONTROL 찾습니다.]**
   ![chlimage_1-491](assets/chlimage_1-491.png)

   다음 속성을 제외하고 구성의 다른 속성은 변경하지 않은 상태로 두십시오.

   * **[!UICONTROL 구성 ID]**

      (*필수*) OAuth 구성 ID는 고유해야 합니다. 클라우드 서비스를 만들 때 자동으로 생성됩니다.

   * **[!UICONTROL 클라이언트 ID]**

      (*필수*&#x200B;사항) 클라우드 서비스를 만들 때 제공된 응용 프로그램 ID입니다.

   * **[!UICONTROL 클라이언트 암호]**

      (*필수*) 클라우드 서비스가 생성될 때 제공된 응용 프로그램 암호입니다.

   * **[!UICONTROL 범위]**

      (*선택*&#x200B;사항) 제공자로부터 허용된 내용에 대한 추가 범위를 요청할 수 있습니다. 기본 범위에서는 소셜 인증 및 프로필 데이터를 제공하는 데 필요한 권한을 다룹니다.

   * **[!UICONTROL 공급자 ID]**

      (*필수*) 클라우드 서비스를 만들 때 AEM Communities에 대한 공급자 ID가 설정됩니다. 편집하지 마십시오. Facebook Connect의 경우 값은 *soco -facebook*&#x200B;입니다. Twitter Connect의 경우 값은 *soco-twitter*&#x200B;입니다.

   * **[!UICONTROL 그룹]**

      (*권장*) 만든 사용자가 추가된 하나 이상의 구성원 그룹입니다. AEM Communities의 경우 커뮤니티 사이트에 대한 구성원 그룹을 나열하는 것이 좋습니다.

   * **[!UICONTROL 콜백 URL]**

      (*선택*&#x200B;사항) 클라이언트를 다시 리디렉션하기 위해 OAuth 공급자로 구성된 URL. 원본 요청의 호스트를 사용하려면 상대 URL을 사용합니다. 원래 요청된 URL을 대신 사용하려면 비워 두십시오. 접미사 &quot;/callback/j_security_check&quot;가 이 url에 자동으로 추가됩니다.
   >[!NOTE]
   >
   >콜백의 도메인은 공급자(Facebook 또는 Twitter)에 등록되어 있어야 합니다.

각 OAuth 인증 핸들러 구성에 대해 인스턴스에서 만들어진 두 개의 추가 구성이 있습니다.

* Apache Jackrabbit Oak Default Sync Handler(org.apache.jackrabbit.oak.security.authentication.external.impl.DefaultSyncHandler) - 편집할 필요가 없지만 Facebook 필드가 CQ 사용자 프로필 노드에 매핑되는 방법을 사용자 필드 매핑을 볼 수 있습니다. 또한 &#39;Sync Handler Name&#39;은 OAuth 공급자 구성의 구성 ID와 일치하는지 확인합니다.
* Apache Jackrabbit Oak 외부 로그인 모듈(org.apache.jackrabbit.spi.security.authentication.external.impl.ExternalLoginModuleFactory) - 편집할 필요가 없지만, &#39;ID 공급자 이름&#39;과 &#39;동기화 처리기 이름&#39;이 각각 동일하며 해당 OAuth 및 동기화 처리기 구성을 가리키는 것을 알 수 있습니다.

자세한 내용은 Apache Oak [외부 로그인 모듈을 사용한 인증을 참조하십시오](https://jackrabbit.apache.org/oak/docs/security/authentication/externalloginmodule.html).

## OAuth 사용자 트래픽 성능 {#oauth-user-traversal-performance}

수십만 명의 사용자가 Facebook 또는 Twitter 로그인을 사용하여 등록하는 커뮤니티 사이트의 경우 사이트 방문자가 소셜 로그인을 사용할 때 수행되는 쿼리의 추적 성능을 다음 Oak 인덱스를 추가하여 향상시킬 수 있습니다.

로그에 트래픽 경고가 표시되는 경우 이 인덱스를 추가하는 것이 좋습니다.

작성자 인스턴스에서 관리 권한으로 로그인했습니다.

1. 전역 탐색에서:도구, **CRX/[DE Lite를 선택합니다](../../help/sites-developing/developing-with-crxde-lite.md).**
1. ntBaseLucene의 복사본에서 ntBaseLucene-oauth라는 인덱스를 만듭니다.

   * /oak:index 노드 아래
   * 노드 ntBaseLucene 선택
   * 복사 **[!UICONTROL 선택]**
   * 선택 `/oak:index`
   * 붙여넣기 **[!UICONTROL 선택]**
   * ntBaseLucene의 복사본 이름을 ntBaseLucene-oauth로 변경합니다.

1. ntBaseLucene-oauth 노드의 속성을 수정합니다.

   * **[!UICONTROL indexPath]**:/oak:index/ntLucene-oauth
   * **[!UICONTROL 이름]**:oauthid-123****
   * **[!UICONTROL 다시 색인]**:true
   * **[!UICONTROL reindexCount]**:1

1. /oak:index/ntBaseLucene-oauth/indexRules/nt:base/properties:

   * cqTags를 제외한 모든 하위 노드를 삭제합니다.
   * cqTags의 이름을 oauthid-123****
   * 노드 authid-123***** 속성 수정

      * **[!UICONTROL 이름]**:oauthid-123****
   * 모두 **[!UICONTROL 저장을 선택합니다]**.


**** &amp;ast;oauthid- **123** 의&#x200B;*경우, Facebook ID* ID *나 Twitter Id* 또는 Twitter API(Consumer API) ***와 함께*** oauthid-123 ****** **** [](social-login.md#adobe-granite-oauth-application-and-provider)을 지정합니다. KeyKeyKeyKey는 Adobe Granite UTH의 클라이언트 ID와 Providgranite의 Application를 대체할 수 및 Application을 지정합니다.

![chlimage_1-492](assets/chlimage_1-492.png)

자세한 내용 및 도구는 Oak 쿼리 [및 색인화를 참조하십시오](../../help/sites-deploying/queries-and-indexing.md).

## Dispatcher Configuration {#dispatcher-configuration}

Dispatcher [for Communities 구성을 참조하십시오](dispatcher.md).
