---
title: 기본적으로 SSL/TLS
description: AEM 6.5에서 기본적으로 SSL을 사용하는 방법에 대해 알아봅니다.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
docset: aem65
exl-id: 574e2fc2-6ebf-49b6-9b65-928237a8a34d
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 0%

---

# 기본적으로 SSL/TLS{#ssl-tls-by-default}

AEM의 보안을 지속적으로 개선하기 위해 Adobe은 기본적으로 SSL이라는 기능을 도입했습니다. 목적은 AEM 인스턴스에 연결하기 위해 HTTPS를 사용하도록 권장하는 것입니다.

## 기본적으로 SSL/TLS 활성화 {#enabling-ssl-tls-by-default}

AEM 홈 화면에서 관련 받은 편지함 메시지를 클릭하여 기본적으로 SSL/TLS 구성을 시작할 수 있습니다. 받은 편지함에 도달하려면 화면의 오른쪽 상단에 있는 벨 아이콘을 누릅니다. 그런 다음 을 클릭합니다. **모두 보기**. 이렇게 하면 목록 보기에서 정렬된 모든 경고 목록이 표시됩니다.

목록에서 을(를) 선택하고 **HTTPS 구성** 경고:

![chlimage_1-103](assets/chlimage_1-103.png)

>[!NOTE]
>
>다음과 같은 경우 **HTTPS 구성** 받은 편지함에 경고가 없으면 다음 위치로 이동하여 HTTPS 마법사로 직접 이동할 수 있습니다. *<http://serveraddress:serverport/libs/granite/security/content/sslConfig.html?item=configuration%2fconfiguressl&_charset_=utf-8>*

서비스 사용자 호출 **ssl 서비스** 이 기능에 대해 만들어졌습니다. 경고를 열면 다음 구성 마법사 가 표시됩니다.

1. 먼저 저장소 자격 증명을 설정합니다. 다음에 대한 자격 증명입니다. **ssl 서비스** https 수신자에 대한 개인 키 및 트러스트 스토어를 포함하는 시스템 사용자의 키 저장소입니다.

   ![chlimage_1-104](assets/chlimage_1-104.png)

