---
title: OSGi 및 AEM Forms JEE 워크플로우에서 양식 중심 AEM 워크플로우의 작업 및 기능
description: OSGi 및 AEM Forms JEE 워크플로우에서 양식 중심 AEM 워크플로우의 작업 및 기능
contentOwner: khsingh
exl-id: 505b8988-b2b3-4222-b3cb-9b3c6259fdd2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '928'
ht-degree: 22%

---

# OSGi 및 AEM Forms JEE 워크플로우에서 양식 중심 AEM 워크플로우의 작업 및 기능 {#actions-and-capabilities-of-form-centric-aem-workflows-on-osgi-and-aem-forms-jee-workflows}

## AEM 받은 편지함 및 HTML 작업 공간 {#aem-inbox-and-html-workspace}

AEM 받은 편지함을 사용하여 OSGi에서 Forms 중심의 AEM 워크플로우를 실행하고 모니터링할 수 있습니다. 반면 HTML 작업 공간에서는 AEM Forms JEE 워크플로우를 실행하고 모니터링할 수 있습니다. 다음 표는 OSGi의 Forms 중심 AEM 워크플로용 AEM 받은 편지함 및 AEM Forms JEE 워크플로용 HTML 작업 영역에서 사용할 수 있는 다양한 중요한 작업을 이해하는 데 도움이 됩니다.

<table>
 <tbody>
  <tr>
   <td>작업</td>
   <td>AEM 받은 편지함</td>
   <td>HTML 작업 영역</td>
  </tr>
  <tr>
   <td>프로세스, 작업 또는 양식 애플리케이션 시작<br /> </td>
   <td>지원됨<br /> </td>
   <td>지원됨<br /> </td>
  </tr>
  <tr>
   <td>작업 제출 중</td>
   <td>지원됨<br /> </td>
   <td>지원됨<br /> </td>
  </tr>
  <tr>
   <td>그룹에 작업 할당</td>
   <td>지원됨<br /> </td>
   <td>지원됨<br /> </td>
  </tr>
  <tr>
   <td>여러 경로에 제출 중</td>
   <td>지원됨<br /> </td>
   <td>지원됨<br /> </td>
  </tr>
  <tr>
   <td>작업 내역 및 작업 요약 추적</td>
   <td>지원됨<br /> </td>
   <td>지원됨<br /> </td>
  </tr>
  <tr>
   <td>이메일 알림</td>
   <td>지원됨<br /> </td>
   <td>지원됨<br /> </td>
  </tr>
  <tr>
   <td>작업 재할당</td>
   <td>지원됨</td>
   <td>지원됨</td>
  </tr>
  <tr>
   <td>적응형 양식용 필드 수준 첨부 파일</td>
   <td>지원됨</td>
   <td>지원되지 않음</td>
  </tr>
  <tr>
   <td>달력 보기</td>
   <td>지원됨</td>
   <td>지원되지 않음</td>
  </tr>
  <tr>
   <td>작업 수준 주석</td>
   <td>지원됨</td>
   <td>지원되지 않음</td>
  </tr>
  <tr>
   <td>대기열(공유 개인 대기열, 대기열에서 작업 청구)</td>
   <td>지원됨</td>
   <td>지원됨</td>
  </tr>
  <tr>
   <td>부재 중 알림</td>
   <td>지원됨</td>
   <td>지원됨</td>
  </tr>
    <tr>
   <td>UI 요소 맞춤화</td>
   <td>지원됨</td>
   <td>지원됨</td>
  </tr>
  <tr>
   <td>여러 사용자에게 작업 할당</td>
   <td>지원되지 않음</td>
   <td>지원됨</td>
  </tr>
 </tbody>
</table>

## OSGi 및 AEM Forms JEE 워크플로우의 양식 중심 AEM 워크플로우 {#form-centric-aem-workflows-on-osgi-and-aem-forms-jee-workflows}

OSGi의 양식 중심의 AEM 워크플로와 JEE의 AEM Forms JEE 워크플로(JEE의 AEM Forms 프로세스 관리)에는 다른 기능 세트가 있습니다. 다음 표는 OSGi의 양식 중심 AEM 워크플로 및 JEE의 AEM Forms 워크플로에서 사용할 수 있는 중요한 기능을 이해하는 데 도움이 됩니다.

