---
title: AEM Form 서비스 팩용 핫픽스
description: AEM Forms 서비스 팩용 핫픽스를 다운로드하고 설치하는 방법에 대한 정보를 제공합니다
source-git-commit: 169d407835098add0312b0d12c2c80035b525762
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 1%

---


# Adobe Experience Manager 핫픽스{#aem-form-hotfix}

최신 버전 설치 [AEM 서비스 팩](/help/release-notes/release-notes.md) 는 Adobe Experience Manager 6.5의 공식 출시 이후에 발표된 보안, 성능, 안정성 및 주요 고객 수정 사항과 개선 사항을 포함하는 것이 좋습니다.

## 적응형 Forms에 대한 핫픽스 {#hotfix-for-adaptive-forms}

<table>
  <tbody>
  <tr>
    <td><strong>날짜</strong></td>
    <td><strong>핫픽스 이름</strong></td>
    <td><strong>수정 사항</strong></td>
   </tr>
   <tr>
    <td>2023년 11월 20일</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-linux-pkg-6.0.1016-002.zip">Linux용 AEM 서비스 팩 6.5.18.0 핫픽스</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-win-pkg-6.0.1016-002.zip">Windows용 AEM 서비스 팩 6.5.18.0용 핫픽스</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-osx-pkg-6.0.1016-002.zip">Mac OS용 AEM 서비스 팩 6.5.18.0용 핫픽스</a></li>
     </ul>
     </td>
    <td>
    <ul>
    <li>리디렉션 URL이 적응형 양식의 안내서 컨테이너에 설정되면 인라인 서명이 작동하지 않습니다. (FORMS-10493)</li>
    <li>지역화된 적응형 Forms에 대해 기록 문서(DoR) 템플릿을 게시할 수 없습니다. (FORMS-10535)</li>
    <li>대형 인라인 이미지가 있는 대화형 통신을 편집 모드에서 열 수 없습니다. (FORMS-10578)</li>
    </ul>
    </td>    
    </tr>
    <tbody>
     </table>

## 핫픽스 다운로드 및 설치 {#download-install-hotfix}

다음 단계를 수행하여 핫픽스를 다운로드하고 설치합니다.

1. 다운로드 [핫픽스](#hotfix-for-adaptive-forms) SD 링크에서 가져옵니다.
1. 핫픽스 아카이브 파일을 추출하여 Experience Manager 패키지(.zip)와 번들(.jar) 파일을 가져올 수 있습니다.
1. 패키지 관리자를 통해 패키지(.zip)를 업로드하고 설치합니다.
1. 구성 관리자 번들을 엽니다. `https://server:host/system/console/bundles`번들(.jar)을 업로드하고 설치합니다.
