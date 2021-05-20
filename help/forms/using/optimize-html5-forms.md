---
title: HTML5 양식 최적화
seo-title: HTML5 양식 최적화
description: HTML5 양식의 출력 크기를 최적화할 수 있습니다.
seo-description: HTML5 양식의 출력 크기를 최적화할 수 있습니다.
uuid: 959f0b6a-9e4d-478a-afa8-4c39011fdf7a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: bdb9edc2-6a37-4d3f-97d5-0fc5664316be
feature: Mobile Forms
exl-id: 14309ebd-8d00-4ca5-b4ab-44d80d97d066
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 0%

---

# HTML5 양식 최적화 {#optimizing-html-forms}

HTML5 양식은 HTML5 형식으로 양식을 렌더링합니다. 결과 출력은 양식 크기 및 양식 이미지와 같은 요소에 따라 클 수 있습니다. 데이터 전송을 최적화하기 위해 권장되는 방법은 요청을 처리할 웹 서버를 사용하여 HTML 응답을 압축하는 것입니다. 이 접근 방식은 응답 크기, 네트워크 트래픽, 서버와 클라이언트 시스템 간의 데이터를 스트리밍하는 데 필요한 시간을 줄입니다.

이 문서에서는 JBoss를 사용하여 Apache Web Server 2.0 32비트에 대해 압축을 활성화하는 데 필요한 단계에 대해 설명합니다.

>[!NOTE]
>
>Apache Web Server 2.0 32비트 이외의 서버에는 다음 지침이 적용되지 않습니다.

운영 체제에 적용할 수 있는 Apache 웹 서버 소프트웨어를 얻습니다.

* Windows의 경우 Apache HTTP Server Project 사이트에서 Apache 웹 서버를 다운로드합니다.
* Solaris 64비트의 경우 Solaris용 Sunfreeware 웹 사이트에서 Apache 웹 서버를 다운로드합니다.
* Linux의 경우 Apache 웹 서버는 Linux 시스템에 미리 설치됩니다.

Apache는 HTTP 또는 AJP 프로토콜을 사용하여 JBoss와 통신할 수 있습니다.

1. *APACHE_HOME/conf/httpd.conf* 파일에서 다음 모듈 구성의 주석을 해제합니다.

   ```java
   LoadModule proxy_balancer_module modules/mod_proxy.so
   LoadModule proxy_balancer_module modules/mod_proxy_http.so
   LoadModule deflate_module modules/mod_deflate.so
   ```

   >[!NOTE]
   >
   >Linux의 경우 기본 APACHE_HOME 디렉토리는 /etc/httpd/ 입니다.

1. JBoss의 포트 8080에서 프록시를 구성합니다.

   다음 구성을 *APACHE_HOME/conf/httpd.conf* 구성 파일에 추가합니다.

   ```java
   ProxyPass / https://<server_Name>:8080/
   ProxyPassReverse / https://<server_Name>:8080/
   ```

   >[!NOTE]
   >
   >프록시를 사용하는 경우 다음 구성 변경 사항이 필요합니다.
   >
   >* 액세스:*https://&lt;server>:&lt;port>/system/console/configMgr*
   * Apache Sling 레퍼러 필터의 구성을 편집합니다
   * 허용 호스트에서 프록시 서버의 항목을 추가합니다


1. 압축을 활성화합니다.

   다음 구성을 *APACHE_HOME/conf/httpd.conf* 구성 파일에 추가합니다.

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

1. AEM 서버에 액세스하려면 https://[Apache_server]:80을 사용하십시오.
