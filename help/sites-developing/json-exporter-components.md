---
title: 구성 요소에 대해 JSON 내보내기 활성화
seo-title: 구성 요소에 대해 JSON 내보내기 활성화
description: 구성 요소를 모델러 프레임워크를 기반으로 컨텐츠의 JSON 내보내기를 생성하기 위해 수정할 수 있습니다.
seo-description: 구성 요소를 모델러 프레임워크를 기반으로 컨텐츠의 JSON 내보내기를 생성하기 위해 수정할 수 있습니다.
uuid: d7cc3347-2adb-4ea5-94a4-a847a2e66d28
contentOwner: User
content-type: reference
topic-tags: components
products: SG_EXPERIENCEMANAGER/6.5/SITES
discoiquuid: 448ad337-d4bb-4603-a27b-77da93feadbd
translation-type: tm+mt
source-git-commit: a430c4de89bde3b907d342106465d3b5a7c75cc8
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 7%

---


# 구성 요소에 대해 JSON 내보내기 활성화{#enabling-json-export-for-a-component}

구성 요소를 모델러 프레임워크를 기반으로 컨텐츠의 JSON 내보내기를 생성하기 위해 수정할 수 있습니다.

## 개요 {#overview}

JSON 내보내기는 [Sling Models](https://sling.apache.org/documentation/bundles/models.html) 및 [Sling Model Exporter](https://sling.apache.org/documentation/bundles/models.html#exporter-framework-since-130) 프레임워크를 기반으로 합니다. 이 프레임워크는 [Jackson annotations](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations)에 의존합니다.

즉, JSON을 내보내야 하는 경우 구성 요소에 Sling 모델이 있어야 합니다. 따라서 모든 구성 요소에서 JSON 내보내기를 사용하려면 이 두 단계를 따라야 합니다.

* [구성 요소에 대한 슬링 모델 정의](/help/sites-developing/json-exporter-components.md#define-a-sling-model-for-the-component)
* [슬링 모델 인터페이스에 주석 달기](#annotate-the-sling-model-interface)

## 구성 요소 {#define-a-sling-model-for-the-component}에 대한 슬링 모델 정의

먼저 구성 요소에 대해 Sling 모델을 정의해야 합니다.

>[!NOTE]
>
>Sling Models를 사용하는 예를 보려면 AEM[에서 Sling 모델 내보내기 개발 문서를 참조하십시오.](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/sling-model-exporter-tutorial-develop.html)

Sling Model 구현 클래스에는 다음과 같은 주석이 포함되어야 합니다.

```java
@Model(... adapters = {..., ComponentExporter.class})
@Exporter(name = ExporterConstants.SLING_MODEL_EXPORTER_NAME, extensions = ExporterConstants.SLING_MODEL_EXTENSION)
@JsonSerialize(as = MyComponent.class)
```

이렇게 하면 `.model` 선택기 및 `.json` 확장을 사용하여 구성 요소를 직접 내보낼 수 있습니다.

또한 Sling Model 클래스를 `ComponentExporter` 인터페이스에 적용할 수 있음을 지정합니다.

>[!NOTE]
>
>잭슨 주석은 일반적으로 Sling Model 클래스 수준에서 지정되지 않고 모델 인터페이스 수준에서 지정됩니다. 이는 JSON 내보내기가 구성 요소 API의 일부로 간주되도록 하기 위한 것입니다.

>[!NOTE]
>
>`ExporterConstants` 및 `ComponentExporter` 클래스는 `com.adobe.cq.export.json` 번들에서 제공됩니다.

### 여러 선택기 사용 {#multiple-selectors}

표준 사용 사례는 아니지만 `model` 선택기 외에 여러 선택기를 구성할 수 있습니다.

```
https://<server>:<port>/content/page.model.selector1.selector2.json
```

그러나 이러한 경우 `model` 선택기는 첫 번째 선택기여야 하며 확장자는 `.json`이어야 합니다.

## Sling 모델 인터페이스에 주석 달기 {#annotate-the-sling-model-interface}

JSON 내보내기 프레임워크에서 고려하려면 모델 인터페이스가 `ComponentExporter` 인터페이스(또는 컨테이너 구성 요소의 경우 `ContainerExporter`)를 구현해야 합니다.

그런 다음 해당 Sling 모델 인터페이스( `MyComponent`)에 [Jackson annotations](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations)를 사용하여 이러한 인터페이스를 내보내기(직렬화)할 방법을 정의할 수 있습니다.

모델 인터페이스에 일련화할 메서드를 정의하려면 적절한 주석을 추가해야 합니다. 기본적으로 getter에 대한 일반적인 명명 규칙을 준수하는 모든 메서드는 직렬화되며 getter 이름에서 JSON 속성 이름을 자연스럽게 파생하게 됩니다. JSON 속성 이름을 바꾸기 위해 `@JsonIgnore` 또는 `@JsonProperty`을 사용하여 이를 방지하거나 재정의할 수 있습니다.

## 예 {#example}

핵심 구성 요소는 핵심 구성 요소](https://docs.adobe.com/content/help/ko-KR/experience-manager-core-components/using/introduction.html)의 [1.1.0 출시 이후 JSON 내보내기를 지원했으며 참조로 사용할 수 있습니다.

예를 들어 이미지 코어 구성 요소의 Sling 모델 구현과 주석 있는 인터페이스를 참조하십시오.

GITHUB에 대한 코드

GitHub에서 이 페이지의 코드를 찾을 수 있습니다

* [GitHub에서 aem-core-wcm-components 프로젝트 열기](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components)
* 프로젝트를 [ZIP 파일](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/archive/master.zip)(으)로 다운로드합니다.

## 관련 설명서 {#related-documentation}

자세한 내용은 다음을 참조하십시오.

* 자산 사용 안내서의 [콘텐츠 조각 항목](https://helpx.adobe.com/experience-manager/6-4/assets/user-guide.html?topic=/experience-manager/6-4/assets/morehelp/content-fragments.ug.js)

* [콘텐츠 조각 모델](/help/assets/content-fragments/content-fragments-models.md)
* [컨텐츠 조각으로 작성](/help/sites-authoring/content-fragments.md)
* [컨텐츠 서비스용 JSON 익스포터](/help/sites-developing/json-exporter.md)
* [핵심 ](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html) 구성 요소 및  [컨텐츠 조각 구성 요소](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html)

