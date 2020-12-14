---
title: 적시 사용자 프로비저닝
seo-title: 적시 사용자 프로비저닝
description: 적시 프로비저닝 기능을 사용하여 인증 성공 후 사용자를 사용자 관리에 추가하고 관련 역할 및 그룹을 새로운 사용자에게 동적으로 할당합니다.
seo-description: 적시 프로비저닝 기능을 사용하여 인증 성공 후 사용자를 사용자 관리에 추가하고 관련 역할 및 그룹을 새로운 사용자에게 동적으로 할당합니다.
uuid: a5ad4698-70bb-487b-a069-7133e2f420c2
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e80c3f98-baa1-45bc-b713-51a2eb5ec165
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 0%

---


# 적시 사용자 프로비저닝 {#just-in-time-user-provisioning}

AEM 양식은 사용자 관리에 아직 존재하지 않는 사용자의 적시 제공을 지원합니다. 적시 프로비저닝 기능을 사용하면 자격 증명이 성공적으로 인증되면 사용자가 사용자 관리에 자동으로 추가됩니다. 또한 관련 역할 및 그룹이 새 사용자에게 동적으로 할당됩니다.

## 적시 사용자 프로비저닝 필요 {#need-for-just-in-time-user-provisioning}

일반적인 인증 작동 방식은 다음과 같습니다.

1. 사용자가 AEM 양식에 로그인하려고 하면 사용자 관리는 사용 가능한 모든 인증 공급자에 사용자 자격 증명을 순차적으로 전달합니다. 로그인 자격 증명에는 사용자 이름/암호 조합, Kerberos 티켓, PKCS7 서명 등이 포함됩니다.
1. 인증 공급자가 자격 증명을 검증합니다.
1. 그러면 인증 공급자가 사용자가 사용자 관리 데이터베이스에 있는지 확인합니다. 다음과 같은 결과가 가능합니다.

   **존재:** 사용자가 현재 상태이고 잠금 해제되어 있으면 사용자 관리는 인증 성공을 반환합니다. 그러나 사용자가 현재 상태가 아니거나 잠겨 있으면 사용자 관리에서 인증 실패를 반환합니다.

   **존재하지 않음:** 사용자 관리가 인증 실패를 반환합니다.

   **유효하지 않음:** 사용자 관리가 인증 오류를 반환합니다.

1. 인증 공급자가 반환한 결과가 평가됩니다. 인증 공급자가 인증 성공을 반환한 경우 사용자가 로그인할 수 있습니다. 그렇지 않은 경우 사용자 관리는 다음 인증 공급자를 확인합니다(2-3단계).
1. 사용 가능한 인증 공급자가 사용자 자격 증명을 검증하지 않으면 인증 오류가 반환됩니다.

적시 프로비저닝이 구현되면 인증 공급자 중 하나가 사용자 자격 증명을 검증하면 사용자 관리에서 새 사용자가 동적으로 만들어집니다. 위의 기존 인증 절차의 3단계 이후)

## 적시 사용자 프로비저닝 구현 {#implement-just-in-time-user-provisioning}

### 적시 프로비저닝용 API {#apis-for-just-in-time-provisioning}

AEM 양식은 Just-In-Time 프로비저닝을 위한 다음 API를 제공합니다.

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

### 적시에 활성화된 도메인 {#considerations-while-creating-a-just-in-time-enabled-domain}을(를) 만드는 동안 고려 사항

* 하이브리드 도메인에 대한 사용자 지정 `IdentityCreator`을(를) 만드는 동안 로컬 사용자에 대해 더미 암호를 지정했는지 확인하십시오. 이 암호 필드를 비워 두지 마십시오.
* 권장 사항:특정 도메인에 대해 사용자 자격 증명을 확인하려면 `DomainSpecificAuthentication`을 사용합니다.

### 적시에 활성화된 도메인 {#create-a-just-in-time-enabled-domain} 만들기

1. &quot;적시 프로비저닝을 위한 API&quot; 섹션에서 API를 구현하는 DSC를 작성합니다.
1. DSC를 양식 서버에 배포합니다.
1. 적시에 활성화된 도메인을 만듭니다.

   * 관리 콘솔에서 설정 > 사용자 관리 > 도메인 관리 > 새 엔터프라이즈 도메인을 클릭합니다.
   * 도메인을 구성하고 Enable Just In Time Provisioning을 선택합니다.<!--Fix broken link (See Setting up and managing domains).-->
   * 인증 공급자를 추가합니다. 인증 공급자를 추가하는 동안 [새 인증] 화면에서 등록된 ID 생성자 및 할당 공급자를 선택합니다.

1. 새 도메인을 저장합니다.

## 백그라운드에서 {#behind-the-scenes}

사용자가 AEM 양식에 로그인하려고 하는데 인증 공급자가 사용자 자격 증명을 수락한다고 가정합니다. 사용자가 아직 사용자 관리 데이터베이스에 없으면 사용자에 대한 ID 검사가 실패합니다. 이제 AEM 양식에서 다음 작업을 수행합니다.

1. 인증 데이터를 사용하여 `UserProvisioningBO` 개체를 만들고 자격 증명 맵에 배치합니다.
1. `UserProvisioningBO`에서 반환한 도메인 정보를 기준으로 도메인에 대해 등록된 `IdentityCreator` 및 `AssignmentProvider`를 가져오고 호출합니다.
1. `IdentityCreator`을(를) 호출합니다. 성공한 `AuthResponse`을 반환하면 자격 증명 맵에서 `UserInfo`을 추출합니다. 사용자를 만든 후 그룹/역할 할당 및 기타 후속 처리를 위해 `AssignmentProvider`에 전달합니다.
1. 사용자가 성공적으로 만들어지면 사용자의 로그인 시도를 성공한 것으로 반환합니다.
1. 하이브리드 도메인의 경우 인증 공급자에 제공된 인증 데이터에서 사용자 정보를 가져옵니다. 이 정보를 성공적으로 가져오면 사용자를 바로 만듭니다.

>[!NOTE]
>
>적시 제공 기능은 사용자를 동적으로 만드는 데 사용할 수 있는 `IdentityCreator`의 기본 구현과 함께 제공됩니다. 사용자는 도메인의 디렉토리와 연관된 정보로 생성됩니다.

