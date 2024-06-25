---
title: AEM Forms 작업 영역 JSON 개체 설명
description: 사용자 지정, 확장, 수정 및 재사용을 위해 AEM Forms 작업 영역 LiveCycle에 사용되는 JSON JavaScript 개체에 대한 개념 정보입니다.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: f837a2b3-4650-4261-84c6-291bb2a46dc7
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '2144'
ht-degree: 8%

---

# AEM Forms 작업 영역 JSON 개체 설명 {#aem-forms-workspace-json-object-description}

AEM Forms 작업 영역에서 사용되는 JSON 개체는 아래에 설명되어 있습니다.

1. 범주

   범주는 작업 영역의 시작 프로세스 탭에 있습니다. 이러한 범주는 시작점을 분류하는 데 사용됩니다.

<table>
 <tbody>
  <tr>
   <td><strong>속성</strong></td>
   <td><strong>클라이언트만</strong></td>
   <td><strong>댓글</strong></td>
  </tr>
  <tr>
   <td>이름</td>
   <td>금</td>
   <td>카테고리 이름</td>
  </tr>
  <tr>
   <td>id</td>
   <td>금</td>
   <td>범주 ID<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>설명<br type="_moz" /> </td>
   <td>금</td>
   <td>범주 설명<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>parentId<br type="_moz" /> </td>
   <td>금</td>
   <td>상위 범주의 oid를 포함합니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>시작 지점 목록<br type="_moz" /> </td>
   <td>화</td>
   <td>범주에 있는 모든 시작 지점 목록을 포함합니다.</td>
  </tr>
  <tr>
   <td>범주 목록</td>
   <td>화</td>
   <td>범주의 직접 하위 범주 목록을 포함합니다.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>모든 시작 지점 및 즐겨찾기는 클라이언트측에 정의된 카테고리입니다. 즐겨찾기 카테고리에는 사용자가 즐겨찾기로 표시한 모든 시작 지점이 포함되어 있습니다. 모든 시작 지점 카테고리는 모든 시작 지점을 포함합니다.

1. 시작점

   시작점은 호출될 때 작업공간에서 프로세스를 시작하는 데 사용됩니다.

   | **속성** | **클라이언트만** | **댓글** |
   |---|---|---|
   | categoryId | 금 | 여기에는 시작 지점이 속한 카테고리의 ID가 포함됩니다. |
   | 설명 | 금 | 시작점에 대한 설명이 포함되어 있습니다. |
   | 이름 | 금 | 시작점의 이름이 포함되어 있습니다. |
   | serializedImageTicket | 금 | 시작점에 해당하는 이미지 티켓이 포함되어 있습니다. 이 이미지 티켓은 서버에서 startpoint의 이미지를 가져오기 위해 startpoint의 imageUrl 필드에 사용됩니다. |
   | serviceName | 금 | 시작점에 대한 서비스 이름이 포함되어 있습니다. |
   | startpointId | 금 | 시작 지점 ID가 포함되어 있습니다. |
   | isFavorite | 화 | 시작 지점이 즐겨찾기인지 여부를 나타냅니다. Startpoint가 Favorite이면 True이고, 그렇지 않으면 False입니다. |
   | isDefaultImage | 화 | 프로세스에 대해 지정된 이미지가 있는지 여부를 나타냅니다. 프로세스와 연결된 이미지가 없으면 True이고, 그렇지 않으면 false입니다. |
   | 작업 | 화 | 시작 지점이 호출될 때 생성된 작업이 포함됩니다. |
   | imageUrl | 화 | 시작점에 해당하는 이미지의 URL이 포함되어 있습니다. |

1. 작업

   작업은 사용자/그룹에 할당되며 데이터로 채울 수 있는 사용자 인터페이스(양식 또는 안내서(더 이상 사용되지 않음))를 포함합니다. 사용자에게 작업이 할당되면 작성 및 제출하기 위한 양식 또는 안내서가 제공됩니다.

