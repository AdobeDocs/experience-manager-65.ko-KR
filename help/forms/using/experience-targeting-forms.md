---
title: AEM Forms에서 타깃팅된 경험 만들기
seo-title: AEM Forms에서 타깃팅된 경험 만들기
description: AEM Forms의 Target을 사용하여 타깃팅된 고객을 위한 사용자 지정된 경험을 만듭니다.
seo-description: AEM Forms의 Target을 사용하여 타깃팅된 고객을 위한 사용자 지정된 경험을 만듭니다.
uuid: 174b6054-8fe3-4ab2-8afd-435e5dff9044
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: 6cf54a08-d429-4a58-8429-a1cb784448d1
exl-id: fdc91054-3f7e-4cbf-bdfa-7d7a621747f1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 0%

---

# AEM Forms {#create-targeted-experiences-in-aem-forms}에서 타깃팅된 경험을 만듭니다

## Adobe Target과 AEM Forms 통합 {#integrate-adobe-target-with-aem-forms}

AEM과 통합된 Adobe Target을 사용하여 타겟 대상에 대해 사용자 지정된 경험을 만들 수 있습니다. Adobe Target을 사용하면 A/B 테스트를 만들고, 사용자 응답을 측정하며, 타깃팅된 사용자를 위한 사용자 지정 웹 컨텐츠를 생성할 수 있습니다. Adobe Target을 AEM Forms과 통합하여 적응형 양식 및 대화형 커뮤니케이션의 이미지 구성 요소를 타깃팅할 수 있습니다.

적응형 양식 및 대화형 커뮤니케이션에서 사용하도록 AEM에서 Adobe Target을 구성하십시오. 자세한 내용은 [AEM](/help/sites-administering/target.md)에서 Target 구성 만들기 및 [프레임워크 추가](/help/sites-administering/target.md)를 참조하십시오.

>[!NOTE]
>
>타깃팅은 적용형 양식 또는 대화형 커뮤니케이션이 호스트 이름 또는 IP 주소를 사용하여 렌더링될 때 작동합니다. 적응형 양식 또는 대화형 커뮤니케이션이 localhost를 사용하여 렌더링되면 실패합니다.

## Target 활동 만들기 {#creating-a-target-activity}

1. **Adobe Experience Manager > 개인화 > 활동**&#x200B;을 누릅니다.

   `https://<hostname>:<port>/libs/cq/personalization/touch-ui/content/v2/activities.html`

1. 활동 페이지에서 **만들기 > 브랜드 만들기**&#x200B;를 탭합니다.
1. 템플릿을 선택하고 속성을 입력하라는 메시지가 표시됩니다.

   템플릿을 선택하고 **다음 을 누릅니다.** 속성 섹션에서 브랜드의 제목을 입력하고 만들기 를  **탭합니다.**
이제 브랜드가 활동 페이지에 나열됩니다.

1. 활동 페이지에서 브랜드를 탭합니다.
1. 브랜드의 기본 영역에서 **만들기** > **활동 만들기**&#x200B;를 탭합니다.

   활동을 만들 때 세부 사항, 타겟 및 설정을 지정합니다.

   세부 사항 섹션에는 이름, 타깃팅 엔진 및 목표가 포함되어 있습니다. 타깃팅 엔진으로 Adobe Target을 선택하면 Target 클라우드 구성 옵션이 활성화됩니다. Target 클라우드 구성을 선택하고 활동 유형을 선택하고 활동의 목표를 제공한 다음 **다음**&#x200B;을 누릅니다. 대화형 커뮤니케이션은 경험 타깃팅 활동 유형만 지원합니다.

   Target 섹션에서 대상 경험을 추가하고 이름을 지정할 수 있습니다. **경험 추가**&#x200B;를 클릭하여 **대상 선택** 및 **경험 이름 지정** 옵션을 활성화합니다. **대상 선택**&#x200B;을 탭하여 대상자 목록과 해당 소스를 확인합니다. 대상 이름 목록에서 대상을 선택합니다. **경험 추가**&#x200B;를 탭하고 경험 이름을 **다음**&#x200B;을 탭합니다.

   목표 및 설정 섹션에서 활동을 예약하고 우선 순위를 지정할 수 있습니다. 활동의 시작 날짜, 종료 날짜 및 우선 순위, 목표 지표, 추가 지표를 설정하고 **저장**&#x200B;을 탭합니다.

   이제 활동이 브랜드 페이지에 나열됩니다.

   >[!NOTE]
   >
   >활동이 저장되었지만 Target과 동기화되지 않았다는 오류를 무시할 수 있습니다. 이유:다음 경험에 &quot;오퍼가 없습니다.&quot;가 있어야 합니다.

