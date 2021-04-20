---
title: Forms에 플로우 가능한 레이아웃 미리 채우기
seo-title: Forms에 플로우 가능한 레이아웃 미리 채우기
description: Java API 및 웹 서비스 API를 사용하여 렌더링된 양식 내에서 사용자에게 데이터를 표시하려면 양식을 플로우 가능한 레이아웃으로 미리 채웁니다.
seo-description: Java API 및 웹 서비스 API를 사용하여 렌더링된 양식 내에서 사용자에게 데이터를 표시하려면 양식을 플로우 가능한 레이아웃으로 미리 채웁니다.
uuid: 93ccb496-e1c2-4b79-8e89-7a2abfce1537
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 30a12fc6-07b8-4c7c-b9e2-caa2bec0ac48
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '3534'
ht-degree: 0%

---


# Forms에 플로우 가능한 레이아웃 {#prepopulating-forms-with-flowable-layouts1}으로 미리 채우기

## Forms에 플로우 가능한 레이아웃 {#prepopulating-forms-with-flowable-layouts2}으로 미리 채우기

양식을 미리 채우면 렌더링된 양식 내의 사용자에게 데이터가 표시됩니다. 예를 들어 사용자가 사용자 이름과 암호를 사용하여 웹 사이트에 로그인한다고 가정합니다. 인증이 완료되면 클라이언트 응용 프로그램은 데이터베이스에 사용자 정보를 쿼리합니다. 데이터가 양식에 병합된 후 양식이 사용자에게 렌더링됩니다. 따라서 사용자는 양식 내에서 개인화된 데이터를 볼 수 있습니다.

양식을 미리 채우면 다음과 같은 이점이 있습니다.

* 사용자가 양식에서 사용자 지정 데이터를 볼 수 있도록 합니다.
* 사용자가 양식을 채우도록 입력하는 시간이 줄어듭니다.
* 데이터 배치 위치를 제어하여 데이터 무결성을 보장합니다.

다음 2개의 XML 데이터 소스가 양식을 미리 채울 수 있습니다.

* XFA 구문(또는 Acrobat을 사용하여 만든 양식을 미리 채우기 위한 XFDF 데이터)을 준수하는 XML인 XDP 데이터 소스입니다.
* 양식의 필드 이름과 일치하는 이름/값 쌍이 포함된 임의 XML 데이터 소스(이 섹션의 예에서는 임의의 XML 데이터 소스를 사용합니다.)

미리 채우려는 모든 양식 필드에 대해 XML 요소가 있어야 합니다. XML 요소 이름은 필드 이름과 일치해야 합니다. XML 요소는 양식 필드에 해당되지 않거나 XML 요소 이름이 필드 이름과 일치하지 않는 경우 무시됩니다. 모든 XML 요소가 지정된 한 XML 요소가 표시되는 순서와 일치할 필요는 없습니다.

이미 데이터가 포함된 양식을 채울 때는 XML 데이터 소스 내에 이미 표시된 데이터를 지정해야 합니다. 필드가 10개인 양식에 데이터가 4개 필드에 있다고 가정합니다. 그런 다음 나머지 6개 필드를 미리 채우도록 가정해 봅니다. 이 경우 양식을 미리 채우는 데 사용되는 XML 데이터 소스에 10개의 XML 요소를 지정해야 합니다. 6개의 요소만 지정하면 원래 4개의 필드가 비어 있습니다.

예를 들어 샘플 확인 양식과 같은 양식을 미리 채울 수 있습니다. ([대화형 PDF forms 렌더링](/help/forms/developing/rendering-interactive-pdf-forms.md)의 &quot;확인 양식&quot;을 참조하십시오.)

샘플 확인 양식을 미리 채우려면 양식에서 3개의 필드와 일치하는 3개의 XML 요소가 포함된 XML 데이터 소스를 만들어야 합니다. 이 양식에는 다음과 같은 세 개의 필드가 포함됩니다.`FirstName`, `LastName` 및 `Amount`. 첫 번째 단계는 양식 디자인에 있는 필드와 일치하는 XML 요소를 포함하는 XML 데이터 소스를 만드는 것입니다. 다음 단계는 다음 XML 코드와 같이 XML 요소에 데이터 값을 할당하는 것입니다.

