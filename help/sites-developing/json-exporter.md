---
title: 컨텐츠 서비스용 JSON 익스포터
seo-title: 컨텐츠 서비스용 JSON 익스포터
description: AEM Content Services는 웹 페이지에 초점을 두지 않고 AEM에서 컨텐츠 설명 및 게재를 일반화하기 위해 디자인되었습니다. 모든 클라이언트가 사용할 수 있는 표준화된 방법을 사용하여 기존 AEM 웹 페이지가 아닌 채널에 컨텐츠를 게재할 수 있습니다.
seo-description: AEM Content Services는 웹 페이지에 초점을 두지 않고 AEM에서 컨텐츠 설명 및 게재를 일반화하기 위해 디자인되었습니다. 모든 클라이언트가 사용할 수 있는 표준화된 방법을 사용하여 기존 AEM 웹 페이지가 아닌 채널에 컨텐츠를 게재할 수 있습니다.
uuid: be6457b1-fa9c-4f3b-b219-01a4afc239e7
contentOwner: User
content-type: reference
topic-tags: components
products: SG_EXPERIENCEMANAGER/6.5/SITES
discoiquuid: 4c7e33ea-f2d3-4d69-b676-aeb50c610d70
translation-type: tm+mt
source-git-commit: a430c4de89bde3b907d342106465d3b5a7c75cc8
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 42%

---


# 컨텐츠 서비스용 JSON 익스포터{#json-exporter-for-content-services}

AEM Content Services는 웹 페이지에 초점을 두지 않고 AEM에서 컨텐츠 설명 및 게재를 일반화하기 위해 디자인되었습니다.

모든 클라이언트가 사용할 수 있는 표준화된 방법을 사용하여 기존 AEM 웹 페이지가 아닌 채널에 컨텐츠를 게재할 수 있습니다. 이러한 채널에는 다음과 같은 것들이 포함될 수 있습니다.

* [SPA(Single Page Applications)](spa-walkthrough.md)
* 기본 모바일 애플리케이션
* AEM 외부에 있는 기타 채널 및 터치포인트

구조화된 컨텐츠를 사용하는 컨텐츠 조각을 사용하면 JSON 내보내기 도구를 사용하여 (y) AEM 페이지의 컨텐츠를 JSON 데이터 모델 형식으로 전달하여 컨텐츠 서비스를 제공할 수 있습니다. 그런 다음 사용자 자신의 응용 프로그램에서 사용할 수 있습니다.

>[!NOTE]
>
>여기에 설명된 기능은 코어 구성 요소](https://docs.adobe.com/content/docs/en/core-components/v1.html)의 [릴리스 1.1.0 이후 모든 핵심 구성 요소에 사용할 수 있습니다.

## 컨텐츠 조각 핵심 구성 요소가 있는 JSON 내보내기 {#json-exporter-with-content-fragment-core-components}

AEM JSON 내보내기 도구를 사용하여 (y) AEM 페이지의 콘텐츠를 JSON 데이터 모델 형식으로 제공할 수 있습니다. 그런 다음 사용자 자신의 응용 프로그램에서 사용할 수 있습니다.

AEM 내에서 선택기 `model` 및 `.json` 확장을 사용하여 배달을 수행합니다.

`.model.json`

1. 예를 들어 다음과 같은 URL입니다.

   ```shell
   http://localhost:4502/content/we-retail/language-masters/en.model.json
   ```

1. 다음과 같은 컨텐츠를 제공합니다.

   ![chlimage_1-192](assets/chlimage_1-192.png)

구조화된 컨텐츠 조각을 구체적으로 타깃팅하여 컨텐츠를 전달할 수도 있습니다.

이 작업은 조각에 대한 전체 경로( `jcr:content` 사용)를 사용하여 수행됩니다.예를 들어

`.../jcr:content/root/responsivegrid/contentfragment.model.json`

페이지에는 단일 컨텐츠 조각 또는 다양한 유형의 여러 구성 요소가 포함될 수 있습니다. 목록 구성 요소와 같은 메커니즘을 사용하여 관련 컨텐츠를 자동으로 검색할 수도 있습니다.

* 예를 들어 다음과 같은 URL입니다.

   ```shell
   http://localhost:4502/content/we-retail/language-masters/en/manchester-airport/jcr:content/root/responsivegrid/contentfragment.model.json
   ```

* 다음과 같은 컨텐츠를 제공합니다.

   ![chlimage_1-193](assets/chlimage_1-193.png)

   >[!NOTE]
   >
   >[자신의 구성 요소](/help/sites-developing/json-exporter-components.md)를 조정하여 이 데이터에 액세스하고 사용할 수 있습니다.

   >[!NOTE]
   >
   >표준 구현은 아니지만 [여러 선택기가 지원되지만 ](json-exporter-components.md#multiple-selectors)은(는) 첫 번째여야 합니다.`model`

### 추가 정보 {#further-information}

참고 항목:

* 자산 HTTP API

   * [자산 HTTP API](/help/assets/mac-api-assets.md)

* Sling Models:

   * [Sling Models - 130부터 리소스 유형과 모델 클래스 연결](https://sling.apache.org/documentation/bundles/models.html#associating-a-model-class-with-a-resource-type-since-130)

* AEM(JSON 포함):

   * [JSON 형식으로 페이지 정보 얻기](/help/sites-developing/pageinfo.md)

## 관련 설명서 {#related-documentation}

자세한 내용은 다음을 참조하십시오.

* 자산 사용자 안내서의 [콘텐츠 조각 항목](https://helpx.adobe.com/experience-manager/6-4/assets/user-guide.html?topic=/experience-manager/6-4/assets/morehelp/content-fragments.ug.js)

* [콘텐츠 조각 모델](/help/assets/content-fragments/content-fragments-models.md)
* [컨텐츠 조각으로 작성](/help/sites-authoring/content-fragments.md)
* [구성 요소에 대해 JSON 내보내기 활성화](/help/sites-developing/json-exporter-components.md)

* [핵심 ](https://docs.adobe.com/content/help/ko-KR/experience-manager-core-components/using/introduction.html) 구성 요소 및  [컨텐츠 조각 구성 요소](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html)

