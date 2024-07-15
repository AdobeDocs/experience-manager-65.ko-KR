---
title: 양식 작업
description: AEM Forms 앱에서 작업 또는 시작 지점과 연결된 양식을 보고 업데이트합니다
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: adff5339-e026-4924-a401-f249f37fc6e6
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 0%

---

# 양식 작업 {#working-with-a-form}

양식 앱에서 양식을 동기화할 수 있는 경우 양식이 다운로드되므로 직접 작업할 수 있습니다.

양식은 앱에서 다운로드되고 오프라인에서 사용할 수 있습니다. 예를 들어, 은행 회사를 운영하고 있는 경우, 고객이 사이트에서 애플리케이션을 작성합니다. 애플리케이션은 고객의 정보를 수락하고 검토를 위해 저장하는 적응형 양식입니다. 관리자가 양식을 검토하고 AEM 작성자 인스턴스에서 확인 양식을 만듭니다. 관리자는 양식을 AEM Forms 앱과 동기화할 수 있습니다. AEM Forms 앱에서 확인 양식을 사용할 수 있는 경우 필드 에이전트는 모바일 장치를 사용하여 고객의 세부 정보를 확인할 수 있습니다. 모바일 장치가 서버와 동기화되고 확인 양식이 앱에 로드됩니다. 현장 상담원은 고객을 방문하여 세부 정보를 확인하거나 데이터를 초안으로 저장하거나 확인 양식을 제출할 수 있습니다. 앱은 온라인 상태일 때마다 양식이 서버와 동기화됩니다.

AEM Forms 앱에서 양식을 동기화하려면:

1. 작성자 인스턴스에서 양식을 선택하고 **속성 보기**&#x200B;를 클릭합니다.
1. 속성 페이지에서 **고급**&#x200B;을 클릭합니다.
1. [고급]에서 옵션 **AEM Forms 앱과 동기화**&#x200B;를 사용하도록 설정하고 **저장**&#x200B;을 선택합니다.

작성자 인스턴스에서 여러 양식을 동기화하려면 Forms Manager에서 여러 양식을 선택하고 **AEM Forms 앱과 동기화**&#x200B;를 선택합니다. 양식이 게시되면 AEM Forms 앱에서 게시 서버에 연결하여 양식을 가져올 수 있습니다.

AFA(AEM Form Application) Android 앱이 동기화되지 않을 경우 다음 단계를 수행하여 동기화 문제를 해결합니다.

1. **https://[server]:[port]/system/console/configMgr**(으)로 이동합니다.
1. **[!UICONTROL Adobe Granite 토큰 인증 처리기]**&#x200B;를 검색하고 **[!UICONTROL 편집]**&#x200B;을(를) 클릭합니다.
1. 로그인 토큰 쿠키&#x200B;]**특성에 대한**[!UICONTROL  SameSite 특성에 대한 드롭다운 메뉴에서 **[!UICONTROL 없음]** 옵션을 선택합니다.
1. **[!UICONTROL 저장]**&#x200B;을 클릭합니다.

![AFA Android 앱과 이미지 동기화](/help/forms/using/assets/afaandroid.png)

>[!NOTE]
>
>지원되는 양식:
>
>* 적응형 양식(소극적 로드 없음)
>* 모바일 양식
>
>양식 수준 첨부 파일은 AEM Forms OSGi 서버와 동기화된 AEM Forms 앱에서 가져온 적응형 양식에서 지원되지 않습니다. 사용자는 작성자가 양식 작성 시 필드 수준의 첨부 파일을 활성화한 경우 필드에 파일을 첨부할 수 있습니다.


**양식을 열고 업데이트하려면**

1. 양식을 열려면 홈 화면에서 **[!UICONTROL 양식]**&#x200B;을 선택합니다.
1. 양식의 필드를 업데이트하고, 첨부 파일을 추가하고, 초안으로 저장하고, 제출할 수 있습니다.
