---
title: UI 테스트
seo-title: Testing Your UI
description: AEM에서는 AEM UI에 대한 테스트를 자동화하는 프레임워크를 제공합니다
seo-description: AEM provides a framework for automating tests for your AEM UI
uuid: 408a60b5-cba9-4c9f-abd3-5c1fb5be1c50
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components, testing
discoiquuid: 938100ad-94f9-408a-819d-72657dc115f7
docset: aem65
exl-id: 2d28cee6-31b0-4288-bad3-4d2ecad7b626
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '737'
ht-degree: 3%

---

# UI 테스트{#testing-your-ui}

>[!NOTE]
>
>AEM 6.5 이상에서 hobbes.js UI 테스트 프레임워크는 더 이상 사용되지 않습니다. Adobe은 향후 Selenium 자동화를 개선할 계획이 없으며 고객이 Selenium 자동화를 사용할 것을 권장합니다.
>
>자세한 내용은 [사용이 중단되거나 제거된 기능](/help/release-notes/deprecated-removed-features.md).

AEM에서는 AEM UI에 대한 테스트를 자동화하는 프레임워크를 제공합니다. 프레임워크를 사용하면 웹 브라우저에서 직접 UI 테스트를 작성하고 실행할 수 있습니다. 프레임워크는 테스트 생성을 위한 Javascript API를 제공합니다.

AEM 테스트 프레임워크는 Javascript로 작성된 테스트 라이브러리인 Hobbes.js를 사용합니다. Hobbes.js 프레임워크는 개발 프로세스의 일부로 AEM을 테스트하기 위해 개발되었습니다. 이제 AEM 애플리케이션을 테스트하는 데 프레임워크를 공용 용도로 사용할 수 있습니다.

>[!NOTE]
>
>Hobbes.js 를 참조하십시오 [설명서](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/test-api/index.html) 를 참조하십시오.

## 테스트 구조 {#structure-of-tests}

AEM 내에서 자동화된 테스트를 사용할 때는 다음 용어를 이해하고 있어야 합니다.

| 작업 | An **작업** 는 링크 또는 단추 클릭과 같은 웹 페이지의 특정 활동입니다. |
|---|---|
| 테스트 사례 | A **테스트 사례** 은 하나 이상으로 구성될 수 있는 특정 상황입니다 **작업**. |
| 테스트 세트 | A **테스트 세트** 는 관련된 그룹입니다 **테스트 사례** 이렇게 하면 특정 사용 사례를 함께 테스트할 수 있습니다. |

## 테스트 실행 {#executing-tests}

### 테스트 세트 보기 {#viewing-test-suites}

테스트 콘솔을 열어 등록된 테스트 세트를 확인합니다. 테스트 패널에는 테스트 세트 및 해당 테스트 사례 목록이 포함되어 있습니다.

를 통해 도구 콘솔로 이동합니다 **전역 탐색 -> 도구 > 작업 -> 테스트**.

![chlimage_1-63](assets/chlimage_1-63.png)

콘솔을 열면 테스트 세트가 왼쪽과 함께 나열되며 이 모든 세트를 순차적으로 실행하는 옵션이 제공됩니다. 오른쪽에 체크된 배경과 함께 표시되는 공백은 테스트 실행 시 페이지 컨텐츠를 표시하기 위한 자리 표시자입니다.

![chlimage_1-64](assets/chlimage_1-64.png)

### 단일 테스트 세트 실행 {#running-a-single-test-suite}

테스트 세트는 개별적으로 실행할 수 있습니다. 테스트 세트를 실행하면 페이지가 테스트 사례 및 해당 작업이 실행되어 테스트가 완료된 후 결과가 나타납니다. 아이콘은 결과를 나타냅니다.

확인 표시 아이콘은 전달된 테스트를 나타냅니다.

![](do-not-localize/chlimage_1-2.png)

X 아이콘은 실패한 테스트를 나타냅니다.

![](do-not-localize/chlimage_1-3.png)

테스트 세트를 실행하려면

1. 테스트 패널에서 실행할 테스트 사례 이름을 클릭하거나 탭하여 작업의 세부 사항을 확장합니다.

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. 을 클릭하거나 탭합니다 **테스트 실행** 버튼을 클릭합니다.

   ![](do-not-localize/chlimage_1-4.png)

1. 테스트가 실행될 때 자리 표시자가 페이지 콘텐츠로 바뀝니다.

   ![chlimage_1-66](assets/chlimage_1-66.png)

