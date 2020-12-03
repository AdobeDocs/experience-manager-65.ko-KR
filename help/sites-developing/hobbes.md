---
title: UI 테스트
seo-title: UI 테스트
description: AEM은 AEM UI에 대한 테스트 자동화를 위한 프레임워크를 제공합니다.
seo-description: AEM은 AEM UI에 대한 테스트 자동화를 위한 프레임워크를 제공합니다.
uuid: 408a60b5-cba9-4c9f-abd3-5c1fb5be1c50
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components, testing
discoiquuid: 938100ad-94f9-408a-819d-72657dc115f7
docset: aem65
translation-type: tm+mt
source-git-commit: 46f2ae565fe4a8cfea49572eb87a489cb5d9ebd7
workflow-type: tm+mt
source-wordcount: '751'
ht-degree: 3%

---


# UI 테스트{#testing-your-ui}

>[!NOTE]
>
>AEM 6.5 이상 버전에서 hobbes.js UI 테스트 프레임워크는 더 이상 사용되지 않습니다. Adobe은 추가적인 개선 계획을 가지고 있지 않으며 고객이 Selenium 자동화를 사용하도록 권장합니다.
>
>[더 이상 사용되지 않고 제거된 기능](/help/release-notes/deprecated-removed-features.md)을 참조하십시오.

AEM은 AEM UI에 대한 테스트를 자동화하는 프레임워크를 제공합니다. 이 프레임워크를 사용하면 웹 브라우저에서 직접 UI 테스트를 작성하고 실행할 수 있습니다. 프레임워크는 테스트를 만들기 위한 javascript API를 제공합니다.

AEM 테스트 프레임워크는 Javascript로 작성된 테스트 라이브러리인 Hobes.js를 사용합니다. Hobes.js 프레임워크는 개발 프로세스의 일환으로 AEM을 테스트하기 위해 개발되었습니다. 이 프레임워크는 이제 AEM 애플리케이션을 테스트하는 데 공개적으로 사용할 수 있습니다.

>[!NOTE]
>
>API에 대한 자세한 내용은 Hobes.js [documentation](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/test-api/index.html)을 참조하십시오.

## 테스트 구조 {#structure-of-tests}

AEM 내에서 자동화된 테스트를 사용하는 경우 다음 용어를 이해해야 합니다.

| 작업 | **작업**&#x200B;은 링크나 단추를 클릭하는 것과 같은 웹 페이지의 특정 활동입니다. |
|---|---|
| 테스트 케이스 | **테스트 케이스**&#x200B;는 하나 이상의 **Actions**&#x200B;로 구성될 수 있는 특정 상황입니다. |
| 테스트 세트 | **Test Suite**&#x200B;는 특정 사용 사례를 함께 테스트하는 관련 **테스트 케이스**&#x200B;의 그룹입니다. |

## 테스트 실행 {#executing-tests}

### 테스트 세트 보기 {#viewing-test-suites}

등록된 테스트 세트를 보려면 테스트 콘솔을 엽니다. 테스트 패널에는 테스트 세트 및 테스트 케이스 목록이 포함되어 있습니다.

**전역 탐색 -> 도구 > 작업 -> 테스트**&#x200B;를 통해 도구 콘솔로 이동합니다.

![chlimage_1-63](assets/chlimage_1-63.png)

콘솔을 열면 테스트 세트가 모든 콘솔을 순차적으로 실행하는 옵션과 함께 왼쪽에 나열됩니다. 체크된 배경이 있는 오른쪽에 표시되는 공백은 테스트가 실행될 때 페이지 컨텐츠를 표시하는 자리 표시자입니다.

![chlimage_1-64](assets/chlimage_1-64.png)

### 단일 테스트 세트 실행 {#running-a-single-test-suite}

테스트 세트는 개별적으로 실행할 수 있습니다. Test Suite를 실행하면 테스트 케이스 및 해당 작업이 실행되면서 페이지가 변경되고 테스트 완료 후 결과가 나타납니다. 아이콘은 결과를 나타냅니다.

확인 표시 아이콘은 전달된 테스트를 나타냅니다.

![](do-not-localize/chlimage_1-2.png)

&quot;X&quot; 아이콘은 실패한 테스트를 나타냅니다.

![](do-not-localize/chlimage_1-3.png)

테스트 세트를 실행하려면

1. 테스트 패널에서 실행할 테스트 케이스 이름을 클릭하거나 탭하여 작업의 세부 사항을 확장합니다.

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. **테스트 실행** 단추를 클릭하거나 탭합니다.

   ![](do-not-localize/chlimage_1-4.png)

