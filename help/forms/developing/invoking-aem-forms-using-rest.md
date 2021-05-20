---
title: REST 요청을 사용하여 AEM Forms 호출
seo-title: REST 요청을 사용하여 AEM Forms 호출
description: REST 요청을 사용하여 Workbench에서 만든 프로세스를 호출합니다.
seo-description: REST 요청을 사용하여 Workbench에서 만든 프로세스를 호출합니다.
uuid: 3a19a296-f3fe-4e50-9143-b68aed37f9ef
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: df7b60bb-4897-479e-a05e-1b1e9429ed87
role: Developer
exl-id: 991fbc56-f144-4ae6-b010-8d02f780d347
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2520'
ht-degree: 0%

---

# REST 요청을 사용하여 AEM Forms 호출 {#invoking-aem-forms-using-rest-requests}

**이 문서의 샘플 및 예제는 JEE 환경의 AEM Forms용입니다.**

Workbench에서 만든 프로세스는 REST(대리 상태 전송) 요청을 통해 호출할 수 있도록 구성할 수 있습니다. REST 요청은 HTML 페이지에서 전송됩니다. 즉, REST 요청을 사용하여 웹 페이지에서 직접 Forms 프로세스를 호출할 수 있습니다. 예를 들어 웹 페이지의 새 인스턴스를 열 수 있습니다. 그런 다음 Forms 프로세스를 호출하고 HTTP POST 요청에서 전송된 데이터로 렌더링된 PDF 문서를 로드할 수 있습니다.

