---
title: OSGi 그룹 및 권한의 AEM Forms
seo-title: OSGi 그룹 및 권한의 AEM Forms
description: OSGi에서 AEM Forms을 관리할 그룹에 사용자 할당
seo-description: OSGi에서 AEM Forms을 관리할 그룹에 사용자 할당
uuid: f269a206-356d-4cee-b449-05c5da87121a
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
topic-tags: Configuration
discoiquuid: 1717b1b4-1c2a-450e-8e79-4156a974d5fa
docset: aem65
role: Administrator
exl-id: d802ac53-e3db-45ca-afcb-7e99d0bb7877
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 1%

---

# OSGi 그룹의 AEM Forms 및 Privileges{#aem-forms-on-osgi-groups-and-privileges}

[그룹](/help/sites-administering/user-group-ac-admin.md#group-administration)을 만들고, 정책 및 [사용자](/help/sites-administering/user-group-ac-admin.md#user-administration)를 AEM의 그룹에 할당할 수 있습니다. 이러한 정책은 그룹에 속하는 사용자의 권한을 제어합니다.

[AEM Forms 추가 기능 패키지](../../forms/using/installing-configuring-aem-forms-osgi.md)를 설치하면 forms-users 및 forms-power-user와 같이 이 문서에 언급된 그룹을 자동으로 할당에 사용할 수 있습니다. 다음 표에는 그룹 할당을 기반으로 사용자가 OSGi에서 AEM Forms에 대해 수행할 수 있는 작업이 나열되어 있습니다.

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
     <li>적응형 양식 만들기, 미리 보기, 게시 및 제출</li> 
     <li>대화형 커뮤니케이션 및 문서 조각 만들기, 미리 보기 및 게시</li> 
     <li>AEM 인스턴스에 자산 업로드</li> 
     <li>테마 만들기</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>forms-power-users</td> 
   <td>
    <ul> 
     <li>적응형 양식 만들기, 미리 보기, 게시 및 제출</li> 
     <li>대화형 커뮤니케이션 및 문서 조각 만들기, 미리 보기 및 게시</li> 
     <li>코드 편집기를 사용하여 적응형 양식의 스크립트 만들기</li> 
     <li>스크립트를 포함한 자산 업로드</li> 
     <li>테마 만들기</li> 
     <li>XDP가 포함된 패키지 가져오기</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>forms 제출 검토자</td> 
   <td>
    <ul> 
     <li>제출 검토</li> 
     <li>제출 승인 또는 거부</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>template-authors <sup>[2]</sup></td> 
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
   <td>cm-agent-users</td> 
   <td>
    <ul> 
     <li>에이전트 UI를 사용하여 서신 관리 편지 또는 대화형 커뮤니케이션에 액세스</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td><p>workflow-editors</p> </td> 
   <td>
    <ul> 
     <li>받은 편지함 애플리케이션 만들기</li> 
     <li>워크플로우 모델 만들기</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>workflow-users</td> 
   <td>
    <ul> 
     <li>AEM 받은 편지함 응용 프로그램 사용<br /> <strong>참고:</strong>AEM 받은 편지함에서 Interactive Communications Agent UI에 액세스하려면 cm-agent-users 및 workflow-users 그룹이 할당되어 있어야 합니다.</li> 
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

1. forms-users 그룹 권한이 있는 사용자는 적응형 양식에 대한 스크립트를 작성할 수 없습니다.
1. 템플릿 작성자 그룹 권한이 있는 사용자는 템플릿에 대한 스크립트를 작성할 수 없습니다.
