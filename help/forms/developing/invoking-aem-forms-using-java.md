---
title: JavaAPI를 사용하여 AEM Forms 호출
description: 원격 호출에는 RMI 전송 프로토콜용 AEM Forms Java API, 로컬 호출에는 VM 전송, 원격 호출에는 SOAP, 사용자 이름 및 암호와 같은 다양한 인증, 동기 및 비동기 호출 요청을 사용합니다.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
role: Developer
exl-id: 036c35c1-1be7-4825-bbb6-ea025e49c6f6
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '5393'
ht-degree: 0%

---

# Java API를 사용하여 AEM Forms 호출 {#invoking-aem-forms-using-the-javaapi}

**이 문서의 샘플 및 예제는 JEE 환경의 AEM Forms에 대해서만 적용됩니다.**

AEM Forms은 AEM Forms Java API를 사용하여 호출할 수 있습니다. AEM Forms Java API를 사용하는 경우 호출 API 또는 Java 클라이언트 라이브러리를 사용할 수 있습니다. Java 클라이언트 라이브러리는 Rights Management 서비스와 같은 서비스에 사용할 수 있습니다. 이러한 강력한 형식의 API를 사용하면 AEM Forms을 호출하는 Java 애플리케이션을 개발할 수 있습니다.

호출 API는 `com.adobe.idp.dsc` 패키지. 이러한 클래스를 사용하여 서비스에 직접 호출 요청을 보내고 반환되는 호출 응답을 처리할 수 있습니다. Workbench를 사용하여 생성된 단기 또는 장기 프로세스를 호출하려면 호출 API를 사용합니다.

서비스를 프로그래밍 방식으로 호출하는 권장 방법은 Invocation API와 반대로 서비스에 해당하는 Java 클라이언트 라이브러리를 사용하는 것입니다. 예를 들어 암호화 서비스를 호출하려면 암호화 서비스 클라이언트 라이브러리를 사용합니다. 암호화 서비스 작업을 수행하려면 암호화 서비스 클라이언트 개체에 속하는 메서드를 호출합니다. 암호로 PDF 문서를 암호화하려면 `EncryptionServiceClient` 개체 `encryptPDFUsingPassword` 메서드를 사용합니다.

Java API는 다음 기능을 지원합니다.

* 원격 호출을 위한 RMI 전송 프로토콜
* 로컬 호출을 위한 VM 전송
* 원격 호출용 SOAP
* 다른 인증(예: 사용자 이름 및 암호)
* 동기 및 비동기 호출 요청