<table>
 <tbody>
  <tr>
   <td>속성<br /> </td>
   <td>클라이언트만<br /> </td>
   <td>댓글<br /> </td>
  </tr>
  <tr>
   <td>classOfTask</td>
   <td>금</td>
   <td>작업이 lc8 작업 또는 "표준"인 경우 작업 클래스는 "LC8"입니다.<br /> </td>
  </tr>
  <tr>
   <td>completeTime<br /> </td>
   <td>금</td>
   <td>여기에는 작업이 완료될 때의 타임스탬프가 포함됩니다.<br /> </td>
  </tr>
  <tr>
   <td>consultGroupId<br /> </td>
   <td>금</td>
   <td>여기에는 작업을 참조할 수 있는 그룹의 ID가 포함되어 있습니다. 이는 프로세스 설계 중에 설정됩니다.<br /> </td>
  </tr>
  <tr>
   <td>createTime<br /> </td>
   <td>금</td>
   <td>여기에는 작업이 생성될 때의 타임스탬프가 포함됩니다.<br /> </td>
  </tr>
  <tr>
   <td>creationId<br /> </td>
   <td>금</td>
   <td>여기에는 작업을 만든 사용자의 ID가 포함되어 있습니다.<br /> </td>
  </tr>
  <tr>
   <td>currentAssignment<br /> </td>
   <td>금</td>
   <td>여기에는 현재 작업 할당에 대한 세부 정보가 포함되어 있습니다.<br /> </td>
  </tr>
  <tr>
   <td>기한<br /> </td>
   <td>금</td>
   <td>여기에는 작업이 기한에 도달하게 되는 타임스탬프가 포함되어 있습니다.<br /> </td>
  </tr>
  <tr>
   <td>설명<br /> </td>
   <td>금</td>
   <td>작업에 대한 설명이 포함되어 있습니다.<br /> </td>
  </tr>
  <tr>
   <td>displayName<br /> </td>
   <td>금</td>
   <td>여기에는 작업의 표시 이름이 포함되어 있습니다.<br /> </td>
  </tr>
  <tr>
   <td>forwardGroupId<br /> </td>
   <td>금</td>
   <td>여기에는 작업을 전달할 수 있는 그룹의 ID가 포함되어 있습니다. 이는 프로세스 설계 중에 설정됩니다.<br /> </td>
  </tr>
  <tr>
   <td>지침<br /> </td>
   <td>금</td>
   <td>여기에는 작업에 대한 지침이 포함되어 있습니다.<br /> </td>
  </tr>
  <tr>
   <td>isLocked<br /> </td>
   <td>금</td>
   <td>작업이 잠겨 있으면 True입니다.<br /> </td>
  </tr>
  <tr>
   <td>isMustOpenToComplete<br /> </td>
   <td>금</td>
   <td>작업을 완료하려면 작업 양식을 열어야 하는 경우 True입니다.<br /> </td>
  </tr>
  <tr>
   <td>isOpenFullScreen<br /> </td>
   <td>금</td>
   <td>true인 경우 작업을 열 때 양식이 처음 전체 화면을 표시합니다.<br /> </td>
  </tr>
  <tr>
   <td>isRouteSelectionRequired<br /> </td>
   <td>금</td>
   <td>true인 경우 경로를 선택하여 작업을 완료해야 합니다.<br /> </td>
  </tr>
  <tr>
   <td>isShowAttachments<br /> </td>
   <td>금</td>
   <td>true인 경우 첨부 파일이 표시됩니다.<br /> </td>
  </tr>
  <tr>
   <td>isStartTask<br /> </td>
   <td>금</td>
   <td>true인 경우 작업은 시작 지점에서 생성됩니다.<br /> </td>
  </tr>
  <tr>
   <td>표시 가능<br /> </td>
   <td>금</td>
   <td>작업이 작업 영역에 표시되면 True입니다.<br /> </td>
  </tr>
  <tr>
   <td>다음 알림 메시지<br /> </td>
   <td>금</td>
   <td>다음 미리 알림에 대한 타임스탬프.<br /> </td>
  </tr>
  <tr>
   <td>우선 순위<br /> </td>
   <td>금</td>
   <td>여기에는 작업의 우선 순위가 포함되어 있습니다.<br /> 1 = 가장 높은 우선 순위<br /> 2 = 높은 우선 순위<br /> 3 = 일반 우선 순위<br /> 4 = 낮은 우선 순위<br /> 5 = 최저 우선순위<br /> </td>
  </tr>
  <tr>
   <td>processInstanceId</td>
   <td>금</td>
   <td>작업이 속한 프로세스 인스턴스의 ID.<br /> </td>
  </tr>
  <tr>
   <td>processInstanceStatus<br /> </td>
   <td>금</td>
   <td>작업의 프로세스 인스턴스 상태.<br /> </td>
  </tr>
  <tr>
   <td>reminderCount<br /> </td>
   <td>금</td>
   <td>작업에 대한 미리 알림 수가 포함되어 있습니다.<br /> </td>
  </tr>
  <tr>
   <td>routeList<br /> </td>
   <td>금</td>
   <td>여기에는 작업과 연결된 경로 목록이 포함되어 있습니다. 사용자는 경로 목록에서 경로 중 하나를 선택하여 작업을 완료할 수 있습니다.<br /> </td>
  </tr>
  <tr>
   <td>선택됨 경로<br /> </td>
   <td>금</td>
   <td>작업이 완료되었을 때 선택한 경로의 이름이 포함됩니다.<br /> </td>
  </tr>
  <tr>
   <td>serializedImageTicket<br /> </td>
   <td>금</td>
   <td>작업에 해당하는 이미지 티켓이 포함되어 있습니다. 이 이미지 티켓은 작업의 imageUrl 필드에서 서버의 작업 이미지를 가져오는 데 사용됩니다.<br /> <br /> </td>
  </tr>
  <tr>
   <td>serviceName<br /> </td>
   <td>금</td>
   <td>여기에는 작업의 서비스 이름이 포함되어 있습니다.<br /> </td>
  </tr>
  <tr>
   <td>serviceTitle<br /> </td>
   <td>금</td>
   <td>여기에는 작업에 대한 서비스 제목이 포함되어 있습니다.<br /> </td>
  </tr>
  <tr>
   <td>상태<br /> </td>
   <td>금</td>
   <td>1 = 생성됨(작업이 시작 지점에서 생성됨)<br /> 2 = 생성 및 저장됨(작업이 시작 지점에서 생성되어 저장됨)<br /> 3 = 할당됨(프로세스가 시작된 후 작업이 사용자에게 할당됨)<br /> 4 = 지정 및 저장(작업이 지정 및 저장됨)<br /> 100 = 완료됨(작업이 완료되었습니다.)<br /> 101 = 기한 지남(작업이 기한에 도달했습니다.)<br /> 102 = 종료됨<br /> </td>
  </tr>
  <tr>
   <td>stepName<br /> </td>
   <td>금</td>
   <td>여기에는 프로세스 설계 중 작업 세트의 이름이 포함됩니다.<br /> </td>
  </tr>
  <tr>
   <td>summaryUrl<br /> </td>
   <td>금</td>
   <td>작업 요약 URL이 포함되어 있습니다.<br /> </td>
  </tr>
  <tr>
   <td>taskACL<br /> </td>
   <td>금</td>
   <td>작업의 액세스 제어 목록입니다.<br /> </td>
  </tr>
  <tr>
   <td>taskId<br /> </td>
   <td>금</td>
   <td>작업 ID.<br /> </td>
  </tr>
  <tr>
   <td>updateTime<br /> </td>
   <td>금</td>
   <td>작업을 마지막으로 업데이트한 타임스탬프.<br /> </td>
  </tr>
  <tr>
   <td>formUrl<br /> </td>
   <td>화</td>
   <td>여기에는 작업에 대한 양식 URL이 포함되어 있습니다.<br /> </td>
  </tr>
  <tr>
   <td>taskFormType<br /> </td>
   <td>화</td>
   <td>작업 양식 유형이 포함되어 있습니다. 이 필드를 사용하면 작업이 클라이언트에서 pdf, swf 양식 등으로 렌더링됩니다.<br /> </td>
  </tr>
  <tr>
   <td>showDirectActions<br /> </td>
   <td>화</td>
   <td>true인 경우 경로 작업이 작업 영역에 표시됩니다.<br /> </td>
  </tr>
  <tr>
   <td>showACLAactions<br /> </td>
   <td>화</td>
   <td>true인 경우 작업 영역에 전달, 참조, 공유 등의 작업이 표시됩니다.<br /> </td>
  </tr>
  <tr>
   <td>supportOffline<br /> </td>
   <td>화</td>
   <td>true인 경우 양식을 오프라인으로 전환할 수 있습니다. PDF 양식에만 해당됩니다.<br /> </td>
  </tr>
  <tr>
   <td>supportsSave<br /> </td>
   <td>화</td>
   <td>true인 경우 사용자가 작업을 저장할 수 있습니다.<br /> </td>
  </tr>
  <tr>
   <td>readerSubmitOptions<br /> </td>
   <td>화</td>
   <td>이 개체에는 pdf 양식에 제출 단추가 없는 경우 판독기를 통해 pdf 양식을 제출하는 데 사용되는 옵션이 포함되어 있습니다.<br /> </td>
  </tr>
  <tr>
   <td>isDefaultImage<br /> </td>
   <td>화</td>
   <td>프로세스에 대해 지정된 이미지가 있는지 여부를 나타냅니다. 프로세스와 연결된 이미지가 없으면 True이고, 그렇지 않으면 false입니다.<br /> </td>
  </tr>
  <tr>
   <td>historyTaskList<br /> </td>
   <td>화</td>
   <td>여기에는 작업 세부 정보의 기록 탭에 사용되는 작업 목록이 포함되어 있습니다.<br /> </td>
  </tr>
  <tr>
   <td>isOwner<br /> </td>
   <td>화</td>
   <td>로그인한 사용자가 작업의 소유자인 경우 True입니다.<br /> </td>
  </tr>
  <tr>
   <td>사용 가능한 명령<br /> </td>
   <td>화</td>
   <td>여기에는 작업 시 수행할 수 있는 모든 작업이 포함되어 있습니다.<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.directCommands<br /> </td>
   <td>화</td>
   <td>여기에는 작업에 사용할 수 있는 모든 경로 작업이 포함됩니다.<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.taskACLCommands<br /> </td>
   <td>화</td>
   <td>여기에는 작업에 사용 가능한 경우 전달, 공유 및 참조와 같은 명령이 포함되어 있습니다.<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.otherCommands<br /> </td>
   <td>화</td>
   <td>여기에는 잠금, 잠금 해제, 포기, 반환, 클레임 등과 같은 명령이 포함되어 있습니다.<br /> </td>
  </tr>
  <tr>
   <td>processInstanceInfo<br /> </td>
   <td>화</td>
   <td>여기에는 작업의 프로세스 인스턴스에 대한 정보가 포함되어 있습니다.<br /> </td>
  </tr>
  <tr>
   <td>프로세스 변수<br /> </td>
   <td>T<br /> </td>
   <td>이 개체에는 프로세스 변수의 개체 배열(있는 경우)이 포함되어 있습니다.<br /> </td>
  </tr>
  <tr>
   <td>pendingTasks<br /> </td>
   <td>화</td>
   <td>여기에는 작업의 프로세스 인스턴스에 대해 보류 중인 작업 목록이 포함되어 있습니다.<br /> </td>
  </tr>
  <tr>
   <td>사용자 작업<br /> </td>
   <td>화</td>
   <td>개체 배열입니다. 각 객체에는 경로 및 해당 확인 메시지(있는 경우)에 대한 세부 정보가 포함되어 있습니다.<br /> </td>
  </tr>
  <tr>
   <td>dataUrl<br /> </td>
   <td>화</td>
   <td>작업 형식의 데이터에 대한 URL입니다.<br /> </td>
  </tr>
  <tr>
   <td>externalAppConfig<br /> </td>
   <td>화</td>
   <td>타사 애플리케이션 양식용 구성입니다.<br /> </td>
  </tr>
  <tr>
   <td>제출됨<br /> </td>
   <td>화</td>
   <td>작업이 제출되면 True입니다.<br /> </td>
  </tr>
  <tr>
   <td>첨부 파일<br /> </td>
   <td>화</td>
   <td>작업에 대한 첨부 파일 목록입니다.<br /> </td>
  </tr>
  <tr>
   <td>할당<br /> </td>
   <td>화</td>
   <td>작업 할당 목록입니다.<br /> </td>
  </tr>
 </tbody>
