---
title: HTML 5 양식과 PDF forms 간의 기능 차별화
seo-title: Feature differentiation between HTML5 forms and PDF forms
description: HTML 5 양식 및 PDF forms에서 지원되는 기능
seo-description: Feature supported in HTML5 forms and PDF forms
uuid: 6ddee197-d108-4897-9976-77d115a06504
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: bdd97c20-d1f2-4898-9862-1a6a8071be88
docset: aem65
feature: Mobile Forms
exl-id: 3150f95f-7150-4eee-b5a9-121422dec2a1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 2%

---

# HTML 5 양식과 PDF forms 간의 기능 차별화 {#feature-differentiation-between-html-forms-and-pdf-forms}

다음 표에서는 HTML5 양식 및 PDF forms에 제공된 기능을 지정합니다.

<table>
 <tbody>
  <tr>
   <th>기능</th>
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
   <td><strong>디지털 서명</strong> 는 지원되지 않지만, 새로운 <strong>스크리블 서명</strong> 서명과 같은 종이에 대한 필드가 추가되었습니다. 그 위에 서명을 써넣을 수 있다 <strong>스크리블 서명</strong> 필드. 서명은 양식에 이미지로 저장됩니다. 지리적 위치 정보를 <strong>스크리블 서명</strong> 필드.</td>
   <td>서명 필드에 사용할 수 있습니다. <strong>디지털 서명</strong>.</td>
  </tr>
  <tr>
   <td>데이터 병합</td>
   <td>지원됨</td>
   <td>지원됨</td>
  </tr>
  <tr>
   <td>이미지</td>
   <td>데이터 URI 체계는 이미지를 표시하는 데 사용됩니다. 모든 최신 버전의 브라우저는 이 체계를 지원하지만 각 브라우저가 지원하는 이미지 형식 범위에 차이가 있습니다.<br /> </td>
   <td>.gif, .png, .jpeg, .bmp 및 .tiff 형식이 지원됩니다.</td>
  </tr>
  <tr>
   <td>페이지 매김<br /> </td>
   <td><p>HTML5 양식은 PDF forms과 유사한 모양을 제공하기 위해 패널과 상자로 나누어집니다. 페이지 크기는 동적으로 계산됩니다. HTML5 양식에 있는 페이지의 모든 컨텐츠가 삭제되거나 숨겨진 것으로 표시되면 빈 페이지가 숨겨지고 빈 페이지 및 빈 페이지 사이에 빈 공간(빈 공간)이 표시되지 않습니다.</p> <p>데이터 병합 또는 스크립트가 페이지에 컨텐츠를 추가하는 경우 페이지 길이는 새로 추가된 컨텐츠를 수용하도록 확장됩니다. 새로 추가된 콘텐츠를 수용하기 위해 양식에 새 페이지가 추가되지 않습니다. </p> <p><strong>참고:</strong> HTML5 양식에 있는 페이지의 모든 컨텐츠가 삭제되거나 숨겨진 것으로 표시되면 빈 페이지(빈 공간)는 첫 번째 페이지와 두 번째 페이지 사이에 표시되지만 다른 페이지 간에는 표시되지 않습니다.</p> </td>
   <td>PDF의 페이지 매김이 병합된 데이터 콘텐츠 또는 사용자 콘텐츠 수에 따라 다르며, 이 페이지 수에 따라 페이지 수가 증가/감소합니다.</td>
  </tr>
  <tr>
   <td>머리글/바닥글 </td>
   <td>지원됨. <br /> <br /> HTML5 모바일 양식에서는 페이지 나누기를 지원하지 않으므로 머리글과 바닥글은 한 번만 표시됩니다. 그러나 레이아웃에 설정하여 모바일 양식 미리 보기에서 여러 위치에 표시할 수 있습니다.<br /> </td>
   <td>지원됨</td>
  </tr>
  <tr>
   <td>사용자 지정 위젯</td>
   <td>위젯을 사용자 지정하여 모바일 장치에서 사용자 경험을 향상시킬 수 있습니다.<br /> </td>
   <td>모든 위젯이 잠기고 사용자 지정 위젯을 연결할 수 없습니다.<br /> </td>
  </tr>
  <tr>
   <td>XFA 스크립트 API</td>
   <td>가장 일반적으로 사용되는 XFA 스크립트 구문을 지원합니다. 지원되는 구문에 대한 자세한 내용은 <a href="/help/forms/using/scripting-support.md">스크립팅 지원</a>.</td>
   <td>모든 XFA 스크립트 구문을 지원합니다.</td>
  </tr>
  <tr>
   <td>Acrobat 스크립트 API </td>
   <td>HTML5 양식은 가장 일반적으로 사용되는 API를 지원합니다. 자세한 내용은 <a href="/help/forms/using/scripting-support.md">스크립팅 지원</a>.</td>
   <td>PDF 파일이 Acrobat 또는 Reader 내에 열려 있는 경우 Acrobat에서 제공하는 모든 스크립트 API도 지원합니다.</td>
  </tr>
  <tr>
   <td>오른쪽에서 왼쪽 쓰기 언어 지원 </td>
   <td>지원됨</td>
   <td>지원됨</td>
  </tr>
 </tbody>
</table>

<!--Follow the best practices to enable a form template for HTML5 renditions and ensure that the behavior and appearance of HTML5 forms and XFA-based PDF is consistent. For detailed list of best practices, see [Best practices to design an HTML5 form.](/help/forms/using/best-practices-design-html5-forms.md)-->
