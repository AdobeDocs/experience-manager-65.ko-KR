---
title: 디지털 자산 구성
description: Experience Manager을 사용하여 디지털 에셋, 이미지, 파일, 폴더 등을 구성합니다.
contentOwner: AG
role: User
feature: Asset Management,Search
exl-id: d6f815b5-e4fc-4f8c-a6c1-9e50035ab9f2
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 2%

---

# 디지털 자산 구성 {#organize-digital-assets}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| Adobe Experience Manager(AEM as a Cloud Service) | [여기 클릭](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/organize-assets.html?lang=ko) |
| AEM 6.5 | 이 문서 |

Microsoft® Office 및 PDF 문서의 모든 디지털 에셋, 메타데이터 및 콘텐츠를 추출하여 검색할 수 있도록 만듭니다. 검색을 통해 에셋을 정교하게 필터링할 수 있으며 적절한 권한을 완전히 준수할 수 있습니다. 메타데이터는 Digital Asset Management의 메타데이터에서 자세히 다룹니다.

[!DNL Experience Manager Assets]은(는) 다양한 콘텐츠 구성 방법을 지원합니다. 폴더를 사용하여 계층적 방식으로 구성하거나 태그 등을 사용하여 비순차적, 임시 방식으로 구성할 수 있습니다. 사용자는 DAM 자산 편집기에서 하위 자산, 렌디션 및 메타데이터가 표시되는 태그를 편집할 수 있습니다.

## 폴더에서 에셋 구성 {#organize-using-folders}

에셋을 구성하는 가장 기본적인 방법은 이러한 에셋을 폴더에 저장하는 것입니다. 로컬 파일 시스템의 폴더에 파일을 구성하는 것과 유사합니다. 폴더를 만들고 관리하는 방법에 대한 자세한 내용은 [자산 관리](manage-assets.md)를 참조하십시오. 파일 및 폴더의 이름 지정 방법, 하위 폴더를 정렬하는 방법 및 이러한 폴더 내의 파일을 처리하는 방법은 이러한 에셋이 처리되는 방식에 상당한 영향을 줄 수 있습니다. 좋은 메타데이터 사례와 함께 일관되고 적절한 파일 및 폴더 이름 지정 전략을 사용하면 디지털 에셋 저장소를 최대한 활용할 수 있습니다.

* 일반적으로 디지털 에셋 저장소는 항상 증가하고 있습니다. 따라서 콘텐츠 생성 주기 초기에 메타데이터 사용, 폴더 구조 및 파일 이름을 공식화하는 것이 중요합니다.
* 폴더만 사용하여 디지털 에셋에 일관된 스토리지 구조를 적용합니다. 이러한 일관성은 프로세스 및 자산 관리에 도움이 됩니다. 예를 들어 다음 유형의 폴더에 배치된 자산은 적절한 [프로필을 사용하여 자산 처리에](processing-profiles.md)하는 데 도움이 될 수 있습니다.

   * **개발 폴더**: 현재 작업 중인 디지털 에셋이 포함되어 있습니다.
   * **클라이언트 폴더**: 클라이언트 또는 프로젝트 이름을 기반으로 하는 디지털 에셋을 포함합니다.
   * **기본 폴더**: 원본, 원본 디지털 자산을 포함합니다.
   * **렌디션 폴더**: 원본 소스 디지털 에셋의 렌디션과 복사본을 포함합니다.
   * **파일 크기 폴더**: 작은 파일, 중간 파일 또는 큰 파일 크기를 기반으로 하는 디지털 에셋을 포함합니다.
   * **준비 폴더**: 웹 사이트에 실시간으로 게시할 준비가 된 디지털 에셋이 포함되어 있습니다.
   * **MIME 형식 폴더**: 이미지, 문서 및 멀티미디어와 같은 MIME 형식에 해당하는 디지털 에셋이 포함되어 있습니다.
   * **보관 폴더**: 사용되지 않는 디지털 자산을 포함합니다.
   * **날짜 기반 폴더**: 만든 날짜 또는 마지막으로 수정한 날짜를 기준으로 디지털 에셋을 포함합니다.

