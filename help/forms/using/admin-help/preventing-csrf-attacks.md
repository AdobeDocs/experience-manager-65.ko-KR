---
title: CSRF 공격 방지
description: 크로스 사이트 요청 위조(CSRF) 공격을 방지하고 사용자 데이터가 손상되지 않도록 보호하는 방법을 알아봅니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: e17fc114-eba5-4e1b-8e70-ad6af7008018
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Security
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: ht
source-wordcount: '955'
ht-degree: 100%

---

# CSRF 공격 방지 {#preventing-csrf-attacks}

## CSRF 공격의 작동 방식 {#how-csrf-attacks-work}

크로스 사이트 요청 위조(CSRF)는 유효한 사용자의 브라우저를 이용하여 iFrame을 통해 악의적인 요청을 보내는 웹 사이트 취약점입니다. 브라우저는 도메인 기반으로 쿠키를 전송하므로 사용자가 애플리케이션에 로그인한 경우 사용자 데이터가 손상될 수 있습니다.

예를 들어 브라우저에서 관리 콘솔에 로그인하는 시나리오를 생각해 보십시오. 링크가 포함된 이메일 메시지를 받습니다. 링크를 클릭하면 브라우저에서 새 탭이 열립니다. 열린 페이지에는 인증된 AEM Forms 세션의 쿠키를 사용하여 Forms 서버에 악의적인 요청을 보내는 숨겨진 iFrame이 포함되어 있습니다. 사용자 관리에서는 유효한 쿠키를 수신하므로 해당 요청을 전달합니다.

## CSRF 관련 용어 {#csrf-related-terms}

**레퍼러:** 요청이 들어오는 소스 페이지 주소입니다. 예를 들어 site1. com의 웹 페이지에는 site2. com으로 이동하는 링크가 포함되어 있습니다. 이 링크를 클릭하면 site2. com에 요청이 게시됩니다. 이 요청의 레퍼러는 소스가 site1.com인 페이지에서 요청이 이루어졌으므로 site1.com입니다.

**허용 목록에 추가된 URI:** URI는 요청을 받고 있는 Forms 서버의 리소스를 식별합니다(예: /adminui 또는 /contentspace). 일부 리소스는 외부 사이트에서 애플리케이션으로 들어가라는 요청을 허용할 수 있습니다. 해당 리소스는 허용 목록에 추가된 URI로 간주됩니다. Forms 서버는 허용 목록에 추가된 URI에서 레퍼러 확인을 수행하지 않습니다.

**Null 레퍼러:** 새 브라우저 창이나 탭을 열고 주소를 입력한 후 Enter 키를 누르면 레퍼러가 null입니다. 이 요청은 완전히 새로운 요청이며 상위 웹 페이지에서 발생한 것이 아니므로 해당 요청에 대한 레퍼러가 없습니다. Forms 서버는 다음과 같은 경우 null 레퍼러를 수신할 수 있습니다.

* Acrobat에서 SOAP 또는 REST 엔드포인트에 대해 수행된 요청
* AEM Forms SOAP 또는 REST 엔드포인트에서 HTTP 요청을 보내는 모든 데스크탑 클라이언트
* 새 브라우저 창이 열리고 AEM Forms 웹 애플리케이션 로그인 페이지의 URL이 입력되는 경우

