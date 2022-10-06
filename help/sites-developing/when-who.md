---
title: 테스트 - 언제 누구와 함께?
seo-title: Testing - when and with whom?
description: 다양한 역할이 테스트 및 프로젝트 개발 단계에 포함될 수 있습니다
seo-description: Various roles can be involved in testing and at various stages of project development
uuid: 431e8f06-80eb-4fb3-a4c7-2580608b0a1c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: 6148f8e6-ab62-4eb8-8a2d-c431b8318000
exl-id: 5a16be40-eede-4a47-b03b-3993e285232e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 4%

---

# 테스트 - 언제 누구와 함께?{#testing-when-and-with-whom}

다양한 역할이 테스트 및 프로젝트 개발 단계에 포함될 수 있습니다.

<table>
 <tbody>
  <tr>
   <td>테스트 팀</td>
   <td>책임... </td>
   <td>http 화이트보드...</td>
  </tr>
  <tr>
   <td>개발 팀</td>
   <td>개발 팀은 단위 테스트 및 일부 통합 테스트를 수행합니다.</td>
   <td>이러한 테스트는 개발 중에 반복되거나 연장될 것이지만, 체인에서 먼저 수행됩니다.</td>
  </tr>
  <tr>
   <td>품질 보증 팀</td>
   <td><p>기능 및 성능 테스트를 위해서는 품질 보증 팀(적절한 크기)이 필요합니다.</p> <p>이러한 테스터는 중립적이고 전용 테스터이며, 소프트웨어의 황금률은 항상 개발자가 자신의 작업을 테스트해서는 안 된다고 명시합니다.</p> <p>이 팀의 구성원은 Day 프로젝트 팀, 파트너 및/또는 고객 팀에서 인선될 수 있습니다.</p> </td>
   <td><p>첫 번째 기능 릴리스는 테스터가 사용할 수 있도록 해야 합니다(가능한 한 빨리). 초기 중간 릴리스는 많은 버그를 생성할 수 있지만 중요한 문제에 대한 조기 피드백을 제공할 수 있습니다.</p> </td>
  </tr>
  <tr>
   <td>고객 테스트 팀</td>
   <td><p>선택한 프로젝트 모델에 따라 고객 팀의 구성원이 테스트와 관련된 계획(특히 고객 사이트의 작성자)이 될 수 있습니다.</p> <p>는 다음과 같은 이점을 제공합니다.</p>
    <ul>
     <li><p>개발 중인 프로젝트의 경험을 고객에게 제공합니다.</p> </li>
     <li><p>고객으로부터 조기 피드백을 제공합니다.</p> </li>
     <li><p>사용자는 과거 경험에 비추어 자신의 요구 사항을 종종 표현합니다. 고객이 가능한 한 빨리 테스트하면 <i>직접 사용</i> 경험으로 제어됩니다.</p> </li>
    </ul> </td>
   <td><p>고객이 사용하는 모든 릴리스는 안정적이고 합리적인 기능이 있어야 하지만 초기 참여가 좋습니다.</p> <p>첫인상은 항상 중요하다.</p> </td>
  </tr>
 </tbody>
</table>
