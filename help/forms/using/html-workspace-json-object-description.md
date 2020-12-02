---
title: AEM Forms 작업 공간 JSON 개체 설명
seo-title: AEM Forms 작업 공간 JSON 개체 설명
description: 사용자 정의, 확장, 수정 및 재사용을 위해 LiveCycle AEM Forms 작업 공간에 사용되는 JSON JavaScript 객체에 대한 개념 정보입니다.
seo-description: 사용자 정의, 확장, 수정 및 재사용을 위해 LiveCycle AEM Forms 작업 공간에 사용되는 JSON JavaScript 객체에 대한 개념 정보입니다.
uuid: 91c923c8-144a-4453-ba91-6a5193f1c4c4
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 61b7246d-ed28-4470-a0a2-a4aaf1a061a4
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '2134'
ht-degree: 4%

---


# AEM Forms 작업 공간 JSON 개체 설명 {#aem-forms-workspace-json-object-description}

AEM Forms 작업 영역에서 사용되는 JSON 개체는 아래에 설명되어 있습니다.

1. 카테고리

   카테고리는 작업 공간의 시작 프로세스 탭에 있습니다. 이러한 카테고리는 시작점을 분류하는 데 사용됩니다.

<table>
 <tbody>
  <tr>
   <td><strong>속성</strong></td>
   <td><strong>클라이언트만</strong></td>
   <td><strong>댓글</strong></td>
  </tr>
  <tr>
   <td>이름</td>
   <td>F</td>
   <td>범주 이름</td>
  </tr>
  <tr>
   <td>id</td>
   <td>F</td>
   <td>카테고리 ID<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>설명<br type="_moz" /> </td>
   <td>F</td>
   <td>범주 설명<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>parentOid<br type="_moz" /> </td>
   <td>F</td>
   <td>상위 카테고리<br type="_moz" />의 oid 포함 </td>
  </tr>
  <tr>
   <td>startPointsList<br type="_moz" /> </td>
   <td>T</td>
   <td>카테고리에 있는 모든 시작 지점 목록 포함</td>
  </tr>
  <tr>
   <td>categoryList</td>
   <td>T</td>
   <td>범주<br type="_moz" />의 직접 하위 범주 목록을 포함합니다. </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>모든 시작점 및 즐겨찾기는 클라이언트측에서 정의된 카테고리입니다. 즐겨찾기 카테고리에는 사용자가 즐겨찾기로 표시한 모든 시작점이 포함됩니다. 모든 시작 지점 카테고리는 모든 시작 지점을 포함합니다.

1. 시작 지점

   시작점은 호출될 때 작업공간에서 프로세스를 시작하는 데 사용됩니다.

   | **속성** | **클라이언트만** | **댓글** |
   |---|---|---|
   | categoryId | F | 여기에는 시작점이 속하는 카테고리 ID가 포함됩니다. |
   | 설명 | F | 여기에는 시작점에 대한 설명이 포함됩니다. |
   | 이름 | F | 시작 지점 이름이 포함되어 있습니다. |
   | serializedImageTicket | F | 시작점에 해당하는 이미지 티켓이 포함되어 있습니다. 이 이미지 티켓은 서버로부터 시작점에 대한 이미지를 얻기 위해 시작점의 imageUrl 필드에 사용됩니다. |
   | serviceName | F | 여기에는 시작점에 대한 서비스 이름이 포함되어 있습니다. |
   | startpointId | F | 시작 지점 id가 포함되어 있습니다. |
   | isFavorite | T | 시작점이 즐겨찾기인지 여부를 나타냅니다. startpoint가 다른 false를 즐겨찾는 경우 true입니다. |
   | isDefaultImage | T | 프로세스에 대해 지정된 이미지가 있는지 여부를 나타냅니다. 프로세스와 연결된 이미지가 없으면 true입니다. 그렇지 않으면 false입니다. |
   | 작업 | T | 여기에는 startpoint를 호출할 때 만들어진 작업이 포함됩니다. |
   | imageUrl | T | 시작 지점에 해당하는 이미지의 URL이 포함되어 있습니다. |

