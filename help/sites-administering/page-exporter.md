---
title: 페이지 내보내기
description: Adobe Experience Manager(AEM) 페이지 익스포터를 사용하는 방법을 알아봅니다.
exl-id: 15d08758-cf75-43c0-9818-98a579d64183
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '997'
ht-degree: 0%

---

# 페이지 내보내기{#the-page-exporter}

Adobe Experience Manager(AEM)를 사용하면 이미지, `.js` 및 `.css` 파일을 포함하여 전체 웹 페이지로 페이지를 내보낼 수 있습니다.

구성된 경우 URL에서 `html`을(를) `export.zip`(으)로 바꾸어 브라우저에서 페이지 내보내기를 요청합니다. 이렇게 하면 참조된 에셋과 함께 렌더링된 페이지가 html 형식으로 포함된 아카이브(zip) 파일이 생성됩니다. 페이지의 모든 경로(예: 이미지 경로)는 아카이브에 포함된 파일 또는 서버의 리소스를 가리키도록 다시 작성됩니다. 그런 다음 아카이브 (zip) 파일을 브라우저에서 다운로드할 수 있습니다.

>[!NOTE]
>
>브라우저 및 설정에 따라 다운로드는 다음 중 하나입니다.
>
>* 보관 파일(`<page-name>.export.zip`)
>* 폴더(`<page-name>`)입니다. 아카이브 파일이 이미 확장되었습니다.

## 페이지 내보내기 {#exporting-a-page}

