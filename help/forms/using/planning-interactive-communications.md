---
title: '"자습서:인터랙티브 커뮤니케이션 계획"'
seo-title: 인터랙티브 커뮤니케이션 계획
description: 인터랙티브 커뮤니케이션을 위한 구조 계획
seo-description: 인터랙티브 커뮤니케이션을 위한 구조 계획
uuid: 1c2b5c5b-c655-4559-8748-3e0b343779c2
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 75b2d424-91d3-45b4-a5d7-fb49ab558582
feature: 대화형 통신
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '667'
ht-degree: 3%

---


# 자습서:대화형 통신 계획 {#tutorial-plan-the-interactive-communication}

인터랙티브 커뮤니케이션을 위한 구조 계획

![02-create-adaptive-form-main-image](assets/02-create-adaptive-form-main-image.png)

이 자습서는 [첫 번째 대화형 통신 만들기](/help/forms/using/create-your-first-interactive-communication.md) 시리즈의 한 단계입니다. 전체 자습서 사용 사례를 이해하고, 실행하고, 시연하기 위해 시리즈를 시간순으로 따르는 것이 좋습니다.

대화형 통신을 계획하는 첫 번째 단계는 대화형 커뮤니케이션의 내용을 마무리하는 것입니다. 법률, 재무, 지원 또는 마케팅과 같은 부서의 주제 전문가가 컨텐츠를 마무리하는 데 도움이 될 수 있습니다. 컨텐츠가 완료되면 분석을 통해 인터랙티브 커뮤니케이션을 만드는 데 필요한 다양한 자산 유형을 식별해야 합니다.

## 계획 고려 사항 {#planning-considerations}

대화형 통신에는 다음 요소가 포함됩니다.

* **정적** 텍스트에는 일반적으로 모든 고객과의 커뮤니케이션에 포함되어 있는 인터랙티브한 커뮤니케이션의 일부가 포함되어 있습니다. 예를 들어 머리글, 바닥글, 인사말 또는 면책 사항이 있습니다.
* **백엔드 시스템(양식 데이터 모델)에서 가져온 데이터** 는 고객별로 다르며 인터랙티브한 커뮤니케이션과 동적으로 통합됩니다. 예를 들어 양식 데이터 모델을 사용하여 정책 번호 또는 주소를 소싱할 수 있습니다.
* **인터랙티브** 커뮤니케이션의 인쇄 및 웹 버전에 대한 레이아웃 또는 템플릿입니다.
* **대화형** 통신에 다양한 텍스트 단락이 표시되는 순서.
* **커뮤니케이션을 전송하기 전에 사용자 지정하고** 있는 최전선 직원(에이전트 UI)이 입력한 데이터 예: 지불 기한.

* **사전** 정의된 조건을 기반으로 채워지는 조건부 데이터입니다. 예를 들어 대화형 통신이 생성되는 날짜입니다.
* **로고 및 서명 이미지** 등 저장소에 저장된 이미지. 기업 로고와 같은 이미지는 인터랙티브한 커뮤니케이션의 대부분 또는 모든 부분에 표시됩니다.
* **인터랙티브** 커뮤니케이션에서 복잡한 데이터의 표현을 간소화하는 데 필요한 차트 및 표

## 대화형 통신 구조 {#anatomy-of-the-interactive-communication}

