---
title: WebLogic Server에 대한 SSL 구성
seo-title: WebLogic Server에 대한 SSL 구성
description: WebLogic 서버에서 사용할 SSL 자격 증명을 만드는 방법과 WebLogic Server에 대한 SSL을 구성하는 방법에 대해 알아봅니다.
seo-description: WebLogic 서버에서 사용할 SSL 자격 증명을 만드는 방법과 WebLogic Server에 대한 SSL을 구성하는 방법에 대해 알아봅니다.
uuid: 8ee979fd-2615-451b-a607-4f73ecfed4f9
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 968c2574-ec9a-45ca-9c64-66f4caeec285
translation-type: tm+mt
source-git-commit: 06335b9a85414b6b1141dd19c863dfaad0812503

---


# WebLogic Server에 대한 SSL 구성 {#configuring-ssl-for-weblogic-server}

WebLogic Server에서 SSL을 구성하려면 인증을 위한 SSL 자격 증명이 필요합니다. Java 키 도구를 사용하여 다음 작업을 수행하여 자격 증명을 만들 수 있습니다.

* 공개/개인 키 쌍을 만들고, 단일 요소 인증서 체인으로 저장된 X.509 v1 자체 서명된 인증서에서 공개 키를 래핑한 다음 인증서 체인과 개인 키를 새 키 저장소에 저장합니다. 이 키 저장소는 응용 프로그램 서버의 사용자 지정 ID 키 저장소입니다.
* 인증서를 추출하여 새 키 저장소에 삽입합니다. 이 키 저장소는 응용 프로그램 서버의 사용자 지정 트러스트 키 저장소입니다.

그런 다음 만든 사용자 지정 ID 키 저장소 및 사용자 지정 트러스트 키 저장소를 사용하도록 WebLogic을 구성합니다. 또한 키 저장소 파일을 만드는 데 사용되는 고유 이름에 WebLogic을 호스팅하는 컴퓨터의 이름이 포함되어 있지 않으므로 WebLogic 호스트 이름 확인 기능을 비활성화합니다.

## WebLogic Server에서 사용할 SSL 자격 증명 만들기 {#creating-an-ssl-credential-for-use-on-weblogic-server}

keytool 명령은 일반적으로 Java jre/bin 디렉토리에 있으며 다음 표에 나열된 여러 옵션 및 옵션 값을 포함해야 합니다.

<table>
 <thead>
  <tr>
   <th><p>Keytool 옵션</p></th>
   <th><p>설명</p></th>
   <th><p>옵션 값</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>-alias</p></td>
   <td><p>키 저장소의 별칭입니다.</p></td>
   <td>
    <ul>
     <li><p>사용자 지정 ID 키 저장소: <code>ads-credentials</code></p></li>
     <li><p>사용자 지정 트러스트 키 저장소: <code>bedrock</code></p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>-keyalg</p></td>
   <td><p>키 쌍을 생성하는 데 사용할 알고리즘입니다.</p></td>
   <td><p>RSA</p><p>회사의 정책에 따라 다른 알고리즘을 사용할 수 있습니다.</p></td>
  </tr>
  <tr>
   <td><p>-keystore</p></td>
   <td><p>키 저장소 파일의 위치와 이름입니다.</p><p>위치에 파일의 절대 경로가 포함될 수 있습니다. 또는 keytool 명령을 입력하는 명령 프롬프트의 현재 디렉토리에 상대적일 수 있습니다.</p></td>
   <td>
    <ul>
     <li><p>사용자 지정 ID 키 저장소: <code>[</code><i>appserverdomain]</i><code>/adobe/</code><i>[server name]</i><code>/ads-ssl.jks</code></p></li>
     <li><p>사용자 지정 트러스트 키 저장소: <code>[</code><i>appserverdomain]</i><code>/adobe/</code><i>[server name]</i><code>/ads-ca.jks</code></p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>-file</p></td>
   <td><p>인증서 파일의 위치 및 이름입니다.</p></td>
   <td><code> ads-ca.cer</code></td>
  </tr>
  <tr>
   <td><p>-validity</p></td>
   <td><p>인증서가 유효한 것으로 간주되는 일 수입니다.</p></td>
   <td><p>3650</p><p>회사 정책에 따라 다른 값을 사용할 수 있습니다.</p></td>
  </tr>
  <tr>
   <td><p>-storepass</p></td>
   <td><p>키 저장소의 컨텐츠를 보호하는 암호입니다. </p></td>
   <td>
    <ul>
     <li><p>사용자 지정 ID 키 저장소:키 저장소 암호는 관리 콘솔의 Trust Store 구성 요소에 대해 지정된 SSL 자격 증명 암호와 일치해야 합니다.</p></li>
     <li><p>사용자 지정 트러스트 키 저장소:사용자 지정 ID 키 저장소에 사용한 암호와 동일한 암호를 사용합니다.</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>-keypass</p></td>
   <td><p>키 쌍의 개인 키를 보호하는 암호입니다.</p></td>
   <td><p>옵션에 사용한 것과 동일한 암호를 <code>-storepass</code> 사용하십시오. 키 암호는 6자 이상이어야 합니다.</p></td>
  </tr>
  <tr>
   <td><p>-dname</p></td>
   <td><p>키 저장소를 소유한 사람을 식별하는 고유 이름입니다.</p></td>
   <td><p><code>"CN=</code><code>[User name]</code><code>,OU=</code><code>[Group Name]</code><code>, O=</code><code>[Company Name]</code><code>, L=</code><code>[City Name]</code><code>, S=</code><code>[State or province]</code><code>, C=</code><code>[Country Code]</code><code>"</code></p>
    <ul>
     <li><p><code><i>[User name]</i></code> 는 키 저장소를 소유한 사용자의 ID입니다.</p></li>
     <li><p><code><i>[Group Name]</i></code> 는 키 저장소 소유자가 속한 기업 그룹의 ID입니다.</p></li>
     <li><p><code><i>[Company Name]</i></code> 은 조직의 이름입니다.</p></li>
     <li><p><code><i>[City Name]</i></code> 는 조직이 위치한 도시입니다.</p></li>
     <li><p><code><i>[State or province]</i></code> 는 조직이 위치한 시/도입니다.</p></li>
     <li><p><code><i>[Country Code]</i></code> 는 조직이 있는 국가의 두 문자 코드입니다.</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

