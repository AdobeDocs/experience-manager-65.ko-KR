---
title: 터치 UI 기능 상태
description: Adobe Experience Manager Touch-Enabled UI와 관련된 릴리스 노트입니다.
uuid: ceb081cc-7c33-4408-8032-3ac83d461268
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: f736581d-e6ea-4ec8-bfc7-16b9aa592097
docset: aem65
translation-type: tm+mt
source-git-commit: 57bad4e74b2dfd9e389643bfe58ef25564c5c545

---


# 터치 UI 기능 상태{#touch-ui-feature-status}

>[!CAUTION]
>
>[클래식 UI는 AEM 6.4 이후 더 이상 사용되지 않습니다](../release-notes/deprecated-removed-features.md) .Adobe는 클래식 UI를 추가로 개선할 계획이 없으며 사용자는 터치 지원 UI에서 사용할 수 있는 강력한 새로운 기능을 활용할 수 있습니다.

버전 6.0부터 AEM은 Adobe Marketing Cloud 및 전체 Adobe 사용자 인터페이스 가이드라인에 맞춰 제공되는 &quot;터치 지원 UI&quot;(간단히 &quot;터치 UI&quot;라고도 함)라는 새로운 사용자 인터페이스를 도입했습니다. 거의 비슷한 기능 패리티가 도달하여, 이것은 &quot;클래식 UI&quot;라고 하는 레거시 데스크톱 기반 인터페이스를 사용하는 AEM의 표준 UI가 되었습니다.

대부분의 기능이 터치 지원 UI에 있지만 아직 완전하지 않은 기능이 있으며 향후 릴리스에 추가될 예정입니다.

다음 목록은 AEM 6.5에서 구현된 기능의 현재 상태를 보여줍니다.

AEM 6.5로 업그레이드하는 고객을 위한 권장 사항은 [고객을 위한 사용자 인터페이스 권장 사항을](/help/sites-deploying/ui-recommendations.md) 참조하십시오.

>[!NOTE]
>
>이 페이지에서는 클래식 UI와 동일한 기능 패리티만 다룹니다.
>
>클래식 UI에 없는 터치 지원 UI에 추가되거나 고유한 기능은 나열되지 않습니다.

>[!NOTE]
>
>이 목록은 완성에 중점을 두지만 완전한 것으로 간주해서는 안 됩니다.

## 범례 {#legend}

* **완료**:이 기능은 터치 지원 UI에서 사용할 수 있습니다.
* **대부분**:이 기능은 대부분 터치 지원 UI에서 사용할 수 있습니다.
* **누락**:터치 지원 UI에 이 기능이 없으므로 클래식 UI를 사용하여 이 작업을 수행해야 합니다.
* **교체**:이 기능은 다르게 작동하는 새로운 구현으로 대체되었습니다.
* **제거됨**:이 기능은 터치 지원 UI에 더 이상 존재하지 않으며 교체되지 않습니다.

## 기능 상태:사이트 관리 {#feature-status-sites-admin}

클래식 UI 사이트 관리자()의 기능 목록과 터치 지원 UI( `/siteadmin``/sites.html`)의 상태입니다.

