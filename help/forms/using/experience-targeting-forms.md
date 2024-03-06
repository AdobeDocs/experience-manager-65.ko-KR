---
title: AEM Forms에서 타깃팅된 경험 만들기
description: AEM Forms의 Target을 사용하여 타깃팅된 고객을 위한 사용자 지정된 경험을 만듭니다.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
exl-id: fdc91054-3f7e-4cbf-bdfa-7d7a621747f1
source-git-commit: 9d497413d0ca72f22712581cf7eda1413eb8d643
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 0%

---

# AEM Forms에서 타깃팅된 경험 만들기 {#create-targeted-experiences-in-aem-forms}

## Adobe Target과 AEM Forms 통합 {#integrate-adobe-target-with-aem-forms}

AEM과 통합된 Adobe Target을 통해 타겟 대상에 맞게 사용자 지정된 경험을 만들 수 있습니다. Adobe Target을 사용하면 A/B 테스트를 만들고, 사용자 응답을 측정하고, 타깃팅된 사용자에 대한 사용자 지정 웹 컨텐츠를 생성할 수 있습니다. Adobe Target을 AEM Forms과 통합하여 적응형 양식 및 대화형 커뮤니케이션의 이미지 구성 요소를 타겟팅할 수 있습니다.

적응형 양식 및 대화형 통신과 함께 사용하도록 AEM에서 Adobe Target을 구성합니다. 다음을 참조하십시오. [AEM에서 Target 구성 만들기](/help/sites-administering/target.md) 및 [프레임워크 추가](/help/sites-administering/target.md).

>[!NOTE]
>
>타겟팅은 적응형 양식 또는 대화형 통신이 호스트 이름 또는 IP 주소를 사용하여 렌더링될 때 작동합니다. 적응형 양식 또는 대화형 통신이 localhost를 사용하여 렌더링되면 실패합니다.

## Target 활동 만들기 {#creating-a-target-activity}

1. 선택 **Adobe Experience Manager > 개인화 > 활동**.

   `https://<hostname>:<port>/libs/cq/personalization/touch-ui/content/v2/activities.html`

1. 활동 페이지에서 을 선택합니다 **만들기 > 브랜드 만들기**.
1. 템플릿을 선택하고 속성을 입력하라는 메시지가 표시됩니다.

   템플릿을 선택하고 **다음.** 속성 섹션에 브랜드 제목을 입력하고 다음을 선택합니다. **만들기.**
이제 브랜드가 활동 페이지에 나열됩니다.

1. 활동 페이지에서 브랜드를 선택합니다.
1. 브랜드의 기본 영역에서 을 선택합니다. **만들기** > **활동 만들기**.

   활동을 만들 때 세부 사항, 대상 및 설정을 지정합니다.

   세부 정보 섹션에는 이름, 타겟팅 엔진 및 목표가 포함됩니다. 타겟팅 엔진으로 Adobe Target을 선택하면 Target 클라우드 구성 옵션이 활성화됩니다. Target 클라우드 구성을 선택하고 활동 유형을 선택한 다음, 활동의 목표를 입력하고 을 선택합니다. **다음**. 대화형 커뮤니케이션은 경험 타깃팅 활동 유형만 지원합니다.

   타겟 섹션에서 대상 경험을 추가하고 이름을 지정할 수 있습니다. 클릭 **경험 추가** 을(를) 활성화하려면 **대상 선택** 및 **이름 환경** 옵션. 선택 **대상 선택** 대상 및 해당 소스 목록을 봅니다. 대상자 이름 목록에서 대상자를 선택합니다. 선택 **경험 추가** 을 클릭하여 경험에 이름을 지정하고 **다음**.

   목표 및 설정 섹션을 통해 활동을 예약하고 활동의 우선 순위를 지정할 수 있습니다. 활동의 시작 날짜, 종료 날짜 및 우선 순위, 목표 지표, 추가 지표를 설정하고 을 선택합니다. **저장**.

   이제 활동이 브랜드 페이지에 나열됩니다.

   >[!NOTE]
   >
   >&quot;활동이 저장되었지만 Target에 동기화되지 않았습니다. 이유: 다음 경험에는 오퍼가 없습니다.&quot;(활동 저장 시 발생한 경우)