</table>

1. 필터

   필터는 기본적으로 사용자 또는 그룹의 큐입니다. 작업이 사용자/그룹에 할당되면 해당 큐에 작업이 추가됩니다.

<table>
 <tbody>
  <tr>
   <td><strong>속성</strong></td>
   <td><strong>클라이언트만</strong></td>
   <td><strong>댓글</strong></td>
  </tr>
  <tr>
   <td>isDefault <br type="_moz" /> </td>
   <td>금</td>
   <td>대기열이 로그인한 사용자의 기본 대기열이면 true이고, 그렇지 않으면 false입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>이름<br type="_moz" /> </td>
   <td>금</td>
   <td>큐 소유자의 이름입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>qid</td>
   <td>금</td>
   <td>큐의 ID입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>유형</td>
   <td>금</td>
   <td>여기에는 대기열 유형이 포함되어 있습니다.<br /> 0 - 사용자 큐.<br /> 1. 공유 큐.<br /> 2. 그룹 큐.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>쿼리</td>
   <td>화</td>
   <td>여기에는 필터와 연결된 쿼리가 포함됩니다. 이 쿼리는 전체 작업 목록에서 작업을 검색하는 데 사용됩니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>작업</td>
   <td>화</td>
   <td>필터에 속하는 모든 작업 목록이 포함되어 있습니다.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 부재 중

   부재 중 부재 일정을 관리하고 자신에게 할당된 작업의 흐름을 제어할 수 있습니다.

