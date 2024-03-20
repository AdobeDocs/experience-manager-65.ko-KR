---
title: 대화형 통신 구성 속성
description: 대화형 커뮤니케이션에 대한 기본 구성 속성 편집
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
topic-tags: interactive-communications
docset: aem65
feature: Interactive Communication
exl-id: 09eeade6-e16d-4159-b26a-803c7201097a
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 6%

---

# 대화형 통신 구성 속성{#interactive-communications-configuration-properties}

대화형 통신에는 를 설치한 후 자동으로 구성되는 속성이 포함되어 있습니다. [AEM Forms 추가 기능](../../forms/using/installing-configuring-aem-forms-osgi.md) 패키지. 대화형 통신 작성자는 다음을 사용하여 이러한 기본 구성 속성을 편집할 수 있습니다 **Adobe Experience Manager 웹 콘솔 구성** 페이지를 가리키도록 업데이트하는 중입니다.

를 엽니다. **Adobe Experience Manager 웹 콘솔 구성** 다음 URL을 사용하는 페이지:

`https:/[server]:[port]/<contextPath>/system/console/configMgr`

구성 속성은 다음과 같습니다.

* [문서 단편 구성](#document-fragments-configuration)
* [서신 구성 만들기](#create-correspondence-configuration)
* [적응형 양식 및 대화형 통신 웹 채널 구성](#adaptive-form-and-interactive-communication-web-channel-configuration)
* [적응형 양식 및 대화형 통신 웹 채널 테마 구성](#adaptive-form-and-interactive-communication-web-channel-theme-configuration)

## 문서 단편 구성 {#document-fragments-configuration}

선택 **문서 단편 구성** 다음에 있음 **Adobe Experience Manager 웹 콘솔 구성** 문서 조각에 대한 구성 속성을 볼 수 있는 페이지입니다.

<table>
 <tbody> 
  <tr> 
   <td>속성</td> 
   <td>설명</td> 
   <td>기본값</td> 
   <td>허용되는 값</td> 
  </tr> 
  <tr> 
   <td>데이터 표시 형식</td> 
   <td>인쇄 및 웹 채널용 대화형 통신을 만드는 동안 사용할 수 있는 필드, 변수 및 양식 데이터 모델 요소의 로케일별 표시 형식입니다.</td> 
   <td> 
    <ul> 
     <li>locale = en_US, de_DE, fr_FR 및 ja_JP</li> 
     <li>날짜 형식 = dd-MM-yyyy</li> 
     <li>numberDecimalSeparator = .</li> 
     <li>numberGroupSeparator = ,</li> 
     <li>numberUseGroupSeparator = true</li> 
    </ul> </td> 
   <td><p>—</p> </td> 
  </tr> 
  <tr> 
   <td>들여쓰기</td> 
   <td>목록 문서 조각의 텍스트에 적용된 단일 들여쓰기 단위 폭입니다.</td> 
   <td>12.7밀리미터</td> 
   <td>숫자</td> 
  </tr> 
  <tr> 
   <td>로마 숫자 최소 너비</td> 
   <td>목록 문서 조각에서 로마 숫자를 사용할 때 글머리 기호 또는 숫자 필드에 적용할 최소 너비입니다. </td> 
   <td>12.7밀리미터</td> 
   <td>숫자</td> 
  </tr> 
  <tr> 
   <td>숫자 최소 너비</td> 
   <td>목록 문서 조각에서 로마자 숫자 이외의 번호 매기기 목록을 사용할 때 글머리 기호 또는 번호 필드에 적용할 최소 너비입니다.</td> 
   <td>8.0mm</td> 
   <td>숫자</td> 
  </tr> 
 </tbody> 
</table>

## 서신 구성 만들기 {#create-correspondence-configuration}

선택 **서신 구성 만들기** 다음에 있음 **Adobe Experience Manager 웹 콘솔 구성** 에이전트 UI에 대한 구성 속성을 볼 수 있는 페이지입니다.

<table>
 <tbody> 
  <tr> 
   <td>속성</td> 
   <td>설명</td> 
   <td>기본값</td> 
   <td>허용되는 값</td> 
  </tr> 
  <tr> 
   <td>편집을 위해 해결된 컨텐츠 표시</td> 
   <td>에이전트 UI에서 텍스트 모듈을 편집하는 동안 해결된 콘텐츠(자리 표시자 대신 실제 값)를 표시하려면 확인란을 선택합니다.</td> 
   <td>선택되지 않음</td> 
   <td>해당되지 않음</td> 
  </tr> 
  <tr> 
   <td>미리 보는 동안 워터마크 적용</td> 
   <td>미리보기 모드에서 대화형 통신의 인쇄 채널에 워터마크를 적용하려면 확인란을 선택합니다.</td> 
   <td>선택되지 않음</td> 
   <td>해당되지 않음</td> 
  </tr> 
  <tr> 
   <td>PDF에서 글꼴 임베드 활성화</td> 
   <td><p>PDF 문서에서 글꼴 임베딩을 활성화하려면 확인란을 선택합니다. 이 옵션을 선택하면 에이전트 UI를 사용하여 PDF 문서를 생성하거나 미리 본 후 새 글꼴을 포함할 수 있습니다. 대화형 통신의 인쇄 채널을 사용하여 PDF 문서를 생성하고 미리 볼 수 있습니다.</p> <p>PDF 문서에 글꼴을 포함하는 것은 PDF을 생성하는 데 사용되는 시스템에서 글꼴을 사용할 수 있고 PDF에 액세스하는 클라이언트 시스템에서 글꼴을 사용할 수 없는 경우에 유용합니다.</p> <p>글꼴 포함에 대한 자세한 내용은 <a href="../../forms/using/customize-text-editor.md" target="_blank">텍스트 편집기 사용자 지정</a>.</p> </td> 
   <td>선택되지 않음</td> 
   <td>해당되지 않음</td> 
  </tr> 
 </tbody> 
</table>

## 적응형 양식 및 대화형 통신 웹 채널 구성 {#adaptive-form-and-interactive-communication-web-channel-configuration}

선택 **적응형 양식 및 대화형 통신 웹 채널 구성** 다음에 있음 **Adobe Experience Manager 웹 콘솔 구성** 적응형 Forms 및 대화형 통신 웹 채널에 대한 구성 속성을 볼 수 있는 페이지입니다. 다음 표에서는 대화형 통신 관련 속성을 설명합니다.

| 속성 | 설명 | 기본값 | 허용되는 값 |
|---|---|---|---|
| 자리 표시자 표시 | 적응형 양식 및 대화형 커뮤니케이션에 포함된 필드에 대한 자리 표시자 표시를 활성화하려면 확인란을 선택합니다. | 선택됨 | 해당되지 않음 |
| 최대 캐시 항목 수 | 캐시 메모리를 사용하여 검색할 수 있는 적응형 양식 및 대화형 통신의 최대 수를 설정합니다. | 100 | 숫자 |
| 파일 이름을 고유하게 지정 | 적응형 Forms 및 대화형 커뮤니케이션에 첨부 파일로 포함된 파일의 고유한 이름을 설정하려면 확인란을 선택합니다. | 선택되지 않음 | 해당되지 않음 |

## 적응형 양식 및 대화형 통신 웹 채널 테마 구성 {#adaptive-form-and-interactive-communication-web-channel-theme-configuration}

선택 **적응형 양식 및 대화형 통신 웹 채널 테마 구성** 다음에 있음 **Adobe Experience Manager 웹 콘솔 구성** 적응형 Forms 및 대화형 통신 웹 채널 테마에 대한 구성 속성을 볼 수 있는 페이지입니다.

<table>
 <tbody> 
  <tr> 
   <td>속성</td> 
   <td>설명</td> 
   <td>기본값</td> 
   <td>허용되는 값</td> 
  </tr> 
  <tr> 
   <td>글꼴 목록 이름</td> 
   <td>적응형 Forms 및 대화형 커뮤니케이션을 만드는 동안 사용할 수 있는 글꼴 목록입니다.</td> 
   <td><p>Georgia</p> <p>Book Antiqua</p> <p>Times New Roman</p> <p>Arial</p> <p>Arial Black</p> <p>영향</p> <p>Palatino Linotype</p> </td> 
   <td>유효한 모든 Adobe 서버 글꼴</td> 
  </tr> 
 </tbody> 
</table>
