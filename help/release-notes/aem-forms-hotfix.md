---
title: AEM Forms용 핫픽스
description: AEM Forms용 핫픽스를 다운로드하고 설치하는 방법에 대해 설명합니다.
exl-id: 37287332-3c8d-4ddc-a77e-3c5ee332898b
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: fb689e86deaabcc4033ed75f615086b630a9a525
workflow-type: tm+mt
source-wordcount: '903'
ht-degree: 1%

---

# Adobe Experience Manager Forms 핫픽스{#aem-form-hotfix}

이 문서에서는 알려진 문제를 해결하고, 시스템 안정성을 향상시키며, AEM Forms의 전반적인 성능을 개선하기 위해 구현된 주요 수정 사항을 나열합니다.

>[!NOTE]
>
> 핫픽스는 이전의 모든 수정 사항을 포함하여 누적되도록 설계되었습니다. 릴리스에 최신 핫픽스를 적용하면 최신 문제를 해결할 수 있을 뿐만 아니라 이전의 모든 버그 수정 및 개선 사항이 통합되어 있습니다.

## 적응형 Forms에 대한 핫픽스 {#hotfix-for-adaptive-forms}

<table>
  <tbody>
  <tr>
    <td><strong>날짜</strong></td>
    <td><strong>핫픽스 다운로드 링크(AEM Software Distribution 링크)</strong></td>
    <td><strong>해결된 문제</strong></td>
  </tr>
  <tr>
    <td>2024년 7월 10일 목요일</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/jboss/win/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-windows-jboss.zip.zip">JBoss JEE 서버 </a>용 Windows의 AEM 서비스 팩 6.5.21.0용 핫픽스 </li>
      <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/jboss/linux/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-linux-jboss.tar.gz">JBoss JEE 서버용 Linux의 AEM 서비스 팩 6.5.21.0용 핫픽스 </a> </li>
       <li>Webshpere JEE 서버 </a>용 Windows의 AEM 서비스 팩 6.5.21.0용 <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/websphere/win/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-windows-websphere.zip.zip">핫픽스 </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/websphere/linux/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-linux-websphere.tar.gz">Webshpere JEE 서버용 Linux의 AEM 서비스 팩 6.5.21.0용 핫픽스</a> </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/weblogic/win/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-windows-weblogic.zip.zip">Weblogic JEE 서버 </a>용 Windows의 AEM 서비스 팩 6.5.21.0용 핫픽스 </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/weblogic/linux/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-linux-weblogic.tar.gz">Weblogic JEE 서버용 Linux의 AEM 서비스 팩 6.5.21.0용 핫픽스</a> </li>
     </ul>
     </td>
    <td>
    <ul><li>사용자가 JEE 서버에서 AEM Forms 서비스 팩 20(6.5.20.0)으로 업데이트하고 출력 서비스를 사용하여 PDF을 생성하는 경우 PDF이 접근성 문제로 렌더링됩니다. (LC-3922112)</li><li>AEM Forms JEE의 출력 서비스를 사용하여 생성된 태그가 지정된 PDF에 "부적절한 구조 경고"가 표시됩니다. (LC-3922038)</li><li>AEM Forms JEE에서 양식을 제출하면 반복되는 XML 요소의 인스턴스가 데이터에서 제거됩니다. (LC-3922017)</li><li>Linux 환경의 사용자가 HTML에서 적응형 양식(JEE의)을 렌더링할 때 제대로 렌더링되지 않습니다. (LC-3921957)</li><li>사용자가 AEM Forms JEE의 출력 서비스를 사용하여 XTG 파일을 PostScript 형식으로 변환할 때 다음 오류로 인해 실패합니다. AEM_OUT_001_003: 예기치 않은 예외: PAExecute 실패: XFA_RENDER_FAILURE. (LC-3921720)</li><li>JEE 서버에서 AEM Forms 서비스 팩 18(6.5.18.0)으로 업그레이드한 후 사용자가 양식을 제출할 때 HTML5를 렌더링하지 못하거나 PDF forms 및 XMLFM이 충돌합니다. (LC-3921718)
    </ul>
    </td>    
  </tr>
  <tr>
    <td>2024년 6월 21일 토요일</td>
     <td>
     <ul>
     <li><a href="https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&amp;data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&amp;sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&amp;reserved=0">JBoss JEE 서버 </a>의 AEM 서비스 팩 6.5.21.0용 핫픽스 </li>
      <li><a href="https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&amp;data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&amp;sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&amp;reserved=0">Weblogic JEE 서버 </a>의 AEM 서비스 팩 6.5.21.0용 핫픽스 </li>
       <li><a href="https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&amp;data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&amp;sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&amp;reserved=0">Webshpere JEE 서버 </a>의 AEM 서비스 팩 6.5.21.0용 핫픽스 </li>
        <li><a href="https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&amp;data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&amp;sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&amp;reserved=0">OSGi 서버 </a>의 AEM 서비스 팩 6.5.21.0용 핫픽스 </li>
     </ul>
     </td>
    <td>
    <ul>
    <li> AEM Forms 서비스 팩 6.5.21.0으로 업그레이드한 후 PaperCapture 서비스가 PDF에서 OCR(Optical Character Recognition) 작업을 수행하지 못합니다. 설치 지침은 <a href="/help/forms/using/papercapture-service-resolution.md"> 문제 해결</a> 문서를 참조하십시오.(CQDOC-21680) </li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>2024년 6월 21일 토요일</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2Fccm-ccr-content-10.0.206.zip">AEM 서비스 팩 6.5.21.0용 핫픽스 </a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li>미리 보는 동안 XML 데이터가 있는 초안 문자가 로드 상태에서 멈춥니다. 핫픽스의 다운로드 및 설치 지침은 <a href="#install-hotfix"> 초안 문제에 대한 핫픽스 다운로드 및 설치</a> 섹션을 참조하십시오.(FORMS-14521)</li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>2024년 5월 16일 금요일</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-win-pkg-6.0.1192-010.zip">Microsoft Windows용 AEM 서비스 팩 6.5.20.0용 핫픽스</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-linux-pkg-6.0.1192-010.zip">Linux용 AEM 서비스 팩 6.5.20.0용 핫픽스 </a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-osx-pkg-6.0.1192-010.zip">Apple macOS용 AEM 서비스 팩 6.5.20.0용 핫픽스</a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li>확인란에 스크립트가 포함된 XDP를 기반으로 하는 적응형 양식에서는 이러한 확인란 이후의 요소에 대해 스크립트가 실행되지 않습니다. 이 문제에 대해 핫픽스를 사용할 수 있습니다. (FORMS-14244) </li>
     <li> 날짜 선택기 위젯의 행은 편집/표시 패턴이 있는 필드의 팝업 위젯에서 월을 트래버스할 때 잘립니다. 이 문제에 대해 핫픽스를 사용할 수 있습니다. (FORMS-13620) </li>
     <li>백엔드에서 DOR(기록 문서) 서비스를 사용하려고 할 때 양식 제출이 실패했습니다. 오류 메시지: "양식 리소스가 올바르게 할당되지 않아 제출 액션을 완료할 수 없습니다." (FORMS-13798) </li>
     <li>Adobe Experience Manager Publish 인스턴스에서 Adobe Experience Manager 워크플로우로 적응형 양식을 제출하는 경우 워크플로우가 첨부 파일을 저장하지 못합니다.  (FORMS-14209) </li>
     <li> AEM 6.5 Forms 서비스 팩 20 패키지(SP20용 AEM Forms 추가 기능 패키지)를 설치할 때 AEM Sites UI(사용자 인터페이스)의 성능이 크게 저하되었습니다.  (FORMS-13791) </li>
     <li>대화형 통신에서 미리 채우기 서비스가 실패하고 null 포인터 예외가 발생합니다. (CQDOC-21355)</li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>2024년 1월 29일 화요일</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fforms-foundation-qs-content-4.0.170-FORMS-12692-B0001.zip">JEE 서버의 Windows용 AEM 서비스 팩 6.5.19.0용 핫픽스</a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li>JEE 서버의 AEM Forms에서 컨텍스트 경로를 사용하는 HTML5 Forms이 렌더링되지 않습니다. (FORMS-12485, FORMS-12691).</li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>2024년 1월 29일 화요일</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fadobe-aemfd-win-pkg-6.0.1016-004.zip">Microsoft Windows용 AEM 서비스 팩 6.5.18.0용 핫픽스</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fadobe-aemfd-linux-pkg-6.0.1016-004.zip">Linux용 AEM 서비스 팩 6.5.18.0 핫픽스</a></li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fadobe-aemfd-osx-pkg-6.0.1016-004.zip">Apple macOS용 AEM 서비스 팩 6.5.18.0 핫픽스</a></li>
     </ul>
     </td>
    <td>
    <ul>
    <li> 즉시 사용 가능한 스크리블 서명 구성 요소가 적응형 양식의 미리 보기에 대해 렌더링되지 않습니다. (FORMS-12073).</li>
    </ul>
    </td>    
   </tr>
   <tr>
    <td>2023년 11월 20일 화요일</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-linux-pkg-6.0.1016-002.zip">Linux용 AEM 서비스 팩 6.5.18.0용 핫픽스</a> </li>
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

1. 소프트웨어 배포 링크에서 [핫픽스](#hotfix-for-adaptive-forms)를 다운로드합니다.
1. 핫픽스 아카이브 파일을 추출하여 Experience Manager 패키지(.zip)와 번들(.jar) 파일을 가져올 수 있습니다.
1. [패키지 관리자](https://experienceleague.adobe.com/docs/experience-manager-65/content/sites/administering/contentmanagement/package-manager.html?lang=es#accessing)를 통해 패키지(.zip)를 업로드하고 설치합니다.
1. Configuration Manager 번들 `https://server:host/system/console/bundles`을(를) 열고 번들(.jar)을 업로드한 후 설치합니다. 핫픽스가 설치되었습니다.


## 초안 편지 문제에 대한 핫픽스 다운로드 및 설치 {#install-hotfix}

이 문제를 해결하려면 다음 단계를 수행하십시오.

1. 소프트웨어 배포 포털에서 [핫픽스](#hotfix-for-adaptive-forms)를 다운로드합니다.
2. [CRX 패키지 관리자](https://experienceleague.adobe.com/docs/experience-manager-65/content/sites/administering/contentmanagement/package-manager.html?lang=es#accessing)를 사용하여 패키지(.zip)를 업로드하고 설치합니다.