<table>
 <tbody>
  <tr>
   <td><strong>속성</strong><br type="_moz" /> </td>
   <td><strong>클라이언트만</strong><br type="_moz" /> </td>
   <td><strong>댓글</strong><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>날짜 범위<br type="_moz" /> </td>
   <td>금</td>
   <td>여기에는 사용자의 부재 중 일정 배열 개체가 포함되어 있습니다. 각 예약 개체에서 startDate 필드는 예약의 시작 날짜를 포함하고 endDate 필드는 예약의 종료 날짜를 포함합니다. endDate가 일정에서 null이면 사용자가 부재 중 일정의 종료 일자를 예약하지 않았음을 의미합니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>isNoPrimaryDesignate<br type="_moz" /> </td>
   <td>금</td>
   <td>사용자가 부재 중인 경우 기본 지정이 없는 경우 true입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>isOutOfOffice<br type="_moz" /> </td>
   <td>금</td>
   <td>사용자가 부재 중인 경우 True입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>outOfOfficeDesignate<br type="_moz" /> </td>
   <td>금</td>
   <td>여기에는 사용자가 지정한 기본 사용자로 할당된 사용자에 대한 세부 정보가 포함되어 있습니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processSpecificDesignes<br type="_moz" /> </td>
   <td>금</td>
   <td>여기에는 프로세스별 부재 중 지정을 위한 객체 배열이 포함됩니다. 각 프로세스별 지정 객체에서 processName은 프로세스 이름을 포함하며, 해당 프로세스에 할당된 사용자가 없으면 isNotDesignated가 true이고, 할당된 사용자가 없으면 userDesignated가 null이며, 그 밖에 해당 프로세스에 할당된 사용자의 세부 정보가 없습니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>프로세스<br type="_moz" /> </td>
   <td>화</td>
   <td>여기에는 사용자가 사용할 수 있는 모든 프로세스 목록이 포함되어 있습니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>initialOutOfOfficeSettings<br type="_moz" /> </td>
   <td>화</td>
   <td>여기에는 처음에 가져오는 사용자의 초기 부재 설정이 포함됩니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>outOfOfficeSettings<br type="_moz" /> </td>
   <td>화</td>
   <td>여기에는 수정된 부재 중 설정이 포함되어 있습니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>userSearchHistory<br type="_moz" /> </td>
   <td>화</td>
   <td>날짜까지 로그인한 사용자가 검색하는 사용자 목록이 포함되어 있습니다.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 프로세스 인스턴스

   프로세스 인스턴스는 Workspace 또는 Workbench를 통해 프로세스가 호출될 때 생성됩니다.

