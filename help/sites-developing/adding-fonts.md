---
title: 그래픽 렌더링용 글꼴 추가
seo-title: Adding Fonts for Graphic-Rendering
description: AEM을 사용하면 콘텐츠에서 동적으로 가져온 텍스트가 포함된 그래픽을 생성할 수 있습니다
seo-description: AEM lets you generate graphics incorporating text dynamically taken from your content
uuid: 67d9b10f-e986-4d29-bde2-10e08075fe17
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 6af48ef5-75e6-4b66-bc0d-ecf254b1c4ef
exl-id: 725c81d0-0258-4118-8b01-29fd7bcaf9b3
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 5%

---

# 그래픽 렌더링용 글꼴 추가{#adding-fonts-for-graphic-rendering}

AEM을 사용하면 콘텐츠에서 동적으로 가져온 텍스트가 포함된 그래픽을 생성할 수 있습니다.

이렇게 하려면 나만의 글꼴을 로드하여 사용할 수도 있습니다.

현재 Java Platform의 모든 구현이 지원됩니다 [TrueType](https://en.wikipedia.org/wiki/Truetype) 글꼴.

1. CRXDE Lite을 열고 프로젝트 애플리케이션 폴더로 이동합니다.

   `/apps/<your-project>/`

1. 아래 `/apps/<your-project>/` 노드 만들기:

   * **이름**: `fonts`
   * **유형**: `sling:Folder`

   모든 변경 사항을 저장합니다.

1. WebDAV를 사용하여 글꼴 파일을 이 폴더에 복사합니다.

   >[!NOTE]
   >
   >저장소의 글꼴 파일에는 접미사가 있어야 합니다. `*.ttf` 또는 `*.TTF`.

1. 업데이트 [OSGi 구성](/help/sites-deploying/configuring-osgi.md) / [Day Commons GFX 글꼴 도우미](/help/sites-deploying/osgi-configuration-settings.md). 글꼴 폴더에 경로를 추가합니다(예: ). `/apps/<your-project>/fonts`.

1. CRXDE Lite으로 돌아갑니다. 이제 다음이 표시됩니다. `.fontlist` 가져온 글꼴의 이름이 들어 있는 폴더의 노드입니다.

   이제 이러한 글꼴을 Java API에서 사용할 준비가 되었습니다.

Java API와 함께 글꼴을 사용하는 방법에 대한 자세한 내용은 [java API의 Font 클래스에 대한 설명서](https://download.oracle.com/javase/6/docs/api/java/awt/Font.html).
