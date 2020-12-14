---
title: 즉시 사용 가능한 앱 핸들러
seo-title: 즉시 사용 가능한 앱 핸들러
description: AEM을 사용하는 Adobe PhoneGap Enterprise의 핸들러에 대해 알아보려면 이 페이지를 따르십시오.
seo-description: AEM을 사용하는 Adobe PhoneGap Enterprise의 핸들러에 대해 알아보려면 이 페이지를 따르십시오.
uuid: 436038cb-fb76-4bb5-ae79-5d4043b81dd9
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: fec86f03-f81e-460a-9f84-d6304c95128c
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1430'
ht-degree: 0%

---


# 박스 앱 핸들러{#out-of-the-box-app-handlers}

>[!NOTE]
>
>단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: 응답)이 필요한 프로젝트에는 SPA 편집기를 사용하는 것이 좋습니다. [추가 정보](/help/sites-developing/spa-overview.md).

콘텐츠 동기화 핸들러를 개발하기 위한 다음 지침을 참조하십시오.

* 핸들러는 *com.day.cq.contentsync.handler.ContentUpdateHandler*(직접 또는 해당 클래스를 확장해야 함)
* 핸들러는 *com.adobe.cq.mobile.platform.impl.contentsync.handler.AbstractSlingResourceUpdateHandler*
* 처리기는 ContentSync 캐시를 업데이트한 경우에만 true를 보고해야 합니다. 거짓으로 보고하면 AEM에서 업데이트를 만들 수 있습니다.
* 핸들러는 컨텐츠가 실제로 변경된 경우에만 캐시를 업데이트해야 합니다. 흰색이 필요하지 않고 불필요한 업데이트를 만들지 않는 경우 캐시에 쓰지 마십시오.

## 박스 핸들러 {#out-of-the-box-handlers}

다음은 바로 사용 가능한 앱 핸들러에 대한 목록입니다.

**mobileapppages** 앱 페이지를 렌더링합니다.

* ***type - String*** - mobileapppages
* ***경로 - 문자열***  - 페이지의 경로
* ***확장 - 문자열***  - 요청에 사용해야 하는 확장입니다. 페이지의 경우 거의 항상 *html*&#x200B;이지만 다른 페이지는 여전히 사용할 수 있습니다.

* ***선택기 - 문자열***  - 선택적인 선택기는 점으로 구분됩니다. 일반적인 예는 페이지의 모바일 버전을 렌더링하기 위한 *touch*&#x200B;입니다.

* ***deep - 부울***  - 하위 페이지를 포함해야 하는지 여부를 확인하는 선택적 부울 속성입니다. 기본값은 *true입니다.*

* ***includeImages - Boolean***  - 이미지를 포함해야 하는지 여부를 결정하는 선택적 부울 속성입니다. 기본값은 *true*&#x200B;입니다.

   * 기본적으로 리소스 유형의 foundation/components/image가 있는 이미지 구성 요소만 포함으로 간주됩니다.

* ***includeVideos - Boolean***  - 선택적 부울 속성으로 비디오가 포함되어야 하는지 결정할 수 있습니다. 기본값은 *true*&#x200B;입니다.

* ***includeModifiedPagesOnly - Boolean*** - false 또는 생략된 경우 모든 페이지를 렌더링하고 렌더링에서 업데이트를 확인합니다. true인 경우 마지막 수정됨 페이지의 변경 사항에 따라 다릅니다.
* ***+ 다시 작성(노드)***
   ***- relativeParentPath - String***  - 관련된 다른 모든 경로를 기록할 경로입니다.

>[!NOTE]
>
>이 핸들러의 영향을 받는 이미지 및 비디오 구성 요소의 리소스 유형은 *com.adobe.cq.mobile.platform.impl.contentsync.handler*&#x200B;의 속성을 구성하여 설정됩니다.*MobilePagesUpdateHandler OSGi 서비스*.

**mobilepageassets** 앱 페이지 자산을 수집합니다.

**mobilecontentlists** ContentSync zip의 콘텐트를 나열합니다. 장치의 클라이언트측 js에서 AEM 앱에 필요한 초기 파일 복사를 수행하는 데 사용됩니다.

이 핸들러는 모든 AEM Apps ContentSync 구성에 추가해야 합니다.

* ***type - String - mobilecontentlisting***
* ***path*** - String - keep empty가 있어야 유효한 핸들러로 표시되지만 경로를 현재 ContentSync 캐시로 유추할 수 있습니다. 이 값은 무시됩니다.
* ***targetRootDirectory* -**String - 이 핸들러의 컨텐츠 업데이트에 대한 대상 루트로 경로에 추가할 접두사입니다.
* ***순서 - ContentSync* 가 **이 핸들러를 실행할 수 있는 긴 주문입니다. 이 숫자는 100과 같은 다른 모든 핸들러보다 높게 설정해야 합니다. 기존 컨텐츠 핸들러 이후에 실행되어야 합니다.

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

