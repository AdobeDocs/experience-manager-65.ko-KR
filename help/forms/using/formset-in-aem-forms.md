---
title: AEM Forms 양식 세트
seo-title: AEM Forms 양식 세트
description: 이 문서에서는 양식 세트를 소개하고 HTML5 양식을 결합하여 양식 세트를 만드는 방법을 설명합니다. 이 문서에서는 양식 세트에 xml 데이터를 미리 채울 수 있는 방법과 양식 세트를 프로세스 관리에서 사용하는 방법에 대해 설명합니다.
seo-description: 이 문서에서는 양식 세트를 소개하고 HTML5 양식을 결합하여 양식 세트를 만드는 방법을 설명합니다. 이 문서에서는 양식 세트에 xml 데이터를 미리 채울 수 있는 방법과 양식 세트를 프로세스 관리에서 사용하는 방법에 대해 설명합니다.
uuid: a1a2f267-26a9-4f45-bcfc-dbdedad95973
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 80e3eec4-95e0-4731-a0e5-a617e9bcb069
docset: aem65
translation-type: tm+mt
source-git-commit: 998a127ce00c6cbb3db3a81d8a89d97ab9ef7469
workflow-type: tm+mt
source-wordcount: '2860'
ht-degree: 0%

---


# AEM Forms{#form-set-in-aem-forms}에 설정된 양식

## 개요 {#overview}

서비스 또는 혜택에 신청하려면 여러 양식을 제출해야 하는 경우가 많습니다. 관련 양식을 모두 찾는 작업이 수반됩니다.작성, 제출 및 개별적으로 추적할 수 있습니다. 또한 양식에서 여러 번 공통적인 세부 사항을 작성해야 합니다. 양식 수가 많을 경우 전체 프로세스가 번거롭고 오류가 발생하기 쉽습니다. AEM Forms의 양식 세트 기능을 사용하면 이러한 시나리오의 사용자 경험을 간소화할 수 있습니다.

양식 세트는 함께 그룹화되고 최종 사용자에게 하나의 양식 세트로 제공되는 HTML5 양식의 컬렉션입니다. 최종 사용자가 양식 세트를 채우기 시작하면 양식 간에 원활하게 전환됩니다. 한 번의 클릭으로 모든 양식을 제출할 수 있습니다.

AEM Forms은 양식 작성자에게 양식 세트를 생성, 구성 및 관리할 수 있는 직관적인 유저 인터페이스를 제공합니다. 작성자는 최종 사용자가 팔로우할 특정 순서로 양식을 주문할 수 있습니다. 또한 개별 양식에 조건 또는 자격 조건 표현식을 적용하여 사용자 입력에 따라 양식의 가시성을 제어할 수 있습니다. 예를 들어 혼인 상태가 기혼(Bodary)으로 지정된 경우에만 나타나도록 배우자 세부 정보 양식을 구성할 수 있습니다.

또한 다른 양식의 공통 필드를 구성하여 공통 데이터 바인딩을 공유할 수 있습니다. 적절한 데이터 바인딩이 있는 경우 최종 사용자는 이후 양식에 자동 채워진 일반적인 정보를 한 번만 입력해야 합니다.

또한 AEM Forms 앱에서도 양식 세트가 지원되므로 현장 직원이 양식을 오프라인으로 설정하고 고객을 방문하고 데이터를 입력하며 나중에 AEM Forms 서버와 동기화하여 양식 데이터를 비즈니스 프로세스에 제출할 수 있습니다.

## 양식 세트 {#creating-and-managing-form-set} 만들기 및 관리

디자이너를 사용하여 만든 여러 XDP 또는 양식 템플릿을 양식 세트에 연결할 수 있습니다. 그런 다음 사용자가 초기 양식과 프로필에 입력한 값을 기반으로 XDP를 선별적으로 렌더링할 수 있습니다.

[AEM Forms 사용자 인터페이스](../../forms/using/introduction-managing-forms.md)를 사용하여 모든 양식, 양식 세트 및 관련 자산을 관리합니다.

### 양식 세트 {#create-a-form-set} 만들기

양식 세트를 만들려면 다음을 수행하십시오.

1. Forms > Forms 및 문서를 선택합니다.
1. 만들기 > 양식 세트를 선택합니다.