<table>
 <tbody>
  <tr>
   <td><strong>속성</strong></td>
   <td><strong>클라이언트만</strong></td>
   <td><strong>댓글</strong></td>
  </tr>
  <tr>
   <td>설명<br type="_moz" /> </td>
   <td>금</td>
   <td>프로세스 인스턴스 설명<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>개시자</td>
   <td>금</td>
   <td>프로세스 인스턴스의 초기자 이름.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>initiatorId</td>
   <td>금</td>
   <td>프로세스 인스턴스의 개시자 ID.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processCompleteTime<br type="_moz" /> </td>
   <td>금</td>
   <td>프로세스 완료 시 타임스탬프.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processInstanceId<br type="_moz" /> </td>
   <td>금</td>
   <td>프로세스 인스턴스의 ID.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processInstanceStatus<br type="_moz" /> </td>
   <td>금</td>
   <td>0 = 시작됨<br /> 1 = 실행 중<br /> 2 = 완료<br /> 3 = 완료 중<br /> 4 = 종료됨<br /> 5 = 종료 중<br /> 6 = 일시 중단됨<br /> 7 = 일시 중단<br /> 8 = 일시 중단 해제<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processName<br type="_moz" /> </td>
   <td>금</td>
   <td>프로세스 이름.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processStartTime<br type="_moz" /> </td>
   <td>금</td>
   <td>프로세스 시작 시점 타임스탬프.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>프로세스 변수<br type="_moz" /> </td>
   <td>금</td>
   <td>프로세스 변수의 오브젝트 배열. 각 프로세스 변수 객체에는 프로세스 변수의 이름인 name, 프로세스 변수의 값인 value 및 프로세스 변수의 유형인 type이 포함됩니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>작업 목록<br type="_moz" /> </td>
   <td>화</td>
   <td>이 프로세스 인스턴스에서 생성한 작업.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 프로세스 이름

