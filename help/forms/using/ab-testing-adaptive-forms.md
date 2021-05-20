---
title: 적응형 양식에 대한 A/B 테스트 만들기 및 관리
seo-title: 적응형 양식에 대한 A/B 테스트 만들기 및 관리
description: AEM Forms은 적응형 양식에 대한 A/B 테스트를 실행하여 고객 경험을 향상시키고 전환율을 향상시킬 수 있는 Adobe Target과 통합됩니다.
seo-description: AEM Forms은 적응형 양식에 대한 A/B 테스트를 실행하여 고객 경험을 향상시키고 전환율을 향상시킬 수 있는 Adobe Target과 통합됩니다.
uuid: e258805c-4da8-4c5d-ae91-7bea78a6a71b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: 8f776f30-ff93-4d19-94c6-c4bfe6f1fae2
docset: aem65
exl-id: be2444df-c772-4a8e-83f9-0f565c15a44e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1569'
ht-degree: 0%

---

# 적응형 양식에 대한 A/B 테스트 만들기 및 관리{#create-and-manage-a-b-test-for-adaptive-forms}

## 개요 {#overview-br}

고객이 이 기능을 제공하지 않는 경험을 통해 양식을 포기할 가능성이 높습니다. 고객에게 좌절감을 주지만 조직에 대한 지원 볼륨과 비용을 늘릴 수도 있습니다. 전환율을 높일 수 있는 올바른 고객 경험을 식별 및 제공하기 어려운 것도 중요합니다. Adobe Experience Manager Forms은 이 문제의 열쇠를 쥐고 있습니다.

AEM Forms은 Adobe Marketing Cloud 솔루션인 Adobe Target과 통합되어 있으며, 여러 디지털 채널에서 개인화되고 매력적인 고객 경험을 제공할 수 있습니다. Target의 주요 기능 중 하나는 동시 A/B 테스트를 신속하게 설정하고, 타깃팅된 사용자에게 관련 컨텐츠를 제공하고, 전환율을 높이는 경험을 식별할 수 있도록 하는 A/B 테스트입니다.

AEM Forms을 사용하면 적응형 양식에 대해 A/B 테스트를 실시간으로 설정하고 실행할 수 있습니다. 또한 기본 제공 및 사용자 지정 가능한 보고 기능을 제공하여 양식 경험의 실시간 성능을 시각화하고 사용자 참여도와 전환을 극대화하는 것을 식별합니다.

## AEM Forms {#set-up-and-integrate-target-in-aem-forms}에서 Target 설정 및 통합

적응형 양식에 대한 A/B 테스트를 만들고 분석하기 전에 Target 서버를 설정하고 AEM Forms에 통합해야 합니다.

### Target {#set-up-target} 설정

AEM을 Target과 통합하려면 유효한 Adobe Target 계정이 있는지 확인합니다. Adobe Target에 등록하면 클라이언트 코드가 전송됩니다. AEM을 Target과 연결하려면 클라이언트 코드, Target 계정과 연결된 이메일 및 암호가 필요합니다.

