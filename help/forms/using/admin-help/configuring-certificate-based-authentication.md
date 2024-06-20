---
title: 인증서 기반 인증 구성
description: CA(인증 기관) 인증서를 Trust Store로 가져오고 인증서 기반 인증을 위한 인증서 매핑을 만듭니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 9cbea8c8-4d42-446b-b98d-c090709624d7
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms, Security
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 0%

---

# 인증서 기반 인증 구성 {#configuring-certificate-based-authentication}

User Management는 일반적으로 사용자 이름과 암호를 사용하여 인증을 수행합니다. 또한 사용자 관리는 Acrobat을 통해 사용자를 인증하거나 프로그래밍 방식으로 사용자를 인증하는 데 사용할 수 있는 인증서 기반 인증을 지원합니다. 프로그래밍 방식으로 사용자 인증에 대한 자세한 내용은 [AEM Forms를 사용한 프로그래밍](https://www.adobe.com/go/learn_aemforms_programming_63).

인증서 기반 인증을 사용하려면 신뢰할 수 있는 CA(인증 기관) 인증서를 Trust Store로 가져온 다음 인증서 매핑을 만듭니다.

## CA 인증서 가져오기 {#import-the-ca-certificate}

인증서를 가져올 때 인증서 인증을 위한 신뢰 및 ID를 위한 신뢰 옵션과 필요한 기타 옵션을 선택합니다. 인증서 가져오기에 대한 자세한 내용은 [인증서 관리](/help/forms/using/admin-help/certificates.md#managing-certificates).

## 인증서 매핑 구성 {#configuring-certificate-mapping}

사용자에 대해 인증서 기반 인증을 활성화하려면 인증서 매핑을 만듭니다. A *인증서 매핑* 는 인증서의 속성과 도메인의 사용자 속성 간의 맵을 정의합니다. 동일한 도메인에 두 개 이상의 인증서를 매핑할 수 있습니다.

인증서를 테스트할 때 User Management에서 인증서 검사를 업로드하여 다음 요구 사항을 충족하는지 확인합니다.

* 인증서가 유효합니다.
* 지정한 발급자가 인증서를 확인할 수 있습니다.
* 인증서에는 매핑에 필요한 속성이 포함되어 있습니다.
* 지정한 매핑은 AEM Forms 데이터베이스의 한 사용자만 인증서를 매핑합니다. 현재 사용자와 오래된(삭제된) 사용자 모두 매핑 기준과 일치하는지 여부를 확인하기 위해 확인됩니다. 따라서 오래된 사용자를 포함하여 두 명 이상의 사용자에게 속성 값이 고려되는 경우 인증서 테스트가 실패합니다.

>[!NOTE]
>
>기존 인증서 매핑은 편집할 수 없습니다.

**인증서 매핑 추가**

1. 관리 콘솔에서 설정 > 사용자 관리 > 구성 > 인증서 매핑 을 클릭합니다.
1. 새 인증서 매핑 을 클릭하고 발급자용 목록에서 Trust Store Management에 구성된 인증서 별칭을 선택합니다.
1. 인증서의 속성 중 하나를 사용자의 속성에 매핑합니다. 예를 들어 인증서의 일반 이름을 사용자의 로그인 ID에 매핑할 수 있습니다.

   인증서의 속성 콘텐츠가 사용자 관리 데이터베이스의 사용자 속성에 있는 콘텐츠와 다른 경우 Java 정규 표현식(regex)을 사용하여 두 속성을 일치시킬 수 있습니다. 예를 들어 인증서의 일반 이름이 와 같은 이름인 경우 *Alex Pink (인증)* 및 *Alex Pink(서명)* 및 사용자 관리 데이터베이스의 일반 이름은 입니다. *알렉스 핑크*&#x200B;를 설정하는 경우 정규 표현식을 사용하여 인증서 속성의 필요한 부분을 추출합니다(이 예에서는 *알렉스 핑크*.) 지정하는 정규 표현식은 Java 정규 표현식 사양을 준수해야 합니다.

   사용자 지정 순서 상자에서 그룹의 순서를 지정하여 표현식을 변환할 수 있습니다. 사용자 지정 순서는 `java.util.regex.Matcher.replaceAll()` 메서드를 사용합니다. 표시되는 비헤이비어는 해당 메서드의 비헤이비어에 해당하며, 이에 따라 입력 문자열(사용자 지정 순서)을 지정해야 합니다.

   정규 표현식을 테스트하려면 테스트 매개변수(Test Parameter) 상자에 값을 입력하고 테스트(Test)를 클릭합니다.

   정규 표현식에서 다음 문자를 사용할 수 있습니다.

   * . (모든 문자)
   * &amp;ast;(0회 이상)
   * ()(대괄호로 그룹 지정)
   * \ (정규 표현식 문자를 일반 문자로 이스케이프하는 데 사용됨)
   * $n (n번째 그룹을 참조하는 데 사용됨)

   정규 표현식의 예:

   * &quot;Alex Pink&quot;(인증)에서 &quot;Alex Pink&quot;를 추출하려면

     **정규 표현식:** (.&amp;ast;) \(Authentication\)

   * Alex (Authentication) Pink에서 &quot;Alex Pink&quot;를 추출하려면

     **정규 표현식:** (.&amp;ast;)\(Authentication\)(.&amp;ast;)

   * Alex (Authentication) Pink에서 &quot;Pink Alex&quot;를 추출하려면

     **정규 표현식:** (.&amp;ast;)\(Authentication\)(.&amp;ast;)

     사용자 정의 주문: $2 $1(첫 번째 그룹에 연결된 두 번째 그룹을 반환하고 공백 문자로 캡처됨)

   * &quot;smtp:apink@sampleorg.com&quot;에서 &quot;apink@sampleorg.com&quot;을 추출하려면

     **정규 표현식:** smtp:(.&amp;ast;)

   정규 표현식 사용에 대한 자세한 내용은 를 참조하십시오. [정규 표현식에 대한 Java 자습서](https://java.sun.com/docs/books/tutorial/essential/regex/).

1. 도메인용 목록에서 사용자의 도메인을 선택합니다.
1. 이 구성을 테스트하려면 찾아보기 를 클릭하여 샘플 사용자 인증서를 업로드하고 인증서 테스트 를 클릭한 다음 구성이 올바른 경우 확인 을 클릭합니다.

**기존 인증서 매핑 편집**

1. Administration Console에서 설정 > 사용자 관리 > 구성을 클릭합니다.
1. 인증서 매핑 을 클릭합니다.
1. 구성을 편집 및 편집하려면 인증서 매핑을 선택합니다. 정규 표현식과 사용자 지정 순서를 업데이트할 수 있습니다.
1. 변경 사항을 테스트하려면 [찾아보기]를 클릭하여 샘플 인증서를 업로드하고 [인증서 테스트]를 클릭한 다음 [확인]을 클릭합니다.

**인증서 매핑 삭제**

1. 관리 콘솔에서 설정 > 사용자 관리 > 구성 > 인증서 매핑 을 클릭합니다.
1. 삭제할 인증서 매핑에 대한 확인란을 선택하고 삭제 를 클릭한 다음 확인 을 클릭합니다.
