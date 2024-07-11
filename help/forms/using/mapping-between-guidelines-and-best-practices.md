---
title: Forms Designer에서 양식을 만들기 위한 지침 및 최상의 액세스 가능성 사례
description: Forms Designer에서 양식을 개발하는 동안의 액세스 가능성에 대한 모범 사례 및 지침입니다.
feature: Adaptive Forms, Forms Designer
solution: Experience Manager, Experience Manager Forms
role: User, Developer
hide: true
hidefromtoc: true
source-git-commit: 38fb132f0eb5b710745db11e7ddf59efc0f0ae95
workflow-type: tm+mt
source-wordcount: '3366'
ht-degree: 1%

---

# 지침과 모범 사례 간 매핑

다음 섹션은 섹션 508 및 WCAG 지침을 이 안내서에 설명된 모범 사례에 매핑합니다.

## § 1194.21 지침 설명 및 우수 사례

### 섹션 508 §1194.21: 소프트웨어 응용 프로그램 및 운영 체제

| § 1194.21 지침 | 지침 설명 | 규정 준수를 위한 필수 LiveCycle Designer 우수 사례 | 메모 |
|-----------|-----------------------|-----------------------------------------------------------|-------|
| 가. | 키보드가 있는 시스템에서 소프트웨어를 구동하도록 설계하는 경우, 기능 자체 또는 기능 수행 결과를 텍스트적으로 식별할 수 있는 키보드에서 제품 기능을 실행할 수 있어야 합니다. | <li> 2.7 양식 컨트롤을 키보드로 액세스할 수 있는지 확인 </li><li> 2.6 읽기 및 탭 순서가 올바른지 확인합니다.</li> | |
| 나. | 애플리케이션은 접근성 기능으로 식별된 다른 제품의 활성화된 기능이 업계 표준에 따라 개발 및 문서화된 경우 이를 중단하거나 비활성화해서는 안 됩니다. 또한 응용 프로그램은 액세스 가능성 기능으로 식별된 운영 체제의 활성화된 기능을 중단하거나 비활성화해서는 안 됩니다. 이러한 액세스 가능성 기능에 대한 응용 프로그램 프로그래밍 인터페이스는 운영 체제의 제조업체에서 문서화했으며 제품 개발자가 사용할 수 있습니다. | Designer 특정 기법 LiveCycle 없음 - 이 지침은 PDF forms을 위해 Adobe Reader에서 처리됩니다. | |
| 다. | 입력 포커스가 변화함에 따라 대화형 인터페이스 요소들 사이에서 이동하는 현재 포커스의 잘 정의된 온-스크린 표시가 제공되어야 한다. 초점은 보조 기술이 초점과 초점 변화를 추적할 수 있도록 프로그래밍 방식으로 노출되어야 한다. | 2.3 올바른 컨트롤을 선택합니다. 포커스가 프로그래밍 방식뿐만 아니라 시각적으로 표시되도록 하려면 항상 표준 컨트롤을 사용하십시오. | |
| 라. | 요소의 신원, 동작 및 상태를 포함하는 사용자 인터페이스 요소에 대한 충분한 정보는 보조 기술에서 이용 가능해야 한다. 이미지가 프로그램 요소를 나타내는 경우 이미지에 의해 전달된 정보를 텍스트로도 사용할 수 있어야 합니다. | <ul><li>2.1 양식을 단순하고 사용하기 쉽게 유지</li> <li>2.1.1 컨텐츠 이동, 깜박임 또는 깜박임 방지</li> <li>2.2 접근성 정보를 생성하도록 양식 속성 구성</li> <li>2.5 양식 컨트롤에 적절한 레이블 제공</li></ul> | |
| 마. | 비트맵 이미지를 사용하여 컨트롤, 상태 표시기 또는 기타 프로그래밍 요소를 식별하는 경우 해당 이미지에 할당된 의미는 응용 프로그램의 성능 전체에서 일관되어야 합니다. | <ul><li>2.4 이미지에 상응하는 텍스트 제공</li><li> 2.5 양식 컨트롤에 적절한 레이블 제공 이 표준은 양식의 여러 위치에서 동일한 이미지를 사용하는 경우에만 적용됩니다. 이미지 기반 사용자 지정 컨트롤은 사용하지 않는 것이 좋습니다. 대신 LiveCycle Designer에서 제공하는 표준 컨트롤만 사용하십시오. 컨트롤에 이미지를 사용하는 경우 항상 일관되게 사용되는지 확인하십시오.</li> | |
| 바. | 문자정보는 문자표시를 위한 운영체제 기능을 통해 제공하여야 한다. 사용할 수 있는 최소 정보는 텍스트 컨텐츠, 텍스트 입력 캐럿 위치 및 텍스트 속성입니다. | 2.3 올바른 컨트롤을 선택합니다. 텍스트 정보를 전달하기 위해 이미지를 사용하지 마십시오. 텍스트 속성을 운영 체제에 제대로 노출하지 않을 수 있는 사용자 지정 입력 구성 요소를 사용하는 대신 항상 표준 컨트롤을 사용하십시오. | |
| 사. | 응용 프로그램은 사용자가 선택한 대비와 색상 선택 및 기타 개별 표시 속성을 재정의해서는 안 됩니다. | Designer 특정 기법 LiveCycle 없음 | 가능하면 기본 시스템 색상을 사용합니다. |
| 아. | 애니메이션을 표시할 경우에는 사용자의 선택에 따라 하나 이상의 비애니메이션 프레젠테이션 모드로 정보를 표시할 수 있다. | 2.1 양식을 간단하고 쉽게 사용할 수 있도록 유지 양식에 애니메이션을 사용하지 않거나 애니메이션이 정적 이미지로 대체되는 별도의 버전을 제공합니다. | |
| (i) | 색상 코딩은 정보를 전달하거나, 동작을 나타내거나, 반응을 나타내거나, 시각적 요소를 구별하는 유일한 수단으로 사용되어서는 안 된다. | 2.8 색상 사용 책임 | |
| 차. | 제품이 사용자가 색상 및 대비 설정을 조정할 수 있도록 할 때, 다양한 대비 수준을 생성할 수 있는 다양한 색상 선택이 제공되어야 한다. | 해당되지 않음 | 이 기능은 일반적으로 양식 개발자가 아닌 Adobe Reader에서 제공합니다. |
| 카. | 소프트웨어는 깜박이거나 깜박이는 텍스트, 개체 또는 2Hz보다 크고 55Hz보다 작은 플래시 또는 깜박임 주파수를 갖는 기타 요소를 사용하지 않습니다. | 2.1.1 컨텐츠 이동, 깜박임 또는 깜박임 방지 | |
| 타. | 전자서식을 사용할 때는 양식에서 보조공학기술을 사용하는 사람들이 전방위적, 큐를 포함하여 양식을 작성·제출하는데 필요한 정보·현장요소 및 기능성에 접근할 수 있도록 하여야 한다. | 2.5 양식 컨트롤에 적절한 레이블 제공 | |