<table>
 <tbody>
  <tr>
   <td><strong>기능<br /> </strong></td>
   <td><strong>상태<br /> </strong></td>
   <td><strong>주석</strong></td>
  </tr>
  <tr>
   <td>사이트 계층 탐색</td>
   <td>완료<br /> </td>
   <td>AEM 6.4에서는 <a href="/help/sites-authoring/basic-handling.md#content-tree">콘텐츠 트리 보기를</a>도입했습니다.</td>
  </tr>
  <tr>
   <td>워크플로우 시작</td>
   <td>완료<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>새 페이지 만들기</td>
   <td>완료</td>
   <td> </td>
  </tr>
  <tr>
   <td>새 사이트 만들기</td>
   <td>완료</td>
   <td> </td>
  </tr>
  <tr>
   <td>새 론치 만들기</td>
   <td>완료</td>
   <td> </td>
  </tr>
  <tr>
   <td>새 Live Copy 만들기 <br /> </td>
   <td>완료<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>폴더 만들기</td>
   <td>완료</td>
   <td> </td>
  </tr>
  <tr>
   <td>게시 상태 표시</td>
   <td>완료</td>
   <td>AEM 6.5를 시작하면 워크플로우 상태가 목록 보기에 표시됩니다.</td>
  </tr>
  <tr>
   <td>검색</td>
   <td>완료<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>페이지 복사/붙여넣기(복제)</td>
   <td>완료</td>
   <td> </td>
  </tr>
  <tr>
   <td>페이지 이동</td>
   <td>완료</td>
   <td> </td>
  </tr>
  <tr>
   <td>페이지 게시</td>
   <td>완료</td>
   <td> </td>
  </tr>
  <tr>
   <td>복제 권한 없이 페이지 게시</td>
   <td>완료</td>
   <td> </td>
  </tr>
  <tr>
   <td>나중에 게시</td>
   <td>완료</td>
   <td> </td>
  </tr>
  <tr>
   <td>트리 게시</td>
   <td>완료</td>
   <td> </td>
  </tr>
  <tr>
   <td>페이지 게시 취소</td>
   <td>완료</td>
   <td> </td>
  </tr>
  <tr>
   <td>복제 권한 없이 페이지 게시 취소</td>
   <td>완료</td>
   <td> </td>
  </tr>
  <tr>
   <td>나중에 게시 취소</td>
   <td>완료<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>삭제</td>
   <td>완료</td>
   <td> </td>
  </tr>
  <tr>
   <td>잠금/잠금 해제</td>
   <td>완료</td>
   <td> </td>
  </tr>
  <tr>
   <td>속성 보기/편집</td>
   <td>완료</td>
   <td> </td>
  </tr>
  <tr>
   <td>페이지에 대한 권한 설정</td>
   <td>완료</td>
   <td> </td>
  </tr>
  <tr>
   <td>버전 내역</td>
   <td>완료</td>
   <td> </td>
  </tr>
  <tr>
   <td>버전 복원</td>
   <td>완료<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>트리 복원 및 삭제된 페이지 복원</td>
   <td>누락</td>
   <td>클래식 UI 사용을 참조하십시오.</td>
  </tr>
  <tr>
   <td>이전 버전과 현재 버전 간의 차이 표시<br /> </td>
   <td>완료<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Livecopy 작업(롤아웃)</td>
   <td>완료</td>
   <td> </td>
  </tr>
  <tr>
   <td>언어 사본 보기</td>
   <td>완료</td>
   <td> </td>
  </tr>
  <tr>
   <td>찾기 및 바꾸기</td>
   <td>Missing<br /> </td>
   <td>클래식 UI 사용을 참조하십시오.</td>
  </tr>
  <tr>
   <td>알림 받은 편지함(JCR 이벤트)</td>
   <td>누락</td>
   <td>클래식 UI 사용을 참조하십시오. 다른 구현으로 대체됩니다.</td>
  </tr>
  <tr>
   <td>참조</td>
   <td>완료</td>
   <td>AEM 6.5에 추가된 들어오는 페이지 링크 표시<br /> </td>
  </tr>
 </tbody>
</table>

## 기능 상태:페이지 편집기 {#feature-status-page-editor}

클래식 UI 페이지 편집기( `/cf#`)의 기능 목록과 터치 활성화 상태( `/editor.html`)입니다.

