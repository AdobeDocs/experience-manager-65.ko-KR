---
title: 동적 PDF forms에서 해시를 생성하고 사용하는 방법
description: 동적 PDF forms에서 해시 생성 및 작업
exl-id: 026f5686-39ea-4798-9d1f-031f15941060
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1189'
ht-degree: 0%

---

# 동적 PDF forms에서 해시 생성 및 작업 {#generate-work-with-hashes-dynamic-pdf-forms}

## 전제 조건 지식 {#prerequisite-knowledge}

스크립트 개체의 함수에 액세스하고 호출하는 기능과 마찬가지로 JEE Designer의 AEM Forms에 대한 일부 경험이 필요합니다.

## 사용자 수준 {#user-level}

시작

PDF 양식에서 암호를 숨기고 소스 코드 내부나 PDF 문서의 다른 곳에서 일반 텍스트로 숨기고 싶지 않을 경우 MD4, MD5, SHA-1 및 SHA-256 해시를 생성하고 사용하는 방법을 잘 알고 있어야 합니다.

고유한 해시를 생성하여 암호를 난독화하고 이 해시를 PDF 문서에 저장하자는 아이디어입니다. 이 고유한 해시는 다른 해시 함수에 의해 생성될 수 있으며 이 문서에서는 PDF 양식 내에서 해시 함수를 생성하는 방법과 이 함수를 사용하는 방법에 대해 설명합니다.

해시 함수는 임의의 길이의 긴 문자열(또는 메시지)을 입력으로 취하여 고정 길이의 문자열을 출력으로 생성하며, 메시지 다이제스트 또는 디지털 지문이라고도 합니다.

AEM Forms on JEE Designer를 사용하면 스크립트 개체에 있는 서로 다른 해시 함수를 JavaScript로 구현하고 동적 PDF 문서 내에서 실행할 수 있습니다. 이 문서의 샘플 파일에 포함된 예제 PDF은 다음 해시 함수의 오픈 소스 구현을 사용합니다.

* MD4 및 MD5 - Ronald Rivest 설계

* SHA-1 및 SHA-256 - NIST에 의해 정의된 대로

해시를 사용할 때 가장 큰 장점은 명확한 텍스트 문자열을 비교하여 암호를 직접 비교할 필요가 없다는 것입니다. 대신 두 암호의 두 해시를 비교할 수 있습니다. 두 개의 다른 문자열이 동일한 해시를 가질 가능성은 없으므로 두 해시가 동일하면 비교된 문자열(이 경우 암호)도 동일하다고 가정할 수 있습니다.

