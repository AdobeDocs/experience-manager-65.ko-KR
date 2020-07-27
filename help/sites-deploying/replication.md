---
title: 복제
seo-title: 복제
description: AEM에서 복제 에이전트를 구성하고 모니터링하는 방법에 대해 학습합니다.
seo-description: AEM에서 복제 에이전트를 구성하고 모니터링하는 방법에 대해 학습합니다.
uuid: 6c0bc2fe-523a-401f-8d93-e5795f2e88b9
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 3cae081e-93e3-4317-b307-1316283c307a
docset: aem65
translation-type: tm+mt
source-git-commit: d281ea4a5e7711aafa906bc0c43009c3c2cc8947
workflow-type: tm+mt
source-wordcount: '3661'
ht-degree: 3%

---


# 복제{#replication}

복제 에이전트는 다음 작업을 위한 메커니즘으로 AEM(Adobe Experience Manager)의 중심입니다.

* [작성자의 컨텐츠를 게시(활성화)](/help/sites-authoring/publishing-pages.md#activatingcontent) 환경으로 게시합니다.
* Dispatcher 캐시에서 컨텐츠를 명시적으로 플러시합니다.
* 작성 환경의 제어하에 게시 환경에서 작성 환경에 대한 사용자 입력(예: 양식 입력)을 반환합니다.

요청은 [처리를 위해 적절한 에이전트로 큐에](/help/sites-deploying/osgi-configuration-settings.md#apacheslingjobeventhandler) 대기됩니다.

>[!NOTE]
>
>사용자 데이터(사용자, 사용자 그룹 및 사용자 프로필)는 작성자와 게시 인스턴스 간에 복제되지 않습니다.
>
>여러 게시 인스턴스의 경우 사용자 동기화가 활성화되면 사용자 데이터 [가](/help/sites-administering/sync.md) 배포됩니다.

## 작성자에서 게시로 복제 {#replicating-from-author-to-publish}

게시 인스턴스 또는 디스패처에 대한 복제는 몇 가지 단계를 수행합니다.

* 작성자는 특정 컨텐츠가 게시(활성화)될 것을 요청합니다. 수동 요청이나 미리 구성된 자동 트리거를 통해 시작할 수 있습니다.
* 요청이 적절한 기본 복제 에이전트로 전달됩니다. 환경에는 이러한 작업에 대해 항상 선택되는 몇 개의 기본 에이전트가 있을 수 있습니다.
* 복제 에이전트가 컨텐츠를 &quot;패키지&quot;하여 복제 대기열에 넣습니다.
* 웹 사이트 탭에서 개별 페이지에 대해 [색상 상태](/help/sites-authoring/publishing-pages.md#determiningpagepublicationstatus) 표시기가 설정됩니다.
* 컨텐츠는 대기열에서 꺼지고 구성된 프로토콜을 사용하여 게시 환경으로 전송됩니다. 일반적으로 HTTP입니다.
* 게시 환경의 서블릿은 요청을 받고 수신된 컨텐트를 게시합니다. 기본 서블릿은 입니다 `https://localhost:4503/bin/receive`.

* 여러 작성 및 게시 환경을 구성할 수 있습니다.

![chlimage_1-21](assets/chlimage_1-21.png)

### 게시에서 작성자로 복제 {#replicating-from-publish-to-author}

일부 기능을 사용하면 사용자가 게시 인스턴스의 데이터를 입력할 수 있습니다.

경우에 따라, 역방향 복제라고 하는 복제 유형이 이 데이터를 다른 게시 환경으로 재배포되는 작성 환경으로 반환해야 합니다. 보안 고려 사항으로 인해 게시 환경에서 작성 환경에 대한 트래픽은 엄격히 제어되어야 합니다.

역방향 복제는 게시 환경에서 작성 환경을 참조하는 에이전트를 사용합니다. 이 에이전트는 데이터를 보낼 편지함에 배치합니다. 이 outbox는 작성 환경의 복제 리스너와 일치합니다. 수신자는 옵박스를 폴링하여 입력한 데이터를 수집한 다음 필요에 따라 배포합니다. 이렇게 하면 작성 환경에서 모든 트래픽을 제어할 수 있습니다.

커뮤니티 기능(예: 포럼, 블로그, 댓글 및 검토) 등의 경우, 게시 환경에 입력하는 사용자 생성 컨텐츠(UGC)의 양은 복제를 사용하여 AEM 인스턴스 간에 효율적으로 동기화하기가 어렵습니다.

AEM [Communities](/help/communities/overview.md) 는 UGC에 대한 복제를 사용하지 않습니다. 대신, 커뮤니티를 배포하려면 UGC에 대한 공용 저장소가 필요합니다( [커뮤니티 콘텐츠 저장소](/help/communities/working-with-srp.md)참조).

### 복제 - 기본 제공 {#replication-out-of-the-box}

AEM의 표준 설치에 포함된 Adobe-소매 웹 사이트를 복제 예시 용도로 사용할 수 있습니다.

이 예를 따르고 기본 복제 에이전트를 사용하려면 다음을 사용하여 AEM [을](/help/sites-deploying/deploy.md) 설치해야 합니다.

* 포트의 작성 환경 `4502`
* 포트의 게시 환경 `4503`

>[!NOTE]
>
>기본적으로 활성화됨 :
>
>* 작성자의 에이전트: 기본 에이전트(게시)
>
>
기본적으로 효과적으로 비활성화됨(AEM 6.1 기준):
>
>* 작성자의 에이전트: 역방향 복제 에이전트(publish_reverse)
>* 게시 중인 에이전트: 역방향 복제(보낼 편지함)

>
>
에이전트나 큐의 상태를 확인하려면 **도구 콘솔을** 사용합니다.
>복제 에이전트 [모니터링을 참조하십시오](#monitoring-your-replication-agents).

#### 복제(제작자로 게시) {#replication-author-to-publish}

1. 작성 환경에서 지원 페이지로 이동합니다.
   **https://localhost:4502/content/we-retail/us/en/experience.html** `<pi>`
1. 페이지를 편집하여 새 텍스트를 추가합니다.
1. **페이지를** 활성화하여 변경 사항을 게시합니다.
1. 게시 환경에서 지원 페이지를 엽니다.
   **https://localhost:4503/content/we-retail/us/en/experience.html**
1. 이제 작성자에 입력한 변경 사항을 볼 수 있습니다.

이 복제는 작성 환경에서 다음을 통해 수행됩니다.

* **기본 에이전트(게시)**이 에이전트는 컨텐츠를 기본 게시 인스턴스에 복제합니다.
이(구성 및 로그)의 세부 사항은 작성 환경의 도구 콘솔에서 액세스할 수 있습니다. 또는:

   `https://localhost:4502/etc/replication/agents.author/publish.html`.

#### 복제 에이전트 - 기본 {#replication-agents-out-of-the-box}

표준 AEM 설치에서는 다음 에이전트를 사용할 수 있습니다.

* [기본 에이전트](#replication-author-to-publish)작성자에서 게시로 복제하는 데 사용됩니다.

* Dispatcher 플러시Dispatcher 캐시를 관리하는 데 사용됩니다. 자세한 [내용은 제작 환경에서 Dispatcher 캐시 무효화](https://helpx.adobe.com/experience-manager/dispatcher/using/page-invalidate.html#invalidating-dispatcher-cache-from-the-authoring-environment) 및 게시 인스턴스에서 [Dispatcher 캐시 무효화를](https://helpx.adobe.com/experience-manager/dispatcher/using/page-invalidate.html#invalidating-dispatcher-cache-from-a-publishing-instance) 참조하십시오.

* [역방향 복제](#reverse-replication-publish-to-author)에서 작성자로 복제하는 데 사용됩니다. 역 복제는 포럼, 블로그 및 댓글과 같은 커뮤니티 기능에는 사용되지 않습니다. 보낼 편지함이 활성화되지 않아 실제로 비활성화됩니다. 역방향 복제를 사용하려면 사용자 지정 구성이 필요합니다.

* 정적 에이전트이는 &quot;노드의 정적 표현을 파일 시스템에 저장하는 에이전트&quot;입니다.
예를 들어 기본 설정을 사용하면 컨텐츠 페이지 및 dam 에셋이 HTML 또는 해당 에셋 형식 `/tmp`으로 저장됩니다. 구성에 대한 `Settings` 및 `Rules` 탭을 참조하십시오.
응용 프로그램 서버에서 직접 페이지를 요청할 때 내용을 볼 수 있도록 이 요청을 했습니다. 이것은 전문 에이전트이며 (아마도) 대부분의 경우 필요하지 않습니다.

## 복제 에이전트 - 구성 매개 변수 {#replication-agents-configuration-parameters}

도구 콘솔에서 복제 에이전트를 구성할 때 대화 상자 내에 4개의 탭을 사용할 수 있습니다.

### 설정 {#settings}

* **이름**

   복제 에이전트의 고유한 이름입니다.

* **설명**

   이 복제 에이전트가 사용할 용도에 대한 설명입니다.

* **활성화됨**

   복제 에이전트가 현재 활성화되어 있는지 여부를 나타냅니다.

   에이전트가 **활성화되면** 대기열이 다음과 같이 표시됩니다.

   * **항목이 처리되는** 경우 활성화됩니다.
   * **대기열이 비어 있을** 때 유휴 상태입니다.
   * **항목이 큐에 있지만 처리할 수 없을 때 차단됨** ; 예를 들어 수신 대기열이 비활성화된 경우

* **직렬화 유형**

   직렬화의 유형:

   * **기본값**: 에이전트가 자동으로 선택되도록 설정합니다.
   * **Dispatcher 플러시**: 디스패처 캐시를 플러싱하는 데 에이전트를 사용하려면 이 옵션을 선택합니다.

* **다시 시도 지연**

   두 재시도 사이의 지연(대기 시간(밀리초)으로 문제가 발생할 경우

   기본값: `60000`

* **에이전트 사용자 ID**

   환경에 따라 에이전트는 이 사용자 계정을 사용하여 다음을 수행합니다.

   * 작성 환경에서 컨텐츠 수집 및 패키징
   * 게시 환경에서 컨텐츠 만들기 및 쓰기

   시스템 사용자 계정(관리자 사용자로 sling에 정의된 계정)을 사용하려면 이 필드를 비워 두십시오. 기본적으로 이것은 `admin`).

   >[!CAUTION]
   >
   >작성 환경의 에이전트의 경우 이 계정은 복제하려는 모든 경로에 대한 읽기 액세스 권한을 *가져야* 합니다.

   >[!CAUTION]
   >
   >게시 환경의 에이전트의 경우 이 계정은 컨텐츠를 복제하는 데 필요한 만들기/쓰기 액세스 권한이 *있어야* 합니다.

   >[!NOTE]
   >
   >이 방법은 복제용 특정 컨텐츠를 선택하는 메커니즘으로 사용할 수 있습니다.

* **로그 수준**

   로그 메시지에 사용할 세부 정보 수준을 지정합니다.

   * `Error`: 오류만 기록됨
   * `Info`: 오류, 경고 및 기타 정보 메시지가 기록됩니다.
   * `Debug`: 메시지에 주로 디버그 목적으로 높은 수준의 세부 정보가 사용됩니다

   기본값: `Info`

* **역복제에 사용**

   이 에이전트가 역방향 복제에 사용되는지 여부를 나타냅니다. 게시 환경에서 작성 환경에 대한 사용자 입력을 반환합니다.

* **별칭 업데이트**

   이 옵션을 선택하면 Dispatcher에 대한 별칭 또는 별칭 경로 무효화 요청이 활성화됩니다. Dispatcher [플러시 에이전트 구성을 참조하십시오](/help/sites-deploying/replication.md#configuring-a-dispatcher-flush-agent).

#### 전송 {#transport}

* **URI**

   대상 위치의 수신 서블릿을 지정합니다. 특히 여기에서 대상 인스턴스의 호스트 이름(또는 별칭) 및 컨텍스트 경로를 지정할 수 있습니다.

   예:

   * 기본 에이전트는 `https://localhost:4503/bin/receive`
   * Dispatcher 플러쉬 에이전트는 `https://localhost:8000/dispatcher/invalidate.cache`

   여기에 지정된 프로토콜(HTTP 또는 HTTPS)이 전송 방법을 결정합니다.

   Dispatcher 플러시 에이전트의 경우 URI 속성은 경로 기반 가상 호스트 항목을 사용하여 팜 간 구별하는 경우에만 사용되며 이 필드를 사용하여 팜을 대상으로 하여 무효화합니다. 예를 들어, 팜 #1에는 가상 호스트가 `www.mysite.com/path1/*` 있고 팜 #2에는 가상 호스트가 `www.mysite.com/path2/*`있습니다. 의 URL을 사용하여 첫 번째 팜 `/path1/invalidate.cache` 을 타깃팅하고 두 번째 팜을 타깃팅할 `/path2/invalidate.cache` 수 있습니다.

* **사용자**

   대상에 액세스하는 데 사용할 계정의 사용자 이름입니다.

* **암호**

   대상에 액세스하는 데 사용할 계정의 비밀번호입니다.

* **NTLM 도메인**

   NTML 인증을 위한 도메인.

* **NTLM 호스트**

   NTML 인증을 위한 호스트입니다.

* **느슨한 SSL 허용**

   자체 인증 SSL 인증서를 수락하려는 경우 활성화합니다.

* **만료된 인증서 허용**

   만료된 SSL 인증서를 수락하려면 활성화합니다.

#### 프록시 {#proxy}

다음 설정은 프록시가 필요한 경우에만 필요합니다.

* **프록시 호스트**

   전송에 사용되는 프록시의 호스트 이름입니다.

* **프록시 포트**

   프록시의 포트입니다.

* **프록시 사용자**

   사용할 계정의 사용자 이름입니다.

* **프록시 암호**

   사용할 계정의 암호.

* **프록시 NTLM 도메인**

   프록시 NTLM 도메인.

* **프록시 NTLM 호스트**

   프록시 NTLM 도메인.

#### 확장됨 {#extended}

* **인터페이스**

   바인딩할 소켓 인터페이스를 정의할 수 있습니다.

   연결을 만들 때 사용할 로컬 주소를 설정합니다. 이 옵션이 설정되지 않으면 기본 주소가 사용됩니다. 다중 홈 또는 클러스터된 시스템에서 사용할 인터페이스를 지정하는 데 유용합니다.

* **HTTP 메서드**

   사용할 HTTP 메서드입니다.

   Dispatcher 플러쉬 에이전트의 경우 거의 항상 GET이며 변경해서는 안 됩니다(POST는 다른 가능한 값).

* **HTTP 헤더**

   Dispatcher 플러시 에이전트에 사용되며 플러시되어야 하는 요소를 지정합니다.

   Dispatcher 플러시 에이전트의 경우 세 가지 표준 항목을 변경할 필요가 없습니다.

   * `CQ-Action:{action}`
   * `CQ-Handle:{path}`
   * `CQ-Path:{path}`

   이러한 속성은 핸들 또는 경로를 플러시할 때 사용할 동작을 나타내는 데 사용됩니다. 하위 매개 변수는 동적입니다.

   * `{action}` 복제 작업을 나타냅니다.

   * `{path}` 경로 표시

   이러한 속성은 요청과 관련된 경로/작업으로 대체되므로 &quot;하드 코딩되지 않아도 됩니다.

   >[!NOTE]
   >
   >권장 기본 컨텍스트 이외의 컨텍스트에 AEM을 설치한 경우 HTTP 헤더에서 컨텍스트를 등록해야 합니다. 예:
   >`CQ-Handle:/<*yourContext*>{path}`

* **연결 끊기**

   각 요청 후 연결을 닫을 수 있습니다.

* **연결 시간 초과**

   연결을 설정할 때 적용할 시간 초과(밀리초)입니다.

* **소켓 시간 초과**

   연결이 설정된 후 트래픽을 기다릴 때 적용할 시간 초과(밀리초)입니다.

* **프로토콜 버전**

   프로토콜 버전; 예 `1.0` (예: HTTP/1.0).

#### 트리거 {#triggers}

이러한 설정은 자동 복제를 위한 트리거를 정의하는 데 사용됩니다.

* **기본값 무시**

   선택하는 경우 에이전트는 기본 복제에서 제외됩니다. 즉, 컨텐츠 작성자가 복제 작업을 실행하면 사용되지 않습니다.

* **수정 시**

   이 에이전트에서는 페이지가 수정되면 자동으로 복제됩니다. Dispatcher Flush 에이전트에 주로 사용되지만 역 복제에도 사용됩니다.

* **배포 시**

   이 확인란을 선택하면 에이전트는 수정될 때 배포용으로 표시된 모든 컨텐츠를 자동으로 복제하게 됩니다.

* **온/오프타임 도달**

   그러면 페이지에 대해 정의된 시간 또는 오프타임이 발생할 때 자동 복제(페이지에 대해 적절히 활성화하거나 비활성화하기 위해)가 트리거됩니다. Dispatcher 플러시 에이전트에 주로 사용됩니다.

* **수신 시**

   이 확인란을 선택하면 에이전트는 복제 이벤트를 수신할 때마다 복제를 체인합니다.

* **상태 업데이트 없음**

   에이전트를 선택해도 복제 상태 업데이트가 강제 수행되지 않습니다.

* **버전 관리 안함**

   이 확인란을 선택하면 에이전트가 활성화된 페이지의 버전 지정을 강제 수행하지 않습니다.

## 복제 에이전트 구성 {#configuring-your-replication-agents}

MSSL을 사용하여 복제 에이전트를 게시 인스턴스에 연결하는 방법에 대한 자세한 내용은 [상호 SSL을 사용하여 복제를 참조하십시오](/help/sites-deploying/mssl-replication.md).

### 작성 환경에서 복제 에이전트 구성 {#configuring-your-replication-agents-from-the-author-environment}

작성 환경의 도구 탭에서 작성 환경(작성자의&#x200B;**에이전트**) 또는 게시 환경(게시&#x200B;**의 에이전트)에 있는 복제 에이전트를 구성할 수 있습니다**. 다음 절차는 작성 환경에 대한 에이전트의 구성을 설명하지만 두 가지 모두를 사용할 수 있습니다.

>[!NOTE]
>
>디스패처가 작성자 또는 게시 인스턴스에 대한 HTTP 요청을 처리할 때 복제 에이전트의 HTTP 요청에는 PATH 헤더가 포함되어야 합니다. 다음 절차 외에 클라이언트 헤더의 발송자 목록에 PATH 헤더를 추가해야 합니다. ( [/clientheaders(클라이언트 헤더)를 참조하십시오](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#specifying-the-http-headers-to-pass-through-clientheaders). [](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#specifying-the-http-headers-to-pass-through-clientheaders)


1. AEM의 **도구** 탭에 액세스합니다.
1. 복제 **를** 클릭합니다(폴더를 열려면 왼쪽 창).
1. 작성자의 **에이전트** (왼쪽 또는 오른쪽 창)를 두 번 클릭합니다.
1. 해당 에이전트에 대한 자세한 정보를 표시하려면 해당 에이전트 이름(링크임)을 클릭합니다.
1. 편집 **을** 클릭하여 구성 대화 상자를 엽니다.

   ![chlimage_1-22](assets/chlimage_1-22.png)

1. 제공된 값은 기본 설치에 충분해야 합니다. 변경 작업을 수행하는 경우 **확인을** 클릭하여 [저장합니다(개별 매개 변수에 대한 자세한 내용은](#replication-agents-configuration-parameters) 복제 에이전트 - 구성 매개 변수참조).

>[!NOTE]
>
>AEM의 표준 설치는 기본 복제 에이전트 내 전송 자격 증명 `admin` 의 사용자로 지정합니다.
>
>필요한 경로를 복제할 수 있는 권한이 있는 사이트별 복제 사용자 계정으로 변경해야 합니다.

### 역방향 복제 구성 {#configuring-reverse-replication}

역 복제는 게시 인스턴스에서 생성된 사용자 컨텐츠를 다시 작성자 인스턴스로 가져오는 데 사용됩니다. 일반적으로 설문 조사 및 등록 양식과 같은 기능에 사용됩니다.

보안상의 이유로 대부분의 네트워크 토폴로지는 외부 서비스를 인터넷과 같은 신뢰할 수 없는 네트워크에 노출하 *는* &quot;비무장 지대&quot;로부터의 연결을 허용하지 않습니다.

게시 환경은 일반적으로 DMZ에 있으므로 컨텐츠를 다시 작성 환경으로 가져오려면 작성 인스턴스에서 연결을 시작해야 합니다. 이 작업은 다음을 통해 수행됩니다.

* 컨텐츠가 *배치된 게시 환경의* 상자.
* 새 컨텐츠에 대해 주기적으로 게시되는 작성자 환경의 에이전트(게시)입니다.

>[!NOTE]
>
>AEM [Communities](/help/communities/overview.md)의 경우, 게시 인스턴스에서 사용자가 생성한 콘텐츠에 대한 복제가 사용되지 않습니다. 커뮤니티 [컨텐츠 저장소를 참조하십시오](/help/communities/working-with-srp.md).

이를 위해서는 다음을 수행해야 합니다.

**작성 환경의** 역방향 복제 에이전트 게시 환경의 보낸 편지함에서 정보를 수집하는 활성 구성 요소 역할을 합니다.

역방향 복제를 사용하려면 이 에이전트가 활성화되었는지 확인하십시오.

![chlimage_1-23](assets/chlimage_1-23.png)

**게시 환경의 역방향 복제 에이전트(보낼 상자)** 이것은 &quot;보낼 편지함&quot;으로 작동할 때의 수동 요소입니다. 사용자 입력은 작성자 환경의 에이전트가 수집하는 위치에서 여기에 배치됩니다.

![chlimage_1-1](assets/chlimage_1-1.jpeg)

### 여러 게시 인스턴스에 대한 복제 구성 {#configuring-replication-for-multiple-publish-instances}

>[!NOTE]
>
>콘텐트만 복제되며 사용자 데이터는 복제되지 않습니다(사용자, 사용자 그룹 및 사용자 프로필).
>
>여러 게시 인스턴스에 걸쳐 사용자 데이터를 동기화하려면 [사용자 동기화를 활성화합니다](/help/sites-administering/sync.md).

설치 시 로컬 호스트의 포트 4503에서 실행 중인 게시 인스턴스에 컨텐츠를 복제하도록 기본 에이전트가 이미 구성되었습니다.

추가 게시 인스턴스에 대한 컨텐츠 복제를 구성하려면 새 복제 에이전트를 만들고 구성해야 합니다.

1. AEM에서 **도구** 탭을 엽니다.
1. 왼쪽 **패널에서 복제**, **작성자의** 에이전트 순으로 선택합니다.
1. 새로 **만들기..**.
1. 제목 **과** **이름**&#x200B;을 설정한 다음 **복제 에이전트**&#x200B;를 선택합니다.
1. 만들기를 **클릭하여** 새 에이전트를 만듭니다.
1. 새 에이전트 항목을 두 번 클릭하여 구성 패널을 엽니다.
1. [ **편집** ] **** - [ **에이전트 설정** ] 대화 상자가 열립니다. [직렬화 유형]이 이미 [기본값]으로 정의되어 있으므로이 대화 상자가 그대로 유지됩니다.

   * 설정 **탭에서 다음을** 수행합니다.

      * 활성화 **를 참조하십시오**.
      * Enter a **Description**.
      * 재시도 **지연** 을 설정합니다 `60000`.

      * 직렬화 **유형을** 그대로 둡니다 `Default`.
   * 전송 **탭에서 다음을** 수행합니다.

      * 새 게시 인스턴스에 필요한 URI를 입력합니다. 예를 들면
         `https://localhost:4504/bin/receive`.

      * 복제에 사용되는 사이트별 사용자 계정을 입력합니다.
      * 필요에 따라 다른 매개 변수를 구성할 수 있습니다.


1. Click **OK** to save the settings.

그런 다음 작성 환경에서 페이지를 업데이트한 다음 게시하여 작업을 테스트할 수 있습니다.

업데이트는 위와 같이 구성된 모든 게시 인스턴스에 나타납니다.

문제가 발생하면 작성 인스턴스의 로그를 확인할 수 있습니다. 필요한 세부 사항 수준에 따라 위와 같이 [ **에이전트 설정] 대화 상자를** 사용하여 [ `Debug` 로그 수준 **]** 을 설정할 수도있습니다.

>[!NOTE]
>
>개별 게시 환경에 복제할 다른 컨텐츠를 선택하는 [에이전트 사용자](#agentuserid) ID와 함께 사용할 수 있습니다. 각 게시 환경의 경우:
>
>1. 해당 게시 환경에 복제할 복제 에이전트를 구성합니다.
>1. 사용자 계정 구성; 특정 게시 환경에 복제될 컨텐츠를 읽는 데 필요한 액세스 권한
>1. 사용자 계정을 복제 에이전트의 **에이전트 사용자** ID로 할당합니다.

>



### Dispatcher 플러시 에이전트 구성 {#configuring-a-dispatcher-flush-agent}

설치 시 기본 에이전트가 포함됩니다. 그러나 새 에이전트를 정의하는 경우에도 특정 구성이 여전히 필요하며 동일한 사항이 적용됩니다.

1. AEM에서 **도구** 탭을 엽니다.
1. 배포를 **클릭합니다**.
1. 복제 **를** 선택한 다음 **게시**&#x200B;시 에이전트를 선택합니다.
1. Dispatcher **플러쉬** 항목을 두 번 클릭하여 개요를 엽니다.
1. 편집을 **클릭합니다** . [ **에이전트 설정** ] 대화 상자가 열립니다.

   * 설정 **탭에서 다음을** 수행합니다.

      * 활성화 **를 참조하십시오**.
      * Enter a **Description**.
      * 직렬화 유형 **을** `Dispatcher Flush`그대로 두거나, 새 에이전트를 만드는 것처럼 설정하십시오.

      * (선택 사항) **Dispatcher에 대한 별칭 또는 별칭 경로 무효화 요청을 활성화하려면 별칭** 업데이트를 선택합니다.
   * 전송 **탭에서 다음을** 수행합니다.

      * 새 게시 인스턴스에 필요한 URI를 입력합니다. 예를 들면
         `https://localhost:80/dispatcher/invalidate.cache`.

      * 복제에 사용되는 사이트별 사용자 계정을 입력합니다.
      * 필요에 따라 다른 매개 변수를 구성할 수 있습니다.

   Dispatcher 플러시 에이전트의 경우 URI 속성은 경로 기반 가상 호스트 항목을 사용하여 팜 간 구별하는 경우에만 사용되며 이 필드를 사용하여 팜을 대상으로 하여 무효화합니다. 예를 들어, 팜 #1에는 가상 호스트가 `www.mysite.com/path1/*` 있고 팜 #2에는 가상 호스트가 `www.mysite.com/path2/*`있습니다. 의 URL을 사용하여 첫 번째 팜 `/path1/invalidate.cache` 을 타깃팅하고 두 번째 팜을 타깃팅할 `/path2/invalidate.cache` 수 있습니다.

   >[!NOTE]
   >
   >권장 기본 컨텍스트 이외의 컨텍스트에 AEM을 설치한 경우 [확장](#extended) 탭에서 **HTTP 헤더** 를 구성해야 합니다.

1. **확인**&#x200B;을 클릭하여 변경 사항을 저장합니다.
1. [ **도구** ] 탭으로 **돌아가서** DispatcherFlush **에이전트(** Publish의&#x200B;**에이전트)를 활성화할**&#x200B;수 있습니다.

작성자에서 **Dispatcher Flush** 복제 에이전트가 활성 상태가 아닙니다. 동일한 URI를 사용하여 게시 환경에서 동일한 페이지에 액세스할 수 있습니다. 예를 들면 다음과 같습니다 `https://localhost:4503/etc/replication/agents.publish/flush.html`.

### 복제 에이전트에 대한 액세스 제어 {#controlling-access-to-replication-agents}

복제 에이전트를 구성하는 데 사용되는 페이지에 대한 액세스는 노드에서 사용자 및/또는 그룹 페이지 권한을 사용하여 제어할 수 `etc/replication` 있습니다.

>[!NOTE]
>
>이러한 권한을 설정해도 사용자가 컨텐트(예: 웹 사이트 콘솔 또는 사이드 킥에서)를 복제하는 경우에는 영향을 주지 않습니다. 복제 프레임워크에서는 페이지를 복제할 때 현재 사용자의 &quot;사용자 세션&quot;을 복제 에이전트에 액세스하는 데 사용하지 않습니다.

### CRXDE Lite에서 복제 에이전트 구성 {#configuring-your-replication-agents-from-crxde-lite}

>[!NOTE]
>
>복제 에이전트 만들기는 저장소 위치에서만 `/etc/replication` 지원됩니다. 연결된 ACL을 제대로 처리하려면 이 작업이 필요합니다. 트리의 다른 위치에 복제 에이전트를 만들면 권한 없는 액세스가 발생할 수 있습니다.

CRXDE Lite를 사용하여 복제 에이전트의 다양한 매개 변수를 구성할 수 있습니다.

탐색하면 다음 세 개의 노드가 `/etc/replication` 표시됩니다.

* `agents.author`
* `agents.publish`
* `treeactivation`

두 `agents` 환경은 해당 환경에 대한 구성 정보를 보유하며 해당 환경이 실행 중일 때만 활성화됩니다. 예를 들어 게시 환경에서만 `agents.publish` 사용됩니다. 다음 스크린샷은 AEM WCM에 포함된 작성 환경의 게시 에이전트를 보여줍니다.

![chlimage_1-24](assets/chlimage_1-24.png)

## 복제 에이전트 모니터링 {#monitoring-your-replication-agents}

복제 에이전트를 모니터링하려면:

1. AEM의 **도구** 탭에 액세스합니다.
1. **복제**&#x200B;를 클릭합니다.
1. 해당 환경(왼쪽 또는 오른쪽 창)에 대한 에이전트 링크를 두 번 클릭합니다. 예: 작성자 **의 에이전트**.

   결과 창에는 대상 및 상태를 포함하여 작성 환경에 대한 모든 복제 에이전트에 대한 개요가 표시됩니다.

1. 해당 에이전트에 대한 자세한 정보를 표시하려면 해당 에이전트 이름(링크임)을 클릭합니다.

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

   여기에서 다음을 수행할 수 있습니다.

   * 에이전트가 활성화되어 있는지 확인합니다.
   * 복제 타겟을 확인합니다.
   * 복제 큐가 현재 활성 상태인지(활성화되었는지 여부)를 확인합니다.
   * 대기열에 항목이 있는지 확인합니다.
   * **큐 항목** 표시를 **업데이트하려면 새로 고침** 또는 지우기; 항목을 보고 대기열에서 나가는 것을 볼 수 있습니다.

   * **복제 에이전트가** 수행하는 모든 작업의 로그에 액세스하려면 로그 보기를 참조하십시오.
   * **대상 인스턴스에 대한 연결** 테스트를 참조하십시오.
   * **필요한 경우 모든 큐 항목에 대해 강제로 다시** 시도하십시오.

   >[!CAUTION]
   >
   >게시 인스턴스의 역방향 복제 출력 상자에 대해 &quot;연결 테스트&quot; 링크를 사용하지 마십시오.
   >
   >
   >Outbox 큐에 대한 복제 테스트가 수행되는 경우 테스트 복제보다 오래된 항목은 모든 역방향 복제를 사용하여 다시 처리됩니다.

   >이러한 항목이 이미 큐에 있는 경우 다음 XPath JCR 쿼리를 통해 찾을 수 있으므로 제거해야 합니다.
   >
   >
   >`/jcr:root/var/replication/outbox//*[@cq:repActionType='TEST']`

## 일괄 복제 {#batch-replication}

일괄 처리 복제는 개별 페이지 또는 자산을 복제하지 않지만, 시간 또는 크기를 기반으로 두 페이지의 첫 번째 임계값이 트리거되기를 기다립니다.

그런 다음 모든 복제 항목을 패키지로 팩트한 다음 게시자에게 단일 파일로 복제됩니다.

발행자는 모든 항목의 압축을 풀고 이를 저장하고 작성자에게 다시 보고합니다.

### 일괄 복제 구성 {#configuring-batch-replication}

1. 다음으로 이동:`http://serveraddress:serverport/siteadmin`
1. 화면 상단에 있는 **[!UICONTROL 도구]** 아이콘을 누릅니다.
1. 왼쪽 탐색 레일에서 작성자의 **[!UICONTROL 복제 - 에이전트]** 로 이동하고 **[!UICONTROL 기본 에이전트를 두 번 클릭합니다]**.
   * 기본 게시 복제 에이전트로 직접 이동하여 `http://serveraddress:serverport/etc/replication/agents.author/publish.html`
1. 복제 큐 **[!UICONTROL 위에 있는]** 편집 단추를 누릅니다.
1. 다음 창에서 일괄 처리 **[!UICONTROL 탭으로]** 이동합니다.
   ![일괄 복제](assets/batchreplication.png)
1. 에이전트를 구성합니다.

### 매개 변수 {#parameters}

* `[!UICONTROL Enable Batch Mode]` - 일괄 처리 복제 모드 활성화 또는 비활성화
* `[!UICONTROL Max Wait Time]` - 일괄 처리 요청이 시작될 때까지 최대 대기 시간(초)입니다. 기본값은 2초입니다.
* `[!UICONTROL Trigger Size]` - 이 크기 제한 시 일괄 복제 시작

## 추가 리소스 {#additional-resources}

문제 해결에 대한 자세한 내용은 복제 문제 해결 [페이지를](/help/sites-deploying/troubleshoot-rep.md) 참조하십시오.

자세한 내용을 보려면 Adobe는 복제와 관련된 일련의 기술 자료 문서를 보유하고 있습니다.

[https://helpx.adobe.com/experience-manager/kb/ReplicationSiblingReordering.html](https://helpx.adobe.com/experience-manager/kb/ReplicationSiblingReordering.html)https://helpx.adobe.com/experience-manager/kb/ReplicationFailureAfterNewIP.htmlhttps://helpx.adobe.com/experience-manager/kb/HowToUseReverseReplication.html[https://helpx.adobe.com/experience-manager/kb/LimitAccessToReplicationAgents.htmlhttps://helpx.adobe.com/experience-manager/kb/PagePermissionsNotReplicatedWithUser.html](https://helpx.adobe.com/experience-manager/kb/ReplicationFailureAfterNewIP.html)https://helpx.adobe.com/experience-manager/kb/CQ5ReplicateToSpecificAgents.html[https://helpx.adobe.com/experience-manager/kb/ReplicationListener.html](https://helpx.adobe.com/experience-manager/kb/LimitAccessToReplicationAgents.html)https://helpx.adobe.com/experience-manager/kb/replication-stuck.html6https://helpx.adobe.com/experience-manager/kb/replication-privileges-missing-after-upgrade-to-cq-5-5.htmlhttps://helpx.adobe.com/experience-manager/kb/CQ53UnableToCreateJobQueueDueToMaxQueues.htmlhttps://helpx.adobe.com/experience-manager/kb/ACLReplication.htmlhttps://helpx.adobe.com/experience-manager/kb/content-grow-due-reverse-replication.htmlhttps://helpx.adobe.com/experience-manager/kb/ReplicationAgentUsingAnonUser.htmlhttps://helpx.adobe.com/experience-manager/kb/ReplicationSiblingReordering.htmlhttps://helpx.adobe.com/experience-manager/kb/ReplicationFailureAfterNewIP.htmlhttps://helpx.adobe.com/experience-manager/kb/LimitAccessToReplicationAgents.htmlhttps://helpx.adobe.com/experience-manager/kb/PagePermissionsNotReplicatedWithUser.htmlhttps://helpx.adobe.com/experience-manager/kb/HowToUseReverseReplication.htmlhttps://helpx.adobe.com/experience-manager/kb/CQ5ReplicateToSpecificAgents.htmlhttps://helpx.adobe.com/experience-manager/kb/ReplicationListener.htmlhttps://helpx.adobe.com/experience-manager/kb/replication-stuck.htmlhttps://helpx.adobe.com/experience-manager/kb/replication-privileges-missing-after-upgrade-to-cq-5-5.htmlhttps://helpx.adobe.com/experience-manager/kb/CQ53UnableToCreateJobQueueDueToMaxQueues.htmlhttps://helpx.adobe.com/experience-manager/kb/ACLReplication.htmlhttps://helpx.adobe.com/experience-manager/kb/content-grow-due-reverse-replication.htmlhttps://helpx.adobe.com/experience-manager/kb/ReplicationAgentUsingAnonUser.html[](https://helpx.adobe.com/experience-manager/kb/PagePermissionsNotReplicatedWithUser.html)[](https://helpx.adobe.com/experience-manager/kb/HowToUseReverseReplication.html)[](https://helpx.adobe.com/experience-manager/kb/CQ5ReplicateToSpecificAgents.html)이이이이이이이이이이이이이이이이이이이이이이이이을이이이이이이을이이이이이이이이이이이[이이이이이이이을이이이이이이이이](https://helpx.adobe.com/experience-manager/kb/ReplicationListener.html)이[](https://helpx.adobe.com/experience-manager/kb/replication-stuck.html)[](https://helpx.adobe.com/experience-manager/kb/replication-privileges-missing-after-upgrade-to-cq-5-5.html)[](https://helpx.adobe.com/experience-manager/kb/CQ53UnableToCreateJobQueueDueToMaxQueues.html)[](https://helpx.adobe.com/experience-manager/kb/ACLReplication.html)[](https://helpx.adobe.com/experience-manager/kb/content-grow-due-reverse-replication.html)[](https://helpx.adobe.com/experience-manager/kb/ReplicationAgentUsingAnonUser.html)이이이이