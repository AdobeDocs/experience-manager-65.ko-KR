---
title: HTML 5 양식 최적화
description: HTML5 양식의 출력 크기를 최적화할 수 있습니다.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
feature: Mobile Forms
exl-id: 14309ebd-8d00-4ca5-b4ab-44d80d97d066
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---

# HTML 5 양식 최적화 {#optimizing-html-forms}

HTML5 forms는 HTML5 형식으로 양식을 렌더링합니다. 결과 출력은 형태의 크기 및 형태의 이미지와 같은 요인에 따라 클 수 있다. 데이터 전송을 최적화하려면 요청이 제공되는 웹 서버를 사용하여 HTML 응답을 압축하는 것이 좋습니다. 이 접근 방식은 응답 크기, 네트워크 트래픽 및 서버와 클라이언트 컴퓨터 간에 데이터를 스트리밍하는 데 필요한 시간을 줄입니다.

이 문서에서는 JBoss를 사용하여 Apache 웹 서버 2.0 32비트에 대한 압축을 활성화하는 데 필요한 단계에 대해 설명합니다.

>[!NOTE]
>
>다음 지침은 Apache 웹 서버 2.0 32비트 이외의 서버에는 적용되지 않습니다.

운영 체제에 적용할 수 있는 Apache 웹 서버 소프트웨어를 얻습니다.

* Windows의 경우 Apache HTTP Server 프로젝트 사이트에서 Apache 웹 서버를 다운로드합니다.
* Solaris 64비트의 경우 Sunfreeware for Solaris 웹 사이트에서 Apache 웹 서버를 다운로드합니다.
* Linux의 경우 Apache 웹 서버가 Linux 시스템에 사전 설치됩니다.

Apache는 HTTP 또는 AJP 프로토콜을 사용하여 JBoss와 통신할 수 있습니다.

1. 에서 다음 모듈 구성의 주석 처리를 제거합니다. *APACHE_HOME/conf/httpd.conf* 파일.

   ```java
   LoadModule proxy_balancer_module modules/mod_proxy.so
   LoadModule proxy_balancer_module modules/mod_proxy_http.so
   LoadModule deflate_module modules/mod_deflate.so
   ```

   >[!NOTE]
   >
   >Linux의 경우 기본 APACHE_HOME 디렉토리는 /etc/httpd/입니다.

1. JBoss의 포트 8080에서 프록시를 구성합니다.

   에 다음 구성 추가 *APACHE_HOME/conf/httpd.conf* 구성 파일입니다.

   ```java
   ProxyPass / https://<server_Name>:8080/
   ProxyPassReverse / https://<server_Name>:8080/
   ```

   >[!NOTE]
   >
   >프록시를 사용하는 경우 다음 구성 변경이 필요합니다.
   >
   >* 액세스: *https://&lt;server>:&lt;port>/system/console/configMgr*
   * Apache Sling Referrer Filter 구성 편집
   * 호스트 허용에서 프록시 서버에 대한 항목을 추가합니다

1. 압축을 활성화합니다.

   에 다음 구성 추가 *APACHE_HOME/conf/httpd.conf* 구성 파일입니다.

   ```xml
   <Location /content/xfaforms>
     <IfModule mod_deflate.c>
        SetOutputFilter DEFLATE
        # Don’t compress
        SetEnvIfNoCase Request_URI \.(?:gif|jpe?g|png)$ no-gzip dont-vary
        SetEnvIfNoCase Request_URI \.(?:exe|t?gz|zip|bz2|sit|rar)$ no-gzip dont-vary
       #Dealing with proxy servers
   
        <IfModule mod_headers.c>
           Header append Vary User-Agent
        </IfModule>
     </IfModule>
   </Location>
   ```

1. AEM 서버에 액세스하려면 https:// 를 사용합니다.[Apache_server]:80.