```xml
     <Untitled>
         <FirstName>Jerry</FirstName>
         <LastName>Johnson</LastName>
         <Amount>250000</Amount>
     </Untitled>
```

확인 양식을 이 XML 데이터 소스로 미리 채우고 양식을 렌더링하면 다음 다이어그램과 같이 XML 요소에 할당한 데이터 값이 표시됩니다.

![pf_confirmxml3](assets/pf_pf_confirmxml3.png)

### 양식 채우기 및 플로우 가능한 레이아웃 {#prepopulating_forms_with_flowable_layouts-1}

플로우 가능한 레이아웃이 있는 Forms은 사용자에게 정해지지 않은 양의 데이터를 표시하는 데 유용합니다. 양식의 레이아웃은 병합된 데이터의 양에 따라 자동으로 조정되므로 고정 레이아웃이 있는 폼에서 수행해야 하는 고정 레이아웃이나 양식의 페이지 수를 미리 결정할 필요가 없습니다.

일반적으로 양식은 런타임 중에 얻은 데이터로 채워집니다. 따라서 메모리 내 XML 데이터 소스를 만들고 데이터를 메모리 내 XML 데이터 소스에 직접 배치하여 양식을 미리 채울 수 있습니다.

온라인 스토어와 같은 웹 기반 응용 프로그램을 고려합니다. 온라인 구매자가 항목 구매를 완료하면 구입한 모든 항목이 양식을 미리 채우는 데 사용되는 메모리 내 XML 데이터 소스에 배치됩니다. 다음 다이어그램은 이 프로세스를 보여 줍니다. 이 프로세스는 다이어그램 아래의 표에 설명되어 있습니다.

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
   <td><p>사용자는 웹 기반 온라인 스토어에서 항목을 구매합니다. </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>사용자가 항목 구입을 마치고 [제출] 단추를 클릭하면 메모리 내 XML 데이터 소스가 생성됩니다. 구입한 항목 및 사용자 정보는 메모리 내 XML 데이터 소스에 배치됩니다. </p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>XML 데이터 소스는 구매 발주 양식을 미리 채우는 데 사용됩니다(이 표의 예는 다음 표에 나와 있습니다). </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>구매 주문서 양식이 클라이언트 웹 브라우저에 렌더링됩니다. </p></td>
  </tr>
 </tbody>
</table>

다음 다이어그램은 구매 발주 양식의 예를 보여줍니다. 테이블의 정보는 XML 데이터의 레코드 수에 맞게 조정할 수 있습니다.

![pdf_pdf_form](assets/pf_pf_poform.png)

>[!NOTE]
>
>기업 데이터베이스 또는 외부 애플리케이션과 같은 다른 소스의 데이터로 양식을 미리 채울 수 있습니다.

### 양식 디자인 고려 사항 {#form-design-considerations}

