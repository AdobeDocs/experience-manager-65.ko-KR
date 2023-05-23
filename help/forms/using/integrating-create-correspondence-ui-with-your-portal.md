---
title: 서신 만들기 UI를 사용자 정의 포털과 통합
seo-title: Integrating Create Correspondence UI with your custom portal
description: 서신 만들기 UI를 사용자 정의 포털과 통합하는 방법을 알아봅니다
seo-description: Learn how to integrate create correspondence UI with your custom portal
uuid: 68ef5bf2-b271-4c44-8840-6c495069164d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 0d3bb98e-7139-4d8e-b110-6ebd11debda1
docset: aem65
feature: Correspondence Management
exl-id: c3b6ee31-ccbb-4446-86c8-f618226fefc4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 4%

---

# 서신 만들기 UI를 사용자 정의 포털과 통합{#integrating-create-correspondence-ui-with-your-custom-portal}

## 개요 {#overview}

이 문서에서는 서신 만들기 솔루션을 환경과 통합하는 방법에 대해 자세히 설명합니다.

## URL 기반 호출 {#url-based-invocation}

사용자 지정 포털에서 서신 만들기 애플리케이션을 호출하는 한 가지 방법은 다음 요청 매개 변수로 URL을 준비하는 것입니다.

* 문자 템플릿의 식별자(cmLetterId 매개 변수 사용).

* 원하는 데이터 소스에서 가져온 XML 데이터의 URL(cmDataUrl 매개 변수 사용).

예를 들어 사용자 정의 포털은 다음과 같이 URL을 준비합니다.\
`https://'[server]:[port]'/[contextPath]/aem/forms/createcorrespondence.html?random=[timestamp]&cmLetterId=[letter identifier]&cmDataUrl=[data URL]`: 포털에 있는 링크의 href일 수 있습니다.

>[!NOTE]
>
>이러한 방식으로 호출하는 것은 필요한 매개 변수가 URL에 동일한 매개 변수(명확하게 표시됨)를 노출하여 GET 요청으로 전달되기 때문에 안전하지 않습니다.

>[!NOTE]
>
>서신 만들기 애플리케이션을 호출하기 전에 데이터를 저장하고 업로드하여 지정된 dataURL에서 서신 만들기 UI를 호출합니다. 이 작업은 사용자 정의 포털 자체에서 수행하거나 다른 백엔드 프로세스를 통해 수행할 수 있습니다.

## 인라인 데이터 기반 호출 {#inline-data-based-invocation}

응답 만들기 애플리케이션을 호출하는 또 다른(및 보다 안전한) 방법은 https://&#39;의 URL을 단순히 히트하는 것입니다.[server]:[포트]&#39;/[contextPath]/aem/forms/createcorrespondence.html 을 사용하여 매개 변수 및 데이터를 전송하여 응답 만들기 애플리케이션을 POST 요청으로 호출합니다(최종 사용자에게 숨기기). 즉, 이전 접근 방법에서는 불가능하거나 이상적이지 않았던 서신 작성 애플리케이션 인라인(cmData 매개 변수를 사용하여 동일한 요청의 일부로)에 대한 XML 데이터를 전달할 수 있습니다.

### 편지 지정을 위한 매개변수 {#parameters-for-specifying-letter}

| **이름** | **유형** | **설명** |
|---|---|---|
| cmLetterInstanceId | 문자열 | 편지 인스턴스에 대한 식별자. |
| cmLetterId | 문자열 | Letter 템플릿의 이름입니다. |

표의 매개 변수 순서는 문자 로드에 사용되는 매개 변수의 기본 설정을 지정합니다.

### XML 데이터 소스를 지정하기 위한 매개 변수 {#parameters-for-specifying-the-xml-data-source}

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
   <td>cq, ftp, http 또는 file과 같은 기본 프로토콜을 사용하는 소스 파일의 XML 데이터입니다.<br /> </td> 
  </tr>
  <tr>
   <td>cmLetterInstanceId</td> 
   <td>문자열</td> 
   <td>편지 인스턴스에서 사용할 수 있는 xml 데이터를 사용합니다.</td> 
  </tr>
  <tr>
   <td>cmUseTestData</td> 
   <td>부울</td> 
   <td>데이터 사전에 첨부된 테스트 데이터를 재사용합니다.</td> 
  </tr>
 </tbody>
</table>

표의 매개 변수 순서는 XML 데이터 로드에 사용되는 매개 변수의 기본 설정을 지정합니다.

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
   <td>True로 설정하면 편지가 미리 보기 모드로 열립니다<br /> </td> 
  </tr>
  <tr>
   <td>임의</td> 
   <td>타임스탬프</td> 
   <td>브라우저 캐싱 문제를 해결하려면.</td> 
  </tr>
 </tbody>
</table>

cmDataURL에 http 또는 cq 프로토콜을 사용하는 경우 http/cq의 URL은 익명으로 액세스할 수 있어야 합니다.
