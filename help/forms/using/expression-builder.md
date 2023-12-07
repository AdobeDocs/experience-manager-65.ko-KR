---
title: Expression Builder의 원격 함수
description: 서신 관리의 표현식 빌더 를 사용하여 표현식과 원격 함수를 만들 수 있습니다.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
docset: aem65
feature: Correspondence Management
exl-id: b41af9fe-c698-44b3-9ac6-97d42cdc02d4
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 1%

---

# Expression Builder의 원격 함수{#remote-functions-in-expression-builder}

표현식 빌더를 사용하여 데이터 사전이나 최종 사용자가 제공한 데이터 값에 대한 계산을 수행하는 표현식 또는 조건을 만들 수 있습니다. 서신 관리는 표현식 평가 결과를 사용하여 텍스트, 이미지, 목록 및 조건 등의 에셋을 선택하고 필요에 따라 서신에 삽입합니다.

## 표현식 빌더를 사용하여 표현식 및 원격 함수 만들기 {#creating-expressions-and-remote-functions-with-expression-builder}

표현식 빌더는 내부적으로 JSP EL 라이브러리를 사용하므로 표현식은 JSPEL 구문을 준수합니다. 자세한 내용은 [표현식 예](#exampleexpressions).

![표현식 빌더](assets/expressionbuilder.png)

### 연산자 {#operators}

표현식에서 사용할 수 있는 연산자는 표현식 빌더의 맨 위 막대에서 사용할 수 있습니다.

### 표현식 예 {#exampleexpressions}

다음은 서신 관리 솔루션에서 사용할 수 있는 일반적으로 사용되는 JSP EL 예입니다.

* 두 개의 숫자를 추가하려면: ${number1 + number2}
* 두 문자열을 연결하려면 ${str1} ${str2}
* 두 숫자를 비교하려면: ${age &lt; 18}

다음에서 자세한 정보를 찾을 수 있습니다. [JSP EL 사양](https://download.oracle.com/otn-pub/jcp/jsp-2.1-fr-spec-oth-JSpec/jsp-2_1-fr-spec-el.pdf). 클라이언트측 표현식 관리자는 JSP EL 사양의 특정 변수 및 함수, 특히

* 컬렉션 인덱스 및 맵 키(사용) [] notation)은 클라이언트측에서 평가된 표현식에 대한 변수 이름에서 지원되지 않습니다.
* 다음은 표현식에 사용되는 매개 변수 유형 또는 함수 반환 유형입니다.

   * java.lang.String
   * java.lang.Character
   * Char
   * java.lang.Boolean
   * 부울
   * java.lang.Integer
   * 정수
   * java.util.list
   * java.lang.Short
   * 짧음
   * java.lang.Byte
   * 바이트
   * java.lang.Double
   * 더블
   * java.lang.Long
   * 긴
   * java.lang.Float
   * 부동
   * java.util.Calendar
   * java.util.Date
   * java.util.List

### 원격 기능 {#remote-function}

원격 함수는 표현식에서 사용자 지정 논리를 사용하는 기능을 제공합니다. Java에서 메서드로 표현식에 사용할 사용자 지정 논리를 작성할 수 있으며 표현식 내에서 동일한 함수를 사용할 수 있습니다. 사용 가능한 원격 함수는 표현식 편집기 왼쪽의 &quot;원격 함수&quot; 탭에 나열됩니다.

![remotefunction](assets/remotefunction.png)

#### 사용자 정의 원격 함수 추가 {#adding-custom-remote-functions}

사용자 지정 번들을 만들어 표현식 내에서 사용할 고유한 원격 함수를 내보낼 수 있습니다. 사용자 정의 번들을 만들어 자신의 원격 함수를 내보내려면 다음 작업을 수행하십시오. 입력 문자열을 대문자로 사용하는 사용자 지정 함수를 작성하는 방법을 보여 줍니다.

1. Expression Manager에서 사용하기 위해 내보내는 메서드가 포함된 OSGi 서비스에 대한 인터페이스를 정의합니다.
1. 인터페이스 A에서 메서드를 선언하고 @ServiceMethod 주석(com.adobe.exm.expeval.ServiceMethod)으로 주석을 답니다. Expression Manager에서는 주석이 없는 메서드는 모두 무시합니다. ServiceMethod 주석에는 다음과 같은 선택적 특성이 있으며 이 특성을 지정할 수도 있습니다.

   1. **활성화됨**: 이 메서드가 활성화되어 있는지 여부를 결정합니다. 표현식 관리자는 비활성화된 메서드를 무시합니다.
   1. **familyId**: 메서드의 제품군(그룹)을 지정합니다. 비어 있는 경우 Expression Manager는 메서드가 기본 패밀리에 속한다고 가정합니다. 함수가 선택된 패밀리(기본 패밀리는 제외)의 레지스트리는 없습니다. Expression Manager는 다양한 번들에서 내보낸 모든 함수에 지정된 모든 패밀리 ID를 결합하여 레지스트리를 동적으로 만듭니다. 여기서 지정하는 ID는 표현식 작성 사용자 인터페이스에도 표시되므로 합리적으로 읽을 수 있는지 확인합니다.
   1. **displayName**: 사람이 인식할 수 있는 함수 이름입니다. 이 이름은 작성 사용자 인터페이스에서 표시 목적으로 사용됩니다. 비어 있는 경우 Expression Manager는 함수의 접두사와 local-name을 사용하여 기본 이름을 구성합니다.
   1. **설명**: 함수에 대한 자세한 설명입니다. 이 설명은 작성 사용자 인터페이스에서 표시 목적으로 사용됩니다. 비어 있는 경우 Expression Manager는 함수의 접두사와 local-name을 사용하여 기본 설명을 구성합니다.

   ```java
   package mergeandfuse.com;
   import com.adobe.exm.expeval.ServiceMethod;
   
   public interface RemoteFunction {
    @ServiceMethod(enabled=true,displayName="Returns_all_caps",description="Function to convert to all CAPS", familyId="remote")
    public String toAllCaps(String name);
   
   }
   ```

   @ServiceMethodParameter 주석(com.adobe.exm.expeval.ServiceMethodParameter)을 사용하여 메서드의 매개 변수에 선택적으로 주석을 추가할 수도 있습니다. 이 주석은 작성 사용자 인터페이스에서 사용할 메서드 매개 변수의 사람이 읽을 수 있는 이름 및 설명을 지정하는 데만 사용됩니다. 인터페이스 메서드의 매개 변수와 반환 값이 다음 유형 중 하나에 속하는지 확인합니다.

   * java.lang.String
   * java.lang.Character
   * Char
   * java.lang.Boolean
   * 부울
   * java.lang.Integer
   * 정수
   * java.lang.Short
   * 짧음
   * java.lang.Byte
   * 바이트
   * java.lang.Double
   * 더블
   * java.lang.Long
   * 긴
   * java.lang.Float
   * 부동
   * java.util.Calendar
   * java.util.Date
   * java.util.List

1. 인터페이스의 구현을 정의하고 OSGI 서비스로 구성한 다음 다음 서비스 속성을 정의합니다.

```jsp
@org.apache.felix.scr.annotations.Properties({
  @org.apache.felix.scr.annotations.Property(name = "connectors.jsoninvoker", boolValue = true),
  @org.apache.felix.scr.annotations.Property(name = "connectors.jsoninvoker.alias", value = "<service_id>"),
  @org.apache.felix.scr.annotations.Property(name = "exm.service", boolValue = true)})
```

exm.service=true 항목은 Expression Manager에게 해당 서비스에 표현식에 사용하기에 적합한 원격 함수가 포함되어 있음을 알립니다. 다음 &lt;service_id> 값은 유효한 Java 식별자(영숫자,$, _(다른 특수 문자 없음)여야 합니다. REMOTE_ 키워드 접두사가 있는 이 값은 표현식 내에서 사용되는 접두사를 형성합니다. 예를 들어 서비스 속성에서 서비스 ID foo 및 주석이 달린 인터페이스는 REMOTE_foo:bar()를 사용하여 표현식 내에서 참조할 수 있습니다.

```java
package mergeandfuse.com;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;

@Component(metatype = true, immediate = true, label = "RemoteFunctionImpl")
@Service(value = RemoteFunction.class)
@org.apache.felix.scr.annotations.Properties({
  @org.apache.felix.scr.annotations.Property(name = "connectors.jsoninvoker", boolValue = true),
  @org.apache.felix.scr.annotations.Property(name = "connectors.jsoninvoker.alias", value = "test1"),
  @org.apache.felix.scr.annotations.Property(name = "exm.service", boolValue = true)})
public class RemoteFuntionImpl implements RemoteFunction {

 @Override
 public String toAllCaps(String name) {
  System.out.println("######Got######"+name);
  
  return name.toUpperCase();
 }
 
}
```

다음은 사용할 샘플 아카이브입니다.

* **GoodFunctions.jar.zip** 는 샘플 원격 함수 정의가 포함된 번들이 있는 jar 파일입니다. GoodFunctions.jar.zip 파일을 다운로드하고 압축 해제하여 jar 파일을 가져옵니다.
* **GoodFunctions.zip** 사용자 지정 원격 함수를 정의하고 해당 함수를 위한 번들을 만들기 위한 소스 코드 패키지입니다.

GoodFunctions.jar.zip

[파일 가져오기](assets/goodfunctions.jar.zip)

GoodFunctions.zip

[파일 가져오기](assets/goodfunctions.zip)
