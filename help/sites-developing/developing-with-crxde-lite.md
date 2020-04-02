---
title: CRXDE Lite를 사용한 개발
seo-title: CRXDE Lite를 사용한 개발
description: CRXDE Lite가 AEM에 포함되어 있으므로 브라우저에서 표준 개발 작업을 수행할 수 있습니다.
seo-description: CRXDE Lite가 AEM에 포함되어 있으므로 브라우저에서 표준 개발 작업을 수행할 수 있습니다.
uuid: f4890354-d8b8-4fb9-af2f-3359f931f883
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 4537c1fb-f99c-42e2-a222-b037794bdb52
docset: aem65
translation-type: tm+mt
source-git-commit: 78133b41e1c99f8f86f4c0d51961287735423fe2

---


# CRXDE Lite를 사용한 개발{#developing-with-crxde-lite}

이 섹션에서는 CRXDE Lite를 사용하여 AEM 애플리케이션을 개발하는 방법에 대해 설명합니다.

사용 가능한 다양한 개발 환경에 대한 자세한 내용은 개요 설명서를 참조하십시오.

CRXDE Lite가 AEM에 포함되어 있으므로 브라우저에서 표준 개발 작업을 수행할 수 있습니다. CRXDE Lite를 사용하면 프로젝트를 만들고 파일(예: .jsp 및 .java), 폴더, 템플릿, 구성 요소, 대화 상자, 노드, 속성 및 번들을 만들고 편집할 수 있으며 SVN과 로깅 및 통합할 수 있습니다.
CRXDE Lite는 AEM 서버에 직접 액세스할 수 없는 경우, 기본 구성 요소 및 Java 번들을 확장 또는 수정하여 애플리케이션을 개발할 때 또는 전용 디버거, 코드 완성 및 구문 강조 표시가 필요하지 않은 경우에 권장됩니다.

