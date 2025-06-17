---
title: SPA에 대한 React 구성 요소 구현
description: 이 문서에서는 간단한 기존 React 구성 요소를 Adobe Experience Manager(AEM) SPA 편집기에서 작동하도록 조정하는 방법에 대한 예를 제공합니다.
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
docset: aem65
exl-id: f4959c12-54c5-403a-9973-7a4ab5f16bed
solution: Experience Manager, Experience Manager Sites
feature: Developing,SPA Editor
role: Developer
index: false
source-git-commit: 1509ca884e2f9eb931fc7cd416801957459cc4a0
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 9%

---


# SPA에 대한 React 구성 요소 구현{#implementing-a-react-component-for-spa}

SPA(단일 페이지 애플리케이션)는 웹 사이트 사용자에게 적합한 멋진 경험을 제공할 수 있습니다. 개발자는 SPA 프레임워크를 사용하여 사이트를 작성하려고 하며 작성자는 SPA 프레임워크를 사용하여 빌드된 사이트의 Adobe Experience Manager(AEM) 내에서 콘텐츠를 원활하게 편집하려고 합니다.

SPA 작성 기능은 AEM 내에서 SPA를 지원하는 포괄적인 솔루션을 제공합니다. 이 문서에서는 간단한 기존 React 구성 요소를 AEM SPA 편집기에서 작동하도록 조정하는 방법에 대한 예를 제공합니다.

{{ue-over-spa}}

## 소개 {#introduction}

AEM에서 필요로 하고 SPA와 SPA 편집기 간에 수립된 간단하고 가벼운 계약 덕분에 기존 JavaScript 애플리케이션을 AEM에서 SPA에 사용하도록 채택하는 것은 간단한 문제입니다.

이 문서에서는 We.Retail 저널 샘플 SPA에 있는 날씨 구성 요소의 예를 보여줍니다.

이 문서를 읽기 전에 AEM용 SPA 응용 프로그램의 [구조](/help/sites-developing/spa-getting-started-react.md)에 익숙해야 합니다.

>[!CAUTION]
>이 문서에서는 데모용으로만 [We.Retail 저널 앱](https://github.com/adobe/aem-sample-we-retail-journal)을 사용합니다. 프로젝트 작업에는 사용하지 마십시오.
>
>AEM 프로젝트는 React 또는 Angular를 통해 SPA 프로젝트를 지원하고 SPA SDK를 사용하는 [AEM Project Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)을 사용해야 합니다.

## 날씨 구성 요소 {#the-weather-component}

날씨 구성 요소는 We.Retail 저널 앱의 왼쪽 상단에 있습니다. 정의된 위치의 현재 날씨를 표시하여 날씨 데이터를 동적으로 가져옵니다.

### 날씨 위젯 사용 {#using-the-weather-widget}

![screen_shot_2018-06-08at143224](assets/screen_shot_2018-06-08at143224.png)

SPA 편집기에서 SPA의 콘텐츠를 작성할 때 날씨 구성 요소는 도구 모음이 포함된 다른 AEM 구성 요소로 표시되며 편집할 수 있습니다.

![screen_shot_2018-06-08at143304](assets/screen_shot_2018-06-08at143304.png)

도시는 다른 AEM 구성 요소와 마찬가지로 대화 상자에서 업데이트할 수 있습니다.

![screen_shot_2018-06-08at143446](assets/screen_shot_2018-06-08at143446.png)

변경은 지속되고 구성 요소는 새로운 날씨 데이터로 자동으로 업데이트됩니다.

![screen_shot_2018-06-08at143524](assets/screen_shot_2018-06-08at143524.png)

### 날씨 구성 요소 구현 {#weather-component-implementation}

날씨 구성 요소는 공개적으로 사용 가능한 React 구성 요소([React Open Weather](https://www.npmjs.com/package/react-open-weather))를 기반으로 합니다. We.Retail Journal 샘플 SPA 애플리케이션 내에서 구성 요소로 작동하도록 조정되었습니다.

다음은 React Open Weather 구성 요소 사용에 대한 NPM 설명서의 스니펫입니다.

![screen_shot_2018-06-08at144723](assets/screen_shot_2018-06-08at144723.png) ![screen_shot_2018-06-08at144215](assets/screen_shot_2018-06-08at144215.png)

We.Retail Journal 응용 프로그램에서 사용자 지정된 날씨 구성 요소(`Weather.js`)의 코드 검토:

* **줄 16**: 필요에 따라 React Open Weather 위젯이 로드됩니다.
* **줄 46**: `MapTo` 함수는 SPA 편집기에서 편집할 수 있도록 이 React 구성 요소를 해당 AEM 구성 요소와 연결합니다.

* **줄 22-29**: `EditConfig`이(가) 정의되어 있으며, 도시가 채워졌는지 확인하고 비어 있는 경우 값을 정의합니다.

* **줄 31-44**: 날씨 구성 요소는 `Component` 클래스를 확장하고 React Open Weather 구성 요소에 대한 NPM 사용 설명서에 정의된 대로 필요한 데이터를 제공하고 구성 요소를 렌더링합니다.

```javascript
/*~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
 ~ Copyright 2018 Adobe Systems Incorporated
 ~
 ~ Licensed under the Apache License, Version 2.0 (the "License");
 ~ you may not use this file except in compliance with the License.
 ~ You may obtain a copy of the License at
 ~
 ~     https://www.apache.org/licenses/LICENSE-2.0
 ~
 ~ Unless required by applicable law or agreed to in writing, software
 ~ distributed under the License is distributed on an "AS IS" BASIS,
 ~ WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 ~ See the License for the specific language governing permissions and
 ~ limitations under the License.
 ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~*/
import React, {Component} from 'react';
import ReactWeather from 'react-open-weather';
import {MapTo} from '@adobe/aem-react-editable-components';

require('./Weather.css');

const WeatherEditConfig = {

    emptyLabel: 'Weather',

    isEmpty: function() {
        return !this.props || !this.props.cq_model || !this.props.cq_model.city || this.props.cq_model.city.trim().length < 1;
    }
};

class Weather extends Component {

    render() {
        let apiKey = "12345678901234567890";
        let city;

        if (this.props.cq_model) {
            city = this.props.cq_model.city;
            return <ReactWeather key={'react-weather' + Date.now()} forecast="today" apikey={apiKey} type="city" city={city} />
        }

        return null;
    }
}

MapTo('we-retail-journal/global/components/weather')(Weather, WeatherEditConfig);
```

백엔드 구성 요소가 이미 존재해야 하지만, 프론트엔드 개발자는 We.Retail 저널 SPA에서 적은 코딩으로 React 오픈 날씨 구성 요소를 사용할 수 있습니다.

## 다음 단계 {#next-step}

AEM용 SPA 개발에 대한 자세한 내용은 [AEM용 SPA 개발](/help/sites-developing/spa-architecture.md) 문서를 참조하십시오.
