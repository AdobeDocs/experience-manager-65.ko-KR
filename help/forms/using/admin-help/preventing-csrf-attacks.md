---
title: CSRF 공격 방지
seo-title: CSRF 공격 방지
description: CSRF(교차 사이트 요청 위조) 공격을 방지하고 사용자 데이터가 손상되지 않도록 보호하는 방법을 알아봅니다.
seo-description: CSRF(교차 사이트 요청 위조) 공격을 방지하고 사용자 데이터가 손상되지 않도록 보호하는 방법을 알아봅니다.
uuid: f3553826-f5eb-40ea-aeb7-90e4ad30598c
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a3cbffb7-c1d1-47c2-bcfd-70f1e2d81ac9
exl-id: e17fc114-eba5-4e1b-8e70-ad6af7008018
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '990'
ht-degree: 0%

---

# CSRF 공격 방지 {#preventing-csrf-attacks}

## CSRF 공격 작동 방식 {#how-csrf-attacks-work}

CSRF(Cross-site request forgery)는 유효한 사용자의 브라우저가 iFrame을 통해 악의적인 요청을 보내는 데 사용되는 웹 사이트 취약성입니다. 브라우저는 도메인에 따라 쿠키를 전송하므로 사용자가 현재 애플리케이션에 로그인한 경우 사용자의 데이터가 손상될 수 있습니다.

예를 들어 브라우저에서 관리 콘솔에 로그인한 시나리오를 생각해 보십시오. 링크가 포함된 이메일 메시지를 받게 됩니다. 링크를 클릭하면 브라우저에서 새 탭이 열립니다. 연 페이지에는 인증된 AEM Forms 세션의 쿠키를 사용하여 Forms 서버에 악의적인 요청을 하는 숨겨진 iFrame이 포함되어 있습니다. 사용자 관리는 유효한 쿠키를 수신하므로 요청을 전달합니다.

## CSRF 관련 용어 {#csrf-related-terms}

**Referer:**  요청이 오고 있는 소스 페이지의 주소입니다. 예를 들어 site1.com의 웹 페이지에는 site2.com에 대한 링크가 포함되어 있습니다. 링크를 클릭하면 site2.com에 요청이 게시됩니다. 이 요청의 레퍼러는 site1.com입니다. 이 요청은 소스가 site1.com인 페이지에서 수행되기 때문입니다.

**허용 목록에추가된 URI:**  URI는 요청 중인 양식 서버의 리소스(예: /adminui 또는 /contentspace)를 식별합니다. 일부 리소스에서 외부 사이트의 응용 프로그램 입력을 요청할 수 있습니다. 이러한 리소스는 허용 목록에추가된 URI로 간주됩니다. Forms 서버는 허용 목록에추가된 URI에서 레퍼러 검사를 수행하지 않습니다.

**Null 레퍼러:** 새 브라우저 창이나 탭을 연 다음 주소를 입력하고 Enter 키를 누르면 레퍼러가 null입니다. 요청은 완전히 새로운 것으로 상위 웹 페이지에서 시작하지 않습니다.따라서 요청에 대한 레퍼러가 없습니다. 양식 서버는 다음에서 null 레퍼러를 수신할 수 있습니다.

* Acrobat의 SOAP 또는 REST 종단점에 대한 요청
* AEM Forms SOAP 또는 REST 끝점에서 HTTP 요청을 수행하는 모든 데스크탑 클라이언트
* 새 브라우저 창을 열고 AEM forms 웹 애플리케이션 로그인 페이지의 URL을 입력하면

