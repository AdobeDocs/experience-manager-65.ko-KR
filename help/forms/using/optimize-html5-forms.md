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
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 0%

---


# HTML5 양식 최적화 {#optimizing-html-forms}

HTML5 양식은 HTML5 형식으로 양식을 렌더링합니다. 결과 출력은 양식의 양식 크기 및 이미지와 같은 요소에 따라 클 수 있습니다. 데이터 전송을 최적화하기 위해 권장 방법은 요청이 제공되는 웹 서버를 사용하여 HTML 응답을 압축하는 것입니다. 이 방법을 사용하면 응답 크기, 네트워크 트래픽 및 서버와 클라이언트 컴퓨터 간의 데이터를 스트리밍하는 데 필요한 시간을 줄일 수 있습니다.

이 문서에서는 JBoss와 함께 Apache Web Server 2.0 32비트의 압축을 활성화하는 데 필요한 단계에 대해 설명합니다.

>[!NOTE]
>
>다음 지침은 Apache Web Server 2.0 32비트 이외의 서버에는 적용되지 않습니다.

운영 체제에 적용할 수 있는 Apache 웹 서버 소프트웨어를 가져옵니다.

* Windows의 경우 Apache HTTP Server 프로젝트 사이트에서 Apache 웹 서버를 다운로드합니다.
* Solaris 64비트의 경우 Solaris용 Sunfreeware 웹 사이트에서 Apache 웹 서버를 다운로드합니다.
* Linux의 경우 Apache 웹 서버가 Linux 시스템에 미리 설치됩니다.

Apache는 HTTP 또는 AJP 프로토콜을 사용하여 JBoss와 통신할 수 있습니다.

1. *APACHE_HOME/conf/httpd.conf* 파일에서 다음 모듈 구성의 주석을 해제합니다.

   ```java
   LoadModule proxy_balancer_module modules/mod_proxy.so
   LoadModule proxy_balancer_module modules/mod_proxy_http.so
   LoadModule deflate_module modules/mod_deflate.so
   ```

   >[!NOTE]
   >
   >Linux의 경우 기본 APACHE_HOME 디렉토리는 /etc/httpd/입니다.

1. JBoss의 포트 8080에서 프록시를 구성합니다.

   *APACHE_HOME/conf/httpd.conf* 구성 파일에 다음 구성을 추가합니다.

   ```java
   ProxyPass / https://<server_Name>:8080/
   ProxyPassReverse / https://<server_Name>:8080/
   ```

   >[!NOTE]
   >
   >프록시를 사용할 때는 다음 구성을 변경해야 합니다.
   >
   >* 액세스:*https://&lt;서버>:&lt;포트>/system/console/configMgr*
   * Apache Sling 레퍼러 필터의 구성 편집
   * 호스트 허용에서 프록시 서버의 항목을 추가합니다


1. 압축 사용을 참조하십시오.

   *APACHE_HOME/conf/httpd.conf* 구성 파일에 다음 구성을 추가합니다.

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

1. AEM 서버에 액세스하려면 https://[Apache_server]:80을 사용합니다.
