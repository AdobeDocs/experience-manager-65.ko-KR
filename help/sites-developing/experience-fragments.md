---
title: 경험 구성요소
seo-title: 경험 구성요소
description: 경험 조각 사용자 지정에 대해 알아봅니다.
seo-description: 경험 조각 사용자 지정에 대해 알아봅니다.
uuid: fc9f7e59-bd7c-437a-8c63-de8559b5768d
contentOwner: aheimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: c02e713e-15f3-408b-879a-d5eb014aef02
docset: aem65
translation-type: tm+mt
source-git-commit: 25eff10d4be811774e7a25cebf7e0506acfd5b0b
workflow-type: tm+mt
source-wordcount: '1667'
ht-degree: 3%

---


# 경험 조각{#experience-fragments}

## 기본 사항 {#the-basics}

[경험 조각](/help/sites-authoring/experience-fragments.md)은 페이지 내에서 참조할 수 있는 컨텐츠 및 레이아웃을 포함한 하나 이상의 구성 요소 그룹입니다.

경험 조각 기본 및/또는 변형은 다음을 사용합니다.

* `sling:resourceType` : `/libs/cq/experience-fragments/components/xfpage`

`/libs/cq/experience-fragments/components/xfpage/xfpage.html`이 없으므로

* `sling:resourceSuperType` :  `wcm/foundation/components/page`

## 일반 HTML 표현물 {#the-plain-html-rendition}

URL의 `.plain.` 선택기를 사용하여 일반 HTML 변환에 액세스할 수 있습니다.

이는 브라우저에서 사용할 수 있지만 주요 목적은 URL만 사용하여 다른 응용 프로그램(예: 타사 웹 앱, 사용자 지정 모바일 구현)이 경험 조각의 컨텐츠에 직접 액세스하도록 허용하는 것입니다.

일반 HTML 변환은 다음과 같은 경로에 프로토콜, 호스트 및 컨텍스트 경로를 추가합니다.

* 의 유형:`src`, `href` 또는 `action`

* 또는 다음으로 끝남:`-src` 또는 `-href`

예:

`.../brooklyn-coat/master.plain.html`

>[!NOTE]
>
>링크는 항상 게시 인스턴스를 참조합니다. 이러한 링크는 타사에서 소비하기 위한 것이므로 작성자가 아닌 게시 인스턴스에서 항상 호출됩니다.

![xf-14](assets/xf-14.png)

일반 변환 선택기는 추가 스크립트 대신 변환기를 사용합니다.[Sling Rewriter](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html)는 변환기로 사용됩니다. 이 설정은

* `/libs/experience-fragments/config/rewriter/experiencefragments`

## 소셜 변형 {#social-variations}

소셜 변형을 소셜 미디어(텍스트 및 이미지)에 게시할 수 있습니다. AEM에서 이러한 소셜 변형은 구성 요소를 포함할 수 있습니다.예를 들어 텍스트 구성 요소, 이미지 구성 요소 등이 있습니다.

소셜 게시물의 이미지와 텍스트는 모든 이미지 리소스 유형이나 심도의 텍스트 리소스 유형에서 가져올 수 있습니다(빌딩 블록 또는 레이아웃 컨테이너).

소셜 변형을 사용하면 게시 환경에서 소셜 작업을 수행할 때 구성 요소를 고려하고 고려합니다.

올바른 텍스트 및 이미지를 소셜 미디어 네트워크에 게시하려면 사용자 정의된 구성 요소를 개발하는 경우 일부 규칙을 준수해야 합니다.

이를 위해서는 다음 속성을 사용해야 합니다.

* 이미지 추출

   * `fileReference`
   * `fileName`

* 텍스트 추출

   * `text`

이 규칙을 사용하지 않는 구성 요소는 고려하지 않습니다.

## 경험 조각에 대한 템플릿 {#templates-for-experience-fragments}

>[!CAUTION]
>
>***경험 조각*** [에 대해 ](/help/sites-developing/page-templates-editable.md) 온라이드 템플릿이 지원됩니다.

경험 조각에 대한 새 템플릿을 개발할 때 [편집 가능한 템플릿](/help/sites-developing/page-templates-editable.md)에 대한 표준 방침을 따를 수 있습니다.

**경험 조각 만들기** 마법사에서 감지한 경험 조각 템플릿을 만들려면 다음 규칙 세트 중 하나를 따라야 합니다.

1. 모두:

   1. 템플릿의 리소스 유형(초기 노드)은 다음에서 상속되어야 합니다.
      `cq/experience-fragments/components/xfpage`

   1. 템플릿의 이름은 다음으로 시작해야 합니다.
      `experience-fragments`
