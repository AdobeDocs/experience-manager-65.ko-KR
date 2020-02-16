---
title: 고급 시스템 속성 구성
seo-title: 고급 시스템 속성 구성
description: '[고급 시스템 속성 구성] 페이지에서는 파일을 내보내고 편집하고 가져올 필요 없이 구성 파일의 특정 설정을 수정할 수 있습니다.'
seo-description: '[고급 시스템 속성 구성] 페이지에서는 파일을 내보내고 편집하고 가져올 필요 없이 구성 파일의 특정 설정을 수정할 수 있습니다.'
uuid: 6bcfbaa9-f492-46aa-97d2-00fc3e67d0d7
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 533ad3f7-3905-420d-8bb9-8ae8f14fb28e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 고급 시스템 속성 구성 {#configure-advanced-system-attributes}

[고급 시스템 속성 구성] 페이지에서는 파일을 내보내고 편집하고 가져올 필요 없이 구성 파일의 특정 설정을 수정할 수 있습니다. 구성 [파일](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file)가져오기 및 내보내기를 참조하십시오.

1. 관리 콘솔에서 설정 > 사용자 **[!UICONTROL 관리 > 구성 > 고급 시스템 속성 구성을 클릭합니다]**.
1. (선택 사항) 다음 세션 속성을 변경합니다.

   **** 세션 시간 제한(분):사용자가 시스템에서 자동으로 로그아웃되기 전의 시간(분)입니다. 기본적으로 Workbench와 같은 AEM 양식 구성 요소는 활동 또는 비활동과는 상관없이 2시간 후 시간 초과되며 사용자는 다시 로그인해야 합니다. 유효한 값은 `1` 입니다 `1440`. 기본값은 `120` (2시간)입니다. 이 설정은 구성 파일의 `SAML/Producer/assertionValidityInMinutes` 시작 키를 업데이트합니다.

   >[!NOTE]
   >
   >시스템이 제대로 작동하지 않을 수 있으므로 세션 시간 초과 제한을 10분 미만으로 설정하면 안 됩니다. 권장 값은 10-120(분)입니다.

   **** 어설션 임계값(초):클러스터의 AEM 양식 응용 프로그램 서버 간 시스템 시간 차이로 인해 지연을 상쇄하는 버퍼 시간입니다. AEM Forms는 이 속성에 지정된 시간(초)만큼 사용자의 로그인 시간을 소급 적용합니다. 유효한 값은 `0` 입니다 `3600`. 기본값은 `60`입니다. 이 설정은 구성 파일의 `SAML/Producer/assertionThresholdInSeconds` 시작 키를 업데이트합니다.

   **** 어설션의 최대 허용 갱신:로그인 없이 사용자의 세션을 투명하게 갱신할 수 있는 최대 횟수입니다. 유효한 값은 `0` 입니다 `9999`. 값은 `0` 어설션이 갱신되지 않음을 의미합니다. 기본값은 10입니다. 이 설정은 구성 파일의 `SAML/Producer/maxAssertionRenewalCount` 시작 키를 업데이트합니다.

1. (선택 사항) 다음 디렉토리 동기화 속성을 변경합니다.

   **** 통계 로깅 동기화:사용자 관리에서 동기화 프로세스 동안 세부 통계를 기록할지 여부를 지정합니다. 동기화 [중 자세한 로깅 활성화 또는 비활성화를](/help/forms/using/admin-help/synchronizing-directories.md#enable-or-disable-detailed-logging-during-synchronization)참조하십시오.

   **** 마무리 처리자 변환 식 동기화:사용자 관리 재시도가 실패한 동기화 간격입니다. 자세한 내용은 [디렉토리 동기화 재시도 옵션](/help/forms/using/admin-help/synchronizing-directories.md#configure-the-directory-synchronization-retry-option)구성을 참조하십시오.

   **** 클러스터 작업 잠금 제한 시간(분):클러스터된 환경에서 사용됩니다. 한 노드의 동기화가 실패하고 클러스터 잠금이 해제되지 않은 경우 이 값은 다른 노드가 잠금을 강제로 가져오기 전에 대기하는 시간(분)을 지정합니다. 기본값은 `15` 분입니다. 유효한 값은 `1` 분 단위입니다 `1440` .

1. (선택 사항) 다음 속성을 변경한 다음 확인을 **[!UICONTROL 클릭합니다]**.

   **** 사용자 관리자 이벤트 감사:디렉토리 동기화 이벤트 및 성공, 실패 및 잠금과 같은 인증 이벤트 감사를 활성화하려면 이 옵션을 선택합니다. 기본적으로 이 옵션은 권한 관리와 같은 감사를 필요로 하는 구성 요소를 설치하지 않는 한 선택되지 않습니다. 이 설정은 구성 파일의 `APSAuditService` 시작 키를 업데이트합니다.

   **** 동적 그룹 자동 생성:이메일 도메인을 기반으로 동적 그룹을 자동으로 만들 수 있습니다. (동적 [그룹](/help/forms/using/admin-help/creating-configuring-groups.md#create-a-dynamic-group)만들기를 참조하십시오.)

다시 로드를 클릭하여 원래 사용자 관리 설정으로 되돌릴 수도 있습니다.
