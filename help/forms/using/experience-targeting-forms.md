---
title: AEM Forms에서 타깃팅된 경험 만들기
seo-title: AEM Forms에서 타깃팅된 경험 만들기
description: AEM Forms의 Target을 사용하여 타깃팅된 고객에 맞는 경험을 만들 수 있습니다.
seo-description: AEM Forms의 Target을 사용하여 타깃팅된 고객에 맞는 경험을 만들 수 있습니다.
uuid: 174b6054-8fe3-4ab2-8afd-435e5dff9044
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: 6cf54a08-d429-4a58-8429-a1cb784448d1
translation-type: tm+mt
source-git-commit: 9d90bc5f77f827925e3e1ecd12d56a94a2bbae30
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 0%

---


# AEM Forms {#create-targeted-experiences-in-aem-forms}에서 타깃팅된 경험 만들기

## Adobe Target과 AEM Forms {#integrate-adobe-target-with-aem-forms} 통합

AEM과 통합된 Adobe Target을 사용하면 타겟 고객에 맞게 맞춤화된 경험을 제작할 수 있습니다. Adobe Target을 사용하면 A/B 테스트를 만들고, 사용자 응답을 측정하며, 타깃팅된 사용자를 위한 맞춤형 웹 컨텐츠를 생성할 수 있습니다. Adobe Target을 AEM Forms과 통합하여 적응형 양식 및 인터랙티브한 커뮤니케이션의 이미지 구성 요소를 타깃팅할 수 있습니다.

적응형 양식 및 대화형 통신과 함께 사용하도록 AEM에서 Adobe Target을 구성합니다. AEM[ 및 ](/help/sites-administering/target.md)프레임워크 추가[를 참조하십시오.](/help/sites-administering/target.md)

>[!NOTE]
>
>타깃팅은 응용 양식 또는 대화형 통신이 호스트 이름 또는 IP 주소를 사용하여 렌더링될 때 작동합니다. 적응형 양식 또는 대화형 통신이 localhost를 사용하여 렌더링되면 실패합니다.

## Target 활동 만들기 {#creating-a-target-activity}

1. **Adobe Experience Manager > 개인화 > 활동**&#x200B;을 누릅니다.

   `https://<hostname>:<port>/libs/cq/personalization/touch-ui/content/v2/activities.html`

1. 활동 페이지에서 **만들기 > 브랜드 만들기**&#x200B;를 탭합니다.
1. 템플릿을 선택하고 속성을 입력하라는 메시지가 표시됩니다.

   템플릿을 선택하고 **다음을 누릅니다.** 속성 섹션에 브랜드 제목을 입력하고 만들기를  **누릅니다.**
이제 브랜드가 활동 페이지에 나열됩니다.

1. 활동 페이지에서 브랜드를 누릅니다.
1. 브랜드 기본 영역에서 **만들기** > **활동 만들기**&#x200B;를 탭합니다.

   활동을 만들 때 세부 사항, 타겟 및 설정을 지정합니다.

   세부 사항 섹션에는 이름, 타깃팅 엔진 및 목표가 포함됩니다. 타깃팅 엔진으로 Adobe Target을 선택하면 Target 클라우드 구성 옵션이 활성화됩니다. Target 클라우드 구성을 선택하고 활동 유형을 선택하고 활동의 목표를 제공한 다음 **다음**&#x200B;을 누릅니다. 대화형 통신은 경험 타깃팅 활동 유형만 지원합니다.

   Target 섹션에서 대상 경험을 추가하고 이름을 지정할 수 있습니다. **경험 추가**&#x200B;를 클릭하여 **대상 선택** 및 **이름 경험** 옵션을 활성화합니다. 대상 및 해당 소스의 목록을 보려면 **대상 선택**&#x200B;을 누릅니다. 대상자 이름 목록에서 대상자를 선택합니다. **경험 추가**&#x200B;를 눌러 경험 이름을 지정하고 **다음**&#x200B;을 누릅니다.

   목표 및 설정 섹션에서 활동을 예약하고 우선 순위를 지정할 수 있습니다. 활동의 시작 날짜, 종료 날짜 및 우선 순위, 목표 지표, 추가 지표를 설정하고 **저장**&#x200B;을 탭합니다.

   이제 활동이 브랜드 페이지에 나열됩니다.

   >[!NOTE]
   >
   >&quot;활동이 저장되었지만 Target에 동기화되지 않았습니다. 이유:활동을 저장할 때 발생한 경우 다음 경험에 &quot;오퍼가 없습니다.&quot;가 표시됩니다.

