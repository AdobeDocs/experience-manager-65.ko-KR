---
title: 반복 가능한 섹션이 있는 양식 만들기
description: 반복 가능한 섹션은 양식에 동적으로 추가하거나 제거할 수 있는 패널입니다.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 01724ca0-6901-45e7-b045-f44814ed574e
feature: Adaptive Forms, Foundation Components
exl-id: f2abae0a-f7fd-4a39-bd8c-03492ce06fe9
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1139'
ht-degree: 4%

---

# 반복 가능한 섹션이 있는 양식 만들기 {#creating-forms-with-repeatable-sections}

<span class="preview"> [새 적응형 양식 만들기](/help/forms/using/create-an-adaptive-form-core-components.md) 또는 [AEM Sites 페이지에 적응형 양식 추가](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md) 작업을 할 때 현대적이고 확장 가능한 데이터 캡처 [핵심 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)를 사용하는 것이 좋습니다. 이러한 구성 요소는 적응형 양식 만들기 작업이 대폭 개선되어 우수한 사용자 경험을 보장할 수 있게 되었음을 나타냅니다. 이 문서에서는 기초 구성 요소를 사용하여 적응형 양식을 작성하는 이전 접근법에 대해 설명합니다. </span>

반복 가능한 섹션은 양식에 동적으로 추가하거나 제거할 수 있는 패널입니다.

예를 들어, 구직자는 구직에 지원하는 동안 상호, 역할, 프로젝트 및 기타 정보 등 이전의 취업 내역을 제공한다. 모든 고용주의 정보는 서로 다르지만 비슷한 모양의 섹션을 필요로 합니다. 이러한 시나리오에서 고용 양식은 고용주 섹션을 제공하고 이러한 섹션을 더 동적으로 추가하는 옵션도 제공합니다. 동적으로 추가되는 이러한 섹션을 반복 가능 섹션이라고 합니다.

다음 방법 중 하나를 사용하여 반복 가능한 패널을 만들 수 있습니다.

## 스크립트를 통해 인스턴스 관리자 사용  {#using-instance-manager-via-scripts-nbsp}

1. 편집 모드에서 패널을 선택한 다음 를 선택합니다 ![cmppr](assets/cmppr.png). 사이드바의 속성에서 **패널이 반복 가능하도록 설정**. 다음에 대한 값 지정 **[!UICONTROL 최대]** 및 **[!UICONTROL 최소]** 필드.

   최대 필드는 페이지에 패널이 나타날 수 있는 최대 횟수를 지정합니다. 최대 개수 필드에 -1을 지정하여 패널을 무제한 표시할 수 있습니다.

   최소 필드는 양식에 패널이 표시되는 최소 횟수를 지정합니다. 최소 수 필드를 0으로 설정하면 나중에 렌디션이 완료된 후 스크립트를 통해 모든 인스턴스를 제거할 수 있습니다.

   >[!NOTE]
   >
   >반복할 수 없는 패널을 만들려면 최대 및 최소 필드의 값을 1로 설정합니다. 아코디언 레이아웃은 최대 개수 필드에서 -1을 지원하지 않습니다. 높은 숫자를 지정하여 무한 값의 개념을 부여할 수 있습니다.

