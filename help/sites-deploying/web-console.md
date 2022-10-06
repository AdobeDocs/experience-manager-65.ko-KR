---
title: 웹 콘솔
seo-title: Web Console
description: AEM 웹 콘솔을 사용하는 방법을 알아봅니다.
seo-description: Learn how to use the AEM web console.
uuid: 7856b2b3-4216-421d-a315-cd9a55936362
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 4a33fddd-0399-40e4-8687-564fb6765b76
feature: Configuring
exl-id: 9acbf61f-73a8-4998-9421-dd933f30ac8a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 4%

---

# 웹 콘솔{#web-console}

AEM의 웹 콘솔은 [Apache Felix 웹 관리 콘솔](https://felix.apache.org/documentation/subprojects/apache-felix-web-console.html). Apache Felix는 OSGi 프레임워크 및 표준 서비스가 포함된 OSGi R4 서비스 플랫폼을 구현하기 위한 커뮤니티 활동입니다.

>[!NOTE]
>
>웹 콘솔에서 Sling 기본값과 관련된 기본 설정을 언급하는 설명이 있습니다.
>
>AEM에는 자체 기본값이 있으므로 기본값 세트가 콘솔에 설명된 것과 다를 수 있습니다.

웹 콘솔에는 다음과 같은 OSGi 번들을 유지 관리하기 위한 다양한 탭이 있습니다.

* [구성](#configuration): OSGi 번들을 구성하는 데 사용되며, 따라서 AEM 시스템 매개 변수를 구성하는 기본 메커니즘입니다
* [번들](#bundles): 번들 설치에 사용됨
* [구성 요소](#components): AEM에 필요한 구성 요소의 상태를 제어하는 데 사용됩니다.

변경된 내용은 실행 중인 시스템에 즉시 적용됩니다. 다시 시작할 필요가 없습니다.

콘솔에서 액세스할 수 있습니다 `../system/console`; 예:

`http://localhost:4502/system/console/components`

## 구성 {#configuration}

다음 **구성** 탭은 OSGi 번들을 구성하는 데 사용되며, 따라서 AEM 시스템 매개 변수를 구성하는 기본 메커니즘입니다.

>[!NOTE]
>
>자세한 내용은 [웹 콘솔을 사용한 OSGi 구성](/help/sites-deploying/configuring-osgi.md) 자세한 내용

다음 **구성** 탭은 다음 중 한 방법으로 액세스할 수 있습니다.

* 드롭다운 메뉴:

   **OSGi >**

* URL; 예:

   `http://localhost:4502/system/console/configMgr`

구성 목록이 표시됩니다.

![screen_shot_2012-02-15at52308pm](assets/screen_shot_2012-02-15at52308pm.png)

이 화면의 드롭다운 목록에서 사용할 수 있는 구성 유형은 다음 두 가지가 있습니다.

* **구성**
기존 구성을 업데이트할 수 있습니다. 여기에는 PID(영구 ID)가 있으며 다음 중 하나일 수 있습니다.

   * AEM에 대한 표준 및 필수 사항입니다. 이러한 값은 삭제된 경우 기본 설정으로 반환됩니다.
   * 공장 구성에서 생성된 인스턴스 이러한 인스턴스는 사용자가 만들고, 삭제하면 인스턴스가 제거됩니다.

* **출하 시 구성**
필요한 기능 개체의 인스턴스를 만들 수 있습니다.

   영구 ID를 할당받은 다음 구성 드롭다운 목록에 나열됩니다.

목록에서 항목을 선택하면 해당 구성과 관련된 매개 변수가 표시됩니다.

![chlimage_1-21](assets/chlimage_1-21a.png)

그런 다음 필요에 따라 매개 변수를 업데이트하고

* **저장**

   변경한 내용을 저장합니다.

   공장 구성의 경우 영구 ID가 있는 새 인스턴스가 생성됩니다. 그런 다음 새 인스턴스가 구성 아래에 나열됩니다.

* **재설정**

   화면에 표시된 매개 변수를 마지막으로 저장된 매개 변수로 재설정합니다.

* **삭제**

   현재 구성을 삭제합니다. standard이면 매개 변수가 기본 설정으로 반환됩니다. 출하 시 구성에서 생성된 경우 특정 인스턴스가 삭제됩니다.

* **바인딩 해제**

   번들에서 현재 구성을 바인딩 해제합니다.

* **취소**

   현재 변경 내용을 취소합니다.

## 번들 {#bundles}

다음 **번들** 탭은 AEM에 필요한 OSGi 번들을 설치하는 메커니즘입니다. 탭은 다음 방법 중 하나로 액세스할 수 있습니다.

* 드롭다운 메뉴:

   **OSGi >**

* URL; 예:

   `http://localhost:4502/system/console/bundles`

번들 목록이 표시됩니다.

![screen_shot_2012-02-15at44740pm](assets/screen_shot_2012-02-15at44740pm.png)

이 탭을 사용하여 다음을 수행할 수 있습니다.

* **설치 또는 업데이트**

   다음을 수행할 수 있습니다 **찾아보기** 번들이 포함된 파일을 찾고 이 파일을 사용할지 여부를 지정합니다 **시작** 즉시 **시작 수준**.

* **다시 로드**

   표시된 목록을 새로 고칩니다.

* **패키지 새로 고침**

   모든 패키지의 참조를 확인하고 필요에 따라 새로 고칩니다.

   예를 들어 업데이트 후에도 이전 참조로 인해 이전 버전과 새 버전이 모두 계속 실행될 수 있습니다. 이 옵션을 선택하면 모든 참조를 새 버전으로 이동하여 이전 버전이 중지됩니다.

* **시작**

   지정된 시작 수준에 따라 번들을 시작합니다.

* **중지**

   번들을 중지합니다.

* **제거**

   시스템에서 번들을 제거합니다.

* **상태 보기**

   목록에는 번들의 현재 상태가 지정됩니다. 자세한 내용을 보려면 특정 번들의 이름을 클릭하십시오.

>[!NOTE]
>
>후 **업데이트** 다음을 수행하는 것이 좋습니다 **패키지 새로 고침**.

## 구성 요소 {#components}

다음 **구성 요소** 탭에서는 다양한 구성 요소를 활성화 및/또는 비활성화할 수 있습니다. 다음 중 한 방법으로 액세스할 수 있습니다.

* 드롭다운 메뉴:

   **기본 >**

* URL; 예:

   `http://localhost:4502/system/console/components`

구성 요소 목록이 표시됩니다. 특정 구성 요소에 대한 구성 세부 사항을 활성화, 비활성화 또는(해당되는 경우)하는 데 다양한 아이콘을 사용할 수 있습니다.

![screen_shot_2012-02-15at52144pm](assets/screen_shot_2012-02-15at52144pm.png)

특정 구성 요소의 이름을 클릭하면 해당 상태에 대한 추가 정보가 표시됩니다. 구성 요소를 활성화, 비활성화 또는 다시 로드할 수도 있습니다.

![chlimage_1-22](assets/chlimage_1-22a.png)

>[!NOTE]
>
>활성화 또는 비활성화는 AEM/CRX가 다시 시작될 때만 적용됩니다.
>
>시작 상태는 구성 요소 설명자 내에 정의되며, 구성 설명자는 개발 중에 생성되며 번들 생성 시 번들에 저장됩니다.