1. 속성 추가 페이지에서 다음 세부 사항을 추가하고 다음을 클릭합니다.

   * 제목:문서의 제목을 지정합니다. 제목은 AEM Forms 사용자 인터페이스에 설정된 양식을 식별하는 데 도움이 됩니다.
   * 설명:문서에 대한 자세한 정보를 지정합니다.
   * 태그:양식 세트를 고유하게 식별하는 태그를 지정합니다. 태그는 양식 세트를 검색하는 데 도움이 됩니다. 태그를 만들려면 태그 상자에 새 태그 이름을 입력합니다.
   * 제출 URL:양식 세트의 독립 실행형 변환(AEM Forms 이외 앱 사용 사례)에 대해 제출된 데이터가 게시되는 URL을 지정합니다. 데이터는 다음 요청 매개 변수를 사용하여 이 끝점에 다중 부분/형식 데이터로 제출됩니다.
   * dataXML:이 매개 변수에는 제출된 양식 세트 데이터의 XML 표현이 포함됩니다. 양식 세트의 모든 양식에 공통 스키마를 사용하는 경우 XML이 해당 스키마에 따라 생성됩니다. 그렇지 않으면 XML 루트 태그에는 양식 첨부 파일의 데이터가 포함된 양식 세트의 채워진 각 양식에 대한 하위 태그가 포함됩니다.
   * formsetPath:CRXDE에서 제출된 형식 집합의 경로입니다.
   * HTML 렌더링 프로필:부동 필드, 첨부 파일 및 초안 지원(독립 실행형 양식 세트 변환의 경우)과 같은 특정 옵션을 구성하여 양식 세트의 모양, 동작 및 상호 작용을 사용자 정의할 수 있습니다. HTML 양식 프로필 설정을 변경하기 위해 기존 프로필을 사용자 지정하거나 확장할 수 있습니다.

   ![양식 세트:속성 추가](assets/createformset1.png)

1. 양식 선택 화면에는 사용 가능한 XDP 양식 또는 XDP 파일이 표시됩니다. 양식 세트에 포함할 양식을 검색하고 선택한 다음 양식에 추가를 클릭합니다. 필요한 경우 추가할 양식을 다시 검색합니다. 모든 양식을 양식 세트에 추가한 후 다음을 클릭합니다.

   >[!NOTE]
   >
   >XDP 양식의 필드 이름에 점 문자가 포함되어 있지 않아야 합니다. 그렇지 않으면 점 문자가 있는 필드를 해결하려고 하는 모든 스크립트를 해결할 수 없습니다.

