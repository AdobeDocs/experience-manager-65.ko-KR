---
title: 프로세스 인스턴스 목록 사용자 정의
seo-title: 프로세스 인스턴스 목록 사용자 정의
description: AEM Forms 작업 공간의 프로세스 인스턴스에 표시되는 속성을 사용자 지정하는 방법
seo-description: AEM Forms 작업 공간의 프로세스 인스턴스에 표시되는 속성을 사용자 지정하는 방법
uuid: 3b55d9b9-7f73-46dd-9eb6-42be218440a1
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 40d7d43f-ee0a-4e34-ae93-20c9c940f76b
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 3%

---


# 프로세스 인스턴스 목록 사용자 정의 {#customizing-the-listing-of-process-instances}

프로세스 인스턴스 목록은 AEM Forms 작업 공간의 추적 탭에 표시됩니다.

프로세스 인스턴스 목록에서 각 프로세스 인스턴스에 대해 AEM Forms 작업 공간에 해당 인스턴스의 일부 속성이 표시됩니다. 각 프로세스 인스턴스에 다음 속성을 사용할 수 있습니다. 이러한 속성은 프로세스 인스턴스 구성 요소 모델에 속성으로 저장되며 해당 보기 및 템플릿에서 사용할 수 있습니다.

<table>
 <tbody>
  <tr>
   <td><strong>속성</strong></td>
   <td><strong>댓글</strong></td>
  </tr>
  <tr>
   <td>설명</td>
   <td>프로세스 인스턴스에 대한 설명입니다.</td>
  </tr>
  <tr>
   <td>이니시에이터</td>
   <td>프로세스 인스턴스의 초기자 이름입니다.</td>
  </tr>
  <tr>
   <td>initiatorId</td>
   <td>프로세스 인스턴스의 초기자 ID.</td>
  </tr>
  <tr>
   <td>processCompleteTime</td>
   <td>프로세스가 완료된 타임스탬프</td>
  </tr>
  <tr>
   <td>processInstanceId</td>
   <td>프로세스 인스턴스의 ID입니다.</td>
  </tr>
  <tr>
   <td>processInstanceStatus</td>
   <td>0 = 시작됨<br /> 1 = 실행<br /> 2 = 완료<br /> 3 = 종료<br /> 5 = 종료<br /> 6 = 종료<br /> 6 = 일시 중지됨<br /> 7 = 일시 중지됨<br /> 7 = 일시 중지됨 8 = 일시 중지되지 않음</td>
  </tr>
  <tr>
   <td>processName</td>
   <td>프로세스의 이름입니다.</td>
  </tr>
  <tr>
   <td>processStartTime</td>
   <td>프로세스가 시작될 때 타임스탬프</td>
  </tr>
  <tr>
   <td>processVariables</td>
   <td>프로세스 변수의 객체 배열. 각 프로세스 변수 객체에는 <strong>이름</strong> (프로세스 변수 이름), <strong>값</strong> (프로세스 변수 값) 및<strong> 유형</strong> (프로세스 변수 유형)이 포함됩니다.</td>
  </tr>
 </tbody>
</table>

**예:**

프로세스 인스턴스 카드에 프로세스 인스턴스의 `description` 속성을 표시하려면 다음 단계를 수행하십시오.

1. AEM Forms 작업 공간 사용자 [지정에 대한 일반 단계를 따릅니다](/help/forms/using/generic-steps-html-workspace-customization.md).
1. 다음을 수행합니다.

   1. /libs/ws/js/runtime/templates/processinstance.html이 없는 경우을 복사합니다. 모두 **저장을 클릭합니다**.
   1. 클래스 = &#39;processDescription&#39; inprocessinstance.html을 사용하여 프로세스 설명 div를 추가합니다.

   ```jsp
   <div class="processDescription" title="<%= description%>"><%= description%></div>
   ```

1. 다음을 수행합니다.

   1. /apps/ws/js/registry.js을 열어 편집할 수 있습니다.
   1. 검색 및 바꾸기 `text!/lc/libs/ws/js/runtime/templates/processinstance.html`는 /ws/js/runtime/templates/processinstance.html `text!/lc/`**앱으로&#x200B;**바꿉니다.

1. 위의 변경 사항은 다음 방법으로 /apps/ws/css/newStyle.css스타일 시트에서 항목을 추가하여 CSS 파일을 업데이트해야 할 수 있습니다.

   ```css
   .processinstance .processDescription {
    <!--Dummy values, need to be configured by user as per requirement as well as user can add or delete any property depending upon requirement-->
       width : 250px;
       font-size : 11pt;
       padding : 2px;
   }
   ```
