---
title: 그래픽 렌더링용 글꼴 추가
seo-title: 그래픽 렌더링용 글꼴 추가
description: AEM을 사용하면 컨텐츠에서 동적으로 가져온 텍스트를 포함하는 그래픽을 생성할 수 있습니다
seo-description: AEM을 사용하면 컨텐츠에서 동적으로 가져온 텍스트를 포함하는 그래픽을 생성할 수 있습니다
uuid: 67d9b10f-e986-4d29-bde2-10e08075fe17
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 6af48ef5-75e6-4b66-bc0d-ecf254b1c4ef
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 그래픽 렌더링용 글꼴 추가{#adding-fonts-for-graphic-rendering}

AEM을 사용하면 컨텐츠에서 동적으로 가져온 텍스트를 포함하는 그래픽을 생성할 수 있습니다.

이를 위해 고유한 글꼴을 로드하고 사용할 수도 있습니다.

현재 Java 플랫폼의 모든 구현은 TrueType [글꼴을 지원합니다](https://en.wikipedia.org/wiki/Truetype) .

1. CRXDE Lite를 열고 프로젝트 애플리케이션 폴더로 이동합니다.

   `/apps/<your-project>/`

1. 새 노드 `/apps/<your-project>/` 만들기 아래에서 다음을 수행합니다.

   * **이름**: `fonts`
   * **유형**: `sling:Folder`
   모든 변경 내용을 저장합니다.

1. 글꼴 파일을 이 폴더에 복사합니다.예를 들어, WebDAV를 사용합니다.

   >[!NOTE]
   >
   >저장소의 글꼴 파일에는 접미사 `*.ttf` 또는 접미어가 있어야 합니다 `*.TTF`.

1. Day [Commons GFX Font Helper](/help/sites-deploying/configuring-osgi.md) 의 OSGi 구성을 [업데이트합니다](/help/sites-deploying/osgi-configuration-settings.md). 글꼴 폴더의 경로를 추가합니다.예. `/apps/<your-project>/fonts`Adobe

1. CRXDE Lite로 돌아갑니다. 이제 가져온 글꼴의 이름이 포함된 노드가 폴더에 `.fontlist` 표시됩니다.

   이제 이러한 글꼴을 Java API에서 사용할 수 있습니다.

Java API에서 글꼴을 사용하는 방법에 대한 자세한 내용은 Java API의 글꼴 클래스에 대한 [설명서를 참조하십시오](https://download.oracle.com/javase/6/docs/api/java/awt/Font.html).