1. 테스트 실행 시 자리 표시자가 페이지 컨텐츠로 대체됩니다.

   ![chlimage_1-66](assets/chlimage_1-66.png)

1. 설명을 탭하거나 클릭하여 **결과** 패널을 열어 테스트 케이스 결과를 검토합니다. **결과** 패널에서 테스트 케이스 이름을 탭하거나 클릭하면 모든 세부 사항이 표시됩니다.

   ![chlimage_1-67](assets/chlimage_1-67.png)

### 여러 테스트 실행 {#running-multiple-tests}

테스트 세트는 콘솔에 나타나는 순서대로 실행됩니다. 테스트를 드릴다운하여 자세한 결과를 볼 수 있습니다.

![chlimage_1-68](assets/chlimage_1-68.png)

1. 테스트 패널에서 **모든 테스트 실행** 단추 또는 실행할 테스트 세트 제목 아래에 있는 **테스트 실행** 단추를 누르거나 클릭합니다.

   ![](do-not-localize/chlimage_1-5.png)

1. 각 테스트 케이스의 결과를 보려면 테스트 케이스의 제목을 누르거나 클릭합니다. **결과** 패널에서 테스트 이름을 탭하거나 클릭하면 모든 세부 사항이 표시됩니다.

   ![chlimage_1-69](assets/chlimage_1-69.png)

## 단순 테스트 세트 만들기 및 사용 {#creating-and-using-a-simple-test-suite}

다음 절차에서는 [We.Retail content](/help/sites-developing/we-retail.md)을 사용하여 Test Suite를 만들고 실행하는 과정을 단계이지만 다른 웹 페이지를 사용하도록 테스트를 쉽게 수정할 수 있습니다.

자체 테스트 세트 만들기에 대한 자세한 내용은 [Hobes.js API 설명서](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/test-api/index.html)를 참조하십시오.

1. CRXDE Lite 열기 ([https://localhost:4502/crx/de](https://localhost:4502/crx/de))
1. `/etc/clientlibs` 폴더를 마우스 오른쪽 단추로 클릭하고 **만들기 > 폴더 만들기**&#x200B;를 클릭합니다. 이름에 `myTests`을 입력하고 **확인**&#x200B;을 클릭합니다.
1. `/etc/clientlibs/myTests` 폴더를 마우스 오른쪽 단추로 클릭하고 **만들기 > 노드 만들기**&#x200B;를 클릭합니다. 다음 속성 값을 사용한 다음 **OK**&#x200B;을 클릭합니다.

   * 이름: `myFirstTest`
   * 유형: `cq:ClientLibraryFolder`

1. myFirstTest 노드에 다음 속성을 추가합니다.

   | 이름 | 유형 | 값 |
   |---|---|---|
   | `categories` | String[] | `granite.testing.hobbes.tests` |
   | `dependencies` | 문자열[] | `granite.testing.hobbes.testrunner` |

   >[!NOTE]
   >
   >**AEM Forms 전용**
   >
   >
   >적응형 양식을 테스트하려면 카테고리 및 종속성에 다음 값을 추가합니다. 예:
   >
   >
   >**카테고리**:  `granite.testing.hobbes.tests, granite.testing.hobbes.af.commons`
   >
   >
   >**종속성**:  `granite.testing.hobbes.testrunner, granite.testing.hobbes.af`

1. **모두 저장**&#x200B;을 클릭합니다.
1. `myFirstTest` 노드를 마우스 오른쪽 단추로 클릭하고 **만들기 > 파일 만들기**&#x200B;를 클릭합니다. `js.txt` 파일의 이름을 지정하고 **확인**&#x200B;을 클릭합니다.
1. `js.txt` 파일에서 다음 텍스트를 입력합니다.

   ```
   #base=.
   myTestSuite.js
   ```

1. **모두 저장**&#x200B;을 클릭한 다음 `js.txt` 파일을 닫습니다.
1. `myFirstTest` 노드를 마우스 오른쪽 단추로 클릭하고 **만들기 > 파일 만들기**&#x200B;를 클릭합니다. `myTestSuite.js` 파일의 이름을 지정하고 **확인**&#x200B;을 클릭합니다.
1. 다음 코드를 `myTestSuite.js` 파일에 복사한 다음 파일을 저장합니다.

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

1. 테스트 세트를 시도하려면 **테스트** 콘솔로 이동합니다.
