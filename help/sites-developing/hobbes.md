---
title: UI 테스트
description: AEM은 AEM UI에 대한 테스트를 자동화하기 위한 프레임워크를 제공합니다
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components, testing
docset: aem65
exl-id: 2d28cee6-31b0-4288-bad3-4d2ecad7b626
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '759'
ht-degree: 3%

---

# UI 테스트{#testing-your-ui}

>[!NOTE]
>
>AEM 6.5 이상에서는 hobbes.js UI 테스트 프레임워크가 더 이상 사용되지 않습니다. Adobe은 추가 개선 사항을 계획하지 않으며 고객에게 Selenium 자동화를 사용할 것을 권장합니다.
>
>다음을 참조하십시오 [사용이 중단되거나 제거된 기능](/help/release-notes/deprecated-removed-features.md).

AEM은 AEM UI에 대한 테스트를 자동화하기 위한 프레임워크를 제공합니다. 프레임워크를 사용하여 웹 브라우저에서 직접 UI 테스트를 작성하고 실행합니다. 프레임워크는 테스트 생성을 위한 JavaScript API를 제공합니다.

AEM 테스트 프레임워크는 JavaScript로 작성된 테스트 라이브러리인 Hobbes.js를 사용합니다. Hobbes.js 프레임워크는 개발 프로세스의 일부로 AEM을 테스트하기 위해 개발되었습니다. 이제 프레임워크를 AEM 애플리케이션 테스트에 공개적으로 사용할 수 있습니다.

