---
title: 작업 또는 양식을 초안으로 저장
seo-title: 작업 또는 양식을 초안으로 저장
description: 작업 또는 양식의 초안 사본을 AEM Forms 앱에 저장하는 절차
seo-description: 작업 또는 양식의 초안 사본을 AEM Forms 앱에 저장하는 절차
uuid: 1192d2c2-05a4-4a96-9015-e56111aa2646
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 9950288c-b5a2-4945-afad-be9ce2abc8e9
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 0%

---


# 작업 또는 양식을 초안 {#saving-a-task-or-form-as-a-draft}으로 저장

초안으로 저장 옵션을 사용하면 작업 또는 양식의 스냅숏과 연결된 양식에 입력된 데이터를 저장할 수 있습니다. 템플릿에서 초안을 만들 수도 있습니다. 초안이 모바일 장치에 저장되고 나중에 검색할 수 있도록 Adobe Experience Manager Forms 서버와 동기화됩니다.

[양식](/help/forms/using/working-with-form.md), [에 사진 및 스크리블 메모와 함께 주석을 추가할 수 있습니다. ](/help/forms/using/add-attachments.md) 양식을 계속 업데이트하면 초안으로 저장하는 것이 좋습니다. 나중에 작성한 양식을 제출하기로 결정한 경우 초안으로 저장하는 것이 도움이 됩니다.

양식 포털에 저장된 양식에 대한 초안 기능으로 저장을 활성화하려면 [HTML5 양식을 초안](/help/forms/using/saving-html5-form-draft.md)으로 저장을 참조하십시오.
적응형 양식의 제출을 구성하려면 [초안 및 제출 구성 요소](/help/forms/using/draft-submission-component.md)을 참조하십시오. (AEM Forms JEE 서버와 동기화된 양식은 사용할 수 없습니다.)

초안을 만들려면 양식을 열고 **Save as Draft** ![save-as-draft](assets/save-as-draft.png)를 누릅니다. 초안 이름을 입력하고 **저장**&#x200B;을 누릅니다. 초안이 초안 폴더에 저장되고 서버와 동기화됩니다. 앱이 오프라인 상태인 경우 보낼 편지함 폴더에 저장됩니다.

이후 해당 양식을 업데이트하면 변경 내용이 즉시 반영됩니다. AEM Forms 앱을 AEM Forms 서버와 동기화할 때 초안이 AEM Forms 서버에 업로드됩니다. 또한 초안이 보낼 편지함에서 작업 또는 초안 폴더로 이동합니다. 편집 아이콘이 그 옆에 표시됩니다.

여러 작업 및 시작점 작업을 계속 수행하고 저장하므로 초안이 저장됩니다. 앱이 AEM Forms 서버와 동기화될 때마다 초안이 서버에 저장됩니다. 이렇게 하면 언제든지 마지막으로 저장한 날짜와 시간을 기준으로 초안을 복구할 수 있습니다. 예를 들어 앱을 다시 설치하거나 모바일 장치를 변경하는 경우 서버에서 초안을 다운로드할 수 있습니다.

## 초안 삭제 {#delete-a-draft}

초안 폴더에는 모든 초안이 나열됩니다. 초안 삭제 옵션을 사용하여 모바일 장치 및 서버에서 초안을 영구적으로 삭제할 수 있습니다.

작업에서 만든 초안을 삭제하는 옵션은 사용할 수 없습니다. 작업에서 생성된 초안을 삭제하면 작업이 중단됩니다.

오프라인 모드와 온라인 모드 모두에서 초안을 취소할 수 있습니다. 오프라인 모드에서 초안을 폐기하면 서버와의 연결이 복구될 때만 서버에서 초안이 삭제됩니다.

초안을 삭제하려면 다음 단계를 수행하십시오.

1. AEM Forms 앱에서 **Forms으로 이동합니다.**
1. 검색 옆의 드롭다운에서 **초안**&#x200B;을 선택합니다.
1. 편집 아이콘 ![edit-draft-app](assets/edit-draft-app.png)이 있는 양식은 초안을 나타냅니다. 초안 옆에 있는 가로 줄임표를 누릅니다.
1. 수평 줄임표를 누를 때 나타나는 옵션에서 **초안 삭제**&#x200B;을 누릅니다.
