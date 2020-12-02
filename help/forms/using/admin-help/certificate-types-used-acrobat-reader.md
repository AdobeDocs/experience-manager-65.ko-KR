---
title: Acrobat Reader DC 익스텐션에서 사용하는 인증서 유형
seo-title: Acrobat Reader DC 익스텐션에서 사용하는 인증서 유형
description: Acrobat Reader DC 익스텐션에서 사용하는 인증서 유형에 대해 알아봅니다.
seo-description: Acrobat Reader DC 익스텐션에서 사용하는 인증서 유형에 대해 알아봅니다.
uuid: 93c02abc-2d5a-44ed-b93c-981afbd0553d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 331b9317-87b5-4a96-a1bc-429675ff90c5
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '955'
ht-degree: 3%

---


# Acrobat Reader DC 익스텐션 {#certificate-types-used-by-acrobat-reader-dc-extensions}에서 사용하는 인증서 유형

인증서 뷰어는 인증서에 대한 다음 정보를 제공합니다.

* 인증서 &quot;친숙한&quot; 이름
* 인증서 프로필
* 유효 기간
* Acrobat Reader DC 확장 사용 권한

## 인증서 &quot;친숙한&quot; 이름 {#certificate-friendly-name}

다음 예제와 같이 Acrobat Reader DC 확장 인증서의 &quot;친숙한&quot; 이름은 인증서의 속성을 설명하는 문자열입니다.

2D 바코드 풀 프로덕션 V6.1 P8 0002054

문자열에는 다음 요소가 포함됩니다.

**인증서 유형:** 인증서가 활성화되는 AEM 양식 모듈과 활성화 수준(예: ARE 2D 바코드 풀)을 설명합니다. 사용 가능한 인증서 유형 목록은 인증서 프로필 섹션에 있는 테이블의 유형 열을 참조하십시오.

**배포 유형:** 프로덕션과 같은 인증서의 의도된 사용을 나타냅니다. 값은 평가 또는 제작일 수 있습니다. 각 인증서 유형과 연관된 배포 유형 목록은 인증서 프로파일 섹션의 표의 배포 유형 열을 참조하십시오.

**사용 권한 버전:** V6.1과 같이 인증서를 사용할 수 있는 사용 권한 알고리즘 버전을 설명합니다. 이 버전은 Acrobat 또는 Acrobat Reader DC 확장 버전을 의미하지 않습니다.

**프로필 코드:** 프로필 코드는 전체 인증서 속성의 약칭입니다(예: P8). 각 파일 형식과 연관된 프로필 코드 목록은 인증서 프로필 섹션의 표의 프로필 코드 열을 참조하십시오.

**일련 번호:** 일련 번호는 002054와 같이 Adobe이 발행한 각 인증서에 할당됩니다. Adobe 엔터프라이즈 지원 또는 Adobe 엔터프라이즈 계정 담당자는 이 시리얼 번호를 사용하여 특정 제품 주문 또는 OEM 관계로 인증서를 추적할 수 있습니다.

## 인증서 프로필 {#certificate-profiles}

다음 표에는 Acrobat Reader DC 확장 인증서를 분석할 때 발생할 수 있는 인증서 프로필이 나와 있습니다.