<table>
 <tbody>
  <tr>
   <td><strong>기능</strong></td>
   <td><strong>상태</strong></td>
   <td><strong>주석</strong></td>
  </tr>
  <tr>
   <td>웹 페이지 편집</td>
   <td>완료</td>
   <td> </td>
  </tr>
  <tr>
   <td>모바일 웹 페이지 편집<br /> </td>
   <td>완료<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Design Importer를 통해 가져온 컨텐츠 편집<br /> </td>
   <td>완료</td>
   <td> </td>
  </tr>
  <tr>
   <td>이메일 편집</td>
   <td>완료</td>
   <td> </td>
  </tr>
  <tr>
   <td>하이브리드 모바일 앱 편집</td>
   <td>완료<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>양식 편집</td>
   <td>완료<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>오퍼 편집</td>
   <td>완료<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>워크플로우 모델 편집<br /> </td>
   <td>완료</td>
   <td> </td>
  </tr>
  <tr>
   <td>ode:편집 및 미리 보기</td>
   <td>완료</td>
   <td> </td>
  </tr>
  <tr>
   <td>반응형 미리 보기<br /> </td>
   <td>완료</td>
   <td> </td>
  </tr>
  <tr>
   <td>모드:디자인 편집</td>
   <td>완료</td>
   <td> </td>
  </tr>
  <tr>
   <td>모드:Scaffolding</td>
   <td>완료</td>
   <td> </td>
  </tr>
  <tr>
   <td>모드:Live Copy 상태<br /> </td>
   <td>완료</td>
   <td> </td>
  </tr>
  <tr>
   <td>주석 추가</td>
   <td>완료</td>
   <td> </td>
  </tr>
  <tr>
   <td>속성 편집<br /> </td>
   <td>완료</td>
   <td> </td>
  </tr>
  <tr>
   <td>롤아웃 페이지</td>
   <td>완료<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>워크플로우 시작 및 표시</td>
   <td>완료</td>
   <td> </td>
  </tr>
  <tr>
   <td>워크플로우 패키지 처리</td>
   <td>대부분</td>
   <td>터치 지원 UI에서 액세스 가능 여러 워크플로우 페이로드가 여전히 클래식 UI에 표시됩니다.<br /> </td>
  </tr>
  <tr>
   <td>페이지 잠금/잠금 해제</td>
   <td>완료</td>
   <td> </td>
  </tr>
  <tr>
   <td>페이지 게시 <br /> </td>
   <td>완료<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>페이지 게시 취소</td>
   <td>완료</td>
   <td> </td>
  </tr>
  <tr>
   <td>페이지 복사</td>
   <td>제거됨<br /> </td>
   <td>사이트 관리자를 사용하여 페이지를 <a href="/help/sites-authoring/managing-pages.md#copying-and-pasting-a-page">복사합니다</a>.<br /> </td>
  </tr>
  <tr>
   <td>페이지 이동</td>
   <td>제거됨</td>
   <td>사이트 관리자를 사용하여 페이지를 <a href="/help/sites-authoring/managing-pages.md#moving-or-renaming-a-page">이동합니다</a>.<br /> </td>
  </tr>
  <tr>
   <td>페이지 삭제</td>
   <td>제거됨</td>
   <td>사이트 관리자를 사용하여 페이지를 <a href="/help/sites-authoring/managing-pages.md#deleting-a-page">삭제합니다</a>.<br /> </td>
  </tr>
  <tr>
   <td>참조 표시</td>
   <td>제거됨</td>
   <td>사이트 관리자를 <a href="/help/sites-authoring/author-environment-tools.md#references">사용하여 자세한 참조 목록을</a>봅니다.<br /> </td>
  </tr>
  <tr>
   <td>감사 로그</td>
   <td>제거됨</td>
   <td>사이트 관리자를 사용하고 <a href="/help/sites-authoring/author-environment-tools.md#events-timeline">활동 레일을</a>엽니다.<br /> </td>
  </tr>
  <tr>
   <td>버전 만들기</td>
   <td>제거됨</td>
   <td>사이트 관리자를 사용하여 새 버전을 <a href="/help/sites-authoring/working-with-page-versions.md#creating-a-new-version">만듭니다</a>.<br /> </td>
  </tr>
  <tr>
   <td>버전 복원</td>
   <td>제거됨</td>
   <td>사이트 관리자를 사용하여 버전을 <a href="/help/sites-authoring/working-with-page-versions.md#reverting-to-a-page-version">복원합니다</a>.</td>
  </tr>
  <tr>
   <td>시작 전환</td>
   <td>제거됨</td>
   <td>사이트 관리자를 사용하여 론치 <a href="/help/sites-authoring/launches-promoting.md">간을</a>전환합니다.<br /> </td>
  </tr>
  <tr>
   <td>페이지 번역</td>
   <td>제거됨</td>
   <td>사이트 관리자를 사용하여 번역 프로젝트에 <a href="/help/sites-administering/tc-manage.md">페이지를</a>추가합니다.<br /> </td>
  </tr>
  <tr>
   <td>타임워프(날짜/시간 선택 및 검색 사이트 선택)<br /> </td>
   <td>완료</td>
   <td> </td>
  </tr>
  <tr>
   <td>권한 설정</td>
   <td>완료</td>
   <td> </td>
  </tr>
  <tr>
   <td>클라이언트 컨텍스트 UI<br /> </td>
   <td>대체됨</td>
   <td>앞으로 ContextHub <a href="/help/sites-authoring/ch-previewing.md">UI를</a> 사용합니다.</td>
  </tr>
  <tr>
   <td>다양한 미디어 유형을 위한 컨텐츠 파인더<br /> </td>
   <td>완료</td>
   <td> </td>
  </tr>
  <tr>
   <td>구성 요소 목록</td>
   <td>완료<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>구성 요소 복사 및 붙여넣기<br /> </td>
   <td>완료</td>
   <td> </td>
  </tr>
  <tr>
   <td>클립보드의 구성 요소 목록</td>
   <td>누락</td>
   <td> </td>
  </tr>
  <tr>
   <td>실행 취소/다시 실행</td>
   <td>완료</td>
   <td> </td>
  </tr>
  <tr>
   <td>컨텐츠를 구성 요소 자리 표시자로 드래그하여 놓기</td>
   <td>완료</td>
   <td> </td>
  </tr>
  <tr>
   <td>구성 요소 자동 생성을 사용하여 컨텐츠를 parsys 자리 표시자로 바로 드래그 앤 드롭<br /> </td>
   <td>완료</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## 기능 상태:텍스트, 표 및 이미지 편집기 {#feature-status-text-table-and-image-editors}

