---
title: 재사용 가능한 구성 요소에 대한 설명
description: 파일 이름과 종속성이 포함된 재사용 가능한 구성 요소의 전체 목록으로, 웹 애플리케이션에서 AEM Forms 작업 공간 구성 요소를 통합할 수 있습니다.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: b8cb7233-3d9e-41d4-85c5-8e8c2481f89c
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '1231'
ht-degree: 9%

---

# 재사용 가능한 구성 요소에 대한 설명 {#description-of-reusable-components}

AEM Forms 작업 영역은 다음으로 구성됩니다. [재사용 가능](/help/forms/using/integrating-html-ws-components-web.md) 특정 구성 요소로 구성된 구성 요소 [폴더 구조](/help/forms/using/folder-structure.md) CRX™. 각 구성 요소에는 폴더 구조에 지정된 위치에 모델, 보기 및 템플릿 파일이 있으며, JavaScript™은 다른 구성 요소 파일에 대한 종속성, 구성 요소가 수신하는 이벤트 및 AEM Forms 작업 영역에서 이러한 이벤트를 트리거하는 JavaScript 개체가 있습니다. 여기에 구성 파일 이름 및 종속성을 포함하여 재사용 가능한 구성 요소의 전체 목록이 제공됩니다.

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
     <li><p>사용자 검색</p></li>
     <li><p>작업</p></li>
     <li><p>Teamtask</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>JS 종속성</p></td>
   <td>
    <ul>
     <li><p>작업 모델</p></li>
     <li><p>teamtask 모델</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>이벤트 수신(이벤트 이름 - 트리거)</p></td>
   <td>
    <ul>
     <li><p>filterSelected - 작업 목록 모델</p></li>
     <li><p>제거 - 작업 목록 모델</p></li>
     <li><p>updateQueue - 작업 목록 모델</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>사용자 지정 애플리케이션에서 이 구성 요소에 대한 filterSelected 이벤트를 트리거하는 경우 이 구성 요소는 AEM Forms 작업 영역과 독립적으로 사용할 수 있습니다.

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
   <td><p>이벤트 수신(이벤트 이름 - 트리거)</p></td>
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
>작업 영역은 TaskList 모델의 fetchTasks 함수를 호출하여 이 구성 요소에 대한 작업 모델을 생성합니다.

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
   <td><p>이벤트 수신(이벤트 이름 - 트리거)</p></td>
   <td>
    <ul>
     <li><p>가져옴 - 작업 목록 모델 </p></li>
     <li><p>제거 - 작업 목록 모델 </p></li>
     <li><p>updateQueue - 작업 목록 모델 </p></li>
     <li><p>refreshedQueue - 작업 목록 모델 </p></li>
     <li><p>filterSelected - 작업 목록 모델</p></li>
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
     <li><p>필드: 대기열: { name, qid, isDefault, type}</p> </li>
     <li><p>필드: 쿼리: 문자열</p> </li>
     <li><p>필드: parentView: 필터 목록 보기</p> </li>
     <li><p>필드: parentModel: tasklist 모델</p> </li>
     <li><p>필드: 유틸리티</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>이벤트 청취됨</p> </td>
   <td><p>NA</p> </td>
  </tr>
 </tbody>
</table>

## 팀 큐 {#teamqueues}

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
   <td><p>이벤트 수신(이벤트 이름 - 트리거)</p></td>
   <td>
    <ul>
     <li><p>가져옴 - 작업 목록 모델 </p></li>
     <li><p>제거 - 작업 목록 모델 </p></li>
     <li><p>updateQueue - 작업 목록 모델 </p></li>
     <li><p>teamQueuesFetched - 작업 목록 모델 </p></li>
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
     <li><p>필드 : 큐 :{ name, qid, isDefault, type }</p> </li>
     <li><p>필드 : 쿼리 : 문자열</p> </li>
     <li><p>필드 : parentView : 필터링 목록 보기</p> </li>
     <li><p>필드 : parentModel : tasklist 모델</p> </li>
     <li><p>필드 : 유틸리티</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>이벤트 청취됨</p> </td>
   <td><p>NA</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>TeamFilter는 TaskList 구성 요소에서 선택한 작업을 나타내는 이벤트를 가져옵니다. 이러한 구성 요소는 모델 클래스를 공유하지만 다른 종속성은 없습니다.

