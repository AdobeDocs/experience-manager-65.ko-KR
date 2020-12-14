---
title: JBoss 응용 프로그램 서버에 대한 SSL 구성
seo-title: JBoss 응용 프로그램 서버에 대한 SSL 구성
description: JBoss 응용 프로그램 서버에 대해 SSL을 구성하는 방법에 대해 알아봅니다.
seo-description: JBoss 응용 프로그램 서버에 대해 SSL을 구성하는 방법에 대해 알아봅니다.
uuid: 7c13cf00-ea89-4894-a4fc-aaeec7ae9f66
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c187daa4-41b7-47dc-9669-d7120850cafd
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 0%

---


# JBoss 응용 프로그램 서버에 대한 SSL 구성 {#configuring-ssl-for-jboss-application-server}

JBoss 응용 프로그램 서버에서 SSL을 구성하려면 인증을 위한 SSL 자격 증명이 필요합니다. Java 키 도구를 사용하여 자격 증명을 만들거나 CA(인증 기관)에서 자격 증명을 요청하고 가져올 수 있습니다. 그런 다음 JBoss에서 SSL을 활성화해야 합니다.

키 저장소를 만드는 데 필요한 모든 정보를 포함하는 단일 명령을 사용하여 키 도구를 실행할 수 있습니다.

다음 절차에서:

* `[appserver root]` 는 AEM 양식을 실행하는 응용 프로그램 서버의 홈 디렉토리입니다.
* `[type]` 은 수행한 설치 유형에 따라 다른 폴더 이름입니다.

## SSL 자격 증명 {#create-an-ssl-credential} 만들기

1. 명령 프롬프트에서 *[JAVA HOME]*/bin으로 이동하고 다음 명령을 입력하여 자격 증명 및 키 저장소를 만듭니다.

   `keytool -genkey -dname "CN=`*호스트* `, OU=`*이름 그룹* `, O=`*이름 회사* `,L=`*이름City* `, S=`** `, C=`NameStateCountry 코드&quot;  `-alias "AEMForms Cert"` `-keyalg RSA -keypass`*key_* `-keystore`*passwordkeystorname* `.keystore`

   >[!NOTE]
   >
   >`[JAVA_HOME]`을(를) JDK가 설치된 디렉토리로 바꾸고 기울임꼴로 된 텍스트를 환경에 해당하는 값으로 바꿉니다. 호스트 이름은 응용 프로그램 서버의 정규화된 도메인 이름입니다.

1. 암호를 입력하라는 메시지가 표시되면 `keystore_password`을 입력합니다. 키 저장소 및 키의 암호가 동일해야 합니다.

   >[!NOTE]
   >
   >이 단계에서 입력한 `keystore_password` *이 1단계에서 입력한 암호(key_password)와 같을 수도 있고, 다른 것일 수도 있습니다.*

1. 다음 명령 중 하나를 입력하여 *keystorename*.keystore를 `[appserver root]/server/[type]/conf` 디렉토리로 복사합니다.

   * (Windows 단일 서버) `copy` `keystorename.keystore[appserver root]\standalone\configuration`
   * (Windows Server 클러스터) 복사본 `keystorename.keystore[appserver root]\domain\configuration`
   * (Linux 단일 서버) `cp keystorename.keystore [appserver root]/standalone/configuration`
   * (Linux Server 클러스터) `cp <em>keystorename</em>.keystore<em>[appserver root]</em>/domain/configuration`


1. 다음 명령을 입력하여 인증서 파일을 내보냅니다.

   * (단일 서버) `keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer -keystore [appserver root]/standalone/configuration/keystorename.keystore`
   * (서버 클러스터) `keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer -keystore [appserver root]/domain/configuration/keystorename.keystore`

1. 암호를 입력하라는 메시지가 표시되면 *keystore_password*&#x200B;를 입력합니다.
1. 다음 명령을 입력하여 AEMForms_cert.cer 파일을 *[appserver root] \conf* 디렉토리로 복사합니다.

   * (Windows 단일 서버) `copy AEMForms_cert.cer [appserver root]\standalone\configuration`
   * (Windows Server 클러스터) `copy AEMForms_cert.cer [appserver root]\domain\configuration`
   * (Linux 단일 서버) `cp AEMForms _cert.cer [appserver root]\standalone\configuration`
   * (Linux Server 클러스터) `cp AEMForms _cert.cer [appserver root]\domain\configuration`

