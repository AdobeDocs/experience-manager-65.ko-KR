---
title: Security 검사 목록
seo-title: Security Checklist
description: AEM을 구성 및 배포할 때 발생하는 다양한 보안 고려 사항에 대해 알아봅니다.
seo-description: Learn about the various security considerations when configuring and deploying AEM.
uuid: 8e293316-4177-4271-87c6-9dc1a2e85a07
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: de7d7209-c194-4d19-853b-468ebf3fa4b2
docset: aem65
exl-id: 314a6409-398c-470b-8799-0c4e6f745141
feature: Security
source-git-commit: f60d3049b10a8ec500dd0cd4b1b5d4efbe415d84
workflow-type: tm+mt
source-wordcount: '2859'
ht-degree: 4%

---

# Security 검사 목록 {#security-checklist}

이 섹션에서는 배포 시 AEM 설치가 안전한지 확인하는 데 수행해야 하는 다양한 단계를 다룹니다. 검사 목록은 위쪽에서 아래쪽으로 적용하기 위한 것입니다.

>[!NOTE]
>
>[OWASP(Open Web Application Security Project)](https://owasp.org/www-project-top-ten/)에서 게시한 가장 위험한 보안 위협에 대한 정보도 확인할 수 있습니다.

>[!NOTE]
>
>개발 단계에서 적용할 수 있는 추가 [보안 고려 사항](/help/sites-developing/dev-guidelines-bestpractices.md#security-considerations)이 있습니다.

## 주요 보안 조치 {#main-security-measures}

### 프로덕션 준비 모드에서 AEM 실행 {#run-aem-in-production-ready-mode}

자세한 내용은 [프로덕션 준비 모드에서 AEM 실행](/help/sites-administering/production-ready.md)을 참조하십시오.

### 전송 계층 보안을 위해 HTTPS 활성화 {#enable-https-for-transport-layer-security}

보안 인스턴스가 있으려면 작성자 및 게시 인스턴스 모두에서 HTTPS 전송 계층을 활성화해야 합니다.

>[!NOTE]
>
>자세한 내용은 [SSL을 통해 HTTP 활성화](/help/sites-administering/ssl-by-default.md) 섹션을 참조하십시오.

### 보안 핫픽스 설치 {#install-security-hotfixes}

Adobe](https://helpx.adobe.com/kr/experience-manager/kb/aem63-available-hotfixes.html)에서 제공하는 최신 [보안 핫픽스를 설치했는지 확인합니다.

### AEM 및 OSGi 콘솔 관리 계정에 대한 기본 암호 변경 {#change-default-passwords-for-the-aem-and-osgi-console-admin-accounts}

Adobe은 설치 후 권한 있는 [**AEM** `admin` 계정](#changing-the-aem-admin-password)(모든 인스턴스에서)에 대한 암호를 변경할 것을 강력히 권장합니다.

이러한 계정은 다음과 같습니다.

* AEM `admin` 계정

   AEM 관리자 계정의 암호를 변경한 경우 CRX에 액세스할 때 새 암호를 사용해야 합니다.

* OSGi 웹 콘솔의 `admin` 암호

   이 변경 사항은 웹 콘솔에 액세스하는 데 사용되는 관리 계정에도 적용되므로, 이 계정에 액세스할 때 동일한 암호를 사용해야 합니다.

이 두 계정은 별도의 자격 증명을 사용하고 각 계정을 위한 강력한 암호를 가지는 것이 안전한 배포를 위해 중요합니다.

#### AEM 관리자 암호 변경 {#changing-the-aem-admin-password}

AEM 관리자 계정의 암호는 [Granite Operations - Users](/help/sites-administering/granite-user-group-admin.md) 콘솔을 통해 변경할 수 있습니다.

여기서 `admin` 계정을 편집하고 [암호를 변경할 수 있습니다](/help/sites-administering/granite-user-group-admin.md#changing-the-password-for-an-existing-user).

>[!NOTE]
>
>관리 계정을 변경하면 OSGi 웹 콘솔 계정도 변경됩니다. 관리 계정을 변경한 후에는 OSGi 계정을 다른 계정으로 변경해야 합니다.

#### OSGi 웹 콘솔 암호 변경의 중요성 {#importance-of-changing-the-osgi-web-console-password}

AEM `admin` 계정 외에, OSGi 웹 콘솔 암호의 기본 암호를 변경하지 않으면 다음 오류가 발생할 수 있습니다.

* 시작 및 종료 중에 기본 암호가 있는 서버 노출(대규모 서버의 경우 몇 분 정도 걸릴 수 있음);
* 저장소가 다운되거나 다시 시작되는 경우 번들이 실행되고 OSGI가 실행 중일 때 서버가 노출됩니다.

웹 콘솔 암호 변경에 대한 자세한 내용은 아래의 [OSGi 웹 콘솔 관리자 암호 변경](/help/sites-administering/security-checklist.md#changing-the-osgi-web-console-admin-password)을 참조하십시오.

#### OSGi 웹 콘솔 관리자 암호 변경 {#changing-the-osgi-web-console-admin-password}

웹 콘솔에 액세스하는 데 사용되는 암호도 변경해야 합니다. 이 작업은 [Apache Felix OSGi Management Console](/help/sites-deploying/osgi-configuration-settings.md)의 다음 속성을 구성하여 수행합니다.

**Apache** Felix  **Web Management Console 자체에 액세스하기 위한 자격 증명인 사용자 이름 및 암호**.
인스턴스의 보안을 위해서는 초기 설치 후 암호를 변경해야 합니다.

이를 위해 진행되는 작업:

1. `<server>:<port>/system/console/configMgr`에서 웹 콘솔로 이동합니다.
1. **Apache Felix OSGi Management Console**&#x200B;로 이동하여 **사용자 이름** 및 **암호**&#x200B;를 변경합니다.

   ![chlimage_1-3](assets/chlimage_1-3.png)

1. **저장**&#x200B;을 클릭합니다.

### 사용자 지정 오류 처리기 구현 {#implement-custom-error-handler}

Adobe은 정보 공개를 방지하기 위해 특히 404 및 500 HTTP 응답 코드에 대한 사용자 지정 오류 처리기 페이지를 정의할 것을 권장합니다.

>[!NOTE]
>
>자세한 내용은 [사용자 지정 스크립트나 오류 핸들러](https://helpx.adobe.com/experience-manager/kb/CustomErrorHandling.html) 기술 자료 문서를 작성하는 방법 을 참조하십시오.

### Dispatcher 보안 검사 목록 완료 {#complete-dispatcher-security-checklist}

AEM Dispatcher는 인프라의 중요한 부분입니다. Adobe은 [dispatcher 보안 검사 목록](https://helpx.adobe.com/kr/experience-manager/dispatcher/using/security-checklist.html)을 완료하는 것이 좋습니다.

>[!CAUTION]
>
>Dispatcher를 사용하여 &quot;.form&quot; 선택기를 비활성화해야 합니다.

## 확인 단계 {#verification-steps}

### 복제 및 전송 사용자 구성 {#configure-replication-and-transport-users}

AEM의 표준 설치에서는 `admin`을 기본 [복제 에이전트](/help/sites-deploying/replication.md) 내에서 전송 자격 증명을 위한 사용자로 지정합니다. 또한 관리자 사용자는 작성자 시스템에서 복제를 소스 지정하는 데 사용됩니다.

보안 고려 사항의 경우, 다음 두 가지 측면을 모두 염두에 두고 특정 사용 사례를 반영하도록 변경해야 합니다.

* **전송 사용자**&#x200B;는 관리 사용자가 아니어야 합니다. 대신, 게시 시스템의 관련 부분에 대한 액세스 권한만 가진 게시 시스템에서 사용자를 설정하고 해당 사용자의 자격 증명을 사용하여 전송에 사용하십시오.

   번들로 제공되는 복제 수신자 사용자부터 시작하여 사용자의 상황에 맞게 이 사용자의 액세스 권한을 구성할 수 있습니다

* **복제 사용자** 또는 **에이전트 사용자 ID**&#x200B;도 관리 사용자가 아니어야 하며, 복제되어야 하는 컨텐츠만 볼 수 있는 사용자여야 합니다. 복제 사용자는 게시자에게 전송되기 전에 작성자 시스템에서 복제될 컨텐츠를 수집하는 데 사용됩니다.

### 작업 대시보드 보안 상태 확인을 선택합니다. {#check-the-operations-dashboard-security-health-checks}

AEM 6에서는 시스템 운영자가 문제 해결 및 인스턴스의 상태를 모니터링하는 데 도움이 되는 새로운 작업 대시보드를 도입합니다.

대시보드에는 보안 상태 점검 컬렉션도 포함되어 있습니다. 프로덕션 인스턴스로 전환하기 전에 모든 보안 상태 확인의 상태를 확인하는 것이 좋습니다. 자세한 내용은 [작업 대시보드 설명서](/help/sites-administering/operations-dashboard.md)를 참조하십시오.

### 예제 컨텐츠가 있는지 확인 {#check-if-example-content-is-present}

모든 예제 컨텐츠 및 사용자(예: Geometrixx 프로젝트 및 해당 구성 요소)는 공개적으로 액세스할 수 있도록 하기 전에 프로덕션 시스템에서 완전히 제거하고 삭제해야 합니다.

>[!NOTE]
>
>이 인스턴스가 [프로덕션 준비 모드](/help/sites-administering/production-ready.md)에서 실행 중인 경우 샘플 We.Retail 애플리케이션이 제거됩니다. 어떤 이유로든 이런 경우가 아닌 경우 패키지 관리자로 이동한 다음 모든 We.Retail 패키지를 검색하여 제거하여 샘플 컨텐츠를 제거할 수 있습니다. 자세한 내용은 [패키지 작업](package-manager.md)을 참조하십시오.

### CRX 개발 번들이 있는지 확인합니다 {#check-if-the-crx-development-bundles-are-present}

이러한 개발 OSGi 번들을 액세스 가능하게 하기 전에 작성자와 게시 생산적인 시스템 모두에서 제거해야 합니다.

* Adobe CRXDE 지원(com.adobe.granite.crxde-support)
* Adobe Granite CRX Explorer(com.adobe.granite.crx-explorer)
* Adobe Granite CRXDE Lite(com.adobe.granite.crxde-lite)

### Sling 개발 번들이 있는지 확인합니다 {#check-if-the-sling-development-bundle-is-present}

[AEM Developer Tools for Eclipse](/help/sites-developing/aem-eclipse.md)에서 Apache Sling Tools 지원 설치(org.apache.sling.tooling.support.install)를 배포합니다.

이 OSGi 번들을 액세스 가능하게 하기 전에 작성자 및 게시 생산적인 시스템 모두에서 제거해야 합니다.

### Protect, 사이트 간 요청 위조 방지 {#protect-against-cross-site-request-forgery}

#### CSRF 보호 프레임워크 {#the-csrf-protection-framework}

AEM 6.1은 **CSRF 보호 프레임워크**&#x200B;라고 하는 사이트 간 요청 위조 공격으로부터 보호하는 메커니즘을 제공합니다. 사용 방법에 대한 자세한 내용은 [설명서](/help/sites-developing/csrf-protection.md)를 참조하십시오.

#### Sling 레퍼러 필터 {#the-sling-referrer-filter}

CRX WebDAV 및 Apache Sling에서 CSRF(교차 사이트 요청 위조) 관련 알려진 보안 문제를 해결하려면 레퍼러 필터에 대한 구성을 추가해야 합니다.

레퍼러 필터 서비스는 다음을 구성할 수 있는 OSGi 서비스입니다.

* 필터링해야 하는 http 메서드
* 빈 레퍼러 헤더가 허용되는지 여부
* 서버 호스트 외에 허용되는 서버 목록입니다.

   기본적으로 로컬 호스트의 모든 변형과 서버가 바인딩된 현재 호스트 이름이 목록에 있습니다.

레퍼러 필터 서비스를 구성하려면:

1. 다음 위치에서 Apache Felix 콘솔(**구성**)을 엽니다.

   `https://<server>:<port_number>/system/console/configMgr`

1. `admin`(으)로 로그인합니다.
1. **구성** 메뉴에서 다음을 선택합니다.

   `Apache Sling Referrer Filter`

1. `Allow Hosts` 필드에 레퍼러로 허용되는 모든 호스트를 입력합니다. 각 항목은 형식이어야 합니다

   &lt;protocol>://&lt;server>:&lt;port>

   예:

   * `https://allowed.server:80` 지정된 포트를 사용하여 이 서버의 모든 요청을 허용합니다.
   * https 요청도 허용하려면 두 번째 줄을 입력해야 합니다.
   * 해당 서버의 모든 포트를 허용하는 경우 `0` 을 포트 번호로 사용할 수 있습니다.

1. 빈/누락된 레퍼러 헤더를 허용하려면 `Allow Empty` 필드를 선택합니다.

   >[!CAUTION]
   >
   >시스템이 CSRF 공격에 노출될 수 있으므로 빈 값을 허용하는 대신 `cURL` 등의 명령줄 도구를 사용하는 동안 레퍼러를 제공하는 것이 좋습니다.

1. 이 필터가 `Filter Methods` 필드를 사용하여 확인하는 데 사용해야 하는 방법을 편집합니다.

1. **저장**&#x200B;을 클릭하여 변경 내용을 저장합니다.

### OSGI 설정 {#osgi-settings}

일부 OSGI 설정은 응용 프로그램을 쉽게 디버깅할 수 있도록 기본적으로 설정되어 있습니다. 내부 정보가 공개로 누설되지 않도록 게시 및 작성 생산적인 인스턴스에서 이러한 작업을 변경해야 합니다.

>[!NOTE]
>
>**Day CQ WCM Debug 필터**&#x200B;를 제외한 아래의 모든 설정은 [프로덕션 준비 모드](/help/sites-administering/production-ready.md)에서 자동으로 다룹니다. 따라서 프로덕션 환경에서 인스턴스를 배포하기 전에 모든 설정을 검토하는 것이 좋습니다.

다음 각 서비스에 대해 지정된 설정을 변경해야 합니다.

* [Adobe Granite HTML 라이브러리 관리자](/help/sites-deploying/osgi-configuration-settings.md#day-cq-html-library-manager):

   * **Minify**(CRLF 및 공백 문자를 제거하려면) 활성화합니다.
   * **Gzip**&#x200B;을 활성화합니다(하나의 요청으로 파일을 압축하고 액세스할 수 있도록 허용).
   * **Debug** 비활성화
   * **타이밍** 비활성화

* [일 CQ WCM 디버그 필터](/help/sites-deploying/osgi-configuration-settings.md#day-cq-wcm-debug-filter):

   * **Enable** 선택 취소

* [일 CQ WCM 필터](/help/sites-deploying/osgi-configuration-settings.md):

   * 게시 전용 시 **WCM Mode**&#x200B;를 &quot;disabled&quot;로 설정합니다.

* [Apache Sling Java Script 핸들러](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-javascript-handler):

   * 비활성화 **디버그 정보 생성**

* [Apache Sling JSP 스크립트 핸들러](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-jsp-script-handler):

   * 비활성화 **디버그 정보 생성**
   * **매핑된 콘텐츠 비활성화**

자세한 내용은 [OSGi 구성 설정](/help/sites-deploying/osgi-configuration-settings.md)을 참조하십시오.

AEM을 사용하여 작업하는 경우 이러한 서비스에 대한 구성 설정을 관리하는 방법에는 몇 가지가 있습니다. 자세한 내용 및 권장 방법은 [OSGi](/help/sites-deploying/configuring-osgi.md) 구성 을 참조하십시오.

## 추가 읽기 {#further-readings}

### DoS(서비스 거부) 공격 완화 {#mitigate-denial-of-service-dos-attacks}

서비스 거부(DoS) 공격은 의도한 사용자가 컴퓨터 리소스를 사용할 수 없게 하려고 시도하는 것입니다. 이 작업은 종종 리소스를 오버로드하여 수행됩니다. 예:

* 외부 소스의 요청이 쇄도하고
* 추가 정보 요청이 있으면 시스템이 성공적으로 전달할 수 있습니다.

   예를 들어 전체 리포지토리의 JSON 표현입니다.

* URL은 URL이 무제한으로 포함된 컨텐츠 페이지를 요청하여 핸들, 일부 선택기, 확장 및 접미사를 포함할 수 있으며 이 모든 것은 수정할 수 있습니다.

   예를 들어 `.../en.html`은 다음과 같이 요청할 수 있습니다.

   * `.../en.ExtensionDosAttack`
   * `.../en.SelectorDosAttack.html`
   * `.../en.html/SuffixDosAttack`

   유효한 모든 변형(예: `200` 응답을 반환하고 캐시되도록 구성된)은 Dispatcher에 의해 캐시되므로 결국 전체 파일 시스템이 되고 추가 요청에 대한 서비스가 없습니다.

이러한 공격을 방지하기 위한 구성 요소는 다양하며, 여기서는 AEM과 직접적으로 관련된 사항만 설명합니다.

**DoS를 방지하기 위한 Sling 구성**

Sling은 *컨텐츠 중심의*&#x200B;입니다. 즉, 각(HTTP) 요청이 JCR 리소스(저장소 노드) 형식의 컨텐츠에 매핑될 때 처리에 중점을 둡니다.

* 첫 번째 타겟은 컨텐츠를 포함하는 리소스(JCR 노드)입니다.
* 둘째, 렌더러 또는 스크립트는 요청의 특정 부분(예: 선택기 및/또는 확장)과 함께 리소스 속성에서 위치합니다.

>[!NOTE]
>
>이 내용은 [Sling 요청 처리](/help/sites-developing/the-basics.md#sling-request-processing)에서 자세히 다룹니다.

이 접근 방식을 통해 Sling은 매우 강력하고 유연하지만, 항상 신중하게 관리해야 하는 유연성이 있습니다.

DoS 오용을 방지하려면 다음을 수행할 수 있습니다.

1. 애플리케이션 수준에서 컨트롤 통합 가능한 변형 수로 인해 기본 구성이 불가능합니다.

   애플리케이션에서 다음을 수행해야 합니다.

   * *만 필요한 명시적 선택기를 제공하고 다른 모든 선택기에 `404`만 반환하도록 애플리케이션에서 선택기를 제어합니다.*
   * 무제한의 컨텐츠 노드 출력을 방지합니다.

1. 기본 렌더러의 구성을 확인합니다. 이 경우 문제가 발생할 수 있습니다.

   * 특히 트리 구조를 여러 수준으로 가로지를 수 있는 JSON 렌더러입니다.

      예를 들어, 요청:

      `http://localhost:4502/.json`

      전체 저장소를 JSON 표현으로 덤프할 수 있습니다. 이로 인해 심각한 서버 문제가 발생합니다. 이러한 이유로 Sling은 최대 결과 수에 제한을 설정합니다. JSON 렌더링 깊이를 제한하려면 다음 항목에 대한 값을 설정할 수 있습니다.

      **JSON 최대 결과** (  `json.maximumresults`)

      [Apache Sling GET 서블릿](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-get-servlet)에 대한 구성에서 다음을 수행합니다. 이 제한을 초과하면 렌더링이 축소됩니다. AEM 내의 Sling에 대한 기본값은 `1000`입니다.

   * 예방 조치로 다른 기본 렌더러(HTML, 일반 텍스트, XML)를 비활성화합니다. 다시 [Apache Sling GET 서블릿](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-get-servlet)을 구성하여
   >[!CAUTION]
   >
   >JSON 렌더러를 비활성화하지 마십시오. 이 렌더러는 AEM의 일반적인 작업에 필요합니다.

1. 인스턴스에 대한 액세스를 필터링하려면 방화벽을 사용하십시오.

   * 보호되지 않은 상태로 서비스 거부 공격을 초래할 수 있는 인스턴스 포인트에 대한 액세스를 필터링하려면 운영 체제 수준 방화벽을 사용해야 합니다.

**양식 선택기를 사용한 DoS에 대한 완화**

>[!NOTE]
>
>이러한 완화는 Forms을 사용하지 않는 AEM 환경에서만 수행해야 합니다.

AEM은 `FormChooserServlet`에 대한 기본 인덱스를 제공하지 않으므로 쿼리의 양식 선택기를 사용하면 비용이 많이 드는 저장소 순회가 트리거되며, 일반적으로 AEM 인스턴스를 중단합니다. 양식 선택기는 **&amp;ast;.form이 있어도 감지할 수 있습니다.쿼리의 &amp;ast;** 문자열.

이를 완화하려면 아래 단계를 수행하십시오.

1. 브라우저를 *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*&#x200B;로 이동하여 웹 콘솔로 이동합니다.

1. **일 CQ WCM 양식 선택기 서블릿**&#x200B;을 검색합니다.
1. 항목을 클릭한 후 다음 창에서 **고급 검색 필요**&#x200B;를 비활성화합니다.

1. **저장**&#x200B;을 클릭합니다.

**자산 다운로드 서블릿으로 인한 DoS에 대한 완화**

기본 자산 다운로드 서블릿을 사용하면 인증된 사용자가 임의로 크기가 큰 동시 다운로드 요청을 발행하여 자산의 ZIP 파일을 만들 수 있습니다. 큰 ZIP 아카이브를 만들면 서버와 네트워크에 과부하가 발생할 수 있습니다. 이 동작으로 인한 잠재적 서비스 거부(DoS) 위험을 완화하려면 `AssetDownloadServlet` 게시 인스턴스에서 기본적으로 [!DNL Experience Manager] OSGi 구성 요소를 사용할 수 없습니다. 기본적으로 [!DNL Experience Manager] 작성자 인스턴스에서 활성화됩니다.

다운로드 기능이 필요하지 않으면 작성자 및 게시 배포의 서블릿을 비활성화합니다. 설치 프로그램에서 자산 다운로드 기능이 활성화되어 있어야 하는 경우 자세한 내용은 [이 문서](/help/assets/download-assets-from-aem.md)를 참조하십시오. 배포에서 지원할 수 있는 최대 다운로드 제한을 정의할 수도 있습니다.

### WebDAV 사용 안 함 {#disable-webdav}

작성 환경과 게시 환경 모두에서 WebDAV를 사용하지 않도록 설정해야 합니다. 이 작업은 적절한 OSGi 번들을 중지하여 수행할 수 있습니다.

1. 다음에 실행되는 **Felix Management Console**&#x200B;에 연결합니다.

   `https://<*host*>:<*port*>/system/console`

   예 `http://localhost:4503/system/console/bundles`.

1. 번들 목록에서 이름이 인 번들을 찾습니다.

   `Apache Sling Simple WebDAV Access to repositories (org.apache.sling.jcr.webdav)`

1. 작업 열에서 중지 단추를 클릭하여 이 번들을 중지합니다.

1. 번들 목록에서 이름이 인 번들을 다시 찾습니다.

   `Apache Sling DavEx Access to repositories (org.apache.sling.jcr.davex)`

1. 이 번들을 중지하려면 중지 단추를 클릭하십시오.

   >[!NOTE]
   >
   >AEM을 다시 시작할 필요가 없습니다.

### 사용자 홈 경로에서 개인 식별 정보를 공개하지 않는지 확인합니다. {#verify-that-you-are-not-disclosing-personally-identifiable-information-in-the-users-home-path}

리포지토리 사용자 홈 경로에 개인 식별 정보가 표시되지 않도록 하여 사용자를 보호하는 것이 중요합니다.

AEM 6.1 이후, 사용자(인증 가능)라고도 하는 ID 노드 이름이 저장되는 방법은 `AuthorizableNodeName` 인터페이스의 새로운 구현으로 변경됩니다. 새 인터페이스는 더 이상 노드 이름에 사용자 ID를 표시하지 않고 대신 임의 이름을 생성합니다.

이제 AEM에서 작성 가능한 ID를 생성하는 기본 방법이므로 이를 활성화하기 위해 구성을 수행할 필요가 없습니다.

권장되지는 않지만, 기존 애플리케이션과의 이전 호환성을 위해 이전 구현이 필요한 경우 비활성화할 수 있습니다. 이를 수행하려면 다음을 수행해야 합니다.

1. 웹 콘솔로 이동하고 **Apache Jackrabbit Oak SecurityProvider**&#x200B;의 속성 **requiredServicePids**&#x200B;에서 ** org.apache.jackrabbit.oak.security.user.RandomAuthorizableNodeName** 항목을 제거합니다.

   OSGi 구성에서 **org.apache.jackrabbit.oak.security.internal.SecurityProviderRegistration** PID를 검색하여 Oak 보안 공급자를 찾을 수도 있습니다.

1. 웹 콘솔에서 **Apache Jackrabbit Oak Random Authorizable 노드 이름** OSGi 구성을 삭제합니다.

   쉽게 조회할 수 있도록 이 구성에 대한 PID는 **org.apache.jackrabbit.oak.security.user.RandomAuthorizableNodeName**&#x200B;입니다.

>[!NOTE]
>
>자세한 내용은 [인가 가능한 노드 이름 생성](https://jackrabbit.apache.org/oak/docs/security/user/authorizablenodename.html)의 Oak 설명서를 참조하십시오.

### 클릭재킹 방지 {#prevent-clickjacking}

클릭재킹을 방지하려면 `SAMEORIGIN`으로 설정된 `X-FRAME-OPTIONS` HTTP 헤더를 제공하도록 웹 서버를 구성하는 것이 좋습니다.

[클릭재킹에 대한 자세한 내용은 OWASP 사이트를 참조하십시오](https://www.owasp.org/index.php/Clickjacking).

### 필요한 경우 암호화 키를 올바르게 복제해야 합니다. {#make-sure-you-properly-replicate-encryption-keys-when-needed}

특정 AEM 기능 및 인증 체계를 사용하려면 모든 AEM 인스턴스에 대해 암호화 키를 복제해야 합니다.

이렇게 하기 전에 키 복제가 버전 간에 다르게 수행됩니다. 키 저장 방식이 6.3과 이전 버전 간에 다르기 때문입니다.

자세한 내용은 아래를 참조하십시오.

#### AEM 6.3용 키 복제 {#replicating-keys-for-aem}

반면 이전 버전에서는 복제 키가 저장소에 저장되었으며 AEM 6.3부터 파일 시스템에 저장됩니다.

따라서 인스턴스 간에 키를 복제하려면 소스 인스턴스에서 파일 시스템의 타겟 인스턴스 위치로 키를 복사해야 합니다.

특히 다음을 수행해야 합니다.

1. 복사할 주요 자료가 포함된 AEM 인스턴스(일반적으로 작성자 인스턴스)에 액세스합니다.
1. 로컬 파일 시스템에서 com.adobe.granite.crypto.file 번들을 찾습니다. 예를 들어, 이 경로 아래에서:

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`

   각 폴더 내의 `bundle.info` 파일은 번들 이름을 식별합니다.

1. 데이터 폴더로 이동합니다. 예:

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. HMAC 및 마스터 파일을 복사합니다.
1. 그런 다음 HMAC 키를 복제할 대상 인스턴스로 이동하여 데이터 폴더로 이동합니다. 예:

   * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. 이전에 복사한 두 파일을 붙여넣습니다.
1. [대상 인스턴스가 ](/help/communities/deploy-communities.md#refresh-the-granite-crypto-bundle) 이미 실행 중인 경우 Crypto 번들을 새로 고칩니다.
1. 키를 복제할 모든 인스턴스에 대해 위의 단계를 반복합니다.

>[!NOTE]
>
>AEM을 처음 설치할 때 아래 매개 변수를 추가하여 키를 저장하는 6.3 이전 방법으로 되돌릴 수 있습니다.
>
>`-Dcom.adobe.granite.crypto.file.disable=true`

#### AEM 6.2 및 이전 버전에 대한 키 복제 {#replicating-keys-for-aem-and-older-versions}

AEM 6.2 및 이전 버전에서 키는 `/etc/key` 노드 아래의 저장소에 저장됩니다.

인스턴스 간에 키를 안전하게 복제하는 데 권장되는 방법은 이 노드만 복제하는 것입니다. CRXDE Lite을 통해 노드를 선택적으로 복제할 수 있습니다.

1. *https://&lt;serveraddress>:4502/crx/de/index.jsp*&#x200B;로 이동하여 CRXDE Lite을 엽니다.
1. `/etc/key` 노드를 선택합니다.
1. **복제** 탭으로 이동합니다.
1. **복제** 단추를 누릅니다.

### 침투 테스트 수행 {#perform-a-penetration-test}

Adobe는 프로덕션을 시작하기 전에 AEM 인프라에 대한 침투 테스트를 수행할 것을 강력히 권장합니다.

### 개발 우수 사례 {#development-best-practices}

AEM 환경을 안전하게 유지하기 위해 새로운 개발이 [보안 우수 사례](/help/sites-developing/security.md)에 따라 수행되어야 합니다.
