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
role: Administrator
exl-id: dbe28334-3b38-4362-b4f8-e0630e634503
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 1%

---

# 커뮤니티에 대한 FFmpeg {#ffmpeg-for-communities}

## 개요 {#overview}

FFmpeg는 오디오 및 비디오를 변환 및 스트리밍하는 솔루션이며, 설치된 경우 AEM Communities 지원 기능뿐만 아니라 [비디오 자산](../../help/sites-authoring/default-components-foundation.md#video)의 적절한 코드 변환에 사용됩니다.

FFmpeg는 작성 환경에서 업로드된 지원 리소스에 대한 메타데이터를 가져오고 지원 리소스를 나열할 때 표시할 축소판을 생성하는 데 사용됩니다.

## FFmpeg 설치 {#installing-ffmpeg}

FFmpeg는 AEM *author* 인스턴스를 호스팅하는 서버에 설치해야 합니다.

1. [https://www.ffmpeg.org](https://www.ffmpeg.org/)로 이동합니다.
1. 특정 환경(Macintosh, Windows 또는 Linux)용 최신 버전의 FFmpeg를 다운로드합니다.

   * 이전 버전의 보안 취약점으로 인해 FFmpeg를 최신 상태로 유지하는 것이 중요합니다.

1. OS에 대한 지침에 따라 FFmpeg를 설치합니다.

1. FFmpeg 실행 파일이 시스템 경로에 설정되어 있는지 확인합니다.

   시스템의 모든 디렉토리에서 FFmpeg를 실행할 수 있습니다.

   * 예, `ffmpeg -version`.

## FFmpeg 코드 변환 서비스 구성 {#configure-ffmpeg-transcoding-service}

기본적으로 FFmpeg가 설치되면 여러 표현물이 [!UICONTROL DAM 자산 업데이트] 워크플로우 정의에 따라 구성(전송)됩니다.

전송은 CPU가 많이 사용되므로 대상 표현물 목록을 수정하는 것이 좋습니다. 대부분의 경우 코드 변환이 필요하지 않습니다.

[!UICONTROL DAM 자산 업데이트] 워크플로우를 수정하려면 다음을 수행합니다. 이 예에서 코드 변환을 끄십시오.

* 관리자 권한으로 작성자 인스턴스에 로그인합니다.
* 전역 탐색에서 **[!UICONTROL 도구]** > **[!UICONTROL 워크플로우]** > **[!UICONTROL 모델]**&#x200B;로 이동합니다.
* **[!UICONTROL DAM 자산 업데이트]**&#x200B;를 찾습니다.
* 클래식 UI에서 편집할 워크플로우를 두 번 클릭하여 엽니다.

   결과 위치:[http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html](http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html)

* **[!UICONTROL FFmpeg 코드 변환]** 단계를 두 번 클릭하여 단계 속성 대화 상자에 액세스합니다.
* **[!UICONTROL 프로세스]** 탭에서 다음을 수행합니다.

   * **[!UICONTROL 배치]**:코드 변환을 비활성화하려면 모든 항목을 선택 취소합니다. 기본값:  `profile:format_ogg,profile:format_aac,profile:format_flv,profile:format_aac_ie`

   ![configure-ffmpeg](assets/configure-ffmpeg.png)

* **[!UICONTROL 확인]** 을 선택하여 `Step Properties` 대화 상자를 닫습니다.

* **[!UICONTROL 저장]**&#x200B;을 선택하여 `DAM Update Asset` 워크플로우를 저장합니다.
