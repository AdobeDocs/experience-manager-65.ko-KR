---
title: 페이지 내보내기
description: AEM 페이지 내보내기 기능을 사용하는 방법을 알아봅니다.
translation-type: tm+mt
source-git-commit: 6aee1506b54a932bae8f2521fce4488de7d2a52a
workflow-type: tm+mt
source-wordcount: '1065'
ht-degree: 0%

---


# 페이지 내보내기{#the-page-exporter}

AEM에서는 이미지, `.js` 및 `.css` 파일을 포함하는 전체 웹 페이지로 페이지를 내보낼 수 있습니다.

구성한 후에는 URL에서 `html`을 `export.zip`으로 대체하여 브라우저에서 페이지 내보내기를 요청합니다. 이렇게 하면 렌더링된 페이지가 참조된 자산과 함께 html 형식으로 포함된 보관(zip) 파일이 생성됩니다. 페이지의 모든 경로(예: 이미지 경로)는 아카이브에 포함된 파일 또는 서버의 리소스를 가리키도록 다시 작성됩니다. 그런 다음 보관(zip) 파일을 브라우저에서 다운로드할 수 있습니다.

>[!NOTE]
>
>브라우저 및 설정에 따라 다운로드가 다음 중 하나가 됩니다.
>* 아카이브 파일(`<page-name>.export.zip`)
>* 폴더(`<page-name>`);이미 확장된 아카이브 파일을 효과적으로 활용


## 페이지 {#exporting-a-page} 내보내기

