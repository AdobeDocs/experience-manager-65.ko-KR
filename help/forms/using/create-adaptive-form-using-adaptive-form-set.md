---
title: 적응형 양식 세트를 사용하여 적응형 양식 만들기
seo-title: 적응형 양식 세트를 사용하여 적응형 양식 만들기
description: 'AEM Forms을 사용하면 적응형 양식을 함께 가져와서 하나의 대규모 적응형 양식을 작성하고 해당 기능을 이해합니다. '
seo-description: 'AEM Forms을 사용하면 적응형 양식을 함께 가져와서 하나의 대규모 적응형 양식을 작성하고 해당 기능을 이해합니다. '
uuid: e52e4f90-8821-49ec-89ff-fbf07db69bd2
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 264aa8c0-ba64-4768-b3d1-1b9baa6b4d72
docset: aem65
feature: 적응형 양식
exl-id: 4254c2cb-66cc-4a46-b447-bc5e32def7a0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 0%

---

# 적응형 양식 세트를 사용하여 적응형 양식 만들기{#create-an-adaptive-form-using-a-set-of-adaptive-forms}

## 개요 {#overview}

은행 계좌 개설 애플리케이션과 같은 워크플로우에서 사용자는 여러 양식을 입력합니다. 양식 세트를 채우도록 하는 대신 양식을 함께 스택하고 큰 양식(상위 양식)을 작성할 수 있습니다. 적응형 양식을 더 큰 양식에 추가하면 패널(하위 양식)로 추가됩니다. 하위 양식 세트를 추가하여 상위 양식을 만듭니다. 사용자 입력에 따라 패널을 표시하거나 숨길 수 있습니다. 제출 및 재설정과 같은 상위 양식의 단추는 하위 양식의 단추를 덮어씁니다. 상위 양식에 적응형 양식을 추가하려면 자산 브라우저(적응형 양식 조각 등)에서 적응형 양식을 드래그하여 놓을 수 있습니다.

사용 가능한 기능은 다음과 같습니다.

* 독립 작성
* 적절한 양식 표시/숨기기
* 지연 로드

독립 작성 및 지연 로드 등의 기능을 사용하면 개별 구성 요소를 사용하여 상위 양식을 만들 때보다 성능이 향상됩니다.

>[!NOTE]
>
>XFA 기반 적응형 양식/조각을 하위 양식 또는 상위 양식으로 사용할 수 없습니다.

## {#behind-the-scenes} 백그라운드에서

XSD 기반 적응형 양식 및 조각을 상위 양식에 추가할 수 있습니다. 상위 양식의 구조는 [모든 적응형 양식](../../forms/using/prepopulate-adaptive-form-fields.md)과 동일합니다. 적응형 양식을 하위 양식으로 추가하면 상위 양식의 패널로 추가됩니다. 바인딩된 하위 양식의 데이터는 상위 양식의 XML 스키마의 `afBoundData` 섹션의 `data`루트 아래에 저장됩니다.

예를 들어 고객이 애플리케이션 양식을 채우는 경우가 있습니다. 양식의 처음 두 필드는 이름과 ID입니다. XML:

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

고객이 사무실 주소를 입력할 수 있도록 다른 양식을 애플리케이션에 추가합니다. 하위 양식의 스키마 루트는 `officeAddress`입니다. `bindref` `/application/officeAddress` 또는 `/officeAddress`를 적용합니다. `bindref`을 제공하지 않으면 하위 양식이 `officeAddress` 하위 트리로 추가됩니다. 아래의 양식 XML을 참조하십시오.

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

고객이 집 주소를 제공할 수 있도록 다른 양식을 삽입하는 경우 `bindref` `/application/houseAddress or /houseAddress.`XML을 적용하면 다음과 같습니다.

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

스키마 루트( 이 예에서 `Address`와) 동일한 하위 루트 이름을 유지하려면 인덱싱된 bindrefs를 사용하십시오.

예를 들어 bindrefs `/application/address[1]` 또는 `/address[1]` 및 `/application/address[2]` 또는 `/address[2]`를 적용합니다. 양식의 XML은 다음과 같습니다.

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

자식 폼의 바인딩이 해제된 경우 해당 데이터는 상위 양식의 XML 스키마의 `afUnboundData` 섹션의 `data`루트 아래에 저장됩니다.

적응형 양식을 하위 양식으로 여러 번 추가할 수 있습니다. 적응형 양식의 사용된 각 인스턴스가 데이터 루트 아래에 있는 다른 하위 루트를 가리키도록 `bindRef` 이 올바르게 수정되었는지 확인합니다.

>[!NOTE]
>
>다른 양식/조각이 동일한 하위 루트에 매핑되면 데이터를 덮어씁니다.

## 자산 브라우저 {#adding-an-adaptive-form-as-a-child-form-using-asset-browser}를 사용하여 적응형 양식을 하위 양식으로 추가

자산 브라우저를 사용하여 적응형 양식을 하위 양식으로 추가하려면 다음 단계를 수행하십시오.

1. 편집 모드에서 상위 양식을 엽니다.
1. 사이드바에서 **자산** ![자산-브라우저](assets/assets-browser.png)를 클릭합니다. 자산의 드롭다운에서 **적응형 양식**을 선택합니다.
   [ ![자산에서 적응형 양식 선택](assets/asset.png)](assets/asset-1.png)

1. 추가할 적응형 양식을 하위 양식으로 드래그 드롭합니다.
   [ ![사이트에 적응형 양식을 ](assets/drag-drop.png)](assets/drag-drop-1.png)드래그하여 놓습니다. 놓는 적응형 양식이 하위 양식으로 추가됩니다.
