---
title: 론치 홍보
description: 게시 전에 콘텐츠를 소스(프로덕션)로 다시 이동하려면 론치 페이지를 홍보해야 합니다. 론치 페이지가 홍보되면 해당 소스 페이지가 홍보된 페이지의 콘텐츠로 바뀝니다.
uuid: 91f1c6ac-8c4e-4459-aaab-feaa32befc45
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 8d38c6f7-8fea-4d27-992d-03b604b9541f
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
exl-id: 3013adc3-bec6-4ecc-aefd-f8df2b86dfef
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 32%

---

# 론치 홍보{#promoting-launches}

게시 전에 콘텐츠를 소스(프로덕션)로 다시 이동하려면 론치 페이지를 홍보해야 합니다. 론치 페이지가 홍보되면 해당 소스 페이지가 홍보된 페이지의 콘텐츠로 바뀝니다. 론치 페이지를 홍보할 때 사용할 수 있는 옵션은 다음과 같습니다.

* 현재 페이지만 홍보할지 전체 론치를 홍보할지 여부입니다.
* 현재 페이지의 하위 페이지를 승격할지 여부입니다.
* 전체 론치를 홍보할지 또는 변경된 페이지만 홍보할지 여부입니다.

## 론치 페이지 홍보 {#promoting-launch-pages}

페이지를 홍보하려면 홍보할 론치 페이지를 편집하면서 다음 단계를 수행하십시오.

1. 다음에서 **페이지** 사이드 킥에서 탭을 클릭하고 **출시 홍보**.
1. 홍보할 페이지 지정:

   * (기본값) 현재 페이지만 승격하려면 **프로덕션 버전에 대한 페이지 변경 사항 홍보**.
   * 현재 페이지의 하위 페이지도 홍보하려면 을 선택합니다. **하위 페이지 포함**.
   * 론치의 모든 페이지를 홍보하려면 **프로덕션 버전에 대한 전체 론치 홍보**.

1. 프로덕션 페이지를 워크플로우 패키지에 추가하려면 다음을 선택합니다. **워크플로우 패키지에 추가** 그런 다음 워크플로우 패키지를 선택합니다.
1. 클릭 **홍보**.

## AEM 워크플로를 사용하여 홍보된 페이지 처리 {#processing-promoted-pages-using-aem-workflow}

워크플로우 모델을 사용하여 판촉된 론치 페이지의 일괄 처리를 수행합니다.

1. 워크플로우 패키지를 만듭니다.
1. 작성자가 Launch 페이지를 홍보하면 워크플로우 패키지에 저장합니다.
1. 패키지를 페이로드로 사용하여 워크플로우 모델을 시작합니다.

페이지가 홍보될 때 워크플로를 자동으로 시작하려면 [워크플로우 런처 구성](/help/sites-administering/workflows-starting.md#workflows-launchers) 패키지 노드의 경우.

예를 들어 작성자가 론치 페이지를 승격하면 페이지 활성화 요청을 자동으로 생성할 수 있습니다. 패키지 노드가 수정되면 활성화 요청 워크플로를 시작하도록 워크플로 시작 관리자를 구성합니다.

![chlimage_1-136](assets/chlimage_1-136.png)