SOAP 및 REST 끝점에 null 레퍼러를 허용합니다. /adminui 및 /contentspace와 같은 모든 URI 로그인 페이지와 해당 매핑된 리소스에서 null 레퍼러를 사용할 수도 있습니다. 예를 들어 /contentspace에 대해 매핑된 서블릿은 /contentspace/faces/jsp/login.jsp 이며, 이것은 null 레퍼러 예외여야 합니다. 이 예외는 웹 응용 프로그램에 대해 GET 필터링을 활성화하는 경우에만 필요합니다. 응용 프로그램에서 null 레퍼러를 허용할지 여부를 지정할 수 있습니다. AEM Forms](https://help.adobe.com/en_US/livecycle/11.0/HardeningSecurity/index.html)용 보안 강화 [에서 &quot;사이트 간 요청 위조 공격으로부터 보호&quot;를 참조하십시오.

**허용된 Referer 예외:** 허용된 Referer Exception은 요청이 차단되는 허용된 레퍼러 목록의 하위 목록입니다. 허용된 참조 예외는 웹 응용 프로그램에만 적용됩니다. 허용된 레퍼러 중 하위 집합에서 특정 웹 응용 프로그램을 호출할 수 없는 경우 허용된 레퍼러 예외를 통해 레퍼러를 테스트할 수 차단 목록에 추가하다 있습니다. 응용 프로그램의 web.xml 파일에 허용되는 Referer 예외가 지정됩니다. (도움말 및 Tutorials 페이지에서 AEM Forms에 대한 보안 강화 및 강화에서 &quot;사이트 간 요청 위조 방지&quot;를 참조하십시오.)

## 허용되는 레퍼러가 작동하는 방식 {#how-allowed-referers-work}

AEM Forms에서는 CSRF 공격을 방지하는 데 도움이 되는 레퍼러 필터링을 제공합니다. 다음은 레퍼러 필터링이 작동하는 방식입니다.

1. Forms 서버는 호출에 사용된 HTTP 메서드를 확인합니다.

   * POST인 경우 Forms 서버에서 레퍼러 헤더 검사를 수행합니다.
   * CSRF_CHECK_GETS가 true로 설정된 경우를 제외하고 GET인 경우 Forms 서버는 레퍼러 헤더 검사를 수행하지 않습니다. 응용 프로그램의 web.xml 파일에 CSRF_CHECK_GETS가 지정됩니다. ( [경화 및 보안 안내서](https://help.adobe.com/en_US/livecycle/11.0/HardeningSecurity/index.html)에서 &quot;사이트 간 요청 위조 공격으로부터 보호&quot;를 참조하십시오.)

1. 양식 서버는 요청된 URI가 허용 목록에추가된인지 여부를 확인합니다.

   * URI가 허용 목록에추가된이면 서버가 요청을 전달합니다.
   * 요청한 URI가 허용 목록에추가된이 아닌 경우 서버는 요청의 레퍼러를 검색합니다.

1. 요청에 레퍼러가 있는 경우 서버가 레퍼러가 허용된 참조자인지 확인합니다. 허용되는 경우 서버에서 레퍼러 예외를 확인합니다.

   * 예외인 경우 요청이 차단됩니다.
   * 예외가 아닌 경우 요청이 전달됩니다.

1. 요청에 레퍼러가 없는 경우 서버에서 null 레퍼러가 허용되는지 확인합니다.

   * null 레퍼러가 허용되면 요청이 전달됩니다.
   * null 레퍼러가 허용되지 않는 경우 서버는 요청된 URI가 null 레퍼러에 대한 예외인지 확인하고 그에 따라 요청을 처리합니다.

## 허용되는 레퍼러 구성 {#configure-allowed-referers}

구성 관리자를 실행하면 기본 호스트 및 IP 주소 또는 양식 서버가 허용된 참조 목록에 추가됩니다. 관리 콘솔에서 이 목록을 편집할 수 있습니다.

1. 관리 콘솔에서 설정 > 사용자 관리 > 구성 > 허용된 레퍼러 URL 구성 을 클릭합니다.페이지 하단에 허용된 레퍼러 목록이 나타납니다.
1. 허용되는 레퍼러를 추가하려면 다음을 수행하십시오.

   * 허용된 참조 상자에 호스트 이름 또는 IP 주소를 입력합니다. 한 번에 허용되는 레퍼러를 두 개 이상 추가하려면 새 줄에 각 호스트 이름 또는 IP 주소를 입력합니다.
   * HTTP 포트 및 HTTPS 포트 상자에서 HTTP, HTTPS 또는 둘 다에 대해 허용할 포트를 지정합니다. 이 상자를 비워 두면 기본 포트(HTTP의 경우 포트 80, HTTPS의 경우 포트 443)가 사용됩니다. 상자에 `0`(영)을 입력하면 해당 서버의 모든 포트가 활성화됩니다. 특정 포트 번호를 입력하여 해당 포트만 활성화할 수도 있습니다.
   * 추가를 클릭합니다.

1. 허용된 참조 목록에서 항목을 제거하려면 목록에서 항목을 선택하고 삭제를 누릅니다.

   허용된 참조 목록이 비어 있으면 CSRF 기능이 작동하지 않고 시스템이 비보안 상태가 됩니다.

1. 허용된 레퍼러 목록을 변경한 후 AEM Forms 서버를 다시 시작합니다.
