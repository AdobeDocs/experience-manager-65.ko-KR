---
title: HTML 5 양식과 PDF forms 간의 차별화된 기능
description: HTML 5 양식과 PDF forms 간의 기능 차이점에 대해 알아봅니다.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: Mobile Forms
exl-id: 3150f95f-7150-4eee-b5a9-121422dec2a1
source-git-commit: 5e56441d2dc9b280547c91def8d971e7b1dfcfe3
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 2%

---

# HTML 5 양식과 PDF forms 간의 차별화된 기능 {#feature-differentiation-between-html-forms-and-pdf-forms}

다음 표는 HTML5 양식 및 PDF forms에 대해 제공되는 기능 지원을 지정합니다.

<table>
 <tbody>
  <tr>
   <th>특별 포함</th>
   <th>HTML5 양식</th>
   <th>PDF</th>
  </tr>
  <tr>
   <td>바코드<br /> </td>
   <td>사용자 인터페이스 수준에서 사용할 수 없습니다. </td>
   <td>지원됨</td>
  </tr>
  <tr>
   <td>서명 필드<br /> </td>
   <td><strong>디지털 서명</strong> 은(는) 지원되지 않지만 새 항목 <strong>낙서 서명</strong> 서명과 같은 용지에 대한 필드가 추가됩니다. 다음을 사용하여 양식에 서명할 수 있습니다. <strong>낙서 서명</strong> 필드. 서명은 양식에 이미지로 저장됩니다. 지리적 위치 정보를 저장할 수 있습니다. <strong>낙서 서명</strong> 필드.</td>
   <td>사용 가능한 서명 필드: <strong>디지털 서명</strong>.</td>
  </tr>
  <tr>
   <td>데이터 병합</td>
   <td>지원됨</td>
   <td>지원됨</td>
  </tr>
  <tr>
   <td>이미지</td>
   <td>데이터 URI 스키마는 이미지를 표시하는 데 사용됩니다. 모든 최신 버전의 브라우저는 이 체계를 지원하지만 각 브라우저가 지원하는 이미지 형식 범위에는 차이가 있습니다.<br /> </td>
   <td>.gif, .png, .jpeg, .bmp, .tiff 형식이 지원됩니다.</td>
  </tr>
  <tr>
   <td>페이지 매김<br /> </td>
   <td><p>HTML5 폼은 패널과 상자로 나뉘어 PDF forms과 비슷한 모양을 제공합니다. 페이지 크기는 동적으로 계산됩니다. HTML5 양식에 있는 페이지의 모든 콘텐츠가 삭제되거나 숨겨진 것으로 표시되면 빈 페이지가 숨겨집니다. 빈 페이지의 위와 아래에 있는 페이지 사이에는 빈 공간(빈 공간)이 표시되지 않습니다.</p> <p>데이터 병합 또는 스크립트가 페이지에 콘텐츠를 추가하는 경우, 새로 추가된 콘텐츠에 맞게 페이지 길이가 확장됩니다. 새로 추가된 콘텐츠를 수용하기 위해 양식에 새 페이지가 추가되지 않습니다. </p> <p><strong>참고:</strong> HTML5 양식에 있는 페이지의 모든 콘텐츠가 삭제되거나 숨겨진 것으로 표시되면 빈 페이지(공백)는 첫 번째 페이지와 두 번째 페이지 사이에 표시되지만 다른 페이지 사이에는 표시되지 않습니다.</p> </td>
   <td>PDF의 페이지 매김 은 병합된 데이터 콘텐츠 또는 사용자 콘텐츠에 따라 다르며 페이지 수는 그에 따라 증가/감소합니다.</td>
  </tr>
  <tr>
   <td>머리글/바닥글 </td>
   <td>지원됨. <br /> <br /> HTML5 모바일 양식에서는 페이지 나누기를 지원하지 않으므로 머리글과 바닥글은 한 번만 표시됩니다. 그러나 모바일 양식 미리 보기의 여러 위치에 나타나도록 레이아웃에서 설정할 수 있습니다.<br /> </td>
   <td>지원됨</td>
  </tr>
  <tr>
   <td>사용자 정의 위젯</td>
   <td>위젯을 사용자 정의하여 모바일 디바이스에서 사용자 경험을 향상시킬 수 있습니다.<br /> </td>
   <td>모든 위젯이 잠기고 사용자 정의 위젯을 연결할 수 없습니다.<br /> </td>
  </tr>
  <tr>
   <td>XFA 스크립트 API</td>
   <td>가장 일반적으로 사용되는 XFA 스크립트 구문을 지원합니다. 지원되는 구문의 자세한 목록은 다음을 참조하십시오. <a href="/help/forms/using/scripting-support.md">스크립팅 지원</a>.</td>
   <td>모든 XFA 스크립트 구문을 지원합니다.</td>
  </tr>
  <tr>
   <td>Acrobat 스크립트 API </td>
   <td>HTML 5 양식은 가장 일반적으로 사용되는 API를 지원합니다. 자세한 내용은 <a href="/help/forms/using/scripting-support.md">스크립팅 지원</a>.</td>
   <td>PDF 파일이 Acrobat 또는 Reader 내에서 열려 있는 경우 Acrobat에서 제공하는 모든 스크립트 API도 지원합니다.</td>
  </tr>
  <tr>
   <td>오른쪽에서 왼쪽 쓰기 언어 지원 </td>
   <td>지원됨</td>
   <td>지원됨</td>
  </tr>
 </tbody>
</table>

<!--Follow the best practices to enable a form template for HTML5 renditions and ensure that the behavior and appearance of HTML5 forms and XFA-based PDF is consistent. For detailed list of best practices, see [Best practices to design an HTML5 form.](/help/forms/using/best-practices-design-html5-forms.md)-->
