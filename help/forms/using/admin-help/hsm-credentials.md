---
title: HSM 자격 증명 관리
seo-title: Managing HSM credentials
description: HSM 자격 증명을 관리하는 방법을 알아봅니다.
seo-description: Learn how to manage HSM credentials.
uuid: 30ddcd4a-f771-44d5-bdef-4826adcd0c44
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e5f17ba8-8aab-4449-811a-20ad33de1c6f
exl-id: facbeab2-de95-4778-894c-faa771d3391e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1304'
ht-degree: 0%

---

# HSM 자격 증명 관리 {#managing-hsm-credentials}

[Trust Store 관리] 페이지에서 HSM(Hardware Security Module) 자격 증명을 관리할 수 있습니다. HSM은 개인 키를 안전하게 생성하고 저장하는 데 사용할 수 있는 타사 PKCS#11 디바이스입니다. HSM은 개인 키에 대한 액세스와 사용을 물리적으로 보호합니다.

클라이언트 소프트웨어는 HSM과 통신하는 데 필요합니다. HSM 클라이언트 소프트웨어는 AEM Forms와 동일한 컴퓨터에 설치 및 구성되어야 합니다.

AEM Forms 디지털 서명은 HSM에 저장된 자격 증명을 사용하여 서버측 디지털 서명을 적용할 수 있습니다. 이 섹션의 지침에 따라 디지털 서명에서 사용할 각 HSM 자격 증명에 대한 별칭을 만듭니다. 별칭에는 HSM에 필요한 모든 매개 변수가 포함되어 있습니다.

>[!NOTE]
>
>HSM 구성을 변경한 후 AEM Forms 서버를 다시 시작합니다.

## HSM 장치가 온라인 상태일 때 HSM 자격 증명에 대한 별칭 생성 {#create-an-alias-for-an-hsm-credential-when-the-hsm-device-is-online}

1. 관리 콘솔에서 설정 > Trust Store Management > HSM 자격 증명 을 클릭한 다음 추가 를 클릭합니다.
1. 프로파일 이름 상자에 별칭을 식별하는 데 사용되는 문자열을 입력합니다. 이 값은 서명 필드 작업과 같은 일부 디지털 서명 작업에 속성으로 사용됩니다.
1. PKCS11 Library 상자에 서버에 있는 HSM 클라이언트 라이브러리의 정규화된 경로를 입력합니다. 예, `c:\Program Files\LunaSA\cryptoki.dll`. 클러스터된 환경에서 이 경로는 클러스터의 모든 서버에 대해 동일해야 합니다.
1. HSM 연결 테스트 를 클릭합니다. AEM Forms에서 HSM 장치에 연결할 수 있는 경우 HSM을 사용할 수 있다는 메시지가 표시됩니다. 다음을 클릭합니다.
1. 토큰 이름, 슬롯 ID 또는 슬롯 목록 인덱스를 사용하여 HSM에서 자격 증명이 저장되는 위치를 식별합니다.

   * **토큰 이름:** 사용할 HSM 파티션 이름(예: HSMPART1)에 해당합니다.
   * **슬롯 ID:** 슬롯 ID는 long 데이터 유형의 슬롯 식별자입니다.
   * **슬롯 목록 인덱스:** 슬롯 목록 인덱스(Slot List Index)를 선택하는 경우 슬롯 정보(Slot Info)를 슬롯에 해당하는 정수로 설정합니다. 이는 0 기반 인덱스입니다. 즉, 클라이언트가 HSMPART1 파티션에 먼저 등록되면 SlotListIndex 값 0을 사용하여 HSMPART1이 참조됩니다.

1. 토큰 고정 상자에 HSM 키에 액세스하는 데 필요한 암호를 입력하고 다음 을 클릭합니다.
1. 자격 증명 상자에서 자격 증명을 선택합니다. 저장을 클릭합니다.

## HSM 장치가 오프라인일 때 HSM 자격 증명에 대한 별칭 생성 {#create-an-alias-for-an-hsm-credential-when-the-hsm-device-is-offline}