## 작업 세부 정보 {#taskdetails}

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
     <li><p>notes 유틸리티</p> </li>
     <li><p>첨부 파일 유틸리티</p> </li>
     <li><p>작업 유틸리티</p> </li>
     <li><p>기록 유틸리티</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>이벤트 수신(이벤트 이름 - 트리거)</p> </td>
   <td>
    <ul>
     <li><p>전달됨 - 작업 모델</p> </li>
     <li><p>공유 - 작업 모델</p> </li>
     <li><p>참조 - 작업 모델</p> </li>
     <li><p>거부됨 - 작업 모델</p> </li>
     <li><p>중단됨 - 작업 모델</p> </li>
     <li><p>잠금 해제됨 - 작업 모델</p> </li>
     <li><p>잠김 - 작업 모델</p> </li>
     <li><p>클레임됨 - 작업 모델</p> </li>
     <li><p>변경:taskselected - 작업 목록 모델</p> </li>
     <li><p>change:formUrl - 작업 모델</p> </li>
     <li>attachmentURLFetched - 작업 모델</li>
    </ul>
    <ul>
     <li>newAttachment - 작업 모델</li>
     <li><p>taskHistoryFetch - 작업 모델</p> </li>
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
   <td><p>startprocess.html(경로 폴더 내)</p></td>
  </tr>
  <tr>
   <td><p>구성 요소 필요</p></td>
   <td><p>범주</p></td>
  </tr>
  <tr>
   <td><p>JS 종속성</p></td>
   <td>
    <ul>
     <li><p>즐겨찾기범주팩토리 모델</p></li>
     <li><p>allcategoryfactory 모델</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>이벤트 수신(이벤트 이름 - 트리거)</p></td>
   <td>
    <ul>
     <li><p>allStartpointsFetch - categorylist 모델 </p></li>
     <li><p>추가 - categorylist 모델 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>이 구성 요소는 StartPointList, StartPoint 및 Task와 같은 다른 구성 요소의 모델 클래스를 사용합니다. 이 종속성 외에 CategoryList는 독립적으로 사용할 수 있습니다.

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
   <td><p>이벤트 수신(이벤트 이름 - 트리거)</p></td>
   <td>
    <ul>
     <li><p>변경됨 - 범주 모델 </p></li>
     <li><p>childrenFetch - 범주 모델 </p></li>
     <li><p>category:selected - categorylist 모델 </p></li>
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
   <td><p>startprocess.html(경로 폴더 내)</p></td>
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
     <li><p>즐겨찾기범주팩토리 모델</p></li>
     <li><p>allcategoryfactory 모델</p></li>
     <li><p>시작 지점 보기</p></li>
     <li><p>startpointlist 모델</p></li>
     <li><p>시작점 모델</p></li>
     <li><p>작업 모델</p></li>
     <li><p>작업 모델</p></li>
     <li><p>작업 목록 모델</p></li>
     <li><p>teamtask 모델</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>이벤트 수신(이벤트 이름 - 트리거)</p></td>
   <td>
    <ul>
     <li><p>category:selected - categorylist 모델 </p></li>
     <li><p>allStartpointsFetch - categorylist 모델 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>StartPointList 및 CategoryList 구성 요소는 모델 클래스를 공유하므로 전자는 후자에 따라 다릅니다. CategoryList는 표시되는 카테고리의 시작 지점에 대한 정보에 액세스합니다. StartPointList를 독립적으로 사용하려면 CategoryList에서 이벤트 트리거를 시뮬레이션합니다.

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
   <td><p>이벤트 수신(이벤트 이름 - 트리거)</p></td>
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
     <li><p>사용자 검색</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>JS 종속성</p> </td>
   <td>
    <ul>
     <li><p>범주 모델</p> </li>
     <li><p>즐겨찾기범주팩토리 모델</p> </li>
     <li><p>allcategoryfactory 모델</p> </li>
     <li><p>formrendering 유틸리티</p> </li>
     <li><p>notes 유틸리티</p> </li>
     <li><p>첨부 파일 유틸리티</p> </li>
     <li><p>작업 유틸리티</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>이벤트 수신(이벤트 이름 - 트리거)</p> </td>
   <td>
    <ul>
     <li><p>category:selected - categorylist 모델</p> </li>
     <li><p>change:invokedTask - startpointlist 모델</p> </li>
     <li><p>change:formUrl - 작업 모델</p> </li>
     <li><p>startpoint:selected - startpointlist 모델</p> </li>
     <li><p>전달됨 - 작업 모델</p> </li>
     <li><p>중단됨 - 작업 모델</p> </li>
     <li><p>잠금 해제됨 - 작업 모델</p> </li>
     <li><p>잠김 - 작업 모델</p> </li>
     <li>attachmentURLFetched - 작업 모델</li>
     <li>newAttachment - 작업 모델</li>
     <li>prepareForSubmitComplete - 작업 모델 </li>
     <li><p>submitComplete - 작업 모델</p> </li>
     <li><p>allStartpointsFetch - categorylist 모델</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>StartProcess 및 StartPointList 구성 요소는 모델 클래스를 공유합니다. 이 구성 요소는 StartPointList에서 시작점을 선택하는 것과 관련이 있습니다.

