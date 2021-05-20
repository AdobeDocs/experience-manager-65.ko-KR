---
title: HTML5 양식에 대한 그림 절 지원
seo-title: HTML5 양식에 대한 그림 절 지원
description: HTML5 양식은 날짜, 텍스트 및 숫자 심볼에 대한 표시 값과 형식이 지정된 값에 대한 XFA Picture 절을 지원합니다.
seo-description: HTML5 양식은 날짜, 텍스트 및 숫자 심볼에 대한 표시 값과 형식이 지정된 값에 대한 XFA Picture 절을 지원합니다.
uuid: ca5074ce-8219-4f27-a37c-b1f0dca4ce03
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 5e344be7-46cd-4e1f-ae3a-1f89c645cffe
feature: Mobile Forms
exl-id: 7f9c77c6-447a-407f-ae58-6735176dc99c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 1%

---

# HTML5 양식에 대한 그림 절 지원 {#picture-clause-support-for-html-forms}

HTML5 양식은 날짜, 텍스트 및 숫자 심볼에 대한 표시 값과 형식이 지정된 값에 대한 XFA Picture 절을 지원합니다. 다음 그림 절 식이 지원됩니다.

* category(locale){picture-clause} | category(locale){picture-clause} | category(locale){picture-clause}
* category.subcategory{}

>[!NOTE]
>
>현재 Mobiles Forms은 그림 편집 절을 지원하지 않습니다. 또한 DateTime 및 Time Picture 절 기호가 지원되지 않습니다.

## 지원되는 날짜 필드 기호 {#supported-date-field-symbols}

날짜 그림 절에 대해 지원되는 식:

* date.long{}
* date.short{}
* date.medium{}
* date.full{}
* date.short{}
* 날짜{날짜 그림 절 기호}

>[!NOTE]
>
>그림 절의 기본 패턴은 {MMM D, YYYY} 패턴입니다. 패턴이 적용되지 않으면 기본 패턴이 사용됩니다.

<table>
 <tbody>
  <tr>
   <th><strong>기호</strong></th>
   <th>해석</th>
  </tr>
  <tr>
   <td>D</td>
   <td>월의 1자리 또는 2자리(1-31) 날짜</td>
  </tr>
  <tr>
   <td>DD</td>
   <td>0으로 채워지는 두 자리(01-31)일.<br /> </td>
  </tr>
  <tr>
   <td>M</td>
   <td>해당 연도의 1 또는 2자리(1-12) 월<br /> </td>
  </tr>
  <tr>
   <td>MM</td>
   <td>한 해의 두 자리(01-12)를 0으로 패딩합니다.<br /> </td>
  </tr>
  <tr>
   <td>MMM</td>
   <td>현재 로케일의 축약된 월 이름<br /> </td>
  </tr>
  <tr>
   <td>MMMM</td>
   <td>현재 로케일의 전체 월 이름<br /> </td>
  </tr>
  <tr>
   <td>EEE</td>
   <td>현재 로케일의 약식 요일 이름<br /> </td>
  </tr>
  <tr>
   <td>EEE</td>
   <td>현재 로케일의 전체 요일 이름<br /> </td>
  </tr>
  <tr>
   <td>YY</td>
   <td>2자리 연도, 여기서 00 = 2000, 29 = 2029, 30 = 1930 및 99 = 1999<br /> </td>
  </tr>
  <tr>
   <td>YYYY</td>
   <td>4자리 연도<br /> </td>
  </tr>
 </tbody>
</table>

## 숫자 그림 절 {#numeric-picture-clause}

HTML5 양식은 숫자 그림 기호를 지원합니다. 그러나 PDF forms과 HTML Forms 간에 지원에 차이가 있습니다.

**PDF forms**&#x200B;에서는 Picture 절의 기호 수에 관계없이 숫자가 지정됩니다

**HTML Forms**&#x200B;에서는 숫자가 Picture 절의 기호 수보다 작은 경우에만 숫자가 서식이 지정됩니다.

