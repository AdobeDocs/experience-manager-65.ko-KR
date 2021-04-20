---
title: JavaAPI를 사용하여 AEM Forms 호출
seo-title: JavaAPI를 사용하여 AEM Forms 호출
description: 원격 호출을 위한 RMI 전송 프로토콜용 AEM Forms Java API, 로컬 호출을 위한 VM 전송, 원격 호출을 위한 SOAP, 사용자 이름 및 암호와 같은 다른 인증, 동기 및 비동기 호출 요청 등을 사용하십시오.
seo-description: 원격 호출을 위한 RMI 전송 프로토콜용 AEM Forms Java API, 로컬 호출을 위한 VM 전송, 원격 호출을 위한 SOAP, 사용자 이름 및 암호와 같은 다른 인증, 동기 및 비동기 호출 요청 등을 사용하십시오.
uuid: 5e2fef2a-05f3-4283-8fd3-2d7dca411000
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: 0e6e7850-6137-42c5-b8e2-d4e352fddae2
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '5495'
ht-degree: 0%

---


# Java API {#invoking-aem-forms-using-the-javaapi}를 사용하여 AEM Forms 호출

**이 문서의 샘플과 예는 JEE 환경의 AEM Forms에만 해당됩니다.**

AEM Forms은 AEM Forms Java API를 사용하여 호출할 수 있습니다. AEM Forms Java API를 사용할 때 호출 API 또는 Java 클라이언트 라이브러리를 사용할 수 있습니다. Java 클라이언트 라이브러리는 Rights Management 서비스와 같은 서비스에 사용할 수 있습니다. 강력한 형식의 API를 사용하여 AEM Forms을 호출하는 Java 애플리케이션을 개발할 수 있습니다.

호출 API는 `com.adobe.idp.dsc` 패키지에 있는 클래스입니다. 이러한 클래스를 사용하여 서비스에 직접 호출 요청을 보내고 반환된 호출 응답을 처리할 수 있습니다. Invocation API를 사용하여 Workbench를 사용하여 만든 단기 또는 긴 수명 프로세스를 호출할 수 있습니다.

프로그래밍 방식으로 서비스를 호출하는 권장되는 방법은 호출 API가 아닌 서비스에 해당하는 Java 클라이언트 라이브러리를 사용하는 것입니다. 예를 들어 암호화 서비스를 호출하려면 암호화 서비스 클라이언트 라이브러리를 사용합니다. 암호화 서비스 작업을 수행하려면 암호화 서비스 클라이언트 개체에 속하는 메서드를 호출합니다. `EncryptionServiceClient` 개체의 `encryptPDFUsingPassword` 메서드를 호출하여 암호로 PDF 문서를 암호화할 수 있습니다.

Java API는 다음 기능을 지원합니다.

* 원격 호출을 위한 RMI 전송 프로토콜
* 로컬 호출을 위한 VM 전송
* 원격 호출을 위한 SOAP
* 사용자 이름 및 암호와 같은 다른 인증
* 동기 및 비동기 호출 요청

**Adobe 개발자 웹 사이트**

Adobe 개발자 웹 사이트에는 Java API를 사용한 AEM Forms 서비스 호출과 관련된 다음 문서가 포함되어 있습니다.