1. 작업

   작업은 사용자/그룹에 할당되고 데이터로 채울 수 있는 양식이나 안내선(더 이상 사용되지 않음)과 같은 사용자 인터페이스를 포함합니다. 사용자에게 작업이 할당되면 완료 및 제출을 위한 양식이나 안내서가 제공됩니다.

<table>
 <tbody>
  <tr>
   <td>속성<br /> </td>
   <td>클라이언트만<br /> </td>
   <td>댓글<br /> </td>
  </tr>
  <tr>
   <td>classOfTask</td>
   <td>F</td>
   <td>작업이 lc8 작업 또는 'Standard'인 경우 작업의 클래스는 'LC8'입니다.<br /> </td>
  </tr>
  <tr>
   <td>completeTime<br /> </td>
   <td>F</td>
   <td>작업이 완료된 타임스탬프가 들어 있습니다.<br /> </td>
  </tr>
  <tr>
   <td>consultGroupId<br /> </td>
   <td>F</td>
   <td>여기에는 작업을 확인할 수 있는 그룹의 ID가 포함되어 있습니다. 디자인 프로세스 중에 설정됩니다.<br /> </td>
  </tr>
  <tr>
   <td>createTime<br /> </td>
   <td>F</td>
   <td>작업을 만들 때의 타임스탬프가 포함되어 있습니다.<br /> </td>
  </tr>
  <tr>
   <td>creationId<br /> </td>
   <td>F</td>
   <td>작업을 만든 사용자의 ID가 포함되어 있습니다.<br /> </td>
  </tr>
  <tr>
   <td>currentAssignment<br /> </td>
   <td>F</td>
   <td>현재 작업 지정에 대한 세부 정보가 포함되어 있습니다.<br /> </td>
  </tr>
  <tr>
   <td>시한<br /> </td>
   <td>F</td>
   <td>작업 마감 시간에 도달하는 타임스탬프가 포함되어 있습니다.<br /> </td>
  </tr>
  <tr>
   <td>설명<br /> </td>
   <td>F</td>
   <td>작업에 대한 설명이 포함되어 있습니다.<br /> </td>
  </tr>
  <tr>
   <td>displayName<br /> </td>
   <td>F</td>
   <td>작업의 표시 이름이 포함되어 있습니다.<br /> </td>
  </tr>
  <tr>
   <td>forwardGroupId<br /> </td>
   <td>F</td>
   <td>작업을 전달할 수 있는 그룹의 ID가 포함되어 있습니다. 디자인 프로세스 중에 설정됩니다.<br /> </td>
  </tr>
  <tr>
   <td>instructions<br /> </td>
   <td>F</td>
   <td>작업에 대한 지침을 포함합니다.<br /> </td>
  </tr>
  <tr>
   <td>isLocked<br /> </td>
   <td>F</td>
   <td>작업이 잠긴 경우 true입니다.<br /> </td>
  </tr>
  <tr>
   <td>isMustOpenToComplete<br /> </td>
   <td>F</td>
   <td>작업을 완료하려면 작업 양식을 열어야 하는 경우 True입니다.<br /> </td>
  </tr>
  <tr>
   <td>isOpenFullScreen<br /> </td>
   <td>F</td>
   <td>true인 경우 작업을 열 때 양식에서 처음으로 전체 화면이 나타납니다.<br /> </td>
  </tr>
  <tr>
   <td>isRouteSelectionRequired<br /> </td>
   <td>F</td>
   <td>true인 경우 작업을 완료하려면 경로를 선택해야 합니다.<br /> </td>
  </tr>
  <tr>
   <td>isShowAttachments<br /> </td>
   <td>F</td>
   <td>첨부 파일이 true이면 표시됩니다.<br /> </td>
  </tr>
  <tr>
   <td>isStartTask<br /> </td>
   <td>F</td>
   <td>true이면 시작 지점에서 작업이 만들어집니다.<br /> </td>
  </tr>
  <tr>
   <td>isVisible<br /> </td>
   <td>F</td>
   <td>작업 영역에 작업이 표시되는 경우 true입니다.<br /> </td>
  </tr>
  <tr>
   <td>nextReminder<br /> </td>
   <td>F</td>
   <td>다음 미리 알림의 타임스탬프입니다.<br /> </td>
  </tr>
  <tr>
   <td>우선 순위<br /> </td>
   <td>F</td>
   <td>작업의 우선 순위가 포함되어 있습니다.<br /> 1 = 가장 높은 우선 순위<br /> 2 = 높은 우선 순위<br /> 3 = 일반 우선 순위<br />  4 = 낮은 우선 순위<br />  5 = 가장 낮은 우선 순위<br /> </td>
  </tr>
  <tr>
   <td>processInstanceId</td>
   <td>F</td>
   <td>작업이 속한 프로세스 인스턴스의 ID입니다.<br /> </td>
  </tr>
  <tr>
   <td>processInstanceStatus<br /> </td>
   <td>F</td>
   <td>작업 프로세스 인스턴스의 상태입니다.<br /> </td>
  </tr>
  <tr>
   <td>reminderCount<br /> </td>
   <td>F</td>
   <td>작업에 대한 미리 알림 수가 포함되어 있습니다.<br /> </td>
  </tr>
  <tr>
   <td>routeList<br /> </td>
   <td>F</td>
   <td>작업에 연결된 경로 목록이 포함되어 있습니다. 사용자는 경로 목록에서 경로 중 하나를 선택하여 작업을 완료할 수 있습니다.<br /> </td>
  </tr>
  <tr>
   <td>selectedRoute<br /> </td>
   <td>F</td>
   <td>작업이 완료될 때 선택한 라우트의 이름이 포함되어 있습니다.<br /> </td>
  </tr>
  <tr>
   <td>serializedImageTicket<br /> </td>
   <td>F</td>
   <td>작업에 해당하는 이미지 티켓이 포함되어 있습니다. 이 이미지 티켓은 서버의 작업을 위한 이미지를 가져오기 위해 작업의 imageUrl 필드에 사용됩니다.<br /> <br /> </td>
  </tr>
  <tr>
   <td>serviceName<br /> </td>
   <td>F</td>
   <td>작업에 대한 서비스 이름이 포함되어 있습니다.<br /> </td>
  </tr>
  <tr>
   <td>serviceTitle<br /> </td>
   <td>F</td>
   <td>작업에 대한 서비스 제목이 포함되어 있습니다.<br /> </td>
  </tr>
  <tr>
   <td>상태<br /> </td>
   <td>F</td>
   <td>1 = 생성됨(시작 지점에서 작업이 생성됨)<br /> 2 = 생성 및 저장(작업은 시작점에서 생성되어 저장됨)<br /> 3 = 할당됨(프로세스가 시작된 후 작업이 사용자에게 할당됩니다.)<br /> 4 = 지정됨 및 저장됨(작업이 할당되고 저장됨)<br /> 100 = 완료(작업이 완료됨)<br /> 101 = 마감 시간(작업이 마감 시간에 도달했습니다.)<br /> 102 = 종료됨<br /> </td>
  </tr>
  <tr>
   <td>stepName<br /> </td>
   <td>F</td>
   <td>디자인 프로세스 중에 설정된 작업의 이름이 포함되어 있습니다.<br /> </td>
  </tr>
  <tr>
   <td>summaryUrl<br /> </td>
   <td>F</td>
   <td>작업 요약 url이 포함되어 있습니다.<br /> </td>
  </tr>
  <tr>
   <td>taskACL<br /> </td>
   <td>F</td>
   <td>작업의 액세스 제어 목록입니다.<br /> </td>
  </tr>
  <tr>
   <td>taskId<br /> </td>
   <td>F</td>
   <td>작업의 ID입니다.<br /> </td>
  </tr>
  <tr>
   <td>updateTime<br /> </td>
   <td>F</td>
   <td>작업이 마지막으로 업데이트된 타임스탬프입니다.<br /> </td>
  </tr>
  <tr>
   <td>formUrl<br /> </td>
   <td>T</td>
   <td>작업에 대한 양식 URL을 포함합니다.<br /> </td>
  </tr>
  <tr>
   <td>taskFormType<br /> </td>
   <td>T</td>
   <td>작업 양식 유형이 포함되어 있습니다. 이 필드를 사용하면 작업이 클라이언트에서 swf 양식 등에 대해 pdf로 렌더링됩니다.<br /> </td>
  </tr>
  <tr>
   <td>showDirectActions<br /> </td>
   <td>T</td>
   <td>true이면 경로 작업이 작업 영역에 표시됩니다.<br /> </td>
  </tr>
  <tr>
   <td>showACLActions<br /> </td>
   <td>T</td>
   <td>true인 경우 앞으로, 참조, 공유와 같은 작업이 작업 영역에 표시됩니다.<br /> </td>
  </tr>
  <tr>
   <td>supportsOffline<br /> </td>
   <td>T</td>
   <td>true이면 양식을 오프라인으로 만들 수 있습니다. pdf 양식에만 해당됩니다.<br /> </td>
  </tr>
  <tr>
   <td>supportsSave<br /> </td>
   <td>T</td>
   <td>true이면 사용자가 작업을 저장할 수 있습니다.<br /> </td>
  </tr>
  <tr>
   <td>readerSubmitOptions<br /> </td>
   <td>T</td>
   <td>이 개체에는 pdf 양식에 전송 단추가 없는 경우 reader를 통해 pdf 양식을 제출하는 데 사용되는 옵션이 포함되어 있습니다.<br /> </td>
  </tr>
  <tr>
   <td>isDefaultImage<br /> </td>
   <td>T</td>
   <td>프로세스에 대해 지정된 이미지가 있는지 여부를 나타냅니다. 프로세스와 연결된 이미지가 없으면 true이고, 그렇지 않으면 false입니다.<br /> </td>
  </tr>
  <tr>
   <td>historyTaskList<br /> </td>
   <td>T</td>
   <td>작업 세부 사항의 내역 탭에 사용되는 작업 목록이 포함되어 있습니다.<br /> </td>
  </tr>
  <tr>
   <td>isOwner<br /> </td>
   <td>T</td>
   <td>로그인한 사용자가 작업의 소유자인 경우 true입니다.<br /> </td>
  </tr>
  <tr>
   <td>availableCommands<br /> </td>
   <td>T</td>
   <td>작업에 수행할 수 있는 모든 작업이 포함되어 있습니다.<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.directCommands<br /> </td>
   <td>T</td>
   <td>작업에 사용할 수 있는 모든 경로 작업이 포함되어 있습니다.<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.taskACLCommands<br /> </td>
   <td>T</td>
   <td>여기에는 앞으로, 공유 및 작업에 사용 가능한 경우 참조와 같은 명령이 포함되어 있습니다.<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.otherCommands<br /> </td>
   <td>T</td>
   <td>여기에는 잠금, 잠금 해제, 포기, 반환, 클레임 등의 명령이 포함되어 있습니다.<br /> </td>
  </tr>
  <tr>
   <td>processInstanceInfo<br /> </td>
   <td>T</td>
   <td>작업의 프로세스 인스턴스에 대한 정보가 포함되어 있습니다.<br /> </td>
  </tr>
  <tr>
   <td>processVariables<br /> </td>
   <td>T<br /> </td>
   <td>여기에는 프로세스 변수의 개체 배열이 포함됩니다(있는 경우).<br /> </td>
  </tr>
  <tr>
   <td>pendingTasks<br /> </td>
   <td>T</td>
   <td>작업의 프로세스 인스턴스에 대한 보류 중인 작업 목록이 포함되어 있습니다.<br /> </td>
  </tr>
  <tr>
   <td>userActions<br /> </td>
   <td>T</td>
   <td>개체 배열입니다. 각 개체에는 경로 및 해당 확인 메시지가 있을 경우 그에 대한 세부 정보가 포함되어 있습니다.<br /> </td>
  </tr>
  <tr>
   <td>dataUrl<br /> </td>
   <td>T</td>
   <td>작업 형식의 데이터에 대한 URL입니다.<br /> </td>
  </tr>
  <tr>
   <td>externalAppConfig<br /> </td>
   <td>T</td>
   <td>타사 응용 프로그램 양식에 대한 구성입니다.<br /> </td>
  </tr>
  <tr>
   <td>submitted<br /> </td>
   <td>T</td>
   <td>작업이 제출되면 true입니다.<br /> </td>
  </tr>
  <tr>
   <td>첨부 파일<br /> </td>
   <td>T</td>
   <td>작업의 첨부 목록.<br /> </td>
  </tr>
  <tr>
   <td>할당<br /> </td>
   <td>T</td>
   <td>작업의 할당 목록입니다.<br /> </td>
  </tr>
 </tbody>
