---
title: 기본 제공 앱 핸들러
description: AEM을 사용하는 Adobe PhoneGap Enterprise의 기본 핸들러에 대해 알려면 이 페이지를 따르십시오.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: e2ddf5d1-0f5b-4f3b-9666-0f388915730e
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '1387'
ht-degree: 0%

---

# 기본 제공 앱 핸들러{#out-of-the-box-app-handlers}

{{ue-over-mobile}}

Content Sync Handler 개발에 대한 다음 지침을 참조하십시오.

* 처리기는 *com.day.cq.contentsync.handler.ContentUpdateHandler*&#x200B;을(를) 구현하거나 이 작업을 수행하는 클래스를 확장해야 합니다.
* 처리기는 *com.adobe.cq.mobile.platform.impl.contentsync.handler.AbstractSlingResourceUpdateHandler*&#x200B;를 확장할 수 있습니다.
* 처리기는 ContentSync 캐시를 업데이트한 경우에만 true를 보고해야 합니다. true를 잘못 보고하면 AEM에서 업데이트를 만들 수 있습니다.
* 처리기는 콘텐츠가 실제로 변경된 경우에만 캐시를 업데이트해야 합니다. 흰색이 필요하지 않은 경우 캐시에 쓰지 말고 불필요한 업데이트를 만들지 마십시오.

## 기본 제공 핸들러 {#out-of-the-box-handlers}

다음은 기본 제공 앱 핸들러를 나열한 것입니다.

**mobileapppages** 앱 페이지를 렌더링합니다.

* ***type - String*** - mobileapppages
* ***경로 - 문자열*** - 페이지 경로
* ***확장 - 문자열*** - 요청에 사용해야 하는 확장. 페이지의 경우 거의 항상 *html*&#x200B;이지만 다른 항목은 가능합니다.

* ***선택기 - 문자열*** - 점으로 구분된 선택적 선택기입니다. 페이지의 모바일 버전을 렌더링하기 위한 일반적인 예로는 *touch*&#x200B;가 있습니다.

* ***딥 - 부울*** - 하위 페이지도 포함해야 하는지 여부를 결정하는 선택적 부울 속성입니다. 기본값은 *true.*&#x200B;입니다.

* ***includeImages - 부울*** - 이미지를 포함해야 하는지 여부를 결정하는 선택적 부울 속성. 기본값은 *true*&#x200B;입니다.

   * 기본적으로 기본/구성 요소/이미지 리소스 유형의 이미지 구성 요소만 포함할 것으로 간주됩니다.

* ***includeVideos - 부울*** - 선택적 부울 속성은 비디오가 포함되어야 하는지 여부를 결정합니다. 기본값은 *true*&#x200B;입니다.

* ***includeModifiedPagesOnly - 부울*** - false이거나 생략하면 모든 페이지를 렌더링하고 렌더링 시 업데이트를 확인합니다. true이면 lastModified 페이지의 변경 내용에 따라 달라집니다.
* ***+ 다시 작성(노드)***
  ***- relativeParentPath - String*** - 다른 모든 경로를 상대적으로 쓰는 경로.

>[!NOTE]
>
>이 처리기의 영향을 받는 이미지 및 비디오 구성 요소의 리소스 유형은 *com.adobe.cq.mobile.platform.impl.contentsync.handler*&#x200B;의 속성을 구성하여 설정합니다.*MobilePagesUpdateHandler OSGi 서비스*.

**mobilepageassets** 앱 페이지 자산을 수집합니다.

**mobilecontentlisting** ContentSync zip의 콘텐츠를 나열합니다. 이는 장치의 클라이언트측 js에서 AEM 앱에 필요한 초기 파일 복사를 수행하는 데 사용됩니다.

이 처리기는 AEM Apps ContentSync 구성에 추가해야 합니다.

* ***type - 문자열 - mobilecontentlisting***
* ***경로*** - 문자열 - 빈 상태로 유지해야 올바른 처리기로 표시되지만 경로가 현재 ContentSync 캐시로 유추됩니다. 이 값은 무시됩니다.
* ***targetRootDirectory* -**문자열 - 이 처리기의 콘텐츠 업데이트에 대한 대상 루트로 경로에 추가할 접두사입니다.
* ContentSync에서 이 처리기를 실행하려면 ***순서 - Long* -**순서를 지정합니다. 이 숫자는 100과 같은 다른 모든 처리기보다 높게 설정해야 합니다. 기존 콘텐츠 핸들러 다음에 실행해야 합니다.

```xml
{
  "files": [
    "config.xml",
    "res/screens/ios/screen-ipad-portrait-2x.png",
    "res/screens/ios/screen-ipad-landscape.png",
    "res/screens/ios/screen-iphone-portrait-2x.png",
    "res/screens/ios/screen-iphone-landscape.png",
    "res/screens/ios/screen-iphone-portrait.png",
    "apps/weretail-app/components/splash-page/clientlibs.css",
    ...
    "pge-content-packages.json"
  ],
  "count": 382,
  "lastModified": 1422902754733
}
```

