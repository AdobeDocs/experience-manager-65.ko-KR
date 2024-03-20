---
title: OSGi 그룹 및 권한의 AEM Forms
description: OSGi에서 Adobe Experience Manager(AEM) Forms을 관리하도록 그룹에 사용자 할당
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
topic-tags: Configuration
docset: aem65
role: Admin
exl-id: d802ac53-e3db-45ca-afcb-7e99d0bb7877
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 6%

---

# OSGi 그룹 및 권한의 AEM Forms{#aem-forms-on-osgi-groups-and-privileges}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/forms-groups-privileges-tasks.html) |
| AEM 6.5 | 이 문서 |

다음을 수행할 수 있습니다. [그룹 만들기](/help/sites-administering/user-group-ac-admin.md#group-administration) 및 정책 할당 [사용자](/help/sites-administering/user-group-ac-admin.md#user-administration) Adobe Experience Manager(AEM)의 그룹에 연결합니다. 이러한 정책은 그룹에 속한 사용자의 권한을 제어합니다.

를 설치한 후 [AEM Forms 추가 기능 패키지](../../forms/using/installing-configuring-aem-forms-osgi.md)이 문서에 언급된 그룹(예: forms-users 및 forms-power-user)은 자동으로 할당에 사용할 수 있습니다. 다음 표에는 사용자가 그룹 할당을 기반으로 OSGi에서 AEM Forms에 대해 수행할 수 있는 작업이 나열되어 있습니다.

<table>
 <tbody>
  <tr>
   <td>그룹</td> 
   <td>작업</td> 
  </tr>
  <tr>
   <td>forms-users <sup>[1]</sup></td> 
   <td>
    <ul> 
     <li>적응형 양식 만들기, 미리보기, 게시 및 제출</li> 
     <li>대화형 통신 및 문서 조각 만들기, 미리보기 및 게시</li> 
     <li>AEM 인스턴스에 자산 업로드</li> 
     <li>테마 만들기</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>forms-power-users</td> 
   <td>
    <ul> 
     <li>적응형 양식 만들기, 미리보기, 게시 및 제출</li> 
     <li>대화형 통신 및 문서 조각 만들기, 미리보기 및 게시</li> 
     <li>코드 편집기를 사용하여 적응형 양식용 스크립트 만들기</li> 
     <li>스크립트를 포함한 에셋 업로드</li> 
     <li>테마 만들기</li> 
     <li>XDP가 포함된 패키지 가져오기</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>forms-submission-reviewers</td> 
   <td>
    <ul> 
     <li>제출 검토</li> 
     <li>제출 승인 또는 거부</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>템플릿 작성자 <sup>[2]</sup></td> 
   <td>
    <ul> 
     <li>적응형 양식 또는 대화형 커뮤니케이션 템플릿 만들기 및 미리 보기</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td><p>fdm-authors</p> </td> 
   <td>
    <ul> 
     <li>양식 데이터 모델 만들기 및 수정</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>cm-agent-user</td> 
   <td>
    <ul> 
     <li>에이전트 UI를 사용하여 서신 관리 편지 또는 대화형 통신에 액세스</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td><p>워크플로우 편집기</p> </td> 
   <td>
    <ul> 
     <li>받은 편지함 응용 프로그램 만들기</li> 
     <li>워크플로우 모델 만들기</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>워크플로 사용자</td> 
   <td>
    <ul> 
     <li>AEM 받은 편지함 애플리케이션 사용<br /> <strong>참고: </strong>AEM 받은 편지함에서 대화형 통신 에이전트 UI에 액세스하려면 cm-agent-users 및 workflow-users 그룹을 할당해야 합니다.</li> 
     <li>워크플로우 인스턴스 관리</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>fd-administrators</td> 
   <td>
    <ul> 
     <li>PDF 생성기 구성</li> 
     <li>감시 폴더 구성</li> 
     <li>워크플로우 애플리케이션 관리</li> 
    </ul> </td> 
  </tr>
 </tbody>
</table>

1. 양식 사용자 그룹 권한이 있는 사용자는 적응형 양식에 대한 스크립트를 작성할 수 없습니다.
1. 템플릿 작성자 그룹 권한이 있는 사용자는 템플릿에 대한 스크립트를 작성할 수 없습니다.