</table>

1. 필터

   필터는 기본적으로 사용자 또는 그룹의 대기열입니다. 작업이 사용자/그룹에 할당되면 해당 대기열에 작업이 추가됩니다.

<table>
 <tbody>
  <tr>
   <td><strong>속성</strong></td>
   <td><strong>클라이언트만</strong></td>
   <td><strong>댓글</strong></td>
  </tr>
  <tr>
   <td>isDefault <br type="_moz" /> </td>
   <td>F</td>
   <td>대기열이 로그인한 사용자의 기본 큐인 경우 true, 그렇지 않은 경우 false입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>이름<br type="_moz" /> </td>
   <td>F</td>
   <td>큐 소유자의 이름입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>qid</td>
   <td>F</td>
   <td>큐의 ID입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>유형</td>
   <td>F</td>
   <td>큐 유형이 포함되어 있습니다.<br /> 0 - 사용자 큐.<br /> 1. 공유 큐를 참조하십시오.<br /> 2. 그룹 큐.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>쿼리</td>
   <td>T</td>
   <td>여기에는 필터와 연관된 쿼리가 포함됩니다. 이 쿼리는 전체 작업 목록에서 작업을 검색하는 데 사용됩니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>작업</td>
   <td>T</td>
   <td>필터에 속하는 모든 작업의 목록이 포함되어 있습니다.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 부재 중

   부재 중 일정을 관리하고 부재 시 할당된 작업 흐름을 제어할 수 있습니다.