keytool 명령 사용에 대한 자세한 내용은 JDK 설명서의 일부인 keytool.html 파일을 참조하십시오.

## 사용자 지정 ID 및 트러스트 키 저장소 만들기 {#create-the-custom-identity-and-trust-keystores}

1. 명령 프롬프트에서 appserverdomain *[/adobe/]* server 이름으로&#x200B;*[]*&#x200B;이동합니다.
1. 다음 명령을 입력합니다.

   `[JAVA_HOME]/bin/keytool -genkey -v -alias ads-credentials -keyalg RSA -keystore "ads-credentials.jks" -validity 3650 -storepass store_password -keypass key_password -dname "CN=Hostname, OU=Group Name, O=Company Name, L=City Name, S=State,C=Country Code`

   >[!NOTE]
   >
   >JDK가 설치된 디렉토리로 `[JAVA_HOME]`*대체하고 기울임꼴로 표시된 텍스트를 환경에 해당하는 값으로 바꿉니다.*

   예:

   ```as3
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -genkey -v -alias ads-credentials -keyalg RSA -keystore "ads-credentials.jks" -validity 3650 -storepass P@ssw0rd -keypass P@ssw0rd -dname "CN=wasnode01, OU=LC, O=Adobe, L=Noida, S=UP,C=91
   ```

   &quot;ads-credentials.jks&quot;라는 사용자 정의 ID 키 저장소 파일은 [appserverdomain]/adobe/[server name] 디렉토리에 만들어집니다.

1. 다음 명령을 입력하여 ads-credentials 키 저장소에서 인증서를 추출합니다.

   [JAVA_HOME]`/bin/keytool -export -v -alias ads-credentials`

   `-file "ads-ca.cer" -keystore "ads-credentials.jks"`

   `-storepass` `*store*`*_**password**

   >[!NOTE]
   >
   >JDK가 설치된 디렉토리로 `[JAVA_HOME]` 대체하고 `store`*_**를`password`사용자 정의 ID 키 저장소의 암호로 바꿉니다.*

   예:

   ```as3
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -export -v -alias ads-credentials -file "ads-ca.cer" -keystore "ads-credentials.jks" -storepass P@ssw0rd
   ```

   &quot;ads-ca.cer&quot;라는 인증서 파일은 [appserverdomain]/adobe/[*server name*] 디렉토리에 만들어집니다.

1. 응용 프로그램 서버와의 보안 통신이 필요한 모든 호스트 컴퓨터에 ads-ca.cer 파일을 복사합니다.
1. 다음 명령을 입력하여 새 키 저장소 파일(사용자 지정 트러스트 키 저장소)에 인증서를 삽입합니다.

   [JAVA_HOME]`/bin/keytool -import -v -noprompt -alias bedrock -file "ads-ca.cer" -keystore "ads-ca.jks" -storepass store_password -keypass key_password`

   >[!NOTE]
   >
   >JDK가 설치된 디렉토리로 `[JAVA_HOME]` 대체하고 `store`*_and *_`password``key`*_*`password`*를 자신의 비밀번호로 바꿉니다.*

   예:

   ```as3
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -import -v -noprompt -alias bedrock -file "ads-ca.cer" -keystore "ads-ca.jks" -storepass Password1 -keypass Password1
   ```

