---
title: Adobe Sign과 통합| 사용자 데이터 처리
seo-title: Adobe Sign과 통합| 사용자 데이터 처리
description: 'null'
seo-description: 'null'
uuid: cb3a455d-2e33-44c8-8f71-3a7ecd939cd8
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e9e0d8fb-955e-4021-9e9a-9c95c6ffe88d
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Adobe Sign과 통합| 사용자 데이터 처리 {#integration-with-adobe-sign-handling-user-data}

AEM Forms는 Adobe Sign과 통합되므로 적응형 양식의 전자 서명 워크플로우를 통해 법률, 영업, 급여, 인사 관리 워크플로우에 대한 양식 또는 계약을 처리할 수 있습니다. 단일 및 다중 사용자 서명, 순차적 동시 서명 워크플로우, 익명 또는 로그인 사용자로 양식 서명, 사용자를 인증하는 다양한 방법 등을 지원합니다.

서명자 또는 여러 서명자가 적응형 양식에 서명하여 제출하는 경우 서명자에 대한 정보가 포함된 Adobe Sign 계약이 생성됩니다.

Adobe Sign과 AEM Forms 통합에 대한 자세한 내용은 적응형 [양식에서](/help/forms/using/working-with-adobe-sign.md)Adobe Sign 사용을 참조하십시오.

## 사용자 데이터 및 데이터 저장소 {#data}

Adobe Sign이 활성화된 적응형 양식에는 서명자에 대한 정보가 포함되며 적응형 양식으로 수집된 다른 사용자 데이터가 포함될 수 있습니다. Adobe Sign 서비스는 계약 내에서 서명을 사용하여 사용자 데이터를 저장합니다. 계약은 AEM Forms 클라우드 서비스에 구성된 Adobe Sign 서버에 저장됩니다. 또한 적응형 양식이 Forms 포털 제출 작업을 사용하도록 구성된 경우 계약 데이터는 양식 데이터와 함께 양식 포털 데이터 저장소에 저장됩니다.

## 사용자 데이터 액세스 및 삭제 {#access-and-delete-user-data}

사용자 데이터는 계약 내에서 수집되지만 서비스 테이블에 저장되지 않습니다. 관리자는 Adobe Sign을 사용하여 서비스에서 제어하는 데이터를 관리할 수 있습니다. Adobe Sign 서비스의 개인 정보 관리자는 요청자의 이메일 주소를 기준으로 계약서를 나열하거나 제거할 수 있습니다.

Adobe Sign은 참가자의 계약 검색을 허용하고 필요한 경우 계약 삭제를 허용하는 웹 애플리케이션을 제공합니다. 자세한 내용은 Adobe Sign - [기능:사용자 정보 삭제를 참조하십시오](https://helpx.adobe.com/sign/help/adobesign_gdpr_user_deletion.html).

양식 포털 제출 작업을 사용하도록 구성된 적응형 양식에 대한 계약 데이터도 양식 포털 데이터 저장소에 저장됩니다. 양식 포털 데이터 저장소에서 데이터에 액세스하고 삭제하려면 양식 포털을 [참조하십시오| 사용자 데이터](/help/forms/using/forms-portal-handling-user-data.md)처리.
