---
title: Acrobat Reader DC 확장 프로그램에서 사용하는 인증서 유형
description: Acrobat Reader DC 확장 프로그램에서 사용하는 인증서 유형을 알아봅니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 800bffd5-0cdc-4251-bba4-e350f226f019
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: ht
source-wordcount: '944'
ht-degree: 100%

---

# Acrobat Reader DC 확장 프로그램에서 사용하는 인증서 유형 {#certificate-types-used-by-acrobat-reader-dc-extensions}

인증서 뷰어에서는 인증서에 대한 다음과 같은 정보를 제공합니다.

* 인증서의 &#39;친숙한&#39; 이름
* 인증서 프로필
* 유효 기간
* Acrobat Reader DC 확장 프로그램 사용 권한

## 인증서의 &#39;친숙한&#39; 이름 {#certificate-friendly-name}

Acrobat Reader DC 확장 프로그램 인증서의 &#39;친숙한&#39; 이름은 다음 예와 같이 인증서의 속성을 설명하는 문자열입니다.

ARE 2D 바코드 전체 프로덕션 V6.1 P8 0002054

이 문자열에는 다음 요소가 포함되어 있습니다.

**인증서 유형:** 인증서에서 활성화하는 AEM Forms 모듈과 ARE 2D 바코드 전체와 같은 활성화 수준을 설명합니다. 사용 가능한 인증서 유형 목록은 인증서 프로필 섹션의 표에서 유형 열을 참조하십시오.

**배포 유형:** 프로덕션과 같이 인증서의 용도를 나타냅니다. 이 값은 평가 또는 프로덕션일 수 있습니다. 각 인증서 유형과 연결된 배포 유형 목록은 인증서 프로필 섹션의 표에서 배포 유형 열을 참조하십시오.

**사용 권한 버전:** V6.1과 같이 인증서를 사용할 수 있는 사용 권한 알고리즘의 버전을 설명합니다. 이 버전은 Acrobat 또는 Acrobat Reader DC 확장 프로그램의 버전을 나타내는 것이 아닙니다.

**프로필 코드:** 프로필 코드는 P8과 같이 전체 인증서 속성을 간단히 설명합니다. 각 파일 유형과 연결된 프로필 코드 목록은 인증서 프로필 섹션의 표에서 프로필 코드 열을 참조하십시오.

**일련번호:** Adobe에서 발급한 각 인증서에는 0002054와 같은 일련번호가 할당됩니다. Adobe Enterprise Support 또는 Adobe Enterprise 계정 담당자는 이 일련번호를 사용하여 해당 인증서를 특정 제품 주문이나 OEM 관계로 추적할 수 있습니다.

## 인증서 프로필 {#certificate-profiles}

다음 표에는 Acrobat Reader DC 확장 프로그램 인증서를 분석할 때 접할 수 있는 인증서 프로필이 나열되어 있습니다.

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
   <td><p>SAP 프로덕션</p></td>
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
   <td><p>Acrobat Reader DC 확장 프로그램, 프로덕션</p></td>
   <td><p>최대</p></td>
   <td><p>프로덕션</p></td>
  </tr>
  <tr>
   <td><p>P4</p></td>
   <td><p>Acrobat Reader DC 확장 프로그램, Adobe 내부 사용</p></td>
   <td><p>2년</p></td>
   <td><p>프로덕션</p></td>
  </tr>
  <tr>
   <td><p>P5</p></td>
   <td><p>Acrobat Reader DC 확장 프로그램, 파트너 통합</p></td>
   <td><p>2년</p></td>
   <td><p>평가 및 테스트</p></td>
  </tr>
  <tr>
   <td><p>P6</p></td>
   <td><p>Acrobat Reader DC 확장 프로그램, 평가</p></td>
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
   <td><p>Forms, OEM에서 사용할 수 있음</p></td>
   <td><p>최대</p></td>
   <td><p>프로덕션 및 평가</p></td>
  </tr>
  <tr>
   <td><p>I11</p></td>
   <td><p>Forms, OEM에서 사용할 수 있음</p></td>
   <td><p>최대</p></td>
   <td><p>프로덕션 및 평가</p></td>
  </tr>
  <tr>
   <td><p>I12</p></td>
   <td><p>서명만 가능, OEM에서 사용할 수 있음</p></td>
   <td><p>최대</p></td>
   <td><p>프로덕션 및 평가</p></td>
  </tr>
  <tr>
   <td><p>I13</p></td>
   <td><p>오프라인 주석 달기만 가능, OEM에서 사용할 수 있음</p></td>
   <td><p>최대</p></td>
   <td><p>프로덕션 및 평가</p></td>
  </tr>
  <tr>
   <td><p>I14</p></td>
   <td><p>주석 달기만 가능, OEM에서 사용할 수 있음</p></td>
   <td><p>최대</p></td>
   <td><p>프로덕션 및 평가</p></td>
  </tr>
  <tr>
   <td><p>I15</p></td>
   <td><p>전체 권한, OEM에서 사용할 수 있음</p></td>
   <td><p>최대</p></td>
   <td><p>프로덕션 및 평가</p></td>
  </tr>
 </tbody>
</table>

## 유효 기간 {#validity-period}

