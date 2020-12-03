---
title: 장치 그룹 필터 만들기
seo-title: 장치 그룹 필터 만들기
description: 장치 그룹 필터를 만들어 장치 기능 요구 사항 집합 정의
seo-description: 장치 그룹 필터를 만들어 장치 기능 요구 사항 집합 정의
uuid: 30c0699d-2388-41b5-a062-f5ea9d6f08bc
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
discoiquuid: 9fef1f91-a222-424a-8e20-3599bedb8b41
docset: aem65
legacypath: /content/docs/en/aem/6-0/develop/mobile/groupfilters
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5
workflow-type: tm+mt
source-wordcount: '816'
ht-degree: 1%

---


# 장치 그룹 필터 만들기{#creating-device-group-filters}

>[!NOTE]
>
>단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: 응답)이 필요한 프로젝트에서는 SPA 편집기를 사용하는 것이 좋습니다. [추가 정보](/help/sites-developing/spa-overview.md).

장치 그룹 필터를 만들어 장치 기능 요구 사항 집합을 정의합니다. 필요한 장치 기능 그룹을 타게팅하는 데 필요한 만큼 필터를 만듭니다.

필터를 디자인하여 필터 조합을 사용하여 기능 그룹을 정의할 수 있습니다. 일반적으로 서로 다른 장치 그룹의 기능이 겹칩니다. 따라서 여러 장치 그룹 정의가 있는 일부 필터를 사용할 수 있습니다.

