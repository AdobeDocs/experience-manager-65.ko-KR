---
title: Commerce 다중 스토어 설정
description: Adobe Commerce에서 AEM으로 여러 스토어 보기를 매핑하는 방법을 알아봅니다. 이를 통해 프로젝트는 다중 임차인 및 다국어 사용 사례를 지원할 수 있습니다.
sub-product: Commerce
doc-type: technical-video
activity: setup
audience: administrator
feature: Commerce Integration Framework
exl-id: 1d4e9b7b-848b-4007-b884-dd48682d62e8
solution: Experience Manager,Commerce
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 2%

---

# Commerce 다중 스토어 설정 {#multi-store}

AEM CIF 핵심 구성 요소는 여러 AEM 사이트 구조에서 사용할 수 있으며 기본 GraphQL 클라이언트 구현은 다양한 Adobe Commerce 스토어/스토어 보기에 연결할 수 있습니다. 이를 통해 프로젝트는 복잡한 다중 스토어/다중 사이트 설정을 구현할 수 있습니다.

여러 Adobe Commerce 스토어 보기를 Adobe Experience Manager Sites과 통합하기 위한 옵션을 자세히 설명하는 비디오 연습입니다.

>[!VIDEO](https://video.tv.adobe.com/v/28952/?quality=12)

라이브 카피 및 언어 사본의 AEM 다중 사이트 관리 기능은 Commerce integration framework과 함께 사용하여 지역 및 로케일에서 사이트를 전역적으로 관리합니다.

권장되는 설정은 AEM 사이트와 Adobe Commerce 스토어 보기 간에 1:1 관계를 사용하는 것입니다.

AEM 사이트 및 AEM CIF 핵심 구성 요소를 전용 스토어 보기에 연결하려면 아래 단계를 따르십시오.

## 구성 {#configuration}

1. 에 설명된 패턴에 따라 여러 스토어 및 스토어 보기를 구성합니다. [Adobe Commerce 웹 사이트, 스토어 및 보기](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html)

2. AEM과 Adobe Commerce 간 연결이 작동하는지 확인합니다.

3. 다음 단계에 따라 CIF Cloud Service 구성의 하위 구성을 만듭니다.

   * AEM에서 도구 > 일반으로 이동합니다. [구성 브라우저](/help/sites-administering/configurations.md#using-configuration-browser)
   * 생성한 기본 구성 선택
   * 위의 지점 2에 설명된 단계를 사용하여 구성을 생성

   이 새 구성은 기본 구성의 하위 구성으로 작성됩니다. 이제 도구 > 일반 > 구성 브라우저로 이동하여 구성 설정을 만들 수 있습니다.

   >[!TIP]
   >
   >Commerce 카탈로그는 ID 또는 UID를 사용하여 해결할 수 있습니다. UID는 Adobe Commerce 2.4.2에서 도입되었습니다. 상거래 백엔드가 버전 2.4.2 이상의 GraphQL 스키마를 지원하는 경우에만 활성화하십시오.

4. AEM 사이트에 하위 구성 할당

   * AEM Sites 콘솔로 이동
   * 사이트 구조의 영역 또는 언어 루트로 이동합니다(예: /content/venia/us). _또는_ /content/venia/us/en(Venia 샘플 페이지)
   * 페이지를 선택하고 페이지 속성을 엽니다
   * 고급 탭을 선택합니다.
   * 다음에서 `Configuration` 섹션에서, 단계에서 생성한 구성을 선택합니다

## 추가 리소스

* [Adobe Commerce 웹 사이트, 스토어 및 보기](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html)
* [AEM CIF 핵심 구성 요소 - 다중 스토어/사이트 구성](https://github.com/adobe/aem-core-cif-components#multi-store--site-configuration)
* [다중 사이트 관리자 사용](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/translation/multi-site-manager-feature-video-use.html)
* [콘텐츠 재사용: 다중 사이트 관리자 및 Live Copy](/help/sites-administering/msm.md)
