---
title: 구성 및 구성 브라우저
description: AEM 구성 및 AEM에서 작업 공간 설정을 관리하는 방법을 이해합니다.
source-git-commit: 8f5159d92f64b218d9e2e72d119e6de9d3e01ce6
workflow-type: tm+mt
source-wordcount: '1496'
ht-degree: 2%

---


# 구성 및 구성 브라우저 {#configuration-browser}

AEM 구성은 AEM에서 설정을 관리하고 작업 공간으로 사용할 수 있습니다.

## 구성이란 무엇입니까?{#what-is-a-configuration}

구성은 두 개의 다른 관점에서 고려될 수 있다.

* [관리자는 ](#configurations-administrator) 구성을 AEM 내의 작업 공간으로 사용하여 설정 그룹을 정의하고 관리합니다.
* [개발자](#configurations-developer) 는 AEM에서 설정을 유지하고 조회하기 위해 구성을 구현하는 기본 구성 메커니즘을 사용합니다.

요약하면 다음과 같습니다.관리자의 관점에서 구성은 AEM에서 설정을 관리하는 작업 공간을 만드는 방법이지만, 개발자는 AEM이 저장소 내에서 이러한 구성을 사용하고 관리하는 방법을 이해해야 합니다.

사용자의 관점에 상관없이 구성은 AEM에서 두 가지 주요 목적을 제공합니다.

* 구성은 특정 사용자 그룹에 대해 특정 기능을 활성화합니다.
* 구성은 이러한 기능에 대한 액세스 권한을 정의합니다.

## 관리자로 구성 {#configurations-administrator}

작성자와 AEM 관리자는 구성을 작업 공간으로 고려할 수 있습니다. 이러한 작업 공간은 이러한 기능에 대한 액세스 권한을 구현하여 조직 목적을 위해 관련 컨텐츠와 설정 그룹을 함께 수집하는 데 사용할 수 있습니다.

AEM 내의 다양한 기능에 대한 구성을 만들 수 있습니다.

* [클라우드 구성](/help/sites-administering/configurations.md)
* [Context Hub 세그먼트](/help/sites-administering/segmentation.md)
* [컨텐츠 조각 모델](/help/assets/content-fragments/content-fragments-models.md)
* [편집 가능한 템플릿](/help/sites-authoring/templates.md)

### 예 {#administrator-example}

예를 들어, 관리자는 편집 가능한 템플릿에 대해 두 개의 구성을 만들 수 있습니다.

* WKND-일반
* WKND-Magazine

그런 다음 관리자는 WKND-General 구성을 사용하여 일반 페이지 템플릿을 작성한 다음 WKND-Magazine 아래에 있는 매거진에 대한 템플릿을 만들 수 있습니다.

그런 다음 관리자는 WKND-General를 WKND 사이트의 모든 컨텐츠와 연결할 수 있습니다. 그러나 WKND-Magazine 구성은 잡지 사이트와만 연관될 것입니다.

다음을 수행하십시오.

* 컨텐츠 작성자가 잡지의 새 페이지를 만들면, 작성자는 일반 템플릿(WKND-General) 또는 잡지 템플릿(WKND-Magazine)에서 선택할 수 있습니다.
* 컨텐츠 작성자가 매거진이 아닌 사이트의 다른 부분에 대한 새 페이지를 만들면 작성자는 일반 템플릿(WKND-General)에서만 선택할 수 있습니다.

편집 가능한 템플릿뿐만 아니라 클라우드 구성, ContextHub 세그먼트 및 컨텐츠 조각 모델에 대해서도 유사한 설정을 수행할 수 있습니다.

### 구성 브라우저 {#using-configuration-browser} 사용

관리자는 구성 브라우저를 사용하여 AEM에서 구성에 대한 액세스 권한을 쉽게 생성, 관리 및 구성할 수 있습니다.

>[!NOTE]
>
>사용자에게 `admin` 권한이 있는 경우에만 구성 브라우저를 사용하여 구성을 만들 수 있습니다. `admin` 구성에 액세스 권한을 할당하거나 구성을 수정하려면 또한 권한이 필요합니다.

#### 구성 만들기 {#creating-a-configuration}

구성 브라우저를 사용하여 AEM에서 새 구성을 만드는 것은 매우 간단합니다.

1. AEM에 Cloud Service으로 로그인하고 기본 메뉴에서 **도구** -> **일반** -> **구성 브라우저**&#x200B;를 선택합니다.
1. **만들기**&#x200B;를 탭하거나 클릭합니다.
1. 구성에 **제목** 및 **이름**&#x200B;을 입력합니다.

   ![구성 만들기](assets/configuration-create.png)

   * **제목**&#x200B;은 설명적이어야 합니다.
   * **이름**&#x200B;은 저장소의 노드 이름이 됩니다.
      * 제목 기준 자동 생성되며 [AEM 이름 지정 규칙에 따라 조정됩니다.](/help/sites-developing/naming-conventions.md)
      * 필요하면 조정할 수 있다.
1. 허용할 구성 유형을 확인합니다.
   * [클라우드 구성](/help/sites-administering/configurations.md)
   * [Context Hub 세그먼트](/help/sites-administering/segmentation.md)
   * [컨텐츠 조각 모델](/help/assets/content-fragments/content-fragments-models.md)
   * [편집 가능한 템플릿](/help/sites-authoring/templates.md)
1. **만들기**&#x200B;를 탭하거나 클릭합니다.

>[!TIP]
>
>구성이 중첩될 수 있습니다.

#### 구성 및 해당 액세스 권한 편집 {#access-rights}

구성을 작업 공간으로 생각할 경우, 해당 구성에 액세스 권한을 설정하여 해당 작업 영역에 액세스할 수 있는 사용자와 액세스할 수 없는 사용자를 적용할 수 있습니다.

1. AEM에 Cloud Service으로 로그인하고 기본 메뉴에서 **도구** -> **일반** -> **구성 브라우저**&#x200B;를 선택합니다.
1. 수정할 구성을 선택한 다음 도구 모음에서 **속성**&#x200B;을 탭하거나 클릭합니다.
1. 구성에 추가할 추가 기능을 선택합니다
   >[!NOTE]
   >
   >구성이 생성되면 피쳐를 선택 취소할 수 없습니다.
1. **유효 권한** 단추를 사용하여 역할 매트릭스와 현재 구성에 부여된 권한을 확인합니다.
   ![유효 권한 창](assets/configuration-effective-permissions.png)
1. 새 권한을 할당하려면 **새 권한 추가** 섹션의 **사용자 또는 그룹 선택** 필드에 사용자 또는 그룹 이름을 입력합니다.
   * **사용자 또는 그룹 선택** 필드는 기존 사용자 및 역할에 따라 자동 완성 기능을 제공합니다.
1. 자동 완료 결과에서 적절한 사용자 또는 역할을 선택합니다.
   * 두 명 이상의 사용자 또는 역할을 선택할 수 있습니다.
1. 선택한 사용자 또는 역할이 가져야 하는 액세스 옵션을 선택하고 **추가**를 클릭합니다.
   ![구성에 액세스 권한 추가](assets/configuration-edit.png)
1. 단계를 반복하여 사용자 또는 역할을 선택하고 필요에 따라 추가 액세스 권한을 할당합니다.
1. 완료되면 **저장 및 닫기**&#x200B;를 탭하거나 클릭합니다.

## 개발자로서 구성 {#configurations-developer}

개발자로서 AEM as a Cloud Service이 구성에서 작동하는 방식과 구성 해상도를 처리하는 방법을 알고 있어야 합니다.

### 구성 및 컨텐츠 분리 {#separation-of-config-and-content}

[관리자 및 사용자는 다른 설정 및 컨텐츠를 관리하기 위해 구성을 workplace](#configurations-administrator)로 생각할 수 있지만 구성 및 컨텐츠는 저장소에서 AEM에 의해 별도로 저장되고 관리된다는 것을 이해하는 것이 중요합니다.

* `/content` 은 모든 컨텐츠가 있는 홈입니다.
* `/conf` 은 모든 구성의 홈 상태입니다.

콘텐츠는 `cq:conf` 속성을 통해 연결된 구성을 참조합니다. AEM에서는 컨텐츠를 기반으로 조회를 수행하고 상황에 맞는 `cq:conf` 속성을 사용하여 적절한 구성을 찾습니다.

### 예 {#developer-example}

이 예에서는 DAM 설정에 관심이 있는 애플리케이션 코드가 있다고 가정합니다.

```java
Conf conf = resource.adaptTo(Conf.class);
ValueMap imageServerSettings = conf.getItem("dam/imageserver");
String bgkcolor = imageServerSettings.get("bgkcolor", "FFFFFF");
```

모든 구성 조회의 시작점은 컨텐츠 리소스이며, 일반적으로 `/content` 아래에 있습니다. 페이지, 페이지 내의 구성 요소, 자산 또는 DAM 폴더일 수 있습니다. 이 컨텍스트에서 적용되는 올바른 구성을 찾고 있는 실제 콘텐츠입니다.

이제 `Conf` 개체가 있으면 원하는 특정 구성 항목을 검색할 수 있습니다. 이 경우 `dam/imageserver` 은 `imageserver`과 관련된 설정 모음입니다. `getItem` 호출은 `ValueMap`을 반환합니다. 그런 다음 `bgkcolor` 문자열 속성을 읽고 속성(또는 전체 구성 항목)이 없는 경우 기본값이 &quot;FFFF&quot;를 제공합니다.

이제 해당 JCR 컨텐츠를 살펴보겠습니다.

```text
/content/dam/wknd
    + jcr:content
      - cq:conf = "/conf/wknd"
    + image.png [dam:Asset]

/conf/wkns
    + settings
      + dam
        + imageserver [cq:Page]
          + jcr:content
            - bgkcolor = "FF0000"
```

이 예에서는 여기서 WKND별 DAM 폴더 및 해당 구성을 가정합니다. 해당 폴더 `/content/dam/wknd`부터 하위 트리에 적용해야 하는 구성을 참조하는 `cq:conf` 문자열 속성이 있는 것을 확인할 수 있습니다. 속성은 일반적으로 자산 폴더 또는 페이지의 `jcr:content`에서 설정됩니다. 이러한 `conf` 링크는 명시적 링크이므로 CRXDE의 콘텐츠만 보면 쉽게 찾을 수 있습니다.

`/conf` 안으로 이동하면 참조를 따르며 `/conf/wknd` 노드가 있음을 알 수 있습니다. 구성입니다. 해당 조회는 응용 프로그램 코드에 완전히 투명합니다. 예제 코드에는 전용 참조가 없으며 `Conf` 개체 뒤에 숨겨집니다. 적용되는 구성은 JCR 컨텐츠를 통해 완전히 제어됩니다.

이 경우에 필요한 `dam/imageserver`을 포함하여 실제 항목을 포함하는 고정 이름이 인 `settings` 노드가 구성에 포함되어 있는 것을 볼 수 있습니다. 이러한 항목은 &quot;설정 문서&quot;로 생각할 수 있으며 일반적으로 실제 컨텐츠를 포함하는 `jcr:content`를 포함하는 `cq:Page`로 표시됩니다.

마지막으로 샘플 코드에 필요한 속성 `bgkcolor`이 표시됩니다. `getItem`에서 다시 가져오는 `ValueMap`은 페이지의 `jcr:content` 노드를 기반으로 합니다.

### 구성 해상도 {#configuration-resolution}

위의 기본 예는 단일 구성을 보여줍니다. 하지만 기본 전역 구성, 각 브랜드에 대한 다른 구성, 하위 프로젝트에 대한 특정 구성과 같이 서로 다른 구성을 하려는 경우가 많습니다.

이를 지원하기 위해 AEM의 구성 조회에는 다음과 같은 기본 설정 순서로 상속 및 폴백 메커니즘이 있습니다.

1. `/conf/<siteconfig>/<parentconfig>/<myconfig>`
   * `cq:conf`에서 참조한 특정 구성(`/content` 위치)
   * 계층은 자의적이며 사이트 구조처럼 디자인될 수 있으며, 이를 아는 것은 애플리케이션 코드의 사업이 아닙니다
   * 구성 권한이 있는 사용자가 런타임 시 변경 가능
1. `/conf/<siteconfig>/<parentconfig>`
   * 대체 구성을 위해 부모 트래버스
   * 구성 권한이 있는 사용자가 런타임 시 변경 가능
1. `/conf/<siteconfig>`
   * 대체 구성을 위해 부모 트래버스
   * 구성 권한이 있는 사용자가 런타임 시 변경 가능
1. `/conf/global`
   * 시스템 전역 설정
   * 일반적으로 설치에 대한 전역 기본값
   * `admin` 역할에 의해 설정됩니다.
   * 구성 권한이 있는 사용자가 런타임 시 변경 가능
1. `/apps`
   * 애플리케이션 기본값
   * 애플리케이션 배포와 관련된 문제가 해결되었습니다.
   * 런타임 시 읽기 전용
1. `/libs`
   * AEM 제품 기본값
   * Adobe로만 변경할 수 있으며 프로젝트 액세스는 허용되지 않습니다
   * 애플리케이션 배포와 관련된 문제가 해결되었습니다.
   * 런타임 시 읽기 전용

### 구성 사용 {#using-configurations}

AEM의 구성은 Sling 컨텍스트 인식 구성을 기반으로 합니다. Sling 번들은 컨텍스트 인식 구성을 가져오는 데 사용할 수 있는 서비스 API를 제공합니다. 컨텍스트 인식 구성은 앞의 예에서 설명한 [과 같이 컨텐츠 리소스 또는 리소스 트리와 관련된 구성입니다.](#developer-example)

컨텍스트 인식 구성, 예 및 사용 방법에 대한 자세한 내용은 [Sling 설명서를 참조하십시오.](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration.html)

### ConfMgr 웹 콘솔 {#confmgr-web-console}

디버깅 및 테스트 목적으로 **ConfMgr** 웹 콘솔이 `https://<host>:<port>/system/console/conf`에 있으며, 이 콘솔은 지정된 경로/항목에 대한 구성을 표시할 수 있습니다.

![ConfMgr](assets/configuration-confmgr.png)

다음을 제공하면 됩니다.

* **컨텐츠 경로**
* **항목**
* **사용자**

확인되는 구성을 확인하고 해당 구성을 확인할 샘플 코드를 받으려면 **해결** 을 클릭하십시오.

### 컨텍스트 인식 구성 웹 콘솔 {#context-aware-web-console}

디버깅 및 테스트 목적으로 저장소에서 컨텍스트 인식 구성을 쿼리하고 해당 속성을 볼 수 있는 **컨텍스트 인식 구성** 웹 콘솔이 `https://<host>:<port>/system/console/slingcaconfig`에 있습니다.

![컨텍스트 인식 구성 웹 콘솔](assets/configuration-context-aware-console.png)

다음을 제공하면 됩니다.

* **컨텐츠 경로**
* **구성 이름**

**해결** 을 클릭하여 선택한 구성에 대한 연관된 컨텍스트 경로 및 속성을 검색합니다.
