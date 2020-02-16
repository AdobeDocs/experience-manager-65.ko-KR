---
title: AEM Commerce - GDPR 준비
seo-title: AEM Commerce - GDPR 준비
description: 'null'
seo-description: 'null'
uuid: 7ca26587-8cce-4c75-8629-e0e5cfb8166c
contentOwner: carlino
discoiquuid: c637964a-dfcb-41fe-9c92-934620fe2cb3
translation-type: tm+mt
source-git-commit: 85a3dac5db940b81da9e74902a6aa475ec8f1780

---


# AEM Commerce - GDPR 준비{#aem-commerce-gdpr-readiness}

>[!IMPORTANT]
>
>GDPR은 아래 섹션에 소개되어 있지만, 자세한 내용은 모든 데이터 보호 및 개인 정보 보호 규정에 적용됩니다.(예: GDPR, CCPA 등)

2018년 5월부터 유럽 연합의 데이터 개인 정보 보호 규정이 적용됩니다. 자세한 내용은 Adobe 개인 정보 [보호 센터에서 GDPR 페이지를 참조하십시오](https://www.adobe.com/privacy/general-data-protection-regulation.html).

>[!NOTE]
>
>자세한 [내용은 AEM GDPR](/help/managing/data-protection-and-privacy.md) 준비를 참조하십시오.

![screen_shot_2018-03-22at111606](assets/screen_shot_2018-03-22at111606.jpg)

기본적으로 제공되는 상거래 통합에서 AEM은 서비스를 사용하고 헤드리스 모드에서 실행되는 고객 상거래 플랫폼으로 데이터를 다시 전송하는 경험 계층입니다.

일부 상거래 플랫폼의 경우 프로필 정보() 및 상거래 토큰(상거래 플랫폼에서 로그인)을 AEM에 저장합니다. `/home/users` 이러한 사용 사례는 AEM Platform [에 대한 GDPR 요청 처리를 참조하십시오](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md).

![screen_shot_2018-03-22at111621](assets/screen_shot_2018-03-22at111621.jpg)

## AEM Commerce에 대한 GDPR 요청 처리 {#handling-gdpr-requests-for-aem-commerce}

Salesforce Commerce Cloud 통합의 경우 AEM Commerce는 GDPR 관련 정보를 저장하지 않습니다. 요청을 Salesforce Cloud에 전달해야 [합니다](https://documentation.demandware.com/).

hybris 및 IBM WebSphere 통합의 경우 AEM 파섹 AEM Platform GDPR [지침을](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md) 사용하고 다음 질문을 고려해야 합니다.

1. **내 데이터는 어디에 저장되고 사용됩니까?** 이름, 상거래 사용자 식별자, 토큰, 암호, 주소 데이터 등과 같은 캐시된 사용자 프로필 정보가 AEM에서 표시됩니다.
1. **GDPR 관련 데이터는 누구에게 공유합니까?** AEM Commerce의 GDPR 관련 데이터 업데이트는 저장되지 않지만(위에 언급된 관련 프로필 정보 제외) 상거래 플랫폼으로 다시 프록시됩니다.
1. **사용자 데이터를**&#x200B;삭제하는 방법 AEM에서 사용자 프로필을 삭제하고 커머스 플랫폼에서 사용자 삭제를 호출합니다.

>[!NOTE]
>
>필요한 경우 [hybris wiki](https://wiki.hybris.com/) 또는 Websphere [Commerce 설명서를](https://www-01.ibm.com/support/docview.wss?uid=swg27036450) 살펴보십시오.