**mobilecontentpackageslisting** 업데이트 요청을 할 serverURL과 지정된 앱의 AEM 콘텐츠 패키지를 나열합니다. 장치의 클라이언트측 js를 사용하여 내용 업데이트를 요청합니다

처리기는 AEM App Shell ContentSync 구성(page-type=app-instance가 있는 노드)에서 사용해야 합니다.

* ***type - String - mobilecontentpackageslisting***
* ***path **-**String*** - 앱 셸에 대한 경로(page-type=app-instance가 있는 노드)
* ***targetRootDirectory - 문자열***  - 이 핸들러의 컨텐츠 업데이트에 대한 대상 루트로 경로에 추가할 접두사입니다.
* ***순서 - ContentSync* 가 **이 핸들러를 실행하려면 긴 순서가 필요합니다. 이 숫자는 100과 같은 다른 모든 핸들러보다 높게 설정해야 합니다. 기존 컨텐츠 핸들러 이후에 실행되어야 합니다.

>[!NOTE]
>
>다음 코드 블록은 정확한 구현이 아니며 참조 예로 사용해야 합니다.

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

**widgetconfig** 명령 센터를 통해 수행한 모든 편집 내용을 제공된 config.xml과 병합하는 업데이트된 config.xml을 포함합니다. 이 처리기가 관리 인터페이스를 통해 변경된 앱 세부 사항을 포함하지 않는 경우 캐시에 포함되지 않습니다.

이 핸들러는 AEM App Shell ContentSync 구성(page-type=[app-instance]인 노드)에서 사용해야 합니다.

* ***type - 문자열* - **widgetconfig
* ***path **-**String*** - 모든 앱 셸 하위 노드의 경로(page-type=[app-instance]가 있는 노드)입니다.
* ***targetRootDirectory - 문자열***  - 이 핸들러의 컨텐츠 업데이트에 대한 대상 루트로 경로에 추가할 접두사입니다.
* ***targetIconDirectory - 문자열***  - 앱용 아이콘을 배치할 디렉토리

**** mobileADBMobileConfigJSONIAMS cloudservice가 구성된 경우 ADBMobileConfig.JSON 파일을 포함합니다.

분석 지원을 위해 AMS 플러그인을 구성하는 데 컴파일 타임에 사용됩니다.

처리기는 AEM App Shell ContentSync 구성(page-type=app-instance가 있는 노드)에서 사용해야 합니다.

* ***type - String*** - mobileADBMobileConfigJSON
* ***경로 - 문자열***  - 앱 셸에 대한 경로(pge-type=app-instance가 있는 노드 또는 /libs/mobileapps/core/components/instance를 확장하는 RT 포함)
* ***targetRootDirectory - 문자열***  - 이 핸들러의 컨텐츠 업데이트에 대한 대상 루트로 경로에 추가할 접두사입니다.

**notificationconfig** 장치에서 필요한 알림 구성을 추출합니다. 속성은 앱과 연관된 각 푸시 서비스 클라우드 서비스 구성에서 추출됩니다.

클라우드 서비스의 jcr:content 노드에 있는 AEM이 아닌 속성은 추출되어 앱 컨텐츠의 www 루트에 포함할 수 있도록 **page-notifications-config.json** JSON 파일에 추가됩니다.

AEM 속성은 &quot;cq&quot;, &quot;sling&quot; 또는 &quot;jcr&quot;로 네임스페이스가 지정된 속성입니다. 기타 속성은 content-sync 구성 노드에서 &quot;excludeProperties&quot; 속성을 사용하여 제외할 수 있습니다.

* ***type - String*** - notificationconfig
* ***excludeProperties - 제외할[]***  String-속성

**contentsyncconfigcontent** 기존 ContentSync 구성에서 컨텐츠를 수집합니다.

* ***type - String*** - contentsyncconfigcontent
* ***경로 - 문자열***  - 다음 중 하나에 대한 경로입니다.

   * 다른 ContentSync 구성
   * 컨텐츠 패키지로 전환(phonegap-exportTemplate 속성을 사용하여 ContentSync 구성 찾기)
   * 모바일 리소스(app-content는 해당 리소스 아래에서 발견되며, 해당 컨텐츠 패키지에 true인 page-includeInBuild 속성이 있으면 phonegap-exportTemplate을 사용하여 ContentSync 구성을 찾습니다.)

* ***autoCreateFirstUpdateBeforeImport - Boolean*** - true인 경우, 한  **** 번 더 이상 존재하지 않으면 가져오기 전에 대상 구성에서 초기 업데이트를 만드십시오

