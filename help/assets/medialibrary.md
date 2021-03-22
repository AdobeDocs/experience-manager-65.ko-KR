---
title: 디지털 에셋 관리를 위한 미디어 라이브러리
description: '[!DNL Experience Manager Assets] 에셋 관리를 위한 미디어 라이브러리'
contentOwner: AG
role: 건축가, 리더
translation-type: tm+mt
source-git-commit: 10e5ca2fb6e108a7201e6114b61b3d0266ff80d2
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 0%

---


<!--

Define Media Lib
Define req for it
Define use cases
Define what is not included

-->

# 미디어 라이브러리를 사용하여 기본 에셋 관리 {#manage-assets-using-media-library}

[!DNL Adobe Experience Manager] 플랫폼은 디지털 자산을 관리하는 다양한 기능을 제공합니다. 미디어 라이브러리를 통해 사용자는 적은 수의 자산을 저장소에 업로드하고 웹 페이지에서 해당 에셋을 검색 및 사용하며 자산에서 간단한 에셋 관리 작업을 수행할 수 있습니다.

미디어 라이브러리는 [!DNL Adobe Experience Manager Sites] 라이선스와 함께 무료로 제공되는 경량의 DAM(Digital Asset Management) 솔루션입니다. [!DNL Sites] 는 WCM(Web Content Management) 제품입니다. 미디어 라이브러리는 Experience Manager의 모든 기능과 연동됩니다.

[!DNL Adobe Experience Manager Assets] 라이선스는 별도로 구입할 수 있습니다. [!DNL Experience Manager Assets] 엔터프라이즈 사용 사례, 메타데이터, 스키마, 검색 및 사용자 인터페이스에 대한 사용자 정의 및 미디어 라이브러리에서 제공하는 기능 이외의 다양한 기능을 통해 에셋을 안전하게 처리할 수 있습니다.

## 라이선스 요구 사항 {#avail-media-library-license}

[!DNL Sites] 라이선스를 보유한 고객은 미디어 라이브러리를 사용할 수 있습니다. 이 구성 요소는 [!DNL Experience Manager]의 모든 구성 요소에서 작동합니다.

미디어 라이브러리는 사이트의 일부로 설치됩니다. 사이트 라이선스 및 설치 이외에 추가 라이선스 또는 패키지가 필요하지 않습니다.

## [!DNL Assets] 대 미디어 라이브러리  {#assets-and-media-library}

Experience Manager 자산은 엔터프라이즈급 DAM 기능을 제공합니다. 자산 기능은 하나의 패키지에서 [!DNL Experience Manager]과(와) 함께 제공됩니다. 그러나 자산 라이선스를 구매하지 않은 사용자는 고급 DAM 기능을 사용할 수 없습니다. 에셋 라이선스가 없으면 미디어 라이브러리 DAM 기능만 사용할 수 있습니다.

라이선스가 부여되지 않은 [!DNL Assets] 기능의 의도하지 않은 사용을 방지하려면 [!DNL Experience Manager]에서 [!DNL Assets] 특정 워크플로우, 구성 요소, 분류 체계, 옵션 및 [!DNL Assets] 관리자를 모두 제거하십시오. 이렇게 하면 사용자가 라이선스를 부여하지 않은 [!DNL Assets] 기능을 실수로 사용하지 못하도록 합니다.

## 미디어 라이브러리 사용자가 사용할 수 있는 기능 {#media-library-features}

미디어 라이브러리는 다음과 같은 사용 사례를 광범위하게 다룹니다.

* [!DNL Adobe Experience Manager Sites]을(를) 사용하여 만든 웹 페이지에 대한 기본 DAM 기능을 제공합니다.
* [!DNL Adobe Experience Manager Forms]을(를) 사용하여 만든 적응형 양식 및 통신.
* [!DNL Adobe Experience Manager Screens]을(를) 사용하여 만든 디지털 화면 경험입니다.
* [!DNL Assets] 헤드리스 작업을 위한 HTTP REST API.


<!-- TBD: Remove this after confirmation. May need to merge this list with the list provided by PMs.

* Basic metadata properties
* Tag management
* Version control
* Static renditions
* Projects, tasks, workflow authoring
* Activity stream (timeline)
* Query Builder (API)
* Marketing Cloud integration
* User interface customization and extension
* Comments and annotation
-->

미디어 라이브러리를 사용하여 다음과 같은 특정 작업을 수행할 수 있습니다.

* 폴더를 만들어 자산을 구성합니다.
* 자산을 업로드합니다.
* 자산을 게시합니다.
* 에셋 편집, 이동 및 복사
* 에셋 검색, 필터링 및 검색(유사성 검색 포함)
* 기본적으로 자산의 [!UICONTROL 속성] 페이지의 [!UICONTROL 기본] 탭에서 사용할 수 있는 메타데이터 필드를 추가하고 편집합니다.<!-- excluding Smart Tags -->
* 정적 표현물을 추가하고 삭제합니다.
* 폴더, 자산 및 자산 표현물을 다운로드합니다.
* 자산 버전을 만듭니다.
* 자산에 대한 검토 작업을 만들고 수행합니다.
* 자산에 주석 달기.
* Content Finder를 통해 [!DNL Sites] 페이지에 자산을 추가합니다.
* 사용 [!DNL Content Fragments].

<!-- TBD: Define exactly which basic Assets workflow are available for use with Media Library?
-->

[!DNL Experience Manager Assets] 설명서 홈 페이지에서 살펴볼 수 있는 다른 많은 DAM 사용  [[!DNL Assets] 사례를](https://experienceleague.adobe.com/docs/experience-manager-65/assets/home.html) 실현합니다. 위에 나열되지 않은 사용 사례는 미디어 라이브러리에서 사용할 수 없습니다.

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 6.5 Managed Services 제품 설명](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html)
>* [[!DNL Experience Manager] 6.5 온-프레미스 제품 설명](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html)

