---
title: 페이지 템플릿 - 편집 가능
seo-title: 페이지 템플릿 - 편집 가능
description: 편집 가능한 템플릿은 개발자가 아닌 사람이 템플릿을 만들고 편집할 수 있도록 도입되었으며, 템플릿을 사용하여 만든 페이지에 대한 동적 연결을 유지하고 페이지 구성 요소를 보다 일반화하기 위해 고안되었습니다
seo-description: 편집 가능한 템플릿은 개발자가 아닌 사람이 템플릿을 만들고 편집할 수 있도록 도입되었으며, 템플릿을 사용하여 만든 페이지에 대한 동적 연결을 유지하고 페이지 구성 요소를 보다 일반화하기 위해 고안되었습니다
uuid: 61791960-fdef-4e49-878a-11fdf1d4f0ab
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 1099cc44-de6d-499e-8b52-f2f5811ae086
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5

---


# 페이지 템플릿 - 편집 가능 {#page-templates-editable}

편집 가능한 템플릿은 다음과 같이 도입되었습니다.

* 전문 작성자가 템플릿을 [만들고 편집할 수](/help/sites-authoring/templates.md)있습니다.

   * 이러한 전문 작성자를 **템플릿 작성자라고 합니다**
   * 템플릿 작성자는 `template-authors` 그룹의 구성원이어야 합니다.

* 템플릿에서 만든 모든 페이지에 대한 동적 연결을 유지하는 템플릿을 제공합니다. 이렇게 하면 템플릿의 변경 사항이 페이지 자체에 반영됩니다.
* 페이지 구성 요소를 좀 더 일반화하면 핵심 페이지 구성 요소를 사용자 지정 없이 사용할 수 있습니다.

편집 가능한 템플릿을 사용하면 페이지를 만드는 부분은 구성 요소 내에서 분리됩니다. UI에서 필요한 구성 요소 조합을 구성할 수 있으므로 각 페이지 변형에 대해 새 페이지 구성 요소를 개발할 필요가 없습니다.

>[!NOTE]
>
>[정적 템플릿을](/help/sites-developing/page-templates-static.md) 사용할 수도 있습니다.

이 문서:

* 편집 가능한 템플릿 만들기에 대한 개요를 제공합니다.

   * 자세한 내용은 페이지 [템플릿 만들기를 참조하십시오.](/help/sites-authoring/templates.md)

* 편집 가능한 템플릿을 만드는 데 필요한 관리/개발자 작업에 대해 설명합니다.
* 편집 가능한 템플릿의 기술적 이해를 설명합니다.

이 문서에서는 템플릿 작성 및 편집에 이미 익숙하다고 가정합니다. 템플릿 작성자에게 [노출된 대로](/help/sites-authoring/templates.md)편집 가능한 템플릿의 기능에 대해 자세히 설명하는 작성 문서 페이지 템플릿 만들기를 참조하십시오.

>[!NOTE]
>
>다음 자습서는 새 프로젝트에서 편집 가능한 페이지 템플릿을 설정하는 데에도 유용합니다.
>[AEM Sites 시작하기 파트 2 - 기본 페이지 및 템플릿 만들기](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop/part2.html)

## Creating a New Template {#creating-a-new-template}

편집 가능한 템플릿 만들기는 기본적으로 [템플릿 콘솔 및 템플릿 작성자의 템플릿 편집기를](/help/sites-authoring/templates.md) 사용하여 수행됩니다. 이 섹션에서는 이 프로세스에 대한 개요를 제공하며 기술 수준에서 발생하는 사항에 대한 설명을 따릅니다.