### 섹션 508 §11942: 웹 기반 인트라넷 및 인터넷 정보 및 응용 프로그램

| §11942 지침 | 지침 설명 | 규정 준수를 위한 필수 LiveCycle Designer 우수 사례 | 메모 |
|-----------|-----------------------|-----------------------------------------------------------|-------|
| 가. | 텍스트가 아닌 모든 요소에 해당하는 텍스트가 제공됩니다(예: &quot;alt&quot;, &quot;longdesc&quot;를 통해 또는 요소 콘텐츠에서). | 2.4 이미지에 상응하는 텍스트 제공 | |
| 나. | 모든 멀티미디어 프레젠테이션에 대해 동등한 대안은 프레젠테이션과 동기화되어야 합니다. | 2.12 모든 멀티미디어 콘텐츠에 액세스할 수 있는지 확인합니다. | |
| 다. | 웹 페이지는 예를 들어 컨텍스트나 마크업에서 색상을 사용하여 전달되는 모든 정보도 색상 없이 사용할 수 있도록 디자인되어야 합니다. | 2.8 색상 사용 책임 | |
| 라. | 문서는 연계된 스타일시트를 필요로 하지 않고 읽을 수 있도록 구성되어야 한다. | 해당되지 않음 | |
| 마. | 서버측 이미지 맵의 활성 영역 별로 중복 텍스트 링크가 제공됩니다. | 해당되지 않음 | |
| 바. | 사용 가능한 기하학적 형상으로 영역을 정의할 수 없는 경우를 제외하고 서버측 이미지 맵 대신 클라이언트측 이미지 맵이 제공되어야 합니다. | 해당되지 않음 | |
| 사. | 데이터 테이블에 대해 행 및 열 머리글을 식별해야 합니다. | 2.9 표용 머리글 셀 제공 | |
| 아. | 마크업은 행 또는 열 머리글의 논리적 레벨이 두 개 이상인 데이터 테이블에 대한 데이터 셀과 머리글 셀을 연결하는 데 사용됩니다. | 2.9 표용 머리글 셀 제공 | |
| (i) | 프레임은 프레임 식별 및 탐색을 용이하게 하는 텍스트로 제목을 지정해야 합니다. | 해당되지 않음 | |
| 차. | 페이지는 2Hz보다 크고 55Hz보다 낮은 주파수로 화면이 깜박거리는 것을 방지하도록 설계되어야 한다. | 2.1 양식을 단순하고 사용하기 쉽게 유지 | |
| 카. | 웹 사이트가 다른 방법으로 규정을 준수할 수 없을 때 이 부분의 규정을 준수하도록 동등한 정보 또는 기능이 포함된 텍스트 전용 페이지가 제공됩니다. 텍스트 전용 페이지의 콘텐츠는 기본 페이지가 변경될 때마다 업데이트됩니다. | 해당되지 않음 | |
| 타. | 페이지가 콘텐츠를 표시하거나 인터페이스 요소를 만들기 위해 스크립팅 언어를 사용할 때 스크립트에서 제공하는 정보는 보조 기술로 읽을 수 있는 기능 텍스트로 식별되어야 합니다. | 2.11 스크립팅 중단 방지 | |
| 파. | 웹 페이지에서 페이지 콘텐츠를 해석하기 위해 클라이언트 시스템에 애플릿, 플러그인 또는 기타 응용 프로그램이 있어야 하는 경우 페이지는 §1194.21(a)에서 (l)까지 호환되는 플러그인 또는 애플릿에 대한 링크를 제공해야 합니다. | 해당되지 않음 | PDF forms에 연결하는 웹 페이지는 Adobe Reader에 대한 링크를 제공해야 합니다. |
| (n) | 전자서식이 온라인상에서 완성되도록 설계된 때에는 서식은 전방위적, 큐를 비롯하여 서식의 완성·제출에 필요한 정보·현장요소 및 기능성에 보조공학기술을 이용한 사람이 접근할 수 있도록 하여야 한다. | 2.5 양식 컨트롤에 적절한 레이블 제공 | |
| (o) | 사용자가 반복 내비게이션 링크를 건너뛸 수 있도록 하는 방법을 제공하여야 한다. | 2.10 탐색 가능한 양식 구조 제공 | |
| (p) | 시간이 지정된 응답이 필요한 경우 사용자에게 알림을 보내고 더 많은 시간이 필요함을 나타낼 수 있는 충분한 시간이 주어집니다. | 2.11 스크립팅 중단 방지 | |