<table>
 <tbody>
  <tr>
   <td><strong>속성</strong></td>
   <td><strong>클라이언트만</strong></td>
   <td><strong>댓글</strong></td>
  </tr>
  <tr>
   <td>processMajorVersion<br type="_moz" /> </td>
   <td>금</td>
   <td>프로세스의 주요 버전입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processMinorVersion<br type="_moz" /> </td>
   <td>금</td>
   <td>프로세스의 부 버전입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processName<br type="_moz" /> </td>
   <td>금</td>
   <td>프로세스 이름.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processTitle<br type="_moz" /> </td>
   <td>금</td>
   <td>프로세스 제목.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processInstanceList<br type="_moz" /> </td>
   <td>화</td>
   <td>이 프로세스의 프로세스 인스턴스 목록입니다.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 작업 할당 개체

   작업 할당 개체에는 작업 할당에 대한 정보가 들어 있습니다. 다음은 작업 할당의 속성입니다.

<table>
 <tbody>
  <tr>
   <td><strong>속성</strong></td>
   <td><strong>클라이언트만</strong></td>
   <td><strong>댓글</strong></td>
  </tr>
  <tr>
   <td>assignmentCreateTime<br type="_moz" /> </td>
   <td>금</td>
   <td>이 작업 할당이 생성될 때의 타임스탬프.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>assignmentType<br type="_moz" /> </td>
   <td>금</td>
   <td>0 = 초기 할당<br /> 1 = 전달(작업이 현재 작업 소유자에게 전달됨)<br /> 2 = 반환됨(이전 작업 소유자가 작업을 현재 작업 소유자에게 반환함)<br /> 3 = 요청됨(작업의 현재 소유자가 작업을 요청했습니다.)<br /> 4 = 에스컬레이션(에스컬레이션 후 작업이 작업의 현재 소유자에게 할당됨)<br /> 5 = 관리자 할당됨(관리자가 작업의 현재 소유자에게 작업을 할당함)<br /> 6 = 컨설팅됨(작업이 현재 작업 소유자에게 컨설팅됨)<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>assignmentUpdateTime<br type="_moz" /> </td>
   <td>금</td>
   <td>이 작업 할당이 업데이트될 때의 타임스탬프.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>queueId<br type="_moz" /> </td>
   <td>금</td>
   <td>작업 현재 소유자의 대기열 ID.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>큐 소유자<br type="_moz" /> </td>
   <td>금</td>
   <td>작업의 현재 소유자 이름.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>queueOwnerId<br type="_moz" /> </td>
   <td>금</td>
   <td>작업의 현재 소유자 ID.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 작업 ACL 개체

   작업 ACL 개체에는 작업의 전달, 공유, 참조 등의 권한에 대한 정보가 들어 있습니다. 다음은 작업 ACL의 속성입니다.

