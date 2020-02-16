---
title: 기본적으로 SSL
seo-title: 기본적으로 SSL
description: AEM 파섹
seo-description: AEM 파섹
uuid: 2fbfd020-1d33-4b22-b963-c698e62f5bf6
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
discoiquuid: 68077369-0549-4c0f-901b-952e323013ea
docset: aem65
translation-type: tm+mt
source-git-commit: 4b965d8f7814816126601f6366c1ba313e404538

---


# 기본적으로 SSL{#ssl-by-default}

AEM의 보안을 지속적으로 개선하기 위해 Adobe는 기본적으로 SSL이라는 기능을 도입했습니다. 목적은 HTTPS를 사용하여 AEM 인스턴스에 연결하도록 장려하기 위한 것입니다.

## 기본적으로 SSL 활성화 {#enabling-ssl-by-default}

AEM 홈 화면에서 관련 받은 편지함 메시지를 클릭하여 기본적으로 SSL 구성을 시작할 수 있습니다. 받은 편지함에 도착하려면 화면 오른쪽 상단에 있는 벨 아이콘을 누릅니다. 그런 다음 모두 **보기를 클릭합니다**. 이렇게 하면 목록 보기에 정렬된 모든 경고 목록이 표시됩니다.

목록에서 HTTPS 구성 **경고를 선택하고 엽니다** .

![chlimage_1-103](assets/chlimage_1-103.png)

>[!NOTE]
>
>HTTPS **구성** 경고가 받은 편지함에 없는 경우 *<http://serveraddress:serverport/libs/granite/security/content/sslConfig.html?item=configuration%2fconfiguressl&_charset_=utf-8>*

이 기능에 대해 **ssl-service** 라는 서비스 사용자가 생성되었습니다. 경고를 열면 다음 구성 마법사가 안내됩니다.

1. 먼저 스토어 자격 증명을 설정합니다. HTTPS 리스너에 대한 개인 키 및 트러스트 저장소가 포함될 **ssl 서비스** 시스템 사용자의 키 저장소에 대한 자격 증명입니다.

   ![chlimage_1-104](assets/chlimage_1-104.png)

