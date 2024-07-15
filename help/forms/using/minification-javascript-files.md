---
title: JavaScript 파일 축소
description: 웹용 JS 파일을 최적화하기 위해 AEM Forms 작업 공간 사용자 지정 후 축소된 코드를 생성하는 지침입니다.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: d88c6831-8ae9-426d-acb5-2a7e066ad158
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 1%

---

# JavaScript 파일 축소 {#minification-of-the-javascript-files}

축소하면 소스 코드에서 공백, 새 줄 및 설명과 같은 중복 문자가 제거됩니다. 이렇게 하면 코드 크기를 줄여 성능이 향상됩니다. 축소는 기능에 영향을 주지 않지만 코드의 가독성을 낮춥니다.

의미 체계 변경에 대해 축소된 코드를 생성하려면 다음 단계를 수행합니다.

1. 파일 시스템의 src-package에서 `client-html/src/main/webapp/js` 복사

   >[!NOTE]
   >
   >패키지에 대한 자세한 내용은 [AEM Forms 작업 영역 사용자 지정 소개](/help/forms/using/introduction-customizing-html-workspace.md)를 참조하십시오.

1. 추가된/업데이트된 모델/보기에 대해 client-html/src/main/webapp/js 아래에 있는 `main.js`의 경로를 업데이트합니다.

   예를 들어, 새로운 Sharequeue 모델, 즉 mySharequeue를 추가하면 변경됩니다.

   ```javascript
   sharequeuemodel : pathprefix + 'runtime/models/sharequeue',
   ```

   끝

   ```javascript
   sharequeuemodel : pathprefix + 'runtime/myModels/mySharequeue',
   ```

1. `main.js`에 별칭이 변경/추가된 경우 `registry-config.xml, located at client-html/src/main/webapp/js/resource_generator,`을(를) 업데이트합니다.

   예를 들어, 새로운 Sharequeue 모델, 즉 mySharequeue를 추가하면 변경됩니다.

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
