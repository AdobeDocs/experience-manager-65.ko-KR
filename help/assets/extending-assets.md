---
title: Adobe Experience Manager Assets 사용자 정의 및 확장
description: 사용자에게 특별히 맞춤화된 인터페이스와 기능 세트를 제공하는 자산 공유 및 자산 편집기를 사용자 정의하고 확장할 수 있는 방법을 알아봅니다.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 2%

---


# Customize and extend Assets {#customizing-and-extending-assets}

자산 편집기는 Adobe Enterprise Manager 웹 사이트 사용자가 저장소에서 디지털 자산을 검색, 확인 및 조작하는 데 사용하는 기본 액세스 포인트입니다.

Adobe Experience Manager Developer에서는 사용자에게 특별히 맞춤화된 인터페이스와 일련의 기능을 제공하여 다양한 방법으로 에셋 편집기를 사용자 정의하고 확장할 수 있습니다.

이 기능의 다음 측면을 사용자 정의하거나 향상시킬 수 있습니다.

* [자산 편집기 확장](asseteditorx.md)
* [자산 검색 확장](searchx.md)
* [미디어 핸들러 및 워크플로우를 사용하여 자산 처리](media-handlers.md)
* [활동 스트림과 자산 통합](extending-activity-stream.md)
* [자산 프록시 개발](proxy.md)
* [ImageMagick 구성 우수 사례](best-practices-for-imagemagick.md)

## 모양 사용자 정의 {#customizing-the-look-and-feel}

자산 편집기의 다음과 같은 모양 및 느낌을 사용자 정의할 수 있습니다.

* 로고: 인터페이스에 조직의 로고를 추가할 수 있습니다.
* 색상 및 글꼴: 인터페이스에 사용된 색상과 글꼴을 변경할 수 있습니다.
* HTML 코드: 보다 정확한 사용자 지정을 위해 인터페이스를 정의하는 기본 HTML 코드를 변경할 수 있습니다.

## 변환 사용자 정의 {#customizing-renditions}

Adobe Experience Manager Assets 용어에서는 변환이 자산이 표시되는 양식입니다. 일반적으로 특정 자산에 여러 표현물이 있을 수 있습니다. 예를 들어, 전체 색상 이미지에는 원래 크기의 표현물, 축소된 크기의 표현물 및 축소된 회색 음영으로 변환되는 표현물이 있을 수 있습니다.

특정 자산을 사용할 수 있는 변환은 사용자 지정할 수 있으며 새 표현물을 만들 수 있습니다.
