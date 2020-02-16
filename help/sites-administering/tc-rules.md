---
title: 변환할 컨텐츠 식별
seo-title: 변환할 컨텐츠 식별
description: 번역해야 하는 컨텐츠를 식별하는 방법을 알아봅니다.
seo-description: 번역해야 하는 컨텐츠를 식별하는 방법을 알아봅니다.
uuid: 81b9575c-1c7a-4955-b03f-3f26cbd4f956
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: eedff940-4a46-4c24-894e-a5aa1080d23d
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd

---


# 변환할 컨텐츠 식별{#identifying-content-to-translate}

번역 규칙은 번역 프로젝트에 포함되거나 포함되지 않은 페이지, 구성 요소 및 자산에 대해 번역할 컨텐츠를 식별합니다. 페이지 또는 자산을 번역하는 경우 AEM에서 이 컨텐츠를 추출하여 번역 서비스로 전송할 수 있습니다.

페이지와 자산은 JCR 저장소에서 노드로 표시됩니다. 추출된 컨텐츠는 노드의 속성 값 중 하나 이상입니다. 번역 규칙은 추출할 컨텐츠가 들어 있는 속성을 식별합니다.

번역 규칙은 XML 형식으로 표현되어 다음과 같은 위치에 저장됩니다.

* `/libs/settings/translation/rules/translation_rules.xml`
* `/apps/settings/translation/rules/translation_rules.xml`
* `/conf/global/settings/translation/rules/translation_rules.xml`

이 파일은 모든 번역 프로젝트에 적용됩니다.

>[!NOTE]
>
>6.4로 업그레이드한 후 /etc에서 파일을 이동하는 것이 좋습니다. 자세한 [내용은 AEM 6.5의](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-rules) 공용 저장소 구조화를 참조하십시오.

규칙에는 다음 정보가 포함됩니다.

* 규칙이 적용되는 노드의 경로입니다. 이 규칙은 노드의 하위 항목에도 적용됩니다.
* 변환할 컨텐츠가 들어 있는 노드 속성의 이름입니다. 속성은 특정 리소스 유형이나 모든 리소스 유형에 따라 달라질 수 있습니다.

예를 들어 작성자가 페이지의 모든 AEM 기반 텍스트 구성 요소에 추가하는 컨텐츠를 변환하는 규칙을 만들 수 있습니다. 규칙은 `/content` 구성 요소에 대한 노드 및 `text` `foundation/components/text` 속성을 식별할 수 있습니다.

