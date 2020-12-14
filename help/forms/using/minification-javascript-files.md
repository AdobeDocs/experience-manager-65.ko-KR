---
title: JavaScript 파일 축소
seo-title: JavaScript 파일 축소
description: AEM Forms 작업 영역 사용자 정의 후 축소된 코드를 생성하여 웹용 JS 파일을 최적화하는 지침
seo-description: AEM Forms 작업 영역 사용자 정의 후 축소된 코드를 생성하여 웹용 JS 파일을 최적화하는 지침
uuid: ad91e380-a988-4740-9534-e09657e0322a
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: c88a3013-5da2-4b09-9f29-ac1fb00822ec
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---


# JavaScript 파일 축소{#minification-of-the-javascript-files}

분류는 소스 코드에서 공백, 새 줄 및 주석과 같은 중복 문자를 제거합니다. 이렇게 하면 코드 크기를 줄여 성능이 향상됩니다. 축소는 기능에 영향을 주지 않지만 코드의 가독성은 줄어듭니다.

의미 변경을 위한 축소 코드를 생성하려면 다음 단계를 수행합니다.

1. 파일 시스템의 src-package에서 `client-html/src/main/webapp/js`을(를) 복사합니다.

   >[!NOTE]
   >
   >패키지에 대한 자세한 내용은 [AEM Forms 작업 영역 사용자 정의 소개](/help/forms/using/introduction-customizing-html-workspace.md)를 참조하십시오.

1. 추가되거나 업데이트된 모델/보기에 대해 client-html/src/main/webapp/js 아래에 있는 `main.js`의 경로를 업데이트합니다.

   예를 들어 mySharequeue와 같이 새 Sharequeue 모델을 추가하면 다음과 같이 변경됩니다.

   ```javascript
   sharequeuemodel : pathprefix + 'runtime/models/sharequeue',
   ```

   끝

   ```javascript
   sharequeuemodel : pathprefix + 'runtime/myModels/mySharequeue',
   ```

1. `main.js`에 별칭이 변경/추가되는 경우 `registry-config.xml, located at client-html/src/main/webapp/js/resource_generator,`을(를) 업데이트합니다.

   예를 들어 mySharequeue와 같이 새 Sharequeue 모델을 추가하면 다음과 같이 변경됩니다.

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

1. client-html/src/main/webapp/js/minifier에서 명령을 실행합니다.

   ```shell
   mvn clean install
   ```

   client-html/src/main/webapp/js 아래에 minified-files 폴더(minified main.js 및 registry.js 포함)를 생성합니다.

>[!NOTE]
>
>Minification은 64비트 JVM에서만 작동합니다.

>[!NOTE]
>
>축소하는 경우 업그레이드에 영향을 줍니다.
