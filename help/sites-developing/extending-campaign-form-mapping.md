---
title: 사용자 지정 양식 매핑 만들기
seo-title: 사용자 지정 양식 매핑 만들기
description: Adobe Campaign에서 사용자 지정 테이블을 만들 때 해당 사용자 지정 테이블로 매핑되는 양식을 AEM에서 만들 수 있습니다
seo-description: Adobe Campaign에서 사용자 지정 테이블을 만들 때 해당 사용자 지정 테이블로 매핑되는 양식을 AEM에서 만들 수 있습니다
uuid: f3bde513-6edb-4eb6-9048-40045ee08c4a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: d5dac1db-2dde-4b75-a31b-e057b447f6e2
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 사용자 지정 양식 매핑 만들기{#creating-custom-form-mappings}

Adobe Campaign에서 사용자 지정 테이블을 만들 때 해당 사용자 지정 테이블로 매핑되는 양식을 AEM에서 만들 수 있습니다.

이 문서에서는 사용자 지정 양식 매핑을 만드는 방법에 대해 설명합니다. 이 문서의 단계를 완료하면 사용자에게 예정된 이벤트에 등록할 수 있는 이벤트 페이지를 제공합니다. 그런 다음 Adobe Campaign을 통해 이러한 사용자를 팔로우합니다.

## 전제 조건 {#prerequisites}

다음을 설치해야 합니다.

* Adobe Experience Manager
* Adobe Campaign Classic

See [Integrating AEM with Adobe Campaign Classic](/help/sites-administering/campaignonpremise.md) for more information.

## 사용자 지정 양식 매핑 만들기 {#creating-custom-form-mappings-2}

사용자 지정 양식 매핑을 만들려면 다음 섹션에 자세히 설명된 상위 수준 단계를 따라야 합니다.

1. 사용자 지정 표를 만듭니다.
1. 시드 **테이블을 확장합니다** .
1. 사용자 정의 매핑을 만듭니다.
1. 사용자 지정 매핑을 기반으로 배달을 만듭니다.
1. 생성된 배달을 사용할 AEM에서 양식을 작성합니다.
1. 테스트할 양식을 제출합니다.

### Adobe Campaign에서 사용자 지정 테이블 만들기 {#creating-the-custom-table-in-adobe-campaign}

먼저 Adobe Campaign에서 사용자 지정 테이블을 만듭니다. 이 예에서는 다음 정의를 사용하여 이벤트 테이블을 만듭니다.

```xml
<element autopk="true" label="Event" labelSingular="Event" name="event">
 <attribute label="Event Date" name="eventdate" type="date"/>
 <attribute label="Event Name" name="eventname" type="string"/>
 <attribute label="Email" name="email" type="string"/>
 <attribute label="Number of Seats" name="seats" type="long"/>
</element>
```

이벤트 테이블을 만든 후 데이터베이스 구조 **업데이트 마법사를** 실행하여 테이블을 만듭니다.

### 시드 테이블 확장 {#extending-the-seed-table}

Adobe Campaign에서 추가를 탭/ **클릭하여** 시드 주소( **nms)** 테이블의 새 확장을 만듭니다.

![chlimage_1-194](assets/chlimage_1-194.png)

이제 **이벤트** 테이블의 필드를 사용하여 **시드** 테이블을 확장합니다.

```xml
<element label="Event" name="custom_cus_event">
 <attribute name="eventname" template="cus:event:event/@eventname"/>
 <attribute name="eventdate" template="cus:event:event/@eventdate"/>
 <attribute name="email" template="cus:event:event/@email"/>
 <attribute name="seats" template="cus:event:event/@seats"/>
 </element>
```

그런 다음 데이터베이스 **업데이트 마법사를** 실행하여 변경 내용을 적용합니다.

### 사용자 지정 타겟 매핑 만들기 {#creating-custom-target-mapping}

관리/ **캠페인**&#x200B;관리에서 타겟 **매핑으로** 이동하여 새&#x200B;**대상 매핑을추가합니다.**

>[!NOTE]
>
>내부 이름에 **의미 있는 이름을 사용해야**&#x200B;합니다.

![chlimage_1-195](assets/chlimage_1-195.png)

### 사용자 지정 배달 템플릿 만들기 {#creating-a-custom-delivery-template}

이 단계에서는 생성된 Target 매핑을 사용하는 배달 템플릿을 **추가합니다**.

리소스/ **템플릿에서**&#x200B;배달 템플릿으로 이동하여 기존 AEM 배달을 복제합니다. [받는 사람] **을**&#x200B;클릭할 때 이벤트 만들기 타겟 **매핑을**&#x200B;선택합니다.

![chlimage_1-196](assets/chlimage_1-196.png)

### AEM에서 양식 작성 {#building-the-form-in-aem}

AEM에서 페이지 속성에 클라우드 서비스를 **구성했는지 확인합니다**.

그런 다음 Adobe **Campaign** 탭에서 사용자 지정 배달 템플릿 만들기에서 만든 [배달을 선택합니다](#creating-a-custom-delivery-template).

![chlimage_1-197](assets/chlimage_1-197.png)

필드를 구성할 때는 양식 필드에 고유한 요소 이름을 지정해야 합니다.

필드를 구성한 후에는 매핑을 수동으로 변경해야 합니다.

CRXDE-lite에서 **jcr:content** (페이지의) 노드로 이동하고 **acMapping** 값을 Target 매핑의 내부 이름으로 **변경합니다**.

![chlimage_1-198](assets/chlimage_1-198.png)

양식 구성에서 확인란을 선택하여 없는 경우 만듭니다

![chlimage_1-199](assets/chlimage_1-199.png)

### 양식 제출 {#submitting-the-form}

이제 양식을 제출하고 값이 저장되었는지 여부를 Adobe Campaign 측에서 확인할 수 있습니다.

![chlimage_1-200](assets/chlimage_1-200.png)

## 문제 해결 {#troubleshooting}

**&quot;@events&#39; 요소의 값 &#39;02/02/2015&#39;에 대한 형식이 잘못되었습니다(문서 형식 &#39;이벤트([adb:event])&#39;).&quot;**

양식을 제출할 때 이 오류는 AEM의 **error.log** 파일에 기록됩니다.

날짜 필드의 형식이 잘못되었기 때문입니다. 해결 방법은 yyyy- **mm-dd** 값을 제공하는 것입니다.