[AEM Forms Java 라이브러리 파일 포함](#including-aem-forms-java-library-files)

[인간 중심의 장기 프로세스 호출](invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)

[웹 서비스를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md)

[연결 속성 설정](#setting-connection-properties)

[Java API를 사용하여 AEM Forms 서비스에 데이터 전달](#passing-data-to-aem-forms-services-using-the-java-api)

[Java 클라이언트 라이브러리를 사용하여 서비스 호출](#invoking-a-service-using-a-java-client-library)

[호출 API를 사용하여 단기 프로세스 호출](#invoking-a-short-lived-process-using-the-invocation-api)

[인간 중심의 장기 프로세스를 호출하는 Java 웹 애플리케이션 만들기](/help/forms/developing/invoking-human-centric-long-lived.md)

## AEM Forms Java 라이브러리 파일 포함 {#including-aem-forms-java-library-files}

Java API를 사용하여 AEM Forms 서비스를 프로그래밍 방식으로 호출하려면 Java 프로젝트의 클래스 경로에 필수 라이브러리 파일(JAR 파일)을 포함합니다. 클라이언트 응용 프로그램의 클래스 경로에 포함하는 JAR 파일은 다음과 같은 몇 가지 요소에 따라 다릅니다.

* 호출할 AEM Forms 서비스입니다. 클라이언트 애플리케이션은 하나 이상의 서비스를 호출할 수 있습니다.
* AEM Forms 서비스를 호출할 모드입니다. EJB 또는 SOAP 모드를 사용할 수 있습니다. (참조: [연결 속성 설정](invoking-aem-forms-using-java.md#setting-connection-properties).)

>[!NOTE]
>
>(Turnkey만 해당) 명령을 사용하여 AEM Forms 서버 시작 `standalone.bat -b <Server IP> -c lc_turnkey.xml` EJB에 대한 서버 IP를 지정하려면

* AEM Forms이 배포되는 J2EE 애플리케이션 서버입니다.

### 서비스별 JAR 파일 {#service-specific-jar-files}

다음 표에는 AEM Forms 서비스를 호출하는 데 필요한 JAR 파일이 나와 있습니다.

<table>
 <thead>
  <tr>
   <th><p>파일</p></th>
   <th><p>설명</p></th>
   <th><p>위치</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>adobe-livecycle-client.jar</p></td>
   <td><p>항상 Java 클라이언트 애플리케이션의 클래스 경로에 포함되어야 합니다.</p></td>
   <td><p>&lt;<i>설치 디렉토리</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-usermanager-client.jar</p></td>
   <td><p>항상 Java 클라이언트 애플리케이션의 클래스 경로에 포함되어야 합니다.</p></td>
   <td><p>&lt;<i>설치 디렉토리</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-utilities.jar</p></td>
   <td><p>항상 Java 클라이언트 애플리케이션의 클래스 경로에 포함되어야 합니다.</p></td>
   <td><p>&lt;<i>설치 디렉토리</i>&gt;/sdk//client-libs/&lt;app server=""&gt;</p></td>
  </tr>
  <tr>
   <td><p>adobe-applicationmanager-client-sdk.jar</p></td>
   <td><p>응용 프로그램 관리자 서비스를 호출하는 데 필요합니다.</p></td>
   <td><p>&lt;<i>설치 디렉토리</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-assembler-client.jar</p></td>
   <td><p>어셈블러 서비스를 호출하는 데 필요합니다. </p></td>
   <td><p>&lt;<i>설치 디렉토리</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-backup-restore-client-sdk.jar</p></td>
   <td><p>백업 및 복원 서비스 API를 호출하는 데 필요합니다.</p></td>
   <td><p>&lt;<i>설치 디렉토리</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-barcodedforms-client.jar</p></td>
   <td><p>바코드 양식 서비스를 호출하는 데 필요합니다. </p></td>
   <td><p>&lt;<i>설치 디렉토리</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-convertpdf-client.jar</p></td>
   <td><p>PDF 변환 서비스를 호출하는 데 필요합니다. </p></td>
   <td><p>&lt;<i>설치 디렉토리</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-distiller-client.jar</p></td>
   <td><p>Distiller 서비스를 호출하는 데 필요합니다.</p></td>
   <td><p>&lt;<i>설치 디렉토리</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-docconverter-client.jar</p></td>
   <td><p>DocConverter 서비스를 호출하는 데 필요합니다.</p></td>
   <td><p>&lt;<i>설치 디렉토리</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-contentservices-client.jar</p></td>
   <td><p>문서 관리 서비스를 호출하는 데 필요합니다.</p></td>
   <td><p>&lt;<i>설치 디렉토리</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-encryption-client.jar</p></td>
   <td><p>암호화 서비스를 호출하는 데 필요합니다.</p></td>
   <td><p>&lt;<i>설치 디렉토리</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-forms-client.jar</p></td>
   <td><p>Forms 서비스를 호출하는 데 필요합니다.</p></td>
   <td><p>&lt;<i>설치 디렉토리</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-formdataintegration-client.jar</p></td>
   <td><p>양식 데이터 통합 서비스를 호출하는 데 필요합니다.</p></td>
   <td><p>&lt;<i>설치 디렉토리</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-generatepdf-client.jar</p></td>
   <td><p>PDF 생성 서비스를 호출하는 데 필요합니다.</p></td>
   <td><p>&lt;<i>설치 디렉토리</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-generate3dpdf-client.jar</p></td>
   <td><p>3D PDF 생성 서비스를 호출하는 데 필요합니다.</p></td>
   <td><p>&lt;<i>설치 디렉토리</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-jobmanager-client-sdk.jar</p></td>
   <td><p>작업 관리자 서비스를 호출하는 데 필요합니다. </p></td>
   <td><p>&lt;<i>설치 디렉토리</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-output-client.jar</p></td>
   <td><p>출력 서비스를 호출하는 데 필요합니다.</p></td>
   <td><p>&lt;<i>설치 디렉토리</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-pdfutility-client.jar</p></td>
   <td><p>PDF 유틸리티 또는 XMP 유틸리티 서비스를 호출하는 데 필요합니다.</p></td>
   <td><p>&lt;<i>설치 디렉토리</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-reader-extensions-client.jar</p></td>
   <td><p>Acrobat Reader DC 확장 서비스를 호출하는 데 필요합니다.</p></td>
   <td><p>&lt;<i>설치 디렉토리</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-repository-client.jar</p><p>commons-codec-1.3.jar</p></td>
   <td><p>저장소 서비스를 호출하는 데 필요합니다.</p></td>
   <td><p>&lt;<i>설치 디렉토리</i>&gt;/sdk/client-libs/common</p><p>&lt;<i>설치 디렉토리</i>&gt;/sdk/client-libs\thirdparty</p></td>
  </tr>
  <tr>
   <td>
    <ul>
     <li><p>adobe-rightsmanagement-client.jar</p></li>
     <li><p>namespace.jar</p></li>
     <li><p>jaxb-api.jar</p></li>
     <li><p>jaxb-impl.jar</p></li>
     <li><p>jaxb-libs.jar</p></li>
     <li><p>jaxb-xjc.jar</p></li>
     <li><p>relaxngDatatype.jar</p></li>
     <li><p>xsdlib.jar</p></li>
    </ul></td>
   <td><p>Rights Management 서비스를 호출하는 데 필요합니다.</p><p>AEM Forms이 JBoss에 배포된 경우 이러한 모든 파일을 포함합니다. </p></td>
   <td><p>&lt;<i>설치 디렉토리</i>&gt;/sdk/client-libs/common</p><p>JBoss 관련 lib 디렉터리</p></td>
  </tr>
  <tr>
   <td><p>adobe-signatures-client.jar</p></td>
   <td><p>서명 서비스를 호출하는 데 필요합니다.</p></td>
   <td><p>&lt;<i>설치 디렉토리</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-taskmanager-client-sdk.jar</p></td>
   <td><p>작업 관리자 서비스를 호출하는 데 필요합니다. </p></td>
   <td><p>&lt;<i>설치 디렉토리</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-truststore-client.jar</p></td>
   <td><p>Trust Store 서비스를 호출하는 데 필요합니다. </p></td>
   <td><p>&lt;<i>설치 디렉토리</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
 </tbody>
</table>

### 연결 모드 및 J2EE 응용 프로그램 JAR 파일 {#connection-mode-and-j2ee-application-jar-files}

다음 표에는 연결 모드에 따라 달라지는 JAR 파일과 AEM Forms이 배포되는 J2EE 애플리케이션 서버가 나열되어 있습니다.

<table>
 <thead>
  <tr>
   <th><p>파일</p> </th>
   <th><p>설명</p> </th>
   <th><p>위치</p> </th>
  </tr>
 &lt;/thead align="left"&gt;
 <tbody>
  <tr>
   <td>
    <ul>
     <li><p>activation.jar</p> </li>
     <li><p>axis.jar</p> </li>
     <li><p>commons-codec-1.3.jar</p> </li>
     <li><p>commons-collections-3.1.jar</p> </li>
     <li><p>commons-discovery.jar</p> </li>
     <li><p>commons-logging.jar</p> </li>
     <li><p>dom3-xml-apis-2.5.0.jar</p> </li>
     <li><p>jaxen-1.1-beta-9.jar</p> </li>
     <li><p>jaxrpc.jar</p> </li>
     <li><p>log4j.jar</p> </li>
     <li><p>mail.jar</p> </li>
     <li><p>saaj.jar</p> </li>
     <li><p>wsdl4j.jar</p> </li>
     <li><p>xalan.jar</p> </li>
     <li><p>xbean.jar</p> </li>
    </ul>
    <ul>
     <li>xercesImpl.jar<br /> </li>
     <li>commons-httpclient-3.1.jar</li>
    </ul> <p> </p> </td>
   <td><p>soap 모드를 사용하여 AEM Forms을 호출하는 경우 이러한 JAR 파일을 포함하십시오.</p> </td>
   <td><p>&lt;<em>설치 디렉토리</em>&gt;/sdk/client-libs/thirdparty</p> </td>
  </tr>
  <tr>
   <td><p> jboss-client.jar</p> </td>
   <td><p>AEM Forms이 JBoss Application Server에 배포된 경우 이 JAR 파일을 포함합니다.</p> <p>jboss-client.jar와 참조된 jar가 함께 위치하지 않으면 클래스 로더에서 필수 클래스를 찾을 수 없습니다.</p> </td>
   <td><p>JBoss 클라이언트 라이브러리 디렉터리</p> <p>동일한 J2EE 응용 프로그램 서버에 클라이언트 응용 프로그램을 배포하는 경우 이 파일을 포함할 필요가 없습니다.</p> </td>
  </tr>
  <tr>
   <td><p>wlclient.jar</p> </td>
   <td><p>AEM Forms이 BEA WebLogic Server®에 배포된 경우 이 JAR 파일을 포함합니다.</p> </td>
   <td><p>WebLogic 관련 라이브러리 디렉터리</p> <p>동일한 J2EE 응용 프로그램 서버에 클라이언트 응용 프로그램을 배포하는 경우 이 파일을 포함할 필요가 없습니다.</p> </td>
  </tr>
  <tr>
   <td>
    <ul>
     <li><p>com.ibm.ws.admin.client_6.1.0.jar</p> </li>
     <li><p>com.ibm.ws.webservices.thinclient_6.1.0.jar</p> </li>
    </ul> </td>
   <td>
    <ul>
     <li><p>AEM Forms이 WebSphere Application Server에 배포된 경우 이러한 JAR 파일을 포함합니다.</p> </li>
     <li><p>(com.ibm.ws.webservices.thinclient_6.1.0.jar은 웹 서비스 호출에 필요합니다.)</p> </li>
    </ul> </td>
   <td><p>WebSphere 관련 라이브러리 디렉터리(<em>[WAS_HOME]</em>/runtimes)</p> <p>동일한 J2EE 응용 프로그램 서버에 클라이언트 응용 프로그램을 배포하는 경우 이러한 파일을 포함할 필요가 없습니다.</p> </td>
  </tr>
 </tbody>
</table>

### 시나리오 호출 {#invoking-scenarios}

다음 표는 호출 시나리오를 지정하고 AEM Forms을 성공적으로 호출하는 데 필요한 JAR 파일을 나열합니다.

<table>
 <thead>
  <tr>
   <th><p>서비스</p> </th>
   <th><p>호출 모드</p> </th>
   <th><p>J2EE 응용 프로그램 서버</p> </th>
   <th><p>필수 JAR 파일</p> </th>
  </tr>
 &lt;/thead align="left"&gt;
 <tbody>
  <tr>
   <td><p>Forms 서비스</p> </td>
   <td><p>EJB</p> </td>
   <td><p>JBoss</p> </td>
   <td>
    <ul>
     <li><p>adobe-livecycle-client.jar</p> </li>
     <li><p>adobe-usermanager-client.jar</p> </li>
    </ul>
    <ul>
     <li>jboss-client.jar</li>
    </ul>
    <ul>
     <li>adobe-forms-client.jar<br /> </li>
     <li>commons-httpclient-3.1.jar</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Forms 서비스</p> <p>Acrobat Reader DC 확장 서비스</p> <p>서명 서비스</p> </td>
   <td><p>EJB</p> </td>
   <td><p>JBoss</p> </td>
   <td>
    <ul>
     <li><p>adobe-livecycle-client.jar</p> </li>
     <li><p>adobe-usermanager-client.jar</p> </li>
    </ul>
    <ul>
     <li>jboss-client.jar<br /> </li>
     <li>commons-httpclient-3.1.jar</li>
    </ul>
    <ul>
     <li><p>adobe-forms-client.jar</p> </li>
     <li><p>adobe-reader-extensions-client.jar</p> </li>
     <li><p>adobe-signatures-client.jar</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Forms 서비스</p> </td>
   <td><p>SOAP</p> </td>
   <td><p>WebLogic</p> </td>
   <td>
    <ul>
     <li><p>adobe-livecycle-client.jar</p> </li>
     <li><p>adobe-usermanager-client.jar</p> </li>
     <li><p>wlclient.jar</p> </li>
     <li><p>activation.jar</p> </li>
     <li><p>axis.jar</p> </li>
     <li><p>commons-codec-1.3.jar</p> </li>
     <li><p>commons-collections-3.1.jar</p> </li>
     <li><p>commons-discovery.jar</p> </li>
     <li><p>commons-logging.jar</p> </li>
     <li><p>dom3-xml-apis-2.5.0.jar</p> </li>
     <li><p>jai_imageio.jar</p> </li>
     <li><p>jaxen-1.1-beta-9.jar</p> </li>
     <li><p>jaxrpc.jar</p> </li>
     <li><p>log4j.jar</p> </li>
     <li><p>mail.jar</p> </li>
     <li><p>saaj.jar</p> </li>
     <li><p>wsdl4j.jar</p> </li>
     <li><p>xalan.jar</p> </li>
     <li><p>xbean.jar</p> </li>
     <li><p>xercesImpl.jar</p> </li>
     <li><p>adobe-forms-client.jar</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Forms 서비스</p> <p>Acrobat Reader DC 확장 서비스</p> <p>서명 서비스</p> </td>
   <td><p>SOAP</p> </td>
   <td><p>WebLogic</p> </td>
   <td>
    <ul>
     <li><p>adobe-livecycle-client.jar</p> </li>
     <li><p>adobe-usermanager-client.jar</p> </li>
     <li><p>wlclient.jar</p> </li>
     <li><p>activation.jar</p> </li>
     <li><p>axis.jar</p> </li>
     <li><p>commons-codec-1.3.jar</p> </li>
     <li><p>commons-collections-3.1.jar</p> </li>
     <li><p>commons-discovery.jar</p> </li>
     <li><p>commons-logging.jar</p> </li>
     <li><p>dom3-xml-apis-2.5.0.jar</p> </li>
     <li><p>jai_imageio.jar</p> </li>
     <li><p>jaxen-1.1-beta-9.jar</p> </li>
     <li><p>jaxrpc.jar</p> </li>
     <li><p>log4j.jar</p> </li>
     <li><p>mail.jar</p> </li>
     <li><p>saaj.jar</p> </li>
     <li><p>wsdl4j.jar</p> </li>
     <li><p>xalan.jar</p> </li>
     <li><p>xbean.jar</p> </li>
     <li><p>xercesImpl.jar</p> </li>
     <li><p>adobe-forms-client.jar</p> </li>
     <li><p>adobe-reader-extensions-client.jar</p> </li>
     <li><p>adobe-signatures-client.jar</p> </li>
    </ul> </td>
  </tr> xmp-uti
 </tbody>
</table>

### JAR 파일 업그레이드 {#upgrading-jar-files}

LiveCycle에서 AEM Forms으로 업그레이드하는 경우 Java 프로젝트의 클래스 경로에 AEM Forms JAR 파일을 포함하는 것이 좋습니다. 예를 들어 Rights Management 서비스와 같은 서비스를 사용하는 경우 클래스 경로에 AEM Forms JAR 파일을 포함하지 않으면 호환성 문제가 발생합니다.

AEM Forms으로 업그레이드한다고 가정합니다. Rights Management 서비스를 호출하는 Java 애플리케이션을 사용하려면 다음 JAR 파일의 AEM Forms 버전을 포함합니다.

* adobe-rightsmanagement-client.jar
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar

**추가 참조**

[Java API를 사용하여 AEM Forms 호출](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[연결 속성 설정](invoking-aem-forms-using-java.md#setting-connection-properties)

[Java API를 사용하여 AEM Forms 서비스에 데이터 전달](invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)

[Java 클라이언트 라이브러리를 사용하여 서비스 호출](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## 연결 속성 설정 {#setting-connection-properties}

Java API를 사용할 때 AEM Forms을 호출하도록 연결 속성을 설정합니다. 연결 속성을 설정할 때 서비스를 원격으로 호출할지 로컬로 호출할지 지정하고 연결 모드 및 인증 값도 지정합니다. 서비스 보안이 활성화된 경우 인증 값이 필요합니다. 그러나 서비스 보안이 비활성화되어 있으면 인증 값을 지정할 필요가 없습니다.

연결 모드는 SOAP 또는 EJB 모드일 수 있습니다. EJB 모드는 RMI/IIOP 프로토콜을 사용하며 EJB 모드의 성능이 SOAP 모드의 성능보다 좋습니다. SOAP 모드는 J2EE 애플리케이션 서버 종속성을 제거하거나 AEM Forms과 클라이언트 애플리케이션 사이에 방화벽이 있는 경우에 사용됩니다. SOAP 모드는 https 프로토콜을 기본 전송으로 사용하며 방화벽 경계를 넘어 통신할 수 있습니다. J2EE 애플리케이션 서버 종속성과 방화벽이 모두 문제가 되지 않는 경우 EJB 모드를 사용하는 것이 좋습니다.

AEM Forms 서비스를 성공적으로 호출하려면 다음 연결 속성을 설정하십시오.

* **DSC_DEFAULT_EJB_ENDPOINT:** EJB 연결 모드를 사용하는 경우 이 값은 AEM Forms이 배포되는 J2EE 애플리케이션 서버의 URL을 나타냅니다. AEM Forms을 원격으로 호출하려면 AEM Forms이 배포되는 J2EE 응용 프로그램 서버 이름을 지정합니다. 클라이언트 응용 프로그램이 동일한 J2EE 응용 프로그램 서버에 있는 경우 `localhost`. AEM Forms이 배포된 J2EE 응용 프로그램 서버에 따라 다음 값 중 하나를 지정합니다.

   * JBos: `https://<ServerName>:8080 (default port)`
   * WebSphere: `iiop://<ServerName>:2809 (default port)`
   * 웹 논리: `t3://<ServerName>:7001 (default port)`

* **DSC_DEFAULT_SOAP_ENDPOINT**: SOAP 연결 모드를 사용하는 경우 이 값은 호출 요청이 전송되는 종단점을 나타냅니다. AEM Forms을 원격으로 호출하려면 AEM Forms이 배포되는 J2EE 응용 프로그램 서버 이름을 지정합니다. 클라이언트 응용 프로그램이 동일한 J2EE 응용 프로그램 서버에 있는 경우 `localhost` (예: `http://localhost:8080`.)

   * 포트 값 `8080` J2EE 응용 프로그램이 JBoss인 경우 적용됩니다. J2EE 응용 프로그램 서버가 IBM® WebSphere®인 경우 포트를 사용합니다 `9080`. 마찬가지로, J2EE 응용 프로그램 서버가 WebLogic인 경우 포트를 사용합니다 `7001`. 이 값은 기본 포트 값입니다. 포트 값을 변경하는 경우 해당 포트 번호를 사용하십시오.)

* **DSC_TRANSPORT_PROTOCOL**: EJB 연결 모드를 사용하는 경우 다음을 지정합니다 `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL` 이 값에 사용할 수 있습니다. SOAP 연결 모드를 사용하는 경우 `ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL`.
* **DSC_SERVER_TYPE**: AEM Forms이 배포되는 J2EE 애플리케이션 서버를 지정합니다. 유효한 값은 다음과 같습니다. `JBoss`, `WebSphere`, `WebLogic`.

   * 이 연결 속성을 다음으로 설정하는 경우 `WebSphere`, `java.naming.factory.initial` 값이 (으)로 설정됨 `com.ibm.ws.naming.util.WsnInitCtxFactory`.
   * 이 연결 속성을 다음으로 설정하는 경우 `WebLogic`, `java.naming.factory.initial` 값이 (으)로 설정됨 `weblogic.jndi.WLInitialContextFactory`.
   * 마찬가지로, 이 연결 속성을 다음으로 설정하면 `JBoss`, `java.naming.factory.initial` 값이 (으)로 설정됨 `org.jnp.interfaces.NamingContextFactory`.
   * 다음을 설정할 수 있습니다. `java.naming.factory.initial` 속성을 기본값을 사용하지 않으려면 요구 사항을 충족하는 값으로 설정하십시오.

  >[!NOTE]
  >
  >문자열을 사용하여 `DSC_SERVER_TYPE` connection 속성에서 의 정적 멤버를 `ServiceClientFactoryProperties` 클래스. 다음 값을 사용할 수 있습니다. `ServiceClientFactoryProperties.DSC_WEBSPHERE_SERVER_TYPE`, `ServiceClientFactoryProperties.DSC_WEBLOGIC_SERVER_TYPE`, 또는 `ServiceClientFactoryProperties.DSC_JBOSS_SERVER_TYPE`.

* **DSC_CREDENTIAL_USERNAME:** AEM Forms 사용자 이름을 지정합니다. 사용자가 AEM Forms 서비스를 성공적으로 호출하려면 서비스 사용자 역할이 필요합니다. 사용자는 서비스 호출 권한을 포함하는 다른 역할도 가질 수 있습니다. 그렇지 않으면 서비스를 호출하려고 할 때 예외가 throw됩니다. 서비스 보안이 비활성화되어 있으면 이 연결 속성을 지정할 필요가 없습니다.
* **DSC_CREDENTIAL_PASSWORD:** 해당 암호 값을 지정합니다. 서비스 보안이 비활성화되어 있으면 이 연결 속성을 지정할 필요가 없습니다.
* **DSC_REQUEST_TIMEOUT:** SOAP 요청에 대한 기본 요청 시간 제한1200000 밀리초(20분)입니다. 작업을 완료하는 데 요청이 더 오래 걸릴 수 있는 경우가 있습니다. 예를 들어 큰 레코드 집합을 검색하는 SOAP 요청에는 더 긴 시간 제한 제한이 필요할 수 있습니다. 다음을 사용할 수 있습니다. `ServiceClientFactoryProperties.DSC_REQUEST_TIMEOUT` SOAP 요청에 대한 요청 호출 시간 제한 을 늘리려면 다음을 수행하십시오.

  **참고**: SOAP 기반 호출만 DSC_REQUEST_TIMEOUT 속성을 지원합니다.

연결 등록 정보를 설정하려면 다음 작업을 수행하십시오.

1. 만들기 `java.util.Properties` 개체를 만들 때 사용됩니다.
1. 을(를) 설정하려면 `DSC_DEFAULT_EJB_ENDPOINT` 연결 속성, 호출 `java.util.Properties` 개체 `setProperty` 메서드를 실행하고 다음 값을 전달합니다.

   * 다음 `ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT` 열거형 값
   * AEM Forms을 호스팅하는 J2EE 애플리케이션 서버의 URL을 지정하는 문자열 값

   >[!NOTE]
   >
   >SOAP 연결 모드를 사용하는 경우 `ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT` 열거형 값 대신 `ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT` 열거형 값입니다.

1. 을(를) 설정하려면 `DSC_TRANSPORT_PROTOCOL` 연결 속성, 호출 `java.util.Properties` 개체 `setProperty` 메서드를 실행하고 다음 값을 전달합니다.

   * 다음 `ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL` 열거형 값
   * 다음 `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL` 열거형 값

   >[!NOTE]
   >
   >SOAP 연결 모드를 사용하는 경우 `ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL`열거형 값 대신 `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL` 열거형 값입니다.

1. 을(를) 설정하려면 `DSC_SERVER_TYPE` 연결 속성, 호출 `java.util.Properties` 개체 `setProperty` 메서드를 실행하고 다음 값을 전달합니다.

   * 다음 `ServiceClientFactoryProperties.DSC_SERVER_TYPE`열거형 값
   * AEM Forms을 호스팅하는 J2EE 응용 프로그램 서버를 지정하는 문자열 값(예: AEM Forms이 JBoss에 배포된 경우 지정) `JBoss`).

      1. 을(를) 설정하려면 `DSC_CREDENTIAL_USERNAME` 연결 속성, 호출 `java.util.Properties` 개체 `setProperty` 메서드를 실행하고 다음 값을 전달합니다.

   * 다음 `ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME` 열거형 값
   * AEM Forms을 호출하는 데 필요한 사용자 이름을 지정하는 문자열 값

      1. 을(를) 설정하려면 `DSC_CREDENTIAL_PASSWORD` 연결 속성, 호출 `java.util.Properties` 개체 `setProperty` 메서드를 실행하고 다음 값을 전달합니다.

   * 다음 `ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD` 열거형 값
   * 해당 암호 값을 지정하는 문자열 값

**JBoss에 대한 EJB 연결 모드 설정**

다음 Java 코드 예제에서는 JBoss에 배포되고 EJB 연결 모드를 사용하는 AEM Forms을 호출하는 연결 속성을 설정합니다.

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "https://<hostname>:8080");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DOCUMENT_HTTP_ENDPOINT,"https://<hostname>:8080");
```

**WebLogic에 대한 EJB 연결 모드 설정**

다음 Java 코드 예제에서는 WebLogic에 배포되고 EJB 연결 모드를 사용하는 AEM Forms을 호출하는 연결 속성을 설정합니다.

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "t3://localhost:7001");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "WebLogic");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
```

**WebSphere에 대한 EJB 연결 모드 설정**

다음 Java 코드 예제에서는 연결 속성을 설정하여 WebSphere에 배포되고 EJB 연결 모드를 사용하는 AEM Forms을 호출합니다.

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "iiop://localhost:2809");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "WebSphere");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
```

**SOAP 연결 모드 설정**

다음 Java 코드 예제에서는 JBoss에 배포된 AEM Forms을 호출하기 위해 SOAP 모드의 연결 속성을 설정합니다.

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "http://localhost:8080");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
```

>[!NOTE]
>
>SOAP 연결 모드를 선택하는 경우 클라이언트 응용 프로그램의 클래스 경로에 추가 JAR 파일을 포함해야 합니다.

**서비스 보안이 비활성화될 때 연결 속성 설정**

다음 Java 코드 예제에서는 JBoss Application Server에 배포된 AEM Forms을 호출하는 데 필요한 연결 속성을 설정하고 서비스 보안이 비활성화되어 있습니다.

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "jnp://localhost:1099");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
```

>[!NOTE]
>
>AEM Forms을 사용한 프로그래밍과 연결된 모든 Java 빠른 시작은 EJB 및 SOAP 연결 설정을 모두 표시합니다.

**사용자 지정 요청 시간 제한을 사용하여 SOAP 연결 모드 설정**

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "http://localhost:8080");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_REQUEST_TIMEOUT, "1800000"); // Request timeout limit 30 Minutes
```

**Context 개체를 사용하여 AEM Forms 호출**

다음을 사용할 수 있습니다. `com.adobe.idp.Context` 인증된 사용자로 AEM Forms 서비스를 호출하는 개체( `com.adobe.idp.Context` 개체는 인증된 사용자를 나타냅니다.) 사용 시 `com.adobe.idp.Context` 개체, 를 설정할 필요가 없습니다 `DSC_CREDENTIAL_USERNAME` 또는 `DSC_CREDENTIAL_PASSWORD` 속성. 다음을 얻을 수 있습니다. `com.adobe.idp.Context` 개체 `AuthenticationManagerServiceClient` 개체 `authenticate` 메서드를 사용합니다.

다음 `authenticate` 메서드가 다음을 반환합니다. `AuthResult` 인증 결과가 포함된 개체입니다. 다음을 만들 수 있습니다. `com.adobe.idp.Context` 해당 생성자를 호출하여 개체를 작성합니다. 그런 다음 를 호출합니다 `com.adobe.idp.Context` 개체 `initPrincipal` 메서드 및 전달 `AuthResult` 다음 코드와 같이 개체를 선택합니다.

```java
 Context myCtx = new Context();
 myCtx.initPrincipal(authResult);
```

를 설정하는 대신 `DSC_CREDENTIAL_USERNAME` 또는 `DSC_CREDENTIAL_PASSWORD` 속성을 사용하여 `ServiceClientFactory` 개체 `setContext` 메서드 및 전달 `com.adobe.idp.Context` 개체. AEM Forms 사용자를 사용하여 서비스를 호출하는 경우 다음과 같은 역할이 있는지 확인하십시오 `Services User` AEM Forms 서비스를 호출하는 데 필요합니다.

다음 코드 예제에서는 를 사용하는 방법을 보여 줍니다 `com.adobe.idp.Context` 개체를 만드는 데 사용되는 연결 설정 내의 개체 `EncryptionServiceClient` 개체.

```java
 //Authenticate a user and use the Context object within connection settings
 // Authenticate the user
 String username = "wblue";
 String password = "password";
 AuthResult authResult = authClient.authenticate(username, password.getBytes());
 
 //Set a Content object that represents the authenticated user
 //Use the Context object to invoke the Encryption service
 Context myCtx = new Context();
 myCtx.initPrincipal(authResult);
 
 //Set connection settings
 Properties connectionProps = new Properties();
 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "jnp://<server>:1099");
 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL, ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, ServiceClientFactoryProperties.DSC_JBOSS_SERVER_TYPE);
 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DOCUMENT_HTTP_ENDPOINT,"jnp://<server>:1099");

 
 //Create a ServiceClientFactory object
 ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 myFactory.setContext(myCtx);
 
 //Create an EncryptionServiceClient object
 EncryptionServiceClient encryptClient  = new EncryptionServiceClient(myFactory);
```

>[!NOTE]
>
>사용자 인증에 대한 자세한 내용은 [사용자 인증](/help/forms/developing/users.md#authenticating-users).

### 시나리오 호출 {#invoking_scenarios-1}

이 섹션에서는 다음 호출 시나리오에 대해 설명합니다.

* 자체 JVM(Java Virtual Machine)에서 실행되는 클라이언트 애플리케이션은 독립형 AEM Forms 인스턴스를 호출합니다.
* 자체 JVM에서 실행되는 클라이언트 애플리케이션은 클러스터된 AEM Forms 인스턴스를 호출합니다.

### 독립형 AEM Forms 인스턴스 호출 클라이언트 애플리케이션 {#client-application-invoking-a-stand-alone-aem-forms-instance}

다음 다이어그램은 자체 JVM에서 실행 중인 클라이언트 응용 프로그램과 독립형 AEM Forms 인스턴스 호출을 보여 줍니다.

이 시나리오에서 클라이언트 애플리케이션은 자체 JVM에서 실행 중이며 AEM Forms 서비스를 호출합니다.

>[!NOTE]
>
>이 시나리오는 모든 빠른 시작의 기반이 되는 호출 시나리오입니다.

### 클러스터된 AEM Forms 인스턴스를 호출하는 클라이언트 애플리케이션 {#client-application-invoking-clustered-aem-forms-instances}

다음 다이어그램은 자체 JVM에서 실행되고 있으며 클러스터에서 AEM Forms 인스턴스를 호출하는 클라이언트 응용 프로그램을 보여 줍니다.

이 시나리오는 클라이언트 애플리케이션이 독립 실행형 AEM Forms 인스턴스를 호출하는 것과 유사합니다. 그러나 공급자 URL은 다릅니다. 클라이언트 애플리케이션이 특정 J2EE 애플리케이션 서버에 접속하려는 경우 애플리케이션은 특정 J2EE 애플리케이션 서버를 참조하도록 URL을 변경해야 합니다.

응용 프로그램 서버가 중지되면 클라이언트 응용 프로그램과 AEM Forms 간의 연결이 종료되므로 특정 J2EE 응용 프로그램 서버를 참조하지 않는 것이 좋습니다. 공급자 URL은 특정 J2EE 응용 프로그램 서버 대신 셀 레벨 JNDI 관리자를 참조하는 것이 좋습니다.

SOAP 연결 모드를 사용하는 클라이언트 응용 프로그램은 클러스터에 대해 HTTP 로드 밸런서 포트를 사용할 수 있습니다. EJB 연결 모드를 사용하는 클라이언트 응용 프로그램은 특정 J2EE 응용 프로그램 서버의 EJB 포트에 연결할 수 있습니다. 이 작업은 클러스터 노드 간의 로드 밸런싱을 처리합니다.

**WebSphere**

다음 예제는 WebSphere에 배포된 AEM Forms에 연결하는 데 사용되는 jndi.properties 파일의 내용을 보여 줍니다.

```ini
 java.naming.factory.initial=com.ibm.websphere.naming.
 WsnInitialContextFactory
 java.naming.provider.url=corbaloc::appserver1:9810,:appserver2:9810
```

**Weblogic**

다음 예는 WebLogic에 배포 된 AEM Forms에 연결 하는 데 사용 되는 jndi 속성 파일의 컨텐트를 보여줍니다.

```ini
 java.naming.factory.initial=weblogic.jndi.WLInitialContextFactory
 java.naming.provider.url=t3://appserver1:8001, appserver2:8001
```

**Jboss**

다음 예는 JBoss에 배포 된 AEM Forms에 연결 하는 데 사용 되는 jndi 속성 파일의 컨텐트를 보여줍니다.

```ini
 java.naming.factory.initial= org.jnp.interfaces.NamingContextFactory
 java.naming.provider.url= jnp://appserver1:1099, appserver2:1099,
 appserver3:1099
```

>[!NOTE]
>
>J2EE 애플리케이션 서버 이름과 포트 번호를 확인하려면 관리자에게 문의하십시오.

**추가 참조**

[AEM Forms Java 라이브러리 파일 포함](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Java API를 사용 하 여 AEM Forms 서비스로 데이터 전달](invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)

[Java 클라이언트 라이브러리를 사용 하 여 서비스 호출](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## Java API를 사용 하 여 AEM Forms 서비스로 데이터 전달 {#passing-data-to-aem-forms-services-using-the-java-api}

AEM Forms 서비스 작업은 일반적으로 PDF 문서를 사용하거나 생성합니다. 서비스를 호출할 때 경우에 따라 PDF 문서(또는 XML 데이터와 같은 기타 문서 유형)를 서비스에 전달해야 합니다. 마찬가지로 때로는 서비스에서 반환되는 PDF 문서를 처리해야 합니다. AEM Forms 서비스로 데이터를 주고 받을 수 있는 Java 클래스는 다음과 같습니다 `com.adobe.idp.Document`.

AEM Forms 서비스에서는 PDF 문서를 와 같은 다른 데이터 유형으로 승인하지 않습니다. `java.io.InputStream` 개체 또는 바이트 배열입니다. A `com.adobe.idp.Document` 개체를 사용하여 XML 데이터와 같은 다른 유형의 데이터를 서비스에 전달할 수도 있습니다.

A `com.adobe.idp.Document` 개체가 Java 직렬화 가능 유형이므로 RMI 호출을 통해 전달될 수 있습니다. 수신측은 동일 호스트, 동일 클래스 로더, 로컬(동일 호스트, 상이한 클래스 로더) 또는 원격(상이한 호스트)일 수 있다. 문서 콘텐츠 전달은 각 사례에 맞게 최적화됩니다. 예를 들어 보낸 사람과 받은 사람이 동일한 호스트에 있으면 콘텐츠가 로컬 파일 시스템을 통해 전달됩니다. (경우에 따라 문서를 메모리에 전달할 수 있습니다.)

에 따라 `com.adobe.idp.Document` 개체 크기입니다. 데이터는 다음 내에서 전달됩니다. `com.adobe.idp.Document` 객체 또는 서버의 파일 시스템에 저장됩니다. 가 사용 중인 모든 임시 스토리지 리소스 `com.adobe.idp.Document` 객체는 다음 위치에서 자동으로 제거됩니다. `com.adobe.idp.Document` 폐기. (참조: [문서 객체 배치](invoking-aem-forms-using-java.md#disposing-document-objects).)

경우에 따라 의 콘텐츠 유형을 알고 있어야 합니다. `com.adobe.idp.Document` 를 서비스에 전달하기 전에 개체를 작성합니다. 예를 들어 작업에 다음과 같은 특정 콘텐츠 유형이 필요한 경우 `application/pdf`, 콘텐츠 유형을 결정하는 것이 좋습니다. (참조: [문서의 컨텐트 유형 확인](invoking-aem-forms-using-java.md#determining-the-content-type-of-a-document).)

다음 `com.adobe.idp.Document` 객체는 제공된 데이터를 사용하여 콘텐츠 유형을 확인하려고 합니다. 제공된 데이터에서 컨텐츠 유형을 검색할 수 없는 경우(예: 데이터가 바이트 배열로 제공된 경우) 컨텐츠 유형을 설정합니다. 콘텐츠 유형을 설정하려면 `com.adobe.idp.Document` 개체 `setContentType` 메서드를 사용합니다. (참조: [문서의 컨텐트 유형 확인](invoking-aem-forms-using-java.md#determining-the-content-type-of-a-document))

자료 파일이 동일한 파일 시스템에 있는 경우 `com.adobe.idp.Document` 개체가 더 빠릅니다. 부수적 파일이 원격 파일 시스템에 있는 경우 복사 작업을 수행해야 하므로 성능에 영향을 줍니다.

응용 프로그램에는 두 항목이 모두 포함될 수 있습니다. `com.adobe.idp.Document` 및 `org.w3c.dom.Document` 데이터 유형. 그러나 의 자격을 완전히 갖추었는지 확인합니다. `org.w3c.dom.Document` 데이터 유형. 전환에 대한 정보 `org.w3c.dom.Document` 에 대한 오브젝트 `com.adobe.idp.Document` 개체, 참조 [빠른 시작(EJB 모드): Java API를 사용하여 유동성 레이아웃으로 Forms 미리 채우기](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-prepopulating-forms-with-flowable-layouts-using-the-java-api).

>[!NOTE]
>
>를 사용하는 동안 WebLogic에서 메모리 누수를 방지하려면 `com.adobe.idp.Document` 개체. 문서 정보를 2048바이트 이하의 청크로 읽습니다. 예를 들어 다음 코드는 문서 정보를 2048바이트 단위로 읽습니다.

```java
        // Set up the chunk size to prevent a potential memory leak
        int buffSize = 2048;
 
        // Determine the total number of bytes to read
        int docLength = (int) inDoc.length();
        byte [] byteDoc = new byte[docLength];
 
        // Set up the reading position
        int pos = 0;
 
        // Loop through the document information, 2048 bytes at a time
        while (docLength > 0) {
      // Read the next chunk of information
            int toRead = Math.min(buffSize, docLength);
            int bytesRead = inDoc.read(pos, byteDoc, pos, toRead);
 
            // Handle the exception in case data retrieval failed
            if (bytesRead == -1) {
 
                inDoc.doneReading();
                inDoc.dispose();
                throw new RuntimeException("Data retrieval failed!");
 
            }
 
             // Update the reading position and number of bytes remaining
             pos += bytesRead;
             docLength -= bytesRead;
 
        }
 
        // The document information has been successfully read
        inDoc.doneReading();
        inDoc.dispose();
```

**추가 참조**

[Java API를 사용하여 AEM Forms 호출](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[연결 속성 설정](invoking-aem-forms-using-java.md#setting-connection-properties)

### 문서 만들기 {#creating-documents}

만들기 `com.adobe.idp.Document` PDF 문서(또는 다른 문서 유형)가 입력 값으로 필요한 서비스 작업을 호출하기 전에 개체를 가져옵니다. 다음 `com.adobe.idp.Document` 클래스는 다음 콘텐츠 형식에서 문서를 만들 수 있는 생성자를 제공합니다.

* 바이트 배열
* 기존 항목 `com.adobe.idp.Document` 오브젝트
* A `java.io.File` 오브젝트
* A `java.io.InputStream` 오브젝트
* A `java.net.URL` 오브젝트

#### 바이트 배열을 기반으로 문서 만들기 {#creating-a-document-based-on-a-byte-array}

다음 코드 예제에서는 `com.adobe.idp.Document` 바이트 배열을 기반으로 하는 개체입니다.

**바이트 배열을 기반으로 하는 Document 개체 만들기**

```java
 Document myPDFDocument = new Document(myByteArray);
```

#### 다른 문서를 기반으로 문서 만들기 {#creating-a-document-based-on-another-document}

다음 코드 예제에서는 `com.adobe.idp.Document` 다른 개체를 기반으로 하는 개체 `com.adobe.idp.Document` 개체.

**다른 문서를 기반으로 하는 Document 객체 만들기**

```java
 //Create a Document object based on a byte array
 InputStream is = new FileInputStream("C:\\Map.pdf");
 int len = is.available();
 byte [] myByteArray = new byte[len];
 int i = 0;
 while (i < len) {
       i += is.read(myByteArray, i, len);
 }
 Document myPDFDocument = new Document(myByteArray);
 
 //Create another Document object
 Document anotherDocument = new Document(myPDFDocument);
```

#### 파일을 기반으로 문서 만들기 {#creating-a-document-based-on-a-file}

다음 코드 예제에서는 `com.adobe.idp.Document` 이라는 PDF 파일을 기반으로 하는 개체 *map.pdf*. 이 파일은 C 하드 드라이브의 루트에 있습니다. 이 생성자는 의 MIME 콘텐츠 유형 설정을 시도합니다. `com.adobe.idp.Document` 파일 이름 확장자를 사용하는 개체입니다.

다음 `com.adobe.idp.Document` 을(를) 허용하는 생성자 `java.io.File` 객체도 부울 매개 변수를 허용합니다. 이 매개 변수를 로 설정하여 `true`, `com.adobe.idp.Document` 개체가 파일을 삭제합니다. 이 작업은 파일을 로 전달한 후 제거할 필요가 없음을 의미합니다. `com.adobe.idp.Document` 생성자입니다.

이 매개 변수를 로 설정 `false` 은(는) 이 파일의 소유권을 유지함을 의미합니다. 이 매개 변수를 로 설정 `true` 보다 효율적입니다. 그 이유는 `com.adobe.idp.Document` 개체는 파일을 복사하는 대신 로컬 관리 영역으로 직접 이동할 수 있습니다(속도가 느림).

**PDF 파일을 기반으로 하는 Document 객체 만들기**

```java
 //Create a Document object based on the map.pdf source file
 File mySourceMap = new File("C:\\map.pdf");
 Document myPDFDocument = new Document(mySourceMap,true);
```

#### InputStream 개체를 기반으로 문서 만들기 {#creating-a-document-based-on-an-inputstream-object}

다음 Java 코드 예제에서는 `com.adobe.idp.Document` 를 기반으로 하는 개체 `java.io.InputStream` 개체.

**InputStream 개체를 기반으로 문서 만들기**

```java
 //Create a Document object based on an InputStream object
 InputStream is = new FileInputStream("C:\\Map.pdf");
 Document myPDFDocument = new Document(is);
```

#### URL에서 액세스할 수 있는 컨텐츠를 기반으로 문서 만들기 {#creating-a-document-based-on-content-accessible-from-an-url}

다음 Java 코드 예제에서는 `com.adobe.idp.Document` 이라는 PDF 파일을 기반으로 하는 개체 *map.pdf*. 이 파일은 이름이 인 웹 응용 프로그램 내에 있습니다. `WebApp` 실행 중인 대상: `localhost`. 이 생성자는 다음을 설정하려고 합니다. `com.adobe.idp.Document` url 프로토콜과 함께 반환되는 콘텐츠 형식을 사용하는 개체의 MIME 콘텐츠 형식입니다.

에 제공된 URL `com.adobe.idp.Document` 개체는 항상 원본이 있는 쪽에서 읽습니다. `com.adobe.idp.Document` 다음 예제와 같이 개체가 만들어집니다.

```java
     Document doc = new Document(new java.net.URL("file:c:/temp/input.pdf"));
```

C:/temp/input .pdf 파일은 클라이언트 컴퓨터 (서버 컴퓨터가 아님)에 있어야 합니다. 클라이언트 컴퓨터는 URL를 읽고 개체를 `com.adobe.idp.Document` 만든 위치입니다.

**URL에서 액세스할 수 있는 컨텐츠 기반 문서 만들기**

```java
 //Create a Document object based on a java.net.URL object
 URL myURL = new URL("http", "localhost", 8080,"/WebApp/map.pdf");
 
 //Create another Document object
 Document myPDFDocument = new Document(myURL);
```

**추가 참조**

[Java API를 사용하여 AEM Forms 호출](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[연결 속성 설정](invoking-aem-forms-using-java.md#setting-connection-properties)

### 반환된 문서 처리 {#handling-returned-documents}

PDF 문서 (또는 XML 데이터와 같은 기타 데이터 유형)를 출력 값으로 반환 하는 서비스 작업은 개체를 `com.adobe.idp.Document` 반환 합니다. 개체를 받은 `com.adobe.idp.Document` 후 다음 형식으로 전환 수 있습니다.

* `java.io.File`개체
* `java.io.InputStream`개체
* 바이트 배열

다음 코드 행은 `com.adobe.idp.Document` 에 대한 오브젝트 `java.io.InputStream` 개체. 다음과 같이 가정합니다. `myPDFDocument` 은(는) `com.adobe.idp.Document` 개체:

```java
     java.io.InputStream resultStream = myDocument.getInputStream();
```

마찬가지로 의 내용을 복사할 수 있습니다. `com.adobe.idp.Document` 다음 작업을 수행하여 로컬 파일로 복사합니다.

1. 만들기 `java.io.File` 개체.
1. 호출 `com.adobe.idp.Document` 개체 `copyToFile` 메서드 및 전달 `java.io.File`개체.

다음 코드 예제에서는 의 내용을 `com.adobe.idp.Document` 이라는 파일에 대한 개체 *AnotherMap.pdf*.

**문서 객체의 내용을 파일에 복사**

```java
 File outFile = new File("C:\\AnotherMap.pdf");
 myDocument.copyToFile (outFile);
```

**추가 참조**

[Java API를 사용하여 AEM Forms 호출](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[연결 속성 설정](invoking-aem-forms-using-java.md#setting-connection-properties)

### 문서의 컨텐트 유형 확인 {#determining-the-content-type-of-a-document}

의 MIME 유형 확인 `com.adobe.idp.Document` 를 호출하여 개체 `com.adobe.idp.Document` 개체 `getContentType` 메서드를 사용합니다. 이 메서드는 의 콘텐츠 형식을 지정하는 문자열 값을 반환합니다. `com.adobe.idp.Document` 개체. 다음 표에서는 AEM Forms이 반환하는 다양한 콘텐츠 유형을 설명합니다.

<table>
 <thead>
  <tr>
   <th><p>MIME 유형</p></th>
   <th><p>설명</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p><code>application/pdf</code></p></td>
   <td><p>PDF 문서</p></td>
  </tr>
  <tr>
   <td><p><code>application/vnd.adobe.xdp+xml</code></p></td>
   <td><p>내보낸 XML Forms 아키텍처(XFA) 양식에 사용되는 XDP(XML 데이터 패키징)</p></td>
  </tr>
  <tr>
   <td><p><code>text/xml</code></p></td>
   <td><p>책갈피, 첨부 파일 또는 기타 XML 문서</p></td>
  </tr>
  <tr>
   <td><p><code>application/vnd.fdf</code></p></td>
   <td><p>내보낸 Acrobat 양식에 사용되는 Forms 데이터 형식(FDF)</p></td>
  </tr>
  <tr>
   <td><p><code>application/vnd.adobe.xfdf</code></p></td>
   <td><p>내보낸 Acrobat 양식에 사용되는 XFDF(XML Forms 데이터 형식)</p></td>
  </tr>
  <tr>
   <td><p><code>application/rdf+xml</code></p></td>
   <td><p>리치 데이터 형식 및 XML</p></td>
  </tr>
  <tr>
   <td><p><code>application/octet-stream</code></p></td>
   <td><p>범용 데이터 형식</p></td>
  </tr>
  <tr>
   <td><p><code>NULL</code></p></td>
   <td><p>지정되지 않은 MIME 유형</p></td>
  </tr>
 </tbody>
</table>

다음 코드 예제에서는 `com.adobe.idp.Document` 개체.

**문서 객체의 컨텐트 유형 확인**

```java
 //Determine the content type of the Document object
 String ct = myDocument.getContentType();
 System.out.println("The content type of the Document object is " +ct);
```

**추가 참조**

[Java API를 사용하여 AEM Forms 호출](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[연결 속성 설정](invoking-aem-forms-using-java.md#setting-connection-properties)

### 문서 객체 배치 {#disposing-document-objects}

더 이상 필요하지 않은 경우 `Document` 개체를 삭제하려면 개체를 호출하는 것이 좋습니다 `dispose` 메서드를 사용합니다. 각 `Document` 객체는 파일 설명자와 애플리케이션의 호스트 플랫폼에서 최대 75MB의 RAM 공간을 사용합니다. 다음과 같은 경우 `Document` 객체가 배치되지 않으면 Java Garage 수집 프로세스에서 객체를 처리합니다. 그러나 다음을 사용하여 더 빨리 폐기함으로써 `dispose` 메서드에서 사용 중인 메모리를 `Document` 개체.

**추가 참조**

[Java API를 사용하여 AEM Forms 호출](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Java 클라이언트 라이브러리를 사용하여 서비스 호출](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## Java 클라이언트 라이브러리를 사용하여 서비스 호출 {#invoking-a-service-using-a-java-client-library}

AEM Forms 서비스 작업은 Java 클라이언트 라이브러리로 알려진 서비스의 강력한 형식의 API를 사용하여 호출할 수 있습니다. A *Java 클라이언트 라이브러리* 는 서비스 컨테이너에 배포된 서비스에 대한 액세스를 제공하는 구체적인 클래스 세트입니다. 를 만드는 대신 호출할 서비스를 나타내는 Java 개체를 인스턴스화합니다 `InvocationRequest` 호출 API를 사용하여 개체를 작성합니다. 호출 API는 Workbench에서 생성된 장기 프로세스와 같은 프로세스를 호출하는 데 사용됩니다. (참조: [인간 중심의 장기 프로세스 호출](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).)

서비스 작업을 수행하려면 Java 개체에 속하는 메서드를 호출합니다. Java 클라이언트 라이브러리에는 일반적으로 서비스 작업과 함께 일대일 매핑되는 메서드가 포함되어 있습니다. Java 클라이언트 라이브러리를 사용할 때 필요한 연결 속성을 설정합니다. (참조: [연결 속성 설정](invoking-aem-forms-using-java.md#setting-connection-properties).)

연결 속성을 설정한 후 `ServiceClientFactory` 서비스를 호출할 수 있는 Java 개체를 인스턴스화하는 데 사용되는 개체입니다. Java 클라이언트 라이브러리가 있는 각 서비스에는 해당 클라이언트 개체가 있습니다. 예를 들어 Repository 서비스를 호출하려면 `ResourceRepositoryClient` 개체를 생성자를 사용하고 `ServiceClientFactory` 개체. 다음 `ServiceClientFactory` 개체는 AEM Forms 서비스를 호출하는 데 필요한 연결 설정을 유지 관리하는 역할을 합니다.

를 가져오는 중 `ServiceClientFactory` 는 일반적으로 속도가 빠르며 공장이 처음 사용될 때 약간의 오버헤드가 발생합니다. 이 객체는 재사용을 위해 최적화되므로 가능한 경우 동일한 객체를 사용합니다 `ServiceClientFactory` 객체 여러 Java 클라이언트 객체를 작성하는 경우 즉, 별도의 을 만들지 마십시오 `ServiceClientFactory` 작성한 각 클라이언트 라이브러리 개체에 대한 개체입니다.

내부에 있는 SAML 어설션의 수명을 제어하는 사용자 관리자 설정이 있습니다. `com.adobe.idp.Context` 에 영향을 주는 개체 `ServiceClientFactory` 개체. 이 설정은 Java API를 사용하여 수행되는 모든 호출을 포함하여 AEM Forms 전체의 모든 인증 컨텍스트 수명을 제어합니다. 기본적으로 `ServiceCleintFactory` 개체를 사용할 수 있는 시간은 2시간입니다.

>[!NOTE]
>
>Java API를 사용하여 서비스를 호출하는 방법을 설명하기 위해 저장소 서비스의 `writeResource` 작업이 호출됩니다. 이 작업은 새 리소스를 저장소에 배치 합니다.

Java 클라이언트 라이브러리를 사용 하 고 다음 단계를 수행 하 여 리포지토리 서비스를 실행할 수 있습니다.

1. Java 프로젝트의 클래스 경로에 adobe-repository-client와 같은 클라이언트 JAR 파일을 포함 합니다. 이러한 파일의 위치에 대 한 자세한 내용은 AEM Forms Java 라이브러리 파일 ](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files) 포함을 참조 [ 하십시오.
1. 서비스를 호출 하는 데 필요한 연결 속성을 설정 합니다.
1. 만들기 `ServiceClientFactory` 를 호출하여 개체 `ServiceClientFactory` 오브젝트의 정적 `createInstance` 메서드 및 전달 `java.util.Properties` 연결 속성을 포함하는 개체입니다.
1. 만들기 `ResourceRepositoryClient` 개체를 생성자를 사용하고 `ServiceClientFactory` 개체. 개체를 `ResourceRepositoryClient` 사용 하 여 저장소 서비스 작업을 호출 합니다.
1. 해당 생성자를 사용 하 여 개체를 `RepositoryInfomodelFactoryBean` 만들기 전달 `null` 합니다. 이 개체를 사용 하 여 저장소에 추가 되는 컨텐츠를 나타내는 개체를 `Resource` 만들 수 있습니다.
1. 개체의 `newImage` 메서드를 호출 `RepositoryInfomodelFactoryBean` 하 고 다음 값을 전달 하 여 개체를 만들기 합니다 `Resource` .

   * 지정 `new Id()` 하 여 고유한 ID 값입니다.
   * 다음을 지정하는 고유 UUID 값 `new Lid()`.
   * 리소스의 이름입니다. XDP 파일의 파일 이름을 지정할 수 있습니다.

   반환 값을 다음으로 캐스트 `Resource`.

1. 만들기 `ResourceContent` 를 호출하여 개체 `RepositoryInfomodelFactoryBean` 개체 `newImage` 반환 값을 로 캐스팅하는 방법 `ResourceContent`. 이 객체는 저장소에 추가된 컨텐츠를 나타냅니다.
1. 만들기 `com.adobe.idp.Document` 를 전달하여 개체 `java.io.FileInputStream` 저장소에 추가할 XDP 파일을 저장하는 객체입니다. (참조: [InputStream 개체를 기반으로 문서 만들기](invoking-aem-forms-using-java.md#creating-a-document-based-on-an-inputstream-object).)
1. 의 콘텐츠 추가 `com.adobe.idp.Document` 에 대한 오브젝트 `ResourceContent` 를 호출하여 개체 `ResourceContent` 개체 `setDataDocument` 메서드를 사용합니다. 전달 `com.adobe.idp.Document` 개체.
1. 를 호출하여 저장소에 추가할 XDP 파일의 MIME 유형을 설정합니다. `ResourceContent` 개체 `setMimeType` 방법 및 전달 `application/vnd.adobe.xdp+xml`.
1. 의 콘텐츠 추가 `ResourceContent` 에 대한 오브젝트 `Resource` 를 호출하여 개체 `Resource` 의 오브젝트 `setContent` 메서드 및 전달 `ResourceContent` 개체.
1. 를 호출하여 리소스에 대한 설명을 추가합니다. `Resource` 의 오브젝트 `setDescription` 리소스에 대한 설명을 나타내는 문자열 값을 전달하는 메서드입니다.
1. 를 호출하여 저장소에 양식 디자인을 추가합니다. `ResourceRepositoryClient` 개체 `writeResource` 메서드 및 다음 값 전달:

   * 새 리소스를 포함하는 리소스 컬렉션의 경로를 지정하는 문자열 값
   * 다음 `Resource` 생성된 개체

**추가 참조**

[빠른 시작(EJB 모드): Java API를 사용하여 리소스 쓰기](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)

[Java API를 사용하여 AEM Forms 호출](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

## 호출 API를 사용하여 단기 프로세스 호출 {#invoking-a-short-lived-process-using-the-invocation-api}

Java 호출 API를 사용하여 단기 프로세스를 호출할 수 있습니다. Invocation API를 사용하여 단기 프로세스를 호출하는 경우 `java.util.HashMap` 개체. 서비스로 전달할 각 매개 변수에 대해 `java.util.HashMap` 개체 `put` 지정한 작업을 수행하는 데 필요한 이름-값 쌍을 지정합니다. 단기 프로세스에 속하는 매개변수의 정확한 이름을 지정합니다.

>[!NOTE]
>
>오래 지속되는 프로세스 호출에 대한 자세한 내용은 [인간 중심의 장기 프로세스 호출](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).

여기에서는 호출 API를 사용하여 다음과 같은 AEM Forms 단기 프로세스를 호출하는 방법에 대해 설명합니다. `MyApplication/EncryptDocument`.

>[!NOTE]
>
>이 프로세스는 기존 AEM Forms 프로세스를 기반으로 하지 않습니다. 코드 예제를 따르려면 `MyApplication/EncryptDocument` Workbench를 사용합니다. (참조: [Workbench 사용](https://www.adobe.com/go/learn_aemforms_workbench_63).)

이 프로세스가 호출되면 다음 작업을 수행합니다.

1. 프로세스에 전달되는 비보안 PDF 문서를 가져옵니다. 이 작업은 `SetValue` 작업. 이 프로세스의 입력 매개 변수는 `document` 이름이 인 프로세스 변수 `inDoc`.
1. 암호로 PDF 문서를 암호화합니다. 이 작업은 `PasswordEncryptPDF` 작업. 암호로 암호화된 PDF 문서가 이라는 프로세스 변수에 반환됩니다 `outDoc`.

### Java 호출 API를 사용하여 MyApplication/EncryptDocument 단기 프로세스 호출 {#invoke-the-myapplication-encryptdocument-short-lived-process-using-the-java-invocation-api}

호출 `MyApplication/EncryptDocument` java 호출 API를 사용한 단기 프로세스:

1. Java 프로젝트의 클래스 경로에 adobe-livecycle-client.jar과 같은 클라이언트 JAR 파일을 포함합니다. (참조: [AEM Forms Java 라이브러리 파일 포함](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).)
1. 만들기 `ServiceClientFactory` 연결 속성을 포함하는 개체입니다. (참조: [연결 속성 설정](invoking-aem-forms-using-java.md#setting-connection-properties).)
1. 만들기 `ServiceClient` 개체를 생성자를 사용하고 `ServiceClientFactory` 개체. A `ServiceClient` 개체를 사용하면 서비스 작업을 호출할 수 있습니다. 호출 요청 찾기, 발송 및 라우팅 등의 작업을 처리합니다.
1. 만들기 `java.util.HashMap` 개체를 만들 때 사용됩니다.
1. 호출 `java.util.HashMap` 개체 `put` 각 입력 매개 변수에 대한 메서드를 long-lived 프로세스에 전달합니다. 이유: `MyApplication/EncryptDocument` 단기 프로세스에는 유형의 입력 매개 변수가 한 개 필요합니다. `Document`, 를 호출하기만 하면 됩니다. `put` 다음 예제와 같이 한 번 메서드입니다.

   ```java
    //Create a Map object to store the parameter value for inDoc
    Map params = new HashMap();
    InputStream inFile = new FileInputStream("C:\\Adobe\Loan.pdf");
    Document inDoc = new Document(inFile);
    params.put("inDoc", inDoc);
   ```

1. 만들기 `InvocationRequest` 를 호출하여 개체 `ServiceClientFactory` 개체 `createInvocationRequest` 메서드 및 다음 값 전달:

   * 호출할 장기 프로세스의 이름을 지정하는 문자열 값입니다. 를 호출하려면 `MyApplication/EncryptDocument` 프로세스, 지정 `MyApplication/EncryptDocument`.
   * 프로세스 작업 이름을 나타내는 문자열 값입니다. 일반적으로 단기 프로세스 작업의 이름은 다음과 같습니다. `invoke`.
   * 다음 `java.util.HashMap` 서비스 작업에 필요한 매개 변수 값을 포함하는 개체입니다.
   * 을 지정하는 부울 값 `true`- 동기 요청을 생성합니다(이 값은 단기 프로세스 호출에 적용할 수 있음).

1. 를 호출하여 호출 요청을 서비스에 보냅니다. `ServiceClient` 개체 `invoke` 메서드 및 전달 `InvocationRequest` 개체. 다음 `invoke` 메서드가 다음을 반환합니다. `InvocationReponse` 개체.

   >[!NOTE]
   >
   >값을 전달하여 장기 프로세스를 호출할 수 있습니다 `false`의 네 번째 매개 변수로 `createInvocationRequest` 메서드를 사용합니다. 값 전달 `false`*비동기 요청을 만듭니다.*

1. 를 호출하여 프로세스의 반환 값을 검색합니다. `InvocationReponse` 개체 `getOutputParameter` 메서드 및 출력 매개 변수의 이름을 지정하는 문자열 값 전달 이 경우 다음을 지정합니다. `outDoc` ( `outDoc` 는 의 출력 매개 변수 이름입니다. `MyApplication/EncryptDocument` 프로세스). 반환 값을 다음으로 캐스트 `Document`다음 예제와 같이 을 참조하십시오.

   ```java
    InvocationResponse response = myServiceClient.invoke(request);
    Document encryptDoc = (Document) response.getOutputParameter("outDoc");
   ```

1. 만들기 `java.io.File` 개체로 식별되고 파일 확장명이 .pdf인지 확인합니다.
1. 호출 `com.adobe.idp.Document` 개체 `copyToFile` 콘텐츠 복사 방법 `com.adobe.idp.Document` 파일에 대한 개체입니다. 다음을 사용하는지 확인합니다. `com.adobe.idp.Document` 에서 반환한 개체 `getOutputParameter` 메서드를 사용합니다.

**추가 참조**

[빠른 시작: 호출 API를 사용하여 단기 프로세스 호출](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-short-lived-process-using-the-invocation-api)

[인간 중심의 장기 프로세스 호출](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)

[AEM Forms Java 라이브러리 파일 포함](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