1. 자격 증명을 입력한 후 을(를) 클릭합니다. **다음** 페이지의 오른쪽 상단에 있습니다. 그런 다음 SSL/TLS 연결에 대한 관련 개인 키 및 인증서를 업로드합니다.

   ![chlimage_1-105](assets/chlimage_1-105.png)

   >[!NOTE]
   >
   >마법사에서 사용할 개인 키 및 인증서를 생성하는 방법에 대한 자세한 내용은 [이 절차](/help/sites-administering/ssl-by-default.md#generating-a-private-key-certificate-pair-to-use-with-the-wizard) 아래요.

1. 마지막으로 HTTPS 수신자에 대한 HTTPS 호스트 이름과 TCP 포트를 지정합니다.

   ![screen_shot_2018-07-25at31658pm](assets/screen_shot_2018-07-25at31658pm.png)

## 기본적으로 SSL/TLS 자동화 {#automating-ssl-tls-by-default}

기본적으로 SSL/TLS를 자동화하는 방법에는 세 가지가 있습니다.

### HTTP POST 사용 {#via-http-post}

첫 번째 방법은 구성 마법사에서 사용 중인 SSLSetup 서버에 게시하는 것입니다.

```shell
POST /libs/granite/security/post/sslSetup.html
```

POST에서 다음 페이로드를 사용하여 구성을 자동화할 수 있습니다.

```xml
------WebKitFormBoundaryyBO4ArmGlcfdGDbs
Content-Disposition: form-data; name="keystorePassword"

test
------WebKitFormBoundaryyBO4ArmGlcfdGDbs
Content-Disposition: form-data; name="keystorePasswordConfirm"
test
------WebKitFormBoundaryyBO4ArmGlcfdGDbs
Content-Disposition: form-data; name="truststorePassword"
test
------WebKitFormBoundaryyBO4ArmGlcfdGDbs
Content-Disposition: form-data; name="truststorePasswordConfirm"
test
------WebKitFormBoundaryyBO4ArmGlcfdGDbs
Content-Disposition: form-data; name="privatekeyFile"; filename="server.der"
Content-Type: application/x-x509-ca-cert

------WebKitFormBoundaryyBO4ArmGlcfdGDbs
Content-Disposition: form-data; name="certificateFile"; filename="server.crt"
Content-Type: application/x-x509-ca-cert

------WebKitFormBoundaryyBO4ArmGlcfdGDbs
Content-Disposition: form-data; name="httpsPort"
8443
```

모든 sling POST 서블릿과 마찬가지로 서블릿은 200 OK 또는 오류 HTTP 상태 코드로 응답합니다. 응답의 HTML 본문에서 상태에 대한 세부 정보를 찾을 수 있습니다.

다음은 성공적인 응답과 오류 모두에 대한 예입니다.

**성공 예** (상태 = 200):

```xml
<!DOCTYPE html>
<html lang='en'>
<head>
<title>OK</title>
</head>
<body>
<h1>OK</h1>
<dl>
<dt class='foundation-form-response-status-code'>Status</dt>
<dd>200</dd>
<dt class='foundation-form-response-status-message'>Message</dt>
<dd>SSL successfully configured</dd>
<dt class='foundation-form-response-title'>Title</dt>
<dd>OK</dd>
<dt class='foundation-form-response-description'>Description</dt>
<dd>HTTPS has been configured on port 8443. The private key and
certificate were stored in the key store of the user ssl-service.
Take note of the key store password you provided. You need
it for any subsequent updating of the private key or certificate.</dd>
</dl>
<h2>Links</h2>
<ul class='foundation-form-response-links'>
<li><a class='foundation-form-response-redirect' href='/'>Done</a></li>
</ul>
</body>
</html>
```

**오류 예** (상태 = 500):

```xml
<!DOCTYPE html>
<html lang='en'>
<head>
<title>Error</title>
</head>
<body>
<h1>Error</h1>
<dl>
<dt class='foundation-form-response-status-code'>Status</dt>
<dd>500</dd>
<dt class='foundation-form-response-status-message'>Message</dt>
<dd>The provided file is not a valid key, DER format expected</dd>
<dt class='foundation-form-response-title'>Title</dt>
<dd>Error</dd>
</dl>
</body>
</html>
```

### 패키지 통과 {#via-package}

또는 다음 필수 항목이 이미 들어 있는 패키지를 업로드하여 SSL/TLS 설정을 자동화할 수 있습니다.

* ssl 서비스 사용자의 키 저장소입니다. 다음 위치에 있습니다. */home/users/system/security/ssl-service/keystore* 저장소에서 입니다.
* 다음 `GraniteSslConnectorFactory` 구성

### 마법사에서 사용할 개인 키/인증서 쌍 생성 {#generating-a-private-key-certificate-pair-to-use-with-the-wizard}

아래에서는 SSL/TLS 마법사가 사용할 수 있는 DER 형식의 자체 서명된 인증서를 만드는 예를 찾을 수 있습니다. 운영 체제를 기반으로 OpenSSL을 설치하고 OpenSSL 명령 프롬프트를 열고 디렉터리를 개인 키/인증서를 생성할 폴더로 변경합니다.

>[!NOTE]
>
>자체 서명된 인증서의 사용은 샘플용으로만 사용됩니다. 프로덕션에 를 사용하지 마십시오.

1. 먼저 개인 키를 만듭니다.

   ```shell
   openssl genrsa -aes256 -out localhostprivate.key 4096
   openssl rsa -in localhostprivate.key -out localhostprivate.key
   ```

1. 그런 다음 개인 키를 사용하여 CSR(인증서 서명 요청)을 생성합니다.

   ```shell
   openssl req -sha256 -new -key localhostprivate.key -out localhost.csr -subj "/CN=localhost"
   ```

1. SSL/TLS 인증서를 생성하고 개인 키로 서명합니다. 이 예에서 은 지금부터 1년 후에 만료됩니다.

   ```shell
   openssl x509 -req -days 365 -in localhost.csr -signkey localhostprivate.key -out localhost.crt
   ```

개인 키를 DER 형식으로 변환합니다. 이는 SSL 마법사에서 키가 DER 형식이어야 하기 때문입니다.

```shell
openssl pkcs8 -topk8 -inform PEM -outform DER -in localhostprivate.key -out localhostprivate.der -nocrypt
```

마지막으로 **localhostprivate.der** 개인 키로 및 **localhost.crt** 그래픽 SSL/TLS 마법사의 2단계에서 이 페이지의 시작 부분에 설명되어 있는 SSL/TLS 인증서

### cURL을 통해 SSL/TLS 구성 업데이트 {#updating-the-ssl-tls-configuration-via-curl}

>[!NOTE]
>
>다음을 참조하십시오 [AEM에서 cURL 사용](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/curl.html) AEM에서 유용한 cURL 명령의 중앙 집중식 목록입니다.

cURL 도구를 사용하여 SSL/TLS 구성을 자동화할 수도 있습니다. 이 URL에 구성 매개 변수를 게시하여 이 작업을 수행할 수 있습니다.

*https://&lt;serveraddress>:&lt;serverport>/libs/granite/security/post/sslSetup.html*

다음은 구성 마법사에서 다양한 설정을 변경하는 데 사용할 수 있는 매개 변수입니다.

* `-F "keystorePassword=password"` - 키 저장소 암호;

* `-F "keystorePasswordConfirm=password"` - 키 저장소 암호를 확인합니다.

* `-F "truststorePassword=password"` - truststore 암호;

* `-F "truststorePasswordConfirm=password"` - truststore 암호 확인

* `-F "privatekeyFile=@localhostprivate.der"` - 개인 키를 지정합니다.

* `-F "certificateFile=@localhost.crt"` - 인증서를 지정합니다.

* `-F "httpsHostname=host.example.com"`- 호스트 이름을 지정합니다.
* `-F "httpsPort=8443"` - HTTPS 수신자가 작동할 포트입니다.

>[!NOTE]
>
>cURL을 실행하여 SSL/TLS 구성을 자동화하는 가장 빠른 방법은 DER 및 CRT 파일이 있는 폴더에서 가져옵니다. 또는 `privatekeyFile` 및 certificateFile 인수
>
>또한 업데이트를 수행하려면 인증을 받아야 하므로 cURL 명령을 `-u user:passeword` 매개 변수.
>
>올바른 cURL post 명령은 다음과 같아야 합니다.

```shell
curl -u user:password -F "keystorePassword=password" -F "keystorePasswordConfirm=password" -F "truststorePassword=password" -F "truststorePasswordConfirm=password" -F "privatekeyFile=@localhostprivate.der" -F "certificateFile=@localhost.crt" -F "httpsHostname=host.example.com" -F "httpsPort=8443" https://host:port/libs/granite/security/post/sslSetup.html
```

#### cURL을 사용하는 여러 인증서 {#multiple-certificates-using-curl}

다음과 같이 certificateFile 매개 변수를 반복하여 서블릿에 인증서 체인을 보낼 수 있습니다.

`-F "certificateFile=@root.crt" -F "certificateFile=@localhost.crt"..`

명령을 실행한 후에는 모든 인증서가 키 저장소에 대해 작업을 수행했는지 확인합니다. 다음 확인: **키 저장소** 시작 위치:
[http://localhost:4502/libs/granite/security/content/v2/usereditor.html/home/users/system/security/ssl-service](http://localhost:4502/libs/granite/security/content/v2/usereditor.html/home/users/system/security/ssl-service)

### TLS 1.3 연결 활성화 {#enabling-tls-connection}

1. 웹 콘솔로 이동
1. 그런 다음 로 이동합니다. **OSGi** - **구성** - **Adobe Granite SSL 커넥터 팩토리**
1. 로 이동 **포함된 암호 세트** 을(를) 필드에 추가하고 다음 항목을 추가합니다. 를 눌러 각 추가를 확인할 수 있습니다.**+**&quot;각 필드를 추가한 후 필드 왼쪽에 있는 버튼:

   * `TLS_AES_256_GCM_SHA384`
   * `TLS_AES_128_GCM_SHA256`
   * `TLS_CHACHA20_POLY1305_SHA256`
   * `TLS_AES_128_CCM_SHA256`
   * `TLS_AES_128_CCM_8_SHA256`