1. 관리 콘솔에서 설정 > Trust Store Management > HSM 자격 증명 을 클릭한 다음 추가 를 클릭합니다.
1. 프로파일 이름 상자에 별칭을 식별하는 데 사용되는 문자열을 입력합니다. 이 값은 서명 필드 작업과 같은 일부 디지털 서명 작업에 속성으로 사용됩니다.
1. PKCS11 Library 상자에 서버에 있는 HSM 클라이언트 라이브러리의 정규화된 경로를 입력합니다. 예, `c:\Program Files\LunaSA\cryptoki.dll`. 클러스터된 환경에서 이 경로는 클러스터의 모든 서버에 대해 동일해야 합니다.
1. 오프라인 프로필 만들기 확인란을 선택합니다. 다음을 클릭합니다.
1. HSM 장치 목록에서 자격 증명이 저장된 HSM 장치의 제조업체를 선택합니다.
1. Slot Type 목록에서 Slot Id, Slot Index 또는 Token Name 을 선택하고 Slot Info 상자에 값을 지정합니다. AEM forms는 이러한 설정을 사용하여 HSM에서 자격 증명이 저장되는 위치를 결정합니다.

   * **토큰 이름:** 파티션 이름(예: HSMPART1)에 해당합니다.
   * **슬롯 ID:** 슬롯 ID는 슬롯에 해당하는 정수로 파티션에 해당합니다. 예를 들어 클라이언트(forms 서버)가 HSMPART1 파티션에 먼저 등록되어 있습니다. 이 클라이언트의 경우 슬롯 1을 HSMPART1 파티션에 매핑합니다. HSMPART1은 등록된 첫 번째 파티션이므로 슬롯 ID는 1이고 Slot Info를 1로 설정합니다.

      슬롯 ID는 클라이언트별로 설정됩니다. 두 번째 시스템을 다른 파티션(예: 동일한 HSM 장치의 HSMPART2)에 등록한 경우 슬롯 1은 해당 클라이언트에 대한 HSMPART2 파티션과 연결됩니다.

   * **슬롯 색인:** 슬롯 인덱스 를 선택하는 경우 슬롯 정보 를 슬롯에 해당하는 정수로 설정합니다. 이는 0부터 시작하는 인덱스입니다. 즉, 클라이언트가 HSMPART1 파티션에 먼저 등록되면 슬롯 1이 이 클라이언트의 HSMPART1에 매핑됩니다. HSMPART1은 등록된 첫 번째 파티션이므로 슬롯 인덱스는 0입니다.

1. 다음 옵션 중 하나를 선택하고 경로를 제공합니다.

   * **인증서**: (SHA1을 사용하는 경우에는 필요하지 않음) 찾아보기를 클릭하고 사용 중인 자격 증명의 공개 키 경로를 찾습니다.
   * **인증서 SHA1:** (실제 인증서를 사용하는 경우에는 필요하지 않습니다.) 사용 중인 자격 증명에 대한 공개 키(.cer) 파일의 SHA1 값(지문)을 입력합니다. SHA1 값에 사용된 공백이 없는지 확인합니다.

1. 암호 상자에 지정된 슬롯 정보에 대한 HSM 키를 액세스하는 데 필요한 암호를 입력한 다음 저장 을 클릭합니다.

## HSM 자격 증명 별칭 속성 보기 {#view-hsm-credential-alias-properties}

1. 관리 콘솔에서 설정 > 보안 저장소 관리 > HSM 자격 증명 을 클릭합니다.
1. 자격 증명 별칭의 별칭 이름을 클릭하여 속성을 확인한 다음 확인을 클릭합니다.

## HSM 자격 증명의 상태 확인 {#check-the-status-of-an-hsm-credential}

1. 관리 콘솔에서 설정 > 보안 저장소 관리 > HSM 자격 증명 을 클릭합니다.
1. 확인할 자격 증명 옆의 확인란을 클릭하고 상태 확인 을 클릭합니다.

