---
title: 코딩 팁
seo-title: Coding Tips
description: AEM 코딩 팁
seo-description: Tips for coding for AEM
uuid: 1bb1cc6a-3606-4ef4-a8dd-7c08a7cf5189
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 4adce3b4-f209-4a01-b116-a5e01c4cc123
exl-id: 85ca35e5-6e2b-447a-9711-b12601beacdd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 0%

---

# 코딩 팁{#coding-tips}

## 가능한 한 taglibs 또는 HTL을 사용하십시오 {#use-taglibs-or-htl-as-much-as-possible}

JSP에 scriptlet을 포함하면 코드에서 문제를 디버깅하는 것이 어렵습니다. 또한 JSP에 scriptlet을 포함함으로써 단일 책임 원칙 및 MVC 디자인 패턴을 위반하는 뷰 레이어와 비즈니스 로직을 구분하기 어렵습니다.

### 읽을 수 있는 코드 작성 {#write-readable-code}

코드는 한 번 작성되지만 여러 번 읽습니다. 우리가 쓰는 코드를 정리하기 위해 시간을 좀 더 내야만 우리는 다른 개발자들이 나중에 그것을 읽어야 할 때 그 길을 따라 배당금을 지불할 것입니다.

### 이름 표시 선택 {#choose-intention-revealing-names}

이상적으로는 다른 프로그래머가 모듈을 열어 자신의 기능을 파악할 필요가 없습니다. 마찬가지로, 그들은 그것을 읽지 않고 어떤 방법이 하는지 말할 수 있어야 합니다. 이러한 아이디어를 더 잘 구독하면 코드를 더 쉽게 읽을 수 있고 코드를 더 빨리 작성하고 변경할 수 있습니다.

AEM 코드 베이스에서 다음 규칙이 사용됩니다.


* 인터페이스의 단일 구현에는 이름이 지정됩니다 `<Interface>Impl`예, `ReaderImpl`.
* 인터페이스의 여러 구현에 대해 이름이 지정됩니다 `<Variant><Interface>`예, `JcrReader` 및 `FileSystemReader`.
* 추상 기본 클래스의 이름은 다음과 같습니다 `Abstract<Interface>` 또는 `Abstract<Variant><Interface>`.
* 패키지의 이름은 다음과 같습니다 `com.adobe.product.module`.  각 Maven 아티팩트 또는 OSGi 번들에는 자체 패키지가 있어야 합니다.
* Java 구현은 API 아래에 있는 impl 패키지에 배치됩니다.


이러한 규칙을 반드시 고객 구현에 적용할 필요는 없지만, 코드를 유지 관리할 수 있도록 규칙을 정의하고 이 규칙에 적용하는 것이 중요합니다.

이상적으로는 자신의 의도를 드러내야 한다. 이름이 분명하지 않은 경우에 대한 일반적인 코드 테스트에서는 변수나 방법이 무엇인지 설명하는 주석이 있습니다.

<table>
 <tbody>
  <tr>
   <td><p><strong>불명확하게</strong></p> </td>
   <td><p><strong>지우기</strong></p> </td>
  </tr>
  <tr>
   <td><p>d. //경과된 시간(일)</p> </td>
   <td><p>int elapsedTimeInDays;</p> </td>
  </tr>
  <tr>
   <td><p>//태그가 지정된 이미지 가져오기<br /> 공용 목록 getItems() {}</p> </td>
   <td><p>공용 목록 getTaggedImages() {}</p> </td>
  </tr>
 </tbody>
</table>

### 반복하지 마  {#don-t-repeat-yourself}

DRY에서는 동일한 코드 세트가 중복되지 않도록 합니다. 이는 문자열 리터럴과 같은 경우에도 적용됩니다. 코드 중복은 어떤 것이 변해야 할 때마다 결함의 문을 열고, 찾고 제거되어야 한다.

### 벌거벗은 CSS 규칙 방지 {#avoid-naked-css-rules}

