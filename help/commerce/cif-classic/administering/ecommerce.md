---
title: eCommerce 통합 프레임워크
description: AEM eCommerce는 마케터가 웹, 모바일 및 소셜 터치포인트 전반에서 브랜딩되고 개인화된 쇼핑 경험을 제공할 수 있도록 지원합니다.
topic-tags: e-commerce
content-type: reference
docset: aem65
exl-id: d995f0d6-9e48-4228-ac82-f33a0b25b9d3
solution: Experience Manager,Commerce
source-git-commit: 1751bfb32386685e3a159939113b9667b5e17f0e
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 2%

---

# eCommerce{#ecommerce}

* [개념](/help/commerce/cif-classic/administering/concepts.md)
* [관리(일반)](/help/commerce/cif-classic/administering/generic.md)

Adobe은 두 가지 버전의 Commerce integration framework을 제공합니다.

<table>
 <tbody>
  <tr>
   <th><p> </p> </th>
   <th><p>CIF 온-프레미스</p> </th>
   <th><p>CIF Cloud</p> </th>
  </tr>
  <tr>
   <td><p>지원되는 AEM 버전</p> </td>
   <td><p>AEM 온-프레미스 또는 AMS 6.x</p> </td>
   <td>AEM AMS 6.4 및 6.5</td>
  </tr>
  <tr>
   <td><p>백엔드</p> </td>
   <td>
    <ul>
     <li>AEM, Java</li>
     <li>모놀리식 통합, 빌드 전 매핑(템플릿)</li>
     <li>JCR 저장소</li>
    </ul> </td>
   <td>
    <ul>
     <li>Adobe Commerce</li>
     <li>Java 및 JavaScript</li>
     <li>JCR 저장소에 저장된 상거래 데이터 없음</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>프론트엔드</p> </td>
   <td><p>AEM 서버측 렌더링 페이지</p> </td>
   <td>혼합 페이지 애플리케이션(하이브리드 렌더링)</td>
  </tr>
  <tr>
   <td><p>제품 카탈로그</p> </td>
   <td>
    <ul>
     <li>제품 가져오기, 편집기, AEM의 캐싱</li>
     <li>AEM 또는 프록시 페이지가 있는 일반 카탈로그</li>
    </ul> </td>
   <td>
    <ul>
     <li>제품 가져오기 없음</li>
     <li>일반 템플릿</li>
     <li>커넥터를 통한 온디맨드 데이터</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>확장성</p> </td>
   <td>
    <ul>
     <li>최대 몇 백만 개의 제품 지원 가능(사용 사례에 따라 다름)</li>
     <li>Dispatcher에서 캐싱</li>
    </ul> </td>
   <td>
    <ul>
     <li>볼륨 제한 없음</li>
     <li>Dispatcher 또는 CDN에서 캐싱</li>
    </ul> </td>
  </tr>
  <tr>
   <td>표준화된 데이터 모델</td>
   <td>아니요</td>
   <td>예, Adobe Commerce GraphQL 스키마</td>
  </tr>
  <tr>
   <td>사용 가능</td>
   <td><p>예. SAP Commerce Cloud(AEM 6.4 및 Hybris 5(기본값)를 지원하도록 업데이트되었으며 Hybris 4와의 호환성을 유지합니다.</p> <p>Salesforce Commerce Cloud(AEM 6.4를 지원하도록 오픈 소스로 제공되는 커넥터)</p> </td>
   <td>GitHub를 통해 오픈 소스를 통해 지원. Adobe Commerce(2.3.2(기본값)를 지원하고 2.3.1과 호환)</td>
  </tr>
  <tr>
   <td>사용 시기</td>
   <td>제한된 사용 사례: 예를 들어 작은 정적 카탈로그를 가져와야 하는 시나리오가 이에 해당합니다</td>
   <td>대부분의 사용 사례에서 선호하는 솔루션</td>
  </tr>
 </tbody>
</table>

eCommerce는 제품 정보 관리(PIM)와 함께 온라인 스토어를 통해 제품을 판매하는 데 중점을 둔 웹 사이트의 활동을 처리합니다.

* 제품의 생성, 수명 및 노후화
* 가격 관리
* 거래 관리
* 전체 카탈로그 관리
* 라이브 및 중앙 집중식 스토리지 레코드
* 웹 인터페이스

AEM eCommerce는 마케터가 웹, 모바일 및 소셜 터치포인트 전반에서 브랜딩되고 개인화된 쇼핑 경험을 제공할 수 있도록 지원합니다. AEM 작성 환경에서는 타겟 방문자 컨텍스트 및 머천다이징 전략에 따라 페이지 및 구성 요소를 사용자 지정할 수 있습니다. 예를 들면 다음과 같습니다.

* 제품 페이지
* 장바구니 구성 요소
* 구성 요소 체크아웃

구현을 통해 제품 정보에 실시간으로 액세스할 수 있습니다. 이를 사용하여 다음을 적용할 수 있습니다.

* 제품 정보 무결성
* 가격 책정
* 재고 관리 재고
* 장바구니 상태의 변형

>[!NOTE]
>
>외부 전자 상거래 공급자와 통합 프레임워크를 사용하려면 먼저 필요한 패키지를 설치해야 합니다. 자세한 내용은 [전자 상거래 배포](/help/commerce/cif-classic/deploying/ecommerce.md).
>
>전자 상거래 기능 확장에 대한 자세한 내용은 [eCommerce 개발](/help/commerce/cif-classic/developing/ecommerce.md).

## 주요 기능 {#main-features}

AEM eCommerce는 다음을 제공합니다.

* 숫자 **기본 AEM 구성 요소** 프로젝트에 대해 달성할 수 있는 사항을 보여 주는 방법:

   * 제품 표시
   * 장바구니
   * 체크아웃
   * 최근에 본 제품
   * 바우처
   * 외

  ![geometrixx 구성 요소 예제](/help/sites-administering/assets/chlimage_1-130.png)

  >[!NOTE]
  >
  >AEM에서 제공하는 통합 프레임워크를 사용하면 특정 eCommerce 엔진과 관계없이 상거래 기능을 위한 추가 AEM 구성 요소를 빌드할 수도 있습니다.

* **검색** - 다음 중 하나를 사용합니다.

   * AEM 검색
   * eCommerce 시스템 검색
   * 서드파티 검색
   * 또는 둘의 조합.

  ![검색 예](/help/sites-administering/assets/chlimage_1-131.png)

* AEM 기능을 사용하여 다음을 수행합니다 **여러 채널에서 콘텐츠 제공**, 전체 브라우저 창 또는 모바일 디바이스이어야 합니다. 방문자가 필요로 하는 형식으로 콘텐츠를 제공합니다.

  ![모바일 보기 예](/help/sites-administering/assets/chlimage_1-132.png)

* 다음에 대한 기능: **를 기반으로 자체 통합 구현 개발 [AEM eCommerce 프레임워크](#the-framework)**.

  현재 사용할 수 있는 두 구현은 모두 일반 API(프레임워크)를 기반으로 동일한 기반으로 구축됩니다. 새 통합 구현에는 통합에 필요한 기능 구현만 포함됩니다. 프론트엔드 구성 요소는 인터페이스를 사용하기 때문에 새로운 구현에서 사용할 수 있습니다(따라서 구현과 독립적).

* 개발 가능성 **쇼퍼 데이터 및 활동을 기반으로 한 경험 기반 상거래**. 이를 통해 다음과 같은 많은 시나리오를 실현할 수 있습니다.

   * 예를 들어 총 주문이 특정 금액을 초과할 경우 배송 비용을 절감할 수 있습니다.
   * 또 다른 방법에서는 프로필 데이터(예: 위치)를 사용하는 시즌 오퍼를 제공할 수 있습니다. 그런 다음 필요할 때 다른 요인에 따라 다시 강조할 수 있습니다.

  아래 예에는 장바구니의 콘텐츠가 $75 미만인 하나의 티저가 표시됩니다.

  ![클라이언트 컨텍스트가 있는 장바구니](/help/sites-administering/assets/chlimage_1-133.png)

  장바구니의 콘텐츠가 $75를 초과하는 경우 변경할 수 있습니다.

  ![변경 후 클라이언트 컨텍스트가 있는 장바구니](/help/sites-administering/assets/chlimage_1-134.png)

* 및 다음을 포함한 기타 기능:

   * 여러 세션에 걸쳐 유지되는 장바구니 콘텐츠
   * 전체 주문 내역
   * 빠른 카탈로그 업데이트

## 프레임워크 {#the-framework}

다음 [개념](/help/commerce/cif-classic/administering/concepts.md) 이 섹션에서는 프레임워크를 좀 더 자세히 살펴보지만, 다음에서는 프레임워크를 세부적으로 고속으로 볼 수 있습니다.

### 뭐? {#what}

* 통합 프레임워크는 API, 기능을 보여 주는 다양한 구성 요소 및 연결 방법의 예를 제공하는 몇 가지 확장을 제공합니다.
* 프레임워크는 프로젝트 구현에 필요한 기본 구조를 제공합니다.
* 프레임워크는 확장 가능합니다.
* 프레임워크는 즉시 사용 가능한 사이트를 제공하지 않습니다. 사용자 사양에 맞게 프레임워크를 조정하려면 항상 일정한 양의 개발 작업이 필요합니다.

### 왜일까요? {#why}

* 맞춤형 전자 상거래 사이트를 빠르게 구현하는 데 필요한 기본 메커니즘을 제공합니다.
* Tp는 실제 전자 상거래 사이트를 개발하는 데 필요한 유연성을 제공합니다.
* 모범 사례를 보여 줍니다.
