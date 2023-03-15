---
title: 비디오 표현물
description: 비디오 표현물
uuid: a02f9ec1-30d9-4cbb-8746-8391ac614f0a
contentOwner: rbrough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: 1601b473-7227-4a56-bb7c-289de2987e4b
exl-id: a644558e-5be9-4ba2-b560-fc300497fbdf
source-git-commit: 77687a0674b939460bd34011ee1b94bd4db50ba4
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 3%

---

# 비디오 표현물 {#video-renditions}

Adobe Experience Manager Assets는 OGG, FLV 등을 비롯한 다양한 형식의 비디오 자산에 대한 비디오 렌디션을 생성합니다.

Experience Manager Assets은 미디어 자산에 대한 정적 및 동적 변환(DM 인코딩 변환)을 지원합니다.

정적 렌디션은 기본적으로 FFMPEG(시스템 경로에 설치되고 사용 가능)를 사용하여 생성되고 콘텐츠 저장소에 저장됩니다.

DM 인코딩 렌디션은 프록시 서버에 저장되고 런타임 시 제공됩니다.

Experience Manager Assets은 클라이언트측에서 이러한 렌디션에 대한 재생 지원을 제공합니다.

특정 비디오 에셋의 렌디션을 보려면 에셋 페이지를 열고 전역 탐색 아이콘을 선택합니다. 그런 다음 을(를) 선택합니다 **[!UICONTROL 표현물]** 목록에서 삭제할 수 있습니다.

![chlimage_1-478](assets/chlimage_1-478.png)

비디오 렌디션 목록은 **[!UICONTROL 표현물]** 패널.

![chlimage_1-479](assets/chlimage_1-479.png)

DM 인코딩 표현물에 대해 프록시 서버를 구성하려면 다음을 수행합니다. [Dynamic Media 클라우드 서비스 구성](config-dynamic.md).

원하는 매개 변수를 사용하여 비디오 렌디션을 생성하려면 다음을 수행하십시오. [해당 비디오 프로필 만들기](video-profiles.md).

프록시 서버를 구성하고 비디오 프로필을 만든 후 이 비디오 사전 설정을 처리 프로필에 포함하고 처리 프로필을 폴더에 적용할 수 있습니다.

>[!NOTE]
>
>Microsoft® Internet Explorer 11의 OGG 및 WAV 파일에 대해 오디오 재생이 작동하지 않습니다. 오류 `Invalid Source` 확장이 OGG 또는 WAV인 에셋의 에셋 세부 사항 페이지에 표시됩니다.
>
>MS® Edge 및 iPad에서 OGG 파일이 재생되지 않고 지원되지 않는 형식 오류가 발생합니다.