CSS 규칙은 애플리케이션 컨텍스트에서 대상 요소에만 적용됩니다. 예를 들어 *.content.center* 이는 지나치게 광범위할 수 있으므로 결과적으로 시스템 전반에 걸쳐 많은 컨텐츠에 영향을 줄 수 있으므로 나중에 다른 사용자가 이러한 스타일을 재정의하도록 할 수 있습니다. *.myapp-centertext* 를 지정하는 경우 가운데에 보다 구체적인 규칙이 *텍스트* 를 입력합니다.

### 더 이상 사용되지 않는 API의 사용 방지 {#eliminate-usage-of-deprecated-apis}

API가 더 이상 사용되지 않는 경우 더 이상 사용되지 않는 API에 의존하는 대신 새로운 권장 접근 방식을 찾는 것이 좋습니다. 이를 통해 향후에 더욱 원활한 업그레이드가 가능합니다.

### 지역화 가능한 코드 작성 {#write-localizable-code}

작성자가 제공하지 않는 모든 문자열은 *I18n.get()* JSP/Java 및 *CQ.I18n.get()* ( JavaScript에서)를 참조하십시오. 이 구현은 구현을 찾을 수 없으면 전달된 문자열을 반환하므로 기본 언어로 기능을 구현한 후 로컬라이제이션을 구현할 수 있는 유연성을 제공합니다.

### 안전한 리소스 경로 이스케이프 처리 {#escape-resource-paths-for-safety}

JCR의 경로에 공백이 있으면 안 되지만, 경로가 있으면 코드가 중단되지 않아야 합니다. Jackrabbit은 *escape()* 및 *escapePath()* 메서드를 사용합니다. JSP의 경우 Granite UI가 *granite:encodeURIPath() EL* 함수 위에 있어야 합니다.

### XSS API 및/또는 HTL을 사용하여 사이트 간 스크립팅 공격으로부터 보호합니다 {#use-the-xss-api-and-or-htl-to-protect-against-cross-site-scripting-attacks}

AEM은 XSS API를 제공하여 매개 변수를 쉽게 지우고 교차 사이트 스크립팅 공격으로부터 안전을 보장합니다. 또한 HTL에는 이러한 보호 기능이 템플릿 언어로 바로 내장되어 있습니다. API 치트 시트 를 다운로드할 수 있습니다 [개발 - 지침 및 우수 사례](/help/sites-developing/dev-guidelines-bestpractices.md).

### 적절한 로깅 구현 {#implement-appropriate-logging}

Java 코드의 경우 AEM은 메시지 로깅에 대한 표준 API로 slf4j를 지원하며 관리 일관성을 위해 OSGi 콘솔을 통해 사용할 수 있는 구성과 함께 사용해야 합니다. Slf4j는 5개의 서로 다른 로깅 수준을 표시합니다. 메시지를 기록할 수준을 선택할 때 다음 지침을 사용하는 것이 좋습니다.

* 오류: 코드가 손상되어 처리를 계속할 수 없습니다. 이는 종종 예상치 못한 예외로 인해 발생합니다. 일반적으로 이러한 시나리오에 스택 추적을 포함하는 것이 좋습니다.
* 경고: 제대로 작동하지 않지만 처리를 계속할 수 있는 경우 이는 종종 다음과 같이 우리가 예상했던 예외적인 결과로 나타날 것입니다. *PathNotFoundException*.
* 정보: 시스템을 모니터링할 때 유용한 정보입니다. 이것은 기본값이며 대부분의 고객은 이 설정을 환경에 그대로 둡니다. 따라서 너무 사용하지 마십시오.
* 디버그: 처리에 대한 낮은 수준 정보입니다. 지원 시 문제를 디버깅할 때 유용합니다.
* TRACE: 입력/종료와 같은 가장 낮은 수준 정보입니다. 일반적으로 개발자만 사용됩니다.

JavaScript의 경우 *console.log* 는 개발 중에만 사용해야 하며 모든 로그 문은 릴리스 전에 제거해야 합니다.

### 카고 컬트 프로그램 금지 {#avoid-cargo-cult-programming}

코드 내용을 이해하지 않고 코드를 복사하지 마십시오. 확실하지 않은 경우에는 모듈 또는 API에 대한 경험이 더 많은 사람에게 확실하지 않은 것이 좋습니다.