두 가지 유형의 HTML 클라이언트가 있습니다. 첫 번째 HTML 클라이언트는 JavaScript로 작성된 AJAX 클라이언트입니다. 두 번째 클라이언트는 전송 단추가 포함된 HTML 양식입니다. HTML 기반 클라이언트 응용 프로그램만 가능한 REST 클라이언트가 아닙니다. HTTP 요청을 지원하는 모든 클라이언트 응용 프로그램은 REST 호출을 사용하여 서비스를 호출할 수 있습니다. 예를 들어 PDF 양식에서 REST 호출을 사용하여 서비스를 호출할 수 있습니다. ([Acrobat에서 MyApplication/EncryptDocument 프로세스 호출](#rest-invocation-examples)을 참조하십시오.)

REST 요청을 사용할 때는 Forms 서비스를 직접 호출하지 않는 것이 좋습니다. 대신 Workbench에서 만든 프로세스를 호출합니다. REST 호출을 위한 프로세스를 만들 때는 프로그래밍 방식의 시작 지점을 사용하십시오. 이 경우 REST 엔드포인트가 자동으로 추가됩니다. Workbench에서 프로세스 만들기에 대한 내용은 [Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63) 사용을 참조하십시오.

REST를 사용하여 서비스를 호출하는 경우 AEM Forms 사용자 이름과 암호를 입력하라는 메시지가 표시됩니다. 그러나 사용자 이름과 암호를 지정하지 않으려면 서비스 보안을 비활성화할 수 있습니다.

REST를 사용하여 Forms 서비스를 호출하려면(프로세스가 활성화되면 프로세스가 서비스가 됨) REST 엔드포인트를 구성합니다. ([관리 도움말](https://www.adobe.com/go/learn_aemforms_admin_63)의 &quot;끝점 관리&quot;를 참조하십시오.)

REST 엔드포인트가 구성된 후에는 HTTP GET 메서드 또는 POST 메서드를 사용하여 Forms 서비스를 호출할 수 있습니다.

```java
 action="https://hiro-xp:8080/rest/services/[ServiceName]/[OperationName]:[ServiceVersion]" method="post" enctype="multipart/form-data"
```

필수 `ServiceName` 값은 호출할 Forms 서비스의 이름입니다. 선택적 `OperationName` 값은 서비스 작업의 이름입니다. 이 값을 지정하지 않으면 기본적으로 이 이름은 `invoke`으로 설정됩니다. 이 이름은 프로세스를 시작하는 작업 이름입니다. 선택적 `ServiceVersion` 값은 X.Y 형식으로 인코딩된 버전입니다. 이 값을 지정하지 않으면 최신 버전이 사용됩니다. `enctype` 값은 `application/x-www-form-urlencoded`일 수도 있습니다.

## 지원되는 데이터 형식 {#supported-data-types}

REST 요청을 사용하여 AEM Forms 서비스를 호출할 때 다음 데이터 유형이 지원됩니다.

* 문자열 및 정수와 같은 Java 기본 데이터 유형
* `com.adobe.idp.Document` 데이터 유형
* `org.w3c.Document` 및 `org.w3c.Element` 등의 XML 데이터 유형
* `java.util.List` 및 `java.util.Map` 등의 컬렉션 개체

   이러한 데이터 유형은 일반적으로 Workbench에서 생성된 프로세스에 입력 값으로 수락됩니다.

   Forms 서비스가 HTTP POST 메서드와 함께 호출되면 HTTP 요청 본문 내에 인수가 전달됩니다. AEM Forms 서비스의 서명에 문자열 입력 매개 변수가 있는 경우 요청 본문에 입력 매개 변수의 텍스트 값이 포함될 수 있습니다. 서비스의 서명이 여러 문자열 매개 변수를 정의하는 경우 요청은 HTTP의 `application/x-www-form-urlencoded` 표기법을 따르며 매개 변수의 이름을 양식의 필드 이름으로 사용할 수 있습니다.

   Forms 서비스가 문자열 매개 변수를 반환하는 경우 결과는 출력 매개 변수의 텍스트 표현입니다. 서비스에서 여러 문자열 매개 변수를 반환하는 경우 출력 매개 변수를 다음 형식으로 인코딩하는 XML 문서가 표시됩니다.
   ` <result> <output-paramater1>output-parameter-value-as-string</output-paramater1> . . . <output-paramaterN>output-parameter-value-as-string</output-paramaterN> </result>`

   >[!NOTE]
   >
   >`output-paramater1` 값은 출력 매개 변수 이름을 나타냅니다.

   Forms 서비스에 `com.adobe.idp.Document` 매개 변수가 필요한 경우 HTTP POST 메서드를 사용해야만 서비스를 호출할 수 있습니다. 서비스에 하나의 `com.adobe.idp.Document` 매개 변수가 필요한 경우 HTTP 요청 본문은 입력 Document 개체의 내용이 됩니다.

   AEM Forms 서비스에 여러 개의 입력 매개 변수가 필요한 경우 HTTP 요청 본문은 RFC 1867에 정의된 대로 다중 부분 MIME 메시지여야 합니다. (RFC 1867은 웹 브라우저에서 웹 사이트에 파일을 업로드하기 위해 사용하는 표준입니다.) 각 입력 매개 변수는 다중 부분 메시지의 개별 부분으로 전송되고 `multipart/form-data` 형식으로 인코딩되어야 합니다. 각 부품의 이름은 매개변수 이름과 일치해야 합니다.

   목록 및 맵은 Workbench에서 만든 AEM Forms 프로세스에 대한 입력 값으로도 사용됩니다. 따라서 REST 요청을 사용할 때 이러한 데이터 유형을 사용할 수 있습니다. Java 배열은 AEM Forms 프로세스에 대한 입력 값으로 사용되지 않으므로 지원되지 않습니다.

   입력 매개 변수가 목록인 경우 REST 클라이언트는 매개 변수를 여러 번 지정하여(목록의 각 항목에 대해 한 번) 전송할 수 있습니다. 예를 들어, A가 문서 목록인 경우 입력은 A라는 여러 부분으로 구성된 다중 부분 메시지여야 합니다. 이 경우 A라는 각 부품이 입력 목록의 항목이 됩니다. B가 문자열 목록인 경우 입력은 B라는 여러 필드로 구성된 `application/x-www-form-urlencoded` 메시지일 수 있습니다. 이 경우 B라는 각 양식 필드는 입력 목록의 항목이 됩니다.

   입력 매개 변수가 맵이고 서비스 전용 입력 매개 변수인 경우 입력 메시지의 모든 부분/필드가 맵에서 키/값 레코드가 됩니다. 각 부품/필드의 이름이 레코드의 키가 됩니다. 각 부품/필드의 컨텐츠가 레코드의 값이 됩니다.

   입력 맵이 서비스 전용 입력 매개 변수가 아닌 경우 매개 변수 이름과 레코드 키의 연결로 이름이 지정된 매개 변수를 사용하여 맵에 속한 각 키/값 레코드를 전송할 수 있습니다. 예를 들어 다음 키/값 쌍 목록을 사용하여 `attributes` 이라는 입력 맵을 보낼 수 있습니다.

   `attributesColor=red`

   `attributesShape=box`

   `attributesWidth=5`

   이는 다음 세 개의 레코드 맵으로 변환됩니다.`Color=red`, `Shape=box` 및 `Width=5`

   목록 및 맵 유형의 출력 매개 변수는 결과 XML 메시지의 일부가 됩니다. 출력 목록은 목록에 있는 각 항목에 대해 하나의 요소가 있는 일련의 XML 요소로 XML에 표시됩니다. 모든 요소에는 출력 목록 매개 변수와 동일한 이름이 지정됩니다. 각 XML 요소의 값은 다음 두 가지 중 하나입니다.

* 목록에 있는 항목의 텍스트 표현(목록이 문자열 유형으로 구성된 경우)
* 문서의 컨텐츠를 가리키는 URL(목록이 `com.adobe.idp.Document` 개체로 구성된 경우)

   다음 예는 정수 목록인 *list*라는 단일 출력 매개 변수를 가진 서비스에서 반환한 XML 메시지입니다.
   ` <result>   <list>12345</list>   . . .   <list>67890</list>  </result>`출력 맵 매개 변수는 결과 XML 메시지에 맵의 각 레코드에 대해 하나의 요소가 있는 일련의 XML 요소로 표시됩니다. 모든 요소에는 맵 레코드의 키와 동일한 이름이 지정됩니다. 각 요소의 값은 맵 레코드 값의 텍스트 표현(맵이 문자열 값이 있는 레코드로 구성된 경우) 또는 문서 컨텐츠를 가리키는 URL입니다(맵이 `com.adobe.idp.Document` 값이 있는 레코드로 구성된 경우). 다음은 `map` 라는 단일 출력 매개 변수를 가진 서비스에서 반환한 XML 메시지의 예입니다. 이 매개 변수 값은 문자를 `com.adobe.idp.Document` 개체와 연결하는 레코드로 구성된 맵입니다.
   ` <result>   http://localhost:8080/DocumentManager/docm123/4567   . . .   <Z>http://localhost:8080/DocumentManager/docm987/6543</Z>  </result>  `

## 비동기 호출 {#asynchronous-invocations}

인간 중심 장기 프로세스와 같은 일부 AEM Forms 서비스는 완료하는 데 오랜 시간이 필요합니다. 이러한 서비스는 비차단 방식으로 비동기식으로 호출할 수 있습니다. ([인간 중심의 장기 프로세스 호출](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes) 참조)

다음 예와 같이 호출 URL에서 `services` 을 `async_invoke` 로 대체하여 AEM Forms 서비스를 비동기식으로 호출할 수 있습니다.

```java
 http://localhost:8080/rest/async_invoke/SomeService. SomeOperation?integer_input_variable=123&string_input_variable=abc
```

이 URL은 이 호출을 담당하는 작업의 식별자 값(&quot;text/plain&quot; 형식)을 반환합니다.

비동기 호출의 상태는 `async_status` 로 대체된 `services` 호출 URL을 사용하여 검색할 수 있습니다. URL에는 이 호출과 연결된 작업의 식별자 값을 지정하는 `job_id` 매개 변수가 포함되어야 합니다. 예:

```java
 http://localhost:8080/rest/async_status/SomeService.SomeOperation?job_id=2345353443366564
```

이 URL은 작업 관리자의 사양에 따라 작업 상태를 인코딩하는 정수 값(&quot;text/plain&quot; 형식)을 반환합니다(예: 2는 실행 중임을 의미하며 3은 완료됨을 의미하며 4는 실패함 등).

작업이 완료되면 URL은 서비스가 동기식으로 호출된 것처럼 동일한 결과를 반환합니다.

작업이 완료되고 결과가 검색되면 작업이 `services`과 함께 호출 URL을 사용하여 `async_dispose`로 대체될 수 있습니다. URL에는 작업의 식별자 값을 지정하는 `job_id` 매개 변수도 포함되어야 합니다. 예:

```java
 http://localhost:8080/rest/async_dispose/SomeService.SomeOperation?job_id=2345353443366564
```

작업이 성공적으로 처리되면 이 URL은 빈 메시지를 반환합니다.

## {#error-reporting} 보고 오류

서버에서 throw되는 예외로 인해 동기 또는 비동기 호출 요청을 완료할 수 없는 경우 HTTP 응답 메시지의 일부로 예외가 보고됩니다. 호출 URL(또는 비동기 호출의 경우 `async_result` URL에 .xml 접미사가 없는 경우 REST 공급자는 HTTP 코드 `500 Internal Server Error` 다음에 예외 메시지를 반환합니다.

호출 URL(또는 비동기 호출의 경우 `async_result` URL에 .xml 접미사가 있는 경우, REST 공급자는 HTTP 코드 `200 OK`를 반환하고 다음 형식의 예외를 설명하는 XML 문서를 반환합니다.

```xml
 <exception>
       <exception_class_name>[
       <DSCError>
          <componentUID>component_UUD</componentUID>
         <errorCode>error_code</errorCode>
         <minorCode>minor_code</minorCode>
         <message>error_message</message>
       </DSCError>
 ]
       <message>exception_message</message>
     <stackTrace>exception_stack_trace</stackTrace>
       </exception_class_name>
     <exception>
       </exception>
 </exception>
```

`DSCError` 요소는 선택 사항이며 예외가 `com.adobe.idp.dsc.DSCException` 인스턴스인 경우에만 나타납니다.

## 보안 및 인증 {#security-and-authentication}

AEM Forms 관리자는 보안 전송을 통해 REST 호출을 제공하기 위해 AEM Forms을 호스팅하는 J2EE 애플리케이션 서버에서 HTTPS 프로토콜을 활성화할 수 있습니다. 이 구성은 J2EE 애플리케이션 서버에만 적용됩니다.양식 서버 구성의 일부가 아닙니다.

>[!NOTE]
>
>REST 종단점을 통해 프로세스를 노출하려는 Workbench 개발자로서, XSS 취약성 문제를 기억하십시오. XSS 취약점은 쿠키를 훔치거나 조작하고, 컨텐츠의 프레젠테이션을 수정하고, 기밀 정보를 손상시키는 데 사용할 수 있습니다. XSS 취약성 문제가 발생하는 경우 추가 입력 및 출력 데이터 유효성 검사 규칙으로 프로세스 논리를 확장하는 것이 좋습니다.

## REST 호출을 지원하는 AEM Forms 서비스 {#aem-forms-services-that-support-rest-invocation}

직접 서비스와 비교하여 Workbench를 사용하여 만든 프로세스를 호출하는 것이 좋지만 REST 호출을 지원하는 일부 AEM Forms 서비스가 있습니다. 프로세스를 직접 호출하는 것이 권장되는 이유는 프로세스를 호출하는 것이 더 효율적이기 때문입니다. 다음 시나리오를 고려하십시오. REST 클라이언트에서 정책을 작성한다고 가정합니다. 즉, REST 클라이언트가 정책 이름, 오프라인 임대 기간과 같은 값을 정의하도록 합니다.

정책을 만들려면 `PolicyEntry` 개체와 같은 복잡한 데이터 유형을 정의해야 합니다. `PolicyEntry` 개체는 정책과 연결된 권한과 같은 속성을 정의합니다. ( [정책 만들기](/help/forms/developing/protecting-documents-policies.md#creating-policies) 참조)

정책을 만들기 위해 REST 요청을 보내는 대신( `PolicyEntry` 개체 등 복잡한 데이터 형식 정의 포함) Workbench를 사용하여 정책을 만드는 프로세스를 만듭니다. 프로세스 이름을 정의하는 문자열 값 또는 오프라인 임대 기간을 정의하는 정수와 같은 기본 입력 변수를 허용하는 프로세스를 정의합니다.

이렇게 하면 작업에 필요한 복잡한 데이터 형식이 포함된 REST 호출 요청을 만들 필요가 없습니다. 이 프로세스는 복잡한 데이터 유형을 정의하며, REST 클라이언트에서 수행하는 모든 작업은 프로세스를 호출하고 기본 데이터 유형을 전달합니다. REST를 사용하여 프로세스를 호출하는 방법에 대한 자세한 내용은 [REST](#rest-invocation-examples)를 사용하여 MyApplication/EncryptDocument 프로세스 호출 을 참조하십시오.

다음 목록은 직접 REST 호출을 지원하는 AEM Forms 서비스를 지정합니다.

* Distiller 서비스
* Rights Management 서비스
* GeneratePDF 서비스
* Generate3dPDF 서비스
* FormDataIntegration

## REST 호출 예 {#rest-invocation-examples}

다음 REST 호출 예가 제공됩니다.

* AEM Forms 프로세스에 부울 값 전달
* AEM Forms 프로세스에 날짜 값 전달
* AEM Forms 프로세스에 문서 전달
* AEM Forms 프로세스에 문서 및 텍스트 값 전달
* AEM Forms 프로세스에 열거형 값 전달
* REST를 사용하여 MyApplication/EncryptDocument 프로세스를 호출하는 중
* Acrobat에서 MyApplication/EncryptDocument 프로세스를 호출하는 중

   각 예제는 AEM Forms 프로세스에 다양한 데이터 유형을 전달하는 방법을 보여줍니다

**프로세스에 부울 값 전달**

다음 HTML 예는 두 개의 `Boolean` 값을 `RestTest2` 라는 AEM Forms 프로세스에 전달합니다. 호출 메서드의 이름은 `invoke`이고 버전은 1.0입니다. HTML Post 메서드가 사용되고 있습니다.

```html
 <html>
 <body>
 
 <form name="input" action="http://localhost:9080/rest/services/RestTest2/invoke/1.0" method="post">
 
 Boolean 1: <input type="text" name="inBooleanList" value="true">
 Boolean 2: <input type="text" name="inBooleanList" value="false">
 <input type="submit" value="Submit">
 
 </form>
 
 </body>
 </html>
```

**프로세스에 날짜 값 전달**

다음 HTML 예는 날짜 값을 `SOAPEchoService` AEM Forms 프로세스에 전달합니다. 호출 메서드의 이름은 `echoCalendar`입니다. HTML `Post` 메서드가 사용된다는 점에 주목합니다.

```html
 <html>
 <body>
 
 <form name="input" action="http://localhost:9080/rest/services/SOAPEchoService/echoCalendar" method="post">
 
 Date: <input type="text" name="value-to-echo" value="2009-01-02T12:15:30Z">
 <input type="submit" value="Submit">
 
 </form>
 
 </body>
 </html>
```

**프로세스에 문서 전달**

다음 HTML 예는 PDF 문서가 필요한 `MyApplication/EncryptDocument`(이)라는 AEM Forms 프로세스를 호출합니다. 이 프로세스에 대한 정보는 [MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)을 사용하여 AEM Forms 호출 을 참조하십시오.

```html
 <html>
 <body>
 
 <form name="input" action="http://localhost:9080/rest/services/MyApplication/EncryptDocument/invoke" method="post"
          enctype="multipart/form-data">
 
 File: <input type="file" name="value-to-echo">
 <input type="submit" value="Submit"/>
 
 </form>
 
 </body>
 </html>
```

**프로세스에 문서 및 텍스트 값 전달**

다음 HTML 예는 문서와 두 개의 텍스트 값이 필요한 `RestTest3` 이라는 AEM Forms 프로세스를 호출합니다. HTML Post 메서드가 사용됩니다.

```html
 <html>
 <body>
 
 <form name="input" action="http://localhost:9080/rest/services/RestTest3" method="post"
          enctype="multipart/form-data">
 
 Doc: <input type="file" name="inDoc">
 String 1: <input type="text" name="inListOfStrings" value="hello">
 String 2: <input type="text" name="inListOfStrings" value="privet">
 <input type="submit" value="Submit"/>
 
 </form>
 
 </body>
 </html>
```

**열거형 값을 프로세스에 전달**

다음 HTML 예는 열거형 값이 필요한 `SOAPEchoService`(이)라는 AEM Forms 프로세스를 호출합니다. HTML Post 메서드가 사용됩니다.

```html
 <html>
 <body>
 
 <form name="input" action="https://hiro-xp:8080/rest/services/SOAPEchoService/echoEnum" method="post">
 
 Color Enum Value: <input type="text" name="value-to-echo" value="green">
 <input type="submit" value="Submit">
 
 </form>
 
 </body>
 </html>
```

**REST를 사용하여 MyApplication/EncryptDocument 프로세스를 호출하는 중**

REST를 사용하여 *MyApplication/EncryptDocument*&#x200B;라는 AEM Forms 단기 프로세스를 호출할 수 있습니다.

>[!NOTE]
>
>이 프로세스는 기존 AEM Forms 프로세스를 기반으로 하지 않습니다. 코드 예제와 함께 사용하려면 workbench를 사용하여 `MyApplication/EncryptDocument` 프로세스를 만듭니다. ([Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63) 사용 을 참조하십시오.)

이 프로세스가 호출되면 다음 작업을 수행합니다.

1. 프로세스에 전달되는 보안되지 않은 PDF 문서를 가져옵니다. 이 작업은 `SetValue` 작업을 기반으로 합니다. 이 프로세스의 입력 매개 변수는 `inDoc` 프로세스 변수입니다.`document`
1. 암호로 PDF 문서를 암호화합니다. 이 작업은 `PasswordEncryptPDF` 작업을 기반으로 합니다. 암호로 암호화된 PDF 문서는 `outDoc` 프로세스 변수에 반환됩니다.

   REST 요청을 사용하여 이 프로세스를 호출하면 암호화된 PDF 문서가 웹 브라우저에 표시됩니다. PDF 문서를 보기 전에 암호를 지정합니다(보안을 사용하지 않는 경우). 다음 HTML 코드는 `MyApplication/EncryptDocument` 프로세스에 대한 REST 호출 요청을 나타냅니다.

   ```html
    <html>
    <body>
    <form action="https://hiro-xp:8080/rest/services/MyApplication/EncryptDocument" method="post" enctype="multipart/form-data">
         <p>Chose a PDF file (.pdf) to send to the EncryptDocument process.</p>
         <p>file:
           <input type="file" name="inDoc" />
         </p>
         <p>
           <input type="submit"/>
         </p>
    </form>
    </body>
   ```

**Acrobat에서 MyApplication/EncryptDocument 프로세스를 호출하는 중** {#invoke-process-acrobat}

REST 요청을 사용하여 Acrobat에서 Forms 프로세스를 호출할 수 있습니다. 예를 들어 *MyApplication/EncryptDocument* 프로세스를 호출할 수 있습니다. Acrobat에서 Forms 프로세스를 호출하려면 디자이너 내의 XDP 파일에 제출 단추를 놓습니다. ( [디자이너 도움말](https://www.adobe.com/go/learn_aemforms_designer_63) 참조)

다음 그림과 같이 단추의 *URL에 제출* 필드 내에서 프로세스를 호출할 URL을 지정합니다.

프로세스를 호출하는 전체 URL은 https://hiro-xp:8080/rest/services/MyApplication/EncryptDocument입니다.

프로세스에 입력 값으로 PDF 문서가 필요한 경우, 이전 그림에서 보듯이 양식을 PDF로 제출하십시오. 또한 프로세스를 성공적으로 호출하려면 PDF 문서를 반환해야 합니다. 그렇지 않으면 반환 값을 처리할 수 없으며 오류가 발생합니다. 입력 프로세스 변수의 이름을 지정하지 않아도 됩니다. 예를 들어 *MyApplication/EncryptDocument* 프로세스에는 `inDoc`라는 입력 변수가 있습니다. 양식이 PDF로 제출되는 한 문서에 지정할 필요가 없습니다.

양식 데이터를 XML로 Forms 프로세스에 제출할 수도 있습니다. XML 데이터를 제출하려면 `Submit As` 드롭다운에서 XML을 지정하는지 확인하십시오. 프로세스의 반환 값은 PDF 문서여야 하므로 Acrobat에 PDF 문서가 표시됩니다.
