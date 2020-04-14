---
title: 적응형 양식 필드 미리 채우기
seo-title: 적응형 양식 필드 미리 채우기
description: 기존 데이터를 사용하여 적응형 양식의 필드를 미리 채웁니다.
seo-description: 적응형 양식을 사용하면 사용자가 소셜 프로필로 로그인하여 양식의 기본 정보를 미리 채울 수 있습니다. 이 문서에서는 이 작업을 수행하는 방법에 대해 설명합니다.
uuid: 574de83a-7b5b-4a1f-ad37-b9717e5c14f1
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 7139a0e6-0e37-477c-9e0b-aa356991d040
docset: aem65
translation-type: tm+mt
source-git-commit: 49da3dbe590f70b98185a6bc330db6077dc864c0

---


# 적응형 양식 필드 미리 채우기{#prefill-adaptive-form-fields}

## 소개 {#introduction}

기존 데이터를 사용하여 적응형 양식의 필드를 미리 채울 수 있습니다. 사용자가 양식을 열면 해당 필드에 대한 값이 미리 채워집니다. 적응형 양식의 데이터를 미리 채우려면 사용자 데이터를 적응형 양식의 데이터 구조를 미리 채우기 방식으로 자동 채우기 XML/JSON으로 사용할 수 있도록 하십시오.

## 프리필 데이터 구조 {#the-prefill-structure}

적응형 양식에는 바운드 필드와 언바운드 필드가 혼합되어 있을 수 있습니다. 바운드 필드는 Content Finder 탭에서 드래그하고 필드 편집 대화 상자에 비어 있지 않은 `bindRef` 속성 값을 포함하는 필드입니다. 바인딩되지 않은 필드는 사이드 킥의 구성 요소 브라우저에서 바로 드래그되며 빈 `bindRef` 값이 있습니다.

적응형 양식의 바운드 필드와 언바운드 필드를 모두 미리 채울 수 있습니다. 자동 완성 데이터에는 aBoundData 및 afUnBoundData 섹션이 포함되어 있어 적응형 양식의 바운드 필드와 바인딩되지 않은 필드를 모두 미리 채웁니다. 이 `afBoundData` 섹션에는 바운드 필드 및 패널에 대한 프리필 데이터가 포함되어 있습니다. 이 데이터는 연결된 양식 모델 스키마와 호환되어야 합니다.

