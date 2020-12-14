---
title: 프록시 서버 도구(proxy.jar)
seo-title: 프록시 서버 도구(proxy.jar)
description: AEM의 프록시 서버 도구에 대해 알아보십시오.
seo-description: AEM의 프록시 서버 도구에 대해 알아보십시오.
uuid: 2fc1df24-8d5a-4be7-83fa-238ae65591b0
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: ca98dc3c-7056-4cdc-b4d3-23e471da5730
docset: aem65
translation-type: tm+mt
source-git-commit: 4e5e6ef022dc9f083859e13ab9c86b622fc3d46e
workflow-type: tm+mt
source-wordcount: '1173'
ht-degree: 0%

---


# 프록시 서버 도구(proxy.jar){#proxy-server-tool-proxy-jar}

프록시 서버는 클라이언트와 서버 간의 요청을 재전달하는 중간 서버 역할을 합니다. 프록시 서버는 모든 클라이언트-서버 상호 작용을 추적하고 전체 TCP 통신에 대한 로그를 출력합니다. 따라서 주 서버에 액세스하지 않고도 진행 상황을 정확하게 모니터링할 수 있습니다.

해당 설치 폴더에서 프록시 서버를 찾을 수 있습니다.

* &lt;cq_install_path>/opt/helpers/proxy.jar
* &lt;crx_install_path>/opt/helpers/proxy.jar

기본 통신 프로토콜에 상관없이 프록시 서버를 사용하여 모든 클라이언트-서버 상호 작용을 모니터링할 수 있습니다. 예를 들어 다음 프로토콜을 모니터링할 수 있습니다.

* 웹 페이지용 HTTP
* 보안 웹 페이지를 위한 HTTPS
* 전자 메일 메시지에 대한 SMTP
* 사용자 관리를 위한 LDAP

예를 들어 TCP/IP 네트워크를 통해 통신하는 두 응용 프로그램 간에 프록시 서버를 배치할 수 있습니다.예: 웹 브라우저 및 AEM AEM 페이지를 요청할 때 발생하는 상황을 정확하게 모니터링할 수 있습니다.

## 프록시 서버 도구 {#starting-the-proxy-server-tool} 시작

이 도구는 AEM 설치의 /opt/helpers 폴더에 있습니다. 유형을 시작하려면 다음을 수행합니다.

```xml
java -jar proxy.jar <host> <remoteport> <localport> [options]
```

### 옵션 {#options}

* **q(자동 모드)** 콘솔 창에 요청을 쓰지 않습니다. 연결 속도를 늦추거나 출력을 파일에 로깅하는 경우(-logfile 옵션 참조) 사용합니다.
* **b(이진 모드)** 트래픽에서 특정 바이트 조합을 찾는 경우 이진 모드를 활성화합니다. 그런 다음 출력에는 16진수 및 문자 출력이 포함됩니다.
* **t(타임스탬프 로그 항목)** 각 로그 출력에 타임스탬프를 추가합니다. 타임스탬프가 초 단위의 것이므로 단일 요청을 확인하는 데 적합하지 않을 수 있습니다. 장시간 동안 프록시 서버를 사용하는 경우 특정 시간에 발생한 이벤트를 찾을 수 있습니다.
* **로그 파일  &lt;filename> (로그 파일에 쓰기)** 클라이언트-서버 대화를 로그 파일에 씁니다. 이 매개 변수는 조용한 모드에서도 작동합니다.
* **i  &lt;numindentions> (들여쓰기 추가)** 각 활성 연결은 가독성을 높이기 위해 들여쓰기됩니다. 기본값은 16개 수준입니다. (proxy.jar 버전 1.16의 새로운 기능).

## 프록시 서버 도구 {#uses-of-the-proxy-server-tool} 사용

다음 시나리오에서는 프록시 서버 도구를 사용할 수 있는 몇 가지 목적을 설명합니다.

**쿠키 및 해당 값 확인**

다음 로그 항목 예는 프록시 시작 이후 열린 6번째 연결에서 클라이언트가 보낸 모든 쿠키와 해당 값을 보여 줍니다.

```xml
C-6-#000635 -> [Cookie: cq3session=7e39bc51-ac72-3f48-88a9-ed80dbac0693; Show=ShowMode; JSESSIONID=68d78874-cabf-9444-84a4-538d43f5064d ]
```

**머리글 및 해당 값** 확인다음 로그 항목 예는 서버가 활성 상태 유지 연결을 만들 수 있고 내용 길이 헤더가 올바르게 설정되었음을 보여 줍니다.

```xml
S-7-#000017 -> [Connection: Keep-Alive ]
...
S-7-#000107 -> [Content-Length: 124 ]
```

**Keep-Alive 작동 여부 확인**

**클라이언트** 가 서버에 대한 연결을 다시 사용하여 여러 파일(페이지 코드, 사진, 스타일 시트 등)을 전송하는 유지-별칭 클라이언트가 항상 활성 상태를 유지하지 않으면 각 요청에 대해 새 연결을 설정해야 합니다.

keep-alive가 작동하는지 확인하려면

1. 프록시 서버를 시작합니다.
1. 페이지 요청