### WCAG 1.0 우선 순위 1 체크포인트

| 체크포인트 | 체크포인트 설명 | 규정 준수를 위한 필수 LiveCycle Designer 우수 사례 | 메모 |
|------------|------------------------|-----------------------------------------------------------|-------|
| [1.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-text-equivalent) | 텍스트가 아닌 모든 요소에 해당하는 텍스트를 입력합니다(예: &quot;alt&quot;, &quot;longdesc&quot; 또는 요소 컨텐츠 참조). 여기에는 이미지, 텍스트 그래픽 표현(심볼 포함), 이미지 맵 영역, 애니메이션(예: 애니메이션 GIF), 애플릿 및 프로그래밍 방식 객체, ASCII art, 프레임, 스크립트, 목록 글머리 기호로 사용되는 이미지, 스페이서, 그래픽 단추, 사운드(사용자 상호 작용과 함께 또는 사용자 상호 작용 없이 재생됨), 독립형 오디오 파일, 비디오의 오디오 트랙 및 비디오가 포함됩니다. | <ul><li>2.4 이미지에 상응하는 텍스트 제공</li> <li>2.12 모든 멀티미디어 콘텐츠에 액세스할 수 있는지 확인합니다.</li> | |
| [1.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-redundant-server-links) | 서버측 이미지 맵의 각 활성 영역에 대해 중복 텍스트 링크를 제공합니다. | 해당되지 않음 | |
| [1.3](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-auditory-descriptions) | 사용자 에이전트가 시각적 트랙에 해당하는 텍스트를 자동으로 읽을 수 있을 때까지 멀티미디어 프레젠테이션의 시각적 트랙에 대한 중요한 정보에 대한 청각적 설명을 제공합니다. | 2.12 모든 멀티미디어 콘텐츠에 액세스할 수 있는지 확인합니다. | |
| [1.4](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-synchronize-equivalents) | 시간 기반 멀티미디어 프레젠테이션(예: 동영상 또는 애니메이션)의 경우, 동등한 대체 요소(예: 시각적 트랙의 캡션 또는 청각 설명)를 프레젠테이션과 동기화합니다. | 2.12 모든 멀티미디어 콘텐츠에 액세스할 수 있는지 확인합니다. | |
| [2.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-color-convey) | 색상을 사용하여 전달되는 모든 정보도 컨텍스트 또는 마크업과 같이 색상 없이 사용할 수 있어야 합니다. | 2.8 색상 사용 책임 | |
| [4.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-identify-changes) | 문서 텍스트의 자연어 변경 내용과 이에 상응하는 텍스트(예: 캡션)를 명확하게 식별합니다. | 2.13 언어 변경 사항 확인 | |
| [5.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-table-headers) | 데이터 테이블의 경우 행 및 열 헤더를 식별합니다. | 2.9 표용 머리글 셀 제공 | |
| [5.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-table-structure) | 행 또는 열 머리글의 논리적 수준이 두 개 이상인 데이터 표의 경우 마크업을 사용하여 데이터 셀과 머리글 셀을 연결합니다. | 2.9 표용 머리글 셀 제공 | |
| [6.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-order-style-sheets) | 스타일시트 없이 읽을 수 있도록 문서를 구성합니다. 예를 들어, HTML 문서가 연관된 스타일 시트 없이 렌더링되는 경우에도 문서를 읽을 수 있어야 합니다. | 해당되지 않음 | |
| [6.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-dynamic-source) | 다이내믹 컨텐츠가 변경될 때 다이내믹 컨텐츠에 해당하는 항목이 업데이트되도록 하십시오. | 2.11 스크립팅 중단 방지 | |
| [6.3](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-scripts) | 스크립트, 애플릿 또는 기타 프로그래밍 방식 객체가 꺼져 있거나 지원되지 않을 때 페이지를 사용할 수 있는지 확인합니다. 불가능한 경우 액세스 가능한 대체 페이지에 동일한 정보를 제공합니다. | 2.11 스크립팅 중단 방지 | |
| [7.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-avoid-flicker) | 사용자 에이전트에서 사용자가 깜박임을 제어할 수 있을 때까지 화면이 깜박이는 것을 방지하십시오. | 2.1 양식을 단순하고 사용하기 쉽게 유지 | |
| [9.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-client-side-maps) | 사용 가능한 기하학적 형상으로 영역을 정의할 수 없는 경우를 제외하고 서버측 이미지 맵 대신 클라이언트측 이미지 맵을 제공합니다. | 해당되지 않음 | |
| [11.4](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-alt-pages) | 최상의 노력을 기울였으나 액세스 가능한 페이지를 만들 수 없는 경우 W3C 기술을 사용하고, 액세스할 수 있고, 동등한 정보(또는 기능)를 가지고 있고, 액세스할 수 없는(원래) 페이지만큼 자주 업데이트되는 대체 페이지에 대한 링크를 제공합니다. | 해당되지 않음 | |
| [12.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-frame-titles) | 프레임 식별 및 탐색이 용이하도록 각 프레임의 제목을 지정합니다. | 해당되지 않음 | |
| [14.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-simple-and-straightforward) | 사이트 콘텐츠에 적합한 가장 명확하고 간단한 언어를 사용합니다. | 2.1 양식을 단순하고 사용하기 쉽게 유지 | |

