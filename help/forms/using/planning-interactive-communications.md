---
title: "자습서: 대화형 통신 계획"
seo-title: Plan your Interactive Communication
description: 대화형 커뮤니케이션에 대한 구조 계획
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

대화형 커뮤니케이션에 대한 구조 계획

![02-create-adaptive-form-main-image](assets/02-create-adaptive-form-main-image.png)

이 튜토리얼의 단계는 다음과 같습니다. [첫 번째 대화형 통신 만들기](/help/forms/using/create-your-first-interactive-communication.md) 시리즈. 전체 자습서 사용 사례를 이해하고, 수행하고, 시연하려면 연대순으로 시리즈를 따르는 것이 좋습니다.

대화형 통신을 계획하는 첫 번째 단계는 대화형 통신의 내용을 완료하는 것입니다. 법률, 재무, 지원 또는 마케팅 등의 부서의 주제 전문가가 콘텐츠 최종 작성에 도움을 줄 수 있습니다. 콘텐츠가 완료되면 이를 분석하여 대화형 커뮤니케이션을 만드는 데 필요한 다양한 에셋 유형을 식별해야 합니다.

## 계획 고려 사항 {#planning-considerations}

대화형 통신에는 다음 요소가 포함됩니다.

* **정적 텍스트** 대부분은 기본적으로 포괄적이며 모든 고객과의 통신에 포함된 대화형 통신의 일부를 포함합니다. 예: 머리글, 바닥글, 인사말 또는 면책조항.
* **백엔드 시스템에서 가져온 데이터(양식 데이터 모델)** 는 고객별로 고유하며 대화형 통신과 동적으로 병합됩니다. 예를 들어 양식 데이터 모델을 사용하여 정책 번호 또는 주소를 가져올 수 있습니다.
* **레이아웃 또는 템플릿** (Interactive Communication의 인쇄 및 웹 버전)
* **주문** Interactive Communication에서 다양한 텍스트 단락이 나타나는 위치.
* **일선 직원이 입력한 데이터(에이전트 UI)** 메시지를 보내기 전에 커뮤니케이션을 사용자 지정하는 사람입니다. 예: 결제 기한.

* **조건부 데이터** 사전 정의된 조건을 기반으로 채워집니다. 예를 들어 대화형 통신이 생성된 날짜입니다.
* **저장소에 저장된 이미지**&#x200B;로고 및 서명 이미지와 같은 을 포함합니다. 기업 로고와 같은 이미지는 대화형 통신의 대부분 또는 전체에 나타납니다.
* **차트 및 표** 대화형 통신에서 복잡한 데이터의 표현을 단순화하는 데 필요합니다.

## 대화형 통신의 해부학 {#anatomy-of-the-interactive-communication}

대화형 통신을 만드는 데 사용되는 콘텐츠 및 요소를 완료하면 대화형 통신의 구조를 만들 수 있습니다. 해부에는 다음 목록에 나열된 세부 정보가 있어야 합니다. [계획 고려 사항](/help/forms/using/planning-interactive-communications.md#planning-considerations) 섹션. 당사의 사용 사례를 토대로, 통신사가 고객에게 보내는 월별 청구서의 해부학적 구조를 예시하면 다음과 같습니다.

해부학에는 다음과 같은 입력 모드가 있는 데이터가 포함됩니다.

* 정적 텍스트
* 양식 데이터 모델
* 에이전트 UI
* 조건부 데이터
* 이미지

각 섹션에서 굵은 글꼴의 텍스트는 정적 텍스트를 나타냅니다. 데이터베이스에는 고객, 청구서 및 호출 테이블이 포함됩니다. 양식 데이터 모델은 이러한 테이블 중 하나에서 데이터를 받을 수 있습니다. 자세한 내용은 [양식 데이터 모델 만들기](/help/forms/using/create-form-data-model0.md).

다음 표는 대화형 통신 구조의 각 필드에 대한 데이터 소스를 보여 줍니다.

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
   <td>청구 세부 정보</td>
   <td><p>송장 번호</p> <p>청구 일자</p> <p>청구 기간</p> <p>내 플랜</p> </td>
   <td><p>값 <strong>내 플랜 </strong>필드</p> <p>표 - 고객</p> </td>
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
   <td>--</td>
  </tr>
  <tr>
   <td>청구 요약</td>
   <td><p>이전 잔액</p> <p>결제</p> <p>조정</p> <p>현재 청구 기간 청구</p> <p>미수금</p> <p>기한</p> </td>
   <td><p>값: <strong>현재 청구 기간 청구 </strong> 필드</p> <p>테이블 - 청구서</p> </td>
   <td><p>다음 필드의 값:</p>
    <ul>
     <li>이전 잔액</li>
     <li>결제</li>
     <li>조정</li>
     <li>미수금</li>
     <li>기한</li>
    </ul> </td>
   <td>--</td>
  </tr>
  <tr>
   <td>청구 요약</td>
   <td><p>통화 요금</p> <p>전화 회의 비용</p> <p>SMS 요금 </p> <p>모바일 인터넷 요금</p> <p>국가 로밍 요금</p> <p>국제 로밍 요금</p> <p>부가 서비스 요금</p> <p>총 청구 요금</p> <p>총 지불 금액</p> <p>부가 서비스 비용 필드의 조건</p> </td>
   <td><p>다음 필드의 값:</p>
    <ul>
     <li>통화 요금</li>
     <li>전화 회의 비용</li>
     <li>SMS 요금 </li>
     <li>모바일 인터넷 요금</li>
     <li>국가 로밍 요금</li>
     <li>국제 로밍 요금</li>
     <li>부가 서비스 요금</li>
     <li>총 요금(usagecharges 계산 필드)</li>
     <li>총 AP(usagecharges 계산 필드)</li>
    </ul> <p>테이블 - 청구서</p> </td>
   <td>필드 없음</td>
   <td>--</td>
  </tr>
  <tr>
   <td>항목별 통화 - 발신</td>
   <td><p>열 이름:</p>
    <ul>
     <li>날짜</li>
     <li>시간</li>
     <li>숫자</li>
     <li>기간</li>
     <li>청구</li>
    </ul> </td>
   <td><p>모든 값</p> <p>테이블 - 호출</p> </td>
   <td>필드 없음</td>
   <td>--</td>
  </tr>
  <tr>
   <td>지금 결제</td>
   <td>--</td>
   <td>--</td>
   <td>--</td>
   <td>PayNow</td>
  </tr>
  <tr>
   <td>부가 가치 서비스</td>
   <td>--</td>
   <td>--</td>
   <td>--</td>
   <td>ValueAddedServices</td>
  </tr>
 </tbody>
</table>
