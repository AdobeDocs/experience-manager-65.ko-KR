---
title: Touch UI 기능 상태
description: ' [!DNL Adobe Experience Manager] 터치 사용 UI에 대한 릴리스 노트입니다.'
exl-id: 7b71e8db-e8c6-4470-bc22-db3d4600b7fc
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '1076'
ht-degree: 15%

---

# Touch UI 기능 상태 {#touch-ui-feature-status}

Adobe Experience Manager(AEM) 6.4 이상 [클래식 UI는 더 이상 사용되지 않습니다](../release-notes/deprecated-removed-features.md). Adobe은 클래식 UI를 더 이상 개선하지 않으며 사용자는 터치 지원 UI에서 사용할 수 있는 강력한 새 기능을 사용하는 것이 좋습니다.

버전 6.0부터 AEM에서는 [!DNL Adobe Experience Cloud] 및 전체 Adobe 사용자 인터페이스 지침에 맞게 조정된 &quot;터치 지원 UI&quot;(터치 UI라고 함)라는 새로운 사용자 인터페이스를 도입했습니다. 거의 기능 패리티에 도달함에 따라 &quot;클래식 UI&quot;라고 하는 레거시 데스크탑 지향 인터페이스를 사용하는 AEM의 표준 UI가 되었습니다.

터치 사용 UI에 대부분의 기능이 표시되지만 아직 완성되지 않은 기능이 있으며 향후 릴리스에서 추가될 예정입니다.

다음 목록은 AEM 6.5에 구현된 기능의 상태를 보여 줍니다.

AEM 6.5로 업그레이드하는 고객을 위한 권장 사항은 [고객을 위한 사용자 인터페이스 권장 사항](/help/sites-deploying/ui-recommendations.md)을 참조하십시오.

>[!NOTE]
>
>이 페이지는 기능 패리티를 클래식 UI로만 다룹니다. 클래식 UI에 없는 터치 지원 UI에 추가된 고유한 기능은 나열되지 않습니다.

>[!NOTE]
>
>이 목록은 완전하기 위해 노력하지만 완전하지 않습니다.

## 범례 {#legend}

* **완료**: 터치 사용 UI에서 기능을 완전히 사용할 수 있습니다.
* **대부분**: 터치 사용 UI에서 주로 사용할 수 있는 기능입니다.
* **누락**: 터치 사용 UI에 기능이 없습니다. 이 작업을 수행하려면 클래식 UI를 사용해야 합니다.
* **대체**: 기능이 다르게 작동하는 새 구현으로 대체되었습니다.
* **제거됨**: 터치 사용 UI에 기능이 더 이상 없으므로 교체되지 않습니다.

## 기능 상태: 사이트 관리자 {#feature-status-sites-admin}

클래식 UI 사이트 관리자(`/siteadmin`)의 기능 목록과 터치 사용 UI(`/sites.html`)의 상태입니다.