>[!NOTE]
>
>Hobbes.js를 참조하십시오 [설명서](https://developer.adobe.com/experience-manager/reference-materials/6-5/test-api/index.html) API에 대한 전체 세부 정보.

## 테스트 구조 {#structure-of-tests}

AEM 내에서 자동화된 테스트를 사용할 때 다음 용어를 이해하는 것이 중요합니다.

| 작업 | An **작업** 링크 또는 버튼 클릭과 같은 웹 페이지의 특정 활동입니다. |
|---|---|
| 테스트 사례 | A **테스트 사례** 하나 이상으로 구성할 수 있는 특정 상황입니다 **작업**. |
| 테스트 세트 | A **테스트 세트** 은(는) 관련 그룹입니다. **테스트 사례** 특정 사용 사례를 함께 테스트합니다. |

## 테스트 실행 {#executing-tests}

### 테스트 세트 보기 {#viewing-test-suites}

테스트 콘솔을 열어 등록된 테스트 세트를 확인합니다. 테스트 패널에는 테스트 세트와 테스트 사례 목록이 포함되어 있습니다.

를 통해 도구 콘솔로 이동합니다. **전역 탐색 > 도구 > 작업 > 테스트**.

![chlimage_1-63](assets/chlimage_1-63.png)

콘솔을 열면 테스트 세트 가 왼쪽의 목록과 함께 모든 테스트 세트를 순서대로 실행합니다. 체크무늬 배경과 함께 표시되는 오른쪽의 공간은 테스트가 실행될 때 페이지 콘텐츠를 표시하기 위한 자리 표시자입니다.

![chlimage_1-64](assets/chlimage_1-64.png)

### 단일 테스트 세트 실행 {#running-a-single-test-suite}

테스트 세트는 개별적으로 실행할 수 있습니다. 테스트 세트를 실행하면 테스트 사례 및 해당 작업이 실행되고 테스트 완료 후 결과가 표시되면서 페이지가 변경됩니다. 아이콘은 결과를 나타냅니다.

확인 표시 아이콘은 합격한 테스트를 나타냅니다.

![확인 표시 아이콘](do-not-localize/chlimage_1-2.png)

&quot;X&quot; 아이콘은 실패한 테스트를 나타냅니다.

![원형 안에 X가 표시된 테스트 실패 아이콘.](do-not-localize/chlimage_1-3.png)

테스트 세트를 실행하려면:

1. [테스트] 패널에서 실행할 테스트 사례의 이름을 클릭하여 작업의 세부 정보를 확장합니다.

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. 클릭 **테스트 실행**.

   ![테스트 실행 단추의 이미지로, 원 안에 있는 오른쪽 포인터로 표시됩니다.](do-not-localize/chlimage_1-4.png)

1. 자리 표시자는 테스트가 실행될 때 페이지 콘텐츠로 대체됩니다.

   ![chlimage_1-66](assets/chlimage_1-66.png)

1. 설명을 탭하거나 클릭하여 을(를) 열어 테스트 사례 결과를 검토합니다. **결과** 패널. 에서 테스트 케이스의 이름을 탭하거나 클릭합니다. **결과** 패널에 모든 세부 정보가 표시됩니다.

   ![chlimage_1-67](assets/chlimage_1-67.png)

### 여러 테스트 실행 {#running-multiple-tests}

테스트 세트는 콘솔에 표시되는 순서로 순차적으로 실행됩니다. 테스트로 드릴다운하여 자세한 결과를 확인할 수 있습니다.

![chlimage_1-68](assets/chlimage_1-68.png)

1. 테스트 패널에서 다음을 클릭합니다. **모든 테스트 실행** 단추 또는 **테스트 실행** 실행할 테스트 세트의 제목 아래에 있는 단추입니다.

   ![원 안에 있는 오른쪽 포인터가 가리키는 모든 테스트 실행 단추와 테스트 실행 단추의 이미지입니다.](do-not-localize/chlimage_1-5.png)

1. 각 테스트 사례의 결과를 보려면 테스트 사례의 제목을 클릭합니다. 에서 테스트 이름 클릭 **결과** 패널에 모든 세부 정보가 표시됩니다.

   ![chlimage_1-69](assets/chlimage_1-69.png)

## 간단한 테스트 세트 만들기 및 사용 {#creating-and-using-a-simple-test-suite}

다음 절차에서는 를 사용하여 테스트 세트를 만들고 실행하는 과정을 단계별로 안내합니다 [We.Retail 콘텐츠](/help/sites-developing/we-retail.md)다른 웹 페이지를 사용하도록 테스트를 쉽게 수정할 수 있습니다.

고유한 테스트 세트 만들기에 대한 자세한 내용은 [Hobbes.js API 설명서](https://developer.adobe.com/experience-manager/reference-materials/6-5/test-api/index.html).

1. CRXDE Lite 열기. ([https://localhost:4502/crx/de](https://localhost:4502/crx/de))
1. 마우스 오른쪽 단추 클릭 `/etc/clientlibs` 폴더 및 클릭 **만들기 > 폴더 만들기**. 유형 `myTests` 을(를) 클릭하고 을(를) 클릭합니다. **확인**.
1. 마우스 오른쪽 단추 클릭 `/etc/clientlibs/myTests` 폴더 및 클릭 **만들기 > 노드 만들기**. 다음 속성 값을 사용한 다음 **확인**:

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
   >적응형 양식을 테스트하려면 범주 및 종속 항목에 다음 값을 추가하십시오. 예:
   >
   >
   >**카테고리**: `granite.testing.hobbes.tests, granite.testing.hobbes.af.commons`
   >
   >
   >**종속성**: `granite.testing.hobbes.testrunner, granite.testing.hobbes.af`

1. **모두 저장**&#x200B;을 클릭합니다.
1. 마우스 오른쪽 단추 클릭 `myFirstTest` 노드 및 클릭 **만들기 > 파일 만들기**. 파일 이름을 지정합니다 `js.txt` 및 클릭 **확인**.
1. 다음에서 `js.txt` 파일에 다음 텍스트를 입력합니다.

   ```
   #base=.
   myTestSuite.js
   ```

1. 클릭 **모두 저장** 그런 다음 을(를) 닫습니다. `js.txt` 파일.
1. 마우스 오른쪽 단추 클릭 `myFirstTest` 노드 및 클릭 **만들기 > 파일 만들기**. 파일 이름을 지정합니다 `myTestSuite.js` 및 클릭 **확인**.
1. 다음 코드를 `myTestSuite.js` 파일을 저장한 다음 다음 파일을 저장합니다.

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

1. 다음 위치로 이동 **테스트** 콘솔을 사용하여 테스트 제품군을 테스트해 보십시오.
