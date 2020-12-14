---
title: AEM Forms 작업 공간에 대한 문제 해결 지침
seo-title: AEM Forms 작업 공간에 대한 문제 해결 지침
description: 로그를 활성화하고 브라우저에서 디버거를 사용하여 AEM Forms 작업 영역의 문제를 해결합니다.
seo-description: 로그를 활성화하고 브라우저에서 디버거를 사용하여 AEM Forms 작업 영역의 문제를 해결합니다.
uuid: 07b8c8ed-f1ff-4be5-8005-251ff7b2ac85
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 5dae9ed9-77a3-44f5-a94d-ca5c355c8730
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '747'
ht-degree: 1%

---


# AEM Forms 작업 영역 {#troubleshooting-guidelines-for-aem-forms-workspace}에 대한 문제 해결 지침

이 문서에서는 로깅을 활성화하고 브라우저에서 디버거를 사용하여 AEM Forms 작업 공간을 디버깅하는 방법에 대해 설명합니다. 또한 AEM Forms 작업 영역을 사용할 때 발생할 수 있는 몇 가지 일반적인 문제와 해결책을 설명합니다.

## AEM Forms 작업 영역 패키지 {#unable-to-install-aem-forms-workspace-package}을(를) 설치할 수 없습니다.

패치를 설치한 후 AEM Forms 작업 공간을 엽니다. 리소스를 찾을 수 없음 오류가 발생하면 CRX 패키지 관리자를 열고 `adobe-lc-workspace-pkg-<version>.zip` 패키지를 다시 설치하십시오.

패키지를 설치하는 동안 오류 `javax.jcr.nodetype.ConstraintViolationException: OakConstraint0025: Authorizable property rep:authorizableId may not be removed`이 발생하면 다음 단계를 수행하십시오.

1. CRX DE lite에 로그인합니다. 기본 url은 `https://[localhost]:'port'/lc/crx/de/index.jsp`입니다.
1. 다음 노드를 삭제합니다.

   `/home/groups/P/PERM_WORKSPACE_USER`

1. 패키지 관리자로 이동합니다. 기본 URL은 `https://[localhost]:'port'/lc/crx/packmgr/index.jsp.`
1. `adobe-lc-workspace-pkg-[version].zip` 패키지를 검색하고 설치합니다.
1. 응용 프로그램 서버를 다시 시작합니다.

## AEM Forms 작업 영역 로깅 {#aem-forms-workspace-nbsp-logging}

다양한 수준에서 로그를 생성하여 오류를 최적의 문제 해결을 활성화할 수 있습니다. 예를 들어 복잡한 응용 프로그램에서 구성 요소 수준에서 로깅은 특정 구성 요소를 디버깅하고 문제 해결하는 데 도움이 됩니다.

AEM Forms 작업 영역에서:

* 특정 구성 요소 파일에 대한 로깅 정보를 가져오려면 URL에 `/log/<ComponentFile>/<LogLevel>`을 추가하고 `Enter` 키를 누릅니다. 지정된 로그 수준에서 구성 요소 파일에 대한 모든 로깅 정보가 콘솔에 인쇄됩니다.

* 모든 구성 요소 파일의 로깅 정보를 가져오려면 URL에 `/log/all/trace`을 추가하고 `Enter` 키를 누릅니다.

* 로그 형식:`<Component file> <Date>:<Time>: <Log Level> : <Log Message>`

>[!NOTE]
>
>기본적으로 모든 구성 요소의 로그 수준은 INFO로 설정됩니다.

* 사용자가 설정한 로그 수준은 해당 브라우저 세션에 대해서만 유지됩니다. 사용자가 페이지를 새로 고칠 때 로그 수준은 모든 구성 요소에 대한 초기 값으로 설정됩니다.

### AEM Forms 작업 영역 {#list-of-component-files-in-nbsp-aem-forms-workspace}의 구성 요소 파일 목록

<table>
 <tbody>
  <tr>
   <td><p>allcategoryModel</p> </td>
   <td><p>processinstanceModel</p> </td>
   <td><p>tasklistModel</p> </td>
  </tr>
  <tr>
   <td><p>appnavigationModel</p> </td>
   <td><p>processInstanceView</p> </td>
   <td><p>tasklist보기</p> </td>
  </tr>
  <tr>
   <td><p>appnavigationView</p> </td>
   <td><p>processnamelistModel</p> </td>
   <td><p>taskModel</p> </td>
  </tr>
  <tr>
   <td><p>categorylistModel</p> </td>
   <td><p>processnamelistView</p> </td>
   <td><p>taskView</p> </td>
  </tr>
  <tr>
   <td><p>categorylistView</p> </td>
   <td><p>processnameModel</p> </td>
   <td><p>teamqueuesView</p> </td>
  </tr>
  <tr>
   <td><p>categoryModel</p> </td>
   <td><p>processnameView</p> </td>
   <td><p>todoView</p> </td>
  </tr>
  <tr>
   <td><p>categoryView</p> </td>
   <td><p>searchtemplatedetails보기</p> </td>
   <td><p>trackingView</p> </td>
  </tr>
  <tr>
   <td><p>favoritecategoryModel</p> </td>
   <td><p>sharequeueModel</p> </td>
   <td><p>uisettingsModel</p> </td>
  </tr>
  <tr>
   <td><p>filterlistView</p> </td>
   <td><p>sharequeueView</p> </td>
   <td><p>uiView</p> </td>
  </tr>
  <tr>
   <td><p>filterView</p> </td>
   <td><p>startpointlistModel</p> </td>
   <td><p>userinfoModel</p> </td>
  </tr>
  <tr>
   <td><p>otofofficeModel</p> </td>
   <td><p>startpointlistView</p> </td>
   <td><p>userinfoView</p> </td>
  </tr>
  <tr>
   <td><p>otofofficeView</p> </td>
   <td><p>startpointModel</p> </td>
   <td><p>usersearchModel</p> </td>
  </tr>
  <tr>
   <td><p>preferencesView</p> </td>
   <td><p>startpointView</p> </td>
   <td><p>usersearchView</p> </td>
  </tr>
  <tr>
   <td><p>processinstancehistoryView</p> </td>
   <td><p>startProcessView</p> </td>
   <td><p>wserrorModel</p> </td>
  </tr>
  <tr>
   <td><p>processincelistModel</p> </td>
   <td><p>startprocessView</p> </td>
   <td><p>wserrorView</p> </td>
  </tr>
  <tr>
   <td><p>processincelistView</p> </td>
   <td><p>taskdetails보기</p> </td>
   <td><p>wsmessageView</p> </td>
  </tr>
 </tbody>
