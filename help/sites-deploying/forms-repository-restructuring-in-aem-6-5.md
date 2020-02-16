---
title: AEM 6.5의 양식 저장소 재구성
seo-title: AEM 6.5의 양식 저장소 재구성
description: AEM 6.5 for Forms의 새로운 저장소 구조로 마이그레이션하기 위해 필요한 변경 사항을 수행하는 방법을 알아봅니다.
seo-description: AEM 6.5 for Forms의 새로운 저장소 구조로 마이그레이션하기 위해 필요한 변경 사항을 수행하는 방법을 알아봅니다.
uuid: e60830d4-23ca-4be9-941a-ee4abe4786a6
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 1ce9a622-5968-407f-a74b-d325a2bff669
translation-type: tm+mt
source-git-commit: d20ddba254c965e1b0c0fc84a482b7e89d4df5cb

---


# AEM 6.5의 양식 저장소 재구성{#forms-repository-restructuring-in-aem}

AEM 6.5 [의 상위 리포지토리 재조정](/help/sites-deploying/repository-restructuring.md) 페이지에 설명된 대로, AEM 6.5로 업그레이드하는 고객은 이 페이지를 사용하여 AEM Forms 솔루션에 영향을 주는 리포지토리 변경과 관련된 작업 노력을 평가해야 합니다. 일부 변경 사항은 AEM 6.5 업그레이드 프로세스 동안 작업해야 하는 반면, 다른 변경 사항은 향후 업그레이드될 때까지 연기될 수 있습니다.

**6.5 업그레이드 포함**

