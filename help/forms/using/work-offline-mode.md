---
title: 오프라인 모드에서 작업
seo-title: 오프라인 모드에서 작업
description: 모바일 디바이스를 AEM Forms 네트워크 범위 외부 또는 오프라인 모드에서 오프라인으로 전환하고 AEM Forms 앱에서 작업
seo-description: 모바일 디바이스를 AEM Forms 네트워크 범위 외부 또는 오프라인 모드에서 오프라인으로 전환하고 AEM Forms 앱에서 작업
uuid: b900a0f8-90ce-486a-bde6-6cdf11bd2801
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 9a3c6ab4-8bb9-40c7-8c56-59153b364887
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 0%

---


# 오프라인 모드에서 작업 중 {#working-in-the-offline-mode}

AEM Forms 앱의 오프라인 모드를 사용하면 앱이 오프라인 상태에 있더라도 매끄럽게 작업할 수 있습니다. 네트워크를 연결하지 않고도 양식을 열고 업데이트 및 제출할 수 있습니다.

앱을 AEM Forms 서버와 동기화하여 AEM Forms 앱에서 작업을 시작합니다. 본인에게 할당된 모든 양식이 앱에 다운로드됩니다. JEE의 AEM Forms의 경우 작업은 [작업] 탭에서 가져온 후 Forms 탭에서 연결된 양식 및 기타 양식을 시작점으로 가져올 수 있습니다. OSGi 기반의 AEM Forms의 경우 Forms만 Forms 탭에 로드됩니다.

앱 동기화 방법에 대한 자세한 내용은 [앱 동기화](/help/forms/using/sync-app.md)를 참조하십시오.

## Forms을 오프라인으로 사용 가능하게 만들기 {#making-forms-available-offline}

앱을 AEM Forms 서버와 동기화하면 모바일 장치에 양식이 다운로드됩니다. 그러나 기본적으로 양식과 관련된 첨부 파일은 다운로드되지 않습니다. 이는 온라인일 경우 첨부 파일을 볼 수 있음을 의미합니다. 그러나 오프라인 모드에서 첨부 파일을 볼 수 있도록 앱에서 기본 설정을 변경하십시오.

연관된 첨부 파일이 각 양식과 함께 다운로드되도록 하려면 첨부 파일 가져오기를 ON으로 설정합니다. 자세한 내용은 [일반 설정 업데이트](/help/forms/using/update-general-settings.md)를 참조하십시오.

모바일 장치에서 데이터를 다운로드하면 장치의 성능에 영향을 줄 수 있으므로 기본적으로 첨부 파일 가져오기 설정이 OFF로 설정됩니다. 설정이 켜짐으로 업데이트된 후 서버에서 다운로드한 모든 작업에 대해 첨부 파일을 장치로 가져옵니다. 오프라인 모드에서 사용자는 **첨부 파일 가져오기** 옵션을 ON으로 설정한 후 장치에 다운로드한 모든 작업을 수행할 수 있습니다.

## AEM Forms 앱 {#configuring-offline-service-for-aem-forms-app-br}에 대한 오프라인 서비스 구성

AEM Forms 앱 오프라인 서비스는 양식에 사용된 리소스를 식별합니다. AEM Forms 앱은 이 서비스를 사용하여 양식 종속성에 대한 정보를 가져옵니다. 오프라인 기능을 활성화하려면 양식 종속성 정보가 필요합니다. AEM Forms 앱 오프라인 서비스는 양식에 사용된 리소스의 경로 또는 URL을 캐시합니다. 캐시는 양식의 변경 사항 및 오프라인 서비스에 대해 구성된 유효 기간에 따라 업데이트됩니다. 양식에서 사용되는 리소스의 경로 또는 URL을 캐시하면 서버측 성능이 향상됩니다.

AEM Forms 앱의 서버측 오프라인 구성 요소를 구성하려면:

1. 작성자 인스턴스에서 **Adobe Experience Manager** >**도구** > **Forms** > **Forms App Offline 서비스 구성**&#x200B;으로 이동합니다.

   URL: `https://<server>:<port>/<context-path>/libs/fd/workspace-offline/gui/content/config.html`

1. 일반 설정에서 다음을 수행할 수 있습니다.

   * **캐시 지우기**:양식 종속성의 서버측 캐시를 지웁니다.
   * **구성 재설정**:AEM Forms 앱 오프라인 구성을 재설정합니다.
   * **캐시 유효성**:서버측 오프라인 캐시에 대한 유효 기간을 지정합니다.
   * **리소스 관찰 경로**:오프라인 서비스가 리소스 변경을 모니터하는 경로를 지정합니다. 지정된 경로에 변경 사항이 발생하면 모든 종속 양식의 오프라인 캐시가 업데이트됩니다. 예, `/etc/clientlibs/fd,/content/dam/images`.

1. **수동 리소스 캐시** 탭에서 오프라인 서비스를 식별할 수 없는 양식 종속성을 지정합니다. JavaScript 내에서 로드된 이미지와 같은 리소스를 지정할 수 있습니다. AEM Forms 앱은 이러한 리소스와 오프라인 모드를 다운로드합니다.