1. 반복할 패널의 상위에는 반복 가능한 패널의 인스턴스를 관리할 수 있는 추가 및 삭제 단추가 포함되어야 합니다. 상위에 단추를 삽입하고 단추에 스크립트를 활성화하려면 다음 단계를 수행하십시오.

   1. 사이드바에서 버튼 구성 요소를 패널의 상위로 드래그 앤 드롭합니다. 구성 요소를 선택하고 을 선택합니다. ![규칙 편집](assets/edit-rules.png). 버튼의 규칙이 규칙 편집기에 열립니다.
   1. 규칙 편집기 창에서 **만들기**.

      선택 **비주얼 편집기** 양식 개체 및 함수 행에서

      1. 규칙 영역의 WHEN에서 state를 선택합니다 **클릭됨**.
      1. Then:

         * 패널 추가 단추를 만들려면 다음을 선택합니다. **인스턴스 추가**&#x200B;을 클릭하고 다음을 사용하여 패널을 드래그 앤 드롭합니다 ![토글 사이드 패널](assets/toggle-side-panel.png) 또는 다음을 사용하여 선택 **개체를 놓거나 여기를 선택하십시오.**
         * 패널 삭제 단추를 만들려면 다음을 선택합니다. **인스턴스 제거**&#x200B;을 클릭하고 다음을 사용하여 패널을 드래그 앤 드롭합니다 ![토글 사이드 패널](assets/toggle-side-panel.png) 또는 다음을 사용하여 선택 **개체를 놓거나 여기를 선택하십시오.**

      선택 **코드 편집기** 양식 개체 및 함수 행에서 클릭 **규칙 편집** 코드 영역에서 다음을 수행합니다.

      * 패널 추가 단추를 만들려면 다음을 지정합니다 `this.panel.instanceManager.addInstance()`
      * 패널 삭제 단추를 만들려면 다음을 지정합니다 `this.panel.instanceManager.removeInstance(this.panel.instanceIndex)`

      **완료**&#x200B;를 클릭합니다.

      >[!NOTE]
      >
      >필드가 반복 가능 패널에 속해 있으면 스크립트에서 해당 이름을 사용하여 직접 액세스할 수 없습니다. 필드에 액세스하려면 다음을 사용하여 필드가 속한 반복 가능 인스턴스를 지정합니다. `instances` 의 API `InstanceManager`. 사용할 구문 `instances` 의 API `InstanceManager` 은(는)
      >
      >
      >`<panelName>.instanceManager.instances[<instanceNumber>].<fieldname>`
      >
      >
      >예를 들어 텍스트 상자가 있는 반복 가능 패널이 있는 적응형 양식을 만들 수 있습니다. 반복 가능한 텍스트 상자 3개로 양식을 미리 채우려면 아래 xml이 필요합니다.
      >
      >
      >`<panel1><textbox1>AA1</panel1></textbox1>`
      >
      >
      >`<panel1><textbox1>AA2</panel1></textbox1>`
      >
      >
      >`<panel1><textbox1>AA3</panel1></textbox1>`
      >
      >
      >AA1 데이터를 읽으려면 다음을 지정합니다.
      >
      >
      >`Panel1.instanceManager.instances[0].textbox.value`
      >
      >
      >AA2 데이터를 읽으려면 다음을 지정합니다.
      >
      >
      >`Panel1.instanceManager.instances[1].textbox.value`
      >
      >
      >자세한 내용은 클래스: InstanceManager#instances를 참조하십시오. [AEM Forms Java API 참조](https://adobe.com/go/learn_aemforms_documentation_63).

      >[!NOTE]
      >
      >적응형 양식에서 패널의 모든 인스턴스가 제거되면 제거된 패널의 인스턴스를 추가하려면 _panelName 구문을 사용하여 패널의 인스턴스 관리자를 캡처하고 인스턴스 관리자의 addInstance API를 사용하여 삭제된 인스턴스를 추가합니다. 예: _panelName.addInstance(). 제거된 패널의 인스턴스가 추가됩니다.

## 상위 패널에 대해 아코디언 레이아웃 사용   {#using-the-accordion-layout-for-the-parent-panel-nbsp}

패널에는 다양한 레이아웃 옵션이 있습니다. 아코디언 디자인을 위한 레이아웃 옵션에는 반복 가능한 패널에 대한 기본 지원이 있습니다. 아코디언 디자인 옵션의 레이아웃이 있는 반복 가능한 패널에 대해 다음 단계를 수행합니다.

1. 반복할 패널의 상위에서 을 선택합니다. ![cmppr](assets/cmppr.png). 사이드바에서 속성을 볼 수 있습니다. 다음에서 **레이아웃** 드롭다운, 선택 **어코디언**.
1. 반복할 패널에서 을 선택합니다. ![cmppr](assets/cmppr.png). 사이드바에서 패널 속성을 볼 수 있습니다. 활성화 **패널이 반복 가능하도록 설정** 탭을 클릭하고 다음에 대한 값을 지정합니다 **최대** 및 **최소** 필드.

   이제 더하기(+) 및 삭제(+)를 사용할 수 있습니다. ![패널 삭제](assets/delete-panel.png)) 단추를 클릭하여 패널을 추가하고 제거합니다.

