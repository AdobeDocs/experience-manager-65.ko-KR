---
title: AEM에서 사용자 인터페이스 선택
description: Adobe Experience Manager 6.5에서 작동하는 데 사용하는 인터페이스를 구성합니다.
exl-id: 01cab3c3-4c0d-44d9-b47c-034de9a08cb1
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '738'
ht-degree: 1%

---

# UI 선택{#selecting-your-ui}

Adobe Experience Manager(AEM) 터치 지원 UI는 이제 표준 UI이며 사이트 관리 및 편집으로 기능 패리티에 거의 도달했습니다. 그러나 사용자가 로 전환하고자 하는 경우가 있을 수 있습니다. [클래식 UI](/help/sites-classic-ui-authoring/classicui.md). 이 작업을 수행하는 데에는 몇 가지 옵션이 있습니다.

>[!NOTE]
>
>클래식 UI를 사용하는 기능 패리티의 상태에 대한 자세한 내용은 [Touch UI 기능 패리티](/help/release-notes/touch-ui-features-status.md) 문서.

사용할 UI를 정의할 수 있는 위치는 다양합니다.

* [인스턴스에 대한 기본 UI 구성](#configuring-the-default-ui-for-your-instance)
사용자 로그인 시 표시할 기본 UI를 설정합니다. 사용자는 이를 무시하고 계정 또는 현재 세션에 대해 다른 UI를 선택할 수 있습니다.

* [계정에 대한 클래식 UI 작성 설정](/help/sites-authoring/select-ui.md#setting-classic-ui-authoring-for-your-account)
사용자가 UI를 재정의하고 계정 또는 현재 세션에 대해 다른 UI를 선택할 수 있지만, 이렇게 하면 페이지를 편집할 때 UI가 기본값으로 설정됩니다.

* [현재 세션의 클래식 UI로 전환](#switching-to-classic-ui-for-the-current-session)
현재 세션의 클래식 UI로 전환합니다.

* 의 경우에 [페이지 작성 시, 시스템은 UI와 관련하여 특정 무시를 수행합니다](#ui-overrides-for-the-editor).

>[!CAUTION]
>
>클래식 UI로 전환하는 다양한 옵션은 즉시 사용할 수 없으며, 인스턴스에 맞게 구성해야 합니다.
>
>다음을 참조하십시오 [클래식 UI에 대한 액세스 활성화](/help/sites-administering/enable-classic-ui.md) 추가 정보.

>[!NOTE]
>
>이전 버전에서 업그레이드된 인스턴스는 페이지 작성을 위한 클래식 UI를 유지합니다.
>
>업그레이드 후 페이지 작성은 터치 지원 UI로 자동으로 전환되지 않지만 다음을 사용하여 이를 구성할 수 있습니다. [OSGi 구성](/help/sites-deploying/configuring-osgi.md) / **WCM 작성 UI 모드 서비스** ( `AuthoringUIMode` service). 다음을 참조하십시오 [편집기에 대한 UI 무시](#ui-overrides-for-the-editor).

## 인스턴스에 대한 기본 UI 구성 {#configuring-the-default-ui-for-your-instance}

시스템 관리자는 를 사용하여 시작 및 로그인 시 표시되는 UI를 구성할 수 있습니다. [루트 매핑](/help/sites-deploying/osgi-configuration-settings.md#daycqrootmapping).

사용자 기본값이나 세션 설정으로 재정의할 수 있습니다.

## 계정에 대한 클래식 UI 작성 설정 {#setting-classic-ui-authoring-for-your-account}

각 사용자는 자신의 고유 기능에 액세스할 수 있습니다 [사용자 환경 설정](/help/sites-authoring/user-properties.md#userpreferences) 페이지 작성에 기본 UI 대신 클래식 UI를 사용할지 여부를 정의합니다.

세션 설정으로 재정의할 수 있습니다.

## 현재 세션의 클래식 UI로 전환 {#switching-to-classic-ui-for-the-current-session}

터치 사용 UI를 사용할 때 데스크탑 사용자는 클래식(데스크탑 전용) UI로 되돌릴 수 있습니다. 현재 세션에 대한 클래식 UI로 전환하는 방법에는 몇 가지가 있습니다.

* **탐색 링크**

  >[!CAUTION]
  >
  >클래식 UI로 전환하는 이 옵션은 즉시 사용할 수 없으며, 인스턴스에 맞게 구성해야 합니다.
  >
  >
  >다음을 참조하십시오 [클래식 UI에 대한 액세스 활성화](/help/sites-administering/enable-classic-ui.md) 추가 정보.

  이 기능이 활성화되어 있으면 해당 콘솔 위에 마우스를 올려 놓을 때마다 아이콘(모니터 기호)이 나타납니다. 이 아이콘을 탭하거나 클릭하면 클래식 UI에서 적절한 위치가 열립니다.

  예를 들어 의 링크입니다 **사이트** 끝 **siteadmin**:

  ![syui-01](assets/syui-01.png)

* **URL**

  의 시작 화면에 대한 URL을 사용하여 클래식 UI에 액세스할 수 있습니다. `welcome.html`. 예:

  `https://localhost:4502/welcome.html`

  >[!NOTE]
  >
  >터치 지원 UI는 를 통해 액세스할 수 있습니다. `sites.html`. 예:
  >
  >
  >`https://localhost:4502/sites.html`

### 페이지 편집 시 클래식 UI로 전환 {#switching-to-classic-ui-when-editing-a-page}

>[!CAUTION]
>
>클래식 UI로 전환하는 이 옵션은 즉시 사용할 수 없으며, 인스턴스에 맞게 구성해야 합니다.
>
>다음을 참조하십시오 [클래식 UI에 대한 액세스 활성화](/help/sites-administering/enable-classic-ui.md) 추가 정보.

활성화된 경우 **클래식 UI 열기** 다음에서 사용할 수 있습니다. **페이지 정보** 대화 상자:

![syui-02](assets/syui-02.png)

### 편집기에 대한 UI 무시 {#ui-overrides-for-the-editor}

페이지 작성이 있는 경우 사용자 또는 시스템 관리자가 정의한 설정이 시스템에 의해 재정의될 수 있습니다.

* 페이지 작성 시:

   * 를 사용하여 페이지에 액세스할 때 클래식 편집기를 사용해야 합니다. `cf#` 를 입력합니다. 예:
     `https://localhost:4502/cf#/content/geometrixx/en/products/triangle.html`

   * 을 사용할 때는 터치 지원 편집기를 사용해야 합니다 `/editor.html` URL에서 또는 터치 장치를 사용할 때. 예:
     `https://localhost:4502/editor.html/content/geometrixx/en/products/triangle.html`

* 모든 강제 작업은 일시적이며 브라우저 세션에만 유효합니다

   * 쿠키 세트는 터치 활성화 여부에 따라 설정됩니다( `editor.html`) 또는 classic ( `cf#`)가 사용됩니다.

* 페이지를 여는 중 `siteadmin`에서 다음 항목이 있는지 확인합니다.

   * 쿠키
   * 사용자 환경 설정
   * 둘 다 없는 경우 기본값은 다음에 설정된 정의로 설정됩니다. [OSGi 구성](/help/sites-deploying/configuring-osgi.md) / **WCM 작성 UI 모드 서비스** ( `AuthoringUIMode` service).

>[!NOTE]
>
>If [사용자가 페이지 작성에 대한 기본 설정을 이미 정의했습니다.](#settingthedefaultauthoringuiforyouraccount)OSGi 속성을 변경해도 재정의되지 않습니다.

>[!CAUTION]
>
>이미 설명한 대로 쿠키를 사용하므로 다음 중 하나를 수행하는 것은 권장되지 않습니다.
>
>* URL을 수동으로 편집 - 비표준 URL은 알 수 없는 상황과 기능 부재를 초래할 수 있습니다.
>* 두 편집기를 동시에 엽니다(예: 별도의 창에서).
