---
title: 요약 URL에서 작업 변수 가져오기
seo-title: 요약 URL에서 작업 변수 가져오기
description: 작업에 대한 정보를 다시 사용하고 요약 URL을 생성하여 작업을 요약하거나 설명하는 방법입니다.
seo-description: 작업에 대한 정보를 다시 사용하고 요약 URL을 생성하여 작업을 요약하거나 설명하는 방법입니다.
uuid: 9eab3a6a-a99a-40ae-b483-33ec7d21c5b6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 6dc31bec-b02d-47db-a4f4-be8c14c5619e
exl-id: b5e27b54-d141-48dd-a4ed-dd0a691319a5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 0%

---

# 요약 URL {#getting-task-variables-in-summary-url}의 작업 변수 가져오기

요약 페이지에 작업 관련 정보가 표시됩니다. 이 문서에서는 요약 페이지에서 작업 관련 정보를 다시 사용할 수 있는 방법에 대해 설명합니다.

이 샘플 오케스트레이션에서 직원이 Leave 애플리케이션 양식을 제출합니다. 그러면 신청서가 승인을 위해 직원 관리자에게 전달됩니다.

1. ResourceType **Employees/PtoApplication**&#x200B;에 대한 샘플 HTML 렌더러(html.esp)를 만듭니다.

   렌더러는 노드에서 설정할 다음 속성을 가정합니다.

   * 이름
   * empid
   * 이유
   * 기간

   >[!NOTE]
   >
   >이 렌더러는 요약 페이지 템플릿입니다.

   이 렌더러에 대한 다음 샘플 코드는에 포함되어 있습니다.

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

1. 오케스트레이션을 수정하여 제출된 양식 데이터에서 4개의 속성을 추출할 수 있습니다. 그런 다음 **Employees/PtoApplication** 유형의 CRX에 속성이 채워지는 노드를 생성합니다.

   1. 프로세스 **PTO 요약 생성**&#x200B;을 생성하고 이를 오케스트레이션의 **작업 지정** 작업 전의 하위 프로세스로 사용하십시오.
   1. **employeeName**, **employeeID**, **ptoReason**, **totalDays** 및 **nodeName**&#x200B;을(를) 새 프로세스에서 입력 변수로 정의합니다. 이러한 변수는 제출된 양식 데이터로 전달됩니다.

      요약 Url을 설정하는 동안 사용할 출력 변수 **ptoNodePath**&#x200B;도 정의합니다.

   1. **PTO 요약 만들기** 프로세스에서 **값** 구성 요소를 사용하여 **nodeProperty**(**nodeProps**) 맵에서 입력 세부 정보를 설정합니다.

      이 맵의 키는 이전 단계에서 HTML 렌더러에 정의된 키와 동일해야 합니다.

      또한 맵에 **Employees/PtoApplication** 값과 함께 **sling:resourceType** 키를 추가합니다.

   1. **PTO 요약 만들기** 프로세스의 **ContentRepositoryConnector** 서비스의 하위 프로세스 **storeContent**&#x200B;를 사용합니다. 이 하위 프로세스는 CRX 노드를 만듭니다.

      이렇게 하려면 세 개의 입력 변수가 필요합니다.

      * **폴더 경로**:새 CRX 노드가 만들어지는 경로입니다. 경로를 **/content**&#x200B;로 설정합니다.
      * **노드 이름**:이 필드에 입력 변수 nodeName을 지정합니다. 고유한 노드 이름 문자열입니다.
      * **노드 유형**:유형을  **nt:un구조화되지 않음**&#x200B;으로 정의합니다. 이 프로세스의 출력은 nodePath입니다. nodePath 는 새로 만든 노드의 CRX 경로입니다. ndoePath는 **PTO** 요약 프로세스를 작성하는 최종 출력입니다.
   1. 제출된 양식 데이터(**employeeName**, **employeeID**, **ptoReason** 및 **totalDays**)를 새 프로세스 **PTO 요약 만들기**&#x200B;에 입력으로 전달합니다. 출력을 **ptoSummaryNodePath**&#x200B;로 가져옵니다.


1. 요약 Url을 **ptoSummaryNodePath**&#x200B;와 함께 서버 세부 정보가 포함된 XPath 식으로 정의합니다.

   XPath: `concat('https://[*server*]:[*port*]/lc',/process_data/@ptoSummaryNodePath,'.html')`.

AEM Forms 작업 공간에서 작업을 열면 요약 Url이 CRX 노드에 액세스하고 HTML 렌더러에 요약이 표시됩니다.

요약 레이아웃은 프로세스를 수정하지 않고 변경할 수 있습니다. HTML 렌더러는 요약을 적절하게 표시합니다.
