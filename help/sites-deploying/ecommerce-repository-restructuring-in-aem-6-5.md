---
title: AEM 6.5의 전자 상거래 저장소 재구성
seo-title: AEM 6.5의 전자 상거래 저장소 재구성
description: 전자 상거래용 AEM 6.5의 새 저장소 구조로 마이그레이션하기 위해 필요한 변경 방법을 알아봅니다.
seo-description: 전자 상거래용 AEM 6.5의 새 저장소 구조로 마이그레이션하기 위해 필요한 변경 방법을 알아봅니다.
uuid: 1fff1a4b-c8d0-4016-92fb-e2ea26e3a302
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 28c92e7d-2106-4333-afa6-c5528a00d7b4
translation-type: tm+mt
source-git-commit: d20ddba254c965e1b0c0fc84a482b7e89d4df5cb

---


# AEM 6.5의 전자 상거래 저장소 재구성{#e-commerce-repository-restructuring-in-aem}

AEM 6.5 [의 상위 리포지토리 재조정](/help/sites-deploying/repository-restructuring.md) 페이지에 설명된 대로, AEM 6.5로 업그레이드하는 고객은 이 페이지를 사용하여 AEM E-Commerce 솔루션에 영향을 주는 리포지토리 변경과 관련된 작업 노력을 평가해야 합니다. 일부 변경 사항은 AEM 6.5 업그레이드 프로세스 동안 작업해야 하는 반면, 다른 변경 사항은 향후 업그레이드될 때까지 연기될 수 있습니다.

## 6.5 업그레이드 포함 {#with-upgrade}

### 제품, 주문, 컬렉션, 분류, 운송 방법 및 지불 방법 데이터 {#product-order-collections-classifications-shipping-methods-and-payment-methods-data}

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
   <td><p>레이지 마이그레이션 <a href="/help/sites-deploying/lazy-content-migration.md" target="_blank">작업을</a> 사용하여 전자 상거래 데이터를 마이그레이션할 수 있습니다.</p> <p>다음 단계를 수행합니다.</p>
    <ul>
     <li>새 위치를 가리키도록 이전 위치에 대한 참조를 조정합니다.</li>
     <li>컨텐츠를 이전 위치에서 새 위치로 이동</li>
     <li>이전 위치를 제거하여 전체 시스템에서 새 위치의 사용을 활성화합니다.</li>
    </ul> <p>작업이 다루는 위치는 다음과 같습니다.</p>
    <ul>
     <li>/etc/commerce/products</li>
     <li>/etc/commerce/collections<br /> </li>
     <li>/etc/commerce/orders<br /> </li>
     <li>/etc/commerce/payment-methods<br /> </li>
     <li>/etc/commerce/shipping-methods<br /> </li>
    </ul> <p>큰 카탈로그의 경우 다음 Java 시스템 속성을 AEM에 전달하여 상거래 마이그레이션 작업을 개별적으로 실행해야 합니다.</p> <p><code>propertyname: com.adobe.upgrade.forcemigration</code></p> <p><code>property value: com.day.cq.compat.codeupgrade.impl.cq64.CQ64CommerceMigrationTask</code></p> <p>마이그레이션 후 AEM을 다시 시작해야 합니다.</p> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