* [기타](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#misc)

**업그레이드 전**

* [Echosign 클라우드 서비스 구성](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#echosign-cloud-service-configuration)
* [Recaptcha Cloud 서비스 구성](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#recaptcha-cloud-service-configurations)
* [Typekit 클라우드 서비스 구성](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#typekit-cloud-service-configurations)
* [기타](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#misc)

## 6.5 업그레이드 포함 {#with-upgrade}

### 기타 {#misc}

| **이전 위치** | `/etc/clientlibs/fd/fp` |
|---|---|
| **새 위치** | `/libs/fd/fp/components` |
| **구조 조정 지침** | 기존 위치에 대한 사용자 지정 코드의 명시적 참조는 새 위치로 업데이트해야 합니다. |
| **메모** | 이러한 클라이언트 라이브러리는 수정하거나 확장해서는 안 됩니다. |

| **이전 위치** | `/etc/clientlibs/fd/rte` |
|---|---|
| **새 위치** | `/libs/fd/rte` |
| **구조 조정 지침** | 절대 경로로 참조할 수 있는 클라이언트 라이브러리의 리소스를 보려면 새 자산에 새 경로를 사용해야 합니다. |
| **메모** | N/A |

| **이전 위치** | `/etc/clientlibs/fd/af` |
|---|---|
| **새 위치** | `/libs/fd/af/authoring/clientlibs` |
| **구조 조정 지침** | 절대 경로로 참조할 수 있는 클라이언트 라이브러리의 리소스를 보려면 새 자산에 새 경로를 사용해야 합니다. |
| **메모** | N/A |

| **이전 위치** | `/etc/clientlibs/fd/xfaforms` |
|---|---|
| **새 위치** | `/libs/fd/xfaforms/clientlibs/` |
| **구조 조정 지침** | 절대 경로로 참조할 수 있는 클라이언트 라이브러리의 리소스를 보려면 새 자산에 새 경로를 사용해야 합니다. |
| **메모** | N/A |

| **이전 위치** | `/etc/clientlibs/fd/af` |
|---|---|
| **새 위치** | `/libs/fd/af/runtime/clientlibs` |
| **구조 조정 지침** | 절대 경로로 참조할 수 있는 클라이언트 라이브러리의 리소스를 보려면 새 자산에 새 경로를 사용해야 합니다. |
| **메모** | N/A |

| **이전 위치** | `/etc/clientlibs/fd/af` |
|---|---|
| **새 위치** | `/libs/fd/af/runtime/clientlibs` |
| **구조 조정 지침** | 절대 경로로 참조할 수 있는 클라이언트 라이브러리의 리소스를 보려면 새 자산에 새 경로를 사용해야 합니다. |
| **메모** | N/A |

| **이전 위치** | `/etc/clientlibs/fd/expeditor` |
|---|---|
| **새 위치** | `/libs/fd/expeditor/clientlibs` |
| **구조 조정 지침** | 절대 경로로 참조할 수 있는 클라이언트 라이브러리의 리소스를 보려면 새 자산에 새 경로를 사용해야 합니다. |
| **메모** | N/A |

| **이전 위치** | `/etc/clientlibs/fd/fmaddon` |
|---|---|
| **새 위치** | `/libs/fd/fmaddon` |
| **구조 조정 지침** | 이러한 clientlibs 변경은 권장 또는 지원되지 않았습니다. 이러한 clientlibs를 수정한 경우 AEM 제공 코드를 사용하기 위해 롤백해야 합니다. |
| **메모** | N/A |

| **이전 위치** | `/etc/aep` |
|---|---|
| **새 위치** | `/var/fd/content/annotations` |
| **구조 조정 지침** | 이러한 clientlibs 변경은 권장 또는 지원되지 않았습니다. 이러한 clientlibs를 수정한 경우 AEM 제공 코드를 사용하기 위해 롤백해야 합니다. |
| **메모** | N/A |

## 업그레이드 전 {#prior-to-upgrade}

### Echosign 클라우드 서비스 구성 {#echosign-cloud-service-configuration}

| **이전 위치** | `/etc/cloudservices/echosign` |
|---|---|
| **새 위치** | `/conf/<tenant>/settings/cloudconfigs/echosign` |
| **구조 조정 지침** | 양식 [마이그레이션](/help/sites-deploying/lazy-content-migration.md) UI에서 트리거되는 레이지 컨텐츠 마이그레이션 유틸리티 |
| **메모** | N/A |

### Recaptcha Cloud 서비스 구성 {#recaptcha-cloud-service-configurations}

| **이전 위치** | `/etc/cloudservices/recaptcha` |
|---|---|
| **새 위치** | `/conf/<tenant>/settings/cloudconfigs/recaptcha` |
| **구조 조정 지침** | 양식 [마이그레이션](/help/sites-deploying/lazy-content-migration.md) UI에서 트리거되는 레이지 컨텐츠 마이그레이션 유틸리티 |
| **메모** | N/A |

### Typekit 클라우드 서비스 구성 {#typekit-cloud-service-configurations}

| **이전 위치** | `/etc/cloudservices/typekit` |
|---|---|
| **새 위치** | `/conf/<tenant>/settings/cloudconfigs/typekit` |
| **구조 조정 지침** | 양식 [마이그레이션](/help/sites-deploying/lazy-content-migration.md) UI에서 트리거되는 레이지 컨텐츠 마이그레이션 유틸리티 |
| **메모** | N/A |

### 기타 {#misc-1}

| **이전 위치** | `/etc/cloudservices/fdm` |
|---|---|
| **새 위치** | `/conf/<tenant>/settings/cloudconfigs/fdm` |
| **구조 조정 지침** | 양식 [마이그레이션](/help/sites-deploying/lazy-content-migration.md) UI에서 트리거되는 레이지 컨텐츠 마이그레이션 유틸리티 |
| **메모** | N/A |

| **이전 위치** | `/etc/designs/fd/fp` |
|---|---|
| **새 위치** | `/libs/fd/fp` |
| **구조 조정 지침** | /etc 템플릿에 대한 모든 참조는 해당 `/libs` 템플릿을 가리키도록 업데이트해야 합니다. |
| **메모** | N/A |