&quot;ads-ca.jks&quot;라는 사용자 정의 트러스트 키 저장소 파일은 [appserverdomain]/adobe/[server] 디렉터리에 만들어집니다.

사용자가 만든 사용자 지정 ID 키 저장소 및 사용자 지정 트러스트 키 저장소를 사용하도록 WebLogic을 구성합니다. 또한 키 저장소 파일을 만드는 데 사용되는 고유 이름에 WebLogic Server를 호스팅하는 컴퓨터의 이름이 포함되어 있지 않으므로 WebLogic 호스트 이름 확인 기능을 비활성화합니다.

## SSL을 사용하도록 WebLogic 구성 {#configure-weblogic-to-use-ssl}

1. 웹 브라우저의 URL 행에 `https://`*[호스트 이름을&#x200B;]*입력하여 WebLogic Server 관리 콘솔을 시작합니다`:7001/console`.
1. 환경의 도메인 구성에서 서버 > 서버 **>[서버]> 구성 > 일반을 선택합니다**.
1. [일반]의 [구성]에서 [수신 포트 **활성화** ] 및 [SSL **수신 포트 사용]이** 선택되어 있는지 확인합니다. 활성화되지 않은 경우 다음을 수행합니다.

   1. 변경 센터에서 잠금 및 편집을 클릭하여 **선택** 사항과 값을 수정합니다.
   1. [수신 **포트 활성화** ] 및 [SSL 수신 **포트 활성화** ] 확인란을선택합니다.

1. 이 서버가 관리 서버인 경우 수신 포트를 사용하지 않은 포트 값(예: 8001)으로 변경하고 SSL 수신 포트를 사용하지 않은 포트 값(예: 8002)으로 변경합니다. 독립 실행형 서버에서 기본 SSL 포트는 7002입니다.
1. 릴리즈 **구성을 클릭합니다**.
1. 환경의 도메인 구성에서 서버 > 관리 **서버&#x200B;[*> 구성*]> 일반을 클릭합니다**.
1. [일반]의 [구성]에서 [키 저장소]를 **선택합니다**.
1. 변경 센터에서 잠금 및 편집을 클릭하여 **선택** 사항과 값을 수정합니다.
1. 변경을 **클릭하여** 키 저장소 목록을 드롭다운 목록으로 가져오고 사용자 지정 ID 및 **사용자 지정 트러스트를 선택합니다**.
1. ID 아래에서 다음 값을 지정합니다.

   **사용자 지정 ID 키 저장소**:appserverdomain *[/adobe/]* server name *[/ads-credentials.jks여기에서 *]* appserverdomain[*은 실제 경로이며] *[]* 서버 이름은 응용 프로그램 서버의 이름입니다.

   **사용자 지정 ID 키 저장소 유형**:JKS

   **사용자 지정 ID 키 저장소 암호**: *mypassword* (사용자 정의 ID 키 저장소 암호)

1. [신뢰]에서 다음 값을 지정합니다.

   **사용자 지정 Trust Keystore 파일 이름**: `*[appserverdomain]*/adobe/*[server]*/ads-ca.jks`여기서 `*[appserverdomain]*` 실제 경로는

   **사용자 지정 Trust Keystore 유형**:JKS

   **사용자 지정 Trust Keystore 암호 구문**: *mypassword* (사용자 지정 트러스트 키 암호)

1. [일반]의 [구성]에서 SSL을 **선택합니다**.
1. 기본적으로 Keystore는 ID 및 신뢰 위치에 대해 선택됩니다. 그렇지 않은 경우 키 스토어로 변경합니다.
1. ID 아래에서 다음 값을 지정합니다.

   **개인 키 별칭**:ads-credentials

   **암호**: *mypassword*

1. 릴리즈 **구성을 클릭합니다**.

## 호스트 이름 확인 기능 비활성화 {#disable-the-hostname-verification-feature}

1. [구성] 탭에서 SSL을 클릭합니다.
1. 고급의 호스트 이름 확인 목록에서 없음을 선택합니다.

   호스트 이름 확인을 비활성화하지 않으면 CN(일반 이름)에 서버 호스트 이름이 포함되어야 합니다.

1. 변경 센터에서 잠금 및 편집을 클릭하여 선택 및 값을 수정합니다.
1. 응용 프로그램 서버를 다시 시작합니다.

