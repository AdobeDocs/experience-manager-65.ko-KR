---
title: 그래픽 렌더링용 글꼴 추가
description: AEM을 사용하면 콘텐츠에서 동적으로 가져온 텍스트가 포함된 그래픽을 생성할 수 있습니다
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: 725c81d0-0258-4118-8b01-29fd7bcaf9b3
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 6%
---
# 그래픽 렌더링용 글꼴 추가{#adding-fonts-for-graphic-rendering}

AEM을 사용하면 콘텐츠에서 동적으로 가져온 텍스트가 포함된 그래픽을 생성할 수 있습니다.

이렇게 하려면 나만의 글꼴을 로드하여 사용할 수도 있습니다.

현재 Java 플랫폼의 모든 구현은 [TrueType](https://en.wikipedia.org/wiki/Truetype) 글꼴을 지원합니다.

1. CRXDE Lite을 열고 프로젝트 애플리케이션 폴더로 이동합니다.

   `/apps/<your-project>/`

1. `/apps/<your-project>/`에서 노드 만들기:

   * **이름**: `fonts`
   * **유형**: `sling:Folder`

   모든 변경 사항을 저장합니다.

1. WebDAV를 사용하여 글꼴 파일을 이 폴더에 복사합니다.

   >[!NOTE]
   >
   >저장소의 글꼴 파일에는 접미사 `*.ttf` 또는 `*.TTF`이(가) 있어야 합니다.

1. [Day Commons GFX 글꼴 도우미](/help/sites-deploying/osgi-configuration-settings.md)의 [OSGi 구성](/help/sites-deploying/configuring-osgi.md)을 업데이트합니다. 글꼴 폴더에 경로를 추가합니다. 즉, `/apps/<your-project>/fonts`입니다.

1. CRXDE Lite으로 돌아갑니다. 이제 가져온 글꼴 이름이 포함된 폴더에 `.fontlist` 노드가 표시됩니다.

   이제 이러한 글꼴을 Java API에서 사용할 준비가 되었습니다.

Java API와 함께 글꼴을 사용하는 방법에 대한 자세한 내용은 Java API의 Font 클래스에 대한 [설명서](https://download.oracle.com/javase/6/docs/api/java/awt/Font.html)를 참조하십시오.