1. 대상을 활성화하려면 .jsp 파일을 편집하여 적응형 양식 템플릿에서 사용하는 클라이언트 라이브러리를 포함합니다.

   예를 들어 기본 구현에서 **도구** > **CRXDE Lite**&#x200B;을 클릭합니다.

   CRXDE Lite 주소 표시줄에 /libs/fd/af/components/page/base/head.jsp을 입력하여 head.jsp 파일을 편집합니다.

   이 구현에서는 simpleEnrollment 템플릿을 사용합니다. 이 구현에서 다음 클라이언트 라이브러리를 포함하도록 head.jsp 파일을 수정합니다.

   `<cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>`

   `<cq:include path="clientcontext_optimized" resourceType="/libs/cq/personalization/components/clientcontext_optimized"/>`

   `<cq:include path="config" resourceType="cq/personalization/components/clientcontext_optimized/config"/>`

1. 적응형 양식의 대상 프레임워크를 활성화하려면 양식이나 대화형 커뮤니케이션으로 이동하여 편집 모드에서 엽니다.

   편집 모드에서 양식 또는 대화형 통신을 열려면 **Select**&#x200B;을 누른 다음 **열기**&#x200B;를 탭합니다.

   또는 포인터를 폼이나 대화형 통신 아이콘 위로 가져가면 선택하지 않고 4개의 단추가 나타납니다. 나타나는 **편집** 단추를 눌러 편집 모드에서 양식을 열 수 있습니다.

1. 페이지 도구 모음에서 **페이지 정보** ![테마 옵션](assets/theme-options.png) > **속성 열기**&#x200B;를 탭합니다.
1. 일반 탭에서 **Adobe Target** 필드에 대한 구성을 선택합니다. **저장 및 닫기**&#x200B;를 누릅니다.

## 응용 양식 이미지 또는 대화형 통신 이미지에 만든 활동 적용 {#applying-created-activity-to-an-adaptive-form-image-or-an-interactive-communication-image}

1. 적응형 양식 및 대화형 통신을 열어 편집합니다. 대화형 통신을 여는 경우 웹 채널을 엽니다.

1. 대화형 통신 또는 응용 양식의 작성 모드에서 타깃팅할 이미지를 추가합니다.

   >[!NOTE]
   >
   >AEM Forms에서는 이미지 구성 요소만 타깃팅할 수 있습니다. 이미지 구성 요소를 호스팅하는 패널에 다른 구성 요소가 없는지 확인하고 패널의 열 수가 1로 설정되어 있는지 확인합니다.

1. **편집**&#x200B;에서 **타깃팅** 모드로 전환합니다. 모드를 전환하는 옵션은 오른쪽 위 모서리 근처에 있습니다.
1. **BRAND**&#x200B;을 선택하고 **ACTIVITY**&#x200B;을 선택하고 **타깃팅 시작**&#x200B;을 탭합니다. **대상** 메뉴가 편집기의 오른쪽에 나타납니다.

   ![targeting-menu](assets/targeting-menu.png)

1. **대상** 메뉴에서 대상을 선택하고 타깃팅할 이미지를 누릅니다. 메뉴가 나타납니다. 메뉴에서 **Target**&#x200B;을 누릅니다. 이미지를 누르고 **구성**&#x200B;을 누릅니다. 속성 창에서 선택한 대상에 대해 표시할 이미지를 선택합니다. 모든 대상에 대해 단계를 반복합니다. 경험 타깃팅은 대화형 통신 또는 응용 양식의 이미지에 대해 활성화됩니다.

## 생성된 활동이 Target 서버 {#check-if-the-created-activity-syncs-with-the-target-server}과 동기화되는지 확인합니다.

타깃팅이 Target 서버와 동기화되는 데 사용되는 활동입니다. 활동이 타겟 서버와 동기화되어 있는지 확인하려면 브랜드 페이지에서 활동 상태를 확인하십시오.

활동의 상태가 동기화되었는지 확인합니다.

## Target 동작 유효성 검사 {#validate-target-behavior}

Target 비헤이비어의 유효성을 검사하려면

* 작성자 모드에서 `wcmmode preview`과(와) 함께 타깃팅 사용
* 게시 모드에서 `wcmmode preview` 및 `wcmmode disabled`로 타깃팅을 사용합니다.

## 이미지 구성 요소 {#monitor-targeting-for-the-image-component}에 대한 타깃팅 모니터링

양식에서 이미지 구성 요소에 대한 타깃팅을 모니터링하려면 이미지, 활동 및 적응형 양식을 게시합니다.

## 열기 문제 {#open-issues}

적응형 양식의 대상 이미지에 대한 가시성 표현식을 사용하여 포커스를 설정할 수 없습니다.
