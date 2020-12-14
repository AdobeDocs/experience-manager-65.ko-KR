---
title: 재사용 가능한 구성 요소에 대한 설명
seo-title: 재사용 가능한 구성 요소에 대한 설명
description: 웹 애플리케이션에서 AEM Forms 작업 영역 구성 요소를 통합하는 데 도움이 되는 파일 이름 및 종속성이 있는 재사용 가능한 구성 요소의 전체 목록입니다.
seo-description: 웹 애플리케이션에서 AEM Forms 작업 영역 구성 요소를 통합하는 데 도움이 되는 파일 이름 및 종속성이 있는 재사용 가능한 구성 요소의 전체 목록입니다.
uuid: 8e6accc7-0935-4d7b-b838-d23676df5cda
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: d3facd17-ceb0-4799-8cd9-ff9e81e09793
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '1257'
ht-degree: 9%

---


# 재사용 가능한 구성 요소 {#description-of-reusable-components} 설명

AEM Forms 작업 영역은 CRX™의 특정 [폴더 구조](/help/forms/using/folder-structure.md)로 구성된 [재사용 가능한](/help/forms/using/integrating-html-ws-components-web.md) 구성 요소로 구성됩니다. 각 구성 요소에는 폴더 구조에 지정된 위치에 모델, 보기 및 템플릿 파일, 다른 구성 요소 파일에 대한 JavaScript™ 종속성, 구성 요소가 수집한 이벤트 및 AEM Forms 작업 공간에서 이러한 이벤트를 트리거하는 JavaScript 객체가 있습니다. 구성 파일 이름 및 종속성이 있는 재사용 가능한 구성 요소의 전체 목록은 여기에 나와 있습니다.

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
   <td><p>경청된 이벤트(이벤트 이름 - 트리거)</p></td>
   <td>
    <ul>
     <li><p>filterSelected - tasklist 모델</p></li>
     <li><p>제거 - 작업 목록 모델</p></li>
     <li><p>updateQueue - tasklist 모델</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>사용자 지정 애플리케이션에서 이 구성 요소에 대해 filterSelected 이벤트를 트리거하는 경우 이 구성 요소는 AEM Forms 작업 영역과 별도로 사용할 수 있습니다.

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
   <td><p>경청된 이벤트(이벤트 이름 - 트리거)</p></td>
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
>작업 공간 호출은 이 구성 요소에 대한 작업 모델을 만들기 위해 TaskList 모델의 fetchTasks 함수를 호출합니다.

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
   <td><p>경청된 이벤트(이벤트 이름 - 트리거)</p></td>
   <td>
    <ul>
     <li><p>가져오기 - 작업 목록 모델 </p></li>
     <li><p>제거 - 작업 목록 모델 </p></li>
     <li><p>updateQueue - tasklist 모델 </p></li>
     <li><p>refreshQueue - tasklist 모델 </p></li>
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
     <li><p>필드:대기열:{ name, qid, isDefault, type}</p> </li>
     <li><p>필드:쿼리:문자열</p> </li>
     <li><p>필드:parentView:필터 목록 보기</p> </li>
     <li><p>필드:parentModel:작업 목록 모델</p> </li>
     <li><p>필드:유틸리티</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>이벤트가 경청됨</p> </td>
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
   <td><p>경청된 이벤트(이벤트 이름 - 트리거)</p></td>
   <td>
    <ul>
     <li><p>가져오기 - 작업 목록 모델 </p></li>
     <li><p>제거 - 작업 목록 모델 </p></li>
     <li><p>updateQueue - tasklist 모델 </p></li>
     <li><p>teamQueuesConcepted - tasklist 모델 </p></li>
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
     <li><p>확장:필터 보기</p> </li>
     <li><p>필드:queue :{ name, qid, isDefault, type }</p> </li>
     <li><p>필드:query :문자열</p> </li>
     <li><p>필드:parentView :필터 목록 보기</p> </li>
     <li><p>필드:parentModel :작업 목록 모델</p> </li>
     <li><p>필드:유틸리티</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>이벤트가 경청됨</p> </td>
   <td><p>NA</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>TeamFilter는 TaskList 구성 요소에서 선택한 작업을 나타내는 이벤트를 가져옵니다. 이러한 구성 요소는 모델 클래스를 공유하지만 다른 종속성은 없습니다.

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
     <li><p>formrendering utility</p> </li>
     <li><p>메모 유틸리티</p> </li>
     <li><p>첨부 파일 유틸리티</p> </li>
     <li><p>작업 유틸리티</p> </li>
     <li><p>작업 내역 유틸리티</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>경청된 이벤트(이벤트 이름 - 트리거)</p> </td>
   <td>
    <ul>
     <li><p>전달 - 작업 모델</p> </li>
     <li><p>공유 - 작업 모델</p> </li>
     <li><p>상담 - 작업 모델</p> </li>
     <li><p>거부됨 - 작업 모델</p> </li>
     <li><p>중단된 - 작업 모델</p> </li>
     <li><p>잠금 해제 - 작업 모델</p> </li>
     <li><p>잠김 - 작업 모델</p> </li>
     <li><p>claim - 작업 모델</p> </li>
     <li><p>변경:작업 선택 - 작업 목록 모델</p> </li>
     <li><p>change:formUrl - 작업 모델</p> </li>
     <li>attachmentURLFlocked - 작업 모델</li>
    </ul>
    <ul>
     <li>newAttachment - 작업 모델</li>
     <li><p>taskHistoryConcepted - 작업 모델</p> </li>
     <li>prepareForSubmitComplete - 작업 모델</li>
     <li><p>submitComplete - 작업 모델</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## CategoryList {#categorylist}

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
   <td><p>카테고리</p></td>
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
   <td><p>경청된 이벤트(이벤트 이름 - 트리거)</p></td>
   <td>
    <ul>
     <li><p>allStartpointsConcepted - categorylist model </p></li>
     <li><p>add - categorylist model </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>이 구성 요소는 StartPointList, StartPoint 및 Task와 같은 다른 구성 요소의 모델 클래스를 사용합니다. 이러한 종속성 외에도 CategoryList를 독립적으로 사용할 수 있습니다.

