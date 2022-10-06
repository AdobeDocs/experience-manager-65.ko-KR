---
title: 게시된 양식 액세스 및 채우기
seo-title: Accessing and filling published forms
description: Forms Portal은 웹 개발자에게 Adobe Experience Manager(AEM)을 사용하여 작성된 웹 사이트에서 양식 포털을 만들고 사용자 지정할 수 있는 구성 요소를 제공합니다.
seo-description: Forms Portal equips Web Developers with components to create and customize a forms portal on websites authored using Adobe Experience Manager (AEM).
uuid: 44731604-5d97-46fa-baa9-0c020c634fa7
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 88dc8ef2-95ce-4906-ac28-eecc3a32a64e
docset: aem65
exl-id: aedf890c-a2f1-412f-8897-2492ffab335a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 0%

---

# 게시된 양식 액세스 및 채우기{#accessing-and-filling-published-forms}

양식 중심의 포털 배포 설정에서 양식 개발 및 포털 개발은 두 가지 서로 다른 활동입니다. 양식 디자이너는 양식을 디자인하고 저장소에 저장하는 동안 Web Developers에서 양식을 나열하고 제출을 처리하는 웹 응용 프로그램을 만듭니다. 그런 다음 양식 리포지토리와 웹 애플리케이션 간에 통신이 없으므로 Forms이 웹 계층에 복사됩니다.

이로 인해 설정 및 프로덕션 지연 관리에 문제가 발생하는 경우가 많습니다. 예를 들어 저장소에서 최신 버전의 양식을 사용할 수 있는 경우 양식 디자이너는 웹 계층의 양식을 대체하고 웹 애플리케이션을 수정한 다음 공용 사이트에서 양식을 다시 배포합니다. 웹 응용 프로그램을 다시 배포하면 서버 다운타임이 발생할 수 있습니다. 서버 다운타임은 계획된 활동이므로 변경 사항을 즉시 공용 사이트에 푸시할 수 없습니다.

Forms 포털은 관리 오버헤드 및 프로덕션 지연을 줄였습니다. AEM(Adobe Experience Manager)을 사용하여 작성된 웹 사이트에서 양식 포털을 만들고 사용자 지정하는 구성 요소를 웹 개발자에게 제공합니다.

forms 포털 및 해당 기능에 대한 자세한 내용은 [포털에서 양식 게시 소개](/help/forms/using/introduction-publishing-forms.md).

## 양식 포털 시작 {#getting-started-with-forms-portal}

게시된 양식 포털 페이지로 이동합니다. Forms 포털 페이지 만들기에 대한 자세한 내용은 [양식 포털 페이지 만들기](../../forms/using/creating-form-portal-page.md).

Roms 포털의 검색 및 목록 구성 요소는 AEM 서버의 게시 인스턴스에서 사용할 수 있는 양식을 표시합니다. 이 목록에는 모든 양식 또는 Forms 포털 페이지를 작성할 때 필터에 정의된 양식이 포함되어 있습니다. Forms 포털 페이지는 다음 이미지에 표시된 것과 비슷하게 보입니다.

![샘플 양식 포털 페이지 ](assets/forms-portal-page.png)

샘플 양식 포털 페이지

### 검색 및 목록 {#search-and-lister}

검색 및 목록 구성 요소를 사용하면 Forms 포털에 다음 기능을 추가할 수 있습니다.

* 즉시 사용 가능한 패널, 카드 또는 그리드 보기의 양식을 나열합니다. 또한 Forms Manager에서 특정 폴더의 사용자 지정 템플릿 목록 양식을 지원합니다.
* 양식을 렌더링하는 방법(HTML5, PDF 또는 둘 다)을 지정합니다.
* PDF 및 XFA 양식을 렌더링하는 방법(HTML 5, PDF 또는 둘 다)을 지정합니다. 비 XFA 양식을 HTML 5으로 구성합니다.
* 양식 속성, 메타데이터 및 태그와 같은 기준에 따라 양식을 검색할 수 있도록 설정합니다.
* 서블릿에 양식 데이터를 제출합니다.
* CSS(사용자 지정 스타일 시트)를 사용하여 포털의 모양과 느낌을 사용자 지정합니다.
* 양식에 대한 링크를 만듭니다.