<table>
 <tbody>
  <tr>
   <td>기능</td>
   <td>OSGi의 양식 중심의 AEM 워크플로<br /> </td>
   <td>AEM Forms JEE 워크플로</td>
  </tr>
  <tr>
   <td>적응형 양식</td>
   <td>지원됨</td>
   <td>지원됨<br />을 따르지 않는 경우입니다 </td>
  </tr>
  <tr>
   <td>다른 AEM 솔루션과 통합</td>
   <td>지원됨</td>
   <td>지원됨</td>
  </tr>
  <tr>
   <td>낙서 서명</td>
   <td>지원됨</td>
   <td>지원됨<br />을 따르지 않는 경우입니다 </td>
  </tr>
  <tr>
   <td>사용자 정의 이메일 템플릿</td>
   <td>지원됨</td>
   <td>지원됨<br />을 따르지 않는 경우입니다 </td>
  </tr>
  <tr>
   <td>작업 우선 순위 정의</td>
   <td>지원됨</td>
   <td>지원됨</td>
  </tr>
  <tr>
   <td>기한 이후 작업 시간 초과</td>
   <td>지원됨</td>
   <td>지원됨</td>
  </tr>
  <tr>
   <td>워크플로우 내 루프</td>
   <td>지원됨</td>
   <td>지원됨</td>
  </tr>
  <tr>
   <td>동적으로 담당자 선택 </td>
   <td>지원됨</td>
   <td>지원됨</td>
  </tr>
  <tr>
   <td>사용자 지정 메타데이터 사용</td>
   <td>지원됨</td>
   <td>지원됨</td>
  </tr>
  <tr>
   <td>전자 서명(Adobe Sign)</td>
   <td>지원됨 <sup>[1]</sup></td>
   <td>지원됨 <sup>[5]</sup></td>
  </tr>
  <tr>
   <td>작업 및 양식 애플리케이션 관리</td>
   <td>지원됨 <sup>[2]</sup><br /> </td>
   <td>지원됨 <sup>[2]</sup></td>
  </tr>
  <tr>
   <td>문서 서비스</td>
   <td>지원됨 <sup>[3]</sup></td>
   <td>지원됨 <sup>[3]</sup></td>
  </tr>
  <tr>
   <td>완료된 작업을 적응형 양식 또는 PDF 문서로 렌더링</td>
   <td>지원됨</td>
   <td>지원됨 [4]</td>
  </tr>
  <tr>
   <td>서신 관리와 통합</td>
   <td>지원됨</td>
   <td>지원됨</td>
  </tr>
   <tr>
   <td>게이트웨이 , 대기 없음 </td>
   <td>지원됨</td>
   <td>지원됨</td>
  </tr>
   <tr>
   <td>데이터를 저장할 변수 </td>
   <td>지원됨</td>
   <td>지원됨</td>
  </tr>
  <tr>
   <td>OR, AND 분할</td>
   <td>지원됨</td>
   <td>지원됨</td>
  </tr>
  <tr>
   <td>사용자 아바타</td>
   <td>지원됨</td>
   <td>지원됨</td>
  </tr>
  <tr>
   <td>워크플로우 끝에 이메일 보내기</td>
   <td>지원됨 <sup>[7]</sup></td>
   <td>지원됨</td>
  </tr>
  <tr>
   <td>워크플로우에서 웹 서비스 호출</td>
   <td>지원됨</td>
   <td>지원됨</td>
  </tr>
  <tr>
   <td>디지털 서명</td>
   <td>지원됨<br /> </td>
   <td>지원됨<br /> </td>
  </tr>
  <tr>
   <td>재설정 버튼</td>
   <td>지원됨</td>
   <td>지원되지 않음</td>
  </tr>
  <tr>
   <td>워크플로 단계</td>
   <td>지원됨</td>
   <td>지원되지 않음</td>
  </tr>
  <tr>
   <td>읽기 전용 적응형 양식</td>
   <td>지원됨</td>
   <td>지원되지 않음</td>
  </tr>
  <tr>
   <td>기본 저장 단추 숨기기</td>
   <td>지원됨</td>
   <td>지원되지 않음</td>
  </tr>
  <tr>
   <td>워크플로우 세부 정보 섹션에 대한 세분화된 제어</td>
   <td>지원됨</td>
   <td>지원되지 않음</td>
  </tr>
  <tr>
   <td>폴링/예약 서비스</td>
   <td>즉시 사용 가능</td>
   <td>사용자 정의 구현 필요</td>
  </tr>
  <tr>
   <td>적응형 Forms 앱</td>
   <td>지원됨</td>
   <td>지원됨</td>
  </tr>
  <tr>
   <td>어셈블러 서비스</td>
   <td>지원됨</td>
   <td>지원됨</td>
  </tr>
  <tr>
   <td>PDF 생성기 서비스</td>
   <td>지원됨</td>
   <td>지원됨</td>
  </tr>
  <tr>
   <td>Forms 서비스</td>
   <td>지원됨</td>
   <td>지원됨</td>
  </tr>
  <tr>
   <td>출력 서비스</td>
   <td>지원됨</td>
   <td>지원됨</td>
  </tr>
  <tr>
   <td>문서 보증</td>
   <td>지원됨</td>
   <td>지원됨 </td>
  </tr>
  <tr>
   <td>스크립트 실행</td>
   <td>ECMAScript 지원</td>
   <td>Java 코드 조각 지원</td>
  </tr>
  <tr>
   <td>어셈블러</td>
   <td>지원됨</td>
   <td>지원됨</td>
  </tr>  
  <tr>
   <td>HTML5 Forms, 대화형 PDF forms, 양식 세트</td>
   <td>지원되지 않음</td>
   <td>지원됨</td>
  </tr>
  <tr>
   <td>프로세스 보고</td>
   <td>지원되지 않음</td>
   <td>지원됨</td>
  </tr>
  <tr>
   <td>디지털 서명</td>
   <td>지원됨</td>
   <td>지원됨</td>
  </tr>
  <tr>
   <td>시작점 카테고리</td>
   <td>지원되지 않음 </td>
   <td>지원됨 </td>
  </tr>
  <tr>
   <td>일괄 작업 승인 </td>
   <td>지원되지 않음 </td>
   <td>지원됨 </td>
  </tr>
  <tr>
   <td>사용자 지정 이름으로 초안 저장</td>
   <td>지원되지 않음 </td>
   <td>지원됨 </td>
  </tr>
  <tr>
   <td>기존 프로세스 데이터로 프로세스 시작<br /> </td>
   <td>지원되지 않음</td>
   <td>지원됨 </td>
  </tr>
  <tr>
   <td>시작점을 초안으로 저장</td>
   <td>지원되지 않음</td>
   <td>지원됨</td>
  </tr>
  <tr>
   <td>관리자 보기</td>
   <td>지원되지 않음</td>
   <td>지원됨<br /> </td>
  </tr>
  <tr>
   <td>템플릿 검색</td>
   <td>지원되지 않음</td>
   <td>지원됨<br /> </td>
  </tr>
  <tr>
   <td>타사 애플리케이션과 통합</td>
   <td>지원되지 않음 <sup>[6]</sup></td>
   <td>지원됨</td>
  </tr>
  <tr>
   <td>워크플로 응용 프로그램 또는 시작 지점에 대한 작업 수준 첨부 파일</td>
   <td>지원되지 않음</td>
   <td>지원됨</td>
  </tr>
  <tr>
   <td>미리 알림 이메일</td>
   <td>지원되지 않음</td>
   <td>지원됨</td>
  </tr>
  <tr>
   <td>작업 시간 초과 시 제목 변경</td>
   <td>지원되지 않음</td>
   <td>지원됨</td>
  </tr>
  <tr>
   <td>작업 위임 및 작업 클레임에 대한 이메일</td>
   <td>지원되지 않음</td>
   <td>지원됨</td>
  </tr>
  <tr>
   <td>분리된 그룹 간 위임</td>
   <td>지원되지 않음</td>
   <td>지원됨</td>
  </tr>
  <tr>
   <td>XSLT 변환</td>
   <td>지원되지 않음</td>
   <td>지원됨</td>
  </tr>
  <tr>
   <td>동적 작업 우선 순위</td>
   <td>지원되지 않음</td>
   <td>지원되지 않음</td>
  </tr>
  <tr>
   <td>동적 제목</td>
   <td>지원되지 않음</td>
   <td>지원되지 않음</td>
  </tr>
    <tr>
   <td>동적 설명</td>
   <td>지원되지 않음</td>
   <td>지원되지 않음</td>
  </tr>
 </tbody>