>[!NOTE]
>
>기본적으로 모든 AEM 사용자는 CRXDE Lite에 액세스할 수 있습니다. 원하는 경우 개발자만 CRX DE [Lite에 액세스할 수 있도록 다음 노드에 대한 ACL을](/help/sites-administering/security.md#permissions-and-acls) 구성합니다.
>
>`/libs/granite/crxde`

>[!NOTE]
>
>프로젝트 개발 중에는 Eclipse용 AEM [개발자 도구 및 AEM HTL](/help/sites-developing/aem-eclipse.md) Brackets [확장을](/help/sites-developing/aem-brackets.md) 사용하는 것이좋습니다.

## CRXDE Lite 시작하기 {#getting-started-with-crxde-lite}

CRXDE Lite를 시작하려면 다음과 같이 하십시오.

1. AEM 설치.
1. 브라우저에서 을 입력합니다 `https://<host>:<port>/crx/de`. 기본적으로 `https://localhost:4502/crx/de`표시됩니다.
1. 사용자 **이름과** **암호를**&#x200B;입력합니다. 기본적으로 `admin` 및 `admin`입니다.

1. **확인**&#x200B;을 클릭합니다.

CRXDE Lite 사용자 인터페이스는 브라우저에서 다음과 같이 표시됩니다.

![chlimage_1-18](assets/chlimage_1-18.png)

이제 CRXDE Lite를 사용하여 애플리케이션을 개발할 수 있습니다.

## 사용자 인터페이스 개요 {#overview-of-the-user-interface}

CRXDE Lite는 다음 기능을 제공합니다.

<table>
 <tbody>
  <tr>
   <td>상단 전환기 막대</td>
   <td>CRXDE Lite, 패키지 관리자 및 패키지 공유 간을 신속하게 전환할 수 있습니다.</td>
  </tr>
  <tr>
   <td>노드 경로 위젯</td>
   <td><p>현재 선택된 노드의 경로를 표시합니다.</p> <p>노드를 직접 입력하거나 다른 곳에서 붙여넣은 다음 Enter 키를 눌러 이동할 수도 있습니다.</p> <p>또한 특정 노드 이름이 있는 노드를 찾을 수 있도록 지원합니다. 찾을 노드의 이름을 입력하고 기다리거나(또는 오른쪽에 있는 검색 기호를 누르십시오). 위젯에 문자열 <em>oak</em> 문자열을 입력해서 작동 방식을 확인할 수 있습니다. 지정된 노드 또는 노드가 탐색기 창에 로드되면 목록이 표시되고, 경로를 선택하고 Enter 키를 눌러 탐색합니다. 브라우저에서 CRXDE 클라이언트 애플리케이션에 현재 로드되어 있는 노드에만 작동합니다. 전체 저장소를 검색하려면 도구, 쿼리를 차례로 사용합니다.</p> </td>
  </tr>
  <tr>
   <td>탐색기 창</td>
   <td><p>저장소의 모든 노드의 트리를 표시합니다.</p> <p>노드를 클릭하여 속성 탭에 속성을 <strong>표시합니다</strong> . 노드를 클릭한 후 도구 모음에서 작업을 선택할 수 있습니다. 노드를 다시 클릭하여 이름을 변경합니다.</p> <p>트리 탐색 필터(쌍안경 아이콘):저장소에서 이름에 입력 텍스트가 포함된 노드를 필터링할 수 있습니다. 로컬로 로드된 노드에만 적용됩니다.<br /> </p> </td>
  </tr>
  <tr>
   <td>편집 창</td>
   <td><p><strong>홈</strong> 탭:컨텐츠 및/또는 문서를 검색하고 개발자 리소스(설명서, 개발자 블로그, 기술 자료) 및 지원(Adobe 홈 페이지 및 지원 센터)에 액세스할 수 있습니다.<br /> </p> <p>탐색기 창에서 파일을 두 번 <strong>클릭하여</strong> 해당 컨텐츠를 표시합니다.예: .jsp 또는 .java 파일 그런 다음 수정한 후 변경 내용을 저장할 수 있습니다.</p> <p>편집 창에서 파일을 편집한 <strong>후</strong> 도구 모음에서 다음 도구를 사용할 수 있습니다.<br /> </p> - <strong>트리에 표시:저장소 트리에 파일을 </strong>표시합니다.<br /> - <strong>검색/바꾸기 ...</strong>:검색하거나 바꾸십시오.<br /> 편집 <br /> 창의 상태 줄을 두 번 클릭하면 <strong>이동</strong> <strong>라인</strong> 대화 상자가 열리면서 이동할 특정 라인 번호를 입력할 수 있습니다.<br /> </td>
  </tr>
  <tr>
   <td>속성 탭<br /> </td>
   <td>선택한 노드의 속성을 표시합니다. 새 속성을 추가하거나 기존 속성을 삭제할 수 있습니다.<br /> </td>
  </tr>
  <tr>
   <td>액세스 제어 탭</td>
   <td><p>현재 경로, 저장소 수준 또는 주체에 따라 권한을 표시합니다.</p> <p>권한은</p> <p>- <strong>해당 액세스 제어 정책</strong>:현재 선택 항목에 적용할 수 있는 정책입니다.</p> <p>- <strong>로컬 액세스 제어 정책</strong>:현재 선택 항목에 로컬로 적용된 현재 정책.</p> <p>- <strong>효과적인 액세스 제어 정책</strong>:현재 선택 항목에 적용된 현재 정책은 로컬에서 설정되거나 상위 노드에서 상속될 수 있습니다.</p> <p>메모. 액세스 제어 정보를 전혀 볼 수 있으려면 CRXDE Lite에 로그인한 사용자가 ACL 항목을 읽을 수 있는 권한이 있어야 합니다. 익명의 사용자는 기본적으로 이 정보를 볼 수 없습니다. 예를 들어, 관리자로 로그인하여 정보를 확인하십시오.</p> </td>
  </tr>
  <tr>
   <td>복제 탭</td>
   <td><p>현재 노드의 복제 상태를 표시합니다. 현재 노드를 복제 및 복제할 수 있습니다.</p> </td>
  </tr>
  <tr>
   <td>콘솔 탭<br /> </td>
   <td><p><strong>서버 로그</strong>:</p> <p>로그 메시지를 표시합니다. 로그 수준을 구성하고, 콘솔을 지우고, 선택한 스크롤 위치에 고정하고, 메시지 표시를 활성화/비활성화할 수 있습니다.<br /> </p> <p><strong>버전 제어</strong>:</p> <p>버전 제어 메시지를 표시합니다.<br /> </p> </td>
  </tr>
  <tr>
   <td>빌드 정보 탭<br /> </td>
   <td>번들을 빌드할 때 정보를 표시합니다.<br /> </td>
  </tr>
  <tr>
   <td>새로 고침<br /> </td>
   <td>현재 선택 항목을 새로 고칩니다. 다른 사용자의 변경 사항은 저장소 보기에서 업데이트됩니다. 변경한 내용은 영향을 받지 않습니다.<br /> </td>
  </tr>
  <tr>
   <td>모두 저장</td>
   <td><p><strong>모두 저장</strong>:<br /> </p> <p>변경한 모든 내용을 저장합니다. 저장을 클릭할 때까지 변경 사항은 일시적이며 콘솔을 종료하면 손실됩니다.</p> <p><strong>되돌리기</strong>:</p> <p>마지막 저장 작업 이후 선택한 노드에서 수행한 모든 변경 사항을 삭제한 다음 선택한 노드에 대한 저장소의 현재 상태를 다시 로드합니다.</p> <p><strong>모두 되돌리기</strong>:</p> <p>마지막 저장 작업 이후 전체 저장소 전체에서 수행한 모든 변경 내용을 삭제한 다음 저장소의 현재 상태를 다시 로드합니다.</p> </td>
  </tr>
  <tr>
   <td>만들기 ...<br /> </td>
   <td><p>드롭다운 메뉴를 사용하여 선택한 노드 아래에 다음을 만듭니다.<br /> </p> <p>- <strong>노드</strong>:임의 노드 유형이 있는 노드<br /> </p> <p>- <strong>파일</strong>:nt:file node and its nt:resource subnode</p> <p>- <strong>폴더</strong>:nt:folder 노드</p> <p>- <strong>템플릿</strong>:AEM 템플릿</p> <p>- <strong>구성 요소</strong>:AEM 구성 요소</p> <p>- <strong>대화 상자</strong>:AEM 대화 상자</p> </td>
  </tr>
  <tr>
   <td>삭제<br /> </td>
   <td>선택한 노드를 삭제합니다.<br /> </td>
  </tr>
  <tr>
   <td>복사</td>
   <td>선택한 노드를 복사합니다.<br /> </td>
  </tr>
  <tr>
   <td>붙여넣기<br /> </td>
   <td>복사한 노드를 선택한 노드 아래에 붙여 넣습니다.<br /> </td>
  </tr>
  <tr>
   <td>이동 ...<br /> </td>
   <td>선택한 노드를 대화 상자를 통해 설정된 노드로 이동합니다.</td>
  </tr>
  <tr>
   <td>이름 변경 ...<br /> </td>
   <td>선택한 노드의 이름을 변경합니다.<br /> </td>
  </tr>
  <tr>
   <td>Mixins ...<br /> </td>
   <td>노드 유형에 혼합형 유형을 추가할 수 있습니다. 대부분의 mixin 유형은 버전 관리, 액세스 제어, 참조 및 노드 잠금과 같은 고급 기능을 추가하는 데 사용됩니다.</td>
  </tr>
  <tr>
   <td>팀<br /> </td>
   <td><p>표준 버전 제어 작업을 수행하는 드롭다운 메뉴:</p> <p>- <strong>SVN</strong> 서버의 저장소 업데이트</p> <p>- <strong>SVN</strong> 서버에 로컬 변경 내용 커밋</p> <p>- <strong>현재</strong> 노드의 상태 보기</p> <p>- <strong>현재</strong> 노드의 하위 트리에서 재귀적 상태 보기</p> <p>- <strong>SVN</strong> 서버에서 작업 복사본 체크 아웃</p> <p>- <strong>SVN</strong> 서버에서 프로젝트 내보내기(작업 복사본을 만들지 않음)</p> <p>- <strong>저장소에서 SVN</strong> 서버로 프로젝트 가져오기<br /> </p> <p>일부 작업(특히 로컬 저장소에 쓰는 작업)을 실행할 수 있으려면 충분한 권한이 있는 사용자로 로그인해야 합니다.<br /> </p> </td>
  </tr>
  <tr>
   <td>도구<br /> </td>
   <td><p>다음 도구가 있는 드롭다운 메뉴:</p> <p>- <strong>서버 구성 ...</strong>:를 클릭하여 Felix Console에 액세스합니다.</p> <p>- <strong>쿼리 ...</strong>:to query the repository.</p> <p>- <strong>권한 ...</strong>:권한을 보고 추가할 수 있는 권한 관리를 엽니다.</p> <p>- <strong>테스트 액세스 제어 ...</strong>:특정 경로 및/또는 주체에 대한 권한을 테스트할 수 있는 장소.</p> <p>- <strong>내보내기 노드 유형</strong>:to export node types in the system as cnd notation.</p> <p>- <strong>노드 유형 가져오기 ...</strong>:를 사용하여 노드 유형을 가져옵니다.</p> <p>- <strong>SiteCatalyst 디버거 설치 ...</strong>:analytics Debugger 설치 방법에 대한 지침.</p> </td>
  </tr>
  <tr>
   <td>로그인 위젯<br /> </td>
   <td><p>현재 로그인한 사용자와 사용자가 로그인한 작업 영역(예: admin@crx.default)을 표시합니다.</p> <p>이 아이콘을 클릭하여 로그인하거나 특정 사용자로 다시 로그인합니다. 로그인할 작업 영역을 지정하지 않으면 기본 작업 영역인 crx.default에 로그인됩니다.</p> <p>저장소를 익명 사용자로 찾아보려면 로그인 이름과 암호(예: 공간 또는 점)로 <strong>익명의</strong> 사용자를 사용하십시오.<br /> </p> <p>인증이 더 이상 유효하지 않은 경우(예: 만료됨) 로그인 위젯에 "권한 없음 -<strong>로그인..</strong>"이 표시됩니다. 다시 로그인하려면 클릭합니다.</p> </td>
  </tr>
 </tbody>
</table>

## 프로젝트 만들기 {#creating-a-project}

CRXDE Lite를 사용하면 3번의 클릭으로 작업 프로젝트를 만들 수 있습니다. 프로젝트 마법사는 새 프로젝트를 만들고, `/apps`일부 컨텐츠는 `/conten`t 아래에, 패키지는 모든 프로젝트에 해당 컨텐츠가 래핑됩니다 `/etc/packages`. 이 프로젝트는 저장소에서 속성을 렌더링하고 Java 클래스를 호출하여 일부 텍스트를 렌더링하는 **jsp**&#x200B;스크립트를 기반으로 Hello World를 표시하는 샘플 페이지를 바로 렌더링하는 데 사용할 수 있습니다.

CRXDE Lite를 사용하여 프로젝트를 만들려면

1. 브라우저에서 CRXDE Lite를 엽니다.
1. 탐색 창에서 노드를 마우스 오른쪽 단추로 클릭하고 만들기... ****, 프로젝트 **만들기...를 선택합니다.**.
참고:새 프로젝트 노드는 디자인 방식으로 아래 및 `/apps,``/content` 에서 만든 것처럼 트리 탐색 시 노드를 마우스 오른쪽 단추로 클릭할 수 `/etc/packages`있습니다.

1. 정의:

   * **프로젝트** 이름 - 프로젝트 이름은 새 노드 및 번들을 만드는 데 사용됩니다(예: `myproject`Adobe

   * **Java** 패키지 - Java 패키지 이름 접두사(예: `com.mycompany`Adobe

1. **만들기**&#x200B;를 클릭합니다.
1. 모두 **저장을** 클릭하여 변경 내용을 서버에 저장합니다.

Hello World를 표시하는 샘플 **페이지에 액세스하려면**&#x200B;브라우저에서 다음을 가리킵니다.

`https://localhost:4502/content/<project-name>.html`

Hello **World** 페이지는 속성을 통해 jsp 스크립트를 호출하는 컨텐츠 노드를 기반으로 `sling:resourceType` 합니다. 스크립트는 저장소에서 속성을 읽고 프로젝트 번들에 있는 SampleUtil 클래스의 메서드를 호출하여 본문 컨텐츠를 가져옵니다. `jcr:title`

다음 노드가 만들어집니다.

* `/apps/<project-name>`:응용 프로그램 컨테이너입니다.
* `/apps/<project-name>/components`:페이지를 렌더링하는 데 사용되는 샘플 html.jsp 파일을 포함하는 구성 요소 컨테이너입니다.

* `/apps/<project-name>/src`:샘플 프로젝트 번들을 포함하는 번들 컨테이너입니다.

* `/apps/<project-name>/install`:컴파일된 샘플 프로젝트 번들을 포함하는 컴파일된 번들 컨테이너입니다.
* `/content/<project-name>`:컨텐츠 컨테이너.
* /etc/packages/&lt;java-suffix>/&lt;project-name>.zip, 모든 프로젝트 앱 및 콘텐츠를 래핑하는 패키지 프로젝트를 다시 빌드하여 추가 배포(예: 다른 환경으로)하거나 패키지 공유를 통해 공유할 수 있습니다.

구조는 CRXDE Lite에서 **myproject** 및 **mycompany**&#x200B;라는 java 패키지 접미사를 사용하여 다음과 같이 보입니다.

![chlimage_1-19](assets/chlimage_1-19.png)

![chlimage_1-20](assets/chlimage_1-20.png)

## Creating a Folder {#creating-a-folder}

CRXDE Lite를 사용하여 폴더를 만들려면:

1. 브라우저에서 CRXDE Lite를 엽니다.
1. 탐색 창에서 새 폴더를 만들 폴더를 마우스 오른쪽 단추로 클릭하고 만들기... ****, 폴더 **만들기...를 선택합니다.**.

1. 폴더 이름을 **입력하고** 확인을 **클릭합니다**.

1. 모두 **저장을** 클릭하여 변경 내용을 서버에 저장합니다.

## Creating a Template {#creating-a-template}

CRXDE Lite를 사용하여 템플릿을 만들려면:

1. 브라우저에서 CRXDE Lite를 엽니다.
1. 탐색 창에서 템플릿을 만들 폴더를 마우스 오른쪽 단추로 클릭하고 만들기... ****, 템플릿 **만들기...를 선택합니다.**.

1. 레이블, **제목**, **설명******&#x200B;리소스 **유형,** 범위 및 규칙의 등급 **** 템플릿을 입력합니다. **다음**&#x200B;을 클릭합니다.

1. 이 단계는 선택 사항입니다.허용되는 **경로를 설정합니다**. **다음**&#x200B;을 클릭합니다

1. 이 단계는 선택 사항입니다.허용된 **부모를 설정합니다**. **다음**&#x200B;을 클릭합니다.

1. 이 단계는 선택 사항입니다.허용 **하위 설정을 지정합니다**. **확인**&#x200B;을 클릭합니다.

1. 모두 **저장을** 클릭하여 변경 내용을 서버에 저장합니다.

이렇게 하면 다음과 같은 기능이 생성됩니다.

* 템플릿 속성이 `cq:Template` 있는 유형 노드

* 페이지 컨텐츠 속성이 `cq:PageContent` 있는 유형의 하위 노드

템플릿에 속성을 추가할 수 있습니다.속성 [만들기 섹션을](#creating-a-property) 참조하십시오.

## 구성 요소 만들기 {#creating-a-component}

여기에 설명된 기능은 CQ5가 설치되어 있는 경우에만 사용할 수 있습니다. 즉, 저장소에서 노드 유형을 사용할 수 `cq:Component` 있습니다.

CRXDE Lite를 사용하여 구성 요소를 만들려면

1. 브라우저에서 CRXDE Lite를 엽니다.
1. 탐색 창에서 구성 요소를 만들 폴더를 마우스 오른쪽 단추로 클릭하고 만들기... ****, 구성 요소 **만들기...를 선택합니다.**.

1. 레이블, ****&#x200B;제목 **,****설명**, **슈퍼 리소스 유형 및 구성 요소의** **** SuperResource Type 및 Cohnightgroup을 입력합니다. **다음**&#x200B;을 클릭합니다.

1. 이 단계는 선택 사항입니다.구성 요소 속성Is 컨테이너, 데코레이션 **없음** , **셀 이름**&#x200B;및 **대화 상자** 경로를 ****&#x200B;설정합니다. **다음**&#x200B;을 클릭합니다.

1. 이 단계는 선택 사항입니다.구성 요소 속성 허용 **부모를 설정합니다**. **다음**&#x200B;을 클릭합니다.

1. 이 단계는 선택 사항입니다.구성 요소 속성 Allowed **Children을 설정합니다**. **확인**&#x200B;을 클릭합니다.

1. 모두 **저장을** 클릭하여 변경 내용을 서버에 저장합니다.

이렇게 하면 다음과 같은 기능이 생성됩니다.

* A node of type `cq:Component`
* 구성 요소 속성
* 구성 요소 .jsp 스크립트

## 대화 상자 만들기 {#creating-a-dialog}

CRXDE Lite를 사용하여 대화 상자를 만들려면

1. 브라우저에서 CRXDE Lite를 엽니다.
1. 탐색 창에서 대화 상자를 만들 구성 요소를 마우스 오른쪽 단추로 클릭하고 만들기... ****, 대화 **상자 만들기...를 선택합니다.**.

1. 레이블과 **제목을** 입력합니다 ****. **확인**&#x200B;을 클릭합니다.

1. [ **모두**&#x200B;저장]을 클릭하여 변경 내용을 서버에 저장합니다.

다음 구조를 갖는 대화 상자가 만들어집니다.

`dialog[cq:Dialog]/items[cq:Widget]/items[cq:WidgetCollection]/tab1[cq:Panel]`

이제 속성을 수정하거나 새 노드를 만들어 대화 상자를 필요에 맞게 조정할 수 있습니다.

대화 상자 편집기를 사용하여 대화 상자를 편집할 수도 있습니다. CRXDE Lite에서 대화 상자 노드를 두 번 클릭하면 편집기가 표시됩니다. 대화 상자 편집기에 대한 자세한 내용은 [여기에서](/help/sites-developing/dialog-editor.md)확인할 수 있습니다.

## 노드 생성 {#creating-a-node}

CRXDE Lite를 사용하여 노드를 만들려면

1. 브라우저에서 CRXDE Lite를 엽니다.
1. 탐색 창에서 새 노드를 만들 노드를 마우스 오른쪽 단추로 클릭하고 만들기... ****, 노드 **만들기...를 선택합니다.**.
1. 이름과 **유형을** 입력합니다 ****. **확인**&#x200B;을 클릭합니다.
1. 모두 **저장을** 클릭하여 변경 내용을 서버에 저장합니다.

이제 속성을 수정하거나 새 노드를 만들어 필요에 맞게 노드를 조정할 수 있습니다.

>[!NOTE]
>
>노드 만들기를 비롯한 대부분의 편집 작업은 메모리에 모든 변경 사항을 저장하고 저장 시(모두 저장) 저장소에 저장합니다. 그러나 이동 같은 일부 작업은 자동으로 지속됩니다.
>
>변경 사항을 저장할 때 JCR 보관소에서 새로 생성된 노드를 상위 노드의 노드 유형으로 허용하는지 여부에 대한 유효성 검사도 먼저 수행됩니다. 노드를 저장하는 동안 오류 메시지가 표시되는 경우 컨텐츠 구조가 유효한지 확인하십시오(예: 노드를 `nt:unstructured` `nt:folder` 노드의 자식으로 만들 수 없음).

## 속성 만들기 {#creating-a-property}

CRXDE Lite를 사용하여 속성을 만들려면:

1. 브라우저에서 CRXDE Lite를 엽니다.
1. 탐색 창에서 새 속성을 추가할 노드를 선택합니다.
1. 하단 **창의** 속성 **탭에서 이름,**&#x200B;유형 **및** 값 **값을**&#x200B;입력합니다. **추가**&#x200B;를 클릭합니다.

1. 모두 **저장을** 클릭하여 변경 내용을 서버에 저장합니다.

## 스크립트 만들기 {#creating-a-script}

새 스크립트를 만들려면:

1. 브라우저에서 CRXDE Lite를 엽니다.
1. 탐색 창에서 스크립트를 만들 구성 요소를 마우스 오른쪽 단추로 클릭하고 만들기... ****, 파일 **만들기...를 선택합니다.**.

1. 확장자를 **포함하는 파일** 이름을 입력합니다. **확인**&#x200B;을 클릭합니다.

1. 새 파일이 편집 창에서 탭으로 열립니다.
1. 파일을 편집합니다.
1. 모두 **저장을** 클릭하여 변경 내용을 저장합니다.

## 번들 관리 {#managing-a-bundle}

CRXDE Lite를 사용하면 OSGI 번들을 손쉽게 제작하고 Java 클래스를 추가한 다음 구축할 수 있습니다. 그러면 번들이 자동으로 설치되고 OSGI 컨테이너에서 시작됩니다.

이 섹션에서는 Hello World! `Test` `HelloWorld` **** 을 클릭합니다.

### 번들 만들기 {#creating-a-bundle}

CRXDE Lite를 사용하여 테스트 번들을 만들려면:

1. CRXDE Lite에서 `myapp` 프로젝트 마법사를 [](#creating-a-project)사용하여 프로젝트를 만듭니다. 그 외에도 다음과 같은 노드가 만들어집니다.

   * `/apps/myapp/src`
   * `/apps/myapp/install`

1. 번들이 `/apps/myapp/src` 들어 있는 폴더를 마우스 오른쪽 단추로 클릭하고 만들기 ... `Test` , **번들 만들기****를 선택합니다.**.

1. 번들 속성을 다음과 같이 설정합니다.

   * 기호 번들 이름: `com.mycompany.test.TestBundle`

   * 번들 이름: `Test Bundle`
   * 번들 설명:

      ```
      This is my Test Bundle
      ```

   * 패키지:

      ```
      com.mycompany.test
      ```
   **확인**&#x200B;을 클릭합니다.

1. 모두 **저장을** 클릭하여 변경 내용을 서버에 저장합니다.

마법사는 다음 요소를 만듭니다.

* It `com.mycompany.test.TestBundle` 유형의 노드는 `nt:folder.` 번들 컨테이너 노드입니다.

* 파일 `com.mycompany.test.TestBundle.bnd`. 번들의 배포 설명자 역할을 하며 일련의 헤더로 구성됩니다.

* 폴더 구조:

   * `src/main/java/com/mycompany/test`. 여기에는 패키지와 Java 클래스가 포함됩니다.

   * `src/main/resources`. 번들 내에서 사용되는 리소스가 포함됩니다.

* 파일 `Activator.java` . 번들 시작 및 중지 이벤트에 대한 알림을 받을 수 있는 선택적 리스너 클래스입니다.

다음 표에는 .bnd 파일의 모든 속성, 해당 값 및 설명이 나와 있습니다.

<table>
 <tbody>
  <tr>
   <td><strong>속성</strong></td>
   <td><strong>값(번들 생성 시)<br /> </strong></td>
   <td><strong>설명</strong></td>
  </tr>
  <tr>
   <td>내보내기 패키지:</td>
   <td><p>*</p> <p>참고:번들의 특성을 반영하려면 이 값을 수정해야 합니다.</p> </td>
   <td>Export-Package 헤더는 번들에서 내보낸 패키지(쉼표로 구분된 패키지 목록)를 정의합니다. 내보낸 패키지는 번들의 공개<br /> 보기를 구성합니다.<br /> </td>
  </tr>
  <tr>
   <td>가져오기 패키지:</td>
   <td><p>*</p> <p>참고:번들의 특성을 반영하려면 이 값을 수정해야 합니다.</p> </td>
   <td>Import-Package 헤더는 번들에 대해 가져온 패키지(쉼표로 구분된 패키지 목록)를 정의합니다.</td>
  </tr>
  <tr>
   <td>비공개 패키지:</td>
   <td><p>*</p> <p>참고:번들의 특성을 반영하려면 이 값을 수정해야 합니다.</p> </td>
   <td>Private-Package 헤더는 번들의 전용 패키지(쉼표로 구분된 패키지 목록)를 정의합니다. 비공개 패키지는 내부 구현을 구성합니다.<br /> </td>
  </tr>
  <tr>
   <td>번들 이름:</td>
   <td>테스트 번들</td>
   <td>번들에 대해 사람이 읽을 수 있는 짧은 이름을 정의합니다.</td>
  </tr>
  <tr>
   <td>번들 설명:</td>
   <td>테스트 번들입니다.</td>
   <td>번들에 대해 사람이 읽을 수 있는 간단한 설명을 정의합니다.</td>
  </tr>
  <tr>
   <td>번들-기호 이름:</td>
   <td>com.mycompany.test.TestBundle</td>
   <td>번들에 대해 지역화할 수 없는 고유한 이름을 지정합니다.</td>
  </tr>
  <tr>
   <td>번들 버전:</td>
   <td>1.0.0-스냅샷</td>
   <td>번들의 버전을 지정합니다</td>
  </tr>
  <tr>
   <td>번들 활성화 툴:</td>
   <td>com.mycompany.test.Activator</td>
   <td>번들 시작 및 중지 이벤트에 대한 알림을 받을 선택적 리스너 클래스의 이름을 지정합니다.</td>
  </tr>
 </tbody>
</table>

두 번째 형식에 대한 자세한 내용은 CRXDE에서 OSGI 번들을 [만드는 데 사용되는 두 번째 유틸리티를](https://bndtools.org/) 참조하십시오.

### Java 클래스 만들기 {#creating-a-java-class}

테스트 번들 내에서 `HelloWorld` Java 클래스를 만들려면:

1. 브라우저에서 CRXDE Lite를 엽니다.
1. 탐색 창에서 `Activator.java` 파일()이 들어 있는 노드를 마우스 오른쪽 단추로 클릭하고 만들기.. `/apps/myapp/src/com.mycompany.test.TestBundle/src/main/java`. ****, **파일만들기...를 선택합니다.**.

1. 파일 이름을 `HelloWorld.java`지정합니다. **확인**&#x200B;을 클릭합니다.

1. 편집 창에서 파일이 `HelloWorld.java` 열립니다.
1. 다음 줄을 `HelloWorld.java`추가합니다.

   ```
     package com.mycompany.test;
   
     public class HelloWorld {
     public String getString(){
     return "Hello World!";
     }
     }
   ```

1. 모두 **저장을** 클릭하여 변경 내용을 서버에 저장합니다.

### 번들 만들기 {#building-a-bundle}

테스트 번들을 빌드하려면

1. 브라우저에서 CRXDE Lite를 엽니다.
1. 탐색 창에서 .bnd 파일을 마우스 오른쪽 단추로 클릭하고 도구, **번들**&#x200B;순으로&#x200B;**선택합니다**.

번들 빌드 마법사:

* Java 클래스를 컴파일합니다.
* 컴파일된 Java 클래스 및 리소스가 포함된 .jar 파일을 만들어 `myapp/install` 폴더에 배치합니다.
* OSGI 컨테이너에 번들을 설치하고 시작합니다.

테스트 번들의 효과를 보려면 Java 메서드 HelloWorld.getString()과 이 구성 요소로 렌더링되는 리소스를 사용하는 구성 요소를 만드십시오.

1. 에서 구성 요소를 `mycomp` 만듭니다 `myapp/components`.

1. 코드를 편집하고 다음 줄로 `mycomp.jsp` 바꿉니다.

   ```
     <%@ page import="com.mycompany.test.HelloWorld"%><%
     %><%@ include file="/libs/foundation/global.jsp"%><%
     %><% HelloWorld hello = new HelloWorld();%><%
     %>
     <html>
     <body>
     <b><%= hello.getString() %></b><br>
     </body>
     </html>
   ```

1. 아래에서 `test_node` 유형의 리소스를 `nt:unstructured` 만듭니다 `/content`.

1. for `test_node`create the following property:이름 = `sling:resourceType`, 유형 = `String`, 값 = `myapp/components/mycomp`입니다.

1. 모두 **저장을** 클릭하여 변경 내용을 서버에 저장합니다.

1. 브라우저에서 요청 `test_node`: `https://<hostname>:<port>/content/test_node.html`Adobe

1. Hello World와 함께 페이지가 **표시됩니다.** message.

## 노드 유형 내보내기 및 가져오기 {#exporting-and-importing-node-types}

CRXDE Lite를 사용하면 CND(Compact Namespace 및 Node Type Definition) [표기법으로](https://jackrabbit.apache.org/jcr/node-type-notation.html)노드 유형 정의를 가져오거나 내보낼 수 있습니다.

노드 유형 정의를 내보내려면

1. 브라우저에서 CRXDE Lite를 엽니다.
1. 필요한 노드를 선택합니다.
1. 도구 **를** 선택한 다음 노드 **유형 내보내기를 선택합니다**.

1. 정의는 브라우저에 표시됩니다. 필요한 경우 정보를 저장합니다.

노드 유형 정의를 가져오려면 다음을 수행하십시오.

1. 브라우저에서 CRXDE Lite를 엽니다.
1. 도구 **를** 선택한 다음 **노드 유형 가져오기...를 선택합니다.**.

1. 텍스트 상자에 정의에 대한 CND 표기법을 입력합니다.
1. 기존 **정의를** 업데이트하는 경우 업데이트 허용을 선택합니다.
1. **가져오기**&#x200B;를 클릭합니다. 

## 로깅 {#logging}

CRXDE Lite를 사용하면 파일 시스템에 `error.log` 있는 파일을 표시하고 적절한 로그 수준으로 필터링할 `<crx-install-dir>/crx-quickstart/server/logs` 수 있습니다. 다음과 같이 진행합니다.

1. 브라우저에서 CRXDE Lite를 엽니다.
1. 창 **하단의 콘솔** 탭에서 오른쪽의 드롭다운 메뉴에서 서버 로그를 **선택합니다**.

1. 중지 **아이콘을** 클릭하여 메시지를 표시합니다.

다음을 작업을 수행할 수 있습니다.

* Felix Console에서 로깅 구성 **아이콘을 클릭하여 로그 매개 변수를** 조정합니다.
* 브러시 아이콘을 클릭하여 메시지를 **지웁니다** .
* [고정] 아이콘을 클릭하여 현재 선택 영역에서 메시지를 **고정할** 수 있습니다.
* 중지 아이콘을 클릭하여 메시지 표시를 활성화 또는 **비활성화합니다** .

## 액세스 제어 {#access-control}

>[!NOTE]
>
>자세한 [내용은 사용자, 그룹 및 액세스 권한](/help/sites-administering/user-group-ac-admin.md) 관리를 참조하십시오.