SOAP 및 REST 엔드포인트에서 null 레퍼러를 허용합니다. 또한 /adminui 및 /contentspace와 매핑된 해당 리소스와 같은 모든 URI 로그인 페이지에서 null 레퍼러를 허용합니다. 예를 들어 /contentspace에 매핑된 서블릿은 /contentspace/faces/jsp/login. jsp이며 null 레퍼러 예외여야 합니다. 이 예외는 웹 애플리케이션에 대해 GET 필터링을 활성화한 경우에만 필요합니다. 애플리케이션에서 null 레퍼러를 허용할지 여부를 지정할 수 있습니다. [AEM Forms 강화 및 보안](https://help.adobe.com/ko_KR/livecycle/11.0/HardeningSecurity/index.html)의 &#39;크로스 사이트 요청 위조 공격으로부터 보호&#39;를 참조하십시오.

**허용된 레퍼러 예외:** 허용된 레퍼러 예외는 요청이 차단되는 허용된 레퍼러 목록의 하위 목록입니다. 허용된 레퍼러 예외는 웹 애플리케이션에만 적용됩니다. 허용된 레퍼러의 하위 집합이 특정 웹 애플리케이션을 호출할 수 있도록 허용해서는 안 되는 경우 허용된 레퍼러 예외를 통해 레퍼러를 차단 목록에 추가할 수 있습니다. 허용된 레퍼러 예외는 애플리케이션의 web. xml 파일에 지정되어 있습니다. (도움말 및 튜토리얼 페이지에서 AEM Forms 강화 및 보안의 &#39;크로스 사이트 요청 위조 공격으로부터 보호&#39;를 참조하십시오.)

## 허용된 레퍼러의 작동 방식 {#how-allowed-referers-work}

AEM Forms는 CSRF 공격을 방지하는 데 도움이 되는 레퍼러 필터링을 제공합니다. 레퍼러 필터링의 작동 방식은 다음과 같습니다.

1. Forms 서버에서 호출에 사용된 HTTP 메서드를 확인합니다.

   * 해당 메서드가 POST인 경우 Forms 서버는 레퍼러 헤더 확인을 수행합니다.
   * 해당 메서드가 GET인 경우 Forms 서버는 CSRF_CHECK_GETS가 true로 설정되어 있지 않으면 레퍼러 확인을 우회하고, true로 설정되어 있으면 레퍼러 헤더 확인을 수행합니다. CSRF_CHECK_GETS는 애플리케이션의 web. xml 파일에 지정되어 있습니다. ([강화 및 보안 안내서](https://help.adobe.com/ko_KR/livecycle/11.0/HardeningSecurity/index.html)의 &#39;크로스 사이트 요청 위조 공격으로부터 보호&#39;를 참조하십시오.)

1. Forms 서버에서 요청된 URI가 허용 목록에 추가되어 있는지 확인합니다.

   * URI가 허용 목록에 추가되어 있으면 서버에서 해당 요청을 전달합니다.
   * 요청된 URI가 허용 목록에 추가되어 있지 않으면 서버에서 요청의 레퍼러를 가져옵니다.

1. 요청에 레퍼러가 있는 경우 서버에서 해당 레퍼러가 허용된 레퍼러인지 여부를 확인합니다. 허용된 레퍼러인 경우 서버에서 레퍼러 예외를 확인합니다.

   * 예외인 경우 해당 요청이 차단됩니다.
   * 예외가 아닌 경우 해당 요청이 전달됩니다.

1. 요청에 레퍼러가 없는 경우 서버에서 null 레퍼러가 허용되는지 여부를 확인합니다.

   * null 레퍼러가 허용되면 해당 요청이 전달됩니다.
   * null 레퍼러가 허용되지 않으면 서버에서 요청된 URI가 null 레퍼러에 대한 예외인지 확인하고 그에 따라 요청을 처리합니다.

## 허용된 레퍼러 구성 {#configure-allowed-referers}

구성 관리자를 실행하면 기본 호스트와 IP 주소 또는 Forms 서버가 허용된 레퍼러 목록에 추가됩니다. 이 목록은 관리 콘솔에서 편집할 수 있습니다.

1. 관리 콘솔에서 설정 > 사용자 관리 > 구성 > 허용된 레퍼러 URL 구성을 클릭합니다. 그러면 페이지 하단에 허용된 레퍼러 목록이 나타납니다.
1. 허용된 레퍼러를 추가하려면 다음 작업을 수행합니다.

   * 허용된 레퍼러 상자에 호스트 이름 또는 IP 주소를 입력합니다. 허용된 레퍼러를 한 번에 두 개 이상 추가하려면 각 호스트 이름 또는 IP 주소를 새 줄에 입력합니다.
   * HTTP 포트 및 HTTPS 포트 상자에서 HTTP, HTTPS 또는 둘 다에 허용할 포트를 지정합니다. 해당 상자를 비워 두면 기본 포트(HTTP의 경우 포트 80, HTTPS의 경우 포트 443)가 사용됩니다. 해당 상자에 `0`을 입력하면 해당 서버의 모든 포트가 활성화됩니다. 특정 포트 번호를 입력하여 해당 포트만 활성화할 수도 있습니다.
   * 추가를 클릭합니다.

1. 허용된 레퍼러 목록에서 항목을 제거하려면 해당 목록에서 항목을 선택하고 삭제를 클릭합니다.

   허용된 레퍼러 목록이 비어 있으면 CSRF 기능이 작동을 멈추고 시스템이 안전하지 않게 됩니다.

1. 허용된 레퍼러 목록을 변경한 후 AEM Forms 서버를 다시 시작합니다.
