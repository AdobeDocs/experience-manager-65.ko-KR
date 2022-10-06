---
title: 재사용 가능한 구성 요소에 대한 설명
seo-title: Description of reusable components
description: 웹 애플리케이션에서 AEM Forms 작업 공간 구성 요소를 통합하는 데 도움이 되는 파일 이름 및 종속성이 있는 재사용 가능한 구성 요소의 전체 목록입니다.
seo-description: A complete list of reusable components with filenames and dependencies, to help you integrate AEM Forms workspace component in your web applications.
uuid: 8e6accc7-0935-4d7b-b838-d23676df5cda
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: d3facd17-ceb0-4799-8cd9-ff9e81e09793
exl-id: b8cb7233-3d9e-41d4-85c5-8e8c2481f89c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1231'
ht-degree: 9%

---

# 재사용 가능한 구성 요소에 대한 설명 {#description-of-reusable-components}

AEM Forms 작업 공간은 [재사용 가능](/help/forms/using/integrating-html-ws-components-web.md) 특정 구성 요소로 구성된 구성 요소 [폴더 구조](/help/forms/using/folder-structure.md) CRX™. 각 구성 요소에는 폴더 구조에 지정된 위치에 모델, 보기 및 템플릿 파일이 있으며, 다른 구성 요소 파일에 대한 JavaScript™ 종속성, 구성 요소에서 수신한 이벤트 및 AEM Forms 작업 영역에서 이러한 이벤트를 트리거하는 JavaScript 개체가 있습니다. 구성 파일 이름 및 종속성이 있는 재사용 가능한 구성 요소의 전체 목록이 여기에 제공됩니다.

## 작업 목록 {#tasklist}

<table>
 <tbody>
  <tr>
   <td><p>모델</p></td>
   <td><p>tasklist.js</p></td>
  </tr>
  <tr>
   <td><p>보기</p></td>
   <td><p>tasklist.js</p></td>
  </tr>
  <tr>
   <td><p>템플릿</p></td>
   <td><p>tasklist.html</p></td>
  </tr>
  <tr>
   <td><p>구성 요소 필요</p></td>
   <td>
    <ul>
     <li><p>UserSearch</p></li>
     <li><p>작업</p></li>
     <li><p>팀 작업</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>JS 종속성</p></td>
   <td>
    <ul>
     <li><p>작업 모델</p></li>
     <li><p>팀 작업 모델</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>수신한 이벤트(이벤트 이름 - 트리거)</p></td>
   <td>
    <ul>
     <li><p>filterSelected - tasklist 모델</p></li>
     <li><p>제거 - tasklist 모델</p></li>
     <li><p>updateQueue - tasklist 모델</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>사용자 지정 애플리케이션에서 이 구성 요소에 대해 filterSelected 이벤트를 트리거하는 경우, 이 구성 요소는 AEM Forms 작업 공간과 독립적으로 사용할 수 있습니다.

## 작업 {#task}

<table>
 <tbody>
  <tr>
   <td><p>모델</p></td>
   <td><p>task.js</p></td>
  </tr>
  <tr>
   <td><p>보기</p></td>
   <td><p>task.js</p></td>
  </tr>
  <tr>
   <td><p>템플릿</p></td>
   <td><p>task.html</p></td>
  </tr>
  <tr>
   <td><p>구성 요소 필요</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>JS 종속성</p></td>
   <td>
    <ul>
     <li><p>작업 목록 모델</p></li>
     <li><p>작업 유틸리티</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>수신한 이벤트(이벤트 이름 - 트리거)</p></td>
   <td>
    <ul>
     <li><p>submitComplete - 작업 모델</p></li>
     <li><p>거부 - 작업 모델</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>작업 공간에서 이 구성 요소에 대한 작업 모델을 만들기 위해 TaskList 모델의 fetchTasks 함수를 호출합니다.

## 필터 목록 {#filterlist}

