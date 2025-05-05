---
title: 적응형 양식 세트를 사용하여 적응형 양식 만들기
description: AEM Forms을 사용하면 적응형 양식을 함께 가져와서 하나의 큰 적응형 양식을 작성하고 해당 기능을 이해할 수 있습니다.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
docset: aem65
feature: Adaptive Forms,Foundation Components
exl-id: 4254c2cb-66cc-4a46-b447-bc5e32def7a0
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 8%

---

# 적응형 양식 세트를 사용하여 적응형 양식 만들기{#create-an-adaptive-form-using-a-set-of-adaptive-forms}

<span class="preview"> [새 적응형 양식 만들기](/help/forms/using/create-an-adaptive-form-core-components.md) 또는 [AEM Sites 페이지에 적응형 양식 추가](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md) 작업을 할 때 현대적이고 확장 가능한 데이터 캡처 [핵심 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)를 사용하는 것이 좋습니다. 이러한 구성 요소는 적응형 양식 만들기 작업이 대폭 개선되어 우수한 사용자 경험을 보장할 수 있게 되었음을 나타냅니다. 이 문서에서는 기초 구성 요소를 사용하여 적응형 양식을 작성하는 이전 접근법에 대해 설명합니다. </span>

## 개요 {#overview}

은행 계좌 개설 신청서와 같은 워크플로우에서 사용자는 여러 양식을 작성합니다. 양식 세트를 채우라고 하는 대신 양식을 함께 스택하고 큰 양식(상위 양식)을 작성할 수 있습니다. 적응형 양식을 큰 양식에 추가하면 패널(하위 양식)로 추가됩니다. 하위 양식 세트를 추가하여 상위 양식을 만듭니다. 사용자 입력에 따라 패널을 표시하거나 숨길 수 있습니다. 제출 및 재설정과 같은 상위 양식의 단추는 하위 양식의 단추를 덮어씁니다. 상위 양식에 적응형 양식을 추가하려면 에셋 브라우저(적응형 양식 단편 등)에서 적응형 양식을 드래그 앤 드롭할 수 있습니다.

사용 가능한 기능은 다음과 같습니다.

* 독립 작성
* 적절한 양식 표시/숨기기
* 지연 로드

독립 작성 및 지연 로드와 같은 기능을 사용하면 개별 구성 요소를 사용하여 상위 양식을 만들 때보다 성능이 향상됩니다.

>[!NOTE]
>
>XFA 기반 적응형 양식/조각은 하위 또는 상위 양식으로 사용할 수 없습니다.

## 비하인드 스토리 {#behind-the-scenes}

상위 양식에 XSD 기반 적응형 양식 및 단편을 추가할 수 있습니다. 상위 양식의 구조가 [모든 적응형 양식](../../forms/using/prepopulate-adaptive-form-fields.md)과(와) 같습니다. 적응형 양식을 하위 양식으로 추가하면 상위 양식의 패널로 추가됩니다. 바인딩된 자식 양식의 데이터가 부모 양식의 XML 스키마에 있는 `afBoundData` 섹션의 `data`루트 아래에 저장됩니다.

예를 들어, 고객이 지원서를 작성합니다. 양식의 처음 두 필드는 이름과 ID입니다. 해당 XML은 다음과 같습니다.

```xml
<afData>
    <afUnboundData>
        <data />
    </afUnboundData>
    <afBoundData>
        <data xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
            <applicantName>Sarah Rose</applicantName>
            <applicantId>1234</applicantId>
        </data>
    </afBoundData>
</afData>
```

고객이 사무실 주소를 기입할 수 있도록 애플리케이션에 다른 양식을 추가합니다. 하위 양식의 스키마 루트는 `officeAddress`입니다. `bindref` `/application/officeAddress` 또는 `/officeAddress` 적용. `bindref`을(를) 제공하지 않으면 자식 양식이 `officeAddress` 하위 트리로 추가됩니다. 아래 양식의 XML을 참조하십시오.