다음 단계에서는 페이지를 내보내는 방법을 설명하고 사이트에 대한 내보내기 템플릿이 있다고 가정합니다. 내보내기 템플릿은 페이지를 내보내는 방법을 정의하며 사이트에 따라 다릅니다. 내보내기 템플릿을 만들려면 [사이트에 대한 페이지 내보내기 구성 만들기](#creating-a-page-exporter-configuration-for-your-site)를 참조하십시오.

페이지를 내보내려면 다음을 수행하십시오.

1. **사이트** 콘솔에서 필요한 페이지로 이동합니다.

1. 페이지를 선택한 다음 **속성** 대화 상자를 엽니다.

1. **고급** 탭을 선택합니다.

1. **내보내기** 필드를 확장하여 내보내기 템플릿을 선택합니다.
사이트에 필요한 템플릿을 선택한 다음 **확인**&#x200B;을 사용하여 확인하십시오.

1. 페이지 속성 대화 상자를 닫으려면 **저장 및 닫기**&#x200B;를 선택하십시오.

1. 내보낼 페이지를 요청하여 URL에서 접미사 `html`을(를) `export.zip`(으)로 바꿉니다.

   예:
   * localhost:4502/content/we-retail/language-masters/en.html

   다음을 통해 액세스됨:
   * localhost:4502/content/we-retail/language-masters/en.export.zip

1. 아카이브 파일을 파일 시스템에 다운로드합니다.

1. 파일 시스템에서 필요한 경우 파일의 압축을 해제합니다. 확장하면 선택한 페이지와 같은 이름의 폴더가 있습니다. 이 폴더에는 다음이 포함되어 있습니다.

   * 하위 폴더 `content`은(는) 저장소의 페이지 경로를 반영하는 일련의 하위 폴더의 루트입니다.

      * 이 구조에는 선택한 페이지(`<page-name>.html`)에 대한 html 파일이 있습니다.

   * 기타 리소스(`.js`개 파일, `.css`개 파일, 이미지 등)는 내보내기 템플릿의 설정에 따라 배치됩니다.

1. 렌더링을 확인할 수 있도록 브라우저에서 페이지 html 파일(`<unzip-dir>/<path>/<to>/<page>/<page-path>.html`)을 엽니다.

## 사이트에 대한 페이지 내보내기 구성 만들기 {#creating-a-page-exporter-configuration-for-your-site}

페이지 내보내기는 [콘텐츠 동기화 프레임워크](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/contentsync/package-summary.html)를 기반으로 합니다. **페이지 속성** 대화 상자에서 사용할 수 있는 구성은 페이지에 필요한 종속성을 정의하는 내보내기 템플릿입니다.

페이지 내보내기가 트리거되면 내보내기 템플릿이 참조됩니다. 페이지 경로와 디자인 경로는 모두 동적으로 적용됩니다. 그런 다음 표준 콘텐츠 동기화 기능을 사용하여 zip 파일을 만듭니다.

기본 AEM 설치에는 `/etc/contentsync/templates/default` 아래에 기본 템플릿이 포함되어 있습니다.

* 이 템플릿은 저장소에 내보내기 템플릿이 없는 경우 대체 템플릿입니다.

* `default` 템플릿은 페이지 내보내기를 구성하는 방법을 보여 주므로 새 내보내기 템플릿의 기반으로 사용할 수 있습니다.

* 브라우저에서 템플릿의 노드 구조를 JSON 형식으로 보려면 다음 URL을 요청하십시오.
  `http://localhost:4502/etc/contentsync/templates/default.json`

페이지 내보내기 템플릿을 만드는 가장 쉬운 방법은 다음과 같습니다.

* `default` 템플릿 복사,

* 사이트에 적합한 새 이름을 할당합니다.

* 그런 다음 필요한 업데이트를 수행합니다.

완전히 새로운 템플릿을 만들려면 다음 작업을 수행하십시오.

1. **CRXDE Lite**&#x200B;에서 `/etc/contentsync/templates` 아래에 노드를 만드십시오.

   * `Name`: 사이트에 적합한 이름입니다(예: `<mysite>`). 이 이름은 페이지 내보내기 템플릿을 선택할 때 페이지 속성 대화 상자에 나타납니다.

   * `Type`: `nt:unstructured`

2. 여기에서 `mysite`이라고 하는 템플릿 노드 아래에 아래 설명된 구성 노드를 사용하여 노드 구조를 만듭니다.

## 페이지에 대한 페이지 내보내기 템플릿 활성화 {#activating-a-page-exporter-configuration-for-your-pages}

템플릿이 구성되면 사용할 수 있도록 합니다.

1. CRXDE에서 `/content` 분기의 필요한 페이지로 이동합니다. 개별 페이지이거나 하위 트리의 루트 페이지일 수 있습니다.

1. 페이지의 `jcr:content` 노드에서 속성을 만듭니다.
   * `Name`: `cq:exportTemplate`
   * `Type`: `String`
   * `Value`: 템플릿 경로(예: `/etc/contentsync/templates/mysite`)

### 페이지 내보내기 구성 노드 {#page-exporter-configuration-nodes}

[콘텐츠 동기화 프레임워크](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/contentsync/package-summary.html)를 사용하므로 템플릿은 노드 구조로 구성됩니다. 각 노드에는 zip 파일 생성 프로세스의 특정 작업을 정의하는 `type` 속성이 있습니다.

<!-- For more details about the type property, see the Overview of configuration types section in the Content Sync framework page.
-->

다음 노드를 사용하여 내보내기 템플릿을 작성할 수 있습니다.

* `page`
페이지 노드는 페이지 html을 zip 파일로 복사하는 데 사용됩니다. 다음과 같은 특징이 있습니다.

   * 필수 노드입니다.
   * `/etc/contentsync/templates/<mysite>` 아래에 있습니다.
   * `Name` 속성이 `page`(으)로 설정된 상태에서 정의됩니다.
   * 노드 유형은 `nt:unstructured`입니다.

  `page` 노드에는 다음 속성이 있습니다.

   * 값이 `pages`인 `type` 속성이 설정되었습니다.

   * 현재 페이지 경로가 구성에 동적으로 복사되므로 `path` 속성이 없습니다.
  <!--
  * The other properties are described in the Overview of configuration types section of the Content Sync framework.
  -->

* `rewrite`
다시 작성 노드는 내보낸 페이지에서 링크가 다시 작성되는 방식을 정의합니다. 다시 작성된 링크는 zip 파일에 포함된 파일이나 서버의 리소스를 가리킬 수 있습니다.
  <!-- See the Content Sync page for a complete description of the `rewrite` node. -->

* `design`
디자인 노드는 내보낸 페이지에 사용된 디자인을 복사하는 데 사용됩니다. 다음과 같은 특징이 있습니다.

   * 선택 사항입니다.
   * `/etc/contentsync/templates/<mysite>` 아래에 있습니다.
   * `Name` 속성이 `design`(으)로 설정된 상태에서 정의됩니다.
   * 노드 유형은 `nt:unstructured`입니다.

  `design` 노드에는 다음 속성이 있습니다.

   * `type` 속성이 `copy` 값으로 설정되어 있습니다.

   * 현재 페이지 경로가 구성에 동적으로 복사되므로 `path` 속성이 없습니다.

* `generic`
일반 노드는 clientlib `.js` 또는 `.css` 파일과 같은 리소스를 zip 파일로 복사하는 데 사용됩니다. 다음과 같은 특징이 있습니다.

   * 선택 사항입니다.
   * `/etc/contentsync/templates/<mysite>` 아래에 있습니다.
   * 특정 이름이 없습니다.
   * 노드 유형은 `nt:unstructured`입니다.
   * `type` 속성과 `type` 관련 속성이 있습니다. <!--Has a `type` property and any `type` related properties as defined in the Overview of configuration types section of the Content Sync framework.-->

  예를 들어 다음 구성 노드는 `mysite.clientlibs.js` 파일을 zip 파일에 복사합니다.

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

일부 특정 요구 사항을 충족하려면 [사용자 지정 업데이트 처리기](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/contentsync/handler/package-summary.html)를 구현하십시오.

<!-- To meet some specific requirements, you may need to implement a custom `type` property. To do so, see the Implementing a custom update handler section in the Content Sync page.
-->

## 프로그래밍 방식으로 페이지 내보내기 {#programmatically-exporting-a-page}

페이지를 프로그래밍 방식으로 내보내려면 [PageExporter](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/index.html?com/day/cq/wcm/contentsync/PageExporter.html) OSGI 서비스를 사용할 수 있습니다. 이 서비스를 사용하면 다음 작업을 수행할 수 있습니다.

* 페이지를 내보내고 HTTP 서블릿 응답에 씁니다.
* 페이지를 내보내고 특정 위치에 zip 파일을 저장합니다.

`export` 선택기와 `zip` 확장에 바인딩된 서블릿은 PageExporter 서비스를 사용합니다.

## 문제 해결 {#troubleshooting}

zip 파일 다운로드에 문제가 발생하면 저장소에서 `/var/contentsync` 노드를 삭제하고 내보내기 요청을 다시 보낼 수 있습니다.
