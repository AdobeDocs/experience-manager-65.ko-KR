---
title: 사용자 적시 프로비저닝
description: 적시 프로비저닝을 사용하여 사용자가 인증에 성공한 후 해당 사용자를 사용자 관리에 추가하고 관련 역할 및 그룹을 새 사용자에게 동적으로 할당합니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 7bde0a09-192a-44a8-83d0-c18e335e9afa
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: ht
source-wordcount: '575'
ht-degree: 100%

---

# 사용자 적시 프로비저닝 {#just-in-time-user-provisioning}

AEM Forms는 사용자 관리에 아직 존재하지 않는 사용자의 적시 프로비저닝을 지원합니다. 적시 프로비저닝을 사용하면 자격 증명 인증에 성공한 후 사용자가 사용자 관리에 자동으로 추가됩니다. 또한 관련 역할 및 그룹이 새 사용자에게 동적으로 할당됩니다.

## 사용자 적시 프로비저닝의 필요성 {#need-for-just-in-time-user-provisioning}

기존 인증의 작동 방식은 다음과 같습니다.

1. 사용자가 AEM Forms에 로그인을 시도하면 사용자 관리에서 사용자의 자격 증명을 사용 가능한 모든 인증 공급자에게 순차적으로 전달합니다. (로그인 자격 증명에는 사용자 이름/암호 조합, Kerberos 티켓, PKCS7 서명 등이 포함됩니다.)
1. 인증 공급자가 자격 증명의 유효성을 검사합니다.
1. 그런 다음, 인증 공급자는 사용자가 사용자 관리 데이터베이스에 있는지 확인합니다. 다음과 같은 결과가 발생할 수 있습니다.

   **존재함:** 사용자가 현재 상태이고 잠금 해제된 경우 사용자 관리에서 인증 성공을 반환합니다. 그러나 사용자가 현재 상태가 아니거나 잠겨 있는 경우 사용자 관리에서 인증 실패를 반환합니다.

   **존재하지 않음:** 사용자 관리에서 인증 실패를 반환합니다.

   **잘못됨:** 사용자 관리에서 인증 실패를 반환합니다.

1. 인증 공급자가 반환한 결과를 평가합니다. 인증 공급자가 인증 성공을 반환하면 사용자는 로그인할 수 있습니다. 그렇지 않은 경우 사용자 관리에서는 다음 인증 공급자에게 확인합니다(2~3단계).
1. 사용 가능한 인증 공급자가 사용자 자격 증명의 유효성을 검사하지 못하면 인증 실패가 반환됩니다.

적시 프로비저닝이 구현된 경우 인증 공급자 중 하나가 사용자가 보유한 자격 증명의 유효성을 검사하면 사용자 관리에서 새 사용자가 동적으로 생성됩니다. (위에 명시된 기존 인증 절차의 3단계 이후)

## 사용자 적시 프로비저닝 구현 {#implement-just-in-time-user-provisioning}

### 적시 프로비저닝 API {#apis-for-just-in-time-provisioning}

AEM Forms는 다음과 같은 적시 프로비저닝 API를 제공합니다.

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

### 적시 프로비저닝이 활성화된 도메인 생성 시 고려 사항 {#considerations-while-creating-a-just-in-time-enabled-domain}

* 하이브리드 도메인에 대한 사용자 정의 `IdentityCreator`를 만드는 동안 로컬 사용자에 대해 더미 암호가 지정되었는지 확인합니다. 이 암호 필드를 비워 두지 마십시오.
* 권장 사항: `DomainSpecificAuthentication`을 사용하여 특정 도메인에 대해 사용자 자격 증명의 유효성을 검사합니다.

### 적시 프로비저닝이 활성화된 도메인 만들기 {#create-a-just-in-time-enabled-domain}

1. &#39;적시 프로비저닝 API&#39; 섹션의 API를 구현하는 DSC를 작성합니다.
1. DSC를 Forms 서버에 배포합니다.
1. 다음과 같이 적시 프로비저닝이 활성화된 도메인을 만듭니다.

   * 관리 콘솔에서 설정 > 사용자 관리 > 도메인 관리 > 새 엔터프라이즈 도메인을 클릭합니다.
   * 도메인을 구성하고 적시 프로비저닝 활성화를 선택합니다. <!--Fix broken link (See Setting up and managing domains).-->
   * 인증 공급자를 추가합니다. 인증 공급자를 추가하는 동안 새 인증 화면에서 등록된 ID 생성자와 할당 공급자를 선택합니다.

1. 새 도메인을 저장합니다.

## 백그라운드 동작 {#behind-the-scenes}

사용자가 AEM Forms에 로그인을 시도하고 인증 공급자가 해당 사용자 자격 증명을 수락한다고 가정해 보십시오. 사용자가 사용자 관리 데이터베이스에 아직 존재하지 않으면 해당 사용자의 신원 확인이 실패합니다. AEM Forms는 이제 다음 작업을 수행합니다.

1. 인증 데이터가 포함된 `UserProvisioningBO` 오브젝트를 만들고 자격 증명 맵에 배치합니다.
1. `UserProvisioningBO`에서 반환된 도메인 정보를 기반으로 해당 도메인에 등록된 `IdentityCreator` 및 `AssignmentProvider`를 가져오고 호출합니다.
1. `IdentityCreator`를 호출합니다. 성공적인 `AuthResponse`가 반환되면 자격 증명 맵에서 `UserInfo`를 추출합니다. 사용자가 생성된 후 그룹/역할 할당 및 기타 사후 처리를 위해 해당 정보를 `AssignmentProvider`에게 전달합니다.
1. 사용자가 성공적으로 생성되면 사용자의 로그인 시도를 성공으로 반환합니다.
1. 하이브리드 도메인의 경우 인증 공급자에게 제공된 인증 데이터에서 사용자 정보를 가져옵니다. 이 정보를 성공적으로 가져오면 사용자가 즉시 생성됩니다.

>[!NOTE]
>
>적시 프로비저닝 기능은 사용자를 동적으로 만드는 데 사용할 수 있는 `IdentityCreator`의 기본 구현과 함께 제공됩니다. 사용자는 도메인의 디렉터리와 연결된 정보를 사용하여 생성됩니다.
