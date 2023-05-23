---
title: 전역 설정 가져오기 및 내보내기
seo-title: Importing and exporting global settings
description: 작업 공간에 대한 검색 템플릿 정의와 전역 설정을 가져오고 내보낼 수 있습니다.
seo-description: You can import and export search template definitions and global settings for Workspace.
uuid: 8f1f210d-e850-4b2c-bb5a-942fa8299791
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_workspace
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 72fe5749-2fa2-442f-b679-7889faeafcac
exl-id: cdb7ff54-7891-45b1-a921-10b01ef5188d
source-git-commit: 0c7dba43dad8608b4a5de271e1e44942c950fb16
workflow-type: tm+mt
source-wordcount: '1245'
ht-degree: 0%

---

# 전역 설정 가져오기 및 내보내기 {#importing-and-exporting-global-settings}

작업 공간에 대한 검색 템플릿 정의와 전역 설정을 가져오고 내보낼 수 있습니다.

>[!NOTE]
>
>Flex Workspace는 AEM Forms 릴리스에서 더 이상 사용되지 않습니다.

예를 들어 검색 템플릿 정의 및 전역 설정을 한 환경에서 내보내고 이를 다른 환경으로 가져와서 개발 환경에서 프로덕션 환경으로 이동할 수 있습니다.

