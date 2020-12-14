---
title: AEM Mobile - GDPR 준비
seo-title: AEM Mobile - GDPR 준비
description: 'null'
seo-description: 'null'
uuid: 817c434f-4b78-40f7-99d6-6efafdedb77e
contentOwner: trushton
discoiquuid: 9399dd3d-a485-4f53-a6f2-7b190da4235b
translation-type: tm+mt
source-git-commit: 85a3dac5db940b81da9e74902a6aa475ec8f1780
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 5%

---


# AEM Mobile - GDPR 준비 {#aem-mobile-gdpr-readiness}

>[!IMPORTANT]
>
>아래 섹션에서는 GDPR이 예로 사용되지만, 포함된 세부 사항은 GDPR, CCPA 등 모든 데이터 보호 및 개인 정보 보호 규정에 적용됩니다.

## AEM Mobile GDPR 지원 {#aem-mobile-gdpr-support}

AEM Mobile은 고객의 GDPR 준수 의무를 지원할 준비가 되었습니다. AEM Mobile에는 개인 데이터가 저장되지 않습니다. 프로비저닝된 경우 Adobe ID을 사용하여 Adobe Experience Mobile에 로그인할 수 있습니다.

[https://aemmobile.adobe.com/signin/index.html](https://aemmobile.adobe.com/signin/index.html)

## Adobe Digital Publishing Suite {#adobe-digital-publishing-suite}

Adobe의 디지털 출판 제품(AEM Mobile 이전)은 Adobe의 GDPR 준비 정책을 지원합니다. [https://www.adobe.com/privacy/general-data-protection-regulation.html](https://www.adobe.com/privacy/general-data-protection-regulation.html)을(를) 참조하십시오. 다음은 Adobe을 사용하여 GDPR 요청을 시작하는 방법을 비롯하여 Digital Publishing Suite 제품에서 GDPR 관련 기능에 대한 지원에 대한 세부 정보를 제공합니다.

이전 Digital Publishing Suite 제품과 AEM Mobile을 혼동하지 않도록 하려면 다음 링크를 통해 Digital Publishing Suite 제품에 로그인하십시오.

[https://digitalpublishing.acrobat.com/welcome.html](https://digitalpublishing.acrobat.com/welcome.html)

### GDPR 요청 시작 {#initiating-a-gdpr-request}

Digital Publishing Suite에 대한 GDPR 요청을 시작하려면 Adobe 고객 지원 센터에 문의하십시오.

고객 데이터를 찾으려면 다음 ID가 필요합니다. 받은 하위 집합은 이 사용자에게 적용되지 않은 다른 ID를 의미합니다.

필수:

* 고객의 계약 ID:*dpsc-contractId*

다음 중 최소 1개를 제공합니다.

* 최종 사용자의 고객이 제공한 OAuth ID(고객의 직접 권한 부여 시스템에 사용된 ID):*dpsc-directEntitlementId*
* Windows 앱 사용자의 경우 최종 사용자의 App Store ID:*dpsc-windowsAppStoreId*
* 최종 사용자가 DPS 앱과 상호 작용하는 데 사용한 이메일 주소:*이메일*

### FAQ(FAQ) {#frequently-asked-questions-faq}

**DELETE 요청을 시작할 때 Adobe에서 내 App Store 구매를 삭제하시겠습니까?**

Adobe은 앱스토어 구매(구독 등)에 대한 정보를 삭제합니다. 그러나 앱 스토어에서는 여전히 구매 내역을 기록하고 있습니다. 앱(최종 사용자)이 App Store에 로그인되어 있는 경우 해당 영수증은 다시 주워 Adobe으로 전송되고 그 후에는 새 구매로 간주되어 다시 액세스할 수 있도록 앱이 복원됩니다.

**DELETE 요청을 시작할 때 Adobe에서 제공한 권한을 삭제할 수 있습니까?**

Adobe은 고객의 추가 직접 권한 부여 수당에 대한 정보를 삭제합니다. 앱(최종 사용자)이 고객이 사용한 OAuth 메커니즘에 로그인하면 Adobe에 정보를 전송하게 되고 서비스는 추가 권한을 다시 받게 됩니다.

**최종 사용자가 예상하는 것은?**

앱에 권한을 할당하는 키는 뷰어 소프트웨어의 일부로 장치에 있으므로 최종 사용자는 앱을 제거해야 합니다. 최종 사용자는 앱을 다시 설치하는 경우, 기존 구매(App Store 사용자와 관련) 및 직접 권한 부여 수당(고객의 OAuth 사용자와 관련)이 여전히 복원된다는 것을 깨달아야 합니다.

**디바이스의 사용자 간에 앱이 공유되면 어떻게 됩니까?**

Adobe에는 특정 사용자에게 직접 연결하는 정보가 거의 없습니다. 앱의 데이터에 저장되어 앱이 시작하는 모든 요청에서 전달된 임의로 생성된 UUID를 사용하여 데이터를 연결합니다. 즉, 동일한 장치에서 앱을 공유하는 최종 사용자가 동일한 UUID를 사용하고 모든 데이터가 GDPR 요청을 수행하는 사람이 소유로 간주됩니다. 액세스 및 삭제 요청에 대해 DPSC는 앱을 공유하는 사람을 한 사람으로 간주합니다.

**Analytics에서 추적할 개인 데이터는 무엇입니까?**

없음. 추적 중인 데이터가 있지만 앱 수준에 있습니다(개인 데이터가 아님). 여기에는 시작, 충돌, 닫기, 활동, 구매 또는 Folio 오버레이와 같은 이벤트가 포함됩니다. 지리적 위치, 이름, 장치 ID 또는 IP 주소는 추적되지 않습니다.

**최종 사용자가 정보를 제공했지만 찾을 수 없습니다. 왜 안 되나요?**

Digital Publishing Suite 제품이 발전함에 따라 서비스 구현이 변경되었으며 더 많은 데이터가 난독화되었습니다. 사용자가 제공한 데이터를 사용하여 데이터를 찾을 수 없는 경우 사용자의 데이터를 해당 사용자에게 다시 추적할 수 없음을 의미합니다.

### 예 {#example}

GDPR 요청을 시작하려면 Adobe 고객 지원 센터에 문의하십시오.

다음은 Digital Publishing Suite GDPR 요청의 입력 및 결과 출력 예입니다.

#### 입력:{#inputs}

```
dpsc-contractId = “12345-1234-12416234” 
directEntitlementId = “1234-1234-1234” 
windowsAppStoreId = “testWinAppStoreId” 
email = “test@what.com”
```

#### 출력 {#outputs}

```
{

    "jobId": "test-1524750204384",

    "product": "DPSC",

    "action": "access",

    "userIDS": [

        {

        "namespace": "email",

        "value": "test@what.com"

        },

        {

        "namespace": "windowsAppStoreId",

        "value": "testWinAppStoreId"

        },

        {

        "namespace": "directEntitlementId",

        "value": "1234-1234-1234"

        }

    ],

    "receiptData": {

    "recordsFound": 6,

    "recordsAffected": 0,

    "tablesModified": 0,

    "subscriptionsFound": 24,

    "entitlementsFound": 24

    },

    "records": {

        "DPS_Stage_EntitlementUserDevices": [

        {

            "user_id": "testc685-c9ca-4c1e-a11b-07d10ec724cf",

            "device_id": "appleStore:test1b16-f032-4d9c-9200-0d19999405c4",

            "account_id": "test@what.com"

        },

        {

            "user_id": "test967d-5179-4dc6-958c-facd9d94da38",

            "device_id": "appleStore:test3f07-d5aa-4b32-8fac-b2b690b7ccd7",

            "account_id": "test@what.com"

        },

        {

            "user_id": "test1838-6494-4e74-912c-1edf61581d0e",

            "device_id": "appleStore:test3813-f8cc-49ce-b021-50eb0814a3bb",

            "account_id": "1234-1234-1234"

        },

        {

            "user_id": "test5468-1a11-4e4c-be43-274181a9ef81",

            "device_id": "appleStore:testf082-2783-498d-ab62-b1b2e3eb67ae",

            "account_id": "1234-1234-1234"

        }

        ],

            "DPS_Stage_EntitlementUsers": [

        {

            "id": "store:test04a7-33a3-4b90-863d-79981ead0f19:appleStore",

            "part_id": "0",

            "alias_user_id": "testWinAppStoreId"

        },

        {

            "id": "internal:testd2da-0606-4444-87ef-0d5a1d4a121d:adobe",

            "part_id": "0",

            "user_id": "test@what.com"

        }

        ],

            "DPS_Stage_Subscriptions": [

        {

            "id": "appleStore:testc685-c9ca-4c1e-a11b-07d10ec724cf",

            "account_id": "test3531-a209-4391-beb9-951c7822244e",

            "overflow": "test4e59-86a8-4b75-b699-77e980c287ab",

            "entitlement_count": "12"

        },

        {

            "id": "appleStore:test5468-1a11-4e4c-be43-274181a9ef81",

            "account_id": "test491b-379e-4d24-96ef-e481bf8d3062",

            "overflow": "test931b-7422-485d-85a5-134828187b6c",

            "entitlement_count": "12"

        }

        ],

            "DPS_Stage_Entitlements": [

        {

            "id": "samsungStore:testc685-c9ca-4c1e-a11b-07d10ec724cf",

            "account_id": "test7332-60a0-42b8-a508-474668d83d2e",

            "overflow": "test9bc3-94d0-43cf-b132-0629868f7d9d",

            "entitlement_count": "12"

        },

        {

            "id": "appleStore:test5468-1a11-4e4c-be43-274181a9ef81",

            "account_id": "testf766-102a-460d-8f5a-42f7bb9d68b7",

            "overflow": "test4d96-2197-45a8-9caf-2aa2846b770c",

            "entitlement_count": "12"

        }

        ],

            "s3Buckets": {

            "name": "DPS-Entitlements-Overflow",

            "folder": "stage/",

            "overflows": {

            "subscriptions": [

            "test4e59-86a8-4b75-b699-77e980c287ab",

            "test931b-7422-485d-85a5-134828187b6c"

        ],

            "entitlements": [

            "test9bc3-94d0-43cf-b132-0629868f7d9d",

            "test4d96-2197-45a8-9caf-2aa2846b770c"

                ]

            }

        }

    }

}
```

