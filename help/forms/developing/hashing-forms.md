---
title: 동적 PDF forms에서 해시를 생성하고 사용하는 방법
description: 동적 PDF forms에서 해시 생성 및 작업
exl-id: 026f5686-39ea-4798-9d1f-031f15941060
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: tm+mt
source-wordcount: '1256'
ht-degree: 0%

---

# 동적 PDF forms에서 해시 생성 및 작업 {#generate-work-with-hashes-dynamic-pdf-forms}


## 전제 조건 지식 {#prerequisite-knowledge}

스크립트 개체에서 함수 액세스 및 호출을 수행하는 기능처럼 JEE Designer에서 AEM Forms에 대한 경험이 필요합니다.

## 사용자 수준 {#user-level}

시작

PDF 양식에서 암호를 숨기려고 할 때 소스 코드 내부 또는 PDF 문서의 다른 곳에서 암호를 지우지 않으려면 MD4, MD5, SHA-1 및 SHA-256 해시를 생성하고 사용하는 방법을 알고 있어야 합니다.

고유한 해시를 생성하여 암호를 난독화하고 이 해시를 PDF 문서에 저장하는 것이 좋습니다. 이 고유한 해시는 다른 해시 함수에 의해 생성할 수 있으며, 이 문서에서 PDF 양식 내에 해시 함수를 생성하는 방법과 해시 함수를 사용하는 방법을 보여 드리겠습니다.

해시 함수는 임의의 길이의 긴 문자열(또는 메시지)을 입력으로 사용하고 메시지 다이제스트 또는 디지털 지문이라고도 하는 고정 길이 문자열을 출력으로 만듭니다.

JEE Designer의 AEM Forms을 사용하면 스크립트 개체에서 다른 해시 함수를 JavaScript로 구현하고 동적 PDF 문서 내에서 실행할 수 있습니다. 이 문서의 샘플 파일에 포함된 예제 PDF은 다음 해시 함수의 오픈 소스 구현을 사용합니다.

* MD4 및 MD5 - Ronald Rivest에서 설계

* NIST에 의해 정의된 대로 SHA-1 및 SHA-256

해시를 사용할 때 가장 큰 이점은 명확한 텍스트 문자열을 비교하여 직접 암호를 비교할 필요가 없다는 것입니다. 대신 두 암호의 두 해시를 비교할 수 있습니다. 두 개의 다른 문자열에 동일한 해시가 있을 가능성이 거의 없으므로 두 해시가 모두 동일하면 비교 문자열(이 경우 암호)도 동일하다고 간주할 수 있습니다.