[Java 서블릿을 사용하여 AEM Forms 프로세스 호출](https://www.adobe.com/devnet/livecycle/articles/java_servlets.html)

[Java의 AEM Forms Distiller API 호출](https://www.adobe.com/devnet/livecycle/articles/distiller_java_03.html)

**참고 항목**

[AEM Forms Java 라이브러리 파일 포함](#including-aem-forms-java-library-files)

[인간 중심의 오랜 프로세스 호출](invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)

[웹 서비스를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md)

[연결 속성 설정](#setting-connection-properties)

[Java API를 사용하여 AEM Forms 서비스로 데이터 전달](#passing-data-to-aem-forms-services-using-the-java-api)

[Java 클라이언트 라이브러리를 사용하여 서비스 호출](#invoking-a-service-using-a-java-client-library)

[호출 API를 사용하여 짧은 기간 프로세스 호출](#invoking-a-short-lived-process-using-the-invocation-api)

[인간 중심의 오랜 프로세스를 호출하는 Java 웹 애플리케이션 제작](/help/forms/developing/invoking-human-centric-long-lived.md)

## AEM Forms Java 라이브러리 파일 포함 {#including-aem-forms-java-library-files}

Java API를 사용하여 프로그래밍 방식으로 AEM Forms 서비스를 호출하려면 Java 프로젝트의 클래스 경로에 필수 라이브러리 파일(JAR 파일)을 포함합니다. 클라이언트 응용 프로그램의 클래스 경로에 포함하는 JAR 파일은 다음과 같은 여러 요인에 따라 달라집니다.

* 호출할 AEM Forms 서비스. 클라이언트 응용 프로그램은 하나 이상의 서비스를 호출할 수 있습니다.
* AEM Forms 서비스를 호출할 모드. EJB 또는 SOAP 모드를 사용할 수 있습니다. ([연결 속성 설정](invoking-aem-forms-using-java.md#setting-connection-properties)을 참조하십시오.)

>[!NOTE]
>
>(턴키만) `standalone.bat -b <Server IP> -c lc_turnkey.xml` 명령으로 AEM Forms 서버를 시작하여 EJB용 서버 IP를 지정합니다.

* AEM Forms이 배포된 J2EE 응용 프로그램 서버.

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
   <td><p>Java 클라이언트 응용 프로그램의 클래스 경로에 항상 포함되어야 합니다.</p></td>
   <td><p>&lt;&gt;설치 디렉토리</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-usermanager-client.jar</p></td>
   <td><p>Java 클라이언트 응용 프로그램의 클래스 경로에 항상 포함되어야 합니다.</p></td>
   <td><p>&lt;&gt;설치 디렉토리</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-utilities.jar</p></td>
   <td><p>Java 클라이언트 응용 프로그램의 클래스 경로에 항상 포함되어야 합니다.</p></td>
   <td><p>&lt;&gt;설치 디렉토리</i>&gt;/sdk//client-libs/&lt;app server=""&gt;<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-applicationmanager-client-sdk.jar</p></td>
   <td><p>Application Manager 서비스를 호출하는 데 필요합니다.</p></td>
   <td><p>&lt;&gt;설치 디렉토리</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-assembler-client.jar</p></td>
   <td><p>Assembler 서비스를 호출하는 데 필요합니다. </p></td>
   <td><p>&lt;&gt;설치 디렉토리</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-backup-restore-client-sdk.jar</p></td>
   <td><p>백업 및 복원 서비스 API를 호출하는 데 필요합니다.</p></td>
   <td><p>&lt;&gt;설치 디렉토리</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-barcodedforms-client.jar</p></td>
   <td><p>바코드 양식 서비스를 호출해야 합니다. </p></td>
   <td><p>&lt;&gt;설치 디렉토리</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-convertpdf-client.jar</p></td>
   <td><p>PDF 변환 서비스를 호출하는 데 필요합니다. </p></td>
   <td><p>&lt;&gt;설치 디렉토리</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-distiller-client.jar</p></td>
   <td><p>Distiller 서비스를 호출하는 데 필요합니다.</p></td>
   <td><p>&lt;&gt;설치 디렉토리</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-docconverter-client.jar</p></td>
   <td><p>DocConverter 서비스를 호출하는 데 필요합니다.</p></td>
   <td><p>&lt;&gt;설치 디렉토리</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-contentservices-client.jar</p></td>
   <td><p>Document Management 서비스를 호출하는 데 필요합니다.</p></td>
   <td><p>&lt;&gt;설치 디렉토리</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-encryption-client.jar</p></td>
   <td><p>암호화 서비스를 호출하는 데 필요합니다.</p></td>
   <td><p>&lt;&gt;설치 디렉토리</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-forms-client.jar</p></td>
   <td><p>Forms 서비스를 호출하는 데 필요합니다.</p></td>
   <td><p>&lt;&gt;설치 디렉토리</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-formdataintegration-client.jar</p></td>
   <td><p>양식 데이터 통합 서비스를 호출하는 데 필요합니다.</p></td>
   <td><p>&lt;&gt;설치 디렉토리</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-generatepdf-client.jar</p></td>
   <td><p>PDF 생성 서비스를 호출하는 데 필요합니다.</p></td>
   <td><p>&lt;&gt;설치 디렉토리</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-generate3dpdf-client.jar</p></td>
   <td><p>3D PDF 생성 서비스를 호출하는 데 필요합니다.</p></td>
   <td><p>&lt;&gt;설치 디렉토리</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-jobmanager-client-sdk.jar</p></td>
   <td><p>작업 관리자 서비스를 호출하는 데 필요합니다. </p></td>
   <td><p>&lt;&gt;설치 디렉토리</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-output-client.jar</p></td>
   <td><p>출력 서비스를 호출하는 데 필요합니다.</p></td>
   <td><p>&lt;&gt;설치 디렉토리</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-pdfutility-client.jar</p></td>
   <td><p>PDF 유틸리티 또는 XMP 유틸리티 서비스를 호출하는 데 필요합니다.</p></td>
   <td><p>&lt;&gt;설치 디렉토리</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-reader-extensions-client.jar</p></td>
   <td><p>Acrobat Reader DC 확장 서비스를 호출하는 데 필요합니다.</p></td>
   <td><p>&lt;&gt;설치 디렉토리</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-repository-client.jar</p><p>commons-codec-1.3.jar</p></td>
   <td><p>저장소 서비스를 호출하는 데 필요합니다.</p></td>
   <td><p>&lt;&gt;설치 디렉토리</i>&gt;/sdk/client-libs/common<i></i></p><p>&lt;&gt;설치 디렉토리</i>&gt;/sdk/client-libs\thirdparty<i></i></p></td>
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
   <td><p>Rights Management 서비스를 호출하는 데 필요합니다.</p><p>AEM Forms이 JBoss에 배포된 경우 이 파일을 모두 포함합니다. </p></td>
   <td><p>&lt;&gt;설치 디렉토리</i>&gt;/sdk/client-libs/common<i></i></p><p>JBoss 특정 lib 디렉토리</p></td>
  </tr>
  <tr>
   <td><p>adobe-signatures-client.jar</p></td>
   <td><p>서명 서비스를 호출하는 데 필요합니다.</p></td>
   <td><p>&lt;&gt;설치 디렉토리</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-taskmanager-client-sdk.jar</p></td>
   <td><p>작업 관리자 서비스를 호출하는 데 필요합니다. </p></td>
   <td><p>&lt;&gt;설치 디렉토리</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-truststore-client.jar</p></td>
   <td><p>Trust Store 서비스를 호출하는 데 필요합니다. </p></td>
   <td><p>&lt;&gt;설치 디렉토리</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
 </tbody>
</table>

### 연결 모드 및 J2EE 응용 프로그램 JAR 파일 {#connection-mode-and-j2ee-application-jar-files}

다음 표에는 연결 모드에 따라 결정되는 JAR 파일과 AEM Forms이 배포되는 J2EE 응용 프로그램 서버가 나열됩니다.

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
     <li><p>dom3-xml-api-2.5.0.jar</p> </li>
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
   <td><p>SOAP 모드를 사용하여 AEM Forms을 호출하면 이러한 JAR 파일을 포함합니다.</p> </td>
   <td><p>&lt;&gt;설치 디렉토리</em>&gt;/sdk/client-libs/thirdparty<em></em></p> </td>
  </tr>
  <tr>
   <td><p> jboss-client.jar</p> </td>
   <td><p>AEM Forms이 JBoss Application Server에 배포되는 경우 이 JAR 파일을 포함합니다.</p> <p>jboss-client.jar 및 참조된 항어가 함께 있지 않으면 classloader에서 필수 클래스를 찾을 수 없습니다.</p> </td>
   <td><p>JBoss 클라이언트 lib 디렉토리</p> <p>클라이언트 응용 프로그램을 동일한 J2EE 응용 프로그램 서버에 배포하는 경우 이 파일을 포함할 필요가 없습니다.</p> </td>
  </tr>
  <tr>
   <td><p>wlclient.jar</p> </td>
   <td><p>AEM Forms이 BEA WebLogic Server®에 배포되는 경우 이 JAR 파일을 포함합니다.</p> </td>
   <td><p>WebLogic 전용 lib 디렉토리</p> <p>클라이언트 응용 프로그램을 동일한 J2EE 응용 프로그램 서버에 배포하는 경우 이 파일을 포함할 필요가 없습니다.</p> </td>
  </tr>
  <tr>
   <td>
    <ul>
     <li><p>com.ibm.ws.admin.client_6.1.0.jar</p> </li>
     <li><p>com.ibm.ws.webservices.thinclient_6.1.0.jar</p> </li>
    </ul> </td>
   <td>
    <ul>
     <li><p>AEM Forms이 WebSphere 응용 프로그램 서버에 배포되는 경우 이러한 JAR 파일을 포함합니다.</p> </li>
     <li><p>(웹 서비스 호출에는 com.ibm.ws.webservices.thinclient_6.1.0.jar가 필요합니다.)</p> </li>
    </ul> </td>
   <td><p>WebSphere 특정 lib 디렉토리(<em>[WAS_HOME]</em>/runtimes)</p> <p>클라이언트 응용 프로그램을 동일한 J2EE 응용 프로그램 서버에 배포하는 경우 이러한 파일을 포함할 필요가 없습니다.</p> </td>
  </tr>
 </tbody>
</table>

### 시나리오 호출 {#invoking-scenarios}

다음 표에서는 호출 시나리오를 지정하고 AEM Forms을 성공적으로 호출할 필수 JAR 파일을 나열합니다.

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
   <td><p>Forms 서비스</p> <p>Acrobat Reader DC 익스텐션 서비스</p> <p>서명 서비스</p> </td>
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
     <li><p>dom3-xml-api-2.5.0.jar</p> </li>
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
   <td><p>Forms 서비스</p> <p>Acrobat Reader DC 익스텐션 서비스</p> <p>서명 서비스</p> </td>
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
     <li><p>dom3-xml-api-2.5.0.jar</p> </li>
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

### JAR 파일 {#upgrading-jar-files} 업그레이드

LiveCycle에서 AEM Forms으로 업그레이드하는 경우 Java 프로젝트의 클래스 경로에 AEM Forms JAR 파일을 포함하는 것이 좋습니다. 예를 들어 Rights Management 서비스와 같은 서비스를 사용하는 경우 클래스 경로에 AEM Forms JAR 파일을 포함하지 않으면 호환성 문제가 발생합니다.

AEM Forms으로 업그레이드하는 경우 Rights Management 서비스를 호출하는 Java 애플리케이션을 사용하려면 다음 JAR 파일의 AEM Forms 버전을 포함합니다.

* adobe-rightsmanagement-client.jar
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar

**참고 항목**

[Java API를 사용하여 AEM Forms 호출](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[연결 속성 설정](invoking-aem-forms-using-java.md#setting-connection-properties)

[Java API를 사용하여 AEM Forms 서비스로 데이터 전달](invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)

[Java 클라이언트 라이브러리를 사용하여 서비스 호출](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## 연결 속성 {#setting-connection-properties} 설정

Java API를 사용할 때 AEM Forms을 호출하도록 연결 속성을 설정합니다. 연결 속성을 설정할 때 서비스를 원격으로 호출할지 로컬로 호출할지 여부를 지정하고 연결 모드 및 인증 값도 지정합니다. 서비스 보안이 활성화된 경우 인증 값이 필요합니다. 그러나 서비스 보안이 비활성화된 경우에는 인증 값을 지정할 필요가 없습니다.

연결 모드는 SOAP 또는 EJB 모드일 수 있습니다. EJB 모드는 RMI/IIOP 프로토콜을 사용하며 EJB 모드의 성능은 SOAP 모드의 성능보다 뛰어납니다. SOAP 모드는 J2EE 응용 프로그램 서버 종속성을 제거하거나 방화벽이 AEM Forms과 클라이언트 응용 프로그램 사이에 있는 경우에 사용됩니다. SOAP 모드는 https 프로토콜을 기본 전송으로 사용하며 방화벽 경계를 넘어 통신할 수 있습니다. J2EE 응용 프로그램 서버 종속성 또는 방화벽이 모두 문제가 아니면 EJB 모드를 사용하는 것이 좋습니다.

AEM Forms 서비스를 성공적으로 호출하려면 다음 연결 속성을 설정합니다.

* **DSC_DEFAULT_EJB_ENDPOINT:** EJB 연결 모드를 사용하는 경우 이 값은 AEM Forms이 배포된 J2EE 응용 프로그램 서버의 URL을 나타냅니다. AEM Forms을 원격으로 불러오려면 AEM Forms이 배포된 J2EE 응용 프로그램 서버 이름을 지정합니다. 클라이언트 응용 프로그램이 동일한 J2EE 응용 프로그램 서버에 있는 경우 `localhost`을(를) 지정할 수 있습니다. J2EE 응용 프로그램 서버 AEM Forms이 배포된 항목에 따라 다음 값 중 하나를 지정합니다.

   * JBoss:`https://<ServerName>:8080 (default port)`
   * WebSphere:`iiop://<ServerName>:2809 (default port)`
   * WebLogic:`t3://<ServerName>:7001 (default port)`

* **DSC_DEFAULT_SOAP_ENDPOINT**:SOAP 연결 모드를 사용하는 경우 이 값은 호출 요청이 전송되는 끝점을 나타냅니다. AEM Forms을 원격으로 불러오려면 AEM Forms이 배포된 J2EE 응용 프로그램 서버 이름을 지정합니다. 클라이언트 응용 프로그램이 동일한 J2EE 응용 프로그램 서버에 있는 경우 `localhost`(예: `http://localhost:8080`)을 지정할 수 있습니다.

   * 포트 값 `8080`은 J2EE 응용 프로그램이 JBoss인 경우 적용할 수 있습니다. J2EE 응용 프로그램 서버가 IBM® WebSphere®인 경우 `9080` 포트를 사용합니다. 마찬가지로 J2EE 응용 프로그램 서버가 WebLogic이면 `7001` 포트를 사용합니다. 이러한 값은 기본 포트 값입니다. 포트 값을 변경하는 경우 해당 포트 번호를 사용하십시오.)

* **DSC_TRANSPORT_PROTOCOL**:EJB 연결 모드를 사용 중인 경우 이 값 `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL` 에 대해 지정합니다. SOAP 연결 모드를 사용 중인 경우 `ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL`을 지정합니다.
* **DSC_SERVER_TYPE**:AEM Forms이 배포되는 J2EE 응용 프로그램 서버를 지정합니다. 유효한 값은 `JBoss`, `WebSphere`, `WebLogic`입니다.

   * 이 연결 속성을 `WebSphere`으로 설정하면 `java.naming.factory.initial` 값이 `com.ibm.ws.naming.util.WsnInitCtxFactory`로 설정됩니다.
   * 이 연결 속성을 `WebLogic`으로 설정하면 `java.naming.factory.initial` 값이 `weblogic.jndi.WLInitialContextFactory`로 설정됩니다.
   * 마찬가지로 이 연결 속성을 `JBoss`으로 설정하면 `java.naming.factory.initial` 값이 `org.jnp.interfaces.NamingContextFactory`로 설정됩니다.
   * 기본값을 사용하지 않으려는 경우 `java.naming.factory.initial` 속성을 요구 사항을 충족하는 값으로 설정할 수 있습니다.

   >[!NOTE]
   >
   >문자열을 사용하여 `DSC_SERVER_TYPE` 연결 속성을 설정하는 대신 `ServiceClientFactoryProperties` 클래스의 정적 멤버를 사용할 수 있습니다. 다음 값을 사용할 수 있습니다.`ServiceClientFactoryProperties.DSC_WEBSPHERE_SERVER_TYPE`, `ServiceClientFactoryProperties.DSC_WEBLOGIC_SERVER_TYPE` 또는 `ServiceClientFactoryProperties.DSC_JBOSS_SERVER_TYPE`.

* **DSC_CREDENTIAL_USERNAME:** AEM 양식 사용자 이름을 지정합니다. 사용자가 AEM Forms 서비스를 성공적으로 호출하려면 서비스 사용자 역할이 필요합니다. 사용자는 서비스 호출 권한을 포함하는 다른 역할을 가질 수도 있습니다. 그렇지 않으면 서비스를 호출하려고 할 때 예외가 발생합니다. 서비스 보안이 비활성화된 경우 이 연결 속성을 지정할 필요가 없습니다.
* **DSC_CREDENTIAL_PASSWORD:** 해당 암호 값을 지정합니다. 서비스 보안이 비활성화된 경우 이 연결 속성을 지정할 필요가 없습니다.
* **DSC_REQUEST_TIMEOUT:** SOAP 요청에 대한 기본 요청 시간 초과 제한은 1200000 밀리초(20분)입니다. 때로는 요청을 완료하는 데 시간이 더 걸릴 수 있습니다. 예를 들어 대량의 레코드를 검색하는 SOAP 요청에는 더 긴 시간 제한 제한이 필요할 수 있습니다. `ServiceClientFactoryProperties.DSC_REQUEST_TIMEOUT`을 사용하여 SOAP 요청에 대한 요청 호출 시간 초과 제한을 늘릴 수 있습니다.

   **참고**:SOAP 기반 호출만 DSC_REQUEST_TIMEOUT 속성을 지원합니다.

연결 속성을 설정하려면 다음 작업을 수행합니다.

1. 생성자를 사용하여 `java.util.Properties` 객체를 만듭니다.
1. `DSC_DEFAULT_EJB_ENDPOINT` 연결 속성을 설정하려면 `java.util.Properties` 객체의 `setProperty` 메서드를 호출하고 다음 값을 전달합니다.

   * `ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT` 열거형 값
   * AEM Forms을 호스팅하는 J2EE 응용 프로그램 서버의 URL을 지정하는 문자열 값

   >[!NOTE]
   >
   >SOAP 연결 모드를 사용하는 경우 `ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT` 열거형 값 대신 `ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT` 열거형 값을 지정합니다.

1. `DSC_TRANSPORT_PROTOCOL` 연결 속성을 설정하려면 `java.util.Properties` 객체의 `setProperty` 메서드를 호출하고 다음 값을 전달합니다.

   * `ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL` 열거형 값
   * `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL` 열거형 값

   >[!NOTE]
   >
   >SOAP 연결 모드를 사용하는 경우 `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL` 열거형 값 대신 `ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL`열거형 값을 지정합니다.

1. `DSC_SERVER_TYPE` 연결 속성을 설정하려면 `java.util.Properties` 객체의 `setProperty` 메서드를 호출하고 다음 값을 전달합니다.

   * `ServiceClientFactoryProperties.DSC_SERVER_TYPE`열거형 값
   * AEM Forms을 호스팅하는 J2EE 응용 프로그램 서버를 지정하는 문자열 값(예: AEM Forms이 JBoss에 배포된 경우 `JBoss` 지정).

      1. `DSC_CREDENTIAL_USERNAME` 연결 속성을 설정하려면 `java.util.Properties` 객체의 `setProperty` 메서드를 호출하고 다음 값을 전달합니다.
   * `ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME` 열거형 값
   * AEM Forms을 호출하는 데 필요한 사용자 이름을 지정하는 문자열 값

      1. `DSC_CREDENTIAL_PASSWORD` 연결 속성을 설정하려면 `java.util.Properties` 객체의 `setProperty` 메서드를 호출하고 다음 값을 전달합니다.
   * `ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD` 열거형 값
   * 해당 암호 값을 지정하는 문자열 값



**JBoss에 대한 EJB 연결 모드 설정**

다음 Java 코드 예제에서는 연결 속성을 설정하여 JBoss에 배포된 AEM Forms을 호출하고 EJB 연결 모드를 사용합니다.

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "https://<hostname>:8080");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DOCUMENT_HTTP_ENDPOINT,"https://<hostname>:8080");
```

**WebLogic용 EJB 연결 모드 설정**

다음 Java 코드 예제에서는 연결 속성을 설정하여 WebLogic에 배포된 AEM Forms을 호출하고 EJB 연결 모드를 사용합니다.

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "t3://localhost:7001");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "WebLogic");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
```

**WebSphere에 대한 EJB 연결 모드 설정**

다음 Java 코드 예제에서는 연결 속성을 설정하여 WebSphere에 배포된 AEM Forms을 호출하고 EJB 연결 모드를 사용합니다.

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "iiop://localhost:2809");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "WebSphere");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
```

**SOAP 연결 모드 설정**

다음 Java 코드 예제에서는 SOAP 모드에서 연결 속성을 설정하여 JBoss에 배포된 AEM Forms을 호출합니다.

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

**서비스 보안이 비활성화된 경우 연결 속성 설정**

다음 Java 코드 예제에서는 JBoss Application Server에 배포된 AEM Forms을 호출하는 데 필요한 연결 속성을 설정하고 서비스 보안이 비활성화된 경우를 설정합니다.

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "jnp://localhost:1099");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
```

>[!NOTE]
>
>AEM Forms을 사용한 프로그래밍과 연관된 모든 Java 빠른 시작은 EJB 및 SOAP 연결 설정을 모두 보여줍니다.

**사용자 지정 요청 시간 초과 제한으로 SOAP 연결 모드 설정**

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

`com.adobe.idp.Context` 개체를 사용하여 인증된 사용자와 AEM Forms 서비스를 호출할 수 있습니다(`com.adobe.idp.Context` 개체는 인증된 사용자를 나타냅니다.). `com.adobe.idp.Context` 개체를 사용할 때는 `DSC_CREDENTIAL_USERNAME` 또는 `DSC_CREDENTIAL_PASSWORD` 속성을 설정할 필요가 없습니다. 사용자를 인증할 때 `AuthenticationManagerServiceClient` 개체의 `authenticate` 메서드를 사용하여 `com.adobe.idp.Context` 개체를 가져올 수 있습니다.

`authenticate` 메서드는 인증 결과를 포함하는 `AuthResult` 객체를 반환합니다. 생성자를 호출하여 `com.adobe.idp.Context` 객체를 만들 수 있습니다. 그런 다음 `com.adobe.idp.Context` 객체의 `initPrincipal` 메서드를 호출하고 다음 코드와 같이 `AuthResult` 객체를 전달합니다.

```java
 Context myCtx = new Context();
 myCtx.initPrincipal(authResult);
```

`DSC_CREDENTIAL_USERNAME` 또는 `DSC_CREDENTIAL_PASSWORD` 속성을 설정하는 대신 `ServiceClientFactory` 객체의 `setContext` 메서드를 호출하고 `com.adobe.idp.Context` 객체를 전달할 수 있습니다. AEM 양식 사용자를 사용하여 서비스를 호출할 때는 AEM Forms 서비스를 호출하는 데 필요한 `Services User` 역할이 있는지 확인합니다.

다음 코드 예제에서는 `EncryptionServiceClient` 개체를 만드는 데 사용되는 연결 설정 내에서 `com.adobe.idp.Context` 개체를 사용하는 방법을 보여 줍니다.

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
>사용자 인증에 대한 자세한 내용은 [사용자 인증](/help/forms/developing/users.md#authenticating-users)을 참조하십시오.

### 시나리오 호출 {#invoking_scenarios-1}

다음 호출 시나리오에 대해서는 이 섹션에서 설명합니다.

* 자체 JVM(Java Virtual Machine)에서 실행되는 클라이언트 응용 프로그램은 독립 실행형 AEM Forms 인스턴스를 호출합니다.
* 자체 JVM에서 실행 중인 클라이언트 응용 프로그램은 클러스터된 AEM Forms 인스턴스를 호출합니다.

### 독립 실행형 AEM Forms 인스턴스 {#client-application-invoking-a-stand-alone-aem-forms-instance}를 호출하는 클라이언트 응용 프로그램

다음 다이어그램은 자체 JVM에서 실행되고 독립 실행형 AEM Forms 인스턴스를 호출하는 클라이언트 응용 프로그램을 보여 줍니다.

이 시나리오에서는 클라이언트 애플리케이션이 자체 JVM에서 실행되고 AEM Forms 서비스를 호출합니다.

>[!NOTE]
>
>이 시나리오는 모든 빠른 시작을 기반으로 하는 호출 시나리오입니다.

### 클러스터된 AEM Forms 인스턴스 {#client-application-invoking-clustered-aem-forms-instances}를 호출하는 클라이언트 응용 프로그램

다음 다이어그램은 자체 JVM에서 실행되고 클러스터에 있는 AEM Forms 인스턴스를 호출하는 클라이언트 응용 프로그램을 보여 줍니다.

이 시나리오는 독립 실행형 AEM Forms 인스턴스를 호출하는 클라이언트 응용 프로그램과 유사합니다. 그러나 공급자 URL은 다릅니다. 클라이언트 응용 프로그램이 특정 J2EE 응용 프로그램 서버에 연결하려는 경우 응용 프로그램은 특정 J2EE 응용 프로그램 서버를 참조하도록 URL을 변경해야 합니다.

응용 프로그램 서버가 중지되면 클라이언트 응용 프로그램과 AEM Forms 간의 연결이 종료되므로 특정 J2EE 응용 프로그램 서버를 참조하는 것은 권장되지 않습니다. 공급자 URL은 특정 J2EE 응용 프로그램 서버 대신 셀 수준 JNDI 관리자를 참조하는 것이 좋습니다.

SOAP 연결 모드를 사용하는 클라이언트 응용 프로그램은 클러스터에 대해 HTTP 부하 균형 조정기 포트를 사용할 수 있습니다. EJB 연결 모드를 사용하는 클라이언트 응용 프로그램은 특정 J2EE 응용 프로그램 서버의 EJB 포트에 연결할 수 있습니다. 이 작업은 클러스터 노드 간 로드 밸런싱을 처리합니다.

**WebSphere**

다음 예제는 WebSphere에 배포된 AEM Forms에 연결하는 데 사용되는 jndi.properties 파일의 컨텐츠를 보여줍니다.

```ini
 java.naming.factory.initial=com.ibm.websphere.naming.
 WsnInitialContextFactory
 java.naming.provider.url=corbaloc::appserver1:9810,:appserver2:9810
```

**WebLogic**

다음 예제는 WebLogic에 배포된 AEM Forms에 연결하는 데 사용되는 jndi.properties 파일의 컨텐츠를 보여줍니다.

```ini
 java.naming.factory.initial=weblogic.jndi.WLInitialContextFactory
 java.naming.provider.url=t3://appserver1:8001, appserver2:8001
```

**JBoss**

다음 예제는 JBoss에 배포된 AEM Forms에 연결하는 데 사용되는 jndi.properties 파일의 컨텐츠를 보여줍니다.

```ini
 java.naming.factory.initial= org.jnp.interfaces.NamingContextFactory
 java.naming.provider.url= jnp://appserver1:1099, appserver2:1099,
 appserver3:1099
```

>[!NOTE]
>
>J2EE 응용 프로그램 서버 이름과 포트 번호를 확인하려면 관리자에게 문의하십시오.

**참고 항목**

[AEM Forms Java 라이브러리 파일 포함](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Java API를 사용하여 AEM Forms 서비스로 데이터 전달](invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)

[Java 클라이언트 라이브러리를 사용하여 서비스 호출](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## Java API {#passing-data-to-aem-forms-services-using-the-java-api}를 사용하여 AEM Forms 서비스에 데이터 전달

AEM Forms 서비스 작업은 일반적으로 PDF 문서를 소비하거나 생성합니다. 서비스를 호출할 때 PDF 문서(또는 XML 데이터와 같은 기타 문서 유형)를 서비스에 전달해야 하는 경우가 있습니다. 마찬가지로 서비스에서 반환되는 PDF 문서를 처리해야 하는 경우도 있습니다. AEM Forms 서비스를 통해 데이터를 주고 받을 수 있는 Java 클래스는 `com.adobe.idp.Document`입니다.

AEM Forms 서비스는 PDF 문서를 `java.io.InputStream` 개체 또는 바이트 배열과 같은 다른 데이터 유형으로 허용하지 않습니다. 또한 `com.adobe.idp.Document` 객체를 사용하여 XML 데이터와 같은 다른 유형의 데이터를 서비스에 전달할 수도 있습니다.

`com.adobe.idp.Document` 개체는 Java 직렬화 가능 형식이므로 RMI 호출을 통해 전달할 수 있습니다. 받는 쪽의 위치는 동일한 호스트, 동일한 클래스 로더), 로컬(동일한 호스트, 다른 클래스 로더) 또는 원격(다른 호스트)일 수 있습니다. 문서 컨텐츠 전달은 각 케이스에 맞게 최적화되어 있습니다. 예를 들어, 발신자와 수신자가 동일한 호스트에 있는 경우 해당 컨텐츠는 로컬 파일 시스템을 통해 전달됩니다. (경우에 따라 문서를 메모리에 전달할 수 있습니다.)

`com.adobe.idp.Document` 개체 크기에 따라 데이터는 `com.adobe.idp.Document` 개체 내에서 전달되거나 서버의 파일 시스템에 저장됩니다. `com.adobe.idp.Document` 객체가 차지하는 모든 임시 스토리지 리소스는 `com.adobe.idp.Document` 처리 시 자동으로 제거됩니다. ([문서 개체 처리](invoking-aem-forms-using-java.md#disposing-document-objects)를 참조하십시오.)

서비스에 전달하기 전에 `com.adobe.idp.Document` 개체의 내용 유형을 알아야 하는 경우가 있습니다. 예를 들어 작업에 `application/pdf` 같은 특정 컨텐츠 유형이 필요한 경우 컨텐츠 유형을 결정하는 것이 좋습니다. (문서](invoking-aem-forms-using-java.md#determining-the-content-type-of-a-document)의 내용 유형 결정을 참조하십시오.)[

`com.adobe.idp.Document` 개체는 제공된 데이터를 사용하여 콘텐트 유형을 확인합니다. 제공된 데이터에서 내용 유형을 검색할 수 없는 경우(예: 데이터가 바이트 배열로 제공되었을 때) 내용 유형을 설정합니다. 내용 유형을 설정하려면 `com.adobe.idp.Document` 객체의 `setContentType` 메서드를 호출합니다. ([문서 내용 유형 확인](invoking-aem-forms-using-java.md#determining-the-content-type-of-a-document) 참조)

부수적 파일이 동일한 파일 시스템에 있는 경우 `com.adobe.idp.Document` 개체를 만드는 것이 더 빠릅니다. 부수적 파일이 원격 파일 시스템에 있는 경우 복사 작업을 수행해야 하므로 성능에 영향을 줍니다.

응용 프로그램에는 `com.adobe.idp.Document` 및 `org.w3c.dom.Document` 데이터 유형이 모두 포함될 수 있습니다. 그러나 `org.w3c.dom.Document` 데이터 유형의 자격을 완전히 갖추었는지 확인하십시오. `org.w3c.dom.Document` 개체를 `com.adobe.idp.Document` 개체로 변환하는 방법에 대한 자세한 내용은 [빠른 시작(EJB 모드)을 참조하십시오.Java API](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-prepopulating-forms-with-flowable-layouts-using-the-java-api)를 사용하여 Forms에 플로우 가능한 레이아웃을 미리 채웁니다.

>[!NOTE]
>
>`com.adobe.idp.Document` 개체를 사용하는 동안 WebLogic에서 메모리 누수를 방지하려면 2048바이트 이하의 청크(chunk)로 문서 정보를 읽으십시오. 예를 들어 다음 코드는 2048바이트 단위로 문서 정보를 읽습니다.

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

**참고 항목**

[Java API를 사용하여 AEM Forms 호출](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[연결 속성 설정](invoking-aem-forms-using-java.md#setting-connection-properties)

### 문서 만들기 {#creating-documents}

PDF 문서(또는 다른 문서 유형)를 입력 값으로 필요로 하는 서비스 작업을 호출하기 전에 `com.adobe.idp.Document` 객체를 만듭니다. `com.adobe.idp.Document` 클래스는 다음과 같은 내용 형식에서 문서를 만들 수 있는 생성자를 제공합니다.

* 바이트 배열
* 기존 `com.adobe.idp.Document` 개체
* `java.io.File` 개체
* `java.io.InputStream` 개체
* `java.net.URL` 개체

#### 바이트 배열 {#creating-a-document-based-on-a-byte-array}을 기반으로 문서 만들기

다음 코드 예제에서는 바이트 배열을 기반으로 하는 `com.adobe.idp.Document` 객체를 만듭니다.

**바이트 배열을 기반으로 하는 Document 객체 만들기**

```java
 Document myPDFDocument = new Document(myByteArray);
```

#### 다른 문서 {#creating-a-document-based-on-another-document} 기반 문서 만들기

다음 코드 예제에서는 다른 `com.adobe.idp.Document` 객체를 기반으로 하는 `com.adobe.idp.Document` 객체를 만듭니다.

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

#### {#creating-a-document-based-on-a-file} 파일을 기반으로 문서 만들기

다음 코드 예제에서는 *map.pdf*&#x200B;라는 PDF 파일을 기반으로 하는 `com.adobe.idp.Document` 개체를 만듭니다. 이 파일은 C 하드 드라이브의 루트에 있습니다. 이 생성자는 파일 이름 확장명을 사용하여 `com.adobe.idp.Document` 개체의 MIME 콘텐츠 형식을 설정하려고 합니다.

`java.io.File` 객체를 허용하는 `com.adobe.idp.Document` 생성자도 부울 매개 변수를 사용합니다. 이 매개 변수를 `true`으로 설정하면 `com.adobe.idp.Document` 객체가 파일을 삭제합니다. 이 작업은 파일을 `com.adobe.idp.Document` 생성자에 전달한 후 파일을 제거할 필요가 없음을 의미합니다.

이 매개 변수를 `false`으로 설정하면 이 파일의 소유권이 유지됨을 의미합니다. 이 매개 변수를 `true`으로 설정하는 것이 더 효율적입니다. 이유는 `com.adobe.idp.Document` 객체가 파일을 복사하는 대신 로컬 관리 영역으로 직접 이동할 수 있기 때문입니다(속도가 느림).

**PDF 파일을 기반으로 하는 문서 객체 만들기**

```java
 //Create a Document object based on the map.pdf source file
 File mySourceMap = new File("C:\\map.pdf");
 Document myPDFDocument = new Document(mySourceMap,true);
```

#### InputStream 객체 {#creating-a-document-based-on-an-inputstream-object} 기반 문서 만들기

다음 Java 코드 예제에서는 `java.io.InputStream` 객체를 기반으로 하는 `com.adobe.idp.Document` 객체를 만듭니다.

**InputStream 객체를 기반으로 문서 만들기**

```java
 //Create a Document object based on an InputStream object
 InputStream is = new FileInputStream("C:\\Map.pdf");
 Document myPDFDocument = new Document(is);
```

#### URL {#creating-a-document-based-on-content-accessible-from-an-url}에서 액세스할 수 있는 내용을 기반으로 문서 만들기

다음 Java 코드 예제에서는 *map.pdf*&#x200B;라는 PDF 파일을 기반으로 하는 `com.adobe.idp.Document` 개체를 만듭니다. 이 파일은 `localhost`에서 실행 중인 `WebApp` 웹 응용 프로그램 내에 있습니다. 이 생성자는 URL 프로토콜과 함께 반환된 내용 유형을 사용하여 `com.adobe.idp.Document` 객체의 MIME 내용 유형을 설정하려고 합니다.

다음 예제와 같이 `com.adobe.idp.Document` 개체에 제공된 URL은 항상 원래 `com.adobe.idp.Document` 개체가 만들어진 곳에서 읽습니다.

```java
     Document doc = new Document(new java.net.URL("file:c:/temp/input.pdf"));
```

c:/temp/input.pdf 파일은 서버 컴퓨터가 아닌 클라이언트 컴퓨터에 있어야 합니다. 클라이언트 컴퓨터는 URL을 읽는 곳이고 `com.adobe.idp.Document` 개체가 만들어진 곳입니다.

**URL에서 액세스할 수 있는 내용을 기반으로 문서 만들기**

```java
 //Create a Document object based on a java.net.URL object
 URL myURL = new URL("http", "localhost", 8080,"/WebApp/map.pdf");
 
 //Create another Document object
 Document myPDFDocument = new Document(myURL);
```

**참고 항목**

[Java API를 사용하여 AEM Forms 호출](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[연결 속성 설정](invoking-aem-forms-using-java.md#setting-connection-properties)

### 반환된 문서 처리 {#handling-returned-documents}

출력 값으로 PDF 문서(또는 XML 데이터와 같은 기타 데이터 유형)를 반환하는 서비스 작업에서는 `com.adobe.idp.Document` 객체를 반환합니다. `com.adobe.idp.Document` 개체를 받은 후 다음 형식으로 변환할 수 있습니다.

* `java.io.File` 개체
* `java.io.InputStream` 개체
* 바이트 배열

다음 코드 행은 `com.adobe.idp.Document` 객체를 `java.io.InputStream` 객체로 변환합니다. `myPDFDocument`은 `com.adobe.idp.Document` 개체를 나타낸다고 가정합니다.

```java
     java.io.InputStream resultStream = myDocument.getInputStream();
```

마찬가지로 다음 작업을 수행하여 `com.adobe.idp.Document`의 내용을 로컬 파일에 복사할 수 있습니다.

1. `java.io.File` 개체를 만듭니다.
1. `com.adobe.idp.Document` 개체의 `copyToFile` 메서드를 호출하고 `java.io.File` 개체를 전달합니다.

다음 코드 예제에서는 `com.adobe.idp.Document` 개체의 내용을 *AnotherMap.pdf* 파일에 복사합니다.

**문서 객체의 내용을 파일에 복사**

```java
 File outFile = new File("C:\\AnotherMap.pdf");
 myDocument.copyToFile (outFile);
```

**참고 항목**

[Java API를 사용하여 AEM Forms 호출](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[연결 속성 설정](invoking-aem-forms-using-java.md#setting-connection-properties)

### 문서 {#determining-the-content-type-of-a-document}의 내용 유형 결정

`com.adobe.idp.Document` 객체의 `getContentType` 메서드를 호출하여 `com.adobe.idp.Document` 객체의 MIME 유형을 결정합니다. 이 메서드는 `com.adobe.idp.Document` 객체의 내용 유형을 지정하는 문자열 값을 반환합니다. 다음 표에서는 AEM Forms이 반환하는 다양한 컨텐츠 유형에 대해 설명합니다.

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
   <td><p>내보낸 XFA(XML Forms Architecture) 양식에 사용되는 XDP(XML Data Packaging)</p></td>
  </tr>
  <tr>
   <td><p><code>text/xml</code></p></td>
   <td><p>책갈피, 첨부 파일 또는 기타 XML 문서</p></td>
  </tr>
  <tr>
   <td><p><code>application/vnd.fdf</code></p></td>
   <td><p>Acrobat 양식을 내보내는 데 사용되는 Forms FDF(Data Format)</p></td>
  </tr>
  <tr>
   <td><p><code>application/vnd.adobe.xfdf</code></p></td>
   <td><p>Acrobat 양식을 내보내는 데 사용되는 XFDF(XML Forms Data Format)</p></td>
  </tr>
  <tr>
   <td><p><code>application/rdf+xml</code></p></td>
   <td><p>풍부한 데이터 포맷 및 XML</p></td>
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

다음 코드 예제에서는 `com.adobe.idp.Document` 객체의 내용 유형을 결정합니다.

**Document 객체의 내용 유형 결정**

```java
 //Determine the content type of the Document object
 String ct = myDocument.getContentType();
 System.out.println("The content type of the Document object is " +ct);
```

**참고 항목**

[Java API를 사용하여 AEM Forms 호출](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[연결 속성 설정](invoking-aem-forms-using-java.md#setting-connection-properties)

### 문서 객체 삭제 {#disposing-document-objects}

더 이상 `Document` 개체가 필요하지 않은 경우 `dispose` 메서드를 호출하여 해당 객체를 처리하는 것이 좋습니다. 각 `Document` 개체는 응용 프로그램의 호스트 플랫폼에서 파일 설명자와 최대 75MB의 RAM 공간을 사용합니다. `Document` 객체가 처리되지 않으면 Java Garage 컬렉션 프로세스에서 객체를 삭제합니다. 그러나 `dispose` 메서드를 사용하여 더 빨리 처리하면 `Document` 객체에 사용된 메모리를 해제할 수 있습니다.

**참고 항목**

[Java API를 사용하여 AEM Forms 호출](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Java 클라이언트 라이브러리를 사용하여 서비스 호출](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## Java 클라이언트 라이브러리 {#invoking-a-service-using-a-java-client-library}를 사용하여 서비스 호출

AEM Forms 서비스 작업은 Java 클라이언트 라이브러리라는 강력한 형식의 서비스의 API를 사용하여 호출할 수 있습니다. *Java 클라이언트 라이브러리*&#x200B;는 서비스 컨테이너에 배포된 서비스에 대한 액세스를 제공하는 구체적인 클래스 세트입니다. 호출 API를 사용하여 `InvocationRequest` 객체를 만드는 대신 호출할 서비스를 나타내는 Java 객체를 인스턴스화합니다. 호출 API는 Workbench에서 만든 장기 처리 프로세스와 같은 프로세스를 호출하는 데 사용됩니다. ([인간 중심의 긴 수명 프로세스 호출](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes) 참조)

서비스 작업을 수행하려면 Java 객체에 속하는 메서드를 호출합니다. Java 클라이언트 라이브러리에는 일반적으로 서비스 작업과 일대일로 매핑되는 메서드가 포함되어 있습니다. Java 클라이언트 라이브러리를 사용할 때는 필수 연결 속성을 설정합니다. ([연결 속성 설정](invoking-aem-forms-using-java.md#setting-connection-properties)을 참조하십시오.)

연결 속성을 설정한 후 서비스를 호출할 수 있는 Java 객체를 인스턴스화하는 데 사용되는 `ServiceClientFactory` 객체를 만듭니다. Java 클라이언트 라이브러리가 있는 각 서비스에는 해당 클라이언트 개체가 있습니다. 예를 들어 저장소 서비스를 호출하려면 해당 생성자를 사용하여 `ResourceRepositoryClient` 개체를 만들고 `ServiceClientFactory` 개체를 전달합니다. `ServiceClientFactory` 개체는 AEM Forms 서비스를 호출하는 데 필요한 연결 설정을 유지 관리하는 책임이 있습니다.

일반적으로 `ServiceClientFactory`을(를) 얻는 것이 빠르지만, 팩터리를 처음 사용할 때 일부 오버헤드가 발생합니다. 이 개체는 재사용을 위해 최적화되므로, 가능한 경우 여러 Java 클라이언트 개체를 만들 때 동일한 `ServiceClientFactory` 개체를 사용합니다. 즉, 사용자가 만드는 각 클라이언트 라이브러리 개체에 대해 별도의 `ServiceClientFactory` 개체를 만들지 마십시오.

`ServiceClientFactory` 개체에 영향을 주는 `com.adobe.idp.Context` 개체 내에 있는 SAML 어설션의 수명을 제어하는 사용자 관리자 설정이 있습니다. 이 설정은 Java API를 사용하여 수행한 모든 호출을 비롯하여 AEM Forms 전체의 모든 인증 컨텍스트 라이프타임을 제어합니다. 기본적으로 `ServiceCleintFactory` 개체를 사용할 수 있는 기간은 2시간입니다.

>[!NOTE]
>
>Java API를 사용하여 서비스를 호출하는 방법을 설명하는 경우 저장소 서비스의 `writeResource` 작업이 호출됩니다. 이 작업을 수행하면 새 리소스가 저장소에 배치됩니다.

Java 클라이언트 라이브러리를 사용하고 다음 단계를 수행하여 저장소 서비스를 호출할 수 있습니다.

1. Java 프로젝트의 클래스 경로에 adobe-repository-client.jar와 같은 클라이언트 JAR 파일을 포함합니다. 이러한 파일의 위치에 대한 자세한 내용은 [AEM Forms Java 라이브러리 파일 포함](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)을 참조하십시오.
1. 서비스를 호출하는 데 필요한 연결 속성을 설정합니다.
1. `ServiceClientFactory` 객체의 정적 `createInstance` 메서드를 호출하고 연결 속성이 포함된 `java.util.Properties` 객체를 전달하여 `ServiceClientFactory` 객체를 만듭니다.
1. 생성자를 사용하여 `ResourceRepositoryClient` 개체를 만들고 `ServiceClientFactory` 개체를 전달합니다. `ResourceRepositoryClient` 개체를 사용하여 저장소 서비스 작업을 호출합니다.
1. 생성자를 사용하여 `RepositoryInfomodelFactoryBean` 개체를 만들고 `null`을 전달합니다. 이 객체를 사용하면 저장소에 추가되는 컨텐츠를 나타내는 `Resource` 객체를 만들 수 있습니다.
1. `RepositoryInfomodelFactoryBean` 객체의 `newImage` 메서드를 호출하고 다음 값을 전달하여 `Resource` 객체를 만듭니다.

   * `new Id()`을(를) 지정하여 고유한 ID 값입니다.
   * `new Lid()`을(를) 지정하여 고유한 UUID 값입니다.
   * 리소스의 이름입니다. XDP 파일의 파일 이름을 지정할 수 있습니다.

   반환 값을 `Resource`으로 캐스팅합니다.

1. `RepositoryInfomodelFactoryBean` 객체의 `newImage` 메서드를 호출하고 반환 값을 `ResourceContent`으로 변환하여 `ResourceContent` 개체를 만듭니다. 이 객체는 저장소에 추가되는 컨텐츠를 나타냅니다.
1. 저장소에 추가할 XDP 파일을 저장하는 `java.io.FileInputStream` 개체를 전달하여 `com.adobe.idp.Document` 개체를 만듭니다. 자세한 내용은 [InputStream 객체](invoking-aem-forms-using-java.md#creating-a-document-based-on-an-inputstream-object)를 기반으로 문서 만들기를 참조하십시오.
1. `ResourceContent` 객체의 `setDataDocument` 메서드를 호출하여 `com.adobe.idp.Document` 객체의 내용을 `ResourceContent` 객체에 추가합니다. `com.adobe.idp.Document` 개체를 전달합니다.
1. `ResourceContent` 객체의 `setMimeType` 메서드를 호출하고 `application/vnd.adobe.xdp+xml`를 전달하여 저장소에 추가할 XDP 파일의 MIME 유형을 설정합니다.
1. `Resource` 개체 &#39;s `setContent` 메서드를 호출하고 `ResourceContent` 개체를 전달하여 `ResourceContent` 개체의 내용을 `Resource` 개체에 추가합니다.
1. `Resource` 개체 &#39;s `setDescription` 메서드를 호출하고 리소스의 설명을 나타내는 문자열 값을 전달하여 리소스에 대한 설명을 추가합니다.
1. `ResourceRepositoryClient` 객체의 `writeResource` 메서드를 호출하고 다음 값을 전달하여 양식 디자인을 저장소에 추가합니다.

   * 새 리소스를 포함하는 리소스 컬렉션의 경로를 지정하는 문자열 값
   * 만든 `Resource` 개체

**참고 항목**

[빠른 시작(EJB 모드):Java API를 사용하여 리소스 쓰기](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)

[Java API를 사용하여 AEM Forms 호출](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

## 호출 API {#invoking-a-short-lived-process-using-the-invocation-api}를 사용하여 짧은 기간 프로세스 호출

Java 호출 API를 사용하여 단기 프로세스를 호출할 수 있습니다. 호출 API를 사용하여 단기 프로세스를 호출할 때 `java.util.HashMap` 객체를 사용하여 필수 매개 변수 값을 전달합니다. 각 매개 변수가 서비스로 전달되도록 하려면 `java.util.HashMap` 객체의 `put` 메서드를 호출하고 지정된 작업을 수행하기 위해 서비스에 필요한 이름-값 쌍을 지정합니다. 단기 프로세스에 속하는 매개 변수의 정확한 이름을 지정합니다.

>[!NOTE]
>
>오래 지속되는 프로세스 호출에 대한 자세한 내용은 [인간 중심의 긴 수명 프로세스 호출](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)을 참조하십시오.

여기서 논의되는 내용은 호출 API를 사용하여 `MyApplication/EncryptDocument`이라는 AEM Forms의 단기 프로세스를 호출하는 것입니다.

>[!NOTE]
>
>이 프로세스는 기존 AEM Forms 프로세스를 기반으로 하지 않습니다. 코드 예제를 따라 하려면 Workbench를 사용하여 `MyApplication/EncryptDocument` 프로세스를 만듭니다. ([Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63) 사용 참조)

이 프로세스가 호출되면 다음 작업을 수행합니다.

1. 프로세스에 전달된 보안되지 않은 PDF 문서를 가져옵니다. 이 작업은 `SetValue` 작업을 기반으로 합니다. 이 프로세스의 입력 매개 변수는 `inDoc`이라는 `document` 프로세스 변수입니다.
1. 암호로 PDF 문서를 암호화합니다. 이 작업은 `PasswordEncryptPDF` 작업을 기반으로 합니다. 암호로 암호화된 PDF 문서는 `outDoc` 프로세스 변수에 반환됩니다.

### Java 호출 API {#invoke-the-myapplication-encryptdocument-short-lived-process-using-the-java-invocation-api}를 사용하여 MyApplication/EncryptDocument가 짧은 기간 프로세스를 호출합니다.

Java 호출 API를 사용하여 `MyApplication/EncryptDocument` 단기 프로세스를 호출합니다.

1. Java 프로젝트의 클래스 경로에 adobe-livecycle-client.jar 등의 클라이언트 JAR 파일을 포함합니다. ([AEM Forms Java 라이브러리 파일 포함](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files) 참조)
1. 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다. ([연결 속성 설정](invoking-aem-forms-using-java.md#setting-connection-properties)을 참조하십시오.)
1. 생성자를 사용하여 `ServiceClient` 개체를 만들고 `ServiceClientFactory` 개체를 전달합니다. `ServiceClient` 객체를 사용하면 서비스 작업을 호출할 수 있습니다. 호출 요청 찾기, 전달 및 라우팅 등의 작업을 처리합니다.
1. 생성자를 사용하여 `java.util.HashMap` 객체를 만듭니다.
1. 각 입력 매개 변수에 대해 `java.util.HashMap` 객체의 `put` 메서드를 호출하여 오래 지속되는 프로세스로 전달합니다. `MyApplication/EncryptDocument` 단기 프로세스 시 `Document` 유형의 입력 매개 변수가 하나만 필요하므로 다음 예제와 같이 `put` 메서드를 한 번만 호출하면 됩니다.

   ```java
    //Create a Map object to store the parameter value for inDoc
    Map params = new HashMap();
    InputStream inFile = new FileInputStream("C:\\Adobe\Loan.pdf");
    Document inDoc = new Document(inFile);
    params.put("inDoc", inDoc);
   ```

1. `ServiceClientFactory` 객체의 `createInvocationRequest` 메서드를 호출하고 다음 값을 전달하여 `InvocationRequest` 객체를 만듭니다.

   * 호출할 긴 기간의 프로세스 이름을 지정하는 문자열 값입니다. `MyApplication/EncryptDocument` 프로세스를 호출하려면 `MyApplication/EncryptDocument`을 지정합니다.
   * 프로세스 작업 이름을 나타내는 문자열 값입니다. 일반적으로 짧은 프로세스 작업의 이름은 `invoke`입니다.
   * 서비스 작업에 필요한 매개 변수 값을 포함하는 `java.util.HashMap` 객체입니다.
   * 동기 요청을 만드는 `true`을 지정하는 부울 값(이 값은 단기 프로세스를 호출하는 데 적용 가능)

1. `ServiceClient` 개체의 `invoke` 메서드를 호출하고 `InvocationRequest` 개체를 전달하여 호출 요청을 서비스로 보냅니다. `invoke` 메서드는 `InvocationReponse` 객체를 반환합니다.

   >[!NOTE]
   >
   >`createInvocationRequest` 메서드의 네 번째 매개 변수로 `false`이라는 값을 전달하여 긴 프로세스를 호출할 수 있습니다. `false`*값을 전달하면 비동기 요청이 만들어집니다.*

1. `InvocationReponse` 객체의 `getOutputParameter` 메서드를 호출하고 출력 매개 변수의 이름을 지정하는 문자열 값을 전달하여 프로세스의 반환 값을 검색합니다. 이러한 경우 `outDoc`(`outDoc`은 `MyApplication/EncryptDocument` 프로세스에 대한 출력 매개 변수의 이름입니다). 다음 예와 같이 반환 값을 `Document`으로 캐스팅합니다.

   ```java
    InvocationResponse response = myServiceClient.invoke(request);
    Document encryptDoc = (Document) response.getOutputParameter("outDoc");
   ```

1. `java.io.File` 개체를 만들고 파일 확장자가 .pdf인지 확인합니다.
1. `com.adobe.idp.Document` 객체의 `copyToFile` 메서드를 호출하여 `com.adobe.idp.Document` 객체의 내용을 파일에 복사합니다. `getOutputParameter` 메서드에서 반환된 `com.adobe.idp.Document` 개체를 사용해야 합니다.

**참고 항목**

[빠른 시작:호출 API를 사용하여 짧은 기간 프로세스 호출](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-short-lived-process-using-the-invocation-api)

[인간 중심의 오랜 프로세스 호출](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)

[AEM Forms Java 라이브러리 파일 포함](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)