**mobilecontentpackagelistening** 지정된 앱에 있는 AEM 콘텐츠 패키지와 업데이트 요청을 할 serverURL을 나열합니다. 이는 장치의 클라이언트측 js를 사용하여 콘텐츠 업데이트를 요청합니다

핸들러는 AEM 앱 셸 ContentSync 구성(pge-type=app-instance를 사용하는 노드)에서 사용해야 합니다.

* ***type - 문자열 - mobilecontentpackagelistening***
* ***경로&#x200B;**-**문자열*** - 앱 셸의 경로(페이지 유형=app-instance인 노드).
* ***targetRootDirectory - 문자열*** - 이 처리기의 콘텐츠 업데이트에 대한 대상 루트로 경로에 추가할 접두사입니다.
* ***순서 - Long* -**ContentSync에서 이 처리기를 실행하는 순서. 이 숫자는 100과 같은 다른 모든 처리기보다 높게 설정해야 합니다. 기존 콘텐츠 핸들러 다음에 실행해야 합니다.

>[!NOTE]
>
>다음 코드 블록은 정확한 구현이 아니므로 참조 예제로 사용해야 합니다.

```xml
{
  "content": [
    {
      "name": "en",
      "title": "We Retail Mobile App - English",
      "type": "CONTENT",
      "path": "/content/phonegap/weretail-outdoors/en",
      "updatePath": "/content/phonegap/weretail/en/jcr:content/pge-app/app-config"
    },
    {
      "name": "shell",
      "title": "We Retail Mobile App",
      "type": "INSTANCE",
      "path": "/content/phonegap/weretail-outdoors/shell",
      "updatePath": "/content/phonegap/weretail/shell/jcr:content/pge-app/app-config"
    }
  ],
  "serverURL": "http://localhost:4503/"
}
```

**widgetconfig** 명령 센터를 통해 편집한 내용을 제공된 config.xml과 병합하는 업데이트된 config.xml이 포함되어 있습니다. 이 처리기가 포함되어 있지 않으면 관리 인터페이스를 통해 변경된 앱 세부 사항이 캐시에 포함되지 않습니다.

이 처리기는 AEM 앱 셸 ContentSync 구성(페이지 유형=[앱 인스턴스]인 노드)에서 사용해야 합니다.

* ***type - String* - **widgetconfig
* ***경로&#x200B;**-**문자열*** - 모든 앱 셸 하위 노드의 경로(pge-type=[app-instance]인 노드).
* ***targetRootDirectory - 문자열*** - 이 처리기의 콘텐츠 업데이트에 대한 대상 루트로 경로에 추가할 접두사입니다.
* ***targetIconDirectory - 문자열*** - 앱의 아이콘을 배치할 디렉터리입니다.

**mobileADBMobileConfigJSON** AMS cloudservice가 구성된 경우 ADBMobileConfig.JSON 파일을 포함합니다.

컴파일 타임에 분석 지원을 위해 AMS 플러그인을 구성하는 데 사용됩니다.

핸들러는 AEM 앱 셸 ContentSync 구성(pge-type=app-instance를 사용하는 노드)에서 사용해야 합니다.

* ***유형 - 문자열*** - mobileADBMobileConfigJSON
* ***경로 - 문자열*** - 앱 셸의 경로(pge-type=app-instance가 있는 노드 또는 /libs/mobileapps/core/components/instance를 확장하는 RT)
* ***targetRootDirectory - 문자열*** - 이 처리기의 콘텐츠 업데이트에 대한 대상 루트로 경로에 추가할 접두사입니다.

**notificationsconfig** 장치에서 필요한 알림 구성을 추출합니다. 속성은 앱과 연결된 각 푸시 서비스 클라우드 서비스 구성에서 추출됩니다.

클라우드 서비스의 jcr:content 노드에서 비 AEM 속성이 추출되고 앱 컨텐츠의 www 루트에 포함할 **pge-notifications-config.json** JSON 파일에 추가됩니다.

AEM 속성은 &quot;cq&quot;, &quot;sling&quot; 또는 &quot;jcr&quot;로 이름이 지정된 속성입니다. content-sync 구성 노드에서 &quot;excludeProperties&quot; 속성을 사용하여 다른 속성을 제외할 수 있습니다.

* ***유형 - 문자열*** - notificationsconfig
* ***excludeProperties - 문자열[]*** - 제외할 속성

**contentsyncconfigcontent** 기존 ContentSync 구성에서 콘텐츠를 수집합니다.

* ***유형 - 문자열*** - contentsyncconfigcontent
* ***경로 - 문자열*** - 다음 중 하나의 경로:

   * 다른 ContentSync 구성
   * 콘텐츠 패키지(phonegap-exportTemplate 속성을 사용하여 ContentSync 구성 찾기)
   * 모바일 리소스(app-content의 는 해당 리소스 아래에 있으며, 해당 콘텐츠 패키지에 true인 pge-includeInBuild 속성이 있는 경우 phonegap-exportTemplate을 사용하여 ContentSync 구성을 찾습니다.)

