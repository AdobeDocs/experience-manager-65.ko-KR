---
title: 요약 URL에서 작업 변수를 가져오는 중
description: 작업 정보를 재사용하고 요약 URL을 생성하여 작업을 요약하거나 설명하는 방법.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: b5e27b54-d141-48dd-a4ed-dd0a691319a5
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 0%

---

# 요약 URL에서 작업 변수를 가져오는 중 {#getting-task-variables-in-summary-url}

요약 페이지에는 작업 관련 정보가 표시됩니다. 이 문서에서는 요약 페이지에서 작업 관련 정보를 재사용하는 방법에 대해 설명합니다.

이 샘플 오케스트레이션에서는 직원이 휴가 신청 양식을 제출합니다. 그러면 지원서는 승인을 위해 직원의 관리자에게 제출됩니다.

1. resourseType **Employees/PtoApplication**&#x200B;에 대한 샘플 HTML 렌더러(html.esp)를 만듭니다.

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

1. 오케스트레이션을 수정하여 제출된 양식 데이터에서 4가지 속성을 추출합니다. 이렇게 하면 속성이 채워진 **직원/PtoApplication** 유형의 CRX에 노드가 만들어집니다.

   1. 오케스트레이션에서 **작업 할당** 작업 전에 **PTO 요약 만들기** 프로세스를 만들고 하위 프로세스로 사용합니다.
   1. 새 프로세스에서 **employeeName**, **employeeID**, **ptoReason**, **totalDays** 및 **nodeName**&#x200B;을(를) 입력 변수로 정의합니다. 이러한 변수는 제출된 양식 데이터로 전달됩니다.

      또한 요약 URL을 설정하는 동안 사용되는 출력 변수 **ptoNodePath**&#x200B;을(를) 정의합니다.

   1. **PTO 요약 만들기** 프로세스에서 **값 설정** 구성 요소를 사용하여 **nodeProperty**(**nodeProps**) 맵에서 입력 세부 정보를 설정합니다.

      이 맵의 키는 이전 단계에서 HTML 렌더러에 정의된 키와 동일해야 합니다.

      또한 맵에 값 **Employees/PtoApplication**&#x200B;을(를) 가진 **sling:resourceType** 키를 추가하십시오.

   1. **PTO 요약 만들기** 프로세스에서 **ContentRepositoryConnector** 서비스의 하위 프로세스 **storeContent**&#x200B;을(를) 사용합니다. 이 하위 프로세스는 CRX 노드를 만듭니다.

      세 개의 입력 변수가 필요합니다.

      * **폴더 경로**: 새 CRX 노드가 만들어지는 경로입니다. 경로를 **/content**(으)로 설정합니다.
      * **노드 이름**: 이 필드에 입력 변수 nodeName을 할당합니다. 고유한 노드 이름 문자열입니다.
      * **노드 형식**: 형식을 **nt:unstructured**(으)로 정의합니다. 이 프로세스의 출력은 nodePath입니다. nodePath는 새로 만든 노드의 CRX 경로입니다. NodePath는 **PTO 만들기** 요약 프로세스의 최종 출력입니다.

   1. 제출된 양식 데이터(**employeeName**, **employeeID**, **ptoReason** 및 **totalDays**)를 새 프로세스 **PTO 요약 만들기**&#x200B;에 입력으로 전달합니다. 출력을 **ptoSummaryNodePath**(으)로 가져옵니다.

1. 요약 URL을 **ptoSummaryNodePath**&#x200B;과(와) 함께 서버 세부 정보가 포함된 XPath 식으로 정의합니다.

   XPath: `concat('https://[*server*]:[*port*]/lc',/process_data/@ptoSummaryNodePath,'.html')`.

AEM Forms workspace에서 작업을 열면 요약 URL이 CRX 노드에 액세스하고 HTML 렌더러가 요약을 표시합니다.

요약 레이아웃은 프로세스를 수정하지 않고 변경할 수 있습니다. HTML 렌더러는 요약을 적절히 표시합니다.
