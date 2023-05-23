---
title: 번역할 콘텐츠 식별
seo-title: Identifying Content to Translate
description: 번역이 필요한 콘텐츠를 식별하는 방법에 대해 알아봅니다.
seo-description: Learn how to identify content that needs translating.
uuid: 81b9575c-1c7a-4955-b03f-3f26cbd4f956
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: eedff940-4a46-4c24-894e-a5aa1080d23d
feature: Language Copy
exl-id: 8ca7bbcc-413a-49a8-a836-7083a9cadda1
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '1150'
ht-degree: 67%

---

# 번역할 콘텐츠 식별{#identifying-content-to-translate}

번역 규칙은 번역 프로젝트에 포함되어 있거나 번역 프로젝트에서 제외된 페이지, 구성 요소 및 에셋에 대해 번역할 콘텐츠를 식별합니다. 페이지 또는 에셋이 번역될 때 AEM은 이 콘텐츠를 추출하여 번역 서비스로 전송될 수 있도록 합니다.

페이지 및 에셋은 JCR 저장소의 노드로 표시됩니다. 추출되는 콘텐츠는 하나 이상의 노드 속성 값입니다. 번역 규칙은 추출할 콘텐츠가 포함된 속성을 식별합니다.

번역 규칙은 XML 형식으로 표시되며 다음과 같은 위치에 저장됩니다.

* `/libs/settings/translation/rules/translation_rules.xml`
* `/apps/settings/translation/rules/translation_rules.xml`
* `/conf/global/settings/translation/rules/translation_rules.xml`

파일은 모든 번역 프로젝트에 적용됩니다.

>[!NOTE]
>
>6.4로 업그레이드한 후에는 /etc에서 파일을 이동하는 것이 좋습니다. 다음을 참조하십시오 [AEM 6.5의 일반적인 저장소 재구성](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-rules) 을 참조하십시오.

규칙에는 다음과 같은 정보가 포함됩니다.

* 규칙이 적용되는 노드의 경로. 규칙은 노드의 하위 항목에도 적용됩니다.
* 번역할 콘텐츠가 포함된 노드 속성의 이름. 속성은 특정 리소스 타입 또는 모든 리소스 타입에 한정될 수 있습니다.

예를 들어 작성자가 페이지의 모든 AEM Foundation 텍스트 구성 요소에 추가하는 콘텐츠를 번역하는 규칙을 만들 수 있습니다. 규칙은 `foundation/components/text` 구성 요소에 대한 `/content` 노드 및 `text` 속성을 식별할 수 있습니다.

