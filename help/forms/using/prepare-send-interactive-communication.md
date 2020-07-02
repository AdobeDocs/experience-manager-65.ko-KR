---
title: 에이전트 UI를 사용하여 대화형 통신 준비 및 보내기
seo-title: 에이전트 UI를 사용하여 대화형 통신 준비 및 보내기
description: 에이전트 UI를 사용하면 에이전트가 인터랙티브 커뮤니케이션을 준비하고 사후 프로세스로 전송할 수 있습니다. 에이전트는 허용된 대로 필요한 수정 사항을 수행하고 이메일 또는 인쇄와 같은 대화형 통신을 게시물 프로세스로 제출합니다.
seo-description: 에이전트 UI를 사용하여 대화형 통신 준비 및 보내기
uuid: d1a19b83-f630-4648-9ad2-a22374e31aa9
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 110c86ea-9bd8-4018-bfcc-ca33e6b3f3ba
translation-type: tm+mt
source-git-commit: 4c4a5a15e9cbb5cc22bc5999fb40f1d6db3bb091
workflow-type: tm+mt
source-wordcount: '1641'
ht-degree: 2%

---


# 에이전트 UI를 사용하여 대화형 통신 준비 및 보내기 {#prepare-and-send-interactive-communication-using-the-agent-ui}

에이전트 UI를 사용하면 에이전트가 인터랙티브 커뮤니케이션을 준비하고 사후 프로세스로 전송할 수 있습니다. 에이전트는 허용된 대로 필요한 수정 사항을 수행하고 이메일 또는 인쇄와 같은 대화형 통신을 게시물 프로세스로 제출합니다.

## 개요 {#overview}

대화형 통신이 만들어지면, 에이전트는 에이전트 UI에서 대화형 통신을 열고 데이터를 입력하고 컨텐트 및 첨부 파일을 관리하여 수신자별 사본을 준비할 수 있습니다. 마지막으로, 에이전트는 대화형 통신을 게시물 프로세스에 제출할 수 있습니다.

에이전트 UI를 사용하여 대화형 통신을 준비하는 동안 에이전트는 에이전트 UI에서 대화형 커뮤니케이션의 다음 측면을 관리한 후 게시물 프로세스에 제출합니다.

* **데이터**: 에이전트 UI의 [데이터] 탭은 임의의 에이전트 편집 가능한 변수와 잠금 해제된 양식 데이터 모델 속성을 대화형 통신에 표시합니다. 이러한 변수/속성은 대화형 통신에 포함된 문서 조각을 편집하거나 만드는 동안 만들어집니다. 데이터 탭에는 XDP/인쇄 채널 템플릿에 내장된 모든 필드도 포함되어 있습니다. [데이터] 탭은 에이전트가 편집할 수 있는 대화형 통신에 변수, 양식 데이터 모델 속성 또는 필드가 있을 때만 나타납니다.
* **컨텐츠**: [콘텐트] 탭에서 에이전트는 대화형 통신에서 문서 조각 및 컨텐츠 변수와 같은 내용을 관리합니다. 에이전트는 문서 조각 속성에서 대화형 통신을 생성하는 동안 허용된 대로 문서 조각에서 변경을 수행할 수 있습니다. 또한 에이전트는 문서 조각을 다시 정렬하거나 추가/제거하고 페이지 나누기를 추가할 수 있습니다(허용되는 경우).
* **첨부 파일**: [첨부 파일] 탭은 대화형 통신에 첨부 파일이 있거나 에이전트에 라이브러리 액세스 권한이 있는 경우에만 에이전트 UI에 나타납니다. 에이전트는 첨부 파일을 변경하거나 편집할 수 없거나 허용되지 않을 수 있습니다.

## 에이전트 UI를 사용하여 대화형 통신 준비 {#prepare-interactive-communication-using-the-agent-ui}

1. [ **[!UICONTROL 양식]** ] > [ **[!UICONTROL 양식 및 문서]를 선택합니다]**.
1. 적절한 대화형 통신을 선택하고 [에이전트 **[!UICONTROL UI 열기]를 누릅니다]**.

   >[!NOTE]
   >
   >에이전트 UI는 선택한 대화형 통신에 인쇄 채널이 있는 경우에만 작동합니다.

   ![opentiui](assets/openagentiui.png)

   Interactive Communication의 컨텐츠 및 속성에 따라 다음 세 개의 탭이 있는 에이전트 UI가 나타납니다. 데이터, 컨텐트 및 첨부 파일.

   ![aginuatabs](assets/agentuitabs.png)

   데이터 입력, 컨텐츠 관리 및 첨부 파일 관리로 이동합니다.