필터를 만든 후 [그룹 구성에서 사용할 수 있습니다.](/help/sites-developing/mobile.md#creating-a-device-group)

## 필터 Java 클래스 {#the-filter-java-class}

장치 그룹 필터는 [com.day.cq.wcm.mobile.api.device.DeviceGroupFilter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/wcm/mobile/api/device/DeviceGroupFilter.html) 인터페이스를 구현하는 OSGi 구성 요소입니다. 배포 시 구현 클래스는 장치 그룹 구성에 사용할 수 있는 필터 서비스를 제공합니다.

이 문서에서 설명하는 솔루션은 Apache Felix Maven SCR 플러그인을 사용하여 구성 요소 및 서비스의 개발을 촉진합니다. 따라서 예제 Java 클래스는 `@Component`및 `@Service` 주석을 사용합니다. 이 클래스는 다음과 같은 구조를 가집니다.

```java
package com.adobe.example.myapp;

import java.util.Map;

import com.day.cq.wcm.mobile.api.device.DeviceGroup;
import com.day.cq.wcm.mobile.api.device.DeviceGroupFilter;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;

@Component(metatype = false)
@Service
public class myDeviceGroupFilter implements DeviceGroupFilter {

       public String getDescription() {
  return null;
 }

 public String getTitle() {
  return null;
 }

 public boolean matches(DeviceGroup arg0, String arg1, Map arg2) {
  return false;
 }

}
```

다음 메서드에 대한 코드를 제공해야 합니다.

* `getDescription`:필터 설명을 반환합니다. 장치 그룹 구성 대화 상자에 설명이 나타납니다.
* `getTitle`:필터 이름을 반환합니다. 장치 그룹의 필터를 선택하면 이름이 나타납니다.
* `matches`:장치에 필요한 기능이 있는지 확인합니다.

### 필터 이름 및 설명 {#providing-the-filter-name-and-description} 제공

`getTitle` 및 `getDescription` 메서드는 각각 필터 이름과 설명을 반환합니다. 다음 코드는 가장 간단한 구현을 보여 줍니다.

```java
public String getDescription() {
    return "An example device group filter";
}

public String getTitle() {
 return "myFilter";
}
```

이름과 설명 텍스트를 하드 코딩하는 것은 단언어 작성 환경에서 충분합니다. 다중 언어 사용을 위해 문자열을 외부화하거나 소스 코드를 다시 컴파일하지 않고 문자열을 변경할 수 있도록 하는 것이 좋습니다.

### 필터 기준 평가 {#evaluating-against-filter-criteria}

장치 기능이 모든 필터 기준을 충족하는 경우 `matches` 함수는 `true`을 반환합니다. 메서드 인수에 제공된 정보를 평가하여 장치가 그룹에 속하는지 확인합니다. 다음 값이 인수로 제공됩니다.

* DeviceGroup 개체
* 사용자 에이전트 이름
* 장치 기능을 포함하는 Map 개체입니다. 맵 키는 WURFL™ 기능 이름이며 값은 WURFL™ 데이터베이스의 해당 값입니다.

[com.day.cq.wcm.mobile.api.devicspecs.DeviceSpecsConstants](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/wcm/mobile/api/device/DeviceGroupFilter.html) 인터페이스에는 정적 필드에 있는 WURFL™ 기능 이름의 하위 세트가 포함되어 있습니다. 장치 맵에서 값을 검색할 때 이러한 필드 상수를 키로 사용합니다.

예를 들어 다음 코드 예제에서는 장치가 CSS를 지원하는지 여부를 결정합니다.

```xml
boolean cssSupport = true;
cssSupport = NumberUtils.toInt(capabilities.get(DeviceSpecsConstants.DSPEC_XHTML_SUPPORT_LEVEL)) > 1;
```

`org.apache.commons.lang.math` 패키지는 `NumberUtils` 클래스를 제공합니다.

>[!NOTE]
>
>AEM에 배포된 WURFL™ 데이터베이스에 필터 기준으로 사용하는 기능이 포함되어 있는지 확인합니다. ([장치 감지](/help/sites-developing/mobile.md#server-side-device-detection)를 참조하십시오.)

### 화면 크기 {#example-filter-for-screen-size}에 대한 필터 예

다음 DeviceGroupFilter 구현 예제에서는 장치의 물리적 크기가 최소 요구 사항을 충족하는지 여부를 결정합니다. 이 필터는 터치 장치 그룹에 세부기간을 추가하기 위한 것입니다. 응용 프로그램 UI의 단추 크기는 실제 화면 크기와 상관없이 동일해야 합니다. 텍스트와 같은 다른 항목의 크기는 다를 수 있습니다. 이 필터는 UI 요소의 크기를 제어하는 특정 CSS의 동적 선택을 활성화합니다.

이 필터는 크기 기준을 `physical_screen_height` 및 `physical_screen_width` WURFL™ 속성 이름에 적용합니다.

```java
package com.adobe.example.myapp;

import java.util.Map;

import com.day.cq.wcm.mobile.api.device.DeviceGroup;
import com.day.cq.wcm.mobile.api.device.DeviceGroupFilter;

import org.apache.commons.lang.math.NumberUtils;
import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;

@Component(metatype = false)
@Service
@SuppressWarnings("unused")
public class ScreenSizeLarge implements DeviceGroupFilter {
    private int len=400;
    private int wid=200;
    public String getDescription() {

        return "Requires the physical size of the screen to have minimum dimensions " + len + "x" + wid+".";
    }

    public String getTitle() {
        return "Screen Size Large ("+len + "x" + wid+")";
    }

    public boolean matches(DeviceGroup deviceGroup, String userAgent,
            Map<String, String> deviceCapabilities) {

        boolean longEnough=true;
        boolean wideEnough=false;
        int dimension1=NumberUtils.toInt(deviceCapabilities.get("physical_screen_height"));
        int dimension2=NumberUtils.toInt(deviceCapabilities.get("physical_screen_width"));
        if(dimension1>dimension2){
            longEnough=dimension1>=len;
            wideEnough=dimension2>=wid;
        }else{
            longEnough=dimension2>=len;
            wideEnough=dimension1>=wid;
        }

        return longEnough && wideEnough;
    }
}
```

getTitle 메서드가 반환하는 문자열 값이 장치 그룹 속성의 드롭다운 목록에 나타납니다.

![filteraddtogroup](assets/filteraddtogroup.png)

getTitle 및 getDescription 메서드가 반환하는 문자열 값은 장치 그룹 요약 페이지 하단에 포함됩니다.

![필터 설명](assets/filterdescription.png)

### Maven POM 파일 {#the-maven-pom-file}

다음 POM 코드는 Maven을 사용하여 응용 프로그램을 빌드하는 경우에 유용합니다. POM은 몇 가지 필수 플러그인 및 종속성을 참조합니다.

**플러그인:**

* Apache Maven Compiler 플러그인:소스 코드에서 Java 클래스를 컴파일합니다.
* Apache Felix Maven Bundle 플러그인:번들 및 매니페스트 만들기
* Apache Felix Maven SCR Plugin:구성 요소 설명자 파일을 만들고 서비스 구성 요소 매니페스트 헤더를 구성합니다.

**종속성:**

* `cq-wcm-mobile-api-5.5.2.jar`:DeviceGroup 및 DeviceGroupFilter 인터페이스를 제공합니다.

* `org.apache.felix.scr.annotations.jar`:구성 요소 및 서비스 주석을 제공합니다.

DeviceGroup 및 DeviceGroupFilter 인터페이스는 Day Communication 5 WCM Mobile API 번들에 포함되어 있습니다. Felix 주석은 Apache Felix 선언적 서비스 번들에 포함되어 있습니다. 이 JAR 파일을 공용 Adobe 저장소에서 가져올 수 있습니다.

작성 시 5.5.2는 최신 AEM 릴리스에 있는 WCM Mobile API 번들 버전입니다. Adobe 웹 콘솔([https://localhost:4502/system/console/bundles](https://localhost:4502/system/console/bundles))을 사용하여 환경에 배포된 번들 버전인지 확인합니다.

**POM:** (POM은 다른 groupId 및 버전을 사용합니다.)

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
        xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
      <modelVersion>4.0.0</modelVersion>
      <groupId>com.adobe.example.myapp</groupId>
      <artifactId>devicefilter</artifactId>
      <version>0.0.1-SNAPSHOT</version>
      <name>my app device filter</name>
      <url>https://dev.day.com/docs/en/cq/current.html</url>
  <packaging>bundle</packaging>
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <configuration>
                <source>1.5</source>
                <target>1.5</target>
            </configuration>
        </plugin>
        <plugin>
            <groupId>org.apache.felix</groupId>
            <artifactId>maven-scr-plugin</artifactId>
            <executions>
                  <execution>
                    <id>generate-scr-scrdescriptor</id>
                    <goals>
                          <goal>scr</goal>
                    </goals>
                  </execution>
            </executions>
          </plugin>
        <plugin>
            <groupId>org.apache.felix</groupId>
            <artifactId>maven-bundle-plugin</artifactId>
            <version>1.4.3</version>
            <extensions>true</extensions>
            <configuration>
                <instructions>
                    <Export-Package>com.adobe.example.myapp.*;version=${project.version}</Export-Package>
                </instructions>
            </configuration>
        </plugin>
    </plugins>
</build>
<dependencies>
     <dependency>
         <groupId>com.day.cq.wcm</groupId>
         <artifactId>cq-wcm-mobile-api</artifactId>
         <version>5.5.2</version>
         <scope>provided</scope>
     </dependency>
     <dependency>
        <groupId>org.apache.felix</groupId>
        <artifactId>org.apache.felix.scr.annotations</artifactId>
        <version>1.6.0</version>
        <scope>compile</scope>
    </dependency>
</dependencies>
</project>
```

공용 Adobe 리포지토리를 사용할 수 있도록 [콘텐츠 패키지 Maven 플러그인](/help/sites-developing/vlt-mavenplugin.md) 섹션에서 maven 설정 파일에 제공하는 프로필을 추가합니다.