<table>
 <tbody>
  <tr>
   <td><p>모델</p></td>
   <td><p>tasklist.js</p></td>
  </tr>
  <tr>
   <td><p>보기</p></td>
   <td><p>filterlist.js</p></td>
  </tr>
  <tr>
   <td><p>템플릿</p></td>
   <td><p>filterlist.html</p></td>
  </tr>
  <tr>
   <td><p>구성 요소 필요</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>JS 종속성</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>수신한 이벤트(이벤트 이름 - 트리거)</p></td>
   <td>
    <ul>
     <li><p>가져오기 - 작업 목록 모델 </p></li>
     <li><p>제거 - tasklist 모델 </p></li>
     <li><p>updateQueue - tasklist 모델 </p></li>
     <li><p>새로 고침큐 - 작업 목록 모델 </p></li>
     <li><p>filterSelected - tasklist 모델</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

## 필터 {#filter}

<table>
 <tbody>
  <tr>
   <td><p>보기</p> </td>
   <td><p>filter.js</p> </td>
  </tr>
  <tr>
   <td><p>템플릿</p> </td>
   <td><p>filter.html</p> </td>
  </tr>
  <tr>
   <td><p>구성 요소 필요</p> </td>
   <td><p>NA</p> </td>
  </tr>
  <tr>
   <td><p>JS 종속성</p> </td>
   <td>
    <ul>
     <li><p>필드: 큐: { name, qid, isDefault, type}</p> </li>
     <li><p>필드: 쿼리: string</p> </li>
     <li><p>필드: parentView: 필터 목록 보기</p> </li>
     <li><p>필드: parentModel: 작업 목록 모델</p> </li>
     <li><p>필드: 유틸리티</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>이벤트가 수신됨</p> </td>
   <td><p>NA</p> </td>
  </tr>
 </tbody>
</table>

## TeamQueues {#teamqueues}

<table>
 <tbody>
  <tr>
   <td><p>모델</p></td>
   <td><p>tasklist.js</p></td>
  </tr>
  <tr>
   <td><p>보기</p></td>
   <td><p>teamqueues.js</p></td>
  </tr>
  <tr>
   <td><p>템플릿</p></td>
   <td><p>teamqueues.html</p></td>
  </tr>
  <tr>
   <td><p>구성 요소 필요</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>JS 종속성</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>수신한 이벤트(이벤트 이름 - 트리거)</p></td>
   <td>
    <ul>
     <li><p>가져오기 - 작업 목록 모델 </p></li>
     <li><p>제거 - tasklist 모델 </p></li>
     <li><p>updateQueue - tasklist 모델 </p></li>
     <li><p>teamQueuesConverted - tasklist 모델 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

## TeamFilter {#teamfilter}

<table>
 <tbody>
  <tr>
   <td><p>모델</p> </td>
   <td><p>NA</p> </td>
  </tr>
  <tr>
   <td><p>보기</p> </td>
   <td><p>teamfilter.js</p> </td>
  </tr>
  <tr>
   <td><p>템플릿</p> </td>
   <td><p>teamfilter.html</p> </td>
  </tr>
  <tr>
   <td><p>구성 요소 필요</p> </td>
   <td><p>NA</p> </td>
  </tr>
  <tr>
   <td><p>JS 종속성</p> </td>
   <td>
    <ul>
     <li><p>확장 : 필터 보기</p> </li>
     <li><p>필드 : queue :{ name, qid, isDefault, type }</p> </li>
     <li><p>필드 : 쿼리 : string</p> </li>
     <li><p>필드 : parentView : 필터 목록 보기</p> </li>
     <li><p>필드 : parentModel : 작업 목록 모델</p> </li>
     <li><p>필드 : 유틸리티</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>이벤트가 수신됨</p> </td>
   <td><p>NA</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>TeamFilter는 TaskList 구성 요소에서 선택한 작업을 나타내는 이벤트를 가져옵니다. 이러한 구성 요소가 모델 클래스를 공유하지만 다른 종속성은 없습니다.

