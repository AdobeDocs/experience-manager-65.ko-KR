---
title: 코딩 팁
seo-title: 코딩 팁
description: AEM 코딩 팁
seo-description: AEM 코딩 팁
uuid: 1bb1cc6a-3606-4ef4-a8dd-7c08a7cf5189
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 4adce3b4-f209-4a01-b116-a5e01c4cc123
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '874'
ht-degree: 0%

---


# 코딩 팁{#coding-tips}

## {#use-taglibs-or-htl-as-much-as-possible}만큼 태그릿이나 HTL을 사용하십시오.

JSP에 scriptlet을 포함하면 코드에서 문제를 디버깅하는 것이 어렵습니다. 또한 JSP에 scriptlet을 포함함으로써 단일 책임 원칙 및 MVC 디자인 패턴을 위반하는 보기 레이어와 비즈니스 로직을 구분하는 것은 어렵습니다.

### 읽을 수 있는 코드 {#write-readable-code} 쓰기

코드는 한 번 작성되지만 여러 번 읽습니다. 작성 코드를 정리하기 위해 시간을 좀 더 할애하면 Adobe와 다른 개발자들이 나중에 이 코드를 읽어야 할 때 배당금을 지불할 것입니다.

### {#choose-intention-revealing-names} 이름을 표시하는 의도 선택

이상적으로 다른 프로그래머는 컨텐츠를 이해하기 위해 모듈을 열 필요가 없습니다. 마찬가지로, 그들은 어떤 방법이 그것을 읽지 않고 무엇을 하는지 말할 수 있어야 한다. 이러한 아이디어를 보다 잘 구독하면 보다 쉽게 코드를 읽을 수 있고 보다 빠르게 코드를 작성하고 변경할 수 있습니다.

AEM 코드 베이스에서 다음 규칙이 사용됩니다.


