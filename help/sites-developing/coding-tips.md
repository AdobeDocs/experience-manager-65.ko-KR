---
title: 코딩 팁
description: Adobe Experience Manager의 코딩 모범 사례에 대한 몇 가지 팁을 알아봅니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 85ca35e5-6e2b-447a-9711-b12601beacdd
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 0%

---

# 코딩 팁{#coding-tips}

## 가능한 한 taglibs 또는 HTL 사용 {#use-taglibs-or-htl-as-much-as-possible}

JSP에 스크립틀릿을 포함하면 코드에서 문제를 디버깅하기 어렵습니다. 또한 JSP에 스크립틀릿을 포함시킴으로써 비즈니스 논리를 뷰 레이어와 분리하기가 어렵고, 이는 단일 책임 원칙 및 MVC 디자인 패턴을 위반합니다.

### 읽기 가능한 코드 작성 {#write-readable-code}

코드는 한 번 작성되지만 여러 번 읽습니다. 작성된 코드를 정리하기 위해 미리 시간을 투자하면 나중에 개발자와 사용자가 읽을 때 향후 배당금이 지급됩니다.

### 의도가 드러나는 이름 선택 {#choose-intention-revealing-names}

이상적으로 다른 프로그래머는 모듈을 열어 자신이 수행하는 작업을 이해해서는 안 됩니다. 마찬가지로, 그들은 독서 없이 방법이 무엇을 하는지 알 수 있어야 한다. 이러한 아이디어를 더 잘 구독할수록 코드를 더 쉽게 읽을 수 있으며 코드를 더 빨리 작성하고 변경할 수 있습니다.

AEM 코드 베이스에서는 다음 규칙이 사용됩니다.


* 인터페이스의 단일 구현 이름이 `<Interface>Impl`, 즉 `ReaderImpl`입니다.
* 인터페이스의 여러 구현 이름이 `<Variant><Interface>`, 즉 `JcrReader` 및 `FileSystemReader`입니다.
* 추상 기본 클래스의 이름은 `Abstract<Interface>` 또는 `Abstract<Variant><Interface>`입니다.
* 패키지 이름이 `com.adobe.product.module`입니다. 각 Maven 아티팩트 또는 OSGi 번들에는 고유한 패키지가 있어야 합니다.
* Java™ 구현은 API 아래의 impl 패키지에 배치됩니다.


이러한 규칙은 고객 구현에 반드시 적용되는 것은 아니지만 코드를 유지 관리할 수 있도록 규칙을 정의하고 준수하는 것이 중요합니다.

이상적으로 이름은 그들의 의도를 드러내야 한다. 이름이 원래대로 명확하지 않은 경우에 대한 일반적인 코드 테스트는 변수나 메서드의 용도를 설명하는 주석이 있는 것입니다.

<table>
 <tbody>
  <tr>
   <td><p><strong>명확하지 않음</strong></p> </td>
   <td><p><strong>지우기</strong></p> </td>
  </tr>
  <tr>
   <td><p>int d; //경과된 시간(일)</p> </td>
   <td><p>int elapsedTimeInDays;</p> </td>
  </tr>
  <tr>
   <td><p>//태그 지정된 이미지 가져오기<br /> 공용 목록 getItems() {}</p> </td>
   <td><p>공용 목록 getTaggedImages() {}</p> </td>
  </tr>
 </tbody>
</table>

### 반복하지 마십시오.  {#don-t-repeat-yourself}

DRY는 동일한 코드 세트를 복제해서는 안 된다고 설명합니다. 이는 문자열 리터럴과 같은 것에도 적용됩니다. 코드 복제는 무언가를 변경해야 할 때마다 결함을 찾아 제거해야 하는 문을 열어줍니다.

### 알몸 CSS 규칙 방지 {#avoid-naked-css-rules}

CSS 규칙은 애플리케이션 컨텍스트에서 타겟 요소에 따라 달라야 합니다. 예를 들어, *.content .center*&#x200B;에 적용되는 CSS 규칙은 너무 광범위하며 시스템의 많은 컨텐츠에 영향을 줄 수 있으므로 다른 사용자가 나중에 이 스타일을 재정의해야 합니다. 반면, 응용 프로그램 컨텍스트에서 *text*&#x200B;을(를) 지정하는 경우 *.myapp-centertext*&#x200B;이(가) 더 구체적인 규칙입니다.