## 프로세스 이름 목록 {#processnamelist}

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
   <td><p>tracking.html (route 폴더)</p></td>
  </tr>
  <tr>
   <td><p>구성 요소 필요</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>JS 종속성</p></td>
   <td><p>processname 모델</p></td>
  </tr>
  <tr>
   <td><p>이벤트 수신(이벤트 이름 - 트리거)</p></td>
   <td>
    <ul>
     <li><p>add - processnamelist 모델 </p></li>
     <li><p>가져온:processnames - processnamelist 모델 </p></li>
     <li><p>변경 - processnamelist 모델 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessNameList는 다른 구성 요소에 종속되지 않습니다. 그러나 내부적으로 ProcessInstanceList 모델 클래스에 따라 다르며, 이 클래스는 다른 구성 요소에 따라 다릅니다. 따라서 ProcessNameList는 ProcessInstanceList, ProcessInstance, TaskList, Teamtask 및 Task와 같은 많은 모델 클래스를 사용합니다. 이러한 종속성 외에 ProcessNameList는 독립적으로 사용할 수 있습니다.

## 프로세스 이름 {#processname}

<table>
 <tbody>
  <tr>
   <td><p>모델</p></td>
   <td><p>processname.js</p></td>
  </tr>
  <tr>
   <td><p>보기</p></td>
   <td><p>processname(processnamelist.js)</p></td>
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
   <td><p>processinstancelist 모델</p></td>
  </tr>
  <tr>
   <td><p>이벤트 수신(이벤트 이름 - 트리거)</p></td>
   <td><p>변경 - processname 모델 </p></td>
  </tr>
 </tbody>
</table>

## 프로세스 인스턴스 목록 {#processinstancelist}

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
   <td><p>tracking.html (route 폴더)</p></td>
  </tr>
  <tr>
   <td><p>구성 요소 필요</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>JS 종속성</p></td>
   <td><p>processname 모델</p></td>
  </tr>
  <tr>
   <td><p>이벤트 수신(이벤트 이름 - 트리거)</p></td>
   <td>
    <ul>
     <li><p>processname:selected - processnamelist 모델 </p></li>
     <li><p>processname:instancesefetch - processnamelist 모델 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessInstanceList에는 인스턴스를 가져오고 표시할 프로세스 이름을 나타내는 ProcessNameList의 이벤트가 필요합니다. ProcessInstanceList를 독립적으로 사용하려면 이벤트 트리거를 개별적으로 시뮬레이트합니다.

## 프로세스 인스턴스 {#processinstance}

<table>
 <tbody>
  <tr>
   <td><p>모델</p></td>
   <td><p>processinstance.js</p></td>
  </tr>
  <tr>
   <td><p>보기</p></td>
   <td><p>processnamelist.js 내의 processname</p></td>
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
   <td><p>이벤트 수신(이벤트 이름 - 트리거)</p></td>
   <td><p>변경 - 프로세스 인스턴스 모델 </p></td>
  </tr>
 </tbody>
</table>

