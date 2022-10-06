---
title: 서신 관리 구성 속성
seo-title: Correspondence Management Configuration Properties
description: 이 항목에서는 솔루션별 구성으로 자산 작성기를 수정하는 방법을 설명합니다. 이 항목에서는 편집할 수 있는 속성에 대해 설명, 기본값 및 허용 가능한 값을 제공합니다.
seo-description: This topic explains how you can modify Asset Composer with solution-specific configurations. This topic details the properties you can edit, with their description, default values, and acceptable values.
uuid: 6b401d51-9332-459b-b751-42a9b5a1462d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: f2955419-c680-44a7-9913-c594b4577551
feature: Correspondence Management
exl-id: c9c007d0-c545-4738-b11b-4c50986342ee
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '845'
ht-degree: 3%

---

# 서신 관리 구성 속성 {#correspondence-management-configuration-properties}

이러한 속성을 구성하려면 브라우저에서 다음 URL을 엽니다. `https://<server>:<port>/<contextPath>/system/console/configMgr` 을(를) 선택합니다. **서신 관리 구성**.

서신 관리에는 다음 구성 속성이 있습니다.

<table>
 <tbody>
  <tr>
   <th><p><strong>속성</strong></p> </th>
   <th><p><strong>설명</strong></p> </th>
   <th><p><strong>기본값</strong></p> </th>
   <th><p><strong>허용되는 값</strong></p> </th>
  </tr>
  <tr>
   <td><p>들여쓰기</p> </td>
   <td>모듈에 대한 들여쓰기<p> </p> </td>
   <td><p>12.7밀리미터</p> </td>
   <td><p>임의 번호</p> </td>
  </tr>
  <tr>
   <td>최소 너비 수</td>
   <td>로마자 숫자와 별도로 번호 목록을 사용할 때 글머리 기호/번호 필드에 적용할 최소 너비</td>
   <td>8.0밀리미터</td>
   <td>임의 번호</td>
  </tr>
  <tr>
   <td><p>최소 너비 로마자 숫자</p> </td>
   <td><p>로마자 숫자를 사용할 때 글머리 기호/번호 필드에 적용할 최소 너비</p> </td>
   <td><p>12.7밀리미터</p> </td>
   <td><p>임의 번호</p> </td>
  </tr>
  <tr>
   <td>표현물 유형</td>
   <td>편지 미리 보기를 렌더링하는 데 Create Correspondence 애플리케이션에서 사용하는 표현물의 유형입니다. </td>
   <td>HTML 표현물</td>
   <td>HTML 표현물/PDF 표현물</td>
  </tr>
  <tr>
   <td><p>CCR PDF 강조 표시 활성화</p> </td>
   <td><p>서신 응용 프로그램 만들기에서 PDF에 대해 강조 표시를 활성화합니다</p> </td>
   <td><p>true</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Target 강조 표시 유형</p> </td>
   <td><p>서신 작성 응용 프로그램의 Target 강조 표시 유형</p> </td>
   <td><p>테두리</p> </td>
   <td><p>테두리/채우기/없음</p> </td>
  </tr>
  <tr>
   <td><p>Target 강조 색상</p> </td>
   <td><p>서신 작성 응용 프로그램에서 Target 강조 색상</p> </td>
   <td><p>90;155;245</p> </td>
   <td><p>R;G;B 형식의 모든 RGB 색상</p> </td>
  </tr>
  <tr>
   <td><p>컨텐츠 강조 표시 유형</p> </td>
   <td><p>서신 만들기 애플리케이션의 컨텐츠 강조 유형</p> </td>
   <td><p>채우기</p> </td>
   <td><p>테두리/채우기/없음</p> </td>
  </tr>
  <tr>
   <td><p>컨텐츠 강조 표시 색상</p> </td>
   <td><p>서신 작성 애플리케이션에서 컨텐츠 강조 색상</p> </td>
   <td><p>210;225;245</p> </td>
   <td><p>R;G;B 형식의 모든 RGB 색상</p> </td>
  </tr>
  <tr>
   <td><p>필드 강조 표시 유형</p> </td>
   <td><p>Create Correspondence 응용 프로그램의 필드 강조 표시 유형</p> </td>
   <td><p>채우기</p> </td>
   <td><p>테두리/채우기/없음</p> </td>
  </tr>
  <tr>
   <td><p>필드 강조 색상</p> </td>
   <td><p>Create Correspondence 응용 프로그램에서 필드 강조 색상</p> </td>
   <td><p>210;225;245</p> </td>
   <td><p>R;G;B 형식의 모든 RGB 색상</p> </td>
  </tr>
  <tr>
   <td><p>애플리케이션 시간 초과</p> </td>
   <td><p>애플리케이션 시간 초과(초)</p> </td>
   <td><p>1200</p> </td>
   <td><p>임의 번호</p> </td>
  </tr>
  <tr>
   <td><p>PDF 문서 매개 변수 이름</p> </td>
   <td><p>사후 프로세스의 PDF 문서에 대한 매개 변수 이름</p> </td>
   <td><p>inPDFDoc</p> </td>
   <td><p>모든 문자열 변수 이름</p> </td>
  </tr>
  <tr>
   <td><p>XML 데이터 매개 변수 이름</p> </td>
   <td><p>사후 프로세스의 XML 문서(데이터)에 대한 매개 변수 이름</p> </td>
   <td><p>inXMLDoc</p> </td>
   <td><p>모든 문자열 변수 이름</p> </td>
  </tr>
  <tr>
   <td><p>XDP 문서 매개 변수 이름</p> </td>
   <td><p>이후 프로세스에 전송된 XDP 문서의 매개 변수 이름</p> </td>
   <td><p>inXDPDoc</p> </td>
   <td><p>모든 문자열 변수 이름</p> </td>
  </tr>
  <tr>
   <td><p>리디렉션 URL 매개 변수 이름</p> </td>
   <td><p>post 프로세스에서 전송된 리디렉션 URL의 매개 변수 이름 이 값은 모든 문자열 변수 이름일 수 있습니다</p> </td>
   <td><p>redirectURL</p> </td>
   <td><p>모든 문자열 변수 이름</p> </td>
  </tr>
  <tr>
   <td><p>PDF 제출 유형</p> </td>
   <td><p>PDF 제출 유형(서신 애플리케이션 생성에서 제출 시 생성된 PDF 유형)</p> </td>
   <td><p>nonInteractive</p> </td>
   <td><p>대화형/비대화형</p> </td>
  </tr>
  <tr>
   <td><p>데이터 사전 인스턴스 최적화</p> </td>
   <td><p>서버 및 클라이언트별로 데이터 사전 인스턴스 전송을 최적화합니다.</p> </td>
   <td><p>true</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>자동 수정 불일치 </p> </td>
   <td><p>이 옵션을 활성화하면 편지 할당에서 가능한 불일치를 자동으로 처리합니다</p> </td>
   <td><p>true</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>구성된 데이터 형식 사용</p> </td>
   <td><p>구성된 데이터 편집 형식 및 데이터 표시 형식 사용 여부를 제어합니다</p> </td>
   <td><p>true</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>데이터 표시 형식</p> </td>
   <td><p>데이터의 로케일 특정 표시 형식을 지정합니다</p> </td>
   <td><p>locale=en_US; dateFormat=dd-MM-yyyy; numberDecimalSeparator=.; numberGroupSeparator=,; numberUseGroupSeparator=truelocale=de_DE; dateFormat=dd-MM-yyyy; numberDecimalSeparator=,; numberGroupSeparator=.; numberUseGroupSeparator=truelocale=fr_FR; dateFormat=dd-MM-yyyy; numberDecimalSeparator=,; numberGroupSeparator= ; numberUseGroupSeparator=truelocale=ja_JP; dateFormat=dd-MM-yyyy; numberDecimalSeparator=.; numberGroupSeparator=,; numberUseGroupSeparator=true</p> </td>
   <td><p>—</p> </td>
  </tr>
  <tr>
   <td><p>데이터 편집 형식</p> </td>
   <td><p>데이터의 형식을 편집합니다. 데이터를 문자열로 작성하거나 문자열에서 데이터를 구문 분석할 때 사용됩니다</p> </td>
   <td><p>locale=en_US; dateFormat=dd-MM-yyyy; numberDecimalSeparator=.; numberGroupSeparator=,; numberUseGroupSeparator=true</p> </td>
   <td>—<p> </p> </td>
  </tr>
  <tr>
   <td><p>게시할 때 편지 인스턴스 관리</p> </td>
   <td><p>편지 관리 기능 활성화/비활성화(게시 서버에만 해당)</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>감사 활성화</p> </td>
   <td><p>감사 기능을 활성화/비활성화합니다. false이면 모든 작업에 대한 감사 로그가 비활성화됩니다</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>읽기 감사 활성화</p> </td>
   <td><p>자산 읽기에 대한 감사 기능 활성화/비활성화</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>감사 만들기 활성화</p> </td>
   <td><p>자산 만들기에 대한 감사 기능 활성화/비활성화</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>업데이트 감사 활성화</p> </td>
   <td><p>자산 업데이트에 대한 감사 기능 활성화/비활성화</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>감사 되돌리기 활성화</p> </td>
   <td><p>자산 되돌림에 대한 감사 기능 활성화/비활성화</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>게시 감사 활성화</p> </td>
   <td><p>자산 게시에 대한 감사 기능 활성화/비활성화</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>SaveAsDraft 감사 활성화</p> </td>
   <td><p>편지 초안 저장을 위한 감사 기능 활성화/비활성화</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>제출 감사 활성화</p> </td>
   <td><p>편지 제출에 대한 감사 기능 활성화/비활성화</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>이메일 감사 활성화</p> </td>
   <td><p>전자 메일로 보내는 감사 기능 활성화/비활성화</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>인쇄 감사 활성화</p> </td>
   <td><p>편지 인쇄에 대한 감사 기능 활성화/비활성화</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>사용자 지정 게재 감사 활성화</p> </td>
   <td><p>사용자 지정 편지 배달에 대한 감사 기능 활성화/비활성화</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>첨부 문서 매개변수 이름</p> </td>
   <td><p>이후 프로세스에 전송된 첨부 문서의 매개변수 이름</p> </td>
   <td><p>inAttachmentDocs</p> </td>
   <td><p>모든 문자열 변수 이름</p> </td>
  </tr>
  <tr>
   <td><p>CM 사용자 루트</p> </td>
   <td><p>모든 서신 관리 사용자 자산이 포함된 폴더의 URL</p> </td>
   <td><p>—</p> </td>
   <td><p>유효한 폴더 위치</p> </td>
  </tr>
  <tr>
   <td><p>편지 캐시 크기</p> </td>
   <td><p>캐시에 유지할 최대 글자 수를 지정합니다.</p> <p>이 값을 변경하면 정리 작업이 수행됩니다 <code>in-memory</code> 캐시.</p> </td>
   <td><p>100</p> </td>
   <td><p>모든 숫자 값</p> </td>
  </tr>
  <tr>
   <td><p>편지 캐시 사용</p> </td>
   <td><p>편지 캐시를 활성화/비활성화합니다.</p> <p>이 값을 변경하면 정리 작업이 수행됩니다 <code>in-memory </code> 캐시.</p> </td>
   <td><p>true</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>데이터 요소 순서 지정</p> </td>
   <td><p>Letter의 시퀀스에 따라 서신 인터페이스를 만드는 데 데이터 요소 순서를 유지합니다</p> </td>
   <td><p>true</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>다시 로드 지원</p> </td>
   <td><p>서버 측에 렌더링된 편지에서 재로드 지원을 활성화/비활성화합니다.</p> <p>이를 비활성화하면 편지 렌더링 성능이 향상됩니다.</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> <p> </p> </td>
  </tr>
  <tr>
   <td>임시 폴더</td>
   <td>임시 폴더의 위치입니다.</td>
   <td>acm.tpmFolder</td>
   <td> </td>
  </tr>
  <tr>
   <td>원격 저장</td>
   <td>지정된 처리 작성자에 편지 인스턴스 를 저장합니다.</td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>호환성 옵션</td>
   <td>configname:configvalue 형식의 호환성 옵션이 쉼표로 구분되어 있습니다.</td>
   <td>acm.compatibilityOptions</td>
   <td> </td>
  </tr>
  <tr>
   <td><p>디버그 디렉토리 </p> <p> </p> </td>
   <td>디버깅을 위한 파일 시스템 폴더 위치입니다. 디렉토리가 없는 경우 <code>exists</code>로 설정되면 디버그 덤프가 생성되지 않습니다.</td>
   <td>acm.debugDirectory</td>
   <td> </td>
  </tr>
 </tbody>
</table>