* ***autoFillBeforeImport - Boolean*** - true이면 가져오기 전에 대상 구성을 업데이트/채웁니다.
* ***configSuffix - String***  - app-content의 &quot;phonegap-exportTemplate&quot; 속성에 지정된 경로에 추가할 문자열입니다. 다른 내보내기 템플릿을 구분하는 데 사용할 수 있습니다. 예를 들어 이 속성을 **&quot;-dev&quot;**&#x200B;로 설정하여 *&quot;/././../appconfig-dev&quot;*(예: *&quot;/../../../appconfig&quot;*&#x200B;와는 반대)를 나타낼 수 있습니다.

**app-** assets앱 인스턴스와 연결된 모든 자산을 포함합니다. 이 핸들러는 앱 인스턴스의 appAssetPath 속성이 참조하는 모든 자산과 함께 지정된 경로 아래에 있는 모든 자산을 포함합니다.

* ***type - String*** - app-assets

* ***경로&#x200B;**-**문자열***  - 앱 에셋이 저장되는 앱 인스턴스 아래의 위치에 대한 경로

**mobileappoffers** 타깃팅된 컨텐츠를 렌더링하기 위해 개인화 사용 사례에 대한 새로운 컨텐츠 동기화 핸들러가 도입되었습니다. &#39;mobileappoffers&#39; 핸들러는 컨텐츠 작성자가 만든 관련 대상 오퍼를 렌더링하는 방법을 알고 있습니다. mobileappoffer 핸들러는 추상 페이지 업데이트 핸들러를 확장하므로 대부분의 속성이 유사합니다. mobileappoffer 핸들러의 세부 사항에는 다음 속성이 있습니다.

mobileappsoffers 핸들러는 mobileappspages 핸들러를 내보내고 다음 속성을 추가합니다.

* ***locationRoot - String***  - 모바일 응용 프로그램의 위치를 지정합니다.
* ***includePageTypes - String***  - cq/personalization/components/teaserpage 및 cq/personalization/components/offerproxy를 지원하는 기본값
* ***선택기 - 문자열***  - tandt로 설정해야 합니다.
* ***경로 - 문자열*** - 캠페인 브랜드의 경로

**mobileappconfig** mobileappconfig 콘텐츠 동기화 핸들러는 JSON 데이터를 MobileAppsConfig.json에 주입하는 방법을 제공합니다. 공급자 클래스 개발자를 등록하려면 MobileAppsInfoProvider 클래스를 공급자 목록에 추가합니다. 핸들러는 MobileAppsInfoProviders 목록을 반복하고 공급자가 결과 json 파일에 데이터를 삽입할 수 있도록 허용합니다. 이 처리기가 지원하는 속성 목록은 다음과 같습니다.

* ***path **-***** String- pge-type=app-instance 또는 /libs/mobileapps/core/components/instance를 확장하는 RT가 있는 앱 인스턴스 노드의 경로입니다.
* ***providers - 문자열*** `[]`  - 정규화된 MobileAppsInfoProviders 목록
* ***targetRootDirectory - 문자열***  - MobileAppsConfig.json 파일을 작성할 디렉토리.
* **fileName - 문자열**  - JSON을 다음으로 기록할 파일의 선택적 이름, 기본값은 MobileAppsConfig.json입니다.

여러 개의 mobileappconfig 핸들러가 각기 다른 JSON 파일에 쓰는 고유한 공급자 세트로 구성되어 있을 수 있습니다.

### 컨텐츠 동기화 핸들러 테스트 중 {#testing-content-sync-handlers}

**Integrity캐시** 지우기 단계

* 캐시 지우기
* 핸들러 실행(캐시 업데이트됨)
* 핸들러를 다시 실행합니다(캐시를 업데이트할 수 없음).

**디버깅 단계**

* 구성 실행
* 구성 내보내기 또는 디바이스에서 검토
* 렌더링에 실패하는 경우 누락된 *styles/assets/libs*&#x200B;을 확인하거나 *styles/assets/libs*&#x200B;에 대한 잘못된 경로를 확인하십시오.

**로깅** 패키지의 OSGI 로거 구성을 통해 ContentSync 디버그 로깅 활성화  `com.day.cq.contentsync` 그러면 실행된 핸들러와 캐시를 업데이트했는지 그리고 캐시 업데이트를 보고했는지 여부를 추적할 수 있습니다.

## 추가 리소스 {#additional-resources}

관리자 및 개발자의 역할 및 책임을 살펴보려면 아래 리소스를 참조하십시오.

* [AEM을 사용한 Adobe PhoneGap Enterprise 저작](/help/mobile/phonegap.md)
* [AEM에서 Adobe PhoneGap Enterprise용 컨텐츠 관리](/help/mobile/administer-phonegap.md)

>[!NOTE]
>
>AEM Mobile 앱 개발을 시작하려면 [여기](/help/mobile/getting-started-aem-mobile.md)를 클릭하십시오.

