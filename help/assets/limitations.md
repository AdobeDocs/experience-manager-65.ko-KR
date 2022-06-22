---
title: Dynamic Media 제한 사항
description: '이미지 세트 또는 스핀 세트를 만들거나 PDF을 업로드할 때 모범 사례 및 강제 제한에 대해 알아봅니다. Dynamic Media Viewer용 지원되지 않는 웹 브라우저 및 운영 체제 조합에 대해서도 알아봅니다. '
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/Dynamic-Media-Classic
geptopics: SG_SCENESEVENONDEMAND_PK/categories/ecatalogs
feature: Dynamic Media Classic,Asset Management,Viewers,Image Sets,Spin Sets,eCatalog
role: User
source-git-commit: cd3dcd0232e1ecf69c79b03ab960cfbfc283ee76
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 3%

---

# Dynamic Media 제한 사항

다음 섹션에서는 Dynamic Media의 제한 사항에 대해 설명합니다.

이 주제에는 다음 섹션이 포함됩니다.

* 자산 유형에 대한 Dynamic Media의 우수 사례 및 강제 제한

<!-- * Unsupported web browser and operating system combinations for Dynamic Media Viewers -->

## 자산 유형에 대한 Dynamic Media의 우수 사례 및 강제 제한

스핀 세트 또는 이미지 세트를 만들거나 페이지 추출을 위해 PDF을 업로드할 때 Adobe은 다음 우수 사례를 권장하고 다음 제한을 적용합니다.

| 자산 - 제한 유형 | 우수 사례 | 구현된 제한 | 제한 변경: 2022년 12월 31일 |
| --- | --- | --- | --- |
| **이미지** - 이미지당 스마트 자르기 수 | 5 | 100 |  |
| **이미지 세트** - 세트당 중복 자산 수 | 중복 없음 | 100년 | 20 |
| **이미지 세트** - 세트당 최대 이미지 수 | 세트당 5-10개 이미지 | 1000 |
| **스핀 세트** - 2D 세트당 최대 행/열 수 | 세트당 12-18개 이미지 | 1000년 |
| **PDF** - 추출할 PDF에 대한 최대 페이지 수 |  | 5000(새 업로드의 경우) | 100년 |

<!-- See also [Dynamic Media limitations](/help/assets/limitations.md). -->

<!-- ## Unsupported web browser and operating system combinations for Dynamic Media Viewers

Dynamic Media Viewers do not support following combinations of web browser and operating system.

* Internet Explorer 11 + Windows 7
* Internet Explorer 11 + Windows 8.1
* Internet Explorer 11 + Windows Phone 8.1
* Internet Explorer 11 + Windows Phone 8.1 Update
* Safari 6 + iOS 6.0.1
* Safari 7 + iOS 7.1
* Safari 7 + macOS X 10.9 Mavericks
* Safari 8 + iOS 8.4
* Safari 8 + macOS X 10.10 Yosemite -->