다음 옵션을 사용하여 Forms 포털 페이지에서 양식을 검색할 수 있습니다.

* 전체 텍스트 검색
* 고급 검색

전체 텍스트 검색을 사용하면 지정된 키워드를 기반으로 양식을 찾아 나열할 수 있습니다.

![고급 검색 대화 상자](assets/search-panel.png)

고급 검색 대화 상자

고급 검색을 사용하면 지정된 양식 속성에 따라 양식을 검색할 수 있습니다. 전체 텍스트 검색보다 더 구체적인 결과를 제공합니다. 고급 검색에는 태그, 속성(예: 작성자, 설명 및 제목), 수정 날짜 및 전체 텍스트를 기반으로 하는 검색이 포함됩니다.

라이스터는 검색 매개 변수에 따라 양식을 표시합니다. 검색 결과의 각 양식은 연결된 양식에 하이퍼링크되는 아이콘과 함께 표시됩니다. 아이콘을 클릭하여 관련 양식을 열고 작업할 수 있습니다.

### 양식 채우기 {#filling-a-form}

![샘플 적응형 양식](assets/filling_a_form.png)

샘플 적응형 양식

페이지의 검색 및 목록 구성 요소에서 양식과 함께 제공된 링크에서 양식에 액세스할 수 있습니다.

각 양식에는 사용자가 양식을 채울 수 있는 도움말 정보가 포함되어 있습니다.

#### 초안 및 제출 {#drafts-and-submission}

사용자는 저장 단추를 클릭하여 양식 초안을 저장할 수 있습니다. 이를 통해 사용자는 양식을 제출하기 전에 일정 기간 동안 양식 작업을 수행할 수 있습니다.

양식에 입력된 데이터(첨부 파일 포함)는 서버의 초안으로 저장됩니다. 양식 초안은 여러 번 저장할 수 있습니다. 저장된 양식은 페이지의 초안 및 제출 구성 요소의 초안 탭에 나타납니다.

양식 채우기가 완료되면 사용자는 양식의 제출 단추를 클릭하여 양식을 제출합니다. 제출된 양식은 페이지의 초안 및 제출 구성 요소의 제출 탭에 표시됩니다.

>[!NOTE]
>
>제출된 양식은 적응형 양식에 대한 제출 작업이 Forms Portal 제출 작업으로 구성된 경우에만 제출됨 Forms 탭에 표시됩니다. 제출 작업에 대한 자세한 내용은 [제출 작업 구성](../../forms/using/configuring-submit-actions.md).

![초안 및 제출 구성 요소](assets/draft-submission.png)

초안 및 제출 구성 요소

## 제출된 양식 데이터를 사용하여 새 양식 시작 {#start-a-new-form-using-submitted-form-data}

작성해서 제출해야 하는 양식이 있습니다. 예를 들어, 세금 신고 양식은 매년 제출됩니다. 이런 경우 양식을 작성할 때마다 일부 정보가 변경되지만 개인 및 가족 세부 정보가 변경되지 않습니다. 그러나 처음부터 전체 양식을 다시 채워야 합니다.

AEM Forms을 사용하면 양식 채우기 환경을 최적화하고 양식을 다시 작성하고 제출하는 시간을 크게 줄일 수 있습니다. 최종 사용자는 제출된 양식의 데이터를 사용하여 새 양식을 시작할 수 있습니다. 이 기능은 [초안 및 제출 구성 요소](../../forms/using/draft-submission-component.md). 양식 포털 페이지에 초안 및 제출 구성 요소를 추가하고 게시하면 최종 사용자는 제출된 Forms 및 초안 Forms 탭에서 제출된 양식의 데이터를 사용하여 새 양식을 시작하는 옵션을 찾습니다. 다음 이미지는 해당 옵션을 강조 표시합니다.

![새 양식 시작](assets/start-a-new-form.png)

단추를 클릭하여 새 양식을 시작하면 해당 제출된 양식의 데이터가 있는 새 양식이 열립니다. 이제 필요에 따라 정보를 검토 및 업데이트하여 양식을 제출할 수 있습니다.
