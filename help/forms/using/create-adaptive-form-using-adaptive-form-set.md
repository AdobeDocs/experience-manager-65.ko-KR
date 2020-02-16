---
title: 적응형 양식 세트를 사용하여 적응형 양식 만들기
seo-title: 적응형 양식 세트를 사용하여 적응형 양식 만들기
description: 'AEM Forms를 사용하면 적응형 양식을 함께 가져와 하나의 대규모 적응형 양식을 작성하고 해당 기능을 파악할 수 있습니다. '
seo-description: 'AEM Forms를 사용하면 적응형 양식을 함께 가져와 하나의 대규모 적응형 양식을 작성하고 해당 기능을 파악할 수 있습니다. '
uuid: e52e4f90-8821-49ec-89ff-fbf07db69bd2
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 264aa8c0-ba64-4768-b3d1-1b9baa6b4d72
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# 적응형 양식 세트를 사용하여 적응형 양식 만들기{#create-an-adaptive-form-using-a-set-of-adaptive-forms}

## 개요 {#overview}

은행 계좌 개설 신청과 같은 워크플로우에서는 사용자가 여러 양식을 채웁니다. 양식을 채우도록 요청하지 않고 양식을 함께 스택하고 큰 양식(상위 양식)을 만들 수 있습니다. 응용 양식을 더 큰 양식에 추가하면 패널로서 추가됩니다(하위 양식). 하위 양식 세트를 추가하여 상위 양식을 만듭니다. 사용자 입력에 따라 패널을 표시하거나 숨길 수 있습니다. 제출 및 재설정과 같은 상위 양식의 단추는 하위 양식의 단추를 덮어씁니다. 상위 양식에 적응형 양식을 추가하려면 적응형 양식 조각과 같은 자산 브라우저에서 적응형 양식을 드래그하여 놓을 수 있습니다.

사용 가능한 기능은 다음과 같습니다.

* 독립적인 제작
* 적절한 양식 표시/숨기기
* 레이지 로딩

독립적인 작성 및 레이지 로딩과 같은 기능을 사용하면 개별 구성 요소를 사용하여 상위 양식을 만들 때보다 성능이 향상됩니다.

>[!NOTE]
>
>XFA 기반 적응형 양식/조각을 하위 양식 또는 상위 양식으로 사용할 수 없습니다.

## 비하인드 스토리 {#behind-the-scenes}

XSD 기반 응용 양식 및 조각을 상위 양식에 추가할 수 있습니다. 상위 양식의 구조는 [모든 적응형 양식과](../../forms/using/prepopulate-adaptive-form-fields.md)동일합니다. 적응형 양식을 자식 양식으로 추가하면 상위 양식에 패널로 추가됩니다. 바인딩된 자식 양식의 데이터는 상위 양식의 XML 스키마의 `data`루트 `afBoundData` 아래에 저장됩니다.

예를 들어 고객이 애플리케이션 양식을 채웁니다. 양식의 처음 두 필드는 이름과 ID입니다. XML은 다음과 같습니다.

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

고객이 자신의 사무실 주소를 채울 수 있도록 애플리케이션에 다른 양식을 추가합니다. 하위 양식의 스키마 루트는 입니다 `officeAddress`. 적용 `bindref` 또는 `/application/officeAddress` `/officeAddress`을 참조하십시오. 제공되지 `bindref`않으면 하위 양식이 `officeAddress` 하위 트리로 추가됩니다. 아래 양식의 XML을 참조하십시오.

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

고객이 집 주소를 제공할 수 있도록 다른 양식을 삽입하는 경우 XML `bindref` 을 `/application/houseAddress or /houseAddress.`다음과 같이 적용합니다.

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

스키마 루트와 동일한 하위 루트 이름(이 `Address`예제의 경우)을 유지하려면 인덱싱된 바인드를 사용합니다.

예를 들어, `/application/address[1]` 또는 `/address[1]` 및 `/application/address[2]` 또는 `/address[2]`를 적용합니다. 양식의 XML은 다음과 같습니다.

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

이 `bindRef` 속성을 사용하여 응용 양식/조각의 기본 하위 트리를 변경할 수 있습니다. 이 `bindRef` 속성을 사용하면 XML 스키마의 트리 구조에서 위치를 가리키는 경로를 지정할 수 있습니다.

자식 양식이 바인딩되지 않으면 해당 데이터는 상위 양식의 XML 스키마의 `data`루트 `afUnboundData` 아래에 저장됩니다.

적응형 양식을 여러 번 하위 양식으로 추가할 수 있습니다. 응용 양식의 사용된 각 인스턴스가 데이터 루트 아래에 있는 다른 하위 루트를 가리키도록 `bindRef` 가 제대로 수정되었는지 확인합니다.

>[!NOTE]
>
>다른 양식/단편이 동일한 하위 루트에 매핑되면 데이터를 덮어씁니다.

## 자산 브라우저를 사용하여 응용 양식을 하위 양식으로 추가 {#adding-an-adaptive-form-as-a-child-form-using-asset-browser}

자산 브라우저를 사용하여 적응형 양식을 하위 양식으로 추가하려면 다음 단계를 수행하십시오.

1. 편집 모드에서 상위 양식을 엽니다.
1. 세로 막대에서 **자산** - ![브라우저를](assets/assets-browser.png)클릭합니다. 자산 아래의 **드롭다운에서** 적응형 양식을 선택합니다.
   [ 자산에서 적응형 ![양식 선택](assets/asset.png)](assets/asset-1.png)

1. 하위 양식으로 추가할 적응형 양식을 드래그하여 놓습니다.
   [ 사이트에 적응형 ![양식을 드래그하여](assets/drag-drop.png)](assets/drag-drop-1.png)놓기놓는 적응형 양식이 하위 양식으로 추가됩니다.

