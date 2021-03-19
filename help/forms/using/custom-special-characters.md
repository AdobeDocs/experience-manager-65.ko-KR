---
title: 통신 관리의 사용자 지정 특수 문자
seo-title: 통신 관리의 사용자 지정 특수 문자
description: 통신 관리에서 사용자 지정 특수 문자를 추가하는 방법을 알아봅니다.
seo-description: 통신 관리에서 사용자 지정 특수 문자를 추가하는 방법을 알아봅니다.
uuid: a1890f6d-8e0c-471f-a9bd-861acf1f17e6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 9f26565c-a7ba-4e9e-bf77-a95eb8e351f2
docset: aem65
feature: 서신 관리
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 1%

---


# 통신 관리의 사용자 지정 특수 문자{#custom-special-characters-in-correspondence-management}

## 개요 {#overview}

Correspondence Management에는 210개의 특수 문자를 쉽게 삽입할 수 있는 기본 지원이 내장되어 있습니다.

예를 들어 다음 특수 문자를 삽입할 수 있습니다.

* 통화 기호(예:, and £)
* ∑, √, ∂ 및 ^과 같은 수학 기호
* 구두점 기호 ‟ 및&quot;

다음 글자에 특수 문자를 삽입할 수 있습니다.

* [텍스트 편집기](/help/forms/using/document-fragments.md#createtext)에서
* [편집 가능한 통신](../../forms/using/create-correspondence.md#managecontent)의 인라인 모듈

![specialcharacterslinemodule](assets/specialcharactersinlinemodule.png)

관리자는 맞춤화를 통해 추가/사용자 정의 특수 문자 지원을 추가할 수 있습니다. 이 문서에서는 사용자 지정 특수 문자에 대한 지원을 추가하는 방법에 대해 설명합니다.

## 통신 관리 {#creatingfolderstructure}에서 사용자 지정 특수 문자에 대한 지원을 추가하거나 수정합니다.

사용자 지정 특수 문자에 대한 지원을 추가하려면 다음 단계를 따르십시오.

1. `https://'[server]:[port]'/[ContextPath]/crx/de`으로 이동하여 관리자로 로그인합니다.
1. apps 폴더에서 specialcharacters 폴더(libs 아래의 textEditorConfig 폴더에 있음)와 유사한 경로/구조를 가진 **[!UICONTROL specialcharacters]**&#x200B;라는 폴더를 만듭니다.

   1. 다음 경로에서 **specialcharacters** 폴더를 마우스 오른쪽 단추로 클릭하고 **오버레이 노드**&#x200B;을 선택합니다.

      `/libs/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters`

   1. [오버레이 노드] 대화 상자에 다음 값이 있는지 확인합니다.

      **경로:** /libs/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters

      **오버레이 위치:** /apps/

      **노드 유형 일치:** 선택됨

      >[!NOTE]
      >
      >/libs 분기에서는 변경하지 마십시오. 이 분기는 다음을 수행할 때마다 변경될 수 있으므로 변경한 내용이 손실될 수 있습니다.
      >
      >
      >
      >    * 인스턴스 업그레이드
      >    * 핫픽스 적용
      >    * 기능 팩 설치


   1. **확인**&#x200B;을 클릭한 다음 **모두 저장**&#x200B;을 클릭합니다. specialcharacters 폴더가 지정된 경로에 생성됩니다.

      오버레이를 만든 후 노드 구조 태그를 확인합니다. 오버레이를 사용하여 /apps에서 만들어진 각 노드는 해당 노드의 /libs에 정의된 클래스 및 속성이 같아야 합니다. /apps 위치 아래의 노드 구조에 속성이나 태그가 없는 경우 /libs의 해당 노드와 태그를 동기화하십시오.



1. **[!UICONTROL textEditorConfig]** 노드에 다음과 같은 속성과 값이 있는지 확인합니다.

   | 이름 | 유형 | 값 |
   |---|---|---|
   | cmConfigurationType | 문자열 | cmTextEditorConfiguration |
   | cssPath | 문자열 | /libs/fd/cm/ma/gui/components/admin/createasset/textcontrol/clientlibs/textcontrol |

1. 다음 경로에서 **[!UICONTROL specialcharacters]** 폴더를 마우스 오른쪽 단추로 클릭하고 **만들기 > 하위 노드**&#x200B;를 선택한 다음 **모두 저장**&#x200B;을 클릭합니다.

   /apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters/&lt;YourChildNode>

1. 텍스트 편집기 새로 고침\Create Correspondence UI 페이지. 추가한 노드는 UI의 특수 문자 목록에 있는 마지막 노드입니다.
1. **모두 저장**&#x200B;을 클릭합니다.
1. 필요에 따라 특수 문자를 변경합니다.

<table>
 <tbody>
  <tr>
   <td><strong>끝...</strong></td>
   <td><strong>다음 단계를 완료합니다.</strong></td>
  </tr>
  <tr>
   <td>사용자 정의 특수 문자 추가</td>
   <td>
    <ol>
     <li>필수 속성을 사용하여 "/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters" 아래에 하위 노드를 추가합니다.</li>
     <li>모두 저장을 클릭합니다.</li>
     <li>텍스트 편집기 새로 고침\Create Responsive UI를 사용하여 변경 사항을 확인합니다.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>기존 특수 문자 속성 업데이트</td>
   <td>
    <ol>
     <li>위에 설명한 대로 업데이트할 노드를 오버레이하고 태그 및 클래스를 확인합니다.</li>
     <li>캡션, 값, endValue 및 multipleCaption 등의 값을 변경합니다. </li>
     <li>모두 저장을 클릭합니다. </li>
     <li>텍스트 편집기 새로 고침\Create Responsive UI를 사용하여 변경 사항을 확인합니다.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>특수 문자 숨기기</td>
   <td>
    <ol>
     <li>"/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters" 아래에 숨길 노드를 오버레이합니다.</li>
     <li>숨길 노드(앱 아래)에 sling:hideResource(부울) 속성을 추가합니다. </li>
     <li>모두 저장을 클릭합니다. </li>
     <li>텍스트 편집기 새로 고침\메일 UI를 만들어 변경 내용을 확인합니다.<br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td>여러 특수 문자 숨기기</td>
   <td>
    <ol>
     <li>"/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters"에 "sling:hideChildren (String 또는 String[])" 속성을 추가합니다. </li>
     <li>"sling:hideChildren" 속성 값으로 노드 이름(숨길 특수 문자)을 추가합니다. </li>
     <li>모두 저장을 클릭합니다. </li>
     <li>텍스트 편집기 새로 고침\메일 UI를 만들어 변경 내용을 확인합니다.<br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td>특수 문자 순서 지정</td>
   <td>
    <ol>
     <li>필수 속성을 사용하여 "/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters" 아래에 하위 노드를 추가합니다. </li>
     <li>새로 만든 자식 노드에 "sling:orderBefore (String)" 속성을 추가합니다. </li>
     <li>새로 추가된 특수 문자를 표시하기 전에 노드 이름을 값으로 추가합니다. </li>
     <li>모두 저장을 클릭합니다. </li>
     <li>텍스트 편집기 새로 고침\메일 UI를 만들어 변경 내용을 확인합니다.<br /> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>