<table>
 <tbody>
  <tr>
   <td><strong>속성</strong><br type="_moz" /> </td>
   <td><strong>클라이언트만</strong><br type="_moz" /> </td>
   <td><strong>댓글</strong><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>dateRange<br type="_moz" /> </td>
   <td>F</td>
   <td>사용자 사무실 밖 일정의 배열 개체를 포함합니다. 각 예약 객체에서 startDate 필드는 일정의 시작 날짜를 포함하며 endDate 필드는 일정의 종료 날짜를 포함합니다. 일정에 endDate가 null이면 사용자가 부재 중 일정의 종료 날짜를 예약하지 않았음을 의미합니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>isNoPrimaryDesignate<br type="_moz" /> </td>
   <td>F</td>
   <td>사용자가 부재 중인 경우 기본 지정이 없는 경우 True입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>isOutOfOffice<br type="_moz" /> </td>
   <td>F</td>
   <td>사용자가 부재 중인 경우 true입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>outOfOfficeDesignate<br type="_moz" /> </td>
   <td>F</td>
   <td>여기에는 사용자가 기본 지정자로 지정한 사용자의 세부 정보가 포함됩니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processSpecificDesignates<br type="_moz" /> </td>
   <td>F</td>
   <td>여기에는 프로세스 특정 부재 중 지정을 위한 개체 배열이 포함됩니다. 각 프로세스 특정 지정 개체에서 processName은 프로세스 이름을 포함하며, 해당 프로세스에 대해 사용자가 할당되지 않은 경우에는 isNotDesignated가 true이고, 해당 프로세스에 대해 할당된 사용자의 다른 세부 정보를 사용자가 지정하지 않은 경우 userDesignated가 null입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>프로세스<br type="_moz" /> </td>
   <td>T</td>
   <td>사용자가 사용할 수 있는 모든 프로세스 목록이 포함되어 있습니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>initialOutOfOfficeSettings<br type="_moz" /> </td>
   <td>T</td>
   <td>여기에는 처음에 가져오는 사용자의 초기 부재 중 설정이 포함되어 있습니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>outOfOfficeSettings<br type="_moz" /> </td>
   <td>T</td>
   <td>수정된 부재 중 설정이 포함되어 있습니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>userSearchHistory<br type="_moz" /> </td>
   <td>T</td>
   <td>이 목록에는 날짜까지 로그인한 사용자가 검색하는 사용자 목록이 포함되어 있습니다.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 프로세스 인스턴스

   프로세스 인스턴스는 작업 공간이나 워크벤치를 통해 프로세스를 호출할 때 생성됩니다.