* 사용자 지정 또는 자동화가 계속 작동하도록 변경되지 않는 폴더의 디렉토리를 만듭니다. 예를 들어 할당된 처리 프로필이 계속 작동합니다.
* 자산이 이미 게시되어 있다면 [!DNL Experience Manager]을(를) 사용하여 자산을 다른 폴더로 이동하고 새 위치에서 다시 게시하면 새로 다시 게시된 자산과 함께 원래 게시된 자산 위치를 계속 사용할 수 있습니다. 그러나 원래 게시된 자산은 [!DNL Experience Manager]에 대해 *손실됨*&#x200B;이며 게시를 취소할 수 없습니다. 따라서 가장 좋은 방법은 먼저 에셋의 게시를 취소한 다음 다른 폴더로 이동하는 것입니다.

## 태그를 사용하여 에셋 구성 {#use-tags-to-organize-assets}

태그를 메타데이터로 사용하면 쉽게 자산을 검색하고, 검색 결과를 사용하여 컬렉션을 만들고, 일부 자산에 대한 검색 등급을 높이고, 자산 검색에 Adobe Sensei의 인공 지능 알고리즘을 사용할 수 있습니다.

[!DNL Adobe Experience Manager Assets]은(는) 자체 학습 알고리즘을 사용하여 몇 번의 클릭만으로 적합한 자산을 찾을 수 있도록 설명하는 태그를 만듭니다. 스마트 태깅은 Adobe의 인공 지능 및 머신 러닝 프레임워크인 Adobe Sensei을 사용하며, 이를 통해 표준 및 비즈니스별 태그를 모두 인식하고 이미지에 적용하는 교육을 받을 수 있습니다. 스마트 태그는 컨텐츠, 개별 단어 또는 구를 식별하고 설명 태그를 자산에 자동으로 적용할 수도 있습니다

자세한 내용은 다음 문서를 참조하십시오.

* [Experience Manager의 태그 정보](/help/sites-authoring/tags.md)
* [에셋 메타데이터 편집](metadata.md)
* [Assets의 향상된 스마트 태그](enhanced-smart-tags.md)

## 컬렉션으로 구성 {#organize-as-collections}

[!DNL Experience Manager Assets]의 에셋 컬렉션을 사용하면 에셋을 만들고 편집하고 사용자 간에 공유하는 기능을 간소화할 수 있습니다. 에셋, 폴더 및 컬렉션의 정적 참조 목록이 포함된 컬렉션 및 검색 기준에 따라 에셋을 가져오는 컬렉션 등 컬렉션 사용 방법을 기반으로 여러 유형의 컬렉션을 만듭니다. 또한 서로 다른 위치의 에셋으로 컬렉션을 만들고 액세스, 보기 및 편집 권한 수준이 다른 여러 사용자와 공유할 수 있습니다.

자세한 내용은 [컬렉션 관리](manage-collections.md)를 참조하세요.

<!-- TBD items: add screenshots where applicable
Any hints/recommendations of when to use what method of organizing? Some examples of how organizing helps towards a better taxonomy and improved content velocity.
Add back links to blog posts by marketing?
-->

## 프로필을 사용하도록 자산 구성 {#organize-to-use-profiles}

처리 프로필에는 사전 정의된 폴더에 업로드되는 자산에 적용되는 처리 명령 [!DNL Assets]개가 포함되어 있습니다. 프로필은 폴더 또는 새로 업로드한 에셋의 콘텐츠 처리를 자동화하는 데 사용됩니다. 프로필을 사용하여 에셋을 보다 효율적으로 구성할 수 있습니다.

메타데이터 사용, 파일 이름 지정 및 폴더 구조를 표준화하면 디지털 에셋 풀이 증가함에 따라 처리 프로필을 보다 정밀하고 일관성 있게 폴더에 적용할 수 있습니다.

>[!MORELIKETHIS]
>
>* [메타데이터, 이미지 및 비디오를 처리할 프로필](processing-profiles.md).
>* [메타데이터 프로필](/help/assets/metadata-config.md#metadata-profiles).
>* [비디오 프로필](video-profiles.md).
>* [Dynamic Media 이미지 프로필](image-profiles.md).
