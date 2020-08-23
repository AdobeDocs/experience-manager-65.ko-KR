---
title: 릴리즈 차량 정의 갱신
seo-title: 릴리즈 차량 정의 갱신
description: 이 문서에서는 전체 릴리스, 기능 팩 및 서비스 팩 등 다양한 유형의 AEM 릴리스에 대해 자세히 설명합니다.
seo-description: 이 문서에서는 전체 릴리스, 기능 팩 및 서비스 팩 등 다양한 유형의 AEM 릴리스에 대해 자세히 설명합니다.
uuid: 388fb6f5-0249-41e2-a460-1bb4cd0f8494
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 32695db5-d62d-4959-8a24-3d56b4a19904
translation-type: tm+mt
source-git-commit: 80b8571bf745b9e7d22d7d858cff9c62e9f8ed1e
workflow-type: tm+mt
source-wordcount: '768'
ht-degree: 4%

---


# AEM 업데이트 릴리스 차량 정의{#update-release-vehicle-definitions}

본 문서에는 Adobe이 고객에게 제공하는 전체 릴리스, 기능 팩 및 서비스 팩 등 다양한 유형의 Adobe Experience Manager(AEM) 릴리스에 대한 세부 정보가 포함되어 있습니다.

>[!NOTE]
>
>AEM 업데이트 릴리스의 릴리스 일정은 [AEM 업데이트 릴리스 로드맵을 참조하십시오.](https://helpx.adobe.com/kr/experience-manager/update-releases-roadmap.html)

## 전체 릴리스 {#full-release}

<table>
 <tbody>
  <tr>
   <td><strong>정의</strong></td>
   <td>
    <ul>
     <li>예약된 릴리스</li>
     <li>릴리스 노트에 정의된 특정 버전에 대한 업그레이드 경로 지원</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>이름 지정</strong></td>
   <td>
    <ul>
     <li>주요 릴리스의 버전 번호는 X+1.Y.Z 공식에 따라 증가합니다. </li>
     <li>부 릴리스의 버전 번호는 공식 X.Y+1.Z를 기준으로 증가합니다</li>
    </ul> <p>여기서 X는 주 버전 번호이고 Y는 보조 버전 번호이고 Z는 패치 번호입니다.</p> </td>
  </tr>
  <tr>
   <td><strong>포함</strong></td>
   <td>
    <ul>
     <li>새로운 기능</li>
     <li>향상된 기능</li>
     <li>버그 수정</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>설명서</strong></td>
   <td>
    <ul>
     <li>릴리스 노트는 설명서 포털에서 확인할 수 있습니다</li>
     <li>기능, 개선 사항 및 버그 수정에 대한 설명서는 설명서 포털에서 확인할 수 있습니다</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>캐든스</strong></td>
   <td>연간</td>
  </tr>
  <tr>
   <td><strong>가용성 및 설치</strong></td>
   <td>
    <ul>
     <li>독립 실행형 제품 설치 프로그램으로 제공</li>
     <li>라이센스 웹 사이트 및 Managed Services 라이센스 웹 사이트에서 이용 가능</li>
     <li>컨텐츠 저장소 마이그레이션이 필요할 수 있습니다.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>테스트 수준</strong></td>
   <td>QA에 의해 완전히 검증됨</td>
  </tr>
 </tbody>
</table>

## 서비스 팩 {#service-pack}

<table>
 <tbody>
  <tr>
   <td><strong>정의</strong></td>
   <td>
    <ul>
     <li>예약된 릴리스</li>
     <li>현재 롤백할 수 없습니다.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>이름 지정</strong></td>
   <td>
    <ul>
     <li>패치 릴리스 번호는 한 자리 숫자입니다.</li>
     <li>설치 후 X.Y.Z.SPx 공식에 따라 설치된 릴리스 번호 패치 숫자가 증가합니다</li>
     <li>여기서 X는 주 버전 번호이고 Y는 보조 버전 번호이고 Z는 패치 번호입니다. x는 서비스 팩 번호입니다.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>포함</strong></td>
   <td>
    <ul>
     <li>새로운 기능</li>
     <li>향상된 기능</li>
     <li>버그 수정</li>
     <li>공통 관심 기능 팩(있는 경우)</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>설명서</strong></td>
   <td>
    <ul>
     <li>설명서 포털에 있는 릴리스 노트</li>
     <li>설명서 포털의 기능, 개선 사항, 버그 수정</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>캐든스</strong></td>
   <td>분기별</td>
  </tr>
  <tr>
   <td><strong>가용성 및 설치</strong></td>
   <td>
    <ul>
     <li>패키지로 제공</li>
     <li>패키지 공유에서 사용 가능</li>
     <li>기존 기능 설치 필요</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>테스트 수준</strong></td>
   <td>
    <ul>
     <li>모든 수정 사항 QA 유효성 검사</li>
     <li>자동화를 통한 전체 패키지 안정성 실행</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 누적 수정 팩  {#cumulative-fix-pack-aem}

<table>
 <tbody>
  <tr>
   <td><strong>정의</strong></td>
   <td>
    <ul>
     <li>수정 사항 릴리스의 단일 전달 모델</li>
     <li>개별 구성 요소의 컨텐츠 패키지를 포함하는 수집기 컨텐츠 패키지</li>
     <li>CFP는 핫픽스의 롤오버이며, 그 일부에는 개선사항이 없습니다.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>이름 지정</strong></td>
   <td><p>X.Y.Z.CFPx</p> <p>여기서 X는 주 버전 번호이고 Y는 보조 버전 번호이고 Z는 패치 번호입니다. x는 누적 서비스 팩 번호입니다.</p> </td>
  </tr>
  <tr>
   <td><strong>포함</strong></td>
   <td><p>CFP는 지정된 날짜까지 모든 구성 요소의 수정 사항이 포함된 누적 수정 팩입니다. 예를 들어 고객이 CFP3을 적용하는 경우 CFP3 = CFP1 + CFP2가 됩니다.</p> </td>
  </tr>
  <tr>
   <td><strong>설명서</strong></td>
   <td>설명서 포털에 있는 릴리스 노트</td>
  </tr>
  <tr>
   <td><strong>캐든스</strong></td>
   <td>쿼터리</td>
  </tr>
  <tr>
   <td><strong>가용성 및 설치</strong></td>
   <td>
    <ul>
     <li>패키지로 제공</li>
     <li>패키지 공유에서 사용 가능</li>
     <li>최신 서비스 팩에 따라 다름</li>
     <li>CFP는 자체 종속 국가입니다. 고객은 종속성을 찾거나 해결하는 것에 대해 걱정하지 않아도 됩니다. CFP는 최신 서비스 팩에 설치해야 합니다.</li>
     <li>CFP는 단일 패키지로 설치되므로 고객 경험을 향상시킬 수 있습니다.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>테스트 수준</strong></td>
   <td>통합 수준 및 회귀 테스트에서 QA가 검증되었습니다.</td>
  </tr>
 </tbody>
</table>

## 오버레이 {#overlay}

<table>
 <tbody>
  <tr>
   <td><strong>정의</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>이름 지정</strong></td>
   <td>overlay-&lt;ticket ID&gt;</td>
  </tr>
  <tr>
   <td><strong>포함</strong></td>
   <td>JS 또는 JSP 파일에 대한 버그 수정</td>
  </tr>
  <tr>
   <td><strong>설명서</strong></td>
   <td>없음</td>
  </tr>
  <tr>
   <td><strong>캐든스</strong></td>
   <td>필요한 경우</td>
  </tr>
  <tr>
   <td><strong>가용성 및 설치</strong></td>
   <td>
    <ul>
     <li>AEM 고객 지원 센터에서 패키지로 제공</li>
     <li>서비스 팩 또는 전체 릴리스에 반드시 포함되지 않음</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>테스트 수준</strong></td>
   <td>고객 지원 센터에서 확인</td>
  </tr>
 </tbody>
</table>

## Feature Pack {#feature-pack}

<table>
 <tbody>
  <tr>
   <td><strong>정의</strong></td>
   <td>
    <ul>
     <li>기능 팩은 추가 기능이며 서비스 팩을 통해 제공됩니다. AEM 버전에서 마지막 서비스 팩을 릴리스한 경우 Adobe은 향후 기능 팩을 제공하지 않습니다.</li>
     <li>FP에는 후속 제품 릴리스로 예정되어 있지만 Adobe 제품 관리의 결정에 따라 일찍 배달되는 향상된 제품이 포함되어 있습니다.</li>
     <li>기능은 항상 다음 주요 릴리스와 병합된 다음 고객이 필요로 하는 AEM 버전으로 지원됩니다</li>
     <li>공통 관심 및 GA 기능 팩은 다음 서비스 팩에 병합됩니다.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>이름 지정</strong></td>
   <td>cq-&lt;릴리스 버전&gt;-featurepack-&lt;featurepack ID&gt;-&lt;featurepack version&gt;</td>
  </tr>
  <tr>
   <td><strong>포함</strong></td>
   <td>
    <ul>
     <li>새로운 기능</li>
     <li>향상된 기능</li>
     <li>버그 수정(증분 제품 업데이트)</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>설명서</strong></td>
   <td>설명서는 helpx.adobe.com에서 제공됩니다.</td>
  </tr>
  <tr>
   <td><strong>캐든스</strong></td>
   <td>제품 영역에 따라 다름</td>
  </tr>
  <tr>
   <td><strong>가용성 및 설치</strong></td>
   <td>
    <ul>
     <li>서비스 팩을 통해 제공</li>
     <li>패키지 공유에서 사용할 수 있습니다. 고객은 패키지 공유를 통해 Adobe의 약관에 동의합니다.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>테스트 수준</strong></td>
   <td>일반 가용성 기능 팩은 QA의 유효성을 검사함</td>
  </tr>
 </tbody>
</table>

* [1]:OAK 수정 사항은 개별 핫픽스로 제공되지 않습니다. 하지만 다음의 누적 오크 핫픽스에 포함되어 있습니다. 필요한 경우 최신 COFP 위에 진단 빌드를 제공할 수 있습니다. 고객의 요구 사항은 최신 COFP가 실행되고 있다는 것입니다. 진단 빌드는 핫픽스와 동일한 수준의 품질 보증만 제공합니다. 따라서 누적 수정 팩, 서비스 팩 또는 제품 릴리스와 동일한 수준의 품질 보증을 제공하지 않습니다. 최종 수정 사항은 다음 CFP와 함께 전달됩니다.

