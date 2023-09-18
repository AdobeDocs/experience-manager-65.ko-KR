---
title: 커뮤니티 사이트 콘솔
description: 커뮤니티 사이트 콘솔에 액세스하는 방법
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: 426e3adf-3723-4d17-a988-6eb050939e68
source-git-commit: ab3d016c7c9c622be361596137b150d8719630bd
workflow-type: tm+mt
source-wordcount: '3082'
ht-degree: 4%

---

# 커뮤니티 사이트 콘솔 {#communities-sites-console}

커뮤니티 사이트 콘솔에서는 다음에 액세스할 수 있습니다.

* 사이트 생성
* 사이트 편집
* 사이트 관리
* [중첩 그룹 만들기 및 편집](/help/communities/groups.md) (하위 커뮤니티)

다음을 참조하십시오 [AEM Communities 시작하기](/help/communities/getting-started.md) 작성자 환경에서 커뮤니티 사이트를 만드는 속도와 작성자 및 게시 환경에서 커뮤니티 그룹을 만드는 방법을 경험할 수 있습니다.

>[!NOTE]
>
>만들기 기본 커뮤니티 메뉴 [커뮤니티 사이트](/help/communities/sites-console.md), [커뮤니티 사이트 템플릿](/help/communities/sites.md), [커뮤니티 그룹 템플릿](/help/communities/tools-groups.md), 및 [커뮤니티 기능](/help/communities/functions.md) 는 작성 환경에서만 사용됩니다.

## 사전 요구 사항 {#prerequisites}

커뮤니티 사이트를 만들기 전에 *필수* 끝:

