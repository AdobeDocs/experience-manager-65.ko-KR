---
title: 미디어 핸들러 및 워크플로우를 사용하여 자산 처리
description: 미디어 핸들러와 워크플로우를 사용하여 디지털 자산에 대한 작업을 수행하는 방법에 대해 알아봅니다.
contentOwner: AG
role: 비즈니스 전문가
translation-type: tm+mt
source-git-commit: ebe7042b931869c3b4b7204e3ce7afa52d56f0ef
workflow-type: tm+mt
source-wordcount: '2163'
ht-degree: 2%

---


# 미디어 핸들러 및 워크플로우를 사용하여 자산 처리 {#processing-assets-using-media-handlers-and-workflows}

[!DNL Adobe Experience Manager Assets] 자산 처리를 위한 기본 워크플로우 및 미디어 핸들러 세트가 함께 제공됩니다. 워크플로우는 에셋에서 실행할 작업을 정의한 다음 축소판 생성 또는 메타데이터 추출 등의 미디어 핸들러에 특정 작업을 위임합니다.

특정 MIME 유형의 자산이 업로드될 때 워크플로우를 자동으로 실행하도록 구성할 수 있습니다. 처리 단계는 일련의 [!DNL Assets] 미디어 핸들러에 따라 정의됩니다. [!DNL Experience Manager] 는  [내장된 일부 핸들러를 제공하며,](#default-media-handlers)  추가적인 핸들러는 사용자 정의  [개발 또는 ](#creating-a-new-media-handler) 명령줄 도구로 프로세스를 위임하여  [정의할 수 ](#command-line-based-media-handler)있습니다.

미디어 핸들러는 자산에 대한 특정 작업을 수행하는 [!DNL Assets]의 서비스입니다. 예를 들어 MP3 오디오 파일이 [!DNL Experience Manager]에 업로드되면 워크플로우는 메타데이터를 추출하고 축소판을 생성하는 MP3 핸들러를 트리거합니다. 미디어 핸들러는 일반적으로 워크플로우와 함께 사용됩니다. 대부분의 일반 MIME 유형은 [!DNL Experience Manager] 내에서 지원됩니다. 워크플로우를 확장/생성하고 미디어 핸들러를 확장/만들거나 미디어 핸들러를 비활성화/활성화하여 자산에 대해 특정 작업을 수행할 수 있습니다.

>[!NOTE]
>
>[!DNL Assets]에서 지원하는 모든 형식 및 각 형식에 지원되는 기능에 대한 설명은 [자산 지원 형식](assets-formats.md) 페이지를 참조하십시오.

## 기본 미디어 핸들러 {#default-media-handlers}

다음 미디어 핸들러는 [!DNL Assets] 내에서 사용할 수 있으며 가장 일반적인 MIME 형식을 처리합니다.

<!-- TBD: Java versions shouldn't be set to 1.5. Must be updated.
-->

| 처리기 이름 | 서비스 이름(시스템 콘솔) | 지원되는 MIME 유형 |
|--------------|--------------------------------------|----------------------|
| [!UICONTROL TextHandler] | com.day.cq.dam.core.impl.handler.TextHandler | text/plain |
| [!UICONTROL PdfHandler] | com.day.cq.dam.handler.standard.pdf.PdfHandler | <ul><li>application/pdf</li><li>응용 프로그램/illustrator</li></ul> |
| [!UICONTROL JpegHandler] | com.day.cq.dam.core.impl.handler.JpegHandler | image/jpeg |
| [!UICONTROL Mp3Handler] | com.day.cq.dam.handler.standard.mp3.Mp3Handler | audio/mpeg<br><b>중요</b> - MP3 파일을 업로드할 때 타사 라이브러리](http://www.zxdr.it/programmi/SistEvolBDD/LibJava/doc/de/vdheide/mp3/MP3File.html)를 사용하여 [처리됩니다. 라이브러리는 MP3에 VBR(가변 비트 전송률)이 있는 경우 정확한 개수의 근사 길이를 계산합니다. |
| [!UICONTROL ZipHandler] | com.day.cq.dam.handler.standard.zip.ZipHandler | <ul><li>application/java-archive </li><li> application/zip</li></ul> |
| [!UICONTROL PictHandler] | com.day.cq.dam.handler.standard.pict.PictHandler | 이미지/사진 |
| [!UICONTROL StandardImageHandler] | com.day.cq.dam.core.impl.handler.StandardImageHandler | <ul><li>image/gif </li><li> image/png </li> <li>application/photoshop </li> <li>이미지/jpeg </li><li> image/tiff </li> <li>image/x-ms-bmp </li><li> image/bmp</li></ul> |
| [!UICONTROL MSOfficeHandler] | com.day.cq.dam.handler.standard.msoffice.MSOfficeHandler | application/msword |
| [!UICONTROL MSPowerPointHandler] | com.day.cq.dam.handler.standard.msoffice.MSPowerPointHandler | application/vnd.ms-powerpoint |
| [!UICONTROL OpenOfficeHandler] | com.day.cq.dam.handler.standard.ooxml.OpenOfficeHandler | <ul><li>application/vnd.openxmlformats-officedocument.wordprocessingml.document</li><li> application/vnd.openxmlformats-officedocument.spreadsheetml.sheet</li><li> application/vnd.openxmlformats-officedocument.presentationml.presentation</li></ul> |
| [!UICONTROL EPubHandler] | com.day.cq.dam.handler.standard.epub.EPubHandler | application/epub+zip |
| [!UICONTROL GenericAssetHandler] | com.day.cq.dam.core.impl.handler.GenericAssetHandler | 에셋에서 데이터를 추출하는 다른 핸들러가 없는 경우에 대비책 |

모든 핸들러는 다음 작업을 수행합니다.

* 자산에서 사용 가능한 모든 메타데이터를 추출하는 중입니다.
* 에셋의 축소판 이미지 만들기.

활성 미디어 핸들러를 보려면:

1. 브라우저에서 `http://localhost:4502/system/console/components`으로 이동합니다.
1. 클릭 `com.day.cq.dam.core.impl.store.AssetStoreImpl`.
1. 모든 활성 미디어 핸들러가 있는 목록이 표시됩니다. 예:

![chlimage_1-437](assets/chlimage_1-437.png)

## 워크플로우의 미디어 핸들러를 사용하여 자산 {#using-media-handlers-in-workflows-to-perform-tasks-on-assets} 작업 수행

미디어 핸들러는 일반적으로 워크플로우와 함께 사용되는 서비스입니다.

[!DNL Experience Manager] 자산 처리를 위한 몇 가지 기본 워크플로우가 있습니다. 이 항목을 보려면 워크플로우 콘솔을 열고 **[!UICONTROL 모델]** 탭을 클릭합니다.[!DNL Assets]로 시작하는 워크플로우 제목은 자산별 제목입니다.

기존 워크플로우를 확장할 수 있으며 특정 요구 사항에 따라 자산을 처리하기 위해 새로운 워크플로우를 만들 수 있습니다.

다음 예제에서는 PDF 문서를 제외한 모든 자산에 대해 하위 자산이 생성되도록 **[!UICONTROL AEM Assets 동기화]** 작업 과정을 향상시키는 방법을 보여 줍니다.

### 미디어 핸들러 {#disabling-enabling-a-media-handler} 비활성화 또는 활성화

미디어 핸들러는 Apache Felix 웹 관리 콘솔을 통해 비활성화하거나 활성화할 수 있습니다. 미디어 핸들러가 비활성화되면 해당 작업이 자산에 대해 수행되지 않습니다.

미디어 핸들러를 활성화/비활성화하려면:

1. 브라우저에서 `https://<host>:<port>/system/console/components`으로 이동합니다.
1. 미디어 핸들러의 이름 옆에 있는 **[!UICONTROL 비활성화]**&#x200B;를 클릭합니다. 예: `com.day.cq.dam.handler.standard.mp3.Mp3Handler`.
1. 페이지를 새로 고칩니다.미디어 핸들러 옆에 비활성화되었음을 나타내는 아이콘이 표시됩니다.
1. 미디어 핸들러를 활성화하려면 미디어 핸들러의 이름 옆에 있는 **[!UICONTROL 활성화]**&#x200B;를 클릭합니다.

### 새 미디어 핸들러 {#creating-a-new-media-handler} 만들기

새 미디어 유형을 지원하거나 자산에서 특정 작업을 실행하려면 새 미디어 핸들러를 만들어야 합니다. 이 섹션에서는 진행 방법에 대해 설명합니다.

#### 중요 클래스 및 인터페이스 {#important-classes-and-interfaces}

구현을 시작하는 가장 좋은 방법은 대부분의 작업을 처리하고 적절한 기본 비헤이비어를 제공하는 제공된 추상 구현에서 상속하는 것입니다.`com.day.cq.dam.core.AbstractAssetHandler` 클래스입니다.

이 클래스는 추상 서비스 설명자를 이미 제공합니다. 따라서 이 클래스에서 상속하고 maven-sling-plugin을 사용하는 경우 inherit 플래그를 `true`으로 설정해야 합니다.

다음 메서드를 구현합니다.

* `extractMetadata()`:사용 가능한 모든 메타데이터를 추출합니다.
* `getThumbnailImage()`:전달된 자산에서 축소판 이미지를 만듭니다.
* `getMimeTypes()`:자산 MIME 형식을 반환합니다.

다음은 예제 템플릿입니다.

```Java
package my.own.stuff; /** * @scr.component inherit="true" * @scr.service */ public class MyMediaHandler extends com.day.cq.dam.core.AbstractAssetHandler { // implement the relevant parts }
```

인터페이스와 클래스에는 다음이 포함됩니다.

* `com.day.cq.dam.api.handler.AssetHandler` 인터페이스:이 인터페이스는 특정 MIME 유형에 대한 지원을 추가하는 서비스에 대해 설명합니다. 이 인터페이스를 구현하려면 새 MIME 형식을 추가해야 합니다. 인터페이스에는 축소판을 만들고 메타데이터를 추출하기 위해 특정 문서를 가져오거나 내보내는 방법이 포함되어 있습니다.
* `com.day.cq.dam.core.AbstractAssetHandler` class:이 클래스는 다른 모든 에셋 처리기 구현의 기초로 사용되고 있는 일반적인 기능을 제공합니다.
* `com.day.cq.dam.core.AbstractSubAssetHandler` 클래스:
   * 이 클래스는 다른 모든 에셋 처리기 구현의 기본 역할을 하며 일반적인 사용 기능뿐만 아니라 하위 에셋 추출에 일반적인 사용 기능을 제공합니다.
   * 구현을 시작하는 가장 좋은 방법은 대부분의 작업을 처리하고 적절한 기본 비헤이비어를 제공하는 제공된 추상 구현에서 상속하는 것입니다.com.day.cq.dam.core.AbstractAssetHandler 클래스.
   * 이 클래스는 추상 서비스 설명자를 이미 제공합니다. 따라서 이 클래스에서 상속하고 maven-sling-plugin을 사용하는 경우 inherit 플래그를 true로 설정해야 합니다.

다음 메서드를 구현해야 합니다.

* `extractMetadata()`:이 메서드는 사용 가능한 모든 메타데이터를 추출합니다.
* `getThumbnailImage()`:이 방법을 사용하면 전달된 자산에서 축소판 이미지가 만들어집니다.
* `getMimeTypes()`:이 메서드는 자산 MIME 형식을 반환합니다.

다음은 예제 템플릿입니다.

package my.own.stuff;/&amp;ast;&amp;ast;&amp;ast;@scr.component inherit=&quot;true&quot; &amp;ast;@scr.service &amp;ast;/ 공용 클래스 MyMediaHandler가 com.day.cq.dam.core.AbstractAssetHandler { // 관련 부분 구현 }

인터페이스와 클래스에는 다음이 포함됩니다.

* `com.day.cq.dam.api.handler.AssetHandler` 인터페이스:이 인터페이스는 특정 MIME 유형에 대한 지원을 추가하는 서비스에 대해 설명합니다. 이 인터페이스를 구현하려면 새 MIME 형식을 추가해야 합니다. 인터페이스에는 축소판을 만들고 메타데이터를 추출하기 위해 특정 문서를 가져오거나 내보내는 방법이 포함되어 있습니다.
* `com.day.cq.dam.core.AbstractAssetHandler` class:이 클래스는 다른 모든 에셋 처리기 구현의 기초로 사용되고 있는 일반적인 기능을 제공합니다.
* `com.day.cq.dam.core.AbstractSubAssetHandler` class:이 클래스는 다른 모든 에셋 처리기 구현의 기본 역할을 하며 일반적인 사용 기능뿐만 아니라 하위 에셋 추출에 사용되는 일반적인 기능을 제공합니다.

#### 예:특정 텍스트 핸들러 {#example-create-a-specific-text-handler} 만들기

이 섹션에서는 워터마크가 있는 축소판을 생성하는 특정 텍스트 핸들러를 만듭니다.

다음과 같이 진행합니다.

[!DNL Maven] 플러그인으로 Eclipse를 설치 및 설정하고 [!DNL Maven] 프로젝트에 필요한 종속성을 설정하려면 [개발 도구](../sites-developing/dev-tools.md)를 참조하십시오.

다음 절차를 수행한 후 TXT 파일을 [!DNL Experience Manager]에 업로드하면 파일의 메타데이터가 추출되고 워터마크가 있는 2개의 축소판이 생성됩니다.

1. Eclipse에서 `myBundle` [!DNL Maven] 프로젝트를 만듭니다.

   1. 메뉴 모음에서 **[!UICONTROL 파일]** > **[!UICONTROL 새로 만들기]** > **[!UICONTROL 기타]**&#x200B;를 클릭합니다.
   1. 대화 상자에서 [!DNL Maven] 폴더를 확장하고 [!DNL Maven] 프로젝트를 선택하고 **[!UICONTROL 다음]**&#x200B;을 클릭합니다.
   1. 간단한 프로젝트 만들기 상자와 기본 작업 공간 위치 사용 상자를 선택한 다음 **[!UICONTROL 다음]**&#x200B;을 클릭합니다.
   1. [!DNL Maven] 프로젝트를 정의합니다.

      * 그룹 ID:`com.day.cq5.myhandler`.
      * 아티팩트 ID:myBundle을 참조하십시오.
      * 이름:내 [!DNL Experience Manager] 번들.
      * 설명:이것은 내 [!DNL Experience Manager] 번들입니다.
   1. **[!UICONTROL 완료]**&#x200B;를 클릭합니다.


1. [!DNL Java] 컴파일러를 버전 1.5로 설정합니다.

   1. `myBundle` 프로젝트를 마우스 오른쪽 단추로 클릭하고 [!UICONTROL 속성]을 선택합니다.
   1. [!UICONTROL Java Compiler]를 선택하고 다음 속성을 1.5로 설정합니다.

      * 컴파일러 준수 수준
      * 생성된 .class 파일 호환성
      * 소스 호환성
   1. **[!UICONTROL 확인]**&#x200B;을 클릭합니다. 대화 상자 창에서 **[!UICONTROL 예]**&#x200B;를 클릭합니다.


1. `pom.xml` 파일의 코드를 다음 코드로 바꿉니다.

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

1. `myBundle/src/main/java` 아래에 [!DNL Java] 클래스가 들어 있는 패키지 `com.day.cq5.myhandler`을 만듭니다.

   1. myBundle 아래에서 `src/main/java`을 마우스 오른쪽 단추로 클릭하고 새로 만들기, 패키지 순으로 선택합니다.
   1. 이름을 `com.day.cq5.myhandler`으로 지정하고 [마침]을 클릭합니다.

1. [!DNL Java] 클래스 `MyHandler` 만들기:

   1. [!DNL Eclipse]의 `myBundle/src/main/java`에서 `com.day.cq5.myhandler` 패키지를 마우스 오른쪽 단추로 클릭합니다. [!UICONTROL 새로 만들기]를 선택하고 [!UICONTROL 클래스]를 선택합니다.
   1. 대화 상자 창에서 [!DNL Java] 클래스 `MyHandler`의 이름을 지정하고 [!UICONTROL 완료]를 클릭합니다. [!DNL Eclipse] 파일을 만들고 엽니다 `MyHandler.java`.
   1. `MyHandler.java`에서 기존 코드를 다음으로 바꾼 다음 변경 내용을 저장합니다.

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
      watermarkLayer = ImageHelper.createLayer(session, "/content/dam/geometrixx/icons/certificate.png");
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

1. [!DNL Java] 클래스를 컴파일하고 번들을 만듭니다.

   1. `myBundle` 프로젝트를 마우스 오른쪽 단추로 클릭하고 **[!UICONTROL Run As]**&#x200B;을 선택한 다음 **[!UICONTROL Maven Install]**&#x200B;을 선택합니다.
   1. `myBundle-0.0.1-SNAPSHOT.jar` 번들(컴파일된 클래스 포함)은 `myBundle/target` 아래에 생성됩니다.

1. CRX 탐색기에서 `/apps/myApp` 아래에 새 노드를 만듭니다. 이름 = `install`, 유형 = `nt:folder`.
1. 번들 `myBundle-0.0.1-SNAPSHOT.jar`을(를) 복사하고 `/apps/myApp/install` 아래에 저장합니다(예: WebDAV). 이제 새 텍스트 핸들러가 [!DNL Experience Manager]에서 활성화됩니다.
1. 브라우저에서 [!UICONTROL Apache Felix 웹 관리 콘솔]을 엽니다. [!UICONTROL 구성 요소] 탭을 선택하고 기본 텍스트 핸들러 `com.day.cq.dam.core.impl.handler.TextHandler`를 비활성화합니다.

## 명령줄 기반 미디어 핸들러 {#command-line-based-media-handler}

[!DNL Experience Manager] 워크플로우 내에서 명령줄 도구를 실행하여 자산(예:)을  [!DNL ImageMagick]변환하고 새 변환을 자산에 추가할 수 있습니다. [!DNL Experience Manager] 서버를 호스팅하는 디스크에 명령줄 도구를 설치하고 워크플로우에 프로세스 단계를 추가하고 구성해야 합니다. 호출된 프로세스(`CommandLineProcess`)는 특정 MIME 유형에 따라 필터링하고 새 변환에 따라 여러 축소판을 만들 수도 있습니다.

다음 변환은 [!DNL Assets] 내에서 자동으로 실행 및 저장할 수 있습니다.

* [ImageMagick](https://www.imagemagick.org/script/index.php) 및 [Ghostscript](https://www.ghostscript.com/)를 사용하는 EPS 및 AI 변환.
* [FFmpeg](https://ffmpeg.org/)을 사용하여 FLV 비디오 트랜스코딩.
* [LAME](https://lame.sourceforge.io/)을(를) 사용한 MP3 인코딩.
* [SOX](https://sox.sourceforge.net/)을(를) 사용한 오디오 처리.

>[!NOTE]
>
>Windows가 아닌 시스템에서 FFmpeg 도구는 파일 이름에 작은 따옴표(&#39;)가 있는 비디오 자산에 대한 변환을 생성하는 동안 오류를 반환합니다. 비디오 파일 이름에 단일 인용 부호가 포함되어 있으면 [!DNL Experience Manager]에 업로드하기 전에 해당 부호를 제거합니다.

`CommandLineProcess` 프로세스는 나열된 순서대로 다음 작업을 수행합니다.

* 지정된 경우 특정 MIME 유형에 따라 파일을 필터링합니다.
* [!DNL Experience Manager] 서버를 호스팅하는 디스크에 임시 디렉토리를 만듭니다.
* 원본 파일을 임시 디렉토리로 스트리밍합니다.
* 단계의 인수로 정의된 명령을 실행합니다. [!DNL Experience Manager]을(를) 실행하는 사용자의 권한이 있는 임시 디렉터리 내에서 명령을 실행하고 있습니다.
* 결과를 다시 [!DNL Experience Manager] 서버의 변환 폴더로 스트리밍합니다.
* 임시 디렉토리를 삭제합니다.
* 지정된 경우 이러한 변환에 따라 축소판을 만듭니다. 축소판의 수와 크기는 단계의 인수로 정의됩니다.

### [!DNL ImageMagick] {#an-example-using-imagemagick} 사용 예

다음 예제에서는 miMIME e-type GIF 또는 TIFF가 있는 에셋이 [!DNL Experience Manager] 서버에서 `/content/dam`에 추가될 때마다 역진행 상태의 원본 이미지가 3개의 추가 축소판(140x100, 48x48 및 10x25)과 함께 작성되도록 명령줄 프로세스 단계를 설정하는 방법을 보여 줍니다. 0).

이렇게 하려면 [!DNL ImageMagick]을(를) 사용합니다. [!DNL ImageMagick] 은 비트맵 이미지를 만들고 편집하고 구성하는 데 사용되는 무료 명령줄 소프트웨어입니다.

[!DNL Experience Manager] 서버를 호스팅하는 디스크에 [!DNL ImageMagick]을(를) 설치합니다.

1. [!DNL ImageMagick] 설치:[ImageMagick 설명서](https://www.imagemagick.org/script/download.php)를 참조하십시오.
1. 명령줄에서 변환을 실행할 수 있도록 도구를 설정합니다.
1. 도구가 제대로 설치되었는지 확인하려면 명령줄에서 `convert -h` 명령을 실행하십시오.

   변환 도구의 가능한 모든 옵션이 포함된 도움말 화면이 표시됩니다.

   >[!NOTE]
   >
   >일부 버전의 Windows에서는 변환 명령이 [!DNL Windows] 설치의 일부인 기본 변환 유틸리티와 충돌하기 때문에 실행되지 않을 수도 있습니다. 이 경우 이미지 파일을 축소판으로 변환하는 데 사용되는 [!DNL ImageMagick] 소프트웨어의 전체 경로를 언급합니다. 예, `"C:\Program Files\ImageMagick-6.8.9-Q16\convert.exe" -define jpeg:size=319x319 ${filename} -thumbnail 319x319 cq5dam.thumbnail.319.319.png`.

1. 도구가 제대로 실행되는지 확인하려면 작업 디렉토리에 JPG 이미지를 추가하고 명령줄에 `<image-name>.jpg -flip <image-name>-flipped.jpg` 변환 명령을 실행합니다. 역진행 이미지가 디렉토리에 추가됩니다. 그런 다음 명령줄 프로세스 단계를 **[!UICONTROL DAM 자산 업데이트]** 워크플로우에 추가합니다.
1. **[!UICONTROL 워크플로]** 콘솔로 이동합니다.
1. **[!UICONTROL 모델]** 탭에서 **[!UICONTROL DAM 자산 업데이트]** 모델을 편집합니다.
1. **[!UICONTROL 웹이 활성화된 변환]** 단계의 [!UICONTROL Arguments]을 다음과 같이 변경합니다.`mime:image/gif,mime:image/tiff,tn:140:100,tn:48:48,tn:10:250,cmd:convert ${directory}/${filename} -flip ${directory}/${basename}.flipped.jpg`.
1. 워크플로우를 저장합니다.

수정된 작업 흐름을 테스트하려면 `/content/dam`에 자산을 추가합니다.

1. 파일 시스템에서 원하는 TIFF 이미지를 가져옵니다. WebDAV를 사용하여 이름을 `myImage.tiff`으로 변경하고 `/content/dam`에 복사합니다.
1. **[!UICONTROL CQ5 DAM]** 콘솔로 이동합니다(예: `http://localhost:4502/libs/wcm/core/content/damadmin.html`).
1. **[!UICONTROL myImage.tiff]** 에셋을 열고 역진행 이미지와 3개의 축소판이 만들어졌는지 확인합니다.

#### CommandLineProcess 프로세스 단계 {#configuring-the-commandlineprocess-process-step} 구성

이 섹션에서는 [!UICONTROL CommandLineProcess]의 [!UICONTROL 프로세스 인수]를 설정하는 방법을 설명합니다.

[!UICONTROL 프로세스 인수]의 값을 쉼표를 사용하여 구분하고 공백으로 시작하지 마십시오.

| 인수 형식 | 설명 |
|---|---|
| mime:&lt;mime-type> | 선택적 인수입니다. 자산이 인수 중 하나와 동일한 MIME 형식을 갖는 경우 프로세스가 적용됩니다. <br>여러 MIME 형식을 정의할 수 있습니다. |
| tn:&lt;너비>:&lt;높이> | 선택적 인수입니다. 인수에 정의된 치수로 축소판을 만듭니다. <br>여러 축소판을 정의할 수 있습니다. |
| cmd:&lt;command> | 실행되는 명령을 정의합니다. 구문은 명령줄 도구에 따라 다릅니다. 하나의 명령만 정의할 수 있습니다. <br>다음 변수를 사용하여 명령을 만들 수 있습니다<br>`${filename}`.입력 파일의 이름(예: original.jpg)  <br> `${file}`:입력 파일의 전체 경로 이름(예:  `/tmp/cqdam0816.tmp/original.jpg` <br> `${directory}`:입력 파일의 디렉토리입니다(예:  `/tmp/cqdam0816.tmp` <br>`${basename}`:입력 파일의 확장명이 없는 이름(예: 원본  <br>`${extension}`:JPG와 같은 입력 파일의 확장입니다. |

예를 들어 [!DNL ImageMagick]이(가) [!DNL Experience Manager] 서버를 호스팅하는 디스크에 설치되어 있고 [!UICONTROL CommandLineProcess]를 구현으로 사용하여 프로세스 단계를 만드는 경우 다음 값을 [!UICONTROL 프로세스 인수]로 사용합니다.

`mime:image/gif,mime:image/tiff,tn:140:100,tn:48:48,tn:10:250,cmd:convert ${directory}/${filename} -flip ${directory}/${basename}.flipped.jpg`

그런 다음 워크플로우가 실행되면 이 단계는 `image/gif` 또는 `mime:image/tiff` 가 `mime-types`인 에셋에만 적용되며, 전환된 원본 이미지가 만들어지고 해당 이미지를 JPG로 변환하며 크기가 다음 3개의 축소판이 만들어집니다.140x100, 48x48 및 10x250.

[!DNL ImageMagick]를 사용하여 3개의 표준 축소판을 만들려면 다음 [!UICONTROL Process 인수]을 사용합니다.

`mime:image/tiff,mime:image/png,mime:image/bmp,mime:image/gif,mime:image/jpeg,cmd:convert ${filename} -define jpeg:size=319x319 -thumbnail "319x319>" -background transparent -gravity center -extent 319x319 -write png:cq5dam.thumbnail.319.319.png -thumbnail "140x100>" -background transparent -gravity center -extent 140x100 -write cq5dam.thumbnail.140.100.png -thumbnail "48x48>" -background transparent -gravity center -extent 48x48 cq5dam.thumbnail.48.48.png`

다음 [!UICONTROL 프로세스 인수]를 사용하여 [!DNL ImageMagick]를 사용하여 웹이 활성화된 변환을 만드십시오.

`mime:image/tiff,mime:image/png,mime:image/bmp,mime:image/gif,mime:image/jpeg,cmd:convert ${filename} -define jpeg:size=1280x1280 -thumbnail "1280x1280>" cq5dam.web.1280.1280.jpeg`

>[!NOTE]
>
>[!UICONTROL CommandLineProcess] 단계는 자산(`dam:Asset` 유형의 노드) 또는 자산의 하위 항목에만 적용됩니다.

>[!MORELIKETHIS]
>
>* [자산 처리](assets-workflow.md)