### 더 이상 사용되지 않는 API 사용 제거 {#eliminate-usage-of-deprecated-apis}

API가 더 이상 사용되지 않는 경우, 더 이상 사용되지 않는 API에 의존하는 대신 새로운 권장 접근 방식을 찾는 것이 좋습니다. 이렇게 하면 향후 더 원활한 업그레이드를 보장할 수 있습니다.

### 지역화 가능 코드 작성 {#write-localizable-code}

작성자가 제공하지 않는 모든 문자열은 AEM의 i18n 사전 호출에서 JSP/Java의 *I18n.get()* 및 JavaScript의 *CQ.I18n.get()*&#x200B;을 통해 래핑해야 합니다. 이 구현은 구현을 찾을 수 없는 경우 전달된 문자열을 반환하므로 기본 언어로 기능을 구현한 후 현지화를 유연하게 구현할 수 있습니다.

### 안전을 위해 리소스 경로 이스케이프 처리 {#escape-resource-paths-for-safety}

JCR의 경로에는 공백이 없어야 하지만 공백이 있으면 코드가 손상되지 않아야 합니다. Jackrabbit은 *escape()* 및 *escapePath()* 메서드와 함께 Text 유틸리티 클래스를 제공합니다. JSP의 경우 Granite UI는 *granite:encodeURIPath() EL* 함수를 노출합니다.

### XSS API 및/또는 HTL을 사용하여 크로스 사이트 스크립팅 공격으로부터 보호 {#use-the-xss-api-and-or-htl-to-protect-against-cross-site-scripting-attacks}

AEM은 손쉽게 매개 변수를 정리하고 교차 사이트 스크립팅 공격으로부터 안전을 보장하기 위한 XSS API를 제공합니다. 또한 HTL은 템플릿 언어에 바로 내장된 이러한 보호 기능을 제공합니다. API 치트 시트는 [개발 - 지침 및 모범 사례](/help/sites-developing/dev-guidelines-bestpractices.md)에서 다운로드할 수 있습니다.

### 적절한 로깅 구현 {#implement-appropriate-logging}

Java™ 코드의 경우 AEM은 메시지 로깅을 위한 표준 API로 slf4j를 지원하며 관리의 일관성을 위해 OSGi 콘솔을 통해 사용할 수 있는 구성과 함께 사용해야 합니다. Slf4j는 다섯 가지 로깅 수준을 노출합니다. Adobe은 메시지를 기록할 수준을 선택할 때 다음 지침을 사용하는 것을 권장합니다.

* 오류: 코드에서 오류가 발생하여 처리를 계속할 수 없습니다. 이는 종종 예상치 못한 예외로 인해 발생합니다. 이러한 시나리오에 스택 추적을 포함하는 것이 유용합니다.
* 경고: 제대로 작동하지 않지만 처리가 계속되는 경우. 이는 종종 *PathNotFoundException*&#x200B;과 같이 필요한 예외로 인해 발생합니다.
* INFO: 시스템을 모니터링할 때 유용한 정보. 이 항목은 기본값이며 대부분의 고객은 이 항목을 환경에 그대로 둡니다. 따라서 과도하게 사용하지 마십시오.
* DEBUG: 처리에 대한 하위 수준 정보. 지원을 통해 문제를 디버깅할 때 유용합니다.
* TRACE: 입력/종료 방법과 같은 최하위 레벨 정보입니다. 일반적으로 개발자만 사용합니다.

JavaScript이 있는 경우 *console.log*&#x200B;은(는) 개발 중에만 사용해야 하며 릴리스 전에 모든 로그 문을 제거해야 합니다.

### 화물 숭배 프로그래밍 방지 {#avoid-cargo-cult-programming}

코드가 수행하는 작업을 이해하지 못한 채 코드를 복사하지 마십시오. 확실하지 않은 모듈 또는 API에 대한 경험이 더 많은 사람에게 문의하는 것이 좋습니다.
