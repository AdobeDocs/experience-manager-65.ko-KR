---
title: AEM 6.5의 Forms 저장소 구조 변경
seo-title: AEM 6.5의 Forms 저장소 구조 변경
description: AEM 6.5 for Forms의 새 저장소 구조로 마이그레이션하기 위해 필요한 변경 작업을 수행하는 방법을 알아봅니다.
seo-description: AEM 6.5 for Forms의 새 저장소 구조로 마이그레이션하기 위해 필요한 변경 작업을 수행하는 방법을 알아봅니다.
uuid: e60830d4-23ca-4be9-941a-ee4abe4786a6
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 1ce9a622-5968-407f-a74b-d325a2bff669
feature: 업그레이드
exl-id: d555422e-dc97-4d45-9525-4299d22315e2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 7%

---

# AEM 6.5에서 Forms 저장소 구조 변경{#forms-repository-restructuring-in-aem}

AEM 6.5에서 상위 [저장소 구조 변경 페이지에 설명된 대로 AEM 6.5로 업그레이드하는 고객은 이 페이지에서 AEM Forms 솔루션에 영향을 주는 저장소 변경 사항과 관련된 작업 작업을 평가해야 합니다. ](/help/sites-deploying/repository-restructuring.md) 일부 변경 사항은 AEM 6.5 업그레이드 프로세스 중에 작업 노력이 필요한 반면, 다른 변경 사항은 향후 업그레이드될 때까지 지연될 수 있습니다.

**6.5 업그레이드**

