---
title: 대화형 통신 구성 속성
seo-title: 대화형 통신 구성 속성
description: Interactive Communications에 대한 기본 구성 속성 편집
seo-description: Interactive Communications에 대한 기본 구성 속성 편집
uuid: 4030078f-64a3-40bb-9892-49e22a8da561
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
topic-tags: interactive-communications
discoiquuid: acb61d37-cd22-422e-bbf3-a2979b13ad41
docset: aem65
feature: 대화형 통신
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '627'
ht-degree: 5%

---


# 대화형 통신 구성 속성{#interactive-communications-configuration-properties}

대화형 통신에는 [AEM Forms Add-on](../../forms/using/installing-configuring-aem-forms-osgi.md) 패키지를 설치한 후 자동으로 구성된 속성이 포함됩니다. 대화형 통신 작성자는 **Adobe Experience Manager 웹 콘솔 구성** 페이지를 사용하여 이러한 기본 구성 속성을 편집할 수 있습니다.

다음 URL을 사용하여 **Adobe Experience Manager 웹 콘솔 구성** 페이지를 엽니다.

`https:/[server]:[port]/<contextPath>/system/console/configMgr`

구성 속성은 다음과 같습니다.

* [문서 조각 구성](#document-fragments-configuration)
* [통신 구성 만들기](#create-correspondence-configuration)
* [적응형 양식 및 대화형 커뮤니케이션 웹 채널 구성](#adaptive-form-and-interactive-communication-web-channel-configuration)
* [적응형 양식 및 대화형 커뮤니케이션 웹 채널 테마 구성](#adaptive-form-and-interactive-communication-web-channel-theme-configuration)

## 문서 조각 구성 {#document-fragments-configuration}

문서 조각에 대한 구성 속성을 보려면 **Adobe Experience Manager 웹 콘솔 구성** 페이지에서 **문서 조각 구성**&#x200B;을 누릅니다.

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
   <td>인쇄 및 웹 채널을 위한 대화형 통신을 만드는 동안 사용할 수 있는 필드, 변수 및 양식 데이터 모델 요소에 대한 로케일별 표시 형식.</td> 
   <td> 
    <ul> 
     <li>locale = en_US, de_DE, fr_FR 및 ja_JP</li> 
     <li>dateFormat = dd-MM-yyyy</li> 
     <li>numberDecimalSeparator = .</li> 
     <li>numberGroupSeparator = ,</li> 
     <li>numberUseGroupSeparator = true</li> 
    </ul> </td> 
   <td><p>—</p> </td> 
  </tr> 
  <tr> 
   <td>들여쓰기</td> 
   <td>목록 문서 조각의 텍스트에 적용된 단일 들여쓰기 단위의 폭입니다.</td> 
   <td>12.7밀리미터</td> 
   <td>번호</td> 
  </tr> 
  <tr> 
   <td>로마자 숫자 최소 폭</td> 
   <td>목록 문서 조각에서 로마자 숫자를 사용할 때 글머리 기호 또는 번호 필드에 적용할 최소 폭입니다. </td> 
   <td>12.7밀리미터</td> 
   <td>번호</td> 
  </tr> 
  <tr> 
   <td>최소 폭 수</td> 
   <td>목록 문서 조각에서 로마자 숫자와 별도로 번호 매기기 목록을 사용할 때 글머리 기호 또는 번호 필드에 적용할 최소 너비.</td> 
   <td>8.0밀리미터</td> 
   <td>번호</td> 
  </tr> 
 </tbody> 
</table>

## 통신 구성 만들기 {#create-correspondence-configuration}

에이전트 UI에 대한 구성 속성을 보려면 **Adobe Experience Manager 웹 콘솔 구성** 페이지에서 **메일 구성 만들기**&#x200B;를 누릅니다.

<table>
 <tbody> 
  <tr> 
   <td>속성</td> 
   <td>설명</td> 
   <td>기본값</td> 
   <td>허용되는 값</td> 
  </tr> 
  <tr> 
   <td>편집할 해결된 컨텐츠 표시</td> 
   <td>에이전트 UI에서 텍스트 모듈을 편집하는 동안 해결된 컨텐츠(자리 표시자가 아닌 실제 값)를 표시하려면 확인란을 선택합니다.</td> 
   <td>선택되지 않음</td> 
   <td>해당 없음</td> 
  </tr> 
  <tr> 
   <td>미리 보기 중 워터마크 적용</td> 
   <td>미리 보기 모드에서 대화형 통신 인쇄 채널에 워터마크를 적용하려면 확인란을 선택합니다.</td> 
   <td>선택되지 않음</td> 
   <td>해당 없음</td> 
  </tr> 
  <tr> 
   <td>PDF에서 글꼴 임베드 사용</td> 
   <td><p>PDF 문서에 글꼴을 포함하려면 이 확인란을 선택합니다. 이 옵션을 선택한 후에는 에이전트 UI를 사용하여 PDF 문서를 생성하거나 미리 본 후에 새 글꼴을 포함할 수 있습니다. 인터랙티브 커뮤니케이션의 인쇄 채널을 사용하여 PDF 문서를 생성하고 미리 볼 수 있습니다.</p> <p>PDF 문서에 글꼴을 임베드하는 것은 PDF를 생성하는 데 사용되고 PDF에 액세스하는 클라이언트 컴퓨터에서 사용할 수 없는 글꼴을 시스템에서 사용할 수 있는 경우에 유용합니다.</p> <p>글꼴 임베드에 대한 자세한 내용은 <a href="../../forms/using/customize-text-editor.md" target="_blank">텍스트 편집기 사용자 정의</a>를 참조하십시오.</p> </td> 
   <td>선택되지 않음</td> 
   <td>해당 없음</td> 
  </tr> 
 </tbody> 
</table>

## 적응형 양식 및 대화형 통신 웹 채널 구성 {#adaptive-form-and-interactive-communication-web-channel-configuration}

응용 Forms 및 대화형 통신 웹 채널에 대한 구성 속성을 보려면 **Adobe Experience Manager 웹 콘솔 구성** 페이지에서 **적응형 양식 및 대화형 통신 웹 채널 구성**&#x200B;을 누릅니다. 다음 표에서는 Interactive Communications와 관련된 속성에 대해 설명합니다.

| 속성 | 설명 | 기본값 | 허용되는 값 |
|---|---|---|---|
| 자리 표시자 표시 | 적응형 양식 및 대화형 통신에 포함된 필드의 자리 표시자를 표시하려면 이 확인란을 선택합니다. | 선택 항목 | 해당 없음 |
| 최대 캐시 항목 수 | 캐시 메모리를 사용하여 검색할 수 있는 응용 양식 및 대화형 통신의 최대 수를 설정합니다. | 100 | 번호 |
| 파일 이름을 고유하게 만들기 | 적응형 Forms 및 인터랙티브 커뮤니케이션에 첨부 파일로 포함된 파일의 고유 이름을 사용하려면 이 확인란을 선택합니다. | 선택되지 않음 | 해당 없음 |

## 적응형 양식 및 대화형 커뮤니케이션 웹 채널 테마 구성 {#adaptive-form-and-interactive-communication-web-channel-theme-configuration}

응용 Forms 및 대화형 통신 웹 채널 테마의 구성 속성을 보려면 **Adobe Experience Manager 웹 콘솔 구성** 페이지에서 **적응형 양식 및 대화형 통신 웹 채널 테마 구성**&#x200B;을 누릅니다.

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
   <td>적응형 Forms 및 대화형 통신을 만드는 동안 사용할 수 있는 글꼴 목록.</td> 
   <td><p>조지아</p> <p>Book Antiqua</p> <p>Times New Roman</p> <p>Arial</p> <p>Arial Black</p> <p>영향</p> <p>Palatino Linotype</p> </td> 
   <td>모든 유효한 Adobe 서버 글꼴</td> 
  </tr> 
 </tbody> 
</table>

