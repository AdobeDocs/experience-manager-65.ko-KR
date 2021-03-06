---
title: 사용자 지정 포털과 서신 만들기 UI 통합
seo-title: 사용자 지정 포털과 서신 만들기 UI 통합
description: 사용자 지정 포털과 서신 UI 만들기를 통합하는 방법을 알아봅니다
seo-description: 사용자 지정 포털과 서신 UI 만들기를 통합하는 방법을 알아봅니다
uuid: 68ef5bf2-b271-4c44-8840-6c495069164d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 0d3bb98e-7139-4d8e-b110-6ebd11debda1
docset: aem65
feature: 서신 관리
exl-id: c3b6ee31-ccbb-4446-86c8-f618226fefc4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 4%

---

# 사용자 지정 포털과 서신 만들기 UI 통합{#integrating-create-correspondence-ui-with-your-custom-portal}

## 개요 {#overview}

이 문서에서는 사용자 환경과 서신 솔루션 만들기 를 통합하는 방법을 자세히 설명합니다.

## URL 기반 호출 {#url-based-invocation}

사용자 지정 포털에서 서신 만들기 애플리케이션을 호출하는 한 가지 방법은 다음 요청 매개 변수로 URL을 준비하는 것입니다.

* 편지 템플릿의 식별자(cmLetterId 매개 변수 사용)입니다.

* 원하는 데이터 소스에서 가져온 XML 데이터의 URL입니다(cmDataUrl 매개 변수 사용).

예를 들어 사용자 지정 포털은 다음과 같이 URL을 준비합니다\
`https://'[server]:[port]'/[contextPath]/aem/forms/createcorrespondence.html?random=[timestamp]&cmLetterId=[letter identifier]&cmDataUrl=[data URL]`: 포털에서 링크의 href일 수 있습니다.

>[!NOTE]
>
>필요한 매개 변수가 URL에 동일하게(명확하게 표시)를 노출하여 GET 요청으로 전달되므로 이러한 방식으로 를 호출하는 것은 안전하지 않습니다.

>[!NOTE]
>
>서신 만들기 애플리케이션을 호출하기 전에 데이터를 저장하고 업로드하여 지정된 dataURL에서 서신 만들기 UI를 호출합니다. 이 작업은 사용자 지정 포털 자체 또는 다른 백엔드 프로세스를 통해 수행할 수 있습니다.

## 인라인 데이터 기반 호출 {#inline-data-based-invocation}

또한 보다 안전한 서신 만들기 응용 프로그램을 호출하는 또 다른 방법은 https://&#39;[server]:[port]&#39;/[contextPath]/aem/forms/createcorrespondence.html에서 매개 변수와 데이터를 단순히 URL을 히트하고, 매개 변수와 데이터를 전송하여 Create Correspondence 응용 프로그램을 POST 요청으로 호출하는 것일 수 있습니다(최종 사용자로부터 숨기기도). 즉, 이제 이전 방법에서는 불가능하거나 이상적인 cmData 매개 변수를 사용하여 동일한 요청의 일부로 서신 만들기 응용 프로그램 인라인에 대한 XML 데이터를 전달할 수 있습니다.

### 문자 {#parameters-for-specifying-letter} 지정에 대한 매개 변수

| **이름** | **유형** | **설명** |
|---|---|---|
| cmLetterInstanceId | 문자열 | 편지 인스턴스의 식별자입니다. |
| cmLetterId | 문자열 | 편지 템플릿의 이름입니다. |

테이블의 매개변수 순서는 편지 로딩에 사용되는 매개변수의 기본 설정을 지정합니다.

### XML 데이터 소스 {#parameters-for-specifying-the-xml-data-source} 지정에 대한 매개 변수

<table>
 <tbody>
  <tr>
   <td><strong>이름</strong></td> 
   <td><strong>유형</strong></td> 
   <td><strong>설명</strong></td> 
  </tr>
  <tr>
   <td>cmDataUrl<br /> </td> 
   <td>URL</td> 
   <td>cq, ftp, http 또는 file과 같은 기본 프로토콜을 사용하여 소스 파일의 XML 데이터입니다.<br /> </td> 
  </tr>
  <tr>
   <td>cmLetterInstanceId</td> 
   <td>문자열</td> 
   <td>편지 인스턴스에서 사용할 수 있는 xml 데이터 사용</td> 
  </tr>
  <tr>
   <td>cmUseTestData</td> 
   <td>부울</td> 
   <td>데이터 사전에 첨부된 테스트 데이터를 다시 사용하려면</td> 
  </tr>
 </tbody>
</table>

테이블의 매개변수 순서는 XML 데이터를 로드하는 데 사용되는 매개변수의 기본 설정을 지정합니다.

### 기타 매개 변수 {#other-parameters}

<table>
 <tbody>
  <tr>
   <td><strong>이름</strong></td> 
   <td><strong>유형</strong></td> 
   <td><strong>설명</strong></td> 
  </tr>
  <tr>
   <td>cmPreview<br /> </td> 
   <td>부울</td> 
   <td>미리 보기 모드에서 문자를 열려면 True입니다.<br /> </td> 
  </tr>
  <tr>
   <td>임의</td> 
   <td>Timestamp</td> 
   <td>브라우저 캐싱 문제를 해결하려면</td> 
  </tr>
 </tbody>
</table>

cmDataURL에 http 또는 cq 프로토콜을 사용하는 경우 http/cq의 URL에 익명으로 액세스할 수 있어야 합니다.
