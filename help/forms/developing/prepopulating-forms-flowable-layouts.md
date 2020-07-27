---
title: 순서형 레이아웃으로 양식 미리 채우기
seo-title: 순서형 레이아웃으로 양식 미리 채우기
description: 'null'
seo-description: 'null'
uuid: 93ccb496-e1c2-4b79-8e89-7a2abfce1537
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 30a12fc6-07b8-4c7c-b9e2-caa2bec0ac48
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '3489'
ht-degree: 0%

---


# 순서형 레이아웃으로 양식 미리 채우기 {#prepopulating-forms-with-flowable-layouts1}

## 순서형 레이아웃으로 양식 미리 채우기 {#prepopulating-forms-with-flowable-layouts2}

양식을 미리 채우면 렌더링된 양식 내의 사용자에게 데이터가 표시됩니다. 예를 들어 사용자가 사용자 이름과 암호를 사용하여 웹 사이트에 로그인한다고 가정합니다. 인증이 성공적으로 완료되면 클라이언트 응용 프로그램은 데이터베이스에 사용자 정보를 쿼리합니다. 데이터가 양식에 병합된 후 양식이 사용자에게 렌더링됩니다. 따라서 사용자는 양식 내에서 개인화된 데이터를 볼 수 있습니다.

양식을 미리 채울 때 다음과 같은 이점이 있습니다.

* 사용자가 양식에서 사용자 지정 데이터를 볼 수 있도록 해줍니다.
* 사용자가 양식을 채우도록 입력하는 횟수를 줄입니다.
* 데이터 배치 위치를 제어하여 데이터 무결성을 보장합니다.

다음 두 개의 XML 데이터 소스가 양식을 채울 수 있습니다.

* XFA 구문을 준수하는 XML인 XDP 데이터 소스(또는 XFDF 데이터를 사용하여 만든 양식을 미리 채울 수 있음)
* 양식의 필드 이름과 일치하는 이름/값 쌍을 포함하는 임의 XML 데이터 소스(이 섹션의 예는 임의의 XML 데이터 소스를 사용).

미리 채울 모든 양식 필드에 대해 XML 요소가 있어야 합니다. XML 요소 이름은 필드 이름과 일치해야 합니다. XML 요소는 양식 필드에 해당되지 않거나 XML 요소 이름이 필드 이름과 일치하지 않는 경우 무시됩니다. 모든 XML 요소가 지정된 한 XML 요소가 표시되는 순서와 일치할 필요는 없습니다.

이미 데이터가 포함된 양식을 채울 때는 XML 데이터 소스 내에 이미 표시된 데이터를 지정해야 합니다. 필드가 10개인 양식에 데이터가 4개 필드에 있다고 가정합니다. 그런 다음 나머지 6개 필드를 미리 채우려고 한다고 가정합니다. 이 경우 양식을 채울 때 사용되는 XML 데이터 소스에 10개의 XML 요소를 지정해야 합니다. 6개의 요소만 지정하면 원래 4개의 필드가 비어 있습니다.

예를 들어 샘플 확인 양식과 같은 양식을 미리 채울 수 있습니다. (대화형 PDF forms 렌더링의 &quot; [확인 양식&quot;을 참조하십시오](/help/forms/developing/rendering-interactive-pdf-forms.md).)

샘플 확인 양식을 미리 채우려면 양식의 세 필드와 일치하는 3개의 XML 요소가 포함된 XML 데이터 소스를 만들어야 합니다. 이 양식에는 다음 세 개의 필드가 포함되어 있습니다. `FirstName`, `LastName`and `Amount`. 첫 번째 단계는 양식 디자인에 있는 필드와 일치하는 XML 요소를 포함하는 XML 데이터 소스를 만드는 것입니다. 다음 단계는 다음 XML 코드와 같이 XML 요소에 데이터 값을 할당하는 것입니다.

```xml
     <Untitled>
         <FirstName>Jerry</FirstName>
         <LastName>Johnson</LastName>
         <Amount>250000</Amount>
     </Untitled>
```

확인 양식을 이 XML 데이터 소스로 미리 채우고 양식을 렌더링하면 다음 다이어그램과 같이 XML 요소에 할당한 데이터 값이 표시됩니다.

![pf_pf_confirmxml3](assets/pf_pf_confirmxml3.png)

### 순서별 레이아웃으로 양식 미리 채우기 {#prepopulating_forms_with_flowable_layouts-1}

