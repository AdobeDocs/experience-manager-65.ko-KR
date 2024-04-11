---
title: 최적화된 GraphQL 필터링을 위해 콘텐츠 조각 업데이트
description: Headless 콘텐츠 게재를 위해 Adobe Experience Manager에서 최적화된 GraphQL 필터링을 위해 콘텐츠 조각을 업데이트하는 방법을 알아봅니다.
exl-id: d78ec052-c091-49ca-9f36-a3d24eb9edd5
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,GraphQL,Persisted Queries,Developing
role: Admin,Architect,Data Architect,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 49%

---

# 최적화된 GraphQL 필터링을 위해 콘텐츠 조각 업데이트 {#updating-content-fragments-for-optimized-graphql-filtering}

GraphQL 필터의 성능을 최적화하려면 콘텐츠 조각을 업데이트하는 절차를 실행합니다.

>[!NOTE]
>
>콘텐츠 조각을 업데이트한 후에는 [GraphQL 쿼리 최적화](/help/sites-developing/headless/graphql-api/graphql-optimization.md) 권장 사항을 따를 수 있습니다.

## 사전 요구 사항 {#prerequisites}

AEM의 릴리스 6.5.17.0 이상이 있는지 확인하십시오.

## 콘텐츠 조각 업데이트 {#updating-content-fragments}

이 절차를 실행하려면 다음 단계를 사용합니다.

1. [OSGi 설정 구성](/help/sites-deploying/configuring-osgi.md) 대상: **콘텐츠 조각 마이그레이션 작업 구성**:

   ![OSGi 콘텐츠 조각 마이그레이션 작업 구성](assets/cfm-graphql-update-01.png "OSGi 콘텐츠 조각 마이그레이션 작업 구성")

1. 대화 상자에서 다음 두 매개 변수를 다음과 같이 설정합니다.

   * **ContentFragmentMigration:Enabled** : `1`
   * **ContentFragmentMigration:적용** : `1`

1. **저장** 사양 - 업데이트 절차가 시작됩니다.

1. 절차가 완료될 때까지 기다립니다. 속성은 다음과 같습니다. `cfGlobalVersion` 다음에 표시: `/content/dam` 및 가 로 설정되어 있습니다. `1`.

1. 절차를 비활성화하려면 OSGi 구성으로 돌아갑니다.

   대화 상자에서 **콘텐츠 조각 마이그레이션 작업 구성** 이 두 매개 변수를 다음과 같이 설정합니다.

   * **ContentFragmentMigration:Enabled** : `0`
   * **ContentFragmentMigration:적용** : `0`

## 제한 사항 {#limitations}

다음 제한 사항을 알아 두십시오.

* GraphQL 필터의 성능 최적화는 모든 콘텐츠 조각을 완전히 업데이트한 후에만 가능합니다(JCR 노드 `/content/dam`에 `cfGlobalVersion` 속성이 있으면 업데이트가 완료된 것).

* 업데이트 절차를 실행한 후 콘텐츠 패키지에서 콘텐츠 조각을 가져온 경우(`crx/de` 사용) 해당 콘텐츠 조각은 업데이트 절차가 다시 실행될 때까지 GraphQL 쿼리 결과에서 고려되지 않습니다.
