---
title: Apache Maven을 사용하여 AEM 프로젝트를 작성하는 방법
seo-title: Apache Maven을 사용하여 AEM 프로젝트를 작성하는 방법
description: 이 문서에서는 Apache Maven을 기반으로 AEM 프로젝트를 설정하는 방법에 대해 설명합니다
seo-description: 이 문서에서는 Apache Maven을 기반으로 AEM 프로젝트를 설정하는 방법에 대해 설명합니다
uuid: 5db68639-7393-48b7-9d81-5b19b596ff21
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 3ebc1d22-a7a2-4375-9aa5-a18a7ceb446a
docset: aem65
translation-type: tm+mt
source-git-commit: add17f46dfb292aeaf8425e5f75cfe955ed93cbc
workflow-type: tm+mt
source-wordcount: '2468'
ht-degree: 1%

---


# Apache Maven을 사용하여 AEM 프로젝트를 작성하는 방법{#how-to-build-aem-projects-using-apache-maven}

## 개요 {#overview}

이 문서에서는 [Apache Maven을 기반으로 AEM 프로젝트를 설정하는 방법에 대해 설명합니다](https://maven.apache.org/).

Apache Maven은 빌드를 자동화하고 품질 프로젝트 정보를 제공하여 소프트웨어 프로젝트를 관리하기 위한 오픈 소스 툴입니다. AEM 프로젝트에 권장되는 빌드 관리 툴입니다.

Maven을 기반으로 AEM 프로젝트를 빌드하면 다음과 같은 몇 가지 이점이 있습니다.

* IDE에 관계없이 개발 환경
* Adobe이 제공하는 마웬 원형과 유물의 활용
* Maven 기반 개발 설정을 위한 Apache Sling 및 Apache Felix 도구 세트의 사용
* 간편한 IDE 가져오기예: Eclipse 및/또는 IntelliJ
* 지속적인 통합 시스템과의 간편한 통합

### Maven Project Archetypes {#maven-project-archetypes}

Adobe은 AEM 프로젝트의 기준점으로 사용할 수 있는 두 개의 Maven 원형 모델을 제공합니다. 자세한 내용은 아래 링크를 참조하십시오.

* [AEM 프로젝트 원형](https://github.com/adobe/aem-project-archetype)
* [단일 페이지 애플리케이션 시작 키트를 위한 Maven 원형](https://github.com/adobe/aem-spa-project-archetype)

## Experience Manager API 종속성 {#experience-manager-api-dependencies}

### 우버항아리는 무엇입니까? {#what-is-the-uberjar}

&quot;UberJar&quot;는 Adobe에서 제공하는 특수 JAR(Java Archives) 파일에 지정된 비공식 이름입니다. 이러한 JAR 파일에는 Adobe Experience Manager에서 노출한 모든 공개 Java API가 포함되어 있습니다. 이러한 라이브러리에는 제한된 외부 라이브러리뿐만 아니라, Apache Sling, Apache Jackrabbit, Apache Lucene, Google Guava에서 제공하는 AEM에서 이용할 수 있는 모든 공용 API와 이미지 처리에 사용되는 2개의 라이브러리(Werner Randelshofer의 CYMK JPEG ImageIO 라이브러리 및 12개의 Monkeys 이미지 라이브러리)가 포함되어 있습니다. UberJar에는 API 인터페이스와 클래스만 포함되어 있으므로 AEM에서 OSGi 번들로 내보내지는 인터페이스와 클래스만 포함합니다. 또한 내보낸 모든 패키지에 대해 올바른 패키지 *내보내기 버전이 들어 있는 MANIFEST.MF* 파일도 포함되어 있으므로 UberJar에 대해 빌드된 프로젝트에 올바른 패키지 가져오기 범위가 있는지 확인합니다.

### Adobe이 우버항들을 만든 이유는? {#why-did-adobe-create-the-uberjars}

이전에는 개발자는 서로 다른 AEM 라이브러리에 대한 상대적으로 많은 수의 개별 종속성을 관리해야 했고, 각 새로운 API를 사용할 때는 하나 이상의 개별 종속성을 프로젝트에 추가해야 했습니다. 한 프로젝트에서 UberJar 도입으로 인해 프로젝트에서 30개의 개별 종속성이 제거됩니다.

AEM 6.5부터 Adobe은 두 개의 UberJar를 제공합니다.더 이상 사용되지 않는 인터페이스와 더 이상 사용되지 않는 인터페이스를 제거하는 인터페이스를 포함하는 것입니다. 빌드 시 명시적으로 한 코드를 참조함으로써 가치 하락이 있는 코드에 대한 의존성이 있는지 여부를 고객이 이해해야 합니다.

두 번째 Uber Jar는 가치가 하락하는 모든 클래스, 메서드 및 속성을 제거하므로 고객은 나중에 사용자 정의 코드가 맞는지 컴파일하고 확인할 수 있습니다.

### 어떤 우버jar를 사용해야 합니까? {#which-uberjar-to-use}

AEM 6.5는 두 가지 방법으로 나온다.

1. Uber Jar - 사용 중단으로 표시되지 않은 공용 인터페이스만 포함합니다. 이것은 가치가 떨어진 API에 의존하지 않고 나중에 코드 기반을 방지하는 데 도움이 되므로 **권장되는** UberJar입니다.
1. 더 이상 사용되지 않는 API가 포함된 Uber Jar - 향후 AEM 버전에서 사용 중단으로 표시된 모든 공용 인터페이스를 포함합니다.

>[!NOTE]
>
>AEM 6.5.6부터 UberJar 및 기타 관련 객체는 Adobe Public Maven 리포지토리(repo.adobe.com) 대신 [Maven Central 저장소에서](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/) 사용할 수 있습니다. 기본 UberJar 파일의 이름이 로 변경되었습니다 `uber-jar-<version>.jar`. 그 결과, 태그 `classifier`에 대한 값 `apis` 이 없는 `dependency` 것으로 나타났습니다.

### 우버항아리는 어떻게 사용하나요? {#how-do-i-use-the-uberjars}

빌드 시스템(대부분의 AEM Java 프로젝트의 경우)으로 Apache Maven을 사용하는 경우, pom.xml ** 파일에 하나 또는 두 개의 요소를 추가해야 합니다. 첫 번째 요소는 프로젝트에 실제 종속성을 추가하는 *종속성* 요소입니다.

**Uber Jar 종속성&#x200B;*(더 이상 사용되지 않는 API 없음)***

```xml
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.5.0</version>
    <classifier>apis</classifier>
    <scope>provided</scope>
</dependency>
```

**사용되지 않는 API와 Uber Jar 종속성**

>[!CAUTION]
>
>***does not* **include the deprecated APIs that your applications will be properly on futable version of AEM.
>
>사용되지 않는 API를 사용하는 코드를 수정할 수 없는 경우에만 사용되지 않는 API 지원과 함께 Uber Jar를 사용하십시오.

```xml
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.5.0</version>
    <classifier>apis-with-deprecations</classifier>
    <scope>provided</scope>
</dependency>
```

회사에서 이미 Sonatype Nexus, Apache Archiva 또는 JFrog Artitfactory와 같은 Maven Repository Manager를 사용하고 있는 경우 프로젝트에 적절한 구성을 추가하여 이 저장소 관리자를 참조하고 Adobe Maven 리포지토리([https://repo.maven.apache.org/maven2/](https://repo.maven.apache.org/maven2/))를 저장소 관리자에 추가합니다.

저장소 관리자를 사용하고 있지 않은 경우 *저장소* 요소를 pom.xml 파일에 추가해야 *합니다* .

```xml
<repositories>
    <repository>
        <id>adobe-public-releases</id>
        <name>Adobe Public Repository</name>
        <url>https://repo.maven.apache.org/maven2/</url>
        <layout>default</layout>
    </repository>
</repositories>
<pluginRepositories>
    <pluginRepository>
        <id>adobe-public-releases</id>
        <name>Adobe Public Repository</name>
        <url>https://repo.maven.apache.org/maven2/</url>
        <layout>default</layout>
    </pluginRepository>
</pluginRepositories>
```

### 우버항으로 무엇을 할 수 있습니까? {#what-can-i-do-with-the-uberjar}

UberJar를 사용하면 AEM API(및 위에 언급한 프로젝트에서 사용되는 API에 따라 사용되는 프로젝트 코드를 컴파일할 수 있습니다.) OSGi SCR(Service Component Runtime) 및 OSGi Metatype 정보를 생성할 수도 있습니다. 몇 가지 제한 사항으로 단위 테스트를 작성하고 실행할 수도 있습니다.

### 우버항아리는 어떻게 하면 되죠? {#what-can-t-i-do-with-the-uberjar}

UberJar에는 **API만** 포함되어 있으므로 실행 파일이 아니며 Adobe Experience Manager을 **실행하는 데 사용할** 수 없습니다. AEM을 실행하려면 AEM Quickstart(독립 실행형 또는 웹 애플리케이션 아카이브(WAR) 양식이 필요합니다.

### 단위 테스트에 제한 사항을 언급했습니다. 더 설명해주세요 {#you-mentioned-limitations-on-unit-tests-please-explain-further}

단위 테스트는 일반적으로 세 가지 방법으로 제품 API와 상호 작용하며, 각 테스트는 UberJar에 의해 약간 다르게 영향을 받습니다.

#### 사용 사례 #1 - API 인터페이스를 호출하는 사용자 지정 코드 {#use-case-custom-code-which-calls-a-api-interface}

가장 일반적인 이러한 경우에는 AEM API에서 정의한 Java 인터페이스에서 메서드를 실행하는 몇 가지 사용자 지정 코드가 포함됩니다. 이 인터페이스의 구현은 직접 제공하거나 종속성 삽입 패턴을 사용하여 주입할 수 있습니다. **이 사용 사례는 UberJar로 처리할 수 있습니다.**

이전 버전의 예:

```java
public class ClassWhichHasAEMInterfacePassedIn {
    /**
     * Get the first length characters of the page title.
     */
    public String getTrimmedTitle(Page page, int length) {
         String title = page.getTitle();
         return StringUtils.left(title, length);
    }
}
```

후자의 예는 다음과 같습니다.

```java
@Component
@Service
public class ComponentWhichHasAEMInterfaceInjected implements TitleTrimmer {
    @Reference
    private PageManagerFactory pageManagerFactory;

    /**
     * Get the first length characters of the title of the page containing the provided Resource.
     */
    public String getTrimmedTitle(Resource resource, int length) {
        PageManager pageManager = pageManagerFactory.getPageManager(resource.getResourceResolver());
        Page page = pageManager.getContainingPage(resource);
        if (page == null) {
           return null;
        }
        String title = page.getTitle();
        return StringUtils.left(title, length);
    }
}
```

이러한 방법 중 하나를 유닛 테스트하기 위해 개발자는 JMockit [,](http://jmockit.github.io)Mockito [](https://mockito.org/), [JMock](https://www.jmock.org/), 또는 [](https://easymock.org/) EasymockEasymock등과 같은 조롱하는 프레임워크를 사용하여 참조된 AEM API에 대한 모의 오브젝트를 제작합니다. 이러한 샘플은 JMockit을 사용하지만 이러한 특정 사용 사례에서 이러한 프레임워크의 차이는 일반적으로 구적입니다.

```java
@RunWith(JMockit.class)
public class ClassWhichHasAEMInterfacePassedInTest {

    @Tested
    private ClassWhichHasAEMInterfacePassedIn instance;

    @Mocked
    private Page page;

    @Test
    public void test_that_long_string_is_trimmed() {
        new Expectations() {{
            page.getTitle();
            result = "a really really really really really long string";
        }};
        assertEquals("a really", instance.getTrimmedTitle(page, 8));
    }
}
```

```java
@RunWith(JMockit.class)
public class ComponentWhichHasAEMInterfaceInjectedTest {

    @Tested
    private ComponentWhichHasAEMInterfaceInjected instance;

    @Mocked
    private Page page;

    @Mocked
    private PageManager pageManager;

    @Injectable
    private PageManagerFactory pageManagerFactory;

    @Mocked
    private Resource resource;

    @Mocked
    private ResourceResolver resourceResolver;

    @Test
    public void test_that_long_string_is_trimmed() {
        new Expectations() {{
            resource.getResourceResolver();
            result = resourceResolver;
            pageManagerFactory.getPageManager(resourceResolver);
            result = pageManager;
            pageManager.getContainingPage(resource);
            result = page;
            page.getTitle();
            result = "a really really really really really long string";
        }};
        assertEquals("a really", instance.getTrimmedTitle(resource, 8));
    }
}
```

#### 사용 사례 #2 - API 구현 클래스를 호출하는 사용자 지정 코드 {#use-case-custom-code-which-calls-an-api-implementation-class}

이 사용 사례에서는 사용 사례 #1과 같은 인터페이스가 아닌, 콘크리트 클래스를 참조하는 AEM API에서 클래스의 정적 또는 인스턴스 메서드를 호출하는 작업이 포함됩니다.

```java
public class ClassWhichUsesAStaticMethodFromAPI {

    /**
     * Get a map of asset titles to asset objects.
     *
     * @param resource either an asset resource or a folder containing assets.
     * @return an map of titles to assets. if an asset doesn't have a title, the name is used instead.
     */
    public Map<String, Asset> getAssetTitles(Resource resource) {
        Iterator<Asset> assets = DamUtil.getAssets(resource);
        Map<String, Asset> result = new HashMap<String, Asset>();
        while (assets.hasNext()) {
            Asset asset = assets.next();
            String title = asset.getMetadataValue(DamConstants.DC_TITLE);
            if (title == null) {
                title = asset.getName();
            }
            result.put(title, asset);
        }
        return result;
    }
}
```

```java
public class ClassWhichUsesAnInstanceMethodFromAPI {

    /**
     * Count the number of paragraphs in a parsys.
     *
     * @param resource the parsys resource
     * @return the count
     */
    public int countParagraphs(Resource resource) {
        return new ParagraphSystem(resource).paragraphs().size();
    }
}
```

**이 사용 사례는 UberJar로 처리할 수 있습니다**. 그러나 성능 테스트를 위해 가능한 API를 비웃는 것이 좋습니다.

```java
@RunWith(JMockit.class)
public class ClassWhichUsesAStaticMethodFromAPITest {

    @Tested
    private ClassWhichUsesAStaticMethodFromAPI instance;

    @Mocked(stubOutClassInitialization = true)
    private DamUtil unusedDamUtil = null;

    @Mocked
    private Resource resource;

    @Test
    public void test_that_empty_iterator_produces_empty_map() {
        new Expectations() {
            {
                DamUtil.getAssets(resource);
                result = Collections.<Asset> emptySet().iterator();
            }
        };
        Map<String, Asset> result = new ClassWhichUsesAStaticMethodFromAPI().getAssetTitles(resource);
        assertNotNull(result);
        assertEquals(0, result.size());
    }
    @Test
    public void test_with_reference_search() {
        assertTrue(true);
    }
}
```

```java
@RunWith(JMockit.class)
public class ClassWhichUsesAnInstanceMethodFromAPITest {

    @Tested
    private ClassWhichUsesAnInstanceMethodFromAPI instance;

    @Mocked
    private Resource parsys;

    @Mocked
    private Paragraph firstPar;

    @Mocked
    private Paragraph secondPar;

    @Test
    public void test_empty_parsys_returns_zero() {
        new MockUp<ParagraphSystem>() {
            @Mock
            public void $init(Resource resource) {
                assertEquals(parsys, resource);
            }
            @Mock
            public List<Paragraph> paragraphs() {
                return Collections.<Paragraph> emptyList();
            }
        };
        assertEquals(0, instance.countParagraphs(parsys));
    }
}
```

#### 사용 사례 #3 - API에서 기본 클래스를 확장하는 사용자 지정 코드 {#use-case-custom-code-which-extends-a-base-class-from-the-api}

SCR 생성과 마찬가지로, 코드가 AEM API에서 기본 클래스(추상 또는 콘크리트)를 확장하는 경우 UberJar를 사용하여 테스트해야 **합니다** .

## Maven을 사용한 일반적인 개발 작업 {#common-development-tasks-with-maven}

### 컨텐츠 모듈에 경로를 추가하는 방법 {#how-to-add-paths-to-the-content-module}

컨텐츠 모듈에는 Maven이 구축한 AEM 패키지의 필터를 정의하는 src/main/content/META-INF/vault/filter.xml 파일이 포함되어 있습니다. Maven 원형에 의해 생성된 파일은 다음과 같습니다.

#### src/main/content/META-INF/vault/filter.xml {#src-main-content-meta-inf-vault-filter-xml}

```xml
<?xml version="1.0" encoding="UTF-8"?>
<workspaceFilter version="1.0">
    <filter root="/apps/myproject"/>
</workspaceFilter>
```

이 파일은 다양한 방법으로 사용됩니다.

* 패키지 `content-package-maven-plugin` 에 포함할 컨텐츠를 결정하기 위해
* VLT 도구를 사용하여 고려할 경로를 결정합니다.
* aem Package Manager에서 패키지가 다시 빌드되는 경우, 이 설정은

응용 프로그램의 요구 사항에 따라 다음과 같이 더 많은 컨텐츠를 포함하도록 이러한 경로에 추가할 수 있습니다.

* 롤아웃 구성
* 블루프린트
* 워크플로우 모델
* 디자인 페이지
* 샘플 컨텐츠

패스에 추가하려면 더 많은 `<filter>` 요소를 추가합니다.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<workspaceFilter version="1.0">
    <filter root="/apps/myproject"/>
    <filter root="/content/myproject/sample-content"/>
</workspaceFilter>
```

#### 동기화하지 않고 패키지에 경로 추가 {#adding-paths-to-the-package-without-syncing-them}

content-package-maven-plugin을 통해 빌드했지만 파일 시스템과 저장소 간에 동기화해서는 안 되는 파일을 패키지에 추가해야 하는 경우, `.vltignore` 파일을 사용할 수 있습니다. 이러한 파일은 .gitignore 파일과 같은 [구문을](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html) 가집니다.

예를 들어 원본은 `.vltignore` 파일을 사용하여 번들의 일부로 설치된 JAR 파일이 파일 시스템으로 다시 동기화되지 않도록 합니다.

#### src/main/content/jcr_root/apps/myproject/install/.vltignore {#src-main-content-jcr-root-apps-myproject-install-vltignore}

```xml
*.jar
```

#### 패키지에 추가하지 않고 경로 동기화 {#syncing-paths-without-adding-them-to-the-package}

경우에 따라 파일 시스템과 저장소 간에 특정 경로를 동기화된 상태로 유지하려고 하지만 AEM에 설치되도록 패키지에 포함하지는 않을 수 있습니다.

대표적인 것이 `/libs/foundation` 길이다. 개발 목적으로 파일 시스템에서 이 경로의 내용을 사용할 수 있도록 할 수 있습니다. 이렇게 하면 IDE에서 JSP를 포함하는 JSP를 확인할 수 있습니다 `/libs`. 그러나 구성 요소에는 사용자 지정 구현에 의해 수정되어서는 안 되는 제품 코드가 포함되어 있기 때문에 빌드하는 패키지에 해당 부분을 포함시키지 `/libs` 않을 수 있습니다.

이를 위해 파일을 제공할 수 있습니다 `src/main/content/META-INF/vault/filter-vlt.xml`. 이 파일이 있는 경우 VLT 도구(예: 수행 및 설정 시 `vlt up` 또는 설정 시)에 `vlt ci`사용됩니다 `vlt sync` . content-package-maven-plugin은 패키지를 만들 `src/main/content/META-INF/vault/filter.xml` 때 파일을 계속 사용합니다.

예를 들어, 로컬에서 개발용으로 `/libs/foundation` 사용할 수 있지만 패키지에만 포함하려면 다음 두 파일 `/apps/myproject` 을 사용하십시오.

#### src/main/content/META-INF/vault/filter.xml {#src-main-content-meta-inf-vault-filter-xml-1}

```xml
<?xml version="1.0" encoding="UTF-8"?>
<workspaceFilter version="1.0">
    <filter root="/apps/myproject"/>
</workspaceFilter>
```

#### src/main/content/META-INF/vault/filter-vlt.xml {#src-main-content-meta-inf-vault-filter-vlt-xml}

```xml
<?xml version="1.0" encoding="UTF-8"?>
<workspaceFilter version="1.0">
    <filter root="/libs/foundation"/>
    <filter root="/apps/myproject"/>
</workspaceFilter>
```

패키지에 이러한 파일을 포함하지 않도록 maven-resources-plugin을 다시 구성해야 합니다.패키지 설치 시 filter.xml 파일은 적용되지 않지만 패키지 관리자를 사용하여 패키지를 다시 빌드할 때만 적용됩니다.

콘텐트 `<resources>` 창의 섹션을 다음과 같이 변경합니다.

#### src/main/content/pom.xml {#src-main-content-pom-xml}

```xml
<!-- ... -->
<resources>
 <resource>
  <directory>src/main/content/jcr_root</directory>
  <filtering>false</filtering>
  <excludes>
   <exclude>**/.vlt</exclude>
   <exclude>**/.vltignore</exclude>
   <exclude>libs/</exclude>
  </excludes>
 </resource>
</resources>
<!-- ... -->
```

### How to Work with JSPs {#how-to-work-with-jsps}

지금까지 설명한 Maven 설정은 구성 요소와 해당 JSP를 포함할 수 있는 컨텐츠 패키지를 생성합니다. 하지만 Maven은 이러한 파일을 컨텐츠 패키지에 포함된 다른 파일로 취급하여 JSP로 인식하지 못합니다.

결과 구성 요소는 AEM에서 모두 동일하게 작동하지만 JSP에 대해 Maven이 인식하도록 하는 데는 두 가지 주요 이점이 있습니다

* JSP에 오류가 있는 경우 Maven이 실패할 수 있으므로 빌드 시 이러한 오류가 표시되므로 AEM에서 처음 컴파일된 시기가 아닙니다
* Maven 프로젝트를 가져올 수 있는 IDE의 경우 JSP에서 코드 완성 및 태그 라이브러리 지원을 사용할 수도 있습니다

이 설정을 사용하려면 다음 두 가지가 필요합니다.

1. 태그 라이브러리 종속성 추가
1. Maven 컴파일 프로세스의 일부로 JSP 컴파일

#### 태그 라이브러리 종속성 추가 {#adding-tag-library-dependencies}

모듈의 POM에 아래의 종속성을 추가해야 `content` 합니다.

>[!NOTE]
>
>위의 AEM 제품 종속성 [가져오기에 설명된 대로 제품 종속성을](#importingaemproductdependencies) 가져오지 않으면 위의 종속성 추가에 설명된 대로 AEM 설정과 일치하는 버전과 함께 상위 POM에 해당 종속성을 추가해야 [합니다](#addingdependencies) . 아래 각 항목에 있는 주석에는 종속성 파인더에서 검색할 패키지가 표시됩니다.

>[!NOTE]
>
>아티팩트는 `com.adobe.granite.xssprotection` cq-quickstart-product-dependencies POM에 포함되지 않으며 종속성 파인더에서 얻은 대로 완전한 Maven 좌표가 필요합니다.

#### JSP를 Maven 컴파일 단계의 일부로 컴파일하기 {#compiling-jsps-as-part-of-the-maven-compile-phase}

Maven의 `compile` 단계에서 JSP를 컴파일하기 위해 Apache Sling의 [Maven JspC 플러그인을](https://sling.apache.org/documentation/development/jspc.html) 아래와 같이 사용합니다.

* 목표에 대한 실행 `jspc` (기본적으로 `compile` 단계와 바인딩되므로 단계를 명시적으로 지정할 필요가 없음)

* JSP를 `${project.build.directory}/jsps-to-compile`
* 결과를 다음으로 출력합니다( `${project.build.directory}/ignoredjspc` 이렇게 변환됨 `myproject/content/target/ignoredjspc`).

* maven-resources-plugin을 설정하여 JSP를 generate-sources 단계 `${project.build.directory}/jsps-to-compile` `libs/` 에 복사하고 이 폴더를 복사하지 않도록 구성합니다(이는 AEM 제품 코드이고 프로젝트를 컴파일하기 위해 종속성을 발생시키고자 하지 않으며, 컴파일되었는지 확인할 필요가 없기 때문입니다.

위에 명시된 주요 목표는 JSP의 유효성을 확인하고 오류가 있는 경우 빌드 프로세스가 실패하는지 확인하는 것입니다. 이러한 이유로 무시된 별도의 디렉토리에 컴파일됩니다(그리고 곧 삭제됨).

Maven JspC Plugin의 결과는 OSGi 번들의 일부로 번들로 묶어서 배포할 수도 있지만, 이것은 다른 의미와 부작용으로 JSP의 유효성 검사 목적을 넘어섭니다.

JSP에서 컴파일된 클래스를 삭제하기 위해 아래와 같이 Maven Clean 플러그인을 설정합니다. Maven JspC 플러그인의 결과를 검사하려는 경우, JavaScript 플러그인 `mvn compile` 을 실행한 `myproject/content` 후 결과를 찾을 수 `myproject/content/target/ignoredjspc`있습니다.

#### myproject/content/pom.xml {#myproject-content-pom-xml}

```xml
<build>
  <!-- ... -->
  <plugins>
    <!-- ... -->
    <plugin>
      <artifactId>maven-resources-plugin</artifactId>
      <executions>
        <execution>
          <id>copy-resources</id>
          <phase>generate-sources</phase>
          <goals>
            <goal>copy-resources</goal>
          </goals>
          <configuration>
            <outputDirectory>${project.build.directory}/jsps-to-compile</outputDirectory>
            <resources>
              <resource>
                <directory>src/main/content/jcr_root</directory>
                <excludes>
                  <exclude>libs/**</exclude>
                </excludes>
              </resource>
            </resources>
          </configuration>
        </execution>
      </executions>
    </plugin>
    <plugin>
      <groupId>org.apache.sling</groupId>
      <artifactId>maven-jspc-plugin</artifactId>
      <version>2.0.6</version>
      <executions>
        <execution>
          <id>compile-jsp</id>
          <goals>
            <goal>jspc</goal>
          </goals>
          <configuration>
            <jasperClassDebugInfo>false</jasperClassDebugInfo>
            <sourceDirectory>${project.build.directory}/jsps-to-compile</sourceDirectory>
            <outputDirectory>${project.build.directory}/ignoredjspc</outputDirectory>
          </configuration>
        </execution>
      </executions>
    </plugin>
    <plugin>
      <artifactId>maven-clean-plugin</artifactId>
      <executions>
        <execution>
          <id>remove-compiled-jsps</id>
          <goals>
            <goal>clean</goal>
          </goals>
          <phase>process-classes</phase>
          <configuration>
            <excludeDefaultDirectories>true</excludeDefaultDirectories>
            <filesets>
              <fileset>
                <directory>${project.build.directory}/jsps-to-compile</directory>
                <directory>${project.build.directory}/ignoredjspc</directory>
              </fileset>
            </filesets>
          </configuration>
        </execution>
      </executions>
    </plugin>
  </plugins>
</build>
```

>[!NOTE]
>
>JSP 코드를 실제로 JSP 코드 `/libs` 에서 사용하는지 여부(즉, JSP가 JSP 포함)에 따라 컴파일하기 위해 복사되는 JSP를 세분화해야 합니다.
>
>예를 들어, 포함하는 경우 `/libs/foundation/global.jsp`위의 구성 `maven-resources-plugin` 대신 다음 구성을 사용하여 완전히 건너뛸 수 있습니다 `/libs`.
>
>
```
> <resource>  
>           <directory>src/main/content/jcr_root</directory>  
>           <includes>  
>                   <include>apps/**</include>  
>                   <include>libs/foundation/global.jsp</include>
>       </includes>  
>   </resource>  
>```

### SCM 시스템 사용 방법 {#how-to-work-with-scm-systems}

SCM(소스 구성 관리)을 사용할 때

* VCS는 파일 시스템의 비소스 객체를 무시합니다.
* VLT는 VCS의 객체를 무시하고 저장소에 체크 인하지 않습니다.

>[!NOTE]
>
>이 설명은 Maven이 SCM과 함께 작동하도록 구성하는 방법에 대해서는 다루지 않습니다. SCM은 Maven POM 참조 [및](https://maven.apache.org/pom.html#SCM) Maven SCM 플러그인의 설명서에서 [](https://maven.apache.org/scm/)철저히 설명되어 있습니다.

#### SCM에서 제외할 패턴 {#patterns-to-exclude-from-scm}

다음은 SCM에서 포함할 일반적인 패턴 목록입니다. 예: git을 사용하는 경우 프로젝트의 `.gitignore` 파일에 추가할 수 있습니다.

#### sample .gitgnore {#sample-gitignore}

```shell
# Ignore VLT files
.vlt
.vlt-sync.log
.vlt-sync-config.properties

# Ignore Quickstart launches in the source tree
license.properties
crx-quickstart

# Ignore compilation results
target

# Ignore IDE and Operating System artifacts
.idea
.classpath
.metadata
.project
.settings
maven-eclipse.xml
*.iml
*.ipr
*.iws
.DS_Store
```

#### VLT에서 SCM 제어 파일 무시 {#ignoring-scm-control-files-in-vlt}

보관소에 체크 인하지 않으려는 컨텐츠 소스 트리에 SCM 제어 파일이 있을 수 있습니다.

다음 상황을 생각해 보십시오.

원형은 설치된 번들 jar 파일이 파일 시스템으로 다시 동기화되지 않도록 .vltignore 파일을 이미 만들었습니다.

#### src/main/content/jcr_root/apps/myproject/install/.vltignore {#src-main-content-jcr-root-apps-myproject-install-vltignore-1}

```shell
*.jar
```

SCM에서 이 파일을 원하지 않을 수 있으므로 git을 사용하는 경우 해당 파일을 추가합니다. `gitignore` 파일:

#### src/main/content/jcr_root/apps/myproject/install/.gitignore {#src-main-content-jcr-root-apps-myproject-install-gitignore}

```shell
*.jar
```

. `gitignore` 파일도 저장소로 이동해서는 안 됩니다. `vltignore` 파일을 포함하려면 확장해야 합니다. `gitignore` 파일:

#### src/main/content/jcr_root/apps/myproject/install/.vltignore {#src-main-content-jcr-root-apps-myproject-install-vltignore-2}

```shell
*.jar
.gitignore
```

### 배포 프로필로 작업하는 방법 {#how-to-work-with-deployment-profiles}

빌드 프로세스가 지속적인 통합 프로세스와 같은 대규모 개발 라이프사이클 관리 설정의 일부일 경우 개발자의 로컬 인스턴스가 아닌 다른 컴퓨터에 배포해야 하는 경우가 많습니다.

이러한 시나리오의 경우 새로운 [Maven 빌드 프로필을](https://maven.apache.org/guides/introduction/introduction-to-profiles.html) 프로젝트의 POM에 쉽게 추가할 수 있습니다.

아래 예에는 작성자 및 게시 인스턴스에 대한 호스트 이름 및 포트를 재정의하는 프로필 `integrationServer`이 추가됩니다. 아래 표시된 대로 프로젝트 루트에서 maven을 실행하여 이러한 서버에 배포할 수 있습니다.

```shell
# install on integration test author
$ mvn -PautoInstallPackage -PintegrationServer install

# install on integration test publisher
$ mvn -PautoInstallPackagePublish -PintegrationServer install
```

#### myproject/pom.xml {#myproject-pom-xml}

```xml
<profiles>

    <!-- ... -->

    <profile>
        <id>integrationServer</id>
        <properties>
            <crx.host>dev-author.intranet</crx.host>
            <crx.port>5502</crx.port>
            <publish.crx.host>dev-publish.intranet</publish.crx.host>
            <publish.crx.port>5503</publish.crx.port>
        </properties>
    </profile>
</profiles>
```

### AEM Communities 사용 방법 {#how-to-work-with-aem-communities}

AEM Communities 기능에 대한 라이선스를 부여하면 추가 API jar가 필요합니다.

자세한 내용은 커뮤니티에 대한 [Maven 사용을 참조하십시오.](/help/communities/maven.md)
