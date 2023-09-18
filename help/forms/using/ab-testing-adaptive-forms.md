---
title: 적응형 양식에 대한 A/B 테스트 만들기 및 관리
description: AEM Forms은 적응형 양식에 대한 A/B 테스트를 실행하여 고객 경험을 향상하고 전환율을 향상시킬 수 있는 Adobe Target과 통합됩니다.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
docset: aem65
exl-id: be2444df-c772-4a8e-83f9-0f565c15a44e
source-git-commit: ab3d016c7c9c622be361596137b150d8719630bd
workflow-type: tm+mt
source-wordcount: '1554'
ht-degree: 2%

---

# 적응형 양식에 대한 A/B 테스트 만들기 및 관리{#create-and-manage-a-b-test-for-adaptive-forms}

[!BADGE 중단됨]{type=negative tooltip="이 기능은 현재 사용 중단되었습니다."}

<div class="preview"> 적응형 양식에 대한 A/B 테스트 기능이 종료되었으며 더 이상 지원되지 않습니다. </div>

## 개요 {#overview-br}

고객이 제공하는 경험이 매력적이지 않을 경우 양식을 포기할 가능성이 높습니다. 고객에게는 번거로운 일이지만, 조직의 지원 규모와 비용도 증가할 수 있습니다. 전환율을 높이는 올바른 고객 경험을 파악하고 제공하는 것은 중요하고 어려운 일입니다. Adobe Experience Manager Forms이 이 문제의 열쇠를 쥐고 있다.

AEM Forms은 Adobe Experience Cloud 솔루션인 Adobe Target과 통합되어 여러 디지털 채널에서 개인화되고 매력적인 고객 경험을 제공합니다. Target의 주요 기능 중 하나는 동시 A/B 테스트를 빠르게 설정하고, 타겟팅된 사용자에게 관련 콘텐츠를 제공하고, 더 나은 전환율을 유도하는 경험을 식별할 수 있는 A/B 테스트입니다.

Adobe Experience Manager(AEM) Forms을 사용하면 적응형 양식에 대한 A/B 테스트를 실시간으로 설정하고 실행할 수 있습니다. 또한 양식 경험의 실시간 성능을 시각화하고 사용자 참여 및 전환을 최대화하는 기능을 식별하는 기본 제공 및 사용자 지정 가능한 보고 기능을 제공합니다.

## AEM Forms에서 Target 설정 및 통합 {#set-up-and-integrate-target-in-aem-forms}

적응형 양식에 대한 A/B 테스트를 만들고 분석하기 전에 Target 서버를 설정하고 AEM Forms에 통합해야 합니다.

### Target 설정 {#set-up-target}

AEM을 Target과 통합하려면 유효한 Adobe Target 계정이 있는지 확인하십시오. Adobe Target에 등록하면 클라이언트 코드를 받습니다. AEM을 Target에 연결하려면 클라이언트 코드, Target 계정과 연결된 이메일 및 암호가 필요합니다.

