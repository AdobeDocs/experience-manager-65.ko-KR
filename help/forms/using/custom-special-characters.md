---
title: 서신 관리의 사용자 정의 특수 문자
description: 서신 관리에서 사용자 지정 특수 문자를 추가하는 방법을 알아봅니다.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
docset: aem65
feature: Correspondence Management
exl-id: 3e978c3e-12f2-4dc6-801d-8ab4c5df6700
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 1%

---

# 서신 관리의 사용자 정의 특수 문자{#custom-special-characters-in-correspondence-management}

## 개요 {#overview}

서신 관리에는 편지에 쉽게 삽입할 수 있는 210개의 특수 문자에 대한 기본 지원이 내장되어 있습니다.

예를 들어 다음 특수 문자를 삽입할 수 있습니다.

* 통화 기호(예: €,, £)
* ∑, √, ∂ 및 ^ 등의 수학 기호
* 및 &quot;(으)‟으로 구두점 기호

편지에 특수 문자를 삽입할 수 있습니다.

* 다음에서 [텍스트 편집기](/help/forms/using/document-fragments.md#createtext)
* 다음에서 [서신에 있는 편집 가능한 인라인 모듈](../../forms/using/create-correspondence.md#managecontent)

![specialcharactersinlinemodule](assets/specialcharactersinlinemodule.png)

관리자는 사용자 지정을 통해 추가/사용자 지정 특수 문자에 대한 지원을 추가할 수 있습니다. 이 문서에서는 추가 사용자 정의 특수 문자에 대한 지원을 추가하는 방법에 대한 지침을 제공합니다.

## 서신 관리에서 사용자 지정 특수 문자에 대한 지원 추가 또는 수정 {#creatingfolderstructure}

다음 단계를 사용하여 사용자 지정 특수 문자에 대한 지원을 추가하십시오.

1. 다음으로 이동 `https://'[server]:[port]'/[ContextPath]/crx/de` 관리자로 로그인합니다.
1. 앱 폴더에서 이라는 폴더를 만듭니다. **[!UICONTROL 특수 문자]** libs 아래의 textEditorConfig 폴더에 있는 specialcharacters 폴더와 유사한 경로/구조를 사용합니다.

   1. 마우스 오른쪽 단추 클릭 **특수 문자** 다음 경로에 있는 폴더를 선택하고 **오버레이 노드**:

      `/libs/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters`

   1. 오버레이 노드 대화 상자에 다음 값이 있는지 확인합니다.

      **경로:** /libs/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters

      **오버레이 위치:** /apps/

      **노드 유형 일치:** 선택됨

      >[!NOTE]
      >
      >/libs 분기를 변경하지 마십시오. 이 분기는 다음과 같은 경우 항상 변경되므로 변경한 내용이 손실될 수 있습니다.
      >
      >
      >
      >    * 인스턴스에서 업그레이드
      >    * 핫픽스 적용
      >    * 기능 팩 설치
      >
      >

   1. 클릭 **확인** 그런 다음 을 클릭합니다. **모두 저장**. 지정한 경로에 specialcharacters 폴더가 만들어집니다.

      오버레이를 만든 후 노드 구조 태그를 확인합니다. 오버레이를 사용하여 /apps에서 만든 각 노드에는 해당 노드에 대해 /libs에 정의된 것과 동일한 클래스와 속성이 있어야 합니다. 속성 또는 태그가 /apps 위치 아래의 노드 구조에 없는 경우 해당 태그를 /libs의 해당 노드와 동기화합니다.

1. 다음을 확인합니다. **[!UICONTROL textEditorConfig]** 노드에는 다음과 같은 속성과 값이 있습니다.

   | 이름 | 유형 | 값 |
   |---|---|---|
   | cmConfigurationType | 문자열 | cmTextEditorConfiguration |
   | cssPath | 문자열 | /libs/fd/cm/ma/gui/components/admin/createasset/textcontrol/clientlibs/textcontrol |

1. 마우스 오른쪽 단추 클릭 **[!UICONTROL 특수 문자]** 다음 경로에 있는 폴더를 선택하고 **만들기 > 하위 노드** 그런 다음 을 클릭합니다. **모두 저장**:

   /apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters/&lt;yourchildnode>

1. 텍스트 편집기\서신 UI 만들기 페이지를 새로 고칩니다. 추가한 노드는 UI의 특수 문자 목록에 있는 마지막 노드입니다.
1. **모두 저장**&#x200B;을 클릭합니다.
1. 필요에 따라 특수 문자를 변경합니다.

<table>
 <tbody>
  <tr>
   <td><strong>받는 사람...</strong></td>
   <td><strong>다음 단계를 완료합니다</strong></td>
  </tr>
  <tr>
   <td>사용자 지정 특수 문자 추가</td>
   <td>
    <ol>
     <li>필수 속성을 가진 "/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters" 아래에 하위 노드를 추가합니다.</li>
     <li>모두 저장 을 클릭합니다.</li>
     <li>변경 사항을 볼 수 있도록 텍스트 편집기를 새로 고칩니다.\서신 UI를 만듭니다.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>기존 특수 문자의 속성 업데이트</td>
   <td>
    <ol>
     <li>위에서 설명한 대로 업데이트할 노드를 오버레이하고 태그와 클래스를 확인합니다.</li>
     <li>caption, value, endValue 및 multipleCaption과 같은 모든 값을 변경합니다. </li>
     <li>모두 저장을 클릭합니다. </li>
     <li>변경 사항을 볼 수 있도록 텍스트 편집기를 새로 고칩니다.\서신 UI를 만듭니다.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>특수 문자 숨기기</td>
   <td>
    <ol>
     <li>"/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters" 아래에 숨길 노드를 오버레이합니다.</li>
     <li>숨길 노드(앱 아래)에 sling:hideResource(부울) 속성을 추가합니다. </li>
     <li>모두 저장을 클릭합니다. </li>
     <li>변경 사항을 볼 수 있도록 텍스트 편집기를 새로 고칩니다.\서신 UI를 만듭니다.<br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td>여러 특수 문자 숨기기</td>
   <td>
    <ol>
     <li>속성 "sling:hideChildren (String 또는 String[])"을 "/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters"에 추가합니다. </li>
     <li>노드 이름(숨길 특수 문자)을 "sling:hideChildren" 속성 값으로 추가합니다. </li>
     <li>모두 저장을 클릭합니다. </li>
     <li>변경 사항을 볼 수 있도록 텍스트 편집기를 새로 고칩니다.\서신 UI를 만듭니다.<br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td>특수 문자 순서 지정</td>
   <td>
    <ol>
     <li>필수 속성을 가진 "/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters" 아래에 하위 노드를 추가합니다. </li>
     <li>새로 만든 하위 노드에 "sling:orderBefore (String)" 속성을 추가합니다. </li>
     <li>노드 이름을 새로 추가된 특수 문자를 표시할 값으로 추가합니다. </li>
     <li>모두 저장을 클릭합니다. </li>
     <li>변경 사항을 볼 수 있도록 텍스트 편집기를 새로 고칩니다.\서신 UI를 만듭니다.<br /> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>