### WCAG 1.0 우선 순위 2 체크포인트

| 우선 순위 2 체크포인트 | 체크포인트 설명 | 규정 준수를 위한 필수 LiveCycle 모범 사례 | 메모 |
|------------|------------------------|-------------------------------------------------|-------|
| [2.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-color-contrast) | 전경색과 배경색 조합을 사용하여 색상이 부족한 사용자가 보거나 흑백 화면에서 볼 때 충분한 대비를 제공하는지 확인하십시오. [이미지의 우선 순위 2, 텍스트의 우선 순위 3]. | 2.8 색상 사용 책임 | |
| [3.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-use-markup) | 적절한 마크업 언어가 있는 경우 정보를 전달하기 위해 이미지가 아닌 마크업을 사용합니다. | <ul><li>2.1 양식을 단순하고 사용하기 쉽게 유지</li><li> 2.1.1 컨텐츠 이동, 깜박임 또는 깜박임 방지</li> <li>2.2 접근성 정보를 생성하도록 양식 속성 구성 텍스트 이미지 대신 항상 실제 텍스트를 사용합니다.</li> | |
| [3.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-identify-grammar) | 게시된 형식 문법에 대해 유효성을 검사하는 문서를 만듭니다. | | PDF forms을 Adobe Reader에서 렌더링하려면 게시된 PDF 사양과 일치해야 합니다. |
| [3.3](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-style-sheets) | 스타일 시트를 사용하여 레이아웃 및 프레젠테이션을 제어합니다. | 해당되지 않음 | |
| [3.4](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-relative-units) | 마크업 언어 속성 값 및 스타일 시트 속성 값에 절대 단위가 아닌 상대 단위를 사용합니다. | 해당되지 않음 | |
| [3.5](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-logical-headings) | 머리글 요소를 사용하여 문서 구조를 전달하고 사양에 따라 사용합니다. | 2.10 탐색 가능한 양식 구조 제공 | |
| [3.6](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-list-structure) | 목록 및 목록 항목을 올바르게 표시합니다. | 2.10.3 목록 표시 목록 및 목록 항목 역할을 사용하여 목록 기반 콘텐츠를 목록으로 표시합니다. | |
| [3.7](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-quotes) | 견적에 표시를 하라. 들여쓰기와 같은 서식 효과에 따옴표를 사용하지 마십시오. | 해당되지 않음 | |
| [5.3](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-avoid-table-for-layout) | 선형화할 때 표를 이해할 수 없는 경우 레이아웃에 표를 사용하지 마십시오. 그렇지 않으면 표가 적절하지 않은 경우 그에 해당하는 대체 버전(선형화된 버전일 수 있음)을 제공하십시오. | 특정 LiveCycle 기법 없음 | LiveCycle 양식의 레이아웃에 표를 사용할 이유가 없습니다. 대신 레이아웃 팔레트를 사용하여 양식 필드를 그리드 패턴으로 배치합니다. 표 머리글과 같은 표별 기능을 사용할 때는 표만 사용하십시오. |
| [5.4](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-table-layout) | 레이아웃에 표를 사용하는 경우 시각적 서식 지정을 위해 구조적 마크업을 사용하지 마십시오. | 특정 LiveCycle 기법 없음 | |
| [6.4](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-keyboard-operable-scripts) | 스크립트 및 애플릿의 경우 이벤트 처리기가 입력 장치에 독립적인지 확인합니다. | 2.7 양식 컨트롤을 키보드로 액세스할 수 있는지 확인 | |
| [6.5](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-fallback-page) | 동적 콘텐츠에 액세스할 수 있는지 확인하거나 대체 프레젠테이션 또는 페이지를 제공합니다. | 2.11 스크립팅 중단 방지 | |
| [7.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-avoid-blinking) | 사용자 에이전트가 사용자가 깜박임을 제어할 수 있을 때까지 컨텐츠가 깜박이는 것을 방지합니다(즉, 켜기 및 끄기와 같이 일정한 비율로 프레젠테이션을 변경하는 것). | 2.1 양식을 단순하고 사용하기 쉽게 유지 | |
| [7.3](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-avoid-movement) | 사용자 에이전트가 사용자가 이동하는 콘텐츠를 동결할 수 있을 때까지 페이지에서 이동을 피하십시오. | 2.1 양식을 단순하고 사용하기 쉽게 유지 | |
| [7.4](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-no-periodic-refresh) | 사용자 에이전트가 새로 고침을 중지하는 기능을 제공할 때까지 주기적으로 자동 새로 고침 페이지를 만들지 마십시오. | 해당되지 않음 | |
| [7.5](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-no-auto-forward) | 사용자 에이전트가 자동 리디렉션을 중지하는 기능을 제공할 때까지 태그를 사용하여 페이지를 자동으로 리디렉션하지 마십시오. 대신 리디렉션을 수행하도록 서버를 구성합니다. | 해당되지 않음 | |
| [8.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-directly-accessible) | 스크립트 및 애플릿과 같은 프로그래밍 요소를 보조 기술과 직접 액세스하거나 호환할 수 있습니다 [기능이 중요하고 다른 곳에 제시되지 않은 경우 우선 순위 1, 그렇지 않은 경우 우선 순위 2.] | 2.11 스크립팅 중단 방지 | |
| [9.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-keyboard-operable) | 자체 인터페이스가 있는 모든 요소를 장치 독립적인 방식으로 작동할 수 있습니다. | 2.7 양식 컨트롤을 키보드로 액세스할 수 있는지 확인 | |
| [9.3](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-device-independent-events) | 스크립트의 경우 장치 종속 이벤트 핸들러가 아닌 논리 이벤트 핸들러를 지정합니다. | 2.7 양식 컨트롤을 키보드로 액세스할 수 있는지 확인 | |
| [10.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-avoid-pop-ups) | 사용자 에이전트가 사용자가 생성된 창을 끌 때까지 팝업 또는 다른 창이 나타나지 않도록 하고 사용자에게 알리지 않고 현재 창을 변경하지 마십시오. | 2.11 스크립팅 중단 방지 | |
| [10.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-unassociated-labels) | 사용자 에이전트가 레이블과 양식 컨트롤 간의 명시적 연결을 지원할 때까지 암시적으로 연결된 레이블이 있는 모든 양식 컨트롤에 대해 레이블이 올바르게 배치되었는지 확인합니다. | 2.5 양식 컨트롤에 적절한 레이블 제공 | |
| [11.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-latest-w3c-specs) | 작업에 사용 가능하고 적합한 W3C 기술을 사용하고 지원되는 경우 최신 버전을 사용하십시오. | 해당되지 않음 | |
| [11.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-avoid-deprecated) | 더 이상 사용되지 않는 W3C 기술 기능을 사용하지 마십시오. | 해당되지 않음 | |
| [12.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-frame-longdesc) | 프레임 제목만으로 명확하지 않은 경우 프레임의 목적과 프레임이 서로 관련되는 방식을 설명합니다. | 해당되지 않음 | |
| [12.3](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-group-information) | 정보의 큰 블록을 자연스럽고 적절한 관리가능한 그룹으로 나눕니다. | 2.10 탐색 가능한 양식 구조 제공 | |
| [12.4](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-associate-labels) | 레이블을 해당 컨트롤과 명시적으로 연결합니다. | 2.5 양식 컨트롤에 적절한 레이블 제공 | |
| [13.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-meaningful-links) | 각 링크의 대상을 명확히 식별합니다. | 2.5 양식 컨트롤에 적절한 레이블 제공 2.5.6 링크 텍스트 제공 | |
| [13.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-use-metadata) | 페이지 및 사이트에 의미 체계 정보를 추가하는 메타데이터를 제공합니다. | 해당되지 않음 | |
| [13.3](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-site-description) | 사이트의 일반 레이아웃에 대한 정보(예: 사이트 맵 또는 목차)를 제공합니다. | 2.10 탐색 가능한 양식 구조 제공 | |
| [13.4](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-clear-nav-mechanism) | 일관된 방식으로 탐색 메커니즘을 사용합니다. | 2.10 탐색 가능한 양식 구조 제공 | 마스터 페이지를 사용하여 일관된 탐색 콘텐츠를 만듭니다. |

