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
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 0%

---


# 요약 URL {#getting-task-variables-in-summary-url}에 작업 변수 가져오기

요약 페이지에는 작업 관련 정보가 표시됩니다. 이 문서에서는 요약 페이지에서 작업 관련 정보를 재사용하는 방법에 대해 설명합니다.

이 샘플 오케스트레이션에서 직원은 휴가 신청서 양식을 제출합니다. 그러면 신청서는 승인을 위해 직원 관리자에게 보내진다.

1. recourseType **Employees/PtoApplication**&#x200B;에 대한 샘플 HTML 렌더러(html.esp)를 만듭니다.

   렌더러는 노드에서 설정할 다음 속성을 가정합니다.

   * 이름
   * empid
   * 이유
   * 지속 시간

   >[!NOTE]
   >
   >이 렌더러는 요약 페이지 템플릿입니다.

   이 렌더러의 다음 샘플 코드가 포함되어 있습니다.

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

1. 제출된 양식 데이터에서 4개의 속성을 추출하려면 오케스트레이션을 수정합니다. 이렇게 하면 **Employees/PtoApplication** 유형의 CRX에 속성이 채워진 노드를 만듭니다.

   1. **PTO 요약 생성** 프로세스를 만들고 이 프로세스를 오케스트레이션에서 **작업 지정** 작업 전에 하위 프로세스로 사용하십시오.
   1. 새 프로세스에서 **employeeName**, **employeeID**, **ptoReason**, **totalDays** 및 **nodeName**&#x200B;을 입력 변수로 정의합니다. 이러한 변수는 제출된 양식 데이터로 전달됩니다.

      요약 URL을 설정하는 동안 사용할 출력 변수 **ptoNodePath**&#x200B;도 정의합니다.

   1. **PTO 요약 생성** 프로세스에서 **set 값** 구성 요소를 사용하여 **nodeProperty**(**nodeProp**) 맵에서 입력 세부 정보를 설정합니다.

      이 맵의 키는 이전 단계에서 HTML 렌더러에 정의된 키와 동일해야 합니다.

      또한 맵에 값 **Employees/PtoApplication**&#x200B;과 함께 **sling:resourceType** 키를 추가합니다.

   1. **PTO 요약 만들기** 프로세스의 **ContentRepositoryConnector** 서비스의 하위 프로세스 **storeContent**&#x200B;를 사용합니다. 이 하위 프로세스는 CRX 노드를 만듭니다.

      3개의 입력 변수가 필요합니다.

      * **폴더 경로**:새 CRX 노드가 생성되는 경로입니다. 경로를 **/content**&#x200B;로 설정합니다.
      * **노드 이름**:이 필드에 입력 변수 nodeName을 지정합니다. 이것은 고유한 노드 이름 문자열입니다.
      * **노드 유형**:유형을  **nt:unstructured로 정의합니다**. 이 프로세스의 출력은 nodePath입니다. nodePath는 새로 만든 노드의 CRX 경로입니다. ndoePath는 **PTO** 요약 프로세스 만들기의 최종 출력입니다.
   1. 제출된 양식 데이터(**employeeName**, **employeeID**, **ptoReason** 및 **totalDays**)를 새 프로세스 **에 입력하여 전달합니다.** 출력을 **ptoSummaryNodePath**&#x200B;로 가져옵니다.


1. 요약 URL을 **ptoSummaryNodePath**&#x200B;와 함께 서버 세부 사항을 포함하는 XPath 식으로 정의합니다.

   XPath: `concat('https://[*server*]:[*port*]/lc',/process_data/@ptoSummaryNodePath,'.html')`.

AEM Forms 작업 공간에서 작업을 열면 요약 Url이 CRX 노드에 액세스하고 HTML 렌더러가 요약을 표시합니다.

요약 레이아웃은 프로세스를 수정하지 않고 변경할 수 있습니다. HTML 렌더러는 요약을 적절히 표시합니다.