## 카테고리 {#category}

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
     <li><p>시작점 목록 모델</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>경청된 이벤트(이벤트 이름 - 트리거)</p></td>
   <td>
    <ul>
     <li><p>변경 - 카테고리 모델 </p></li>
     <li><p>childrenBraced - 범주 모델 </p></li>
     <li><p>범주:선택됨 - 범주목록 모델 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

## StartPointList {#startpointlist}

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
     <li><p>시작점 목록 모델</p></li>
     <li><p>시작점 모델</p></li>
     <li><p>작업 모델</p></li>
     <li><p>작업 모델</p></li>
     <li><p>작업 목록 모델</p></li>
     <li><p>팀 작업 모델</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>경청된 이벤트(이벤트 이름 - 트리거)</p></td>
   <td>
    <ul>
     <li><p>범주:선택됨 - 범주목록 모델 </p></li>
     <li><p>allStartpointsConcepted - categorylist model </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>StartPointList 및 CategoryList 구성 요소는 모델 클래스를 공유하므로 모델 클래스는 후자에 따라 달라집니다. CategoryList는 카테고리의 시작 지점이 표시되는 정보에 액세스합니다. StartPointList를 독립적으로 사용하려면 CategoryList에서 이벤트 트리거를 시뮬레이션합니다.

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
   <td><p>경청된 이벤트(이벤트 이름 - 트리거)</p></td>
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
     <li><p>formrendering utility</p> </li>
     <li><p>메모 유틸리티</p> </li>
     <li><p>첨부 파일 유틸리티</p> </li>
     <li><p>작업 유틸리티</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>경청된 이벤트(이벤트 이름 - 트리거)</p> </td>
   <td>
    <ul>
     <li><p>범주:선택됨 - 범주목록 모델</p> </li>
     <li><p>change:includedTask - startpointlist model</p> </li>
     <li><p>change:formUrl - 작업 모델</p> </li>
     <li><p>시작점:선택됨 - 시작점 목록 모델</p> </li>
     <li><p>전달 - 작업 모델</p> </li>
     <li><p>중단된 - 작업 모델</p> </li>
     <li><p>잠금 해제 - 작업 모델</p> </li>
     <li><p>잠김 - 작업 모델</p> </li>
     <li>attachmentURLFlocked - 작업 모델</li>
     <li>newAttachment - 작업 모델</li>
     <li>prepareForSubmitComplete - 작업 모델 </li>
     <li><p>submitComplete - 작업 모델</p> </li>
     <li><p>allStartpointsConcepted - categorylist model</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>StartProcess 및 StartPointList 구성 요소는 모델 클래스를 공유합니다. 이 구성 요소는 StartPointList에서 시작점을 선택하는 것과 관련이 있습니다.

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
   <td><p>처리 모델</p></td>
  </tr>
  <tr>
   <td><p>경청된 이벤트(이벤트 이름 - 트리거)</p></td>
   <td>
    <ul>
     <li><p>add - processnamelist 모델 </p></li>
     <li><p>가져오기:처리 이름 - 처리 이름 목록 모델 </p></li>
     <li><p>변경 - 프로세서 이름 목록 모델 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessNameList는 다른 구성 요소에 종속되지 않습니다. 하지만 내부적으로 다른 구성 요소에 따라 달라지는 ProcessInstanceList 모델 클래스에 따라 달라집니다. 따라서 ProcessNameList는 ProcessInstanceList, ProcessInstance, TaskList, Teamtask 및 Task와 같은 많은 모델 클래스를 사용합니다. 이러한 종속성 외에도 ProcessNameList를 독립적으로 사용할 수 있습니다.

## 프로세스 이름 {#processname}

