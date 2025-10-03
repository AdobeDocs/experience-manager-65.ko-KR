---
title: 인증서 기반 인증 구성
description: CA(인증 기관) 인증서를 Trust Store로 가져와서 인증서 기반 인증을 위한 인증서 매핑을 만듭니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 9cbea8c8-4d42-446b-b98d-c090709624d7
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Security
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '730'
ht-degree: 100%

---

# 인증서 기반 인증 구성 {#configuring-certificate-based-authentication}

>[!NOTE]
> 
> 사용자에게 관리자 콘솔에 액세스할 수 있는 관리자 권한이 있는지 확인하십시오.

사용자 관리에서는 일반적으로 사용자 이름 및 암호를 사용하여 인증을 수행합니다. 인증서 기반 인증도 지원하며 이를 통해 Acrobat을 통해 사용자를 인증하거나 프로그래밍 방식으로 사용자를 인증할 수 있습니다. 프로그래밍 방식으로 사용자를 인증하는 방법에 대한 자세한 내용은 [AEM Forms를 사용한 프로그래밍](https://www.adobe.com/go/learn_aemforms_programming_63)을 참조하십시오.

인증서 기반 인증을 사용하려면 신뢰하는 CA(인증 기관) 인증서를 Trust Store로 가져온 후 인증서 매핑을 만듭니다.

## CA 인증서 가져오기 {#import-the-ca-certificate}

인증서를 가져올 때 인증서 인증에 대한 신뢰 및 ID에 대한 신뢰 옵션을 선택하고 필요한 다른 옵션도 선택합니다. 인증서 가져오기에 대한 자세한 내용은 [인증서 관리](/help/forms/using/admin-help/certificates.md#managing-certificates)를 참조하십시오.

## 인증서 매핑 구성 {#configuring-certificate-mapping}

사용자에 대한 인증서 기반 인증을 활성화하려면 인증서 매핑을 만듭니다. *인증서 매핑*&#x200B;은 인증서 속성과 도메인 내 사용자 속성 간의 맵을 정의합니다. 동일한 도메인에 두 개 이상의 인증서를 매핑할 수 있습니다.

인증서를 테스트할 때 사용자 관리에서는 인증서 검사를 업로드하여 인증서가 다음과 같은 요구 사항을 충족하는지 확인합니다.

* 인증서가 유효합니다.
* 지정한 발급자가 인증서를 확인할 수 있습니다.
* 인증서에는 매핑에 필요한 속성이 포함되어 있습니다.
* 지정한 매핑은 인증서를 AEM Forms 데이터베이스에 있는 사용자 한 명에게만 매핑합니다. 현재 사용자와 더 이상 사용되지 않는(삭제된) 사용자를 모두 검사하여 매핑 기준에 부합하는지 여부를 확인합니다. 따라서 더 이상 사용되지 않는 사용자를 포함하여 두 명 이상의 사용자에게 고려 중인 속성 값이 있으면 인증서 테스트가 실패합니다.

>[!NOTE]
>
>기존 인증서 매핑을 편집할 수 없습니다.

**인증서 매핑 추가**

1. 관리 콘솔에서 설정 > 사용자 관리 > 구성 > 인증서 매핑을 클릭합니다.
1. 새 인증서 매핑을 클릭하고 발급자용 목록에서 Trust Store 관리에 구성된 인증서 별칭을 선택합니다.
1. 인증서 속성 중 하나를 사용자 속성에 매핑합니다. 예를 들어 인증서의 일반 이름을 사용자의 로그인 ID에 매핑할 수 있습니다.

   인증서의 속성 내용이 사용자 관리 데이터베이스의 사용자 속성 내용과 다른 경우 Java 정규 표현식(regex)을 사용하여 두 속성을 일치시킬 수 있습니다. 예를 들어 인증서의 일반 이름이 *Alex Pink(Authentication)* 및 *Alex Pink(Signing)*&#x200B;와 같은 이름이고 사용자 관리 데이터베이스의 일반 이름이 *Alex Pink*&#x200B;인 경우 정규 표현식을 사용하여 인증서 속성의 필수 부분(이 예에서는 *Alex Pink*)을 추출합니다. 지정한 정규 표현식은 Java 정규 표현식 사양을 준수해야 합니다.

   사용자 정의 순서 상자에서 그룹 순서를 지정하여 표현식을 변환할 수 있습니다. 사용자 정의 순서는 `java.util.regex.Matcher.replaceAll()` 메서드와 함께 사용됩니다. 표시되는 동작은 해당 메서드의 동작과 일치하며 입력 문자열(사용자 정의 순서)도 그에 따라 지정해야 합니다.

   정규 표현식을 테스트하려면 테스트 매개변수 상자에 값을 입력하고 테스트를 클릭합니다.

   정규 표현식에서 다음 문자를 사용할 수 있습니다.

   * . (모든 문자)
   * &amp;ast; (0회 이상 발생 횟수)
   * () (괄호 안에 그룹 지정)
   * \ (정규 표현식 문자를 일반 문자로 이스케이프 처리하는 데 사용됨)
   * $n (n번째 그룹을 나타내는 데 사용됨)

   정규 표현식의 예:

   * &#39;Alex Pink(Authentication)&#39;에서 &#39;Alex Pink&#39;를 추출하는 방법

     **정규 표현식:** (.&amp;ast;) \(Authentication\)

   * &#39;Alex (Authentication) Pink&#39;에서 &#39;Alex Pink&#39;를 추출하는 방법

     **정규 표현식:** (.&amp;ast;)\(Authentication\) (.&amp;ast;)

   * &#39;Alex (Authentication) Pink&#39;에서 &#39;Pink Alex&#39;를 추출하는 방법

     **정규 표현식:** (.&amp;ast;)\(Authentication\) (.&amp;ast;)

     사용자 정의 순서: $2 $1(두 번째 그룹을 반환하고 첫 번째 그룹에 연결하며 공백 문자로 캡처됨)

   * &#39;smtp:apink@sampleorg.com&#39;에서 &#39;apink@sampleorg.com&#39;을 추출하는 방법

     **정규 표현식:** smtp:(.&amp;ast;)

   정규 표현식 사용에 대한 자세한 내용은 [Java 정규 표현식 튜토리얼](https://java.sun.com/docs/books/tutorial/essential/regex/)을 참조하십시오.

1. 도메인용 목록에서 사용자 도메인을 선택합니다.
1. 이 구성을 테스트하려면 찾아보기를 클릭하여 샘플 사용자 인증서를 업로드하고 인증서 테스트를 클릭한 후 구성이 올바르면 확인을 클릭합니다.

**기존 인증서 매핑 편집**

1. 관리 콘솔에서 설정 > 사용자 관리 > 구성을 클릭합니다.
1. 인증서 매핑을 클릭합니다.
1. 편집할 인증서 매핑을 선택하고 구성을 편집합니다. 정규 표현식과 사용자 정의 순서를 업데이트할 수 있습니다.
1. 변경 사항을 테스트하려면 찾아보기를 클릭하여 샘플 인증서를 업로드하고 인증서 테스트를 클릭한 후 확인을 클릭합니다.

**인증서 매핑 삭제**

1. 관리 콘솔에서 설정 > 사용자 관리 > 구성 > 인증서 매핑을 클릭합니다.
1. 삭제할 인증서 매핑의 확인란을 선택하고 삭제를 클릭한 후 확인을 클릭합니다.
