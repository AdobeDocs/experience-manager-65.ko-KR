---
title: HSM 자격 증명 관리
description: HSM 자격 증명을 관리하는 방법을 알아봅니다. Trust Store 관리 페이지에서 HSM을 관리할 수 있습니다. HSM 구성 요소를 보고, 확인하고, 업데이트하고, 재설정하고, 삭제할 수 있습니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: facbeab2-de95-4778-894c-faa771d3391e
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Security
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '1334'
ht-degree: 100%

---

# HSM 자격 증명 관리 {#managing-hsm-credentials}

Trust Store 관리 페이지에서 HSM(하드웨어 보안 모듈) 자격 증명을 관리할 수 있습니다. HSM은 개인 키를 안전하게 생성하고 저장하는 데 사용할 수 있는 서드파티 PKCS#11 장치입니다. HSM은 개인 키에 대한 액세스와 개인 키 사용을 물리적으로 보호합니다.

HSM과 통신하려면 클라이언트 소프트웨어가 필요합니다. HSM 클라이언트 소프트웨어는 AEM Forms와 동일한 컴퓨터에 설치하고 구성해야 합니다.

AEM Forms 디지털 서명은 HSM에 저장된 자격 증명을 사용하여 서버측 디지털 서명을 적용할 수 있습니다. 이 섹션의 지침을 따라 디지털 서명에서 사용할 각 HSM 자격 증명에 대한 별칭을 만듭니다. 별칭에는 HSM에 필요한 모든 매개변수가 포함됩니다.

>[!NOTE]
>
>HSM 구성을 변경한 후 AEM Forms 서버를 다시 시작하십시오.

## HSM 장치가 온라인 상태일 때 HSM 자격 증명에 대한 별칭 만들기 {#create-an-alias-for-an-hsm-credential-when-the-hsm-device-is-online}

>[!NOTE]
> 
> 사용자에게 관리자 콘솔에 액세스할 수 있는 관리자 권한이 있는지 확인하십시오.

1. 관리 콘솔에서 설정 > Trust Store 관리 > HSM 자격 증명을 클릭한 후 추가를 클릭합니다.
1. 프로필 이름 상자에 별칭을 식별하는 데 사용되는 문자열을 입력합니다. 이 값은 서명 필드 작업과 같은 일부 디지털 서명 작업의 속성으로 사용됩니다.
1. PKCS11 라이브러리 상자에 서버에 있는 HSM 클라이언트 라이브러리의 정규화된 경로를 입력합니다. 예를 들어, `c:\Program Files\LunaSA\cryptoki.dll`과 같이 입력합니다. 클러스터링된 환경에서 해당 경로는 클러스터의 모든 서버에서 동일해야 합니다.
1. HSM 연결 테스트를 클릭합니다. AEM Forms가 HSM 장치에 연결할 수 있는 경우 HSM을 사용할 수 있다는 메시지가 표시됩니다. 다음을 클릭합니다.
1. 토큰 이름, 슬롯 ID 또는 슬롯 목록 색인을 사용하여 자격 증명이 HSM에 저장되는 위치를 식별합니다.

   * **토큰 이름:** 사용할 HSM 파티션의 이름에 해당합니다(예: HSMPART1).
   * **슬롯 ID:** 슬롯 ID는 long 데이터 유형의 슬롯 식별자입니다.
   * **슬롯 목록 색인:** 슬롯 목록 색인을 선택하는 경우 슬롯 정보를 슬롯에 해당하는 정수로 설정합니다. 이 값은 0부터 시작하는 색인입니다. 즉, 클라이언트가 먼저 HSMPART1 파티션에 등록된 경우 HSMPART1은 SlotListIndex 값 0을 사용하여 참조됩니다.

1. 토큰 PIN 상자에 HSM 키에 액세스하는 데 필요한 암호를 입력하고 다음을 클릭합니다.
1. 자격 증명 상자에서 자격 증명을 선택합니다. 저장을 클릭합니다.

## HSM 장치가 오프라인 상태일 때 HSM 자격 증명에 대한 별칭 만들기 {#create-an-alias-for-an-hsm-credential-when-the-hsm-device-is-offline}