<table>
 <tbody>
  <tr>
   <td><p>모델</p></td>
   <td><p>processname.js</p></td>
  </tr>
  <tr>
   <td><p>보기</p></td>
   <td><p>processname(processname.js에서)</p></td>
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
   <td><p>처리(instancelist) 모델</p></td>
  </tr>
  <tr>
   <td><p>경청된 이벤트(이벤트 이름 - 트리거)</p></td>
   <td><p>변경 - 처리 이름 모델 </p></td>
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
   <td><p>처리 모델</p></td>
  </tr>
  <tr>
   <td><p>경청된 이벤트(이벤트 이름 - 트리거)</p></td>
   <td>
    <ul>
     <li><p>처리 이름:선택됨 - 처리 이름 모델 </p></li>
     <li><p>처리 이름:instancenespeconeded - 처리 이름 모델 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessInstanceList는 인스턴스를 가져오고 표시하기 위한 프로세스 이름을 나타내는 ProcessNameList의 이벤트가 필요합니다. ProcessInstanceList를 독립적으로 사용하려면 이벤트 트리거를 별도로 시뮬레이트합니다.

## ProcessInstance {#processinstance}

<table>
 <tbody>
  <tr>
   <td><p>모델</p></td>
   <td><p>processinstance.js</p></td>
  </tr>
  <tr>
   <td><p>보기</p></td>
   <td><p>processname alist.js 내의 프로세스 이름</p></td>
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
   <td><p>경청된 이벤트(이벤트 이름 - 트리거)</p></td>
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
     <li><p>처리 모델</p></li>
     <li><p>작업 내역 유틸리티</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>경청된 이벤트(이벤트 이름 - 트리거)</p></td>
   <td>
    <ul>
     <li><p>처리 이름:선택됨 - 처리 이름 모델 </p></li>
     <li><p>처리 인스턴스:선택됨 - 처리기팔레트 모델 </p></li>
     <li><p>tasksPected - 처리 인스턴스 모델 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessInstanceHistory는 프로세스 인스턴스의 내역을 표시할 프로세스를 나타내는 ProcessInstanceList의 이벤트를 필요로 합니다. 이 종속성 외에도 구성 요소를 독립적으로 사용할 수 있습니다.

## OoofOffice {#outofoffice}

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
   <td><p>경청된 이벤트(이벤트 이름 - 트리거)</p> </td>
   <td>
    <ul>
     <li><p>outOfOfficeSettingsConcted - Otofoffice 모델</p> </li>
     <li><p>outOfOfficeSettingsSaved - Otofoffice 모델</p> </li>
     <li><p>processesConcepted - Otofoffice 모델</p> </li>
     <li><p>principalSelected - principalsearch view</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>OofOffice는 독립적으로 사용할 수 있습니다.

## ShareQueue {#sharequeue}

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
   <td><p>경청된 이벤트(이벤트 이름 - 트리거)</p> </td>
   <td>
    <ul>
     <li><p>queueAccessGranted - 공유 큐 모델</p> </li>
     <li><p>queueAccessRequested - 공유 큐 모델</p> </li>
     <li><p>grantedUsersConceed - sharequeue 모델</p> </li>
     <li>accessibleUsersConcepted - sharequeue 모델</li>
     <li><p>queueAccessRevoected - 공유 큐 모델</p> </li>
     <li><p>queueAccessRemoved - 공유 큐 모델</p> </li>
     <li><p>principalSelected - principalsearch view</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ShareQueue는 독립적으로 사용할 수 있습니다.

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
   <td><p>경청된 이벤트(이벤트 이름 - 트리거)</p></td>
   <td>
    <ul>
     <li><p>preferencesBraced - 설정 모델 </p></li>
     <li><p>settingUpdated - 설정 모델 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>UISettings는 독립적으로 사용할 수 있습니다.

## AppNavigation {#appnavigation}

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
   <td><p>이벤트가 경청됨</p></td>
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
   <td><p>경청된 이벤트(이벤트 이름 - 트리거)</p> </td>
   <td>
    <ul>
     <li>userImageUrlConcepted - userinfo 모델</li>
     <li>sessionRelated - userinfo 모델 <br /> </li>
     <li>sessionExpired - 사용자 정보 모델 </li>
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
   <td><p>경청된 이벤트(이벤트 이름 - 트리거)</p></td>
   <td><p>newWsError - 오류 모델 </p></td>
  </tr>
 </tbody>
</table>

## 사용자 검색 {#usersearch}

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
   <td><p>경청된 이벤트(이벤트 이름 - 트리거)</p> </td>
   <td>
    <ul>
     <li>principalSearch - principalsearch 모델</li>
     <li>outOfOfficeInfoConcepted - 사용자 검색 모델</li>
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
   <td><p>경청된 이벤트(이벤트 이름 - 트리거)</p> </td>
   <td><p>templateContated- searchtemplate 모델</p> </td>
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
   <td><p>경청된 이벤트(이벤트 이름 - 트리거)</p> </td>
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
   <td><p>경청된 이벤트(이벤트 이름 - 트리거)</p> </td>
   <td><p>searchTemplate:selected - 검색 템플릿 모델</p> </td>
  </tr>
 </tbody>
</table>