<table>
 <tbody>
  <tr>
   <td><strong>속성</strong></td>
   <td><strong>클라이언트만</strong></td>
   <td><strong>댓글</strong></td>
  </tr>
  <tr>
   <td>설명<br type="_moz" /> </td>
   <td>F</td>
   <td>프로세스 인스턴스에 대한 설명<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>이니시에이터</td>
   <td>F</td>
   <td>프로세스 인스턴스의 초기자 이름입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>initiatorId</td>
   <td>F</td>
   <td>프로세스 인스턴스의 초기자 ID입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processCompleteTime<br type="_moz" /> </td>
   <td>F</td>
   <td>처리가 완료된 타임스탬프입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processInstanceId<br type="_moz" /> </td>
   <td>F</td>
   <td>프로세스 인스턴스의 ID입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processInstanceStatus<br type="_moz" /> </td>
   <td>F</td>
   <td>0 = 시작<br /> 1 = 실행 중<br /> 2 = 완료<br /> 3 = 완료<br /> 4 = 종료됨<br /> 5 = 종료 중<br /> 6 = 일시 중단<br /> 7 = 일시 중단 해제<br /> 8 = 일시 중단 해제<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processName<br type="_moz" /> </td>
   <td>F</td>
   <td>프로세스의 이름입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processStartTime<br type="_moz" /> </td>
   <td>F</td>
   <td>프로세스가 시작될 때의 타임스탬프입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processVariables<br type="_moz" /> </td>
   <td>F</td>
   <td>프로세스 변수의 객체 배열. 각 프로세스 변수 개체에는 프로세스 변수의 이름인 이름, 프로세스 변수의 값인 값 및 프로세스 변수의 유형인 유형이 포함됩니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>작업 목록<br type="_moz" /> </td>
   <td>T</td>
   <td>이 프로세스 인스턴스에서 생성된 작업입니다.<br type="_moz" /> </td>
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
   <td>F</td>
   <td>프로세스의 주 버전입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processMinorVersion<br type="_moz" /> </td>
   <td>F</td>
   <td>프로세스의 일부 버전입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processName<br type="_moz" /> </td>
   <td>F</td>
   <td>프로세스의 이름입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processTitle<br type="_moz" /> </td>
   <td>F</td>
   <td>프로세스의 제목입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processInstanceList<br type="_moz" /> </td>
   <td>T</td>
   <td>이 프로세스에 대한 프로세스 인스턴스 목록입니다.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 작업 할당 객체

   작업 할당 객체에는 작업 지정에 대한 정보가 포함되어 있습니다. 작업 할당의 속성은 다음과 같습니다.