다음 단계에서는 페이지를 내보내는 방법을 설명하고 사이트에 내보내기 템플릿이 있다고 가정합니다. 내보내기 템플릿은 페이지를 내보내는 방법을 정의하며, 사이트에 따라 다릅니다. 내보내기 템플릿을 만들려면 사이트](#creating-a-page-exporter-configuration-for-your-site) 섹션에 대한 [페이지 내보내기 구성 만들기 섹션을 참조하십시오.

페이지를 내보내려면:

1. **사이트** 콘솔에서 필요한 페이지로 이동합니다.

1. 페이지를 선택한 다음 **속성** 대화 상자를 엽니다.

1. **고급** 탭을 선택합니다.

1. 내보내기 템플릿을 선택하려면 **내보내기** 필드를 확장합니다.
사이트에 필요한 템플릿을 선택한 다음 **OK**&#x200B;로 확인합니다.

1. **저장 및 닫기**&#x200B;를 선택하여 페이지 속성 대화 상자를 닫습니다.

1. URL에서 접미사 `html`을 `export.zip`로 대체하여 내보낼 페이지를 요청합니다.

   예:
   * localhost:4502/content/we-retail/language-masters/en.html

   다음 아이콘을 통해 액세스합니다.
   * localhost:4502/content/we-retail/language-masters/en.export.zip


1. 파일 시스템에 아카이브 파일을 다운로드합니다.

1. 필요한 경우 파일 시스템에서 파일의 압축을 해제합니다. 확장되면 선택한 페이지와 동일한 이름의 폴더가 표시됩니다. 이 폴더에는 다음이 포함됩니다.

   * 하위 폴더 `content` - 저장소의 페이지 경로를 반영하는 일련의 하위 폴더의 루트입니다.

      * 이 구조 내에 선택한 페이지의 html 파일이 있습니다(`<page-name>.html`).
   * 기타 리소스(`.js` 파일, `.css` 파일, 이미지 등) 는 내보내기 템플릿의 설정에 따라 위치


1. 브라우저에서 페이지 html 파일(`<unzip-dir>/<path>/<to>/<page>/<page-path>.html`)을 열어 렌더링을 확인합니다.

## {#creating-a-page-exporter-configuration-for-your-site} 사이트에 대한 페이지 내보내기 구성 만들기

페이지 내보내기는 [콘텐츠 동기화 프레임워크](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/package-summary.html)를 기반으로 합니다. **페이지 속성** 대화 상자에서 사용할 수 있는 구성은 페이지에 대한 필수 종속성을 정의하는 내보내기 템플릿입니다.

페이지 내보내기가 트리거되면 내보내기 템플릿이 참조되고 페이지 경로와 디자인 경로가 모두 동적으로 적용됩니다. 그런 다음 표준 컨텐츠 동기화 기능을 사용하여 zip 파일을 만듭니다.

기본 AEM 설치에는 `/etc/contentsync/templates/default` 아래에 기본 템플릿이 포함되어 있습니다.

* 이 템플릿은 저장소에서 내보내기 템플릿을 찾을 수 없는 폴백 템플릿입니다.

* `default` 템플릿은 페이지 내보내기를 구성하는 방법을 보여주므로 새 내보내기 템플릿의 기초로 사용할 수 있습니다.

* 브라우저에서 템플릿의 노드 구조를 JSON 형식으로 보려면 다음 URL을 요청하십시오.
   `http://localhost:4502/etc/contentsync/templates/default.json`

새 페이지 내보내기 템플릿을 만드는 가장 쉬운 방법은 다음과 같습니다.

* `default` 템플릿 복사,

* 사이트에 해당하는 새 이름을 할당합니다.

* 그런 다음 필요한 업데이트를 수행합니다.

완전히 새 템플릿을 만들려면:

1. **CRXDE Lite**&#x200B;에서 `/etc/contentsync/templates` 아래에 노드를 만듭니다.

   * `Name`:사이트에 적합한 이름;예를 들면 다음과 같습니다 `<mysite>`. 페이지 내보내기 템플릿을 선택할 때 페이지 속성 대화 상자에 이름이 나타납니다.

   * `Type`: `nt:unstructured`

2. 여기서 `mysite`이라고 하는 템플릿 노드 아래에 아래 설명된 구성 노드를 사용하여 노드 구조를 만듭니다.

## {#activating-a-page-exporter-configuration-for-your-pages} 페이지에 대한 페이지 내보내기 템플릿 활성화

템플릿이 구성되면 사용할 수 있도록 설정해야 합니다.

1. CRXDE에서 `/content` 분기의 필수 페이지로 이동합니다. 개별 페이지이거나 하위 트리의 루트 페이지일 수 있습니다.

1. 페이지의 `jcr:content` 노드에서 속성을 만듭니다.
   * `Name`:  `cq:exportTemplate`
   * `Type`:  `String`
   * `Value`:템플릿에 대한 경로;예를 들면 다음과 같습니다.  `/etc/contentsync/templates/mysite`

### 페이지 내보내기 구성 노드 {#page-exporter-configuration-nodes}

템플릿은 [Content Sync 프레임워크](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/package-summary.html)를 사용하므로 노드 구조로 구성됩니다.  각 노드에는 zip 파일의 작성 프로세스에서 특정 작업을 정의하는 `type` 속성이 있습니다.

<!-- For more details about the type property, refer to the Overview of configuration types section in the Content Sync framework page.
-->

다음 노드를 사용하여 내보내기 템플릿을 작성할 수 있습니다.

* `page`
페이지 노드는 페이지 html을 zip 파일에 복사하는 데 사용됩니다. 다음과 같은 특성이 있습니다.

   * 필수 노드입니다.
   * `/etc/contentsync/templates/<mysite>` 아래에 있습니다.
   * `Name`이(가) `page`로 설정된 상태로 정의됩니다.
   * 노드 유형은 `nt:unstructured`입니다.

   `page` 노드에는 다음 속성이 있습니다.

   * `pages` 값이 있는 `type` 속성 집합.

   * 현재 페이지 경로가 구성에 동적으로 복사되므로 `path` 속성이 없습니다.

   <!--
  * The other properties are described in the Overview of configuration types section of the Content Sync framework.
  -->

* `rewrite`
다시 작성 노드는 내보낸 페이지에서 링크가 어떻게 재작성되는지 정의합니다. 새로 작성된 링크는 zip 파일에 포함된 파일이나 서버의 리소스를 가리킬 수 있습니다.
   <!-- Please refer to the Content Sync page for a complete description of the `rewrite` node. -->

* `design`
디자인 노드는 내보낸 페이지에 사용되는 디자인을 복사하는 데 사용됩니다. 다음과 같은 특성이 있습니다.

   * 선택 사항입니다.
   * `/etc/contentsync/templates/<mysite>` 아래에 있습니다.
   * `Name` 속성이 `design`로 설정된 상태로 정의됩니다.
   * 노드 유형은 `nt:unstructured`입니다.

   `design` 노드에는 다음 속성이 있습니다.

   * `type` 속성이 `copy` 값으로 설정되었습니다.

   * 현재 페이지 경로가 구성에 동적으로 복사되므로 이 파일에는 `path` 속성이 없습니다.


* `generic`
범용 노드는 clientlibs와 같은 리소스를 복사하는 데 사용됩니다. 
`.js` 파일 `.css` 을 zip 파일에 넣습니다. 다음과 같은 특성이 있습니다.

   * 선택 사항입니다.
   * `/etc/contentsync/templates/<mysite>` 아래에 있습니다.
   * 특정 이름이 없습니다.
   * 노드 유형은 `nt:unstructured`입니다.
   * `type` 속성과 `type` 관련 속성이 있습니다.<!--Has a `type` property and any `type` related properties as defined in the Overview of configuration types section of the Content Sync framework.-->

   예를 들어 다음 구성 노드는 `mysite.clientlibs.js` 파일을 zip 파일로 복사합니다.

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
As you may have noticed in the node structure, the **Geometrixx** page export template has a `logo` node with a `type` property set to `image`. This is a special configuration type that has been created to copy the image logo to the zip file. 
-->

일부 특정 요구 사항을 충족하려면 [사용자 지정 업데이트 핸들러](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/handler/package-summary.html)를 구현해야 할 수 있습니다.

<!-- To meet some specific requirements, you may need to implement a custom `type` property: to do so, refer to the Implementing a custom update handler section in the Content Sync page.
-->

## 프로그래밍 방식으로 페이지 {#programmatically-exporting-a-page} 내보내기

페이지를 프로그래밍 방식으로 내보내려면 [PageExporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/wcm/contentsync/PageExporter.html) OSGI 서비스를 사용할 수 있습니다. 이 서비스를 통해 다음과 같은 작업을 수행할 수 있습니다.

* 페이지를 내보내고 HTTP 서블릿 응답으로 씁니다.
* 페이지를 내보내고 특정 위치에 zip 파일을 저장합니다.

`export` 선택기에 바인딩되고 `zip` 확장의 서블릿은 PageExporter 서비스를 사용합니다.

## 문제 해결 {#troubleshooting}

zip 파일의 다운로드에 문제가 있는 경우 저장소의 `/var/contentsync` 노드를 삭제하고 내보내기 요청을 다시 보낼 수 있습니다.
