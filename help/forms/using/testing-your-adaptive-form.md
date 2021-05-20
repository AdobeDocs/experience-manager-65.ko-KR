---
title: '"자습서:적응형 양식 테스트"'
seo-title: '"자습서:적응형 양식 테스트"'
description: 자동화된 테스트를 사용하여 여러 적응형 양식을 한 번에 테스트할 수 있습니다.
seo-description: 자동화된 테스트를 사용하여 여러 적응형 양식을 한 번에 테스트할 수 있습니다.
uuid: 6d182bbc-b47a-4c97-af70-c960b52fdfac
contentOwner: khsingh
discoiquuid: ecddb22e-c148-441f-9088-2e5b35c7021b
docset: aem65
feature: 적응형 양식
exl-id: 343e2e0b-d5ef-4f01-b3d6-45f90e2430fd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 3%

---

# 자습서:적응형 양식 테스트 {#tutorial-testing-your-adaptive-form}

![](do-not-localize/10-test-your-adaptive-form.png)

이 자습서는 [첫 번째 적응형 양식 만들기](https://helpx.adobe.com/kr/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html) 시리즈의 단계입니다. 전체 자습서 사용 사례를 이해하고, 수행하고, 시연하기 위해 시리즈를 시간 순서대로 따르는 것이 좋습니다.

적응형 양식을 준비했으면 최종 사용자에게 롤아웃하기 전에 적응형 양식을 테스트하는 것이 중요합니다. 모든 필드를 수동으로 테스트(기능 테스트)하거나 적응형 양식 테스트를 자동화할 수 있습니다. 적응형 양식이 여러 개 있으면 모든 적응형 양식의 모든 필드를 수동으로 테스트하는 것은 어려운 작업이 됩니다.

AEM [!DNL Forms]은(는) 적응형 양식 테스트를 자동화하는 테스트 프레임워크인 Calvin을 제공합니다. 프레임워크를 사용하면 웹 브라우저에서 직접 UI 테스트를 작성하고 실행할 수 있습니다. 프레임워크는 테스트 생성을 위한 JavaScript API를 제공합니다. 자동화된 테스트를 사용하면 적응형 양식의 미리 채우기 경험을 테스트하고, 적응형 양식, 표현식 규칙, 유효성 검사, 지연 로드 및 UI 상호 작용에서 경험을 제출할 수 있습니다. 이 자습서에서는 적응형 양식에서 자동화된 테스트를 만들고 실행하는 단계를 안내합니다. 이 자습서를 마치면 다음을 수행할 수 있습니다.

* [적응형 양식의 테스트 세트 만들기](../../forms/using/testing-your-adaptive-form.md#step-create-a-test-suite)
* [적응형 양식에 대한 테스트 만들기](../../forms/using/testing-your-adaptive-form.md#step-create-a-test-case-to-prefill-values-in-an-adaptive-form)
* [적응형 양식에 대해 만들어진 테스트 세트 및 테스트 실행](#step-run-all-the-tests-in-a-suite-or-individual-tests-cases)

## 1단계:테스트 세트 {#step-create-a-test-suite} 만들기

테스트 세트에는 테스트 사례 컬렉션이 있습니다. 여러 테스트 세트가 있을 수 있습니다. 각 양식에 대해 별도의 테스트 세트를 사용하는 것이 좋습니다. 테스트 세트를 만들려면 다음을 수행하십시오.

1. 관리자로 AEM [!DNL Forms] 작성자 인스턴스에 로그인합니다. [!UICONTROL CRXDE Lite]을 엽니다. AEM 로고 > **[!UICONTROL 도구]** > **[!UICONTROL 일반]** > **[!UICONTROL CRXDE Lite]**&#x200B;를 탭하거나 브라우저에서 [https://localhost:4502/crx/de/index.jsp](https://localhost:4502/crx/de/index.jsp) URL을 열어 CRXDE Lite을 열 수 있습니다.

1. [!UICONTROL CRXDE Lite]에서 /etc/clientlibs로 이동합니다. /etc/clientlibs 하위 폴더를 마우스 오른쪽 단추로 클릭하고 **[!UICONTROL 만들기]** > **[!UICONTROL 노드 만들기]**&#x200B;를 클릭합니다. **[!UICONTROL 이름]** 필드에 **WeRetailFormTestCases**&#x200B;를 입력합니다. 유형을 **cq:ClientLibraryFolder**(으)로 선택하고 **[!UICONTROL 확인]**&#x200B;을 클릭합니다. 노드를 만듭니다. `WeRetailFormTestCases` 대신 어떤 이름이든 사용할 수 있습니다.
1. 다음 속성을 `WeRetailFormTestCases` 노드에 추가하고 **[!UICONTROL 모두 저장]**&#x200B;을 탭합니다.

   <table>
    <tbody>
     <tr>
      <td><strong>속성</strong></td>
      <td><strong>유형</strong></td>
      <td><strong>다중</strong></td>
      <td><strong>값</strong></td>
     </tr>
     <tr>
      <td>카테고리</td>
      <td>문자열</td>
      <td>활성화됨</td>
      <td>
       <ul>
        <li>granite.testing.hobbes.tests<br /> </li>
        <li>granite.testing.calvin.tests</li>
       </ul> </td>
     </tr>
     <tr>
      <td>종속성</td>
      <td>문자열</td>
      <td>활성화됨</td>
      <td>
       <ul>
        <li>granite.testing.hobbes.testrunner <br /> </li>
        <li>granite.testing.calvin <br /> </li>
        <li>apps.testframework.all</li>
       </ul> </td>
     </tr>
    </tbody>
   </table>

   각 속성이 아래에 표시된 대로 별도의 상자에 추가되어 있는지 확인합니다.

   ![종속성](assets/dependencies.png)

1. **[!UICONTROL WeRetailFormTestCases]** 노드를 마우스 오른쪽 단추로 클릭하고 **[!UICONTROL 만들기]** > **[!UICONTROL 파일 만들기]**&#x200B;를 클릭합니다. **[!UICONTROL 이름]** 필드에 `js.txt`를 입력하고 **[!UICONTROL 확인]**&#x200B;을 클릭합니다.
1. 편집할 js.txt 파일을 열고 다음 코드를 추가한 다음 파일을 저장합니다.

   ```text
   #base=.
    init.js
   ```

1. `WeRetailFormTestCases` 노드에서 init.js 파일을 만듭니다. 아래 코드를 파일에 추가하고 **[!UICONTROL 모두 저장]**&#x200B;을 탭합니다.

   ```javascript
   (function(window, hobs) {
       'use strict';
       window.testsuites = window.testsuites || {};
     // Registering the test form suite to the sytem
     // If there are other forms, all registration should be done here
       window.testsuites.testForm3 = new hobs.TestSuite("We retail - Tests", {
           path: '/etc/clientlibs/WeRetailFormTestCases/init.js',
           register: true
       });
    // window.testsuites.testForm2 = new hobs.TestSuite("testForm2");
   }(window, window.hobs));
   ```

   위의 코드는 **We retail - Tests**&#x200B;라는 테스트 세트를 만듭니다.

1. AEM 테스트 UI 를 엽니다(AEM > **[!UICONTROL 도구]** > **[!UICONTROL 작업]** > **[!UICONTROL 테스트]**). 테스트 세트 - **We retail - Tests** 가 UI에 나열됩니다.

   ![we-retail-test-suite](assets/we-retail-test-suite.png)

## 2단계:적응형 양식 {#step-create-a-test-case-to-prefill-values-in-an-adaptive-form}에 값을 미리 채울 테스트 사례를 만듭니다

테스트 사례는 특정 기능을 테스트하는 작업 세트입니다. 예를 들어, 양식의 모든 필드를 미리 작성하고 일부 필드의 유효성을 검사하여 올바른 값을 입력해야 합니다.

작업은 단추 클릭과 같은 적응형 양식의 특정 활동입니다. 각 적응형 양식 필드에 대한 사용자 입력의 유효성을 검사할 테스트 사례 및 작업을 만들려면,

1. [!UICONTROL CRXDE Lite]에서 `/content/forms/af/create-first-adaptive-form` 폴더로 이동합니다. **[!UICONTROL create-first-adaptive-form]** 폴더 노드를 마우스 오른쪽 단추로 클릭하고 **[!UICONTROL 만들기]** **[!UICONTROL 파일 만들기]**&#x200B;를 클릭합니다. **[!UICONTROL 이름]** 필드에 `prefill.xml`를 입력하고 **[!UICONTROL 확인]**&#x200B;을 클릭합니다. 파일에 다음 코드를 추가합니다.

   ```xml
   <?xml version="1.0" encoding="UTF-8"?><afData>
     <afUnboundData>
       <data>
         <customer_ID>371767</customer_ID>
         <customer_Name>John Jacobs</customer_Name>
         <customer_Shipping_Address>1657 1657 Riverside Drive Redding</customer_Shipping_Address>
         <customer_State>California</customer_State>
         <customer_ZIPCode>096001</customer_ZIPCode>
        </data>
     </afUnboundData>
     <afBoundData>
       <data xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/"/>
     </afBoundData>
   </afData>
   ```

1. 다음으로 이동 `/etc/clientlibs`. `/etc/clientlibs` 하위 폴더를 마우스 오른쪽 단추로 클릭하고 **[!UICONTROL 만들기]** **[!UICONTROL 노드 만들기]**&#x200B;를 클릭합니다.

   **[!UICONTROL 이름]** 필드에 `WeRetailFormTests`를 입력합니다. 유형을 `cq:ClientLibraryFolder`(으)로 선택하고 **[!UICONTROL 확인]**&#x200B;을 클릭합니다.

1. **[!UICONTROL WeRetailFormTests]** 노드에 다음 속성을 추가합니다.

   <table>
    <tbody>
     <tr>
      <td><strong>속성</strong></td>
      <td><strong>유형</strong></td>
      <td><strong>다중</strong></td>
      <td><strong>값</strong></td>
     </tr>
     <tr>
      <td>카테고리</td>
      <td>문자열</td>
      <td>활성화됨</td>
      <td>
       <ul>
        <li>granite.testing.hobbes.tests<br /> </li>
        <li>granite.testing.hobbes.tests.testForm</li>
       </ul> </td>
     </tr>
     <tr>
      <td>종속성</td>
      <td>문자열</td>
      <td>활성화됨</td>
      <td>
       <ul>
        <li>granite.testing.calvin.tests</li>
       </ul> </td>
     </tr>
     </tbody>
   </table>

1. **[!UICONTROL WeRetailFormTests]** 노드에서 파일 js.txt를 만듭니다. 파일에 다음 내용을 추가합니다.

   ```shell
   #base=.
   prefillTest.js
   ```

   **[!UICONTROL 모두 저장]**&#x200B;을 클릭합니다.

1. **[!UICONTROL WeRetailFormTests]** 노드에서 파일 `prefillTest.js`을 만듭니다. 아래 코드를 파일에 추가합니다. 이 코드는 테스트 사례를 만듭니다. 테스트 케이스는 양식의 모든 필드를 미리 작성하고 일부 필드의 유효성을 검사하여 올바른 값을 입력했는지 확인합니다.

   ```javascript
   (function (window, hobs) {
       'use strict';
   
       var ts = new hobs.TestSuite("Prefill Test", {
           path: '/etc/clientlibs/WeRetailFormTests/prefillTest.js',
           register: false
       })
   
       .addTestCase(new hobs.TestCase("Prefill Test")
           // navigate to the testForm which is to be test
           .navigateTo("/content/forms/af/create-first-adaptive-form/shipping-address-add-update-form.html?wcmmode=disabled&dataRef=crx:///content/forms/af/create-first-adaptive-form/prefill.xml")
           // check if adaptive form is loaded
           .asserts.isTrue(function () {
               return calvin.isFormLoaded()
           })
           .asserts.isTrue(function () {
               return calvin.model("customer_ID").value == 371767;
           })
           .asserts.isTrue(function () {
               return calvin.model("customer_ZIPCode").value == 96001;
           })
       );
   
       // register the test suite with testForm
       window.testsuites.testForm3.add(ts);
   
   }(window, window.hobs));
   ```

   테스트 사례가 만들어져서 실행할 준비가 되었습니다. 테스트 사례를 만들어 스크립트 실행 확인, 패턴 확인 및 적응형 양식의 제출 경험 검증과 같은 적응형 양식의 다양한 측면을 확인할 수 있습니다. 적응형 양식 테스트의 다양한 측면에 대한 자세한 내용은 적응형 양식 테스트 자동화 를 참조하십시오.

## 3단계:세트 또는 개별 테스트 사례 {#step-run-all-the-tests-in-a-suite-or-individual-tests-cases}에서 모든 테스트를 실행합니다.

테스트 세트에는 여러 테스트 사례가 있을 수 있습니다. 테스트 세트의 모든 테스트 사례를 한 번에 실행하거나 개별적으로 실행할 수 있습니다. 테스트를 실행하면 아이콘이 결과를 나타냅니다.

* 확인 표시 아이콘은 전달된 테스트를 나타냅니다.![save_icon](assets/save_icon.svg)
* X 아이콘은 실패한 테스트를 나타냅니다.![close-icon](assets/close-icon.svg)

1. AEM 아이콘 > **[!UICONTROL 도구]** **[!UICONTROL 작업]** **[!UICONTROL 테스트]**&#x200B;로 이동합니다.
1. 테스트 세트의 모든 테스트를 실행하려면

   1. [!UICONTROL 테스트] 패널에서 **[!UICONTROL We retail - 테스트 (1)]**&#x200B;를 탭합니다. 이 도구 모음이 확장되어 테스트 목록이 표시됩니다.
   1. **[!UICONTROL 테스트 실행]** 단추를 누릅니다. 화면 오른쪽의 빈 영역은 테스트가 실행될 때 적응형 양식으로 대체됩니다.

      ![모든 테스트 실행](assets/run-all-test.png)

1. 테스트 세트에서 단일 테스트를 실행하려면

   1. 테스트 패널에서 **[!UICONTROL We retail - Tests (1)]**&#x200B;를 누릅니다. 이 도구 모음이 확장되어 테스트 목록이 표시됩니다.
   1. **[!UICONTROL Prefill Test]**&#x200B;를 탭하고 **[!UICONTROL 테스트 실행]** 단추를 탭합니다. 화면 오른쪽의 빈 영역은 테스트가 실행될 때 적응형 양식으로 대체됩니다.

1. 테스트 이름 미리 채우기 테스트를 눌러 테스트 사례 결과를 검토합니다. [!UICONTROL 결과] 패널이 열립니다. [!UICONTROL 결과] 패널에서 테스트 사례 이름을 탭하여 테스트의 모든 세부 사항을 볼 수 있습니다.

   ![검토 결과](assets/review-results.png)

이제 적응형 양식을 게시할 준비가 되었습니다.
