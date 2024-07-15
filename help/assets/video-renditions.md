---
title: 비디오 표현물
description: Adobe Experience Manager Assets을 사용하여 OGG, FLV 등을 비롯한 다양한 형식의 비디오 자산에 대한 비디오 렌디션을 생성하는 방법을 알아봅니다.
contentOwner: rbrough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
exl-id: a644558e-5be9-4ba2-b560-fc300497fbdf
solution: Experience Manager, Experience Manager Assets
feature: Video
role: User
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 1%

---

# 비디오 표현물 {#video-renditions}

Adobe Experience Manager Assets은 OGG, FLV 등을 비롯한 다양한 형식의 비디오 자산에 대한 비디오 렌디션을 생성합니다.

Experience Manager Assets은 미디어 자산에 대한 정적 및 동적 변환(DM 인코딩 변환)을 지원합니다.

정적 렌디션은 기본적으로 FFMPEG(시스템 경로에 설치되고 사용 가능)를 사용하여 생성되고 콘텐츠 저장소에 저장됩니다.

DM 인코딩 렌디션은 프록시 서버에 저장되고 런타임 시 제공됩니다.

Experience Manager Assets은 클라이언트측에서 이러한 렌디션에 대한 재생 지원을 제공합니다.

특정 비디오 에셋의 렌디션을 보려면 에셋 페이지를 열고 전역 탐색 아이콘을 선택합니다. 그런 다음 목록에서 **[!UICONTROL 렌디션]**&#x200B;을 선택합니다.

![chlimage_1-478](assets/chlimage_1-478.png)

비디오 렌디션 목록이 **[!UICONTROL 렌디션]** 패널에 표시됩니다.

![chlimage_1-479](assets/chlimage_1-479.png)

DM 인코딩 변환에 대한 프록시 서버를 구성하려면 [Dynamic Media Cloud 서비스를 구성](config-dynamic.md)하십시오.

원하는 매개 변수를 사용하여 비디오 변환을 생성하려면 [해당 비디오 프로필을 만듭니다](video-profiles.md).

프록시 서버를 구성하고 비디오 프로필을 만든 후 이 비디오 사전 설정을 처리 프로필에 포함하고 처리 프로필을 폴더에 적용할 수 있습니다.

>[!NOTE]
>
>Microsoft® Internet Explorer 11의 OGG 및 WAV 파일에 대해 오디오 재생이 작동하지 않습니다. 확장 OGG 또는 WAV가 있는 자산의 자산 세부 정보 페이지에 `Invalid Source` 오류가 표시됩니다.
>
>MS® Edge 및 iPad에서 OGG 파일이 재생되지 않고 지원되지 않는 형식 오류가 발생합니다.