순서도 가능한 레이아웃이 있는 양식은 사용자에게 확인되지 않은 양의 데이터를 표시하는 데 유용합니다. 양식의 레이아웃은 병합된 데이터의 양에 따라 자동으로 조정되므로 고정 레이아웃이 있는 양식의 경우 필요한 만큼 양식의 고정 레이아웃이나 페이지 수를 미리 확인하지 않아도 됩니다.

일반적으로 양식은 런타임 동안 얻은 데이터로 채워집니다. 따라서 메모리 내 XML 데이터 소스를 만들고 데이터를 메모리 내 XML 데이터 소스에 직접 배치하여 양식을 미리 채울 수 있습니다.

온라인 스토어와 같은 웹 기반 애플리케이션을 고려해 보십시오. 온라인 구매자가 항목 구입을 마치면 구입한 모든 항목이 양식을 미리 채우는 데 사용되는 메모리 내 XML 데이터 소스에 배치됩니다. 다음 다이어그램은 이 프로세스를 보여 줍니다. 이 프로세스는 다이어그램 아래의 표에 설명되어 있습니다.

![pf_findsrv_webapp_v1](assets/pf_pf_finsrv_webapp_v1.png)

다음 표에서는 이 다이어그램의 단계를 설명합니다.

<table>
 <thead>
  <tr>
   <th><p>단계</p></th>
   <th><p>설명</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>사용자가 웹 기반 온라인 스토어에서 항목을 구매합니다. </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>사용자가 항목 구입을 마치고 [전송] 단추를 클릭하면 메모리 내 XML 데이터 소스가 생성됩니다. 구입한 항목 및 사용자 정보는 메모리 내 XML 데이터 소스에 배치됩니다. </p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>XML 데이터 소스는 구매 발주 양식을 미리 채우는 데 사용됩니다(이 양식의 예는 이 표 다음에 표시됨). </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>구매 주문서 양식이 클라이언트 웹 브라우저에 렌더링됩니다. </p></td>
  </tr>
 </tbody>
</table>

다음 다이어그램은 구매 발주 양식의 예를 보여줍니다. 테이블의 정보는 XML 데이터의 레코드 수에 맞게 조정할 수 있습니다.

![pf_pdf](assets/pf_pf_poform.png)

>[!NOTE]
>
>기업 데이터베이스 또는 외부 애플리케이션과 같은 다른 소스의 데이터로 양식을 미리 채울 수 있습니다.

### 양식 디자인 고려 사항 {#form-design-considerations}

