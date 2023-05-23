---
title: JavaScript 파일 축소
seo-title: Minification of the JavaScript files
description: 웹용 JS 파일을 최적화하기 위해 AEM Forms 작업 공간 사용자 지정 후 축소된 코드를 생성하는 지침입니다.
seo-description: Instructions to generate minified code after AEM Forms workspace customizations to optimize the JS files for the web.
uuid: ad91e380-a988-4740-9534-e09657e0322a
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: c88a3013-5da2-4b09-9f29-ac1fb00822ec
exl-id: d88c6831-8ae9-426d-acb5-2a7e066ad158
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 1%

---

# JavaScript 파일 축소 {#minification-of-the-javascript-files}

축소하면 소스 코드에서 공백, 새 줄 및 설명과 같은 중복 문자가 제거됩니다. 이렇게 하면 코드 크기를 줄여 성능이 향상됩니다. 축소는 기능에 영향을 주지 않지만 코드의 가독성을 낮춥니다.

의미 체계 변경에 대해 축소된 코드를 생성하려면 다음 단계를 수행하십시오.

1. 복사 `client-html/src/main/webapp/js` 파일 시스템의 src-package에서

   >[!NOTE]
   >
   >다음을 참조하십시오 [AEM Forms 작업 영역 사용자 정의 소개](/help/forms/using/introduction-customizing-html-workspace.md) 패키지를 참조하십시오.

1. 에서 경로 업데이트 `main.js` 추가된/업데이트된 모델/보기에 대해 client-html/src/main/webapp/js 아래에 있습니다.

   예를 들어, 새로운 Sharequeue 모델을 추가하면 즉, mySharequeue가 변경됩니다.

   ```javascript
   sharequeuemodel : pathprefix + 'runtime/models/sharequeue',
   ```

   끝

   ```javascript
   sharequeuemodel : pathprefix + 'runtime/myModels/mySharequeue',
   ```

1. 업데이트 `registry-config.xml, located at client-html/src/main/webapp/js/resource_generator,` 에 별칭이 변경/추가된 경우 `main.js`.

   예를 들어, 새로운 Sharequeue 모델을 추가하면 즉, mySharequeue가 변경됩니다.

   ```xml
   <sharequeue
               name="sharequeue"
               path="runtime/models/sharequeue.js"
               service="service"/>
   ```

   끝

   ```xml
   <sharequeue
               name="sharequeue"
               path="runtime/myModels/mySharequeue.js"
               service="service"/>
   ```

1. client-html/src/main/webapp/js/minifier에서 다음 명령을 실행합니다.

   ```shell
   mvn clean install
   ```

   축소된 main.js 및 registry.js를 사용하여 client-html/src/main/webapp/js 아래에 축소된 파일 폴더를 생성합니다.

>[!NOTE]
>
>축소는 64비트 JVM에서만 작동합니다.

>[!NOTE]
>
>축소하는 경우 업그레이드가 영향을 받습니다.