* 연결 카운터가 5-10개 연결을 넘지 않아야 합니다.
* keep-alive가 작동하지 않으면 연결 카운터가 빠르게 증가합니다.

**유실된 요청 찾기**

방화벽 및 디스패처가 있는 경우와 같이 복잡한 서버 설정에서 요청을 손실할 경우 프록시 서버를 사용하여 요청이 손실된 위치를 확인할 수 있습니다. 방화벽의 경우:

1. 방화벽 전에 프록시 시작
1. 방화벽 후 다른 프록시 시작
1. 요청을 받는 정도를 보려면 이 아이콘을 사용합니다.

**요청 보류**

때때로 요청 내어쓰기를 경험하는 경우:

1. proxy.jar를 시작합니다.
1. 각 항목에 타임스탬프가 있는 액세스 로그를 파일에 기다리거나 기록합니다.
1. 요청 내어쓰기를 시작하면 열린 연결 수와 문제를 일으키는 요청을 확인할 수 있습니다.

## 로그 메시지 형식 {#the-format-of-log-messages}

proxy.jar로 생성되는 로그 항목의 형식은 모두 다음과 같습니다.

```xml
[timestamp (optional)] [<b>C</b>lient|<b>S</b>erver]-[ConnectionNumber]-[BytePosition] ->[Character Stream]
```

예를 들어 웹 페이지에 대한 요청은 다음과 같이 나타날 수 있습니다.

```xml
C-0-#000000 -> [GET /author/prox.html?CFC_cK=1102938422341 HTTP/1.1 ]
```

* C는 이 항목이 클라이언트에서 왔음을 의미합니다(웹 페이지에 대한 요청임).
* 0은 연결 번호입니다(연결 카운터는 0부터 시작).
* # 00000을 바이트 스트림의 오프셋입니다. 첫 번째 항목이므로 오프셋은 0입니다.
* [GET &lt;?>] 는 HTTP 헤더(url) 중 하나의 예에서 요청의 컨텐츠입니다.

연결이 닫히면 다음 정보가 기록됩니다.

```xml
C-6-Finished: 758 bytes (1.0 kb/s)
S-6-Finished: 665 bytes (1.0 kb/s)
```

이것은 6번째 연결에서 클라이언트와 서버 사이에 전달된 바이트 수와 평균 속도를 보여줍니다.

## 로그 출력 예 {#an-example-of-log-output}

요청시 다음 코드를 생성하는 간단한 템플릿을 검토할 것입니다.

```xml
<html>
  <head>
    <title>Welcome</title>
  </head>
  <body>
    Welcome to Playground<br>
    <img src="/logo.gif">
  </body>
</html>
```

AEM이 localhost:4303에서 실행 중인 경우 다음과 같이 프록시 서버를 시작합니다.

```xml
java -jar proxy.jar localhost 4303 4444 -logfile test.log
```

프록시 서버 없이 서버(`localhost:4303`)에 액세스할 수 있지만, `localhost:4444`를 통해 액세스하면 프록시 서버에서 통신을 기록합니다. 브라우저를 열고 위 템플릿으로 만든 페이지에 액세스합니다. 그런 다음 로그 파일을 확인합니다.

>[!NOTE]
>
>proxy.jar 버전 1.14까지는 한 연결의 로그 항목이 동기화되지 않으므로 하나의 클라이언트/서버 연결의 로그 항목이 올바른 순차적 순서로 필요하지 않음을 의미합니다. 프록시 서버의 최신 버전(>=1.14)에는 이 문제가 없습니다.

시작할 때 다음 정보가 로그에 기록됩니다.

```xml
starting proxy for localhost:4303 on port 4444
using logfile: C:\CQUnify355default\opt\helpers\test.log
```

기본 HTML 페이지를 요청하는 첫 번째 연결(0)의 시작 부분에 다음 헤더 필드가 나열됩니다.

```xml
C-0-#000000 -> [GET /author/prox.html?CFC_cK=1102936796533 HTTP/1.1 ]
C-0-#000053 -> [Accept: image/gif, image/x-xbitmap, image/jpeg, image/pjpeg, application/vnd.ms-powerpoint, application/vnd.ms-excel, application/msword, appl]
C-0-#000194 -> [ication/x-shockwave-flash, */* ]
C-0-#000227 -> [Accept-Language: de-ch ]
C-0-#000251 -> [Accept-Encoding: gzip, deflate ]
C-0-#000283 -> [User-Agent: Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.0) ]
C-0-#000347 -> [Host: localhost:4444 ]
```

클라이언트가 연결 상태를 유지하도록 요청하면 서버가 동일한 연결을 통해 여러 파일을 보낼 수 있습니다.

```xml
C-0-#000369 -> [Connection: Keep-Alive ]
```

프록시 서버는 쿠키가 제대로 설정되어 있는지 여부를 확인하는 좋은 도구입니다. 여기에서 다음을 볼 수 있습니다.

* aem에서 생성된 cq3session 쿠키
* CFC에서 생성된 표시 모드 전환 쿠키
* JSESSIONID라는 쿠키;&lt;%@ page session=&quot;false&quot; %>를 사용하여 명시적으로 비활성화하지 않은 경우 JSP에서 자동으로 생성합니다.