AEM 프로젝트에서 편집 가능한 템플릿을 사용하는 방법에 대한 자세한 내용은 Lazybones를 [사용하여 AEM 프로젝트 만들기를 참조하십시오](https://helpx.adobe.com/experience-manager/using/aem_lazybones.html).

편집 가능 템플릿을 새로 만들 때 다음을 수행합니다.

1. 템플릿의 [폴더를 만듭니다](#template-folders). 이는 필수는 아니지만 권장 우수 사례입니다.
1. [템플릿 유형을](#template-type)선택합니다. 이 [템플릿 정의를](#template-definitions)만들기 위해 복사됩니다.

   >[!NOTE]
   >
   >다양한 템플릿 유형이 기본적으로 제공됩니다. 필요한 경우 고유한 사이트 특정 템플릿 유형을 [](/help/sites-developing/page-templates-editable.md#creating-template-types) 만들 수도 있습니다.

1. 새 템플릿의 구조, 컨텐츠 정책, 초기 컨텐츠 및 레이아웃을 구성합니다.

   **구조**

   * 구조를 사용하면 템플릿의 구성 요소와 컨텐츠를 정의할 수 있습니다.
   * 템플릿 구조에 정의된 구성 요소는 결과 페이지 안에서 이동하거나 결과 페이지에서 삭제할 수 없습니다.

      * We.Retail 샘플 컨텐츠 외부에 있는 사용자 지정 폴더에 템플릿을 만드는 경우 기본 구성 요소를 선택하거나 핵심 구성 요소를 사용할 [수 있습니다](https://helpx.adobe.com/experience-manager/core-components/using/developing.html).
   * 페이지 작성자가 구성 요소를 추가 및 제거할 수 있도록 하려면 템플릿에 단락 시스템을 추가하십시오.
   * 초기 컨텐츠를 정의할 수 있도록 하려면 구성 요소 잠금을 해제했다가 다시 잠글 수 있습니다.
   템플릿 작성자가 구조를 정의하는 방법에 대한 자세한 내용은 페이지 템플릿 [만들기를 참조하십시오](/help/sites-authoring/templates.md#editing-a-template-structure-template-author).

   구조에 대한 자세한 내용은 이 [문서의 구조를](/help/sites-developing/page-templates-editable.md#structure) 참조하십시오.

   **정책**

   * 컨텐츠 정책은 구성 요소의 디자인 속성을 정의합니다.

      * 예: 사용 가능한 구성 요소 또는 최소/최대 크기.
   * 이러한 속성은 템플릿(및 템플릿으로 만든 페이지)에 적용될 수 있습니다.
   템플릿 작성자가 정책을 정의하는 방법에 대한 자세한 내용은 페이지 템플릿 [만들기를 참조하십시오](/help/sites-authoring/templates.md#editing-a-template-structure-template-author).

   정책에 대한 기술 세부 정보는 이 [문서의 컨텐츠](/help/sites-developing/page-templates-editable.md#content-policies) 정책을 참조하십시오.

   **초기 컨텐츠**

   * 초기 컨텐츠는 템플릿을 기반으로 페이지를 처음 만들 때 표시되는 컨텐츠를 정의합니다.
   * 그런 다음 페이지 작성자가 초기 컨텐츠를 편집할 수 있습니다.
   템플릿 작성자가 구조를 정의하는 방법에 대한 자세한 내용은 페이지 템플릿 [만들기를 참조하십시오](/help/sites-authoring/templates.md#editing-a-template-initial-content-author).

   초기 컨텐츠에 대한 자세한 내용은 이 [문서의 초기](/help/sites-developing/page-templates-editable.md#initial-content) 컨텐츠를 참조하십시오.

   **레이아웃**

   * 장치 범위에 대한 템플릿 레이아웃을 정의할 수 있습니다.
   * 템플릿에 대한 반응형 레이아웃은 페이지 작성과 동일하게 작동합니다.
   템플릿 작성자가 템플릿 레이아웃을 정의하는 방법에 대한 자세한 내용은 페이지 템플릿 [만들기를 참조하십시오](/help/sites-authoring/templates.md#editing-a-template-layout-template-author).

   템플릿 레이아웃에 대한 자세한 내용은 [이](/help/sites-developing/page-templates-editable.md#layout) 문서의 레이아웃을 참조하십시오.

1. 템플릿을 활성화한 다음 특정 컨텐츠 트리에 대해 허용합니다.

   * 템플릿을 활성화하거나 비활성화하여 페이지 작성자가 사용할 수 있도록 하거나 사용할 수 없게 할 수 있습니다.
   * 특정 페이지 분기에서 템플릿을 사용하거나 사용할 수 없게 지정할 수 있습니다.
   템플릿 작성자가 템플릿을 활성화하는 방법에 대한 자세한 내용은 페이지 템플릿 [만들기를 참조하십시오](/help/sites-authoring/templates.md#enabling-and-allowing-a-template-template-author).

   템플릿 활성화에 대한 자세한 내용은 이 [문서에서 템플릿](/help/sites-developing/page-templates-editable.md#enabling-and-allowing-a-template-for-use)사용 활성화 및 허용을 참조하십시오.

1. 컨텐츠 페이지를 만드는 데 사용합니다.

   * 템플릿을 사용하여 새 페이지를 만들 경우 정적 및 편집 가능 템플릿 간에 차이점은 없으며 구분하는 표시도 없습니다.
   * 페이지 작성자를 위해 프로세스는 투명하게 진행됩니다.
   페이지 작성자가 템플릿을 사용하여 페이지를 만드는 방법에 대한 자세한 내용은 페이지 [만들기 및 구성을 참조하십시오](/help/sites-authoring/managing-pages.md#templates).

   편집 가능한 템플릿으로 페이지 만들기에 대한 자세한 내용은 이 [문서의 결과 컨텐츠](/help/sites-developing/page-templates-editable.md#resultant-content-pages) 페이지를 참조하십시오.

>[!NOTE]
>
>편집기 클라이언트 라이브러리는 컨텐츠 페이지에 `cq.shared` 네임스페이스가 있다고 가정하고, 없으면 JavaScript 오류가 `Uncaught TypeError: Cannot read property 'shared' of undefined` 발생합니다.
>
>모든 샘플 컨텐츠 페이지에 `cq.shared`포함되어 있으므로 이를 기반으로 하는 모든 컨텐츠가 자동으로 포함됩니다 `cq.shared`. 그러나 샘플 컨텐츠를 기반으로 하지 않고 컨텐츠 페이지를 처음부터 새로 만들려면 `cq.shared` 네임스페이스를 포함해야 합니다.
>
>자세한 [내용은 클라이언트측 라이브러리](/help/sites-developing/clientlibs.md) 사용을 참조하십시오.

>[!CAUTION]
>
>[국제화](/help/sites-developing/i18n.md)해야 하는 정보는 템플릿에 입력하지 마십시오.

## 템플릿 폴더 {#template-folders}

템플릿을 구성하려면 다음 폴더를 사용할 수 있습니다.

* **글로벌**
* 사이트별 템플릿을 구성하기 위해 만드는 사이트별 폴더는 관리자 권한을 가진 계정으로 만들어집니다.

>[!NOTE]
>
>폴더를 중첩할 수 있지만 사용자가 템플릿 콘솔에서 폴더를 **보면** 기본 구조로 표시됩니다.

In a standard AEM instance the **global** folder already exists in the template console. 이 폴더는 기본 템플릿을 보유하며, 현재 폴더에 정책 및/또는 템플릿 유형을 찾을 수 없는 경우 폴백으로 작동합니다. 이 폴더에 기본 템플릿을 추가하거나 새 폴더를 만들 수 있습니다(권장).

>[!NOTE]
>
>전역 폴더를 사용하지 않고 사용자 지정된 템플릿을 저장할 새 폴더를 만드는 것이 좋습니다.

>[!CAUTION]
>
>폴더는 `admin` 권한이 있는 사용자가 만들어야 합니다.

템플릿 유형 및 정책은 다음 우선 순위에 따라 모든 폴더에서 상속됩니다.

1. 현재 폴더입니다.
1. 현재 폴더의 상위
1. `/conf/global`
1. `/apps`
1. `/libs`

허용된 모든 항목 목록이 만들어집니다. 구성이 겹치는 경우( `path`/ `label`) 현재 폴더에 가장 가까운 인스턴스만 사용자에게 표시됩니다.

새 폴더를 만들려면 다음 중 하나를 수행합니다.

* 프로그래밍 방식으로 또는 CRXDE Lite 사용
* 구성 브라우저 사용

## CRXDE Lite 사용 {#using-crxde-lite}

1. 프로그래밍 방식 또는 CRXDE Lite를 사용하여 인스턴스에 대해 새 폴더(/conf 아래)를 만들 수 있습니다.

   다음 구조를 사용해야 합니다.

   ```xml
   /conf
       <your-folder-name> [sling:Folder]
           settings [sling:Folder]
               wcm [cq:Page]
                   templates [cq:Page]
                   policies [cq:Page]
   ```

1. 그런 다음 폴더 루트 노드에서 다음 속성을 정의할 수 있습니다.

   `<your-folder-name> [sling:Folder]`

   이름: `jcr:title`

   * 유형: `String`

   * 값:템플릿 콘솔에 표시할 제목(폴더의 경우) **입니다** .

1. 표준 작성 권한 및 권한 *외에* (예:( `content-authors`) 이제 그룹을 할당하고 작성자가 새 폴더에 템플릿을 만들 수 있도록 필요한 액세스 권한(ACL)을 정의해야 합니다.

   이 `template-authors` 그룹은 할당해야 하는 기본 그룹입니다. 자세한 내용은 다음 섹션 [ACL 및 그룹을](/help/sites-developing/page-templates-editable.md#acls-and-groups) 참조하십시오.

   액세스 [권한 관리](/help/sites-administering/user-group-ac-admin.md#access-right-management) 및 지정에 대한 자세한 내용은 액세스 권한 관리를 참조하십시오.

### 구성 브라우저 사용 {#using-the-configuration-browser}

1. 전역 탐색 **-> 도구** > **구성** 브라우저로 **이동합니다**.

   기존 폴더는 ****&#x200B;전역 폴더를 포함하여 왼쪽에 나열됩니다.

1. **만들기**&#x200B;를 클릭합니다.
1. 구성 **만들기** 대화 상자에서 다음 필드를 구성해야 합니다.

   * **제목**:구성 폴더의 제목을 제공합니다.
   * **편집 가능한 템플릿**:이 폴더 내에서 편집 가능한 템플릿을 사용하려면 확인 표시

1. **만들기**&#x200B;를 클릭합니다

>[!NOTE]
>
>구성 브라우저에서 전역 폴더를 편집하고 편집 가능한 템플릿 **옵션을 활성화할** 수 있지만 이 방법은 권장되지 않습니다.

### ACL 및 그룹 {#acls-and-groups}

템플릿 폴더가 생성되면(CRXDE를 통해 또는 구성 브라우저를 통해) 템플릿 폴더에 적합한 그룹에 대해 ACL을 정의해야 적절한 보안을 보장합니다.

We.Retail [참조 구현의](/help/sites-developing/we-retail.md) 템플릿 폴더를 예로 사용할 수 있습니다.

#### 템플릿 작성자 그룹 {#the-template-authors-group}

이 `template-authors` 그룹은 템플릿 액세스를 관리하는 데 사용되는 그룹이며 AEM과 표준이 제공되지만 비어 있습니다. 프로젝트/사이트의 그룹에 사용자를 추가해야 합니다.

>[!CAUTION]
>
>이 `template-authors` 그룹은 새 템플릿을 만들 수 있어야 하는 사용자에게만 *적용됩니다* .
>
>템플릿 편집은 매우 강력하며, 제대로 종료되지 않은 경우 기존 템플릿을 중단할 수 있습니다. 따라서 이 역할은 초점이 맞춰져야 하며 자격을 갖춘 사용자만 포함해야 합니다.

다음 표에서는 템플릿 편집에 필요한 권한에 대해 자세히 설명합니다.

<table>
 <tbody>
  <tr>
   <th>경로</th>
   <th>역할/그룹</th>
   <th>권한<br /> </th>
   <th>설명</th>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/templates</code></td>
   <td>템플릿 작성자<br /> </td>
   <td>읽기, 쓰기, 복제</td>
   <td>사이트별 <code>/conf</code> 공간에서 템플릿을 작성, 읽기, 업데이트, 삭제 및 복제하는 템플릿 작성자</td>
  </tr>
  <tr>
   <td>익명의 웹 사용자</td>
   <td>read</td>
   <td>익명 웹 사용자는 페이지를 렌더링하는 동안 템플릿을 읽어야 합니다.</td>
  </tr>
  <tr>
   <td>컨텐츠 작성자</td>
   <td>복제</td>
   <td>복제컨텐츠 작성자는 페이지를 활성화할 때 페이지의 템플릿을 활성화해야 합니다</td>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/policies</code></td>
   <td><code>Template Author</code></td>
   <td>읽기, 쓰기, 복제</td>
   <td>사이트별 <code>/conf</code> 공간에서 템플릿을 작성, 읽기, 업데이트, 삭제 및 복제하는 템플릿 작성자</td>
  </tr>
  <tr>
   <td>익명 웹 사용자</td>
   <td>read</td>
   <td>익명 웹 사용자는 페이지를 렌더링하는 동안 정책을 읽어야 합니다.</td>
  </tr>
  <tr>
   <td>컨텐츠 작성자</td>
   <td>복제</td>
   <td>컨텐츠 작성자는 페이지를 활성화할 때 페이지 템플릿의 정책을 활성화해야 합니다</td>
  </tr>
  <tr>
   <td rowspan="2"><code>/conf/&lt;site&gt;/settings/template-types</code></td>
   <td>템플릿 작성자</td>
   <td>read</td>
   <td>템플릿 작성자는 사전 정의된 템플릿 유형 중 하나를 기반으로 새 템플릿을 만듭니다.</td>
  </tr>
  <tr>
   <td>익명의 웹 사용자</td>
   <td>없음</td>
   <td>익명 웹 사용자는 템플릿 유형에 액세스할 수 없습니다.</td>
  </tr>
 </tbody>
</table>

이 기본 `template-authors` `template-authors` 그룹은 모든 구성원이 모든 템플릿에 액세스하고 작성할 수 있는 프로젝트 설정만 다룹니다. 템플릿에 대한 액세스를 구분하기 위해 여러 템플릿 작성자 그룹이 필요한 보다 복잡한 설정의 경우 더 많은 사용자 정의 템플릿 작성자 그룹을 만들어야 합니다. 그러나 템플릿 작성자 그룹에 대한 권한은 여전히 동일합니다.

#### /conf/global 아래의 기존 템플릿 {#legacy-templates-under-conf-global}

템플릿은 더 이상 에 저장되지 `/conf/global`않지만 일부 기존 설치의 경우 이 위치에 템플릿이 여전히 있을 수 있습니다. 이러한 기존 상황에서만 다음 `/conf/global` 경로를 명시적으로 구성해야 합니다.

<table>
 <tbody>
  <tr>
   <th>경로</th>
   <th>역할/그룹</th>
   <th>권한<br /> </th>
   <th>설명</th>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/global/settings/wcm/templates</code></td>
   <td>템플릿 작성자</td>
   <td>읽기, 쓰기, 복제</td>
   <td>템플릿 작성자는 <code>/conf/global</code></td>
  </tr>
  <tr>
   <td>익명의 웹 사용자</td>
   <td>read</td>
   <td>익명 웹 사용자는 페이지를 렌더링하는 동안 템플릿을 읽어야 합니다.</td>
  </tr>
  <tr>
   <td>컨텐츠 작성자</td>
   <td>복제</td>
   <td>컨텐츠 작성자는 페이지를 활성화할 때 페이지의 템플릿을 활성화해야 합니다</td>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/global/settings/wcm/policies</code></td>
   <td><code>Template Author</code></td>
   <td>읽기, 쓰기, 복제</td>
   <td>템플릿 작성자는 <code>/conf/global</code></td>
  </tr>
  <tr>
   <td>익명의 웹 사용자</td>
   <td>read</td>
   <td>익명 웹 사용자는 페이지를 렌더링하는 동안 정책을 읽어야 합니다.</td>
  </tr>
  <tr>
   <td>컨텐츠 작성자</td>
   <td>복제</td>
   <td>컨텐츠 작성자는 페이지를 활성화할 때 페이지 템플릿의 정책을 활성화해야 합니다</td>
  </tr>
  <tr>
   <td rowspan="2"><code>/conf/global/settings/wcm/template-types</code></td>
   <td>템플릿 작성자</td>
   <td>read</td>
   <td>템플릿 작성자는 사전 정의된 템플릿 유형 중 하나를 기반으로 새 템플릿을 만듭니다</td>
  </tr>
  <tr>
   <td>익명의 웹 사용자</td>
   <td>없음</td>
   <td>익명 웹 사용자는 템플릿 유형에 액세스할 수 없습니다.</td>
  </tr>
 </tbody>
</table>

## Template Type {#template-type}

새 템플릿을 만들 때 템플릿 유형을 지정해야 합니다.

* 템플릿 유형은 템플릿에 대한 템플릿을 효과적으로 제공합니다. 새 템플릿을 만들 때 선택한 템플릿 유형의 구조와 초기 컨텐츠가 새 템플릿에 만드는 데 사용됩니다.

   * 템플릿 유형이 복사되어 템플릿을 만듭니다.
   * 복사본이 생성되면 템플릿과 템플릿 유형 사이의 유일한 연결은 정보 제공을 위한 정적 참조입니다.

* 템플릿 유형을 사용하여 다음을 정의할 수 있습니다.

   * 페이지 구성 요소의 리소스 유형입니다.
   * 템플릿 편집기에서 허용되는 구성 요소를 정의하는 루트 노드의 정책입니다.
   * 템플릿 유형에서 반응형 그리드에 대한 중단점과 모바일 에뮬레이터의 설정을 정의하는 것이 좋습니다. 구성은 개별 템플릿에 정의할 수도 있으므로 선택 사항입니다(템플릿 유형 및 모바일 장치 [그룹 참조](/help/sites-developing/page-templates-editable.md#p-template-type-and-mobile-device-groups-br-p)).

* AEM 파섹

   * 추가 예는 We.Retail [샘플 컨텐츠의 일부로](/help/sites-developing/we-retail.md) 제공됩니다.

* 템플릿 유형은 일반적으로 개발자가 정의합니다.

기본 템플릿 유형은 다음과 같이 저장됩니다.

* `/libs/settings/wcm/template-types`

>[!CAUTION]
>
>패스에 있는 것은 변경할 수 `/libs` 없습니다. 이는 다음에 인스턴스를 업그레이드할 때 의 컨텐츠를 `/libs` 덮어쓰게 되기 때문입니다(핫픽스 또는 기능 팩을 적용할 때 덮어쓸 수 있음).

사이트 특정 템플릿 유형은 다음과 같은 위치에 저장해야 합니다.

* `/apps/settings/wcm/template-types`

사용자 정의된 템플릿 유형에 대한 정의는 사용자 정의 폴더(권장)에 저장되거나 또는 에 저장되어야 `global`합니다. 예:

* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/template-types`
* `/conf/<my-folder>/settings/wcm/template-types`
* `/conf/global/settings/wcm/template-types`

>[!CAUTION]
>
>템플릿 유형은 올바른 폴더 구조(예:) `/settings/wcm/...`를 선택하지 않으면 템플릿 유형을 찾을 수 없습니다.

### 템플릿 유형 및 모바일 장치 그룹 {#template-type-and-mobile-device-groups-br}

편집 가능한 템플릿에 사용되는 [장치 그룹](/help/sites-developing/mobile.md#device-groups) (속성의 상대 경로로 설정 `cq:deviceGroups`)은 페이지 작성의 [레이아웃 모드에서](/help/sites-authoring/responsive-layout.md) 에뮬레이터로 사용할 수 있는 모바일 장치를 정의합니다. 이 값은 다음 두 위치에서 설정할 수 있습니다.

* 편집 가능한 템플릿 유형
* 편집 가능한 템플릿에서

새 편집 가능 템플릿을 만들 때 해당 값은 템플릿 유형에서 개별 템플릿으로 복사됩니다. 이 값이 유형에 설정되지 않은 경우 템플릿에서 설정할 수 있습니다. 템플릿이 만들어지면 유형에서 템플릿으로의 상속이 없습니다.

>[!CAUTION]
>
>의 값은 `cq:deviceGroups` 절대 경로가 아니라 `mobile/groups/responsive` 같은 상대 경로로 설정해야 `/etc/mobile/groups/responsive`합니다.

>[!NOTE]
>
>정적 [템플릿을](/help/sites-developing/page-templates-static.md)사용하면 의 값을 사이트 루트에서 설정할 `cq:deviceGroups` 수 있습니다.
>
>편집 가능한 템플릿에서 이 값은 이제 템플릿 수준에서 저장되며 페이지 루트 수준에서 지원되지 않습니다.

### 템플릿 유형 만들기 {#creating-template-types}

다른 템플릿의 기반으로 사용할 수 있는 템플릿을 만든 경우 이 템플릿을 템플릿 유형으로 복사할 수 있습니다.

1. 여기에 [설명된 대로](/help/sites-authoring/templates.md#creating-a-new-template-template-author)템플릿 유형을 기반으로 하는 편집 가능한 템플릿을 만들 수 있습니다.
1. CRXDE Lite를 사용하여 `templates` 노드에서 새로 만든 템플릿을 `template-types` 템플릿 폴더 [아래의](/help/sites-developing/page-templates-editable.md#template-folders)노드로 복사합니다.
1. 템플릿 폴더 `templates` [](/help/sites-developing/page-templates-editable.md#template-folders)아래의 노드에서 템플릿을 삭제합니다.
1. 노드 아래에 있는 템플릿 복사본에서 모든 `template-types` 및 `cq:template` 속성을 삭제합니다 `cq:templateType` `jcr:content` .

또한 GitHub에서 사용할 수 있는 편집 가능한 템플릿 예제를 기반으로 하여 고유한 템플릿 유형을 개발할 수도 있습니다.

GITHUB에 대한 코드

GitHub에서 이 페이지의 코드를 찾을 수 있습니다

* [GitHub에서 aem-sites-example-custom-template-type 프로젝트 열기](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type)
* 프로젝트를 ZIP [파일로 다운로드](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type/archive/master.zip)

## 템플릿 정의 {#template-definitions}

편집 가능한 템플릿에 대한 정의는 [사용자 정의 폴더](/help/sites-developing/page-templates-editable.md#template-folders) (권장)나 또는 에 저장됩니다 `global`. 예:

* `/conf/<my-folder>/settings/wcm/templates`
* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/templates`
* `/conf/global/settings/wcm/templates`

템플릿의 루트 노드는 다음과 같은 뼈대 구조를 `cq:Template` 가진 유형입니다.

```xml
<template-name>
  initial
    jcr:content
      root
        <component>
        ...
        <component>
  jcr:content
    @property status
  policies
    jcr:content
      root
        @property cq:policy
        <component>
          @property cq:policy
        ...
        <component>
          @property cq:policy
  structure
    jcr:content
      root
        <component>
        ...
        <component>
      cq:responsive
        breakpoints
  thumbnail.png
```

기본 요소는 다음과 같습니다.

* `<template-name>`

   * ` [initial](#initial-content)`
   * `jcr:content`
   * ` [structure](#structure)`
   * ` [policies](#policies)`
   * `thumbnail.png`

### jcr:content {#jcr-content}

이 노드에는 템플릿에 대한 속성이 있습니다.

* **이름**: `jcr:title`

* **이름**: `status`

   * ``**유형**: `String`

   * **값**: `draft`, `enabled` 또는 `disabled`

### 구조 {#structure}

결과 페이지의 구조를 정의합니다.

* 새 페이지를 만들 때 초기 컨텐츠( `/initial`)와 병합됩니다.
* 구조에 대한 변경 사항은 템플릿으로 만든 모든 페이지에 반영됩니다.
* ( `root` ) `structure/jcr:content/root`) 노드는 결과 페이지에서 사용할 수 있는 구성 요소 목록을 정의합니다.

   * 템플릿 구조에 정의된 구성 요소는 결과 페이지에서 이동하거나 삭제할 수 없습니다.
   * 구성 요소의 잠금을 해제하면 `editable` 속성이 로 설정됩니다 `true`.

   * 이미 콘텐트가 들어 있는 구성 요소의 잠금을 해제하면 이 콘텐트가 `initial` 분기로 이동합니다.

* 노드는 응답형 레이아웃에 대한 정의를 보유합니다. `cq:responsive`

### 초기 컨텐츠 {#initial-content}

작성 시 새 페이지에 포함할 초기 컨텐츠를 정의합니다.

* 새 페이지에 복사되는 `jcr:content` 노드를 포함합니다.
* 새 페이지를 만들 때 구조( `/structure`)와 병합됩니다.
* 초기 컨텐츠를 만든 후 변경한 경우 기존 페이지는 업데이트되지 않습니다.
* 노드에는 결과 페이지에서 사용할 수 있는 구성 요소 목록이 들어 `root` 있습니다.
* 구조 모드에서 컨텐츠가 구성 요소에 추가되고 해당 구성 요소가 이후에 잠금 해제되거나 그 반대로 잠긴 경우, 이 컨텐츠는 초기 컨텐츠로 사용됩니다.

### 레이아웃 {#layout}

템플릿을 [편집할 때 레이아웃을](/help/sites-authoring/templates.md)정의할 수 있으므로 [구성할](/help/sites-authoring/responsive-layout.md) 수 있는 [표준 반응형 레이아웃을](/help/sites-administering/configuring-responsive-layout.md)사용합니다.

### Content Policies {#content-policies}

컨텐츠(또는 디자인) 정책은 구성 요소의 디자인 속성을 정의합니다. 예: 사용 가능한 구성 요소 또는 최소/최대 크기. 이러한 속성은 템플릿(및 템플릿으로 만든 페이지)에 적용될 수 있습니다. 템플릿 편집기에서 컨텐츠 정책을 만들고 선택할 수 있습니다.

* 노드의 `cq:policy`속성 `root`
   `/conf/<your-folder>/settings/wcm/templates/<your-template>/policies/jcr:content/root`
페이지의 단락 시스템에 대한 컨텐츠 정책에 대한 상대 참조를 제공합니다.

* 아래의 구성 요소 명시적 `cq:policy`노드에서 개별 구성 요소에 대한 정책에 대한 링크를 `root`제공합니다.

* 실제 정책 정의는 다음과 같이 저장됩니다.
   `/conf/<your-folder>/settings/wcm/policies/wcm/foundation/components`

>[!NOTE]
>
>정책 정의의 경로는 구성 요소의 경로에 따라 다릅니다. `cq:policy` 구성 자체에 대한 상대 참조를 보유합니다.

>[!NOTE]
>
>편집 가능한 템플릿으로 만든 페이지는 페이지 편집기에서 디자인 모드를 제공하지 않습니다.
>
>편집 가능한 템플릿의 `policies` 트리는 다음 아래에서 정적 템플릿의 디자인 모드 구성과 동일한 계층 구조를 갖습니다.
>
>`/etc/designs/<my-site>/jcr:content/<component-name>`
>
>정적 템플릿의 디자인 모드 구성은 페이지 구성 요소별로 정의되었습니다.

### 페이지 정책 {#page-policies}

페이지 정책을 사용하면 템플릿 또는 결과 페이지에서 페이지의 [컨텐츠 정책](#content-policies) (기본 parsys)을 정의할 수 있습니다.

### 템플릿 사용 활성화 및 허용 {#enabling-and-allowing-a-template-for-use}

1. **템플릿 활성화**

   템플릿을 사용하려면 다음 중 한 가지 방법으로 템플릿을 활성화해야 합니다.

   * [템플릿](/help/sites-authoring/templates.md#enablingatemplateauthor) 콘솔에서 템플릿 **활성화** .

   * 노드에서 상태 속성을 `jcr:content` 설정합니다.

      * 예를 들면 다음과 같습니다.
         `/conf/<your-folder>/settings/wcm/templates/<your-template>/jcr:content`

      * 속성을 정의합니다.

         * 이름:status
         * 유형:문자열
         * 값: `enabled`

1. **허용된 템플릿**

   * [하위 분기의 해당 페이지 또는 **루트&#x200B;**](/help/sites-authoring/templates.md#allowing-a-template-author)페이지의 페이지 속성에 허용된 템플릿 경로를 정의합니다.
   * 속성을 설정합니다.
      `cq:allowedTemplates`
필요한 분기의 `jcr:content` 노드에 있습니다.
   예를 들어 값이

   `/conf/<your-folder>/settings/wcm/templates/.*`

## 결과 컨텐츠 페이지 {#resultant-content-pages}

편집 가능한 템플릿으로 만든 페이지:

* 템플릿에서 `structure` 및 템플릿에서 병합된 하위 트리를 사용하여 `initial` 만듭니다.

* 템플릿 및 템플릿 유형에 들어 있는 정보에 대한 참조가 있습니다. 이렇게 하려면 속성이 있는 `jcr:content` 노드를 사용합니다.

   * `cq:template`
실제 템플릿에 대한 동적 참조를 제공합니다.템플릿 변경 사항이 실제 페이지에 반영되도록 합니다.

   * `cq:templateType`
템플릿 유형에 대한 참조를 제공합니다.

![chlimage_1-71](assets/chlimage_1-71.png)

위의 다이어그램은 템플릿, 컨텐츠 및 구성 요소가 어떻게 상호 연관되어 있는지 보여줍니다.

* 컨트롤러 - `/content/<my-site>/<my-page>`템플릿을 참조하는 결과 페이지입니다. 컨텐츠는 전체 프로세스를 제어합니다. 정의에 따라 해당 템플릿 및 구성 요소에 액세스합니다.

* 구성 - `/conf/<my-folder>/settings/wcm/templates/<my-template>`[템플릿 및 관련 컨텐츠 정책은](#template-definitions) 페이지 구성을 정의합니다.

* 모델 - OSGi 번들 [OSGI 번들은](/help/sites-deploying/osgi-configuration-settings.md) 기능을 구현합니다.

* 보기 - `/apps/<my-site>/components`작성 환경과 게시 환경 모두에서 컨텐츠는 [구성 요소로](/help/sites-developing/components.md)렌더링됩니다.

페이지를 렌더링할 때:

* **템플릿**:

   * 해당 `cq:template` 노드의 `jcr:content` 속성이 참조되어 해당 페이지에 해당하는 템플릿에 액세스합니다.

* **구성 요소**:

   * 페이지 구성 요소는 템플릿의 `structure/jcr:content` 트리를 페이지의 `jcr:content` 트리와 병합합니다.

   * 페이지 구성 요소는 작성자가 편집 가능한 것으로 표시된 템플릿 구조의 노드(및 하위)만 편집할 수 있도록 허용합니다.
   * 페이지에서 구성 요소를 렌더링할 때 해당 구성 요소의 상대 경로는 `jcr:content` 노드에서 가져옵니다.그런 다음 템플릿의 `policies/jcr:content` 노드 아래에 있는 동일한 경로를 검색합니다.

      * 이 노드의 `cq:policy` 속성은 실제 컨텐트 정책을 가리킵니다(즉, 해당 구성 요소에 대한 디자인 구성을 보유함).

      * 따라서 동일한 컨텐츠 정책 구성을 다시 사용하는 여러 개의 템플릿이 있을 수 있습니다.
