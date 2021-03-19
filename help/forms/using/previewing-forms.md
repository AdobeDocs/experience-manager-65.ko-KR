---
title: 양식 미리 보기
seo-title: 양식 미리 보기
description: 양식을 게시하거나 활성화하기 전에 미리 볼 수 있으므로 예상대로 재생할 수 있습니다. 미리 보기 옵션은 지원되는 양식 유형에 따라 다를 수 있습니다.
seo-description: 양식을 게시하거나 활성화하기 전에 미리 볼 수 있으므로 예상대로 재생할 수 있습니다. 미리 보기 옵션은 지원되는 양식 유형에 따라 다를 수 있습니다.
uuid: 9ec359ea-f518-441c-9c3d-e3c1ea07a532
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 377d804d-4a75-4c93-8125-d2660cf56418
feature: 적응형 양식
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 3%

---


# {#previewing-a-form} 양식 미리 보기

## 개요 {#overview}

AEM Forms에서는 저장소에 있는 양식과 문서를 미리 볼 수 있습니다. 미리 보기를 사용하면 최종 사용자에게 양식을 제공할 때 양식의 모양과 작동 방식을 정확하게 파악할 수 있습니다.

양식을 미리 볼 때 대화형 인터페이스로 렌더링되고 사용자는 데이터로 양식을 채울 수 있습니다. 문서를 미리 볼 때 비대화형 모드로 렌더링되므로 사용자는 문서를 볼 수만 있습니다. 양식의 경우 사용자 정의 미리 보기의 추가 옵션을 사용할 수 있습니다. 이 옵션을 사용하면 XML 파일의 데이터를 사용하여 양식을 미리 볼 수 있습니다. 데이터는 미리 보고 있는 양식의 일부 또는 전체 필드를 채웁니다.

다음 표는 지원되는 다양한 유형의 양식에 사용할 수 있는 미리 보기 옵션을 보여 줍니다.

<table>
 <tbody>
  <tr>
   <td><strong>자산 유형</strong><br /> </td>
   <td><strong>사용 가능한 미리 보기 옵션</strong><br /> </td>
  </tr>
  <tr>
   <td>문서</td>
   <td>PDF 미리 보기</td>
  </tr>
  <tr>
   <td>PDF 양식</td>
   <td>데이터<br />를 사용하여 PDF 미리 보기 및 미리 보기 </td>
  </tr>
  <tr>
   <td>적응형 양식</td>
   <td>데이터를 사용하여 HTML 미리 보기 및 HTML 미리 보기</td>
  </tr>
  <tr>
   <td>양식 템플릿</td>
   <td>PDF 미리 보기, 데이터를 사용한 PDF 미리 보기, HTML 미리 보기, 데이터를 사용한 HTML 미리 보기<br /> </td>
  </tr>
 </tbody>
</table>

## {#previewing-a-form-1} 양식 미리 보기

1. 미리 보려는 자산을 선택하고 작업 도구 모음에서 ![aem6forms_preview](assets/aem6forms_preview.png) 미리 보기를 클릭합니다.

   >[!NOTE]
   >
   >자산을 선택하려면 기본 카드 보기에서 목록 보기로 전환합니다. 보기를 전환하려면 ![aem6forms_viewlist](assets/aem6forms_viewlist.png) 또는 ![aem6forms_viewcard](assets/aem6forms_viewcard.png)를 클릭합니다.

1. 미리 보기를 클릭하면 선택한 자산 유형에 적용할 수 있는 미리 보기 옵션이 나열됩니다. 원하는 옵션을 클릭하여 선택한 자산을 새 탭에서 렌더링합니다.

   옵션은 다음과 같습니다.

   * HTML로 미리 보기
   * 데이터를 포함한 미리 보기
   * PDF로 미리 보기(양식 템플릿에 사용 가능)

## 데이터를 포함한 미리 보기 {#preview-with-data}

**데이터를 사용하여 미리 보기**&#x200B;를 선택하면 실제 데이터를 입력한 양식이 어떻게 표시되는지 확인할 수 있습니다. 데이터로 미리 보기 옵션을 사용하면 샘플 사용자 데이터가 포함된 XML을 업로드할 수 있습니다. 샘플 사용자 데이터는 선택한 형식으로 미리 보기 양식을 채우는 데 사용됩니다.

1. 자산을 선택하고 미리 보기 ![aem6forms_preview](assets/aem6forms_preview.png)를 클릭한 다음 **데이터를 사용하여 미리 보기**&#x200B;를 선택합니다.
1. 양식 미리 보기 대화 상자에서 FormData를 XML 파일로 제공합니다. XML의 병합된 데이터로 양식을 렌더링하려면 [미리 보기]를 클릭합니다.

