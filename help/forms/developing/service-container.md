---
title: 서비스 컨테이너
seo-title: 서비스 컨테이너
description: 서비스 컨테이너에 있는 AEM Forms 서비스
uuid: 89f2fd3d-63d7-4b70-b335-47314441f3ec
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding, development-tools
discoiquuid: dd9c0ec4-a195-4b78-8992-81d0efcc0a7e
translation-type: tm+mt
source-git-commit: a873cf3e7efd3bc9cd4744bf09078d9040efcdda
workflow-type: tm+mt
source-wordcount: '915'
ht-degree: 0%

---


# 서비스 컨테이너 {#service-container}

서비스 컨테이너에 있는 AEM Forms 서비스(암호화 서비스, 장기 및 단기 프로세스 등 표준 서비스 포함)는 EJB 공급자와 같은 다양한 공급자를 사용하여 호출할 수 있습니다. EJB 공급자를 사용하면 AEM Forms 서비스를 RMI/IOP을 통해 호출할 수 있습니다. 웹 서비스 제공자는 SOAP/HTTP 및 SOAP/JMS와 같은 표준을 사용하여 서비스를 웹 서비스(WSDL 생성)로 노출합니다.

다음 표에서는 AEM Forms 서비스를 프로그래밍 방식으로 호출할 수 있는 다양한 방법에 대해 설명합니다.

<table>
 <thead>
  <tr>
   <th><p>호출 메서드</p></th>
   <th><p>설명</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>원격 통합</p></td>
   <td><p>원격 통합은 Flex 클라이언트가 서비스 작업을 호출하는 기능을 제공합니다. (자세한 내용은 <a href="/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting">AEM Forms 호출 사용(AEM 양식에서 더 이상 사용되지 않음) AEM Forms Remoting</a>을 참조하십시오.)</p></td>
  </tr>
  <tr>
   <td><p>Java API</p></td>
   <td><p>Java API는 AEM Forms 서비스를 호출할 수 있습니다. Java API는 클라이언트 라이브러리와 Java 호출 API로 구성됩니다. (Java API<a href="/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api">를 사용하여 AEM Forms 호출 참조)</a></p></td>
  </tr>
  <tr>
   <td><p>웹 서비스</p></td>
   <td><p>AEM Forms은 SOAP/HTTP와 같은 웹 서비스 표준을 지원합니다. 서비스는 W3C에서 정의한 웹 서비스 표준을 준수하는 WSDL을 사용하여 웹 서비스로 노출될 수 있습니다.</p><p>서비스는 .NET Framework 및 Sun™ Web Services SDK를 비롯한 모든 웹 서비스 스택에서 호출할 수 있습니다. (<a href="/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services">웹 서비스를 사용하여 AEM Forms 호출</a>을 참조하십시오.)</p></td>
  </tr>
  <tr>
   <td><p>REST 요청</p></td>
   <td><p>AEM Forms은 REST 요청을 지원합니다. 서비스는 HTML 페이지에서 직접 호출할 수 있습니다. (REST 요청을 사용하여 AEM Forms 호출<a href="/help/forms/developing/invoking-aem-forms-using-rest.md#invoking-aem-forms-using-rest-requests">을 참조하십시오.)</a></p></td>
  </tr>
 </tbody>
</table>

다음 그림은 프로그래밍 방식으로 AEM Forms 서비스를 호출할 수 있는 다양한 방법을 시각적으로 보여줍니다.

>[!NOTE]
>
>AEM Forms SDK를 사용하여 AEM Forms 서비스를 호출할 수 있는 클라이언트 애플리케이션을 만드는 것 외에도, 서비스 컨테이너에 배포할 수 있는 구성 요소를 만들 수도 있습니다. 예를 들어 프로세스에서 사용할 수 있는 사용자 지정 데이터 유형을 포함하는 은행 구성 요소를 만들 수 있습니다. 즉, `com.adobe.idp.BankAccount`과 같은 데이터 유형을 만들 수 있습니다. 그런 다음 클라이언트 응용 프로그램에서 `com.adobe.idp.BankAccount` 인스턴스를 만들 수 있습니다.

서비스 컨테이너는 다음 기능을 제공합니다.