## 양식 템플릿에서 반복되는 하위 양식 사용(XDP/XSD) {#using-repeating-subforms-from-form-template-xdp-xsd}

반복 가능한 하위 양식은 적응형 Forms의 반복 가능한 패널과 유사합니다. AEM Forms Designer에서 다음 단계를 수행하여 반복되는 하위 양식을 만듭니다.

1. 계층 팔레트에서 반복할 하위 양식의 상위 하위 양식을 선택합니다.
1. 개체 팔레트에서 하위 양식 탭을 클릭하고 컨텐츠 목록에서 흐름을 선택합니다.
1. 반복할 하위 양식을 선택합니다.
1. 개체 팔레트에서 하위 양식 탭을 클릭하고 컨텐츠 목록에서 위치함 또는 흐름을 선택합니다.
1. 바인딩 탭을 클릭하고 각 데이터 항목에 대해 하위 양식 반복을 선택합니다.
1. 최소 반복 횟수를 지정하려면 최소 횟수(Min Count)를 선택하고 연관된 상자에 숫자를 입력합니다. 이 옵션을 0으로 설정하고 데이터 병합 시 하위 양식의 개체에 대해 데이터가 제공되지 않으면 양식을 렌더링할 때 하위 양식이 배치되지 않습니다.
1. 하위 양식 반복의 최대 횟수를 지정하려면 최대값을 선택하고 연관된 상자에 숫자를 입력합니다. [최대] 상자에 값을 지정하지 않으면 하위 양식 반복 횟수는 제한이 없습니다.
1. 데이터 수량에 관계없이 하위 양식 반복 횟수를 지정하려면 초기 수를 선택하고 관련 상자에 숫자를 입력합니다. 이 옵션을 선택하고 사용할 수 있는 데이터가 없거나 지정된 초기 개수 값보다 적은 데이터 항목이 있는 경우 하위 양식의 빈 인스턴스가 계속 양식에 배치됩니다.
1. 상위 하위 양식에 인스턴스 추가 단추와 반복 가능한 하위 양식의 인스턴스 삭제 단추 두 개를 추가합니다. 자세한 단계는 를 참조하십시오. [작업 빌드](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/WS107c29ade9134a2c74572b5612a87ca2b56-8000.2.html#WS107c29ade9134a2c-1f74d86012a87d4fe55-8000.2).
1. 이제 양식 템플릿을 적응형 양식에 연결합니다. 자세한 단계는 를 참조하십시오. [템플릿을 기반으로 적응형 양식 만들기](/help/forms/using/creating-adaptive-form.md#create-an-adaptive-form-based-on-a-template).
1. 9단계에서 만든 단추를 사용하여 하위 양식을 추가하거나 제거합니다.

첨부된 .zip 파일에는 반복 가능한 하위 양식 샘플이 포함되어 있습니다.

[파일 가져오기](assets/samplerepeatablesubform.zip)

## XSD(XML 스키마)의 반복 설정 사용 {#using-repeat-settings-of-an-xml-schema-xsd-br}

XML 스키마와 복합 유형 요소의 minOccours 및 maxOccurs 속성에서 반복 가능한 패널을 만들 수 있습니다. XML 스키마에 대한 자세한 내용은 [XML 스키마를 양식 모델로 사용하여 적응형 양식 만들기](/help/forms/using/adaptive-form-xml-schema-form-model.md).

다음 코드에서는 `SampleType`패널은 minOccours 및 maxOccurs 속성을 사용합니다.

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
                <xs:element name="assignmentStartDate" type="xs:date"/>
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
>아코디언이 아닌 레이아웃의 경우 적응형 양식 버튼 구성 요소를 사용하여 인스턴스를 추가하거나 제거합니다.
