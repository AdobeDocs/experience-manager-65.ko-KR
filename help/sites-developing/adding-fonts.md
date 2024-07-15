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
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 1%

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
