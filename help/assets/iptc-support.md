---
title: IPTC 메타데이터 지원
description: AEM(Adobe Experience Manager) 자산이 Adobe Bridge 및 기타 크리에이티브 앱을 통해 자산에 추가된 IPTC 메타데이터, 크리에이티브 등급 및 키워드를 지원하는 방법을 알아봅니다.
contentOwner: AG
translation-type: tm+mt
source-git-commit: c7d0bcbf39adfc7dfd01742651589efb72959603

---


# IPTC 메타데이터 지원 {#support-for-iptc-metadata}

AEM(Adobe Experience Manager) 자산이 Adobe Bridge 및 기타 크리에이티브 앱을 통해 자산에 추가된 IPTC 메타데이터, 크리에이티브 등급 및 키워드를 지원하는 방법을 알아봅니다.

AEM(Adobe Experience Manager) 자산은 자산을 설명하는 데 널리 사용되는 IPTC 메타데이터 표준을 지원합니다. 이러한 방식으로 AEM Assets는 사진 작가, 크리에이티브 에이전시, 라이브러리, 박물관 등을 비롯한 다양한 당사자 간의 이미지 수락을 향상시켜 줍니다.

자산에 대한 기본 메타데이터 스키마는 이제 IPTC Core 및 IPTC Extension 메타데이터 스키마를 통합하여 포괄적인 메타데이터 속성을 정의하여 사용자가 이미지에 표시된 사람, 위치 및 제품에 대한 정확하고 안정적인 데이터를 추가할 수 있습니다. 또한 이미지 만들기와 관련된 날짜, 이름 및 식별자와 권한 정보를 표현하는 유연한 방법을 지원합니다.

이제 자산의 속성 페이지에는 IPTC 코어 및 IPTC 확장 메타데이터를 편집 가능한 필드에 표시하는 별도의 탭이 포함되어 있습니다.

1. 자산 사용자 인터페이스에서 이미지를 선택합니다.
1. Click **[!UICONTROL Properties]** from the toolbar.
1. IPTC **[!UICONTROL 탭을]** 클릭하여 자산에 대한 IPTC 메타데이터를 봅니다.
1. 필요에 따라 IPTC 메타데이터 속성을 편집합니다.

   ![iptc_tab](assets/keywords-in-iptc-tab.png)

1. IPTC **[!UICONTROL 확장]** 탭을 클릭하여 자산에 대한 IPTC 확장 메타데이터를 봅니다.
1. 필요에 따라 IPTC 확장 메타데이터 속성을 편집합니다.
1. 저장 **[!UICONTROL 및 닫기를]** 클릭하여 변경 내용을 저장합니다.

## 크리에이티브 등급 지원 {#creative-rating-support}

속성 페이지에는 개별 사용자 등급 및 집계 등급을 표시하는 것 외에도 Adobe Bridge 및 기타 Creative Apps를 통해 자산에 할당된 등급이 표시됩니다

이러한 등급은 고급 **[!UICONTROL 탭의 크리에이티브]** 등급 섹션에서 사용할 **[!UICONTROL 수]** 있습니다.

이 등급은 읽기 전용 속성이며 1-5 사이의 범위입니다. 검색 패널에서 크리에이티브 등급을 기준으로 자산을 검색할 수 있습니다.

그러나 이 속성은 현재 사용자가 수행한 사용자 지정 변경 사항과 충돌하지 않도록 색인이 되어 있지 않습니다.

## 키워드 지원 {#keyword-support}

속성 **[!UICONTROL 페이지의 IPTC]** 탭에는 [!UICONTROL Adobe Bridge] 및 기타 Adobe Creative Cloud 앱을 통해 자산에 추가된 키워드도 표시됩니다. 이러한 키워드를 편집하고 IPTC 탭에서 키워드를 더 추가할 수도 **[!UICONTROL 있습니다]** .

![keywords](assets/keywords-in-iptc-tab.png)