* 인터페이스의 단일 구현 이름은 `<Interface>Impl`, 즉`ReaderImpl`.
* 인터페이스의 여러 구현 이름이 `<Variant><Interface>`(예:`JcrReader` 및 `FileSystemReader`.
* 추상 기본 클래스의 이름은 `Abstract<Interface>` 또는 `Abstract<Variant><Interface>`입니다.
* 패키지의 이름은 `com.adobe.product.module`입니다.  각 Maven 아티팩트 또는 OSGi 번들에는 고유의 패키지가 있어야 합니다.
* Java 구현은 API 아래의 구현 패키지에 배치됩니다.


이러한 규칙을 고객 구현에 반드시 적용할 필요는 없지만 규칙을 정의하고 준수하여 코드를 유지 관리할 수 있어야 합니다.

이상적으로, 이름들은 그들의 의도를 드러내야 한다. 이름이 분명하지 않은 경우에 대한 일반적인 코드 테스트는 변수나 메서드가 의미하는 것을 설명하는 주석이 있는 것입니다.

<table>
 <tbody>
  <tr>
   <td><p><strong>불명확한 항목</strong></p> </td>
   <td><p><strong>지우기</strong></p> </td>
  </tr>
  <tr>
   <td><p>d.//일 단위 경과 시간</p> </td>
   <td><p>int elapsedTimeInDays;</p> </td>
  </tr>
  <tr>
   <td><p>//태그 있는 이미지<br /> 공용 목록 getItems() {} 가져오기</p> </td>
   <td><p>공용 목록 getTaggedImages() {}</p> </td>
  </tr>
 </tbody>
</table>

### {#don-t-repeat-yourself} 자신을 반복하지 마십시오.

DRY는 동일한 코드 집합을 복제할 수 없다고 말합니다. 이것은 문자열 리터럴과 같은 것에도 적용됩니다. 코드 복사는 어떤 것이 변해야 할 때마다 결함의 문을 열고, 찾고 제거해야만 한다.

### 벌거벗은 CSS 규칙 {#avoid-naked-css-rules} 방지

CSS 규칙은 애플리케이션 컨텍스트에서 대상 요소에 따라 달라야 합니다. 예를 들어 *.content.center*&#x200B;에 적용되는 CSS 규칙은 지나치게 광범위하며 잠재적으로 시스템 전체에 걸쳐 많은 컨텐츠에 영향을 줄 수 있으므로 나중에 다른 사람이 이 스타일을 무시할 것을 요구합니다. *.myapp-* centertext는 응용 프로그램 컨텍스트의 가운데 텍스트를 지정할 때  ** 보다 구체적인 규칙이어야 합니다.

### 사용되지 않는 API {#eliminate-usage-of-deprecated-apis} 사용 제거

API가 더 이상 사용되지 않을 때 사용되지 않는 API에 의존하지 않고 항상 새로운 권장 방법을 찾는 것이 좋습니다. 향후 업그레이드를 보다 원활하게 진행할 수 있습니다.

### 지역화할 수 있는 코드 {#write-localizable-code} 작성

작성자가 제공하지 않는 모든 문자열은 JavaScript의 *I18n.get()* JSP/Java의 *CQ.I18n.get()*&#x200B;을 통해 AEM i18n 사전에 대한 호출로 둘러싸야 합니다. 이 구현은 구현을 찾을 수 없는 경우 전달된 문자열을 반환하므로 기본 언어로 기능을 구현한 후 로컬라이제이션을 유연하게 구현할 수 있습니다.

### 안전을 위한 리소스 경로 이스케이프{#escape-resource-paths-for-safety}

JCR의 패스에는 공백이 없어야 하지만 공백이 있으면 코드가 깨지지 않습니다. Jackrabbit는 *escape()* 및 *escapePath()* 메서드를 사용하여 Text 유틸리티 클래스를 제공합니다. JSP의 경우 Granite UI는 *granite:encodeURIPath() EL* 함수를 표시합니다.

### XSS API 및/또는 HTL을 사용하여 사이트 간 스크립팅 공격 {#use-the-xss-api-and-or-htl-to-protect-against-cross-site-scripting-attacks} 방지

AEM은 XSS API를 통해 손쉽게 매개 변수를 정리하고 사이트 간 스크립팅 공격에 따른 안전 조치를 보장합니다. 또한 HTL은 이러한 보호 기능을 템플릿 언어로 바로 구축했습니다. API 요약서는 [개발 - 지침 및 우수 사례](/help/sites-developing/dev-guidelines-bestpractices.md)에서 다운로드할 수 있습니다.

### 적절한 로깅 구현 {#implement-appropriate-logging}

Java 코드의 경우, AEM은 메시지 로깅을 위한 표준 API로 slf4j를 지원하며 관리의 일관성을 위해 OSGi 콘솔을 통해 사용할 수 있는 구성과 함께 사용해야 합니다. Slf4j는 5개의 서로 다른 로깅 수준을 표시합니다. 메시지를 기록할 수준을 선택할 때는 다음 지침을 사용하는 것이 좋습니다.

* 오류:코드가 손상되어 처리를 계속할 수 없습니다. 이는 예상치 못한 예외로 인해 발생하는 경우가 많습니다. 일반적으로 이러한 시나리오에 스택 추적을 포함하는 것이 유용합니다.
* 경고:제대로 작동하지 않지만 처리를 계속할 수 있습니다. 이것은 종종 *PathNotFoundException*&#x200B;과 같이 우리가 예상했던 예외의 결과입니다.
* 정보:시스템을 모니터링할 때 유용한 정보입니다. 이것이 기본값이며 대부분의 고객은 이 설정을 환경에 그대로 둡니다. 그러므로 그것을 지나치게 사용하지 말아라.
* 디버그:처리에 대한 하위 수준 정보. 지원 관련 문제를 디버깅할 때 유용합니다.
* TRACE:가장 낮은 수준 정보(예: 메서드 입력/종료). 일반적으로 개발자만 사용합니다.

JavaScript의 경우, *console.log*&#x200B;는 개발 중에만 사용해야 하며 모든 로그 문은 릴리스 전에 제거해야 합니다.

### 카고 컬트 프로그램 방지 {#avoid-cargo-cult-programming}

코드 내용을 이해하지 않고 코드를 복사하지 마십시오. 확실하지 않은 경우 모듈 또는 API에 대해 더 많은 경험이 있는 사람에게 명확하지 않은 것을 확인하는 것이 가장 좋습니다.