</table>

### AEM Forms 작업 영역 {#log-levels-available-in-nbsp-aem-forms-workspace}에서 사용할 수 있는 로그 수준

* 치명적
* 오류
* 경고
* 정보
* 디버그
* TRACE
* 끔

## 브라우저 {#debugging-information-for-browsers} 디버깅 정보

스크립트와 스타일은 다른 브라우저에서 디버깅될 수 있습니다.

* **IE에서의 디버깅**:IE에서 AEM Forms 작업 영역을 디버깅하려면 다음을 참조하십시오. [https://msdn.microsoft.com/en-us/library/hh772704(v=vs.85).aspx](https://msdn.microsoft.com/en-us/library/hh772704(v=vs.85).aspx).

* **크롬에서 디버깅**:크롬에서 디버거를 열려면 바로 가기를 사용합니다.Ctrl+Shift+I.자세한 내용은 다음을 참조하십시오. [https://developer.chrome.com/extensions/tut_debugging.html](https://developer.chrome.com/extensions/tut_debugging.html).

* **Firefox에서의 디버깅**:Firefox에서 스크립트 및 스타일을 디버깅하는 데 여러 개의 추가 기능을 사용할 수 있습니다. 예를 들어 Firebug는 이러한 디버깅 유틸리티([https://getfirebug.com](https://getfirebug.com)) 중 하나입니다.

## FAQ {#faqs}

1. PDF 양식이 Google Chrome에서 렌더링되거나 제출되지 않습니다.

   1. Adobe® Reader® 플러그인을 설치합니다.
   1. 사용 가능한 플러그인을 보려면 Chrome에서 chrome://plugins을 엽니다.
   1. Chrome PDF 뷰어 플러그인을 비활성화하고 Adobe Reader 플러그인을 활성화합니다.

1. SWF 양식 또는 안내서가 Google Chrome에서 렌더링되지 않습니다.

   1. 사용 가능한 플러그인을 보려면 Chrome에서 chrome://plugins을 엽니다.
   1. Adobe Flash® Player 플러그인에 대한 자세한 내용을 참조하십시오.
   1. Adobe Flash Player 플러그인에서 PepperFlash를 비활성화합니다.

1. AEM Forms 작업 영역을 사용자 지정했지만 변경 내용을 볼 수 없습니다.

   브라우저의 캐시를 지운 다음 AEM Forms 작업 영역에 액세스합니다.

1. 데스크탑에서 양식을 열 때 HTML로 양식을 렌더링할 수 있도록 하려면 어떻게 해야 합니까?

   워크벤치를 사용하는 동안 할당 작업 단계에서 기본 프로파일에 대한 HTML 라디오 단추를 선택합니다.

1. 클릭하면 첨부 파일이 표시되지 않습니다.

   첨부 파일을 보려면 브라우저에서 팝업을 활성화합니다.

1. 사용자가 양식 애플리케이션에 로그인되었습니다. 사용자가 작업 영역에 로그인하려고 하면 사용자에게 작업 공간 권한이 없는 경우 작업 영역이 로드되지 않을 수 있습니다.

   다른 양식 애플리케이션에서 로그아웃한 다음 작업 영역에 로그인합니다.

1. 디자인에 [프로세스 속성]을 사용하는 HTML 양식은 AEM Forms 작업 영역에서 렌더링하면 양식 내에 [제출] 단추를 표시합니다.

   양식을 디자인할 때 [처리 속성]을 사용할 때 양식 내에 [제출] 단추가 추가됩니다. AEM Forms 작업 영역에서 PDF로 렌더링하면 최종 사용자에게 [제출] 단추가 표시되지 않습니다. 그러나 AEM Forms 작업 영역에서 HTML 양식으로 렌더링할 때 최종 사용자에게 전송 단추가 표시됩니다. 양식 내에서 이 제출 단추를 클릭해도 작업이 시작되지 않습니다. 양식 외부에 있는 AEM Forms 작업 영역의 하단에 있는 제출 단추를 클릭하면 작업이 완료됩니다.