### WCAG 2.0 성공 기준

| 우선 순위 1 G 2 체크포인트 | 규정 준수를 위한 필수 LiveCycle 모범 사례 | 메모 |
| --- | --- | --- |
| 1.1 [텍스트 대체 요소](https://www.w3.org/TR/UNDERSTANDING-WCAG20/text-equiv.html) | | |
| 1.1.1 [텍스트가 아닌 콘텐츠](https://www.w3.org/TR/UNDERSTANDING-WCAG20/text-equiv-all.html) | 2.4 이미지에 상응하는 텍스트 제공 | |
| | 2.5 양식 컨트롤에 적절한 레이블 제공 | |
| 1.2 [시간 기반 미디어](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv.html) | | |
| 1.2.1 [오디오 전용 및 비디오 전용(사전 녹화된)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-av-only-alt.html) | 2.12 모든 오디오 및 비디오 콘텐츠에 액세스할 수 있는지 확인합니다. | |
| 1.2.2 [캡션(사전 기록된)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-captions.html) | 2.12 모든 오디오 및 비디오 콘텐츠에 액세스할 수 있는지 확인합니다. | |
| 1.2.3 [오디오 설명 또는 미디어 대체 요소(사전 녹음된)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-audio-desc.html) | 2.12 모든 오디오 및 비디오 콘텐츠에 액세스할 수 있는지 확인합니다. | |
| 1.2.4 [캡션(라이브)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-real-time-captions.html) | 2.12 모든 오디오 및 비디오 콘텐츠에 액세스할 수 있는지 확인합니다. | |
| 1.2.5 [오디오 설명(사전 녹음된)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-audio-desc-only.html) | 2.12 모든 오디오 및 비디오 콘텐츠에 액세스할 수 있는지 확인합니다. | |
| 1.2.6 [수화(사전 녹음된)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-sign.html) | 2.12 모든 오디오 및 비디오 콘텐츠에 액세스할 수 있는지 확인합니다. | |
| 1.2.7 [확장 오디오 설명(사전 기록됨)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-extended-ad.html) | 2.12 모든 오디오 및 비디오 콘텐츠에 액세스할 수 있는지 확인합니다. | |
| 1.2.8 [미디어 대체 요소(사전 녹음된)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-text-doc.html) | 2.12 모든 오디오 및 비디오 콘텐츠에 액세스할 수 있는지 확인합니다. | |
| 1.2.9 [오디오 전용(라이브)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-live-audio-only.html) | 2.12 모든 오디오 및 비디오 콘텐츠에 액세스할 수 있는지 확인합니다. | |
| 1.3 [적응성](https://www.w3.org/TR/UNDERSTANDING-WCAG20/content-structure-separation.html) | | |
| 1.3.1 [정보 및 관계](https://www.w3.org/TR/UNDERSTANDING-WCAG20/content-structure-separation-programmatic.html) | 2.9 표용 머리글 셀 제공 | |
| 1.3.2 [의미 있는 시퀀스](https://www.w3.org/TR/UNDERSTANDING-WCAG20/content-structure-separation-sequence.html) | 2.6 읽기 및 탭 순서가 올바른지 확인합니다. | |
| | 2.10 탐색 가능한 양식 구조 제공 | |
| 1.3.3 [감각 특성](https://www.w3.org/TR/UNDERSTANDING-WCAG20/content-structure-separation-understanding.html) | 2.8 색상 사용 책임 | |
| 1.4 [구별 가능하](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast.html) | | |
| 1.4.1 [색상 사용](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-without-color.html) | 2.8 색상 사용 책임 | |
| 1.4.2 [오디오 제어](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-dis-audio.html) | 특정 LiveCycle 기법 없음 | |
| 1.4.3 [대비(최소)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-contrast.html) | 2.8 색상 사용 책임 | |
| 1.4.4 [텍스트 크기 조정](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-scale.html) | 특정 LiveCycle 기법 없음 | |
| 1.4.5 [텍스트 이미지](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-text-presentation.html) | 특정 LiveCycle 기법 없음 | |
| 1.4.6 [대비(향상)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast7.html) | 2.8 색상 사용 책임 | |
| 1.4.7 [배경 오디오 낮음 또는 없음](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-noaudio.html) | 특정 LiveCycle 기법 없음 | |
| 1.4.9 [텍스트 이미지(예외 없음)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-text-images.html) | 특정 LiveCycle 기법 없음 | |
| 2.1 [키보드 액세스 가능](https://www.w3.org/TR/UNDERSTANDING-WCAG20/keyboard-operation.html) | | |
| 2.1.1 [키보드](https://www.w3.org/TR/UNDERSTANDING-WCAG20/keyboard-operation-keyboard-operable.html) | 2.6 읽기 및 탭 순서가 올바른지 확인합니다. | |
| | 2.7 양식 컨트롤을 키보드로 액세스할 수 있는지 확인 | |
| 2.1.2 [키보드 트랩 없음](https://www.w3.org/TR/UNDERSTANDING-WCAG20/keyboard-operation-trapping.html) | 2.7 양식 컨트롤을 키보드로 액세스할 수 있는지 확인 | |
| 2.1.3 [키보드(예외 없음)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/keyboard-operation-all-funcs.html) | 2.6 읽기 및 탭 순서가 올바른지 확인합니다. | |
| | 2.7 양식 컨트롤을 키보드로 액세스할 수 있는지 확인 | |
| 2.2 [충분한 시간](https://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits.html) | | |
| 2.2.1 [시간 조정 가능](https://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits-required-behaviors.html) | 특정 LiveCycle 기법 없음 | |
| 2.2.2 [일시 중단, 중지, 숨기기](https://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits-pause.html) | 2.1 양식을 단순하고 사용하기 쉽게 유지 | |
| 2.2.3 [시간 없음](https://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits-no-exceptions.html) | 특정 LiveCycle 기법 없음 | |
| 2.2.4 [중단](https://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits-postponed.html) | 특정 LiveCycle 기법 없음 | |
| 2.2.5 [재인증](https://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits-server-timeout.html) | 특정 LiveCycle 기법 없음 | |
| 2.3 [발작] | | |
| 2.3.1 [3개 Flash 또는 임계값 미만](https://www.w3.org/TR/UNDERSTANDING-WCAG20/seizure-does-not-violate.html) | 2.1 양식을 단순하고 사용하기 쉽게 유지 | |
| 2.3.2 [3개의 Flash](https://www.w3.org/TR/UNDERSTANDING-WCAG20/seizure-three-times.html) | 2.1 양식을 단순하고 사용하기 쉽게 유지 | |
| 2.4 [탐색 가능](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms.html) | | |
| 2.4.1 [블록 우회](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-skip.html) | 2.10 탐색 가능한 양식 구조 제공 | |
| 2.4.2 [제목이 있는 페이지](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-title.html) | 특정 LiveCycle 기법 없음 | |
| 2.4.3 [포커스 순서](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-focus-order.html) | 2.6 읽기 및 탭 순서가 올바른지 확인합니다. | |
| 2.4.4 [링크 목적(컨텍스트 내)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-refs.html) | 특정 LiveCycle 기법 없음 | 링크 목적은 작성자가 연결된 요소에 대해 의미 있는 텍스트를 선택하는 데 따라 다릅니다. |
| 2.4.5 [다양한 방법](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-mult-loc.html) | 2.10 탐색 가능한 양식 구조 제공 | |
| 2.4.6 [제목 및 레이블](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-descriptive.html) | <ul><li>2.5 양식 컨트롤에 적절한 레이블 제공</li><li>2.10 탐색 가능한 양식 구조 제공</li> | |
| 2.4.7 [포커스 표시](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-focus-visible.html) | 특정 LiveCycle 기법 없음 | LiveCycle 양식의 기본 포커스가 표시됩니다. |
| 2.4.8 [위치](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-location.html) | 특정 LiveCycle 기법 없음 | 해당 사항 없음: LiveCycle 양식에는 탐색 시스템이 필요하지 않습니다. |
| 2.4.9 [링크 목적(링크만)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-link.html) | 특정 LiveCycle 기법 없음 | 링크 목적은 작성자가 연결된 요소에 대해 의미 있는 텍스트를 선택하는 데 따라 다릅니다. |
| 2.4.10 [섹션 제목](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-headings.html) | 2.10 탐색 가능한 양식 구조 제공 | |
| 3.1 [읽기 가능](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning.html) | | |
| 3.1.1 [페이지 언어](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-doc-lang-id.html) | 2.13 자연어 및 언어의 모든 변경 사항 식별 | |
| 3.1.2 [부분 언어](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-other-lang-id.html) | 2.13 자연어 및 언어의 모든 변경 사항 식별 | |
| 3.1.3 [특이한 단어](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-idioms.html) | 특정 LiveCycle 기법 없음 | |
| 3.1.4 [약자](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-located.html) | 특정 LiveCycle 기법 없음 | |
| 3.1.5 [읽기 수준](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-supplements.html) | 특정 LiveCycle 기법 없음 | |
| 3.1.6 [발음](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-pronunciation.html) | 특정 LiveCycle 기법 없음 | |
| 3.2 [예측 가능](https://www.w3.org/TR/UNDERSTANDING-WCAG20/consistent-behavior.html) | | |
| 3.2.1 [포커스 맞춤](https://www.w3.org/TR/UNDERSTANDING-WCAG20/consistent-behavior-receive-focus.html) | 2.11 스크립팅 중단 방지 | |
| 3.2.2 [입력 시](https://www.w3.org/TR/UNDERSTANDING-WCAG20/consistent-behavior-unpredictable-change.html) | 2.11 스크립팅 중단 방지 | |
| 3.2.3 [일관된 탐색](https://www.w3.org/TR/UNDERSTANDING-WCAG20/consistent-behavior-consistent-locations.html) | 2.10 탐색 가능한 양식 구조 제공 | |
| 3.2.4 [일관된 식별](https://www.w3.org/TR/UNDERSTANDING-WCAG20/consistent-behavior-consistent-functionality.html) | <ul><li>2.3 적합한 제어 선택</li><li>2.5 양식 컨트롤에 적절한 레이블 제공</li> | |
| 3.2.5 [요청 시 변경](https://www.w3.org/TR/UNDERSTANDING-WCAG20/consistent-behavior-no-extreme-changes-context.html) | 2.11 스크립팅 중단 방지 | |
| 3.3 [입력 지원](https://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error.html) | | |
| 3.3.1 [오류 식별](https://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error-identified.html) |  | LiveCycle Designer은 양식 필드를 필수 항목으로 표시하고 양식 입력 유효성 검사를 수행하는 도구를 제공합니다. |
| 3.3.2 [레이블 또는 지침](https://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error-cues.html) | 2.5 양식 컨트롤에 적절한 레이블 제공 | |
| 3.3.3 [오류 제안](https://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error-suggestions.html) |  | LiveCycle Designer은 양식 필드를 필수 항목으로 표시하고 양식 입력 유효성 검사를 수행하는 도구를 제공합니다. |
| 3.3.4 [오류 방지(법적, 재무, 데이터)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error-reversible.html) | 특정 LiveCycle 기법 없음 | |
| 3.3.5 [도움말](https://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error-context-help.html) | 특정 LiveCycle 기법 없음 | |
| 3.3.6 [오류 방지(모두)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error-reversible-all.html) | 특정 LiveCycle 기법 없음 | |
| 4.1 [호환 가능](https://www.w3.org/TR/UNDERSTANDING-WCAG20/ensure-compat.html) | | |
| 4.1.1 [구문 분석](https://www.w3.org/TR/UNDERSTANDING-WCAG20/ensure-compat-parses.html) | 특정 LiveCycle 기법 없음 | |
| 4.1.2 [이름, 역할, 값](https://www.w3.org/TR/UNDERSTANDING-WCAG20/ensure-compat-rsv.html) | <ul><li>2.3 적합한 제어 선택</li> <li>2.5 양식 컨트롤에 적절한 레이블 제공</li> | |