레이아웃이 포함된 양식은 Designer에서 만든 양식 디자인을 기반으로 합니다. 양식 디자인에서는 사용자 입력을 기반으로 값을 계산하는 것을 포함하여 레이아웃, 프레젠테이션 및 데이터 캡처 규칙 세트를 지정합니다. 데이터를 양식에 입력할 때 규칙이 적용됩니다. 양식에 추가되는 필드는 양식 디자인 내에 있는 하위 양식입니다. 예를 들어 이전 다이어그램에 표시된 구매 주문서 양식에서는 각 라인은 하위 폼입니다. 하위 양식이 포함된 양식 디자인 만들기에 대한 자세한 내용은 플로우 가능한 레이아웃이 [있는 구매 발주 양식 만들기를 참조하십시오](https://www.adobe.com/go/learn_aemforms_qs_poformflowable_9).

### 데이터 하위 그룹 이해 {#understanding-data-subgroups}

XML 데이터 소스는 양식을 고정 레이아웃과 플로우 가능한 레이아웃으로 미리 채우는 데 사용됩니다. 하지만, 다른 점은 양식을 플로우 가능한 레이아웃으로 미리 채우는 XML 데이터 소스에는 양식에서 반복되는 하위 양식을 채울 때 사용되는 반복되는 XML 요소가 포함되어 있다는 것입니다. 이러한 반복되는 XML 요소를 데이터 하위 그룹이라고 합니다.

이전 다이어그램에 표시된 구매 발주 양식을 미리 채우는 데 사용되는 XML 데이터 소스에는 네 개의 반복되는 데이터 하위 그룹이 있습니다. 각 데이터 하위 그룹은 구입한 항목에 해당합니다. 구입한 제품은 모니터, 책상 램프, 전화기 및 주소록입니다.

다음 XML 데이터 소스는 구매 발주 양식을 미리 채우는 데 사용됩니다.

```xml
     <header>
         <!-- XML elements used to prepopulate non-repeating fields such as address
         <!and city
         <txtPONum>8745236985</txtPONum>
         <dtmDate>2004-02-08</dtmDate>
         <txtOrderedByCompanyName>Any Company Name</txtOrderedByCompanyName>
         <txtOrderedByAddress>555, Any Blvd.</txtOrderedByAddress>
         <txtOrderedByCity>Any City</txtOrderedByCity>
         <txtOrderedByStateProv>ST</txtOrderedByStateProv>
         <txtOrderedByZipCode>12345</txtOrderedByZipCode>
         <txtOrderedByCountry>Any Country</txtOrderedByCountry>
         <txtOrderedByPhone>(123) 456-7890</txtOrderedByPhone>
         <txtOrderedByFax>(123) 456-7899</txtOrderedByFax>
         <txtOrderedByContactName>Contact Name</txtOrderedByContactName>
         <txtDeliverToCompanyName>Any Company Name</txtDeliverToCompanyName>
         <txtDeliverToAddress>7895, Any Street</txtDeliverToAddress>
         <txtDeliverToCity>Any City</txtDeliverToCity>
         <txtDeliverToStateProv>ST</txtDeliverToStateProv>
         <txtDeliverToZipCode>12346</txtDeliverToZipCode>
         <txtDeliverToCountry>Any Country</txtDeliverToCountry>
         <txtDeliverToPhone>(123) 456-7891</txtDeliverToPhone>
         <txtDeliverToFax>(123) 456-7899</txtDeliverToFax>
         <txtDeliverToContactName>Contact Name</txtDeliverToContactName>
     </header>
     <detail>
         <!-- A data subgroup that contains information about the monitor>
         <txtPartNum>00010-100</txtPartNum>
         <txtDescription>Monitor</txtDescription>
         <numQty>1</numQty>
         <numUnitPrice>350.00</numUnitPrice>
     </detail>
     <detail>
         <!-- A data subgroup that contains information about the desk lamp>
         <txtPartNum>00010-200</txtPartNum>
         <txtDescription>Desk lamps</txtDescription>
         <numQty>3</numQty>
         <numUnitPrice>55.00</numUnitPrice>
     </detail>
     <detail>
         <!-- A data subgroup that contains information about the Phone>
             <txtPartNum>00025-275</txtPartNum>
             <txtDescription>Phone</txtDescription>
             <numQty>5</numQty>
             <numUnitPrice>85.00</numUnitPrice>
     </detail>
     <detail>
         <!-- A data subgroup that contains information about the address book>
         <txtPartNum>00300-896</txtPartNum>
         <txtDescription>Address book</txtDescription>
         <numQty>2</numQty>
         <numUnitPrice>15.00</numUnitPrice>
     </detail>
```

각 데이터 하위 그룹에는 다음 정보에 해당하는 4개의 XML 요소가 포함되어 있습니다.

* 품목 부품 번호
* 항목 설명
* 품목 수량
* 단가

데이터 하위 그룹의 상위 XML 요소의 이름은 양식 디자인에 있는 하위 폼의 이름과 일치해야 합니다. 예를 들어, 이전 다이어그램에서는 데이터 하위 그룹의 상위 XML 요소의 이름이 입니다 `detail`. 이것은 구매 주문서 양식의 기반이 되는 양식 디자인에 있는 하위 폼의 이름에 해당합니다. 데이터 하위 그룹의 상위 XML 요소와 하위 폼의 이름이 일치하지 않으면 서버측 양식이 미리 채워지지 않습니다.

각 데이터 하위 그룹에는 하위 폼의 필드 이름과 일치하는 XML 요소가 포함되어야 합니다. 양식 디자인에 있는 `detail` 하위 폼에는 다음과 같은 필드가 포함되어 있습니다.

* txtPartNum
* txtDescription
* numQty
* numUnitPrice

>[!NOTE]
>
>반복되는 XML 요소를 포함하는 데이터 소스로 양식을 채울 때 이 `RenderAtClient` `No`옵션을 로 설정하면 첫 번째 데이터 레코드만 양식에 병합됩니다. 모든 데이터 레코드가 양식에 병합되도록 하려면 을 `RenderAtClient` 설정합니다 `Yes`. 옵션에 대한 자세한 내용은 `RenderAtClient` 클라이언트의 [양식 렌더링을 참조하십시오](/help/forms/developing/rendering-forms-client.md).

>[!NOTE]
>
>양식 서비스에 대한 자세한 내용은 AEM Forms에 대한 [서비스 참조를 참조하십시오](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary-of-steps}

순서별 레이아웃으로 양식을 미리 채우려면 다음 작업을 수행하십시오.

1. 프로젝트 파일 포함
1. 메모리 내 XML 데이터 소스를 만듭니다.
1. XML 데이터 소스를 변환합니다.
1. 미리 채워진 양식을 렌더링합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함할 수 있습니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함할 수 있습니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**메모리 내 XML 데이터 소스 만들기**

클래스를 사용하여 메모리 내 XML 데이터 소스를 만들어 순서별 레이아웃으로 양식을 미리 채울 수 있습니다. `org.w3c.dom` 양식을 준수하는 XML 데이터 소스에 데이터를 배치해야 합니다. 순서별 레이아웃과 XML 데이터 소스의 양식 간 관계에 대한 자세한 내용은 데이터 하위 그룹 [이해를 참조하십시오](#understanding-data-subgroups).

**XML 데이터 소스 변환**

클래스를 사용하여 만든 메모리 내 XML 데이터 소스 `org.w3c.dom` 는 양식을 미리 채우는 데 사용하기 전에 `com.adobe.idp.Document` 개체로 변환할 수 있습니다. 메모리 내 XML 데이터 소스는 Java XML 변환 클래스를 사용하여 변환할 수 있습니다.

>[!NOTE]
>
>Forms 서비스의 WSDL을 사용하여 양식을 미리 채우는 경우 `org.w3c.dom.Document` 개체를 `BLOB` 개체로 변환해야 합니다.

**미리 채워진 양식 렌더링**

미리 채워진 양식을 다른 양식과 마찬가지로 렌더링합니다. 유일한 차이는 XML 데이터 소스가 포함된 `com.adobe.idp.Document` 개체를 사용하여 양식을 미리 채우는 것입니다.

**참고 항목**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms Service API 빠른 시작](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[대화형 PDF forms 렌더링](/help/forms/developing/rendering-interactive-pdf-forms.md)

[양식을 렌더링하는 웹 애플리케이션 만들기](/help/forms/developing/creating-web-applications-renders-forms.md)

### Java API를 사용하여 양식 미리 채우기 {#prepopulating-forms-using-the-java-api}

양식 API(Java)를 사용하여 양식 레이아웃으로 양식을 미리 채우려면 다음 단계를 수행하십시오.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-forms-client.jar와 같은 클라이언트 JAR 파일을 포함합니다. 이러한 파일의 위치에 대한 자세한 내용은 AEM Forms Java 라이브러리 파일 [포함을 참조하십시오](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

1. 메모리 내 XML 데이터 소스 만들기

   * 클래스 `DocumentBuilderFactory` 의 메서드를 호출하여 Java `DocumentBuilderFactory` 개체를 `newInstance` 만듭니다.
   * 개체의 메서드를 호출하여 Java `DocumentBuilder` 개체를 `DocumentBuilderFactory` 만듭니다 `newDocumentBuilder` .
   * 개체를 인스턴스화하려면 `DocumentBuilder` 개체의 `newDocument` 메서드를 `org.w3c.dom.Document` 호출합니다.
   * 개체의 메서드를 호출하여 XML 데이터 소스의 루트 요소 `org.w3c.dom.Document` 를 `createElement` 만듭니다. 이렇게 하면 루트 요소를 나타내는 `Element` 개체가 만들어집니다. 요소의 이름을 나타내는 문자열 값을 메서드에 `createElement` 전달합니다. 반환 값을 다음으로 캐스팅합니다 `Element`. 그런 다음 `Document` 개체의 메서드를 호출하여 문서에 루트 요소 `appendChild` 를 추가하고 루트 요소 개체를 인수로 전달합니다. 다음 코드 줄은 이 응용 프로그램 논리를 보여 줍니다.

      ` Element root = (Element)document.createElement("transaction");  document.appendChild(root);`

   * 개체의 메서드를 호출하여 XML 데이터 소스의 헤더 요소를 `Document` `createElement` 만듭니다. 요소의 이름을 나타내는 문자열 값을 메서드에 `createElement` 전달합니다. 반환 값을 다음으로 캐스팅합니다 `Element`. 그런 다음 `root` `appendChild` 개체의 메서드를 호출하여 헤더 요소를 루트 요소에 추가하고 헤더 요소 개체를 인수로 전달합니다. 헤더 요소에 추가되는 XML 요소는 양식의 정적 부분에 해당합니다. 다음 코드 줄은 이 응용 프로그램 논리를 보여 줍니다.

      ` Element header = (Element)document.createElement("header");  root.appendChild(header);`

   * 개체의 메서드를 호출하여 헤더 요소에 속하는 하위 요소를 만들고 `Document` `createElement` 요소의 이름을 나타내는 문자열 값을 전달합니다. 반환 값을 다음으로 캐스팅합니다 `Element`. 그런 다음 해당 메서드를 호출하여 자식 요소의 값을 `appendChild` 설정하고 `Document` 개체의 `createTextNode` 메서드를 인수로 전달합니다. 하위 요소의 값으로 표시되는 문자열 값을 지정합니다. 마지막으로, 헤더 요소의 메서드를 호출하여 하위 요소를 헤더 요소에 추가하고 하위 요소 `appendChild` 개체를 인수로 전달합니다. 다음 코드 줄은 이 응용 프로그램 논리를 보여 줍니다.

      ` Element poNum= (Element)document.createElement("txtPONum");  poNum.appendChild(document.createTextNode("8745236985"));  header.appendChild(LastName);`


   * 양식의 정적 부분에 나타나는 각 필드에 대한 마지막 하위 단계를 반복하여 나머지 모든 요소를 헤더 요소에 추가합니다(XML 데이터 소스 다이어그램에서 이러한 필드는 섹션 A에 표시됩니다. 데이터 하위 그룹 [이해를 참조하십시오](#understanding-data-subgroups).)
   * 개체의 메서드를 호출하여 XML 데이터 소스의 세부 사항 요소를 `Document` `createElement` 만듭니다. 요소의 이름을 나타내는 문자열 값을 메서드에 `createElement` 전달합니다. 반환 값을 다음으로 캐스팅합니다 `Element`. 그런 다음 `root` `appendChild` 개체의 메서드를 호출하여 세부 사항 요소를 루트 요소에 추가하고 세부 요소 개체를 인수로 전달합니다. 세부 사항 요소에 추가되는 XML 요소는 양식의 동적 부분에 해당합니다. 다음 코드 줄은 이 응용 프로그램 논리를 보여 줍니다.

      ` Element detail = (Element)document.createElement("detail");  root.appendChild(detail);`

   * 개체의 메서드를 호출하여 세부 사항 요소에 속하는 하위 요소를 만들고 `Document` 요소의 이름을 나타내는 문자열 값을 `createElement` 전달합니다. 반환 값을 다음으로 캐스팅합니다 `Element`. 그런 다음 해당 메서드를 호출하여 자식 요소의 값을 `appendChild` 설정하고 `Document` 개체의 `createTextNode` 메서드를 인수로 전달합니다. 하위 요소의 값으로 표시되는 문자열 값을 지정합니다. 마지막으로 세부 요소의 메서드를 호출하여 하위 요소를 세부 사항 요소 `appendChild` 에 추가하고 자식 요소 개체를 인수로 전달합니다. 다음 코드 줄은 이 응용 프로그램 논리를 보여 줍니다.

      ` Element txtPartNum = (Element)document.createElement("txtPartNum");  txtPartNum.appendChild(document.createTextNode("00010-100"));  detail.appendChild(txtPartNum);`

   * 모든 XML 요소에 세부 요소에 추가할 마지막 하위 단계를 반복합니다. 구매 발주 양식을 채우는 데 사용되는 XML 데이터 소스를 올바르게 만들려면 다음 XML 요소를 세부 사항 요소에 추가해야 합니다. `txtDescription`, `numQty`and `numUnitPrice`.
   * 양식을 채울 때 사용한 모든 데이터 항목에 대해 마지막 두 개의 하위 단계를 반복합니다.

1. XML 데이터 소스 변환

   * 개체의 정적 `javax.xml.transform.Transformer` 메서드를 호출하여 개체를 `javax.xml.transform.Transformer` 만듭니다 `newInstance` .
   * 개체 `Transformer` 의 메서드를 호출하여 `TransformerFactory` 개체를 `newTransformer` 만듭니다.
   * 생성자를 사용하여 `ByteArrayOutputStream` 개체를 만듭니다.
   * 생성자를 사용하여 `javax.xml.transform.dom.DOMSource` 개체를 만들고 1단계에서 만든 `org.w3c.dom.Document` 개체를 전달합니다.
   * 생성자를 사용하여 개체를 `javax.xml.transform.dom.DOMSource` 만들고 개체를 `ByteArrayOutputStream` 전달합니다.
   * 객체의 메서드를 호출하고 `ByteArrayOutputStream` 및 `javax.xml.transform.Transformer` 객체를 전달하여 Java 객체 `transform` `javax.xml.transform.dom.DOMSource` `javax.xml.transform.stream.StreamResult` 를 채웁니다.
   * 바이트 배열을 만들고 개체의 크기를 바이트 배열에 `ByteArrayOutputStream` 할당합니다.
   * 개체의 메서드를 호출하여 바이트 배열 `ByteArrayOutputStream` 을 `toByteArray` 채웁니다.
   * 생성자를 사용하고 바이트 배열을 전달하여 `com.adobe.idp.Document` 개체를 만듭니다.

1. 미리 채워진 양식 렌더링

   개체의 `FormsServiceClient` 메서드를 `renderPDFForm` 호출하고 다음 값을 전달합니다.

   * 파일 이름 확장자를 포함하여 양식 디자인 이름을 지정하는 문자열 값.
   * 양식과 병합할 데이터가 포함된 `com.adobe.idp.Document` 개체 1단계와 2단계에서 만든 `com.adobe.idp.Document` 개체를 사용해야 합니다.
   * 런타임 옵션을 저장하는 `PDFFormRenderSpec` 개체입니다.
   * Forms 서비스에 필요한 URI 값이 포함된 `URLSpec` 개체입니다.
   * 첨부 파일을 저장하는 `java.util.HashMap` 개체입니다. 선택 매개 변수이며 양식에 파일을 첨부하지 않으려는 `null` 경우 지정할 수 있습니다.

   이 `renderPDFForm` 메서드는 클라이언트 웹 브라우저에 작성해야 하는 양식 데이터 스트림을 포함하는 `FormsResult` 개체를 반환합니다.

   * 양식 데이터 스트림을 클라이언트 웹 브라우저로 전송하는 데 사용되는 `javax.servlet.ServletOutputStream` 개체를 만듭니다.
   * 개체 &#39;s 메서드 `com.adobe.idp.Document` 를 호출하여 개체를 `FormsResult` 만듭니다 `getOutputContent` .
   * 개체 `java.io.InputStream` 의 메서드를 호출하여 `com.adobe.idp.Document` 개체를 `getInputStream` 만듭니다.
   * 바이트 배열을 만들면 `InputStream` 개체의 메서드를 호출하고 바이트 배열을 인수로 전달하여 양식 데이터 스트림으로 해당 `read` 를 채웁니다.
   * 개체의 `javax.servlet.ServletOutputStream` 메서드를 `write` 호출하여 양식 데이터 스트림을 클라이언트 웹 브라우저에 보냅니다. 바이트 배열을 `write` 메서드로 전달합니다.


**참고 항목**

[빠른 시작(SOAP 모드): Java API를 사용하여 양식에 플로우 가능한 레이아웃 미리 채우기](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-prepopulating-forms-with-flowable-layouts-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 양식 채우기 {#prepopulating-forms-using-the-web-service-api}

양식 API(웹 서비스)를 사용하여 양식을 플로우 가능한 레이아웃으로 미리 채우려면 다음 단계를 수행하십시오.

1. 프로젝트 파일 포함

   * Forms 서비스 WSDL을 사용하는 Java 프록시 클래스를 만듭니다. (Apache [Axis를 사용하여 Java 프록시 클래스 만들기를 참조하십시오](/help/forms/developing/invoking-aem-forms-using-web.md#creating-java-proxy-classes-using-apache-axis).)
   * 클래스 경로에 Java 프록시 클래스를 포함합니다.

1. 메모리 내 XML 데이터 소스 만들기

   * 클래스 `DocumentBuilderFactory` 의 메서드를 호출하여 Java `DocumentBuilderFactory` 개체를 `newInstance` 만듭니다.
   * 개체의 메서드를 호출하여 Java `DocumentBuilder` 개체를 `DocumentBuilderFactory` 만듭니다 `newDocumentBuilder` .
   * 개체를 인스턴스화하려면 `DocumentBuilder` 개체의 `newDocument` 메서드를 `org.w3c.dom.Document` 호출합니다.
   * 개체의 메서드를 호출하여 XML 데이터 소스의 루트 요소 `org.w3c.dom.Document` 를 `createElement` 만듭니다. 이렇게 하면 루트 요소를 나타내는 `Element` 개체가 만들어집니다. 요소의 이름을 나타내는 문자열 값을 메서드에 `createElement` 전달합니다. 반환 값을 다음으로 캐스팅합니다 `Element`. 그런 다음 `Document` 개체의 메서드를 호출하여 문서에 루트 요소 `appendChild` 를 추가하고 루트 요소 개체를 인수로 전달합니다. 다음 코드 줄은 이 응용 프로그램 논리를 보여 줍니다.

      ` Element root = (Element)document.createElement("transaction");  document.appendChild(root);`

   * 개체의 메서드를 호출하여 XML 데이터 소스의 헤더 요소를 `Document` `createElement` 만듭니다. 요소의 이름을 나타내는 문자열 값을 메서드에 `createElement` 전달합니다. 반환 값을 다음으로 캐스팅합니다 `Element`. 그런 다음 `root` `appendChild` 개체의 메서드를 호출하여 헤더 요소를 루트 요소에 추가하고 헤더 요소 개체를 인수로 전달합니다. 헤더 요소에 추가되는 XML 요소는 양식의 정적 부분에 해당합니다. 다음 코드 줄은 이 응용 프로그램 논리를 보여 줍니다.

      ` Element header = (Element)document.createElement("header");  root.appendChild(header);`

   * 개체의 메서드를 호출하여 헤더 요소에 속하는 하위 요소를 만들고 `Document` `createElement` 요소의 이름을 나타내는 문자열 값을 전달합니다. 반환 값을 다음으로 캐스팅합니다 `Element`. 그런 다음 해당 메서드를 호출하여 자식 요소의 값을 `appendChild` 설정하고 `Document` 개체의 `createTextNode` 메서드를 인수로 전달합니다. 하위 요소의 값으로 표시되는 문자열 값을 지정합니다. 마지막으로, 헤더 요소의 메서드를 호출하여 하위 요소를 헤더 요소에 추가하고 하위 요소 `appendChild` 개체를 인수로 전달합니다. 다음 코드 줄은 이 응용 프로그램 논리를 보여 줍니다.

      ` Element poNum= (Element)document.createElement("txtPONum");  poNum.appendChild(document.createTextNode("8745236985"));  header.appendChild(LastName);`

   * 양식의 정적 부분에 나타나는 각 필드에 대한 마지막 하위 단계를 반복하여 나머지 모든 요소를 헤더 요소에 추가합니다(XML 데이터 소스 다이어그램에서 이러한 필드는 섹션 A에 표시됩니다. 데이터 하위 그룹 [이해를 참조하십시오](#understanding-data-subgroups).)
   * 개체의 메서드를 호출하여 XML 데이터 소스의 세부 사항 요소를 `Document` `createElement` 만듭니다. 요소의 이름을 나타내는 문자열 값을 메서드에 `createElement` 전달합니다. 반환 값을 다음으로 캐스팅합니다 `Element`. 그런 다음 `root` `appendChild` 개체의 메서드를 호출하여 세부 사항 요소를 루트 요소에 추가하고 세부 요소 개체를 인수로 전달합니다. 세부 사항 요소에 추가되는 XML 요소는 양식의 동적 부분에 해당합니다. 다음 코드 줄은 이 응용 프로그램 논리를 보여 줍니다.

      ` Element detail = (Element)document.createElement("detail");  root.appendChild(detail);`

   * 개체의 메서드를 호출하여 세부 사항 요소에 속하는 하위 요소를 만들고 `Document` 요소의 이름을 나타내는 문자열 값을 `createElement` 전달합니다. 반환 값을 다음으로 캐스팅합니다 `Element`. 그런 다음 해당 메서드를 호출하여 자식 요소의 값을 `appendChild` 설정하고 `Document` 개체의 `createTextNode` 메서드를 인수로 전달합니다. 하위 요소의 값으로 표시되는 문자열 값을 지정합니다. 마지막으로 세부 요소의 메서드를 호출하여 하위 요소를 세부 사항 요소 `appendChild` 에 추가하고 자식 요소 개체를 인수로 전달합니다. 다음 코드 줄은 이 응용 프로그램 논리를 보여 줍니다.

      ` Element txtPartNum = (Element)document.createElement("txtPartNum");  txtPartNum.appendChild(document.createTextNode("00010-100"));  detail.appendChild(txtPartNum);`

   * 모든 XML 요소에 세부 요소에 추가할 마지막 하위 단계를 반복합니다. 구매 발주 양식을 채우는 데 사용되는 XML 데이터 소스를 올바르게 만들려면 다음 XML 요소를 세부 사항 요소에 추가해야 합니다. `txtDescription`, `numQty`and `numUnitPrice`.
   * 양식을 채울 때 사용한 모든 데이터 항목에 대해 마지막 두 개의 하위 단계를 반복합니다.

1. XML 데이터 소스 변환

   * 개체의 정적 `javax.xml.transform.Transformer` 메서드를 호출하여 개체를 `javax.xml.transform.Transformer` 만듭니다 `newInstance` .
   * 개체 `Transformer` 의 메서드를 호출하여 `TransformerFactory` 개체를 `newTransformer` 만듭니다.
   * 생성자를 사용하여 `ByteArrayOutputStream` 개체를 만듭니다.
   * 생성자를 사용하여 `javax.xml.transform.dom.DOMSource` 개체를 만들고 1단계에서 만든 `org.w3c.dom.Document` 개체를 전달합니다.
   * 생성자를 사용하여 개체를 `javax.xml.transform.dom.DOMSource` 만들고 개체를 `ByteArrayOutputStream` 전달합니다.
   * 객체의 메서드를 호출하고 `ByteArrayOutputStream` 및 `javax.xml.transform.Transformer` 객체를 전달하여 Java 객체 `transform` `javax.xml.transform.dom.DOMSource` `javax.xml.transform.stream.StreamResult` 를 채웁니다.
   * 바이트 배열을 만들고 개체의 크기를 바이트 배열에 `ByteArrayOutputStream` 할당합니다.
   * 개체의 메서드를 호출하여 바이트 배열 `ByteArrayOutputStream` 을 `toByteArray` 채웁니다.
   * 생성자를 사용하여 `BLOB` 개체를 만들고 해당 `setBinaryData` 메서드를 호출하고 바이트 배열을 전달합니다.

1. 미리 채워진 양식 렌더링

   개체의 `FormsService` 메서드를 `renderPDFForm` 호출하고 다음 값을 전달합니다.

   * 파일 이름 확장자를 포함하여 양식 디자인 이름을 지정하는 문자열 값.
   * 양식과 병합할 데이터가 포함된 `BLOB` 개체 1단계와 2단계에서 생성된 `BLOB` 객체를 사용해야 합니다.
   * 런타임 옵션을 저장하는 `PDFFormRenderSpecc` 개체입니다. 자세한 내용은 [AEM Forms API 참조를 참조하십시오](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * Forms 서비스에 필요한 URI 값이 포함된 `URLSpec` 개체입니다.
   * 첨부 파일을 저장하는 `java.util.HashMap` 개체입니다. 선택 매개 변수이며 양식에 파일을 첨부하지 않으려는 `null` 경우 지정할 수 있습니다.
   * 메서드로 채워지는 빈 `com.adobe.idp.services.holders.BLOBHolder` 개체입니다. 렌더링된 PDF 양식을 저장하는 데 사용됩니다.
   * 메서드로 채워지는 빈 `javax.xml.rpc.holders.LongHolder` 개체입니다. 이 인수는 양식의 페이지 수를 저장합니다.
   * 메서드로 채워지는 빈 `javax.xml.rpc.holders.StringHolder` 개체입니다. 이 인수는 로케일 값을 저장합니다.
   * 이 작업 결과를 포함할 빈 `com.adobe.idp.services.holders.FormsResultHolder` 개체입니다.

   이 `renderPDFForm` 메서드는 마지막 인수 값으로 전달되는 `com.adobe.idp.services.holders.FormsResultHolder` 개체를 클라이언트 웹 브라우저에 작성해야 하는 양식 데이터 스트림으로 채웁니다.

   * 개체 `FormResult` 의 데이터 멤버 값을 가져와서 `com.adobe.idp.services.holders.FormsResultHolder` 개체를 `value` 만듭니다.
   * 개체의 메서드를 호출하여 양식 데이터 `BLOB` 가 포함된 `FormsResult` `getOutputContent` 개체를 만듭니다.
   * 해당 메서드를 호출하여 개체의 `BLOB` 콘텐츠 유형을 `getContentType` 가져옵니다.
   * 해당 메서드를 호출하고 개체의 컨텐트 유형을 전달하여 `javax.servlet.http.HttpServletResponse` 개체의 컨텐트 유형을 `setContentType` `BLOB` 설정합니다.
   * 개체의 메서드를 호출하여 양식 데이터 스트림을 클라이언트 웹 브라우저에 쓰는 데 사용되는 `javax.servlet.ServletOutputStream` 개체를 `javax.servlet.http.HttpServletResponse` `getOutputStream` 만듭니다.
   * 바이트 배열을 만들고 `BLOB` 개체의 메서드를 호출하여 `getBinaryData` 채웁니다. 이 작업은 개체의 내용을 바이트 배열에 `FormsResult` 할당합니다.
   * 개체의 `javax.servlet.http.HttpServletResponse` 메서드를 `write` 호출하여 양식 데이터 스트림을 클라이언트 웹 브라우저에 보냅니다. 바이트 배열을 `write` 메서드로 전달합니다.

   >[!NOTE]
   >
   >이 `renderPDFForm` 메서드는 마지막 인수 값으로 전달되는 `com.adobe.idp.services.holders.FormsResultHolder` 개체를 클라이언트 웹 브라우저에 작성해야 하는 양식 데이터 스트림으로 채웁니다.

**참고 항목**

[Base64 인코딩을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

