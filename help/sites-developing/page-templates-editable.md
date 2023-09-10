---
title: 페이지 템플릿 - 편집 가능
description: 개발자가 아닌 사용자도 템플릿을 만들고 편집할 수 있으며, 템플릿에서 만든 페이지에 동적 연결을 유지하는 템플릿을 제공하고 페이지 구성 요소를 보다 일반화할 수 있는 편집 가능한 템플릿이 도입되었습니다
uuid: 61791960-fdef-4e49-878a-11fdf1d4f0ab
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 1099cc44-de6d-499e-8b52-f2f5811ae086
docset: aem65
exl-id: dcb66b6d-d731-493e-8936-12d529f6cbde
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '3221'
ht-degree: 7%

---

# 페이지 템플릿 - 편집 가능 {#page-templates-editable}

편집 가능한 템플릿은에 도입되었습니다.

* 전문 작성자의 허용 [템플릿 만들기 및 편집](/help/sites-authoring/templates.md).

   * 이러한 전문 작성자를 라고 합니다. **템플릿 작성자**
   * 템플릿 작성자는 의 멤버여야 합니다. `template-authors` 그룹입니다.

* 템플릿에서 만든 모든 페이지에 대한 동적 연결을 유지하는 템플릿을 제공합니다. 이렇게 하면 템플릿에 대한 모든 변경 사항이 페이지 자체에 반영됩니다.
* 맞춤화 없이 핵심 페이지 구성 요소를 사용할 수 있도록 페이지 구성 요소를 보다 일반화하십시오.

편집 가능한 템플릿을 사용하면 페이지를 만드는 조각이 구성 요소 내에 격리됩니다. UI에서 필요한 구성 요소 조합을 구성할 수 있으므로 각 페이지 변형에 대해 새로운 페이지 구성 요소를 개발할 필요가 없습니다.

>[!NOTE]
>
>[정적 템플릿](/help/sites-developing/page-templates-static.md) 사용할 수도 있습니다.

이 문서는

* 편집 가능한 템플릿 만들기에 대한 개요를 제공합니다.

   * 자세한 내용은 다음을 참조하십시오. [페이지 템플릿 만들기](/help/sites-authoring/templates.md)

* 편집 가능한 템플릿을 만드는 데 필요한 관리/개발자 작업에 대해 설명합니다.
* 편집 가능한 템플릿의 기술 정보를 설명합니다

이 문서에서는 사용자가 이미 템플릿 만들기 및 편집에 익숙하다고 가정합니다. 작성 문서 참조 [페이지 템플릿 만들기](/help/sites-authoring/templates.md)템플릿 작성자에게 노출된 편집 가능한 템플릿의 기능에 대해 자세히 설명합니다.

>[!NOTE]
>
>다음 튜토리얼은 새 프로젝트에서 편집 가능한 페이지 템플릿을 설정하는 데 유용할 수도 있습니다.
>[AEM Sites 2부 시작하기 - 기본 페이지 및 템플릿 만들기](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/project-archetype/pages-templates.html?lang=en)

## 새 템플릿 만들기 {#creating-a-new-template}

편집 가능한 템플릿 만들기는 주로 [템플릿 콘솔 및 템플릿 편집기](/help/sites-authoring/templates.md) 템플릿 작성자에 의해 제어됩니다. 이 섹션은 이 프로세스에 대한 개요를 제공하며 다음 기술 수준에서 발생하는 사항에 대한 설명을 제공합니다.

AEM 프로젝트에서 편집 가능한 템플릿을 사용하는 방법에 대한 자세한 내용은 을 참조하십시오. [Lazybones를 사용하여 AEM 프로젝트 만들기](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/create-aem-project-structure-using-lazybones/m-p/186478).

편집 가능 템플릿을 새로 만들 때 다음 작업을 수행합니다.