클래식 UI 텍스트, 표 및 이미지 편집기의 기능 목록과 터치 지원 UI의 상태입니다.

<table>
 <tbody>
  <tr>
   <td><strong>기능</strong></td>
   <td><strong>상태 </strong></td>
   <td><strong>주석<br /> </strong></td>
  </tr>
  <tr>
   <td>리치 텍스트 편집기</td>
   <td>완료</td>
   <td>전체 화면에서 사용할 수 있습니다.</td>
  </tr>
  <tr>
   <td>RTE 플러그인 활성화/비활성화</td>
   <td>완료<br /> </td>
   <td>템플릿 편집기를 사용하여 수행할 <a href="/help/sites-authoring/templates.md">수 있습니다</a>.</td>
  </tr>
  <tr>
   <td>일반 텍스트에 RTE 사용</td>
   <td>완료<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>RTE 플러그인:링크 및 앵커</td>
   <td>완료</td>
   <td> </td>
  </tr>
  <tr>
   <td>RTE 플러그인:문자 맵</td>
   <td>완료</td>
   <td> </td>
  </tr>
  <tr>
   <td>RTE 플러그인:복사/붙여넣기</td>
   <td>완료</td>
   <td> </td>
  </tr>
  <tr>
   <td>RTE 플러그인:Microsoft Word에서 붙여넣기<br /> </td>
   <td>완료</td>
   <td> </td>
  </tr>
  <tr>
   <td>RTE 플러그인:찾기 및 바꾸기</td>
   <td>완료</td>
   <td> </td>
  </tr>
  <tr>
   <td>RTE 플러그인:텍스트 형식(굵게, ...)</td>
   <td>완료<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>RTE 플러그인:하위 및 위 첨자</td>
   <td>완료</td>
   <td> </td>
  </tr>
  <tr>
   <td>RTE 플러그인:양쪽 맞춤</td>
   <td>완료<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>RTE 플러그인:목록(글머리 기호/번호)</td>
   <td>완료</td>
   <td> </td>
  </tr>
  <tr>
   <td>RTE 플러그인:단락 형식</td>
   <td>완료<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>RTE 플러그인:텍스트 스타일</td>
   <td>완료</td>
   <td> </td>
  </tr>
  <tr>
   <td>RTE 플러그인:소스 편집기(HTML 편집)<br /> </td>
   <td>완료<br /> </td>
   <td>대화 상자와 전체 화면에서만 사용할 수 있습니다.<br /> </td>
  </tr>
  <tr>
   <td>RTE 플러그인:맞춤법 검사기</td>
   <td>완료</td>
   <td> </td>
  </tr>
  <tr>
   <td>RTE 플러그인:표(포함된 테이블 편집기)</td>
   <td>완료</td>
   <td> </td>
  </tr>
  <tr>
   <td>RTE 플러그인:실행 취소/다시 실행<br /> </td>
   <td>완료</td>
   <td> </td>
  </tr>
  <tr>
   <td>RTE 플러그인:인라인 이미지 허용</td>
   <td>완료</td>
   <td> </td>
  </tr>
  <tr>
   <td>테이블 편집기</td>
   <td>완료</td>
   <td>전체 화면에서 사용할 수 있습니다.<br /> </td>
  </tr>
  <tr>
   <td>표 셀에 이미지 드래그하여 놓기<br /> </td>
   <td>완료</td>
   <td>사용 가능한 인라인</td>
  </tr>
  <tr>
   <td>이미지 편집기<br /> </td>
   <td>완료</td>
   <td>전체 화면에서 사용할 수 있습니다.<br /> </td>
  </tr>
  <tr>
   <td>IPE 플러그인 활성화/비활성화</td>
   <td>완료</td>
   <td>AEM 6.3에서는 템플릿 편집기에서 UI를 <a href="/help/sites-authoring/templates.md">도입했습니다</a>.</td>
  </tr>
  <tr>
   <td>IPE 플러그인:자르기</td>
   <td>완료</td>
   <td> </td>
  </tr>
  <tr>
   <td>IPE 플러그인:뒤집기</td>
   <td>완료<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>IPE 플러그인:실행 취소/다시 실행</td>
   <td>완료<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>IPE 플러그인:이미지 맵</td>
   <td>완료</td>
   <td> </td>
  </tr>
  <tr>
   <td>IPE 플러그인:회전</td>
   <td>완료</td>
   <td> </td>
  </tr>
  <tr>
   <td>IPE 플러그인:확대/축소</td>
   <td>완료<br /> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

