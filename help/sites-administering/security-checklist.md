---
title: 보안 검사 목록
description: AEM을 구성하고 배포할 때 고려해야 할 다양한 보안 사항에 대해 알아봅니다.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
docset: aem65
exl-id: 314a6409-398c-470b-8799-0c4e6f745141
feature: Security
solution: Experience Manager, Experience Manager Sites
role: Admin,Developer
source-git-commit: f30decf0e32a520dcda04b89c5c1f5b67ab6e028
workflow-type: tm+mt
source-wordcount: '2959'
ht-degree: 1%

---

# 보안 검사 목록 {#security-checklist}

이 섹션에서는 배포 시 AEM 설치가 안전한지 확인하기 위해 수행해야 하는 다양한 단계를 다룹니다. 체크리스트는 처음부터 끝까지 적용됩니다.

>[!NOTE]
>
>[Open Web Application Security Project(OWASP)](https://owasp.org/www-project-top-ten/)에서 게시한 가장 위험한 보안 위협에 대한 추가 정보도 제공합니다.

>[!NOTE]
>
>개발 단계에서 적용할 수 있는 몇 가지 추가 [보안 고려 사항](/help/sites-developing/dev-guidelines-bestpractices.md#security-considerations)이 있습니다.

## 주요 보안 조치 {#main-security-measures}

### 프로덕션 준비 모드에서 AEM 실행 {#run-aem-in-production-ready-mode}

자세한 내용은 [프로덕션 준비 모드에서 AEM 실행](/help/sites-administering/production-ready.md)을 참조하십시오.

### 전송 계층 보안을 위해 HTTPS 활성화 {#enable-https-for-transport-layer-security}

보안 인스턴스가 있는 경우 작성자 및 게시 인스턴스 모두에서 HTTPS 전송 레이어를 활성화해야 합니다.

>[!NOTE]
>
>자세한 내용은 [SSL을 통한 HTTP 사용](/help/sites-administering/ssl-by-default.md) 섹션을 참조하십시오.

### 보안 핫픽스 설치 {#install-security-hotfixes}

Adobe[&#128279;](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=ko)에서 제공한 최신 보안 핫픽스를 설치했는지 확인하십시오.

### AEM 및 OSGi 콘솔 관리자 계정에 대한 기본 암호 변경 {#change-default-passwords-for-the-aem-and-osgi-console-admin-accounts}

Adobe은 설치 후 권한이 있는 [**AEM** `admin` 계정](#changing-the-aem-admin-password)(모든 인스턴스에서)의 암호를 변경할 것을 권장합니다.

이러한 계정에는 다음이 포함됩니다.

* AEM `admin` 계정

  AEM 관리자 계정의 암호를 변경한 후 CRX에 액세스할 때 새 암호를 사용하십시오.

* OSGi 웹 콘솔의 `admin` 암호

  이 변경 사항은 웹 콘솔에 액세스하는 데 사용되는 관리 계정에도 적용되므로 액세스할 때 동일한 암호를 사용하십시오.

이 두 계정은 별도의 자격 증명을 사용하며, 각각에 대해 고유하고 강력한 암호를 갖는 것이 보안 배포에 필수적입니다.

#### AEM 관리자 암호 변경 {#changing-the-aem-admin-password}

AEM 관리자 계정의 암호는 [Granite 작업 - 사용자](/help/sites-administering/granite-user-group-admin.md) 콘솔을 통해 변경할 수 있습니다.

여기에서 `admin` 계정을 편집하고 [암호를 변경](/help/sites-administering/granite-user-group-admin.md#changing-the-password-for-an-existing-user)할 수 있습니다.

>[!NOTE]
>
>관리자 계정을 변경하면 OSGi 웹 콘솔 계정도 변경됩니다. 관리자 계정을 변경한 후 OSGi 계정을 다른 계정으로 변경해야 합니다.

#### OSGi 웹 콘솔 암호 변경의 중요성 {#importance-of-changing-the-osgi-web-console-password}

AEM `admin` 계정 외에 OSGi 웹 콘솔 암호에 대한 기본 암호를 변경하지 않으면 다음과 같은 결과가 발생할 수 있습니다.

* 시작 및 종료 시 기본 암호가 있는 서버 노출(대형 서버의 경우 몇 분 정도 소요될 수 있음)
* 저장소 중단/재시작 번들 및 OSGI가 실행 중인 경우의 서버 노출.

웹 콘솔 암호 변경에 대한 자세한 내용은 아래의 [OSGi 웹 콘솔 관리자 암호 변경](/help/sites-administering/security-checklist.md#changing-the-osgi-web-console-admin-password)을 참조하십시오.

#### OSGi 웹 콘솔 관리자 암호 변경 {#changing-the-osgi-web-console-admin-password}

웹 콘솔에 액세스하는 데 사용되는 암호를 변경합니다. [OSGI 구성](/help/sites-deploying/configuring-osgi.md)을 사용하여 **Apache Felix OSGi 관리 콘솔**&#x200B;의 다음 속성을 업데이트합니다.

* Apache Felix 웹 관리 콘솔 자체에 액세스하기 위한 자격 증명인 **사용자 이름** 및 **암호**.
인스턴스의 보안을 유지하려면 초기 설치 후 *후*&#x200B;에 암호를 변경해야 합니다.

>[!NOTE]
>
>OSGi 설정 구성에 대한 자세한 내용은 [OSGI 구성](/help/sites-deploying/configuring-osgi.md)을 참조하십시오.

**OSGi 웹 콘솔 관리자 암호를 변경하려면**:

1. **도구**, **작업** 메뉴를 사용하여 **웹 콘솔**&#x200B;을 열고 **구성** 섹션으로 이동합니다.
예: `<server>:<port>/system/console/configMgr`.
1. **Apache Felix OSGi 관리 콘솔**&#x200B;의 항목으로 이동하여 엽니다.
1. **사용자 이름** 및 **암호**&#x200B;를 변경합니다.

   ![chlimage_1-3](assets/chlimage_1-3.png)

1. **저장**&#x200B;을 선택합니다.

### 사용자 지정 오류 처리기 구현 {#implement-custom-error-handler}

Adobe은 특히 404 및 500 HTTP 응답 코드에 대해 사용자 지정 오류 처리기 페이지를 정의하여 정보 공개를 방지할 것을 권장합니다.

>[!NOTE]
>
>자세한 내용은 [사용자 지정 스크립트나 오류 처리기를 만드는 방법](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/full-stack/custom-error-page.html?lang=ko)을 참조하세요.

### Dispatcher 보안 검사 목록 완료 {#complete-dispatcher-security-checklist}

AEM Dispatcher은 인프라의 중요한 부분입니다. Adobe은 [Dispatcher 보안 검사 목록](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/security-checklist.html?lang=ko)을 완료할 것을 권장합니다.

>[!CAUTION]
>
>Dispatcher을 사용하여 &quot;.form&quot; 선택기를 비활성화해야 합니다.

## 확인 단계 {#verification-steps}

### 복제 및 전송 사용자 구성 {#configure-replication-and-transport-users}

AEM의 표준 설치에서는 기본 [복제 에이전트](/help/sites-deploying/replication.md) 내에서 전송 자격 증명의 사용자로 `admin`을(를) 지정합니다. 또한 관리자 사용자는 작성자 시스템에서 복제 소스를 만드는 데 사용됩니다.

보안 고려 사항의 경우 다음 두 가지 측면을 고려하여 두 가지 모두 현재 특정 사용 사례를 반영하도록 변경해야 합니다.

* **전송 사용자**&#x200B;는 관리자 사용자가 아니어야 합니다. 대신 게시 시스템의 관련 부분에 대한 액세스 권한만 있는 게시 시스템에서 사용자를 설정하고 해당 사용자의 자격 증명을 전송에 사용합니다.

  번들 복제 수신기 사용자에서 시작하여 이 사용자의 액세스 권한을 상황에 맞게 구성할 수 있습니다

* **복제 사용자** 또는 **에이전트 사용자 ID**&#x200B;도 관리자 사용자가 아닌 복제된 콘텐츠만 볼 수 있는 사용자여야 합니다. 복제 사용자는 작성자 시스템에서 복제할 콘텐츠를 게시자에게 보내기 전에 수집하는 데 사용됩니다.

### 작업 대시보드 보안 상태 검사 확인 {#check-the-operations-dashboard-security-health-checks}

AEM 6에서는 시스템 운영자가 문제를 해결하고 인스턴스 상태를 모니터링하는 데 도움이 되는 새로운 Operations Dashboard를 도입했습니다.

대시보드에는 보안 상태 검사 컬렉션도 포함되어 있습니다. 프로덕션 인스턴스로 시작하기 전에 모든 보안 상태 검사의 상태를 확인하는 것이 좋습니다. 자세한 내용은 [작업 대시보드 설명서](/help/sites-administering/operations-dashboard.md)를 참조하세요.

### 예제 컨텐츠가 있는지 확인 {#check-if-example-content-is-present}

모든 예의 콘텐츠 및 사용자(예: Geometrixx 프로젝트 및 해당 구성 요소)는 공개적으로 액세스할 수 있도록 하기 전에 프로덕션 시스템에서 제거하고 완전히 삭제해야 합니다.

>[!NOTE]
>
>이 인스턴스가 [프로덕션 준비 모드](/help/sites-administering/production-ready.md)에서 실행 중인 경우 샘플 `We.Retail` 응용 프로그램이 제거됩니다. 그렇지 않은 경우 패키지 관리자로 이동하여 샘플 콘텐츠를 제거한 다음 모든 `We.Retail` 패키지를 검색하여 제거할 수 있습니다.

[패키지 작업](package-manager.md)을 참조하세요.

### CRX 개발 번들이 있는지 확인 {#check-if-the-crx-development-bundles-are-present}

이러한 개발 OSGi 번들은 액세스 가능하게 만들기 전에 작성자 및 게시 프로덕션 시스템에서 제거해야 합니다.

* Adobe CRXDE 지원(com.adobe.granite.crxde-support)
* Adobe Granite CRX 탐색기(com.adobe.granite.crx-explorer)
* Adobe Granite CRXDE Lite(com.adobe.granite.crxde-lite)

### Sling 개발 번들이 있는지 확인 {#check-if-the-sling-development-bundle-is-present}

[AEM 개발자 도구](/help/sites-developing/aem-eclipse.md)에서 Apache Sling 도구 지원 설치(org.apache.sling.tooling.support.install)를 배포합니다.

이 OSGi 번들을 액세스 가능하게 만들기 전에 작성자 및 게시 프로덕션 시스템에서 제거해야 합니다.

### 사이트 간 요청 위조에 대한 Protect {#protect-against-cross-site-request-forgery}

#### CSRF 보호 프레임워크 {#the-csrf-protection-framework}

AEM 6.1에는 **CSRF 보호 프레임워크**&#x200B;라고 하는 크로스 사이트 요청 위조 공격으로부터 보호하는 메커니즘이 포함되어 있습니다. 사용 방법에 대한 자세한 내용은 [설명서](/help/sites-developing/csrf-protection.md)를 참조하세요.

#### Sling 레퍼러 필터 {#the-sling-referrer-filter}

CRX WebDAV 및 Apache Sling에서 CSRF(크로스 사이트 요청 위조)와 관련하여 알려진 보안 문제를 해결하려면 레퍼러 필터에 대한 구성을 추가하여 사용하십시오.

레퍼러 필터 서비스는 다음을 구성할 수 있는 OSGi 서비스입니다.

* 필터링해야 하는 http 메서드
* 빈 레퍼러 헤더 허용 여부
* 및 서버 호스트 외에 허용할 서버 목록입니다.

  기본적으로 서버가 바인딩된 localhost 및 현재 호스트 이름의 모든 변형이 목록에 있습니다.

레퍼러 필터 서비스를 구성하려면 다음 작업을 수행하십시오.

1. 다음 위치에서 Apache Felix 콘솔(**구성**)을 엽니다.

   `https://<server>:<port_number>/system/console/configMgr`

1. `admin`(으)로 로그인합니다.
1. **구성** 메뉴에서 다음을 선택합니다.

   `Apache Sling Referrer Filter`

1. `Allow Hosts` 필드에 레퍼러로 허용된 모든 호스트를 입력합니다. 각 항목은 형식이어야 합니다.

   &lt;프로토콜>://&lt;서버>:&lt;포트>

   예:

   * `https://allowed.server:80`에서 지정된 포트를 사용하여 이 서버의 모든 요청을 허용합니다.
   * https 요청도 허용하려면 두 번째 줄을 입력해야 합니다.
   * 해당 서버의 모든 포트를 허용하면 `0`을(를) 포트 번호로 사용할 수 있습니다.

1. 비어 있거나 누락된 레퍼러 헤더를 허용하려면 `Allow Empty` 필드를 선택합니다.

   >[!CAUTION]
   >
   >Adobe은 CSRF 공격에 시스템을 노출할 수 있으므로 빈 값을 허용하지 않고 `cURL`과(와) 같은 명령줄 도구를 사용하는 동안 레퍼러를 제공할 것을 권장합니다.

1. 이 필터가 `Filter Methods` 필드에 대한 검사에 사용하는 메서드를 편집합니다.

1. 변경 내용을 저장하려면 **저장**&#x200B;을 클릭하세요.

### OSGI 설정 {#osgi-settings}

일부 OSGI 설정은 응용 프로그램을 보다 쉽게 디버깅할 수 있도록 기본적으로 설정됩니다. 내부 정보가 외부로 유출되지 않도록 게시 및 작성자 생산성 인스턴스에서 이러한 설정을 변경합니다.

>[!NOTE]
>
>**일별 CQ WCM 디버그 필터**&#x200B;를 제외한 아래 모든 설정은 자동으로 [프로덕션 준비 모드](/help/sites-administering/production-ready.md)에 의해 적용됩니다. Adobe 따라서 프로덕션 환경에 인스턴스를 배포하기 전에 모든 설정을 검토하는 것이 좋습니다.

다음 각 서비스에 대해 지정된 설정을 변경해야 합니다.

* [Adobe Granite HTML 라이브러리 관리자](/help/sites-deploying/osgi-configuration-settings.md#day-cq-html-library-manager):

   * **축소** 사용(CRLF 및 공백 문자 제거)
   * **Gzip** 사용(한 번의 요청으로 파일을 압축하고 액세스할 수 있도록 허용)
   * **Debug** 사용 안 함
   * **시간** 사용 안 함

* [일 CQ WCM 디버그 필터](/help/sites-deploying/osgi-configuration-settings.md#day-cq-wcm-debug-filter):

   * **사용** 선택 취소

* [일 CQ WCM 필터](/help/sites-deploying/osgi-configuration-settings.md):

   * 게시만 할 때 **WCM 모드**&#x200B;를 &quot;사용 안 함&quot;으로 설정하십시오.

* [Apache Sling JavaScript 처리기](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-javascript-handler):

   * **디버그 정보 생성** 사용 안 함

* [Apache Sling JSP 스크립트 핸들러](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-jsp-script-handler):

   * **디버그 정보 생성** 사용 안 함
   * **매핑된 콘텐츠** 사용 안 함

[OSGi 구성 설정](/help/sites-deploying/osgi-configuration-settings.md)을 참조하십시오.

AEM을 사용하여 작업할 때 이러한 서비스에 대한 구성 설정을 관리할 수 있는 방법에는 몇 가지가 있습니다. 자세한 내용 및 권장 사례를 보려면 [OSGi 구성](/help/sites-deploying/configuring-osgi.md)을 참조하십시오.

## 추가 판독 {#further-readings}

### 서비스 거부(DoS) 공격 완화 {#mitigate-denial-of-service-dos-attacks}

서비스 거부(DoS) 공격은 의도한 사용자가 컴퓨터 리소스를 사용할 수 없게 하려고 시도하는 것입니다. 이 공격은 리소스를 오버로드하여 수행하는 경우가 많습니다. 예:

* 외부 소스의 수많은 요청.
* 시스템이 성공적으로 전달할 수 있는 것보다 더 많은 정보에 대한 요청입니다.

  예를 들어 전체 리포지토리의 JSON 표현입니다.

* 콘텐츠 페이지에 URL을 무제한으로 요청하여 해당 URL에는 핸들, 일부 선택기, 확장 프로그램 및 접미사가 포함될 수 있으며, 이러한 모든 URL은 수정할 수 있습니다.

  예를 들어 `.../en.html`은(는) 다음과 같이 요청할 수도 있습니다.

   * `.../en.ExtensionDosAttack`
   * `.../en.SelectorDosAttack.html`
   * `.../en.html/SuffixDosAttack`

  모든 유효한 변형(예: `200` 응답을 반환하고 캐시되도록 구성됨)이 Dispatcher에 의해 캐시되므로 전체 파일 시스템이 만들어지고 추가 요청에 대한 서비스가 제공되지 않습니다.

이러한 공격을 방지하기 위한 여러 구성 지점이 있지만 여기서는 AEM과 관련된 지점만 설명합니다.

**DoS를 방지하도록 Sling 구성**

Sling은 *콘텐츠 중심*&#x200B;입니다. 각 (HTTP) 요청이 JCR 리소스(저장소 노드) 형태의 컨텐츠에 매핑되므로 처리는 컨텐츠에 중점을 둡니다.

* 첫 번째 타겟은 콘텐츠를 보유하는 리소스(JCR 노드)입니다.
* 두 번째, 렌더러 또는 스크립트는 요청의 특정 부분(예: 선택기 및/또는 확장)이 있는 리소스 속성에서 찾을 수 있습니다.

자세한 내용은 [Sling 요청 처리 중](/help/sites-developing/the-basics.md#sling-request-processing)을 참조하십시오.

이러한 접근 방식을 통해 Sling은 강력하고 유연하지만 항상 그렇듯이 신중하게 관리해야 하는 유연성이 있습니다.

DoS 오용을 방지하기 위해 다음을 수행할 수 있습니다.

1. 응용 프로그램 수준에서 컨트롤을 통합합니다. 가능한 변형의 수로 인해 기본 구성은 실행 가능하지 않습니다.

   응용 프로그램에서 다음을 수행해야 합니다.

   * *만*&#x200B;이(가) 필요한 명시적 선택기를 제공하고 다른 모든 선택기에 대해 `404`을(를) 반환하도록 응용 프로그램에서 선택기를 제어합니다.
   * 무제한의 콘텐츠 노드 출력을 방지합니다.

1. 문제 영역일 수 있는 기본 렌더러의 구성을 확인합니다.

   * 특히 JSON 렌더러는 트리 구조를 여러 레벨에 걸쳐 전환합니다.

     예를 들어, 요청은 다음과 같습니다.

     `http://localhost:4502/.json`

     는 JSON 표현에 전체 저장소를 덤프하여 상당한 서버 문제를 초래할 수 있습니다. 이러한 이유로 Sling은 최대 결과 수에 대한 제한을 설정합니다. JSON 렌더링의 깊이를 제한하려면 다음에 대한 값을 설정합니다.

     **JSON 최대 결과**( `json.maximumresults`)

     [Apache Sling GET 서블릿](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-get-servlet)에 대한 구성에서. 이 제한을 초과하면 렌더링이 축소됩니다. AEM에서 Sling의 기본값은 `1000`입니다.

   * 예방 조치로서 다른 기본 렌더러(HTML, 일반 텍스트, XML)를 비활성화해야 합니다. [Apache Sling GET 서블릿](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-get-servlet)을(를) 구성하여 다시 시도하십시오.

   >[!CAUTION]
   >
   >JSON 렌더러는 AEM의 일반 작업에 필요하므로 비활성화하지 마십시오.

1. 방화벽을 사용하여 인스턴스에 대한 액세스를 필터링합니다.

   * 보호되지 않은 상태로 두면 서비스 거부 공격을 초래할 수 있는 인스턴스 지점에 대한 액세스를 필터링하려면 운영 체제 수준 방화벽을 사용해야 합니다.

**양식 선택기를 사용하여 발생한 Do에 대해 완화**

>[!NOTE]
>
>이 완화 는 Forms을 사용하지 않는 AEM 환경에서만 수행해야 합니다.

AEM은 `FormChooserServlet`에 대한 기본 제공 인덱스를 제공하지 않으므로 쿼리에서 양식 선택기를 사용하면 비용이 많이 드는 저장소 순회를 트리거할 수 있으며 일반적으로 AEM 인스턴스를 중지합니다. **&ast;.form이 있으면 양식 선택기를 감지할 수 있습니다.쿼리의 &ast;** 문자열.

이 문제를 완화하기 위해 다음 단계를 수행할 수 있습니다.

1. 브라우저를 *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*&#x200B;로 지정하여 웹 콘솔로 이동합니다.

1. **일 CQ WCM 양식 선택기 서블릿 검색**
1. 항목을 클릭한 후 다음 창에서 **고급 검색 필요**&#x200B;를 사용하지 않도록 설정하십시오.

1. **저장**&#x200B;을 클릭합니다.

**자산 다운로드 서블릿으로 인한 Do에 대해 완화**

기본 에셋 다운로드 서블릿을 사용하면 인증된 사용자가 임의로 큰 동시 다운로드 요청을 발행하여 에셋의 ZIP 파일을 만들 수 있습니다. 큰 ZIP 아카이브를 만들면 서버와 네트워크가 과부하가 될 수 있습니다. 이 동작으로 인해 발생할 수 있는 서비스 거부(DoS) 위험을 완화하기 위해 [!DNL Experience Manager] 게시 인스턴스에서 `AssetDownloadServlet` OSGi 구성 요소를 기본적으로 사용하지 않도록 설정합니다. 기본적으로 [!DNL Experience Manager] 작성자 인스턴스에서 사용할 수 있습니다.

다운로드 기능이 필요하지 않은 경우 작성자 및 게시 배포에서 서블릿을 비활성화합니다. 에셋 다운로드 기능을 사용하도록 설정해야 하는 경우 자세한 내용은 [Adobe 경험 관리에서 에셋 다운로드](/help/assets/download-assets-from-aem.md)를 참조하십시오. 또한 배포에서 지원할 수 있는 최대 다운로드 제한을 정의할 수 있습니다.

### WebDAV 비활성화 {#disable-webdav}

적절한 OSGi 번들을 중지하여 작성자 및 게시 환경 모두에서 WebDAV를 비활성화합니다.

1. 다음에서 실행 중인 **Felix 관리 콘솔**&#x200B;에 연결:

   `https://<*host*>:<*port*>/system/console`

   예: `http://localhost:4503/system/console/bundles`

1. 번들 목록에서 다음 이름의 번들을 찾습니다.

   `Apache Sling Simple WebDAV Access to repositories (org.apache.sling.jcr.webdav)`

1. 이 번들을 중지하려면 작업 열에서 중지 버튼을 클릭합니다.

1. 다시 번들 목록에서 다음 번들을 찾습니다.

   `Apache Sling DavEx Access to repositories (org.apache.sling.jcr.davex)`

1. 이 번들을 중지하려면 중지 버튼을 클릭합니다.

   >[!NOTE]
   >
   >AEM을 다시 시작할 필요가 없습니다.

### 사용자 홈 경로에서 개인 식별 정보를 공개하지 않는지 확인 {#verify-that-you-are-not-disclosing-personally-identifiable-information-in-the-users-home-path}

저장소 사용자 홈 경로에 개인 식별 정보가 노출되지 않도록 하여 사용자를 보호하는 것이 중요합니다.

AEM 6.1 이후 `AuthorizableNodeName` 인터페이스의 새로운 구현을 통해 사용자(승인 가능 노드)의 ID 노드 이름 저장 방식이 변경되었습니다. 새 인터페이스는 더 이상 노드 이름에 사용자 ID를 표시하지 않고 대신 임의의 이름을 생성합니다.

AEM에서 승인 가능한 ID를 생성하는 기본 방법이므로 이를 활성화하기 위해 구성을 수행할 필요가 없습니다.

권장되지는 않지만 기존 애플리케이션과의 이전 버전과의 호환성을 위해 이전 구현이 필요한 경우 비활성화할 수 있습니다. 이렇게 하려면 다음을 수행해야 합니다.

1. 웹 콘솔로 이동하여 **Apache Jackrabbit Oak SecurityProvider**&#x200B;의 **requiredServicePids** 속성에서 **&#x200B; org.apache.jackrabbit.oak.security.user.RandomAuthorizableNodeName** 항목을 제거합니다.

   OSGi 구성에서 **org.apache.jackrabbit.oak.security.internal.SecurityProviderRegistration** PID를 찾아 Oak 보안 공급자를 찾을 수도 있습니다.

1. 웹 콘솔에서 **Apache Jackrabbit Oak 임의 승인 가능 노드 이름** OSGi 구성을 삭제합니다.

   더 쉬운 조회를 위해 이 구성의 PID는 **org.apache.jackrabbit.oak.security.user.RandomAuthorizableNodeName**&#x200B;입니다.

>[!NOTE]
>
>자세한 내용은 [승인 가능한 노드 이름 생성](https://jackrabbit.apache.org/oak/docs/security/user/authorizablenodename.html)에 대한 Oak 설명서를 참조하십시오.

### 익명 권한 강화 패키지 {#anonymous-permission-hardening-package}

기본적으로 AEM은 `jcr:createdBy` 또는 `jcr:lastModifiedBy`과(와) 같은 시스템 메타데이터를 일반 콘텐츠 옆의 노드 속성으로 저장소에 저장합니다. 구성 및 액세스 제어 설정에 따라, 경우에 따라 이러한 노드가 원시 JSON 또는 XML로 렌더링되는 경우 PII(개인 식별 정보)가 노출될 수 있습니다.

모든 저장소 데이터와 마찬가지로 이러한 속성은 Oak 권한 부여 스택에 의해 매개됩니다. 이들에 대한 접근은 최소특권의 원칙에 따라 제한되어야 한다.

이를 지원하기 위해 Adobe은 고객이 빌드할 수 있는 기반으로 권한 강화 패키지를 제공합니다. 저장소 루트에 &quot;거부&quot; 액세스 제어 항목을 설치하여 일반적으로 사용되는 시스템 속성에 대한 익명 액세스를 제한하여 작동합니다. 패키지는 [다운로드](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/helper/anonymous-permissions-pkg-0.1.2.zip)할 수 있으며 지원되는 모든 AEM 버전에 설치할 수 있습니다.

변경 사항을 설명하기 위해 패키지를 설치하기 전에 익명으로 볼 수 있는 노드 속성을 비교할 수 있습니다.

![패키지 설치 전](/help/sites-administering/assets/before_resized.png)

패키지 설치 후 볼 수 있는 항목을 포함합니다. 여기서 `jcr:createdBy` 및 `jcr:lastModifiedBy`은(는) 표시되지 않습니다.

![패키지 설치 후](/help/sites-administering/assets/after_resized.png)

자세한 내용은 패키지 릴리스 노트 를 참조하십시오.

### 클릭재킹 방지 {#prevent-clickjacking}

Adobe는 클릭재킹을 방지하기 위해 `SAMEORIGIN`으로 설정된 `X-FRAME-OPTIONS` HTTP 헤더를 제공하도록 웹 서버를 구성하는 것을 권장합니다.

클릭재킹에 대한 자세한 내용은 [OWASP 사이트](https://www.owasp.org/index.php/Clickjacking)를 참조하십시오.

### 필요한 경우 암호화 키를 올바르게 복제해야 합니다. {#make-sure-you-properly-replicate-encryption-keys-when-needed}

특정 AEM 기능 및 인증 체계를 사용하려면 모든 AEM 인스턴스에 암호화 키를 복제해야 합니다.

키 저장 방식이 6.3과 이전 버전 간에 다르기 때문에 키 복제는 버전 간에 다르게 수행됩니다.

자세한 내용은 아래를 참조하십시오.

#### AEM 6.3용 키 복제 {#replicating-keys-for-aem}

이전 버전에서는 AEM 6.3부터 복제 키가 저장소에 저장되었지만 파일 시스템에 저장됩니다.

따라서 인스턴스 간에 키를 복제하려면 소스 인스턴스에서 파일 시스템의 타겟 인스턴스 위치로 키를 복제합니다.

특히 다음을 수행해야 합니다.

1. 복사할 주요 자료가 포함된 AEM 인스턴스(일반적으로 작성자 인스턴스)에 액세스합니다.
1. 로컬 파일 시스템에서 com.adobe.granite.crypto.file 번들을 찾습니다. 예를 들어 이 경로에서 다음을 수행합니다.

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`

   각 폴더 내의 `bundle.info` 파일은 번들 이름을 식별합니다.

1. 데이터 폴더로 이동합니다. 예:

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. HMAC 및 마스터 파일을 복사합니다.
1. 그런 다음 HMAC 키를 복제할 대상 인스턴스로 이동하여 데이터 폴더로 이동합니다. 예:

   * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. 이전에 복사한 두 파일을 붙여넣습니다.
1. 대상 인스턴스가 이미 실행 중인 경우 [암호화 번들을 새로 고치십시오](/help/communities/deploy-communities.md#refresh-the-granite-crypto-bundle).
1. 키를 복제할 모든 인스턴스에 대해 위 단계를 반복합니다.

#### AEM 6.2 및 이전 버전용 키 복제 {#replicating-keys-for-aem-and-older-versions}

AEM 6.2 및 이전 버전에서는 키가 `/etc/key` 노드 아래의 저장소에 저장됩니다.

인스턴스 간에 키를 안전하게 복제하는 권장 방법은 이 노드만 복제하는 것입니다. CRXDE Lite을 통해 노드를 선택적으로 복제할 수 있습니다.

1. *`https://&lt;serveraddress&gt;:4502/crx/de/index.jsp`*(으)로 이동하여 CRXDE Lite 열기
1. `/etc/key` 노드를 선택하십시오.
1. **복제** 탭으로 이동합니다.
1. **복제** 단추를 누릅니다.

### 침투 테스트 수행 {#perform-a-penetration-test}

Adobe은 프로덕션을 시작하기 전에 AEM 인프라에 대한 침투 테스트를 수행할 것을 권장합니다.

### 개발 우수 사례 {#development-best-practices}

AEM 환경을 안전하게 유지하기 위해 새 개발이 [보안 모범 사례](/help/sites-developing/security.md)를 따르는 것이 중요합니다.