| 기능 | 상태 | 댓글 |
|--- |--- |--- |
| 사이트 계층 구조 탐색 | 완료 | AEM 6.4에서 [콘텐츠 트리 보기](/help/sites-authoring/basic-handling.md#content-tree)를 도입했습니다. |
| 워크플로 시작 | 완료 |  |
| 새 페이지 만들기 | 완료 |  |
| 새 사이트 만들기 | 완료 |  |
| 새 론치 만들기 | 완료 |  |
| 새 Live Copy 만들기 | 완료 |  |
| 폴더 만들기 | 완료 |  |
| 게시 상태 표시 | 완료 | AEM 6.5부터 목록 보기에 워크플로 상태가 표시됩니다. |
| 검색 | 완료 |  |
| 페이지 복사 및 붙여넣기(복제) | 완료 |  |
| 페이지 이동 | 완료 |  |
| Publish 페이지 | 완료 |  |
| 복제 권한이 없는 Publish 페이지 | 완료 |  |
| 나중에 게시 | 완료 |  |
| Publish 트리 | 완료 |  |
| 페이지 게시 취소 | 완료 |  |
| 복제 권한이 없는 페이지 게시 취소 | 완료 |  |
| 나중에 게시 취소 | 완료 |  |
| 삭제 | 완료 |  |
| 잠금/잠금 해제 | 완료 |  |
| 속성 보기/편집 | 완료 |  |
| 페이지에 대한 권한 설정 | 완료 |  |
| 버전 내역 | 완료 |  |
| 버전 복원 | 완료 |  |
| 트리 복원 및 삭제된 페이지 복원 | 누락 | 클래식 UI를 사용합니다. |
| 이전 버전과 현재 버전 간의 차이점 표시 | 완료 |  |
| 라이브 카피 작업(롤아웃) | 완료 |  |
| 언어 사본 보기 | 완료 |  |
| 찾기 및 바꾸기 | 누락 | 클래식 UI를 사용합니다. |
| 알림 받은 편지함(JCR 이벤트) | 누락 | 클래식 UI를 사용합니다. 나중에 다른 구현으로 대체되었습니다. |
| 참조 | 완료 | AEM 6.5에 추가된 수신 페이지 링크 표시 |

## 기능 상태: 페이지 편집기 {#feature-status-page-editor}

클래식 UI 페이지 편집기(`/cf#`)의 기능과 터치 사용(`/editor.html`)의 상태 목록입니다.

| 기능 | 상태 | 댓글 |
|--- |--- |--- |
| 웹 페이지 편집 | 완료 |  |
| 모바일 웹 페이지 편집 | 완료 |  |
| 디자인 Importer를 통해 가져온 콘텐츠 편집 | 완료 |  |
| 이메일 편집 | 완료 |  |
| 하이브리드 모바일 앱 편집 | 완료 |  |
| Forms 편집 | 완료 |  |
| 오퍼 편집 | 완료 |  |
| 워크플로우 모델 편집 | 완료 |  |
| 모드: 편집 및 미리보기 | 완료 |  |
| 반응형 미리 보기 | 완료 |  |
| 모드: 디자인 편집 | 완료 |  |
| 모드: 스캐폴딩 | 완료 |  |
| 모드: 라이브 카피 상태 | 완료 |  |
| 주석 추가 | 완료 |  |
| 속성 편집 | 완료 |  |
| 페이지 롤아웃 | 완료 |  |
| 워크플로우 시작 및 표시 | 완료 |  |
| 워크플로우 패키지 처리 | 대부분 | 터치 지원 UI에서 액세스할 수 있습니다. 여러 워크플로우 페이로드가 클래식 UI에 계속 표시됩니다. |
| 페이지 잠금/잠금 해제 | 완료 |  |
| 페이지 게시 | 완료 |  |
| 페이지 게시 취소 | 완료 |  |
| 페이지 복사 | 제거됨 | 사이트 관리자를 사용하여 [페이지를 복사](/help/sites-authoring/managing-pages.md#copying-and-pasting-a-page)하십시오. |
| 페이지 이동 | 제거됨 | 사이트 관리자를 사용하여 [페이지를 이동](/help/sites-authoring/managing-pages.md#moving-or-renaming-a-page)하세요. |
| 페이지 삭제 | 제거됨 | 사이트 관리자를 사용하여 [페이지를 삭제](/help/sites-authoring/managing-pages.md#deleting-a-page)하세요. |
| 참조 표시 | 제거됨 | 사이트 관리자를 사용하여 [자세한 참조 목록](/help/sites-authoring/author-environment-tools.md#references)을 확인하세요. |
| 감사 로그 | 제거됨 | 사이트 관리자를 사용하고 [활동 레일을 엽니다](/help/sites-authoring/author-environment-tools.md#events-timeline). |
| 버전 만들기 | 제거됨 | 사이트 관리자를 사용하여 [새 버전을 만듭니다](/help/sites-authoring/working-with-page-versions.md#creating-a-new-version). |
| 버전 복원 | 제거됨 | 사이트 관리자를 사용하여 [버전을 복원](/help/sites-authoring/working-with-page-versions.md#reverting-to-a-page-version)하세요. |
| 시작 전환 | 제거됨 | 사이트 관리자를 사용하여 [시작 간 전환](/help/sites-authoring/launches-promoting.md)하세요. |
| 페이지 번역 | 제거됨 | 사이트 관리자를 사용하여 [번역 프로젝트에 페이지를 추가](/help/sites-administering/tc-manage.md)하세요. |
| 타임워프(날짜/시간을 선택하고 보이는 대로 사이트를 탐색함) | 완료 |  |
| 권한 설정 | 완료 |  |
| Client Context UI | 대체됨 | 앞으로 [ContextHub](/help/sites-authoring/ch-previewing.md) UI를 사용하십시오. |
| 다양한 미디어 유형에 대한 콘텐츠 파인더 | 완료 |  |
| 구성 요소 목록 | 완료 |  |
| 구성 요소 복사 및 붙여넣기 | 완료 |  |
| 클립보드의 구성 요소 목록 | 누락 |  |
| 실행 취소 / 다시 실행 | 완료 |  |
| 콘텐츠를 구성 요소 플레이스홀더로 드래그 | 완료 |  |
| 구성 요소 자동 생성을 사용하여 콘텐츠를 parsys 자리 표시자로 직접 드래그합니다. | 완료 |  |

## 기능 상태: 텍스트, 테이블 및 이미지 편집기 {#feature-status-text-table-and-image-editors}

클래식 UI 텍스트, 테이블 및 이미지 편집기의 기능과 터치 사용 UI의 상태 목록이 표시됩니다.

| 기능 | 상태 | 댓글 |
|--- |--- |--- |
| 리치 텍스트 편집기 | 완료 | 즉석, 대화 상자 및 전체 화면에서 사용할 수 있습니다. |
| RTE 플러그인 활성화/비활성화 | 완료 | [템플릿 편집기](/help/sites-authoring/templates.md)를 사용하여 수행할 수 있습니다. |
| 일반 텍스트에 RTE 사용 | 완료 |  |
| RTE 플러그인: 링크 및 앵커 | 완료 |  |
| RTE 플러그인: 문자 맵 | 완료 |  |
| RTE 플러그인: 복사/붙여넣기 | 완료 |  |
| RTE 플러그인: Microsoft® Word에서 붙여넣기 | 완료 |  |
| RTE 플러그인: 찾기 및 바꾸기 | 완료 |  |
| RTE 플러그인: 텍스트 형식(굵게, ...) | 완료 |  |
| RTE 플러그인: 하위 및 위 첨자 | 완료 |  |
| RTE 플러그인: 양쪽 맞춤 | 완료 |  |
| RTE 플러그인: 목록(글머리 기호 / 숫자) | 완료 |  |
| RTE 플러그인: 단락 형식 | 완료 |  |
| RTE 플러그인: 텍스트 스타일 | 완료 |  |
| RTE 플러그인: Source 편집기(편집 HTML) | 완료 | 대화 상자 및 전체 화면에서만 사용할 수 있습니다. |
| RTE 플러그인: 맞춤법 검사기 | 완료 |  |
| RTE 플러그인: 테이블(포함된 테이블 편집기) | 완료 |  |
| RTE 플러그인: 실행 취소/다시 실행 | 완료 |  |
| RTE 플러그인: 인라인 이미지 허용 | 완료 |  |
| 테이블 편집기 | 완료 | 즉석, 대화 상자 및 전체 화면에서 사용할 수 있습니다. |
| 표 셀로 이미지 드래그 | 완료 | 인라인 사용 가능 |
| 이미지 편집기 | 완료 | 즉석, 대화 상자 및 전체 화면에서 사용할 수 있습니다. |
| IPE 플러그인 활성화/비활성화 | 완료 | AEM 6.3에서 [템플릿 편집기](/help/sites-authoring/templates.md)에 UI를 도입했습니다. |
| IPE 플러그인: 자르기 | 완료 |  |
| IPE 플러그인: 뒤집기 | 완료 |  |
| IPE 플러그인: 실행 취소/다시 실행 | 완료 |  |
| IPE 플러그인: 이미지 맵 | 완료 |  |
| IPE 플러그인: 회전 | 완료 |  |
| IPE 플러그인: 확대/축소 | 완료 |  |

## 기능 상태: 도구 {#feature-status-tools}

클래식 UI에 있는 다양한 도구 목록과 터치 지원 UI의 상태입니다.

| 기능 | 상태 | 댓글 |
|--- |--- |--- |
| 작업 관리 | 대체됨 | 6.0에 프로젝트 및 작업이 도입되었습니다. |
| 워크플로우 받은 편지함 | 완료 |  |
| 페이지 템플릿 구성에 대한 워크플로(`/etc/workflow/wcm/templates.html`) | 누락 | 클래식 UI를 사용합니다. |
| 태그 지정 관리자 UI | 완료 |  |
| MSM/블루프린트 제어 센터 | 완료 |  |
| 블루프린트 관리자 UI | 완료 |  |
| 롤아웃 구성 UI | 누락 | 클래식 UI를 사용합니다. |
| 사용자, 그룹 및 권한 UI | 대부분 완료 | 고급 권한 편집의 경우 클래식 UI를 사용하십시오. |
| 버전 제거(`/etc/versioning/purge.html`) | 누락 | 클래식 UI를 사용합니다. |
| 외부 링크 확인(`/etc/linkchecker.html`) | 누락 | 클래식 UI를 사용합니다. |
| 벌크 편집기(`/etc/importers/bulkeditor.html`) | 누락 | 클래식 UI를 사용합니다. |
| 축소판을 업로드하여 추가하거나 덮어쓰기 | 누락 | 클래식 UI를 사용합니다. |
