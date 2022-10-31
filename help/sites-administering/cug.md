---
title: 폐쇄된 사용자 그룹 생성
seo-title: Creating a Closed User Group
description: 폐쇄된 사용자 그룹을 만드는 방법을 알아봅니다.
seo-description: Learn how to create a Closed User Group.
uuid: dc3c7dbd-2e86-43f9-9377-3b75053203b3
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 6ae57874-a9a1-4208-9001-7f44a1f57cbe
docset: aem65
exl-id: 9efba91d-45e8-42e1-9db6-490d21bf7412
source-git-commit: a5f3e33a6abe7ac1bbd610a8528fd599d1ffd2aa
workflow-type: tm+mt
source-wordcount: '794'
ht-degree: 3%

---

# 폐쇄된 사용자 그룹 생성{#creating-a-closed-user-group}

폐쇄된 사용자 그룹(CUG)은 게시된 인터넷 사이트 내에 있는 특정 페이지에 대한 액세스를 제한하는 데 사용됩니다. 이러한 페이지에서는 지정된 구성원이 로그인하여 보안 자격 증명을 제공해야 합니다.

웹 사이트 내에서 이러한 영역을 구성하려면 다음을 수행합니다.

* [실제 폐쇄된 사용자 그룹을 생성하고 구성원을 지정합니다.](#creating-the-user-group-to-be-used).

* [이 그룹을 필요한 페이지에 적용](#applying-your-closed-user-group-to-content-pages) 및 CUG 구성원이 사용할 로그인 페이지를 선택(또는 만들기)합니다. CUG를 컨텐츠 페이지에 적용할 때도 지정됩니다.

* [일부 양식의 링크를 보호된 영역 내의 적어도 한 페이지에 만듭니다.](#linking-to-the-realm)가 표시되지 않으면 표시되지 않습니다.
* [dispatcher 구성](#configure-dispatcher-for-cugs) 사용 중인 경우.

>[!CAUTION]
>
>폐쇄된 사용자 그룹(CUG)은 항상 성능을 염두에 두고 만들어야 합니다.
>
>CUG의 사용자 및 그룹 수가 제한되지 않지만 페이지의 CUG가 많으면 렌더링 성능이 저하될 수 있습니다.
>
>성능 테스트를 수행할 때 CUG의 영향을 항상 고려해야 합니다.

## 사용할 사용자 그룹 만들기 {#creating-the-user-group-to-be-used}

폐쇄된 사용자 그룹을 생성하려면

1. 이동 **도구 - 보안** AEM 홈 화면

   >[!NOTE]
   >
   >자세한 내용은 [사용자 및 그룹 관리](/help/sites-administering/security.md#managing-users-and-groups) 사용자 및 그룹 만들기 및 구성에 대한 자세한 내용은

1. 을(를) 선택합니다 **그룹** 다음 화면에서 카드를 표시합니다.

   ![스크린샷_2018-10-30at145502](assets/screenshot_2018-10-30at145502.png)

1. 누르기 **만들기** 새 그룹을 만들려면 오른쪽 상단 모서리의 단추를 클릭하십시오.
1. 새 그룹의 이름을 지정합니다. 예 `cug_access`.

   ![스크린샷_2018-10-30at151459](assets/screenshot_2018-10-30at151459.png)

1. 로 이동합니다. **멤버** 탭을 선택하고 필요한 사용자를 이 그룹에 지정합니다.

   ![스크린샷_2018-10-30at151808](assets/screenshot_2018-10-30at151808.png)

1. CUG에 지정한 모든 사용자를 활성화합니다. 이 경우 `cug_access`.
1. 게시 환경에서 사용할 수 있도록 폐쇄된 사용자 그룹을 활성화합니다. 이 예에서 `cug_access`.

## 컨텐츠 페이지에 닫힌 사용자 그룹 적용 {#applying-your-closed-user-group-to-content-pages}

페이지에 CUG를 적용하려면:

1. CUG에 지정할 제한된 섹션의 루트 페이지로 이동합니다.
1. 축소판을 클릭한 다음 클릭하여 페이지를 선택합니다 **속성** 상단 패널에서 을 선택합니다.

   ![스크린샷_2018-10-30at162632](assets/screenshot_2018-10-30at162632.png)

1. 다음 창에서 **고급** 탭.
1. 아래로 스크롤하여 **인증 요구 사항** 섹션을 참조하십시오.

1. 아래의 구성 경로를 추가한 다음 Save 키를 누릅니다.
1. 다음으로, **권한** 탭을 누르고 키를 누릅니다 **폐쇄된 사용자 그룹 편집** 버튼을 클릭합니다.

   ![스크린샷_2018-10-30at163003](assets/screenshot_2018-10-30at163003.png)

   >[!NOTE]
   >
   >권한 탭의 CUG는 블루프린트에서 라이브 카피로 롤아웃할 수 없습니다. 라이브 카피를 구성할 때 이를 염두에 두고 계획을 세우십시오.
   >
   >자세한 내용은 [이 페이지](closed-user-groups.md#aem-livecopy).

1. 다음 창에서 CUG를 찾아 추가합니다. 이 경우 라는 그룹을 추가합니다 **cug_access**. 마지막으로 **저장**.
1. 클릭 **활성화됨** 이 페이지(및 모든 하위 페이지)가 CUG에 속하도록 정의합니다.
1. 을(를) 지정합니다. **로그인 페이지** 해당 그룹의 구성원이 사용할 것입니다. 예:

   `/content/geometrixx/en/toolbar/login.html`

   선택 사항이며, 비워 두면 표준 로그인 페이지가 사용됩니다.

1. 추가 **수락된 그룹**. 그룹을 추가하려면 + 를 사용하고, 제거하려면 -을 사용하십시오. 이러한 그룹의 구성원만 로그인하고 페이지에 액세스할 수 있습니다.
1. 할당 **영역** (필요한 경우 페이지 그룹의 이름입니다.) 페이지 제목을 사용하려면 비워 둡니다.
1. 클릭 **확인** 세부 항목을 저장합니다.

자세한 내용은 [Identity Management](/help/sites-administering/identity-management.md) 게시 환경의 프로필에 대한 정보를 확인하고 로그인 및 로그아웃할 양식을 제공합니다.

## 영역에 연결 {#linking-to-the-realm}

CUG 영역에 대한 모든 링크의 대상이 익명 사용자에게 표시되지 않으므로 링크 검사기는 이러한 링크를 제거합니다.

이를 방지하려면 CUG 영역 내의 페이지를 가리키는 보호되지 않은 리디렉션 페이지를 만드는 것이 좋습니다. 그런 다음 탐색 항목이 링크 확인 문제를 일으키지 않고 렌더링됩니다. 실제로 리디렉션 페이지에 액세스할 때만 로그인 자격 증명을 성공적으로 제공한 후 CUG 영역 내에서 사용자가 리디렉션됩니다.

## CUG에 대한 Dispatcher 구성 {#configure-dispatcher-for-cugs}

Dispatcher를 사용하는 경우 다음 속성을 사용하여 Dispatcher 팜을 정의해야 합니다.

* [virtualhosts](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#identifying-virtual-hosts-virtualhosts): CUG가 적용되는 페이지의 경로와 일치합니다.
* \sessionmanagement: 아래를 참조하십시오.
* [캐시](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#configuring-the-dispatcher-cache-cache): CUG가 적용되는 파일에 대한 전용 캐시 디렉토리입니다.

### CUG에 대한 Dispatcher 세션 관리 구성 {#configuring-dispatcher-session-management-for-cugs}

구성 [dispatcher.any 파일의 세션 관리](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#enabling-secure-sessions-sessionmanagement) CUG용. CUG 페이지에 대한 액세스를 요청할 때 사용되는 인증 처리기는 세션 관리를 구성하는 방법을 결정합니다.

```xml
/sessionmanagement
    ...
    /header "Cookie:login-token"
    ...
```

>[!NOTE]
>
>Dispatcher 팜에 세션 관리가 활성화되어 있으면 팜에서 처리하는 모든 페이지가 캐시되지 않습니다. CUG 외부의 페이지를 캐시하려면 dispatcher에서 두 번째 팜을 만듭니다.any
>CUG가 아닌 페이지를 처리합니다.

1. 구성 [/sessionmanagement](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#enabling-secure-sessions-sessionmanagement) 다음을 정의하여 `/directory`; 예:

   ```xml
   /sessionmanagement
     {
     /directory "/usr/local/apache/.sessions"
     ...
     }
   ```

1. 설정 [/allowAuthorized](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#caching-when-authentication-is-used) to `0`.
