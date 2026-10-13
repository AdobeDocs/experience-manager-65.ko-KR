---
title: AEM Commerce - GDPR 준비 상태
description: AEM Commerce에서 GDPR 요청을 처리하는 절차 및 사용 방법에 대해 알아봅니다.
contentOwner: carlino
exl-id: 3a483b9d-627a-41d3-8ac1-66f9c5e89ad5
solution: Experience Manager, Experience Manager Sites
feature: Compliance
role: Admin, Developer, Leader, User
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: b1210526-416b-4ef6-bcc0-1692e99f30e9
    internal-label: Administration and security
subfeature_v2:
  - id: c42c36cf-eeed-484a-8b39-a33a68192a07
    internal-label: Compliance
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 10%
---
# AEM Commerce - GDPR 준비 상태{#aem-commerce-gdpr-readiness}

>[!IMPORTANT]
>
>아래 섹션에서는 GDPR이 예로 사용되지만, 포함된 세부 사항은 GDPR 및 CCPA와 같은 모든 데이터 보호 및 개인 정보 보호 규정에 적용됩니다.

데이터 사생활 보호권에 관한 유럽 연합의 GDPR(일반 데이터 보호 규정)은 2018년 5월에 발효됩니다. Adobe 개인 정보 보호 센터의 [GDPR 페이지](https://business.adobe.com/kr/privacy/general-data-protection-regulation.html)를 참조하세요.

>[!NOTE]
>
>자세한 내용은 [AEM GDPR 준비 완료](/help/managing/data-protection-and-privacy.md)를 참조하십시오.

![screen_shot_2018-03-22at111606](assets/screen_shot_2018-03-22at111606.jpg)

Adobe의 획기적인 Commerce 통합을 통해 AEM은 서비스를 소비하고 헤드리스 모드에서 실행되는 고객 상거래 플랫폼으로 데이터를 다시 전송하는 경험 계층입니다.

일부 상거래 플랫폼의 경우 Adobe은 프로필 정보(`/home/users`)와 상거래 토큰(상거래 플랫폼에 로그온하기 위한)을 AEM에 저장합니다. 이러한 사용 사례에 대해서는 [AEM 플랫폼에 대한 GDPR 요청 처리](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md)를 참조하십시오.

![screen_shot_2018-03-22at111621](assets/screen_shot_2018-03-22at111621.jpg)

## AEM Commerce에 대한 GDPR 요청 처리 {#handling-gdpr-requests-for-aem-commerce}

Salesforce Commerce Cloud 통합의 경우 AEM Commerce은 GDPR 관련 정보를 저장하지 않습니다. [Salesforce Cloud](https://documentation.b2c.commercecloud.salesforce.com/DOC1/index.jsp)에 요청을 전달합니다.

hybris 및 HCL WebSphere® Commerce 통합의 경우 AEM에 일부 데이터가 있습니다. [AEM Platform GDPR 지침](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md)을 사용하고 다음 질문을 고려하십시오.

1. **내 데이터가 저장/사용되는 위치는 어디입니까?** AEM에 표시된 대로 이름, 상거래 사용자 식별자, 토큰, 암호 및 주소 데이터와 같은 캐시된 사용자 프로필 정보.
1. **적용 GDPR 데이터를 누구와 공유합니까?** AEM Commerce의 GDPR 관련 데이터 업데이트는 저장되지 않지만(위에 언급된 대로 관련 프로필 정보 제외) 상거래 플랫폼으로 다시 프록시됩니다.
1. **내 사용자 데이터를 삭제하는 방법**? AEM에서 사용자 프로필을 삭제하고 상거래 플랫폼에서 사용자 삭제를 호출합니다.

>[!NOTE]
>
>필요한 경우 [hybris wiki](https://wiki.hybris.com/) 또는 [HCL WebSphere® Commerce 설명서](https://help.hcltechsw.com/commerce/index.html)를 살펴보십시오.