<table>
 <thead>
  <tr>
   <th><p>프로필 코드</p></th>
   <th><p>유형</p></th>
   <th><p>유효 기간</p></th>
   <th><p>배포 유형</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>P1</p></td>
   <td><p>SAP Production</p></td>
   <td><p>최대</p></td>
   <td><p>프로덕션</p></td>
  </tr>
  <tr>
   <td><p>P2</p></td>
   <td><p>SAP 내부 테스트</p></td>
   <td><p>2년</p></td>
   <td><p>평가 및 테스트</p></td>
  </tr>
  <tr>
   <td><p>P3</p></td>
   <td><p>Acrobat Reader DC 익스텐션, 프로덕션</p></td>
   <td><p>최대</p></td>
   <td><p>프로덕션</p></td>
  </tr>
  <tr>
   <td><p>P4</p></td>
   <td><p>Acrobat Reader DC 확장, 내부 Adobe 사용</p></td>
   <td><p>2년</p></td>
   <td><p>프로덕션</p></td>
  </tr>
  <tr>
   <td><p>P5</p></td>
   <td><p>Acrobat Reader DC 확장, 파트너 통합</p></td>
   <td><p>2년</p></td>
   <td><p>평가 및 테스트</p></td>
  </tr>
  <tr>
   <td><p>P6</p></td>
   <td><p>Acrobat Reader DC 확장, 평가</p></td>
   <td><p>60일</p></td>
   <td><p>평가</p></td>
  </tr>
  <tr>
   <td><p>P8</p></td>
   <td><p>Forms, 프로덕션</p></td>
   <td><p>최대</p></td>
   <td><p>프로덕션</p></td>
  </tr>
  <tr>
   <td><p>P9</p></td>
   <td><p>Adobe Acrobat 7.x, 프로덕션</p></td>
   <td><p>최대</p></td>
   <td><p>프로덕션</p></td>
  </tr>
  <tr>
   <td><p>I10</p></td>
   <td><p>Forms;은 OEM에서 사용할 수 있습니다.</p></td>
   <td><p>최대</p></td>
   <td><p>제작 및 평가</p></td>
  </tr>
  <tr>
   <td><p>I11</p></td>
   <td><p>Forms;은 OEM에서 사용할 수 있습니다.</p></td>
   <td><p>최대</p></td>
   <td><p>제작 및 평가</p></td>
  </tr>
  <tr>
   <td><p>I12</p></td>
   <td><p>서명 전용;은 OEM에서 사용할 수 있습니다.</p></td>
   <td><p>최대</p></td>
   <td><p>제작 및 평가</p></td>
  </tr>
  <tr>
   <td><p>I13</p></td>
   <td><p>오프라인 주석 달기 전용;은 OEM에서 사용할 수 있습니다.</p></td>
   <td><p>최대</p></td>
   <td><p>제작 및 평가</p></td>
  </tr>
  <tr>
   <td><p>I14</p></td>
   <td><p>주석 달기 전용;은 OEM에서 사용할 수 있습니다.</p></td>
   <td><p>최대</p></td>
   <td><p>제작 및 평가</p></td>
  </tr>
  <tr>
   <td><p>I15</p></td>
   <td><p>전체 권한;은 OEM에서 사용할 수 있습니다.</p></td>
   <td><p>최대</p></td>
   <td><p>제작 및 평가</p></td>
  </tr>
 </tbody>
</table>

## 유효 기간 {#validity-period}

제품 샘플 애플리케이션을 평가 및 개발할 수 있도록 고객 및 개발자에게 평가 인증서가 발급됩니다. 이 인증서의 유효 기간은 60일에서 90일 사이입니다. 문제 자료 다음의 두 번째 달 말에 만료됩니다.

소프트웨어 개발, 통합, 프로토타이핑 및 데모를 지원하기 위해 파트너 통합 인증서가 Adobe 비즈니스 파트너에게 발급됩니다. 이 인증서는 발행 후 2년 동안 유효합니다.

Adobe 내부 사용 인증서는 Adobe 내에서 소프트웨어 개발, 통합, 프로토타이핑 및 데모를 지원하는 데 사용됩니다. 이 인증서는 발행 후 2년 동안 유효합니다.

프로덕션 인증서는 Acrobat Reader DC 익스텐션을 구입한 고객에게 발급됩니다. 이러한 인증서는 인증서 프로필 테이블에 *Max*&#x200B;로 표시된 인증 기관(CA)에서 허용하는 최대 기간 동안 유효합니다.

## Acrobat Reader DC 확장 사용 권한 {#acrobat-reader-dc-extensions-usage-rights}

