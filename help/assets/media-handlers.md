---
title: 미디어 핸들러 및 워크플로우를 사용하여 자산 처리
description: 미디어 핸들러 및 워크플로우를 사용하여 디지털 에셋에서 작업을 수행하는 방법에 대해 알아봅니다.
mini-toc-levels: 1
contentOwner: AG
role: User
feature: Workflow,Renditions
exl-id: cfd6c981-1a35-4327-82d7-cf373d842cc3
source-git-commit: acc4b78f551e0e0694f41149fff7e24d855f504f
workflow-type: tm+mt
source-wordcount: '2161'
ht-degree: 4%

---

# 미디어 핸들러 및 워크플로우를 사용하여 자산 처리 {#processing-assets-using-media-handlers-and-workflows}

[!DNL Adobe Experience Manager Assets] 에는 자산을 처리하는 기본 워크플로우 및 미디어 핸들러 세트가 포함되어 있습니다. 워크플로는 에셋에서 실행할 작업을 정의한 다음 특정 작업을 미디어 핸들러로 위임합니다(예: 썸네일 생성 또는 메타데이터 추출).

특정 MIME 유형의 자산이 업로드되면 자동으로 실행되도록 워크플로우를 구성할 수 있습니다. 처리 단계는 일련의 [!DNL Assets] 미디어 핸들러. [!DNL Experience Manager] 일부 제공 [내장 처리기,](#default-media-handlers) 및 추가 필드는 다음 중 하나일 수 있습니다. [주문 개발](#creating-a-new-media-handler) 또는에 프로세스를 위임하여 정의됩니다. [명령줄 도구](#command-line-based-media-handler).

미디어 핸들러는 의 서비스입니다. [!DNL Assets] 에셋에 대해 특정 작업을 수행합니다. 예를 들어 MP3 오디오 파일이에 업로드되는 경우 [!DNL Experience Manager]워크플로우는 메타데이터를 추출하고 썸네일을 생성하는 MP3 핸들러를 트리거합니다. 미디어 핸들러는 일반적으로 워크플로우와 함께 사용됩니다. 가장 일반적인 MIME 유형은 내에서 지원됩니다. [!DNL Experience Manager]. 자산에 대해 워크플로우 확장/만들기, 미디어 핸들러 확장/만들기 또는 미디어 핸들러를 비활성화/활성화하여 특정 작업을 수행할 수 있습니다.

>[!NOTE]
>
>다음을 참조하십시오. [에셋 지원 형식](assets-formats.md) 에서 지원하는 모든 형식에 대한 설명 페이지입니다. [!DNL Assets] 각 형식에 대해 지원되는 기능을 사용할 수 있습니다.

## 기본 미디어 핸들러 {#default-media-handlers}

다음 미디어 핸들러는 내에서 사용할 수 있습니다. [!DNL Assets] 가장 일반적인 MIME 유형을 처리합니다.

<!-- TBD: Java versions shouldn't be set to 1.5. Must be updated.
-->

| 핸들러 이름 | 서비스 이름(시스템 콘솔) | 지원되는 MIME 유형 |
|--------------|--------------------------------------|----------------------|
| [!UICONTROL TextHandler] | com.day.cq.dam.core.impl.handler.TextHandler | text/plain |
| [!UICONTROL PdfHandler] | com.day.cq.dam.handler.standard.pdf.PdfHandler | <ul><li>application/pdf</li><li>application/illustrator</li></ul> |
| [!UICONTROL JpegHandler] | com.day.cq.dam.core.impl.handler.JpegHandler | image/jpeg |
| [!UICONTROL Mp3Handler] | com.day.cq.dam.handler.standard.mp3.Mp3Handler | audio/mpeg<br><b>중요 사항</b> - MP3 파일을 업로드할 때 [타사 라이브러리를 사용하여 처리됨](https://www.zxdr.it/programmi/SistEvolBDD/LibJava/doc/de/vdheide/mp3/MP3File.html). MP3에 가변 비트율(VBR)이 있는 경우 라이브러리는 정확하지 않은 근사 길이를 계산합니다. |
| [!UICONTROL ZipHandler] | com.day.cq.dam.handler.standard.zip.ZipHandler | <ul><li>application/java-archive </li><li> application/zip</li></ul> |
| [!UICONTROL PictHandler] | com.day.cq.dam.handler.standard.pict.PictHandler | image/pict |
| [!UICONTROL StandardImageHandler] | com.day.cq.dam.core.impl.handler.StandardImageHandler | <ul><li>image/gif </li><li> image/png </li> <li>application/photoshop </li> <li>image/jpeg </li><li> image/tiff </li> <li>image/x-ms-bmp </li><li> image/bmp</li></ul> |
| [!UICONTROL MSOfficeHandler] | com.day.cq.dam.handler.standard.msoffice.MSOfficeHandler | application/msword |
| [!UICONTROL MSPowerPointHandler] | com.day.cq.dam.handler.standard.msoffice.MSPowerPointHandler | application/vnd.ms-powerpoint |
| [!UICONTROL OpenOfficeHandler] | com.day.cq.dam.handler.standard.ooxml.OpenOfficeHandler | <ul><li>application/vnd.openxmlformats-officedocument.wordprocessingml.document</li><li> application/vnd.openxmlformats-officedocument.spreadsheetml.sheet</li><li> application/vnd.openxmlformats-officedocument.presentationml.presentation</li></ul> |
| [!UICONTROL EPubHandler] | com.day.cq.dam.handler.standard.epub.EPubHandler | application/epub+zip |
| [!UICONTROL GenericAssetHandler] | com.day.cq.dam.core.impl.handler.GenericAssetHandler | 자산에서 데이터를 추출할 다른 처리기가 없는 경우 대체 |

{style="table-layout:auto"}

모든 처리기는 다음 작업을 수행합니다.

* 에셋에서 사용 가능한 모든 메타데이터 추출
* 에셋의 축소판 이미지 만들기.

활성 미디어 처리기를 보려면 다음을 수행하십시오.

1. 브라우저에서 다음 위치로 이동합니다 `https://localhost:4502/system/console/components`.
1. 클릭 `com.day.cq.dam.core.impl.store.AssetStoreImpl`.
1. 모든 활성 미디어 처리기가 포함된 목록이 표시됩니다. 예:

![chlimage_1-437](assets/chlimage_1-437.png)

## 워크플로우의 미디어 핸들러를 사용하여 자산에 대한 작업을 수행합니다 {#using-media-handlers-in-workflows-to-perform-tasks-on-assets}

미디어 핸들러는 일반적으로 워크플로와 함께 사용되는 서비스입니다.

[!DNL Experience Manager] 에는 에셋을 처리하는 몇 가지 기본 워크플로가 있습니다. 이를 보려면 워크플로 콘솔을 열고 **[!UICONTROL 모델]** 탭: 다음으로 시작하는 워크플로우 제목 [!DNL Assets] 는 에셋별 에셋입니다.

특정 요구 사항에 따라 에셋을 처리하기 위해 기존 워크플로를 확장하고 새 워크플로를 만들 수 있습니다.

The following example shows how to enhance the **[!UICONTROL AEM Assets Synchronization]** workflow so that sub-assets are generated for all assets except PDF documents.

### 미디어 핸들러 비활성화 또는 활성화 {#disabling-enabling-a-media-handler}

미디어 핸들러는 Apache Felix 웹 관리 콘솔을 통해 비활성화하거나 활성화할 수 있습니다. 미디어 핸들러가 비활성화되면 에셋에서 해당 작업이 수행되지 않습니다.

미디어 핸들러를 활성화/비활성화하려면 다음 작업을 수행하십시오.

1. 브라우저에서 다음 위치로 이동합니다 `https://<host>:<port>/system/console/components`.
1. 클릭 **[!UICONTROL 사용 안 함]** 미디어 핸들러의 이름 옆에 있습니다. 예: `com.day.cq.dam.handler.standard.mp3.Mp3Handler`.
1. 페이지 새로 고침: 미디어 핸들러 옆에 비활성화된 것을 나타내는 아이콘이 표시됩니다.
1. 미디어 처리기를 사용하려면 다음을 클릭하십시오. **[!UICONTROL 사용]** 미디어 핸들러의 이름 옆에 있습니다.

### 새 미디어 핸들러 만들기 {#creating-a-new-media-handler}

새 미디어 유형을 지원하거나 에셋에서 특정 작업을 실행하려면 새 미디어 핸들러를 만들어야 합니다. 이 섹션에서는 진행 방법에 대해 설명합니다.

#### 중요한 클래스 및 인터페이스 {#important-classes-and-interfaces}

구현을 시작하는 가장 좋은 방법은 대부분의 항목을 처리하고 합리적인 기본 동작을 제공하는 제공된 추상적인 구현으로부터 상속하는 것입니다. `com.day.cq.dam.core.AbstractAssetHandler` 클래스.

이 클래스는 이미 추상 서비스 설명자를 제공합니다. 따라서 이 클래스에서 상속하고 maven-sling-plugin을 사용하는 경우 상속 플래그를 로 설정해야 합니다. `true`.

다음 방법을 구현합니다.

* `extractMetadata()`: 사용 가능한 모든 메타데이터를 추출합니다.
* `getThumbnailImage()`: 전달된 에셋에서 썸네일 이미지를 생성합니다.
* `getMimeTypes()`: 에셋 MIME 유형을 반환합니다.

다음은 예제 템플릿입니다.

```Java
package my.own.stuff; /** * @scr.component inherit="true" * @scr.service */ public class MyMediaHandler extends com.day.cq.dam.core.AbstractAssetHandler { // implement the relevant parts }
```

인터페이스 및 클래스는 다음과 같습니다.

* `com.day.cq.dam.api.handler.AssetHandler` 인터페이스: 이 인터페이스에서는 특정 MIME 유형에 대한 지원을 추가하는 서비스에 대해 설명합니다. 새 MIME 유형을 추가하려면 이 인터페이스를 구현해야 합니다. 인터페이스에는 특정 문서를 가져오고 내보내는 방법, 축소판을 만들고 메타데이터를 추출하는 방법이 포함되어 있습니다.
* `com.day.cq.dam.core.AbstractAssetHandler` 클래스: 이 클래스는 다른 모든 에셋 처리기 구현의 기초 역할을 하며 일반적으로 사용되는 기능을 제공합니다.
* `com.day.cq.dam.core.AbstractSubAssetHandler` class:
   * 이 클래스는 다른 모든 에셋 핸들러 구현의 기반으로 사용되며 하위 에셋 추출을 위해 일반적으로 사용되는 기능과 함께 일반적으로 사용되는 기능을 제공합니다.
   * 구현을 시작하는 가장 좋은 방법은 대부분의 항목을 처리하고 적절한 기본 동작을 제공하는 제공된 추상 구현에서 상속하는 것입니다. com.day.cq.dam.core.AbstractAssetHandler 클래스.
   * 이 클래스는 이미 추상 서비스 설명자를 제공합니다. 따라서 이 클래스에서 상속하고 maven-sling-plugin을 사용하는 경우 상속 플래그를 true로 설정해야 합니다.

다음과 같은 방법을 구현해야 합니다.

* `extractMetadata()`: 이 메서드는 사용 가능한 모든 메타데이터를 추출합니다.
* `getThumbnailImage()`: 이 메서드는 전달된 에셋에서 썸네일 이미지를 생성합니다.
* `getMimeTypes()`: 이 메서드는 자산 MIME 유형을 반환합니다.

다음은 예제 템플릿입니다.

package my.own.stuff; /&amp;ast;&amp;ast; &amp;ast; @scr.component inherit=&quot;true&quot; &amp;ast; @scr.service &amp;ast;/ public class MyMediaHandler extends com.day.cq.dam.core.AbstractAssetHandler { // implement the related parts }

인터페이스 및 클래스는 다음과 같습니다.

* `com.day.cq.dam.api.handler.AssetHandler` 인터페이스: 이 인터페이스에서는 특정 MIME 유형에 대한 지원을 추가하는 서비스에 대해 설명합니다. 새 MIME 유형을 추가하려면 이 인터페이스를 구현해야 합니다. 인터페이스에는 특정 문서를 가져오고 내보내는 방법, 축소판을 만들고 메타데이터를 추출하는 방법이 포함되어 있습니다.
* `com.day.cq.dam.core.AbstractAssetHandler` 클래스: 이 클래스는 다른 모든 에셋 처리기 구현의 기초 역할을 하며 일반적으로 사용되는 기능을 제공합니다.
* `com.day.cq.dam.core.AbstractSubAssetHandler` 클래스: 이 클래스는 다른 모든 에셋 처리기 구현의 기초 역할을 하며 하위 에셋 추출에 공통으로 사용되는 기능과 함께 공통으로 사용되는 기능을 제공합니다.

#### 예: 특정 텍스트 핸들러 만들기 {#example-create-a-specific-text-handler}

이 섹션에서는 워터마크로 썸네일을 생성하는 특정 텍스트 처리기를 만듭니다.

다음과 같이 진행합니다.

을(를) 참조하십시오 [개발 도구](../sites-developing/dev-tools.md) 를 사용하여 Eclipse를 설치하고 설정하려면 [!DNL Maven] 플러그인을 추가하고, 및에 필요한 종속성 설정 [!DNL Maven] 프로젝트.

다음 절차를 수행한 후 TXT 파일을에 업로드할 때 [!DNL Experience Manager]로 설정하면 파일의 메타데이터가 추출되고 워터마크가 있는 두 개의 썸네일이 생성됩니다.

1. Eclipse에서 만들기 `myBundle` [!DNL Maven] 프로젝트:

   1. 메뉴 모음에서 를 클릭합니다 **[!UICONTROL 파일]** > **[!UICONTROL 신규]** > **[!UICONTROL 기타]**.
   1. 대화 상자에서 다음을 확장합니다. [!DNL Maven] 폴더, 선택 [!DNL Maven] 프로젝트 및 클릭 **[!UICONTROL 다음]**.
   1. 단순 프로젝트 만들기 상자와 기본 작업 공간 위치 사용 상자를 선택한 다음 를 클릭합니다 **[!UICONTROL 다음]**.
   1. 정의 [!DNL Maven] 프로젝트:

      * 그룹 ID: `com.day.cq5.myhandler`.
      * 아티팩트 ID: myBundle.
      * 이름: 내 [!DNL Experience Manager] 번들.
      * 설명: 내 설명입니다. [!DNL Experience Manager] 번들.
   1. 클릭 **[!UICONTROL 완료]**.


1. 설정 [!DNL Java] 버전 1.5로의 컴파일러:

   1. 마우스 오른쪽 단추 클릭 `myBundle` 프로젝트, 선택 [!UICONTROL 속성].
   1. 선택 [!UICONTROL Java 컴파일러] 및 다음 속성을 1.5로 설정합니다.

      * 컴파일러 규정 준수 수준
      * 생성된 .class 파일 호환성
      * 소스 호환성
   1. **[!UICONTROL 확인]**&#x200B;을 클릭합니다. 대화 상자 창에서 다음을 클릭합니다. **[!UICONTROL 예]**.


1. 의 코드를 바꿉니다. `pom.xml` 다음 코드가 있는 파일:

   ```xml
   <project xmlns="https://maven.apache.org/POM/4.0.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <!-- ====================================================================== -->
    <!-- P A R E N T P R O J E C T D E S C R I P T I O N -->
    <!-- ====================================================================== -->
    <parent>
     <groupId>com.day.cq.dam</groupId>
     <artifactId>dam</artifactId>
     <version>5.2.14</version>
     <relativePath>../parent</relativePath>
    </parent>
    <!-- ====================================================================== -->
    <!-- P R O J E C T D E S C R I P T I O N -->
    <!-- ====================================================================== -->
    <groupId>com.day.cq5.myhandler</groupId>
    <artifactId>myBundle</artifactId>
    <name>My CQ5 bundle</name>
    <version>0.0.1-SNAPSHOT</version>
    <description>This is my CQ5 bundle</description>
    <packaging>bundle</packaging>
    <!-- ====================================================================== -->
    <!-- B U I L D D E F I N I T I O N -->
    <!-- ====================================================================== -->
    <build>
     <plugins>
      <plugin>
       <groupId>org.apache.felix</groupId>
       <artifactId>maven-scr-plugin</artifactId>
      </plugin>
      <plugin>
       <groupId>org.apache.sling</groupId>
       <artifactId>maven-sling-plugin</artifactId>
       <configuration>
        <slingUrlSuffix>/libs/dam/install/</slingUrlSuffix>
       </configuration>
      </plugin>
      <plugin>
       <groupId>org.apache.felix</groupId>
       <artifactId>maven-bundle-plugin</artifactId>
       <extensions>true</extensions>
       <configuration>
        <instructions>
         <Bundle-Category>cq5</Bundle-Category>
         <Export-Package> com.day.cq5.myhandler </Export-Package>
        </instructions>
       </configuration>
      </plugin>
     </plugins>
    </build>
    <!-- ====================================================================== -->
    <!-- D E P E N D E N C I E S -->
    <!-- ====================================================================== -->
    <dependencies>
     <dependency>
      <groupId>com.day.cq.dam</groupId>
      <artifactId>cq-dam-api</artifactId>
      <version>5.2.10</version>
      <scope>provided</scope>
     </dependency>
     <dependency>
      <groupId>com.day.cq.dam</groupId>
      <artifactId>cq-dam-core</artifactId>
      <version>5.2.10</version>
      <scope>provided</scope>
     </dependency>
     <dependency>
      <groupId>com.day.cq</groupId>
      <artifactId>cq-commons</artifactId>
     </dependency>
     <dependency>
      <groupId>javax.jcr</groupId>
      <artifactId>jcr</artifactId>
     </dependency>
     <dependency>
      <groupId>org.apache.felix</groupId>
      <artifactId>org.osgi.compendium</artifactId>
     </dependency>
     <dependency>
      <groupId>org.slf4j</groupId>
      <artifactId>slf4j-api</artifactId>
     </dependency>
     <dependency>
      <groupId>commons-lang</groupId>
      <artifactId>commons-lang</artifactId>
     </dependency>
     <dependency>
      <groupId>commons-collections</groupId>
      <artifactId>commons-collections</artifactId>
     </dependency>
     <dependency>
      <groupId>commons-io</groupId>
      <artifactId>commons-io</artifactId>
     </dependency>
     <dependency>
      <groupId>com.day.commons</groupId>
      <artifactId>day-commons-gfx</artifactId>
     </dependency>
     <dependency>
      <groupId>com.day.commons</groupId>
      <artifactId>day-commons-text</artifactId>
     </dependency>
     <dependency>
      <groupId>com.day.cq.workflow</groupId>
      <artifactId>cq-workflow-api</artifactId>
     </dependency>
     <dependency>
      <groupId>com.day.cq.wcm</groupId>
      <artifactId>cq-wcm-foundation</artifactId>
      <version>5.2.22</version>
     </dependency>
    </dependencies>
   ```

1. 패키지 만들기 `com.day.cq5.myhandler` 다음을 포함하는 [!DNL Java] 클래스 `myBundle/src/main/java`:

   1. myBundle에서 마우스 오른쪽 단추를 클릭합니다. `src/main/java`새로 만들기, 패키지 순으로 선택합니다.
   1. 이름 지정 `com.day.cq5.myhandler` 마침을 클릭합니다.

1. 만들기 [!DNL Java] 클래스 `MyHandler`:

   1. 위치 [!DNL Eclipse], 아래 `myBundle/src/main/java`을(를) 마우스 오른쪽 단추로 클릭합니다. `com.day.cq5.myhandler` 패키지. 선택 [!UICONTROL 신규], 그런 다음 [!UICONTROL 클래스].
   1. 대화 상자 창에서 이름을 로 지정합니다. [!DNL Java] 클래스 `MyHandler` 및 클릭 [!UICONTROL 완료]. [!DNL Eclipse] 파일을 만들고 엽니다. `MyHandler.java`.
   1. 위치 `MyHandler.java` 기존 코드를 다음으로 바꾼 다음 변경 내용을 저장합니다.

   ```java
   package com.day.cq5.myhandler;
   import java.awt.Color;
   import java.awt.Rectangle;
   import java.awt.image.BufferedImage;
   import java.io.IOException;
   import java.io.InputStream;
   import java.io.InputStreamReader;
   import javax.jcr.Node;
   import javax.jcr.RepositoryException;
   import javax.jcr.Session;
   import org.apache.commons.io.IOUtils;
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   import com.day.cq.dam.api.metadata.ExtractedMetadata;
   import com.day.cq.dam.core.AbstractAssetHandler;
   import com.day.image.Font;
   import com.day.image.Layer;
   import com.day.cq.wcm.foundation.ImageHelper;
   
   /**
    * The <code>MyHandler</code> can extract text files
    * @scr.component inherit="true" immediate="true" metatype="false"
    * @scr.service
    *
    **/
   
   public class MyHandler extends AbstractAssetHandler {
    /** * Logger instance for this class. */
    private static final Logger log = LoggerFactory.getLogger(MyHandler.class);
    /** * Music icon margin */
    private static final int MARGIN = 10;
    /** * @see com.day.cq.dam.api.handler.AssetHandler#getMimeTypes() */
    public String[] getMimeTypes() {
     return new String[] {"text/plain"};
    }
   
    public ExtractedMetadata extractMetadata(Node asset) {
     ExtractedMetadata extractedMetadata = new ExtractedMetadata();
     InputStream data = getInputStream(asset);
     try {
      // read text data
      InputStreamReader reader = new InputStreamReader(data);
      char[] buffer = new char[4096];
      String text = "";
      while (reader.read(buffer) != -1) {
       text += new String(buffer);
      }
      reader.close();
      long wordCount = this.wordCount(text);
      extractedMetadata.setProperty("text", text);
      extractedMetadata.setMetaDataProperty("Word Count",wordCount);
      setMimetype(extractedMetadata, asset);
     } catch (Throwable t) {
      log.error("handling error: " + t.toString(), t);
     } finally {
      IOUtils.closeQuietly(data);
     }
     return extractedMetadata; }
    // ----------------------< helpers >----------------------------------------
    protected BufferedImage getThumbnailImage(Node node) {
     ExtractedMetadata metadata = extractMetadata(node);
     final String text = (String) metadata.getProperty("text");
     // create text layer
     final Layer layer = new Layer(500, 600, Color.WHITE);
     layer.setPaint(Color.black);
     Font font = new Font("Arial", 12);
     String displayText = this.getDisplayText(text, 600, 12);
     if(displayText!=null && displayText.length() > 0) {
      // commons-gfx Font class would throw IllegalArgumentException on empty or null text
      layer.drawText(10, 10, 500, 600, displayText, font, Font.ALIGN_LEFT, 0, 0);
     }
     // create watermark and merge with text layer
     Layer watermarkLayer;
     try {
      final Session session = node.getSession();
      watermarkLayer = ImageHelper.createLayer(session, "/content/dam/we-retail/en/products/apparel/gloves/Gloves.jpg");
      watermarkLayer.setX(MARGIN);
      watermarkLayer.setY(MARGIN);
      layer.merge(watermarkLayer);
     } catch (RepositoryException e) {
      // TODO Auto-generated catch block
      e.printStackTrace();
     } catch (IOException e) {
      // TODO Auto-generated catch block
      e.printStackTrace(); }
     layer.crop(new Rectangle(510, 600));
     return layer.getImage(); }
    // ---------------< private >-----------------------------------------------
    /**
     * This method cuts lines if the text file is too long..
     * * @param text
     * * text to check
     * * @param height
     * * text box height (px)
     * * @param fontheight
     * * font height (px)
     * * @return the text which will fit into the box
     */
    private String getDisplayText(String text, int height, int fontheight) {
     String trimmedText = text.trim();
     int numOfLines = height / fontheight;
     String lines[] = trimmedText.split("\n");
     if (lines.length <= numOfLines) {
      return trimmedText;
     } else {
      String cuttetText = "";
      for (int i = 0; i < numOfLines; i++) {
       cuttetText += lines[i] + "\n";
      }
      return cuttetText;
     }
    }
    /**
     * * This method counts the number of words in a string
     * * @param text the String whose words would like to be counted
     * * @return the number of words in the string
     * */
    private long wordCount(String text) {
     // We need to keep track of the last character, if we have two whitespaces in a row we don't want to double count.
     // The starting of the document is always a whitespace.
     boolean prevWhiteSpace = true;
     boolean currentWhiteSpace = true;
     char c; long numwords = 0;
     int j = text.length();
     int i = 0;
     while (i < j) {
      c = text.charAt(i++);
      if (c == 0) { break; }
      currentWhiteSpace = Character.isWhitespace(c);
      if (currentWhiteSpace && !prevWhiteSpace) { numwords++; }
      prevWhiteSpace = currentWhiteSpace;
     }
     // If we do not end with a whitespace then we need to add one extra word.
     if (!currentWhiteSpace) { numwords++; }
     return numwords;
    }
   }
   ```

1. 컴파일 [!DNL Java] 클래스를 만들고 번들을 만듭니다.

   1. 마우스 오른쪽 단추 클릭 `myBundle` 프로젝트, 선택 **[!UICONTROL 다음으로 실행]**, 그런 다음 **[!UICONTROL Maven 설치]**.
   1. 번들 `myBundle-0.0.1-SNAPSHOT.jar` (컴파일된 클래스 포함)은 `myBundle/target`.

1. CRX 탐색기에서 `/apps/myApp`. 이름 = `install`, 유형 = `nt:folder`.
1. 번들 복사 `myBundle-0.0.1-SNAPSHOT.jar` 아래에 저장합니다. `/apps/myApp/install` (예: WebDAV에서) 이제 새 텍스트 처리기가 [!DNL Experience Manager].
1. 브라우저에서 [!UICONTROL Apache Felix 웹 관리 콘솔]. 다음 항목 선택 [!UICONTROL 구성 요소] 기본 텍스트 처리기를 탭하고 비활성화합니다. `com.day.cq.dam.core.impl.handler.TextHandler`.

## 명령줄 기반 미디어 핸들러 {#command-line-based-media-handler}

[!DNL Experience Manager] 워크플로우 내에서 명령줄 도구를 실행하여 자산을 변환할 수 있습니다(예: [!DNL ImageMagick]) 새 렌디션을 에셋에 추가합니다. 를 호스팅하는 디스크에는 명령줄 도구만 설치하면 됩니다. [!DNL Experience Manager] 워크플로우에 프로세스 단계를 추가하고 구성하는 서버 및 입니다. 호출된 프로세스 `CommandLineProcess`를 사용하면 특정 MIME 유형에 따라 필터링하고 새 렌디션을 기반으로 여러 썸네일을 만들 수도 있습니다.

다음 변환은 내에서 자동으로 실행되고 저장될 수 있습니다. [!DNL Assets]:

* 를 사용하는 EPS 및 AI 변환 [ImageMagick](https://www.imagemagick.org/script/index.php) 및 [고스트스크립트](https://www.ghostscript.com/).
* 를 사용한 FLV 비디오 코드 변환 [FFmpeg](https://ffmpeg.org/).
* 를 사용한 MP3 인코딩 [절름발이](https://lame.sourceforge.io/).
* 를 사용한 오디오 처리 [SOX](https://sox.sourceforge.io/).

>[!NOTE]
>
>Windows가 아닌 시스템에서 FFmpeg 도구는 파일 이름에 작은 따옴표(&#39;)가 있는 비디오 에셋에 대한 렌디션을 생성하는 동안 오류를 반환합니다. 비디오 파일의 이름에 작은 따옴표가 포함되어 있는 경우 업로드하기 전에 제거합니다. [!DNL Experience Manager].

다음 `CommandLineProcess` 프로세스는 나열된 순서대로 다음 작업을 수행합니다.

* 지정된 경우 특정 MIME 유형에 따라 파일을 필터링합니다.
* 를 호스팅하는 디스크에 임시 디렉터리를 만듭니다. [!DNL Experience Manager] 서버입니다.
* 원본 파일을 임시 디렉터리로 스트리밍합니다.
* 단계의 인수로 정의된 명령을 실행합니다. 실행 중인 사용자의 권한으로 임시 디렉토리 내에서 명령이 실행되고 있습니다. [!DNL Experience Manager].
* 결과를 의 렌디션 폴더로 다시 스트리밍합니다. [!DNL Experience Manager] 서버입니다.
* 임시 디렉토리를 삭제합니다.
* 지정된 경우 이러한 렌디션을 기반으로 축소판을 만듭니다. 썸네일 수와 차원은 단계의 인수로 정의됩니다.

### 를 사용하는 예 [!DNL ImageMagick] {#an-example-using-imagemagick}

다음 예에서는 miMIME e-type GIF 또는 TIFF이 있는 자산이에 추가될 때마다 명령줄 프로세스 단계를 설정하는 방법을 보여 줍니다 `/content/dam` 다음에 있음 [!DNL Experience Manager] 서버에서는 3개의 추가 썸네일(140x100, 48x48, 10x250)과 함께 원본의 대칭 이미지가 생성됩니다.

이렇게 하려면 다음을 사용합니다. [!DNL ImageMagick]. [!DNL ImageMagick] 는 비트맵 이미지를 작성, 편집 및 작성하는 데 사용되는 무료 명령줄 소프트웨어입니다.

설치 [!DNL ImageMagick] 을(를) 호스팅하는 디스크에서 [!DNL Experience Manager] 서버:

1. 설치 [!DNL ImageMagick]: 를 참조하십시오 [ImageMagick 설명서](https://www.imagemagick.org/script/download.php).
1. 명령줄에서 변환(convert)을 실행할 수 있도록 도구를 설정합니다.
1. 도구가 제대로 설치되었는지 확인하려면 다음 명령을 실행합니다 `convert -h` 명령줄에 있습니다.

   변환 도구의 가능한 모든 옵션이 있는 도움말 화면이 표시됩니다.

   >[!NOTE]
   >
   >일부 버전의 Windows에서는 convert 명령이 의 일부인 기본 convert 유틸리티와 충돌하기 때문에 실행되지 않을 수 있습니다 [!DNL Windows] 설치. 이 경우 의 전체 경로를 언급하십시오. [!DNL ImageMagick] 이미지 파일을 썸네일로 변환하는 데 사용되는 소프트웨어입니다. (예: `"C:\Program Files\ImageMagick-6.8.9-Q16\convert.exe" -define jpeg:size=319x319 ${filename} -thumbnail 319x319 cq5dam.thumbnail.319.319.png`)

1. 도구가 제대로 실행되는지 확인하려면 작업 디렉터리에 JPG 이미지를 추가하고 convert 명령을 실행합니다 `<image-name>.jpg -flip <image-name>-flipped.jpg` 명령줄에 있습니다. 대칭 이동된 이미지가 디렉토리에 추가됩니다. Then, add the command line process step to the **[!UICONTROL DAM Update Asset]** workflow.
1. 로 이동 **[!UICONTROL 워크플로]** 콘솔.
1. 다음에서 **[!UICONTROL 모델]** 탭, 편집 **[!UICONTROL DAM 자산 업데이트]** 모델.
1. 변경 [!UICONTROL 인수] / **[!UICONTROL 웹 사용 표현물]** 단계: `mime:image/gif,mime:image/tiff,tn:140:100,tn:48:48,tn:10:250,cmd:convert ${directory}/${filename} -flip ${directory}/${basename}.flipped.jpg`.
1. 워크플로우를 저장합니다.

수정된 워크플로우를 테스트하려면 에셋을에 추가합니다 `/content/dam`.

1. 파일 시스템에서 원하는 TIFF 이미지를 가져옵니다. 이름 바꾸기 `myImage.tiff` 및 복사 위치: `/content/dam`예를 들어 WebDAV를 사용합니다.
1. 로 이동 **[!UICONTROL CQ5 DAM]** 콘솔(예: ) `https://localhost:4502/libs/wcm/core/content/damadmin.html`.
1. 에셋 열기 **[!UICONTROL myImage.tiff]** 그리고 뒤집힌 이미지와 세 개의 썸네일이 만들어졌는지 확인합니다.

#### CommandLineProcess 프로세스 단계 구성 {#configuring-the-commandlineprocess-process-step}

This section describes how to set the [!UICONTROL Process Arguments] of the [!UICONTROL CommandLineProcess].

의 값 구분 [!UICONTROL 프로세스 인수] 쉼표를 사용하고 공백으로 시작하지 마십시오.

| Argument-Format | 설명 |
|---|---|
| mime:&lt;mime-type> | 선택적 인수입니다. 자산이 인수 중 하나와 동일한 MIME 유형을 갖는 경우 프로세스가 적용됩니다. <br>몇 가지 MIME 유형을 정의할 수 있습니다. |
| tn:&lt;width>:&lt;height> | 선택적 인수입니다. 이 프로세스는 인수에 정의된 차원으로 썸네일을 만듭니다. <br>여러 썸네일을 정의할 수 있습니다. |
| cmd: &lt;command> | 실행되는 명령을 정의합니다. 구문은 명령줄 도구에 따라 다릅니다. 명령은 하나만 정의할 수 있습니다. <br>다음 변수를 사용하여 명령을 만들 수 있습니다.<br>`${filename}`: 입력 파일 이름(예: original.jpg) <br> `${file}`: 입력 파일의 전체 경로 이름(예: ) `/tmp/cqdam0816.tmp/original.jpg` <br> `${directory}`: 입력 파일의 디렉토리(예: ) `/tmp/cqdam0816.tmp` <br>`${basename}`: 확장명이 없는 입력 파일의 이름(예: 원본) <br>`${extension}`: 입력 파일의 확장자(예: JPG) |

예를 들어 다음과 같습니다. [!DNL ImageMagick] 을(를) 호스팅하는 디스크에 설치됩니다. [!DNL Experience Manager] 서버 및 을 사용하여 프로세스 단계를 만드는 경우 [!UICONTROL 명령줄 프로세스] as 구현 및 다음 값 [!UICONTROL 프로세스 인수]:

`mime:image/gif,mime:image/tiff,tn:140:100,tn:48:48,tn:10:250,cmd:convert ${directory}/${filename} -flip ${directory}/${basename}.flipped.jpg`

그런 다음 워크플로우가 실행되면 단계가 인 자산에만 적용됩니다. `image/gif` 또는 `mime:image/tiff` 다음으로: `mime-types`, 원본 이미지의 대칭 이동을 만들고, JPG으로 변환하고, 140x100, 48x48 및 10x250 크기의 세 개의 썸네일을 만듭니다.

다음 사용 [!UICONTROL 프로세스 인수] 을 사용하여 세 개의 표준 축소판을 만들려면 [!DNL ImageMagick]:

`mime:image/tiff,mime:image/png,mime:image/bmp,mime:image/gif,mime:image/jpeg,cmd:convert ${filename} -define jpeg:size=319x319 -thumbnail "319x319>" -background transparent -gravity center -extent 319x319 -write png:cq5dam.thumbnail.319.319.png -thumbnail "140x100>" -background transparent -gravity center -extent 140x100 -write cq5dam.thumbnail.140.100.png -thumbnail "48x48>" -background transparent -gravity center -extent 48x48 cq5dam.thumbnail.48.48.png`

다음 사용 [!UICONTROL 프로세스 인수] 을 사용하여 웹 사용 렌디션을 만들려면 [!DNL ImageMagick]:

`mime:image/tiff,mime:image/png,mime:image/bmp,mime:image/gif,mime:image/jpeg,cmd:convert ${filename} -define jpeg:size=1280x1280 -thumbnail "1280x1280>" cq5dam.web.1280.1280.jpeg`

>[!NOTE]
>
>다음 [!UICONTROL 명령줄 프로세스] 단계는 에셋(유형의 노드)에만 적용됩니다. `dam:Asset`) 또는 에셋의 하위 항목입니다.

>[!MORELIKETHIS]
>
>* [자산 처리](assets-workflow.md)