```xml
C-0-#000393 -> [Cookie: Show=ShowMode; cq3session=3bce15cf-1575-1b4e-8ea6-0d1a0c64738e; JSESSIONID=4161a56b-f193-d748-88a5-e09c5ff7ef2a ]
C-0-#000514 -> [ ]
S-0-#000000 -> [HTTP/1.0 200 OK ]
```

요청 후 서버가 연결 0을 닫습니다. 요청에 물음표가 있기 때문에 [항상 유지]를 수행할 수 없습니다. 즉, 서버는 캐시된 버전을 반환할 수 없으므로 이 시점에서 컨텐츠 길이를 확인할 수 없습니다. 이 길이는 활성 상태 유지 연결에 필요합니다.

```xml
S-0-#000017 -> [Connection: Close ]
S-0-#000036 -> [Server: Communique Servlet Engine/3.5.5 ]
S-0-#000077 -> [Content-Type: text/html;charset=iso-8859-1 ]
S-0-#000121 -> [Date: Tue, 14 Dec 2004 09:46:44 GMT ]
S-0-#000158 -> [Set-Cookie: JSESSIONID=4161a56b-f193-d8-88a5-e09c5ff7ef2a;Path=/author ]
S-0-#000232 -> [ ]
```

여기에서 서버는 연결 0에서 HTML 코드 전송을 시작합니다.

```xml
S-0-#000234 -> [<html> ]
S-0-#000242 -> [.<head> ]
S-0-#000251 -> [..<title>Welcome</title> ]
S-0-#000277 -> [.</head> ]
S-0-#000287 -> [.<body> ]
S-0-#000296 -> [..Welcome to Playground<br> ]
S-0-#000325 -> [..<img src="/author/logo.gif"> ]
S-0-#000357 -> [.</body> ]
S-0-#000367 -> [</html>]
```

연결 0은 HTML 파일을 제공한 직후 닫힙니다.

```xml
C-0-Finished: 516 bytes (0.0 kb/s)
S-0-Finished: 374 bytes (0.0 kb/s)
```

이제 출력 시작: 연결 1이 HTML 코드에 포함된 이미지를 다운로드합니다.

```xml
C-1-#000000 -> [GET /author/logo.gif HTTP/1.1 ]
C-1-#000031 -> [Accept: */* ]
C-1-#000044 -> [Referer: http://localhost:4444/author/prox.html?CFC_cK=1102936796533 ]
C-1-#000114 -> [Accept-Language: de-ch ]
C-1-#000138 -> [Accept-Encoding: gzip, deflate ]
C-1-#000170 -> [User-Agent: Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.0) ]
C-1-#000234 -> [Host: localhost:4444 ]
```

클라이언트는 유지 연결을 다시 요청합니다.

```xml
C-1-#000256 -> [Connection: Keep-Alive ]
C-1-#000280 -> [Cookie: Show=ShowMode; cq3session=3bce15cf-1575-1b4e-8ea6-0d1a0c64738e; JSESSIONID=4161a56b-f193-d748-88a5-e09c5ff7ef2a ]
C-1-#000401 -> [ ]
S-1-#000000 -> [HTTP/1.0 200 OK ]
```

연결 1의 경우 이미지가 고정되어 있으므로 컨텐츠 길이를 알 수 있으므로 서버가 항상 활성 상태를 유지할 수 있습니다.

```xml
S-1-#000017 -> [Connection: Keep-Alive ]
S-1-#000041 -> [Server: Communique Servlet Engine/3.5.5 ]
S-1-#000082 -> [Content-Type: image/gif ]
```

서버는 연결 1에서 이미지의 컨텐츠 길이를 반환합니다.

```xml
S-1-#000107 -> [Content-Length: 124 ]
S-1-#000128 -> [Date: Tue, 14 Dec 2004 09:46:44 GMT ]
S-1-#000165 -> [ ]
```

이제 컨텐츠 길이가 설정되었으므로 서버는 연결 1에서 이미지 데이터를 전송합니다.

```xml
S-1-#000167 -> [GIF87a..........................,.......
...I....0.A..8......YDA.W...1..`i.`..6...Z...$@.F..)`..f..A.....iu.........$..;]
```

지속가능 시간 초과에 도달한 후 연결 1도 닫힙니다.

```xml
S-1-Finished: 291 bytes (0.0 kb/s)
C-1-Finished: 403 bytes (0.0 kb/s)
```

위의 예제는 두 연결이 순차적으로 발생하므로 비교적 간단합니다.

* 먼저 서버가 HTML 코드를 반환합니다.
* 그러면 브라우저가 이미지를 요청하고 새 연결을 엽니다

실제로, 페이지는 이미지, 스타일 시트, JavaScript 파일 등에 대한 여러 개의 병렬 요청을 생성할 수 있습니다. 즉, 로그에 병렬 열린 연결의 항목이 겹칩니다. 이 경우 가독성을 향상시키려면 -i 옵션을 사용하는 것이 좋습니다.