1. 관리 콘솔에서 설정 > Trust Store 관리 > HSM 자격 증명을 클릭한 후 추가를 클릭합니다.
1. 프로필 이름 상자에 별칭을 식별하는 데 사용되는 문자열을 입력합니다. 이 값은 서명 필드 작업과 같은 일부 디지털 서명 작업의 속성으로 사용됩니다.
1. PKCS11 라이브러리 상자에 서버에 있는 HSM 클라이언트 라이브러리의 정규화된 경로를 입력합니다. 예, `c:\Program Files\LunaSA\cryptoki.dll`. 클러스터링된 환경에서 해당 경로는 클러스터의 모든 서버에서 동일해야 합니다.
1. 오프라인 프로필 만들기 확인란을 선택합니다. 다음을 클릭합니다.
1. HSM 장치 목록에서 자격 증명이 저장된 HSM 장치의 제조업체를 선택합니다.
1. 슬롯 유형 목록에서 슬롯 ID, 슬롯 색인 또는 토큰 이름을 선택하고 슬롯 정보 상자에 값을 지정합니다. AEM Forms에서 해당 설정을 사용하여 자격 증명이 HSM에 저장되는 위치를 결정합니다.

   * **토큰 이름:** 파티션 이름에 해당합니다(예: HSMPART1).
   * **슬롯 ID:** 슬롯 ID는 슬롯에 해당하는 정수이며, 이 슬롯은 파티션에 해당합니다. 예를 들어 클라이언트(Forms 서버)가 먼저 HSMPART1 파티션에 등록되었습니다. 이 클라이언트의 슬롯 1이 HSMPART 파티션에 매핑됩니다. HSMPART1이 등록된 첫 번째 파티션이므로 슬롯 ID는 1이고 슬롯 정보를 1로 설정합니다.

     슬롯 ID는 클라이언트별로 설정됩니다. 두 번째 컴퓨터를 다른 파티션(예: 동일한 HSM 장치의 HSMPART2)에 등록한 경우 슬롯 1은 해당 클라이언트의 HSMPART2 파티션과 연결됩니다.

   * **슬롯 색인:** 슬롯 색인을 선택하는 경우 슬롯 정보를 슬롯에 해당하는 정수로 설정합니다. 이 값은 0부터 시작하는 색인입니다. 즉, 클라이언트가 먼저 HSMPART1 파티션에 등록된 경우 슬롯 1이 해당 클라이언트의 HSMPART1에 매핑됩니다. HSMPART1이 등록된 첫 번째 파티션이므로 슬롯 색인은 0입니다.

1. 다음 옵션 중 하나를 선택하고 경로를 제공합니다.

   * **인증서**: (SHA1을 사용하는 경우 필요하지 않음) 찾아보기를 클릭하고 사용 중인 자격 증명에 대한 공개 키 경로를 찾습니다.
   * **인증서 SHA1:** (물리적 인증서를 사용하는 경우 필요하지 않음) 사용 중인 자격 증명에 대한 공개 키(. cer) 파일의 SHA1 값(지문)을 입력합니다. SHA1 값에 공백이 포함되지 않았는지 확인하십시오.

1. 암호 상자에 지정된 슬롯 정보에 대한 HSM 키에 액세스하는 데 필요한 암호를 입력한 후 저장을 클릭합니다.

## HSM 자격 증명 별칭 속성 보기 {#view-hsm-credential-alias-properties}

1. 관리 콘솔에서 설정 > Trust Store 관리 > HSM 자격 증명을 클릭합니다.
1. 자격 증명 별칭의 별칭 이름을 클릭하여 속성을 보고 확인을 클릭합니다.

## HSM 자격 증명 상태 확인 {#check-the-status-of-an-hsm-credential}

1. 관리 콘솔에서 설정 > Trust Store 관리 > HSM 자격 증명을 클릭합니다.
1. 확인할 자격 증명 옆에 있는 확인란을 클릭하고 상태 확인을 클릭합니다.

