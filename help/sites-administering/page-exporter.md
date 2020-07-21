---
title: 페이지 내보내기
description: AEM 페이지 내보내기 기능을 사용하는 방법에 대해 학습합니다.
translation-type: tm+mt
source-git-commit: 000666e0c3f05635a9469d3571a10c67b3b21613
workflow-type: tm+mt
source-wordcount: '1071'
ht-degree: 0%

---


# 페이지 내보내기{#the-page-exporter}

AEM에서는 페이지 `.js` 를 이미지 및 `.css` 파일을 포함한 전체 웹 페이지로 내보낼 수 있습니다.

구성된 경우 브라우저에서 URL로 대체하여 페이지 내보내기 `html` 를 요청합니다 `export.zip` . 이렇게 하면 렌더링된 페이지가 참조되는 자산과 함께 html 형식으로 포함된 보관(zip) 파일이 생성됩니다. 페이지의 모든 경로(예: 이미지 경로)는 아카이브에 포함된 파일 또는 서버의 리소스를 가리키도록 다시 작성됩니다. 그런 다음 브라우저에서 아카이브(zip) 파일을 다운로드할 수 있습니다.

>!![NOTE]
브라우저 및 설정에 따라 다운로드가 다음 중 하나가 됩니다.
* 아카이브 파일 (`<page-name>.export.zip`)
* a 폴더 (`<page-name>`); 이미 확장된 아카이브 파일


## 페이지 내보내기 {#exporting-a-page}

