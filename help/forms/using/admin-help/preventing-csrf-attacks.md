---
title: CSRF 공격 방지
description: CSRF(크로스 사이트 요청 위조) 공격을 방지하고 사용자 데이터가 손상되지 않도록 보호하는 방법을 알아봅니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: e17fc114-eba5-4e1b-8e70-ad6af7008018
source-git-commit: 3d80ea6a6fbad05afcdd1f41f4b9de70921ab765
workflow-type: tm+mt
source-wordcount: '972'
ht-degree: 0%

---

# CSRF 공격 방지 {#preventing-csrf-attacks}

## CSRF 공격 작동 방식 {#how-csrf-attacks-work}

CSRF(크로스 사이트 요청 위조)는 유효한 사용자의 브라우저를 사용하여 iFrame을 통해 악의적인 요청을 보내는 웹 사이트 취약성입니다. 브라우저는 도메인 기반으로 쿠키를 보내기 때문에 사용자가 애플리케이션에 로그인하면 사용자의 데이터가 손상될 수 있습니다.

예를 들어, 브라우저에서 관리 콘솔에 로그인하는 시나리오를 생각해 보십시오. 링크가 포함된 이메일 메시지를 받게 됩니다. 링크를 클릭하면 브라우저에 새 탭이 열립니다. 연 페이지에는 인증된 AEM Forms 세션의 쿠키를 사용하여 Forms 서버에 악의적인 요청을 하는 숨겨진 iFrame이 포함되어 있습니다. 사용자 관리는 유효한 쿠키를 수신하므로 요청을 전달합니다.

## CSRF 관련 용어 {#csrf-related-terms}

**Referer:** 요청이 들어오는 소스 페이지의 주소. 예를 들어 site1.com의 웹 페이지에는 site2.com에 대한 링크가 포함되어 있습니다. 링크를 클릭하면 site2.com에 요청이 게시됩니다. 이 요청은 site1.com이 소스인 페이지에서 수행되므로 이 요청의 레퍼러는 site1.com입니다.

**허용 목록에추가된 URI:** URI는 요청되는 Forms 서버의 리소스를 식별합니다(예: /adminui 또는 /contentspace). 일부 리소스는 외부 사이트에서 애플리케이션에 대한 입력 요청을 허용할 수 있습니다. 이러한 리소스는 허용 목록에추가된 URI로 간주됩니다. Forms 서버는 허용 목록에추가된 URI에서 레퍼러 검사를 수행하지 않습니다.

**Null 참조:** 새 브라우저 창이나 탭을 연 다음 주소를 입력하고 Enter 키를 누르면 레퍼러가 null입니다. 이 요청은 완전히 새로운 것으로, 상위 웹 페이지에서 시작하지 않습니다. 따라서 요청에 대한 레퍼러가 없습니다. Forms 서버는 다음 위치에서 null 레퍼러를 수신할 수 있습니다.

* Acrobat의 SOAP 또는 REST 끝점에 대한 요청
* AEM forms SOAP 또는 REST 끝점에서 HTTP 요청을 하는 모든 데스크탑 클라이언트
* 새 브라우저 창을 열고 AEM forms 웹 응용 프로그램 로그인 페이지의 URL을 입력하면