1. 양식 구성 페이지에서 다음을 수행할 수 있습니다.

   * 양식 순서:양식을 드래그하여 놓는 방식으로 순서를 변경할 수 있습니다. 양식 순서는 AEM Forms 앱 및 독립 실행형 변환에서 최종 사용자에게 양식이 표시되는 순서를 정의합니다.
   * 양식 식별자:자격 표현식에 사용할 양식의 고유 ID를 지정합니다.
   * 데이터 루트:작성자는 양식 세트의 각 양식에 대해 해당 특정 양식의 데이터가 제출된 XML에 배치된 XPATH를 구성할 수 있습니다. 기본값은 / 입니다. 양식 세트의 모든 양식이 스키마 바인딩되어 있고 동일한 XML 스키마를 공유하는 경우 이 값을 변경할 수 있습니다. 양식의 모든 필드에 XDP에 지정된 적절한 데이터 바인딩이 있는 것이 좋습니다. 두 개의 다른 양식의 두 필드가 공통 데이터 바인딩을 공유하는 경우 두 번째 양식의 필드에 첫 번째 양식의 프리플라이트 값이 표시됩니다. 동일한 내부 컨텐츠로 두 개의 하위 양식을 동일한 XML 노드에 바인딩하지 마십시오. 양식 세트의 XML 구조에 대한 자세한 내용은 [양식 세트에 대한 XML 미리 채우기](../../forms/using/formset-in-aem-forms.md#p-prefill-xml-for-form-set-p)를 참조하십시오.
   * 자격 조건 표현식:부울 값을 평가하고 양식 세트의 양식이 채울 수 있는지 여부를 나타내는 JavaScript 표현식을 지정합니다. false이면 채울 양식이 요청되거나 표시되지 않습니다. 일반적으로 표현식은 이 양식 이전에 캡처된 필드의 값을 기반으로 합니다. 또한 표현식에는 양식 세트의 필드 내에서 사용자가 입력한 값을 추출하기 위해 양식 세트 API fs.valueOf에 대한 호출도 포함되어 있습니다.

   *fs.valueOf(&lt;form Identifier=&quot;&quot;>,  &lt;fieldsom expression=&quot;&quot;>) >  &lt;value>*

   예를 들어, 양식 세트에 두 개의 양식이 있는 경우:비즈니스 비용 및 출장 비용, 이러한 양식에서 사용자 입력을 양식의 비용 유형으로 확인하도록 자격 조건 표현식 필드에 JavaScript 조각을 추가할 수 있습니다. 사용자가 사업 비용을 선택하면 비즈니스 비용 양식이 최종 사용자에게 렌더링됩니다. 또는 사용자가 출장 비용을 선택하면 다른 양식이 최종 사용자에게 렌더링됩니다. 자세한 내용은 자격 조건 표현식을 참조하십시오.

   또한 작성자는 각 행의 오른쪽 모서리에 있는 삭제 아이콘을 사용하여 양식 세트에서 양식을 제거하거나 도구 모음에서 &#39;**+**&#39; 아이콘을 사용하여 다른 양식 세트를 추가할 수도 있습니다. 이 &#39;**+**&#39; 아이콘은 사용자가 &#39;양식 선택&#39;에 사용된 마법사의 이전 단계로 돌아갑니다. 기존 선택 사항은 그대로 유지되며 선택한 추가 선택 사항은 해당 페이지의 양식 세트에 추가 아이콘을 사용하여 양식 세트에 추가해야 합니다.

   ![양식 세트:양식 구성](assets/createformset2.png)

   >[!NOTE]
   >
   >양식 세트에 사용되는 모든 양식은 AEM Forms 사용자 인터페이스에서 관리합니다.

### 양식 세트 관리 {#managing-a-form-set}

양식 세트가 만들어지면 해당 양식 세트에 대해 다음 작업을 수행할 수 있습니다.

* 한 번 클릭:양식 세트가 만들어지고 기본 자산 페이지에 나열되면 양식 세트를 한 번 클릭하여 볼 수 있습니다. 양식 세트가 열리고 해당 양식 세트에 모든 양식 템플릿(XDP)이 표시됩니다.
* 편집:양식 세트를 선택한 후 편집을 클릭하면 위에 표시된 양식 구성 화면이 열리고 양식 세트가 생성됩니다. 여기에서 설명하는 모든 기능을 수행할 수 있습니다.
* 복사 + 붙여넣기:이렇게 하면 한 위치에서 전체 양식 세트를 복사하여 같은 위치에 붙여넣거나 다른 위치 또는 폴더에 붙여넣을 수 있습니다.
* 다운로드:모든 종속성이 있는 양식 세트를 다운로드할 수 있습니다.
* 검토 시작/관리:양식 세트가 만들어지면 검토 시작을 클릭하여 검토를 설정할 수 있습니다. 양식 세트에 대한 검토가 시작되면 사용자에게 검토 관리 옵션이 표시됩니다. 검토 관리 화면에서 검토를 업데이트/종료할 수 있습니다. 추가한 검토의 경우 필요한 경우 검토를 확인하고 주석을 추가할 수 있습니다.
* 삭제:전체 양식 세트를 삭제합니다. 삭제된 양식 세트의 양식은 저장소에 남아 있습니다.
* 게시/게시 취소:이 게시에서는 양식 세트가 포함된 모든 양식과 이러한 양식의 관련 에셋을 게시/게시 취소합니다.
* 미리 보기:미리 보기에서는 다음 두 가지 옵션을 제공합니다.데이터 없이 HTML로 미리 보고 샘플 데이터로 사용자 요구에 맞게 미리 볼 수 있습니다.
* 속성 보기/편집:선택한 양식 세트의 메타데이터 속성을 보거나 편집할 수 있습니다.

![createformset3](assets/createformset3.png)

### 양식 세트 {#edit-a-form-set} 편집

양식 세트를 편집하려면 다음을 수행합니다.

1. Forms > Forms 및 문서를 선택합니다.
1. 편집할 양식 세트를 찾습니다. 마우스를 위에 두고 편집( ![에디티콘](assets/editicon.png))을 선택합니다.
1. 양식 구성 페이지에서 다음을 편집할 수 있습니다.

   * 양식 순서
   * 양식 식별자
   * 데이터 루트
   * 자격 조건 표현식

   관련 삭제 아이콘을 클릭하여 양식 세트에서 양식을 삭제할 수도 있습니다.

## 프로세스 관리에 설정된 양식 {#form-set-in-process-management}

AEM Forms 관리 사용자 인터페이스를 사용하여 양식 세트를 만들었으면 시작 지점 또는 워크벤치를 사용하여 작업 지정 활동의 양식 세트를 사용할 수 있습니다.

### 작업 또는 시작 지점 {#using-form-set-in-task-or-start-point}에 설정된 양식 사용

1. 프로세스를 디자인할 때 [작업 지정/시작 지점]의 [프레젠테이션 및 데이터] 섹션에서 **CRX 자산**&#x200B;을 선택합니다. CRX 자산 브라우저가 나타납니다.

   ![프로세스 디자인:CRX 자산 사용](assets/formsetinprocessmgmt1.png)

1. AEM 리포지토리(CRX)에서 양식 세트를 필터링하려면 양식 세트를 선택합니다.

   ![프로세스 디자인:양식 자산 선택 대화 상자](assets/formsetinprocessmgmt2.png)

1. 양식 세트를 선택하고 확인을 클릭합니다.

## 자격 조건 표현식 {#eligibility-expressions}

양식 세트의 자격 식은 사용자에게 표시되는 양식을 정의하고 동적으로 제어하는 데 사용됩니다. 예를 들어 사용자가 특정 연령 그룹에 속한 경우에만 특정 양식을 표시합니다. 양식 관리자를 사용하여 자격 조건 표현식을 지정하고 편집합니다.

자격 조건식은 부울 값을 반환하는 모든 유효한 JavaScript 문이 될 수 있습니다. JavaScript 코드 조각의 마지막 문은 JavaScript 코드 조각의 나머지(이전 줄)에서의 처리를 기반으로 양식의 자격 조건을 결정하는 부울 값으로 취급됩니다. 표현식 값이 true이면 사용자에게 양식을 표시할 수 있습니다. 이러한 양식을 자격 조건을 갖춘 양식으로 알려져 있습니다.

>[!NOTE]
>
>양식 세트의 첫 번째 양식에 대한 자격 식이 실행되지 않습니다. 첫 번째 양식은 자격 표현식에 관계없이 항상 표시됩니다.

표준 JavaScript 함수 외에도 양식 세트는 양식 세트의 양식 필드 값에 대한 액세스를 제공하는 fs.valueOf API도 노출합니다. 이 API를 사용하여 양식 세트의 양식 필드 값에 액세스합니다. API 구문은 fs.valueOf(formUid, fieldSOM)입니다. 여기서

* formUid(문자열):양식 세트에 있는 양식의 고유 ID입니다. 양식 관리자 사용자 인터페이스에서 양식 세트를 만드는 동안 이를 지정할 수 있습니다. 기본적으로 양식 이름입니다.
* fieldSOM(문자열):formUid로 지정된 양식의 필드 SOM 식입니다. SOM 표현식 또는 스크립팅 개체 모델 표현식은 특정 문서 개체 모델(DOM) 내의 값, 속성 및 메서드를 참조하는 데 사용됩니다. 필드를 선택한 동안 양식 디자이너의 스크립트 탭 아래에서 이 필드를 볼 수 있습니다.

>[!NOTE]
>
>formUid 및 fieldSOM 매개 변수는 모두 문자열 리터럴이어야 합니다.

### 예 {#examples}

유효한 API 사용:

`fs.valueOf("form1", "xfa.form.form1.subform1.field1")`

잘못된 API 사용:

```javascript
var formUid = "form1";
 var fieldSOM = “xfa.form.form1.subform1.field1"; fs.valueOf(formUid, fieldSOM);
```

## 양식 세트 {#prefill-xml-for-form-set}에 대한 XML 자동 채우기

양식 세트는 공통되거나 다른 스키마를 갖는 여러 HTML5 양식의 집합입니다. 양식 세트는 XML 파일을 사용하여 양식 필드의 미리 채우기 기능을 지원합니다. XML 파일을 양식 세트와 연결할 수 있으므로 양식 세트에서 양식을 열면 양식의 일부 필드가 미리 폴링됩니다.

양식 세트의 URL의 dataRef 매개 변수를 사용하여 XML 파일을 미리 채웁니다. dataRef 매개 변수는 양식 세트와 병합되는 데이터 XML 파일의 절대 경로를 지정합니다.

예를 들어 다음 구조를 갖는 양식 세트에 3개의 양식(form1, form2 및 form3)이 있습니다.

form1

필드
form1field

form2

필드
form2field

form3

필드
form3field

각 양식에는 &quot;field&quot;라는 이름의 공통 필드와 &quot;form&lt;i>field&quot;라는 고유한 이름의 필드가 있습니다.

다음 구조를 갖는 XML을 사용하여 이 양식 세트를 미리 채울 수 있습니다.

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
>XML 루트 태그에는 이름이 있을 수 있지만 필드에 해당하는 요소 태그의 이름은 필드와 같아야 합니다. XML의 계층은 양식의 계층 구조를 모방해야 합니다. 즉, XML에는 하위 양식 래핑에 해당하는 태그가 있어야 합니다.

위의 XML 코드 조각은 양식 세트에 대한 자동 완성 XML이 개별 양식의 자동 완성 XML 코드 단편을 결합하는 것을 보여줍니다. 다른 양식의 특정 필드에 서로 유사한 데이터 계층/스키마가 있는 경우 해당 필드는 동일한 값으로 자동 입력됩니다. 이 예에서는 세 개의 양식이 모두 공통 필드인 &quot;field&quot;에 대해 동일한 값으로 프리플라이트 됩니다. 이 방법은 데이터를 한 양식에서 다음 양식으로 전달하는 간단한 방법입니다. 또한 필드를 동일한 스키마 또는 데이터 참조에 바인딩하여 이를 수행할 수도 있습니다. 양식의 스키마에 따라 양식 세트 데이터를 분리하려는 경우 양식 세트를 만드는 동안 양식의 &quot;데이터 루트&quot; 속성을 지정하여 이를 수행할 수 있습니다(기본값은 양식 세트 루트 태그에 매핑되는 &quot;/&quot;입니다).

이전 예에서 데이터 루트를 지정하는 경우세 양식에 대해 각각 &quot;/form1&quot;, &quot;/form2&quot; 및 &quot;/form3&quot;을 사용하려면 다음 구조의 자동 완성 XML을 사용해야 합니다.

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
>겹치는 데이터 루트가 있는 두 개의 양식이 있거나 한 양식의 요소 계층 구조가 다른 양식의 데이터 루트 계층과 겹치는 경우, 자동 채우기 xml에서 겹쳐진 요소의 값이 병합됩니다. 제출 XML은 자동 완성 XML과 비슷한 구조이지만, 제출 XML에는 더 많은 래퍼 태그와 끝에 추가된 일부 양식 세트 컨텍스트 데이터 태그가 있습니다.

### XML 요소 설명 자동 완성 {#prefill-xml-elements-description}

자동 완성 XML 파일을 만들기 위한 구문 규칙:

* 상위 요소:요소의 부모가 될 수 있고 여기서 null은 요소가 XML의 루트에 있을 수 있음을 나타냅니다.
* 카디널리티:요소는 상위 요소 내에서 사용할 수 있는 횟수를 나타냅니다.
* submitXML:요소가 항상 제출 XML에 있는지(P) 또는 선택(O)인지 여부를 나타냅니다.
* prefillXML:요소가 자동 완성 XML에서 필수(R) 요소인지 선택(O)인지 여부를 나타냅니다.
* 하위:하위 요소를 나타냅니다.

### FORMSET {#formset}

`parent elements:`

`null`

`cardinality: [0,1]`

`submitXML: P`

`prefillXML: O`

`children: fs_data`

양식 세트 XML의 루트 요소입니다. 이 단어를 양식 세트에 있는 모든 폼의 rootSubform 이름으로 사용하지 않는 것이 좋습니다.

### FS_DATA {#fs-data}

`parent elements:`

`formset`

카디널리티:[1]

submitXML:P

prefillXML:O

`children: xdp:xdp/rootElement`

하위 트리는 양식 세트에 있는 양식의 데이터를 나타냅니다. 양식 세트 요소가 없는 경우에만 자동 완성 XML에서 요소가 선택 사항입니다

### XDP:XDP {#xdp-xdp}

`parent elements: fs_data/null`

`cardinality: [0,1]`

`submitXML: O`

`prefillXML: O`

`children: xfa:datasets`

이 태그는 HTML5 양식 XML의 시작을 나타냅니다. 이 XML은 자동 완성 XML에 있거나 자동 완성 XML이 없는 경우 전송 XML에 추가됩니다. 이 태그는 자동 완성 XML에서 제거할 수 있습니다.

### XFA:데이터 집합 {#xfa-datasets}

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

### ROOTELEMENT {#rootelement}

`parent elements: xfa:datasets/fs_data/null`

`cardinality: [0,1]`

`submitXML: P`

`prefillXML: O`

`children: controlled by the Forms in Form set`

이름 rootElement는 자리 표시자에 불과합니다. 양식 세트에 사용되는 양식에서 실제 이름이 선택됩니다. rootElement로 시작하는 하위 트리는 양식 세트의 Forms 내에 있는 필드 및 하위 양식의 데이터를 포함합니다. rootElement 및 그 하위의 구조를 결정하는 여러 요소가 있습니다.

XML 자동 완성 기능에서는 이 태그는 선택 사항이지만, 누락된 경우 전체 XML은 무시됩니다.

루트 요소 태그의 이름

자동 완성 XML에 루트 요소가 있는 경우 해당 요소의 이름도 전송 XML에서 가져옵니다. prefill xml이 없는 경우 rootElement의 이름은 dataRoot 속성이 &quot;/&quot;로 설정된 양식 세트에서 첫 번째 폼의 루트 하위 폼의 이름입니다. 이러한 양식이 없으면 rootElement 이름은 예약된 키워드인 **fs_dummy_root**&#x200B;입니다.

## AEM Forms 앱 {#formset-in-workspace-app}에 설정된 양식

현장 작업자는 AEM Forms 앱을 사용하여 모바일 장치를 AEM Forms 서버와 동기화하고 작업을 수행할 수 있습니다. 장치가 오프라인 상태일 때도 장치에서 데이터를 로컬로 저장하여 응용 프로그램이 작동합니다. 현장 작업자는 사진과 같은 주석 기능을 사용하여 정확한 정보를 제공하여 비즈니스 프로세스에 통합할 수 있습니다.

<!-- Update link as it is a 404 - For more information on AEM Forms app, see [AEM Forms app overview](/help/forms/using/mobile-workspace-overview.md).-->

## 알려진 제한 사항 - 양식 세트 {#known-limitations-patterns-not-fully-supported-in-form-set}에서 패턴이 완전히 지원되지 않음

다음 데이터 패턴은 양식 세트에서 완전히 지원되지 않습니다.

<table>
 <tbody>
  <tr>
   <td><strong>양식 세트에서 패턴이 완전히 지원되지 않음</strong></td>
   <td><strong>예</strong></td>
  </tr>
  <tr>
   <td>입력 크기 및 패턴 크기 불일치</td>
   <td><p>When pattern= num{z,zzz}</p> <p>입력=</p> <p>12,345 또는</p> <p>1,23</p> </td>
  </tr>
  <tr>
   <td>대괄호가 "(" ")"인 그림 절 패턴</td>
   <td>num{(zz,zzz)}</td>
  </tr>
  <tr>
   <td>다양한 데이터 패턴</td>
   <td>num{zz,zzz} | num{z,zzz,zzz}</td>
  </tr>
  <tr>
   <td>축약형 패턴 </td>
   <td><p>num.integer{},</p> <p>num.decimal{},</p> <p>num.%{} 또는</p> <p>num.currency{}</p> </td>
  </tr>
 </tbody>
</table>