### 데이터 입력 {#enter-data}

1. 데이터 탭에서 필요에 따라 변수, 양식 데이터 모델 속성 및 인쇄 템플릿(XDP) 필드에 데이터를 입력합니다. 별표(&amp;ast;)가 표시된 모든 필수 필드를 채워 **제출 단추를** 활성화합니다.

   대화형 통신 미리 보기에서 데이터 필드 값을 눌러 [데이터] 탭에서 해당 데이터 필드를 강조 표시하거나 그 반대의 경우도 마찬가지입니다.

### 컨텐츠 관리 {#manage-content}

컨텐츠 탭에서 대화형 커뮤니케이션의 문서 조각 및 컨텐츠 변수와 같은 컨텐츠를 관리합니다.

1. Select **[!UICONTROL Content]**. [대화형 통신]의 [콘텐트] 탭이 나타납니다.

   ![agentuicontenttab](assets/agentuicontenttab.png)

1. 필요에 따라 컨텐츠 탭에서 문서 조각을 편집합니다. 컨텐츠 계층의 관련 조각에 초점을 맞추려면 Interactive Communication 미리 보기에서 관련 라인 또는 단락을 탭하거나 컨텐츠 계층에서 직접 조각을 탭할 수 있습니다.

   예를 들어, &quot;지금 온라인으로 지불...&quot;이라는 라인이 있는 문서 조각은 아래 그래픽의 미리 보기에서 선택되고 컨텐츠 탭에서 동일한 문서 조각이 선택되었습니다.

   ![contentmodulefocus](assets/contentmodulefocus.png)

   컨텐츠 또는 데이터 탭에서 미리 보기의 왼쪽 상단에 있는 컨텐츠 ![에서 선택한 모듈 하이라이트( highlightselectedmodulesincontentcr](assets/highlightselectedmodulesincontentccr.png))를 탭하여 미리 보기에서 관련 텍스트, 단락 또는 데이터 필드를 탭/선택하면 문서 조각으로 이동할 수 있는 기능을 비활성화하거나 활성화할 수 있습니다.

   대화형 통신을 만드는 동안 에이전트가 편집할 수 있는 조각에는 선택한 컨텐츠 편집( iconedittedcontent ![](assets/iconeditselectedcontent.png)) 아이콘이 있습니다. 선택한 컨텐츠 편집 아이콘을 눌러 편집 모드에서 조각을 실행하고 변경합니다. 텍스트 서식 지정 및 관리에 다음 옵션을 사용합니다.

   * [서식 옵션](#formattingtext)

      * [다른 애플리케이션에서 서식이 지정된 텍스트 복사](#pasteformattedtext)
      * [텍스트 부분 강조 표시](#highlightemphasize)
   * [특수 문자](#specialcharacters)
   * [키보드 단축키](/help/forms/using/keyboard-shortcuts.md)

   에이전트 사용자 인터페이스의 다양한 문서 조각에 사용할 수 있는 작업에 대한 자세한 내용은 [에이전트 사용자 인터페이스에서 사용 가능한 작업 및 정보를 참조하십시오](#actionsagentui).

1. Interactive Communication의 인쇄 출력에 페이지 나누기를 추가하려면 페이지 나누기를 삽입할 위치에 커서를 놓고 Page Break Before 또는 Page Break After( ![pagebreakeparagraph behave)를 선택합니다](assets/pagebreakbeforeafter.png).

   명확한 페이지 나누기 자리 표시자가 대화형 통신에 삽입됩니다. 명확한 페이지 나누기가 대화형 통신에 미치는 영향을 보려면 인쇄 미리 보기를 참조하십시오.

   ![exicitpagebreak](assets/explicitpagebreak.png)

   Interactive Communication의 첨부 파일을 계속 관리합니다.

### 첨부 파일 관리 {#manage-attachments}

1. 첨부 **[!UICONTROL 를 선택합니다]**. 에이전트 UI는 대화형 통신을 생성하는 동안 설정된 대로 사용 가능한 첨부 파일을 표시합니다.

   보기 아이콘을 눌러 Interactive Communication과 함께 첨부를 제출하지 않도록 선택할 수 있으며, 첨부의 십자가를 눌러 Interactive Communication에서 첨부를 삭제(에이전트가 첨부를 삭제하거나 숨길 수 있는 경우)할 수 있습니다. 대화형 통신을 만드는 동안 필수로 지정된 첨부 파일의 경우 보기 및 삭제 아이콘이 비활성화됩니다.

   ![attachmentsagentui](assets/attachmentsagentui.png)

1. 라이브러리 액세스( ![라이브러리 액세스](assets/libraryaccess.png)) 아이콘을 눌러 콘텐트 라이브러리에 액세스하여 DAM 자산을 첨부 파일로 삽입합니다.

   >[!NOTE]
   >
   >라이브러리 액세스 아이콘은 대화형 통신을 만드는 동안 라이브러리 액세스가 활성화된 경우에만 사용할 수 있습니다(인쇄 채널의 문서 컨테이너 속성에 있음).

1. Interactive Communication을 생성하는 동안 첨부 파일의 순서가 잠겨 있지 않은 경우 첨부 파일을 선택하고 아래쪽 및 위쪽 화살표를 눌러 첨부 파일의 순서를 변경할 수 있습니다.
1. 웹 미리 보기 및 인쇄 미리 보기를 사용하여 두 출력이 요구 사항에 따라 해당하는지 확인합니다.

   미리 보기가 만족스러운 경우 **[!UICONTROL 제출을]** 눌러 대화형 통신을 게시물 프로세스로 전송/전송합니다. 또는 변경 사항을 적용하려면 미리 보기를 종료하여 변경 사항으로 돌아갑니다.

## 텍스트 서식 지정 {#formattingtext}

에이전트 UI에서 텍스트 조각을 편집하는 동안 도구 모음은 선택한 편집 유형에 따라 변경됩니다. 글꼴, 단락 또는 목록:

![typeformatingtoolbar](assets/typeofformattingtoolbar.png) 글꼴 ![도구 모음](do-not-localize/fonttoolbar.png)

글꼴 툴바

![단락 도구 모음](do-not-localize/paragraphtoolbar.png)

단락 도구 모음

![목록 도구 모음](do-not-localize/listtoolbar.png)

목록 도구 모음

### 텍스트 부분 강조/강조 {#highlightemphasize}

편집 가능한 조각의 텍스트 부분을 강조 표시하려면 텍스트를 선택하고 강조 색을 누릅니다.

![highlighttextagentui](assets/highlighttextagentui.png)

### 서식이 지정된 텍스트 붙여넣기 {#pasteformattedtext}

![텍스트 붙여넣기](assets/pastedtext.png)

### 텍스트에 특수 문자 삽입 {#specialcharacters}

에이전트 UI는 210개의 특수 문자를 지원합니다. 관리자는 사용자 [지정을 통해 추가/사용자 지정 특수 문자 지원을 추가할 수 있습니다](/help/forms/using/custom-special-characters.md).

#### 첨부 파일 전달 {#attachmentdelivery}

* 서버측 API를 대화형 또는 비대화형 PDF로 사용하여 대화형 통신이 렌더링되면 렌더링된 PDF에 첨부 파일이 PDF 첨부 파일로 포함됩니다.
* 대화형 통신과 연결된 게시 프로세스가 에이전트 UI를 사용하여 제출의 일부로 로드되면 첨부 파일은 List&lt;com.adobe.idp.Document> inAttachmentDocs 매개 변수로 전달됩니다.
* 이메일 및 인쇄와 같은 전달 메커니즘 워크플로우는 PDF 버전의 인터랙티브 커뮤니케이션과 함께 첨부 파일을 전달합니다.

## 에이전트 사용자 인터페이스에서 사용 가능한 작업 및 정보 {#actionsagentui}

### Document fragments {#document-fragments}

![](do-not-localize/contentoptionsdocfragments.png)

* **위쪽/아래쪽 화살표**: 대화형 통신에서 문서 조각을 위나 아래로 이동하는 화살표
* **삭제**: 허용되는 경우 대화형 통신에서 문서 조각을 삭제합니다.
* **이전** 페이지 나누기(대상 영역의 하위 조각에 적용 가능): 문서 조각 앞에 페이지 나누기를 삽입합니다.
* **들여쓰기**: 문서 조각 들여쓰기 또는 축소
* **페이지 나누기 이후** (대상 영역의 하위 조각에 적용 가능): 문서 조각 뒤에 페이지 나누기를 삽입합니다.

![문서 조각 옵션](assets/docfragoptions.png)

* 편집(텍스트 조각만): 텍스트 문서 조각을 편집할 리치 텍스트 편집기를 엽니다. 자세한 내용은 텍스트 [서식 지정을 참조하십시오](#formattingtext).

* 선택(눈 아이콘): 대화형 통신에서 문서 조각을 포함\제외합니다.
* 채워지지 않은 값(정보): 문서 조각에서 채워지지 않은 변수의 수를 나타냅니다.

### 문서 조각 목록 {#list-document-fragments}

![listoptions](assets/listoptions.png)

* 빈 줄 삽입: 새 빈 줄을 삽입합니다.
* 선택(눈 아이콘): 대화형 통신에서 문서 조각을 포함\제외합니다.
* 글머리 기호/번호 건너뛰기: 목록 문서 조각에서 글머리 기호/번호 매기기를 건너뛸 수 있습니다.
* 채워지지 않은 값(정보): 문서 조각에서 채워지지 않은 변수의 수를 나타냅니다.

## 대화형 커뮤니케이션을 초안으로 저장 {#save-as-draft}

에이전트 UI를 사용하여 각 대화형 커뮤니케이션에 대해 하나 이상의 초안을 저장하고 나중에 초안을 검색하여 계속 작업할 수 있습니다. 각 초안의 다른 이름을 지정하여 해당 초안을 식별할 수 있습니다.

Adobe에서는 이러한 지침을 차례로 실행하여 인터랙티브 커뮤니케이션을 초안으로 저장할 것을 권장합니다.

### 초안으로 저장 기능 활성화 {#before-save-as-draft}

초안으로 저장 기능은 기본적으로 활성화되지 않습니다. 다음 단계를 수행하여 기능을 활성화합니다.

1. ccrDocumentInstance [Service](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/index.html) Provider Interface(SPI)를 구현합니다. SPI를 사용하면 Interactive Communication의 초안 버전을 고유한 식별자로 초안 ID와 함께 데이터베이스에 저장할 수 있습니다.
1. 이동 `https://'[server]:[port]'/system/console/configMgr`.
1. 통신 **[!UICONTROL 구성 만들기를 누릅니다]**.
1. [ **[!UICONTROL CCRDocumentInstanceService를 사용하여 저장 활성화]** ]를 선택하고 **[!UICONTROL 저장을 탭합니다]**.

### 인터랙티브 커뮤니케이션을 초안으로 저장 {#save-as-draft-agent-ui}

다음 단계를 수행하여 Interactive Communication을 초안으로 저장합니다.

1. Forms Manager에서 Interactive Communication을 선택하고 **[!UICONTROL Open Agent UI를 누릅니다]**.

1. 에이전트 UI에서 적절한 변경 작업을 수행하고 초안으로 **[!UICONTROL 저장을 누릅니다]**.

1. 이름 필드에 초안 이름을 **[!UICONTROL 지정하고 완료를]** 누릅니다 ****.

Interactive Communication을 초안으로 저장한 후에는 변경 **[!UICONTROL 내용]** 저장을 눌러 초안의 추가 변경 사항을 저장합니다.

### 대화형 통신 초안 검색 {#retrieve-draft}

Interactive Communication을 초안으로 저장한 후 이를 검색하여 계속 작업할 수 있습니다. 다음을 사용하여 대화형 통신 검색:

`https://server:port/aem/forms/createcorrespondence.hmtl?draftid=[draftid]`

[draftid] 는 Interactive Communication을 초안으로 저장한 후 생성된 초안 버전의 고유 식별자를 나타냅니다.

>[!NOTE]
>
>Interactive Communication을 초안으로 저장한 후 변경하는 경우 초안 버전이 열리지 않습니다.
