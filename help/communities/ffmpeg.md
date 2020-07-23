---
title: 커뮤니티용 FFmpeg
seo-title: 커뮤니티용 FFmpeg
description: 커뮤니티용 FFmpeg 설치 및 구성 방법
seo-description: 커뮤니티용 FFmpeg 설치 및 구성 방법
uuid: ef2f821c-70e9-4889-a8d7-a93b10a1d428
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 739ec991-552b-42cd-85cd-984d1c9fe8fd
translation-type: tm+mt
source-git-commit: 299c4cb377c65e49b94383704a906fdd0bb38d06
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 1%

---


# 커뮤니티용 FFmpeg {#ffmpeg-for-communities}

## 개요 {#overview}

FFmpeg는 오디오 및 비디오를 변환하고 스트리밍하기 위한 솔루션이며, 설치할 때 [비디오 에셋](../../help/sites-authoring/default-components-foundation.md#video) 및 AEM Communities의 활성 기능을 적절하게 트랜스코딩하는 데 사용됩니다.

FFmpeg는 작성자 환경에서 업로드된 활성 리소스에 대한 메타데이터를 얻는 데 사용되며 활성 리소스를 나열할 때 표시할 축소판을 생성합니다.

## FFmpeg 설치 {#installing-ffmpeg}

FFmpeg는 AEM *작성자* 인스턴스를 호스팅하는 서버에 설치해야 합니다.

1. https://www.ffmpeg.org으로 [이동합니다](https://www.ffmpeg.org/).
1. 특정 환경용 최신 버전의 FFmpeg를 다운로드합니다(Macintosh, Windows 또는 Linux).

   * 이전 버전의 보안 취약점으로 인해 FFmpeg를 최신 상태로 유지하는 것이 중요합니다.

1. OS용 지침에 따라 FFmpeg를 설치합니다.

1. FFmpeg 실행 파일이 시스템 경로에 설정되어 있는지 확인합니다.

   시스템의 모든 디렉토리에서 FFmpeg를 실행할 수 있어야 합니다.

   * 예, `ffmpeg -version`.

## FFmpeg 트랜스코딩 서비스 구성 {#configure-ffmpeg-transcoding-service}

기본적으로 FFmpeg가 설치되면 [!UICONTROL DAM 자산 업데이트 워크플로우 정의에 따라 여러 표현물이 구성(변환)] 됩니다.

변환은 CPU 집약이므로 대상 변환 목록을 수정하는 것이 좋습니다. 대부분의 경우 트랜스코딩은 필요하지 않습니다.

DAM 자산 [!UICONTROL 업데이트] 작업 과정을 수정하고 이 예에서는 트랜스코딩 기능을 해제하려면:

* 관리자 권한으로 작성 인스턴스에 로그인합니다.
* 글로벌 탐색에서 도구 > **[!UICONTROL 워크플로우]** > **[!UICONTROL 모델]** 으로 **[!UICONTROL 이동합니다]**.
* DAM 자산 **[!UICONTROL 업데이트를 찾습니다]**.
* 클래식 UI에서 편집할 워크플로우를 두 번 클릭하여 엽니다.

   결과 위치: [http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html](http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html)

* 단계 속성 대화 상자에 액세스하려면 **[!UICONTROL FFmpeg 트랜스코딩]** 단계를 두 번 클릭합니다.
* 프로세스 **[!UICONTROL 탭]** 아래에서

   * **[!UICONTROL 문서]**: 코드 변환을 비활성화하려면 모든 항목을 지웁니다. 기본값: `profile:format_ogg,profile:format_aac,profile:format_flv,profile:format_aac_ie`

   ![chlimage_1-372](assets/chlimage_1-372.png)

* 확인을 **[!UICONTROL 선택하여]** 대화 상자를 `Step Properties` 닫습니다.

* 저장을 **[!UICONTROL 선택하여]** 워크플로우를 `DAM Update Asset` 저장합니다.