1. 다음 명령을 입력하여 인증서 내용을 봅니다.

   * `keytool -printcert -v -file [appserver root]\standalone\configuration\AEMForms_cert.cer`
   * `keytool -printcert -v -file [appserver root]\domain\configuration\AEMForms_cert.cer`

1. 필요한 경우 `[JAVA_HOME]\jre\lib\security`에서 액세스 파일에 대한 쓰기 액세스를 제공하려면 다음 작업을 수행하십시오.

   * (Windows) 캐시 파일을 마우스 오른쪽 단추로 클릭하고 [속성]을 선택한 다음 [읽기 전용] 특성을 선택 취소합니다.
   * (Linux) `chmod 777 cacerts` 입력

1. 다음 명령을 입력하여 인증서를 가져옵니다.

   `keytool -import -alias “AEMForms Cert” -file`*AEMForms_* `.cer -keystore`*certJAVA_HOME* `\jre\lib\security\cacerts`

1. 암호로 `changeit`을 입력합니다. 이 암호는 Java 설치에 대한 기본 암호이며 시스템 관리자가 변경했을 수 있습니다.
1. `Trust this certificate? [no]`: 메시지가 표시되면 `yes`을 입력합니다. &quot;인증서가 키 저장소에 추가되었습니다&quot;라는 확인 메시지가 표시됩니다.
1. Workbench에서 SSL을 통해 연결하는 경우 Workbench 컴퓨터에 인증서를 설치합니다.
1. 텍스트 편집기에서 편집할 다음 파일을 엽니다.

   * 단일 서버 - `[appserver root]`/standalone/configuration/lc_&lt;dbname/turnkey>.xml

   * 서버 클러스터 - `[appserver root]`/domain/configuration/host.xml

   * 서버 클러스터 - `[appserver root]`/domain/configuration/domain_&lt;dbname>.xml

1. 
   * **단일 서버** 의 경우 lc_&lt;dbaname>.xml 파일에서 다음  &lt;security-realms> 섹션 뒤에 추가합니다.

   ```xml
   <security-realm name="SSLRealm">
   <server-identities>
   <ssl>
   <keystore path="C:/Adobe/Adobe_Experience_Manager_Forms/jboss/standalone/configuration/aemformses.keystore" keystore-password="changeit" alias="AEMformsCert" key-password="changeit"/>
   </ssl>
   </server-identities>
   </security-realm>
   ```

   다음 코드 다음에 있는 `<server>` 섹션을 찾습니다.

   `<http-listener name="default" socket-binding="http" redirect-socket="https" max-post-size="104857600"/>`

   위의 코드 다음에 있는 &lt;server> 섹션에 다음을 추가합니다.

   ```xml
   <https-listener name="default-secure" socket-binding="https" security-realm="SSLRealm"/>
   ```

   * **서버 클러스터의 경우 모든 노드** 의  [appserver 루트] \domain\configuration\host.xml &lt;security-realms> 에 다음섹션을 추가합니다.

   ```xml
   <security-realm name="SSLRealm">
   <server-identities>
   <ssl>
   <keystore path="C:/Adobe/Adobe_Experience_Manager_Forms/jboss/standalone/configuration/aemformses.keystore" keystore-password="changeit" alias="AEMForms Cert" key-password="changeit"/>
   </ssl>
   </server-identities>
   </security-realm>
   ```

   서버 클러스터의 주 노드에서 [appserver 루트]\domain\configuration\domain_&lt;dbname>.xml에서 다음 코드 다음에 있는 &lt;server> 섹션을 찾습니다.

   `<http-listener name="default" socket-binding="http" redirect-socket="https" max-post-size="104857600"/>`

   위의 코드 다음에 있는 &lt;server> 섹션에 다음을 추가합니다.

   ```xml
   <https-listener name="default-secure" socket-binding="https" security-realm="SSLRealm"/>
   ```

