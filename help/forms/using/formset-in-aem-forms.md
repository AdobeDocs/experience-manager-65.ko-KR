---
title: AEM Forms에 설정된 양식
seo-title: Form set in AEM Forms
description: 이 문서에서는 양식 세트를 소개하고 HTML5 양식을 함께 결합하여 양식 세트를 만드는 방법을 설명합니다. 이 문서에서는 양식 세트에 xml 데이터를 미리 채우는 방법과 프로세스 관리에서 양식 세트를 사용하는 방법도 설명합니다.
seo-description: This article introduces form set and explains how to create form sets by stitching together HTML5 forms. This article also explains how you can prefill xml data to a form set and how you can use form sets in process management.
uuid: a1a2f267-26a9-4f45-bcfc-dbdedad95973
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 80e3eec4-95e0-4731-a0e5-a617e9bcb069
docset: aem65
feature: Mobile Forms
exl-id: 039afdf3-013b-41b2-8821-664d28617f61
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '2813'
ht-degree: 0%

---

# AEM Forms에 설정된 양식{#form-set-in-aem-forms}

## 개요 {#overview}

고객은 서비스 또는 혜택을 신청하기 위해 여러 양식을 제출해야 하는 경우가 많습니다. 여기에는 모든 관련 양식 검색, 별도로 작성, 제출 및 추적하는 작업이 포함됩니다. 또한 여러 양식에 공통 세부 정보를 여러 번 입력해야 합니다. 많은 수의 양식이 포함되면 전체 프로세스가 번거롭고 오류를 일으키기 쉬워집니다. AEM Forms의 양식 세트 기능을 사용하면 이러한 시나리오에서 사용자 경험을 단순화할 수 있습니다.

양식 세트는 함께 그룹화되어 최종 사용자에게 단일 양식 세트로 제공되는 HTML5 양식의 컬렉션입니다. 최종 사용자가 양식 세트를 채우기 시작하면 한 양식에서 다른 양식으로 원활하게 전환됩니다. 마지막에 모든 양식을 한 번의 클릭으로 제출할 수 있습니다.

AEM Forms은 양식 작성자에게 양식 세트를 만들고, 구성하고, 관리할 수 있는 직관적인 사용자 인터페이스를 제공합니다. 작성자는 최종 사용자가 따라야 할 특정 순서로 양식을 정렬할 수 있습니다. 또한 개별 양식에 조건 또는 자격 표현식을 적용하여 사용자 입력을 기반으로 가시성을 제어할 수 있습니다. 예를 들어, 결혼 상태가 기혼으로 지정된 경우에만 배우자 세부 정보 양식이 나타나도록 구성할 수 있습니다.

또한 서로 다른 양식의 공통 필드를 구성하여 공통 데이터 바인딩을 공유할 수 있습니다. 적절한 데이터 바인딩이 있는 경우 최종 사용자는 공통 정보를 한 번만 채워야 하며, 이 정보가 후속 양식에서 자동으로 채워집니다.

양식 세트는 AEM Forms 앱에서도 지원되므로 현장 인력이 양식 세트를 오프라인으로 전환하고, 고객을 방문하고, 데이터를 입력하고, 나중에 AEM Forms 서버와 동기화하여 양식 데이터를 비즈니스 프로세스에 제출할 수 있습니다.

## 양식 세트 만들기 및 관리 {#creating-and-managing-form-set}

디자이너를 사용하여 만든 여러 XDP 또는 양식 템플릿을 양식 세트에 연결할 수 있습니다. 그런 다음 양식 세트를 사용하여 초기 양식 및 프로필에서 사용자가 입력한 값을 기반으로 XDP를 선택적으로 렌더링할 수 있습니다.

사용 [AEM Forms 사용자 인터페이스](../../forms/using/introduction-managing-forms.md) 모든 양식, 양식 세트 및 관련 에셋을 관리하려면

### 양식 설정 만들기 {#create-a-form-set}

양식 세트를 만들려면 다음을 수행합니다.

1. Forms > Forms 및 문서 를 선택합니다.
1. 만들기 > 양식 세트를 선택합니다.