1. 자격 증명을 입력한 후 **페이지의** 오른쪽 위 모서리에서 [다음]을 클릭합니다. 그런 다음 SSL 연결에 대한 관련 개인 키와 인증서를 업로드합니다.

   ![chlimage_1-105](assets/chlimage_1-105.png)

   >[!NOTE]
   >
   >마법사에서 사용할 개인 키 및 인증서를 생성하는 방법에 대한 자세한 내용은 [아래 절차를](/help/sites-administering/ssl-by-default.md#generating-a-private-key-certificate-pair-to-use-with-the-wizard) 참조하십시오.

1. 마지막으로 HTTPS 수신기의 HTTPS 호스트 이름과 TCP 포트를 지정합니다.

   ![screen_shot_2018-07-25at31658pm](assets/screen_shot_2018-07-25at31658pm.png)

## 기본적으로 SSL 자동화 {#automating-ssl-by-default}

기본적으로 SSL을 자동화하는 방법에는 세 가지가 있습니다.

### HTTP POST를 통해 {#via-http-post}

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

sling POST 서블릿과 마찬가지로 서블릿은 200 OK 또는 오류 HTTP 상태 코드로 응답합니다. 응답의 HTML 본문에서는 상태에 대한 세부 정보를 찾을 수 있습니다.

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
Please take note of the key store password you provided. You will need
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

### 패키지 사용 {#via-package}

또는 다음 필수 항목이 이미 포함되어 있는 패키지를 업로드하여 SSL 설정을 자동화할 수 있습니다.

* ssl 서비스 사용자의 키 저장소입니다. 이 위치는 저장소의 */home/users/system/security/ssl-service/keystore* 아래에 있습니다.
* 구성 `GraniteSslConnectorFactory`

### 마법사와 함께 사용할 개인 키/인증서 쌍 생성 {#generating-a-private-key-certificate-pair-to-use-with-the-wizard}

아래에서 SSL 마법사에서 사용할 수 있는 DER 형식으로 자체 서명된 인증서를 만드는 예를 확인할 수 있습니다.

>[!NOTE]
>
>자체 서명된 인증서의 사용은 예시용으로만 사용되며 프로덕션에서 사용되어서는 안 됩니다.

1. 먼저 개인 키를 만듭니다.

   ```shell
   openssl genrsa -aes256 -out localhostprivate.key 4096
   openssl rsa -in localhostprivate.key -out localhostprivate.key
   ```

1. 그런 다음 개인 키를 사용하여 CSR(인증서 서명 요청)을 생성합니다.

   ```shell
   openssl req -sha256 -new -key localhostprivate.key -out localhost.csr -subj '/CN=localhost'
   ```

1. SSL 인증서를 생성하여 개인 키로 서명합니다. 이 예에서는 지금부터 1년 후에 만료됩니다.

   ```shell
   openssl x509 -req -days 365 -in localhost.csr -signkey localhostprivate.key -out localhost.crt
   ```

개인 키를 DER 형식으로 변환합니다. 이는 SSL 마법사에서 키가 DER 형식이어야 하기 때문입니다.

```shell
openssl pkcs8 -topk8 -inform PEM -outform DER -in localhostprivate.key -out localhostprivate.der -nocrypt
```

마지막으로 **localhostprivate.der** 를 개인 키로 업로드하고 **, 이 페이지의 시작에 설명된 그래픽 SSL 마법사의 2단계에서 localhosthost.crt를** SSL 인증서로 업로드합니다.

### cURL을 통한 SSL 구성 업데이트 {#updating-the-ssl-configuration-via-curl}

>[!NOTE]
>
>AEM [에서 유용한 cURL](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/curl.html) 명령 중앙 목록은 AEM과 함께 cURL 사용을 참조하십시오.

cURL 도구를 사용하여 SSL 구성을 자동화할 수도 있습니다. 이 URL에 구성 매개 변수를 게시하여 이를 수행할 수 있습니다.

*https://&lt;serveraddress>:&lt;serverport>/libs/granite/security/post/sslSetup.html*

다음은 구성 마법사의 다양한 설정을 변경하기 위해 사용할 수 있는 매개 변수입니다.

* `-F "keystorePassword=password"` - 키 저장소 암호;

* `-F "keystorePasswordConfirm=password"` - 키 저장소 암호 확인;

* `-F "truststorePassword=password"` - truststore 암호;

* `-F "truststorePasswordConfirm=password"` - truststore 암호 확인;

* `-F "privatekeyFile=@localhostprivate.der"` - 개인 키 지정;

* `-F "certificateFile=@localhost.crt"` - 인증서 지정;

* `-F "httpsHostname=host.example.com"`- hostname;
* `-F "httpsPort=8443"` - HTTPS 수신기가 작동할 포트입니다.

>[!NOTE]
>
>SSL 구성을 자동화하기 위해 cURL을 실행하는 가장 빠른 방법은 DER 및 CRT 파일이 있는 폴더에서 가져옵니다. 또는 `privatekeyFile` and certificateFile 인수에 전체 경로를 지정할 수 있습니다.
>
>업데이트를 수행하려면 인증을 받아야 하므로 cURL 명령을 `-u user:passeword` 매개 변수에 추가해야 합니다.
>
>올바른 cURL post 명령은 다음과 같아야 합니다.

```shell
curl -u user:password -F "keystorePassword=password" -F "keystorePasswordConfirm=password" -F "truststorePassword=password" -F "truststorePasswordConfirm=password" -F "privatekeyFile=@localhostprivate.der" -F "certificateFile=@localhost.crt" -F "httpsHostname=host.example.com" -F "httpsPort=8443" https://host:port/libs/granite/security/post/sslSetup.html
```

#### cURL을 사용하는 여러 인증서 {#multiple-certificates-using-curl}

다음과 같이 certificateFile 매개 변수를 반복하여 서블릿을 인증서 체인으로 전송할 수 있습니다.

`-F "certificateFile=@root.crt" -F "certificateFile=@localhost.crt"..`

명령을 실행한 후 키 저장소에 대해 모든 인증서가 작성되었는지 확인합니다. 다음 위치에서 키 저장소를 확인합니다.[http://localhost:4502/libs/granite/security/content/userEditor.html/home/users/system/security/ssl-service](http://localhost:4502/libs/granite/security/content/userEditor.html/home/users/system/security/ssl-service)