* XFA 양식 템플릿을 [사용하는 적응형 양식의](../../forms/using/prepopulate-adaptive-form-fields.md)경우 XFA 템플릿의 데이터 스키마를 준수하는 프리필 XML을 사용합니다.
* XML 스키마를 사용하는 적응형 [양식의](#xml-schema-af)경우 XML 스키마 구조를 준수하는 프리필 XML을 사용합니다.
* JSON 스키마를 사용하는 적응형 [양식의](#json-schema-based-adaptive-forms)경우 JSON 스키마를 준수하는 프리필 JSON을 사용하십시오.
* FDM 스키마를 사용하는 적응형 양식의 경우 FDM 스키마와 호환되는 프리필 JSON을 사용합니다.
* 양식 모델이 [없는 적응형 양식의](#adaptive-form-with-no-form-model)경우 바인딩된 데이터가 없습니다. 모든 필드는 언바운드 필드이며 언바운드 XML을 사용하여 프리필됩니다.

### 샘플 프리필 XML 구조 {#sample-prefill-xml-structure}

```xml
<?xml version="1.0" encoding="UTF-8"?>
<afData>
  <afBoundData>
     <employeeData>
        .
     </employeeData>
  </afBoundData>

  <afUnboundData>
    <data>
      <textbox>Hello World</textbox>
         .
         .
      <numericbox>12</numericbox>
         . 
         .              
    </data>
  </afUnboundData>
</afData>
```

### 샘플 프리필 JSON 구조 {#sample-prefill-json-structure}

```
{
   "afBoundData": {
      "employeeData": { }
   },
   "afUnboundData": {
      "data": {
         "textbox": "Hello World",
         "numericbox": "12"
      }
   }
}
```

이름이 같은 바인드레이 또는 언바운드 필드의 경우 XML 태그 또는 JSON 개체에 지정된 데이터가 모든 필드에 채워집니다. 예를 들어, 양식의 두 필드가 미리 채우기 데이터의 이름에 매핑됩니다. `textbox` 런타임 중에 첫 번째 텍스트 상자 필드에 &quot;A&quot;가 포함되어 있으면 두 번째 텍스트 상자에 &quot;A&quot;가 자동으로 채워집니다. 이 연결을 응용 양식 필드의 라이브 링크라고 합니다.

### XFA 양식 템플릿을 사용한 적응형 양식 {#xfa-based-af}

XFA 기반 적응형 양식의 자동 완성 XML 및 제출된 XML의 구조는 다음과 같습니다.

* **XML 구조 미리 채우기**:XFA 기반 응용 양식용 자동 채우기 XML은 XFA 양식 템플릿의 데이터 스키마를 따라야 합니다. 언바운드 필드를 프리필하려면 XML 구조를 `/afData/afBoundData` 태그로 둘러싸십시오.

* **제출된 XML 구조**:XML 프리플라이트 기능을 사용하지 않으면 제출된 XML에 `afData` 래퍼 태그의 바운드 필드와 언바운드 필드 모두에 대한 데이터가 포함됩니다. XML을 프리플라이트 사용하는 경우 제출된 XML의 구조는 미리 채우기 XML과 동일합니다. XML 프리플라이트 시 `afData` 루트 태그로 시작하는 경우 출력 XML의 형식도 동일합니다. 프리플라이트 XML에 `afData/afBoundData`래퍼가 없고 대신 스키마 루트 태그에서 바로 시작하는 `employeeData`경우 제출된 XML도 `employeeData` 태그로 시작합니다.

Prefill-Submit-Data-ContentPackage.zip

[Get File](assets/prefill-submit-data-contentpackage.zip)Sample containing prefill data and submitted data

### XML 스키마 기반의 적응형 양식 {#xml-schema-af}

XML 스키마를 기반으로 적응형 양식을 위해 XML을 프리플라이트 및 제출한 XML의 구조는 다음과 같습니다.

* **XML 구조**&#x200B;자동 채우기:프리필 XML은 연결된 XML 스키마와 호환되어야 합니다. 언바운드 필드를 미리 채우려면 XML 구조를 /afData/afBoundData 태그로 둘러싸십시오.
* **제출된 XML 구조**:prefill XML을 사용하지 않는 경우 제출된 XML에는 `afData` 래퍼 태그의 바운드 필드와 언바운드 필드 모두에 대한 데이터가 포함됩니다. XML 자동 완성 기능을 사용하는 경우 제출한 XML의 구조는 미리 채우기 XML과 동일합니다. XML 프리플라이트 시 `afData` 루트 태그로 시작하는 경우 출력 XML의 형식이 동일합니다. 프리플라이트 XML에 `afData/afBoundData` 래퍼가 없고 대신 스키마 루트 태그에서 바로 시작하면 `employeeData`제출된 XML도 `employeeData` 태그로 시작됩니다.

```xml
<?xml version="1.0" encoding="utf-8" ?> 
<xs:schema targetNamespace="https://adobe.com/sample.xsd"
            xmlns="https://adobe.com/sample.xsd"
            xmlns:xs="https://www.w3.org/2001/XMLSchema">
 
    <xs:element name="sample" type="SampleType"/>
         
    <xs:complexType name="SampleType">
        <xs:sequence>
            <xs:element name="noOfProjectsAssigned" type="xs:string"/>
        </xs:sequence>
    </xs:complexType>
</xs:schema>
```

모델이 XML 스키마인 필드의 경우 아래 샘플 XML에 표시된 대로 데이터가 `afBoundData` 태그에 프리펜드됩니다. 하나 이상의 언바운드 텍스트 필드를 사용하여 적응형 양식을 미리 작성하는 데 사용할 수 있습니다.

```xml
<?xml version="1.0" encoding="UTF-8"?><afData>
  <afUnboundData>
    <data>
      <textbox>Ignorance is bliss :) </textbox>
    </data>
  </afUnboundData>
  <afBoundData>
    <data>
      <noOfProjectsAssigned>twelve</noOfProjectsAssigned>
    </data>
  </afBoundData>
</afData>
```

>[!NOTE]
>
>바운드 패널(사이드 킥이나 데이터 소스 탭에서 구성 요소를 드래그하여 만든 비어 `bindRef` 있지 않은 패널)에서 언바운드 필드를 사용하지 않는 것이 좋습니다. 이로 인해 이러한 언바운드 필드의 데이터가 손실될 수 있습니다. 또한 필드의 이름은 언바운드 필드 전용으로 폼 전체에 적용되는 것이 좋습니다.

#### af 파섹 {#an-example-without-afdata-and-afbounddata-wrapper}

```xml
<?xml version="1.0" encoding="UTF-8"?><config>
 <assignmentDetails descriptionOfAssignment="Some Science Project" durationOfAssignment="34" financeRelatedProject="1" name="Lisa" numberOfMentees="1"/>
 <assignmentDetails descriptionOfAssignment="Kidding, right?" durationOfAssignment="4" financeRelatedProject="1" name="House" numberOfMentees="3"/>
</config>
```

### JSON 스키마 기반 적응형 양식 {#json-schema-based-adaptive-forms}

JSON 스키마를 기반으로 하는 적응형 양식의 경우, JSON과 제출된 JSON의 구조가 아래에 설명되어 있습니다. 자세한 내용은 JSON 스키마를 [사용하여 적응형 양식 만들기를 참조하십시오](../../forms/using/adaptive-form-json-schema-form-model.md).

* **JSON 구조**&#x200B;미리 채우기:프리필 JSON은 연결된 JSON 스키마를 준수해야 합니다. 필요에 따라 언바운드 필드도 미리 채우려면 /afData/afBoundData 개체에 래핑할 수 있습니다.
* **제출된 JSON 구조**:prefill JSON을 사용하지 않는 경우 제출된 JSON은 afData 래퍼 태그의 바운드 및 언바운드 필드 모두에 대한 데이터를 포함합니다. JSON의 프리플라이트 방식을 사용하는 경우 제출된 JSON의 구조는 미리 채우기 JSON과 동일합니다. prefill JSON이 afData 루트 객체로 시작하는 경우 출력 JSON의 형식이 동일합니다. prefill JSON에 afData/afBoundData 래퍼가 없고 대신 사용자와 같은 스키마 루트 개체에서 직접 시작되는 경우 제출된 JSON도 사용자 개체부터 시작됩니다.

```
{
    "id": "https://some.site.somewhere/entry-schema#",
    "$schema": "https://json-schema.org/draft-04/schema#",
    "type": "object",
    "properties": {
        "address": {
            "type": "object",
            "properties": { 
    "name": {
     "type": "string"
    },
    "age": {
     "type": "integer"
}}}}}
```

JSON 스키마 모델을 사용하는 필드의 경우 아래 샘플 JSON에 표시된 대로 데이터가 afBoundData 개체에서 프리필됩니다. 하나 이상의 언바운드 텍스트 필드를 사용하여 적응형 양식을 미리 작성하는 데 사용할 수 있습니다. 다음은 `afData/afBoundData` 래퍼와 관련된 데이터의 예입니다.

```
{
  "afData": {
    "afUnboundData": {
      "data": { "textbox": "Ignorance is bliss :) " }
    },
    "afBoundData": {
      "data": { {
   "user": {
    "address": {
     "city": "Noida",
     "country": "India"
}}}}}}}
```

다음은 `afData/afBoundData` 래퍼가 없는 예입니다.

```
{
 "user": {
  "address": {
   "city": "Noida",
   "country": "India"
}}}
```

>[!NOTE]
>
>바인딩되지 않은 필드(사이드 킥이나 데이터 소스 탭에서 구성 요소를 드래그하여 만든 비비어 있는 bindRef가 있는 패널)를 사용하면 바인딩되지 않은 필드의 데이터가 손실될 수 있으므로 사용하지 **않는** 것이 좋습니다. 특히 언바운드 필드의 경우 양식에 고유한 필드 이름을 지정하는 것이 좋습니다.

### 양식 모델이 없는 적응형 양식 {#adaptive-form-with-no-form-model}

양식 모델이 없는 적응형 양식의 경우 모든 필드의 데이터는 `<data>` 태그 아래에 `<afUnboundData> tag`있습니다.

또한 다음을 참고하십시오.

다양한 필드에 대해 제출된 사용자 데이터에 대한 XML 태그는 필드 이름을 사용하여 생성됩니다. 따라서 필드 이름은 고유해야 합니다.

```xml
<?xml version="1.0" encoding="UTF-8"?><afData>
  <afUnboundData>
    <data>
      <radiobutton>2</radiobutton>
      <repeatable_panel_no_form_model>
        <numericbox>12</numericbox>
      </repeatable_panel_no_form_model>
      <repeatable_panel_no_form_model>
        <numericbox>21</numericbox>
      </repeatable_panel_no_form_model>
      <checkbox>2</checkbox>
      <textbox>Nopes</textbox>
    </data>
  </afUnboundData>
  <afBoundData/>
</afData>
```

## Configuration Manager를 사용하여 미리 채우기 서비스 구성 {#configuring-prefill-service-using-configuration-manager}

자동 채우기 서비스를 활성화하려면 AEM 웹 콘솔 구성에서 기본 자동 채우기 서비스 구성을 지정합니다. Prefill 서비스를 구성하려면 다음 단계를 따르십시오.

>[!NOTE]
>
>자동 채우기 서비스 구성은 적응형 양식, HTML5 양식 및 HTML5 양식 세트에 적용됩니다.

1. URL **[!UICONTROL 을 사용하여 Adobe]** Experience Manager 웹 콘솔 구성을 엽니다.\
   https://&lt;server>:&lt;port>/system/console/configMgr
1. 기본 자동 채우기 **[!UICONTROL 서비스 구성을 검색하고 엽니다]**.

   ![구성 미리 채우기](assets/prefill_config_new.png)

1. 데이터 파일 위치에 **대한 데이터 위치 또는 정규식(정규식)을**&#x200B;입력합니다. 유효한 데이터 파일 위치의 예는 다음과 같습니다.

   * file:///C:/Users/public/Document/Prefill/.*
   * https://localhost:8000/somesamplexmlfile.xml
   >[!NOTE]
   >
   >기본적으로 모든 유형의 적응형 양식(XSD, XDP, JSON, FDM 및 양식 모델 없음)에 대해 crx 파일을 통해 프리필이 허용됩니다. 프리필은 JSON 및 XML 파일에서만 사용할 수 있습니다.

1. 이제 양식에 대해 자동 완성 서비스가 구성됩니다.

   >[!NOTE]
   >
   >crx 프로토콜은 자동 입력 데이터 보안을 사용하므로 기본적으로 허용됩니다. 일반 regex를 사용하여 다른 프로토콜을 통해 프리플링하면 취약성이 발생할 수 있습니다. 구성에서 데이터를 보호하기 위한 보안 URL 구성을 지정합니다.

## 반복 가능한 패널의 흥미로운 사례 {#the-curious-case-of-repeatable-panels}

일반적으로 바운드(양식 스키마) 및 언바운드 필드는 동일한 적응형 양식으로 작성되지만, 바운드가 반복 가능한 경우에 몇 가지 예외가 있습니다.

* 언바운드 반복 가능한 패널은 XFA 양식 템플릿, XSD, JSON 스키마 또는 FDM 스키마를 사용하는 적응형 양식에 대해 지원되지 않습니다.
* 바운드 반복 가능한 패널에 언바운드 필드를 사용하지 마십시오.

>[!NOTE]
>
>제어의 법칙으로서, 제본되지 않은 필드의 최종 사용자가 채운 데이터와 교차하는 경우 제본되지 않은 필드와 바인딩되지 않은 필드를 혼합하지 마십시오. 가능한 경우 스키마나 XFA 양식 템플릿을 수정하고 바인딩되지 않은 필드에 대한 항목을 추가해야 데이터를 제출된 데이터의 다른 필드와 마찬가지로 사용할 수 있습니다.

## 사용자 데이터 자동 입력을 위한 지원되는 프로토콜 {#supported-protocols-for-prefilling-user-data}

적응형 양식은 올바른 정규형으로 구성된 경우 다음 프로토콜을 통해 자동 채우기 데이터 형식의 사용자 데이터로 자동 입력 가능합니다.

### crx:// 프로토콜 {#the-crx-protocol}

```xml
https://localhost:4502/content/forms/af/xml.html?wcmmode=disabled&dataRef=crx:///tmp/fd/af/myassets/sample.xml
```

지정한 노드에는 호출된 속성이 `jcr:data` 있어야 하며 데이터를 보유해야 합니다.

### file:// 프로토콜 {#the-file-protocol-nbsp}

```xml
https://localhost:4502/content/forms/af/someAF.html?wcmmode=disabled&dataRef=file:///C:/Users/form-user/Downloads/somesamplexml.xml
```

참조된 파일은 동일한 서버에 있어야 합니다.

### https:// 프로토콜 {#the-http-protocol}

```xml
https://localhost:4502/content/forms/af/xml.html?wcmmode=disabled&dataRef=https://localhost:8000/somesamplexmlfile.xml
```

### service:// 프로토콜 {#the-service-protocol}

```xml
https://localhost:4502/content/forms/af/abc.html?wcmmode=disabled&dataRef=service://[SERVICE_NAME]/[IDENTIFIER]
```

* SERVICE_NAME은 OSGI 미리 채우기 서비스의 이름을 나타냅니다. 미리 [채우기 서비스](../../forms/using/prepopulate-adaptive-form-fields.md#create-and-run-a-prefill-service)만들기 및 실행을 참조하십시오.
* IDENTIFIER는 OSGI 미리 채우기 서비스에 필요한 메타데이터를 나타냅니다. 로그인한 사용자의 식별자는 사용할 수 있는 메타데이터의 예입니다.

>[!NOTE]
>
>인증 매개 변수 전달은 지원되지 않습니다.

### slingRequest에서 데이터 특성 설정 {#setting-data-attribute-in-slingrequest}

아래 샘플 코드와 같이 `data` 속성이 XML 또는 JSON을 포함하는 문자열인 `slingRequest``data` 에서 속성을 설정할 수도 있습니다(예: XML용).

```java
<%
           String dataXML="<afData>" +
                            "<afUnboundData>" +
                                "<data>" +
                                    "<first_name>"+ "Tyler" + "</first_name>" +
                                    "<last_name>"+ "Durden " + "</last_name>" +
                                    "<gender>"+ "Male" + "</gender>" +
                                    "<location>"+ "Texas" + "</location>" +
                                    "</data>" +
                            "</afUnboundData>" +
                        "</afData>";
        slingRequest.setAttribute("data", dataXML);
%>
```

모든 데이터가 포함된 간단한 XML 또는 JSON 문자열을 작성하여 slingRequest에서 설정할 수 있습니다. 이 작업은 slingRequest 데이터 속성을 설정할 수 있는 페이지에 포함하려는 모든 구성 요소에 대해 렌더러 JSP에서 쉽게 수행할 수 있습니다.

예를 들어 특정 유형의 헤더가 있는 페이지의 특정 디자인을 원할 경우 이를 위해 페이지 구성 요소에 포함할 수 `header.jsp`있는 사용자 고유의 속성을 작성할 수 `data` 있습니다.

다른 좋은 예는 Facebook, Twitter 또는 LinkedIn과 같은 소셜 계정을 통해 로그인 시 데이터를 미리 채우려는 사용 사례입니다. 이 경우 사용자 계정에서 데이터를 가져오고 데이터 매개 변수를 설정하는 간단한 JSP를 포함할 `header.jsp`수 있습니다.

prefill-page component.zip

[페이지 구성](assets/prefill-page-component.zip)요소의 Get File Sample prefill.jsp

## AEM Forms 사용자 정의 미리 채우기 서비스 {#aem-forms-custom-prefill-service}

사전 정의된 소스에서 데이터를 지속적으로 읽는 시나리오에 사용자 정의 자동 채우기 서비스를 사용할 수 있습니다. 자동 완성 서비스는 정의된 데이터 소스의 데이터를 읽고 자동 완성 데이터 파일의 내용으로 응용 양식 필드를 미리 채웁니다. 또한 프리플라이트 데이터를 적응형 양식과 영구히 연결할 수 있습니다.

### 자동 완성 서비스 만들기 및 실행 {#create-and-run-a-prefill-service}

프리플라이트 서비스는 OSGi 서비스이며 OSGi 번들을 통해 패키징됩니다. OSGi 번들을 만들고, 업로드하고, AEM Forms 번들에 설치합니다. 번들 제작을 시작하기 전에

* [AEM Forms 클라이언트 SDK 다운로드](https://helpx.adobe.com/kr/aem-forms/kb/aem-forms-releases.html)
* 상용구 패키지 다운로드

* crx-repository에 데이터(프리필 데이터) 파일을 배치합니다. crx-repository의 \contents 폴더에 있는 위치에 파일을 배치할 수 있습니다.

[파일 가져오기](assets/prefill-sumbit-xmlsandcontentpackage.zip)

#### 자동 완성 서비스 만들기 {#create-a-prefill-service}

상용구 패키지(샘플 프리필 서비스 패키지)에는 AEM Forms 프리필 서비스의 샘플 구현이 포함되어 있습니다. 코드 편집기에서 상용구 패키지를 엽니다. 예를 들어 Eclipse에서 상용구 프로젝트를 열어 편집할 수 있습니다. 코드 편집기에서 상용구 패키지를 연 후 다음 단계를 수행하여 서비스를 만듭니다.

1. 편집할 src\main\java\com\adobe\test\Prefill.java 파일을 엽니다.
1. 코드에서 다음 값을 설정합니다.

   * `nodePath:` crx-repository 위치를 가리키는 노드 경로 변수에는 데이터(프리필) 파일의 경로가 포함됩니다. 예: /content/prefilldata.xml
   * `label:` label 매개 변수는 서비스의 표시 이름을 지정합니다. 예를 들어 기본 미리 채우기 서비스

1. 파일을 저장하고 `Prefill.java` 닫습니다.
1. 상용구 `AEM Forms Client SDK` 프로젝트의 빌드 경로에 패키지를 추가합니다.
1. 프로젝트를 컴파일하고 번들의 .jar를 만듭니다.

#### 미리 채우기 서비스 시작 및 사용 {#start-and-use-the-prefill-service}

미리 채우기 서비스를 시작하려면 JAR 파일을 AEM Forms 웹 콘솔에 업로드하고 서비스를 활성화합니다. 이제 적응형 양식 편집기에 서비스가 나타납니다. 자동 채우기 서비스를 응용 양식에 연결하려면

1. 양식 편집기에서 적응형 양식을 열고 양식 컨테이너에 대한 속성 패널을 엽니다.
1. 속성 콘솔에서 AEM Forms 컨테이너 > 기본 > 자동 채우기 서비스로 이동합니다.
1. 기본 자동 완성 서비스를 선택하고 저장을 **[!UICONTROL 클릭합니다]**. 서비스가 양식과 연결됩니다.

