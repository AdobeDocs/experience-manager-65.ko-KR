---
title: UI 선택
seo-title: UI 선택
description: 작성자는 편의를 위해 필요한 경우 터치 가능 UI를 클래식 UI로 전환할 수 있습니다.
seo-description: 작성자는 편의를 위해 필요한 경우 터치 가능 UI를 클래식 UI로 전환할 수 있습니다.
uuid: 755e513e-990c-4dba-8316-623f17bf5c33
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: dcac2a3a-3241-47de-96ce-982ab0bc05eb
exl-id: 57d45b06-e76e-420c-8cd0-389bd9f811af
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 60%

---

# UI 선택{#selecting-your-ui}

터치 지원 UI가 클래식 UI를 대체하므로 AEM 인스턴스의 사용자 또는 관리자는 클래식 UI를 계속 사용할지에 대해 적극적인 결정을 내려야 합니다. 클래식 UI는 더 이상 유지 관리되지 않으므로 작성 사용자가 클래식 UI에서 터치 지원 UI에 상응하는 UI로 간단하게 전환할 수 있는 방법이 없습니다.

작성자는 편의를 위해 필요한 경우 터치 가능 UI를 클래식 UI로 전환할 수 있습니다. 자세한 내용은 표준 작성 문서의 [UI 선택](/help/sites-authoring/select-ui.md)을 참조하십시오.

>[!NOTE]
>
>이전 버전에서 업그레이드된 인스턴스는 페이지 작성을 위해 클래식 UI를 유지합니다.
>
>업그레이드 후에 페이지 작성이 터치 지원 UI로 자동 전환되지 않지만 **WCM 작성 UI 모드 서비스**( `AuthoringUIMode` 서비스)의[OSGi 구성](/help/sites-deploying/configuring-osgi.md)을 사용하여 구성할 수 있습니다. [편집기에 대해 UI 무시](#uioverridesfortheeditor)를 참조하십시오.

## 인스턴스용 기본 UI 구성 {#configuring-the-default-ui-for-your-instance}

시스템 관리자는 [루트 매핑](/help/sites-deploying/osgi-configuration-settings.md#daycqrootmapping)을 사용하여 시작 및 로그인 시 표시되는 UI를 구성할 수 있습니다.

사용자 기본값이나 세션 설정에 의해 무시될 수 있습니다.
