---
title: 전역 설정 가져오기 및 내보내기
seo-title: 전역 설정 가져오기 및 내보내기
description: 작업 공간에 대한 검색 템플릿 정의 및 전역 설정을 가져오고 내보낼 수 있습니다.
seo-description: 작업 공간에 대한 검색 템플릿 정의 및 전역 설정을 가져오고 내보낼 수 있습니다.
uuid: 8f1f210d-e850-4b2c-bb5a-942fa8299791
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_workspace
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 72fe5749-2fa2-442f-b679-7889faeafcac
translation-type: tm+mt
source-git-commit: 687cdacc2868de16a4df968dddedd330ce3317bb

---


# 전역 설정 가져오기 및 내보내기 {#importing-and-exporting-global-settings}

작업 공간에 대한 검색 템플릿 정의 및 전역 설정을 가져오고 내보낼 수 있습니다.

>[!NOTE]
>
>Flex 작업 공간은 AEM 양식 릴리스에서 더 이상 사용되지 않습니다.

예를 들어 검색 템플릿 정의 및 전역 설정을 한 환경에서 내보내고 다른 환경으로 가져와서 개발 환경에서 프로덕션 환경으로 이동할 수 있습니다.

전역 설정 파일을 내보낸 후 XML 또는 텍스트 편집기에서 설정을 수정할 수 있습니다. 그러나 편집할 수 있는 유일한 설정은 JChannelConnectionProperties, formViewOnly 및 specialRoute 설정입니다. 자세한 내용은 작업 영역 [전역 설정을](importing-exporting-global-settings.md#workspace-global-settings)참조하십시오.


>[!NOTE]
>
>전역 설정 파일에서 이벤트 속성을 변경하는 경우 서버를 다시 시작해야 합니다.

## 검색 템플릿 정의 가져오기 {#import-a-search-template-definition}

1. 관리 콘솔에서 서비스 > 작업 영역 > 전역 관리를 클릭합니다.
1. 검색 템플릿 정의 가져오기 상자에서 파일 선택을 클릭하고 검색 템플릿을 선택합니다. 원래 Workspace 인스턴스에서 내보낸 검색 템플릿 정의만 가져올 수 있습니다.
1. 가져오기를 클릭합니다. 

## 검색 템플릿 정의 내보내기 {#export-a-search-template-definition}

1. 전역 관리 페이지의 검색 템플릿 내보내기 정의에서 모두 목록을 클릭합니다.
1. 검색 템플릿 목록에서 내보낼 템플릿을 선택합니다.

   >[!NOTE]
   >
   >둘 이상의 템플릿을 선택할 수 있지만 마지막으로 선택한 템플릿만 내보내집니다.

1. 내보내기를 클릭한 다음 컴퓨터에 파일을 저장합니다.

## 전역 설정 가져오기 {#import-global-settings}

1. 전역 관리 페이지의 전역 설정 가져오기에서 파일 선택을 클릭하고 전역 설정 파일을 선택합니다. 전역 설정 파일은 XML 형식이어야 합니다.
1. 가져오기를 클릭합니다. 

## 전역 설정 내보내기 {#export-global-settings}

1. 전역 관리 페이지의 전역 설정 내보내기에서 내보내기를 클릭합니다.
1. 컴퓨터에 파일을 저장합니다.

## 작업 영역 전역 설정 {#workspace-global-settings}

전역 설정 파일을 수정할 수 있습니다.그러나 편집할 수 있는 유일한 설정은 JChannelConnectionProperties, formViewOnly 및 specialRoute 설정입니다.

>[!NOTE]
>
>Flex 작업 공간은 AEM 양식 릴리스에서 더 이상 사용되지 않습니다.

Workspace 전역 설정 파일에는 다음 설정이 포함되어 있습니다.

### specialRoute 설정 {#specialroutes-settings}

특수 *경로* 설정은 작업 공간에서 특별 경로의 속성을 지정하고, 승인하거나, 거부합니다. 특정 상황에서 이러한 경로의 단추는 작업 공간의 작업 카드에 표시되며 사용자는 양식을 열지 않고도 해당 경로를 선택할 수 있습니다. 전역 설정 파일에서 specialRoute 설정을 수정하여 승인 및 거부를 위해 사용자 지정된 이름을 추가하거나 추가 경로를 만들 수 있습니다.

**** client_specialRouts_routs_approve_style:승인 단추 아이콘을 식별하는 작업 영역 테마에 있는 스타일의 이름입니다. 스타일은 활성화된 아이콘과 비활성화된 아이콘에 대한 값을 포함해야 합니다. 사용자 지정 단추의 스타일을 정의하려면 다음 템플릿을 사용해야 합니다.작업` .buttonApprove {  icon: Embed('images/LC_DirectApprove_Sm_N.png');  disabledIcon: Embed('images/LC_DirectApprove_Sm_D.png');  paddingLeft: 5;  }` 영역 CSS 파일은 adobe-workspace-client.ear > adobe-workspace-client.war 파일에 있는 workspace-theme.swf 파일에 포함되어 있습니다. 작업 영역의 모양을 변경하려면 workspace-theme.swf 파일을 다시 컴파일해야 합니다.

**** client_specialRouts_routs_deny_names:워크벤치 사용자가 &quot;거부&quot;로 해석하기 위해 사용할 수 있는 다양한 문자열. 문자열은 대소문자를 구분합니다. 예를 들어 기본값은 deny입니다. Workbench 사용자가 프로세스에서 Deny라는 단어를 사용하는 경우 해당 단어는 인식되지 않습니다. 경로 단추를 사용자 지정하고 스타일을 적용하려면 [거부]라는 단어를 이 설정에 추가해야 합니다.

**** client_specialRouts_routs_deny_style:[작업 영역] 테마 파일에 있는 스타일의 이름으로, 거부 단추 아이콘을 식별합니다. 스타일은 활성화된 아이콘과 비활성화된 아이콘에 대한 값을 포함해야 합니다. `  .buttonDeny {   icon: Embed('images/LC_DirectDeny_Sm_N.png');   disabledIcon: Embed('images/LC_DirectDeny_Sm_D.png');   paddingLeft: 0;   }` 사용자 지정 단추의 스타일을 정의하려면 다음 템플릿을 사용해야 합니다.**client_** specialRouts_rows_approve_names:워크벤치 사용자가 &quot;승인&quot;으로 해석하기 위해 사용할 수 있는 다양한 문자열. 문자열은 대소문자를 구분합니다. 예를 들어 기본값은 approve입니다. 워크벤치 사용자가 프로세스에서 승인이라는 단어를 사용하는 경우 해당 단어는 인식되지 않습니다. 경로 단추를 사용자 지정하고 스타일을 적용하려면 승인 단어를 이 설정에 추가해야 합니다.

**** client_specialRouts_names:리소스 파일에서 사용자 지정된 문자열 값을 찾는 데 사용되는 키입니다. 이 설정의 각 항목에는 이름과 스타일에 대한 값이 포함되어야 합니다.

### JGroup 설정 {#jgroup-settings}

이러한 설정은 Adobe LiveCycle ES 2.5 이전 버전에서 업그레이드한 경우에만 나타납니다.

**** server_remoteevents_ClientTimeoutMilliseconds:JGroup이 이벤트 메시지를 기다리는 최대 시간입니다. 이 설정은 변경할 수 없습니다.

**** server_remoteevents_ServerTimeoutMilliseconds:서버에서 JGroup 메시지 수신을 위한 시간 초과. 이 옵션은 서버에서 클라이언트로 메시지를 보내는 지연을 설정합니다.

**** server_remoteevents_JChannelConnectionProperties:RemoteEvent 서비스에서 서비스 이벤트를 처리하는 서버 및 Workspace의 모든 인스턴스 간에 통신하는 데 사용되는 JGroup의 연결 속성입니다.

멀티캐스트 IP 주소(mcast_addr), 멀티캐스트 IP 포트(mcast_port) 및 멀티캐스트 패킷의 TTL(ip_ttl)에 대한 UDP 값을 변경해야 할 수 있습니다. 기본적으로 멀티캐스트 IP 주소와 포트 값은 임의로 생성되며 일반적으로 값을 변경할 필요가 없습니다. 그러나 회사에서 멀티캐스트 IP 주소의 특정 멀티캐스트 범위와 관련된 네트워크 정책을 가지고 있는 경우 값을 변경해야 할 수 있습니다.

***참고&#x200B;**:TTL은 클러스터의 서버 간 네트워크 스위치 수보다 커야 합니다.그러나 값이 너무 높게 설정되면 멀티캐스트 패킷이 서브넷으로 이동하면서 해당 패킷이 무시됩니다.*

이 설정의 나머지 속성은 변경할 수 없습니다.

**** server_remoteevents_JGroupName:원격 이벤트 통신에 사용되는 JGroup의 이름입니다. 이 값은 임의로 생성되어 클러스터의 충돌을 방지합니다. 이 값은 변경할 수 없습니다.

그룹 및 작업 공간에 대한 자세한 내용은 JGroups 및 AEM [양식 작업 영역 - 설명을 참조하십시오](https://blogs.adobe.com/livecycle/2011/03/jgroups-and-livecycle-workspace-explained.html).

### formView 설정 {#formview-settings}

**** client_formView_openFormInFullScreen:작업 공간에서 전체 화면 모드로 모든 양식을 표시하려면 이 옵션을 true로 설정합니다. 기본적으로 이 옵션은 false로 설정되며 양식은 전체 화면 모드로 표시되지 않습니다. 사용자 서비스에는 작업에 연결된 문서를 전체 화면 모드로 여는 옵션이 포함되어 있습니다. 이를 통해 프로세스별로 디스플레이를 제어할 수 있습니다.

**** client_routs_formViewOnly:[True]로 설정하면 경로가 [작업 영역]의 카드 보기나 목록 보기에 표시되지 않습니다. 기본값은 카드 보기 및 목록 보기에 경로가 표시됨을 의미하는 False입니다.

### 기타 설정 {#other-settings}

**** client_mimeTypes_openOutsideBrowser:작업 영역 브라우저 인스턴스 외부에서 열 문서의 MIME 유형입니다. 조직의 프로세스에 추가 MIME 유형이 필요한 경우 여기에서 지정합니다. 기본값은 다음과 같습니다.

* `application/msword`
* `application/msexcel`
* `application/ms-powerpoint`

**** client_customUI_caching:사용자 지정 작업 사용자 인터페이스를 캐시합니다.

**** server_debugLevel:이 설정을 변경하지 마십시오.

**** client_pollingInterval:Flex 작업 영역에서 (JEE의 AEM 양식에 대해 더 이상 사용되지 않음) 새 및 수정된 작업을 감지하기 위해 사용되는 폴링 간격(초)을 설정합니다. 기본값은 3초입니다. AEM Forms 작업 영역에서는 작동하지 않습니다.

**** client_systemContext_name:AEM Forms Workspace에서 작업의 첨부 파일에 대해 추가된 사람 필드(예: 시민)에 표시할 사용자 지정 이름을 지정합니다.

사용자 지정 이름을 정의하려면

`<client_systemContext_name>[custom name to display]</client_systemContext_name>`

**참고**:데모 *애플리케이션의 경우 기본 표시 이름은&#x200B;**시민입니다**. 사용자가 만드는 사용자 정의 응용 프로그램의 경우 기본 표시 이름은&#x200B;**시스템 컨텍스트 계정입니다**.***** client_idleTimeout:사용자가 특정 시간 동안 비활성 상태로 유지되면 AEM Forms 작업 공간 세션이 만료됩니다. 이 기능을 활성화하려면 전역 설정 &lt;client_idleTimeout>IDLE_TIMEOUT_*IN_SECONDS*&lt;/client_idleTimeout>에 항목을 추가합니다. 값 0을 지정하여 유휴 시간 초과를 비활성화할 수 있습니다. 시간은 초 단위로 지정됩니다.
