---
title: CSV로 내보내기
description: 로컬 시스템에서 페이지에 대한 정보를 CSV 파일로 내보내기
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
docset: aem65
exl-id: 18910143-f2f2-4cfe-88b9-651df90d9cb9
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: e2c1b6d3-bb7e-4fe8-8c72-f7b403298e91
    internal-label: Authoring
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 81%
---
# CSV로 내보내기{#export-to-csv}

**CSV 보고서 만들기**&#x200B;를 사용하여 페이지에 대한 정보를 로컬 시스템의 CSV 파일로 내보낼 수 있습니다.

* 다운로드한 파일은 `export.csv`라고 합니다.
* 콘텐츠는 사용자가 선택한 속성에 따라 다릅니다.
* 내보내기에 대한 깊이와 함께 경로를 정의할 수 있습니다.

>[!NOTE]
>
>브라우저의 다운로드 기능 및 기본 대상이 사용됩니다.

**CSV 내보내기 만들기** 마법사를 사용하면 다음을 선택할 수 있습니다.

* 내보낼 속성
  * 메타데이터
    * 이름
    * 수정됨
    * 게시됨
    * 템플릿
    * 워크플로
  * 번역
    * 번역됨
  * 분석
    * 페이지 조회수
    * 고유 방문자
    * 페이지 시간
* 깊이
  * 상위 경로
  * 직접 하위만
  * 하위의 추가 수준
  * 수준

결과 `export.csv` 파일은 Excel 또는 기타 호환되는 애플리케이션에서 열 수 있습니다. 예를 들면 다음과 같습니다.

![etc-01](assets/etc-01.png)

**CSV 보고서** 만들기 옵션은 **사이트** 콘솔(목록 보기)을 탐색할 때 사용할 수 있습니다. 이 옵션은 **만들기** 드롭다운 메뉴의 옵션입니다.

![etc-02](assets/etc-02.png)

CSV 내보내기를 만들려면:

1. **사이트** 콘솔을 열고 필요한 경우 필요한 위치로 이동합니다.
1. 도구 모음에서 **만들기**&#x200B;를 선택한 다음 **CSV 보고서**&#x200B;를 선택하여 마법사를 엽니다.

   ![etc-03](assets/etc-03.png)

1. 내보낼 필수 속성을 선택합니다.
1. **만들기**&#x200B;를 선택합니다.
