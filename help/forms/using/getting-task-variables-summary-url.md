---
title: 요약 URL에서 작업 변수 가져오기
seo-title: 요약 URL에서 작업 변수 가져오기
description: 작업에 대한 정보를 재사용하고 요약 URL을 생성하여 작업을 요약하거나 설명하는 방법
seo-description: 작업에 대한 정보를 재사용하고 요약 URL을 생성하여 작업을 요약하거나 설명하는 방법
uuid: 9eab3a6a-a99a-40ae-b483-33ec7d21c5b6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 6dc31bec-b02d-47db-a4f4-be8c14c5619e
translation-type: tm+mt
source-git-commit: f9389a06f9c2cd720919486765cee76257f272c3

---


# 요약 URL에서 작업 변수 가져오기 {#getting-task-variables-in-summary-url}

요약 페이지에는 작업 관련 정보가 표시됩니다. 이 문서에서는 요약 페이지에서 작업 관련 정보를 재사용하는 방법에 대해 설명합니다.

이 샘플 오케스트레이션에서 직원이 휴가 신청 양식을 제출합니다. 그러면 신청서는 직원의 관리자에게 승인을 요청합니다.

1. 리소스 유형 직원/PtoApplication에 대한 샘플 HTML 렌더러(html.esp) **를 만듭니다**.

   렌더러는 다음 속성이 노드에 설정된다고 가정합니다.

   * 이름
   * empid
   * 이유
   * 지속 시간
   >[!NOTE]
   >
   >이 렌더러는 요약 페이지 템플릿입니다.

   이 렌더러의 다음 샘플 코드는 에 포함되어 있습니다.

   `apps/Employees/PtoApplication/html.esp`

   ```
   <html>
     <body>
       <table>
       <tbody>
       <tr>
           <td>
               <h3>Employee Name: <%= currentNode.ename %></h3>
               <h3>Employee ID: <%= currentNode.eid %></h3>
               <h3>Leave duration: <%= currentNode.duration %> days</h3>
               <h3>Reason: <%= currentNode.reason %></h3>
           </td>
       </tr>
       </tbody>
       </table>
     </body>
   </html>
   ```

1. 제출된 양식 데이터에서 네 개의 속성을 추출하도록 오케스트레이션을 수정합니다. 그런 다음 Employees/PtoApplication 유형의 CRX에 **속성이**&#x200B;채워진 노드를 생성합니다.

   1. PTO 요약을 **생성하는 프로세스를 생성하고 이** 요약을 **하위 프로세스로** 사용하여운영 체제에서 태스크지정 작업을수행합니다.
   1. 사원 **이름**, **employee** ID **,**&#x200B;유급휴가 **사유**, **총 일수,** 총 일수, Person 및 nodeName새 프로세스에서 입력 변수로 정의합니다. 이러한 변수는 제출된 양식 데이터로 전달됩니다.

      또한 요약 URL **을** 설정하는 동안 사용할 출력 변수를 정의합니다.

   1. PTO 요약 ******생성 프로세스에서** 세트 값 **구성 요소를 사용하여 nodeProperty**(nodePropsProp **) 맵의 입력 상세내역을**&#x200B;설정합니다.

      이 맵의 키는 이전 단계에서 HTML 렌더러에 정의된 키와 같아야 합니다.

      또한 맵에 **사원/PtoApplication 값이** 있는 sling:resourceType **키를** 추가합니다.

   1. PTO 요약 **생성** **프로세스의 ContentRepositoryConnector** **서비스의 하위 프로세스** storeContent를사용합니다. 이 하위 프로세스는 CRX 노드를 만듭니다.

      세 가지 입력 변수가 필요합니다.

      * **폴더 경로**:새 CRX 노드가 생성되는 경로입니다. 경로를 **/content**&#x200B;로 설정합니다.
      * **노드 이름**:이 필드에 입력 변수 nodeName을 지정합니다. 이것은 고유한 노드 이름 문자열입니다.
      * **노드 유형**:유형을 **nt:unstructured**&#x200B;형식으로 정의합니다. 이 프로세스의 출력은 nodePath입니다. nodePath는 새로 만든 노드의 CRX 경로입니다. ndoePath는 PTO **생성 요약 프로세스의 최종** 출력입니다.
   1. 제출된 양식 데이터(**employeeName**, **employee** ID **,**&#x200B;유급휴가 **사유**&#x200B;및 총 **일수)를 새 프로세스에 입력으로 전달합니다**.PTO 요약 생성을 참조하십시오. 출력을 ptoSummaryNodePath로 **가져옵니다**.


1. 요약 URL을 ptoSummaryNodePath와 함께 서버 상세내역을 포함하는 XPath 표현식으로 **정의합니다**.

   XPath: `concat('https://[*server*]:[*port*]/lc',/process_data/@ptoSummaryNodePath,'.html')`.

AEM Forms 작업 영역에서 작업을 열면 요약 Url이 CRX 노드에 액세스하고 HTML 렌더러가 요약을 표시합니다.

요약 레이아웃은 프로세스를 수정하지 않고 변경할 수 있습니다. HTML 렌더러는 요약을 적절히 표시합니다.