다음 단계에서는 페이지를 내보내는 방법을 설명하고 사이트에 대한 내보내기 구성 템플릿이 있다고 가정합니다. 구성 템플릿은 페이지를 내보내는 방법을 정의하며 사이트에 따라 다릅니다. 구성 템플릿을 만들려면 사이트에 대한 페이지 [내보내기 구성 만들기 섹션을](#creating-a-page-exporter-configuration-for-your-site) 참조하십시오.

페이지를 내보내려면:

1. 필요한 페이지로 이동하여 페이지를 선택한 다음 속성 대화 **상자를** 엽니다.

1. Select the **Advanced** tab.

1. 내보내기 **필드를** 확장하여 구성 템플릿을 선택합니다.
사이트에 필요한 템플릿을 선택한 다음 **확인을 클릭하여 확인합니다**.

1. 저장 **및 닫기를** 선택하여 페이지 속성 대화 상자를 닫습니다.

1. URL에서 접미사를 다음으로 대체하여 내보낼 페이지 `html` 를 `export.zip` 요청합니다.

   예:
   * localhost:4502/content/we-retail/language-masters/en.html

   액세스 방법:
   * localhost:4502/content/we-retail/language-masters/en.export.zip


1. 파일 시스템에 아카이브 파일을 다운로드합니다.

1. 파일 시스템에서 필요한 경우 파일의 압축을 해제합니다. 확장되면 선택한 페이지와 동일한 이름의 폴더가 생성됩니다. 이 폴더에는 다음이 포함됩니다.

   * 하위 폴더 `content`로, 저장소의 페이지 경로를 반영하는 일련의 하위 폴더의 루트입니다.

   * 이 구조 내에 선택한 페이지의 html 파일이 있습니다(`<page-name>.html`).

   * 기타 리소스(`.js` 파일, `.css` 파일, 이미지 등) 는 내보내기 템플릿의 설정에 따라 위치합니다

1. 브라우저에서 페이지 html 파일(`<unzip-dir>/<path>/<to>/<page>/<page-path>.html`)을 열어 렌더링을 확인합니다.

## 사이트에 대한 페이지 내보내기 구성 만들기 {#creating-a-page-exporter-configuration-for-your-site}

페이지 내보내기 프로그램은 Content Sync 프레임워크를 기반으로 합니다. 페이지 속성 대화 상자에서 사용할 수 **있는** 구성은 페이지에 대한 필수 종속성을 정의하는 내보내기 템플릿입니다.

페이지 내보내기가 트리거되면 내보내기 템플릿이 참조되고 페이지 경로와 디자인 경로가 모두 동적으로 적용됩니다. 그런 다음 표준 컨텐츠 동기화 기능을 사용하여 zip 파일을 만듭니다.

AEM에 기본 템플릿이 포함되어 `/etc/contentsync/templates/default`있습니다.

* 이 템플릿은 저장소에서 구성 템플릿을 찾을 수 없는 폴백 템플릿입니다.

* 템플릿은 페이지 내보내기를 구성하는 방법을 보여주므로 새 구성 템플릿의 기초로 사용할 수 있습니다. `default`

* 브라우저에서 템플릿의 노드 구조를 JSON 형식으로 보려면 다음 URL을 요청하십시오.
   `http://localhost:4502/etc/contentsync/templates/default.json`

새 페이지 내보내기 템플릿을 만드는 가장 쉬운 방법은 다음과 같습니다.

* 템플릿 `default` 복사,

* 사이트에 적절한 새 이름을 할당하고

* 그런 다음 필요한 업데이트를 만듭니다.

완전히 새 템플릿을 만들려면:

1. CRXDE **Lite**&#x200B;에서 아래 노드를 만듭니다 `/etc/contentsync/templates`

   * `Name`: 사이트에 적합한 이름; 예를 들면 다음과 같습니다 `<mysite>`. 페이지 내보내기 템플릿 선택 시 페이지 속성 대화 상자에 이름이 나타납니다.

   * `Type`: `nt:unstructured`

1. 여기에서 호출되는 템플릿 노드 아래에 아래 `mysite`에 설명된 구성 노드를 사용하여 노드 구조를 만듭니다.

## 페이지에 대한 페이지 내보내기 템플릿 활성화 {#activating-a-page-exporter-configuration-for-your-pages}

템플릿이 구성되면 사용할 수 있도록 설정해야 합니다.

1. CRXDE에서 필요한 페이지로 이동합니다.

1. 노드에서 `jcr:content` 속성을 만듭니다.
   * `Name`: `cq:exportTemplate`
   * `Type`: `String`
   * `Value`: 템플릿에 대한 경로; 예를 들면 다음과 같습니다. `/etc/contentsync/templates/mysite`

### 페이지 내보내기 구성 노드 {#page-exporter-configuration-nodes}

템플릿은 노드 구조로 구성됩니다. 각 노드에는 zip 파일의 작성 프로세스에서 특정 작업을 정의하는 `type` 속성이 있습니다. 유형 속성에 대한 자세한 내용은 Content Sync 프레임워크 페이지의 구성 유형 개요 섹션을 참조하십시오.

다음 노드를 사용하여 내보내기 구성 템플릿을 작성할 수 있습니다.

* `page`
페이지 노드는 페이지 html을 zip 파일에 복사하는 데 사용됩니다. 다음과 같은 특성이 있습니다.

   * 필수 노드입니다.
   * 은 아래에 있습니다 `/etc/contentsync/templates/<sitename>`.
   * 이름이 `page`맞습니다
   * 해당 노드 유형은 `nt:unstructured`

   노드에는 `page` 다음 속성이 있습니다.

   * 값이 있는 `type` 속성 집합 `pages`.

   * 현재 페이지 경로가 구성에 동적으로 복사되므로 `path` 속성이 없습니다.

   * 다른 속성은 Content Sync 프레임워크의 구성 유형 개요 섹션에 설명되어 있습니다.


* `rewrite`
다시 작성 노드는 내보낸 페이지에서 링크가 재작성되는 방법을 정의합니다. 새로 작성된 링크는 zip 파일에 포함된 파일 또는 서버의 리소스를 가리킬 수 있습니다.

   노드에 대한 전체 설명은 컨텐츠 동기화 페이지를 `rewrite` 참조하십시오.

* `design`
디자인 노드는 내보낸 페이지에 사용되는 디자인을 복사하는 데 사용됩니다. 다음과 같은 특성이 있습니다.

   * 선택 사항입니다.
   * 은 아래에 있습니다 `/etc/contentsync/templates/<sitename>`.
   * 이름이 `design`맞습니다
   * 해당 노드 유형은 입니다 `nt:unstructured`.

   노드에는 `design` 다음 속성이 있습니다.

   * 값으로 설정된 `type` 속성 `copy`.

   * 현재 페이지 경로가 구성에 동적으로 복사되므로 `path` 속성이 없습니다.


* `generic`
범용 노드는 clientlibs .js 또는 .css 파일과 같은 리소스를 zip 파일로 복사하는 데 사용됩니다. 다음과 같은 특성이 있습니다.

   * 선택 사항입니다.

   * 은 아래에 있습니다 `/etc/contentsync/templates/<sitename>`.

   * 특정 이름이 없습니다.

   * 해당 노드 유형은 입니다 `nt:unstructured`.

   * Content Sync `type` 프레임워크의 구성 유형 개요 섹션에 정의된 대로 속성과 `type` 관련 속성이 있습니다.

   예를 들어 다음 구성 노드는 zip 파일에 `mysite.clientlibs.js` 파일을 복사합니다.

   ```xml
   "mysite.clientlibs.js": {
       "extension": "js",
       "type": "clientlib",
       "path": "/etc/designs/mysite/clientlibs",
       "jcr:primaryType": "nt:unstructured"
   }
   ```

**사용자 지정 구성 구현**

사용자 지정 구성도 가능합니다.

<!--
As you may have noticed in the node structure, the **Geometrixx** page export configuration template has a `logo` node with a `type` property set to `image`. This is a special configuration type that has been created to copy the image logo to the zip file. 
-->

특정 요구 사항을 충족하려면 사용자 지정 `type` 속성을 구현해야 할 수 있습니다. 이렇게 하려면 콘텐츠 동기화 페이지의 사용자 지정 업데이트 처리기 구현 섹션을 참조하십시오.

## 프로그래밍 방식으로 페이지 내보내기 {#programmatically-exporting-a-page}

프로그래밍 방식으로 페이지를 내보내려면 [PageExporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/wcm/contentsync/PageExporter.html) OSGI 서비스를 사용할 수 있습니다. 이 서비스를 통해 다음을 수행할 수 있습니다.

* 페이지를 내보내고 HTTP 서블릿 응답으로 씁니다.
* 페이지를 내보내고 특정 위치에 zip 파일을 저장합니다.

선택기와 확장자에 바인딩된 서블릿은 PageExporter 서비스를 `export` `zip` 사용합니다.

## 문제 해결 {#troubleshooting}

zip 파일의 다운로드에 문제가 있는 경우 저장소의 `/var/contentsync` 노드를 삭제하고 내보내기 요청을 다시 보낼 수 있습니다.