## 프로세스 인스턴스 내역 {#processinstancehistory}

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
     <li><p>processname 모델</p></li>
     <li><p>기록 유틸리티</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>이벤트 수신(이벤트 이름 - 트리거)</p></td>
   <td>
    <ul>
     <li><p>processname:selected - processnamelist 모델 </p></li>
     <li><p>processinstance:selected - processinstancelist 모델 </p></li>
     <li><p>tasksFetch - processinstance 모델 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessInstanceHistory에서는 표시할 프로세스 인스턴스의 내역을 나타내는 ProcessInstanceList의 이벤트가 필요합니다. 이 종속성 외에 구성 요소를 독립적으로 사용할 수 있습니다.

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
   <td><p>사용자 검색</p> </td>
  </tr>
  <tr>
   <td><p>JS 종속성</p> </td>
   <td><p>사용자 검색 보기</p> </td>
  </tr>
  <tr>
   <td><p>이벤트 수신(이벤트 이름 - 트리거)</p> </td>
   <td>
    <ul>
     <li><p>outOfOfficeSettingsFetched - outofoffice 모델</p> </li>
     <li><p>outOfOfficeSettingsSaved - outofoffice 모델</p> </li>
     <li><p>processesFetched - outofoffice 모델</p> </li>
     <li><p>principalSelected - principalsearch 보기</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>OutofOffice는 독립적으로 사용할 수 있습니다.

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
   <td><p>사용자 검색</p> </td>
  </tr>
  <tr>
   <td><p>JS 종속성</p> </td>
   <td><p>사용자 검색 보기</p> </td>
  </tr>
  <tr>
   <td><p>이벤트 수신(이벤트 이름 - 트리거)</p> </td>
   <td>
    <ul>
     <li><p>queueAccessGranted - 공유 모델</p> </li>
     <li><p>queueAccessRequested - 공유 모델</p> </li>
     <li><p>grantedUsersFetch - 공유 모델</p> </li>
     <li>accessibleUsersFetch - 공유 모델</li>
     <li><p>queueAccessRevocated - 공유 모델</p> </li>
     <li><p>queueAccessRemoved - 공유 모델</p> </li>
     <li><p>principalSelected - principalsearch 보기</p> </li>
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
   <td><p>이벤트 수신(이벤트 이름 - 트리거)</p></td>
   <td>
    <ul>
     <li><p>preferencesFetch - uisettings 모델 </p></li>
     <li><p>settingUpdated - uisettings 모델 </p></li>
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
   <td><p>이벤트 청취됨</p></td>
   <td><p>NA</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>AppNavigation은 독립적으로 사용할 수 있습니다.

## 사용자 정보 {#userinfo}

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
   <td><p>이벤트 수신(이벤트 이름 - 트리거)</p> </td>
   <td>
    <ul>
     <li>userImageUrlFetch - userinfo 모델</li>
     <li>sessionRenewed - 사용자 정보 모델 <br /> </li>
     <li>sessionExpired - 사용자 정보 모델 </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>UserInfo는 독립적으로 사용할 수 있습니다.

## WSEerror {#wserror}

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
   <td><p>이벤트 수신(이벤트 이름 - 트리거)</p></td>
   <td><p>newWsError - wserror 모델 </p></td>
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
   <td><p>이벤트 수신(이벤트 이름 - 트리거)</p> </td>
   <td>
    <ul>
     <li>principalSearched - principalsearch 모델</li>
     <li>outOfOfficeInfoFetch - usersearch 모델</li>
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
   <td><p>searchtemplate (searchtemplatelist.js) </p> </td>
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
   <td><p>이벤트 수신(이벤트 이름 - 트리거)</p> </td>
   <td><p>templateFetched- searchtemplate 모델</p> </td>
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
   <td><p>tracking.html (route 폴더)</p> </td>
  </tr>
  <tr>
   <td><p>구성 요소 필요</p> </td>
   <td><p>NA</p> </td>
  </tr>
  <tr>
   <td><p>JS 종속성</p> </td>
   <td><p>searchtemplate 모델</p> </td>
  </tr>
  <tr>
   <td><p>이벤트 수신(이벤트 이름 - 트리거)</p> </td>
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
   <td>해당 없음<br /> </td>
  </tr>
  <tr>
   <td><p>이벤트 수신(이벤트 이름 - 트리거)</p> </td>
   <td><p>searchTemplate:selected - searchtemplate 모델</p> </td>
  </tr>
 </tbody>
</table>