1. Target을 활성화하려면 적응형 양식 템플릿에서 사용하는 클라이언트 라이브러리를 포함하도록 .jsp 파일을 편집합니다.

   예를 들어 기본 구현에서 **도구** >  **CRXDE Lite**.

   CRXDE Lite 주소 표시줄에 /libs/fd/af/components/page/base/head.jsp을 입력하여 head.jsp 파일을 편집합니다.

   이 구현에서는 simpleEnrollment 템플릿을 사용합니다. 이 구현에서 다음 클라이언트 라이브러리를 포함하도록 head.jsp 파일을 수정합니다.

   `<cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>`

   `<cq:include path="clientcontext_optimized" resourceType="/libs/cq/personalization/components/clientcontext_optimized"/>`

   `<cq:include path="config" resourceType="cq/personalization/components/clientcontext_optimized/config"/>`

1. 적응형 양식에 대한 대상 프레임워크를 활성화하려면 양식 또는 대화형 통신으로 이동하여 편집 모드로 엽니다.

   편집 모드에서 양식 또는 대화형 통신을 열려면 다음을 선택합니다. **선택** 다음을 선택합니다. **열기**.

   또는 양식 또는 대화형 통신 아이콘을 선택하지 않고 포인터를 이동하면 네 개의 단추가 나타납니다. 다음을 선택할 수 있습니다. **편집** 단추를 클릭하여 양식을 편집 모드로 엽니다.

1. 페이지 도구 모음에서 를 선택합니다 **페이지 정보** ![theme-options](assets/theme-options.png) > **속성 열기**.
1. 일반 탭에서 다음에 대한 구성을 선택합니다 **Adobe Target** 필드. **저장 후 닫기**&#x200B;를 선택합니다.

## 만들어진 활동을 적응형 양식 이미지 또는 대화형 통신 이미지에 적용 {#applying-created-activity-to-an-adaptive-form-image-or-an-interactive-communication-image}

1. 편집할 적응형 양식 및 대화형 커뮤니케이션을 엽니다. 대화형 통신을 여는 경우 웹 채널을 엽니다.

1. 대화형 통신 또는 적응형 양식의 작성 모드에서 타깃팅할 이미지를 추가합니다.

   >[!NOTE]
   >
   >AEM Forms에서는 이미지 구성 요소만 타깃팅할 수 있습니다. 이미지 구성 요소를 호스팅하는 패널에 다른 구성 요소가 없는지, 그리고 패널의 열 수가 1로 설정되어 있는지 확인하십시오.

1. 다음에서 전환 **편집** 끝 **타겟팅** 모드. 모드를 전환하는 옵션은 오른쪽 상단 모서리 근처에 있습니다.
1. 선택 **브랜드**, 선택 **활동**, 및 선택 **타깃팅 시작**. 다음 **대상** 편집기 오른쪽에 메뉴가 나타납니다.

   ![타깃팅 메뉴](assets/targeting-menu.png)

1. 에서 대상자 선택 **대상** 을 클릭하고 타깃팅할 이미지를 선택합니다. 메뉴가 나타납니다. 메뉴에서 다음을 선택합니다. **Target**. 이미지를 선택하고 **구성**. 속성 창에서 선택한 대상자에 대해 표시할 이미지를 선택합니다. 모든 대상에 대해 단계를 반복합니다. 경험 타깃팅은 대화형 통신 또는 적응형 양식의 이미지에 대해 활성화됩니다.

## 작성된 활동이 Target 서버와 동기화되는지 확인 {#check-if-the-created-activity-syncs-with-the-target-server}

Target 서버와 동기화되는 타겟팅에 사용되는 활동입니다. 활동이 대상 서버와 동기화되는지 확인하려면 브랜드 페이지에서 활동의 상태를 확인하십시오.

활동의 상태가 동기화됨인지 확인합니다.

## Target 동작 유효성 검사 {#validate-target-behavior}

Target 동작의 유효성을 검사하려면 다음을 수행하십시오.

* 타깃팅 사용 `wcmmode preview` 작성자 모드에서
* 타깃팅 사용 `wcmmode preview` 및 `wcmmode disabled` 게시 모드에서

## 이미지 구성 요소에 대한 타겟팅 모니터링 {#monitor-targeting-for-the-image-component}

양식의 이미지 구성 요소에 대한 타겟팅을 모니터링하려면 이미지, 활동 및 적응형 양식을 게시하십시오.

## 미해결 문제 {#open-issues}

적응형 양식의 타깃팅된 이미지에 대한 가시성 표현식, 설정 포커스 오류.