* [Misc](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#misc)

**향후 업그레이드 전**

* [Echosign Cloud Service 구성](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#echosign-cloud-service-configuration)
* [Recaptcha Cloud Service 구성](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#recaptcha-cloud-service-configurations)
* [Typekit Cloud Service 구성](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#typekit-cloud-service-configurations)
* [Misc](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#misc)

## 6.5 업그레이드( {#with-upgrade} 포함)

### Misc {#misc}

| **이전 위치** | `/etc/clientlibs/fd/fp` |
|---|---|
| **새 위치** | `/libs/fd/fp/components` |
| **구조 조정 지침** | 사용자 지정 코드에서 기존 위치에 대한 명시적 참조는 새 위치로 업데이트해야 합니다. |
| **메모** | 이러한 클라이언트 라이브러리는 수정하거나 확장하면 안 됩니다. |

| **이전 위치** | `/etc/clientlibs/fd/rte` |
|---|---|
| **새 위치** | `/libs/fd/rte` |
| **구조 조정 지침** | 절대 경로에서 참조할 수 있는 클라이언트 라이브러리의 리소스는 새 자산에서 최신 경로를 사용해야 합니다. |
| **메모** | N/A |

| **이전 위치** | `/etc/clientlibs/fd/af` |
|---|---|
| **새 위치** | `/libs/fd/af/authoring/clientlibs` |
| **구조 조정 지침** | 절대 경로에서 참조할 수 있는 클라이언트 라이브러리의 리소스는 새 자산에서 최신 경로를 사용해야 합니다. |
| **메모** | 해당 없음 |

| **이전 위치** | `/etc/clientlibs/fd/xfaforms` |
|---|---|
| **새 위치** | `/libs/fd/xfaforms/clientlibs/` |
| **구조 조정 지침** | 절대 경로에서 참조할 수 있는 클라이언트 라이브러리의 리소스는 새 자산에서 최신 경로를 사용해야 합니다. |
| **메모** | 해당 없음 |

| **이전 위치** | `/etc/clientlibs/fd/af` |
|---|---|
| **새 위치** | `/libs/fd/af/runtime/clientlibs` |
| **구조 조정 지침** | 절대 경로에서 참조할 수 있는 클라이언트 라이브러리의 리소스는 새 자산에서 최신 경로를 사용해야 합니다. |
| **메모** | 해당 없음 |

| **이전 위치** | `/etc/clientlibs/fd/af` |
|---|---|
| **새 위치** | `/libs/fd/af/runtime/clientlibs` |
| **구조 조정 지침** | 절대 경로에서 참조할 수 있는 클라이언트 라이브러리의 리소스는 새 자산에서 최신 경로를 사용해야 합니다. |
| **메모** | 해당 없음 |

| **이전 위치** | `/etc/clientlibs/fd/expeditor` |
|---|---|
| **새 위치** | `/libs/fd/expeditor/clientlibs` |
| **구조 조정 지침** | 절대 경로에서 참조할 수 있는 클라이언트 라이브러리의 리소스는 새 자산에서 최신 경로를 사용해야 합니다. |
| **메모** | 해당 없음 |

| **이전 위치** | `/etc/clientlibs/fd/fmaddon` |
|---|---|
| **새 위치** | `/libs/fd/fmaddon` |
| **구조 조정 지침** | 이러한 clientlibs 변경은 권장되거나 지원되지 않습니다. 이러한 clientlibs를 수정한 경우 AEM에서 제공한 코드를 사용하도록 롤백해야 합니다. |
| **메모** | 해당 없음 |

| **이전 위치** | `/etc/aep` |
|---|---|
| **새 위치** | `/var/fd/content/annotations` |
| **구조 조정 지침** | 이러한 clientlibs 변경은 권장되거나 지원되지 않습니다. 이러한 clientlibs를 수정한 경우 AEM에서 제공한 코드를 사용하도록 롤백해야 합니다. |
| **메모** | 해당 없음 |

## 향후 업그레이드 전 {#prior-to-upgrade}

### Echosign Cloud Service 구성 {#echosign-cloud-service-configuration}

| **이전 위치** | `/etc/cloudservices/echosign` |
|---|---|
| **새 위치** | `/conf/<tenant>/settings/cloudconfigs/echosign` |
| **구조 조정 지침** | Forms 마이그레이션 UI에서 트리거될 [레이지 컨텐츠 마이그레이션](/help/sites-deploying/lazy-content-migration.md) 유틸리티입니다. |
| **메모** | 해당 없음 |

### Recaptcha Cloud Service 구성 {#recaptcha-cloud-service-configurations}

| **이전 위치** | `/etc/cloudservices/recaptcha` |
|---|---|
| **새 위치** | `/conf/<tenant>/settings/cloudconfigs/recaptcha` |
| **구조 조정 지침** | Forms 마이그레이션 UI에서 트리거될 [레이지 컨텐츠 마이그레이션](/help/sites-deploying/lazy-content-migration.md) 유틸리티입니다. |
| **메모** | 해당 없음 |

### Typekit Cloud Service 구성 {#typekit-cloud-service-configurations}

| **이전 위치** | `/etc/cloudservices/typekit` |
|---|---|
| **새 위치** | `/conf/<tenant>/settings/cloudconfigs/typekit` |
| **구조 조정 지침** | Forms 마이그레이션 UI에서 트리거될 [레이지 컨텐츠 마이그레이션](/help/sites-deploying/lazy-content-migration.md) 유틸리티입니다. |
| **메모** | 해당 없음 |

### 기타 {#misc-1}

| **이전 위치** | `/etc/cloudservices/fdm` |
|---|---|
| **새 위치** | `/conf/<tenant>/settings/cloudconfigs/fdm` |
| **구조 조정 지침** | Forms 마이그레이션 UI에서 트리거될 [레이지 컨텐츠 마이그레이션](/help/sites-deploying/lazy-content-migration.md) 유틸리티입니다. |
| **메모** | 해당 없음 |

| **이전 위치** | `/etc/designs/fd/fp` |
|---|---|
| **새 위치** | `/libs/fd/fp` |
| **구조 조정 지침** | /etc 템플릿에 대한 모든 참조는 나중에 `/libs` 상대 템플릿을 가리키도록 업데이트해야 합니다. |
| **메모** | 해당 없음 |
