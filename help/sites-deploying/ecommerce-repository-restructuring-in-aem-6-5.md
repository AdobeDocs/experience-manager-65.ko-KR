---
title: AEM 6.5의 E-Commerce 저장소 재구성
description: AEM 6.5 for E-Commerce에서 새 저장소 구조로 마이그레이션하는 데 필요한 변경 작업을 수행하는 방법에 대해 알아봅니다.
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
feature: Upgrading
exl-id: 78b7c497-c474-4308-bfab-8f424b5f7268
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 1%

---

# AEM 6.5의 E-Commerce 저장소 재구성{#e-commerce-repository-restructuring-in-aem}

AEM 6.5의 상위 [저장소 재구성](/help/sites-deploying/repository-restructuring.md) 페이지에 설명된 대로 AEM 6.5로 업그레이드하는 고객은 이 페이지를 사용하여 AEM E-Commerce 솔루션에 영향을 주는 저장소 변경 사항과 관련된 작업 노력을 평가해야 합니다. 일부 변경 사항은 AEM 6.5 업그레이드 프로세스 중에 작업이 필요하지만, 다른 변경 사항은 향후 업그레이드 전까지 연기될 수 있습니다.

## 6.5 업그레이드 포함 {#with-upgrade}

### 제품, 주문, 컬렉션, 분류, 배송 방법 및 결제 방법 데이터 {#product-order-collections-classifications-shipping-methods-and-payment-methods-data}

<table>
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td><p><code>/etc/commerce/products</code></p> <p><code>/etc/commerce/orders</code></p> <p><code>/etc/commerce/collections</code></p> <p><code>/etc/commerce/classifications</code></p> <p><code>/etc/commerce/shipping-methods</code></p> <p><code>/etc/commerce/payment-methods</code></p> </td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><p><code>/var/commerce/products</code></p> <p><code>/var/commerce/orders</code></p> <p><code>/var/commerce/collections</code></p> <p><code>/var/commerce/classifications</code></p> <p><code>/var/commerce/shipping-methods</code></p> <p><code>/var/commerce/payment-methods</code></p> </td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td><p><a href="/help/sites-deploying/lazy-content-migration.md" target="_blank">지연 마이그레이션</a> 작업을 사용하여 E-Commerce 데이터를 마이그레이션할 수 있습니다.</p> <p>다음 단계를 수행합니다.</p>
    <ul>
     <li>새 위치를 가리키도록 이전 위치에 대한 참조를 조정합니다.</li>
     <li>콘텐츠를 이전 위치에서 새 위치로 이동</li>
     <li>은(는) 이전 위치를 제거하여 결국 전체 시스템에서 새 위치의 사용을 활성화합니다</li>
    </ul> <p>작업이 다루는 위치는 다음과 같습니다.</p>
    <ul>
     <li>/etc/commerce/products</li>
     <li>/etc/commerce/collections<br /> </li>
     <li>/etc/commerce/orders<br /> </li>
     <li>/etc/commerce/payment-methods<br /> </li>
     <li>/etc/commerce/shipping-methods<br /> </li>
    </ul> <p>큰 카탈로그의 경우, Adobe은 다음 Java™ 시스템 속성을 AEM에 전달하여 상거래 마이그레이션 작업을 개별적으로 실행할 것을 권장합니다.</p> <p><code>propertyname: com.adobe.upgrade.forcemigration</code></p> <p><code>property value: com.day.cq.compat.codeupgrade.impl.cq64.CQ64CommerceMigrationTask</code></p> <p>마이그레이션 후 AEM을 다시 시작합니다.</p> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>해당 없음<br /> </td>
  </tr>
 </tbody>
</table>
