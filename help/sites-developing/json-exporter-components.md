---
title: 구성 요소에 대해 JSON 내보내기 활성화
seo-title: Enabling JSON Export for a Component
description: 구성 요소는 모델러 프레임워크를 기반으로 콘텐츠의 JSON 내보내기를 생성하도록 조정할 수 있습니다.
seo-description: Components can be adapted to generate JSON export of their content based on a modeler framework.
uuid: d7cc3347-2adb-4ea5-94a4-a847a2e66d28
contentOwner: User
content-type: reference
topic-tags: components
products: SG_EXPERIENCEMANAGER/6.5/SITES
discoiquuid: 448ad337-d4bb-4603-a27b-77da93feadbd
exl-id: 6d127e14-767e-46ad-aaeb-0ce9dd14d553
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 8%

---

# 구성 요소에 대해 JSON 내보내기 활성화{#enabling-json-export-for-a-component}

구성 요소는 모델러 프레임워크를 기반으로 콘텐츠의 JSON 내보내기를 생성하도록 조정할 수 있습니다.

## 개요 {#overview}

JSON 내보내기는 다음을 기반으로 합니다. [Sling 모델](https://sling.apache.org/documentation/bundles/models.html), 및 [Sling 모델 내보내기](https://sling.apache.org/documentation/bundles/models.html#exporter-framework-since-130) 프레임워크(자체 의존도) [Jackson 주석](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations)).

즉, JSON을 내보내야 하는 구성 요소에는 슬링 모델이 있어야 합니다. 따라서 구성 요소에서 JSON 내보내기를 활성화하려면 다음 두 단계를 수행해야 합니다.

* [구성 요소의 슬링 모델 정의](/help/sites-developing/json-exporter-components.md#define-a-sling-model-for-the-component)
* [Sling 모델 인터페이스에 주석 달기](#annotate-the-sling-model-interface)

## 구성 요소에 대한 슬링 모델 정의 {#define-a-sling-model-for-the-component}

먼저 구성 요소에 대해 슬링 모델 을 정의해야 합니다.

>[!NOTE]
>
>Sling 모델 사용의 예는 문서 를 참조하십시오 [AEM에서 Sling 모델 내보내기 개발](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/sling-model-exporter-tutorial-develop.html).

Sling 모델 구현 클래스에는 다음 주석이 포함되어야 합니다.

```java
@Model(... adapters = {..., ComponentExporter.class})
@Exporter(name = ExporterConstants.SLING_MODEL_EXPORTER_NAME, extensions = ExporterConstants.SLING_MODEL_EXTENSION)
@JsonSerialize(as = MyComponent.class)
```

이렇게 하면 를 사용하여 구성 요소를 자체적으로 내보낼 수 있습니다. `.model` 선택기 및 `.json` 확장명.

또한 Sling 모델 클래스를 `ComponentExporter` 인터페이스.

>[!NOTE]
>
>Jackson 주석은 일반적으로 슬링 모델 클래스 수준에서 지정되지 않고 모델 인터페이스 수준에서 지정됩니다. 이는 JSON 내보내기가 구성 요소 API의 일부로 간주되도록 하기 위한 것입니다.

>[!NOTE]
>
>다음 `ExporterConstants` 및 `ComponentExporter` 클래스는 다음에서 제공됩니다. `com.adobe.cq.export.json` 번들.

### 여러 선택기 사용 {#multiple-selectors}

표준 사용 사례는 아니지만, `model` 선택기.

```
https://<server>:<port>/content/page.model.selector1.selector2.json
```

그러나 이러한 경우에는 `model` 선택기는 첫 번째 선택기여야 하며 확장은 이어야 합니다. `.json`.

## Sling 모델 인터페이스에 주석 달기 {#annotate-the-sling-model-interface}

JSON Exporter 프레임워크에서 고려하려면 모델 인터페이스가 다음을 구현해야 합니다. `ComponentExporter` 인터페이스(또는 `ContainerExporter`컨테이너 구성 요소의 경우).

해당 Sling 모델 인터페이스( `MyComponent`)에 주석을 달 수 있습니다 [Jackson 주석](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations) 내보내는 방법(일련화)을 정의할 수 있습니다.

serialize할 메서드를 정의하려면 모델 인터페이스에 적절한 주석을 추가해야 합니다. 기본적으로 getter에 대한 일반적인 명명 규칙을 준수하는 모든 메서드는 serialize되며 getter 이름에서 자연적으로 JSON 속성 이름을 파생합니다. 다음을 사용하여 방지하거나 재정의할 수 있습니다. `@JsonIgnore` 또는 `@JsonProperty` 를 클릭하여 JSON 속성의 이름을 변경합니다.

## 예 {#example}

릴리스 이후 핵심 구성 요소는 JSON 내보내기를 지원합니다. [1.1.0 핵심 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ko) 및 를 참조로 사용할 수 있습니다.

예를 들어 이미지 핵심 구성 요소의 슬링 모델 구현 및 주석이 달린 인터페이스를 참조하십시오.

GITHUB의 코드

GitHub에서 이 페이지의 코드를 확인할 수 있습니다

* [GitHub에서 aem-core-wcm-components 프로젝트 열기](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components)
* 다음으로 프로젝트 다운로드 [ZIP 파일](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/archive/master.zip)

## 관련 설명서 {#related-documentation}

자세한 내용은 다음을 참조하십시오.

* 다음 [에셋 사용 안내서의 콘텐츠 조각 항목](https://helpx.adobe.com/experience-manager/6-4/assets/user-guide.html?topic=/experience-manager/6-4/assets/morehelp/content-fragments.ug.js)

* [콘텐츠 조각 모델](/help/assets/content-fragments/content-fragments-models.md)
* [컨텐츠 조각으로 작성](/help/sites-authoring/content-fragments.md)
* [콘텐츠 서비스에 대한 JSON 내보내기](/help/sites-developing/json-exporter.md)
* [핵심 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ko) 및 [콘텐츠 조각 구성 요소](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html)
