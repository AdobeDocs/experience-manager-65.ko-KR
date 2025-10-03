---
title: 고급 시스템 속성 구성
description: 고급 시스템 속성 구성 페이지에서는 파일을 내보내서 편집한 후 다시 가져오지 않고도 구성 파일의 특정 설정을 수정할 수 있습니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 809af2c0-6f5c-4dd4-af48-dbf476c9ea45
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: ht
source-wordcount: '480'
ht-degree: 100%

---

# 고급 시스템 속성 구성 {#configure-advanced-system-attributes}

고급 시스템 속성 구성 페이지에서는 파일을 내보내서 편집한 후 다시 가져오지 않고도 구성 파일의 특정 설정을 수정할 수 있습니다. ([구성 파일 가져오기 및 내보내기](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file)를 참조하십시오.)

1. 관리 콘솔에서 **[!UICONTROL 설정 > 사용자 관리 > 구성 > 고급 시스템 속성 구성]**&#x200B;을 클릭합니다.
1. (선택 사항) 다음과 같은 세션 속성을 변경합니다.

   **세션 시간 초과 제한(분):** 사용자가 시스템에서 자동으로 로그아웃되기 전까지 걸리는 시간(분)입니다. 기본적으로 워크벤치와 같은 AEM Forms 구성 요소는 활동 여부와 관계없이 2시간 후에 시간이 초과되며 사용자는 다시 로그인해야 합니다. 유효한 값은 `1`~`1440`입니다. 기본값은 `120`(2시간)입니다. 이 설정은 구성 파일의 `SAML/Producer/assertionValidityInMinutes` 항목 키를 업데이트합니다.

   >[!NOTE]
   >
   >시스템이 제대로 작동하지 않을 수 있으므로 세션 시간 초과 제한을 10분 미만으로 설정해서는 안 됩니다. 권장 값은 10~120(분)입니다.

   **어설션 임계값(초):** 클러스터 내 AEM Forms 애플리케이션 서버 간 시스템 시간 차이로 발생하는 지연을 상쇄하기 위한 버퍼 시간입니다. AEM Forms는 이 속성에 지정된 시간(초)만큼 사용자 로그인 시간을 이전 일자로 되돌립니다. 유효한 값은 `0`~`3600`입니다. 기본값은 `60`입니다. 이 설정은 구성 파일의 `SAML/Producer/assertionThresholdInSeconds` 항목 키를 업데이트합니다.

   **최대 허용 어설션 갱신 횟수:** 로그인을 하지 않아도 사용자 세션을 투명하게 갱신할 수 있는 최대 횟수입니다. 유효한 값은 `0`~`9999`입니다. `0` 값은 어설션이 갱신되지 않음을 의미합니다. 기본값은 10입니다. 이 설정은 구성 파일의 `SAML/Producer/maxAssertionRenewalCount` 항목 키를 업데이트합니다.

1. (선택 사항) 다음과 같은 디렉터리 동기화 속성을 변경합니다.

   **동기화 통계 로깅:** 동기화 프로세스 중에 사용자 관리에서 상세 통계를 기록할지 여부를 지정합니다. ([동기화 시 상세 로깅 활성화 또는 비활성화](/help/forms/using/admin-help/synchronizing-directories.md#enable-or-disable-detailed-logging-during-synchronization)를 참조하십시오.)

   **동기화 완료 Cron 표현식:** 사용자 관리에서 실패한 동기화를 재시도하는 간격입니다. ([디렉터리 동기화 재시도 옵션 구성](/help/forms/using/admin-help/synchronizing-directories.md#configure-the-directory-synchronization-retry-option)을 참조하십시오.)

   **클러스터 작업 잠금 시간 초과(분):** 클러스터링된 환경에서 사용됩니다. 한 노드의 동기화가 실패하고 클러스터 잠금이 해제되지 않으면 이 값은 다른 노드가 강제로 잠금을 설정하기 전에 대기하는 시간(분)을 지정합니다. 기본값은 `15`분입니다. 유효한 값은 `1`~`1440`분입니다.

1. (선택 사항) 다음 속성을 변경한 후 **[!UICONTROL 확인]**&#x200B;을 클릭합니다.

   **사용자 관리자 이벤트 감사:** 디렉터리 동기화 이벤트와 성공, 실패, 잠금과 같은 인증 이벤트에 대한 감사를 활성화하려면 이 옵션을 선택합니다. 기본적으로 이 옵션은 Rights Management와 같이 감사가 필요한 구성 요소를 설치하지 않은 한 선택되지 않습니다. 이 설정은 구성 파일의 `APSAuditService` 항목 키를 업데이트합니다.

   **동적 그룹 자동 생성:** 이메일 도메인을 기반으로 동적 그룹을 자동으로 만들 수 있습니다. ([동적 그룹 만들기](/help/forms/using/admin-help/creating-configuring-groups.md#create-a-dynamic-group)를 참조하십시오.)

다시 로드를 클릭하면 원래 사용자 관리 설정으로 되돌릴 수 있습니다.
