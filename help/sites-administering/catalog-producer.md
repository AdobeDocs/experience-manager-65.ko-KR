---
title: 카탈로그 제작자
seo-title: Catalog Producer
seo-description: Learn how to use Catalog Producer in AEM Assets to generate product catalogs using your digital assets.
uuid: da822d83-8b99-4089-ae1b-11d897d4044e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 90e36522-3af1-4a8a-b044-1c828c52974e
description: 카탈로그 제작자
exl-id: 76a46c62-d47d-4970-8a3a-d56015639548
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '882'
ht-degree: 0%

---

# 카탈로그 제작자{#catalog-producer}

AEM Assets에서 카탈로그 프로듀서를 사용하여 디지털 자산을 사용하여 제품 카탈로그를 생성하는 방법을 알아봅니다.

Adobe Experience Manager (AEM) Assets Catalog Producer를 사용하면 InDesign 애플리케이션에서 가져온 InDesign 템플릿을 사용하여 브랜드 제품에 대한 카탈로그를 만들 수 있습니다. InDesign 템플릿을 가져오려면 먼저 AEM Assets을 InDesign 서버와 통합하십시오.

## InDesign 서버와 통합 {#integrating-with-indesign-server}

통합 프로세스의 일부로, **DAM 자산 업데이트** 워크플로우이며, InDesign과 통합하기 위해 적합합니다. 또한 InDesign 서버의 프록시 작업자를 구성합니다. 자세한 내용은 [AEM Assets과 InDesign Server 통합](/help/assets/indesign.md).

