---
title: XML 스키마를 사용하여 적응형 양식 만들기
seo-title: XML 스키마를 사용하여 적응형 양식 만들기
description: 적응형 양식에서 XML 스키마를 양식 모델로 사용할 수 있으므로 기존 XSD 템플릿을 활용하여 적응형 양식을 만들 수 있습니다. XSD의 스키마 요소를 적응형 양식으로 드래그하여 놓을 수 있습니다.
seo-description: 적응형 양식에서 XML 스키마를 양식 모델로 사용할 수 있으므로 기존 XSD 템플릿을 활용하여 적응형 양식을 만들 수 있습니다. XSD의 스키마 요소를 적응형 양식으로 드래그하여 놓을 수 있습니다.
uuid: 84c35728-1b6c-4286-854b-51c03bfd0eac
topic-tags: develop
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 0d6c12b3-3a70-48e9-a83b-974360a8b0b6
docset: aem65
translation-type: tm+mt
source-git-commit: 4ecf5efc568cd21f11801a71d491c3d75ca367fe
workflow-type: tm+mt
source-wordcount: '1081'
ht-degree: 5%

---


# XML 스키마{#creating-adaptive-forms-using-xml-schema}를 사용하여 응용 양식 만들기

## 전제 조건 {#prerequisites}

XML 스키마를 양식 모델로 사용하여 적응형 양식을 작성하려면 XML 스키마에 대한 기본적인 이해가 필요합니다. 또한 이 아티클 이전에 다음 내용을 읽는 것이 좋습니다.

