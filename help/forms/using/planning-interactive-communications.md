---
title: "자습서: 대화형 통신 계획"
seo-title: Plan your Interactive Communication
description: 인터랙티브 통신을 위한 해부학적 계획
seo-description: Plan the anatomy for your Interactive Communication
uuid: 1c2b5c5b-c655-4559-8748-3e0b343779c2
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 75b2d424-91d3-45b4-a5d7-fb49ab558582
feature: Interactive Communication
exl-id: ea0c8971-56f4-4094-87e4-1b222b73951f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 3%

---

# 자습서: 대화형 통신 계획 {#tutorial-plan-the-interactive-communication}

인터랙티브 통신을 위한 해부학적 계획

![02-create-adaptive-form-main-image](assets/02-create-adaptive-form-main-image.png)

이 자습서는 [첫 번째 대화형 통신 만들기](/help/forms/using/create-your-first-interactive-communication.md) 시리즈. 전체 자습서 사용 사례를 이해하고, 수행하고, 시연하기 위해 시리즈를 시간 순서대로 따르는 것이 좋습니다.

대화형 커뮤니케이션을 계획하는 첫 번째 단계는 대화형 커뮤니케이션의 콘텐츠를 완료하는 것입니다. 법률, 재무, 지원 또는 마케팅과 같은 부서의 주제 전문가들은 컨텐츠를 완료하는 데 도움이 될 수 있습니다. 컨텐츠가 완료되면 이를 분석하여 대화형 커뮤니케이션을 만드는 데 필요한 다양한 자산 유형을 식별해야 합니다.

## 계획 고려 사항 {#planning-considerations}

대화형 커뮤니케이션에는 다음 요소가 포함됩니다.

* **정적 텍스트** 대부분 본질적으로 일반적인 대화형 커뮤니케이션의 일부이며 모든 고객과의 통신에 포함됩니다. 예를 들어 머리글, 바닥글, 인사말 또는 면책조항이 있습니다.
* **백엔드 시스템에서 가져온 데이터(양식 데이터 모델)** 은 고객별로 다르며 대화형 커뮤니케이션과 동적으로 병합됩니다. 예를 들어 양식 데이터 모델을 사용하여 정책 번호 또는 주소를 소싱할 수 있습니다.
* **레이아웃 또는 템플릿** Interactive Communication의 인쇄 및 웹 버전에 대해 설명합니다.
* **주문** 인터랙티브 통신에 다양한 텍스트 단락이 표시되는 위치입니다.
* **최전방 직원이 입력한 데이터(에이전트 UI)** 은(는) 메시지를 보내기 전에 사용자 지정하는 것입니다. 예를 들어 지급 만기 일자입니다.

* **조건부 데이터** 은 사전 정의된 조건을 기반으로 채워집니다. 예를 들어 대화형 통신이 생성되는 날짜입니다.
* **저장소에 저장된 이미지**&#x200B;로고 및 서명 이미지 등 회사 로고와 같은 이미지는 대부분의 또는 모든 대화형 커뮤니케이션에 나타납니다.
* **차트 및 표** 대화형 커뮤니케이션에서 복잡한 데이터의 표현을 단순화하는 데 필요합니다.

## 인터랙티브 통신의 해부 {#anatomy-of-the-interactive-communication}

대화형 커뮤니케이션을 만드는 데 사용되는 컨텐츠 및 요소를 완성하면 대화형 커뮤니케이션의 해부를 만들 수 있습니다. 해부학에는 자세한 내용이 기재되어 있어야 한다 [계획 고려 사항](/help/forms/using/planning-interactive-communications.md#planning-considerations) 섹션을 참조하십시오. 사용 사례를 토대로, 다음은 통신 사업자가 고객에게 보내는 월별 청구서 해부의 예입니다.

해부학은 다음과 같은 입력 모드를 가진 데이터를 포함한다.

* 정적 텍스트
* 양식 데이터 모델
* 에이전트 UI
* 조건부 데이터
* 이미지

각 섹션에서 굵게 표시된 텍스트는 정적 텍스트를 나타냅니다. 데이터베이스에는 고객, 청구서 및 호출 테이블이 포함됩니다. 양식 데이터 모델은 이러한 테이블에서 데이터를 받을 수 있습니다. 자세한 내용은 [양식 데이터 모델 만들기](/help/forms/using/create-form-data-model0.md).

다음 표에서는 Interactive Communication 해부의 각 필드에 대한 데이터 소스를 보여 줍니다.

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
   <td>청구 상세내역</td>
   <td><p>송장 번호</p> <p>청구서 날짜</p> <p>청구 기간</p> <p>플랜</p> </td>
   <td><p>값 <strong>플랜 </strong>필드</p> <p>테이블 - 고객</p> </td>
   <td><p>다음 필드의 값:</p>
    <ul>
     <li>송장 번호</li>
     <li>청구서 날짜</li>
     <li>청구 기간</li>
    </ul> <p> </p> </td>
   <td>—</td>
  </tr>
  <tr>
   <td>고객 세부 사항</td>
   <td><p>공급 장소</p> <p>상태 코드</p> <p>모바일 번호</p> <p>대체 연락처 번호</p> <p>관계 번호</p> <p>연결 수</p> </td>
   <td><p>다음 필드의 값:</p>
    <ul>
     <li>이름</li>
     <li>주소</li>
     <li>모바일 번호</li>
     <li>대체 연락처 번호</li>
     <li>관계 번호</li>
    </ul> <p>테이블 - 고객</p> </td>
   <td><p>다음 필드의 값:</p>
    <ul>
     <li>공급 장소</li>
     <li>상태 코드</li>
     <li>연결 수</li>
    </ul> </td>
   <td>—</td>
  </tr>
  <tr>
   <td>청구서 요약</td>
   <td><p>이전 잔액</p> <p>결제</p> <p>조정</p> <p>현재 청구 기간</p> <p>만기 금액</p> <p>기한</p> </td>
   <td><p>값 <strong>현재 청구 기간 </strong> 필드</p> <p>테이블 - 청구서</p> </td>
   <td><p>다음 필드의 값:</p>
    <ul>
     <li>이전 잔액</li>
     <li>결제</li>
     <li>조정</li>
     <li>만기 금액</li>
     <li>기한</li>
    </ul> </td>
   <td>—</td>
  </tr>
  <tr>
   <td>비용 요약</td>
   <td><p>전화 요금</p> <p>전화 회의 요금</p> <p>SMS 요금 </p> <p>모바일 인터넷 요금</p> <p>국가 로밍 요금</p> <p>국제 로밍 요금</p> <p>부가 서비스 요금</p> <p>총 요금</p> <p>AP 총액</p> <p>부가 서비스 요금 필드에 대한 조건</p> </td>
   <td><p>다음 필드의 값:</p>
    <ul>
     <li>전화 요금</li>
     <li>전화 회의 요금</li>
     <li>SMS 요금 </li>
     <li>모바일 인터넷 요금</li>
     <li>국가 로밍 요금</li>
     <li>국제 로밍 요금</li>
     <li>부가 서비스 요금</li>
     <li>총 비용(usagecharges 계산 필드)</li>
     <li>AP 합계(usagecharges 계산 필드)</li>
    </ul> <p>테이블 - 청구서</p> </td>
   <td>필드 없음</td>
   <td>—</td>
  </tr>
  <tr>
   <td>항목별 호출 - 발신</td>
   <td><p>열 이름:</p>
    <ul>
     <li>날짜</li>
     <li>시간</li>
     <li>숫자</li>
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
   <td>지금 지불</td>
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
