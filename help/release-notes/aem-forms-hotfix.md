---
title: AEM Forms용 핫픽스
description: AEM Forms용 핫픽스를 다운로드하고 설치하는 방법에 대해 설명합니다.
exl-id: 37287332-3c8d-4ddc-a77e-3c5ee332898b
source-git-commit: 4c47fc5d03732d206c9eb18feb6e44018e936472
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 1%

---

# Adobe Experience Manager Forms 핫픽스{#aem-form-hotfix}

이 문서에서는 알려진 문제를 해결하고, 시스템 안정성을 향상시키며, AEM Forms의 전반적인 성능을 개선하기 위해 구현된 주요 수정 사항을 나열합니다.

## 적응형 Forms에 대한 핫픽스 {#hotfix-for-adaptive-forms}

<table>
  <tbody>
  <tr>
    <td><strong>날짜</strong></td>
    <td><strong>핫픽스 다운로드 링크(AEM Software Distribution 링크)</strong></td>
    <td><strong>해결된 문제</strong></td>
   </tr>
   <tr>
    <td>2023년 11월 20일 화요일</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-linux-pkg-6.0.1016-002.zip">Linux용 AEM 서비스 팩 6.5.18.0 핫픽스</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-win-pkg-6.0.1016-002.zip">Microsoft Windows용 AEM 서비스 팩 6.5.18.0용 핫픽스</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-osx-pkg-6.0.1016-002.zip">Apple macOS용 AEM 서비스 팩 6.5.18.0 핫픽스</a></li>
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

1. 다운로드 [핫픽스](#hotfix-for-adaptive-forms) 소프트웨어 배포 링크에서 다운로드할 수 있습니다.
1. 핫픽스 아카이브 파일을 추출하여 Experience Manager 패키지(.zip)와 번들(.jar) 파일을 가져올 수 있습니다.
1. 를 통해 패키지(.zip) 업로드 및 설치 [패키지 관리자](https://experienceleague.adobe.com/docs/experience-manager-65/content/sites/administering/contentmanagement/package-manager.html?lang=es#accessing).
1. 구성 관리자 번들을 엽니다. `https://server:host/system/console/bundles`번들(.jar)을 업로드하고 설치합니다. 핫픽스가 설치되었습니다.