<table>
 <tbody>
  <tr>
   <td><strong>속성</strong></td>
   <td><strong>클라이언트만</strong></td>
   <td><strong>댓글</strong></td>
  </tr>
  <tr>
   <td>assignmentCreateTime<br type="_moz" /> </td>
   <td>F</td>
   <td>이 작업 할당을 만드는 경우 타임스탬프입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>assignmentType<br type="_moz" /> </td>
   <td>F</td>
   <td>0 = 초기 할당<br /> 1 = 앞으로(작업이 현재 작업 소유자에게 전달되었습니다.)<br /> 2 = 반환됨(이전 작업 소유자가 작업을 현재 작업 소유자에게 반환했습니다.)<br /> 3 = 청구됨(현재 작업 소유자가 작업을 요청했습니다.)<br /> 4 = 문제 제기(문제 제기 후 작업의 현재 소유자에게 작업이 할당되었습니다.)<br /> 5 = 관리자 지정(작업이 현재 작업 소유자에게 관리자가 할당했습니다.)<br /> 6 = 컨설팅됨(현재 작업 소유자와 작업이 협의되었습니다.)<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>assignmentUpdateTime<br type="_moz" /> </td>
   <td>F</td>
   <td>이 작업 할당이 업데이트될 때 타임스탬프입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>queueId<br type="_moz" /> </td>
   <td>F</td>
   <td>현재 작업 소유자의 큐 ID입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>queueOwner<br type="_moz" /> </td>
   <td>F</td>
   <td>작업의 현재 소유자 이름입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>queueOwnerId<br type="_moz" /> </td>
   <td>F</td>
   <td>현재 작업 소유자의 ID입니다.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 작업 ACL 개체

   작업 ACL 개체에는 전달, 공유, 컨설팅 등과 같은 권한에 대한 정보가 포함되어 있습니다. JavaScript를 참조하십시오. 다음은 작업의 ACL 속성입니다.