상태 열은 자격 증명의 현재 상태를 반영합니다. 실패가 발생하면 상태 열에 빨간색 X가 표시됩니다. 마우스로 X 위를 가리키면 실패 이유가 포함된 도구 팁이 표시됩니다.

## HSM 자격 증명 별칭 속성 업데이트 {#update-hsm-credential-alias-properties}

1. 관리 콘솔에서 설정 > Trust Store 관리 > HSM 자격 증명을 클릭합니다.
1. 자격 증명 별칭의 별칭 이름을 클릭합니다.
1. 자격 증명 업데이트를 클릭하고 필요에 따라 설정을 업데이트합니다.

## 모든 HSM 연결 재설정 {#reset-all-hsm-connections}

Forms 서버와 HSM 장치 간 네트워크 세션이 중단된 후 HSM 장치에 대한 열린 연결을 재설정합니다. 예를 들어 네트워크가 중단되거나 소프트웨어 업데이트를 위해 HSM 장치가 오프라인으로 전환되는 경우 중단이 발생할 수 있습니다. 중단이 발생하면 기존 연결은 더 이상 유효하지 않고 해당 연결에 대한 서명 요청은 모두 실패합니다. 모든 HSM 연결 재설정 옵션을 사용하면 기존 연결이 지워집니다.

1. 관리 콘솔에서 설정 > Trust Store 관리 > HSM 자격 증명을 클릭합니다.
1. 모든 HSM 연결 재설정을 클릭합니다.

## HSM 자격 증명 별칭 삭제 {#delete-an-hsm-credential-alias}

1. 관리 콘솔에서 설정 > Trust Store 관리 > HSM 자격 증명을 클릭합니다.
1. 삭제할 HSM 자격 증명의 확인란을 선택하고 삭제를 클릭한 후 확인을 클릭합니다.

## 원격 HSM 지원 구성 {#configure-remote-hsm-support}

AEM Forms는 웹 서비스 기반 IPC/RPC 메커니즘을 사용합니다. 이 메커니즘을 통해 AEM Forms는 원격 컴퓨터에 설치된 HSM을 사용할 수 있습니다. 이 기능을 사용하려면 HSM이 설치된 원격 컴퓨터에 웹 서비스를 설치합니다. 자세한 내용은 [Sun JDK를 사용하여 Windows 64비트 플랫폼에서 AEM Forms ES에 대한 HSM 지원 구성](https://kb2.adobe.com/cps/808/cpsid_80835.html)을 참조하십시오.

이 메커니즘은 HSM 프로필의 온라인 생성이나 상태 확인을 지원하지 않습니다. 하지만 HSM 프로필을 만들고 상태 확인을 수행하는 두 가지 방법이 있습니다.

* 서명자 인증서를 전달하여 AEM Forms 클라이언트 자격 증명을 만듭니다. [Sun JDK를 사용하여 Windows 64비트 플랫폼에서 AEM Forms ES에 대한 HSM 지원 구성](https://kb2.adobe.com/cps/808/cpsid_80835.html)에 나와 있는 단계를 따릅니다. 웹 서비스 위치가 자격 증명 속성으로 전달됩니다. 인증서 DER 또는 인증서 SHA-1 16진수를 사용하여 생성된 오프라인 HSM 프로필도 지원됩니다. 하지만 이전 버전의 AEM Forms에서 AEM Forms로 업그레이드한 경우 자격 증명에 인증서와 웹 서비스 정보가 포함되어 있으므로 클라이언트를 변경해야 합니다.
* 웹 서비스 위치는 서명 서비스의 관리 콘솔에서 지정됩니다. ([서명 서비스 설정](/help/forms/using/admin-help/configure-service-settings.md#signature-service-settings)을 참조하십시오.) 여기에서 클라이언트는 Trust Store에 HSM 프로필의 별칭만을 포함하고 있습니다. 이전 버전의 AEM Forms에서 AEM Forms로 업그레이드한 경우에도 클라이언트를 변경하지 않고 이 옵션을 원활하게 사용할 수 있습니다. 이 옵션은 인증서 SHA-1을 사용하는 HSM 프로필을 지원하지 않습니다.
