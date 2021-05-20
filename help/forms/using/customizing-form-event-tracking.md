---
title: 양식 이벤트 추적 사용자 지정
seo-title: 양식 이벤트 추적 사용자 지정
description: 사용자가 한 필드에서 60초 이상을 소비하면 필드 방문 이벤트가 트리거되고 필드의 세부 사항이 Adobe SiteCatalyst으로 전송됩니다.
seo-description: 사용자가 한 필드에서 60초 이상을 소비하면 필드 방문 이벤트가 트리거되고 필드의 세부 사항이 Adobe SiteCatalyst으로 전송됩니다.
uuid: 2f790085-2f1a-45be-9a69-6100c76dcae0
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 60d67c6b-5994-42ef-b159-ed6edf5cf9d4
exl-id: d0280a15-5d0d-49cf-bce9-ad1c40530eae
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 1%

---

# 양식 이벤트 추적 사용자 지정 {#customizing-form-event-tracking}

기본적으로 다음 이벤트는 analytics가 활성화된 적응형 양식에서 추적됩니다.

<table>
 <tbody>
  <tr>
   <th>이벤트</th>
   <th>사용 가능한 변수</th>
  </tr>
  <tr>
   <td>렌더링</td>
   <td>formName, formTitle, formInstance, source</td>
  </tr>
  <tr>
   <td>포기</td>
   <td>formName, formTitle, formInstance, panelName, panelTitle</td>
  </tr>
  <tr>
   <td>저장</td>
   <td>formName, formTitle, formInstance, panelName, source</td>
  </tr>
  <tr>
   <td>제출</td>
   <td>formName, formTitle, formInstance, source</td>
  </tr>
  <tr>
   <td>오류</td>
   <td>formName, formTitle, fieldName, fieldTitle, panelTitle</td>
  </tr>
  <tr>
   <td>도움말</td>
   <td>formName, formTitle, fieldName, fieldTitle, panelTitle</td>
  </tr>
  <tr>
   <td>fieldVisit</td>
   <td>formName, formTitle, fieldName, fieldTitle, panelTitle<br /> </td>
  </tr>
  <tr>
   <td>panelVisit</td>
   <td>formName, formTitle, panelName, panelTitle</td>
  </tr>
 </tbody>
</table>

## 필드 방문 이벤트 시간 제한 사용자 지정 {#customizing-the-field-visit-event-timeout}

기본 AEM 양식 설정에서 사용자가 필드에 60초 이상 보내는 경우 `fieldvisit` 이벤트가 트리거되고 필드의 세부 사항이 Adobe Analytics으로 전송됩니다. AEM 구성 콘솔(/system/console/configMgr)의 AEM Forms Analytics 구성 아래에서 필드 시간 추적 기준을 사용자 지정하여 시간 제한 제한을 늘리거나 줄일 수 있습니다.

## 추적 이벤트 사용자 지정 {#customizing-the-tracking-events}

`/libs/afanalytics/js/custom.js` 파일에서 사용할 수 있는 `trackEvent`함수를 수정하여 이벤트 추적을 사용자 지정할 수 있습니다. 추적되는 이벤트가 적응형 양식에서 발생할 때마다 `trackEvent`함수가 호출됩니다. `trackEvent` 함수에서는 두 개의 매개 변수를 사용할 수 있습니다.`eventName`및 `variableValueMap`.

*eventName* 및 *variableValueMap* 인수의 값을 평가하여 이벤트의 추적 동작을 변경할 수 있습니다. 예를 들어 특정 수의 오류 이벤트가 발생한 후 정보를 analytics 서버로 보내도록 선택할 수 있습니다. 다음 사용자 지정을 수행하도록 선택할 수도 있습니다.

* 이벤트를 보내기 전에 임계값 시간을 설정할 수 있습니다.
* 상태를 유지 관리하여 작업을 결정할 수 있습니다. 예를 들어 *fieldVisit*&#x200B;은(는) 마지막 이벤트의 타임스탬프를 기반으로 더미 이벤트를 푸시합니다.
* `pushEvent` 함수를 사용하여 이벤트를 Analytics 서버 *.*

* 이벤트를 Analytics 서버에 전혀 푸시하지 않도록 선택할 수 있습니다.

### 샘플 {#sample}

다음 예에서는 각 *fieldName* 특성의 *error* 이벤트에 대한 상태가 유지됩니다. 오류가 다시 발생하는 경우에만 이벤트가 Analytics 서버로 전송됩니다.

```javascript
case 'error':
        if(errorOccurred[variableValueMap.fieldName] == true) {
            pushEvent(eventName, variableValueMap)
        }
        errorOccurred[variableValueMap.fieldName] = true;
        break;
```

## 패널 방문 이벤트 사용자 지정 {#customizing-the-panelvisit-event}

기본 AEM Forms 설정에서 60초마다 적응형 양식이 포함된 창이 활성 상태인지 확인합니다. 창이 활성화되어 있으면 `panelVisit`이벤트가 Adobe Analytics으로 트리거됩니다. 문서 또는 양식이 활성 상태인지 확인하고 해당 양식 또는 문서에서 보낸 시간을 계산하는 데 도움이 됩니다.

>[!NOTE]
>
>활동을 가져오고 체류 시간을 계산하는 데 사용되는 이벤트 이름은 &quot;panelVisit&quot;입니다. 이 이벤트는 위에 나열된 표에 나열된 패널 방문 이벤트와 다릅니다.

`/libs/afanalytics/js/custom.js` 파일에서 사용할 수 있는 scheduleHeartBeatCheck 함수를 수정하여 정기적으로 Adobe Analytics으로 전송된 이 이벤트를 변경하거나 중지할 수 있습니다.
