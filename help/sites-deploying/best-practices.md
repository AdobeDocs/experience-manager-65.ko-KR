---
title: 배포 우수 사례
seo-title: Deploying Best Practices
description: 배포 및 유지 관리 우수 사례
seo-description: Deploying and maintaining best practices.
uuid: 4546ed2c-43d5-40f3-874f-567b324e78c2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 4b5c0677-c630-4fae-867e-4f4583ac8507
exl-id: 4cbc0a30-d5f6-40ff-b7f6-8d64762e1970
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 16%

---

# 배포 우수 사례{#deploying-best-practices}

배포 우수 사례에서는 가능한 가장 효율적이고 효과적인 방법으로 AEM을 배포하거나 유지 관리하는 방법을 설명합니다. 계속 증가하고 있는 주제 목록에는 AEM의 다양한 영역이 포함되어 있습니다.

다음 영역에는 우수 사례 및 권장 사항 배포 및 유지 관리에 사용할 수 있는 설명서가 있습니다.

* [OAK](#oak)
* [커뮤니티](#communities)
* [UI](#ui)
* [공연](#performance)

관리, 개발 또는 작성에 대한 우수 사례는 다음 중 하나를 참조하십시오.

* [관리 우수 사례](/help/sites-administering/administer-best-practices.md)
* [개발 우수 사례](/help/sites-developing/best-practices.md)
* [작성 우수 사례](/help/sites-authoring/best-practices.md)

관련된 구체적인 문서에 대한 설명과 링크는 다음 표에 나와 있습니다.

## OAK {#oak}

[Oak](/help/sites-deploying/platform.md) 는 AEM의 기반이 되는 확장 가능하고 성능 계층 컨텐츠 저장소입니다.

<table>
 <tbody>
  <tr>
   <td><p>확장성, 성능 및 재해 복구</p> </td>
   <td><a href="/help/sites-deploying/performance.md">성능 및 확장성</a></td>
   <td>기술 민첩성, 고성능 및 안전한 재해 복구 기능을 설명하는 백서를 제공합니다</td>
  </tr>
  <tr>
   <td>권장 OAK 배포</td>
   <td><a href="/help/sites-deploying/recommended-deploys.md">권장 배포</a></td>
   <td>배포 시나리오에 대해 설명합니다.</td>
  </tr>
  <tr>
   <td>Mongo 토폴로지</td>
   <td><a href="/help/sites-deploying/recommended-deploys.md">Mongo 토폴로지 우수 사례</a></td>
   <td>Mongo 토폴로지 - 어떤 토폴로지를 사용할 시기에 대해 설명합니다.</td>
  </tr>
  <tr>
   <td>데이터 저장소 옵션</td>
   <td><a href="/help/sites-deploying/data-store-config.md">노드 및 데이터 저장소 구성</a></td>
   <td>이 문서에서는 이진 데이터 및 콘텐츠 노드 저장과 관련된 모범 사례를 설명합니다. Amazon S3 데이터 저장소 사용에 대한 정보를 포함합니다.</td>
  </tr>
  <tr>
   <td>OAK에서 검색</td>
   <td><a href="/help/sites-deploying/best-practices-for-queries-and-indexing.md">쿼리 및 색인 생성에 대한 우수 사례</a><br /> </td>
   <td>콘텐츠를 색인화하는 방법에 대한 우수 사례를 설명합니다.</td>
  </tr>
 </tbody>
</table>

## 커뮤니티 {#communities}

AEM Communities은 온-프레미스 커뮤니티의 생성 및 관리를 단순화합니다. AEM Communities에 대한 모범 사례는 다음과 같습니다.

[커뮤니티 콘텐츠 저장소](/help/communities/working-with-srp.md) - 사용자가 생성한 컨텐츠(UGC)를 위한 새로운 공유 스토리지 기능 및 기본 스토리지 선택을 위한 고려 사항에 대해 설명합니다. [토폴로지](/help/communities/topologies.md).

[커뮤니티에 대한 권장 배포](/help/sites-deploying/recommended-deploys.md#considerations-for-aem-communities) - Communities에 대한 권장 배포에 대해 설명합니다. |

## UI {#ui}

사용자 인터페이스에 대한 우수 사례는 다음과 같습니다.

[고객을 위한 사용자 인터페이스 Recommendations](/help/sites-deploying/ui-recommendations.md)

AEM에는 현재 두 개의 UI가 있습니다. 클래식 및 터치에 적합한 UI를 동일한 릴리스에서 사용할 수 있습니다. 따라서 고객은 프로젝트 구현 중에 사용할 항목을 결정해야 합니다. 이 문서는 올바른 선택을 찾는 데 도움이 되기 위한 것입니다.

## 공연 {#performance}

성능 관련 모범 사례는 다음과 같습니다.

<table>
 <tbody>
  <tr>
   <td>품질 보증 우수 사례</td>
   <td><a href="/help/sites-deploying/configuring-performance.md#best-practices-for-quality-assurance">품질 보증 우수 사례</a></td>
   <td>Analytics에서 성능 테스트를 위해 특별히 테스트 개념을 정의하는 것과 관련된 문제에 대한 표준화된 개요입니다. <em>게시</em> 환경. QA 엔지니어, 프로젝트 관리자 및 시스템 관리자에게 주로 관심이 있습니다.</td>
  </tr>
  <tr>
   <td>CDN에 Dispatcher 사용</td>
   <td><a href="https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html#using-dispatcher-with-a-cdn">CDN에 Dispatcher 사용</a></td>
   <td>Akamai Edge Delivery 또는 Amazon Cloud Front와 같은 CDN(콘텐츠 전달 네트워크)은 최종 사용자에게 가까운 위치에서 콘텐츠를 제공합니다.</td>
  </tr>
  <tr>
   <td>성능 최적화</td>
   <td><a href="/help/sites-deploying/configuring-performance.md">성능 최적화</a></td>
   <td>주요 문제는 웹 사이트가 방문자 요청에 응답하는 시간입니다.</td>
  </tr>
  <tr>
   <td>성능 테스트</td>
   <td><a href="/help/sites-deploying/best-practices-for-performance-testing.md">성능 테스트 우수 사례</a></td>
   <td>AEM 배포에서 성능 테스트를 실행하기 위한 우수 사례에 대해 설명합니다.<br /> </td>
  </tr>
 </tbody>
</table>
