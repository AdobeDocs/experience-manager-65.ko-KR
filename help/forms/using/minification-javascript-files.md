---
title: JavaScript 파일 축소
seo-title: JavaScript 파일 축소
description: AEM Forms 작업 영역 사용자 지정 후 축소된 코드를 생성하여 웹용 JS 파일을 최적화하는 지침
seo-description: AEM Forms 작업 영역 사용자 지정 후 축소된 코드를 생성하여 웹용 JS 파일을 최적화하는 지침
uuid: ad91e380-a988-4740-9534-e09657e0322a
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: c88a3013-5da2-4b09-9f29-ac1fb00822ec
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# JavaScript 파일 축소 {#minification-of-the-javascript-files}

세부 사항은 소스 코드에서 공백, 새 줄 및 주석과 같은 중복 문자를 제거합니다. 이렇게 하면 코드 크기를 줄여 성능이 향상됩니다. 축소 기능은 기능에 영향을 주지 않지만 코드의 가독성은 줄어듭니다.

의미 변경을 위한 축소 코드를 생성하려면 다음 단계를 따르십시오.

1. 파일 시스템의 src-package `client-html/src/main/webapp/js` 에서 복사

   >[!NOTE]
   >
   >패키지에 [대한 자세한 내용은 AEM Forms 작업 영역](/help/forms/using/introduction-customizing-html-workspace.md) 사용자 지정 소개를 참조하십시오.

1. 추가/업데이트된 모델/보기에 대해 client-html/src/main/webapp/js 아래에 `main.js` 있는 경로를 업데이트합니다.

   예를 들어 mySharequeue와 같이 새 ShareQueue 모델을 추가하면 변경 사항이 적용됩니다.

   ```
   sharequeuemodel : pathprefix + 'runtime/models/sharequeue',
   
   To
   
   sharequeuemodel : pathprefix + 'runtime/myModels/mySharequeue',
   ```

1. 별칭이 변경/추가되는 `registry-config.xml, located at client-html/src/main/webapp/js/resource_generator,` 경우 업데이트합니다 `main.js`.

   예를 들어 mySharequeue와 같이 새 ShareQueue 모델을 추가하면 변경 사항이 적용됩니다.

   ```xml
   <sharequeue
               name="sharequeue"
               path="runtime/models/sharequeue.js"
               service="service"/>
   
   To
   
   <sharequeue
               name="sharequeue"
               path="runtime/myModels/mySharequeue.js"
               service="service"/>
   ```

1. client-html/src/main/webapp/js/minifier에서 명령을 실행합니다.

   ```shell
   mvn clean install
   ```

   client-html/src/main/webapp/js 아래에 미니화된 main.js 및 registry.js가 있는 폴더 미니화된 파일을 생성합니다.

>[!NOTE]
>
>Minification은 64비트 JVM에서만 작동합니다.

>[!NOTE]
>
>축소하는 경우 업그레이드에 영향을 줍니다.
