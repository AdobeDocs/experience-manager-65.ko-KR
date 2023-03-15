---
title: Adobe Sign과 통합 | 사용자 데이터 처리
seo-title: Integration with Adobe Sign | Handling user data
description: Adobe Sign과 통합 | 사용자 데이터 처리
uuid: cb3a455d-2e33-44c8-8f71-3a7ecd939cd8
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e9e0d8fb-955e-4021-9e9a-9c95c6ffe88d
feature: Acrobat Sign
role: Admin
exl-id: b43ed9b7-b1ef-4878-ae3b-643b558eed7b
source-git-commit: 28d092a7713438c27213766f0bb702b699305b88
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 0%

---

# Adobe Sign과 통합 | 사용자 데이터 처리 {#integration-with-adobe-sign-handling-user-data}

[!DNL AEM Forms] 와 통합됨[!DNL  Adobe Sign] 적응형 양식에서 전자 서명 워크플로를 사용하여 법적, 판매, 급여, 인적 자원 관리 워크플로에 대한 양식 또는 계약을 처리할 수 있습니다. 단일 및 다중 사용자 서명, 순차적 및 동시 서명 워크플로, 익명 또는 로그인 사용자로 양식 서명, 여러 사용자 인증 방법이 가능합니다.

서명자 또는 여러 서명자가 서명하고 적응형 양식을 제출하는 경우 [!DNL Adobe Sign] 서명자에 대한 정보가 포함된 계약이 생성됩니다.

에 대한 자세한 내용 [!DNL AEM Forms] 과 통합 [!DNL Adobe Sign], 참조 [적응형 양식에서 Adobe Sign 사용](/help/forms/using/working-with-adobe-sign.md).

## 사용자 데이터 및 데이터 저장소 {#data}

[!DNL Adobe Sign] 활성화된 적응형 양식에는 서명자에 대한 정보가 포함되며, 적응형 양식에 의해 수집된 다른 사용자 데이터가 포함될 수 있습니다. 다음 [!DNL Adobe Sign] 서비스는 계약 내의 서명과 함께 사용자 데이터를 저장합니다. 계약은 다음에 저장됩니다. [!DNL Adobe Sign] 서버 구성 위치 [!DNL AEM Forms] 클라우드 서비스. 또한 적응형 양식이 Forms 포털 제출 액션을 사용하도록 구성된 경우 계약 데이터가 양식 데이터와 함께 양식 포털 데이터 저장소에 저장됩니다.

## 사용자 데이터 액세스 및 삭제 {#access-and-delete-user-data}

사용자 데이터는 계약 내에서 수집되지만 서비스 테이블에는 저장되지 않습니다. [!DNL Adobe Sign] 을 사용하면 관리자가 서비스에서 제어하는 데이터를 스스로 관리할 수 있습니다. 의 개인 정보 관리자 [!DNL Adobe Sign] 서비스는 요청자의 이메일 주소에 따라 계약을 나열하거나 제거할 수 있습니다.

[!DNL Adobe Sign] 은 참가자가 계약을 검색하고 필요한 경우 삭제할 수 있는 웹 애플리케이션을 제공합니다. 자세한 내용은 [Adobe Sign - 기능: 사용자 정보 삭제](https://helpx.adobe.com/sign/help/adobesign_gdpr_user_deletion.html).

Forms 포털 제출 액션을 사용하도록 구성된 적응형 양식에 대한 계약 데이터도 양식 포털 데이터 저장소에 저장됩니다. Forms 포털 데이터 저장소에서 데이터에 액세스하고 삭제하려면 다음을 참조하십시오 [Forms 포털 | 사용자 데이터 처리](/help/forms/using/forms-portal-handling-user-data.md).