이를 통해 사용자는 /content/experience-fragments에서 
`cq:allowedTemplates` 이 폴더의 속성에는 이름을 가진 모든 템플릿이 포함되어 있습니다 `experience-fragment`. 고객은 고유한 이름 지정 구성표 또는 템플릿 위치를 포함하도록 이 속성을 업데이트할 수 있습니다.

1. [허용된 템플릿](/help/sites-authoring/experience-fragments.md#configure-allowed-templates-folder) 은 경험 조각 콘솔에서 구성할 수 있습니다.

<!--
1. Add the template details manually in `cq:allowedTemplates` on the `/content/experience-fragment` node.
-->

<!-- >[!NOTE]
>
>[Allowed templates](/help/sites-authoring/experience-fragments.md#configuring-allowed-templates) can be configured in the Experience Fragments console.
-->

## 경험 조각에 대한 구성 요소 {#components-for-experience-fragments}

[경험 조각](/help/sites-developing/components.md) 과 함께/에서 사용하기 위한 구성 요소를 개발하는 방법은 표준 방법을 따릅니다.

유일한 추가 구성은 구성 요소가 템플릿에서 [허용되는 구성 요소인지 확인하는 것입니다. 이는 콘텐츠 정책](/help/sites-developing/page-templates-editable.md#content-policies)을 통해 이루어집니다.

## 경험 조각 링크 재작성자 공급자 - HTML {#the-experience-fragment-link-rewriter-provider-html}

AEM에서는 경험 조각을 만들 수 있습니다. 경험 조각:

* 구성 요소 그룹과 레이아웃으로 구성되며
* 은 AEM 페이지와 독립적으로 존재할 수 있습니다.

이러한 그룹에 대한 사용 사례 중 하나는 Adobe Target과 같은 타사 터치포인트에 컨텐트를 포함시키는 것입니다.

### 기본 링크 재작성 {#default-link-rewriting}

[Target으로 내보내기](/help/sites-administering/experience-fragments-target.md) 기능을 사용하여 다음을 수행할 수 있습니다.

* 경험 조각 만들기,
* 구성 요소 추가
* 그런 다음 HTML 형식 또는 JSON 형식으로 Adobe Target 오퍼으로 내보냅니다.

이 기능은 AEM[의 작성자 인스턴스에서 활성화될 수 있습니다. ](/help/sites-administering/experience-fragments-target.md#Prerequisites) 링크 외부 도우미에는 유효한 Adobe Target 구성 및 구성이 필요합니다.

링크 외부 도우미는 Target 오퍼의 HTML 버전을 만들 때 필요한 올바른 URL을 결정하는 데 사용되며, 이 URL은 이후 Adobe Target으로 전송됩니다. 이는 Adobe Target에서 Target HTML 오퍼 내의 모든 링크에 공개적으로 액세스할 수 있어야 하기 때문에 필요합니다.즉, 링크 참조 및 경험 조각 자체는 게시되어야 사용할 수 있습니다.

기본적으로 Target HTML 오퍼를 생성할 때 AEM의 사용자 정의 Sling 선택기로 요청이 전송됩니다. 이 선택기를 `.nocloudconfigs.html`이라고 합니다. 이름이 암시하듯이 경험 조각의 일반 HTML 렌더링을 만들지만 클라우드 구성(탁월한 정보)은 포함하지 않습니다.

HTML 페이지를 생성하면 Sling Rewriter 파이프라인이 출력을 수정합니다.

1. `html`, `head` 및 `body` 요소는 `div` 요소로 대체됩니다. `meta`, `noscript` 및 `title` 요소는 제거됩니다(원래 `head` 요소의 하위 요소이며, `div` 요소로 교체할 때 고려되지 않습니다).

   이는 HTML Target 오퍼이 Target 활동에 포함될 수 있도록 하기 위해 수행됩니다.

1. AEM은 게시된 리소스를 가리키도록 HTML에 있는 모든 내부 링크를 수정합니다.

   수정할 링크를 결정하기 위해 AEM은 HTML 요소의 속성에 대해 이 패턴을 따릅니다.

   1. `src` 특성
   1. `href` 특성
   1. `*-src` 속성(data-src, custom-src 등)
   1. `*-href` 속성(예:  `data-href`,  `custom-href` `img-href`, 등)

   >[!NOTE]
   >
   >대부분의 경우 HTML의 내부 링크는 상대 링크이지만 사용자 지정 구성 요소가 HTML에서 전체 URL을 제공하는 경우가 있을 수 있습니다. 기본적으로 AEM은 이러한 완전한 URL을 무시하고 수정하지 않습니다.

   이러한 속성의 링크는 AEM Link Externalizer `publishLink()`를 통해 실행되어 URL을 게시된 인스턴스에서와 같이 공개적으로 사용할 수 있습니다.

기본 구현을 사용하는 경우 위에 설명된 프로세스에서는 경험 조각에서 Target 오퍼을 생성한 다음 Adobe Target으로 내보내는 데 충분해야 합니다. 그러나 이 프로세스에서 고려하지 않은 일부 사용 사례가 있습니다.다음과 같습니다.

* 게시 인스턴스에서만 사용 가능한 Sling 매핑
* Dispatcher 리디렉션

이러한 경우 AEM은 링크 리작성기 공급자 인터페이스를 제공합니다.

### 링크 리작성기 공급자 인터페이스 {#link-rewriter-provider-interface}

>[!NOTE]
>
>이 인터페이스는 [AEM 6.5 SP1(6.5.1.0)](/help/release-notes/sp-release-notes.md)에서 도입되었습니다.

보다 복잡한 경우, [default](#default-link-rewriting)에서 다루지 않는 경우 AEM에서는 링크 리작성기 공급자 인터페이스를 제공합니다. 서비스로 번들에서 구현할 수 있는 `ConsumerType` 인터페이스입니다. 이 메서드는 수정 AEM이 경험 조각에서 렌더링되는 대로 HTML 오퍼의 내부 링크에서 수행하는 작업을 건너뜁니다. 이 인터페이스를 사용하면 비즈니스 요구에 맞게 내부 HTML 링크를 재작성하는 프로세스를 사용자 정의할 수 있습니다.

이 인터페이스를 서비스로 구현하는 데 사용되는 예는 다음과 같습니다.

* Sling 매핑은 게시 인스턴스에서 활성화되지만 작성자 인스턴스에는 활성화되지 않습니다
* 발송자 또는 유사한 기술을 사용하여 내부적으로 URL을 리디렉션합니다.
* 리소스에 대해 `sling:alias mechanisms`이(가) 있습니다.

>[!NOTE]
>
>이 인터페이스는 생성된 Target 오퍼의 내부 HTML 링크만 처리합니다.

링크 리작성기 공급자 인터페이스( `ExperienceFragmentLinkRewriterProvider`)는 다음과 같습니다.

```java
public interface ExperienceFragmentLinkRewriterProvider {

    String rewriteLink(String link, String tag, String attribute);

    boolean shouldRewrite(ExperienceFragmentVariation experienceFragment);

    int getPriority();

}
```

### 링크 리작성기 공급자 인터페이스를 사용하는 방법 {#how-to-use-the-link-rewriter-provider-interface}

인터페이스를 사용하려면 먼저 링크 리저터 공급자 인터페이스를 구현하는 새 서비스 구성 요소가 포함된 번들을 만들어야 합니다.

이 서비스는 다양한 링크에 액세스하기 위해 경험 조각 내보내기에 Target 재작성을 연결하는 데 사용됩니다.

예, `ComponentService`:

```java
import com.adobe.cq.xf.ExperienceFragmentLinkRewriterProvider;
import com.adobe.cq.xf.ExperienceFragmentVariation;
import org.osgi.service.component.annotations.Service;
import org.osgi.service.component.annotations.Component;

@Component
@Service
public class GeneralLinkRewriter implements ExperienceFragmentLinkRewriterProvider {

    @Override
    public String rewriteLink(String link, String tag, String attribute) {
        return null;
    }

    @Override
    public boolean shouldRewrite(ExperienceFragmentVariation experienceFragment) {
        return false;
    }

    @Override
    public int getPriority() {
        return 0;
    }

}
```

서비스가 제대로 작동하기 위해서는 이제 서비스 내에서 구현해야 하는 세 가지 방법이 있습니다.

* ` [shouldRewrite](#shouldrewrite)`
* ` [rewriteLink](#rewritelink)`

   * `rewriteLinkExample2`

* ` [getPriority](#priorities-getpriority)`

#### shouldRewrite {#shouldrewrite}

특정 경험 조각 변형에서 Target으로 내보내기를 호출할 때 링크를 다시 작성해야 하는지 여부를 시스템에 표시해야 합니다. 이 작업은 메서드를 구현하여 수행합니다.

`shouldRewrite(ExperienceFragmentVariation experienceFragment);`

예:

```java
@Override
public boolean shouldRewrite(ExperienceFragmentVariation experienceFragment) {
    return experienceFragment.getPath().equals("/content/experience-fragment/master");
}
```

이 메서드는 매개 변수로 Target으로 내보내기 시스템이 현재 재작성하고 있는 경험 조각 변형을 받습니다.

위의 예에서 다음을 다시 작성하려고 합니다.

* `src`에 있는 링크

* `href` 속성만

* (특정 경험 조각):
   `/content/experience-fragment/master`

Target으로 내보내기 시스템을 통과하는 기타 모든 경험 조각은 무시되며 본 서비스에 구현된 변경 사항에 영향을 받지 않습니다.

#### rewriteLink {#rewritelink}

재작성 프로세스의 영향을 받은 경험 조각 변형에 대해 서비스는 링크 재작성을 처리하도록 진행합니다. 내부 HTML에서 링크가 발생할 때마다 다음 메서드가 호출됩니다.

`rewriteLink(String link, String tag, String attribute)`

입력 시 이 메서드는 매개 변수를 받습니다.

* `link`
 
`String` 현재 처리 중인 링크의 표현. 일반적으로 작성자 인스턴스의 리소스를 가리키는 상대 URL입니다.

* `tag`
현재 처리 중인 HTML 요소의 이름입니다.

* `attribute`
정확한 속성 이름입니다.

예를 들어 Target으로 내보내기 시스템이 현재 이 요소를 처리하는 경우 `CSSInclude`을 다음과 같이 정의할 수 있습니다.

```java
<link rel="stylesheet" href="/etc.clientlibs/foundation/clientlibs/main.css" type="text/css">
```

`rewriteLink()` 메서드에 대한 호출은 다음 매개 변수를 사용하여 수행됩니다.

```java
rewriteLink(link="/etc.clientlibs/foundation/clientlibs/main.css", tag="link", attribute="href" )
```

서비스를 만들 때 주어진 입력에 따라 결정을 내리고 그에 따라 링크를 다시 작성할 수 있습니다.

예를 들어 URL의 `/etc.clientlibs` 부분을 제거하고 적절한 외부 도메인을 추가하려고 합니다. 작업을 단순화하기 위해 Adobe는 `rewriteLinkExample2`에서와 같이 귀하의 서비스에 대한 리소스 해결 프로그램에 대한 액세스 권한이 있음을 고려할 것입니다.

>[!NOTE]
>
>서비스 사용자를 통해 리소스 확인자를 가져오는 방법에 대한 자세한 내용은 AEM[의 서비스 사용자를 참조하십시오.](/help/sites-administering/security-service-users.md)

```java
private ResourceResolver resolver;

private Externalizer externalizer;

@Override
public String rewriteLink(String link, String tag, String attribute) {

    // get the externalizer service
    externalizer = resolver.adaptTo(Externalizer.class);
    if(externalizer == null) {
        // if there was an error, then we do not modify the link
        return null;
    }

    // remove leading /etc.clientlibs from resource link before externalizing
    link = link.replaceAll("/etc.clientlibs", "");

    // considering that we configured our publish domain, we directly apply the publishLink() method
    link = externalizer.publishLink(resolver, link);

    return link;
}
```

>[!NOTE]
>
>위의 메서드가 `null`을 반환하면 Target으로 내보내기 시스템은 해당 링크를 그대로 유지합니다. 리소스 관련 링크입니다.

#### 우선 순위 - getPriority {#priorities-getpriority}

다양한 유형의 경험 조각에 맞는 서비스를 여러 개 필요로 하거나 모든 경험 조각에 대한 외부화 및 매핑을 처리하는 범용 서비스를 필요로 하는 경우도 있습니다. 이러한 경우 사용할 서비스가 충돌할 수 있으므로 AEM에서는 다른 서비스에 대해 **Priority**&#x200B;을 정의할 수 있습니다. 우선 순위는 다음 방법을 사용하여 지정합니다.

* `getPriority()`

이 방법을 사용하면 동일한 경험 조각에 대해 `shouldRewrite()` 메서드가 true를 반환하는 여러 서비스를 사용할 수 있습니다. `getPriority()`메서드에서 가장 높은 수를 반환하는 서비스는 경험 조각 변형을 처리하는 서비스입니다.

예를 들어 모든 경험 조각에 대한 기본 매핑을 처리하고 `shouldRewrite()` 메서드가 모든 경험 조각 변형에 대해 `true`를 반환하는 `GenericLinkRewriterProvider`을(를) 가질 수 있습니다. 몇 개의 특정 경험 조각에 대해 특수 처리를 원할 수 있습니다. 이 경우 `shouldRewrite()` 메서드가 일부 경험 조각 변형에 대해서만 true를 반환하는 `SpecificLinkRewriterProvider`을 제공할 수 있습니다. `SpecificLinkRewriterProvider`이(가) 이러한 경험 조각 변형을 처리하도록 선택되었는지 확인하려면 `getPriority()` 메서드에서 `GenericLinkRewriterProvider.`보다 높은 수를 반환해야 합니다
