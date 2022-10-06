---
title: 번역할 문자열 추출
seo-title: Extracting Strings for Translating
description: xgettext-maven-plugin을 사용하여 번역할 필요가 있는 소스 코드에서 문자열을 추출합니다
seo-description: Use xgettext-maven-plugin to extract strings from your source code that need translating
uuid: 2c586ecb-8494-4f8f-b31a-1ed73644d611
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components
discoiquuid: 034f70f1-fbd2-4f6b-b07a-5758f0461a5b
exl-id: 4acc5f7f-0bcb-4b5a-8531-52e146cffeae
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 2%

---

# 번역할 문자열 추출{#extracting-strings-for-translating}

xgettext-maven-plugin을 사용하여 번역할 필요가 있는 소스 코드에서 문자열을 추출합니다. Maven 플러그인은 번역을 위해 보내는 XLIFF 파일에 문자열을 추출합니다. 문자열은 다음 위치에서 추출됩니다.

* Java 소스 파일
* Javascript 소스 파일
* SVN 리소스의 XML 표현(JCR 노드)

## 문자열 추출 구성 {#configuring-string-extraction}

xgettext-maven-plugin 도구가 프로젝트에 대한 문자열을 추출하는 방법을 구성합니다.

```xml
/filter { }
/parsers {
   /vaultxml { }
   /javascript { }
   /regexp {
      /files {
         /java { }
         /jsp { }
         /extjstemplate { }
      }
   }
}
/potentials { }
```

| 섹션 | 설명 |
|---|---|
| /filter | 구문 분석된 파일을 식별합니다. |
| /parsers/vaultxml | 저장소 파일의 구문 분석을 구성합니다. 외부 문자열 및 현지화 힌트를 포함하는 JCR 노드를 식별합니다. 무시할 JCR 노드를 식별합니다. |
| /parsers/javascript | 문자열을 외부화하는 Javascript 함수를 식별합니다. 이 섹션을 변경할 필요가 없습니다. |
| /parsers/regexp | Java, JSP 및 ExtJS 템플릿 파일의 구문 분석을 구성합니다. 이 섹션을 변경할 필요가 없습니다. |
| /잠재적 | 국제화할 문자열을 감지하는 공식입니다. |

### 구문 분석할 파일 식별 {#identifying-the-files-to-parse}

i18n.any 파일의 /filter 섹션은 xgettext-maven-plugin 도구가 구문 분석하는 파일을 식별합니다. 각각 구문 분석되고 무시되는 파일을 식별하는 몇 개의 포함 및 제외 규칙을 추가합니다. 모든 파일을 포함한 다음 구문 분석하지 않을 파일을 제외해야 합니다. 일반적으로 UI에 기여하지 않는 파일 유형 또는 UI를 정의하지만 번역되지 않는 파일을 제외합니다. 포함 및 제외 규칙은 다음 형식을 갖습니다.

```
{ /include "pattern" }
{ /exclude "pattern" }
```

규칙의 패턴 부분은 포함 또는 제외할 파일의 이름과 일치시키는 데 사용됩니다. 패턴 접두사는 JCR 노드(저장소에서 해당 표시)와 일치하는지 파일 시스템을 일치시키는지 여부를 나타냅니다.

| 접두어 | 효과 |
|---|---|
| / | JCR 경로를 나타냅니다. 따라서 이 접두사는 jcr_root 디렉토리 아래의 파일과 일치합니다. |
| &amp;ast; | 파일 시스템의 일반 파일을 나타냅니다. |
| 없음 | 접두사가 없거나 폴더나 파일 이름으로 시작하는 패턴은 파일 시스템의 일반 파일을 나타냅니다. |

패턴 내에서 사용하는 경우 / 문자는 하위 디렉토리와 &amp;ast;를 나타냅니다. 문자가 모두 일치합니다. 다음 표에는 몇 가지 예제 규칙이 나와 있습니다.

<table>
 <tbody>
  <tr>
   <th>예제 규칙</th>
   <th>효과</th>
  </tr>
  <tr>
   <td><code>{ /include "*" }</code></td>
   <td>모든 파일을 포함합니다.</td>
  </tr>
  <tr>
   <td><code>{ /exclude "*.pdf" }</code></td>
   <td>모든 PDF 파일을 제외합니다.</td>
  </tr>
  <tr>
   <td><code> { /exclude "*/pom.xml" }</code></td>
   <td>POM 파일을 제외합니다.</td>
  </tr>
  <tr>
   <td><code class="code">{ /exclude "/content/*" }
      { /include "/content/catalogs/geometrixx/templatepages" }
      { /include "/content/catalogs/geometrixx/templatepages/*" }</code></td>
   <td><p>/content 노드 아래의 모든 파일을 제외합니다.</p> <p>/content/catalog/geometrixx/templatepages 노드를 포함합니다.</p> <p>/content/catalog/geometrixx/templatepages의 모든 하위 노드를 포함합니다.</p> </td>
  </tr>
 </tbody>
</table>

### 문자열 추출  {#extracting-the-strings}

POM 없음:

```shell
mvn -N com.adobe.granite.maven:xgettext-maven-plugin:1.2.2:extract  -Dxgettext.verbose=true -Dxgettext.target=out -Dxgettext.rules=i18n.any -Dxgettext.root=.
```

POM을 사용하는 경우: POM에 추가:

```xml
<build>
    <plugins>
        <plugin>
            <groupId>com.adobe.granite.maven</groupId>
            <artifactId>xgettext-maven-plugin</artifactId>
            <version>1.1</version>
            <configuration>
                <rules>i18n.any</rules>
                <root>jcr_root</root>
                <xliff>cq.xliff</xliff>
                <verbose>true</verbose>
            </configuration>
        </plugin>
    </plugins>
</build>
```

명령:

```shell
mvn xgettext:extract
```

### 출력 파일 {#output-files}

* `raw.xliff`: 추출된 문자열
* `warn.log`: 경고(있을 경우) `CQ.I18n.getMessage()` API가 잘못 사용됩니다. 항상 수정 후 다시 실행해야 합니다.

* `parserwarn.log`: 파서 경고(있는 경우)(예: js 파서 문제)
* `potentials.xliff`: &quot;잠재적&quot; 후보로서 추출되지 않았지만 번역이 필요한 사람이 읽을 수 있는 문자열일 수 있습니다(무시해도 되고 많은 양의 긍정 오류가 발생함).
* `strings.xliff`: 병합된 xliff 파일, ALF로 가져오기
* `backrefs.txt`: 지정된 문자열에 대한 소스 코드 위치를 빠르게 조회할 수 있도록 허용합니다
