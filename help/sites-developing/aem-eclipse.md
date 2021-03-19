---
title: Eclipse용 AEM 개발자 도구
seo-title: Eclipse용 AEM 개발자 도구
description: Eclipse용 AEM 개발자 도구
seo-description: 'null'
uuid: 566e49f2-6f28-4aa7-bfe0-b5f9675310bf
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: a2ae76a8-50b0-4e43-b791-ad3be25b8582
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '814'
ht-degree: 4%

---


# Eclipse용 AEM 개발자 도구{#aem-developer-tools-for-eclipse}

![](do-not-localize/chlimage_1-9.png)

## 개요 {#overview}

AEM Developer Tools for Eclipse는 Apache License 2 아래에 릴리스된 Apache Sling](https://sling.apache.org/documentation/development/ide-tooling.html)용 [Eclipse 플러그인을 기반으로 하는 Eclipse 플러그인입니다.

AEM 개발을 쉽게 하는 여러 기능을 제공합니다.

* Eclipse Server Connector를 통해 AEM 인스턴스와 원활하게 통합
* 컨텐츠 및 OSGI 번들 모두에 대한 동기화
* 코드 핫 스와핑 기능을 사용하여 지원 디버깅
* 특정 프로젝트 제작 마법사를 통한 AEM 프로젝트의 간단한 부트스트래핑
* 간편한 JCR 속성 편집

## 요구 사항 {#requirements}

AEM 개발자 도구를 사용하기 전에 다음을 수행해야 합니다.

* Java EE 개발자용 [Eclipse IDE](https://eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunar)를 다운로드하여 설치합니다. AEM 개발자 도구는 현재 Eclipse Kepler 이상을 지원합니다.

* AEM 버전 5.6.1 이상에서 사용 가능
* [Eclipse FAQ](https://wiki.eclipse.org/FAQ_How_do_I_increase_the_heap_size_available_to_Eclipse%3F)에 설명된 대로 `eclipse.ini` 구성 파일을 편집하여 Eclipse 설치를 최소 1GB의 더미 메모리가 있는지 확인합니다.

>[!NOTE]
>
>macOS의 경우 **Eclipse.app**&#x200B;을 마우스 오른쪽 단추로 클릭한 다음 **패키지 내용 표시**&#x200B;를 선택하여 `eclipse.ini`**.**

## Eclipse용 AEM 개발자 도구 설치 방법 {#how-to-install-the-aem-developer-tools-for-eclipse}

위의 [요구 사항](#requirements)을 충족하면 다음과 같이 플러그인을 설치할 수 있습니다.

1. [**AEM** 개발자 도구 웹 사이트](https://eclipse.adobe.com/aem/dev-tools/)를 찾습니다.

1. **설치 링크**&#x200B;를 복사합니다.

   또는 설치 링크를 사용하는 대신 아카이브를 다운로드할 수 있습니다. 이렇게 하면 오프라인 설치가 가능하지만 이 방법으로 자동 업데이트 알림이 누락됩니다.

1. Eclipse에서 **도움말** 메뉴를 엽니다.
1. **새 소프트웨어 설치**&#x200B;를 클릭합니다.
1. **추가...를 클릭합니다.**.
1. **이름**&#x200B;에 AEM 개발자 도구를 입력합니다.
1. **위치**&#x200B;에서 설치 URL을 복사합니다.
1. **확인**&#x200B;을 클릭합니다.
1. **AEM** 및 **Sling** 플러그인을 모두 선택합니다.
1. **다음**&#x200B;을 클릭합니다.
1. **다음**&#x200B;을 클릭합니다.
1. 라인 계약에 동의하고 **완료**&#x200B;를 클릭합니다.
1. Eclipse를 다시 시작하려면 **예**&#x200B;를 클릭합니다.

## 기존 프로젝트 {#how-to-import-existing-projects} 가져오기 방법

>[!NOTE]
>
>AEM](https://stackoverflow.com/questions/29699726/how-to-work-with-a-bundle-in-eclipse-when-it-was-downloaded-from-aem/29705407#29705407)에서 다운로드할 때 Eclipse에서 번들을 사용하여 작업하는 방법을 참조하십시오.[

## AEM 원근 {#the-aem-perspective}

Eclipse용 AEM 개발 도구는 AEM 프로젝트 및 인스턴스를 완벽하게 제어할 수 있는 원근감과 함께 제공됩니다.

![chlimage_1-2](assets/chlimage_1-2a.jpeg)

## 샘플 다중 모듈 프로젝트 {#sample-multi-module-project}

AEM Developer Tools for Eclipse는 Eclipse에서 프로젝트 설정을 신속하게 시작할 수 있을 뿐만 아니라 여러 AEM 기능에 대한 모범 사례 가이드 역할을 하는 다양한 모듈 방식의 샘플 프로젝트를 제공합니다. [프로젝트 원형에 대한 자세한 내용을 살펴보십시오](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype).

다음 단계에 따라 샘플 프로젝트를 만듭니다.

1. **파일** > **새로 만들기** > **프로젝트** 메뉴에서 **AEM** 섹션으로 이동하여 **AEM 샘플 다중 모듈 프로젝트**&#x200B;를 선택합니다.

   ![chlimage_1-69](assets/chlimage_1-69a.png)

1. **다음**&#x200B;을 클릭합니다.

   >[!NOTE]
   >
   >m2eclipse가 원형 카탈로그를 스캔해야 하므로 이 단계는 다소 시간이 걸릴 수 있습니다.

   ![chlimage_1-70](assets/chlimage_1-70a.png)

1. **com.adobe.granite.tranypes를 선택합니다.sample-project-tranype :(최고 번호)** 메뉴에서 **다음**&#x200B;을 클릭합니다.

   ![chlimage_1-71](assets/chlimage_1-71a.png)

1. 샘플 프로젝트에 대한 **이름**, **그룹 ID** 및 **아티팩트 ID**&#x200B;를 입력합니다. 일부 고급 속성을 설정하도록 선택할 수도 있습니다.

   ![chlimage_1-72](assets/chlimage_1-72a.png)

1. 그런 다음 Eclipse가 연결할 AEM 서버를 구성해야 합니다.

   디버거 기능을 사용하려면 디버그 모드에서 AEM을 시작해야 합니다. 이 단계는 명령줄에 다음을 추가하여 수행할 수 있습니다.

   ```
       -nofork -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=10123
   ```

   ![chlimage_1-73](assets/chlimage_1-73a.png)

1. **완료**&#x200B;를 클릭합니다. 프로젝트 구조가 만들어집니다.

   >[!NOTE]
   >
   >새로 설치할 때(자세히:maven 종속성을 다운로드하지 않은 경우) 오류가 있는 프로젝트를 만들 수 있습니다. 이 경우 [잘못된 프로젝트 정의 확인](#resolving-invalid-project-definition)에 설명된 절차를 따르십시오.

## 문제 해결 {#troubleshooting}

### 잘못된 프로젝트 정의 {#resolving-invalid-project-definition} 해결

잘못된 종속성 및 프로젝트 정의를 해결하려면 다음과 같이 하십시오.

1. 생성된 프로젝트를 모두 선택합니다.
1. 마우스 오른쪽 버튼을 클릭합니다. **Maven** 메뉴에서 **프로젝트 업데이트**&#x200B;를 선택합니다.
1. **스냅샷/릴리스 업데이트 강제 적용**&#x200B;을 선택합니다.
1. **확인**&#x200B;을 클릭합니다. Eclipse는 필요한 종속성을 다운로드하려고 합니다.

### JSP 파일 {#enabling-tag-library-autocompletion-in-jsp-files}에서 태그 라이브러리 자동 완성 활성화

적절한 종속성이 프로젝트에 추가되면 태그 라이브러리 자동 완성 기능이 즉시 작동합니다. AEM Uber Jar를 사용할 때 필요한 tld 및 TagExtraInfo 파일이 포함되지 않은 알려진 문제가 하나 있습니다.

이 문제를 해결하려면 AEM Uber Jar 앞에 있는 클래스 경로에 org.apache.sling.scripting.jsp.taglib 아티팩트가 있는지 확인합니다. Maven 프로젝트의 경우 Uber Jar 앞에 다음 종속성을 pom.xml에 배치합니다.

```xml
<dependency>
  <groupId>org.apache.sling</groupId>
  <artifactId>org.apache.sling.scripting.jsp.taglib</artifactId>
  <scope>provided</scope>
</dependency>
```

AEM 배포에 적합한 버전을 추가해야 합니다.

## 추가 정보 {#more-information}

Eclipse 웹 사이트용 공식 Apache Sling IDE 툴은 다음과 같은 유용한 정보를 제공합니다.

* Eclipse용 [**Apache Sling IDE 도구** 사용 안내서](https://sling.apache.org/documentation/development/ide-tooling.html)에서 이 설명서는 AEM 개발 도구에서 지원하는 전체 개념, 서버 통합 및 배포 기능을 안내합니다.
* [문제 해결 섹션](https://sling.apache.org/documentation/development/ide-tooling.html#troubleshooting).
* [알려진 문제 목록](https://sling.apache.org/documentation/development/ide-tooling.html#known-issues).

다음 공식 [Eclipse](https://eclipse.org/) 설명서는 환경을 설정하는 데 도움이 될 수 있습니다.

* [Eclipse 시작하기](https://eclipse.org/users/)
* [Eclipse Luna Help System](https://help.eclipse.org/luna/index.jsp)
* [Maven 통합(m2eclipse)](https://www.eclipse.org/m2e/)