* 다른 방법을 사용하여 AEM Forms 서비스를 호출할 수 있습니다. 모든 메서드를 사용하여 호출할 수 있도록 끝점을 설정하여 서비스를 구성할 수 있습니다.Java API, 웹 서비스 및 REST의 Remoting. 자세한 내용은 [프로그래밍 방식으로 끝점 관리](/help/forms/developing/programmatically-endpoints.md#programmatically-managing-endpoints)를 참조하십시오.
* 메시지를 호출 요청이라는 정규화된 형식으로 변환합니다. 호출 요청이 클라이언트 응용 프로그램(또는 다른 서비스)에서 서비스 컨테이너에 있는 서비스로 전송됩니다. 호출 요청에는 호출할 서비스 이름 및 작업을 수행하는 데 필요한 데이터 값과 같은 정보가 포함됩니다. 많은 서비스가 작업을 수행하려면 문서를 필요로 합니다. 따라서 호출 요청에는 일반적으로 PDF 데이터, XDP 데이터, XML 데이터 등의 문서를 포함합니다.
* 호출 요청을 적절한 서비스로 라우팅합니다(호출할 서비스 이름은 호출 요청의 일부임).
* 호출자에게 지정된 서비스 작업을 호출할 수 있는 권한이 있는지 여부를 확인하는 등의 작업을 수행합니다. 호출 요청에는 유효한 AEM 양식 사용자 이름과 암호가 포함되어야 합니다.

   서비스로 호출 요청을 보내는 방법은 다양합니다. 또한 필요한 입력 값을 서비스로 보내는 다른 방법도 있습니다. 예를 들어 Java API를 사용하여 PDF 문서가 필요한 서비스를 호출한다고 가정합니다. 해당 Java 메서드에는 PDF 문서를 허용하는 매개 변수가 포함되어 있습니다. 이 경우 매개 변수의 데이터 유형은 `com.adobe.idp.Document`입니다. (Java API[를 사용하여 AEM Forms 서비스에 데이터 전달을 참조하십시오.)](/help/forms/developing/invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)

   감시 폴더를 사용하여 서비스를 호출하면 구성된 감시 폴더에 파일을 배치할 때 호출 요청이 전송됩니다. 이메일을 사용하여 서비스를 호출하면 이메일 메시지가 구성된 받은 편지함에 도착할 때 호출 요청이 서비스로 전송됩니다.

   작업이 수행되면 서비스 컨테이너는 호출 응답을 다시 전송합니다. 호출 응답에는 작업 결과와 같은 정보가 포함됩니다. 예를 들어, 작업이 PDF 문서를 수정하는 경우 호출 응답에 수정된 PDF 문서가 포함됩니다. 작업이 실패할 경우 호출 응답에 오류 메시지가 포함됩니다.

   호출 요청을 보내는 것과 같은 방식으로 호출 응답을 검색할 수 있습니다. 즉, Java API를 사용하여 호출 요청을 전송하는 경우 Java API를 사용하여 호출 응답을 검색할 수 있습니다. 예를 들어 작업이 PDF 문서를 수정한다고 가정합니다. 서비스를 호출한 Java 메서드의 반환 값을 가져와 수정된 PDF 문서를 검색할 수 있습니다.

   긴 수명 프로세스가 호출되면 호출 응답에는 호출 요청과 연결된 식별자 값이 포함됩니다. 이 식별자 값을 사용하여 나중에 프로세스의 상태를 확인할 수 있습니다. 예를 들어 MortgageLoan의 장기간 서비스를 고려할 수 있습니다. 식별자 값을 사용하여 프로세스가 성공적으로 완료되었는지 확인할 수 있습니다. ([인간 중심의 긴 수명 프로세스 호출](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes) 참조)

   다음 다이어그램은 서비스를 호출하는 클라이언트 응용 프로그램(Java API를 사용)을 보여 줍니다.

   클라이언트 응용 프로그램이 서비스를 호출하면 3개의 이벤트가 발생합니다.

   1. 클라이언트 응용 프로그램이 서비스에 호출 요청을 보냅니다.
   1. 서비스는 호출 요청에 지정된 작업을 수행합니다.
   1. 서비스 컨테이너는 클라이언트 응용 프로그램에 대한 호출 응답을 반환합니다.

**참고 항목**

[AEM Forms 프로세스 이해](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes)

[AEM Forms Remoting을 사용하여 AEM Forms 호출(AEM 양식에 대해 더 이상 사용되지 않음)](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[Java API를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[웹 서비스를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services)

[인간 중심의 오랜 프로세스 호출](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)

[REST 요청을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-rest.md#invoking-aem-forms-using-rest-requests)