1. 속성 추가 페이지에서 다음 세부 사항을 추가하고 다음을 클릭합니다.

   * 제목: 문서의 제목을 지정합니다. 제목을 통해 AEM Forms 사용자 인터페이스에 설정된 양식을 식별할 수 있습니다.
   * 설명: 문서에 대한 자세한 정보를 지정합니다.
   * 태그: 양식 설정을 고유하게 식별하는 태그를 지정합니다. 태그는 양식 세트를 검색하는 데 도움이 됩니다. 태그를 만들려면 [태그] 상자에 새 태그 이름을 입력합니다.
   * 제출 URL: 양식 세트의 독립 실행형 렌디션(AEM Forms 앱 사용 사례가 아닌 경우)에 대해 제출된 데이터가 게시된 URL을 지정합니다. 데이터는 다음 요청 매개 변수를 사용하여 multipart/formdata로 이 끝점에 제출됩니다.
   * dataXML: 이 매개 변수에는 제출된 양식 세트 데이터의 XML 표현이 포함됩니다. 양식 세트의 모든 양식이 공통 스키마를 사용하는 경우 해당 스키마에 따라 XML이 생성됩니다. 그렇지 않은 경우 XML 루트 태그에는 양식 첨부 파일에 대한 데이터가 들어 있는 양식 세트의 각 채워진 양식에 대한 하위 태그가 들어 있습니다.
   * formsetPath: 제출된 CRXDE의 formset 경로
   * HTML 렌더링 프로필: 부동 필드, 첨부 파일 및 초안 지원(독립형 양식 세트 렌디션의 경우)과 같은 특정 옵션을 구성하여 양식 세트의 모양, 동작 및 상호 작용을 사용자 정의할 수 있습니다. 기존 프로파일을 사용자 정의하거나 확장하여 모든 HTML 양식 프로파일 설정을 변경할 수 있습니다.

   ![양식 설정: 속성 추가](assets/createformset1.png)

1. 양식 선택 화면에 사용 가능한 XDP 양식 또는 XDP 파일이 표시됩니다. 양식 설정에 포함할 양식을 검색하여 선택한 다음 양식 설정에 추가를 클릭합니다. 필요한 경우 추가할 양식을 다시 검색합니다. 양식 세트에 모든 양식을 추가한 후 다음을 누릅니다.

   >[!NOTE]
   >
   >XDP 양식의 필드 이름에 점 문자가 포함되어 있지 않은지 확인하십시오. 그렇지 않으면 점 문자가 있는 필드를 확인하려는 스크립트에서 확인할 수 없습니다.