<table>
 <tbody>
  <tr>
   <td><strong>속성</strong></td>
   <td><strong>클라이언트만</strong></td>
   <td><strong>댓글</strong></td>
  </tr>
  <tr>
   <td>canAddAttachments<br type="_moz" /> </td>
   <td>F</td>
   <td>true이면 작업에 첨부 파일을 추가할 수 있습니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canAddNotes<br type="_moz" /> </td>
   <td>F</td>
   <td>true이면 작업에 메모를 추가할 수 있습니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canClaim<br type="_moz" /> </td>
   <td>F</td>
   <td>true이면 작업을 요청할 수 있습니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canConsult<br type="_moz" /> </td>
   <td>F</td>
   <td>true이면 작업을 참조할 수 있습니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canForward<br type="_moz" /> </td>
   <td>F</td>
   <td>true이면 작업을 전달할 수 있습니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canShare<br type="_moz" /> </td>
   <td>F</td>
   <td>true이면 작업을 공유할 수 있습니다.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 작업 첨부

   작업에 첨부 파일을 추가할 수 있습니다. 첨부 파일 유형은 첨부 파일과 메모입니다. 첨부 파일의 속성은 다음과 같습니다.

<table>
 <tbody>
  <tr>
   <td><strong>속성</strong></td>
   <td><strong>클라이언트만</strong></td>
   <td><strong>댓글</strong></td>
  </tr>
  <tr>
   <td>creationDate<br type="_moz" /> </td>
   <td>F</td>
   <td>첨부 파일이 생성된 타임스탬프입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>creatorId<br type="_moz" /> </td>
   <td>F</td>
   <td>첨부 파일을 추가한 사용자의 ID입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>creatorName<br type="_moz" /> </td>
   <td>F</td>
   <td>첨부 파일을 추가한 사용자의 이름입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>설명<br type="_moz" /> </td>
   <td>F</td>
   <td>첨부 파일에 대한 설명입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>fileName<br type="_moz" /> </td>
   <td>F</td>
   <td>첨부 파일의 이름입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>id<br type="_moz" /> </td>
   <td>F</td>
   <td>첨부 파일의 ID입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>lastModifiedDate<br type="_moz" /> </td>
   <td>F</td>
   <td>첨부 파일을 마지막으로 수정한 타임스탬프입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>noteExtended<br type="_moz" /> </td>
   <td>F</td>
   <td>true이면 메모가 확장(긴) 메모입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>권한<br type="_moz" /> </td>
   <td>F</td>
   <td>첨부 파일과 연관된 권한 allowRead 필드는 읽기 권한을 위한 것이며 allowWrite는 쓰기 권한을 위한 것이며 allowDelete는 삭제 권한을 위한 것입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>크기<br type="_moz" /> </td>
   <td>F</td>
   <td>첨부 파일 크기(바이트)입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>taskId<br type="_moz" /> </td>
   <td>F</td>
   <td>첨부가 추가된 작업의 ID입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>유형<br type="_moz" /> </td>
   <td>F</td>
   <td>Type은 파일에 대한 첨부 파일, Type은 메모입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedCreationDate<br type="_moz" /> </td>
   <td>T</td>
   <td>사용자의 UI 설정에 따른 첨부 파일 생성 날짜가 포함되어 있습니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedDescription<br type="_moz" /> </td>
   <td>T</td>
   <td>서식이 지정된 첨부 설명. AEM Forms 작업 영역의 첨부 파일에 있는 특수 문자를 표시하는 데 사용됩니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedFileName<br type="_moz" /> </td>
   <td>T</td>
   <td>서식이 지정된 첨부 이름. AEM Forms 작업 공간에서 첨부 파일에 있는 특수 문자를 표시하는 데 사용됩니다. 참고용입니다.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 사용자

   다음은 사용자 개체의 속성입니다.