<table>
 <tbody>
  <tr>
   <td><strong>속성</strong></td>
   <td><strong>클라이언트만</strong></td>
   <td><strong>댓글</strong></td>
  </tr>
  <tr>
   <td>canAddAttachments<br type="_moz" /> </td>
   <td>금</td>
   <td>true인 경우 첨부 파일을 작업에 추가할 수 있습니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canAddNotes<br type="_moz" /> </td>
   <td>금</td>
   <td>true인 경우 메모를 작업에 추가할 수 있습니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>클레임<br type="_moz" /> </td>
   <td>금</td>
   <td>true인 경우 작업을 요청할 수 있습니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canConsult<br type="_moz" /> </td>
   <td>금</td>
   <td>true인 경우 작업을 참조할 수 있습니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canForward<br type="_moz" /> </td>
   <td>금</td>
   <td>true인 경우 작업을 전달할 수 있습니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canShare<br type="_moz" /> </td>
   <td>금</td>
   <td>true인 경우 작업을 공유할 수 있습니다.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 작업 첨부

   첨부 파일을 작업에 추가할 수 있습니다. 첨부 파일은 첨부 파일 및 메모 유형일 수 있습니다. 다음은 첨부 객체의 등록 정보입니다.

<table>
 <tbody>
  <tr>
   <td><strong>속성</strong></td>
   <td><strong>클라이언트만</strong></td>
   <td><strong>댓글</strong></td>
  </tr>
  <tr>
   <td>creationDate<br type="_moz" /> </td>
   <td>금</td>
   <td>첨부 파일 생성 시 타임스탬프.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>creatorId<br type="_moz" /> </td>
   <td>금</td>
   <td>첨부 파일을 추가한 사용자의 ID.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>creatorName<br type="_moz" /> </td>
   <td>금</td>
   <td>첨부 파일을 추가한 사용자의 이름입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>설명<br type="_moz" /> </td>
   <td>금</td>
   <td>첨부 파일에 대한 설명.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>fileName<br type="_moz" /> </td>
   <td>금</td>
   <td>첨부 파일 이름.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>id<br type="_moz" /> </td>
   <td>금</td>
   <td>첨부 파일 ID.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>lastModifiedDate<br type="_moz" /> </td>
   <td>금</td>
   <td>첨부 파일을 마지막으로 수정한 시간 기록입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>noteExtended<br type="_moz" /> </td>
   <td>금</td>
   <td>true인 경우 참고는 확장(긴) 참고입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>권한<br type="_moz" /> </td>
   <td>금</td>
   <td>첨부 파일과 연결된 권한. allowRead 필드는 읽기 권한용이고, allowWrite는 쓰기 권한용이며, allowDelete는 삭제 권한용입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>크기<br type="_moz" /> </td>
   <td>금</td>
   <td>첨부 파일의 크기(바이트)입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>taskId<br type="_moz" /> </td>
   <td>금</td>
   <td>첨부 파일이 추가되는 작업의 ID.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>유형<br type="_moz" /> </td>
   <td>금</td>
   <td>유형은 파일에 대한 첨부 파일이고 유형은 메모에 대한 메모입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedCreationDate<br type="_moz" /> </td>
   <td>화</td>
   <td>여기에는 사용자의 UI 설정에 따른 첨부 파일 생성일이 포함됩니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedDescription<br type="_moz" /> </td>
   <td>화</td>
   <td>서식 있는 첨부 파일 설명. AEM Forms 작업 영역의 첨부 파일 설명에 있는 특수 문자를 표시하는 데 사용됩니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedFileName<br type="_moz" /> </td>
   <td>화</td>
   <td>서식 있는 첨부 파일 이름. AEM Forms 작업 영역의 첨부 파일 이름에 있는 특수 문자를 표시하는 데 사용됩니다. 이것은 노트 전용입니다.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 사용자

   다음은 사용자 객체의 속성입니다.

