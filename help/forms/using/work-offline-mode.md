---
title: 오프라인 모드에서 작업
description: AEM Forms 네트워크 범위 밖이나 완전히 오프라인 모드에서 모바일 장치를 오프라인으로 전환하고 AEM Forms 앱에서 작업합니다
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: ba4ceef1-510d-41ef-94b8-4834fb7de804
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 0%

---

# 오프라인 모드에서 작업 {#working-in-the-offline-mode}

AEM Forms 앱의 오프라인 모드를 사용하면 앱이 오프라인 상태가 되더라도 원활하게 작업할 수 있습니다. 네트워크 연결 없이도 양식을 열고, 업데이트하고, 제출할 수 있습니다.

앱을 AEM Forms 서버와 동기화하여 AEM Forms 앱에서 작업을 시작합니다. 내게 할당된 모든 양식은 앱에서 다운로드됩니다. JEE의 AEM Forms의 경우 작업은 작업 탭에서 가져오고 시작점은 Forms 탭에서 양식 및 기타 양식에 연결됩니다. OSGi의 AEM Forms의 경우 Forms 탭에 Forms만 로드됩니다.

앱을 동기화하는 방법에 대한 자세한 내용은 [앱 동기화](/help/forms/using/sync-app.md)를 참조하십시오.

## Forms을 오프라인에서 사용 가능하게 만들기 {#making-forms-available-offline}

앱을 AEM Forms 서버와 동기화하면 양식이 모바일 장치에 다운로드됩니다. 그러나 기본적으로 양식과 연결된 첨부 파일은 다운로드되지 않습니다. 이는 온라인 상태인 경우 첨부 파일을 볼 수 있음을 의미합니다. 그러나 오프라인 모드에서 첨부 파일을 볼 수 있도록 앱에서 기본 설정을 변경합니다.

연결된 첨부 파일이 각 양식과 함께 다운로드되도록 하려면 첨부 파일 가져오기를 ON으로 설정합니다. 자세한 내용은 [일반 설정 업데이트](/help/forms/using/update-general-settings.md)를 참조하십시오.

모바일 디바이스에서 데이터를 다운로드하면 디바이스의 성능에 영향을 줄 수 있으므로 기본적으로 첨부 파일 가져오기 설정이 꺼짐으로 설정되어 있습니다. 설정이 ON으로 업데이트된 후 서버에서 다운로드한 모든 작업에 대한 첨부 파일을 장치로 가져옵니다. 오프라인 모드에서 사용자는 **첨부 파일 가져오기** 옵션을 ON으로 설정한 후 장치에 다운로드한 모든 작업을 수행할 수 있습니다.

## AEM Forms 앱에 대한 오프라인 서비스 구성 {#configuring-offline-service-for-aem-forms-app-br}

AEM Forms 앱 오프라인 서비스는 양식에 사용된 리소스를 식별합니다. AEM Forms 앱은 이 서비스를 사용하여 양식 의존성에 대한 정보를 얻습니다. 오프라인 기능을 활성화하려면 양식 종속성에 대한 정보가 필요합니다. AEM Forms 앱 오프라인 서비스는 양식에 사용된 리소스의 경로 또는 URL을 캐시합니다. 양식의 변경 사항과 오프라인 서비스에 대해 구성된 유효 기간에 따라 캐시가 업데이트됩니다. 양식에 사용된 리소스의 경로 또는 URL을 캐시하면 서버측 성능이 향상됩니다.

AEM Forms 앱의 서버측 오프라인 구성 요소를 구성하려면 다음을 수행하십시오.

1. 작성자 인스턴스에서 **Adobe Experience Manager** >**도구** > **Forms** > **Forms 앱 오프라인 서비스 구성**&#x200B;으로 이동합니다.

   URL: `https://<server>:<port>/<context-path>/libs/fd/workspace-offline/gui/content/config.html`

1. 일반 설정에서 다음을 수행할 수 있습니다.

   * **캐시 지우기**: 양식 종속 항목의 서버측 캐시를 지웁니다.
   * **구성 재설정**: AEM Forms 앱 오프라인 구성을 재설정합니다.
   * **캐시 유효성**: 서버측 오프라인 캐시의 유효 기간을 지정합니다.
   * **리소스 감시 경로**: 오프라인 서비스가 리소스 변경을 모니터링하는 경로를 지정합니다. 지정된 경로에 변경 사항이 있으면 모든 종속 양식의 오프라인 캐시가 업데이트됩니다. 예: `/etc/clientlibs/fd,/content/dam/images`

1. **수동 리소스 캐시** 탭에서 오프라인 서비스에서 식별할 수 없는 양식 종속성을 지정합니다. JavaScript 내에서 로드된 이미지와 같은 리소스를 지정할 수 있습니다. AEM Forms 앱은 오프라인 모드에 대해서도 이러한 리소스를 다운로드합니다.