상태 열에는 자격 증명의 현재 상태가 반영됩니다. 장애가 발생하면 상태 열에 빨간색 X 가 표시됩니다. 마우스를 X 위에 놓아 실패 이유가 포함된 도구 설명을 표시합니다.

## HSM 자격 증명 별칭 속성 업데이트 {#update-hsm-credential-alias-properties}

1. 관리 콘솔에서 설정 > 보안 저장소 관리 > HSM 자격 증명 을 클릭합니다.
1. 자격 증명 별칭의 별칭 이름을 클릭합니다.
1. 자격 증명 업데이트 를 클릭하고 필요에 따라 설정을 업데이트합니다.

## 모든 HSM 연결 재설정 {#reset-all-hsm-connections}

Forms 서버와 HSM 장치 간의 네트워크 세션이 중단되면 HSM 장치에 대한 열린 연결을 재설정합니다. 예를 들어, 소프트웨어 업데이트를 위해 HSM 디바이스를 오프라인 상태로 전환하거나 네트워크 중지로 인해 장애가 발생할 수 있습니다. 중단 후 기존 연결이 부실해지고 해당 연결에 대한 모든 서명 요청이 실패합니다. 모든 HSM 연결 재설정 옵션을 사용하면 이전 연결이 지워집니다.

1. 관리 콘솔에서 설정 > 보안 저장소 관리 > HSM 자격 증명 을 클릭합니다.
1. 모든 HSM 연결 재설정 을 클릭합니다.

## HSM 자격 증명 별칭 삭제 {#delete-an-hsm-credential-alias}

1. 관리 콘솔에서 설정 > 보안 저장소 관리 > HSM 자격 증명 을 클릭합니다.
1. 삭제할 HSM 자격 증명의 확인란을 선택하고 삭제 를 클릭한 다음 확인 을 클릭합니다.

## 원격 HSM 지원 구성 {#configure-remote-hsm-support}

AEM forms는 웹 서비스 기반 IPC/RPC 메커니즘을 사용합니다. 이 메커니즘을 통해 AEM Forms는 원격 컴퓨터에 설치된 HSM을 사용할 수 있습니다. 이 기능을 사용하려면 HSM이 설치된 원격 컴퓨터에 웹 서비스를 설치하십시오. 다음을 참조하십시오 [Windows 64비트 플랫폼에서 Sun JDK를 사용하여 AEM Forms ES에 대한 HSM 지원 구성](https://kb2.adobe.com/cps/808/cpsid_80835.html)추가 정보.

이 메커니즘은 HSM 프로필의 온라인 생성 또는 상태 검사를 지원하지 않습니다. 그러나 HSM 프로필을 만들고 상태 검사를 수행하는 방법에는 두 가지가 있습니다.

* 서명자의 인증서를 전달하여 AEM Forms 클라이언트 자격 증명을 만듭니다. 의 단계를 따릅니다. [Windows 64비트 플랫폼에서 Sun JDK를 사용하여 AEM Forms ES에 대한 HSM 지원 구성](https://kb2.adobe.com/cps/808/cpsid_80835.html). 웹 서비스 위치가 자격 증명 속성으로 전달됩니다. 인증서 der 또는 인증서 SHA-1 hex를 사용하여 만드는 오프라인 HSM 프로필도 지원됩니다. 그러나 이전 버전의 AEM forms에서 AEM forms로 업그레이드한 경우 자격 증명에 인증서 및 웹 서비스 정보가 포함되었으므로 클라이언트가 변경됩니다.
* 웹 서비스 위치는 서명 서비스의 관리 콘솔에 지정됩니다. (참조: [서명 서비스 설정](/help/forms/using/admin-help/configure-service-settings.md#signature-service-settings).) 여기서 클라이언트는 트러스트 스토어에서 HSM 프로필의 별칭만 전달했습니다. 이전 버전의 AEM Forms에서 AEM Forms로 업그레이드한 경우에도 클라이언트를 변경하지 않고 이 옵션을 원활하게 사용할 수 있습니다. 이 옵션은 인증서 SHA-1을 사용하는 HSM 프로필을 지원하지 않습니다.