**예**:그림 절을 고려하십시오.num{zzz,zzz,zz9}.

숫자 **10000**&#x200B;은 HTML과 PDF forms 모두에서 **10,000**&#x200B;으로 지정됩니다.

숫자 1000000은 PDF forms에서 1,000,000으로 서식이 지정됩니다. 그러나 HTML Forms에서는 숫자가 1000000.

**HTML Forms**&#x200B;에서 숫자 그림 절에 대해 지원되는 식은 다음과 같습니다.

* num.integer{}
* num.decimal{}
* num.currency{}
* num.percent{}
* num{숫자 그림 절 기호}

<table>
 <tbody>
  <tr>
   <th><strong>기호</strong></th>
   <th><strong>해석</strong></th>
   <th>입력 구문 분석</th>
  </tr>
  <tr>
   <td>9</td>
   <td><strong>출력 형식</strong>:한 자리. 또는 입력 데이터가 비어 있거나 해당 위치의 공백이 있는 경우 0자리 수입니다.<br /> </td>
   <td>단일 숫자</td>
  </tr>
  <tr>
   <td>Z</td>
   <td><strong>출력 형식</strong>:한 자리. 또는 입력 데이터가 비어 있는 경우 해당 위치에서 공백 또는 0자리 숫자가 있는 경우 스페이스의 경우<br /> </td>
   <td>한 자리 또는 공백</td>
  </tr>
  <tr>
   <td>z</td>
   <td><strong>출력 형식</strong>:한 자리. 또는 입력 데이터가 비어 있거나, 공백 또는 해당 위치에서 0자리 숫자가 있는 경우에는 아무 것도 아닙니다.<br /> </td>
   <td>한 자리 또는 아무것도 아님</td>
  </tr>
  <tr>
   <td>오류</td>
   <td><strong>출력 형식</strong>:지수 기호(E)로 구성된 부동 소수점 번호의 지수 부분입니다. 뒤에 선택적 더하기 또는 빼기 기호가 옵니다. 뒤에 지수 값이 옵니다.<br /> </td>
   <td>출력 서식과 동일합니다</td>
  </tr>
  <tr>
   <td>CR 또는 cr<br /> </td>
   <td>음수인 경우 신용 기호(CR) 다른 건 없어요</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>S 또는 s<br /> </td>
   <td>출력 형식:숫자가 음수이면 빼기 기호. Else space.<br /> </td>
   <td>숫자가 음수이면 빼기 기호. 플러스 부호</td>
  </tr>
  <tr>
   <td>V</td>
   <td>일반 로케일의 소수점 반입니다. 입력 구문 분석 시 소수점 반사를 암시하도록 허용합니다.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>v</td>
   <td>일반 로케일의 소수점 반입니다. 입력 구문 분석 및 출력 형식 지정 시 소수점 반사를 암시하도록 허용합니다.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>.</td>
   <td>일반 로케일의 소수점 반입니다.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>, (U+FF0C)</td>
   <td>일반 로케일의 그룹화 구분 기호</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>$(U+FF04)</td>
   <td>일반 로케일의 통화 기호입니다.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>% (U+FF05)</td>
   <td>일반 로케일의 퍼센트 기호입니다.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>( (U+FF08)</td>
   <td>숫자가 음수인 경우 왼쪽 괄호. 다른 공간.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>)(U+FF09)</td>
   <td>숫자가 음수인 경우 오른쪽 괄호. 다른 공간.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>t</td>
   <td>탭 문자</td>
   <td><br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

## 텍스트 그림 절 {#text-picture-clause}

HTML5 양식은 다음 텍스트 그림 절 표현식을 지원합니다.

* text{text} 그림 절 기호}

| **기호** | **해석** |
|---|---|
| A | 단일 알파벳 문자입니다. |
| X | 단일 문자. |
| O | 단일 영숫자 문자입니다. |
| 0(영) | 단일 영숫자 문자입니다. |
| 9 | 한 자리. |