1. target을 활성화하려면 적응형 양식 서식 파일에서 사용하는 클라이언트 라이브러리를 포함하도록 .jsp 파일을 편집합니다.

   예를 들어, 기본 구현에서 **도구** > **CRXDE Lite**&#x200B;을 클릭합니다.

   CRXDE Lite 주소 표시줄에 /libs/fd/af/components/page/base/head.jsp 를 입력하여 head.jsp 파일을 편집합니다.

   이 구현에서는 simpleRegistration 템플릿을 사용합니다. 이 구현에서 다음 클라이언트 라이브러리를 포함하도록 head.jsp 파일을 수정합니다.

   `<cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>`

   `<cq:include path="clientcontext_optimized" resourceType="/libs/cq/personalization/components/clientcontext_optimized"/>`

   `<cq:include path="config" resourceType="cq/personalization/components/clientcontext_optimized/config"/>`

1. 적응형 양식의 target 프레임워크를 활성화하려면 양식 또는 대화형 커뮤니케이션으로 이동한 다음 편집 모드에서 엽니다.

   편집 모드에서 폼이나 대화형 커뮤니케이션을 열려면 **선택**&#x200B;을 누른 다음 **열기**&#x200B;를 탭합니다.

   또는 포인터를 폼이나 대화형 통신 아이콘 위로 가져가면 포인터를 선택하지 않고 단추 4개가 나타납니다. 표시되는 **편집** 단추를 탭하여 편집 모드로 양식을 열 수 있습니다.

1. 페이지 도구 모음에서 **페이지 정보** ![테마-옵션](assets/theme-options.png) > **속성 열기**&#x200B;를 누릅니다.
1. 일반 탭에서 **Adobe Target** 필드에 대한 구성을 선택합니다. **저장 및 닫기**&#x200B;를 누릅니다.

## 생성된 활동을 적응형 양식 이미지 또는 대화형 통신 이미지 {#applying-created-activity-to-an-adaptive-form-image-or-an-interactive-communication-image}에 적용

1. 편집할 적응형 양식 및 대화형 커뮤니케이션을 엽니다. 대화형 커뮤니케이션을 여는 경우 웹 채널을 엽니다.

1. 대화형 통신 또는 적응형 양식의 작성 모드에서 타깃팅할 이미지를 추가합니다.

   >[!NOTE]
   >
   >AEM Forms은 이미지 구성 요소만 타깃팅할 수 있습니다. 이미지 구성 요소를 호스팅하는 패널에 다른 구성 요소가 없는지, 패널에 대한 열 수가 1로 설정되어 있는지 확인합니다.

1. **편집**&#x200B;에서 **타깃팅** 모드로 전환합니다. 모드를 전환하는 옵션이 오른쪽 상단 모서리 근처에 있습니다.
1. **BRAND**&#x200B;을(를) 선택하고 **ACTIVITY**&#x200B;를 선택한 다음 **타깃팅 시작**&#x200B;을(를) 탭합니다. **대상** 메뉴가 편집기의 오른쪽에 나타납니다.

   ![타깃팅 메뉴](assets/targeting-menu.png)

1. **대상** 메뉴에서 대상을 선택하고 타깃팅할 이미지를 탭합니다. 메뉴가 나타납니다. 메뉴에서 **Target**&#x200B;을 누릅니다. 이미지를 탭하고 **구성**&#x200B;을 탭합니다. 속성 창에서 선택한 대상에 대해 표시할 이미지를 선택합니다. 모든 대상에 대해 단계를 반복합니다. 경험 타깃팅은 대화형 통신 또는 적응형 양식의 이미지에 대해 활성화됩니다.

## 생성된 활동이 Target 서버 {#check-if-the-created-activity-syncs-with-the-target-server}과 동기화되는지 확인합니다

타깃팅에 사용되는 활동이 Target 서버와 동기화됩니다. 활동이 Target 서버와 동기화되어 있는지 확인하려면 브랜드 페이지에서 활동의 상태를 확인하십시오.

활동의 상태가 동기화되었는지 확인합니다.

## Target 동작 확인 {#validate-target-behavior}

Target 동작의 유효성을 검사하려면

* 작성자 모드에서 `wcmmode preview`으로 타깃팅 사용
* 게시 모드에서 `wcmmode preview` 및 `wcmmode disabled`과 함께 타깃팅을 사용합니다

## 이미지 구성 요소 {#monitor-targeting-for-the-image-component}에 대한 모니터 타깃팅

양식에 있는 이미지 구성 요소에 대한 타깃팅을 모니터링하려면 이미지, 활동 및 적응형 양식을 게시합니다.

## 열기 문제 {#open-issues}

가시성 표현식, 적응형 양식의 타깃팅된 이미지에 대한 설정 포커스가 실패합니다.
