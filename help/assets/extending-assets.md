---
title: 사용자 지정 및 확장 [!DNL Assets]
description: 사용자에게 특별히 맞춤화된 인터페이스와 기능 세트를 제공하는 에셋 공유 및 에셋 편집기를 사용자 지정하고 확장할 수 있는 방법을 알아봅니다.
contentOwner: AG
role: Developer
feature: Developer Tools
exl-id: 0271c528-23b0-4a3a-b5e8-5baf6cdeecc7
source-git-commit: 5bdf42d1ce7b2126bfb2670049deec4b6eaedba2
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 2%

---

# 사용자 지정 및 확장 [!DNL Assets] {#customizing-and-extending-assets}

에셋 편집기는 Adobe Enterprise Manager 웹 사이트 사용자가 저장소의 디지털 에셋을 찾고, 보고, 조작하는 데 사용하는 기본 액세스 지점입니다.

(으)로 [!DNL Experience Manager] 개발자는 다양한 방식으로 에셋 편집기를 사용자 정의 및 확장하여 사용자에게 특별히 맞춤화된 인터페이스와 기능 세트를 제공할 수 있습니다.

기능의 다음 측면을 사용자 정의하거나 개선할 수 있습니다.

* [자산 편집기 확장](asseteditorx.md)
* [자산 검색 확장](searchx.md)
* [미디어 핸들러 및 워크플로우를 사용하여 에셋 처리](media-handlers.md)
* [자산과 활동 스트림 통합](extending-activity-stream.md)
* [자산 프록시 개발](proxy.md)
* [ImageMagick 구성 우수 사례](best-practices-for-imagemagick.md)

## 모양 사용자 지정 {#customizing-the-look-and-feel}

에셋 편집기의 모양과 느낌에 대한 다음 측면을 사용자 지정할 수 있습니다.

* 로고: 사용자 조직의 로고를 인터페이스에 추가할 수 있습니다.
* 색상 및 글꼴: 인터페이스에 사용되는 색상 및 글꼴을 변경할 수 있습니다.
* HTML 코드: 보다 철저한 맞춤화를 위해 인터페이스를 정의하는 기본 HTML 코드를 변경할 수 있습니다.

## 렌디션 사용자 지정 {#customizing-renditions}

위치 [!DNL Experience Manager Assets] 용어 렌디션은 에셋이 표시되는 형식입니다. 일반적으로 특정 에셋은 여러 렌디션을 가질 수 있습니다. 예를 들어, 전체 색상 이미지에는 원본 크기의 렌디션 하나와 축소된 크기의 렌디션 하나와 축소되고 회색 음영으로 변환되는 렌디션 하나가 있을 수 있습니다.

특정 에셋을 사용할 수 있는 렌디션은 사용자 정의하고 새 렌디션을 만들 수 있습니다.
