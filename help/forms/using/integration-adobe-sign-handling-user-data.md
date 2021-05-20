---
title: Adobe Sign과 통합 | 사용자 데이터 처리
seo-title: Adobe Sign과 통합 | 사용자 데이터 처리
description: Adobe Sign과 통합 | 사용자 데이터 처리
uuid: cb3a455d-2e33-44c8-8f71-3a7ecd939cd8
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e9e0d8fb-955e-4021-9e9a-9c95c6ffe88d
feature: Adobe Sign
role: Administrator
exl-id: b43ed9b7-b1ef-4878-ae3b-643b558eed7b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---

# Adobe Sign과 통합 | 사용자 데이터 처리 {#integration-with-adobe-sign-handling-user-data}

[!DNL AEM Forms] 을([!DNL  Adobe Sign] 를) 통합하여 적응형 양식의 전자 서명 워크플로우를 통합하여 법률, 영업, 급여, 인적 자원 관리 워크플로우에 대한 양식 또는 계약을 처리할 수 있도록 합니다. 단일 및 다중 사용자 서명, 순차적 및 동시 서명 워크플로우, 익명 또는 로그인 사용자로 양식에 서명 및 사용자를 인증할 수 있는 다양한 방법을 허용합니다.

서명자 또는 여러 서명자가 서명하여 적응형 양식을 제출하면 서명자에 대한 정보가 포함된 [!DNL Adobe Sign] 계약이 생성됩니다.

[!DNL AEM Forms] 통합에 [!DNL Adobe Sign]대한 자세한 내용은 적응형 양식](/help/forms/using/working-with-adobe-sign.md)에서 Adobe Sign 사용 을 참조하십시오.[

## 사용자 데이터 및 데이터 저장소 {#data}

[!DNL Adobe Sign] 활성화된 적응형 양식에는 서명자에 대한 정보가 포함되며 적응형 양식으로 수집된 다른 사용자 데이터를 포함할 수 있습니다. [!DNL Adobe Sign] 서비스는 계약 내에 서명과 함께 사용자 데이터를 저장합니다. 계약은 [!DNL AEM Forms] 클라우드 서비스에 구성된 [!DNL Adobe Sign] 서버에 저장됩니다. 또한 적응형 양식이 Forms Portal 제출 작업을 사용하도록 구성된 경우 계약 데이터가 양식 데이터와 함께 Forms 포털 데이터 저장소에 저장됩니다.

## 사용자 데이터 {#access-and-delete-user-data} 액세스 및 삭제

사용자 데이터는 계약 내에서 수집되지만 서비스 테이블에 저장되지 않습니다. [!DNL Adobe Sign] 는 관리자가 서비스에서 제어하는 데이터 관리에 대해 스스로 선택할 수 있도록 합니다. [!DNL Adobe Sign] 서비스의 개인 정보 관리자는 요청자의 전자 메일 주소를 기준으로 계약을 나열하거나 제거할 수 있습니다.

[!DNL Adobe Sign] 참가자가 계약을 검색할 수 있고 필요한 경우 삭제할 수 있는 웹 응용 프로그램을 제공합니다. 자세한 내용은 [Adobe Sign - 기능:사용자 정보 삭제](https://helpx.adobe.com/sign/help/adobesign_gdpr_user_deletion.html).

Forms Portal 제출 작업을 사용하도록 구성된 적응형 양식에 대한 계약 데이터도 forms 포털 데이터 저장소에 저장됩니다. forms 포털 데이터 저장소에서 데이터에 액세스하고 삭제하려면 [Forms 포털 을 참조하십시오 | 사용자 데이터 처리](/help/forms/using/forms-portal-handling-user-data.md).