인증서 뷰어에서 Acrobat Reader DC 확장 인증서를 검사할 때 세부 사항 탭(구성된 경우)에서 사용 권한 항목을 선택하여 인증서가 활성화할 수 있는 Adobe Reader 사용 권한의 항목별 목록을 볼 수 있습니다. 특정 문서에서 활성화된 사용 권한은 인증서에 의해 활성화된 사용 권한 중 일부일 수 있습니다.

공동 작업 환경이 아닌 환경에서 온라인 주석 달기가 필요한 경우 Adobe 지원에 문의하여 자세한 내용을 확인하십시오. Mode 속성은 배포 유형과 일치하며 *production* 또는 *evaluation*&#x200B;입니다.

허용되는 Acrobat Reader DC 확장 사용 권한은 하나 이상의 특정 요소로 구성됩니다. 이러한 요소는 다양한 조합으로 사용되어 다양한 라이센스 제품 기능을 얻을 수 있습니다.

<table>
 <thead>
  <tr>
   <th><p>사용 권한 요소</p></th>
   <th><p>권한이 활성화된 PDF 문서를 볼 때 Adobe Reader에서 사용 가능</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>FormFillInAndSave</p></td>
   <td><p>양식 필드를 입력하고 로컬에 파일을 저장합니다.</p></td>
  </tr>
  <tr>
   <td><p>FormImportExport</p></td>
   <td><p>양식 데이터를 FDF, XFDF, XML 및 XDP 파일로 가져오거나 내보낼 수 있습니다.</p></td>
  </tr>
  <tr>
   <td><p>FormAddDelete</p></td>
   <td><p>PDF 양식에 필드 및 필드 속성을 추가, 변경 또는 삭제할 수 있습니다.</p></td>
  </tr>
  <tr>
   <td><p>SubmitStandalone</p></td>
   <td><p>브라우저 세션에서 실행되고 있지 않은 데이터를 이메일 또는 오프라인으로 서버에 제출합니다.</p></td>
  </tr>
  <tr>
   <td><p>SpailTemplate</p></td>
   <td><p>동일한 PDF 양식의 템플릿 페이지에서 페이지를 만들 수 있습니다.</p></td>
  </tr>
  <tr>
   <td><p>서명</p></td>
   <td><p>PDF 문서에 디지털 서명 및 저장, 디지털 서명 지우기</p></td>
  </tr>
  <tr>
   <td><p>AnnotModify</p></td>
   <td><p>주석과 같은 문서 주석을 만들고 수정할 수 있습니다.</p></td>
  </tr>
  <tr>
   <td><p>AnnotImportExport</p></td>
   <td><p>주석과 같은 주석을 별도의 데이터 파일에 저장하고 파일에서 주석을 로드할 수 있습니다.</p></td>
  </tr>
  <tr>
   <td><p>BarcodePlaintext</p></td>
   <td><p>코드 작성을 위해 라이센스 서버 소프트웨어가 필요 없는 암호화되지 않은 형태로 바코드 된 양식을 인쇄할 수 있습니다.</p></td>
  </tr>
  <tr>
   <td><p>AnnotOnline</p></td>
   <td><p>온라인 문서 검토 및 주석 서버에서 주석을 업로드하고 다운로드할 수 있습니다.</p></td>
  </tr>
  <tr>
   <td><p>FormOnline</p></td>
   <td><p>PDF 양식에 정의된 웹 서비스 또는 데이터베이스에 연결할 수 있습니다.</p></td>
  </tr>
  <tr>
   <td><p>EFModif</p></td>
   <td><p>PDF 문서와 연관된 포함된 파일 객체를 수정합니다.</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Acrobat Reader DC 확장 사용 권한은 함께 작동하는 특정 조합에서만 Adobe에서 라이선스를 부여할 수 있습니다. 이러한 기능을 개별적으로 라이센스할 수는 없습니다. 사용 권한 조합에 대한 자세한 내용은 AEM 양식 계정 담당자에게 문의하십시오.