번역 규칙을 구성하기 위해 추가된 [콘솔이](#translation-rules-ui) 있습니다. UI의 정의가 파일을 자동으로 채웁니다.

AEM의 컨텐츠 번역 기능에 대한 개요는 다국어 [사이트에 대한 컨텐츠 번역을 참조하십시오](/help/sites-administering/translation.md).

>[!NOTE]
>
>AEM 파섹

## 페이지, 구성 요소 및 자산에 대한 규칙 구문 {#rule-syntax-for-pages-components-and-assets}

규칙은 하나 이상의 하위 `node` 요소와 0개 이상의 하위 `property` `node` 요소가 있는 요소입니다.

```xml
<node path="content path">
          <property name="property name" [translate="false"]/>
          <node resourceType="component path" >
               <property name="property name" [translate="false"]/>
          </node>
</node>
```

이러한 각 `node` 요소에는 다음과 같은 특성이 있습니다.

* 이 `path` 속성에는 규칙이 적용되는 분기의 루트 노드에 대한 경로가 포함됩니다.
* 하위 `property` 요소는 모든 리소스 유형에 대해 변환할 노드 속성을 식별합니다.

   * 속성에 속성 이름이 포함되어 `name` 있습니다.
   * 선택적 `translate` 속성은 속성이 번역되지 않는 `false` 경우 같습니다. 기본적으로 값은 `true`입니다. 이 속성은 이전 규칙을 무시할 때 유용합니다.

* 하위 `node` 요소는 특정 리소스 유형에 대해 변환할 노드 속성을 식별합니다.

   * 이 `resourceType` 속성에는 리소스 유형을 구현하는 구성 요소로 확인하는 경로가 포함됩니다.
   * 자식 `property` 요소는 번역할 노드 속성을 식별합니다. 노드 규칙에 대한 하위 `property` 요소와 같은 방법으로 이 노드를 사용합니다.

다음 예제 규칙은 모든 `text` 속성의 컨텐츠가 `/content` 노드 아래의 모든 페이지에 대해 번역되도록 합니다. 규칙은 기본 텍스트 구성 요소 및 기본 이미지 구성 요소와 같은 `text` 속성에 컨텐츠를 저장하는 모든 구성 요소에 적용됩니다.

```xml
<node path="/content">
          <property name="text"/>
</node>
```

다음 예에서는 모든 `text` 속성의 컨텐츠를 번역하고 기본 이미지 구성 요소의 다른 속성을 변환합니다. 다른 구성 요소에 이름이 같은 속성이 있으면 규칙이 적용되지 않습니다.

```xml
<node path="/content">
      <property name="text"/>
      <node resourceType="foundation/components/textimage">
         <property name="image/alt"/>
         <property name="image/jcr:description"/>
         <property name="image/jcr:title"/>
      </node>
</node>
```

## 페이지에서 자산 추출을 위한 규칙 구문 {#rule-syntax-for-extracting-assets-from-pages}

다음 규칙 구문을 사용하여 구성 요소에 포함되거나 구성 요소에서 참조되는 에셋을 포함합니다.

```xml
<assetNode resourceType="path to component" assetReferenceAttribute="property that stores asset"/>
```

각 `assetNode` 요소에는 다음과 같은 특성이 있습니다.

* 구성 요소로 해결하는 경로와 동일한 `resourceType` 속성
* 자산 이진(포함된 자산에 대해) 또는 참조된 자산에 대한 경로를 저장하는 속성의 이름과 같은 하나의 `assetReferenceAttribute` 속성입니다.

다음 예는 기초 이미지 구성 요소에서 이미지를 추출합니다.

```xml
<assetNode resourceType="foundation/components/image" assetReferenceAttribute="fileReference"/>
```

## 규칙 무시 {#overriding-rules}

translation_rules.xml 파일은 여러 하위 `nodelist` 요소가 있는 `node` 요소로 구성됩니다. AEM은 노드 목록을 위에서 아래로 읽습니다. 여러 규칙이 동일한 노드를 타깃팅하면 파일에서 낮은 규칙이 사용됩니다. 예를 들어, 다음 규칙을 사용하면 페이지 분기를 제외한 `text` 속성의 모든 컨텐츠가 `/content/mysite/en` 변환됩니다.

```xml
<nodelist>
     <node path="/content”>
           <property name="text" />
     </node>
     <node path=“/content/mysite/en”>
          <property name=“text” translate=“false" />
     </node>
<nodelist>
```

## 속성 필터링 {#filtering-properties}

요소를 사용하여 특정 속성이 있는 노드를 필터링할 수 `filter` 있습니다.

예를 들어 다음 규칙은 속성이 로 `text` 설정된 노드를 제외하고 `draft` 속성의 모든 컨텐츠를 `true`변환하도록 합니다.

```xml
<nodelist>
    <node path="/content”>
     <filter>
   <node containsProperty="draft" propertyValue="true" />
     </filter>
        <property name="text" />
    </node>
<nodelist>
```

## 번역 규칙 UI {#translation-rules-ui}

번역 규칙을 구성하는 데에도 콘솔을 사용할 수 있습니다.

액세스 방법:

1. 도구로 **이동한** 다음 일반으로 **이동합니다**.

   ![chlimage_1-55](assets/chlimage_1-55.jpeg)

1. 번역 **구성을 선택합니다**.

   ![chlimage_1-56](assets/chlimage_1-56.jpeg)

여기에서 컨텍스트를 **추가할 수 있습니다**. 이렇게 하면 경로를 추가할 수 있습니다.

![chlimage_1-57](assets/chlimage_1-57.jpeg)

그런 다음 컨텍스트를 선택한 다음 편집을 **클릭합니다**. 그러면 번역 규칙 편집기가 열립니다.

![chlimage_1-58](assets/chlimage_1-58.jpeg)

UI를 통해 변경할 수 있는 4가지 속성이 있습니다. `isDeep`및 `inherit``translate` 를 `updateDestinationLanguage`참조하십시오.

**isDeep** 이 속성은 노드 필터에 적용되며 기본적으로 true입니다. 노드(또는 해당 상위 노드)에 필터에 지정된 속성 값이 있는 속성이 포함되어 있는지 확인합니다. false이면 현재 노드에서만 확인합니다.

예를 들어 상위 노드에 초안 컨텐츠 플래그를 지정하는 속성이 true로 `draftOnly` 설정되어 있어도 하위 노드가 번역 작업에 추가됩니다. 여기에서 `isDeep` play를 통해 상위 노드에 속성이 true `draftOnly` 로 설정되어 있는지 확인하고 해당 하위 노드를 제외합니다.

편집기에서 필터 탭에서 심도를 선택하거나 선택 취소할 **수** **있습니다** .

![chlimage_1-59](assets/chlimage_1-59.jpeg)

다음은 UI에서 [깊이 포함] **이** 선택 취소되면 생성되는 xml의 예입니다.

```xml
 <filter>
    <node containsProperty="draftOnly" isDeep="false" propertyValue="true"/>
</filter>
```

**inherit** 속성에 적용할 수 있습니다. 기본적으로 모든 속성은 상속되지만 일부 속성이 자식에 상속되지 않도록 하려면 해당 속성을 false로 표시하여 특정 노드에만 적용할 수 있습니다.

UI에서 속성 **탭에서 상속을** 선택/선택 취소할 **수** 있습니다.

![chlimage_1-60](assets/chlimage_1-60.jpeg)

**translate** The translate attribute is simplically used to specify whether or not to translate a property.

UI에서 속성 **탭에서 번역을** 선택/선택 취소할 **수** 있습니다.

**updateDestination** 언어 이 속성은 텍스트가 아닌 언어 코드(예: jcr:language)가 있는 속성에 사용됩니다. 사용자가 텍스트를 번역하지 않고 언어 로케일을 소스에서 대상으로 번역하고 있습니다. 이러한 속성은 번역용으로 전송되지 않습니다.

UI에서는 [속성] **탭에서** [번역]을 선택/선택 해제할 **수** 있지만 언어 코드를 값으로 포함하는 특정 속성에 대해서는선택 취소할 수 있습니다.

두 가지 규칙만 있는 컨텍스트의 간단한 예를 `updateDestinationLanguage` 들어 `translate`와 의 차이를 명확히 할 수 있습니다.

![chlimage_1-61](assets/chlimage_1-61.jpeg)

xml의 결과는 다음과 같습니다.

```xml
<property inherit="true" name="text" translate="true" updateDestinationLanguage="false"/>
<property inherit="true" name="jcr:language" translate="false" updateDestinationLanguage="true"/>
```

## 수동으로 규칙 파일 편집 {#editing-the-rules-file-manually}

AEM과 함께 설치되는 translation_rules.xml 파일에는 기본 변환 규칙 세트가 포함되어 있습니다. 파일을 편집하여 번역 프로젝트의 요구 사항을 지원할 수 있습니다. 예를 들어 사용자 지정 구성 요소의 컨텐츠가 번역되도록 규칙을 추가할 수 있습니다.

translation_rules.xml 파일을 편집하는 경우 컨텐츠 패키지에 백업 복사본을 보관합니다. AEM 서비스 팩을 설치하거나 특정 AEM 패키지를 다시 설치하면 현재 translation_rules.xml 파일을 원본으로 바꿀 수 있습니다. 이러한 상황에서 규칙을 복원하려면 백업 복사본이 포함된 패키지를 설치할 수 있습니다.

>[!NOTE]
>
>컨텐츠 패키지를 만든 후 파일을 편집할 때마다 패키지를 다시 빌드합니다.

## 번역 규칙 파일 예 {#example-translation-rules-file}

```xml
<nodelist>
    <!-- translation rules for Geometrixx Demo site (example) -->
    <node path="/content/geometrixx">
        <!-- list all node properties that should be translated -->
        <property name="jcr:title" /> <!-- translation workflows running on content saved in /content/geometrixx, will extract jcr:title values independent of the component. -->
        <property name="jcr:description" />
        <node resourceType ="foundation/components/image"> <!-- translation workflows running on content saved in /content/geometrixx, will extract alternateText values only for Image component. -->
            <property name="alternateText"/>
        </node>
        <node resourceType ="geometrixx/components/title">
            <property name="richText"/>
            <property name="jcr:title" translate="false"/> <!-- translation workflows running on content saved in /content/geometrixx, will not extract jcr:title for Title component, but instead use richText. -->
        </node>
        <node pathContains="/cq:annotations">
            <property name="text" translate="false"/> <!-- translation workflows running on content saved in /content/geometrixx, will not extract text if part of cq:annotations node. -->
        </node>
    </node>
    <!-- translation rules for Geometrixx Outdoors site (example) -->
    <node path="/content/geometrixx-outdoors">
        <node resourceType ="foundation/components/image">
            <property name="alternateText"/>
            <property name="jcr:title" />
        </node>
        <node resourceType ="geometrixx-outdoors/components/title">
            <property name="richText"/>
        </node>
    </node>
    <!-- translation rules for ASSETS (example) -->
    <node path="/content/dam">
        <!-- configure list of metadata properties here -->
        <property name="dc:title" />
        <property name="dc:description" />
    </node>
    <!-- translation rules for extracting ASSETS from SITES content, configure all components that embed or reference assets -->
    <assetNode resourceType="foundation/components/image" assetReferenceAttribute="fileReference"/>
    <assetNode resourceType="foundation/components/video" assetReferenceAttribute="asset"/>
    <assetNode resourceType="foundation/components/download" assetReferenceAttribute="fileReference"/>
    <assetNode resourceType="foundation/components/mobileimage" assetReferenceAttribute="fileReference"/>
    <assetNode resourceType="wcm/foundation/components/image" assetReferenceAttribute="fileReference"/>
</nodelist>
```