```xml
<afData>
    <afUnboundData>
        <data />
    </afUnboundData>
    <afBoundData>
        <data xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
            <applicantName>Sarah Rose</applicantName>
            <applicantId>1234</applicantId>
            <officeAddress>
                <addressLine>1, Geometrixx City</addressLine>
                <zip>11111</zip>
            </officeAddress>
        </data>
    </afBoundData>
</afData>
```

고객이 집 주소를 제공할 수 있는 다른 양식을 삽입하면 `bindref`을(를) 적용합니다. `/application/houseAddress or /houseAddress.` XML은 다음과 같습니다.

```xml
<afData>
    <afUnboundData>
        <data />
    </afUnboundData>
    <afBoundData>
        <data xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
            <applicantName>Sarah Rose</applicantName>
            <applicantId>1234</applicantId>
            <officeAddress>
                <addressLine>1, Geometrixx City</addressLine>
                <zip>11111</zip>
            </officeAddress>
            <houseAddress>
                <addressLine>2, Geometrixx City</addressLine>
                <zip>11111</zip>
            </houseAddress>
        </data>
    </afBoundData>
</afData>
```

스키마 루트(`Address` 이 예제에서는 )와 동일한 하위 루트 이름을 유지하려면 인덱싱된 bindrefs를 사용하십시오.

예를 들어 bindrefs `/application/address[1]` 또는 `/address[1]`과(와) `/application/address[2]` 또는 `/address[2]`을(를) 적용합니다. 양식의 XML은

```xml
<afData>
    <afUnboundData>
        <data />
    </afUnboundData>
    <afBoundData>
        <data xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
            <applicantName>Sarah Rose</applicantName>
            <applicantId>1234</applicantId>
            <address>
                <addressLine>1, Geometrixx City</addressLine>
                <zip>11111</zip>
            </address>
            <address>
                <addressLine>2, Geometrixx City</addressLine>
                <zip>11111</zip>
            </address>
        </data>
    </afBoundData>
</afData>
```

`bindRef` 속성을 사용하여 적응형 양식/조각의 기본 하위 트리를 변경할 수 있습니다. `bindRef` 속성을 사용하면 XML 스키마의 트리 구조에서 위치를 가리키는 경로를 지정할 수 있습니다.

자식 폼의 바인딩이 해제되면 해당 데이터는 부모 폼의 XML 스키마에 있는 `afUnboundData` 섹션의 `data`루트 아래에 저장됩니다.

적응형 양식을 하위 양식으로 여러 번 추가할 수 있습니다. 적응형 양식의 각 사용 인스턴스가 데이터 루트 아래의 다른 하위 루트를 가리키도록 `bindRef`이(가) 올바르게 수정되었는지 확인하십시오.

>[!NOTE]
>
>다른 양식/조각이 동일한 하위 루트에 매핑되면 데이터를 덮어씁니다.

## 에셋 브라우저를 사용하여 적응형 양식을 하위 양식으로 추가 {#adding-an-adaptive-form-as-a-child-form-using-asset-browser}

다음 단계를 수행하여 자산 브라우저를 사용하여 적응형 양식을 하위 양식으로 추가합니다.

1. 편집 모드에서 상위 양식을 엽니다.
1. 사이드바에서 **Assets** ![에셋-브라우저](assets/assets-browser.png)을 클릭합니다. Assets 아래의 드롭다운에서 **적응형 양식**&#x200B;을(를) 선택합니다.
   [![Assets에서 적응형 양식 선택](assets/asset.png)](assets/asset-1.png)

1. 하위 양식으로 추가할 적응형 양식을 드래그 앤 드롭합니다.
   [![사이트에서 적응형 양식을 드래그 앤 드롭하십시오](assets/drag-drop.png)](assets/drag-drop-1.png)드롭한 적응형 양식이 하위 양식으로 추가됩니다.
