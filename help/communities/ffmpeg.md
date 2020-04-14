---
title: 커뮤니티를 위한 FFmpeg
seo-title: 커뮤니티를 위한 FFmpeg
description: 커뮤니티용 FFmpeg 설치 및 구성 방법
seo-description: 커뮤니티용 FFmpeg 설치 및 구성 방법
uuid: ef2f821c-70e9-4889-a8d7-a93b10a1d428
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 739ec991-552b-42cd-85cd-984d1c9fe8fd
translation-type: tm+mt
source-git-commit: f24142064b15606a5706fe78bf56866f7f9a40ae

---


# 커뮤니티를 위한 FFmpeg {#ffmpeg-for-communities}

## 개요 {#overview}

FFmpeg는 오디오 및 비디오를 변환 및 스트리밍하기 위한 솔루션으로, 설치되면 [비디오 에셋의](../../help/sites-authoring/default-components-foundation.md#video) 적절한 트랜스코딩과 AEM Communities의 지원 기능에 사용됩니다.

FFmpeg는 작성자 환경에서 업로드된 활성 리소스에 대한 메타데이터를 얻을 수 있을 뿐만 아니라 지원 리소스를 나열할 때 표시할 축소판을 생성할 수 있습니다.

## FFmpeg 설치 {#installing-ffmpeg}

FFmpeg는 AEM *작성자* 인스턴스를 호스팅하는 서버에 설치해야 합니다.

1. https://www.ffmpeg.org으로 [이동](https://www.ffmpeg.org/)
1. 특정 환경용 최신 버전의 FFmpeg 다운로드(Macintosh, Windows 또는 Linux)

   * 이전 버전의 보안 취약점으로 인해 FFmpeg를 최신 상태로 유지하는 것이 중요합니다.

1. OS에 대한 지침에 따라 FFmpeg를 설치합니다.

1. FFmpeg 실행 파일이 시스템 경로에 설정되어 있는지 확인합니다.

   시스템의 모든 디렉토리에서 FFmpeg를 실행할 수 있어야 합니다.

   * for example, `ffmpeg -version`

## FFmpeg 트랜스코딩 서비스 구성 {#configure-ffmpeg-transcoding-service}

기본적으로 FFmpeg가 설치되면 DAM 자산 업데이트 [!UICONTROL 워크플로우 정의에 따라 여러 변환이] 구성(변환)됩니다.

변환은 CPU를 많이 사용하므로 대상 변환 목록을 수정하는 것이 좋습니다. 대부분의 경우 트랜스코딩은 필요하지 않습니다.

DAM 자산 [!UICONTROL 업데이트] 워크플로우를 수정하고 이 예에서는 코드 변환을 끕니다.

* 관리자 권한으로 작성 인스턴스에 로그인
* 전역 탐색에서:도구 **[!UICONTROL > 워크플로우 > 모델]**
* DAM **[!UICONTROL 업데이트 자산 찾기]**
* 클래식 UI에서 편집할 워크플로우를 두 번 클릭하여 엽니다.

   결과 위치: [http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html](http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html)

* FFmpeg **[!UICONTROL 트랜스코딩]** 단계를 두 번 클릭하여 단계 속성 대화 상자에 액세스합니다
* 프로세스 **[!UICONTROL 탭에서]** 다음을 수행합니다.

   * **[!UICONTROL 문서]**:코드 변환을 비활성화하려면 모든 항목 지우기 기본값: `profile:firefoxhq,profile:hq,profile:flv,profile:iehq`

![chlimage_1-372](assets/chlimage_1-372.png)

* 확인을 **[!UICONTROL 선택하여]** 대화 상자를 닫습니다 `Step Properties`

* 저장을 **[!UICONTROL 선택하여]** 워크플로우를 저장합니다 `DAM Update Asset`

   (왼쪽 위 모서리)