>[!NOTE]
>
>MD4 또는 MD5에는 몇 가지 잘 알려진 보안 문제(해시 충돌이라고 함)가 있습니다. 그 해시 충돌과 다른 SHA-1 해킹(무지개 테이블 포함) 때문에, 나는 두 번째 샘플에서 SHA-256 해시 함수에 집중하기로 결정했다. 자세한 내용은 [충돌](https://en.wikipedia.org/wiki/Hash_collision) 및 [무지개 테이블](https://en.wikipedia.org/wiki/Rainbow_table) 위키백과의 페이지들.

## 스크립트 오브젝트 검사 {#examining-script-objects}

JEE Designer의 AEM Forms에서 제공된 두 샘플 중 하나를 열면 계층 팔레트에서 네 개의 스크립트 개체가 표시됩니다(아래 그림 참조).

![변수](assets/variables.jpg)

이러한 스크립트 오브젝트 내에 있는 해시 함수의 JavaScript 구현을 보려면 스크립트 오브젝트를 선택하고 스크립트 편집기에서 코드를 탐색하십시오. 다음과 같은 각 해시 함수가 어떻게 구현되었는지 확인할 수 있습니다.

* soHASHING_MD4.hex_md4()
* soHASHING_MD4.b64_md4()
* soHASHING_MD4.str_md4()
* soHASHING_MD5.hex_md5()
* soHASHING_MD5.b64_md5()
* soHASHING_MD5.str_md5()
* soHASHING_SHA1.hex_sha1()
* soHASHING_SHA1.b64_sha1( )
* soHASHING_SHA1.str_sha1( )
* soHASHING_SHA256.hex_sha256()
* soHASHING_SHA256.b64_sha256()
* soHASHING_SHA256.str_sha256()

이 목록에서 볼 수 있듯이 해시의 출력 유형마다 사용할 수 있는 함수가 다릅니다. 다음 중 하나를 선택할 수 있습니다. `hex_` 16진수의 경우 `b64_` Base64로 인코딩된 출력의 경우 또는 `str_` 간단한 문자열 인코딩에 사용됩니다.

선택하는 해시 함수에 따라 해시의 길이가 달라집니다.

* MD4: 128비트
* MD5: 128비트
* SHA-1: 160비트
* SHA-256: 256비트

## 샘플 PDF forms 시도 {#try-sample-pdf-forms}

이 문서의 샘플 파일에는 두 개의 PDF forms이 포함되어 있습니다. 첫 번째 샘플을 사용하면 문자열을 입력한 다음 문자열에 대한 MD4, MD5, SHA-1 및 SHA-256 해시 값을 생성할 수 있습니다. 두 번째 샘플은 올바른 암호를 입력하면 텍스트 필드의 잠금을 해제하는 간단한 양식입니다.

### 샘플 1: 해시 생성 {#generating-dashes}

첫 번째 샘플을 시도하려면 아래 단계를 따르십시오.

1. 샘플 파일을 다운로드하여 압축을 푼 후에 JEE Designer에서 AEM Forms으로 hashing_forms_sample1.pdf를 엽니다. 또는 Adobe Reader 또는 Adobe Acrobat Professional을 사용하여 샘플을 열고 볼 수 있지만 소스 코드는 볼 수 없습니다.
1. 레이블이 지정된 텍스트 필드에서 [!UICONTROL 텍스트 지우기] 암호나 해시할 다른 메시지를 입력합니다.
1. 4개의 버튼 중 하나를 클릭하여 MD4, MD5, SHA-1 또는 SHA-256 해시를 생성합니다. 누른 단추에 따라 16진수 출력을 생성하는 네 개의 해시 함수 중 하나가 호출되고 문자열이나 메시지가 해시됩니다.

해시 작업의 결과가 레이블이 지정된 필드에 표시됩니다 [!UICONTROL 해시]. 해시의 길이는 선택한 해시 함수에 따라 다릅니다.

모든 샘플은 16진수를 출력 유형으로 사용합니다. 스크립트 편집기를 사용하여 샘플을 수정하고 출력 유형을 Base64 또는 단순 문자열로 변경할 수 있습니다.

### 예제 2: 일치하는 암호 {#matching-passwords}

두 번째 샘플은 실제 암호를 공개할 필요 없이 백그라운드에서 해시를 비교하는 방법을 보여 줍니다. 입력한 암호가 해시되었습니다. 보이지 않는 필드에 저장된 실제 암호도 해시됩니다. 비밀번호는 보이지 않기 때문이 아니라 해시되었기 때문에 안전하다. 해시된 값으로는 암호 재구성이 불가능하기 때문에 해시된 형태로 암호를 노출하는 것이 안전하다. 명확한 텍스트의 암호 사이가 아니라 해시 사이에서만 비교됩니다. 두 해시가 같으면 암호가 동일하다고 가정할 수 있다.

두 번째 샘플을 시도하려면 아래 단계를 따르십시오.

1. 열기 `hashing_forms_sample2.pdf` AEM Forms on JEE Designer. 또는 Adobe Reader 또는 Adobe Acrobat Professional을 사용하여 샘플을 열고 볼 수 있지만 소스 코드는 볼 수 없습니다.
1. 레이블이 지정된 두 개의 암호 필드 중 하나를 선택합니다. [!UICONTROL 비밀번호 담당자] 또는 [!UICONTROL 비밀번호 여자] 암호를 입력합니다.
   1. 그 남자의 암호는 `bob`
   1. 그 여자의 암호는 `alice`
1. 암호 필드 밖으로 포커스를 옮기거나 Enter 키를 누르면 입력한 암호의 해시가 자동으로 생성되고 백그라운드에서 저장된 정확한 암호의 해시와 비교됩니다. 해시된 올바른 암호는 레이블이 지정된 보이지 않는 텍스트 필드에 저장됩니다 `passwd_man_hashed` 및 `passwd_woman_hashed`. 정확한 비밀번호를 입력하면 텍스트 필드에 다음이 표시됩니다 `Man 1` 및 `Man 2` 에 액세스할 수 있으므로 텍스트를 입력할 수 있습니다. 여성의 밭에도 똑같은 행태가 적용된다.
1. 선택적으로 &quot;암호 삭제&quot; 단추를 클릭하여 텍스트 필드를 비활성화하고 테두리를 변경할 수 있습니다.

해시된 두 값을 비교하고 텍스트 필드를 활성화하는 코드는 간단합니다.

```xml
if (soHASHING_SHA256.hex_sha256(this.rawValue) == passwd_man_hashed.rawValue){
     VAL_man_1.access = "open";
     VAL_man_2.access = "open";
     VAL_man_1.borderColor = "0,255,0";
     VAL_man_2.borderColor = "0,255,0";
}
```

## 여기서 어디로 가야 합니까 {#next-steps}

이런 게 필요한 곳은 어디죠? 권한이 있는 개인만 채워야 하는 필드가 있는 PDF 양식을 생각해 보십시오. Sample_2.pdf에서처럼 문서의 어디에서든 일반 텍스트로 볼 수 없는 암호로 이러한 필드를 보호하면 암호를 아는 사용자만 해당 필드에 액세스할 수 있습니다.

두 샘플 PDF 파일을 계속 살펴보시기 바랍니다.  Sample_1.pdf로 새 해시 값을 생성하고 생성된 값을 사용하여 Sample_2.pdf에서 사용되는 암호 또는 해시 함수를 변경할 수 있습니다.  속성 섹션에 나열된 리소스는 해시 및 이 문서에 사용된 특정 JavaScript 구현에 대한 추가 정보도 제공합니다.

## 속성 {#attributions}

* [로널드 리베스트](https://en.wikipedia.org/wiki/Ron_Rivest)
* [NIST](https://csrc.nist.gov/projects/cryptographic-standards-and-guidelines)
* [해시 충돌](https://en.wikipedia.org/wiki/Hash_collision)
* [무지개 테이블](https://en.wikipedia.org/wiki/Rainbow_table)
* [JavaScript MD5 프로젝트 홈 페이지](https://pajhome.org.uk/crypt/md5/)
* [jsSHA2 프로젝트 홈 페이지](https://anmar.eu.org/projects/jssha2/)
