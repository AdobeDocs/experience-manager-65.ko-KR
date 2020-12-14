---
title: 앱 콘텐츠 만들기 및 관리
seo-title: 앱 콘텐츠 만들기 및 관리
description: 앱 컨텐츠를 관리하려면 개발자, 컨텐츠 작성자 및 관리자의 공동 노력이 필요합니다.  작성자는 앱 개발자가 생성한 템플릿과 구성 요소를 기반으로 페이지를 조작합니다.
seo-description: 앱 컨텐츠를 관리하려면 개발자, 컨텐츠 작성자 및 관리자의 공동 노력이 필요합니다.  작성자는 앱 개발자가 생성한 템플릿과 구성 요소를 기반으로 페이지를 조작합니다.
uuid: ca049bad-9be8-47aa-b010-298258feda26
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
discoiquuid: 5c8971ab-b07c-4131-b4cb-f34c52425014
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 1%

---


# 앱 콘텐츠 만들기 및 관리{#creating-and-managing-app-content}

>[!NOTE]
>
>단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: 응답)이 필요한 프로젝트에는 SPA 편집기를 사용하는 것이 좋습니다. [추가 정보](/help/sites-developing/spa-overview.md).

앱 콘텐츠를 관리하려면 [개발자](#developer), [작성자](#author) 및 [관리자](#administrator)의 공동 노력이 필요합니다. 작성자는 앱 개발자가 생성한 템플릿과 구성 요소를 기반으로 페이지를 조작합니다.

마지막으로 관리자는 업데이트된 앱 콘텐츠를 전략적으로 게시합니다.

>[!NOTE]
>
>**전제 조건**:
>
>[배포 및 유지 관리](/help/sites-deploying/deploy.md)에서 개발자는 AEM 구성 요소 및 템플릿 시스템에 익숙해졌습니다.

## 페이지 컨텐츠 관리 타일 {#the-manage-page-content-tile}

>[!CAUTION]
>
>기본 앱 템플릿을 사용하지 않는 경우 새 앱 콘텐츠를 OTA로 게시하려면 콘텐츠 동기화 핸들러를 구성해야 합니다.
>
>자세한 내용은 개발자 섹션의 [컨텐트 동기화](/help/mobile/phonegap-contentsync.md)와 모바일을 참조하십시오.

AEM Sites 에서와 동일한 방식으로 AEM Mobile에서 컨텐츠를 제작, 편집 및 삭제할 수 있습니다.

**페이지 컨텐츠 관리 타일**&#x200B;에는 특정 페이로드에 대해 관리되는 컨텐츠 및 마지막으로 수정한 페이지의 수가 표시됩니다. 타일의 각 레코드를 클릭하여 컨텐츠를 드릴다운하여 페이지를 생성, 복사, 이동, 삭제 및 업데이트할 수 있습니다.

컨텐츠가 업데이트되면 관리자는 **컨텐츠 패키지 관리 타일**&#x200B;을 통해 컨텐츠 업데이트 페이로드 OTA(Over-the-Air)를 고객에게 게시할 수 있습니다.

![chlimage_1-161](assets/chlimage_1-161.png)

나열된 컨텐츠 패키지 중 하나를 선택하여 페이지 만들기, 편집 또는 제거, 탐색 및 페이지 순서 변경, 복사(텍스트) 및 미디어와 같은 컨텐츠 만들기 또는 업데이트 등의 컨텐츠를 만들거나 편집합니다.

참고 *모든 것은 컨텐츠*&#x200B;입니다. 즉, 응용 프로그램 스타일, 복사(텍스트), 미디어, 페이지, 탐색 및 컨텐츠 타깃팅을 의미하며, 앱스토어로 이동하지 않고도 OTA를 모두 편집하고 업데이트할 수 있습니다.

AEM Mobile 컨텐츠를 편집하려면 *AEM 작성자 *는 AEM 컨텐츠 편집 인터페이스에 대한 명확한 이해가 필요합니다.[AEM에서 페이지 작성](/help/sites-authoring/qg-page-authoring.md)

## 콘텐츠 패키지 관리 타일 {#the-manage-content-packages-tile}

여기에서 *AEM 관리자*&#x200B;는 앱을 빠르고 쉽게 업데이트하여 매력적인 경험과 최신 컨텐츠를 전달하여 브랜드 참여도를 높이고 비즈니스 목표를 달성할 수 있도록 개발자 또는 앱스토어를 다시 제출할 필요 없이 할 수 있습니다.

![chlimage_1-162](assets/chlimage_1-162.png)

*AEM 작성자*&#x200B;가 컨텐츠 타일 관리를 통해 컨텐츠를 추가하거나 수정했으면 *AEM 관리자*&#x200B;가 컨텐츠 패키지 업데이트를 통해 해당 변경 사항을 고객에게 푸시할 수 있습니다.

컨텐츠 패키지 작업을 사용하면 개발 팀에서 탐색, 스타일, 서버측 논리, 템플릿 및 구성 요소를 포함한 호스트 애플리케이션 디자인 및 구현을 변경하는 동안 *AEM 작성자*&#x200B;가 페이지 컨텐츠를 만들고 편집할 수 있으며 이러한 변경 사항을 배포하기 위해 다양한 스토어에 다시 제출하지 않고도 고객에게 OTA로 푸시할 수 있습니다.

**새 컨텐츠 또는 업데이트된 컨텐츠를 게시하려면**

타일(이 예: 영어 패키지)에서 컨텐츠 패키지를 선택합니다. 콘텐츠 업데이트 대화 상자에 관련 *콘텐츠 동기화* 구성이 나열됩니다. 이전 업데이트 이후 앱 콘텐츠가 수정된 경우, 아래에 표시된 것처럼 상태가 *보류 중*&#x200B;으로 표시됩니다.

![chlimage_1-163](assets/chlimage_1-163.png)

그런 다음 새 내용 업데이트를 만들 오른쪽 상단의 **스테이지** 동작을 선택합니다. 적절한 업데이트 정보를 추가하고 완료를 누릅니다.

![chlimage_1-164](assets/chlimage_1-164.png)

그런 다음 *Content Sync* 핸들러는 델타(*변경된 것만*&#x200B;만 패키지)를 만들어 필요한 패키지를 만듭니다. 완료되면 이 업데이트 콘텐츠 패키지는 아래와 같이 스테이징되었습니다.

컨텐츠 스테이징과 업데이트를 수행하면 OTA를 모바일 장치에 게시하기 전에 몇 가지 업데이트를 수행할 수 있습니다.

>[!NOTE]
>
>게시하기 전에 AEM Verify 앱을 사용하여 단계 컨텐츠를 확인할 수 있습니다.
>
>AEM Verify 앱에 대한 자세한 내용은 [AEM용 모바일 빠른 시작 확인](/help/mobile/phonegap-mobile-quickstart.md)을 참조하십시오.

![chlimage_1-165](assets/chlimage_1-165.png)

콘텐츠 동기화 OTA를 사용하여 앱 사용자에게 새 콘텐츠를 전달할 준비가 되면 아래와 같이 **게시**&#x200B;를 선택합니다.

![chlimage_1-166](assets/chlimage_1-166.png)

### 다음 단계 {#the-next-steps}

응용 프로그램 대시보드에서 앱 콘텐츠 만들기 및 관리에 대해 알게 되면 다른 제작 역할에 대한 다음 리소스를 참조하십시오.

* [앱 관리 타일](/help/mobile/phonegap-app-details-tile.md)
* [앱 메타데이터 편집](/help/mobile/phonegap-editmetadata.md)
* [앱 정의](/help/mobile/phonegap-app-definitions.md)
* [앱 만들기 마법사를 사용하여 새 앱 만들기](/help/mobile/phonegap-create-new-app.md)
* [기존 하이브리드 앱 가져오기](/help/mobile/phonegap-adding-content-to-imported-app.md)

### 추가 리소스 {#additional-resources}

관리자 및 개발자의 역할 및 책임을 살펴보려면 아래 리소스를 참조하십시오.

* [AEM을 사용하여 Adobe PhoneGap Enterprise를 위한 개발](/help/mobile/developing-in-phonegap.md)
* [AEM에서 Adobe PhoneGap Enterprise용 컨텐츠 관리](/help/mobile/administer-phonegap.md)
