---
title: JBoss 응용 프로그램 서버에 대한 SSL 구성
seo-title: JBoss 응용 프로그램 서버에 대한 SSL 구성
description: JBoss Application Server에 대한 SSL을 구성하는 방법을 알아봅니다.
seo-description: JBoss Application Server에 대한 SSL을 구성하는 방법을 알아봅니다.
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

이 절차에서:

* `[appserver root]` 는 AEM 양식을 실행하는 응용 프로그램 서버의 홈 디렉토리입니다.
* `[type]` 은 수행한 설치 유형에 따라 달라지는 폴더 이름입니다.

## SSL 자격 증명 만들기 {#create-an-ssl-credential}

1. 명령 프롬프트에서 *[JAVA HOME]*/bin으로 이동하고 다음 명령을 입력하여 자격 증명 및 키 저장소를 만듭니다.

   `keytool -genkey -dname "CN=`*호스트 그룹&#x200B;*그룹 이름`, OU=`** 회사 이름 `, O=`*도시 이름&#x200B;*도시 이름`,L=`*StateName* `, S=`**`, C=``-alias "AEMForms Cert"``-keyalg RSA -keypass`** `-keystore`*국가StateCode국가 코드&quot;키_암호Storekeystore키워드 이름&#x200B;*`.keystore`

   >[!NOTE]
   >
   >JDK가 설치되어 있는 디렉토리 `[JAVA_HOME]` 로 대체하고 기울임꼴로 표시된 텍스트를 사용자 환경에 해당하는 값으로 바꿉니다. 호스트 이름은 응용 프로그램 서버의 정규화된 도메인 이름입니다.

1. 암호를 입력하라는 메시지가 `keystore_password` 표시되면 암호를 입력합니다. 키 저장소 및 키의 암호가 동일해야 합니다.

   >[!NOTE]
   >
   >이 단계 `keystore_password` *에서 입력한 암호(key_password)가 1단계에서 입력한 암호(key_password)와 같을 수도 있고 다른 암호일 수도 있습니다.*

1. 다음 명령 중 하나를 입력하여 *keystorename*.keystore를 `[appserver root]/server/[type]/conf` 디렉토리로 복사합니다.

   * (Windows 단일 서버) `copy` `keystorename.keystore[appserver root]\standalone\configuration`
   * (Windows Server 클러스터) 복사 `keystorename.keystore[appserver root]\domain\configuration`
   * (Linux 단일 서버) `cp keystorename.keystore [appserver root]/standalone/configuration`
   * (Linux 서버 클러스터) `cp <em>keystorename</em>.keystore<em>[appserver root]</em>/domain/configuration`


1. 다음 명령을 입력하여 인증서 파일을 내보냅니다.

   * (단일 서버) `keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer -keystore [appserver root]/standalone/configuration/keystorename.keystore`
   * (서버 클러스터) `keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer -keystore [appserver root]/domain/configuration/keystorename.keystore`

1. 암호를 *묻는 메시지가 나타나면 keystore_password* 를 입력합니다.
1. 다음 명령을 입력하여 AEMForms_cert.cer 파일을 *[appserver 루트]\conf *디렉토리로 복사합니다.

   * (Windows 단일 서버) `copy AEMForms_cert.cer [appserver root]\standalone\configuration`
   * (Windows Server 클러스터) `copy AEMForms_cert.cer [appserver root]\domain\configuration`
   * (Linux 단일 서버) `cp AEMForms _cert.cer [appserver root]\standalone\configuration`
   * (Linux 서버 클러스터) `cp AEMForms _cert.cer [appserver root]\domain\configuration`

1. 다음 명령을 입력하여 인증서 내용을 봅니다.

   * `keytool -printcert -v -file [appserver root]\standalone\configuration\AEMForms_cert.cer`
   * `keytool -printcert -v -file [appserver root]\domain\configuration\AEMForms_cert.cer`

1. 필요한 경우 액세스 파일에 대한 쓰기 액세스 권한을 제공하려면 `[JAVA_HOME]\jre\lib\security`다음 작업을 수행하십시오.

   * (Windows) 캐시 파일을 마우스 오른쪽 단추로 클릭하고 [속성]을 선택한 다음 [읽기 전용] 속성을 선택 취소합니다.
   * (Linux) 유형 `chmod 777 cacerts`

1. 다음 명령을 입력하여 인증서를 가져옵니다.

   `keytool -import -alias “AEMForms Cert” -file`*AEMForms_cert *`.cer -keystore`*JAVA_HOME* `\jre\lib\security\cacerts`

1. 암호 `changeit` 로 입력합니다. 이 비밀번호는 Java 설치에 대한 기본 암호이며 시스템 관리자가 변경했을 수 있습니다.
1. 다음을 묻는 메시지가 `Trust this certificate? [no]`표시되면 입력합니다 `yes`. &quot;인증서가 키 저장소에 추가되었습니다&quot;라는 확인 메시지가 표시됩니다.
1. Workbench에서 SSL을 통해 연결하는 경우 Workbench 컴퓨터에 인증서를 설치합니다.
1. 텍스트 편집기에서 편집할 다음 파일을 엽니다.

   * 단일 서버 - `[appserver root]`/standalone/configuration/lc_&lt;dbname/turnkey>.xml

   * 서버 클러스터 - `[appserver root]`/domain/configuration/host.xml

   * 서버 클러스터 - `[appserver root]`/domain/configuration/domain_&lt;dbname>.xml