클라이언트 코드는 Adobe Target 고객 계정을 식별하고 Adobe Target 서버를 호출할 때 URL에서 하위 도메인으로 사용됩니다. 계속하기 전에 자격 증명을 사용하여 [https://testandtarget.omniture.com/](https://testandtarget.omniture.com/)에 로그인할 수 있는지 확인하십시오.

### AEM Forms에서 Target 통합 {#integrate-target-in-aem-forms}

실행 중인 Target 서버를 AEM Forms과 통합하려면 다음 단계를 수행하십시오.

1. AEM 서버에서 https://&lt;*hostname*>:&lt;*port*>/libs/cq/core/content/tools/cloudservices.html으로 이동합니다.

1. **Adobe Target** 섹션에서 **구성 표시** 를 클릭한 다음 **+** 아이콘을 클릭하여 새 구성을 추가합니다.
처음으로 대상을 구성하는 경우 **지금 구성 을 클릭하십시오.**

1. 구성 만들기 대화 상자에서 구성에 대해 **제목** 및 선택적으로 **이름**&#x200B;을 지정합니다.

1. **만들기**&#x200B;를 클릭합니다. 구성 요소 편집 대화 상자가 열립니다.
1. 클라이언트 코드, 이메일 및 암호와 같은 Target 계정 세부 사항을 지정합니다.
1. API 유형 드롭다운 목록에서 **Rest**&#x200B;를 선택합니다.

1. **Adobe Target에 연결**&#x200B;을 클릭하여 Target과의 연결을 초기화합니다. 연결에 성공하면 연결 성공 메시지가 표시됩니다. 메시지에서 **확인**&#x200B;을 클릭한 다음 대화 상자에서 **확인**&#x200B;을 클릭합니다. Target 계정이 구성되었습니다.

1. [프레임워크 추가](/help/sites-administering/target.md)에 설명된 대로 Target 프레임워크을 만듭니다.

1. https://&lt;*hostname*>:&lt;*port*/system/console/configMgr 로 이동합니다.

1. **AEM Forms Target 구성**&#x200B;을 클릭합니다.
1. **Target 프레임워크**&#x200B;를 선택합니다.
1. **Target URL** 필드에서 A/B 테스트가 실행될 모든 URL을 지정합니다. 예: https://&lt;*hostname*>:&lt;*OSGi 또는 https://&lt;* hostname *>:&lt;* JEE의 AEM Forms 서버에 대한 port */lc/.*
게시 인스턴스에 대한 Target URL을 구성하려는 경우 고객이 호스트 이름 또는 IP 주소를 사용하여 URL에 액세스할 수 있다고 가정할 경우 IP 주소와 호스트 이름을 사용하여 둘 다 Target URL로 구성해야 합니다. URL 중 하나만 구성하는 경우 다른 URL에서 오는 고객에 대해서는 A/B 테스트가 실행되지 않습니다. **+** 를 클릭하여 여러 URL을 지정합니다.

1. **저장**&#x200B;을 클릭합니다.

Target 서버가 AEM Forms과 통합되었습니다. 이제 Adobe Target을 활용할 수 있는 전체 라이센스가 있는 경우 A/B 테스트를 활성화할 수 있습니다.

Adobe Target을 활용할 수 있는 전체 라이센스가 있는 경우 AEM Forms과 Target을 통합한 후 다음 매개 변수로 서버를 시작합니다.

`parameter -Dabtesting.enabled=true java -Xmx2048m -XX:MaxPermSize=512M -jar -Dabtesting.enabled=true`

AEM 인스턴스가 JBoss에서 실행 중인 경우, 턴키에서 서비스로 시작된 경우, `jboss\bin\standalone.conf.bat` 파일의 다음 항목에 -Dabtesting.enabled=true 매개 변수를 추가합니다.

`set "JAVA_OPTS=%JAVA_OPTS% -Dadobeidp.serverName=server1 -Dfile.encoding=utf8 -Djava.net.preferIPv4Stack=true -Dabtesting.enabled=true"`

jboss 서버 외에 모든 애플리케이션 서버의 서버 시작 스크립트에서 -Dabtesting.enabled=true jvm 인수를 추가할 수 있습니다. 이제 적응형 양식에 대한 A/B 테스트를 만들고 실행할 수 있습니다.

>[!NOTE]
>
>나중에 구성된 Target URL을 업데이트하는 경우 실행 중인 A/B 테스트가 현재 URL을 가리키도록 업데이트해야 합니다. A/B 테스트 업데이트에 대한 자세한 내용은 [A/B 테스트 업데이트](/help/forms/using/ab-testing-adaptive-forms.md#p-update-a-b-test-p)를 참조하십시오.


## AEM {#create-audiences-within-aem} 내에서 대상 만들기

AEM에서는 대상을 만들고 A/B 테스트에 사용할 수 있습니다. AEM 내에서 만드는 대상은 AEM Forms에서 사용할 수 있습니다. AEM 내에서 대상을 만들려면 다음 단계를 수행하십시오.

1. 작성 인스턴스에서 **Adobe Experience Manager** > **개인화** > **대상**&#x200B;을 누릅니다.

1. 대상 페이지에서 **대상 만들기 > Target 대상 만들기**&#x200B;를 탭합니다.
1. Adobe Target 구성 대화 상자에서 Target 구성을 선택하고 **확인**&#x200B;을 클릭합니다.
1. 새 대상 만들기 페이지에서 규칙을 만듭니다. 규칙을 사용하여 대상을 분류할 수 있습니다. 예를 들어 운영 체제를 기준으로 대상을 분류하려고 합니다. 대상 A는 Windows이고 대상 B는 Linux에서 가져옵니다.

   1. Windows를 기준으로 대상을 분류하려면 규칙 #1에서 **OS** 속성 유형을 선택합니다. When 드롭다운에서 **Windows를 선택합니다.**

   1. Linux를 기준으로 대상을 분류하려면 규칙 #2에서 **OS** 속성 유형을 선택합니다. **When** 드롭다운에서 **Linux**&#x200B;를 선택하고 **다음**&#x200B;을 클릭합니다.

1. 만들어진 대상자의 이름을 지정하고 **저장**&#x200B;을 클릭합니다.

아래 표시된 대로 양식에 대해 A/B 테스트를 구성할 때 대상을 선택할 수 있습니다.

## A/B 테스트 만들기 {#create-a-b-test}

적응형 양식에 대한 A/B 테스트를 만들려면 다음 단계를 수행하십시오.

1. https://&lt;*hostname*>에서 **Forms 및 문서**:&lt;*port*>/aem/forms.html/content/dam/formsanddocuments로 이동합니다.

1. 적응형 양식이 포함된 폴더로 이동합니다.
1. 도구 모음에서 **선택** 도구를 클릭하고 적응형 양식을 선택합니다.
1. 도구 모음에서 **자세히**&#x200B;를 클릭하고 **Configure A/B Testing**&#x200B;을 선택합니다. A/B 테스트 구성 페이지가 열립니다.

[ ](assets/ab-test-configure-1.png)

1. A/B 테스트에 대해 **활동 이름**&#x200B;을 지정합니다.

1. 대상 드롭다운 목록에서 양식의 다른 경험을 제공할 대상을 선택합니다. 예를 들어 **Chrome**&#x200B;을 사용하는 방문자. 대상 목록은 구성된 Target 서버에서 채워집니다.

1. 경험 A 및 B에 대한 **경험 배포** 필드에서 백분율로 전체 대상 간 경험 분포를 결정합니다. 예를 들어, 경험 A와 B에 대해 40, 60을 각각 지정하는 경우 경험 A는 대상자의 40%에게 제공되고, 나머지 60%에는 경험 B가 표시됩니다.
1. **구성**&#x200B;을 클릭합니다. A/B 테스트 만들기를 확인하는 대화 상자가 나타납니다.
1. **경험 편집**&#x200B;을 클릭하여 편집 모드에서 적응형 양식을 엽니다. 양식을 수정하여 기본 경험 A와 다른 경험을 만듭니다. 경험 B에서 사용할 수 있는 가능한 변형은 다음과 같습니다.

   * CSS 또는 스타일링
   * 다른 패널 또는 동일한 패널의 필드 순서
   * 패널 레이아웃
   * 패널 제목
   * 필드에 대한 설명, 레이블 및 도움말 텍스트
   * 제출 흐름에 영향을 주지 않거나 중단되지 않는 스크립트
   * 유효성 검사(클라이언트와 서버 측 모두)
   * 경험 B의 테마(경험 B의 대체 테마를 선택할 수 있음)

1. Forms 및 문서 UI로 이동하고 적응형 양식을 선택하고 **더 보기**&#x200B;를 클릭한 다음 **A/B 테스트 시작**&#x200B;을 선택합니다.

이제 A/B 테스트가 실행되고 있으며 지정된 대상이 지정된 배포를 기반으로 경험을 임의로 제공합니다.

## A/B 테스트 업데이트 {#update-a-b-test}

실행 중인 A/B 테스트의 대상 및 경험 배포를 업데이트할 수 있습니다. 방법은 다음과 같습니다.

1. Forms 및 문서 UI에서 A/B 테스트가 실행 중인 적응형 양식이 포함된 폴더로 이동합니다.
1. 적응형 양식을 선택합니다.
1. **더 보기**&#x200B;를 클릭한 다음 **Edit A/B 테스트**&#x200B;를 선택합니다. A/B 테스트 업데이트 페이지가 열립니다.

1. 필요에 따라 대상 및 경험 배포를 업데이트합니다.
1. **업데이트**&#x200B;를 클릭합니다.

## A/B 테스트 보고서 보기 및 분석 {#view-and-analyze-a-b-test-report}

원하는 기간 동안 A/B 테스트를 실행하도록 허용하면 보고서를 생성하고 더 나은 전환을 초래한 경험을 확인할 수 있습니다. 우승자에게 더 나은 수행 경험을 선언하거나 다른 A/B 테스트를 실행하도록 선택할 수 있습니다. 이렇게 하려면 다음 단계를 수행합니다.

1. 적응형 양식을 선택하고 **더 보기**&#x200B;를 클릭한 다음 **A/B 테스트 보고서**&#x200B;를 클릭합니다. 보고서가 표시됩니다.

[ ](assets/ab-test-report-3.png)

1. 보고서를 분석하고 더 성과가 좋은 경험 중 하나를 승자로 선언할 데이터 포인트가 충분한지 확인합니다. 동일한 A/B 테스트를 더 오랫동안 계속하도록 선택하거나 우승자를 선언하고 A/B 테스트를 종료할 수 있습니다.
1. 우승자를 선언하고 A/B 테스트를 종료하려면 보고 대시보드에서 **End A/B test** 단추를 클릭하십시오. 두 경험 중 하나를 승자로 선언하라는 대화 상자가 표시됩니다. 우승자를 선택하고 확인을 클릭하여 A/B 테스트를 종료합니다.
또는 먼저 각 경험에 대한 **우승자 선언** 단추를 클릭하여 승자를 선언할 수 있습니다. 우승자를 확인하라는 메시지가 표시됩니다. **예**&#x200B;를 클릭하여 A/B 테스트를 종료합니다.

경험 A를 승자로 선택하면 A/B 테스트가 종료되고 앞으로 진행되는 모든 대상에는 경험 A만 제공됩니다.
