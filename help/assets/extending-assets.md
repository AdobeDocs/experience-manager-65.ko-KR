---
title: 사용자 지정 및 확장 [!DNL Assets]
description: 사용자에게 특별한 맞춤형 인터페이스 및 기능 세트를 제공하는 자산 공유 및 자산 편집기를 사용자 지정하고 확장할 수 있는 방법을 알아봅니다.
contentOwner: AG
role: Developer
feature: 개발자 도구
exl-id: 0271c528-23b0-4a3a-b5e8-5baf6cdeecc7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 3%

---

# [!DNL Assets] {#customizing-and-extending-assets} 사용자 지정 및 확장

자산 편집기는 Adobe Enterprise Manager 웹 사이트의 사용자가 저장소에서 디지털 자산을 찾고 보고 조작하는 데 사용할 수 있는 기본 액세스 지점입니다.

[!DNL Experience Manager] 개발자는 다양한 방법으로 자산 편집기를 사용자 지정하고 확장할 수 있으며, 특히 맞춤형 인터페이스와 기능 세트를 사용하여 사용자를 표시할 수 있습니다.

이 기능의 다음 측면을 사용자 정의하거나 개선할 수 있습니다.

* [자산 편집기 확장](asseteditorx.md)
* [자산 검색 확장](searchx.md)
* [미디어 핸들러 및 워크플로우를 사용하여 자산 처리](media-handlers.md)
* [자산과 활동 스트림 통합](extending-activity-stream.md)
* [자산 프록시 개발](proxy.md)
* [ImageMagick 구성 우수 사례](best-practices-for-imagemagick.md)

## 모양 {#customizing-the-look-and-feel} 사용자 정의

자산 편집기의 모양과 느낌에 대한 다음 측면은 사용자 지정할 수 있습니다.

* 로고:인터페이스에 고유한 조직의 로고를 추가할 수 있습니다.
* 색상 및 글꼴:인터페이스에 사용된 색상과 글꼴을 변경할 수 있습니다.
* HTML 코드:보다 완벽한 사용자 지정을 위해 인터페이스를 정의하는 기본 HTML 코드를 변경할 수 있습니다.

## 표현물 사용자 지정 {#customizing-renditions}

[!DNL Experience Manager Assets] 용어에서 표현물은 자산이 표시되는 양식입니다. 일반적으로 특정 자산에는 여러 표현물이 있을 수 있습니다. 예를 들어, 전체 색상 이미지에는 원래 크기의 렌디션이 하나 있고, 크기가 축소된 표현물과 크기가 조절된 표현물과 회색 음영으로 변환된 표현물이 있을 수 있습니다.

특정 자산에서 사용할 수 있는 표현물은 사용자 지정할 수 있으며 새 표현물을 만들 수 있습니다.