플로우 가능한 레이아웃이 있는 Forms은 Designer에서 만든 양식 디자인을 기반으로 합니다. 양식 디자인은 사용자 입력을 기반으로 값을 계산하는 것을 포함하여 레이아웃, 프레젠테이션 및 데이터 캡처 규칙 세트를 지정합니다. 데이터를 양식에 입력할 때 규칙이 적용됩니다. 양식에 추가되는 필드는 양식 디자인 내에 있는 하위 양식입니다. 예를 들어 이전 다이어그램에 표시된 구매 주문서 양식에서는 각 라인이 하위 폼입니다. 하위 양식이 포함된 양식 디자인을 만드는 방법에 대한 자세한 내용은 [플로우 가능한 레이아웃](https://www.adobe.com/go/learn_aemforms_qs_poformflowable_9)이 있는 구매 발주 양식 만들기를 참조하십시오.

### 데이터 하위 그룹 이해 {#understanding-data-subgroups}

XML 데이터 소스는 양식을 고정 레이아웃과 플로우 가능한 레이아웃으로 미리 채우는 데 사용됩니다. 그러나 다른 점은 양식을 플로우 가능한 레이아웃으로 미리 채우는 XML 데이터 소스에는 양식에서 반복되는 하위 양식을 미리 채우는 데 사용되는 반복되는 XML 요소가 포함되어 있다는 것입니다. 이러한 반복 XML 요소를 데이터 하위 그룹이라고 합니다.

이전 다이어그램에 표시된 구매 발주 양식을 미리 채우는 데 사용되는 XML 데이터 소스에는 4개의 반복 데이터 하위 그룹이 있습니다. 각 데이터 하위 그룹은 구매한 항목에 해당합니다. 구입한 품목은 모니터, 책상 램프, 전화기 및 주소록.

다음 XML 데이터 소스를 사용하여 구매 주문 양식을 미리 채웁니다.

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

각 데이터 하위 그룹에는 이 정보에 해당하는 4개의 XML 요소가 포함되어 있습니다.

* 품목 부품 번호
* 항목 설명
* 품목 수량
* 단가

데이터 하위 그룹의 상위 XML 요소의 이름은 양식 디자인에 있는 하위 폼의 이름과 일치해야 합니다. 예를 들어 이전 다이어그램에서 데이터 하위 그룹의 상위 XML 요소의 이름은 `detail`입니다. 이것은 구매 주문서 양식의 기반이 되는 양식 디자인에 있는 하위 폼 이름에 해당합니다. 데이터 하위 그룹의 상위 XML 요소와 하위 폼의 이름이 일치하지 않으면 서버측 양식이 미리 채워지지 않습니다.

각 데이터 하위 그룹은 하위 폼의 필드 이름과 일치하는 XML 요소를 포함해야 합니다. 양식 디자인에 있는 `detail` 하위 양식에는 다음 필드가 포함되어 있습니다.

* txtPartNum
* txtDescription
* numQty
* numUnitPrice

>[!NOTE]
>
>반복 XML 요소가 포함된 데이터 원본으로 양식을 채우려고 하고 `RenderAtClient` 옵션을 `No`으로 설정하면 첫 번째 데이터 레코드만 양식에 병합됩니다. 모든 데이터 레코드가 양식에 병합되도록 하려면 `RenderAtClient`을 `Yes`로 설정합니다. `RenderAtClient` 옵션에 대한 자세한 내용은 [클라이언트](/help/forms/developing/rendering-forms-client.md)에서 Forms 렌더링을 참조하십시오.

>[!NOTE]
>
>Forms 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### {#summary-of-steps} 단계 요약

순서별 레이아웃으로 양식을 미리 채우려면 다음 작업을 수행합니다.

1. 프로젝트 파일 포함
1. 메모리 내 XML 데이터 소스를 만듭니다.
1. XML 데이터 소스를 변환합니다.
1. 미리 채워진 양식을 렌더링합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함할 수 있습니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함할 수 있습니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**메모리 내 XML 데이터 소스 만들기**

`org.w3c.dom` 클래스를 사용하여 메모리 내 XML 데이터 소스를 만들어 순서별 레이아웃으로 양식을 미리 채울 수 있습니다. 양식을 준수하는 XML 데이터 소스에 데이터를 배치해야 합니다. 순서별 레이아웃과 XML 데이터 소스의 양식 간 관계에 대한 자세한 내용은 [데이터 하위 그룹 이해](#understanding-data-subgroups)를 참조하십시오.

**XML 데이터 소스 변환**

`org.w3c.dom` 클래스를 사용하여 만든 메모리 내 XML 데이터 소스는 양식을 미리 채우는 데 사용하기 전에 `com.adobe.idp.Document` 객체로 변환할 수 있습니다. 메모리 내 XML 데이터 소스는 Java XML 변환 클래스를 사용하여 변환할 수 있습니다.

>[!NOTE]
>
>Forms 서비스의 WSDL을 사용하여 양식을 미리 채우는 경우 `org.w3c.dom.Document` 객체를 `BLOB` 객체로 변환해야 합니다.

**미리 채워진 양식 렌더링**

다른 양식과 마찬가지로 미리 채워진 양식을 렌더링합니다. 유일한 차이는 XML 데이터 소스가 포함된 `com.adobe.idp.Document` 개체를 사용하여 양식을 미리 채우는 것입니다.

**참고 항목**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms 서비스 API 빠른 시작](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[대화형 PDF forms 렌더링](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Forms을 렌더링하는 웹 애플리케이션 만들기](/help/forms/developing/creating-web-applications-renders-forms.md)

### Java API {#prepopulating-forms-using-the-java-api}를 사용하여 양식 미리 채우기

Forms API(Java)를 사용하여 플로우 가능한 레이아웃으로 양식을 미리 채우려면 다음 단계를 수행하십시오.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-forms-client.jar 등의 클라이언트 JAR 파일을 포함합니다. 이러한 파일의 위치에 대한 자세한 내용은 [AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)을 참조하십시오.

1. 메모리 내 XML 데이터 소스 만들기

   * `DocumentBuilderFactory` 클래스&#39; `newInstance` 메서드를 호출하여 Java `DocumentBuilderFactory` 개체를 만듭니다.
   * `DocumentBuilderFactory` 개체의 `newDocumentBuilder` 메서드를 호출하여 Java `DocumentBuilder` 개체를 만듭니다.
   * `DocumentBuilder` 개체의 `newDocument` 메서드를 호출하여 `org.w3c.dom.Document` 개체를 인스턴스화합니다.
   * `org.w3c.dom.Document` 객체의 `createElement` 메서드를 호출하여 XML 데이터 소스의 루트 요소를 만듭니다. 루트 요소를 나타내는 `Element` 객체가 만들어집니다. 요소의 이름을 나타내는 문자열 값을 `createElement` 메서드에 전달합니다. 반환 값을 `Element`으로 캐스팅합니다. 그런 다음 `Document` 객체의 `appendChild` 메서드를 호출하여 루트 요소를 문서에 추가하고 루트 요소 객체를 인수로 전달합니다. 다음 코드 행은 이 응용 프로그램 논리를 보여 줍니다.

      ` Element root = (Element)document.createElement("transaction");  document.appendChild(root);`

   * `Document` 객체의 `createElement` 메서드를 호출하여 XML 데이터 소스의 헤더 요소를 만듭니다. 요소의 이름을 나타내는 문자열 값을 `createElement` 메서드에 전달합니다. 반환 값을 `Element`으로 캐스팅합니다. 그런 다음 `root` 객체의 `appendChild` 메서드를 호출하여 헤더 요소를 루트 요소에 추가하고 머리글 요소 객체를 인수로 전달합니다. 헤더 요소에 추가되는 XML 요소는 양식의 정적 부분에 해당합니다. 다음 코드 행은 이 응용 프로그램 논리를 보여 줍니다.

      ` Element header = (Element)document.createElement("header");  root.appendChild(header);`

   * `Document` 객체의 `createElement` 메서드를 호출하여 헤더 요소에 속하는 자식 요소를 만들고 요소의 이름을 나타내는 문자열 값을 전달합니다. 반환 값을 `Element`으로 캐스팅합니다. 그런 다음 `appendChild` 메서드를 호출하여 자식 요소의 값을 설정하고 `Document` 객체의 `createTextNode` 메서드를 인수로 전달합니다. 하위 요소의 값으로 나타나는 문자열 값을 지정합니다. 마지막으로, 헤더 요소의 `appendChild` 메서드를 호출하여 하위 요소를 헤더 요소에 추가하고 자식 요소 객체를 인수로 전달합니다. 다음 코드 행은 이 응용 프로그램 논리를 보여 줍니다.

      ` Element poNum= (Element)document.createElement("txtPONum");  poNum.appendChild(document.createTextNode("8745236985"));  header.appendChild(LastName);`


   * 양식의 정적 부분에 나타나는 각 필드에 대한 마지막 하위 단계를 반복하여 나머지 모든 요소를 헤더 요소에 추가합니다(XML 데이터 소스 다이어그램에서 이러한 필드는 섹션 A에 표시됩니다. [데이터 하위 그룹 이해](#understanding-data-subgroups) 참조).
   * `Document` 객체의 `createElement` 메서드를 호출하여 XML 데이터 소스의 세부 사항 요소를 만듭니다. 요소의 이름을 나타내는 문자열 값을 `createElement` 메서드에 전달합니다. 반환 값을 `Element`으로 캐스팅합니다. 그런 다음 `root` 객체의 `appendChild` 메서드를 호출하여 세부 사항 요소를 루트 요소에 추가하고 detail 요소 객체를 인수로 전달합니다. 세부 사항 요소에 추가되는 XML 요소는 양식의 동적 부분에 해당합니다. 다음 코드 행은 이 응용 프로그램 논리를 보여 줍니다.

      ` Element detail = (Element)document.createElement("detail");  root.appendChild(detail);`

   * `Document` 객체의 `createElement` 메서드를 호출하여 세부 요소에 속하는 하위 요소를 만들고 요소의 이름을 나타내는 문자열 값을 전달합니다. 반환 값을 `Element`으로 캐스팅합니다. 그런 다음 `appendChild` 메서드를 호출하여 자식 요소의 값을 설정하고 `Document` 객체의 `createTextNode` 메서드를 인수로 전달합니다. 하위 요소의 값으로 나타나는 문자열 값을 지정합니다. 마지막으로, detail 요소의 `appendChild` 메서드를 호출하여 하위 요소를 detail 요소에 추가하고 자식 요소 객체를 인수로 전달합니다. 다음 코드 행은 이 응용 프로그램 논리를 보여 줍니다.

      ` Element txtPartNum = (Element)document.createElement("txtPartNum");  txtPartNum.appendChild(document.createTextNode("00010-100"));  detail.appendChild(txtPartNum);`

   * 세부 요소에 추가할 모든 XML 요소에 대해 마지막 하위 단계를 반복합니다. 구매 주문서 양식을 채우는 데 사용되는 XML 데이터 소스를 올바르게 만들려면 다음 XML 요소를 세부 사항 요소에 추가해야 합니다.`txtDescription`, `numQty` 및 `numUnitPrice`.
   * 양식을 미리 채우는 데 사용된 모든 데이터 항목에 대해 마지막 2개의 하위 단계를 반복합니다.

1. XML 데이터 소스 변환

   * `javax.xml.transform.Transformer` 객체의 정적 `newInstance` 메서드를 호출하여 `javax.xml.transform.Transformer` 객체를 만듭니다.
   * `TransformerFactory` 객체의 `newTransformer` 메서드를 호출하여 `Transformer` 객체를 만듭니다.
   * 생성자를 사용하여 `ByteArrayOutputStream` 객체를 만듭니다.
   * 생성자를 사용하여 1단계에서 만든 `org.w3c.dom.Document` 개체를 전달하여 `javax.xml.transform.dom.DOMSource` 개체를 만듭니다.
   * 생성자를 사용하여 `javax.xml.transform.dom.DOMSource` 개체를 만들고 `ByteArrayOutputStream` 개체를 전달합니다.
   * `javax.xml.transform.Transformer` 개체의 `transform` 메서드를 호출하고 `javax.xml.transform.dom.DOMSource` 및 `javax.xml.transform.stream.StreamResult` 개체를 전달하여 Java `ByteArrayOutputStream` 개체를 채웁니다.
   * 바이트 배열을 만들고 `ByteArrayOutputStream` 객체의 크기를 바이트 배열에 할당합니다.
   * `ByteArrayOutputStream` 객체의 `toByteArray` 메서드를 호출하여 바이트 배열을 채웁니다.
   * 생성자를 사용하여 바이트 배열을 전달하여 `com.adobe.idp.Document` 객체를 만듭니다.

1. 미리 채워진 양식 렌더링

   `FormsServiceClient` 객체의 `renderPDFForm` 메서드를 호출하고 다음 값을 전달합니다.

   * 파일 이름 확장자를 포함하여 양식 디자인 이름을 지정하는 문자열 값입니다.
   * 양식과 병합할 데이터가 포함된 `com.adobe.idp.Document` 개체 1단계와 2단계에서 만든 `com.adobe.idp.Document` 개체를 사용해야 합니다.
   * 런타임 옵션을 저장하는 `PDFFormRenderSpec` 객체입니다.
   * Forms 서비스에 필요한 URI 값이 포함된 `URLSpec` 객체입니다.
   * 첨부 파일을 저장하는 `java.util.HashMap` 객체입니다. 이 매개 변수는 선택 사항이며, 양식에 파일을 첨부하지 않으려면 `null`을 지정할 수 있습니다.

   `renderPDFForm` 메서드는 클라이언트 웹 브라우저에 작성해야 하는 양식 데이터 스트림을 포함하는 `FormsResult` 객체를 반환합니다.

   * 양식 데이터 스트림을 클라이언트 웹 브라우저에 보내는 데 사용되는 `javax.servlet.ServletOutputStream` 개체를 만듭니다.
   * `FormsResult` 개체 &#39;s `getOutputContent` 메서드를 호출하여 `com.adobe.idp.Document` 개체를 만듭니다.
   * `com.adobe.idp.Document` 객체의 `getInputStream` 메서드를 호출하여 `java.io.InputStream` 객체를 만듭니다.
   * 바이트 배열을 만들어 `InputStream` 객체의 `read` 메서드를 호출하고 바이트 배열을 인수로 전달하여 양식 데이터 스트림으로 채웁니다.
   * 양식 데이터 스트림을 클라이언트 웹 브라우저에 보내려면 `javax.servlet.ServletOutputStream` 객체의 `write` 메서드를 호출합니다. 바이트 배열을 `write` 메서드에 전달합니다.


**참고 항목**

[빠른 시작(SOAP 모드):Java API를 사용하여 Forms에 플로우 가능한 레이아웃 미리 채우기](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-prepopulating-forms-with-flowable-layouts-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API {#prepopulating-forms-using-the-web-service-api}을(를) 사용하여 양식 미리 채우기

Forms API(웹 서비스)를 사용하여 플로우 가능한 레이아웃으로 양식을 미리 채우려면 다음 단계를 수행하십시오.

1. 프로젝트 파일 포함

   * Forms 서비스 WSDL을 사용하는 Java 프록시 클래스를 만듭니다. (Apache Axis](/help/forms/developing/invoking-aem-forms-using-web.md#creating-java-proxy-classes-using-apache-axis)를 사용하여 Java 프록시 클래스 만들기를 참조하십시오.)[
   * 클래스 경로에 Java 프록시 클래스를 포함합니다.

1. 메모리 내 XML 데이터 소스 만들기

   * `DocumentBuilderFactory` 클래스&#39; `newInstance` 메서드를 호출하여 Java `DocumentBuilderFactory` 개체를 만듭니다.
   * `DocumentBuilderFactory` 개체의 `newDocumentBuilder` 메서드를 호출하여 Java `DocumentBuilder` 개체를 만듭니다.
   * `DocumentBuilder` 개체의 `newDocument` 메서드를 호출하여 `org.w3c.dom.Document` 개체를 인스턴스화합니다.
   * `org.w3c.dom.Document` 객체의 `createElement` 메서드를 호출하여 XML 데이터 소스의 루트 요소를 만듭니다. 루트 요소를 나타내는 `Element` 객체가 만들어집니다. 요소의 이름을 나타내는 문자열 값을 `createElement` 메서드에 전달합니다. 반환 값을 `Element`으로 캐스팅합니다. 그런 다음 `Document` 객체의 `appendChild` 메서드를 호출하여 루트 요소를 문서에 추가하고 루트 요소 객체를 인수로 전달합니다. 다음 코드 행은 이 응용 프로그램 논리를 보여 줍니다.

      ` Element root = (Element)document.createElement("transaction");  document.appendChild(root);`

   * `Document` 객체의 `createElement` 메서드를 호출하여 XML 데이터 소스의 헤더 요소를 만듭니다. 요소의 이름을 나타내는 문자열 값을 `createElement` 메서드에 전달합니다. 반환 값을 `Element`으로 캐스팅합니다. 그런 다음 `root` 객체의 `appendChild` 메서드를 호출하여 헤더 요소를 루트 요소에 추가하고 머리글 요소 객체를 인수로 전달합니다. 헤더 요소에 추가되는 XML 요소는 양식의 정적 부분에 해당합니다. 다음 코드 행은 이 응용 프로그램 논리를 보여 줍니다.

      ` Element header = (Element)document.createElement("header");  root.appendChild(header);`

   * `Document` 객체의 `createElement` 메서드를 호출하여 헤더 요소에 속하는 자식 요소를 만들고 요소의 이름을 나타내는 문자열 값을 전달합니다. 반환 값을 `Element`으로 캐스팅합니다. 그런 다음 `appendChild` 메서드를 호출하여 자식 요소의 값을 설정하고 `Document` 객체의 `createTextNode` 메서드를 인수로 전달합니다. 하위 요소의 값으로 나타나는 문자열 값을 지정합니다. 마지막으로, 헤더 요소의 `appendChild` 메서드를 호출하여 하위 요소를 헤더 요소에 추가하고 자식 요소 객체를 인수로 전달합니다. 다음 코드 행은 이 응용 프로그램 논리를 보여 줍니다.

      ` Element poNum= (Element)document.createElement("txtPONum");  poNum.appendChild(document.createTextNode("8745236985"));  header.appendChild(LastName);`

   * 양식의 정적 부분에 나타나는 각 필드에 대한 마지막 하위 단계를 반복하여 나머지 모든 요소를 헤더 요소에 추가합니다(XML 데이터 소스 다이어그램에서 이러한 필드는 섹션 A에 표시됩니다. [데이터 하위 그룹 이해](#understanding-data-subgroups) 참조).
   * `Document` 객체의 `createElement` 메서드를 호출하여 XML 데이터 소스의 세부 사항 요소를 만듭니다. 요소의 이름을 나타내는 문자열 값을 `createElement` 메서드에 전달합니다. 반환 값을 `Element`으로 캐스팅합니다. 그런 다음 `root` 객체의 `appendChild` 메서드를 호출하여 세부 사항 요소를 루트 요소에 추가하고 detail 요소 객체를 인수로 전달합니다. 세부 사항 요소에 추가되는 XML 요소는 양식의 동적 부분에 해당합니다. 다음 코드 행은 이 응용 프로그램 논리를 보여 줍니다.

      ` Element detail = (Element)document.createElement("detail");  root.appendChild(detail);`

   * `Document` 객체의 `createElement` 메서드를 호출하여 세부 요소에 속하는 하위 요소를 만들고 요소의 이름을 나타내는 문자열 값을 전달합니다. 반환 값을 `Element`으로 캐스팅합니다. 그런 다음 `appendChild` 메서드를 호출하여 자식 요소의 값을 설정하고 `Document` 객체의 `createTextNode` 메서드를 인수로 전달합니다. 하위 요소의 값으로 나타나는 문자열 값을 지정합니다. 마지막으로, detail 요소의 `appendChild` 메서드를 호출하여 하위 요소를 detail 요소에 추가하고 자식 요소 객체를 인수로 전달합니다. 다음 코드 행은 이 응용 프로그램 논리를 보여 줍니다.

      ` Element txtPartNum = (Element)document.createElement("txtPartNum");  txtPartNum.appendChild(document.createTextNode("00010-100"));  detail.appendChild(txtPartNum);`

   * 세부 요소에 추가할 모든 XML 요소에 대해 마지막 하위 단계를 반복합니다. 구매 주문서 양식을 채우는 데 사용되는 XML 데이터 소스를 올바르게 만들려면 다음 XML 요소를 세부 사항 요소에 추가해야 합니다.`txtDescription`, `numQty` 및 `numUnitPrice`.
   * 양식을 미리 채우는 데 사용된 모든 데이터 항목에 대해 마지막 2개의 하위 단계를 반복합니다.

1. XML 데이터 소스 변환

   * `javax.xml.transform.Transformer` 객체의 정적 `newInstance` 메서드를 호출하여 `javax.xml.transform.Transformer` 객체를 만듭니다.
   * `TransformerFactory` 객체의 `newTransformer` 메서드를 호출하여 `Transformer` 객체를 만듭니다.
   * 생성자를 사용하여 `ByteArrayOutputStream` 객체를 만듭니다.
   * 생성자를 사용하여 1단계에서 만든 `org.w3c.dom.Document` 개체를 전달하여 `javax.xml.transform.dom.DOMSource` 개체를 만듭니다.
   * 생성자를 사용하여 `javax.xml.transform.dom.DOMSource` 개체를 만들고 `ByteArrayOutputStream` 개체를 전달합니다.
   * `javax.xml.transform.Transformer` 개체의 `transform` 메서드를 호출하고 `javax.xml.transform.dom.DOMSource` 및 `javax.xml.transform.stream.StreamResult` 개체를 전달하여 Java `ByteArrayOutputStream` 개체를 채웁니다.
   * 바이트 배열을 만들고 `ByteArrayOutputStream` 객체의 크기를 바이트 배열에 할당합니다.
   * `ByteArrayOutputStream` 객체의 `toByteArray` 메서드를 호출하여 바이트 배열을 채웁니다.
   * 생성자를 사용하여 `BLOB` 객체를 만들고 해당 `setBinaryData` 메서드를 호출하고 바이트 배열을 전달합니다.

1. 미리 채워진 양식 렌더링

   `FormsService` 객체의 `renderPDFForm` 메서드를 호출하고 다음 값을 전달합니다.

   * 파일 이름 확장자를 포함하여 양식 디자인 이름을 지정하는 문자열 값입니다.
   * 양식과 병합할 데이터가 포함된 `BLOB` 개체 1단계와 2단계에서 만든 `BLOB` 개체를 사용해야 합니다.
   * 런타임 옵션을 저장하는 `PDFFormRenderSpecc` 객체입니다. 자세한 내용은 [AEM Forms API 참조](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)를 참조하십시오.
   * Forms 서비스에 필요한 URI 값이 포함된 `URLSpec` 객체입니다.
   * 첨부 파일을 저장하는 `java.util.HashMap` 객체입니다. 이 매개 변수는 선택 사항이며, 양식에 파일을 첨부하지 않으려면 `null`을 지정할 수 있습니다.
   * 메서드에 의해 채워지는 빈 `com.adobe.idp.services.holders.BLOBHolder` 객체입니다. 렌더링된 PDF 양식을 저장하는 데 사용됩니다.
   * 메서드에 의해 채워지는 빈 `javax.xml.rpc.holders.LongHolder` 객체입니다. 이 인수는 양식의 페이지 수를 저장합니다.
   * 메서드에 의해 채워지는 빈 `javax.xml.rpc.holders.StringHolder` 객체입니다. 이 인수는 로케일 값을 저장합니다.
   * 이 작업의 결과를 포함할 빈 `com.adobe.idp.services.holders.FormsResultHolder` 객체입니다.

   `renderPDFForm` 메서드는 클라이언트 웹 브라우저에 작성해야 하는 양식 데이터 스트림으로 마지막 인수 값으로 전달되는 `com.adobe.idp.services.holders.FormsResultHolder` 객체를 채웁니다.

   * `com.adobe.idp.services.holders.FormsResultHolder` 개체의 `value` 데이터 멤버의 값을 가져와 `FormResult` 개체를 만듭니다.
   * `FormsResult` 개체의 `getOutputContent` 메서드를 호출하여 양식 데이터를 포함하는 `BLOB` 개체를 만듭니다.
   * `getContentType` 메서드를 호출하여 `BLOB` 객체의 내용 유형을 가져옵니다.
   * `setContentType` 메서드를 호출하고 `BLOB` 개체의 내용 유형을 전달하여 `javax.servlet.http.HttpServletResponse` 개체의 내용 유형을 설정합니다.
   * `javax.servlet.http.HttpServletResponse` 개체의 `getOutputStream` 메서드를 호출하여 양식 데이터 스트림을 클라이언트 웹 브라우저에 쓰는 데 사용되는 `javax.servlet.ServletOutputStream` 개체를 만듭니다.
   * 바이트 배열을 만들고 `BLOB` 객체의 `getBinaryData` 메서드를 호출하여 채웁니다. 이 작업은 바이트 배열에 `FormsResult` 객체의 내용을 할당합니다.
   * 양식 데이터 스트림을 클라이언트 웹 브라우저에 보내려면 `javax.servlet.http.HttpServletResponse` 객체의 `write` 메서드를 호출합니다. 바이트 배열을 `write` 메서드에 전달합니다.

   >[!NOTE]
   >
   >`renderPDFForm` 메서드는 클라이언트 웹 브라우저에 작성해야 하는 양식 데이터 스트림으로 마지막 인수 값으로 전달되는 `com.adobe.idp.services.holders.FormsResultHolder` 객체를 채웁니다.

**참고 항목**

[Base64 인코딩을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

