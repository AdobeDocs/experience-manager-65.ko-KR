---
title: 컨텐츠 처리 필터
seo-title: 컨텐츠 처리 필터
description: 컨텐츠 처리 필터를 사용하여 XSS 공격을 방지하는 방법을 알아봅니다.
seo-description: 컨텐츠 처리 필터를 사용하여 XSS 공격을 방지하는 방법을 알아봅니다.
uuid: 145a88e0-9fa8-42db-b189-eda507c33049
contentOwner: trushton
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: Security
discoiquuid: badfaa18-472e-4777-a7dc-9c28441b38b7
translation-type: tm+mt
source-git-commit: bb50e530f0d015c0e7d06650157e3e3994082483
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---


# 내용 처리 필터{#content-disposition-filter}

내용 처리 필터는 SVG 파일에 대한 XSS 공격에 대한 보안 기능입니다.

설치가 완료되면 필터는 모든 자산에 대한 액세스를 차단합니다. 예를 들어 온라인으로 PDF를 볼 수 없습니다. 이 섹션에서는 필요에 따라 필터를 구성하는 방법에 대해 설명합니다.

## 내용 처리 필터 구성 {#configure-content-disposition-filter}

GitHub](https://github.com/apache/sling-org-apache-sling-security/blob/master/src/main/java/org/apache/sling/security/impl/ContentDispositionFilterConfiguration.java)에서 [Apache Sling 내용 처리 필터를 볼 수 있습니다.

컨텐츠 처리 필터 옵션은 다음 기능을 제공합니다.

* 컨텐츠 처리 경로:필터를 적용할 경로 목록 다음에 해당 경로에서 제외할 MIME 유형 목록이 있습니다. 이 경로는 절대 경로여야 하며 끝에 와일드카드(&#39;&amp;ast;&#39;)를 포함할 수 있으므로 지정된 경로 접두어와 모든 리소스 경로를 일치시킬 수 있습니다. 예:/content/&amp;ast;:image/jpeg,image/svg+xml&quot;은 jpg 및 svg 이미지를 제외한 /content의 모든 노드에 필터를 적용합니다.

* 제외된 리소스 경로:제외된 리소스 목록, 각 리소스 경로는 절대 및 정규화된 경로로 지정해야 합니다. 접두사 일치/와일드카드는 지원되지 않습니다.

* 모든 리소스 경로에 대해 활성화:이 플래그는 제외된 리소스 경로에 정의된 제외된 경로를 제외하고 모든 경로에 대해 이 필터를 활성화할지 여부를 제어합니다. 이 옵션을 &#39;true&#39;로 설정하면 컨텐츠 처리 경로가 무시됩니다. 구성에 관계없이 &#39;jcr:data&#39; 또는 &#39;jcr:content/jcr:data&#39; 속성이 포함된 리소스 경로만 포함됩니다.
