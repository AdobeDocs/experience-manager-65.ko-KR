---
title: 적시 사용자 프로비저닝
description: 인증 성공 후 Just-in-time 프로비저닝을 사용하여 User Management에 사용자를 추가하고 관련 역할 및 그룹을 새 사용자에게 동적으로 할당합니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 7bde0a09-192a-44a8-83d0-c18e335e9afa
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 0%

---

# 적시 사용자 프로비저닝 {#just-in-time-user-provisioning}

AEM forms는 사용자 관리에 아직 존재하지 않는 사용자의 정시 프로비저닝을 지원합니다. 적시 프로비저닝을 사용하면 자격 증명이 성공적으로 인증된 후 사용자가 사용자 관리에 자동으로 추가됩니다. 또한 관련 역할 및 그룹은 새 사용자에게 동적으로 할당됩니다.

## 적시 사용자 프로비저닝 필요 {#need-for-just-in-time-user-provisioning}

다음은 기존 인증 작동 방식입니다.

1. 사용자가 AEM Forms에 로그인하려고 하면 User Management에서 사용 가능한 모든 인증 공급자에게 사용자 자격 증명을 순차적으로 전달합니다. (로그인 자격 증명에는 사용자 이름/암호 조합, Kerberos 티켓, PKCS7 서명 등이 포함됩니다.)
1. 인증 공급자가 자격 증명의 유효성을 검사합니다.
1. 그런 다음 인증 공급자는 사용자가 사용자 관리 데이터베이스에 있는지 여부를 확인합니다. 다음과 같은 결과가 가능합니다.

   **존재함:** 사용자가 현재 상태이고 잠금 해제된 경우 User Management는 인증 성공을 반환합니다. 그러나 사용자가 현재 상태가 아니거나 잠겨 있으면 User Management에서 인증 실패를 반환합니다.

   **존재하지 않음:** User Management가 인증 실패를 반환합니다.

   **잘못됨:** User Management가 인증 실패를 반환합니다.

1. 인증 공급자가 반환한 결과를 평가합니다. 인증 공급자가 인증 성공을 반환한 경우 사용자가 로그인할 수 있습니다. 그렇지 않으면 User Management에서 다음 인증 공급자에게 확인합니다(2-3단계).
1. 사용 가능한 인증 공급자가 사용자 자격 증명의 유효성을 검사하지 않으면 인증 실패가 반환됩니다.

Just-in-time 프로비저닝이 구현되면 인증 공급자 중 하나가 사용자 자격 증명의 유효성을 검사하는 경우 User Management에서 새 사용자가 동적으로 만들어집니다. (위의 기존 인증 절차에서 3단계 이후)

## 적시 사용자 프로비저닝 구현 {#implement-just-in-time-user-provisioning}

### 적시 프로비저닝을 위한 API {#apis-for-just-in-time-provisioning}

AEM forms는 적시 프로비저닝을 위해 다음 API를 제공합니다.

```java
package com.adobe.idp.um.spi.authentication  ;
publ ic interface IdentityCreator {
/**
* Tries  to create a user with the  in formation  provided in the <code>UserProvisioningBO</code> object.
* If the user is successfully created, a valid AuthResponse is returned along with the information using which the user was created.
* It is the responsibility of the IdentityCreator to set the User obje ct  in the cre dential map with th e  ke y  <code>UMA u thenticationUtil.authenticatedUserKey</code>
* The credentials are available in the <code>UserProvisioningBO</code> object in the 'credentials' property.
* If the IdentityCreator is unable to create a user due to any reason, it returns <code>null</code>
* @param userBO An object of <code>com.adobe. i dp.um . spi.authenti c ationUserProvisioningBO</code>
* @return */public AuthResponse create(UserProvisioningBO userBO);
/**
* Returns the name of the IdentityCreator which will be registered in preferences.
* This name is used to associate the IdentityProvider with the Auth Provider Configuration in the domain.
* @return The name of the Identity Creator which is recognized in Configuration.
*/
public String getName();
}
package com.adobe.idp.um.spi.authentication;
import com.adobe.idp.um.api.infomodel.User;
public interface AssignmentProvider {
/**
* Tries to assign roles or permissions or group memberships to users created via Just-in-time provisioning.
* @param user The User created via the Just-in-time provisioning process.
* @return a Boolean flag indicating whether the assignment was successful or not.
*/
public Boolean assign(User user);
/**
* Returns the name of the AssignmentProvider through which it is registered under preferences.
* This name is used to associate the AssignmentProvider with the Auth Provider Configuration in the domain.
* @return The name of the AssignmentProvider which is recognized in Configuration.
*/public String getName();
}
```

### Just-in-Time 활성화 도메인을 만드는 동안 고려 사항 {#considerations-while-creating-a-just-in-time-enabled-domain}

* 사용자 지정 항목을 만드는 동안 `IdentityCreator` 하이브리드 도메인의 경우 로컬 사용자에 대해 더미 암호가 지정되었는지 확인하십시오. 이 암호 필드를 비워 두지 마십시오.
* 권장 사항: 사용 `DomainSpecificAuthentication` 특정 도메인에 대한 사용자 자격 증명의 유효성을 검사합니다.

### 적시 활성화 도메인 만들기 {#create-a-just-in-time-enabled-domain}

1. &quot;API for just-in-time provisioning&quot; 섹션에서 API를 구현하는 DSC를 작성합니다.
1. Forms 서버에 DSC를 배포합니다.
1. Just-In-Time 활성화 도메인 만들기:

   * Administration Console에서 설정 > 사용자 관리 > 도메인 관리 > 새 엔터프라이즈 도메인을 클릭합니다.
   * 도메인을 구성하고 Enable Just In Time Provisioning 을 선택합니다. <!--Fix broken link (See Setting up and managing domains).-->
   * 인증 공급자를 추가합니다. 인증 공급자를 추가하는 동안 새 인증 화면에서 등록된 ID 작성자 및 할당 공급자를 선택합니다.

1. 새 도메인을 저장합니다.

## 비하인드 스토리 {#behind-the-scenes}

사용자가 AEM Forms에 로그인하려고 하고 인증 공급자가 사용자 자격 증명을 수락한다고 가정합니다. 사용자가 User Management 데이터베이스에 아직 없는 경우 해당 사용자에 대한 ID 검사가 실패합니다. 이제 AEM forms에서 다음 작업을 수행합니다.

1. 만들기 `UserProvisioningBO` 인증 데이터가 있는 개체를 자격 증명 맵에 놓습니다.
1. 에서 반환된 도메인 정보 기반 `UserProvisioningBO`, 등록된 을(를) 가져와 호출 `IdentityCreator` 및 `AssignmentProvider` 도메인을 위한 것입니다.
1. 호출 `IdentityCreator`. 성공적인 결과를 반환하는 경우 `AuthResponse`, 추출 `UserInfo` 자격 증명 맵에서 에 전달 `AssignmentProvider` 사용자를 만든 후 그룹/역할 할당 및 기타 모든 사후 처리용
1. 사용자가 성공적으로 생성되면 사용자의 로그인 시도를 성공한 것으로 반환합니다.
1. 하이브리드 도메인의 경우 인증 공급자에게 제공된 인증 데이터에서 사용자 정보를 가져옵니다. 이 정보를 성공적으로 가져오면 즉시 사용자를 만듭니다.

>[!NOTE]
>
>적시 프로비저닝 기능은 의 기본 구현과 함께 제공됩니다. `IdentityCreator` 를 사용하여 사용자를 동적으로 만들 수 있습니다. 사용자는 도메인의 디렉터리와 관련된 정보로 만들어집니다.
