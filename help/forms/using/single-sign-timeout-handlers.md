---
title: Single Sign On 및 시간 초과 핸들러
seo-title: Single Sign On 및 시간 초과 핸들러
description: AEM Forms 작업 영역에 대한 세션 시간 초과 값을 설정하는 방법.
seo-description: AEM Forms 작업 영역에 대한 세션 시간 초과 값을 설정하는 방법.
uuid: 17583fd5-6453-41d3-bb63-a639983fbea9
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 698990a2-dd3f-480f-9d15-d87563860297
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Single Sign On 및 시간 초과 핸들러 {#single-sign-on-and-timeout-handlers}

AEM Forms 작업 영역이 SSO 파섹 사용자가 Forms Manager 또는 PDF Generator 사용자 인터페이스와 같은 AEM Forms 응용 프로그램에 로그인하고 동일한 브라우저 세션에서 AEM Forms 작업 영역에 액세스한 경우, 사용자는 AEM Forms 작업 영역에 로그인하거나 그 반대의 경우도 마찬가지입니다.

## AEM Forms 작업 영역의 서버 시간 초과 처리 {#handling-server-timeout-in-nbsp-aem-forms-workspace}

사용자에 대한 세션 시간 초과는 관리 콘솔에서 구성할 수 있습니다.

시간 초과를 설정하려면 [설정] > [ `https://'[server]:[port]'/adminui`사용자 관리] > [구성] **> [고급 시스템 속성 구성]**&#x200B;으로 이동하여 원하는 설정을 만듭니다.

AEM Forms 작업 영역의 시간 제한은 다음과 같이 처리됩니다.

* 사용자의 세션 기간은 사용자 세션을 초기화하는 `initialize` 호출에 대한 응답으로 사용할 수 있습니다.
* 팝업 대화 상자는 세션 만료 15초 전에 세션이 만료될 것임을 사용자에게 알립니다.

이 팝업 대화 상자에서 다음을 수행합니다.

* 확인을 클릭하여 사용자 세션을 종료합니다.
* 사용자 세션을 다시 초기화하려면 취소를 클릭합니다.

>[!NOTE]
>
>작업이 수행되지 않으면 사용자는 세션 만료 3초 전에 AEM Forms 작업 영역에서 자동으로 로그아웃됩니다.

**[지원 문의](https://www.adobe.com/account/sign-in.supportportal.html)**