* 하나 이상의 게시 인스턴스가 실행 중인지 확인하십시오.
* 활성화 [터널 업무](/help/communities/deploy-communities.md#tunnel-service-on-author) 을 클릭하여 구성원 및 구성원 그룹을 관리합니다.
* 다음 항목 식별 [기본 게시자](/help/communities/deploy-communities.md#primary-publisher).
* [복제 구성](/help/communities/deploy-communities.md#replication-agents-on-author) 기본 게시자 포트가 기본값이 아닌 경우(4503).

사이트가 많은 기능을 지원할 수 있도록 하는 가장 좋은 방법은 다음 단계를 수행하는 것입니다.

* 설치 [최신 기능 팩](/help/communities/deploy-communities.md#latestfeaturepack).
* 사용 [Adobe Analytics](/help/communities/analytics.md) AEM Communities용
* 구성 [이메일](/help/communities/email.md)
* 식별 [커뮤니티 관리자](/help/communities/users.md#creating-community-members).
* [OAuth 처리기 활성화](/help/communities/social-login.md#adobe-granite-oauth-authentication-handler) 소셜 로그인.

## 커뮤니티 사이트 콘솔 액세스 {#accessing-communities-sites-console}

작성 환경에서 커뮤니티 사이트 콘솔에 도달하려면 다음 작업을 수행하십시오.

* 전역 탐색에서: **[!UICONTROL 커뮤니티]** > **[!UICONTROL 사이트]**

커뮤니티 사이트 콘솔에는 기존 커뮤니티 사이트가 모두 표시됩니다. 이 콘솔에서 커뮤니티 사이트를 만들고, 편집하고, 관리하고, 삭제할 수 있습니다.

커뮤니티 사이트를 만들려면 **만들기** 아이콘.

중첩된 그룹의 작성, 수정, 게시, 내보내기 또는 추가를 위해 기존 커뮤니티 사이트에 액세스하려면 사이트의 폴더 아이콘을 선택합니다.

## 사이트 생성 {#site-creation}

사이트 생성 콘솔은 선택한 항목에 따라 사이트의 기능을 조합하는 단계별 접근 방식을 제공합니다 [커뮤니티 사이트 템플릿](/help/communities/sites.md) 및 설정.

콘텐츠를 게시하거나, 메시지를 보내거나, 그룹에 참여하기 전에 사이트 방문자가 로그인해야 하므로 만들어진 모든 사이트에는 로그인 기능이 포함됩니다. 포함된 기타 기능에는 사용자 프로필, 메시지, 알림, 사이트 메뉴, 검색, 테마 및 브랜딩이 있습니다.

프로세스를 시작할 때 `Create` 커뮤니티 사이트 콘솔 상단에 있는 단추입니다.

작성 프로세스는 구성할 기능 세트(하위 패널로 표시)가 포함된 패널로 표시되는 일련의 단계입니다. 다음으로 이동할 수 있습니다. **다음** 단계 또는 **뒤로** 마지막 단계에서 사이트를 커밋하기 전에 이전 단계로 이동합니다.

### 1단계 : 사이트 템플릿 {#step-site-template}

![newsitemplate](assets/newsitetemplate.png)

사이트 템플릿 패널에서 제목, 설명, 사이트 루트, 기본 언어, 이름 및 사이트 템플릿을 지정합니다.

* **커뮤니티 사이트 제목**

  사이트의 표시 제목입니다.

  제목은 게시된 사이트 및 사이트 관리자 UI에 표시됩니다.

* **커뮤니티 사이트 설명**

  사이트에 대한 설명.

  게시된 사이트에 설명이 표시되지 않습니다.

* **커뮤니티 사이트 루트**

  사이트에 대한 루트 경로입니다.

  기본 루트는 입니다. `/content/sites`로 설정되어 있지만 루트는 웹 사이트 내의 원하는 위치로 이동할 수 있습니다.

* **커뮤니티 사이트 기본 언어**

  (단일 언어의 경우 그대로 유지: 영어) 풀다운 메뉴를 사용하여 하나 선택 *이상* 독일어, 이탈리아어, 프랑스어, 일본어, 스페인어, 포르투갈어(브라질), 중국어(번체) 및 중국어(간체)의 기본 언어 커뮤니티 사이트는에 설명된 모범 사례에 따라 추가된 언어마다 하나씩 만들어지며 동일한 사이트 폴더 내에 존재합니다 [다국어 사이트를 위한 콘텐츠 번역](/help/sites-administering/translation.md). 각 사이트의 루트 페이지에는 선택한 언어 중 하나의 언어 코드로 이름이 지정된 하위 페이지(예: 영어의 경우 &#39;en&#39;, 프랑스어의 경우 &#39;fr&#39;)가 포함되어 있습니다.

* **커뮤니티 사이트 이름**:

  URL에 표시되는 사이트 루트 페이지의 이름입니다.

   * 사이트를 만든 후에는 쉽게 변경되지 않으므로 이름을 다시 확인하십시오.
   * 기본 URL( `https://server:port/site root/site name)` 아래에 표시됩니다. `Community Site Name`.

   * 유효한 URL을 보려면 기본 언어 코드 + &quot;.html&quot;을 추가하십시오.

     *예*, `https://localhost:4502/content/sites/mysight/en.html`

* **커뮤니티 사이트 템플릿** 메뉴

  풀다운 메뉴를 사용하여 사용 가능한 항목 선택 [커뮤니티 사이트 템플릿](/help/communities/tools.md).

* **다음**&#x200B;을 선택합니다.

### 2단계 : 디자인 {#step-design}

디자인 패널에는 테마 및 브랜딩 배너를 선택할 수 있는 두 개의 하위 패널이 있습니다.

#### 커뮤니티 사이트 테마 {#community-site-theme}

![사이트 테마](assets/sitetheme.png)

프레임워크는 `Twitter Bootstrap` 를 통해 응답형의 유연한 디자인을 사이트에 도입할 수 있습니다. 다수의 미리 로드된 Bootstrap 테마 중 하나를 선택하여 선택된 커뮤니티 사이트 템플릿을 스타일링하거나, Bootstrap 테마를 업로드할 수 있습니다.

선택하면 테마가 불투명한 파란색 확인 표시로 오버레이됩니다.

커뮤니티 사이트가 게시된 후 다음을 수행할 수 있습니다. [속성 편집](#modifying-site-properties) 다른 테마를 선택하십시오.

#### 커뮤니티 사이트 브랜딩 {#community-site-branding}

![사이트 브랜딩](assets/site-branding.png)

커뮤니티 사이트 브랜딩은 각 페이지 상단에 헤더로 표시되는 이미지입니다.

이미지의 크기는 브라우저에서 예상되는 페이지 표시와 120픽셀 높이의 크기여야 합니다.

이미지를 만들거나 선택할 때는 다음 사항에 유의하십시오.

* 이미지 높이는 이미지의 위쪽 가장자리에서 측정한 120픽셀로 잘립니다.
* 이미지가 브라우저 창의 왼쪽 가장자리에 고정됩니다.
* 이미지 너비가 ...일 때 이미지 크기는 조정되지 않습니다.

   * 브라우저의 너비보다 작은 이미지는 가로로 반복됩니다.
   * 브라우저의 너비보다 크면 이미지가 잘린 것으로 표시됩니다.

* **다음**&#x200B;을 선택합니다.

### 3단계 : 설정 {#step-settings}

설정 패널에는 사이트를 만들기 위한 마지막 단계로 이동하기 전에 구성할 기능을 제공하는 여러 하위 패널이 있습니다.

* [사용자 관리](#user-management)
* [태깅](#tagging)
* [역할](#roles)
* [중재](#moderation)
* [분석](#analytics)
* [번역](#translation)

>[!NOTE]
>
>**터널 서비스 활성화**
>
>일부 설정 하위 패널을 사용하면 트러스트된 구성원을 할당하여 UGC를 중재하거나, 그룹을 관리하거나, 게시 환경의 지원 리소스에 대한 담당자가 될 수 있습니다.
>
>규칙은 게시측을 위한 것입니다. [사용자 및 사용자 그룹](/help/communities/users.md) (구성원 및 구성원 그룹)은 작성 환경에서 복제할 수 없습니다.
>
>따라서 작성 환경에서 커뮤니티 사이트를 만들고 다양한 역할에 신뢰할 수 있는 구성원을 할당할 때 게시 환경에서 구성원 데이터를 검색해야 합니다.
>
>이 작업은 다음을 활성화하여 수행합니다. ` [AEM Communities Publish Tunnel Service](/help/communities/deploy-communities.md#tunnel-service-on-author)` 작성 환경용입니다.

#### 사용자 관리 {#user-management}

![createsitesettings](assets/createsitesettings.png)

* **사용자 등록 허용**

  선택하면 사이트 방문자가 자체 등록에 의해 커뮤니티 구성원이 될 수 있습니다.
선택하지 않으면 커뮤니티 사이트는 *제한됨* 및 사이트 방문자는 커뮤니티 사이트의 구성원 그룹에 할당되거나 요청하거나 이메일로 초대를 받아야 합니다. 선택하지 않으면 익명 액세스를 허용하지 않습니다.
선택 취소 *비공개* 커뮤니티 사이트입니다. 기본값은 선택되어 있습니다.

* **익명 액세스 허용**

  선택하면 커뮤니티 사이트는 *열기* 모든 사이트 방문자가 사이트에 액세스할 수 있습니다.
선택하지 않으면 로그인한 구성원만 사이트에 액세스할 수 있습니다.
선택 취소 *비공개* 커뮤니티 사이트입니다. 기본값은 선택되어 있습니다.

* **메시지 허용**

  선택하면 구성원이 커뮤니티 사이트 내에서 서로 및 그룹에 메시지를 보낼 수 있습니다.
선택하지 않으면 커뮤니티에 대해 메시징이 설정되지 않습니다.
기본값은 선택 취소되어 있습니다.

* **소셜 로그인 허용: Facebook**

  선택하면 사이트 방문자가 Facebook 계정 자격 증명으로 로그인할 수 있도록 허용합니다. 선택한 항목 [Facebook 클라우드 구성](/help/communities/social-login.md#create-a-facebook-connect-cloud-service) 커뮤니티 사이트가 생성되면 커뮤니티 사이트의 구성원 그룹에 사용자를 추가하도록 구성해야 합니다.
선택하지 않으면 Facebook 로그인이 표시되지 않습니다.
에 대해 선택하지 않은 상태로 둡니다. *비공개* 커뮤니티 사이트입니다. 기본값은 선택 취소되어 있습니다.

* **소셜 로그인 허용: Twitter**

  선택하면 사이트 방문자가 Twitter 계정 자격 증명으로 로그인할 수 있도록 허용합니다. 선택한 항목 [Twitter 클라우드 구성](/help/communities/social-login.md#create-a-twitter-connect-cloud-service) 커뮤니티 사이트가 생성되면 커뮤니티 사이트의 구성원 그룹에 사용자를 추가하도록 구성해야 합니다.
선택하지 않으면 Twitter 로그인이 표시되지 않습니다.
에 대해 선택하지 않은 상태로 둡니다. *비공개* 커뮤니티 사이트입니다. 기본값은 선택 취소되어 있습니다.

>[!NOTE]
>
>**소셜 로그인 허용**
>
>반면에 샘플 Facebook 및 Twitter 구성은 존재할 수 있으며 [프로덕션 환경](/help/sites-administering/production-ready.md), 사용자 지정 Facebook 및 Twitter 애플리케이션을 만들어야 합니다. 다음을 참조하십시오 [facebook 및 Twitter을 사용한 소셜 로그인](/help/communities/social-login.md).

#### 태깅 {#tagging}

![사이트 태그 지정](assets/site-tagging.png)

커뮤니티 콘텐츠에 적용할 수 있는 태그는 를 통해 이전에 정의된 Tag Namespaces를 선택하여 제어합니다. [태깅 콘솔](/help/sites-administering/tags.md#tagging-console).

또한 커뮤니티 사이트에 대해 태그 네임스페이스를 선택하면 카탈로그 및 리소스를 정의할 때 표시되는 선택이 제한됩니다.

* 텍스트 검색 상자 : 사이트에서 사용할 수 있는 태그를 식별하는 입력을 시작합니다.

#### 역할 {#roles}

![커뮤니티 역할](assets/site-admin-2.png)

다음 [커뮤니티 구성원의 역할](/help/communities/users.md) 은(는) 이러한 설정으로 할당됩니다.

커뮤니티 회원을 찾는 것은 자동 입력 검색을 사용하여 쉽게 할 수 있습니다.

* **커뮤니티 관리자**

  커뮤니티 구성원 또는 구성원 그룹을 관리할 수 있는 커뮤니티 구성원 또는 구성원 그룹을 하나 이상 선택하려면 입력을 시작합니다.

* **커뮤니티 중재자**

  입력을 시작하여 사용자 생성 콘텐츠의 중재자로 신뢰할 수 있는 커뮤니티 구성원 또는 구성원 그룹을 한 명 이상 선택합니다.

* **커뮤니티 권한이 있는 구성원**

  입력을 시작하여 한 명 이상의 커뮤니티 구성원 또는 구성원 그룹을 선택하면 다음 경우에 콘텐츠를 만들 수 있는 기능이 제공됩니다. `Allow Privileged Member` 이(가) 다음에 대해 선택되었습니다. [커뮤니티 기능](/help/communities/functions.md).

* **커뮤니티 관리자**

  입력을 시작하여 다른 사이트 관리자 및 기본 커뮤니티 관리자와 독립적으로 사이트 구조를 처리할 수 있는 사이트 관리자를 한 명 이상 선택합니다. 계층 구조의 모든 수준에서 그룹을 만들고 중첩된 그룹의 기본 관리자가 될 수 있습니다(하지만 나중에 중첩된 그룹의 관리자 역할에서 제거할 수 있음).

#### 중재 {#moderation}

![site-moderation](assets/site-moderation.png)

UGC(사용자 생성 컨텐츠) 중재에 대한 전역 설정은 이러한 설정에 의해 제어됩니다. 개별 구성 요소에는 중재 제어를 위한 추가 설정이 있습니다.

* **컨텐츠가 미리 중재되었음**

  선택하면 중재자가 승인할 때까지 게시된 커뮤니티 컨텐츠가 표시되지 않습니다. 기본값은 선택 취소되어 있습니다. 자세한 내용은 [커뮤니티 컨텐츠 중재](/help/communities/moderate-ugc.md#premoderation).

* **컨텐츠가 숨겨지기 전에 임계값에 플래그 지정**

  0보다 큰 경우 주제나 게시물이 공개 보기에서 숨겨지기 전에 플래그 지정해야 하는 횟수입니다. -1로 설정하면 플래그가 지정된 항목이나 게시물이 공개 보기에서 숨겨지지 않습니다. 기본값은 5입니다.

#### 분석 {#analytics}

![site-analytics](assets/site-analytics.png)

* **Analytics 활성화**

  Adobe Analytics이 [구성됨](/help/communities/analytics.md) 커뮤니티 기능.
기본값은 선택 취소되어 있습니다. 선택하면 다음과 같은 추가 선택 메뉴가 나타납니다.

![사이트 분석 사용](assets/site-analytics-enable.png)

* **Cloud 구성 프레임워크 참조**

  풀다운 메뉴에서 이 커뮤니티 사이트에 대해 구성된 Analytics Cloud 서비스 프레임워크를 선택합니다.
  `Communities` 는 의 프레임워크 예입니다. [커뮤니티 기능에 대한 Analytics 구성](/help/communities/analytics.md#aem-analytics-framework-configuration) 설명서를 참조하십시오.

#### 번역 {#translation}

![사이트 번역](assets/site-translation.png)

* **기계 번역 허용**

  이 필드를 선택하면(기본값은 선택 해제) 사이트 내에서 UGC에 대해 기계 변환이 활성화됩니다. 이 경우 사이트가 다국어 사이트로 설정된 경우에도 페이지 콘텐츠와 같은 다른 콘텐츠에는 영향을 주지 않습니다. 다음을 참조하십시오 [사용자 생성 콘텐츠 번역](/help/communities/translate-ugc.md) AEM Communities용 라이선스 번역 서비스 구성에 대한 정보입니다. 다음을 참조하십시오 [다국어 사이트를 위한 콘텐츠 번역](/help/sites-administering/translation.md) 전체 개요를 보려면.

![기계 번역 허용](assets/allow-machine-translation.png)

* **선택한 언어에 대한 기계 번역 사용**

  기계 번역을 위해 활성화된 언어는 기본적으로 [번역 통합 구성](/help/communities/translate-ugc.md#translation-integration-configuration). 기본값을 삭제하거나 풀다운 메뉴에서 다른 언어를 선택하여 이 사이트에 대해 이러한 기본 설정이 재정의될 수 있습니다.

* **번역 공급업체 선택**

  기본적으로 서비스 제공업체는 를 사용하는 체험판 서비스입니다 `microsoft` 데모용입니다. 라이센스가 부여된 번역 서비스 공급자가 없는 경우 **기계 번역 허용** 을 선택 취소해야 합니다.

* **글로벌 공유 스토어 선택**

  여러 언어 사본이 있는 웹 사이트의 경우, 글로벌 공유 저장소는 각 언어 사본에서 볼 수 있는 단일 대화 스레드를 제공합니다. 언어 사본으로 포함된 언어 중 하나를 선택하면 됩니다. 기본값은 입니다 *글로벌 공유 스토어 없음*.

* **번역 제공자 구성 선택**

  선택 [번역 통합 프레임워크](/help/sites-administering/tc-tic.md) 라이센스가 부여된 번역 공급업체를 위해 생성되었습니다.

* **커뮤니티 사이트에 대한 번역 옵션 선택**

   * **전체 페이지 번역**

     선택하면 페이지의 모든 UGC가 페이지의 기본 언어로 번역됩니다.

     기본값은 입니다 *선택되지 않음*.

   * **선택 사항만 번역**

     선택하면 개별 게시물을 페이지의 기본 언어로 번역할 수 있는 번역 옵션이 각 게시물 옆에 표시됩니다.
기본값은 입니다 *선택됨*.

* **지속성 옵션 선택**

   * **사용자 요청에 대한 기여도를 번역한 후 유지**
이 옵션을 선택하면 요청이 수행될 때까지 콘텐츠가 번역되지 않습니다. 번역되면 번역은 저장소에 저장됩니다.

     기본값은 입니다 *선택되지 않음*.

   * **번역을 유지하지 않습니다**

     선택하면 번역이 저장소에 저장되지 않습니다.

     선택하지 않으면 번역이 유지됩니다.

     기본값은 입니다 *선택되지 않음*.

* **스마트 렌더링**

  다음 중 하나를 선택합니다.

   * `Always show contributions in the original language` (기본값)
   * `Always show contributions in user preferred language`
   * `Show contributions in user preferred language for only logged-in users`

### 4단계 : 커뮤니티 사이트 만들기 {#step-create-communities-site}

조정이 필요한 경우 **뒤로** 단추를 클릭하여 만듭니다.

한 번 **만들기** 이(가) 선택되고 시작되면 사이트 생성 프로세스를 중단할 수 없습니다.

사이트가 생성되면:

* URL(노드 이름) 변경은 지원되지 않습니다.
* 커뮤니티 사이트 템플릿에 대한 향후 변경 사항은 생성된 커뮤니티 사이트에 영향을 주지 않습니다.
* 커뮤니티 사이트 템플릿을 비활성화해도 생성된 커뮤니티 사이트에는 영향을 주지 않습니다.
* 다음을 편집할 수 있습니다. [구조](#modify-structure) 속성을 수정하여 커뮤니티 사이트에 게시합니다.

![create-site](assets/create-site1.png)

프로세스가 완료되면 새 사이트에 대한 폴더가 커뮤니티 사이트 콘솔에 표시됩니다. 여기서 작성자가 페이지 콘텐츠를 추가하거나 관리자가 사이트 속성을 수정할 수 있습니다.

![modify-site-property](assets/modify-site-property.png)

커뮤니티 사이트를 편집하려면 해당 프로젝트 폴더를 선택하여 엽니다.

![사이트 프로젝트](assets/site-project.png)

마우스로 사이트를 가리키거나 사이트 카드를 터치하면 다음을 허용하는 아이콘이 표시됩니다.

* [작성자 모드에서 사이트 편집](#authoring-site-content)
* [수정할 사이트 속성 열기](#modifying-site-properties)
* [사이트 게시](#publishing-the-site)
* [사이트 내보내기](#exporting-the-site)
* [사이트 삭제](#deleting-the-site)

## 사이트 콘텐츠 작성 {#authoring-site-content}

사이트의 콘텐츠는 다른 AEM 웹 사이트와 동일한 도구로 작성할 수 있습니다. 작성할 사이트를 열려면 다음을 선택합니다. `Open Site` 마우스로 사이트를 가리키면 표시되는 아이콘입니다. 커뮤니티 사이트 콘솔에 계속 액세스할 수 있도록 사이트가 새 탭에서 열립니다.

![site-content](assets/site-content.png)

>[!NOTE]
>
>AEM에 익숙하지 않은 경우 [기본 처리](/help/sites-authoring/basic-handling.md) 및 a [페이지 작성에 대한 빠른 안내](/help/sites-authoring/qg-page-authoring.md).

## 사이트 속성 수정 {#modifying-site-properties}

![사이트 편집](assets/edit-site.png)

사이트 생성 프로세스 중에 지정된 기존 사이트의 속성은 `Edit Site`마우스로 사이트를 가리키면 표시되는 아이콘입니다.

`Details of the following properties match the descriptions provided in the` [사이트 생성](#site-creation) 섹션.

![site-basicinfo 수정](assets/modify-site-basicinfo.png)

### 기본 수정 {#modify-basic}

기본 패널을 통해 다음을 수정할 수 있습니다.

* 커뮤니티 사이트 제목
* 커뮤니티 사이트 설명

커뮤니티 사이트 이름은 수정할 수 없습니다.

템플릿과 사이트 간에 연결이 유지되지 않으므로 다른 커뮤니티 사이트 템플릿을 선택해도 기존 커뮤니티 사이트에 영향을 주지 않습니다.

대신, [구조](#modify-structure) 커뮤니티 사이트의 을(를) 수정할 수 있습니다.

### 구조 수정 {#modify-structure}

구조 패널에서는 선택한 커뮤니티 사이트 템플릿에서 처음에 만든 구조를 수정할 수 있습니다. 패널에서 다음을 수행할 수 있습니다.

* 추가 드래그 앤 드롭 [커뮤니티 기능](/help/communities/functions.md) 를 사이트 구조에 추가합니다.
* 사이트 구조의 커뮤니티 기능 인스턴스에서 다음을 수행합니다.

   * **`gear icon`**

     표시 제목 및 URL 이름 등 설정 편집 [권한이 있는 구성원 그룹](/help/communities/users.md#privilegedmembersgroups).

   * **`trashcan icon`**

     사이트 구조에서 기능을 제거(삭제)합니다.

   * **`grid icon`**

     사이트의 최상위 탐색 막대에 표시되는 함수 순서를 수정합니다.

>[!NOTE]
>
>맨 위에 있는 함수를 제외하고 사이트 구조에 있는 모든 함수의 순서를 변경할 수 있습니다. 따라서 커뮤니티 사이트의 홈페이지는 변경할 수 없습니다.

>[!CAUTION]
>
>* 표시 제목은 부작용 없이 변경할 수 있지만 커뮤니티 사이트에 속한 커뮤니티 기능의 URL 이름은 편집하지 않는 것이 좋습니다.
>
>예를 들어 URL의 이름을 바꾸면 기존 UGC가 이동하지 않아 UGC가 &#39;손실&#39;됩니다.

>[!CAUTION]
>
>groups 함수는 *아님* 다음이 되어야 합니다. *처음도 아니고* 사이트 구조에서 작동합니다.
>
>기타 모든 함수(예: ) [페이지 기능](/help/communities/functions.md#page-function)를 포함해야 하며 먼저 나열되어야 합니다.

#### 예 : 커뮤니티 사이트 구조에 카탈로그 기능 추가 {#example-adding-a-catalog-function-to-a-community-site-structure}

![카탈로그 사이트 추가](assets/add-catalog-site.png)

### 디자인 수정 {#modify-design}

디자인 패널을 통해 새 테마를 적용할 수 있습니다.

* [커뮤니티 사이트 테마](#community-site-theme)
* [커뮤니티 사이트 브랜딩](#community-site-branding)

   * 브랜드 이미지를 변경할 수 있도록 패널 하단으로 스크롤합니다.

### 설정 수정 {#modify-settings}

설정 패널에서는 커뮤니티 사이트 생성 3단계에 대한 의 하위 패널 아래에 있는 대부분의 설정에 액세스할 수 있습니다.

* [사용자 관리](#user-management)
* [태그](#tagging)
* [관리](#moderation)
* [구성원 역할](#roles)
* [분석](#analytics)
* [번역](#translation)

### 썸네일 수정 {#modify-thumbnail}

썸네일 패널을 사용하면 커뮤니티 사이트 콘솔에 사이트를 나타내는 이미지를 업로드할 수 있습니다.

## 사이트 게시 {#publishing-the-site}

커뮤니티 사이트를 새로 만들거나 수정한 후에는 를 선택하여 사이트를 게시(활성화)할 수 있습니다. `Publish Site` 마우스에 표시되는 아이콘은 사이트 위로 마우스를 가져갑니다.

![publish-site](assets/publish-site.png)

사이트가 성공적으로 게시된 후 표시가 있습니다.

![사이트가 게시됨](assets/site-published.png)

### 중첩 그룹으로 게시 {#publishing-with-nested-groups}

커뮤니티 사이트를 게시한 후에는 를 사용하여 만든 각 하위 커뮤니티(중첩된 그룹)를 개별적으로 게시해야 합니다. [그룹 콘솔](/help/communities/groups.md).

## 사이트 내보내기 {#exporting-the-site}

![export-site](assets/export-site.png)

내보내기 아이콘 을 선택하고 사이트에 마우스를 가져다 대면 다음 위치에 저장된 커뮤니티 사이트 패키지를 만들 수 있습니다. [패키지 관리자](/help/sites-administering/package-manager.md) 다운로드되었습니다.

UGC는 사이트 패키지에 포함되어 있지 않습니다.

## 사이트 삭제 {#deleting-the-site}

![deleteicon](assets/deleteicon.png)

커뮤니티 사이트를 삭제하려면 커뮤니티 사이트 콘솔에서 마우스를 사이트 위로 가져갈 때 표시되는 사이트 삭제 아이콘을 선택합니다. 이 작업은 UGC, 사용자 그룹, 에셋 및 데이터베이스 레코드와 같이 사이트와 관련된 모든 항목을 제거합니다.

## 생성된 커뮤니티 사용자 그룹 {#created-community-user-groups}

새 커뮤니티 사이트가 게시되면 다양한 관리 및 구성원 역할에 대해 적절한 권한이 설정된 새 구성원 그룹(사용자 그룹이 게시 환경에서 생성됨)이 생성됩니다.

구성원 그룹에 대해 작성된 이름에는 *site-name* 특정 시점 [1단계](#step13asitetemplate) (URL에 나타나는 이름). 또한 다른 커뮤니티 사이트 루트에 대해 동일한 사이트 이름을 가진 커뮤니티 사이트 및 그룹과의 충돌을 방지하기 위해 고유 ID도 포함되어 있습니다.

예를 들어 이름이 &quot;시작하기 자습서&quot;인 사이트의 이름이 &quot;engage&quot;인 경우 중재자의 사용자 그룹은 가 됩니다.

* title: 커뮤니티 참여 중재자
* 이름: 커뮤니티-*engage-uid*-중재자

사이트를 만드는 동안 중재자 또는 그룹 관리자로 역할을 할당받은 모든 구성원은 적절한 그룹에 할당되고 구성원 그룹에 할당됩니다. 이러한 그룹 및 구성원 할당은 새 사이트가 게시될 때 게시 시 생성됩니다.

자세한 내용은 [사용자 및 사용자 그룹 관리](/help/communities/users.md).

>[!NOTE]
>
>If [소셜 로그인 허용: Facebook](#user-management) 사용자 그룹이 활성화되면 활성화됨 `community-<site-name>-<uid>-members`
>이(가) 만들어지고 이(가) 적용됨 [Facebook 클라우드 서비스](/help/communities/social-login.md#createafacebookcloudservice) 사용자를 이 그룹에 추가하도록 구성해야 합니다.

## 인증 오류 구성 {#configure-for-authentication-error}

기본적으로 커뮤니티 사이트는 사용자가 잘못된 자격 증명을 입력하고 로그인에 실패하면 샘플 로그인 페이지로 리디렉션됩니다. 이 샘플 로그인은 다음에 없습니다. [프로덕션 서버](/help/sites-administering/production-ready.md).

올바르게 리디렉션하려면 사이트가 구성되어 게시로 푸시된 후, 다음 단계를 완료하여 인증 실패를 가져와 커뮤니티 사이트로 리디렉션합니다.

* 각 AEM 게시 인스턴스에서.
* 관리자 권한으로 로그인합니다.
* 액세스 [웹 콘솔](/help/sites-deploying/configuring-osgi.md).

   * 예를 들어, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).

* 찾기 `Adobe Granite Login Selector Authentication Handler`.
* 다음 항목 선택 `pencil` 아이콘을 클릭하면 편집할 구성을 열 수 있습니다.
* 입력 **로그인 페이지 매핑** 다음과 같이:

  `/content/sites/<site-name>/path/to/login/page:/content/sites/<site-name>`

  예:
  `/content/sites/engage/en/signin:/content/sites/engage/en`

* **저장**&#x200B;을 선택합니다.

![auth-error](assets/auth-error.png)

### 인증 리디렉션 테스트 {#test-authentication-redirection}

커뮤니티 사이트에 대한 로그인 페이지 매핑으로 구성된 동일한 AEM 게시 인스턴스에서 다음을 수행합니다.

* 커뮤니티 사이트 홈 페이지로 이동합니다.

   * 예를 들어, [https://localhost:4503/content/sites/engage/en.html](https://localhost:4503/content/sites/engage/en.html)

* 로그아웃을 선택합니다.
* 로그인을 선택합니다.
* 사용자 이름 &quot;x&quot; 및 암호 &quot;x&quot;와 같은 잘못된 자격 증명을 입력합니다.
* 로그인 페이지에 &quot;잘못된 로그인&quot; 오류가 표시되어야 합니다.

![test-authentication](assets/test-authentication.png)

## 기본 사이트 콘솔에서 커뮤니티 사이트 액세스 {#accessing-community-sites-from-main-sites-console}

전역 탐색 사이트 콘솔에서 커뮤니티 사이트는 `Community Sites` 폴더를 삭제합니다.

이러한 방식으로 커뮤니티 사이트에 액세스할 수 있지만 관리 작업의 경우 커뮤니티 사이트 콘솔에서 커뮤니티 사이트에 액세스해야 합니다.

![액세스 사이트](assets/access-site.png)