* ***autoCreateFirstUpdateBeforeImport - 부울*** - true인 경우 한 번 존재하지 않는 경우 가져오기 전에 대상 구성에서 초기 **업데이트**&#x200B;를 만드십시오

* ***autoFillBeforeImport - 부울*** - true인 경우 가져오기 전에 대상 구성을 업데이트/채우십시오
* ***configSuffix - String*** - app-content의 &quot;phonegap-exportTemplate&quot; 속성에 표시된 경로에 추가하는 문자열. 서로 다른 내보내기 템플릿을 구분하는 데 사용할 수 있습니다. 예를 들어 *&quot;/../.././appconfig-dev&quot;*&#x200B;을(를) 사용해야 함을 나타내기 위해 이 속성을 **&quot;-dev&quot;**(으)로 설정할 수 있습니다(*&quot;/.././../appconfig&quot;* 대신).

**app-assets** 앱 인스턴스와 연결된 모든 자산을 포함합니다. 이 처리기에는 앱 인스턴스의 appAssetPath 속성에서 참조하는 자산과 함께 지정된 경로 아래에 있는 모든 자산이 포함됩니다.

* ***유형 - 문자열*** - app-assets

* ***경로&#x200B;**-**문자열*** - 앱 에셋이 저장되는 앱 인스턴스 아래의 위치에 대한 경로

**mobileappoffers** 타깃팅된 콘텐츠를 렌더링하기 위해 Personalization 사용 사례에 새로운 콘텐츠 동기화 처리기가 도입되었습니다. &#39;mobileappoffers&#39; 처리기는 콘텐츠 작성자가 만든 연결된 대상 오퍼를 렌더링하는 방법을 알고 있습니다. mobileappoffers 처리기는 추상 페이지 업데이트 처리기를 확장하므로 많은 속성이 유사합니다. mobileappoffers 처리기의 세부 정보에는 다음 속성이 있습니다.

mobileappsoffers 처리기는 mobileappspages 처리기를 확장하고 다음 속성을 추가합니다.

* ***locationRoot - 문자열*** - 모바일 응용 프로그램의 위치를 지정합니다.
* ***includePageTypes - String*** - cq/personalization/components/teaserpage 및 cq/personalization/components/offerproxy를 지원하는 기본값입니다.
* ***선택기 - 문자열*** - tandt로 설정해야 함
* ***경로 - 문자열*** - 캠페인 브랜드의 경로

**mobileappconfig** mobileappconfig 콘텐츠 동기화 처리기는 MobileAppsConfig.json에 JSON 데이터를 삽입하는 방법을 제공합니다. 공급자 클래스를 등록하려면 개발자가 공급자 목록에 MobileAppsInfoProvider 클래스를 추가합니다. 처리기는 MobileAppsInfoProviders 목록을 반복하고 공급자가 결과 json 파일에 데이터를 삽입할 수 있도록 합니다. 이 핸들러가 지원하는 속성 목록은 다음과 같습니다.

* ***경로&#x200B;**-**문자열*** - pge-type=app-instance 또는 /libs/mobileapps/core/components/instance를 확장하는 RT가 있는 앱 인스턴스 노드의 경로
* ***공급자 - 문자열*** `[]` - 정규화된 MobileAppsInfoProviders 목록
* ***targetRootDirectory - String*** - MobileAppsConfig.json 파일을 쓸 디렉터리.
* **fileName - 문자열** - JSON을 작성할 파일의 선택적 이름으로, 기본값은 MobileAppsConfig.json입니다.

각각 다른 JSON 파일에 쓰는 고유한 공급자 집합으로 여러 mobileappconfig 처리기를 구성할 수 있습니다.

### 콘텐츠 동기화 핸들러 테스트 {#testing-content-sync-handlers}

**무결성 검사 단계** 캐시 지우기

* 캐시 지우기
* 핸들러 실행(캐시 업데이트됨)
* 핸들러를 다시 실행합니다(캐시는 업데이트되지 않음).

**디버깅 단계**

* 구성 실행
* 장치에서 구성 또는 검토 내보내기
* 렌더링이 실패하면 *styles/assets/libs*&#x200B;이(가) 누락되었는지 확인하거나 *styles/assets/libs*&#x200B;에 대한 잘못된 경로를 확인하십시오

**로깅** 패키지 `com.day.cq.contentsync`에서 OSGI 로거 구성을 통해 ContentSync 디버그 로깅을 사용하도록 설정합니다. 이렇게 하면 실행된 처리기와 캐시가 업데이트되고 캐시 업데이트가 보고되었는지 여부를 추적할 수 있습니다.

## 추가 리소스 {#additional-resources}

관리자 및 개발자의 역할과 책임에 대해 알아보려면 아래 리소스를 참조하십시오.

* [AEM을 사용하여 Adobe PhoneGap Enterprise용 작성](/help/mobile/phonegap.md)
* [AEM을 사용하여 Adobe PhoneGap Enterprise용 컨텐츠 관리](/help/mobile/administer-phonegap.md)

>[!NOTE]
>
>AEM Mobile 앱 개발을 시작하려면 [여기](/help/mobile/getting-started-aem-mobile.md)를 클릭하세요.
