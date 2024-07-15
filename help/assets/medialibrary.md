---
title: 기본 디지털 자산 관리에 Media Library 사용
description: "[!DNL Experience Manager Assets] 및 자산 관리용 Media Library"
contentOwner: AG
role: Architect, Leader
feature: Asset Management
exl-id: e10d632d-1d90-4f28-8617-95ee41602997
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 2%

---


# 기본 에셋 관리에 Media Library 사용 {#manage-assets-using-media-library}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/medialibrary.html?lang=en) |
| AEM 6.5 | 이 문서 |

[!DNL Adobe Experience Manager] 플랫폼은 자산을 관리하는 다양한 기능을 제공합니다. Media Library을 사용하면 저장소에 적은 수의 에셋을 업로드하고, 웹 페이지에서 해당 에셋을 검색 및 사용할 수 있으며, 에셋에 대한 간단한 에셋 관리 작업을 수행할 수 있습니다.

Media Library은 [!DNL Adobe Experience Manager Sites] 라이선스와 함께 무료로 제공되는 간단한 DAM(디지털 에셋 관리) 솔루션입니다. [!DNL Sites]은(는) WCM(웹 콘텐츠 관리) 서비스입니다. Media Library은 Experience Manager의 모든 기능을 사용합니다.

[!DNL Adobe Experience Manager Assets] 라이선스는 별도로 구입할 수 있습니다. [!DNL Experience Manager Assets]을(를) 사용하면 엔터프라이즈 사용 사례, 메타데이터, 스키마, 검색 및 사용자 인터페이스에 대한 사용자 지정 및 Media Library에서 제공하는 기능 이외의 다양한 기능을 통해 자산을 효과적으로 처리할 수 있습니다.

## 라이선스 요구 사항 {#avail-media-library-license}

[!DNL Sites] 라이선스가 있는 고객은 Media Library을 사용할 수 있습니다. [!DNL Experience Manager]의 모든 구성 요소에서 작동합니다.

Media Library은 Sites의 일부로 설치됩니다. Sites 라이센스 및 설치 이외에는 추가 라이센스 또는 패키지가 필요하지 않습니다.

## [!DNL Assets] 및 Media Library {#assets-and-media-library}

Experience Manager Assets은 엔터프라이즈급 DAM 기능을 제공합니다. Assets 기능은 단일 패키지로 [!DNL Experience Manager]과(와) 함께 제공됩니다. 그러나 Assets 라이선스를 구입하지 않은 사용자는 고급 DAM 기능을 사용할 자격이 없습니다. Assets 라이선스가 없으면 [Media Library 기능](#use-media-library)만 사용할 수 있습니다.

라이선스가 부여되지 않은 [!DNL Assets] 기능을 의도하지 않게 사용하지 않도록 하려면 [!DNL Experience Manager]에서 모든 [!DNL Assets]별 워크플로, 구성 요소, 분류, 옵션 및 [!DNL Assets] 관리자를 제거하십시오. 이렇게 하면 사용자가 라이선스를 부여하지 않은 [!DNL Assets] 기능을 실수로 사용하지 않도록 방지합니다.

## Media Library 사용 {#use-media-library}

Media Library은 다음과 같은 사용 사례에 대한 기본 DAM 기능을 제공합니다.

* [!DNL Adobe Experience Manager Sites]을(를) 사용하여 만든 웹 페이지입니다.
* [!DNL Adobe Experience Manager Forms]을(를) 사용하여 만든 적응형 양식 및 통신입니다.
* [!DNL Adobe Experience Manager Screens]을(를) 사용하여 만든 디지털 화면 경험입니다.
* Headless 작업용 HTTP REST API [!DNL Assets]개.

<!--
 TBD: Remove this after confirmation. May need to merge this list with the list provided by PMs.
* Static renditions

-->

Media Library 기능을 사용하려면 기본 [!DNL Experience Manager] 사용자 인터페이스를 사용합니다. Media Library은 [!DNL Experience Manager Sites] 설치의 일부이며 별도의 인터페이스나 추가 기능이 필요하지 않습니다. 기존 인터페이스를 사용하여 Media Library 사용자는 다음 작업을 수행할 수 있습니다.

* 폴더를 만들어 자산을 구성합니다.
* 에셋을 업로드합니다.
* Publish 에셋.
* 에셋을 편집하고, 이동하고, 복사합니다.
* 에셋을 검색, 필터링 및 검색(유사성 검색 포함)합니다.
* 메타데이터 필드(스마트 태그 필드 제외)에 값을 추가하고 편집하십시오. 이 값은 기본적으로 자산의 [!UICONTROL 속성] 페이지의 [!UICONTROL 기본] 탭에서 사용할 수 있습니다.
* 정적 렌디션을 추가 및 삭제합니다.
* 폴더, 에셋 및 에셋 렌디션을 다운로드합니다.
* 에셋 버전을 만듭니다.
* 에셋에 대한 검토 작업을 만들고 수행합니다.
* 에셋에 주석을 답니다.
* 콘텐츠 파인더를 통해 [!DNL Sites] 페이지에 자산을 추가합니다.
* [!DNL Content Fragments] 사용.
* Sites 라이선스에서 [!DNL Content Fragments] 및 참조된 미디어 자산에 대한 HTTP REST 및 GraphQL API를 사용합니다.
* Marketing Cloud 통합.
* 자산 관리 사용자 인터페이스를 사용자 정의하고 확장합니다.
* Query Builder(API)에 액세스하여 검색 기능을 확장합니다.
* 정적 태그를 만듭니다.
* 프로젝트 및 작업 작성
* 활동 스트림(타임라인).
* 주석 및 주석.

<!-- TBD: Define exactly which basic Assets workflow are available for use with Media Library?

As per PM, we must avoid stating such a list, as we do not have a list that makes sense in Cloud Service.
-->

>[!IMPORTANT]
>
>[!DNL Experience Manager Assets]은(는) 많은 고급 DAM 사용 사례를 충족합니다. Media Library 라이선스는 Media Library을 사용하여 나열된 사용 사례만 이행할 수 있는 권한을 부여합니다. 사용 사례가 나열되지 않으면 Media Library 라이선스와 함께 사용하지 마십시오. 질문이 있는 경우 Adobe 고객 지원 센터에 문의하십시오.

[!DNL Assets] 라이선스 없이 Media Library에 액세스하려면 스마트 태그, [!DNL Asset] 링크, [!DNL Asset] 선택기, 일괄 태그 지정, 자산 워크플로 수정 또는 표준 [!DNL Adobe Experience Manager] 사용자 인터페이스를 사용할 수 없습니다.

<!-- TBD: Add a CTA - how to contact Adobe for queries. -->

>[!MORELIKETHIS]
>
>* [DAM 기능 [!DNL Experience Manager Assets]](https://experienceleague.adobe.com/docs/experience-manager-65/assets/home.html)
>* [[!DNL Experience Manager] 6.5 Managed Services 제품 설명](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html)
>* [[!DNL Experience Manager] 6.5 온-프레미스 제품 설명](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html)