1. 설명을 탭하거나 클릭하여 테스트 케이스 결과를 검토하여 **결과** 패널. 에서 테스트 사례 이름을 탭하거나 클릭합니다. **결과** 패널에 모든 세부 사항이 표시됩니다.

   ![chlimage_1-67](assets/chlimage_1-67.png)

### 여러 테스트 실행 {#running-multiple-tests}

테스트 세트는 콘솔에 표시되는 순서대로 실행됩니다. 테스트로 드릴다운하여 자세한 결과를 확인할 수 있습니다.

![chlimage_1-68](assets/chlimage_1-68.png)

1. 테스트 패널에서 **모든 테스트 실행** 버튼 또는 **테스트 실행** 단추를 클릭합니다.

   ![](do-not-localize/chlimage_1-5.png)

1. 각 테스트 케이스의 결과를 보려면 테스트 케이스의 제목을 탭하거나 클릭합니다. 에서 테스트 이름을 탭하거나 클릭합니다. **결과** 패널에 모든 세부 사항이 표시됩니다.

   ![chlimage_1-69](assets/chlimage_1-69.png)

## 간단한 테스트 세트 만들기 및 사용 {#creating-and-using-a-simple-test-suite}

다음 절차는 [We.Retail 컨텐츠](/help/sites-developing/we-retail.md)하지만 다른 웹 페이지를 사용하도록 테스트를 쉽게 수정할 수 있습니다.

고유한 테스트 세트 만들기에 대한 자세한 내용은 [Hobbes.js API 설명서](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/test-api/index.html).

1. CRXDE Lite을 엽니다. ([https://localhost:4502/crx/de](https://localhost:4502/crx/de))
1. 마우스 오른쪽 단추를 클릭합니다. `/etc/clientlibs` 폴더를 클릭한 다음 **만들기 > 폴더 만들기**. 유형 `myTests` 이름을 입력하고 을(를) 클릭합니다. **확인**.
1. 마우스 오른쪽 단추를 클릭합니다. `/etc/clientlibs/myTests` 폴더를 클릭한 다음 **만들기 > 노드 만들기**. 다음 속성 값을 사용한 다음 를 클릭합니다 **확인**:

   * 이름: `myFirstTest`
   * 유형: `cq:ClientLibraryFolder`

1. myFirstTest 노드에 다음 속성을 추가합니다.

   | 이름 | 유형 | 값 |
   |---|---|---|
   | `categories` | 문자열[] | `granite.testing.hobbes.tests` |
   | `dependencies` | 문자열[] | `granite.testing.hobbes.testrunner` |

   >[!NOTE]
   >
   >**AEM Forms 전용**
   >
   >
   >적응형 양식을 테스트하려면 카테고리 및 종속성에 다음 값을 추가합니다. 예:
   >
   >
   >**카테고리**: `granite.testing.hobbes.tests, granite.testing.hobbes.af.commons`
   >
   >
   >**종속성**: `granite.testing.hobbes.testrunner, granite.testing.hobbes.af`

1. 클릭 **모두 저장**.
1. 마우스 오른쪽 단추를 클릭합니다. `myFirstTest` 노드 및 **만들기 > 파일 만들기**. 파일 이름을 지정합니다 `js.txt` 을(를) 클릭합니다. **확인**.
1. 에서 `js.txt` 파일에서 다음 텍스트를 입력합니다.

   ```
   #base=.
   myTestSuite.js
   ```

1. 클릭 **모두 저장** 그런 다음 `js.txt` 파일.
1. 마우스 오른쪽 단추를 클릭합니다. `myFirstTest` 노드 및 **만들기 > 파일 만들기**. 파일 이름을 지정합니다 `myTestSuite.js` 을(를) 클릭합니다. **확인**.
1. 다음 코드를 `myTestSuite.js` 파일을 저장한 다음

   ```
   new hobs.TestSuite("Experience Content Test Suite", {path:"/etc/clientlibs/myTests/myFirstTest/myTestSuite.js"})
      .addTestCase(new hobs.TestCase("Navigate to Experience Content")
         .navigateTo("/content/we-retail/us/en/experience/arctic-surfing-in-lofoten.html")
      )
      .addTestCase(new hobs.TestCase("Hover Over Topnav")
         .mouseover("li.visible-xs")
      )
      .addTestCase(new hobs.TestCase("Click Topnav Link")
         .click("li.active a")
   );
   ```

1. 로 이동합니다 **테스트** 콘솔 을 클릭하여 테스트 세트를 테스트합니다.
