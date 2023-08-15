---
title: Adobe 에셋 링크에 대한 Experience Manager Assets 구성
description: Creative Cloud 애플리케이션용 Adobe Asset Link 확장에 사용할 Experience Manager Assets을 구성합니다.
contentOwner: Vishabh Gupta
role: Admin
feature: Asset Management
exl-id: 3a9b44d4-1756-4ad5-91df-df8d53e82193
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '3148'
ht-degree: 2%

---

# Adobe 에셋 링크에 대한 Experience Manager Assets 구성 {#adobe-asset-link}

[AAL(Adobe 에셋 링크)](https://www.adobe.com/kr/creativecloud/business/enterprise/adobe-asset-link.html) 컨텐츠 작성 프로세스에서 광고 팀과 마케터 간의 협업을 간소화합니다. Adobe Experience Manager Assets를 Creative Cloud 데스크탑 앱 Adobe InDesign, Adobe Photoshop 및 Adobe Illustrator과 연결합니다. Asset Link Adobe 패널을 사용하면 크리에이티브가 가장 익숙한 크리에이티브 앱을 종료하지 않고도 AEM Assets에 저장된 컨텐츠에 액세스하고 이를 수정할 수 있습니다.

Asset Link에 사용할 Experience Manager Assets을 구성하려면 다음 작업을 구현하십시오. Experience Manager 관리자 계정을 사용하여 구성을 수행합니다.

1. 필요에 따라 패키지를 설치합니다. 세부 정보 위치: [전제 조건](#prerequisites).

1. 다음 중 한 방법으로 Experience Manager 구성 [수동](#manual-configuration) 또는 를 사용하여 [패키지](#configure-using-package).

1. Creative Cloud 라이선스가 있는 사용자를 Experience Manager 사용자와 매핑하려면 다음을 관리합니다. [사용자 액세스 제어](#user-access).

1. 만들기 [사용자 정의 쿼리 인덱스](#create-custom-index), 구성 [FPO 표현물](/help/assets/configure-fpo-renditions.md) InDesign의 경우 구성 [Adobe Stock 통합](/help/assets/aem-assets-adobe-stock.md), 및 구성 [시각적 또는 유사성 검색](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/search-assets.html#configvisualsearch).

## 다양한 기능에 대한 사전 요구 사항 및 지원 {#prerequisites}

필요에 따라 적절한 서비스 팩과 패키지를 설치해야 합니다. 각 Experience Manager 버전 및 특정 기능에 대한 다음 요구 사항을 참조하십시오.

| 에셋 기능 | Experience Manager 버전 및 지원 요구 사항 |
|--- |--- |
| Asset Link 는 기본적으로 작동합니다 | Experience Manager 6.5 및 6.5.2 이상 </br> Experience Manager 6.4.4 및 6.4.6 이상 </br> Adobe은 최신 버전을 설치할 것을 권장합니다. [Experience Manager 서비스 팩(SP)](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html) aal을 사용하기 전에. |
| 패키지 설치 후 자산 링크가 작동합니다 | Experience Manager 6.4.0 - 6.4.3의 경우 설치 [adobe-asset-link-support](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/featurepack/adobe-asset-link-support) 패키지. |
| Adobe Stock 통합 | Experience Manager 6.4.2 이상 |
| 시각적 또는 유사성 검색 | Experience Manager 6.5.0 이상 |


## 구성 패키지를 사용하여 Experience Manager 구성 {#configure-using-package}

Adobe은 설치를 권장합니다. [adobe-asset-link-config](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/product/assets/adobe-asset-link-config) 대부분의 구성 작업을 자동화한 다음 몇 가지 수동 작업을 수행하는 구성 패키지 또는 다음을 수행할 수 있습니다. [수동으로 구성](#manual-configuration).

>[!CAUTION]
>
>Experience Manager 인스턴스가 Adobe IMS 계정을 사용하여 사용자 로그인하도록 구성된 경우 구성 패키지를 사용하지 마십시오. 대신, [수동으로 구성](#manual-configuration) Experience Manager 인스턴스.

1. 패키지 관리자를 열려면 Experience Manager 웹 인터페이스에서 **[!UICONTROL 도구]** > **[!UICONTROL 배포]** > **[!UICONTROL 패키지 공유]**. 설치 `adobe-asset-link-config` 패키지.

1. **[!UICONTROL 도구]** > **[!UICONTROL 작업]** > **[!UICONTROL 웹 콘솔]**&#x200B;에 액세스합니다. 찾기 **[!UICONTROL Adobe Granite OAuth IMS 공급자]** 을 누르고 을 눌러 편집합니다.

   다음 속성을 설정하고 변경 사항을 저장합니다.

   * [!UICONTROL 그룹 매핑]: 원하지 않는 경우 비워 둡니다. 자세한 내용은 [그룹 매핑](#group-mapping).
   * [!UICONTROL 조직]: Adobe Admin Console에서 사용 중인 조직 ID를 입력합니다. 조직 ID에 대한 자세한 내용은 [사용자 그룹 만들기](https://helpx.adobe.com/enterprise/using/create-aal-user-group.html).

1. 찾기 **[!UICONTROL Adobe Granite 전달자 인증 핸들러]** 을 누르고 을 눌러 편집합니다.

   추가 **[!UICONTROL InDesignAem2]** 클라이언트 ID에 대한 **[!UICONTROL 허용된 OAuth 클라이언트 ID]** 구성 속성입니다.


## 수동 구성 Experience Manager {#manual-configuration}

구성 패키지를 사용하지 않도록 선택하거나 Experience Manager 배포가 Adobe IMS 계정을 사용한 사용자 로그인을 지원하도록 구성된 경우 Experience Manager을 수동으로 구성합니다.

Experience Manager을 수동으로 구성하려면:

1. 구성 관리자에 액세스하려면 다음을 따르십시오. **[!UICONTROL 도구]** > **[!UICONTROL 작업]** > **[!UICONTROL 웹 콘솔]**. 선택 **[!UICONTROL OSGi]** > **[!UICONTROL 구성]** 을 클릭합니다.

1. 를 찾습니다. **[!UICONTROL Adobe Granite OAuth IMS 공급자]** 구성 을 선택하고 을 클릭하여 편집합니다.

   다음 구성을 설정하고 **[!UICONTROL 저장]**.

   * [!UICONTROL 인증 끝점]: ` https://ims-na1.adobelogin.com/ims/authorize/v1`
   * [!UICONTROL 토큰 끝점]: ` https://ims-na1.adobelogin.com/ims/token/v1`
   * [!UICONTROL 프로필 끝점]: ` https://ims-na1.adobelogin.com/ims/profile/v1`
   * [!UICONTROL 유효성 검사 URL]: ` https://ims-na1.adobelogin.com/ims/validate_token/v1`
   * [!UICONTROL 조직]: 의 조직 ID로 설정합니다. [Adobe Admin Console](https://adminconsole.adobe.com/).
   * [!UICONTROL 그룹 매핑]: 특별한 경우가 아니면 비워 둡니다. 자세한 내용은 [그룹 매핑](#group-mapping).

1. 찾기 **[!UICONTROL Adobe Granite 전달자 인증 핸들러]** 을 누르고 을 눌러 편집합니다.

   다음 클라이언트 ID를 **[!UICONTROL 허용된 OAuth 클라이언트 ID]** 구성 속성: `InDesignAem2, cc-europa-desktop_0_1, cc-europa-desktop_1_0, cc-europa-desktop_2_0, cc-europa-desktop_3_0, cc-europa-desktop_4_0, cc-europa-desktop_5_0, cc-europa-desktop_6_0, cc-europa-desktop_7_0, cc-europa-desktop_8_0, cc-europa-desktop_9_0, and cc-europa-desktop_10_0`.

   각각 추가하려면 `Client ID`, 클릭 `+`. 클릭 **[!UICONTROL 저장]** 모든 ID를 추가한 후에

1. 위치 **[!UICONTROL Adobe Granite OAuth 애플리케이션 및 공급자]** 구성, 기존 항목 검사 **[!UICONTROL Adobe Granite OAuth 인증 핸들러]** 인스턴스. 이 있는 인스턴스를 찾는 경우 `Config ID` 값 `ims`이 절차의 지침에 사용합니다. 그렇지 않으면 `+` 구성 인스턴스를 생성합니다. 다음 속성 값을 설정하고 **[!UICONTROL 저장]**.

   * [!UICONTROL 클라이언트 ID]: 변경하지 마십시오
   * [!UICONTROL 클라이언트 암호]: 변경하지 마십시오
   * [!UICONTROL 구성 ID]: ` ims`
   * [!UICONTROL 범위]: `AdobeID, OpenID, read_organizations` (다른 값도 구성에 있을 수 있음)
   * [!UICONTROL 공급자 ID]: ` ims`
   * [!UICONTROL 사용자 만들기]: ` Checked`
   * [!UICONTROL 사용자 ID 속성]: `Email` 새로 생성된 구성. 그렇지 않으면 변경하지 마십시오.

1. 를 찾습니다. **[!UICONTROL Apache Jackrabbit Oak 기본 동기화 핸들러]** 을 사용한 구성 **[!UICONTROL 동기화 핸들러 이름]** `ims` 을(를) 클릭하고 을(를) 클릭하여 편집합니다.

   다음 구성 속성을 설정하고 **[!UICONTROL 저장]**.

   * [!UICONTROL 사용자 만료 시간 및 사용자 멤버십 만료]: 공백 없이 &#39;m&#39;별로 이어지는 분 단위 시간입니다. 예를 들어, `15m` 15분 동안요 자세한 내용은 [그룹 매핑](#group-mapping).
   * [!UICONTROL 사용자 자동 멤버십]: 변경하지 마십시오
   * [!UICONTROL 사용자 동적 멤버십]: ` Deslect`

1. 를 찾습니다. **[!UICONTROL Adobe Granite OAuth 인증 핸들러]** 구성 을 선택하고 을 클릭하여 편집합니다. 변경하지 않고 을 클릭합니다. **[!UICONTROL 저장]**.

1. CRXDE에서 전달자 인증 처리기의 상대적 우선 순위를 조정하려면 로 이동합니다. `/apps/system/config`. 찾기 `com.adobe.granite.auth.oauth.impl.BearerAuthenticationHandler.config` 구성을 엽니다. 끝에 를 추가합니다. `service.ranking=I"-10"`. 변경 사항을 저장합니다.

   >[!NOTE]
   >
   >전달자 토큰으로 인증된 각 요청은 Adobe IMS에 대한 세 번의 호출, 사용자 동기화 및 Experience Manager에서 로그인 토큰 생성을 초래합니다. 이 오버헤드를 극복하기 위해 Adobe 에셋 링크는 Experience Manager의 응답에서 반환되는 로그인 토큰을 캡처하여 후속 요청과 함께 전송합니다. 이 프로세스가 작동하려면 베어러 인증 핸들러의 상대적 우선순위를 조정해야 합니다.

1. (선택 사항) Experience Manager 사용자의 이메일 ID에 대문자 또는 대소문자가 혼합된 도메인 이름이 있는 경우 다음을 선택합니다. **[!UICONTROL 잠금 사용자를 소문자로 변경]** 위치: **[!UICONTROL Adobe Granite ACP 플랫폼 구성]** Experience Manager 웹 콘솔에서 참조할 수 있습니다.

## 비즈니스 프로필로 마이그레이션 후 추가 구성 {#configure-migration-activity}

Adobe Asset Link 사용자는 기업(CCE) 조직의 기본 Creative Cloud에서 IMS 로그인을 허용하도록 Experience Manager에 연결할 수 있습니다. Experience Manager은 클라이언트 ID를 사용하여 허용된 IMS 조직을 식별합니다. 비즈니스 프로필로 마이그레이션한 후 Bearer Authentication Handler의 Experience Manager에서 IMS 조직의 클라이언트 ID와 비밀 키를 구성해야 합니다. 비즈니스 프로필에 대한 자세한 내용은 [Adobe 프로필 소개](https://helpx.adobe.com/enterprise/kb/introducing-adobe-profiles.html).

엔터프라이즈(CCE)의 Experience Manager 및 Creative Cloud에 대해 서로 다른 Adobe IMS 조직을 사용하고 있고 이러한 두 조직 간에 도메인 트러스트 관계가 설정된 경우에만 추가 구성이 필요합니다.

>[!NOTE]
>
>* 비즈니스 프로필 수정 사항은 Experience Manager 6.5.11.0에 제공됩니다.
>* Experience Manager 및 CCE과 함께 동일한 Adobe IMS 조직을 사용하는 경우 기존 구성이 계속 작동합니다.


**전제 조건**

1. AAL에 대해 Bearer 인증이 구성된 실행 중인 Experience Manager 인스턴스.
1. Experience Manager 6.5 인스턴스에 다음 패키지(서비스 팩 11)를 설치합니다.

   [Experience Manager 6.5.11.0 다운로드](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.11.zip)

1. 연락처 [!UICONTROL 고객 지원] ims 조직의 전달자 인증을 위한 클라이언트 ID 및 비밀 키를 가져옵니다.

비즈니스 프로필로 마이그레이션한 후 필요한 추가 구성은 다음과 같습니다.

1. 위치 **[!UICONTROL Adobe Granite OAuth IMS 구성 공급자]** (`com.adobe.granite.auth.ims.impl.ImsConfigProviderImpl`), 다음을 설정합니다.

   * OAuth 구성 ID (`oauth.configmanager.ims.configid`): `ims` (한 번 확인하면 이미 구성되었을 수 있습니다.)

   * IMS 소유 엔티티(`ims.owningEntity`): IMS 조직 ID

   ![IMS 구성 ID](assets/bearer-authentication1.png)

1. 열기 **[!UICONTROL Bearer 인증 핸들러]** 에서 가져온 클라이언트 ID 구성 및 추가 [!UICONTROL 고객 지원] 다음 목록에 추가 **[!UICONTROL 허용된 OAuth 클라이언트 ID]**.

   ![클라이언트 ID 추가](assets/add-clientid-bearer-auth.png)

1. 열기 **[!UICONTROL Adobe Granite OAuth 애플리케이션 및 공급자]** 구성 및 추가 **[!UICONTROL 클라이언트 ID]** 및 **[!UICONTROL 클라이언트 암호]** (비밀 키) 고객 지원 센터에서 가져왔습니다.

   다음을 확인합니다. **[!UICONTROL 구성 ID]** 필드 (`oauth.config.id`)에 제공된 것과 동일한 값을 포함합니다. **[!UICONTROL OAuth 구성 ID]** 필드 (`oauth.configmanager.ims.configid`)을 참조하십시오.

   ![클라이언트 ID 확인](assets/clientid-secretkey.png)

1. 열기 **[!UICONTROL Adobe Granite IMS 클러스터 교환 토큰 전처리기]** 구성 및 설정 `enable`.

## 사용자 액세스 제어 관리 {#user-access}

이 섹션에서는 사용자와 Experience Manager 저장소에 대한 액세스 권한을 관리하는 방법을 설명합니다.

### 그룹 매핑 {#group-mapping}

그룹 매핑은 Experience Manager의 그룹이 Adobe IMS의 그룹에 대응하는 방식을 결정합니다. Adobe Asset Link 사용자에게 Experience Manager Assets에 액세스할 수 있는 권한이 부여된 방법에서 중요한 역할을 합니다.

Adobe 에셋 링크와 함께 사용할 경우, Experience Manager은 사용자 관리 기능을 Adobe IMS에 위임합니다. Adobe IMS의 사용자 및 그룹에 해당하는 사용자 및 그룹을 자동으로 생성합니다. 또한 Adobe IMS의 사용자, 그룹 및 그룹 멤버십을 일치시키기 위해 Experience Manager의 사용자, 그룹 및 그룹 멤버십을 동기화합니다.

예를 들어 Adobe Asset Link 사용자가 Adobe IMS 그룹 assetlink-users의 멤버인 시나리오를 생각해 보십시오. 이 경우 assetlink-users라는 동기화된 그룹은 해당 Adobe IMS 그룹의 사용자가 처음으로 Adobe 에셋 링크에 연결할 때 Experience Manager에 생성됩니다. Adobe IMS 그룹의 각 새 사용자는 Adobe 에셋 링크를 통해 Experience Manager에 처음 연결할 때 Experience Manager의 해당 그룹에 추가됩니다.

Adobe IMS의 그룹에 해당하고 그룹과 동기화된 Experience Manager의 그룹은 직접 또는 다른 그룹의 구성원으로 설정하여 액세스 권한을 부여받을 수 있습니다. 다음은 권한을 관리하는 방법의 예입니다.

![그룹 예](assets/group-examples.png)

Experience Manager의 그룹 매핑에는 다음 규칙이 적용됩니다.

* 다음을 확인합니다. **[!UICONTROL 그룹 매핑]** 의 속성 **[!UICONTROL Adobe Granite OAuth IMS 공급자]** 구성이 비어 있습니다.
* Adobe Asset Link 사용자 그룹 멤버십은 사용자의 인증 및 다음 기간 동안 평가됩니다. **[!UICONTROL 사용자 만료 시간]** 의 속성 **[!UICONTROL Apache Jackrabbit Oak 기본 동기화 핸들러]** 구성이 경과되었습니다. 현재 Experience Manager의 그룹에 사용자를 추가 및 제거하여 Adobe IMS에 있는 항목과 동기화할 수 있습니다.
* 그룹 이름 충돌을 피하십시오. Adobe IMS에서 사용자를 관리하기 위해 만든 그룹에 사용되는 이름이 모든 Experience Manager 시스템 그룹 이름과 다른지 확인합니다.

  예를 들어 가 과(와) 다른지 확인합니다. `dam-users` 그룹 및 Experience Manager 관리자가 생성한 그룹.

  이름이 Experience Manager 시스템 그룹 또는 수동으로 만든 그룹의 이름과 충돌하는 Adobe IMS 그룹은 사용자 권한을 제어하는 데 사용되지 않습니다.
* Adobe IMS 사용자가 사용자 이름이 이전에 만든 Experience Manager 사용자와 충돌하는 Experience Manager 인스턴스에 연결하는 경우 Adobe IMS 사용자에게는 고유하게 하기 위해 숫자가 추가된 다른 이름이 제공됩니다.

**최초 액세스 제어 설정**

에셋 링크 Adobe을 통해 연결하는 사용자는 필요한 권한이 부여된 후에만 에셋을 보고 상호 작용할 수 있습니다. 다음 [그룹 매핑](#group-mapping) 위의 섹션에서는 Adobe IMS 내에서 조직의 사용자 그룹에 해당하고 동기화되는 사용자 그룹이 Experience Manager에서 어떻게 생성되는지 설명합니다. Experience Manager 관리자는 이러한 그룹을 사용하여 Adobe Asset Link 사용자에 대한 액세스 제어를 관리하는 것이 좋습니다.

Adobe IMS 그룹(사용자 액세스 제어 관리에 사용됨)과 동기화된 각 Experience Manager 그룹에 대해 다음을 수행합니다.

1. Adobe 에셋 링크에서 초기 연결에 사용할 수 있는 멤버가 그룹에 있는지 확인합니다.
1. 해당 사용자를 사용하여 Adobe 에셋 링크에 로그인하고 Experience Manager에 연결합니다. 이 연결은 실패할 것으로 예상됩니다.
1. Experience Manager에서 Adobe IMS의 그룹에 해당하는 그룹을 찾아 원하는 액세스 권한을 부여합니다. 예를 들어 새 그룹은 dam-users 그룹의 구성원이 됩니다.
1. Asset Link Adobe을 닫고 Creative Cloud 응용 프로그램을 다시 시작합니다.
1. 사용자에게 예상 액세스 권한이 있는지 확인하려면 Adobe 에셋 링크를 다시 여십시오.

이러한 단계를 수행하면 동일한 그룹의 다른 사용자가 첫 번째 시도에서 Adobe 에셋 링크가 있는 Experience Manager에 연결할 수 있습니다. 이러한 사용자는 자동으로 그룹의 다른 사용자와 동일한 권한을 갖습니다.

## Adobe 에셋 링크에 대한 Experience Manager 사용자 관리 {#manage-users}

Adobe Asset Link 사용자는 Creative Cloud 애플리케이션에 로그인하면 Experience Manager과 연결할 수 있습니다. 이 인증은 Adobe IMS 기술을 사용하며, 존재하지 않는 경우 Experience Manager에서 사용자 정보를 만듭니다. Experience Manager 기업 고객은 Experience Manager과 통합된 외부 ID 공급자를 통해 사용자를 관리하는 것이 일반적입니다. ID 공급자에는 Adobe IMS와 SAML 및 LDAP 프로토콜을 사용하는 기타 제품이 포함됩니다. 또는 Experience Manager에서 로컬로 사용자를 만들고 관리할 수 있습니다.

다음과 같은 경우 에셋 Adobe에서 Experience Manager에 연결하는 사용자는 이전 직접 로그인의 Experience Manager에 저장된 기존 사용자 정보와 충돌하지 않습니다.

* Experience Manager에 직접 로그인하는 데 사용되는 모든 사용자 이름이 Creative Cloud 로그인에 사용되는 Adobe IMS의 사용자 이름과 다릅니다.
* Adobe IMS는 직접 Experience Manager 로그인을 위한 ID 공급자로 사용됩니다.
* 사용자는 동일한 계정으로 Adobe이 직접 로그인하기 전에 Experience Manager 자산 링크에서 Experience Manager에 연결합니다.


반면, 직접 Experience Manager 로그인의 결과로 생성된 사용자 정보는 다음 시나리오에서 Asset Link Adobe을 사용하도록 업데이트해야 합니다.

* 사용자의 이메일 주소와 같은 동일한 사용자 이름은 Adobe IMS를 사용하는 Creative Cloud의 계정과 Adobe IMS가 아닌 외부 ID 공급자의 계정 모두에 사용됩니다.
* Creative Cloud 계정 및 로컬 Experience Manager 계정 둘 다에 동일한 사용자 이름이 사용됩니다.
* Adobe IMS의 Creative Cloud 계정은 Federated ID이며, 직접 로그인을 위해 Experience Manager과 통합된 동일한 외부 ID 공급자에서 제공됩니다.

이러한 시나리오를 통해 만든 사용자에게는 Adobe IMS와 동기화된 사용자에게 필요한 속성이 없습니다.

Asset Link를 사용하여 작업하도록 Experience Manager에서 이러한 Adobe을 업데이트하려면 다음을 수행하십시오.

1. Experience Manager 웹 콘솔에서 을 찾습니다 **[!UICONTROL Apache Jackrabbit Oak 외부 보안 주체 구성]** 구성 을 선택하고 을 클릭하여 편집합니다. 선택 취소 **[!UICONTROL 외부 ID 보호]** 확인란을 선택하고 **[!UICONTROL 저장]**.
1. Experience Manager의 사용자 관리 인터페이스에 액세스하려면 다음으로 이동합니다. **[!UICONTROL 도구]** > **[!UICONTROL 보안]** > **[!UICONTROL 사용자]**. 업데이트하려는 사용자를 선택한 다음 해당 사용자에 대한 브라우저의 URL 경로 끝을 기록합니다(시작: `/home/users`. 또는 CRXDE에서 사용자 이름을 검색할 수 있습니다. 샘플 사용자 경로: `/home/users/x/xTac082TDh-guJzzG7WM`.
1. CRXDE에서 사용자 경로로 이동하고 사용자 노드를 선택한 다음 를 선택하여 노드의 속성을 확인합니다. **[!UICONTROL 속성]** 가운데 아래 영역에 있는 탭입니다. 이 노드에는 `jcr:primaryType` 속성 값: `rep:User`.
1. 의 맨 아래에서 **[!UICONTROL 속성]** 탭 영역에서 `Name` 값 `rep:externalId`, `Type` 값 `String`, 및 `Value` 값 `rep:authorizableId`;`ims`, 여기서 `rep:authorizableId` 은(는) 의 값입니다 `rep:authorizableId` 노드의 속성입니다. (세미콜론은 공백 없이 사용하여 `rep:authorizableId` 값: 부터 `ims`.)
1. 다음을 클릭합니다. **[!UICONTROL 추가]** 새 항목 오른쪽에 있는 단추를 클릭한 다음 **[!UICONTROL 모두 저장]**.
1. Asset Link Adobe을 사용하도록 업그레이드하려는 다른 사용자에 대해 2~5단계를 반복합니다.
1. Experience Manager 웹 콘솔에서 을 찾습니다 **[!UICONTROL Apache Jackrabbit Oak 외부 보안 주체 구성]** 구성 을 선택하고 을 클릭하여 편집합니다. 선택 취소 **[!UICONTROL 외부 ID 보호]** 확인란을 선택하고 **[!UICONTROL 저장]**.

>[!NOTE]
>
>몇 분 안에 서비스가 복원되지 않으면 Experience Manager을 다시 시작하여 성공적인 인증을 허용하십시오.

이 변경 후 업데이트된 Experience Manager 사용자는 Asset Link Adobe에 연결하고 업데이트 전에 사용되었던 Experience Manager에 직접 로그인하는 방법을 계속 사용할 수 있습니다. Adobe IMS를 사용하여 성공적으로 인증하면 Experience Manager 사용자 프로필 정보가 Adobe IMS의 사용자 프로필과 동기화됩니다.

여러 Experience Manager 사용자의 일괄 마이그레이션을 수행하여 Adobe Asset Link에서 작업할 수 있는 방법이 있습니다. 이 옵션을 활성화하는 방법에 대한 자세한 내용과 지원은 Adobe 지원 센터에 문의하십시오.

단계에 대한 대안으로서, 특정 상황에서 Adobe Asset Link 사용자에게 Experience Manager에 대한 빠른 액세스가 제공될 수 있습니다. 이러한 경우 Asset Link에 연결하기 전에 Experience Manager 사용자 관리 또는 Experience Manager CRXDE를 사용하여 기존 Adobe 정보를 찾아서 삭제합니다. 연결 후 Experience Manager에 새 사용자 정보가 만들어집니다. 사용자 노드의 하위 항목으로 추가되는 중요한 데이터가 없는 경우에만 이 접근 방식을 사용합니다. 이러한 추가 데이터는 사용자 노드의 하위 노드가 아닌 다른 노드입니다. `tokens`, `preferences`, `profile`, `profiles`, `profiles/public`, 및 `rep:policy/*` 노드.

## 자산을 조건부로 처리하는 워크플로우 자동 시작 {#auto-start-workflow}

Experience Manager 6.4 및 Experience Manager 6.5에서 관리자는 사전 정의된 조건에 따라 에셋을 자동으로 실행하고 처리하도록 워크플로우를 구성할 수 있습니다.

이 구성은 비즈니스 계열 사용자와 마케터가 몇 개의 특정 폴더에 사용자 지정 워크플로우를 만드는 등의 경우에 유용합니다. 기획사 사진 촬영의 모든 에셋은 워터마크가 될 수도 있고 프리랜서가 업로드한 모든 에셋을 가공하여 특정 렌디션을 만들 수도 있다고 가정해 보겠습니다.

자세한 내용 및 Experience Manager 구성은 다음을 참조하십시오. [에셋에서 워크플로우 자동 실행](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/assets-workflow.html#auto-execute-workflow-on-some-assets).


## Experience Manager 6.4.x 버전에서 사용자 지정 인덱스 만들기 {#create-custom-index}

Experience Manager에 쿼리에 사용되는 인덱스가 포함되어 있습니다. 지정된 버전에 대해 다음 사용자 지정 인덱스를 만듭니다. Experience Manager 6.5.0에는 기본적으로 이 인덱스가 포함되어 있습니다. Asset Link Adobe을 사용하려면 이 색인이 있어야 사용자가 체크 아웃한 에셋을 확인할 수 있습니다.

1. CRXDE에서 `/oak:index` 노드. 다음 이름의 노드 만들기 `cqDrivelock` 및 설정 `Type` 끝 `oak:QueryIndexDefinition`.

1. 새 노드에 다음 속성을 추가하고 변경 사항을 저장합니다.

   * `Name: type; Type: string; Value: property`

   * `Name: propertyNames; Type: Name[] (click the "Multi" button); Value: cq:drivelock`


## 시각적 또는 유사성 검색 구성 {#configure-visual-similarity-search}

시각적 검색 기능을 사용하면 [에셋 링크 Adobe] 패널을 사용하여 AEM Assets 저장소에서 시각적으로 유사한 에셋을 검색할 수 있습니다. 이 기능은 6.5.0 이상 버전에서 사용할 수 있으며 인덱싱된 에셋만 검색됩니다. 자세한 내용은 [시각적 검색 구성 방법](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/search-assets.html#configvisualsearch).

## Adobe InDesign에 대한 배치 전용 렌디션 생성 {#fpo-renditions}

Experience Manager은 배치에만 사용되는 렌디션(FPO)을 제공합니다. 이러한 FPO 렌디션은 파일 크기는 작지만 종횡비가 동일합니다. 에셋에 FPO 렌디션을 사용할 수 없는 경우 Adobe InDesign은 원본 에셋을 대신 사용합니다. 이 대체 메커니즘을 사용하면 크리에이티브 워크플로우가 중단 없이 진행될 수 있습니다. 자세한 내용은 [FPO 표현물 생성](/help/assets/configure-fpo-renditions.md).


## Adobe Stock과 통합 {#adobe-stock-integration}

조직은 Adobe Stock 계정을 Experience Manager Assets과 통합합니다. 이 기능은 마케터가 라이선스가 있는 고품질의 로열티가 없는 사진, 벡터, 일러스트레이션, 비디오, 템플릿 및 3D 자산을 광고 및 마케팅 프로젝트에 사용할 수 있도록 도와줍니다. 크리에이티브 전문가는 Asset Link 패널을 사용하여 이러한 에셋을 사용할 수 있습니다.

Adobe Stock과 통합하려면 다음을 참조하십시오. [Experience Manager Assets의 Adobe Stock 에셋](/help/assets/aem-assets-adobe-stock.md). Adobe Stock과의 통합을 위해 Experience Manager 6.4.2 이상이 필요합니다.


## Experience Manager 관련 문제 해결 {#troubleshoot}


자산 링크 Adobe을 구성하거나 사용할 때 문제가 발생하는 경우 다음을 시도해 보십시오.

* 배포가 사전 요구 사항을 충족하는지 확인합니다. 특히 적절한 기능 팩이나 패키지가 설치되어 있는지 확인하십시오.
* 조직의 파트너 또는 시스템 통합자에게 문의하십시오.
* Creative Cloud 사용자가 체크아웃된 에셋에서 을 확인할 수 없는 경우 이메일 ID에서 도메인 이름의 대/소문자를 확인합니다. 수정하려면 다음을 참조하십시오 [수동 구성](#manual-configuration).
* 자세한 내용은 [asset Link 문제 해결](https://helpx.adobe.com/enterprise/kb/asset-link-troubleshooting.html).


>[!MORELIKETHIS]
>
>* [Adobe Asset Link에 대하여](https://helpx.adobe.com/kr/enterprise/using/adobe-asset-link.html)
>* [Creative Cloud 데스크탑 앱에서 Asset Link 사용 및 자산 관리](https://helpx.adobe.com/kr/enterprise/using/manage-assets-using-adobe-asset-link.html)
>* [Adobe Experience Manager Assets as a Cloud Service 구성](https://helpx.adobe.com/kr/enterprise/using/configure-aem-assets-for-asset-link.html).
