---
title: UI 선택
description: 사용자 작성의 편의를 위해 터치 지원 UI에서는 필요할 때 클래식 UI로 전환할 수 있습니다.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
exl-id: 57d45b06-e76e-420c-8cd0-389bd9f811af
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---

# UI 선택{#selecting-your-ui}

터치 사용 UI가 클래식 UI를 대체하므로 AEM 인스턴스의 사용자나 관리자는 클래식 UI를 계속 사용하려면 활성 결정을 내려야 합니다. 클래식 UI가 더 이상 유지되지 않으므로 작성 사용자가 클래식 UI에서 터치 사용 UI의 해당 UI로 간단히 전환할 수 없습니다.

사용자 작성의 편의를 위해 터치 지원 UI에서는 필요할 때 클래식 UI로 전환할 수 있습니다. 다음을 참조하십시오. [UI 선택](/help/sites-authoring/select-ui.md) 를 참조하십시오.

>[!NOTE]
>
>이전 버전에서 업그레이드된 인스턴스는 페이지 작성을 위한 클래식 UI를 유지합니다.
>
>업그레이드 후 페이지 작성은 터치 지원 UI로 자동으로 전환되지 않지만 다음을 사용하여 이를 구성할 수 있습니다.[OSGi 구성](/help/sites-deploying/configuring-osgi.md) / **WCM 작성 UI 모드 서비스** ( `AuthoringUIMode` service). 다음을 참조하십시오 [편집기에 대한 UI 무시](#uioverridesfortheeditor).

## 인스턴스에 대한 기본 UI 구성 {#configuring-the-default-ui-for-your-instance}

시스템 관리자는 를 사용하여 시작 및 로그인 시 표시되는 UI를 구성할 수 있습니다. [루트 매핑](/help/sites-deploying/osgi-configuration-settings.md#daycqrootmapping).

사용자 기본값이나 세션 설정으로 재정의할 수 있습니다.