## 기능 상태:도구 {#feature-status-tools}

클래식 UI에 있는 다양한 도구 및 터치 지원 UI의 상태입니다.

<table>
 <tbody>
  <tr>
   <td><strong>기능<br /> </strong></td>
   <td><strong>상태<br /> </strong></td>
   <td><strong>주석</strong></td>
  </tr>
  <tr>
   <td>작업 관리</td>
   <td>대체됨</td>
   <td>6.0 도입된 <a href="/help/sites-authoring/projects.md">프로젝트 및 작업</a>.<br /> </td>
  </tr>
  <tr>
   <td>Workflow 받은 편지함<br /> </td>
   <td>완료</td>
   <td> </td>
  </tr>
  <tr>
   <td>페이지 템플릿 구성(<code>/etc/workflow/wcm/templates.html</code>) 워크플로우</td>
   <td>Missing<br /> </td>
   <td>클래식 UI 사용을 참조하십시오.</td>
  </tr>
  <tr>
   <td>관리 UI 태깅<br /> </td>
   <td>완료</td>
   <td> </td>
  </tr>
  <tr>
   <td>MSM/블루프린트 제어 센터</td>
   <td>완료</td>
   <td> </td>
  </tr>
  <tr>
   <td>Blueprint Manager UI</td>
   <td>완료</td>
   <td> </td>
  </tr>
  <tr>
   <td>롤아웃 구성 UI</td>
   <td>누락</td>
   <td>클래식 UI 사용을 참조하십시오.</td>
  </tr>
  <tr>
   <td>사용자, 그룹 및 권한 UI<br /> </td>
   <td>대부분 완료<br /> </td>
   <td>고급 권한 편집의 경우 클래식 UI를 사용합니다.<br /> </td>
  </tr>
  <tr>
   <td>버전 삭제(<code>/etc/versioning/purge.html</code>)</td>
   <td>누락</td>
   <td>클래식 UI 사용을 참조하십시오.</td>
  </tr>
  <tr>
   <td>외부 링크 확인 (<code>/etc/linkchecker.html</code>)</td>
   <td>누락</td>
   <td>클래식 UI 사용을 참조하십시오.<br /> </td>
  </tr>
  <tr>
   <td>벌크 편집기(<code>/etc/importers/bulkeditor.html</code>)</td>
   <td>Missing<br /> </td>
   <td>클래식 UI 사용을 참조하십시오.</td>
  </tr>
  <tr>
   <td>축소판을 업로드하여 축소판 추가 또는 덮어쓰기<br /> </td>
   <td>누락</td>
   <td>클래식 UI 사용을 참조하십시오.</td>
  </tr>
 </tbody>
</table>

