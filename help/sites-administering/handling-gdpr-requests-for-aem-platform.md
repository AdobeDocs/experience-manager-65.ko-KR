---
title: AEM Foundation에 대한 GDPR 요청 처리
seo-title: AEM Foundation에 대한 GDPR 요청 처리
description: AEM Foundation에 대한 GDPR 요청 처리
seo-description: 'null'
uuid: d470061c-bbcf-4d86-9ce3-6f24a764ca39
contentOwner: sarchiz
discoiquuid: 8ee843b6-8cea-45fc-be6c-99c043f075d4
exl-id: 411d40ab-6be8-4658-87f6-74d2ac1a4913
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 7%

---

# AEM Foundation{#handling-gdpr-requests-for-the-aem-foundation}에 대한 GDPR 요청 처리

>[!IMPORTANT]
>
>아래 섹션에서는 GDPR이 예로 사용되지만, 포함된 세부 사항은 GDPR, CCPA 등 모든 데이터 보호 및 개인 정보 보호 규정에 적용됩니다.

## AEM Foundation GDPR 지원 {#aem-foundation-gdpr-support}

AEM Foundation 수준에서 저장된 개인 데이터는 사용자 프로필입니다. 따라서 이 문서의 정보에서는 주로 사용자 프로필에 액세스하여 삭제하고 GDPR 액세스 및 삭제 요청을 각각 처리하는 방법을 다룹니다.

## 사용자 프로필 액세스 {#accessing-a-user-profile}

### 수동 단계 {#manual-steps}

1. **[!UICONTROL 설정 - 보안 - 사용자]**&#x200B;로 이동하거나 `https://<serveraddress>:<serverport>/libs/granite/security/content/useradmin.html`로 직접 이동하여 사용자 관리 콘솔을 엽니다

   ![useradmin2](assets/useradmin2.png)

1. 그런 다음 페이지 상단의 검색 표시줄에 이름을 입력하여 해당 사용자를 검색합니다.

   ![usersearch](assets/usersearch.png)

1. 마지막으로 사용자 프로필을 클릭하여 연 다음 **[!UICONTROL 세부 정보]** 탭 아래에서 을 선택합니다.

   ![userprofile_small](assets/userprofile_small.png)

### HTTP API {#http-api}

앞에서 설명한 바와 같이, Adobe은 자동화를 용이하게 하기 위해 사용자 데이터에 액세스하기 위한 API를 제공합니다. 사용할 수 있는 API 유형에는 몇 가지가 있습니다.

**UserProperties API**

```shell
curl -u user:password http://localhost:4502/libs/granite/security/search/profile.userproperties.json\?authId\=cavery
```

**Sling API**

*사용자 홈 살펴보기:*

```xml
curl -g -u user:password 'http://localhost:4502/libs/granite/security/search/authorizables.json?query={"condition":[{"named":"cavery"}]}'
     {"authorizables":[{"type":"user","authorizableId_xss":"cavery","authorizableId":"cavery","name_xss":"Carlene Avery","name":"Carlene Avery","home":"/home/users/we-retail/DSCP-athB1NYLBXvdTuN"}],"total":1}
```

*사용자 데이터 검색*

위의 명령에서 반환된 JSON 페이로드의 홈 속성의 노드 경로 사용:

```shell
curl -u user:password  'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile.-1.json'
```

```shell
curl -u user:password  'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profiles.-1.json'
```

## 사용자 비활성화 및 연결된 프로필 삭제 {#disabling-a-user-and-deleting-the-associated-profiles}

### 사용자 {#disable-user} 비활성화

1. 위에 설명된 대로 사용자 관리 콘솔을 열고 해당 사용자를 검색합니다.
1. 사용자를 마우스로 가리킨 다음 선택 아이콘을 클릭합니다. 프로필이 선택되었음을 나타내는 회색으로 바뀝니다.

1. 위 메뉴에서 Disable 단추를 눌러 사용자를 비활성화합니다.

   ![userdisable](assets/userdisable.png)

1. 마지막으로 작업을 확인합니다.

   ![image2018-2-6_1-40-58](assets/image2018-2-6_1-40-58.png)

   그러면 사용자 인터페이스에 프로필 카드에 잠금을 로그아웃하고 추가하여 사용자가 비활성화되었음을 나타냅니다.

   ![비활성화된 사용자](assets/disableduser.png)

### 사용자 프로필 정보 삭제 {#delete-user-profile-information}

1. CRXDE Lite에 로그인한 다음 `[!UICONTROL userId]`을 검색합니다.

   ![image2018-2-6_1-57-11](assets/image2018-2-6_1-57-11.png)

1. 기본적으로 `[!UICONTROL /home/users]` 아래에 있는 사용자 노드를 엽니다.

   ![image2018-2-6_1-58-25](assets/image2018-2-6_1-58-25.png)

1. 프로필 노드 및 모든 해당 하위 노드를 삭제합니다. AEM 버전에 따라 프로필 노드에 두 가지 형식이 있습니다.

   1. `[!UICONTROL /profile]` 아래의 기본 개인 프로필
   1. `[!UICONTROL /profiles]`: AEM 6.5를 사용하여 만든 새 프로필의 경우.

   ![image2018-2-6_2-0-4](assets/image2018-2-6_2-0-4.png)

### HTTP API {#http-api-1}

다음 절차에서는 `curl` 명령줄 도구를 사용하여 **[!UICONTROL cavery]** `userId`로 사용자를 비활성화하고 기본 위치에서 사용할 수 있는 프로필을 삭제하는 방법을 보여 줍니다.

* *사용자 홈 살펴보기*

```shell
curl -g -u user:password 'http://localhost:4502/libs/granite/security/search/authorizables.json?query={"condition":[{"named":"cavery"}]}'
     {"authorizables":[{"type":"user","authorizableId_xss":"cavery","authorizableId":"cavery","name_xss":"Carlene Avery","name":"Carlene Avery","home":"/home/users/we-retail/DSCP-athB1NYLBXvdTuN"}],"total":1}
```

* *사용자 비활성화*

위의 명령에서 반환된 JSON 페이로드의 홈 속성의 노드 경로 사용:

```shell
curl -X POST -u user:password -FdisableUser="describe the reasons for disabling this user (GDPR in this case)" 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN.rw.userprops.html'
```

* *사용자 프로필 삭제*

계정 검색 명령에서 반환된 JSON 페이로드의 홈 속성의 노드 경로 및 알려진 기본 프로필 노드 위치 사용:

```shell
curl -X POST -u user:password -H "Accept: application/json,**/**;q=0.9" -d ':operation=delete' 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile'
```

```shell
curl -X POST -u user:password -H "Accept: application/json,**/**;q=0.9" -d ':operation=delete' 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile'
```
