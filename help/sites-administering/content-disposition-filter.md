---
title: 콘텐츠 배치 필터
description: 콘텐츠 처리 필터를 사용하여 XSS 공격을 방지하는 방법에 대해 알아봅니다.
contentOwner: trushton
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: Security
exl-id: 1c3d0d48-5c31-42a8-8698-922d7c2127e9
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: b1210526-416b-4ef6-bcc0-1692e99f30e9
    internal-label: Administration and security
subfeature_v2:
  - id: c35bc059-fd80-4a01-91a6-e48da3c76758
    internal-label: Security practices
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 2%
---
# 콘텐츠 배치 필터 {#content-disposition-filter}

컨텐츠 처리 필터는 SVG 파일에 대한 XSS 공격에 대한 보안 기능입니다.

설치 후 필터는 모든 자산에 대한 액세스를 차단합니다. 예를 들어 온라인에서 PDF을 볼 수 없습니다. 이 섹션에서는 필요에 따라 필터를 구성하는 방법에 대해 설명합니다.

## 컨텐츠 처리 필터 구성 {#configure-content-disposition-filter}

GitHub에서 [Apache Sling 콘텐츠 처리 필터](https://github.com/apache/sling-org-apache-sling-security/blob/master/src/main/java/org/apache/sling/security/impl/ContentDispositionFilterConfiguration.java)를 볼 수 있습니다.

컨텐츠 처리 필터 옵션은 다음과 같은 기능을 제공합니다.

* **컨텐츠 처리 경로:** 필터가 적용된 경로 목록 다음에 해당 경로에서 제외할 MIME 유형 목록이 표시됩니다. 이 경로는 절대 경로여야 하며 지정된 경로 접두사와 모든 리소스 경로를 일치시키려면 끝에 와일드카드(`*`)를 포함할 수 있습니다. 예를 들어 `/content/*:image/jpeg,image/svg+xml`은(는) JPG 및 SVG 이미지를 제외한 `/content?`의 모든 노드에 필터를 적용합니다.

* **제외된 리소스 경로:** 제외된 리소스 목록입니다. 각 리소스 경로는 절대 경로 및 정규화된 경로로 제공되어야 합니다. 접두사 일치/와일드카드는 지원되지 않습니다.

* **모든 리소스 경로에 대해 사용:** 이 플래그는 제외된 리소스 경로에 의해 정의된 제외된 경로를 제외한 모든 경로에 대해 이 필터를 사용할지 여부를 제어합니다. 이 플래그를 &#39;true&#39;로 설정하면 콘텐츠 처리 경로가 무시됩니다. 구성과 관계없이 `jcr:data` 또는 `jcr:content/jcr:data` 속성이 포함된 리소스 경로만 포함됩니다.