클라이언트 코드는 Adobe Target 고객 계정을 식별하며 Adobe Target 서버를 호출할 때 URL에서 하위 도메인으로 사용됩니다. 계속하기 전에 다음으로 로그온하십시오. [https://experience.adobe.com/](https://experience.adobe.com/) 그리고 액세스 권한이 있는 경우 [!DNL Adobe Target] 의 옵션 [!UICONTROL 빠른 액세스] 섹션.

### 실행 중인 Target 서버와 AEM Forms 통합 {#integrate-target-in-aem-forms}

1. AEM 서버에서 https://&lt;*호스트 이름*>:&lt;*포트*>/libs/cq/core/content/tools/cloudservices.html.

1. 다음에서 **Adobe Target** 섹션, 클릭 **구성 표시** 그리고 **+** 구성 추가 아이콘
대상을 처음 구성하는 경우 **지금 구성.**

1. 구성 만들기 대화 상자에서 **제목** 및 선택적으로 **이름** 구성.

1. **만들기**&#x200B;를 클릭합니다. 구성 요소 편집 대화 상자가 열립니다.
1. 클라이언트 코드, 이메일 및 암호 등 Target 계정 세부 사항을 지정합니다.
1. 선택 **Rest** API 유형 드롭다운 목록

1. 클릭 **Adobe Target에 연결** target과의 연결을 초기화할 수 있습니다. 정상적으로 연결되면 연결 성공이라는 메시지가 표시됩니다. 메시지에서 **확인**&#x200B;을 클릭한 다음 대화 상자에서 **확인**&#x200B;을 클릭합니다. Target 계정이 구성되었습니다.

1. 에 설명된 대로 Target 프레임워크 만들기 [프레임워크 추가](/help/sites-administering/target.md).

1. https://으로 이동&lt;*호스트 이름*>:&lt;*포트*>/system/console/configMgr.

1. 클릭 **AEM Forms Target 구성**.
1. 선택 **Target 프레임워크**.
1. 다음에서 **타겟 URL** 필드, A/B 테스트가 실행되는 모든 URL을 지정합니다. 예: https://&lt;*호스트 이름*>:&lt;*포트*>/ OSGi 또는 https://의 AEM Forms 서버용&lt;*호스트 이름*>:&lt;*포트*JEE의 AEM Forms 서버용 >/lc/
게시 인스턴스에 대한 Target URL을 구성하려고 하며, 고객이 호스트 이름 또는 IP 주소를 사용하여 해당 URL에 액세스할 수 있습니다. 이 경우 호스트 이름과 IP 주소를 사용하여 두 를 모두 Target URL로 구성해야 합니다. URL 중 하나만 구성하는 경우 다른 URL에서 온 고객에 대해서는 A/B 테스트가 실행되지 않습니다. 클릭 **+** 를 사용하여 여러 URL을 지정할 수 있습니다.

1. **저장**&#x200B;을 클릭합니다.

Target 서버가 AEM Forms과 통합되었습니다. 이제 Adobe Target을 사용할 수 있는 전체 라이선스가 있는 경우 A/B 테스트를 활성화할 수 있습니다.

Adobe Target을 사용할 수 있는 정식 라이선스가 있는 경우 Target을 AEM Forms과 통합한 후 다음 매개 변수로 서버를 시작합니다.

`parameter -Dabtesting.enabled=true java -Xmx2048m -XX:MaxPermSize=512M -jar -Dabtesting.enabled=true`

AEM 인스턴스가 턴키에서 서비스로 시작된 JBoss®에서 실행 중인 경우 `jboss\bin\standalone.conf.bat` file, 다음 항목에 -Dabtesting.enabled=true 매개 변수를 추가합니다.

`set "JAVA_OPTS=%JAVA_OPTS% -Dadobeidp.serverName=server1 -Dfile.encoding=utf8 -Djava.net.preferIPv4Stack=true -Dabtesting.enabled=true"`

JBoss® 서버 외에 모든 애플리케이션 서버의 서버 시작 스크립트에서 -Dabtesting.enabled=true jvm 인수를 추가할 수 있습니다. 이제 적응형 양식에 대한 A/B 테스트를 만들고 실행할 수 있습니다.

>[!NOTE]
>
>구성된 Target URL을 나중에 업데이트하는 경우, 현재 URL을 가리키도록 실행 중인 A/B 테스트를 업데이트해야 합니다. A/B 테스트 업데이트에 대한 자세한 내용은 [A/B 테스트 업데이트](/help/forms/using/ab-testing-adaptive-forms.md#p-update-a-b-test-p).
>

## AEM 내에서 대상 만들기 {#create-audiences-within-aem}

AEM을 사용하면 대상을 만들고 A/B 테스트에 사용할 수 있습니다. AEM 내에서 생성하는 대상자는 AEM Forms에서 사용할 수 있습니다. AEM 내에서 대상을 만들려면 다음을 수행하십시오.

1. 작성 인스턴스에서 을 누릅니다. **Adobe Experience Manager** > **개인화** > **대상**.

1. 대상 페이지에서 을 누릅니다. **대상 만들기 > 타겟 대상 만들기**.
1. Adobe Target 구성 대화 상자에서 Target 구성을 선택하고 **확인**.
1. 새 대상 만들기 페이지에서 규칙을 만듭니다. 규칙을 사용하여 대상자를 분류할 수 있습니다. 예를 들어 운영 체제에 따라 대상을 분류하려고 합니다. 대상자 A는 Windows에서 가져오고 대상자 B는 Linux®에서 가져옵니다.

   1. Windows를 기준으로 대상을 분류하려면 규칙 #1에서 다음을 선택합니다 **OS** 속성 유형. When 드롭다운에서 **Windows.**

   1. Linux®를 기반으로 대상을 분류하려면 규칙 #2에서 다음을 선택합니다. **OS** 속성 유형. 다음에서 **날짜** 드롭다운, 선택 **Linux®**, 및 클릭 **다음**.

1. 생성된 대상자의 이름을 지정하고 **저장**.

아래 표시된 대로 양식에 대한 A/B 테스트를 구성할 때 대상을 선택할 수 있습니다.

## 적응형 양식에 대한 A/B 테스트 만들기 {#create-a-b-test}

1. 다음으로 이동 **Forms 및 문서** at https://&lt;*호스트 이름*>:&lt;*포트*>/aem/forms.html/content/dam/formsanddocuments.

1. 적응형 양식이 포함된 폴더로 이동합니다.
1. 다음을 클릭합니다. **선택** 도구 모음에서 을 클릭하고 적응형 양식을 선택합니다.
1. 클릭 **자세히** 도구 모음에서 를 클릭하고 를 선택합니다. **A/B 테스트 구성**. A/B 테스트 구성 페이지가 열립니다.

[](assets/ab-test-configure-1.png)

1. 다음 항목 지정 **활동 이름** A/B 테스트용

1. 대상 드롭다운 목록에서 양식의 다양한 경험을 제공할 대상을 선택합니다. 예를 들어, **Chrome 사용 방문자 수**. 대상자 목록은 구성된 Target 서버에서 채워집니다.

1. 다음에서 **경험 배포** 경험 A 및 B의 필드에서 분포를 백분율로 지정하여 총 대상자 간 경험 분포를 결정합니다. 예를 들어 경험 A와 B에 대해 각각 40, 60을 지정하는 경우 경험 A는 대상의 40%에게 제공되고 나머지 60%는 경험 B를 봅니다.
1. 클릭 **구성**. A/B 테스트 만들기를 확인하는 대화 상자가 나타납니다.
1. 클릭 **경험 B 편집** 따라서 적응형 양식을 편집 모드에서 열 수 있습니다. 기본 경험 A가 아닌 다른 경험을 만들어 양식을 수정합니다. 경험 B에서 허용되는 변형은 다음 항목에서의 변경입니다.

   * CSS 또는 스타일링
   * 다른 패널 또는 동일한 패널의 필드 순서
   * 패널 레이아웃
   * 패널 제목
   * 필드에 대한 설명, 레이블 및 도움말 텍스트
   * 제출 흐름에 영향을 주거나 중단되지 않는 스크립트
   * 유효성 검사(클라이언트와 서버 측 모두)
   * 경험 B의 테마(경험 B에 대한 대체 테마를 선택할 수 있음)

1. Forms 및 문서 UI로 이동하여 적응형 양식을 선택하고 **자세히**, 및 선택 **A/B 테스트 시작**.

이제 A/B 테스트가 실행 중이고 지정된 대상자에게 지정된 분포를 기반으로 임의로 경험이 제공됩니다.

## A/B 테스트 업데이트 {#update-a-b-test}

실행 중인 A/B 테스트의 대상자 및 경험 배포를 업데이트할 수 있습니다.

A/B 테스트를 업데이트하려면:

1. Forms 및 문서 UI에서 A/B 테스트가 실행 중인 적응형 양식이 포함된 폴더로 이동합니다.
1. 적응형 양식을 선택합니다.
1. 클릭 **자세히** 다음을 선택합니다. **A/B 테스트 편집**. A/B 테스트 업데이트 페이지가 열립니다.

1. 필요에 따라 대상자 및 경험 배포를 업데이트합니다.
1. **업데이트**&#x200B;를 클릭합니다.

## A/B 테스트 보고서 보기 및 분석 {#view-and-analyze-a-b-test-report}

원하는 기간 동안 A/B 테스트를 실행하도록 허용하면 보고서를 생성하고 어느 경험이 더 나은 전환을 초래했는지 확인할 수 있습니다. 성과가 더 좋은 경험을 우승자로 선언하거나 다른 A/B 테스트를 실행하도록 선택할 수 있습니다.

A/B 테스트 보고서를 보고 분석하려면 다음 작업을 수행하십시오.

1. 적응형 양식을 선택하고 **자세히**&#x200B;을 클릭한 다음 을 클릭합니다 **A/B 테스트 보고서**. 보고서가 표시됩니다.

[](assets/ab-test-report-3.png)

1. 보고서를 분석하여 성과가 더 좋은 경험 중 하나를 우승자로 선언하기에 충분한 데이터 포인트가 있는지 확인합니다. 동일한 A/B 테스트를 더 오랫동안 계속하도록 선택하거나 우승자를 선언하고 A/B 테스트를 종료할 수 있습니다.
1. 우승자를 선언하고 A/B 테스트를 종료하려면 **A/B 테스트 종료** 보고 대시보드의 단추입니다. 대화 상자에 두 경험 중 하나를 우승자로 선언하라는 메시지가 표시됩니다. 우승자를 선택하고 A/B 테스트 종료를 확인합니다.
또는 다음을 클릭하여 우승자를 먼저 선언할 수 있습니다. **우승자 선언** 각 경험에 대한 단추입니다. 우승자를 확인하라는 메시지가 표시됩니다. 클릭 **예** 를 클릭하여 A/B 테스트를 종료합니다.

경험 A를 우승자로 선택한 경우 A/B 테스트가 종료되고 앞으로 경험 A만 대상자에게 제공됩니다.
