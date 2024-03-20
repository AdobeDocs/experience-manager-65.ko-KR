---
title: 사용자 정의 양식 매핑 만들기
description: Adobe Campaign에서 사용자 지정 테이블을 만들 때 해당 사용자 지정 테이블에 매핑되는 양식을 AEM에서 빌드할 수 있습니다
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: bce6c586-9962-4217-82cb-c837e479abc0
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 3%

---

# 사용자 정의 양식 매핑 만들기{#creating-custom-form-mappings}

Adobe Campaign에서 사용자 지정 테이블을 만들 때 해당 사용자 지정 테이블에 매핑되는 양식을 AEM에서 빌드할 수 있습니다.

이 문서에서는 사용자 정의 양식 매핑을 만드는 방법을 설명합니다. 이 문서의 단계를 완료하면 다가오는 이벤트에 등록할 수 있는 이벤트 페이지를 사용자에게 제공합니다. 그런 다음 Adobe Campaign을 통해 이러한 사용자를 후속 조치합니다.

## 사전 요구 사항 {#prerequisites}

다음을 설치해야 합니다.

* Adobe Experience Manager
* Adobe Campaign Classic

다음을 참조하십시오 [AEM과 Adobe Campaign Classic 통합](/help/sites-administering/campaignonpremise.md) 추가 정보.

## 사용자 정의 양식 매핑 만들기 {#creating-custom-form-mappings-2}

사용자 정의 양식 매핑을 생성하려면 다음 섹션에 자세히 설명되어 있는 이러한 높은 수준의 단계를 수행해야 합니다.

1. 사용자 지정 테이블을 만듭니다.
1. 확장 **시드** 테이블.
1. 사용자 지정 매핑을 만듭니다.
1. 사용자 지정 매핑을 기반으로 게재를 만듭니다.
1. 생성된 게재를 사용할 AEM에서 양식을 작성합니다.
1. 테스트할 양식을 제출합니다.

### Adobe Campaign에서 사용자 지정 테이블 만들기 {#creating-the-custom-table-in-adobe-campaign}

Adobe Campaign에서 사용자 지정 테이블을 만들어 시작합니다. 이 예제에서는 다음 정의를 사용하여 이벤트 테이블을 만듭니다.

```xml
<element autopk="true" label="Event" labelSingular="Event" name="event">
 <attribute label="Event Date" name="eventdate" type="date"/>
 <attribute label="Event Name" name="eventname" type="string"/>
 <attribute label="Email" name="email" type="string"/>
 <attribute label="Number of Seats" name="seats" type="long"/>
</element>
```

이벤트 테이블을 만든 후 **데이터베이스 구조 업데이트 마법사** 를 클릭하여 테이블을 생성합니다.

### 시드 테이블 확장 {#extending-the-seed-table}

Adobe Campaign에서 **추가** 의 확장을 만들려면 **시드 주소(nms)** 테이블.

![chlimage_1-194](assets/chlimage_1-194.png)

이제 **이벤트** 표 확장 **시드** 표:

```xml
<element label="Event" name="custom_cus_event">
 <attribute name="eventname" template="cus:event:event/@eventname"/>
 <attribute name="eventdate" template="cus:event:event/@eventdate"/>
 <attribute name="email" template="cus:event:event/@email"/>
 <attribute name="seats" template="cus:event:event/@seats"/>
 </element>
```

이 작업 후 실행 **데이터베이스 업데이트 마법사** 를 눌러 변경 사항을 적용합니다.

### 사용자 지정 대상 매핑 만들기 {#creating-custom-target-mapping}

위치 **관리/캠페인 관리** t, 다음으로 이동 **대상 매핑** 새 T 추가&#x200B;**매핑 가져오기.**

>[!NOTE]
>
>에 대해 의미 있는 이름을 사용해야 합니다. **내부 이름**.

![chlimage_1-195](assets/chlimage_1-195.png)

### 사용자 지정 게재 템플릿 만들기 {#creating-a-custom-delivery-template}

이 단계에서는 생성된 를 사용하는 게재 템플릿을 추가합니다 **대상 매핑**.

위치 **리소스/템플릿**&#x200B;에서 게재 템플릿으로 이동하고 기존 AEM 게재를 복제합니다. 다음을 클릭: **종료**, 이벤트 만들기 선택 **대상 매핑**.

![chlimage_1-196](assets/chlimage_1-196.png)

### AEM에서 양식 작성 {#building-the-form-in-aem}

AEM에서에 Cloud Service을 구성했는지 확인합니다. **페이지 속성**.

그런 다음 **Adobe Campaign** 탭에서 만든 게재를 선택합니다. [사용자 지정 게재 템플릿 만들기](#creating-a-custom-delivery-template).

![chlimage_1-197](assets/chlimage_1-197.png)

필드를 구성할 때는 양식 필드에 고유한 요소 이름을 지정해야 합니다.

필드가 구성된 후 매핑을 수동으로 변경해야 합니다.

CRXDE-lite에서 **jcr:content** (페이지의) 노드 및 변경 **acMapping** 값을 의 내부 이름으로 **대상 매핑**.

![chlimage_1-198](assets/chlimage_1-198.png)

양식 구성에서 존재하지 않는 경우 작성하려면 확인란을 선택해야 합니다

![chlimage_1-199](assets/chlimage_1-199.png)

### 양식 제출 {#submitting-the-form}

이제 양식을 제출하고 Adobe Campaign 측에서 값이 저장되었는지 여부를 확인할 수 있습니다.

![chlimage_1-200](assets/chlimage_1-200.png)

## 문제 해결 {#troubleshooting}

**&quot;요소 &#39;@eventdate&#39;의 값 &#39;02/02/2015&#39; 형식이 잘못되었습니다(&#39;Event(&#39; 형식의 문서).[adb:event])&#39;)&quot;**

양식을 제출할 때 이 오류는 **error.log** AEM.

날짜 필드의 형식이 잘못되었기 때문입니다. 해결 방법은 를 제공하는 것입니다. **yyyy-mm-dd** 을 값으로 추가합니다.
