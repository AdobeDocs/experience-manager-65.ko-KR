---
title: 기본 디지털 자산 관리에 Media Library 사용
description: "[!DNL Experience Manager Assets] 및 Media Library for asset management를 참조하십시오."
contentOwner: AG
role: Architect, Leader
feature: Asset Management
exl-id: e10d632d-1d90-4f28-8617-95ee41602997
source-git-commit: 9d5440747428830a3aae732bec47d42375777efd
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 4%

---


# 기본 자산 관리에 Media Library 사용 {#manage-assets-using-media-library}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기를 클릭하십시오.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/medialibrary.html?lang=en) |
| AEM 6.5 | 이 문서 |
| AEM 6.4 | [여기를 클릭하십시오.](https://experienceleague.adobe.com/docs/experience-manager-64/assets/administer/medialibrary.html?lang=ko-KR) |

[!DNL Adobe Experience Manager] platform은 자산을 관리하는 다양한 기능을 제공합니다. Media Library을 사용하면 적은 수의 자산을 리포지토리에 업로드하고, 웹 페이지에서 해당 자산을 검색 및 사용하고, 자산에서 간단한 자산 관리 작업을 수행할 수 있습니다.

Media Library은 무료로 제공되는 경량 DAM(디지털 자산 관리) 솔루션입니다 [!DNL Adobe Experience Manager Sites] 라이센스. [!DNL Sites] 는 WCM(웹 컨텐츠 관리) 서비스입니다. Media Library은 Experience Manager의 모든 기능과 함께 작동합니다.

[!DNL Adobe Experience Manager Assets] 라이센스는 별도로 구입할 수 있습니다. [!DNL Experience Manager Assets] 엔터프라이즈 사용 사례, 메타데이터, 스키마, 검색 및 사용자 인터페이스 및 Media Library이 제공하는 것 이상의 기타 많은 기능을 위한 사용자 지정 기능을 통해 자산을 강력하게 처리할 수 있습니다.

## 라이선스 요구 사항 {#avail-media-library-license}

고객이 [!DNL Sites] 라이센스는 Media Library을 사용할 수 있습니다. 의 모든 구성 요소에서 작동합니다 [!DNL Experience Manager].

Media Library은 Sites의 일부로 설치됩니다. 사이트 라이선스 및 설치 외에 추가 라이선스 또는 패키지가 필요하지 않습니다.

## [!DNL Assets] Media Library {#assets-and-media-library}

Experience Manager Assets은 엔터프라이즈급 DAM 기능을 제공합니다. 자산 기능은 [!DNL Experience Manager] 단일 패키지로 만듭니다. 그러나 자산 라이센스를 구매하지 않은 사용자는 고급 DAM 기능을 사용할 수 없습니다. Assets 라이센스가 없는 경우에만 [Media Library 기능](#use-media-library) 사용할 수 있습니다.

의도하지 않은 사용을 방지하려면 [!DNL Assets] 라이센스가 없는 기능을 모두 제거한 다음 [!DNL Assets]-특정 워크플로우, 구성 요소, 분류 체계, 옵션 및 [!DNL Assets] 관리 대상 [!DNL Experience Manager]. 이렇게 하면 사용자가 실수로 [!DNL Assets] 라이센스가 없는 기능입니다.

## Media Library 사용 {#use-media-library}

Media Library은 다음 사용 사례에 대한 기본 DAM 기능을 제공합니다.

* 을 사용하여 만든 웹 페이지 [!DNL Adobe Experience Manager Sites].
* 을 사용하여 만든 적응형 양식 및 통신 [!DNL Adobe Experience Manager Forms].
* 을 사용하여 만든 디지털 화면 경험 [!DNL Adobe Experience Manager Screens].
* [!DNL Assets] 헤드리스 작업을 위한 HTTP REST API.

<!--
 TBD: Remove this after confirmation. May need to merge this list with the list provided by PMs.
* Static renditions

-->

Media Library 기능을 사용하려면 기본값을 사용할 수 있습니다 [!DNL Experience Manager] 사용자 인터페이스. Media Library이 [!DNL Experience Manager Sites] 별도의 인터페이스나 추가 기능을 설치할 필요가 없습니다. 기존 인터페이스를 사용하는 Media Library 사용자는 다음 작업을 수행할 수 있습니다.

* 자산을 구성할 폴더를 만듭니다.
* 에셋 업로드.
* 자산을 게시합니다.
* 자산 편집, 이동 및 복사.
* 자산을 탐색, 필터링 및 검색(유사성 검색 포함).
* 에 값을 추가하고, [!UICONTROL 기본] 자산의 탭 [!UICONTROL 속성] 기본적으로 페이지를 표시합니다.
* 정적 표현물을 추가하고 삭제합니다.
* 폴더, 자산 및 자산 표현물을 다운로드합니다.
* 자산 버전을 만듭니다.
* 자산에 대한 검토 작업을 만들고 수행합니다.
* 자산에 주석 달기.
* 에 자산 추가 [!DNL Sites] Content Finder를 통해 페이지를 표시합니다.
* 사용 [!DNL Content Fragments].
* 에 HTTP REST 및 GraphQL API 사용 [!DNL Content Fragments] 및 참조된 미디어 자산을 사이트 라이센스에서 확인합니다.
* Marketing Cloud 통합.
* 자산 관리 사용자 인터페이스를 사용자 지정하고 확장합니다.
* Query Builder(API)에 액세스하여 검색 기능을 확장합니다.
* 정적 태그를 만듭니다.
* 프로젝트 및 작업을 작성합니다.
* 활동 스트림(타임라인).
* 댓글 및 주석.

<!-- TBD: Define exactly which basic Assets workflow are available for use with Media Library?

As per PM, we must avoid stating such a list, as we don't have a list that makes sense in Cloud Service.
-->

>[!IMPORTANT]
>
>많은 고급 DAM 사용 사례가 [!DNL Experience Manager Assets]. Media Library 라이센스를 사용하면 Media Library을 사용하여 나열된 사용 사례만 충족할 수 있습니다. 사용 사례가 나열되지 않은 경우 Media Library 라이센스에서 사용하지 마십시오. 질문이 있는 경우 Adobe 고객 지원에 문의하십시오.

스마트 태그는 사용할 수 없습니다. [!DNL Asset] 링크, [!DNL Asset] 선택기, 벌크 태그 지정, 자산 워크플로우 수정 또는 표준 [!DNL Adobe Experience Manager] 사용자 인터페이스를 사용하여 [!DNL Assets] 라이센스.

<!-- TBD: Add a CTA - how to contact Adobe for queries. -->

>[!MORELIKETHIS]
>
>* [의 DAM 기능 [!DNL Experience Manager Assets]](https://experienceleague.adobe.com/docs/experience-manager-65/assets/home.html)
>* [[!DNL Experience Manager] 6.5 Managed Services 제품 설명](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html)
>* [[!DNL Experience Manager] 6.5 온-프레미스 제품 설명](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html)

