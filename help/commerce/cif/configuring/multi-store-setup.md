---
title: 상거래 다중 스토어 설정
description: 여러 스토어 뷰를 Magento에서 AEM에 매핑하는 방법을 살펴봅니다. 이를 통해 프로젝트는 멀티 테넌트 및 다중 언어 사용 사례를 지원할 수 있습니다.
sub-product: 상거래
doc-type: technical-video
activity: setup
audience: administrator
feature: 전자 상거래 통합 프레임워크
kt: 3046
thumbnail: 28952.jpg
translation-type: tm+mt
source-git-commit: d92a635d41cf1b14e109c316bd7264cf7d45a9fe
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 1%

---

# 상거래 다중 스토어 설정 {#multi-store}

AEM CIF 핵심 구성 요소를 여러 AEM 사이트 구조에 사용할 수 있으며 기본 GraphQL 클라이언트 구현은 서로 다른 Magento 스토어/스토어 보기에 연결할 수 있습니다. 이를 통해 복잡한 다중 저장소/다중 사이트 설정을 구현할 수 있습니다.

여러 Magento 스토어 보기를 Adobe Experience Manager Sites과 통합하는 옵션을 자세히 설명하는 비디오 연습.

>[!VIDEO](https://video.tv.adobe.com/v/28952/?quality=12)

Live Copy 및 언어 복사의 AEM 다중 사이트 관리 기능은 Commerce Integration Framework와 함께 사용하여 지역 및 로케일 간에 사이트를 전역적으로 관리합니다.

AEM 사이트와 Magento 스토어 보기 간에 1:1 관계를 사용하는 것이 좋습니다.

AEM 사이트 및 AEM CIF 핵심 구성 요소를 전용 스토어 보기에 연결하려면 아래 단계를 따르십시오.

## 구성 {#configuration}

1. [Magento 웹 사이트, 스토어 및 보기](https://docs.magento.com/m2/ce/user_guide/stores/websites-stores-views.html)에 설명된 패턴에 따라 여러 스토어 및 스토어 보기 구성

2. AEM 및 Magento 간 연결이 작동하는지 확인합니다.

3. 다음 단계에 따라 CIF Cloud Service 구성의 하위 구성을 만듭니다.

   * AEM에서 도구 -> 일반 -> [구성 브라우저](/help/sites-administering/configurations.md#using-configuration-browser)로 이동합니다.
   * 만든 기본 구성을 선택합니다.
   * 위의 2단계에서 설명한 단계를 사용하여 새 구성을 만듭니다.

   이 새 구성은 기본 구성의 하위 구성으로 생성됩니다. 이제 도구 -> 일반 -> 구성 브라우저로 이동하여 구성 설정을 만들 수 있습니다.

   >[!TIP]
   >
   > 상거래 카탈로그는 ID 또는 UID를 사용하여 처리할 수 있습니다. UID가 Magento 2.4.2에 도입되었습니다. 상거래 백엔드가 버전 2.4.2 이상의 GraphQL 스키마를 지원하는 경우에만 이 기능을 활성화합니다.

4. AEM 사이트에 하위 구성 할당

   * AEM Sites 콘솔으로 이동
   * 사이트 구조의 지역 또는 언어 루트로 이동합니다(예:/content/venia/us _또는_ /content/venia/us/en for the venia 샘플 페이지
   * 페이지를 선택하고 페이지 속성을 엽니다.
   * 고급 탭 선택
   * `Configuration` 섹션에서 단계에서 만든 구성을 선택합니다

## 추가 리소스

* [Magento 웹 사이트, 스토어 및 보기](https://docs.magento.com/m2/ce/user_guide/stores/websites-stores-views.html)
* [AEM CIF 핵심 구성 요소 - 멀티 스토어/사이트 구성](https://github.com/adobe/aem-core-cif-components/wiki/configuration#multi-store--site-configuration)
* [다중 사이트 관리자 사용](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/translation/multi-site-manager-feature-video-use.html)
* [컨텐츠 재활용:다중 사이트 관리자 및 Live Copy](/help/sites-administering/msm.md)