</table>

1. OSGi에서 양식 중심의 AEM 워크플로 를 사용하여 채워진 적응형 양식에 서명할 수 있습니다. OSGi의 양식 중심 AEM 워크플로우는 양식 서명에서 지원합니다. 다음 [양식 내 서명](../../forms/using/working-with-adobe-sign.md#create-in-form-signing-experience) 경험이 지원되지 않습니다.

1. AEM Forms OSGi 및 HTML 작업 공간에서 양식 중심 워크플로우를 실행 및 모니터링하여 AEM Forms JEE 워크플로우를 실행 및 모니터링하려면 AEM 받은 편지함에 대한 액세스 권한이 필요합니다.
1. 기본 AEM Forms 문서 서비스는 OSGi의 양식 중심 AEM 워크플로와 JEE의 AEM Forms 워크플로 모두에서 사용할 수 있습니다. AEM Workflow는 OSGi 및 AEM Forms JEE(프로세스 관리) 워크플로우의 양식 중심의 AEM 워크플로에 기본 문서 서비스를 사용합니다.
1. AEM Forms JEE 워크플로우는 적응형 양식만 렌더링할 수 있습니다. 적응형 양식을 PDF 문서로 렌더링하는 것은 지원되지 않습니다.
1. AEM forms JEE 워크플로에는 Adobe Sign에 대한 별도의 단계가 없습니다. AEM Forms JEE 워크플로우에 대해 Adobe Sign이 활성화된 적응형 양식이 필요합니다. 자세한 내용은 [Adobe Sign 설명서](../../forms/using/working-with-adobe-sign.md#add-and-configure-the-signature-step-component).
1. 다음을 사용할 수 있습니다. [양식 데이터 모델 서비스 호출](../../forms/using/aem-forms-workflow-step-reference.md#p-invoke-form-data-model-service-step-p) 웹 서비스 서비스를 호출하고 서드파티 애플리케이션에서 데이터를 게시하거나 검색하는 단계입니다.
1. 다음을 사용할 수 있습니다. [이메일 보내기](../../forms/using/aem-forms-workflow-step-reference.md#send-email-step) 단계: 이메일을 전송합니다.

## AEM 받은 편지함 및 AEM Forms 앱 기능의 차이점 {#differences-between-aem-inbox-and-aem-forms-app-features}

Forms 중심 워크플로우를 시작하는 두 가지 두드러진 방법은 를 사용하는 것입니다 [AEM 받은 편지함](../../forms/using/manage-applications-inbox.md) 및 AEM Forms 앱. 그러나 AEM Inbox와 AEM Forms 앱의 기능은 다릅니다. AEM 받은 편지함은 [Forms 중심 워크플로](../../forms/using/aem-forms-workflow.md) 반면에 AEM Forms 앱은 Forms 중심 워크플로와 프로세스 관리 모두에서 작동합니다.

다음 표에는 AEM Inbox 및 AEM Forms 앱의 기능이 나와 있습니다.

<table>
 <tbody>
  <tr>
   <td><p><strong>작업</strong></p> </td>
   <td><p><strong>AEM 받은 편지함</strong></p> </td>
   <td><p><strong>AEM Forms 앱</strong></p> </td>
  </tr>
  <tr>
   <td><p>양식 애플리케이션 시작</p> </td>
   <td><p>지원됨</p> </td>
   <td><p>지원됨</p> </td>
  </tr>
  <tr>
   <td><p>작업 제출 중</p> </td>
   <td><p>지원됨</p> </td>
   <td><p>지원됨</p> </td>
  </tr>
  <tr>
   <td><p>작업 위임</p> </td>
   <td><p>지원됨</p> </td>
   <td><p>지원되지 않음</p> </td>
  </tr>
  <tr>
   <td><p>작업 내역 및 작업 요약 추적</p> </td>
   <td><p>지원됨</p> </td>
   <td><p>지원되지 않음</p> </td>
  </tr>
  <tr>
   <td><p>작업 수준 첨부 파일 추가</p> </td>
   <td><p>지원됨</p> </td>
   <td><p>지원됨</p> </td>
  </tr>
  <tr>
   <td><p>작업 레벨 첨부 조회</p> </td>
   <td><p>지원됨</p> </td>
   <td><p>지원됨</p> </td>
  </tr>
  <tr>
   <td><p>필드 수준 첨부 추가</p> </td>
   <td><p>지원됨</p> </td>
   <td><p>지원됨</p> </td>
  </tr>
  <tr>
   <td><p>달력 보기 표시</p> </td>
   <td><p>지원됨</p> </td>
   <td><p>지원되지 않음</p> </td>
  </tr>
  <tr>
   <td><p>주석 추가</p> </td>
   <td><p>지원됨</p> </td>
   <td><p>지원됨</p> </td>
  </tr>
 </tbody>
</table>
