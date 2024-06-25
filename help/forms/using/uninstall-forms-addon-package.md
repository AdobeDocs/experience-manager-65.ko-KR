---
title: 이 문서에는 CRX 패키지 관리자를 사용하여 Forms 추가 기능 패키지를 제거하는 지침이 포함되어 있습니다.
description: CRX 패키지 관리자를 사용하여 Forms 추가 기능 패키지를 제거하는 단계를 알아봅니다.
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
source-git-commit: 2755e414ea23ebc1472e9c08d832eca93f28311b
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 1%

---


# AEM 인스턴스에서 AEM Forms 추가 기능 패키지 제거

이 문서에서는 AEM Forms SDK 인스턴스에서 AEM Forms 추가 기능 패키지를 올바르게 제거하는 데 필요한 절차에 대해 설명합니다. 다음 단계에 따라 Forms 추가 기능 패키지를 제거하여 AEM 환경에 문제가 발생하지 않도록 합니다.

## 전제 조건

데이터 손실을 방지하려면 백업을 수행해야 합니다.

## AEM Forms 추가 기능 패키지를 제거하려면

AEM Forms 추가 기능 패키지를 제거하려면 다음 단계를 수행하십시오.

1. **AEM Forms 추가 기능 패키지를 제거합니다.**
   1. 다음 위치로 이동 `http://[host]:[port]/crx/de/index.jsp`.
   1. 을(를) 찾아 제거합니다. `AEM Forms add-on package`.

   ![패키지 제거](/help/forms/using/assets/uninstall-aem-forms-package.png)

1. **CRXDE에서 기본 폴더를 삭제합니다.**
   1. 다음 위치로 이동 `http://[host]:[port]/crx/de/index.jsp`.
   1. 다음으로 이동 `/libs/fd/native/install` 및 삭제 `native` crxde의 폴더입니다.

      ![CRX/de에서 네이티브 노드 삭제](/help/forms/using/assets/native-install-folder-crxde.png)
   1. 변경 사항을 저장합니다.

1. **AEM Forms SDK를 중지합니다.**
   1. &#39;Ctrl + C&#39; 명령을 사용하여 AEM Forms SDK 인스턴스를 중지합니다.

1. **Crx-quickstart 폴더에 기반을 확인하고 폴더를 설치합니다.**
   1. 다음으로 이동 `..author\crx-quickstart` AEM Forms SDK 인스턴스의 폴더
   1. 다음 이름의 폴더 검색 `bedrock` 및 `install`.
검색되면 다음 항목에서 삭제되는지 확인합니다. `crx-quickstart` AEM Forms SDK 인스턴스의 폴더

   >[!NOTE]
   >
   > 다음 `bedrock` AEM Forms SDK 인스턴스를 다시 시작하면 폴더가 자동으로 다시 생성됩니다.

1. **AEM 인스턴스를 다시 시작합니다.**
   1. 이전 단계가 모두 완료되면, [AEM Forms SDK 인스턴스 다시 시작](/help/forms/using/restart-aem-sdk.md).




