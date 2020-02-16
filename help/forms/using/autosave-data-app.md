---
title: AEM Forms 앱에서 자동 저장 사용
seo-title: AEM Forms 앱에서 자동 저장 사용
description: 데이터 손실을 방지할 수 있는 AEM Forms 앱의 자동 저장 기능을 사용하는 방법을 알아봅니다.
seo-description: 데이터 손실을 방지할 수 있는 AEM Forms 앱의 자동 저장 기능을 사용하는 방법을 알아봅니다.
uuid: 00fe6a10-1a72-443d-a840-0415dc769199
contentOwner: sashanka
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 2c71cc28-b7c8-4785-9fc2-b47fa80cbd70
docset: aem65
translation-type: tm+mt
source-git-commit: d9975c0dcc02ae71ac64aadb6b4f82f7c993f32c

---


# AEM Forms 앱에서 자동 저장 사용{#using-autosave-in-aem-forms-app}

사용자가 Adobe Experience Manager Forms 앱에 데이터를 입력하면 자동 저장 기능이 정기적으로 데이터를 저장합니다. AEM Forms 앱의 자동 저장 기능을 사용하면 앱이 실수로 닫혀 있는 경우 데이터 손실을 방지할 수 있습니다.

앱이 실수로 닫힐 수 있습니다.

* 배터리 부족으로 장치를 종료하는 경우
* 사용자가 앱을 종료하는 경우
* 예기치 않은 충돌이 발생하는 경우

앱이 입력한 데이터를 저장하는 간격을 지정할 수 있습니다.

>[!NOTE]
>
>자동 저장 빈도를 신중하게 선택합니다. 자주 자동 저장 작업을 수행하면 장치의 성능에 현저한 영향을 줄 수 있습니다.

AEM Forms 앱에서 자동 저장 기능을 사용하려면 다음 단계를 수행하십시오.

1. 앱에 로그인하고 설정 > **일반으로 이동합니다**.
1. 일반 화면에서 자동 저장 **빈도** 옵션을 사용하여 앱에서 입력된 데이터를 저장할 간격을 선택합니다.
   [ 자동 저장 빈도 ![설정](assets/using-autosave-freq-07.png)](assets/using-autosave-freq-07-1.png)

1. 앱을 다시 시작하고 동일한 사용자로 로그인하면 저장되지 않은 작업 복구 대화 상자를 사용하여 작업을 복원하라는 메시지가 표시됩니다. 저장되지 **않은 작업 복구** 대화 상자에서 확인을 클릭하여 저장된 작업을 다시 시작합니다. 취소를 클릭하여 **마지막으로** 트리거된 자동 저장에 해당하는 저장된 데이터를 삭제하고 새 작업을 시작할 수 있습니다.

   [확인] **을**클릭하면 앱이 중단되기 전에 트리거된 최신 자동 저장에 해당하는 데이터로 작업이 복원됩니다. 여기에는 양식 데이터 및 작업과 연관된 모든 첨부 파일이 포함됩니다.
   [![](assets/autosave-flow.png)](assets/using-autosave-freq-06.png)****작업**&#x200B;복구&#x200B;**A.진행 중인 작업 양식 B**&#x200B;입니다.응용 프로그램을 강제로 **닫은 C.** 응용 프로그램이 저장되지 않은 작업 복구 대화 상자 D로 다시 **시작되었습니다.원본 데이터로 양식 복원