>[!NOTE]
>
>MD4 또는 MD5에서 잘 알려진 몇 가지 보안 문제(해시 충돌이라고 함)가 있습니다. 이러한 해시 충돌과 다른 SHA-1 해시(무지개 테이블 포함) 때문에 두 번째 샘플에서 SHA-256 해시 함수에 집중하기로 결정했습니다.  자세한 내용은 [충돌](https://en.wikipedia.org/wiki/Hash_collision) 및 [무지개 테이블](https://en.wikipedia.org/wiki/Rainbow_table) 위키백과의 페이지.

## 스크립트 객체 검사 {#examining-script-objects}

JEE Designer의 AEM Forms에서 제공된 두 샘플 중 하나를 열면 계층 팔레트에서 4개의 스크립트 개체가 표시됩니다(아래 그림 참조).

![변수](assets/variables.jpg)

이러한 스크립트 개체 내에서 해시 함수의 JavaScript 구현을 보려면 스크립트 개체를 선택하고 스크립트 편집기에서 코드를 탐색합니다.  다음 각 해시 함수가 구현된 방식을 확인할 수 있습니다.

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

이 목록에서 볼 수 있듯이 해시의 다른 출력 유형에 사용할 수 있는 다양한 함수가 있습니다. 다음 중 하나를 선택할 수 있습니다 `hex_` 16진수의 경우 `b64_` Base64 인코딩 출력의 경우 또는 `str_` 단순 문자열 인코딩에 사용됩니다.

선택한 해시 함수에 따라 해시 길이는 달라집니다.

* MD4: 128비트
* MD5: 128비트
* SHA-1: 160비트
* SHA-256: 256비트

## 샘플 PDF forms 시도 {#try-sample-pdf-forms}

이 문서의 샘플 파일에는 두 개의 PDF forms이 포함되어 있습니다. 첫 번째 샘플에서는 문자열을 입력한 다음 문자열에 대한 MD4, MD5, SHA-1 및 SHA-256 해시 값을 생성할 수 있습니다.  두 번째 샘플은 올바른 암호를 입력하면 텍스트 필드를 잠금 해제하는 간단한 양식입니다.

### 샘플 1: 해시 생성 {#generating-dashes}

아래 절차에 따라 첫 번째 샘플을 사용해 보십시오.

1. 샘플 파일을 다운로드하여 압축을 푼 후에 JEE Designer에서 AEM Forms으로 hashing_forms_sample1.pdf를 엽니다. 또는 Adobe Reader 또는 Adobe Acrobat Professional을 사용하여 샘플을 열고 볼 수 있지만 소스 코드를 볼 수 없습니다.
1. 텍스트 필드에서 [!UICONTROL 텍스트 지우기] 해시할 암호 또는 다른 메시지를 입력합니다.
1. 네 개의 단추 중 하나를 클릭하여 MD4, MD5, SHA-1 또는 SHA-256 해시를 생성합니다. 눌렀던 단추에 따라 16진수 출력을 생성하는 네 개의 해시 함수 중 하나가 호출되고 문자열 또는 메시지가 해시됩니다.

해시 작업의 결과는 레이블이 지정된 필드에 표시됩니다 [!UICONTROL 해시]. 해시 길이는 선택한 해시 함수에 따라 달라집니다.

모든 샘플은 16진수를 출력 유형으로 사용합니다. 스크립트 편집기를 사용하여 샘플을 수정하고 출력 유형을 Base64 또는 단순 문자열로 변경할 수 있습니다.

### 샘플 2: 일치하는 암호 {#matching-passwords}

두 번째 샘플은 실제 암호를 표시하지 않고 백그라운드에서 해시를 비교하는 방법을 보여 줍니다. 입력한 암호가 해시됩니다. 보이지 않는 필드에 저장된 실제 암호도 해시됩니다. 비밀번호는 보이지 않기 때문이 아니라 해시되었기 때문에 안전합니다. 해시된 값에서 암호를 재구성할 수 없으므로 해시된 형식으로 암호를 노출해도 안전합니다. 비교는 해시 사이에만 수행되며, 일반 텍스트의 암호 사이에는 적용되지 않습니다. 두 해시가 모두 동일하면 암호가 동일하다고 간주할 수 있습니다.

아래 절차에 따라 두 번째 샘플을 사용해 보십시오.

1. 열기 `hashing_forms_sample2.pdf` JEE Designer에서 AEM Forms 사용. 또는 Adobe Reader 또는 Adobe Acrobat Professional을 사용하여 샘플을 열고 볼 수 있지만 소스 코드를 볼 수 없습니다.
1. 두 암호 필드 중 하나를 선택합니다. [!UICONTROL 암호 MAN] 또는 [!UICONTROL 암호 여성] 암호를 입력합니다.
   1. 남자의 비밀번호는 `bob`
   1. 여자의 비밀번호는 `alice`
1. 암호 필드에서 포커스를 이동하거나 Enter 키를 누르면 입력한 비밀번호의 해시가 자동으로 생성되어 백그라운드에서 올바른 비밀번호의 저장된 해시와 비교됩니다. 올바른 해시된 암호는 레이블이 지정된 보이지 않는 텍스트 필드에 저장됩니다 `passwd_man_hashed` 및 `passwd_woman_hashed`. 남자의 올바른 암호를 입력하면 텍스트 필드에 `Man 1` 및 `Man 2` 여기에 텍스트를 입력할 수 있도록 액세스할 수 있습니다. 그 여자의 분야에도 같은 행동이 적용된다.
1. 원할 경우 &quot;암호 삭제&quot;라는 버튼을 클릭하여 텍스트 필드를 비활성화하고 테두리를 변경할 수 있습니다.

두 해시된 값을 비교하고 텍스트 필드를 활성화할 코드는 간단합니다.

```xml
if (soHASHING_SHA256.hex_sha256(this.rawValue) == passwd_man_hashed.rawValue){
     VAL_man_1.access = "open";
     VAL_man_2.access = "open";
     VAL_man_1.borderColor = "0,255,0";
     VAL_man_2.borderColor = "0,255,0";
}
```

## 여기서 어디로 가야 합니까 {#next-steps}

이런 게 필요한 곳은 어디인가요? 권한이 있는 사용자만 입력해야 하는 필드가 있는 PDF 양식을 고려하십시오. Sample_2.pdf에서와 같이 문서의 어느 곳에서나 일반 텍스트에서 볼 수 없는 암호로 이러한 필드를 보호하면 암호를 알고 있는 사용자만 해당 필드에 액세스할 수 있습니다.

두 개의 샘플 PDF 파일을 계속 탐색하시기 바랍니다.  Sample_1.pdf를 사용하여 새 해시 값을 생성하고 생성된 값을 사용하여 암호나 Sample_2.pdf에 사용된 해시 함수를 변경할 수 있습니다.  기여도 섹션에 나열된 리소스는 해싱과 이 문서에서 사용되는 특정 JavaScript 구현에 대한 추가 정보도 제공합니다.

## 기여도 {#attributions}

* [로날드 리베스트](https://en.wikipedia.org/wiki/Ron_Rivest)
* [NIST](https://csrc.nist.gov/projects/cryptographic-standards-and-guidelines)
* [해시 충돌](https://en.wikipedia.org/wiki/Hash_collision)
* [무지개 테이블](https://en.wikipedia.org/wiki/Rainbow_table)
* [JavaScript MD5 프로젝트 홈 페이지](http://pajhome.org.uk/crypt/md5/)
* [jsSHA2 프로젝트 홈 페이지](https://anmar.eu.org/projects/jssha2/)
