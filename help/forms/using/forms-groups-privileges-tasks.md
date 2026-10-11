---
title: OSGi 그룹 및 권한에 대한 AEM Forms
description: OSGi에서 Adobe Experience Manager(AEM) Forms을 관리하도록 그룹에 사용자 할당
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
topic-tags: Configuration
docset: aem65
role: Admin,User
exl-id: d802ac53-e3db-45ca-afcb-7e99d0bb7877
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 10%
---
# OSGi 그룹 및 권한에 대한 AEM Forms{#aem-forms-on-osgi-groups-and-privileges}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/forms-groups-privileges-tasks.html?lang=ko) |
| AEM 6.5 | 이 문서 |

Adobe Experience Manager(AEM)의 그룹에 [그룹을 만들고](/help/sites-administering/user-group-ac-admin.md#group-administration) 정책 및 [사용자](/help/sites-administering/user-group-ac-admin.md#user-administration)를 할당할 수 있습니다. 이러한 정책은 그룹에 속한 사용자의 권한을 제어합니다.

[AEM Forms 추가 기능 패키지](../../forms/using/installing-configuring-aem-forms-osgi.md)를 설치하면 이 문서에 언급된 그룹(예: forms-users 및 forms-power-user)을 자동으로 할당할 수 있습니다. 다음 표에는 사용자가 그룹 할당을 기반으로 OSGi에서 AEM Forms에 대해 수행할 수 있는 작업이 나열되어 있습니다.

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
     <li>AEM 받은 편지함 응용 프로그램 사용<br /> <strong>참고: </strong>AEM 받은 편지함의 대화형 통신 에이전트 UI에 액세스하려면 cm 에이전트 사용자와 워크플로 사용자 그룹을 할당해야 합니다.</li> 
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