1. 만들기 [템플릿용 폴더](#template-folders). 이 폴더는 필수가 아니지만 모범 사례에 권장됩니다.
1. 선택 [템플릿 유형](#template-type). 이 유형은 다음을 만들기 위해 복사됩니다. [템플릿 정의](#template-definitions).

   >[!NOTE]
   >
   >다양한 템플릿 유형이 즉시 제공됩니다. 다음을 수행할 수도 있습니다. [사이트별 템플릿 유형 만들기](/help/sites-developing/page-templates-editable.md#creating-template-types)필요한 경우 입니다.

1. 새 템플릿의 구조, 콘텐츠 정책, 초기 콘텐츠 및 레이아웃을 구성합니다.

   **구조**

   * 이 구조를 사용하여 템플릿의 구성 요소와 콘텐츠를 정의할 수 있습니다.
   * 템플릿 구조에 정의된 구성 요소는 결과 페이지 안에서 이동하거나 결과 페이지에서 삭제할 수 없습니다.

      * 의 외부에 있는 사용자 지정 폴더에서 템플릿을 만드는 경우 `We.Retail` 샘플 콘텐츠에서 기초 구성 요소를 선택하거나 [핵심 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/overview.html?lang=ko-KR).

   * 페이지 작성자가 구성 요소를 추가 및 제거할 수 있도록 하려면 템플릿에 단락 시스템을 추가하십시오.
   * 초기 콘텐츠를 정의할 수 있도록 하려면 구성 요소 잠금을 해제했다가 다시 잠글 수 있습니다.

   템플릿 작성자가 구조를 정의하는 방법에 대한 자세한 내용은 [페이지 템플릿 만들기](/help/sites-authoring/templates.md#editing-a-template-structure-template-author).

   구조에 대한 기술적인 세부 정보는 를 참조하십시오. [구조](/help/sites-developing/page-templates-editable.md#structure) 이 문서에서.

   **정책**

   * 콘텐츠 정책은 구성 요소의 디자인 속성을 정의합니다.

      * 예: 사용 가능한 구성 요소 또는 최소/최대 크기.

   * 이러한 정책은 템플릿(및 템플릿으로 만든 페이지)에 적용할 수 있습니다.

   템플릿 작성자가 정책을 정의하는 방법에 대한 자세한 내용은 [페이지 템플릿 만들기](/help/sites-authoring/templates.md#editing-a-template-structure-template-author).

   정책에 대한 기술적인 세부 정보는 다음을 참조하십시오. [컨텐츠 정책](/help/sites-developing/page-templates-editable.md#content-policies) 이 문서에서.

   **초기 콘텐츠**

   * 초기 콘텐츠 는 템플릿을 기반으로 페이지를 처음 만들 때 표시되는 콘텐츠를 정의합니다.
   * 그런 다음 페이지 작성자는 초기 콘텐츠를 편집할 수 있습니다.

   템플릿 작성자가 구조를 정의하는 방법에 대한 자세한 내용은 [페이지 템플릿 만들기](/help/sites-authoring/templates.md#editing-a-template-initial-content-author).

   초기 콘텐츠에 대한 자세한 내용은 [초기 컨텐츠](/help/sites-developing/page-templates-editable.md#initial-content) 이 문서에서.

   **레이아웃**

   * 디바이스 범위에 대한 템플릿 레이아웃을 정의할 수 있습니다.
   * 템플릿에 대한 반응형 레이아웃은 페이지 작성의 경우와 마찬가지로 작동합니다.

   템플릿 작성자가 템플릿 레이아웃을 정의하는 방법에 대한 자세한 내용은 [페이지 템플릿 만들기](/help/sites-authoring/templates.md#editing-a-template-layout-template-author).

   템플릿 레이아웃에 대한 자세한 내용은 [레이아웃](/help/sites-developing/page-templates-editable.md#layout) 이 문서에서.

1. 템플릿을 활성화한 다음 특정 콘텐츠 트리에 대해 허용합니다.

   * 페이지 작성자가 템플릿을 사용하거나 사용할 수 없게 하기 위해 템플릿을 활성화하거나 비활성화할 수 있습니다.
   * 특정 페이지 분기에서 템플릿을 사용하거나 사용할 수 없게 지정할 수 있습니다.

   템플릿 작성자가 템플릿을 활성화하는 방법에 대한 자세한 내용은 [페이지 템플릿 만들기](/help/sites-authoring/templates.md#enabling-and-allowing-a-template-template-author).

   템플릿 활성화에 대한 기술적인 세부 정보는 다음을 참조하십시오. [템플릿 활성화 및 허용](/help/sites-developing/page-templates-editable.md#enabling-and-allowing-a-template-for-use)이 문서의 e

1. 콘텐츠 페이지를 만드는 데 사용합니다.

   * 템플릿을 사용하여 페이지를 만들 때 정적 템플릿과 편집 가능한 템플릿 간에 가시적인 차이점과 표시가 없습니다.
   * 페이지 작성자의 경우 프로세스가 투명합니다.

   페이지 작성자가 템플릿을 사용하여 페이지를 만드는 방법에 대한 자세한 내용은 을 참조하십시오. [페이지 생성 및 구성](/help/sites-authoring/managing-pages.md#templates).

   편집 가능한 템플릿을 사용하여 페이지를 만드는 방법에 대한 자세한 내용은 [결과 컨텐츠 페이지](/help/sites-developing/page-templates-editable.md#resultant-content-pages) 이 문서에서.

>[!TIP]
>
>국제화해야 하는 정보는 템플릿에 입력하지 마십시오. 내재화 목적으로 [핵심 구성 요소의 현지화 기능](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/localization.html) 권장됩니다.

>[!NOTE]
>
>템플릿은 페이지 생성 워크플로를 간소화할 수 있는 강력한 도구입니다. 그러나 템플릿이 너무 많으면 작성자를 압도하고 페이지 작성에 혼란을 초래할 수 있습니다. 가장 좋은 방법은 템플릿의 수를 100 미만으로 유지하는 것입니다.
>
>성능에 영향을 미칠 수 있으므로 1,000개 이상의 템플릿을 사용하지 않는 것이 좋습니다.

>[!NOTE]
>
>편집기 클라이언트 라이브러리는 `cq.shared` 컨텐츠 페이지의 네임스페이스입니다. 없으면 JavaScript 오류가 발생합니다 `Uncaught TypeError: Cannot read property 'shared' of undefined`.
>
>모든 샘플 콘텐츠 페이지에는 다음이 포함되어 있습니다. `cq.shared`, 따라서 이를 기반으로 하는 모든 컨텐츠는 자동으로 다음을 포함합니다 `cq.shared`. 그러나 샘플 콘텐츠를 기반으로 하지 않고 처음부터 고유한 콘텐츠 페이지를 만들려는 경우에는 다음을 포함해야 합니다. `cq.shared` 네임스페이스입니다.
>
>다음을 참조하십시오 [클라이언트측 라이브러리 사용](/help/sites-developing/clientlibs.md) 추가 정보.

## 템플릿 폴더 {#template-folders}

템플릿을 구성할 때는 다음 폴더를 사용할 수 있습니다.

* **글로벌**
* 사이트별 템플릿을 구성하기 위해 만드는 사이트별 폴더는 관리자 권한이 있는 계정으로 만들어집니다.

>[!NOTE]
>
>폴더를 중첩할 수 있음에도 불구하고 **템플릿** 콘솔은 평면 구조로 제공됩니다.

표준 AEM 인스턴스에서 **글로벌** 폴더가 템플릿 콘솔에 있습니다. 이 폴더는 기본 템플릿을 보유하고 있으며 현재 폴더에 정책 및/또는 템플릿 유형이 없는 경우 폴백으로 작동합니다. 이 폴더에 기본 템플릿을 추가하거나 폴더를 만들 수 있습니다(권장).

>[!NOTE]
>
>사용자 지정된 템플릿을 보유하는 폴더를 만들고 전역 폴더를 사용하지 않는 것이 좋습니다.

>[!CAUTION]
>
>폴더는 다음을 사용하여 사용자가 만들어야 합니다. `admin` 권한.

템플릿 유형 및 정책은 다음 우선 순위에 따라 모든 폴더에 상속됩니다.

1. 현재 폴더입니다.
1. 현재 폴더의 상위 또는 상위.
1. `/conf/global`
1. `/apps`
1. `/libs`

허용된 모든 항목의 목록이 만들어집니다. 구성이 겹치는 경우( `path`/ `label`)에서 현재 폴더에 가장 가까운 인스턴스만 사용자에게 표시됩니다.

폴더를 만들려면 다음 작업을 수행하십시오.

* 프로그래밍 방식으로 또는 CRXDE Lite 사용
* 구성 브라우저 사용

## CRXDE Lite 사용 {#using-crxde-lite}

1. 프로그래밍 방식으로 또는 CRXDE Lite을 사용하여 인스턴스에 대해 새 폴더(/conf 아래에)를 만들 수 있습니다.

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

   * 값: 폴더에 표시할 제목 **템플릿** 콘솔.

1. 위치 *추가* 표준 작성 권한 및 권한(예: `content-authors`) 그룹을 할당하고 작성자가 새 폴더에 템플릿을 만들 수 있는 필수 액세스 권한(ACL)을 정의합니다.

   다음 `template-authors` group은 할당해야 하는 기본 그룹입니다. 다음 섹션을 참조하십시오 [ACL 및 그룹](/help/sites-developing/page-templates-editable.md#acls-and-groups) 을 참조하십시오.

   다음을 참조하십시오 [액세스 권한 관리](/help/sites-administering/user-group-ac-admin.md#access-right-management) 액세스 권한 관리 및 할당에 대한 전체 세부 정보.

### 구성 브라우저 사용 {#using-the-configuration-browser}

1. 다음으로 이동 **전역 탐색** -> **도구** > **구성 브라우저**.

   기존 폴더는 다음을 포함하여 왼쪽에 나열됩니다. **글로벌** 폴더를 삭제합니다.

1. **만들기**&#x200B;를 클릭합니다.
1. 다음에서 **구성 만들기** 대화 상자에서 다음 필드를 구성해야 합니다.

   * **제목**: 구성 폴더의 제목 제공
   * **편집 가능한 템플릿**: 이 폴더 내에서 편집 가능한 템플릿을 허용하려면 선택합니다

1. **만들기**&#x200B;를 클릭합니다

>[!NOTE]
>
>구성 브라우저에서 전역 폴더를 편집하고 를 활성화할 수 있습니다. **편집 가능한 템플릿** 이 폴더 내에 템플릿을 만들려면 옵션을 선택합니다. 그러나 이 방법은 권장되는 모범 사례는 아닙니다.
>
>다음을 참조하십시오. [구성 브라우저](/help/sites-administering/configurations.md) 설명서 를 참조하십시오.

### ACL 및 그룹 {#acls-and-groups}

CRXDE를 통해 또는 구성 브라우저를 사용하여 템플릿 폴더를 만든 후 적절한 보안을 위해 템플릿 폴더의 적절한 그룹에 대해 ACL을 정의해야 합니다.

의 템플릿 폴더 [`We.Retail` 참조 구현](/help/sites-developing/we-retail.md) 를 예로 사용할 수 있습니다.

#### 템플릿-작성자 그룹 {#the-template-authors-group}

다음 `template-authors` group 은 템플릿에 대한 액세스를 관리하는 데 사용되는 그룹이며, AEM과 함께 기본으로 제공되지만 는 비어 있습니다. 프로젝트/사이트의 그룹에 사용자를 추가해야 합니다.

>[!CAUTION]
>
>다음 `template-authors` 그룹: *전용* 템플릿을 만들 수 있어야 하는 사용자용
>
>템플릿 편집은 강력하며 제대로 수행하지 않으면 기존 템플릿이 손상될 수 있습니다. 따라서 이 역할에 초점을 맞추고 자격 있는 사용자만 포함해야 합니다.

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
   <td>사이트별 템플릿을 작성, 읽기, 업데이트, 삭제 및 복제하는 템플릿 작성자 <code>/conf</code> 공간</td>
  </tr>
  <tr>
   <td>익명 웹 사용자</td>
   <td>읽기</td>
   <td>익명 웹 사용자는 페이지를 렌더링하는 동안 템플릿을 읽어야 합니다.</td>
  </tr>
  <tr>
   <td>콘텐츠 작성자</td>
   <td>복제</td>
   <td>replicateContent 작성자는 페이지를 활성화할 때 페이지의 템플릿을 활성화해야 합니다</td>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/policies</code></td>
   <td><code>Template Author</code></td>
   <td>읽기, 쓰기, 복제</td>
   <td>사이트별 템플릿을 작성, 읽기, 업데이트, 삭제 및 복제하는 템플릿 작성자 <code>/conf</code> 공간</td>
  </tr>
  <tr>
   <td>익명 웹 사용자</td>
   <td>읽기</td>
   <td>익명 웹 사용자는 페이지를 렌더링하는 동안 정책을 읽어야 합니다.</td>
  </tr>
  <tr>
   <td>콘텐츠 작성자</td>
   <td>복제</td>
   <td>콘텐츠 작성자는 페이지를 활성화할 때 페이지 템플릿의 정책을 활성화해야 합니다</td>
  </tr>
  <tr>
   <td rowspan="2"><code>/conf/&lt;site&gt;/settings/template-types</code></td>
   <td>템플릿 작성자</td>
   <td>읽기</td>
   <td>템플릿 작성자는 미리 정의된 템플릿 유형 중 하나를 기반으로 템플릿을 만듭니다.</td>
  </tr>
  <tr>
   <td>익명 웹 사용자</td>
   <td>없음</td>
   <td>익명 웹 사용자는 템플릿 유형에 액세스할 수 없습니다.</td>
  </tr>
 </tbody>
</table>

이 기본값 `template-authors` 그룹은 프로젝트 설정만 다룹니다. `template-authors` 구성원은 모든 템플릿에 액세스하고 작성할 수 있습니다. 여러 템플릿 작성자 그룹이 템플릿에 대한 액세스 권한을 구분해야 하는 더 복잡한 설정의 경우 더 많은 사용자 지정 템플릿 작성자 그룹을 만들어야 합니다. 그러나 템플릿 작성자 그룹에 대한 권한은 여전히 동일합니다.

#### /conf/global 아래의 기존 템플릿 {#legacy-templates-under-conf-global}

템플릿 저장 안 함 `/conf/global`. 그러나 일부 이전 설치의 경우 이 위치에 템플릿이 남아 있을 수 있습니다. *전용* 이러한 기존 상황에서는 다음을 수행해야 합니다. `/conf/global` 경로를 명시적으로 구성해야 합니다.

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
   <td>에서 템플릿을 작성, 읽기, 업데이트, 삭제 및 복제하는 템플릿 작성자 <code>/conf/global</code></td>
  </tr>
  <tr>
   <td>익명 웹 사용자</td>
   <td>읽기</td>
   <td>익명 웹 사용자는 페이지를 렌더링하는 동안 템플릿을 읽어야 합니다.</td>
  </tr>
  <tr>
   <td>콘텐츠 작성자</td>
   <td>복제</td>
   <td>콘텐츠 작성자는 페이지를 활성화할 때 페이지의 템플릿을 활성화해야 합니다</td>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/global/settings/wcm/policies</code></td>
   <td><code>Template Author</code></td>
   <td>읽기, 쓰기, 복제</td>
   <td>에서 템플릿을 작성, 읽기, 업데이트, 삭제 및 복제하는 템플릿 작성자 <code>/conf/global</code></td>
  </tr>
  <tr>
   <td>익명 웹 사용자</td>
   <td>읽기</td>
   <td>익명 웹 사용자는 페이지를 렌더링하는 동안 정책을 읽어야 합니다.</td>
  </tr>
  <tr>
   <td>콘텐츠 작성자</td>
   <td>복제</td>
   <td>콘텐츠 작성자는 페이지를 활성화할 때 페이지 템플릿의 정책을 활성화해야 합니다</td>
  </tr>
  <tr>
   <td rowspan="2"><code>/conf/global/settings/wcm/template-types</code></td>
   <td>템플릿 작성자</td>
   <td>읽기</td>
   <td>템플릿 작성자는 미리 정의된 템플릿 유형 중 하나를 기반으로 템플릿을 만듭니다</td>
  </tr>
  <tr>
   <td>익명 웹 사용자</td>
   <td>없음</td>
   <td>익명 웹 사용자는 템플릿 유형에 액세스할 수 없습니다.</td>
  </tr>
 </tbody>
</table>

## 템플릿 유형 {#template-type}

템플릿을 만들 때 템플릿 유형을 지정합니다.

* 템플릿 유형은 템플릿에 템플릿을 효과적으로 제공합니다. 템플릿을 만들 때 선택한 템플릿 유형의 구조 및 초기 콘텐츠를 사용하여 템플릿을 만듭니다.

   * 템플릿 유형이 복사되어 템플릿이 생성됩니다.
   * 복사가 발생하면 템플릿과 템플릿 유형 간의 유일한 연결은 정보 제공을 위한 정적 참조입니다.

* 템플릿 유형을 사용하면 다음을 정의할 수 있습니다.

   * 페이지 구성 요소의 리소스 유형입니다.
   * 템플릿 편집기에서 허용되는 구성 요소를 정의하는 루트 노드의 정책입니다.
   * Adobe은 템플릿 유형에서 응답형 격자에 대한 중단점을 정의하고 모바일 에뮬레이터를 설정하는 것을 권장합니다. 구성은 개별 템플릿에서도 정의할 수 있으므로 이 단계는 선택 사항입니다(참조). [템플릿 유형 및 모바일 장치 그룹](/help/sites-developing/page-templates-editable.md#p-template-type-and-mobile-device-groups-br-p)).

* AEM에서는 HTML5 페이지 및 적응형 양식 페이지와 같이 바로 사용할 수 있는 다양한 템플릿 유형을 제공합니다.

   * 추가 예는 의 일부로 제공됩니다. [`We.Retail`](/help/sites-developing/we-retail.md) 샘플 컨텐츠입니다.

* 템플릿 유형은 일반적으로 개발자에 의해 정의됩니다.

기본 제공 템플릿 유형은 아래에 저장됩니다.

* `/libs/settings/wcm/template-types`

>[!CAUTION]
>
>의 아무 것도 변경하지 마십시오. `/libs` 경로. 그 이유는 의 콘텐츠가 `/libs` 는 다음에 인스턴스를 업그레이드할 때 덮어쓰기됩니다(그리고 핫픽스 또는 기능 팩을 적용할 때 덮어쓰기될 수 있음).

사이트별 템플릿 유형은 다음과 유사한 위치에 저장해야 합니다.

* `/apps/settings/wcm/template-types`

사용자 정의된 템플릿 유형에 대한 정의는 사용자 정의 폴더(권장) 또는 `global`. 예:

* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/template-types`
* `/conf/<my-folder>/settings/wcm/template-types`
* `/conf/global/settings/wcm/template-types`

>[!CAUTION]
>
>템플릿 유형은 올바른 폴더 구조를 준수해야 합니다(즉, `/settings/wcm/...`), 그렇지 않으면 템플릿 유형을 찾을 수 없습니다.

### 템플릿 유형 및 모바일 장치 그룹 {#template-type-and-mobile-device-groups-br}

다음 [장치 그룹](/help/sites-developing/mobile.md#device-groups) 편집 가능한 템플릿에 사용됨(속성의 상대 경로로 설정) `cq:deviceGroups`)에서 에뮬레이터로 사용할 수 있는 모바일 장치를 정의합니다. [레이아웃 모드](/help/sites-authoring/responsive-layout.md) 페이지 작성. 이 값은 다음 두 위치에 설정할 수 있습니다.

* 편집 가능한 템플릿 유형에서
* 편집 가능한 템플릿에서

편집 가능한 새 템플릿을 만들 때 템플릿 유형의 값이 개별 템플릿에 복사됩니다. 유형에 값을 설정하지 않으면 템플릿에 설정할 수 있습니다. 템플릿이 만들어지면 유형에서 템플릿으로 상속할 수 없습니다.

>[!CAUTION]
>
>값: `cq:deviceGroups` 은(는) 과 같은 상대 경로로 설정해야 합니다. `mobile/groups/responsive` 절대 경로로 사용되지 않는 예: `/etc/mobile/groups/responsive`.

>[!NOTE]
>
>포함 [정적 템플릿](/help/sites-developing/page-templates-static.md), 값 `cq:deviceGroups` 를 사이트의 루트에서 설정할 수 있습니다.
>
>편집 가능한 템플릿을 사용하면 이 값이 이제 템플릿 수준에서 저장되며 페이지 루트 수준에서 지원되지 않습니다.

### 템플릿 유형 만들기 {#creating-template-types}

다른 템플릿의 기반으로 사용할 수 있는 템플릿을 생성한 경우 이 템플릿을 템플릿 유형으로 복사할 수 있습니다.

1. 편집 가능한 템플릿과 마찬가지로 템플릿을 만듭니다. [여기에 문서화되어 있음](/help/sites-authoring/templates.md#creating-a-new-template-template-author)템플릿 유형의 기반으로 사용할 수 있습니다.
1. CRXDE Lite을 사용하여 `templates` 에 대한 노드 `template-types` 노드 아래의 [템플릿 폴더](/help/sites-developing/page-templates-editable.md#template-folders).
1. 에서 템플릿 삭제 `templates` 노드 아래의 [템플릿 폴더](/help/sites-developing/page-templates-editable.md#template-folders).
1. 아래에 있는 템플릿 사본에서 `template-types` 노드, 모두 삭제 `cq:template` 및 `cq:templateType` 모든 속성 `jcr:content` 노드.

GitHub에서 사용 가능한 편집 가능한 예제 템플릿을 기준으로 자체 템플릿 유형을 개발할 수도 있습니다.

GITHUB의 코드

이 페이지의 코드는 GitHub에서 확인할 수 있습니다

* [GitHub에서 aem-sites-example-custom-template-type 프로젝트 열기](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type)
* 다음으로 프로젝트 다운로드 [ZIP 파일](https://codeload.github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type/zip/refs/heads/master)

## 템플릿 정의 {#template-definitions}

편집 가능한 템플릿에 대한 정의가 저장됩니다 [사용자 정의 폴더](/help/sites-developing/page-templates-editable.md#template-folders) (권장) 또는 `global`. 예:

* `/conf/<my-folder>/settings/wcm/templates`
* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/templates`
* `/conf/global/settings/wcm/templates`

템플릿의 루트 노드가 유형입니다. `cq:Template` 의 뼈대 구조:

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

주요 요소는 다음과 같습니다.

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

   * **유형**: `String`

   * **값**: `draft`, `enabled`, 또는 `disabled`

### 구조 {#structure}

결과 페이지의 구조를 정의합니다.

* 초기 콘텐츠와 병합됩니다( `/initial`)을 클릭하여 페이지를 만듭니다.
* 구조에 대한 변경 사항은 템플릿으로 만든 모든 페이지에 반영됩니다.
* 다음 `root` ( `structure/jcr:content/root`) 노드는 결과 페이지에서 사용할 수 있는 구성 요소 목록을 정의합니다.

   * 템플릿 구조에 정의된 구성 요소는 결과 페이지에서 이동하거나 삭제할 수 없습니다.
   * 구성 요소 잠금이 해제된 후 `editable` 속성이 로 설정되어 있습니다. `true`.

   * 이미 콘텐츠가 포함된 구성 요소의 잠금이 해제된 후 이 콘텐츠가 로 이동됩니다. `initial` 분기입니다.

* 다음 `cq:responsive` 노드는 응답형 레이아웃에 대한 정의를 보관합니다.

### 초기 콘텐츠 {#initial-content}

새 페이지 생성 시 갖는 초기 콘텐츠를 정의합니다.

* 다음 포함: `jcr:content` 새 페이지에 복사되는 노드입니다.
* 구조와 병합( `/structure`)을 클릭하여 페이지를 만듭니다.
* 최초 콘텐츠가 작성 후 변경되는 경우 기존 페이지가 업데이트됩니다.
* 다음 `root` 노드에는 최종 페이지에서 사용할 수 있는 항목을 정의하는 구성 요소 목록이 있습니다.
* 콘텐츠가 구조 모드의 구성 요소에 추가되고 해당 구성 요소의 잠금이 나중에 해제된 경우(또는 반대로) 이 콘텐츠는 초기 콘텐츠로 사용됩니다.

### 레이아웃 {#layout}

날짜 [템플릿을 편집하여 레이아웃을 정의할 수 있습니다](/help/sites-authoring/templates.md), 이 연습에서는 [표준 반응형 레이아웃](/help/sites-authoring/responsive-layout.md) 또한 다음과 같을 수 있습니다. [구성됨](/help/sites-administering/configuring-responsive-layout.md).

### 컨텐츠 정책 {#content-policies}

콘텐츠(또는 디자인) 정책은 구성 요소의 가용성 또는 최소/최대 차원과 같은 구성 요소의 디자인 속성을 정의합니다. 이러한 정책은 템플릿(및 템플릿으로 만든 페이지)에 적용할 수 있습니다. 템플릿 편집기에서 컨텐츠 정책을 만들고 선택할 수 있습니다.

* 속성 `cq:policy`, `root` 노드
  `/conf/<your-folder>/settings/wcm/templates/<your-template>/policies/jcr:content/root`
페이지의 단락 시스템에 대한 콘텐츠 정책에 대한 상대 참조를 제공합니다.

* 속성 `cq:policy`, 구성 요소 명시적 노드 `root`개별 구성 요소에 대한 정책 링크를 제공합니다.

* 실제 정책 정의는 아래에 저장됩니다.
  `/conf/<your-folder>/settings/wcm/policies/wcm/foundation/components`

>[!NOTE]
>
>정책 정의의 경로는 구성 요소의 경로에 따라 다릅니다. 다음 `cq:policy` 구성 자체에 대한 상대 참조를 보유합니다.

>[!NOTE]
>
>편집 가능한 템플릿에서 만든 페이지는 페이지 편집기에서 디자인 모드를 제공하지 않습니다.
>
>다음 `policies` 편집 가능한 템플릿의 트리에는 아래 정적 템플릿의 디자인 모드 구성과 동일한 계층 구조가 있습니다.
>
>`/etc/designs/<my-site>/jcr:content/<component-name>`
>
>정적 템플릿의 디자인 모드 구성이 페이지 구성 요소별로 정의되었습니다.

### 페이지 정책 {#page-policies}

페이지 정책을 사용하면 다음을 정의할 수 있습니다. [콘텐츠 정책](#content-policies) 페이지(main parsys)의 경우 템플릿 또는 결과 페이지에서 참조할 수 있습니다.

### 템플릿 사용 및 사용 허용 {#enabling-and-allowing-a-template-for-use}

1. **템플릿 활성화**

   템플릿을 사용하려면 다음 방법 중 하나를 사용하여 템플릿을 활성화해야 합니다.

   * [템플릿 활성화](/help/sites-authoring/templates.md#enablingatemplateauthor) 다음에서 **템플릿** 콘솔.

   * 에서 상태 속성 설정 `jcr:content` 노드.

      * 예를 들어,
        `/conf/<your-folder>/settings/wcm/templates/<your-template>/jcr:content`

      * 속성을 정의합니다.

         * 이름: 상태
         * 유형: 문자열
         * 값: `enabled`

1. **허용된 템플릿**

   * [에서 허용된 템플릿 경로를 정의합니다. **페이지 속성**](/help/sites-authoring/templates.md#allowing-a-template-author) 하위 분기의 적절한 페이지 또는 루트 페이지
   * 속성을 설정합니다.
     `cq:allowedTemplates`
다음에서 `jcr:content` 필요한 분기의 노드입니다.

   예를 들어, 값이 다음과 같은 경우:

   `/conf/<your-folder>/settings/wcm/templates/.*`

## 결과 컨텐츠 페이지 {#resultant-content-pages}

편집 가능한 템플릿에서 만든 페이지:

* 에서 병합되는 하위 트리로 만들어집니다. `structure` 및 `initial` 템플릿에서

* 템플릿 및 템플릿 유형에 보관된 정보에 대한 참조가 있습니다. 다음을 사용하여 이 기능을 수행할 수 있습니다. `jcr:content` 속성이 있는 노드:

   * `cq:template`
실제 템플릿에 대한 동적 참조를 제공합니다. 템플릿의 변경 사항을 실제 페이지에 반영할 수 있습니다.

   * `cq:templateType`
템플릿 유형에 대한 참조를 제공합니다.

![chlimage_1-71](assets/chlimage_1-71.png)

위의 다이어그램은 템플릿, 콘텐츠 및 구성 요소가 상호 관련되는 방법을 보여 줍니다.

* 컨트롤러 - `/content/<my-site>/<my-page>`
템플릿을 참조하는 결과 페이지입니다. 콘텐츠는 전체 프로세스를 제어합니다. 정의에 따라 적절한 템플릿과 구성 요소에 액세스합니다.

* 구성 - `/conf/<my-folder>/settings/wcm/templates/<my-template>`
다음 [템플릿 및 관련 콘텐츠 정책](#template-definitions) 페이지 구성을 정의합니다.

* 모델 - OSGi 번들 [OSGI 번들](/help/sites-deploying/osgi-configuration-settings.md) 기능을 구현합니다.

* 보기 - `/apps/<my-site>/components`
작성자 및 게시 환경 모두에서 콘텐츠는 렌더링됩니다 [구성 요소](/help/sites-developing/components.md).

페이지를 렌더링할 때:

* **템플릿**:

   * 다음 `cq:template` 속성 `jcr:content` 해당 페이지에 해당하는 템플릿에 액세스하기 위해 노드가 참조됩니다.

* **구성 요소**:

   * 페이지 구성 요소는 `structure/jcr:content` 이 있는 템플릿의 트리 `jcr:content` 페이지 트리.

   * 작성자는 페이지 구성 요소를 통해 편집 가능한 것으로 플래그가 지정된 템플릿 구조의 노드(및 하위 항목 포함)만 편집할 수 있습니다.
   * 페이지에서 구성 요소를 렌더링할 때 해당 구성 요소의 상대 경로는 `jcr:content` 노드, 아래에 있는 동일한 경로 `policies/jcr:content` 그런 다음 템플릿의 노드를 검색합니다.

      * 다음 `cq:policy` 이 노드의 속성은 실제 콘텐츠 정책을 가리킵니다(즉, 구성 요소에 대한 디자인 구성을 보유함).

      * 이 기능을 사용하면 동일한 콘텐츠 정책 구성을 재사용하는 여러 템플릿을 사용할 수 있습니다.
