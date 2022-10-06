---
title: 모바일 디바이스용 페이지 작성
seo-title: Authoring a Page for Mobile Devices
description: 모바일 페이지를 작성할 때는 모바일 디바이스를 에뮬레이션하는 방식으로 페이지가 표시됩니다. 페이지를 작성할 때에는 몇 개의 에뮬레이터 간을 전환하여 페이지에 액세스할 때 최종 사용자에게 표시되는 내용을 확인할 수 있습니다.
seo-description: When authoring a mobile page, the page is displayed in a way that emulates the mobile device. When authoring the page, you can switch between several emulators to see what the end-user sees when accessing the page.
uuid: ca16979d-6e5f-444d-b959-ae92542039b2
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 430a27b5-f344-404f-8bf8-0d91b49b605e
exl-id: d5372474-d8aa-4e64-919d-0bd29ba99d99
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 82%

---

# 모바일 디바이스용 페이지 작성{#authoring-a-page-for-mobile-devices}

모바일 페이지를 작성할 때는 모바일 디바이스를 에뮬레이션하는 방식으로 페이지가 표시됩니다. 페이지를 작성할 때에는 몇 개의 에뮬레이터 간을 전환하여 페이지에 액세스할 때 최종 사용자에게 표시되는 내용을 확인할 수 있습니다.

디바이스는 페이지를 렌더링할 디바이스의 기능에 따라 카테고리 기능, 스마트와 터치로 그룹화됩니다. 최종 사용자가 모바일 페이지에 액세스하면 AEM이 디바이스를 감지하여 디바이스 그룹에 해당하는 표현 데이터를 전송합니다.

>[!NOTE]
>
>기존 표준 사이트를 기반으로 모바일 사이트를 만들려면 표준 사이트의 Live Copy를 만드십시오. (자세한 내용은 [다른 채널용 Live Copy 만들기](/help/sites-administering/msm-livecopy.md))
>
>AEM 개발자는 새 디바이스 그룹을 만들 수 있습니다. (자세한 내용은 [장치 그룹 필터 만들기](/help/sites-developing/groupfilters.md))

다음 절차를 사용하여 모바일 페이지를 작성하십시오.

1. 브라우저에서 **Siteadmin** 콘솔로 이동합니다.
1. 를 엽니다. **제품** 아래의 페이지 **웹 사이트** >> **Geometrixx 모바일 데모 사이트** >> **영어**.

1. 다른 에뮬레이터로 전환합니다. 다음 방법 중 하나를 사용합니다.

   * 페이지 상단의 장치 아이콘을 클릭합니다.
   * **사이드킥**&#x200B;에서 **편집** 단추를 클릭하고 드롭다운 메뉴에서 장치를 선택합니다.

1. 을(를) 끌어다 놓습니다 **텍스트 및 이미지** 구성 요소를 생성하지 않습니다.
1. 구성 요소를 편집하고 텍스트를 추가합니다. **확인**&#x200B;을 클릭하여 변경 사항을 저장합니다.

페이지가 다음과 같이 표시됩니다.

![mobileipademu](assets/mobileipademu.png)

>[!NOTE]
>
>모바일 디바이스에서 작성 인스턴스의 페이지를 요청하면 에뮬레이터가 비활성화됩니다. 그런 다음 터치 지원 UI를 사용하여 작성을 수행할 수 있습니다.
