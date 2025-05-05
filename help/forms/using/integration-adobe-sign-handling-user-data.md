---
title: Adobe Sign과 통합 | 사용자 데이터 처리
description: 적응형 양식의 전자 서명을 위한 Adobe Sign과의 AEM Forms 통합에 대해 알아봅니다. 다양한 워크플로우에 대한 여러 서명 옵션을 지원합니다.
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Acrobat Sign
role: Admin, User, Developer
exl-id: b43ed9b7-b1ef-4878-ae3b-643b558eed7b
solution: Experience Manager, Experience Manager Forms
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---

# Adobe Sign과 통합 | 사용자 데이터 처리 {#integration-with-adobe-sign-handling-user-data}

[!DNL AEM Forms]은(는) [!DNL &#x200B; Adobe Sign]과(와) 통합되어 적응형 양식의 전자 서명 워크플로에서 법률, 판매, 급여, 인적 자원 관리 워크플로에 대한 양식 또는 계약을 처리할 수 있습니다. 단일 및 다중 사용자 서명, 순차적 및 동시 서명 워크플로, 익명 또는 로그인 사용자로 양식 서명, 여러 사용자 인증 방법이 가능합니다.

서명자 또는 여러 서명자가 서명하고 적응형 양식을 제출하면 서명자에 대한 정보가 포함된 [!DNL Adobe Sign] 계약이 생성됩니다.

[!DNL Adobe Sign]과의 [!DNL AEM Forms] 통합에 대한 자세한 내용은 [적응형 양식에서 Adobe Sign 사용](/help/forms/using/working-with-adobe-sign.md)을 참조하세요.

## 사용자 데이터 및 데이터 저장소 {#data}

[!DNL Adobe Sign] 사용 적응형 양식에는 서명자에 대한 정보가 포함되어 있으며 적응형 양식에서 수집한 다른 사용자 데이터가 포함될 수 있습니다. [!DNL Adobe Sign] 서비스는 계약 내의 서명으로 사용자 데이터를 저장합니다. [!DNL AEM Forms] 클라우드 서비스에 구성된 [!DNL Adobe Sign] 서버에 계약서가 저장됩니다. 또한 적응형 양식이 Forms 포털 제출 액션을 사용하도록 구성된 경우 계약 데이터가 양식 데이터와 함께 Forms 포털 데이터 저장소에 저장됩니다.

## 사용자 데이터 액세스 및 삭제 {#access-and-delete-user-data}

사용자 데이터는 계약 내에서 수집되지만 서비스 테이블에는 저장되지 않습니다. [!DNL Adobe Sign]을(를) 사용하면 관리자가 서비스에서 제어하는 데이터를 직접 관리할 수 있습니다. [!DNL Adobe Sign] 서비스의 개인 정보 관리자는 요청자의 전자 메일 주소를 기반으로 계약을 나열하거나 제거할 수 있습니다.

[!DNL Adobe Sign]은(는) 참가자가 계약을 검색하고 필요한 경우 삭제할 수 있도록 허용하는 웹 응용 프로그램을 제공합니다. 자세한 내용은 [Adobe Sign - 기능: 사용자 정보 삭제](https://helpx.adobe.com/kr/sign/help/adobesign_gdpr_user_deletion.html)를 참조하십시오.

Forms 포털 제출 액션을 사용하도록 구성된 적응형 양식에 대한 계약 데이터도 Forms 포털 데이터 저장소에 저장됩니다. Forms 포털 데이터 저장소에서 데이터에 액세스하고 삭제하려면 [Forms 포털을 참조하십시오. | 사용자 데이터 ](/help/forms/using/forms-portal-handling-user-data.md)을(를) 처리하고 있습니다.