1. 
   * **단일 서버의 경우,** lc_&lt;dbame/tunkey>.xml 파일에서 &lt;security-reales> 섹션 뒤에 다음 항목을 추가합니다.

   ```xml
   <security-realm name="SSLRealm">
   <server-identities>
   <ssl>
   <keystore path="C:/Adobe/Adobe_Experience_Manager_Forms/jboss/standalone/configuration/aemformses.keystore" keystore-password="changeit" alias="AEMformsCert" key-password="changeit"/>
   </ssl>
   </server-identities>
   </security-realm>
   ```

   다음 코드 뒤에 `<server>` 있는 섹션을 찾습니다.

   `<http-listener name="default" socket-binding="http" redirect-socket="https" max-post-size="104857600"/>`

   위의 코드 다음에 있는 &lt;server> 섹션에 다음을 추가합니다.

   ```xml
   <https-listener name="default-secure" socket-binding="https" security-realm="SSLRealm"/>
   ```

   * **서버 클러스터의 경우** 모든 노드의 [appserver 루트]\domain\configuration\host.xml에 &lt;security-reales> 섹션 뒤에 다음 항목을 추가합니다.

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

1. 키 저장소를 만들 때 지정한 키 스토어 암호 `keystoreFile` 로 속성 및 `keystorePass` 속성을 변경합니다.
1. 응용 프로그램 서버를 다시 시작합니다.

   * 턴키 설치의 경우:

      * Windows Campaign 컨트롤 패널에서 관리 도구를 클릭한 다음 서비스를 클릭합니다.
      * Adobe Experience Manager 양식에 대해 JBoss를 선택합니다.
      * 작업 > 중지를 선택합니다.
      * 서비스의 상태가 중지된 것으로 나타날 때까지 기다립니다.
      * 작업 > 시작을 선택합니다.
   * Adobe가 미리 구성하거나 수동으로 구성한 JBoss 설치의 경우:

      * 명령 프롬프트에서 *`[appserver root]`*/bin으로 이동합니다.
      * 다음 명령을 입력하여 서버를 중지합니다.

         * (Windows) `shutdown.bat -S`
         * (Linux) `./shutdown.sh -S`
      * JBoss 프로세스가 완전히 종료될 때까지 기다립니다(JBoss 프로세스가 시작한 터미널에 컨트롤을 반환할 때).
      * 다음 명령을 입력하여 서버를 시작합니다.

         * (Windows) `run.bat -c <profile>`
         * (Linux) `./run.sh -c <profile>`



1. SSL을 사용하여 관리 콘솔에 액세스하려면 웹 브라우저 `https://[host name]:'port'/adminui` 에 입력합니다.

   JBoss의 기본 SSL 포트는 8443입니다. 여기서 AEM 양식에 액세스할 때 이 포트를 지정합니다.

## CA에서 자격 증명 요청 {#request-a-credential-from-a-ca}

1. 명령 프롬프트에서 *[JAVA HOME]*/bin으로 이동하고 다음 명령을 입력하여 keystore와 키를 생성합니다.

   `keytool -genkey -dname "CN=`*호스트 그룹&#x200B;*그룹 이름`, OU=`** 회사 이름 `, O=`*City Name *CityNameStateName`, L=`** `, S=`**`, C=`**`-alias "AEMForms Cert"` `-keyalg RSA -keypass`** `-keystore`*StateNameCnameCountry CodeCountry CodeCumulativeCumulative_key passwordKeystore이름&#x200B;*`.keystore`

   >[!NOTE]
   >
   >JDK가 설치되어 있는 디렉토리 *`[JAVA_HOME]`* 로 대체하고 기울임꼴로 표시된 텍스트를 사용자 환경에 해당하는 값으로 바꿉니다.

1. 인증서 기관에 전송할 인증서 요청을 생성하려면 다음 명령을 입력합니다.

   `keytool -certreq -alias` &quot;AEMForms Cert&quot; `-keystore`*keystorename *`.keystore -file`*AEMFormscertRequest.csr*

1. 인증서 파일에 대한 요청이 완료되면 다음 절차를 완료하십시오.

## CA에서 얻은 자격 증명을 사용하여 SSL을 활성화합니다. {#use-a-credential-obtained-from-a-ca-to-enable-ssl}

1. 명령 프롬프트에서 *`[JAVA HOME]`*/bin으로 이동하고 다음 명령을 입력하여 CSR이 서명된 CA의 루트 인증서를 가져옵니다.

   `keytool -import -trustcacerts -file` rootcert.pem -keystore` keystorename.keystore -alias root`

   루트 인증서가 브라우저에 없는 경우 해당 인증서를 브라우저에 가져옵니다.

   >[!NOTE]
   >
   >JDK가 설치되어 있는 디렉토리 *`[JAVA_HOME]`로 대체하고 기울임꼴로 표시된 텍스트를 사용자 환경에 해당하는 값으로 바꿉니다.*

1. 명령 프롬프트에서 *`[JAVA HOME]`*/bin으로 이동하고 다음 명령을 입력하여 자격 증명을 키 저장소에 가져옵니다.

   `keytool -import -trustcacerts -file`*CACertificateName *`.crt -keystore`*키스토어이름* `.keystore`

   >[!NOTE]
   >
   >* JDK가 설치되어 있는 디렉토리 `[JAVA_HOME]` 로 대체하고 기울임꼴로 표시된 텍스트를 사용자 환경에 해당하는 값으로 바꿉니다.
   >* 가져온 CA 서명 인증서는 자체 서명된 공용 인증서가 있는 경우 대체됩니다.


1. SSL 자격 증명 만들기의 13 - 18단계를 완료합니다.