전역 설정 파일을 내보내면 XML 또는 텍스트 편집기에서 설정을 수정할 수 있습니다. 그러나 편집할 수 있는 설정은 JChannelConnectionProperties, formViewOnly 및 specialRoutes 설정뿐입니다. 자세한 내용은 [작업 영역 전역 설정](importing-exporting-global-settings.md#workspace-global-settings).


>[!NOTE]
>
>전역 설정 파일에서 이벤트 속성을 변경한 경우 서버를 다시 시작해야 합니다.

## 검색 템플릿 정의 가져오기 {#import-a-search-template-definition}

1. 관리 콘솔에서 서비스 > 작업 공간 > 전역 관리 를 클릭합니다.
1. 검색 템플릿 정의 가져오기 상자에서 파일 선택을 클릭하고 검색 템플릿을 선택합니다. 원래 Workspace 인스턴스에서 내보낸 검색 템플릿 정의만 가져올 수 있습니다.
1. 가져오기를 클릭합니다.

## 검색 템플릿 정의 내보내기 {#export-a-search-template-definition}

1. 전역 관리 페이지의 검색 템플릿 정의 내보내기에서 모두 나열 을 클릭합니다.
1. 검색 템플릿 목록에서 내보낼 템플릿을 선택합니다.

   >[!NOTE]
   >
   >템플릿을 두 개 이상 선택할 수 있지만, 마지막으로 선택한 템플릿만 내보내집니다.

1. 내보내기 를 클릭한 다음 컴퓨터에 파일을 저장합니다.

## 전역 설정 가져오기 {#import-global-settings}

1. 전역 관리 페이지의 전역 설정 가져오기에서 파일 선택을 클릭하고 전역 설정 파일을 선택합니다. 전역 설정 파일은 XML 형식이어야 합니다.
1. 가져오기를 클릭합니다.

## 전역 설정 내보내기 {#export-global-settings}

1. 전역 관리 페이지의 전역 설정 내보내기에서 내보내기를 클릭합니다.
1. 파일을 컴퓨터에 저장합니다.

## 작업 영역 전역 설정 {#workspace-global-settings}

전역 설정 파일을 수정할 수 있지만 편집할 수 있는 설정은 JChannelConnectionProperties, formViewOnly 및 specialRoutes 설정뿐입니다.

>[!NOTE]
>
>Flex Workspace는 AEM Forms 릴리스에서 더 이상 사용되지 않습니다.

Workspace 전역 설정 파일에는 다음 설정이 포함되어 있습니다.

### specialRoutes 설정 {#specialroutes-settings}

다음 *specialRoutes* 설정은 작업 영역에서 특수 경로 승인 및 거부의 속성을 지정합니다. 특정 상황에서 이러한 경로에 대한 버튼이 Workspace의 작업 카드에 표시되며 사용자는 양식을 열지 않고도 선택할 수 있습니다. 전역 설정 파일에서 specialRoots 설정을 수정하여 승인 및 거부를 위해 사용자 지정된 이름을 추가하거나 추가 경로를 만들 수 있습니다.

**client_specialRoutes_routes_approve_style:** 작업 영역 테마에 있는 스타일의 이름으로, 승인 단추 아이콘을 식별합니다. 스타일에는 활성화 아이콘과 비활성화 아이콘의 값이 포함되어야 합니다. 사용자 지정 단추의 스타일을 정의하려면 다음 템플릿을 사용해야 합니다.
` .buttonApprove {  icon: Embed('images/LC_DirectApprove_Sm_N.png');  disabledIcon: Embed('images/LC_DirectApprove_Sm_D.png');  paddingLeft: 5;  }` 작업 영역 CSS 파일은 adobe-workspace-client.ear > adobe-workspace-client.war 파일에 있는 workspace-theme.swf 파일에 포함되어 있습니다. 작업 영역의 모양을 변경하려면 작업 영역-테마.swf 파일을 다시 컴파일해야 합니다.

**client_specialRoutes_routes_deny_names:** Workbench 사용자가 사용할 수 있는 다양한 문자열은 &quot;거부&quot;로 해석됩니다. 문자열은 대/소문자를 구분합니다. 예를 들어 기본값은 deny입니다. Workbench 사용자가 프로세스에서 Deny라는 단어를 사용하는 경우 해당 단어가 인식되지 않습니다. 경로 단추를 사용자 지정하고 스타일을 적용하려면 이 설정에 거부 라는 단어를 추가해야 합니다.

**client_specialRoutes_routes_deny_style:** 작업 영역 테마 파일에 있는 스타일의 이름으로, 거부 단추 아이콘을 식별합니다. 스타일에는 활성화 아이콘과 비활성화 아이콘의 값이 포함되어야 합니다. 사용자 지정 단추의 스타일을 정의하려면 다음 템플릿을 사용해야 합니다.
`  .buttonDeny {   icon: Embed('images/LC_DirectDeny_Sm_N.png');   disabledIcon: Embed('images/LC_DirectDeny_Sm_D.png');   paddingLeft: 0;   }` **client_specialRoutes_routes_approve_names:** Workbench 사용자가 &quot;승인&quot;으로 해석하는 데 사용할 수 있는 다양한 문자열. 문자열은 대/소문자를 구분합니다. 예를 들어 기본값은 승인입니다. Workbench 사용자가 프로세스에서 승인이라는 단어를 사용하는 경우 해당 단어가 인식되지 않습니다. 경로 단추를 사용자 지정하고 스타일을 적용하려면 이 설정에 승인이라는 단어를 추가해야 합니다.

**client_specialRoutes_names:** 리소스 파일에서 사용자 지정된 문자열 값을 찾는 데 사용되는 키입니다. 이 설정의 각 항목에는 이름 및 스타일에 대한 값이 포함되어야 합니다.

### JGroup 설정 {#jgroup-settings}

이러한 설정은 Adobe LiveCycle ES 2.5 이하에서 업그레이드한 경우에만 나타납니다.

**server_remoteevents_ClientTimeoutMilliseconds:** JGroup이 이벤트 메시지를 기다리는 최대 시간입니다. 이 설정은 변경해서는 안 됩니다.

**server_remoteevents_ServerTimeoutMillisefs:** 서버에서 JGroup 메시지를 수신하기 위한 시간 제한. 이 옵션은 서버에서 클라이언트로 메시지를 보내는 데 걸리는 시간을 설정합니다.

**server_remoteevents_JChannelConnectionProperties:** RemoteEvent 서비스에서 서비스 이벤트를 처리하는 서버와 작업 영역의 모든 인스턴스 간에 통신하는 데 사용되는 JGroup에 대한 연결 속성입니다.

멀티캐스트 IP 주소(mcast_addr), 멀티캐스트 IP 포트(mcast_port) 및 멀티캐스트 패킷 TTL(ip_ttl)의 UDP 값을 변경해야 할 수 있습니다. 기본적으로 멀티캐스트 IP 주소 및 포트 값은 임의로 생성되며 일반적으로 값을 변경할 필요가 없습니다. 그러나 회사에 멀티캐스트 IP 주소의 특정 멀티캐스트 범위와 관련된 네트워크 정책이 있는 경우 값을 변경해야 할 수 있습니다.

>[!NOTE]
>
>TTL은 클러스터의 서버 간 네트워크 스위치 수보다 커야 합니다. 그러나 값이 너무 높게 설정되면 멀티캐스트 패킷이 서브넷으로 이동하여 해당 서브넷이 삭제될 수 있습니다.

이 설정의 나머지 속성은 변경해서는 안 됩니다.

**server_remoteevents_JGroupName:** 원격 이벤트 통신에 사용되는 JGroup의 이름입니다. 이 값은 클러스터에서 충돌을 방지하기 위해 임의로 생성됩니다. 이 값은 변경해서는 안 됩니다.

<!--

For additional information on JGroups and Workspace, see [JGroups and AEM forms Workspace - Explained](https://blogs.adobe.com/livecycle/2011/03/jgroups-and-livecycle-workspace-explained.html).

-->

### formView 설정 {#formview-settings}

**client_formView_openFormInFullScreen:** 작업 영역의 모든 양식을 전체 화면 모드로 표시하려면 이 옵션을 true로 설정합니다. 기본적으로 이 옵션은 false로 설정되어 있고 양식이 전체 화면 모드로 표시되지 않습니다. 사용자 서비스에는 전체 화면 모드에서 작업과 연결된 문서를 여는 옵션이 포함되어 있습니다. 따라서 프로세스별로 디스플레이를 제어할 수 있습니다.

**client_routes_formViewOnly:** True로 설정하면 Workspace의 카드 보기 또는 목록 보기에 경로가 표시되지 않습니다. 기본값은 False로, 카드 보기와 목록 보기에 경로가 표시됨을 의미합니다.

### 기타 설정 {#other-settings}

**client_mimeTypes_openOutsideBrowser:** Workspace 브라우저 인스턴스 외부에서 열리는 문서의 MIME 유형입니다. 조직의 프로세스에 추가 MIME 유형이 필요한 경우 여기에 지정하십시오. 기본값은 다음과 같습니다.

* `application/msword`
* `application/msexcel`
* `application/ms-powerpoint`

**client_customUI_caching:** 사용자 지정 작업 사용자 인터페이스를 캐시합니다.

**server_debugLevel:** 이 설정을 변경하지 마십시오.

**client_pollingInterval:** (JEE에서 AEM Forms가 더 이상 사용되지 않음) Flex 작업 영역에서 새 작업 및 수정된 작업을 감지하는 데 사용되는 폴링 간격(초)을 설정합니다. 기본값은 3초입니다. AEM Forms 작업 영역에서는 작동하지 않습니다.

**client_systemContext_name:** AEM Forms Workspace에서 작업의 첨부 파일에 대한 추가한 사람 필드(첨부 파일 탭)에 표시할 사용자 정의 이름(예: 시민)을 지정합니다.

사용자 정의 이름을 정의하려면

`<client_systemContext_name>[custom name to display]</client_systemContext_name>`

>[!NOTE]
>
>데모 애플리케이션의 경우 기본 표시 이름은 입니다. **Citizen**. 사용자가 만드는 사용자 정의 응용 프로그램의 경우 기본 표시 이름은 입니다. **시스템 컨텍스트 계정**.
>
>**client_idleTimeout:** 사용자가 특정 시간 동안 비활성 상태인 경우 AEM Forms 작업 영역 세션이 만료됩니다. 이 기능을 활성화하려면 [전역 설정]에 항목을 추가합니다 &lt;client_idletimeout>*IDLE_TIMEOUT_IN_SECONDS*&lt;/client_idletimeout>. 값 0을 지정하여 유휴 시간 제한을 비활성화할 수 있습니다. 시간은 초 단위로 지정됩니다.