1. `keystoreFile` 속성 및 `keystorePass` 속성의 값을 키 저장소를 만들 때 지정한 키 저장소 암호로 변경합니다.
1. 응용 프로그램 서버를 다시 시작합니다.

   * 턴키 설치의 경우:

      * Windows Campaign 컨트롤 패널에서 관리 도구를 클릭한 다음 서비스를 클릭합니다.
      * Adobe Experience Manager 양식에 대해 JBoss를 선택합니다.
      * 작업 > 중지를 선택합니다.
      * 서비스의 상태가 중지됨으로 나타날 때까지 기다립니다.
      * 작업 > 시작을 선택합니다.
   * 사전 구성되거나 수동으로 구성된 Adobe 설치의 경우:

      * 명령 프롬프트에서 *`[appserver root]`*/bin으로 이동합니다.
      * 다음 명령을 입력하여 서버를 중지합니다.

         * (Windows) `shutdown.bat -S`
         * (Linux) `./shutdown.sh -S`
      * JBoss 프로세스가 완전히 종료될 때까지 기다립니다(JBoss 프로세스가 시작한 터미널에 컨트롤을 반환할 때).
      * 다음 명령을 입력하여 서버를 시작합니다.

         * (Windows) `run.bat -c <profile>`
         * (Linux) `./run.sh -c <profile>`



1. SSL을 사용하여 관리 콘솔에 액세스하려면 웹 브라우저에서 `https://[host name]:'port'/adminui`을 입력합니다.

   JBoss의 기본 SSL 포트는 8443입니다. 여기서 AEM 양식에 액세스할 때 이 포트를 지정합니다.

## CA {#request-a-credential-from-a-ca}에서 자격 증명 요청

1. 명령 프롬프트에서 *[JAVA HOME]*/bin으로 이동하고 다음 명령을 입력하여 키 스토어와 키를 만듭니다.

   `keytool -genkey -dname "CN=`*호스트* `, OU=`*이름* `, O=`*회사* `, L=`*이름City* `, S=`** `, C=`*NameStateCountry 코드*&quot;  `-alias "AEMForms Cert"` `-keyalg RSA -keypass`-** `-keystore`*key_passwordkeystorname* `.keystore`

   >[!NOTE]
   >
   >*`[JAVA_HOME]`*&#x200B;을(를) JDK가 설치된 디렉토리로 바꾸고 기울임꼴로 된 텍스트를 환경에 해당하는 값으로 바꿉니다.

1. 인증서 기관에 전송할 인증서 요청을 생성하려면 다음 명령을 입력합니다.

   `keytool -certreq -alias` &quot;AEMForms Cert&quot;  `-keystore`** `.keystore -file`*keystorenameAEMFormscertRequest.csr*

1. 인증서 파일에 대한 요청이 완료되면 다음 절차를 완료하십시오.

## CA에서 받은 자격 증명을 사용하여 SSL {#use-a-credential-obtained-from-a-ca-to-enable-ssl} 활성화

1. 명령 프롬프트에서 *`[JAVA HOME]`*/bin으로 이동하고 다음 명령을 입력하여 CSR이 서명된 CA의 루트 인증서를 가져옵니다.

   `keytool -import -trustcacerts -file` rootcert.pem -keystore` keystorename.keystore -alias root`

   루트 인증서가 브라우저에 없는 경우 해당 인증서를 브라우저에 가져옵니다.

   >[!NOTE]
   >
   >*`[JAVA_HOME]`을(를) JDK가 설치된 디렉터리로 바꾸고 기울임꼴로 표시된 텍스트를 사용자 환경에 해당하는 값으로 바꿉니다.*

1. 명령 프롬프트에서 *`[JAVA HOME]`*/bin으로 이동하여 다음 명령을 입력하여 자격 증명을 키 저장소에 가져옵니다.

   `keytool -import -trustcacerts -file`** `.crt -keystore`*CACertificateNamekeystorename* `.keystore`

   >[!NOTE]
   >
   >* `[JAVA_HOME]`을(를) JDK가 설치된 디렉토리로 바꾸고 기울임꼴로 된 텍스트를 환경에 해당하는 값으로 바꿉니다.
   >* 가져온 CA 서명 인증서가 있으면 자체 서명된 공용 인증서가 대체됩니다.


1. SSL 자격 증명 만들기의 13 - 18단계를 완료합니다.