<table>
 <tbody>
  <tr>
   <td><strong>속성</strong></td>
   <td><strong>클라이언트만</strong></td>
   <td><strong>댓글</strong></td>
  </tr>
  <tr>
   <td>주소<br type="_moz" /> </td>
   <td>금</td>
   <td>사용자의 주소입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>commonName<br type="_moz" /> </td>
   <td>금</td>
   <td>사용자의 일반 이름.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>설명<br type="_moz" /> </td>
   <td>금</td>
   <td>사용자에 대한 설명.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>directGroupMemberships<br type="_moz" /> </td>
   <td>금</td>
   <td>사용자 그룹 목록입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>displayName<br type="_moz" /> </td>
   <td>금</td>
   <td>사용자의 표시 이름입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>이메일<br type="_moz" /> </td>
   <td>금</td>
   <td>사용자의 이메일 ID입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>isOutOfOffice<br type="_moz" /> </td>
   <td>금</td>
   <td>사용자가 부재 중인 경우 True입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>성<br type="_moz" /> </td>
   <td>금</td>
   <td>사용자의 성.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>이름<br type="_moz" /> </td>
   <td>금</td>
   <td>사용자의 이름입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>oid<br type="_moz" /> </td>
   <td>금</td>
   <td>사용자 ID.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>org<br type="_moz" /> </td>
   <td>금</td>
   <td>사용자의 조직 이름입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>우편 주소<br type="_moz" /> </td>
   <td>금</td>
   <td>사용자의 우편 주소.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>전화<br type="_moz" /> </td>
   <td>금</td>
   <td>사용자 연락처 번호.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>전화 번호<br type="_moz" /> </td>
   <td>금</td>
   <td>사용자 연락처 번호.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>사용자 id<br type="_moz" /> </td>
   <td>금</td>
   <td>사용자의 로그인 ID입니다.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>