>[!NOTE]
>
>AEM Assets으로 가져오기 전에 InDesign 파일에서 InDesign 템플릿을 생성할 수 있습니다. 자세한 내용은 [파일 및 템플릿 작업](https://helpx.adobe.com/indesign/using/files-templates.html).
>
>InDesign 템플릿의 요소를 XML 태그에 매핑할 수 있습니다. 매핑된 태그는 카탈로그 생성자에서 제품 속성을 템플릿 속성에 매핑할 때 속성으로 표시됩니다. InDesign 파일의 XML 태깅에 대해 알아보려면 [XML에 대한 콘텐츠 태깅](https://helpx.adobe.com/indesign/using/tagging-content-xml.html).

>[!NOTE]
>
>InDesign 파일(.indd)만 템플릿으로 사용됩니다. 확장명이 .indt인 파일은 지원되지 않습니다.

## 카탈로그 만들기 {#creating-a-catalog}

카탈로그 생성자는 PIM(제품 정보 관리) 데이터를 사용하여 제품 속성을 템플릿에 표시된 XML 속성에 매핑합니다. 카탈로그를 만들려면 다음 단계를 수행하십시오.

1. Assets 사용자 인터페이스에서 를 탭/클릭합니다. **AEM 로고**, 및으로 이동합니다. **자산 > 카탈로그**.
1. 에서 **카탈로그** 페이지, 탭/클릭 **만들기** 도구 모음에서 를 선택한 다음 **카탈로그** 참조하십시오.
1. 에서 **카탈로그 만들기** 페이지에서 카탈로그에 대한 이름과 설명(선택 사항)을 입력하고 태그를 지정합니다(있는 경우). 카탈로그에 대한 축소판 이미지를 추가할 수도 있습니다.

   ![create_catalog](assets/create_catalog.png)

1. 탭/클릭 **저장**. 카탈로그가 작성되었음을 알리는 확인 대화 상자가 표시됩니다. 탭/클릭 **완료** 을 클릭하여 대화 상자를 닫습니다.
1. 만든 카탈로그를 열려면 **카탈로그** 페이지.

   >[!NOTE]
   >
   >카탈로그를 열려면 탭하거나 클릭할 수도 있습니다 **열기** 이전 단계에서 언급한 확인 대화 상자에서 다음을 수행합니다.

1. 카탈로그에 페이지를 추가하려면 탭/클릭합니다 **만들기** 도구 모음에서 를 선택한 다음 **새 페이지** 선택 사항입니다.
1. 마법사에서 페이지의 InDesign 템플릿을 선택합니다. 그런 다음 탭/클릭합니다 **다음**.
1. 페이지의 이름과 선택적 설명을 지정합니다. 태그(있는 경우)를 지정합니다.
1. 을 탭/클릭합니다. **만들기** 를 클릭합니다. 그런 다음 탭/클릭합니다 **열기** 클릭합니다. 제품의 속성이 왼쪽 창에 표시됩니다. InDesign 템플릿의 사전 정의된 속성이 오른쪽 창에 나타납니다.
1. 왼쪽 창에서 제품 속성을 InDesign 템플릿 속성으로 드래그하고 해당 속성 간에 매핑을 만듭니다.

   페이지가 실시간으로 표시되는 방식을 보려면 **미리 보기** 오른쪽 창의 탭입니다.

1. 페이지를 더 만들려면 6~9단계를 반복합니다. 다른 제품에 대한 유사한 페이지를 만들려면 페이지를 선택하고 **유사한 페이지 만들기** 아이콘 을 클릭하여 제품에서 사용할 수 있습니다.

   ![create_유사_pages](assets/create_similar_pages.png)

   >[!NOTE]
   >
   >구조가 비슷한 제품에 대해서만 유사한 페이지를 만들 수 있습니다.

   추가 아이콘을 탭/클릭하고, 제품 선택기에서 제품을 선택한 다음 탭/클릭합니다 **선택** 를 클릭합니다.

   ![select_product](assets/select_product.png)

1. 도구 모음에서 클릭/탭합니다 **만들기**. 탭/클릭 **완료** 을 클릭하여 대화 상자를 닫습니다. 비슷한 페이지가 카탈로그에 포함됩니다.
1. 기존 InDesign 파일을 카탈로그에 추가하려면 탭/클릭합니다 **만들기** 도구 모음에서 를 선택하고 **기존 페이지에 추가** 선택 사항입니다.
1. InDesign 파일을 선택하고 탭/클릭합니다 **추가** 를 클릭합니다. 그런 다음 탭/클릭합니다 **확인** 을 클릭하여 대화 상자를 닫습니다.

   카탈로그 페이지에서 참조하는 제품의 메타데이터가 변경되면 변경 사항이 카탈로그 페이지에 자동으로 반영되지 않습니다. 레이블이 지정된 배너 **부실** 참조하는 카탈로그 페이지의 제품 이미지에 나타나 참조된 제품에 대한 메타데이터가 최신 상태가 아님을 나타냅니다.

   ![chlimage_1-117](assets/chlimage_1-117a.png)

   제품 이미지가 최신 메타데이터 변경 사항을 반영하도록 하려면 카탈로그 콘솔에서 페이지를 선택하고 **페이지 업데이트** 아이콘 을 클릭하여 제품에서 사용할 수 있습니다.

   ![chlimage_1-118](assets/chlimage_1-118a.png)

   >[!NOTE]
   >
   >참조된 제품의 메타데이터를 변경하려면 제품 콘솔(**AEM 로고** > **상거래** > **제품**)을 클릭하여 제품을 선택합니다. 그런 다음 **속성 보기** 아이콘을 클릭하여 자산의 속성 페이지에서 메타데이터를 편집합니다.

1. 카탈로그에서 페이지를 다시 정렬하려면 **만들기** 아이콘을 클릭한 다음 **병합** 메뉴 아래의 제품에서 사용할 수 있습니다. 마법사에서 맨 위에 있는 회전 메뉴를 사용하여 페이지를 드래그하여 순서를 변경할 수 있습니다. 페이지를 제거할 수도 있습니다.

1. 탭/클릭 **다음**. 기존 InDesign 파일을 커버 페이지로 추가하려면 탭/클릭합니다 **찾아보기** 옆에 **표지 선택** 상자에서 표지 템플릿의 경로를 지정합니다.
1. 탭/클릭 **저장**, 탭/클릭 **완료** 확인 대화 상자를 닫습니다.
선택 시 **완료** 옵션을 선택하면 대화 상자가 열려 .pdf 변환을 사용할지 여부를 선택합니다.
   ![pdf로 내보내기](assets/CatalogPDF.png)
Acrobat(PDF) 옵션을 선택하면  **/jcr:content/renditions** indesign 렌디션 외에 다운로드 대화 상자에서 &quot;표현물&quot; 확인란을 선택하여 모든 표현물을 다운로드할 수 있습니다.

1. 생성한 카탈로그의 미리 보기를 생성하려면 **카탈로그** 콘솔을 클릭한 다음 **미리 보기** 아이콘 을 클릭하여 제품에서 사용할 수 있습니다.

   ![chlimage_1-119](assets/chlimage_1-119a.png)

   미리 보기에서 카탈로그의 페이지를 검토합니다. 탭/클릭 **닫기** 를 클릭하여 미리 보기를 닫습니다.
