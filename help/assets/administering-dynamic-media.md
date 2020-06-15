---
title: Dynamic Media 설정
description: 다이내믹 미디어를 설정하려면 다이내믹 미디어를 구성하고 이미지 및 뷰어 사전 설정을 관리해야 합니다
uuid: bcd1f9ab-4201-4222-9e4a-ba82b3c7cd6c
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: 36a4a4e7-8bb2-4853-b335-cf9148be410c
translation-type: tm+mt
source-git-commit: df89d5cfd5060d493babb89e92a9a98e851b8879
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 1%

---


# Setting Up Dynamic Media {#setting-up-dynamic-media}

[Dynamic Media](https://www.adobe.com/solutions/web-experience-management/dynamic-media.html) 는 웹, 모바일 및 소셜 사이트에서 사용하도록 자동으로 크기가 조정되는 다양한 시각적 머천다이징 및 마케팅 자산을 on-demand 방식으로 전달하여 자산을 관리하는 데 도움이 됩니다. Dynamic Media은 기본 소스 에셋 세트를 사용하여 글로벌, 확장 가능한 성능 최적화 네트워크를 통해 다양한 유형의 리치 컨텐츠를 실시간으로 생성하고 전달합니다.

>[!NOTE]
>
>이 설명서는 AEM에 직접 통합된 Dynamic Media 기능에 대해 설명합니다. AEM에 통합된 Dynamic Media Classic(이전의 Scene7)을 사용하는 경우 [Dynamic Media Classic 통합 설명서를 참조하십시오](/help/sites-administering/scene7.md).
>
>Dynamic Media과 함께 [Display Classic과 통합된 AEM을 사용하고 싶은 경우 이중 사용 시나리오를](/help/sites-administering/scene7.md#dual-use-scenario) 참조하십시오.

다이내믹 미디어를 관리하는 경우 다음 항목에 관심이 있습니다.

* [Dynamic Media-Scene7 모드](config-dms7.md) 구성 — 새 Dynamic Media 고객인 경우 이 구성을 사용합니다.
* [Dynamic Media-하이브리드 모드](config-dynamic.md) 구성 — AEM을 업그레이드하는 기존 Dynamic Media 고객인 경우 이 구성을 사용합니다.
* [이미지 사전 설정 관리](managing-image-presets.md)
* [뷰어 사전 설정 관리](managing-viewer-presets.md)
* [Dynamic Media 문제 해결 - Scene7 모드](troubleshoot-dms7.md)

다음 항목도 참조하십시오.

* [비디오 인코딩 및 비디오 프로필](video-profiles.md)
* [이미지 프로필](image-profiles.md)

>[!NOTE]
>
>**업그레이드 중인 경우:**
>
>* AEM을 설정하고 실행한 후 업로드하는 모든 자산은 Dynamic Media이 자동으로 활성화됩니다(시스템 관리자가 명시적으로 비활성화하지 않은 경우). AEM의 업그레이드된 인스턴스이고 Dynamic Media의 신규 경우 자산을 재처리하여 Dynamic Media이 활성화되도록 해야 할 수 있습니다.