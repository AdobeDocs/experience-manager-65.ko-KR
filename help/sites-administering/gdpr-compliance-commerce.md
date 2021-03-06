---
title: AEM Commerce - GDPR 준비 완료
seo-title: AEM Commerce - GDPR 준비 완료
description: '"AEM Commerce - GDPR 준비 완료"'
seo-description: 'null'
uuid: 7ca26587-8cce-4c75-8629-e0e5cfb8166c
contentOwner: carlino
discoiquuid: c637964a-dfcb-41fe-9c92-934620fe2cb3
exl-id: 3a483b9d-627a-41d3-8ac1-66f9c5e89ad5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 23%

---

# AEM Commerce - GDPR 준비{#aem-commerce-gdpr-readiness}

>[!IMPORTANT]
>
>아래 섹션에서는 GDPR이 예로 사용되지만, 포함된 세부 사항은 GDPR, CCPA 등 모든 데이터 보호 및 개인 정보 보호 규정에 적용됩니다.

데이터 사생활 보호권에 관한 유럽 연합의 GDPR(일반 데이터 보호 규정)은 2018년 5월에 발효됩니다. 자세한 내용은 [Adobe 개인 정보 보호 센터의 GDPR 페이지](https://www.adobe.com/privacy/general-data-protection-regulation.html)를 참조하십시오.

>[!NOTE]
>
>자세한 내용은 [AEM GDPR 준비 완료](/help/managing/data-protection-and-privacy.md)를 참조하십시오.

![screen_shot_2018-03-22at111606](assets/screen_shot_2018-03-22at111606.jpg)

기본 제공 전자 상거래 통합에서 AEM은 서비스를 사용하고 헤드리스 모드에서 실행되는 고객 상거래 플랫폼으로 데이터를 다시 전송하는 경험 계층입니다.

일부 상거래 플랫폼의 경우, AEM에 프로필 정보( `/home/users`)와 상거래 토큰(상거래 플랫폼에서 로그인)을 저장합니다. 이러한 사용 사례에 대해서는 [AEM Platform](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md)에 대한 GDPR 요청 처리 를 참조하십시오.

![screen_shot_2018-03-22at111621](assets/screen_shot_2018-03-22at111621.jpg)

## AEM Commerce에 대한 GDPR 요청 처리 {#handling-gdpr-requests-for-aem-commerce}

Salesforce Commerce Cloud 통합의 경우 AEM Commerce는 GDPR 관련 정보를 저장하지 않습니다. 요청을 [Salesforce Cloud](https://documentation.demandware.com/)에 전달해야 합니다.

hybris 및 IBM WebSphere 통합의 경우 AEM에 데이터가 일부 있습니다. [AEM Platform GDPR 지침](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md)을 사용하고 다음 질문을 고려해야 합니다.

1. **내 데이터는 어디에 저장/사용됩니까?** 이름, 상거래 사용자 식별자, 토큰, 암호, 주소 데이터 등과 같은 캐시된 사용자 프로필 정보는 AEM에서 표시됩니다.
1. **포함된 GDPR 데이터는 누구와 공유합니까?** AEM Commerce의 GDPR 관련 데이터 업데이트는 (위에서 언급한 대로 관련 프로필 정보 제외)가 저장되지 않고 상거래 플랫폼으로 다시 프록시됩니다.
1. **사용자 데이터를 삭제하는 방법** AEM에서 사용자 프로필을 삭제하고 상거래 플랫폼에서 사용자 삭제를 호출합니다.

>[!NOTE]
>
>필요한 경우 [hybris wiki](https://wiki.hybris.com/) 또는 [Websphere Commerce 설명서](https://www-01.ibm.com/support/docview.wss?uid=swg27036450)를 보십시오.
