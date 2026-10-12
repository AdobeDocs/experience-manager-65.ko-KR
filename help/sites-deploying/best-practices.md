---
title: 배포 모범 사례
description: 가능한 가장 효율적이고 효과적인 방법으로 Adobe Experience Manager(AEM)를 배포하고 유지 관리하는 방법을 알아봅니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 4cbc0a30-d5f6-40ff-b7f6-8d64762e1970
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: 5ef752af-d616-5b23-8312-06964e46b208
    internal-label: Administering
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 22%
---
# 배포 모범 사례{#deploying-best-practices}

배포 모범 사례에서는 가능한 가장 효율적이고 효과적인 방법으로 Adobe Experience Manager(AEM)를 배포하거나 유지 관리하는 방법을 설명합니다. 이렇게 점점 커지는 주제의 목록은 AEM의 다양한 영역을 포함합니다.

다음 영역에는 모범 사례 및 권장 사항의 배포 및 유지에 대한 설명서가 제공됩니다.

* [Oak](#oak)
* [커뮤니티](#communities)
* [UI](#ui)
* [성능](#performance)

관리, 개발 또는 작성에 대한 우수 사례는 다음 중 하나를 참조하십시오.

* [모범 사례 관리](/help/sites-administering/administer-best-practices.md)
* [모범 사례 개발](/help/sites-developing/best-practices.md)
* [모범 사례 작성](/help/sites-authoring/best-practices.md)

특정 문서는 다음에 나오는 표에 설명되어 있고 연결됩니다.

## Oak {#oak}

[Oak](/help/sites-deploying/platform.md)은(는) AEM의 기반이 되는 확장 가능하고 성능이 뛰어난 계층적 콘텐츠 저장소입니다.

<table>
 <tbody>
  <tr>
   <td><p>확장성, 성능 및 재해 복구</p> </td>
   <td><a href="/help/sites-deploying/performance.md">성능 및 확장성</a></td>
   <td>기술 민첩성, 고성능 및 건전한 재해 복구 기능에 대해 설명하는 백서를 제공합니다.</td>
  </tr>
  <tr>
   <td>권장 Oak 배포</td>
   <td><a href="/help/sites-deploying/recommended-deploys.md">권장 배포</a></td>
   <td>배포 시나리오에 대해 설명합니다</td>
  </tr>
  <tr>
   <td>Mongo 토폴로지</td>
   <td><a href="/help/sites-deploying/recommended-deploys.md">Mongo 토폴로지 모범 사례</a></td>
   <td>mongo 토폴로지 - 사용할 토폴로지를 설명합니다.</td>
  </tr>
  <tr>
   <td>데이터 저장소 옵션</td>
   <td><a href="/help/sites-deploying/data-store-config.md">노드 및 데이터 저장소 구성</a></td>
   <td>이 문서에서는 이진 데이터 및 콘텐츠 노드 저장과 관련된 모범 사례에 대해 설명합니다. Amazon S3 데이터 저장소 사용에 대한 정보를 포함합니다.</td>
  </tr>
  <tr>
   <td>Oak에서 검색</td>
   <td><a href="/help/sites-deploying/best-practices-for-queries-and-indexing.md">쿼리 및 색인화 모범 사례</a><br /> </td>
   <td>콘텐츠를 색인화하는 방법에 대한 모범 사례를 설명합니다.</td>
  </tr>
 </tbody>
</table>

## 커뮤니티 {#communities}

AEM Communities을 사용하면 On-Premise 커뮤니티를 간편하게 만들고 관리할 수 있습니다. AEM Communities에 대한 우수 사례는 여기에 설명되어 있습니다.

[커뮤니티 콘텐츠 저장소](/help/communities/working-with-srp.md) - 사용자 생성 콘텐츠(UGC)에 대한 새 공유 저장소 기능과 기본 [토폴로지](/help/communities/topologies.md)를 선택할 때 고려할 사항에 대해 설명합니다.

[커뮤니티에 대한 권장 배포](/help/sites-deploying/recommended-deploys.md#considerations-for-aem-communities) - 커뮤니티에 대한 권장 배포를 설명합니다. |

## UI {#ui}

사용자 인터페이스에 대한 우수 사례는 다음과 같습니다.

[고객을 위한 사용자 인터페이스 권장 사항](/help/sites-deploying/ui-recommendations.md)

AEM에는 현재 동일한 릴리스에 클래식 및 터치에 적합한 UI의 두 가지 UI가 있습니다. 따라서 고객은 프로젝트 구현 중에 사용할 항목을 결정해야 합니다. 이 문서는 올바른 선택을 찾는 데 도움을 주기 위한 것입니다.

## 성능 {#performance}

성능에 대한 우수 사례는 다음과 같습니다.

<table>
 <tbody>
  <tr>
   <td>품질 Assurance 우수 사례</td>
   <td><a href="/help/sites-deploying/configuring-performance.md#best-practices-for-quality-assurance">품질 Assurance 우수 사례</a></td>
   <td><em>게시</em> 환경의 성능 테스트를 위해 테스트 개념을 정의하는 것과 관련된 문제에 대한 표준화된 개요입니다. 이는 주로 QA 엔지니어, 프로젝트 관리자 및 시스템 관리자가 관심을 가질 사항입니다.</td>
  </tr>
  <tr>
   <td>콘텐츠 전송 네트워크에 Dispatcher 사용</td>
   <td><a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html#using-dispatcher-with-a-cdn">콘텐츠 전송 네트워크에 Dispatcher 사용</a></td>
   <td>Akamai Edge Delivery 또는 Amazon Cloud Front와 같은 콘텐츠 전송 네트워크(CDN)는 최종 사용자에게 가까운 위치에서 콘텐츠를 제공합니다.</td>
  </tr>
  <tr>
   <td>성능 최적화</td>
   <td><a href="/help/sites-deploying/configuring-performance.md">성능 최적화</a></td>
   <td>중요한 문제 중 하나는 웹 사이트가 방문자 요청에 응답하는 데 걸리는 시간입니다.</td>
  </tr>
  <tr>
   <td>성능 테스트</td>
   <td><a href="/help/sites-deploying/best-practices-for-performance-testing.md">성능 테스트 모범 사례</a></td>
   <td>AEM 배포에서 성능 테스트를 실행하기 위한 모범 사례를 설명합니다.<br /> </td>
  </tr>
 </tbody>
</table>