1. 양식 구성 페이지에서 다음을 수행할 수 있습니다.

   * 양식 순서: 양식을 드래그 앤 드롭하여 순서를 변경합니다. 양식 순서는 AEM Forms 앱과 독립형 렌디션에서 최종 사용자에게 양식이 표시되는 순서를 정의합니다.
   * 양식 식별자: 자격 식에 사용할 양식의 고유 ID를 지정합니다.
   * 데이터 루트: 양식 세트의 각 양식에 대해 작성자는 제출된 XML에서 특정 양식의 데이터가 배치되는 XPATH를 구성할 수 있습니다. 기본적으로 값은 / 입니다. 양식 세트의 모든 양식이 스키마 바인딩되어 있고 동일한 XML 스키마를 공유하는 경우 이 값을 변경할 수 있습니다. 형식의 모든 필드에는 XDP에 지정된 적절한 데이터 바인딩이 있는 것이 좋습니다. 서로 다른 두 양식의 두 필드가 공통 데이터 바인딩을 공유하는 경우 두 번째 양식의 필드에 첫 번째 양식의 미리 채워진 값이 표시됩니다. 내부 내용이 동일한 두 하위 양식을 동일한 XML 노드에 바인딩하지 마십시오. 양식 집합의 XML 구조에 대한 자세한 내용은 [양식 설정에 대한 XML 미리 채우기](../../forms/using/formset-in-aem-forms.md#p-prefill-xml-for-form-set-p).
   * 자격 표현식: 부울 값을 평가하고 양식 세트의 양식에 데이터를 채울 수 있는지 여부를 나타내는 JavaScript 표현식을 지정합니다. false인 경우 사용자에게 메시지가 표시되지 않거나 채울 양식이 표시됩니다. 일반적으로 표현식은 이 양식 전에 캡처된 필드 값을 기반으로 합니다. 표현식에는 양식 세트 API fs.valueOf에 대한 호출이 포함되어 있어 양식 세트의 양식 필드에서 사용자가 입력한 값을 추출할 수 있습니다.

   *fs.valueOf(&lt;form identifier=&quot;&quot;>, &lt;fieldsom expression=&quot;&quot;>) > &lt;value>*

   예를 들어, 양식 세트에 비즈니스 비용과 출장 비용이라는 두 가지 양식이 있는 경우, 이러한 두 양식에 대한 자격 표현식 필드에 JavaScript 코드 조각을 추가하여 양식의 경비 유형에 대한 사용자 입력을 확인할 수 있습니다. 사용자가 비즈니스 경비를 선택하면 비즈니스 경비 양식이 최종 사용자에게 렌더링됩니다. 또는 사용자가 출장 경비를 선택하면 다른 양식이 최종 사용자에게 렌더링됩니다. 자세한 내용은 자격 표현식을 참조하십시오.

   또한 작성자는 각 행의 오른쪽 모서리에 있는 삭제 아이콘을 사용하여 양식 세트에서 양식을 제거하거나 &#39;를 사용하여 다른 양식 세트를 추가할 수도 있습니다.**+**&#x200B;도구 모음의 &#39; 아이콘 이 &#39;**+**&#39; 아이콘은 사용자를 &#39;양식 선택&#39;에 사용된 마법사의 이전 단계로 돌아갑니다. 기존 선택 사항이 유지되며 추가로 선택한 사항은 해당 페이지의 양식 세트에 추가 아이콘을 사용하여 양식 세트에 추가해야 합니다.

   ![양식 세트: 양식 구성](assets/createformset2.png)

   >[!NOTE]
   >
   >양식 설정에 사용되는 모든 양식은 AEM Forms 사용자 인터페이스에서 관리됩니다.

### 양식 세트 관리 {#managing-a-form-set}

양식 세트가 만들어지면 해당 양식 세트에 대해 다음 작업을 수행할 수 있습니다.

* 한 번 클릭: 양식 세트가 만들어지고 기본 자산 페이지에 나열되면 양식 세트를 한 번 클릭하여 볼 수 있습니다. 양식 세트가 열리고 해당 양식 세트의 모든 양식 템플릿(XDP)이 표시됩니다.
* 편집: 양식 세트를 선택한 후 편집 을 클릭하면 양식 세트를 만드는 단계에서 위에 표시된 양식 구성 화면이 열립니다. 여기에 설명된 모든 기능을 수행할 수 있습니다.
* 복사 + 붙여넣기: 한 위치에서 전체 양식 세트를 복사하여 동일한 위치 또는 다른 위치나 폴더에 붙여넣을 수 있습니다.
* 다운로드: 모든 종속성이 있는 양식 세트를 다운로드할 수 있습니다.
* 검토 시작/관리: 양식 세트가 생성되면 검토 시작을 눌러 검토를 설정할 수 있습니다. 양식 설정에 대한 검토가 시작되면 [검토 관리] 옵션이 사용자에게 표시됩니다. 검토 관리 화면에서 검토를 업데이트/종료할 수 있습니다. 추가한 리뷰에 대해 리뷰를 확인하고 필요한 경우 주석을 추가할 수 있습니다.
* 삭제: 전체 양식 세트를 삭제합니다. 삭제된 양식 세트의 양식은 저장소에 남아 있습니다.
* 게시/게시 취소: 포함된 모든 양식 및 이러한 양식의 관련 에셋과 함께 양식 세트를 게시/게시 취소합니다.
* 미리 보기: 미리 보기는 HTML으로 미리 보기(데이터 없음)와 샘플 데이터를 사용한 사용자 지정 미리 보기의 두 가지 옵션을 제공합니다.
* 속성 보기/편집: 선택한 양식 세트의 메타데이터 속성을 보거나 편집할 수 있습니다.

![createformset3](assets/createformset3.png)

### 양식 설정 편집 {#edit-a-form-set}

양식 설정을 편집하려면 다음을 수행합니다.

1. Forms > Forms 및 문서 를 선택합니다.
1. 편집할 양식 세트를 찾습니다. 마우스를 위에 놓고 편집( ![에디티콘](assets/editicon.png)).
1. 양식 구성 페이지에서 다음을 편집할 수 있습니다.

   * 양식 순서
   * 양식 식별자
   * 데이터 루트
   * 자격 표현식

   관련 삭제 아이콘을 클릭하여 양식 설정에서 양식을 삭제할 수도 있습니다.

## 프로세스 관리의 양식 설정 {#form-set-in-process-management}

AEM Forms Management 사용자 인터페이스를 사용하여 양식 세트를 생성한 후에는 시작 지점에 있는 양식 세트를 사용하거나 워크벤치를 사용하여 태스크 지정 활동을 사용할 수 있습니다.

### 작업 또는 시작 지점에서 양식 설정 사용 {#using-form-set-in-task-or-start-point}

1. 프로세스를 디자인할 때 작업/시작 지점 지정의 프레젠테이션 및 데이터 섹션에서 을(를) 선택합니다. **crx 자산 사용**. CRX 자산 브라우저가 나타납니다.

   ![프로세스 디자인: CRX 자산 사용](assets/formsetinprocessmgmt1.png)

1. CRX(AEM repository)에서 양식 세트를 필터링하려면 양식 세트를 선택합니다.

   ![프로세스 디자인: 양식 에셋 선택 대화 상자](assets/formsetinprocessmgmt2.png)

1. 양식 세트를 선택하고 [확인]을 클릭합니다.

## 자격 표현식 {#eligibility-expressions}

양식 세트의 자격 표현식은 사용자에게 표시되는 양식을 정의하고 동적으로 제어하는 데 사용됩니다. 예를 들어, 사용자가 특정 연령 그룹에 속하는 경우에만 특정 양식을 표시할 수 있습니다. Forms Manager를 사용하여 자격 표현식을 지정하고 편집합니다.

자격 표현식은 부울 값을 반환하는 유효한 JavaScript 문일 수 있습니다. JavaScript 코드 조각의 마지막 문은 JavaScript 코드 조각의 나머지 부분(이전 줄)에 있는 처리를 기반으로 양식의 자격을 결정하는 부울 값으로 처리됩니다. 표현식의 값이 true인 경우 양식을 사용자에게 표시할 수 있습니다. 이러한 양식을 적격 양식이라고 합니다.

>[!NOTE]
>
>양식 세트의 첫 번째 양식에 대한 자격 표현식이 실행되지 않습니다. 첫 번째 양식은 자격 표현식과 관계없이 항상 표시됩니다.

표준 JavaScript 함수 외에도 양식 세트는 양식 세트의 양식 필드 값에 대한 액세스를 제공하는 fs.valueOf API를 노출합니다. 이 API를 사용하여 양식 세트의 양식 필드 값에 액세스합니다. API 구문은 fs.valueOf (formUid, fieldSOM)이며, 여기서 다음을 수행합니다.

* formUid (string): 양식 세트에 있는 양식의 고유 ID입니다. Forms Manager 사용자 인터페이스에서 양식 세트를 만드는 동안 지정할 수 있습니다. 기본적으로 양식 이름입니다.
* fieldSOM(문자열): formUid로 지정된 형식의 필드에 대한 SOM 표현식입니다. SOM 표현식 또는 Scripting Object Model 표현식은 특정 DOM(문서 객체 모델) 내의 값, 속성 및 메서드를 참조하는 데 사용됩니다. 필드를 선택한 동안 스크립트 탭 아래의 양식 디자이너에서 볼 수 있습니다.

>[!NOTE]
>
>formUid 및 fieldSOM 매개 변수는 모두 문자열 리터럴이어야 합니다.

### 예 {#examples}

API의 유효한 사용:

`fs.valueOf("form1", "xfa.form.form1.subform1.field1")`

잘못된 API 사용:

```javascript
var formUid = "form1";
 var fieldSOM = "xfa.form.form1.subform1.field1"; fs.valueOf(formUid, fieldSOM);
```

## 양식 설정에 대한 XML 미리 채우기 {#prefill-xml-for-form-set}

양식 집합은 공통 또는 다른 스키마를 갖는 여러 HTML5 양식의 컬렉션입니다. 양식 집합은 XML 파일을 사용하여 양식 필드를 미리 채울 수 있도록 지원합니다. XML 파일을 양식 집합과 연결할 수 있으므로 양식 집합에서 양식을 열 때 양식의 일부 필드가 미리 생성되도록 할 수 있습니다.

미리 채우기 XML 파일은 양식 세트의 URL에 대한 dataRef 매개 변수를 사용하여 지정됩니다. dataRef 매개 변수는 양식 집합과 병합되는 데이터 XML 파일의 절대 경로를 지정합니다.

예를 들어, 다음 구조를 갖는 양식 세트에 세 개의 양식(form1, form2 및 form3)이 있습니다.

form1

필드 form1field

form2

필드 form2field

form3

필드 form3field

각 양식에는 이름이 &quot;field&quot;인 공통 이름이 지정된 필드와 이름이 &quot;formfield&quot;인 고유한 필드가 있습니다.

다음 구조로 XML을 사용하여 이 양식 세트를 미리 채울 수 있습니다.

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<formSetRootTag>
 <field>common field value</field>
 <form1field>value1</form1field>
 <form2field>value2</form2field>
 <form3field>value3</form3field>
</formSetRootTag>
```

>[!NOTE]
>
>XML 루트 태그는 이름을 가질 수 있지만 필드에 해당하는 요소 태그는 필드와 같은 이름을 가져야 합니다. XML 계층은 양식 계층 구조를 모방해야 합니다. 즉, 하위 양식을 래핑하려면 XML에 해당 태그가 있어야 합니다.

위의 XML 스니펫은 양식 세트에 대한 미리 채우기 XML이 개별 양식의 미리 채우기 XML 스니펫의 통합임을 보여 줍니다. 다른 양식의 특정 필드에 서로 유사한 데이터 계층 구조/스키마가 있는 경우 필드에 동일한 값이 미리 채워집니다. 이 예제에서 세 가지 폼은 모두 공통 필드인 &quot;field&quot;에 대해 동일한 값으로 미리 채워집니다. 이는 데이터를 한 양식에서 다음 양식으로 전달하는 간단한 방법입니다. 필드를 동일한 스키마 또는 데이터 참조에 바인딩하여 이를 수행할 수도 있습니다. 양식의 스키마를 기준으로 양식 세트 데이터를 분리하려면 이 작업은 양식 설정 생성 중에 양식의 &quot;data root&quot; 속성을 지정하여 수행할 수 있습니다(기본값은 양식 설정 루트 태그에 매핑되는 &quot;/&quot;입니다).

앞의 예에서 세 가지 양식에 대해 각각 &quot;/form1&quot;, &quot;/form2&quot; 및 &quot;/form3&quot;인 데이터 루트를 지정하는 경우 다음 구조의 미리 채우기 XML을 사용해야 합니다.

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<formSetRootTag>
 <form1>
  <field>field value1</field>
  <form1field>value1</form1field>
 </form1>
 <form2>
  <field>field value2</field>
  <form2field>value2</form2field>
 </form2>
 <form3>
  <field>field value3</field>
  <form3field>value3</form3field>
 </form3>
</formSetRootTag>
```

양식 세트에서 XML은 다음 구문을 사용하여 XML 스키마를 정의했습니다.

```xml
<formset>
 <fs_data>
  <xdp:xdp xmlns:xdp="https://ns.adobe.com/xdp/">
  <xfa:datasets xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
   <xfa:data>
   <rootElement>
    ... data ....
   </rootElement>
   </xfa:data>
  </xfa:datasets>
  </xdp:xdp>
 </fs_data>
 <fs_draft>
  ... private data...
 </fs_draft>
</formset>
```

>[!NOTE]
>
>데이터 루트가 겹치는 양식이 두 개 있거나 한 양식의 요소 계층이 다른 양식의 데이터 루트 계층과 겹치는 경우 미리 채우기 xml에서 겹치는 요소의 값이 병합됩니다. 제출 XML의 구조는 미리 채우기 XML과 유사하지만, 제출 XML의 끝에 래퍼 태그와 일부 양식 세트 컨텍스트 데이터 태그가 더 많이 추가됩니다.

### XML 요소 설명 미리 채우기 {#prefill-xml-elements-description}

미리 채우기 XML 파일을 만들기 위한 구문 규칙:

* 상위 요소: 상위가 될 수 있는 요소. 여기서 null은 요소가 XML의 루트에 있을 수 있음을 나타냅니다.
* 카디널리티: 요소가 상위 요소 내에서 사용될 수 있는 횟수를 나타냅니다.
* submitXML: 제출 XML에 요소가 항상 있는지(P) 또는 선택 사항인지(O)를 나타냅니다.
* prefillXML: 미리 채우기 XML에 요소가 필요한지(R) 또는 선택(O) 여부를 나타냅니다.
* 1차 하위 구성요소: 1차 하위 구성요소가 될 수 있는 요소를 나타냅니다.

### 양식 세트 {#formset}

`parent elements:`

`null`

`cardinality: [0,1]`

`submitXML: P`

`prefillXML: O`

`children: fs_data`

양식 집합 XML의 루트 요소입니다. 이 단어를 양식 설정에서 양식의 rootSubform 이름으로 사용하지 않는 것이 좋습니다.

### FS_DATA {#fs-data}

`parent elements:`

`formset`

카디널리티: [1]

submitXML: P

prefillXML: O

`children: xdp:xdp/rootElement`

하위 트리는 양식 세트의 양식 데이터를 나타냅니다. 양식 세트 요소가 없는 경우에만 미리 채우기 XML에서 요소가 선택 사항입니다

### XDP:XDP {#xdp-xdp}

`parent elements: fs_data/null`

`cardinality: [0,1]`

`submitXML: O`

`prefillXML: O`

`children: xfa:datasets`

이 태그는 HTML5 양식 XML의 시작을 나타냅니다. 미리 채우기 XML에 있거나 미리 채우기 XML이 없는 경우 제출 XML에 추가됩니다. 이 태그는 미리 채우기 XML에서 제거할 수 있습니다.

### XFA:데이터 세트 {#xfa-datasets}

`parent elements: xdp:xdp`

`cardinality: [1]`

`submitXML: O`

`prefillXML: O`

`children: xfa:data`

### XFA:DATA {#xfa-data}

`parent elements: xfa:datasets`

`cardinality: [1]`

`submitXML: O`

`prefillXML: O`

`children: rootElement`

### 룸서비스 {#rootelement}

`parent elements: xfa:datasets/fs_data/null`

`cardinality: [0,1]`

`submitXML: P`

`prefillXML: O`

`children: controlled by the Forms in Form set`

rootElement 이름은 자리 표시자일 뿐입니다. 실제 이름은 양식 설정에 사용된 양식에서 선택됩니다. rootElement로 시작하는 하위 트리에는 양식 세트의 Forms 내에 있는 필드와 하위 양식의 데이터가 포함됩니다. rootElement와 그 자식 요소의 구조를 결정하는 요소는 여러 가지가 있습니다.

미리 채우기 XML에서 이 태그는 선택 사항이지만 누락된 경우 전체 XML이 무시됩니다.

루트 요소 태그의 이름

미리 채우기 XML에 루트 요소가 있는 경우 해당 요소의 이름도 제출 XML에서 가져옵니다. 미리 채우기 xml이 없는 경우 rootElement의 이름은 dataRoot 속성이 &quot;/&quot;로 설정된 양식 설정에서 첫 번째 양식의 루트 하위 양식 이름입니다. 이러한 양식이 없으면 rootElement 이름은 입니다. **fs_dummy_root**: 예약된 키워드입니다.

## AEM Forms 앱에 설정된 양식 {#formset-in-workspace-app}

AEM Forms 앱을 사용하면 현장 작업자가 모바일 장치를 AEM Forms 서버와 동기화하여 작업을 수행할 수 있습니다. 응용 프로그램은 데이터를 장치에 로컬로 저장하여 장치가 오프라인일 때도 작동합니다. 현장 작업자는 사진과 같은 주석 기능을 사용하여 비즈니스 프로세스에 통합할 수 있는 정확한 정보를 제공할 수 있습니다.

<!-- Update link as it is a 404 - For more information on AEM Forms app, see [AEM Forms app overview](/help/forms/using/mobile-workspace-overview.md).-->

## 알려진 제한 사항 - 양식 설정에서 패턴이 완전히 지원되지 않음 {#known-limitations-patterns-not-fully-supported-in-form-set}

다음 데이터 패턴은 양식 세트에서 완전히 지원되지 않습니다.

<table>
 <tbody>
  <tr>
   <td><strong>양식 설정에서 패턴이 완전히 지원되지 않음</strong></td>
   <td><strong>예</strong></td>
  </tr>
  <tr>
   <td>입력 크기와 패턴 크기 불일치</td>
   <td><p>패턴= num{z,zzz}인 경우</p> <p>및 입력=</p> <p>12,345 또는</p> <p>1,23</p> </td>
  </tr>
  <tr>
   <td>대괄호 "(" ")"가 있는 그림 절 패턴</td>
   <td>num{(zz,zzz)}</td>
  </tr>
  <tr>
   <td>여러 데이터 패턴</td>
   <td>num{zz,zzz} | num{z,zzz,zzz}</td>
  </tr>
  <tr>
   <td>속기 패턴 </td>
   <td><p>num.integer{},</p> <p>num.decimal{},</p> <p>num.%{}, 또는</p> <p>num.currency{}</p> </td>
  </tr>
 </tbody>
</table>