* [응용 양식 만들기](../../forms/using/creating-adaptive-form.md)
* [XML 스키마](https://www.w3.org/TR/xmlschema-2/)

## XML 스키마를 양식 모델 {#using-an-xml-schema-as-form-model}으로 사용

AEM Forms은 기존 XML 스키마를 양식 모델로 사용하여 적응형 양식 작성을 지원합니다. 이 XML 스키마는 조직의 백엔드 시스템에서 데이터를 생성하거나 사용하는 구조를 나타냅니다.

XML 스키마 사용의 주요 기능은 다음과 같습니다.

* XSD의 구조는 적응형 양식의 작성 모드에서 컨텐츠 파인더 탭에 트리로 표시됩니다. XSD 계층의 요소를 응용 양식으로 드래그하여 추가할 수 있습니다.
* 연결된 스키마를 준수하는 XML을 사용하여 양식을 미리 채울 수 있습니다.
* 제출 시 사용자가 입력한 데이터가 관련 스키마에 맞는 XML로 제출됩니다.

XML 스키마는 간단하고 복잡한 요소 유형으로 구성됩니다. 요소에는 요소에 규칙을 추가하는 속성이 있습니다. 이러한 요소와 속성을 적응형 양식으로 드래그하면 해당 적응형 양식 구성 요소에 자동으로 매핑됩니다.

적응형 양식 구성 요소가 있는 XML 요소의 매핑은 다음과 같습니다.

<table>
 <tbody>
  <tr>
   <th><strong>XML 요소 또는 특성 </strong></th>
   <th><strong>적응형 양식 구성 요소</strong></th>
  </tr>
  <tr>
   <td><code>xs:string</code></td>
   <td>텍스트 상자</td>
  </tr>
  <tr>
   <td><code>xs:boolean</code></td>
   <td>확인란</td>
  </tr>
  <tr>
   <td>
    <ul>
     <li><code>xs:unsignedInt</code></li>
     <li><code>xs:xs:int</code></li>
     <li><code class="code">xs:decimal
        </code></li>
     <li>모든 유형의 숫자 값</li>
    </ul> </td>
   <td>숫자 상자</td>
  </tr>
  <tr>
   <td><code>xs:date</code></td>
   <td>날짜 선택</td>
  </tr>
  <tr>
   <td><code class="code">xs:enumeration
      </code></td>
   <td>드롭다운</td>
  </tr>
  <tr>
   <td>모든 복합 유형 요소</td>
   <td>패널</td>
  </tr>
 </tbody>
</table>

## 샘플 XML 스키마 {#sample-xml-schema}

다음은 XML 스키마의 예입니다.

```xml
<?xml version="1.0" encoding="utf-8" ?>
    <xs:schema targetNamespace="https://adobe.com/sample.xsd"
                    xmlns="https://adobe.com/sample.xsd"
                    xmlns:xs="https://www.w3.org/2001/XMLSchema"
                >

        <xs:element name="sample" type="SampleType"/>

        <xs:complexType name="SampleType">
            <xs:sequence>
                <xs:element name="leaderName" type="xs:string" default="Enter Name"/>
                <xs:element name="assignmentStartBirth" type="xs:date"/>
                <xs:element name="gender" type="GenderEnum"/>
                <xs:element name="noOfProjectsAssigned" type="IntType"/>
                <xs:element name="assignmentDetails" type="AssignmentDetails"
                                            minOccurs="0" maxOccurs="10"/>
            </xs:sequence>
        </xs:complexType>

        <xs:complexType name="AssignmentDetails">
            <xs:attribute name="name" type="xs:string" use="required"/>
            <xs:attribute name="durationOfAssignment" type="xs:unsignedInt" use="required"/>
            <xs:attribute name="numberOfMentees" type="xs:unsignedInt" use="required"/>
             <xs:attribute name="descriptionOfAssignment" type="xs:string" use="required"/>
             <xs:attribute name="financeRelatedProject" type="xs:boolean"/>
       </xs:complexType>
  <xs:simpleType name="IntType">
            <xs:restriction base="xs:int">
            </xs:restriction>
        </xs:simpleType>
  <xs:simpleType name="GenderEnum">
            <xs:restriction base="xs:string">
                <xs:enumeration value="Female"/>
                <xs:enumeration value="Male"/>
            </xs:restriction>
        </xs:simpleType>
    </xs:schema>
```

>[!NOTE]
>
>XML 스키마에 루트 요소가 하나만 있는지 확인합니다. 둘 이상의 루트 요소가 있는 XML 스키마가 지원되지 않습니다.

## XML 스키마 {#adding-special-properties-to-fields-using-xml-schema}을(를) 사용하여 필드에 특수 속성 추가

XML 스키마 요소에 다음 속성을 추가하여 관련 적응형 양식의 필드에 특수 속성을 추가할 수 있습니다.

<table>
 <tbody>
  <tr>
   <th><strong>스키마 속성</strong></th>
   <th><strong>적응형 양식으로 사용</strong></th>
   <th><strong>지원되는 위치 </strong></th>
  </tr>
  <tr>
   <td><code>use=required </code></td>
   <td>필수 필드 표시<br /> </td>
   <td>특성</td>
  </tr>
  <tr>
   <td><code>default="default value"</code></td>
   <td>기본값 추가</td>
   <td>요소 및 속성</td>
  </tr>
  <tr>
   <td><code>minOccurs="3"</code></td>
   <td><p>최소 발생 수 지정</p> <p>(반복 가능한 하위 양식(복잡한 유형)</p> </td>
   <td>요소(복잡한 유형)</td>
  </tr>
  <tr>
   <td><code class="code">maxOccurs="10"
      </code></td>
   <td><p>최대 발생 수 지정</p> <p>(반복 가능한 하위 양식(복잡한 유형)</p> </td>
   <td>요소(복잡한 유형)</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>스키마 요소를 응용 양식으로 드래그하면 다음과 같은 방식으로 기본 캡션이 생성됩니다.
>
>* 요소 이름의 첫 문자 대문자
>* 카멜 케이스 경계선에 흰색 공간 삽입

>
>
예를 들어 `userFirstName` 스키마 요소를 추가하는 경우 적응형 양식에서 생성된 캡션은 `User First Name`입니다.

## 응용 양식 구성 요소 {#limit-acceptable-values-for-an-adaptive-form-component}에 사용할 수 있는 값 제한

적응형 양식 구성 요소에 허용되는 값을 제한하기 위해 XML 스키마 요소에 다음 제한 사항을 추가할 수 있습니다.

<table>
 <tbody>
  <tr>
   <td><p><strong> 스키마 속성</strong></p> </td>
   <td><p><strong>데이터 유형</strong></p> </td>
   <td><p><strong>설명</strong></p> </td>
   <td><p><strong>구성 요소</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>totalDigits</code></p> </td>
   <td><p>문자열</p> </td>
   <td><p>구성 요소에 허용되는 최대 숫자 수를 지정합니다. 지정된 자릿수는 0보다 커야 합니다.</p> </td>
   <td>
    <ul>
     <li>숫자 상자</li>
     <li>숫자 스텝퍼</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>maximum</code></p> </td>
   <td><p>문자열</p> </td>
   <td><p>숫자 값과 날짜에 대한 상한을 지정합니다. 기본적으로 최대값이 포함됩니다.</p> </td>
   <td>
    <ul>
     <li>숫자 상자</li>
     <li>숫자 스텝퍼<br /> </li>
     <li>날짜 선택</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>minimum</code></p> </td>
   <td><p>문자열</p> </td>
   <td><p>숫자 값과 날짜에 대해 하한 값을 지정합니다. 기본적으로 최소값이 포함됩니다.</p> </td>
   <td>
    <ul>
     <li>숫자 상자</li>
     <li>숫자 스텝퍼</li>
     <li>날짜 선택</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>exclusiveMaximum</code></p> </td>
   <td><p>부울</p> </td>
   <td><p>true이면 양식의 구성 요소에 지정된 숫자 값 또는 날짜가 최대 속성에 지정된 숫자 값 또는 날짜보다 작아야 합니다.</p> <p>false인 경우 양식의 구성 요소에 지정된 숫자 값 또는 날짜는 최대 속성에 지정된 숫자 값 또는 날짜보다 작거나 같아야 합니다.</p> </td>
   <td>
    <ul>
     <li>숫자 상자</li>
     <li>숫자 스텝퍼</li>
     <li>날짜 선택</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>exclusiveMinimum</code></p> </td>
   <td><p>부울</p> </td>
   <td><p>true이면 양식의 구성 요소에 지정된 숫자 값 또는 날짜가 최소 속성에 지정된 숫자 값 또는 날짜보다 커야 합니다.</p> <p>false인 경우 양식의 구성 요소에 지정된 숫자 값 또는 날짜는 최소 속성에 지정된 숫자 값 또는 날짜보다 크거나 같아야 합니다.</p> </td>
   <td>
    <ul>
     <li>숫자 상자</li>
     <li>숫자 스텝퍼</li>
     <li>날짜 선택</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>minLength</code></p> </td>
   <td><p>문자열</p> </td>
   <td><p>구성 요소에 허용되는 최소 문자 수를 지정합니다. 최소 길이는 0보다 크거나 같아야 합니다.</p> </td>
   <td>
    <ul>
     <li>텍스트 상자</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>maxLength</code></p> </td>
   <td><p>문자열</p> </td>
   <td><p>구성 요소에 허용되는 최대 문자 수를 지정합니다. 최대 길이는 0보다 커야 합니다.</p> </td>
   <td>
    <ul>
     <li>텍스트 상자</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>length</code></p> </td>
   <td><p>문자열</p> </td>
   <td><p>구성 요소에 허용되는 정확한 문자 수를 지정합니다. 길이는 0보다 크거나 같아야 합니다.</p> </td>
   <td>
    <ul>
     <li>텍스트 상자</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>fractionDigits</code></p> </td>
   <td><p>문자열</p> </td>
   <td><p>구성 요소에 허용되는 최대 소수 자릿수를 지정합니다. fractionDigits는 0보다 크거나 같아야 합니다.</p> </td>
   <td>
    <ul>
     <li> 데이터 유형이 부동 또는 소수인 숫자 상자</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>pattern</code></p> </td>
   <td><p>문자열</p> </td>
   <td><p>문자 시퀀스를 지정합니다. 구성 요소는 문자가 지정된 패턴을 따르는 경우 문자를 허용합니다.</p> <p>패턴 속성은 해당 응용 양식 구성 요소의 유효성 검사 패턴에 매핑됩니다.</p> </td>
   <td>
    <ul>
     <li>XSD 스키마에 매핑된 모든 응용 양식 구성 요소 </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## FAQ {#frequently-asked-questions}

**트리의 어떤 요소가 어떤 XML 요소와 연관되어 있는지 어떻게 알 수 있습니까?**

Content Finder에서 요소를 두 번 클릭하면 팝업에는 필드 이름과 `bindRef`이라는 속성이 표시됩니다. 이 속성은 트리 요소를 스키마의 요소 또는 특성에 매핑합니다.

![XML 스키마 요소의 이진 필드](assets/dblclick.png)

bindRef</code> 필드는 스키마의 트리 요소와 요소 또는 특성 간의 연결을 표시합니다.

>[!NOTE]
>
>속성에 `bindRef`값에 `@` 기호가 있으므로 요소와 구별됩니다. 예, `/config/projectDetails/@duration`.

**반복 가능한 하위 폼(minOccours 또는 maxOccurs 값이 1보다 큼)에 대해 하위 폼의 개별 요소(복잡한 형식에서 생성된 구조)를 드래그할 수 없는 이유는 무엇입니까?**

반복 가능한 하위 양식에서는 전체 하위 양식을 사용해야 합니다. 선택적 필드만 원하는 경우 전체 구조를 사용하고 원하지 않는 필드를 삭제합니다.

**Content Finder에는 구조가 매우 복잡합니다. 특정 요소를 어떻게 찾을 수 있습니까?**

두 가지 옵션이 있습니다.

* 트리 구조를 스크롤합니다.
* 검색 상자를 사용하여 요소 찾기

**bindRef 소개**

`bindRef`은 적응형 양식 구성 요소와 스키마 요소 또는 특성 간의 연결입니다. 출력 XML에서 이 구성 요소나 필드에서 캡처된 값을 사용할 수 있는 `XPath`이 지시됩니다. `bindRef`은 미리 입력(미리 채우기) XML에서 필드 값을 미리 채울 때도 사용됩니다.
