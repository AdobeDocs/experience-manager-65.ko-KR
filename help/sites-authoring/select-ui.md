---
title: AEM에서 사용자 인터페이스 선택
description: AEM에서 작업하는 데 사용하는 인터페이스를 구성합니다.
uuid: ab127f2f-2f8a-4398-90dd-c5d48eed9e53
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: e418d330-f234-411d-8cad-3fd9906dcbee
docset: aem65
exl-id: 01cab3c3-4c0d-44d9-b47c-034de9a08cb1
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '745'
ht-degree: 1%

---

# UI 선택{#selecting-your-ui}

터치 활성화 UI가 이제 표준 UI이고 사이트의 관리 및 편집에서 기능 패리티에 거의 도달했지만 사용자가 로 전환하려고 할 수 있습니다 [클래식 UI](/help/sites-classic-ui-authoring/classicui.md). 이를 위해 몇 가지 옵션이 있습니다.

>[!NOTE]
>
>클래식 UI의 기능 패리티 상태에 대한 자세한 내용은 [터치 UI 기능 패리티](/help/release-notes/touch-ui-features-status.md) 문서.

사용할 UI를 정의할 수 있는 다양한 위치가 있습니다.

* [인스턴스에 대한 기본 UI 구성](#configuring-the-default-ui-for-your-instance)
이 경우 사용자가 이 설정을 재정의하고 계정 또는 현재 세션에 대해 다른 UI를 선택할 수 있지만, 사용자 로그인 시 기본 UI가 표시되도록 설정됩니다.

* [계정용 클래식 UI 작성 설정](/help/sites-authoring/select-ui.md#setting-classic-ui-authoring-for-your-account)
이 경우 사용자가 이 설정을 재정의하고 계정 또는 현재 세션에 대해 다른 UI를 선택할 수 있지만, 페이지를 편집할 때 기본적으로 사용할 UI가 설정됩니다.

* [현재 세션에 대한 클래식 UI로 전환](#switching-to-classic-ui-for-the-current-session)
이 설정은 현재 세션에 대한 클래식 UI로 전환합니다.

* 의 경우 [시스템을 작성하는 페이지는 UI와 관련하여 특정 항목을 무시합니다](#ui-overrides-for-the-editor).

>[!CAUTION]
>
>클래식 UI로 전환하는 다양한 옵션은 즉시 사용할 수 없습니다. 인스턴스에 대해 특별히 구성되어 있어야 합니다.
>
>자세한 내용은 [클래식 UI에 대한 액세스 활성화](/help/sites-administering/enable-classic-ui.md) 추가 정보.

>[!NOTE]
>
>이전 버전에서 업그레이드된 인스턴스는 페이지 작성을 위해 클래식 UI를 유지합니다.
>
>업그레이드 후에 페이지 작성이 터치 지원 UI로 자동 전환되지 않지만 [OSGi 구성](/help/sites-deploying/configuring-osgi.md) 의 **WCM 작성 UI 모드 서비스** ( `AuthoringUIMode` 서비스). 자세한 내용은 [편집기에 대해 UI 무시](#ui-overrides-for-the-editor).

## 인스턴스에 대한 기본 UI 구성 {#configuring-the-default-ui-for-your-instance}

시스템 관리자는 를 사용하여 시작 및 로그인 시 표시되는 UI를 구성할 수 있습니다 [루트 매핑](/help/sites-deploying/osgi-configuration-settings.md#daycqrootmapping).

사용자 기본값이나 세션 설정에 의해 대체할 수 있습니다.

## 계정용 클래식 UI 작성 설정 {#setting-classic-ui-authoring-for-your-account}

각 사용자가 자신의 액세스 권한을 갖습니다 [사용자 환경 설정](/help/sites-authoring/user-properties.md#userpreferences) 페이지 작성에 클래식 UI를 사용할지 여부를 정의합니다(기본 UI 대신).

세션 설정에 의해 무시될 수 있습니다.

## 현재 세션에 대한 클래식 UI로 전환 {#switching-to-classic-ui-for-the-current-session}

터치 지원 UI를 사용할 때 데스크톱 사용자는 클래식(데스크톱 전용) UI로 되돌릴 수 있습니다. 현재 세션에 대한 클래식 UI로 전환하는 방법에는 몇 가지가 있습니다.

* **탐색 링크**

   >[!CAUTION]
   >
   >클래식 UI로 전환하는 이 옵션은 즉시 사용할 수 없습니다. 인스턴스에 대해 특별히 구성되어 있어야 합니다.
   >
   >
   >자세한 내용은 [클래식 UI에 대한 액세스 활성화](/help/sites-administering/enable-classic-ui.md) 추가 정보.

   이 옵션이 활성화되어 있으면 적용 가능한 콘솔 위에 마우스를 올려 놓을 때마다 아이콘(모니터 기호)이 나타나고, 이 아이콘을 탭/클릭하면 클래식 UI에서 해당 위치가 열립니다.

   예를 들어 의 링크가 **Sites** to **siteadmin**:

   ![syui-01](assets/syui-01.png)

* **URL**

   클래식 UI는 시작 화면의 URL을 사용하여 액세스할 수 있습니다. `welcome.html`. 예:

   `https://localhost:4502/welcome.html`

   >[!NOTE]
   >
   >터치 지원 UI는 를 통해 액세스할 수 있습니다 `sites.html`. 예:
   >
   >
   >`https://localhost:4502/sites.html`

### 페이지를 편집할 때 클래식 UI로 전환 {#switching-to-classic-ui-when-editing-a-page}

>[!CAUTION]
>
>클래식 UI로 전환하는 이 옵션은 즉시 사용할 수 없습니다. 인스턴스에 대해 특별히 구성되어 있어야 합니다.
>
>자세한 내용은 [클래식 UI에 대한 액세스 활성화](/help/sites-administering/enable-classic-ui.md) 추가 정보.

활성화된 경우 **클래식 UI 열기** 다음에서 사용 가능합니다. **페이지 정보** 대화 상자:

![syui-02](assets/syui-02.png)

### 편집기에 대해 UI 무시 {#ui-overrides-for-the-editor}

사용자 또는 시스템 관리자가 정의한 설정은 페이지 작성의 경우 시스템에 의해 덮어쓸 수 있습니다.

* 페이지를 작성할 때:

   * 클래식 편집기는 `cf#` 를 입력합니다. 예:
      `https://localhost:4502/cf#/content/geometrixx/en/products/triangle.html`

   * 사용할 때는 터치 지원 편집기를 사용할 수 밖에 없습니다 `/editor.html` 를 클릭하거나 터치 장치를 사용할 때 사용됩니다. 예:
      `https://localhost:4502/editor.html/content/geometrixx/en/products/triangle.html`

* 이러한 강제성은 모두 일시적이며 브라우저 세션에 대해서만 유효합니다

   * 설정된 쿠키는 터치 활성화( `editor.html`) 또는 classic( `cf#`사용)

* 페이지를 통과할 때 `siteadmin`은(는) 다음 항목이 있는지 확인하게 됩니다.

   * 쿠키
   * 사용자 환경 설정
   * 어느 쪽도 없을 경우에는, 기본적으로 [OSGi 구성](/help/sites-deploying/configuring-osgi.md) 의 **WCM 작성 UI 모드 서비스** ( `AuthoringUIMode` 서비스).

>[!NOTE]
>
>If [사용자가 페이지 작성에 대한 환경 설정을 이미 정의했습니다.](#settingthedefaultauthoringuiforyouraccount): OSGi 속성을 변경하여 재정의되지 않습니다.

>[!CAUTION]
>
>이미 설명한 대로 쿠키의 사용으로 인해 다음 중 하나를 사용하지 않는 것이 좋습니다.
>
>* URL 수동 편집 - 비표준 URL은 알 수 없는 상황과 기능 부족을 초래할 수 있습니다.
>* 두 편집기를 동시에 열기. 예를 들어 별도의 창으로 엽니다.

