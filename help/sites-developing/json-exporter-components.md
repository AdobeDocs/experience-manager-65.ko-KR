---
title: 구성 요소에 대해 JSON 내보내기 활성화
seo-title: 구성 요소에 대해 JSON 내보내기 활성화
description: 구성 요소는 모델러 프레임워크를 기반으로 컨텐츠의 JSON 내보내기를 생성하기 위해 조정할 수 있습니다.
seo-description: 구성 요소는 모델러 프레임워크를 기반으로 컨텐츠의 JSON 내보내기를 생성하기 위해 조정할 수 있습니다.
uuid: d7cc3347-2adb-4ea5-94a4-a847a2e66d28
contentOwner: User
content-type: reference
topic-tags: components
products: SG_EXPERIENCEMANAGER/6.5/SITES
discoiquuid: 448ad337-d4bb-4603-a27b-77da93feadbd
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 구성 요소에 대해 JSON 내보내기 활성화{#enabling-json-export-for-a-component}

구성 요소는 모델러 프레임워크를 기반으로 컨텐츠의 JSON 내보내기를 생성하기 위해 조정할 수 있습니다.

## 개요 {#overview}

JSON 내보내기는 Sling [Models](https://sling.apache.org/documentation/bundles/models.html)및 [Sling Model Exporter](https://sling.apache.org/documentation/bundles/models.html#exporter-framework-since-130) 프레임워크( [Jackson 주석에](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations)의존)를 기반으로합니다.

즉, JSON을 내보내야 하는 경우 구성 요소에 Sling 모델이 있어야 합니다. 따라서 이 두 단계를 따라 구성 요소에서 JSON 내보내기를 활성화해야 합니다.

* [구성 요소에 대한 슬링 모델 정의](/help/sites-developing/json-exporter-components.md#define-a-sling-model-for-the-component)
* [슬링 모델 인터페이스에 주석 달기](#annotate-the-sling-model-interface)

## 구성 요소에 대한 슬링 모델 정의 {#define-a-sling-model-for-the-component}

먼저 구성 요소에 대해 Sling 모델을 정의해야 합니다.

>[!NOTE]
>
>Sling 모델 사용 예는 AEM에서 Sling [모델 내보내기 개발 문서를 참조하십시오](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/sling-model-exporter-tutorial-develop.html).

Sling Model 구현 클래스에 다음과 같은 주석을 추가해야 합니다.

```java
@Model(... adapters = {..., ComponentExporter.class})
@Exporter(name = ExporterConstants.SLING_MODEL_EXPORTER_NAME, extensions = ExporterConstants.SLING_MODEL_EXTENSION)
@JsonSerialize(as = MyComponent.class)
```

이렇게 하면 `.model` 선택기와 `.json` 확장을 사용하여 구성 요소를 직접 내보낼 수 있습니다.

또한 Sling Model 클래스를 `ComponentExporter` 인터페이스에 적용할 수 있도록 지정합니다.

>[!NOTE]
>
>Jackson 주석은 일반적으로 Sling Model 클래스 수준에서 지정되지 않고 모델 인터페이스 수준에서 지정됩니다. 이는 JSON 내보내기가 구성 요소 API의 일부로 간주되도록 하기 위한 것입니다.

>[!NOTE]
>
>그 `ExporterConstants` 및 `ComponentExporter` 수업은 `com.adobe.cq.export.json` 번들에서 나온다.

## 슬링 모델 인터페이스에 주석 달기 {#annotate-the-sling-model-interface}

JSON Exporter 프레임워크에서 고려하려면 모델 인터페이스가 `ComponentExporter` 인터페이스(또는 `ContainerExporter`컨테이너 구성 요소의 경우)를 구현해야 합니다.

그런 다음 Jackson 주석을 `MyComponent`사용하여 해당 Sling Model 인터페이스() [](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations) 를 내보내야 하는 방법(직렬화)을 정의할 수 있습니다.

모델 인터페이스에 일련화할 메서드를 정의하려면 제대로 주석을 달아야 합니다. 기본적으로 getter에 대한 일반적인 이름 지정 규칙을 따르는 모든 메서드는 직렬화되며 getter 이름에서 JSON 속성 이름을 자연스럽게 파생하게 됩니다. JSON 속성을 사용하거나 이름을 변경하는 `@JsonIgnore` 것을 방지하거나 재정의할 `@JsonProperty` 수 있습니다.

## 예 {#example}

핵심 구성 요소는 핵심 구성 요소의 릴리스 [1.1.0 이후 JSON 내보내기를](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html) 지원하며 참조로 사용할 수 있습니다.

예를 들어 이미지 코어 구성 요소의 Sling 모델 구현 및 주석 인터페이스를 참조하십시오.

GITHUB에 대한 코드

GitHub에서 이 페이지의 코드를 찾을 수 있습니다

* [GitHub에서 aem-core-wcm-components 프로젝트 열기](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components)
* 프로젝트를 ZIP [파일로 다운로드](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/archive/master.zip)

## 관련 설명서 {#related-documentation}

자세한 내용은 다음을 참조하십시오.

* 자산 [사용 안내서의 컨텐츠 조각 항목](https://helpx.adobe.com/experience-manager/6-4/assets/user-guide.html?topic=/experience-manager/6-4/assets/morehelp/content-fragments.ug.js)

* [컨텐츠 조각 모델](/help/assets/content-fragments-models.md)
* [컨텐츠 조각으로 작성](/help/sites-authoring/content-fragments.md)
* [콘텐츠 서비스용 JSON 내보내기](/help/sites-developing/json-exporter.md)
* [핵심 구성 요소](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html) 및 [컨텐츠 조각 구성 요소](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html)

