---
title: 요약 URL에서 작업 변수를 가져오는 중
description: 작업 정보를 재사용하고 요약 URL을 생성하여 작업을 요약하거나 설명하는 방법.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: b5e27b54-d141-48dd-a4ed-dd0a691319a5
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 0%

---

# 요약 URL에서 작업 변수를 가져오는 중 {#getting-task-variables-in-summary-url}

요약 페이지에는 작업 관련 정보가 표시됩니다. 이 문서에서는 요약 페이지에서 작업 관련 정보를 재사용하는 방법에 대해 설명합니다.

이 샘플 오케스트레이션에서는 직원이 휴가 신청 양식을 제출합니다. 그러면 지원서는 승인을 위해 직원의 관리자에게 제출됩니다.

1. resourseType용 샘플 HTML 렌더러(html.esp) 만들기 **직원/PtoApplication**.

   렌더러는 노드에 설정할 다음 속성을 가정합니다.

   * 이름
   * empid
   * 이유
   * 지속 시간

   >[!NOTE]
   >
   >이 렌더러는 요약 페이지 템플릿입니다.

   이 렌더러에 대한 다음 샘플 코드가에 포함되어 있습니다.

   `apps/Employees/PtoApplication/html.esp`

   ```html
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

1. 오케스트레이션을 수정하여 제출된 양식 데이터에서 4가지 속성을 추출합니다. 이 작업 후 유형의 CRX에 노드 만들기 **직원/PtoApplication**, 속성 채워짐

   1. 프로세스 만들기 **PTO 요약 생성** 및 를 다음 앞에 하위 프로세스로 사용: **작업 할당** 오케스트레이션에서 작업합니다.
   1. 정의 **employeeName**, **직원 ID**, **ptoReason**, **totalDays**, 및 **nodeName** 를 새 프로세스의 입력 변수로 사용합니다. 이러한 변수는 제출된 양식 데이터로 전달됩니다.

      출력 변수 정의 **ptoNodePath** 요약 URL 설정 시 사용됩니다.

   1. 다음에서 **PTO 요약 생성** 프로세스, 사용 **값 설정** 에서 입력 세부 사항을 설정할 구성 요소 **nodeProperty**(**nodeProps**) 맵.

      이 맵의 키는 이전 단계에서 HTML 렌더러에 정의된 키와 동일해야 합니다.

      또한 **sling:resourceType** 값이 있는 키 **직원/PtoApplication** 지도에서.

   1. 하위 프로세스 사용 **storeContent** 다음에서 **ContentRepositoryConnector** 의 서비스 **PTO 요약 생성** 프로세스. 이 하위 프로세스는 CRX 노드를 만듭니다.

      세 개의 입력 변수가 필요합니다.

      * **폴더 경로**: 새 CRX 노드가 생성되는 경로입니다. 경로를 다음으로 설정 **/content**.
      * **노드 이름**: 이 필드에 입력 변수 nodeName을 할당합니다. 고유한 노드 이름 문자열입니다.
      * **노드 유형**: 유형을 다음과 같이 정의합니다. **nt:unstructured**. 이 프로세스의 출력은 nodePath입니다. nodePath는 새로 만든 노드의 CRX 경로입니다. NodePath는 **pto 생성** 요약 프로세스.

   1. 제출된 양식 데이터 전달(**employeeName**, **직원 ID**, **ptoReason**, 및 **totalDays**)를 새 프로세스에 대한 입력으로 **PTO 요약 생성**. 출력을 다음으로 가져오기 **ptoSummaryNodePath**.

1. 요약 URL을 과 함께 서버 세부 사항이 포함된 XPath 표현식으로 정의합니다. **ptoSummaryNodePath**.

   XPath: `concat('https://[*server*]:[*port*]/lc',/process_data/@ptoSummaryNodePath,'.html')`.

AEM Forms 작업 영역에서 작업을 열면 요약 URL이 CRX 노드에 액세스하고 HTML 렌더러가 요약을 표시합니다.

요약 레이아웃은 프로세스를 수정하지 않고 변경할 수 있습니다. HTML 렌더러는 요약을 적절히 표시합니다.