번역 규칙을 구성하기 위해 추가된 [콘솔](#translation-rules-ui)이 있습니다. UI의 정의에 의해 파일이 채워집니다.

AEM 콘텐츠 번역 기능의 개요를 확인하려면 [다국어 사이트를 위한 콘텐츠 번역](/help/sites-administering/translation.md)을 살펴보십시오.

>[!NOTE]
>
>AEM은 페이지에서 참조된 콘텐츠의 번역을 위해 리소스 유형과 참조 속성 간의 일대일 매핑을 지원합니다.

## 페이지, 구성 요소 및 에셋에 대한 규칙 구문 {#rule-syntax-for-pages-components-and-assets}

규칙은 하나 이상의 하위 `property` 요소 또는 0개 이상의 하위 `node` 요소가 있는 `node` 요소입니다.

```xml
<node path="content path">
          <property name="property name" [translate="false"]/>
          <node resourceType="component path" >
               <property name="property name" [translate="false"]/>
          </node>
</node>
```

이러한 각 `node` 요소는 다음과 같은 특성을 가지고 있습니다.

* `path` 속성에는 규칙이 적용될 분기의 루트 노드로의 경로가 포함됩니다.
* 하위 `property` 요소는 모든 리소스 유형에 대해 번역할 노드 속성을 식별합니다.

   * `name` 속성에는 속성 이름이 포함됩니다.
   * 선택 사항인 `translate` 속성은 번역되어 있지 않은 경우 `false`와 같습니다. 기본값은 `true`입니다. 이 속성은 이전 규칙을 오버라이드할 때 유용합니다.

* 하위 `node` 요소는 특정 리소스 유형에 대해 번역할 노드 속성을 식별합니다.

   * `resourceType` 속성에는 리소스 유형을 구현하는 구성 요소로 확인되는 경로가 포함됩니다.
   * 하위 `property` 요소는 번역할 노드 속성을 식별합니다. 이 노드를 노드 규칙에 대해 하위 `property` 요소와 동일한 방식으로 사용하십시오.

다음과 같은 예시 규칙을 사용하면 모든 `text` 속성의 콘텐츠가 `/content` 노드 아래의 모든 페이지에 대해 번역됩니다. 이 규칙은 의 콘텐츠를 저장하는 모든 구성 요소에 적용됩니다. `text` 기본 텍스트 구성 요소 및 기본 이미지 구성 요소와 같은 속성입니다.

```xml
<node path="/content">
          <property name="text"/>
</node>
```

다음 예는 모든 의 콘텐츠를 번역합니다 `text` 기본 이미지 구성 요소의 다른 속성을 변환합니다. 다른 구성 요소에 이름이 같은 속성이 있는 경우 규칙이 적용되지 않습니다.

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

## 페이지에서 에셋을 추출하기 위한 규칙 구문  {#rule-syntax-for-extracting-assets-from-pages}

다음 규칙 구문을 사용하여 구성 요소에 임베드되거나 구성 요소에서 참조되는 에셋을 포함할 수 있습니다.

```xml
<assetNode resourceType="path to component" assetReferenceAttribute="property that stores asset"/>
```

각 `assetNode` 요소는 다음과 같은 특성을 가지고 있습니다.

* 구성 요소로 확인되는 경로와 동일한 `resourceType` 속성.
* 에셋 바이너리(임베드된 에셋의 경우) 또는 참조된 에셋으로의 경로를 저장하는 속성의 이름과 동일한 `assetReferenceAttribute` 속성.

다음 예제에서는 기본 이미지 구성 요소에서 이미지를 추출합니다.

```xml
<assetNode resourceType="foundation/components/image" assetReferenceAttribute="fileReference"/>
```

## 오버라이드 규칙 {#overriding-rules}

translation_rules.xml 파일은 `nodelist` 여러 하위 요소가 있는 요소 `node` 요소. AEM은 노드 목록을 위쪽에서 아래쪽으로 읽습니다. 여러 규칙이 동일한 노드를 대상으로 하는 경우 파일에서 아래쪽에 있는 규칙이 사용됩니다. 예를 들어 다음 규칙을 사용하면 페이지의 `/content/mysite/en` 분기를 제외한 `text` 속성의 모든 콘텐츠가 번역됩니다.

```xml
<nodelist>
     <node path="/content">
           <property name="text" />
     </node>
     <node path="/content/mysite/en">
          <property name="text" translate="false" />
     </node>
<nodelist>
```

## 속성 필터링 {#filtering-properties}

`filter` 요소를 사용하여 특정 속성이 있는 노드를 필터링할 수 있습니다.

예를 들어 다음 규칙을 사용하면 속성 `draft`가 `true`로 설정되어 있는 노드를 제외한 `text` 속성의 모든 콘텐츠가 번역됩니다.

```xml
<nodelist>
    <node path="/content">
     <filter>
   <node containsProperty="draft" propertyValue="true" />
     </filter>
        <property name="text" />
    </node>
<nodelist>
```

## 번역 규칙 UI {#translation-rules-ui}

번역 규칙을 구성할 때 콘솔을 사용할 수도 있습니다.

다음 방법으로 액세스할 수 있습니다.

1. **도구**&#x200B;로 이동한 다음 **일반**&#x200B;으로 이동합니다.

   ![chlimage_1-55](assets/chlimage_1-55.jpeg)

1. **번역 구성**&#x200B;을 선택합니다.

   ![chlimage_1-56](assets/chlimage_1-56.jpeg)

여기에서 다음을 수행할 수 있습니다. **컨텍스트 추가**. 경로를 추가할 수 있습니다.

![chlimage_1-57](assets/chlimage_1-57.jpeg)

그런 다음 컨텍스트를 선택하고 **편집**&#x200B;을 선택해야 합니다. 이렇게 하면 번역 규칙 편집기가 열립니다.

![chlimage_1-58](assets/chlimage_1-58.jpeg)

UI를 통해 변경할 수 있는 속성에는 4가지가 있습니다. `isDeep`, `inherit`, `translate` 및 `updateDestinationLanguage`.

**isDeep** 이 속성은 노드 필터에 적용할 수 있으며 기본값은 true입니다. 노드(또는 상위 항목)에 필터에 지정된 속성 값이 있는 속성이 포함되어 있는지 확인합니다. false인 경우 현재 노드에서만 확인합니다.

예를 들어 상위 노드에 속성이 있는 경우에도 하위 노드가 번역 작업에 추가됩니다 `draftOnly` 초안 콘텐츠에 플래그를 지정하려면 true로 설정합니다. 여기서 `isDeep`이 생성되어 상위 노드에 true인 속성 `draftOnly`가 있는지 확인하고 이들 하위 노드를 제외합니다.

편집기에서 선택/선택 취소할 수 있습니다 **하위 항목 포함** 다음에서 **필터** 탭.

![chlimage_1-59](assets/chlimage_1-59.jpeg)

다음은 결과 xml의 예입니다. **하위 항목 포함** 가 UI에서 선택 취소됨:

```xml
 <filter>
    <node containsProperty="draftOnly" isDeep="false" propertyValue="true"/>
</filter>
```

**상속** 이는 속성에 적용됩니다. 기본적으로 모든 속성은 상속되지만, 일부 속성이 하위 속성에서 상속되지 않도록 하려면 해당 속성을 false로 표시하여 특정 노드에만 적용되도록 할 수 있습니다.

UI에서, **속성** 탭에서 **상속**&#x200B;을 선택/선택 취소할 수 있습니다.

![chlimage_1-60](assets/chlimage_1-60.jpeg)

**번역** translate 속성은 속성을 변환할지 여부를 지정하는 데만 사용됩니다.

UI에서, **속성** 탭에서 **번역**&#x200B;을 선택/선택 취소할 수 있습니다.

**updateTargetLanguage** 이 속성은 텍스트가 아닌 언어 코드가 있는 속성(예: jcr:language)에 사용됩니다. 사용자는 텍스트가 아닌 언어 로케일을 소스에서 대상으로 번역하는 것입니다. 이러한 속성은 번역용으로 전송되지 않습니다.

UI에서, 당신은 선택/선택 취소할 수 있습니다 **번역** 다음에서 **속성** 탭으로 설정되어 있지만, 언어 코드를 값으로 가지는 특정 속성만 해당됩니다.

`updateDestinationLanguage`와 `translate` 간의 차이점을 명확하게 이해하기 위해, 2개의 규칙만을 가진 컨텍스트를 예로 들어보겠습니다.

![chlimage_1-61](assets/chlimage_1-61.jpeg)

XML의 결과는 다음과 같이 표시됩니다.

```xml
<property inherit="true" name="text" translate="true" updateDestinationLanguage="false"/>
<property inherit="true" name="jcr:language" translate="false" updateDestinationLanguage="true"/>
```

## 수동으로 규칙 파일 편집 {#editing-the-rules-file-manually}

AEM과 함께 설치되는 translation_rules.xml 파일에는 기본 번역 규칙 세트가 포함되어 있습니다. 번역 프로젝트 요구 사항을 지원하도록 파일을 편집할 수 있습니다. 예를 들어 규칙을 추가하여 사용자 정의 구성 요소의 콘텐츠가 번역되도록 할 수 있습니다.

translation_rules.xml 파일을 편집하는 경우 컨텐츠 패키지에 백업 사본을 보관합니다. AEM 서비스 팩을 설치하거나 특정 AEM 패키지를 다시 설치하면 현재 translation_rules.xml 파일이 원본 파일로 대체될 수 있습니다. 이러한 상황에서 규칙을 복원하기 위해 백업 사본이 포함된 패키지를 설치할 수 있습니다.

>[!NOTE]
>
>콘텐츠 패키지를 제작한 후 파일을 편집할 때마다 패키지를 다시 빌드할 수 있습니다.

## 예제 번역 규칙 파일 {#example-translation-rules-file}

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