인터랙티브 커뮤니케이션을 제작하는 데 사용되는 컨텐츠와 요소를 완료하면 인터랙티브 커뮤니케이션의 구조를 만들 수 있습니다. 해부학은 [계획 고려 사항](/help/forms/using/planning-interactive-communications.md#planning-considerations) 섹션에 나열된 세부 사항을 가지고 있어야 합니다. 우리의 사용 사례에 근거하여, 다음은 통신 사업자가 고객에게 보내는 월간 계산서의 해부의 한 예입니다.

해부학은 다음과 같은 입력 모드를 가진 데이터를 포함한다.

* 정적 텍스트
* 양식 데이터 모델
* 에이전트 UI
* 조건부 데이터
* 이미지

각 섹션에서 굵게 표시된 텍스트는 정적 텍스트를 나타냅니다. 데이터베이스에는 고객, 청구서 및 호출 테이블이 포함되어 있습니다. 양식 데이터 모델은 이러한 표에서 데이터를 받을 수 있습니다. 자세한 내용은 [양식 데이터 모델 만들기](/help/forms/using/create-form-data-model0.md)를 참조하십시오.

다음 표는 대화형 통신 구조에 있는 각 필드에 대한 데이터 소스를 보여 줍니다.

<table>
 <tbody>
  <tr>
   <td>섹션</td>
   <td>정적 텍스트</td>
   <td>FDM </td>
   <td>에이전트 UI</td>
   <td>이미지</td>
  </tr>
  <tr>
   <td>청구서 세부 사항</td>
   <td><p>송장 번호</p> <p>청구 일자</p> <p>청구 기간</p> <p>플랜</p> </td>
   <td><p><strong>계획 </strong>필드에 대한 값</p> <p>표 - 고객</p> </td>
   <td><p>다음 필드의 값:</p>
    <ul>
     <li>송장 번호</li>
     <li>청구 일자</li>
     <li>청구 기간</li>
    </ul> <p> </p> </td>
   <td>—</td>
  </tr>
  <tr>
   <td>고객 세부 정보</td>
   <td><p>공급 장소</p> <p>상태 코드</p> <p>모바일 번호</p> <p>대체 연락처 번호</p> <p>관계 번호</p> <p>연결 수</p> </td>
   <td><p>다음 필드의 값:</p>
    <ul>
     <li>이름</li>
     <li>주소</li>
     <li>모바일 번호</li>
     <li>대체 연락처 번호</li>
     <li>관계 번호</li>
    </ul> <p>표 - 고객</p> </td>
   <td><p>다음 필드의 값:</p>
    <ul>
     <li>공급 장소</li>
     <li>상태 코드</li>
     <li>연결 수</li>
    </ul> </td>
   <td>—</td>
  </tr>
  <tr>
   <td>청구 요약</td>
   <td><p>이전 잔액</p> <p>결제</p> <p>조정</p> <p>현재 청구 기간</p> <p>지불 금액</p> <p>기한</p> </td>
   <td><p><strong>현재 청구 기간 </strong> 필드에 대한 값</p> <p>표 - 청구서</p> </td>
   <td><p>다음 필드의 값:</p>
    <ul>
     <li>이전 잔액</li>
     <li>결제</li>
     <li>조정</li>
     <li>지불 금액</li>
     <li>기한</li>
    </ul> </td>
   <td>—</td>
  </tr>
  <tr>
   <td>비용 요약</td>
   <td><p>전화 요금</p> <p>전화 회의 비용</p> <p>SMS 요금 </p> <p>모바일 인터넷 요금</p> <p>국가 로밍 요금</p> <p>국제 로밍 요금</p> <p>부가가치 서비스 비용</p> <p>총 비용</p> <p>총 지급 수</p> <p>부가가치 서비스 비용 필드에 대한 조건</p> </td>
   <td><p>다음 필드의 값:</p>
    <ul>
     <li>전화 요금</li>
     <li>전화 회의 비용</li>
     <li>SMS 요금 </li>
     <li>모바일 인터넷 요금</li>
     <li>국가 로밍 요금</li>
     <li>국제 로밍 요금</li>
     <li>부가가치 서비스 비용</li>
     <li>총 비용(사용 수수료 계산 필드)</li>
     <li>TOTAL PAYABLE(Usagecharges 계산 필드)</li>
    </ul> <p>표 - 청구서</p> </td>
   <td>필드 없음</td>
   <td>—</td>
  </tr>
  <tr>
   <td>항목별 호출 - 발신</td>
   <td><p>열 이름:</p>
    <ul>
     <li>날짜</li>
     <li>시간</li>
     <li>번호</li>
     <li>기간</li>
     <li>요금</li>
    </ul> </td>
   <td><p>모든 값</p> <p>테이블 - 호출</p> </td>
   <td>필드 없음</td>
   <td>—</td>
  </tr>
  <tr>
   <td>지금 지불</td>
   <td>—</td>
   <td>—</td>
   <td>—</td>
   <td>PayNow</td>
  </tr>
  <tr>
   <td>부가 가치 서비스</td>
   <td>—</td>
   <td>—</td>
   <td>—</td>
   <td>ValueAddedServices</td>
  </tr>
 </tbody>
</table>