<table>
 <tbody>
  <tr>
   <td><strong>속성</strong></td>
   <td><strong>클라이언트만</strong></td>
   <td><strong>댓글</strong></td>
  </tr>
  <tr>
   <td>주소<br type="_moz" /> </td>
   <td>F</td>
   <td>사용자의 주소입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>commonName<br type="_moz" /> </td>
   <td>F</td>
   <td>사용자의 일반 이름입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>설명<br type="_moz" /> </td>
   <td>F</td>
   <td>사용자에 대한 설명입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>directGroupMembership<br type="_moz" /> </td>
   <td>F</td>
   <td>사용자 그룹 목록입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>displayName<br type="_moz" /> </td>
   <td>F</td>
   <td>사용자의 이름을 표시합니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>email<br type="_moz" /> </td>
   <td>F</td>
   <td>사용자의 이메일 ID입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>isOutOfOffice<br type="_moz" /> </td>
   <td>F</td>
   <td>사용자가 부재 중인 경우 true입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>lastName<br type="_moz" /> </td>
   <td>F</td>
   <td>사용자의 성입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>firstName<br type="_moz" /> </td>
   <td>F</td>
   <td>사용자의 이름입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>oid<br type="_moz" /> </td>
   <td>F</td>
   <td>사용자의 ID입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>org<br type="_moz" /> </td>
   <td>F</td>
   <td>사용자 조직의 이름입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>postalAddress<br type="_moz" /> </td>
   <td>F</td>
   <td>사용자의 우편 주소입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>전화<br type="_moz" /> </td>
   <td>F</td>
   <td>사용자의 연락처 번호입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>telephoneNumber<br type="_moz" /> </td>
   <td>F</td>
   <td>사용자의 연락처 번호입니다.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>userid<br type="_moz" /> </td>
   <td>F</td>
   <td>사용자의 로그인 ID입니다.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>
