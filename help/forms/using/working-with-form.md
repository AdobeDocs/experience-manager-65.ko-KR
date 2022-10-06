---
title: 양식 작업
seo-title: Working with a Form
description: AEM Forms 앱의 작업 또는 시작점과 연관된 양식을 보고 업데이트합니다
seo-description: View and update the form associated with a task or Startpoint in the AEM Forms app
uuid: 7481ca5c-a2c0-4697-9008-1e51bce2012e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 8a5e038e-b39a-41de-88a0-47642e5bd5bf
exl-id: adff5339-e026-4924-a401-f249f37fc6e6
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---

# 양식 작업 {#working-with-a-form}

양식 앱에서 동기화를 위해 양식이 활성화된 경우 양식이 다운로드되며 직접 작업할 수 있습니다.

양식은 앱에서 다운로드되며 오프라인에서 사용할 수 있습니다. 예를 들어, 은행 회사를 운영하고 있으며 고객이 귀하의 사이트에서 애플리케이션을 채우는 경우를 들 수 있습니다. 응용 프로그램은 고객의 정보를 받아 검토용으로 저장하는 적응형 양식입니다. 관리자는 양식을 검토하고 AEM 작성자 인스턴스에서 확인 양식을 만듭니다. 관리자는 AEM Forms 앱과 양식을 동기화할 수 있습니다. AEM Forms 앱에서 확인 양식을 사용할 수 있는 경우 필드 에이전트는 모바일 장치를 사용하여 고객의 세부 사항을 확인할 수 있습니다. 모바일 장치가 서버와 동기화되고 확인 양식이 앱에 로드됩니다. 필드 에이전트가 고객을 방문하여 세부 정보를 확인하거나 데이터를 초안으로 저장하거나 확인 양식을 제출할 수 있습니다. 앱이 온라인 상태일 때마다 양식이 서버와 동기화됩니다.

AEM Forms 앱에서 양식을 동기화하려면 다음을 수행하십시오.

1. 작성자 인스턴스에서 양식을 선택하고 **속성 보기**.
1. 속성 페이지에서 **고급.**
1. 고급 아래에서 옵션을 활성화합니다. **AEM Forms 앱과 동기화**, 탭 **저장**.

여러 양식을 동기화하려면 작성자 인스턴스에서 Forms Manager에서 여러 양식을 선택하고 **AEM Forms 앱과 동기화**. 양식이 게시되면 AEM Forms 앱은 게시 서버에 연결하고 양식을 가져올 수 있습니다.

>[!NOTE]
>
>지원되는 양식:
>
>* 적응형 양식(지연 로드 없음)
>* 모바일 양식
>
>AEM Forms OSGi 서버와 동기화된 AEM Forms 앱에서 가져온 적응형 양식에서는 양식 수준 첨부 파일이 지원되지 않습니다. 작성자가 양식을 작성할 때 필드 수준의 첨부 파일을 활성화한 경우 사용자는 필드에 파일을 첨부할 수 있습니다.

**양식을 열고 업데이트하려면**

1. 양식을 열려면 홈 화면에서 양식을 탭합니다.
1. 양식의 필드를 업데이트하고 첨부 파일을 추가하고 초안으로 저장하고 제출할 수 있습니다.
