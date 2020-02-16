---
title: We.Retail에서 글로벌라이제이션 사이트 구조 확인
seo-title: We.Retail에서 글로벌라이제이션 사이트 구조 확인
description: 'null'
seo-description: 'null'
uuid: 5e5a809d-578f-4171-8226-cb65aa995754
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: d674458c-d5f3-4dee-a673-b0777c02ad30
translation-type: tm+mt
source-git-commit: b3e1493811176271ead54bae55b1cd0cf759fe71

---


# We.Retail에서 글로벌라이제이션 사이트 구조 확인{#trying-out-the-globalized-site-structure-in-we-retail}

We.Retail은 국가별 웹 사이트에 실시간으로 복사할 수 있는 언어 마스터를 제공하는 글로벌 사이트 구조로 구축되었습니다. 이 구조 및 내장된 번역 기능을 사용해 볼 수 있도록 모든 것이 기본적으로 설정되어 있습니다.

## 사용해 보기 {#trying-it-out}

1. 전역 탐색 -> **사이트에서 사이트 콘솔을 엽니다**.
1. 열 보기로 전환하고(아직 활성화되지 않은 경우) We.Retail을 선택합니다. 스위스, 미국, 프랑스 등과 함께 Language Masters와 함께 국가 구조의 예를 참조하십시오.

   ![chlimage_1-87](assets/chlimage_1-87a.png)

1. 스위스를 선택하고 해당 국가의 언어에 대한 언어를 확인합니다. 이러한 루트 아래에 아직 콘텐츠가 없습니다.

   ![chlimage_1-88](assets/chlimage_1-88a.png)

1. 목록 보기로 전환하여 해당 국가의 언어 사본이 모두 Live Copy인지 확인합니다.

   ![chlimage_1-89](assets/chlimage_1-89a.png)

1. 열 보기로 돌아가서 언어 마스터를 클릭하고 콘텐츠가 포함된 언어 마스터 루트를 봅니다. 영어에만 컨텐츠가 있습니다.

   We.Retail은 번역된 컨텐츠가 포함되어 있지 않지만, 번역 서비스를 시연할 수 있도록 구조 및 구성이 적용됩니다.

   ![chlimage_1-90](assets/chlimage_1-90a.png)

1. 영어 마스터를 선택한 상태에서 사이트 콘솔에서 **참조** 레일을 열고 언어 **사본을 선택합니다**.

   ![chlimage_1-91](assets/chlimage_1-91.png)

1. 언어 사본 레이블 옆에 있는 **확인란을** 확인하여 모든 언어 사본을 선택합니다. 레일의 **언어 사본** 업데이트 섹션에서 새 번역 프로젝트 **만들기 옵션을**&#x200B;선택합니다. 프로젝트의 이름을 입력하고 [업데이트]를 **클릭합니다**.

   ![chlimage_1-92](assets/chlimage_1-92.png)

1. 각 언어 번역에 대한 프로젝트가 만들어집니다. 탐색 -> **프로젝트에서 볼 수 있습니다**.

   ![chlimage_1-93](assets/chlimage_1-93.png)

1. 번역 프로젝트의 세부 사항을 보려면 독일어를 클릭하십시오. 상태는 초안입니다 ****. Microsoft 번역 서비스로 번역을 시작하려면 번역 작업 머리글 옆에 있는 **V** 화살표를 클릭하고 시작을 **선택합니다**.

   ![chlimage_1-94](assets/chlimage_1-94.png)

1. 번역 프로젝트가 시작됩니다. 번역 작업이라는 카드의 하단에 있는 줄임표를 클릭하여 세부 사항을 확인합니다. 검토 준비 상태가 **있는** 페이지는 번역 서비스에서 이미 번역되었습니다.

   ![chlimage_1-95](assets/chlimage_1-95.png)

1. 목록에서 페이지 중 하나를 선택한 다음 도구 **모음에서** 사이트에서 미리 보기를 선택하면 페이지 편집기에서 번역된 페이지가 열립니다.

   ![chlimage_1-96](assets/chlimage_1-96.png)

>[!NOTE]
>
>이 절차에서는 Microsoft 기계 번역과 내장된 통합을 설명했습니다. AEM [Translation Integration](/help/sites-administering/translation.md)Framework를 사용하여 다양한 표준 번역 서비스와 통합하여 AEM의 번역을 조정할 수 있습니다.

## 추가 정보 {#further-information}

자세한 내용은 작성 문서 다국어 [사이트에 대한 컨텐츠](/help/sites-administering/translation.md) 번역 문서를 참조하십시오.
