---
title: OSGi 그룹 및 권한에 대한 AEM Forms
seo-title: OSGi 그룹 및 권한에 대한 AEM Forms
description: OSGi에서 AEM Forms을 관리할 사용자를 그룹에 할당
seo-description: OSGi에서 AEM Forms을 관리할 사용자를 그룹에 할당
uuid: f269a206-356d-4cee-b449-05c5da87121a
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
topic-tags: Configuration
discoiquuid: 1717b1b4-1c2a-450e-8e79-4156a974d5fa
docset: aem65
translation-type: tm+mt
source-git-commit: 494551d3d886c1ed70d252a28b03cfa9d8e82a6a
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 1%

---


# OSGi 그룹 및 권한에 대한 AEM Forms{#aem-forms-on-osgi-groups-and-privileges}

[그룹](/help/sites-administering/user-group-ac-admin.md#group-administration)을 만들고 정책 및 [사용자](/help/sites-administering/user-group-ac-admin.md#user-administration)를 AEM의 그룹에 할당할 수 있습니다. 이러한 정책은 그룹의 일부인 사용자의 권한을 제어합니다.

[AEM Forms Add-on 패키지](../../forms/using/installing-configuring-aem-forms-osgi.md)를 설치하면 양식 사용자 및 forms-power-user와 같이 이 아티클에 언급된 그룹을 자동으로 할당할 수 있습니다. 다음 표는 그룹 할당을 기반으로 OSGi에서 사용자가 AEM Forms에 대해 수행할 수 있는 작업을 나열합니다.

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
     <li>인터랙티브한 커뮤니케이션 및 문서 조각 제작, 미리 보기 및 게시</li> 
     <li>AEM 인스턴스에 자산 업로드</li> 
     <li>테마 만들기</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>양식 파워 유저</td> 
   <td>
    <ul> 
     <li>적응형 양식 만들기, 미리 보기, 게시 및 제출</li> 
     <li>인터랙티브한 커뮤니케이션 및 문서 조각 제작, 미리 보기 및 게시</li> 
     <li>코드 편집기를 사용하여 적응형 양식에 대한 스크립트 만들기</li> 
     <li>스크립트를 포함한 자산 업로드</li> 
     <li>테마 만들기</li> 
     <li>XDP가 포함된 패키지 가져오기</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>양식 제출 검토자</td> 
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
     <li>적응형 양식 또는 인터랙티브한 커뮤니케이션 템플릿 만들기 및 미리 보기</li> 
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
     <li>에이전트 UI를 사용하여 통신 관리 서신 또는 인터랙티브한 커뮤니케이션에 액세스</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td><p>workflow-editors</p> </td> 
   <td>
    <ul> 
     <li>받은 편지함 응용 프로그램 만들기</li> 
     <li>워크플로우 모델 만들기</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>workflow-users</td> 
   <td>
    <ul> 
     <li>AEM 받은 편지함 응용 프로그램 사용<br /> <strong>참고:AEM 받은 편지함에서 Interactive Communications Agent UI에 액세스하려면 cm-agent-users 및 workflow-users 그룹 할당이 있어야 합니다.</strong></li> 
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