## 작업 세부 사항 {#taskdetails}

<table>
 <tbody>
  <tr>
   <td><p>모델</p> </td>
   <td><p>tasklist.js</p> </td>
  </tr>
  <tr>
   <td><p>보기</p> </td>
   <td><p>taskdetails.js</p> </td>
  </tr>
  <tr>
   <td><p>템플릿</p> </td>
   <td><p>taskdetails.html</p> </td>
  </tr>
  <tr>
   <td><p>구성 요소 필요</p> </td>
   <td><p>대부분의 유틸리티 클래스</p> </td>
  </tr>
  <tr>
   <td><p>JS 종속성</p> </td>
   <td>
    <ul>
     <li><p>processinstancehistory.html</p> </li>
     <li><p>formrendering 유틸리티</p> </li>
     <li><p>참고 유틸리티</p> </li>
     <li><p>첨부 파일 유틸리티</p> </li>
     <li><p>작업 유틸리티</p> </li>
     <li><p>기록 유틸리티</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>수신한 이벤트(이벤트 이름 - 트리거)</p> </td>
   <td>
    <ul>
     <li><p>전달 - 작업 모델</p> </li>
     <li><p>공유 - 작업 모델</p> </li>
     <li><p>상담 - 작업 모델</p> </li>
     <li><p>거부 - 작업 모델</p> </li>
     <li><p>포기 - 작업 모델</p> </li>
     <li><p>unlocked - 작업 모델</p> </li>
     <li><p>잠긴 - 작업 모델</p> </li>
     <li><p>클레임 - 작업 모델</p> </li>
     <li><p>변경:taskselected - tasklist 모델</p> </li>
     <li><p>change:formUrl - 작업 모델</p> </li>
     <li>attachmentURLFenzed - 작업 모델</li>
    </ul>
    <ul>
     <li>newAttachment - 작업 모델</li>
     <li><p>taskHistoryContated - 작업 모델</p> </li>
     <li>prepareForSubmitComplete - 작업 모델</li>
     <li><p>submitComplete - 작업 모델</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 범주 목록 {#categorylist}

<table>
 <tbody>
  <tr>
   <td><p>모델</p></td>
   <td><p>categorylist.js</p></td>
  </tr>
  <tr>
   <td><p>보기</p></td>
   <td><p>categorylist.js</p></td>
  </tr>
  <tr>
   <td><p>템플릿</p></td>
   <td><p>startprocess.html(경로 폴더)</p></td>
  </tr>
  <tr>
   <td><p>구성 요소 필요</p></td>
   <td><p>범주</p></td>
  </tr>
  <tr>
   <td><p>JS 종속성</p></td>
   <td>
    <ul>
     <li><p>favoritecoryfactory 모델</p></li>
     <li><p>allcategoryfactory 모델</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>수신한 이벤트(이벤트 이름 - 트리거)</p></td>
   <td>
    <ul>
     <li><p>allStartpointsForceed - categorylist 모델 </p></li>
     <li><p>add - categorylist 모델 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>이 구성 요소는 StartPointList, StartPoint 및 Task와 같은 일부 다른 구성 요소의 모델 클래스를 사용합니다. 이 종속성 외에 CategoryList를 독립적으로 사용할 수 있습니다.

## 범주 {#category}

<table>
 <tbody>
  <tr>
   <td><p>모델</p></td>
   <td><p>category.js</p></td>
  </tr>
  <tr>
   <td><p>보기</p></td>
   <td><p>category.js</p></td>
  </tr>
  <tr>
   <td><p>템플릿</p></td>
   <td><p>category.html</p></td>
  </tr>
  <tr>
   <td><p>구성 요소 필요</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>JS 종속성</p></td>
   <td>
    <ul>
     <li><p>categorylist 모델</p></li>
     <li><p>startpointlist 모델</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>수신한 이벤트(이벤트 이름 - 트리거)</p></td>
   <td>
    <ul>
     <li><p>변경됨 - 카테고리 모델 </p></li>
     <li><p>childrenConverted - 카테고리 모델 </p></li>
     <li><p>카테고리:선택됨 - 카테고리목록 모델 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

## 시작 지점 목록 {#startpointlist}

<table>
 <tbody>
  <tr>
   <td><p>모델</p></td>
   <td><p>categorylist.js</p></td>
  </tr>
  <tr>
   <td><p>보기</p></td>
   <td><p>startpointlist.js</p></td>
  </tr>
  <tr>
   <td><p>템플릿</p></td>
   <td><p>startprocess.html(경로 폴더)</p></td>
  </tr>
  <tr>
   <td><p>구성 요소 필요</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>JS 종속성</p></td>
   <td>
    <ul>
     <li><p>범주 모델</p></li>
     <li><p>favoritecoryfactory 모델</p></li>
     <li><p>allcategoryfactory 모델</p></li>
     <li><p>시작 지점 보기</p></li>
     <li><p>startpointlist 모델</p></li>
     <li><p>시작점 모델</p></li>
     <li><p>작업 모델</p></li>
     <li><p>작업 모델</p></li>
     <li><p>작업 목록 모델</p></li>
     <li><p>팀 작업 모델</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>수신한 이벤트(이벤트 이름 - 트리거)</p></td>
   <td>
    <ul>
     <li><p>카테고리:선택됨 - 카테고리목록 모델 </p></li>
     <li><p>allStartpointsForceed - categorylist 모델 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>StartPointList 및 CategoryList 구성 요소는 모델 클래스를 공유하므로 모델 클래스는 후자에 따라 다릅니다. 카테고리 목록 은 표시되는 카테고리의 시작 지점에 대한 정보에 액세스합니다. StartPointList를 독립적으로 사용하려면 CategoryList에서 이벤트 트리거를 시뮬레이션합니다.

## 시작 지점 {#startpoint}

<table>
 <tbody>
  <tr>
   <td><p>모델</p></td>
   <td><p>startpoint.js</p></td>
  </tr>
  <tr>
   <td><p>보기</p></td>
   <td><p>startpoint.js</p></td>
  </tr>
  <tr>
   <td><p>템플릿</p></td>
   <td><p>startpoint.html</p></td>
  </tr>
  <tr>
   <td><p>구성 요소 필요</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>JS 종속성</p></td>
   <td><p>작업 모델</p></td>
  </tr>
  <tr>
   <td><p>수신한 이벤트(이벤트 이름 - 트리거)</p></td>
   <td><p>변경 - 시작점 모델 </p></td>
  </tr>
 </tbody>
</table>

## 시작 프로세스 {#startprocess}

<table>
 <tbody>
  <tr>
   <td><p>모델</p> </td>
   <td><p>categorylist.js</p> </td>
  </tr>
  <tr>
   <td><p>보기</p> </td>
   <td><p>startprocess.js</p> </td>
  </tr>
  <tr>
   <td><p>템플릿</p> </td>
   <td><p>startprocess.html</p> </td>
  </tr>
  <tr>
   <td><p>구성 요소 필요</p> </td>
   <td>
    <ul>
     <li><p>대부분의 유틸리티 클래스</p> </li>
     <li><p>UserSearch</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>JS 종속성</p> </td>
   <td>
    <ul>
     <li><p>범주 모델</p> </li>
     <li><p>favoritecoryfactory 모델</p> </li>
     <li><p>allcategoryfactory 모델</p> </li>
     <li><p>formrendering 유틸리티</p> </li>
     <li><p>참고 유틸리티</p> </li>
     <li><p>첨부 파일 유틸리티</p> </li>
     <li><p>작업 유틸리티</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>수신한 이벤트(이벤트 이름 - 트리거)</p> </td>
   <td>
    <ul>
     <li><p>카테고리:선택됨 - 카테고리목록 모델</p> </li>
     <li><p>change:claikedTask - startpointlist 모델</p> </li>
     <li><p>change:formUrl - 작업 모델</p> </li>
     <li><p>시작점:선택됨 - 시작점 목록 모델</p> </li>
     <li><p>전달 - 작업 모델</p> </li>
     <li><p>포기 - 작업 모델</p> </li>
     <li><p>unlocked - 작업 모델</p> </li>
     <li><p>잠긴 - 작업 모델</p> </li>
     <li>attachmentURLFenzed - 작업 모델</li>
     <li>newAttachment - 작업 모델</li>
     <li>prepareForSubmitComplete - 작업 모델 </li>
     <li><p>submitComplete - 작업 모델</p> </li>
     <li><p>allStartpointsForceed - categorylist 모델</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>StartProcess 및 StartPointList 구성 요소가 모델 클래스를 공유합니다. 이 구성 요소는 StartPointList에서 시작점을 선택하는 것과 관련이 있습니다.

## ProcessNameList {#processnamelist}

<table>
 <tbody>
  <tr>
   <td><p>모델</p></td>
   <td><p>processnamelist.js</p></td>
  </tr>
  <tr>
   <td><p>보기</p></td>
   <td><p>processnamelist.js</p></td>
  </tr>
  <tr>
   <td><p>템플릿</p></td>
   <td><p>tracking.html(경로 폴더)</p></td>
  </tr>
  <tr>
   <td><p>구성 요소 필요</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>JS 종속성</p></td>
   <td><p>프로세스 이름 모델</p></td>
  </tr>
  <tr>
   <td><p>수신한 이벤트(이벤트 이름 - 트리거)</p></td>
   <td>
    <ul>
     <li><p>add - processnamelist 모델 </p></li>
     <li><p>가져온:processnames - processnamelist 모델 </p></li>
     <li><p>변경 - processnamist 모델 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessNameList는 다른 구성 요소에 종속되지 않습니다. 그러나 내부적으로 ProcessInstanceList 모델 클래스에 따라 ProcessInstanceList 모델 클래스와 다른 구성 요소에 따라 달라집니다. 따라서 ProcessNameList는 ProcessInstanceList, ProcessInstance, TaskList, Teamtask 및 Task와 같은 많은 모델 클래스를 사용합니다. 이러한 종속성 외에도 ProcessNameList를 독립적으로 사용할 수 있습니다.

## ProcessName {#processname}

<table>
 <tbody>
  <tr>
   <td><p>모델</p></td>
   <td><p>processname.js</p></td>
  </tr>
  <tr>
   <td><p>보기</p></td>
   <td><p>processname(processnamelist.js에서)</p></td>
  </tr>
  <tr>
   <td><p>템플릿</p></td>
   <td><p>processname.html</p></td>
  </tr>
  <tr>
   <td><p>구성 요소 필요</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>JS 종속성</p></td>
   <td><p>processincelist 모델</p></td>
  </tr>
  <tr>
   <td><p>수신한 이벤트(이벤트 이름 - 트리거)</p></td>
   <td><p>변경 - processname 모델 </p></td>
  </tr>
 </tbody>
</table>

## ProcessInstanceList {#processinstancelist}

<table>
 <tbody>
  <tr>
   <td><p>모델</p></td>
   <td><p>processnamelist.js</p></td>
  </tr>
  <tr>
   <td><p>보기</p></td>
   <td><p>processinstancelist.js</p></td>
  </tr>
  <tr>
   <td><p>템플릿</p></td>
   <td><p>tracking.html(경로 폴더)</p></td>
  </tr>
  <tr>
   <td><p>구성 요소 필요</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>JS 종속성</p></td>
   <td><p>프로세스 이름 모델</p></td>
  </tr>
  <tr>
   <td><p>수신한 이벤트(이벤트 이름 - 트리거)</p></td>
   <td>
    <ul>
     <li><p>processname:selected - processnamelist 모델 </p></li>
     <li><p>processname:instanespeduded - processnamelist 모델 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessInstanceList에는 인스턴스를 가져오고 표시하는 프로세스 이름을 나타내는 ProcessNameList의 이벤트가 필요합니다. ProcessInstanceList를 독립적으로 사용하려면 이벤트 트리거를 별도로 시뮬레이션합니다.

## ProcessInstance {#processinstance}

<table>
 <tbody>
  <tr>
   <td><p>모델</p></td>
   <td><p>processinstance.js</p></td>
  </tr>
  <tr>
   <td><p>보기</p></td>
   <td><p>processnamist.js 내의 processname</p></td>
  </tr>
  <tr>
   <td><p>템플릿</p></td>
   <td><p>processinstance.html</p></td>
  </tr>
  <tr>
   <td><p>구성 요소 필요</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>JS 종속성</p></td>
   <td><p>작업 목록 모델</p></td>
  </tr>
  <tr>
   <td><p>수신한 이벤트(이벤트 이름 - 트리거)</p></td>
   <td><p>변경 - 처리 인스턴스 모델 </p></td>
  </tr>
 </tbody>
</table>

## ProcessInstanceHistory {#processinstancehistory}

<table>
 <tbody>
  <tr>
   <td><p>모델</p></td>
   <td><p>processnamelist.js</p></td>
  </tr>
  <tr>
   <td><p>보기</p></td>
   <td><p>processinstancehistory.js</p></td>
  </tr>
  <tr>
   <td><p>템플릿</p></td>
   <td><p>processinstancehistory.html</p></td>
  </tr>
  <tr>
   <td><p>구성 요소 필요</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>JS 종속성</p></td>
   <td>
    <ul>
     <li><p>프로세스 이름 모델</p></li>
     <li><p>기록 유틸리티</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>수신한 이벤트(이벤트 이름 - 트리거)</p></td>
   <td>
    <ul>
     <li><p>processname:selected - processnamelist 모델 </p></li>
     <li><p>처리 인스턴스:선택됨 - processincelist 모델 </p></li>
     <li><p>tasksConverted - processinstance 모델 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessInstanceHistory는 ProcessInstanceList의 이벤트를 사용하여 어떤 프로세스 인스턴스의 기록을 표시할지를 지정합니다. 이 종속성 외에, 구성 요소는 독립적으로 사용할 수 있습니다.

## OutofOffice {#outofoffice}

<table>
 <tbody>
  <tr>
   <td><p>모델</p> </td>
   <td><p>outofoffice.js</p> </td>
  </tr>
  <tr>
   <td><p>보기</p> </td>
   <td><p>outofoffice.js</p> </td>
  </tr>
  <tr>
   <td><p>템플릿</p> </td>
   <td><p>outofoffice.html</p> </td>
  </tr>
  <tr>
   <td><p>구성 요소 필요</p> </td>
   <td><p>UserSearch</p> </td>
  </tr>
  <tr>
   <td><p>JS 종속성</p> </td>
   <td><p>사용자 검색 보기</p> </td>
  </tr>
  <tr>
   <td><p>수신한 이벤트(이벤트 이름 - 트리거)</p> </td>
   <td>
    <ul>
     <li><p>outOfOfficeSettingsConverted - office 모델</p> </li>
     <li><p>outOfOfficeSettingsSaved - office 모델</p> </li>
     <li><p>processesConverted - Outlook 모델</p> </li>
     <li><p>principalSelected - principalsearch view</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>OutofOffice는 독립적으로 사용할 수 있습니다.

## 공유 큐 {#sharequeue}

<table>
 <tbody>
  <tr>
   <td><p>모델</p> </td>
   <td><p>sharequeue.js</p> </td>
  </tr>
  <tr>
   <td><p>보기</p> </td>
   <td><p>sharequeue.js</p> </td>
  </tr>
  <tr>
   <td><p>템플릿</p> </td>
   <td><p>sharequeue.html</p> </td>
  </tr>
  <tr>
   <td><p>구성 요소 필요</p> </td>
   <td><p>UserSearch</p> </td>
  </tr>
  <tr>
   <td><p>JS 종속성</p> </td>
   <td><p>사용자 검색 보기</p> </td>
  </tr>
  <tr>
   <td><p>수신한 이벤트(이벤트 이름 - 트리거)</p> </td>
   <td>
    <ul>
     <li><p>queueAccessGranted - 공유 큐 모델</p> </li>
     <li><p>queueAccessRequested - 공유 큐 모델</p> </li>
     <li><p>grantedUsersConverted - sharequeue 모델</p> </li>
     <li>accessibleUsersConverted - sharequeue 모델</li>
     <li><p>queueAccessRevocted - 공유 큐 모델</p> </li>
     <li><p>queueAccessRemoved - 공유 큐 모델</p> </li>
     <li><p>principalSelected - principalsearch view</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ShareQueue 는 독립적으로 사용할 수 있습니다.

## UISettings {#uisettings}

<table>
 <tbody>
  <tr>
   <td><p>모델</p></td>
   <td><p>uisettings.js</p></td>
  </tr>
  <tr>
   <td><p>보기</p></td>
   <td><p>uisettings.js</p></td>
  </tr>
  <tr>
   <td><p>템플릿</p></td>
   <td><p>uisettings.html</p></td>
  </tr>
  <tr>
   <td><p>구성 요소 필요</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>JS 종속성</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>수신한 이벤트(이벤트 이름 - 트리거)</p></td>
   <td>
    <ul>
     <li><p>preferencesConverted - 설정 모델 </p></li>
     <li><p>settingUpdated - 설정 모델 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>UISettings 는 독립적으로 사용할 수 있습니다.

## 앱 탐색 {#appnavigation}

<table>
 <tbody>
  <tr>
   <td><p>모델</p></td>
   <td><p>appnavigation.js</p></td>
  </tr>
  <tr>
   <td><p>보기</p></td>
   <td><p>appnavigation.js</p></td>
  </tr>
  <tr>
   <td><p>템플릿</p></td>
   <td><p>appnavigation.html</p></td>
  </tr>
  <tr>
   <td><p>구성 요소 필요</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>JS 종속성</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>이벤트가 수신됨</p></td>
   <td><p>NA</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>AppNavigation은 독립적으로 사용할 수 있습니다.

## UserInfo {#userinfo}

<table>
 <tbody>
  <tr>
   <td><p>모델</p> </td>
   <td><p>userinfo.js</p> </td>
  </tr>
  <tr>
   <td><p>보기</p> </td>
   <td><p>userinfo.js</p> </td>
  </tr>
  <tr>
   <td><p>템플릿</p> </td>
   <td><p>userinfo.html</p> </td>
  </tr>
  <tr>
   <td><p>구성 요소 필요</p> </td>
   <td><p>NA</p> </td>
  </tr>
  <tr>
   <td><p>JS 종속성</p> </td>
   <td><p>NA</p> </td>
  </tr>
  <tr>
   <td><p>수신한 이벤트(이벤트 이름 - 트리거)</p> </td>
   <td>
    <ul>
     <li>userImageUrlPeded - userinfo 모델</li>
     <li>sessionResolified - userinfo 모델 <br /> </li>
     <li>sessionExpired - userinfo 모델 </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>UserInfo는 독립적으로 사용할 수 있습니다.

## WSError {#wserror}

<table>
 <tbody>
  <tr>
   <td><p>모델</p></td>
   <td><p>wserror.js</p></td>
  </tr>
  <tr>
   <td><p>보기</p></td>
   <td><p>wserror.js</p></td>
  </tr>
  <tr>
   <td><p>템플릿</p></td>
   <td><p>wserror.html</p></td>
  </tr>
  <tr>
   <td><p>구성 요소 필요</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>JS 종속성</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>수신한 이벤트(이벤트 이름 - 트리거)</p></td>
   <td><p>newWsError - 미러 모델 </p></td>
  </tr>
 </tbody>
</table>

## UserSearch {#usersearch}

<table>
 <tbody>
  <tr>
   <td><p>모델</p> </td>
   <td><p>usersearch.js</p> </td>
  </tr>
  <tr>
   <td><p>보기</p> </td>
   <td><p>usersearch.js</p> </td>
  </tr>
  <tr>
   <td><p>템플릿</p> </td>
   <td><p>usersearch.html</p> </td>
  </tr>
  <tr>
   <td><p>구성 요소 필요</p> </td>
   <td><p>NA</p> </td>
  </tr>
  <tr>
   <td><p>JS 종속성</p> </td>
   <td><p>NA</p> </td>
  </tr>
  <tr>
   <td><p>수신한 이벤트(이벤트 이름 - 트리거)</p> </td>
   <td>
    <ul>
     <li>principalSearch - principalsearch 모델</li>
     <li>outOfOfficeInfoPeded - usersearch 모델</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## SearchTemplate {#searchtemplate}

<table>
 <tbody>
  <tr>
   <td><p>모델</p> </td>
   <td><p>searchtemplate.js</p> </td>
  </tr>
  <tr>
   <td><p>보기</p> </td>
   <td><p>searchtemplate(searchtemplatelist.js에서) </p> </td>
  </tr>
  <tr>
   <td><p>템플릿</p> </td>
   <td><p>searchtemplate.html</p> </td>
  </tr>
  <tr>
   <td><p>구성 요소 필요</p> </td>
   <td><p>NA</p> </td>
  </tr>
  <tr>
   <td><p>JS 종속성</p> </td>
   <td><p>NA</p> </td>
  </tr>
  <tr>
   <td><p>수신한 이벤트(이벤트 이름 - 트리거)</p> </td>
   <td><p>templateConverted-searchtemplate 모델</p> </td>
  </tr>
 </tbody>
</table>

## SearchTemplateList {#searchtemplatelist}

<table>
 <tbody>
  <tr>
   <td><p>모델</p> </td>
   <td><p>searchtemplatelist.js</p> </td>
  </tr>
  <tr>
   <td><p>보기</p> </td>
   <td><p>searchtemplatelist.js</p> </td>
  </tr>
  <tr>
   <td><p>템플릿</p> </td>
   <td><p>tracking.html(경로 폴더)</p> </td>
  </tr>
  <tr>
   <td><p>구성 요소 필요</p> </td>
   <td><p>NA</p> </td>
  </tr>
  <tr>
   <td><p>JS 종속성</p> </td>
   <td><p>검색 템플릿 모델</p> </td>
  </tr>
  <tr>
   <td><p>수신한 이벤트(이벤트 이름 - 트리거)</p> </td>
   <td><p>변경 - searchtemplatelist 모델</p> </td>
  </tr>
 </tbody>
</table>

## SearchTemplateDetails {#searchtemplatedetails}

<table>
 <tbody>
  <tr>
   <td><p>모델</p> </td>
   <td><p>searchtemplatelist.js</p> </td>
  </tr>
  <tr>
   <td><p>보기</p> </td>
   <td><p>searchtemplatedetails.js</p> </td>
  </tr>
  <tr>
   <td><p>템플릿</p> </td>
   <td><p>searchtemplatedetails.html</p> </td>
  </tr>
  <tr>
   <td><p>구성 요소 필요</p> </td>
   <td><p>NA</p> </td>
  </tr>
  <tr>
   <td><p>JS 종속성</p> </td>
   <td>NA<br /> </td>
  </tr>
  <tr>
   <td><p>수신한 이벤트(이벤트 이름 - 트리거)</p> </td>
   <td><p>searchTemplate:selected - searchtemplate model</p> </td>
  </tr>
 </tbody>
</table>