평가판 인증서는 고객과 개발자에게 발급되며 제품에 대한 샘플 애플리케이션을 평가하고 개발할 수 있도록 합니다. 해당 인증서의 유효 기간은 60일에서 90일까지입니다. 발급 일자를 기준으로 두 번째 달 말에 만료됩니다.

파트너 통합 인증서는 소프트웨어 개발, 통합, 프로토타이핑, 데모를 지원하기 위해 Adobe 비즈니스 파트너에게 발급됩니다. 해당 인증서는 발급 일자를 기준으로 2년간 유효합니다.

Adobe 내부 사용 인증서는 Adobe 내부에서 소프트웨어 개발, 통합, 프로토타이핑, 데모를 지원하는 데 사용됩니다. 해당 인증서는 발급 일자를 기준으로 2년간 유효합니다.

프로덕션 인증서는 Acrobat Reader DC 확장 프로그램을 구매한 고객에게 발급됩니다. 해당 인증서는 인증 기관(CA)에서 허용한 최대 기간 동안 유효하며 인증서 프로필 표에 *최대*&#x200B;로 표시됩니다.

## Acrobat Reader DC 확장 프로그램 사용 권한 {#acrobat-reader-dc-extensions-usage-rights}

인증서 뷰어에서 Acrobat Reader DC 확장 프로그램 인증서를 살펴볼 때 세부 정보 탭(구성된 경우)에서 사용 권한 항목을 선택하면 인증서에서 활성화할 수 있는 Adobe Reader 사용 권한의 항목별 목록을 볼 수 있습니다. 특정 문서에 대해 활성화된 사용 권한은 인증서에서 활성화된 사용 권한의 하위 집합일 수 있습니다.

공동 작업 환경이 아닌 곳에서 온라인 주석 달기가 필요한 경우 자세한 내용은 Adobe 지원 팀에 문의하십시오. Mode 속성은 배포 유형과 일치하며 *프로덕션* 또는 *평가*&#x200B;입니다.

허용된 Acrobat Reader DC 확장 프로그램 사용 권한은 하나 이상의 특정 요소로 구성됩니다. 해당 요소는 다양한 조합으로 사용되어 사용 허가된 다양한 제품 기능을 구현합니다.

<table>
 <thead>
  <tr>
   <th><p>사용 권한 요소</p></th>
   <th><p>권한이 활성화된 PDF 문서를 볼 때 Adobe Reader에서 활성화되는 기능</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>FormFillInAndSave</p></td>
   <td><p>양식 필드를 입력하고 파일을 로컬에 저장합니다.</p></td>
  </tr>
  <tr>
   <td><p>FormImportExport</p></td>
   <td><p>FDF, XFDF, XML 및 XDP 파일로 양식 데이터를 가져오고 내보냅니다.</p></td>
  </tr>
  <tr>
   <td><p>FormAddDelete</p></td>
   <td><p>PDF 양식에서 필드와 필드 속성을 추가, 변경 또는 삭제합니다.</p></td>
  </tr>
  <tr>
   <td><p>SubmitStandalone</p></td>
   <td><p>브라우저 세션에서 실행 중이 아닐 때 이메일이나 오프라인으로 서버에 데이터를 제출합니다.</p></td>
  </tr>
  <tr>
   <td><p>SpawnTemplate</p></td>
   <td><p>동일한 PDF 양식 내의 템플릿 페이지에서 페이지를 만듭니다.</p></td>
  </tr>
  <tr>
   <td><p>Signing</p></td>
   <td><p>PDF 문서를 디지털 서명하고 저장하며 디지털 서명을 지웁니다.</p></td>
  </tr>
  <tr>
   <td><p>AnnotModify</p></td>
   <td><p>댓글과 같은 문서 주석을 만들고 수정합니다.</p></td>
  </tr>
  <tr>
   <td><p>AnnotImportExport</p></td>
   <td><p>댓글과 같은 주석을 별도의 데이터 파일에 저장하고 파일에서 댓글을 로드합니다.</p></td>
  </tr>
  <tr>
   <td><p>BarcodePlaintext</p></td>
   <td><p>사용 허가된 서버 소프트웨어 없이도 디코딩할 수 있는 암호화되지 않은 양식에 바코드가 있는 양식 데이터가 포함된 문서를 인쇄합니다.</p></td>
  </tr>
  <tr>
   <td><p>AnnotOnline</p></td>
   <td><p>온라인 문서 검토 및 댓글 서버에서 댓글과 같은 주석을 업로드하고 다운로드합니다.</p></td>
  </tr>
  <tr>
   <td><p>FormOnline</p></td>
   <td><p>PDF 양식 내에 정의된 웹 서비스나 데이터베이스에 연결합니다.</p></td>
  </tr>
  <tr>
   <td><p>EFModif</p></td>
   <td><p>PDF 문서와 연결되고 임베드된 파일 오브젝트를 수정합니다.</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Acrobat Reader DC 확장 프로그램 사용 권한은 함께 작동하는 특정 조합으로만 Adobe에서 라이선스를 부여받을 수 있습니다. 이러한 기능에 대한 라이선스를 독립적으로 부여하는 것은 불가능합니다. 사용 가능한 사용 권한 조합에 대한 자세한 내용은 AEM Forms 계정 담당자에게 문의하십시오.
