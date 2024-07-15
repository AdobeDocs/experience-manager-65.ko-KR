---
title: 단일 사인온 및 시간 제한 핸들러
description: AEM Forms 작업 영역에 대한 세션 시간 초과 값을 설정하는 방법
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 4f824d80-f3f8-4010-9583-5a9ab1151a7b
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---

# 단일 사인온 및 시간 제한 핸들러 {#single-sign-on-and-timeout-handlers}

AEM Forms 작업 영역이 SSO로 활성화되어 있습니다. 사용자가 Forms Manager 또는 PDF Generator 사용자 인터페이스와 같은 AEM Forms 애플리케이션에 로그인하여 동일한 브라우저 세션에서 AEM Forms 작업 영역에 액세스한 경우 AEM Forms 작업 영역에 로그인되고 반대의 경우도 마찬가지입니다.

## AEM Forms 작업 영역에서 서버 시간 제한 처리 {#handling-server-timeout-in-nbsp-aem-forms-workspace}

사용자의 세션 시간 초과는 관리 콘솔에서 구성할 수 있습니다.

시간 제한을 설정하려면 `https://'[server]:[port]'/adminui`에 로그인하고 **설정 > 사용자 관리 > 구성 > 고급 시스템 특성 구성**&#x200B;으로 이동하여 원하는 설정을 만드십시오.

AEM Forms에서 작업 공간 시간 초과는 다음과 같이 처리됩니다.

* 사용자의 세션 기간은 사용자 세션을 초기화하는 `initialize` 호출의 응답에서 사용할 수 있습니다.
* 팝업 대화 상자는 세션 만료 15초 전에 세션이 곧 만료될 것임을 사용자에게 알립니다.

이 팝업 대화 상자에서:

* 확인 을 클릭하여 사용자 세션을 종료합니다.
* 사용자 세션을 다시 초기화하려면 [취소]를 클릭하십시오.

>[!NOTE]
>
>아무 작업도 수행되지 않으면 사용자는 세션 만료 3초 전에 AEM Forms 작업 영역에서 자동으로 로그아웃됩니다.