SOAP 및 REST 끝점에 Null 레퍼러를 허용합니다. 또한 /adminui 및 /contentspace와 같은 모든 URI 로그인 페이지와 해당 매핑된 리소스에 null 레퍼러를 허용합니다. 예를 들어 /contentspace에 대해 매핑된 서블릿은 /contentspace/faces/jsp/login.jsp이며, null 레퍼러 예외여야 합니다. 이 예외는 웹 응용 프로그램에 대해 GET 필터링을 사용하는 경우에만 필요합니다. 애플리케이션은 null 레퍼러를 허용할지 여부를 지정할 수 있습니다. 에서 &quot;사이트 간 요청 위조 공격으로부터 보호&quot;를 참조하십시오. [AEM Forms의 보안 강화](https://help.adobe.com/en_US/livecycle/11.0/HardeningSecurity/index.html).

**허용된 레퍼러 예외:** 허용된 레퍼러 예외는 허용된 레퍼러 목록의 하위 목록으로서 요청이 차단됩니다. 허용됨 참조 예외는 웹 응용 프로그램에만 해당됩니다. 허용된 레퍼러의 하위 집합이 특정 웹 애플리케이션을 호출하도록 허용해서는 안 되는 경우 허용된 레퍼러 예외를 통해 레퍼러를 차단 목록 할 수 있습니다. 허용된 레퍼러 예외는 응용 프로그램의 web.xml 파일에 지정됩니다. (도움말 및 Tutorials 페이지에서 AEM Forms 보안 강화 및 보안 의 &quot;사이트 간 요청 위조 공격으로부터 보호&quot;를 참조하십시오.)

## 허용된 레퍼러 작동 방식 {#how-allowed-referers-work}

AEM Forms은 CSRF 공격을 방지하는 레퍼러 필터링을 제공합니다. 레퍼러 필터링 작동 방식은 다음과 같습니다.

1. Forms 서버는 호출에 사용된 HTTP 메서드를 확인합니다.

   * POST 상태인 경우 Forms 서버가 레퍼러 헤더 검사를 수행합니다.
   * GET 레퍼러인 경우 Forms 서버는 CSRF_CHECK_GETS가 true로 설정되지 않은 경우 레퍼러 헤더 검사를 수행하지 않고 레퍼러 검사를 우회합니다. CSRF_CHECK_GETS는 응용 프로그램의 web.xml 파일에 지정됩니다. (&quot;사이트 간 요청 위조 공격으로부터 보호&quot; 참조) [강화 및 보안 안내서](https://help.adobe.com/en_US/livecycle/11.0/HardeningSecurity/index.html).)

1. Forms 서버는 요청된 URI가 허용 목록에추가된인지 확인합니다.

   * URI가 허용 목록에추가된인 경우 서버가 요청을 전달합니다.
   * 요청한 URI가 허용 목록에추가된이 아닌 경우 서버는 요청의 레퍼러를 검색합니다.

1. 요청에 레퍼러가 있는 경우 서버는 허용된 레퍼러인지 여부를 확인합니다. 허용되는 경우 서버는 레퍼러 예외를 확인합니다.

   * 예외인 경우 요청이 차단됩니다.
   * 예외가 아닌 경우 요청이 전달됩니다.

1. 요청에 레퍼러가 없으면 서버는 null 레퍼러가 허용되는지 여부를 확인합니다.

   * null 레퍼러가 허용되면 요청이 전달됩니다.
   * null 레퍼러가 허용되지 않으면 서버는 요청된 URI가 null 레퍼러에 대한 예외인지 확인하고 그에 따라 요청을 처리합니다.

## 허용된 레퍼러 구성 {#configure-allowed-referers}

구성 관리자를 실행하면 기본 호스트 및 IP 주소 또는 Forms 서버가 허용된 레퍼러 목록에 추가됩니다. 관리 콘솔에서 이 목록을 편집할 수 있습니다.

1. 관리 콘솔에서 설정 > 사용자 관리 > 구성 > 허용된 레퍼러 URL 구성 을 클릭합니다. 페이지 하단에 허용된 레퍼러 목록이 나타납니다.
1. 허용된 레퍼러를 추가하려면:

   * 허용된 레퍼러 상자에 호스트 이름 또는 IP 주소를 입력합니다. 한 번에 두 개 이상의 허용된 레퍼러를 추가하려면 새 줄에 각 호스트 이름 또는 IP 주소를 입력합니다.
   * HTTP 포트 및 HTTPS 포트 상자에서 HTTP, HTTPS 또는 두 가지 모두를 허용할 포트를 지정합니다. 이러한 상자를 비워 두면 기본 포트(HTTP의 경우 포트 80, HTTPS의 경우 포트 443)가 사용됩니다. 를 입력한 경우 `0` (영) 상자에서 해당 서버의 모든 포트가 활성화됩니다. 특정 포트 번호를 입력하여 해당 포트만 활성화할 수도 있습니다.
   * 추가를 클릭합니다.

1. 허용된 레퍼러 목록에서 항목을 제거하려면 목록에서 항목을 선택하고 삭제를 누릅니다.

   허용된 레퍼러 목록이 비어 있으면 CSRF 기능이 작동하지 않고 시스템이 안전하지 않게 됩니다.

1. 허용된 레퍼러 목록을 변경한 후 AEM Forms 서버를 다시 시작합니다.
