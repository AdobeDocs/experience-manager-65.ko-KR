---
title: JEE에서 AEM Forms의 봄 프레임워크 취약점 완화
description: JEE에서 AEM Forms의 봄 프레임워크 취약점 완화
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Security
geptopics: SG_AEMFORMS/categories/jee
role: Admin
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: 61cce7cd8290156bec6dcc351a59093f545a4ec7
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 1%

---


# JEE에서 AEM Forms의 스프링 프레임워크 취약점 완화

이 문서에서는 JEE의 AEM Forms에 영향을 주는 두 가지 중요한 스프링 프레임워크 취약점을 해결하는 방법에 대한 지침을 제공합니다.

- **[CVE-2024-38819](https://spring.io/security/cve-2024-38819)**: 기능 웹 프레임워크의 경로 탐색 취약성
- **[CVE-2024-38820](https://spring.io/security/cve-2024-38820)**: Spring Framework DataBinder 대/소문자 구분 일치 예외

## 영향을 받는 버전

- JEE의 Adobe Experience Manager 6.5 Forms
- 버전 AEM 6.5 Forms GA에서 6.5.22.0(으)로

## 해결 방법

### 버전별 솔루션

| AEM Forms 버전 | 필수 작업 |
|-------------------|-----------------|
| 6.5.22.0 | 1. [환경을 위한 핫픽스를 다운로드](/help/release-notes/aem-forms-hotfix.md). </br> 2. 이 수정 사항을 설치하려면 지침에 따라 [JEE의 AEM 양식에 서비스 팩을 설치](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md)하십시오. |
| 6.5.17.0 - 6.5.21.0 | [수동 완화 단계 적용](#manual-mitigation-steps). |
| 6.5 - 6.5.16.0 | 1. [최신 서비스 팩을 설치합니다](/help/release-notes/release-notes.md)<br>2. 업데이트된 버전을 기반으로 [적절한 솔루션을 구현](#version-specific-solutions)합니다. |

> **참고**: AEM Forms은 공식적으로 최신 서비스 팩 6개만 지원합니다. 이전 버전의 사용자는 먼저 최신 서비스 팩으로 업그레이드한 다음 필요한 핫픽스를 설치해야 합니다.

## 배포 고려 사항

### 클러스터된 환경의 경우

클러스터형 배포 작업 시:

- 클러스터의 **모든 노드**&#x200B;에서 JAR 파일 대체 요소 적용(#4단계)
- 모든 서버에서 동일한 JAR 버전을 사용하여 일관성 유지
- 서비스를 다시 시작하기 전에 모든 노드에 대한 전체 업데이트
- 시스템 다운타임을 최소화하기 위해 조정된 재시작 전략 구현

### 단일 노드 환경의 경우

독립형 배포로 작업할 때:

- 관리할 로케이터 서버가 없으므로 간소화된 프로세스를 따르십시오.
- 로케이터 서버 구성 또는 시작과 관련된 단계를 생략합니다
- 다른 모든 단계(특히 JAR 교체 및 매니페스트 업데이트)를 완료하십시오.
- 모든 변경 사항을 구현한 후 애플리케이션 서버 다시 시작

## 수동 완화 단계

1. 애플리케이션 서버를 중지합니다.
1. 및 로케이터 서버를 중지합니다.
1. 코어 EAR에서 스프링 JAR 제거:
   1. 다음으로 이동 `[Adobe_Experience_Manager_Forms installation directory]/deploy`.
   1. 보관 관리자 도구를 사용하여 `adobe-core-<appserver>.ear` 파일을 엽니다. 환경에 따라 `<appserver>`이(가) JBoss, WebLogic 또는 WebSphere일 수 있습니다.
   - **JBoss:**&#x200B;의 경우 `ear/lib` 폴더로 이동하여 다음 JAR 파일을 삭제합니다.
- `spring-core-<version>.jar`
- `spring-web-<version>.jar`

   - **WebLogic 또는 WebSphere의 경우:** EAR의 루트에서 다음 JAR 파일을 삭제합니다.
- `spring-core-<version>.jar`
- `spring-web-<version>.jar`

   - **모든 응용 프로그램 서버의 경우:** `adobe-core-<appserver>.ear`의 루트 수준에서 `adobe-dscf.jar` 파일을 열고 `META-INF/MANIFEST.MF` 파일을 편집하여 다음 JAR 파일에 대한 참조를 제거하십시오.
- `spring-core-<version>.jar`
- `spring-web-<version>.jar`

1. Geode 배포에서 JAR 파일 바꾸기:
   1. `<Adobe_Experience_Manager_Forms>/lib/caching/lib`(으)로 이동
   1. 기존 JAR 파일을 업데이트된 버전으로 바꿉니다.
   - `spring-context-<version>.jar` → `spring-context-6.1.14.jar`
   - `spring-beans-<version>.jar` → `spring-beans-6.1.14.jar`
   - `spring-core-<version>.jar` → `spring-core-6.1.14.jar`
   - `spring-jcl-<version>.jar` → `spring-jcl-6.1.14.jar`
   - `spring-web-<version>.jar` → `spring-web-6.1.14.jar`

   최신 JAR 파일을 가져오려면 [Adobe 소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-vuln-30727/spring-6.1.14-jars.zip)에서 spring-6.1.14-jars.zip 파일을 다운로드하고 ZIP 파일을 추출하여 업데이트된 Spring 프레임워크 JAR 파일에 액세스합니다.

   1. 다음 JAR 파일에서 MANIFEST.MF 파일을 업데이트합니다.
   - `geode-server-all-<version>.jar`
   - `gfsh-dependencies.jar`

   각 JAR에 대해
   - 아카이브 관리자 도구를 사용하여 JAR 열기
   - `META-INF/MANIFEST.MF` 파일을 찾아 추출합니다.
   - 텍스트 편집기에서 MANIFEST.MF 파일 편집
   - &quot;Class-Path&quot; 섹션을 찾아 모든 Spring 프레임워크 참조를 업데이트합니다.
      - `spring-core-<version>.jar` - `spring-core-6.1.14.jar`
      - `spring-web-<version>.jar` - `spring-web-6.1.14.jar`
      - `spring-context-<version>.jar` - `spring-context-6.1.14.jar`
      - `spring-beans-<version>.jar` - `spring-beans-6.1.14.jar`
      - `spring-jcl-<version>.jar` - `spring-jcl-6.1.14.jar`
   - 수정된 MANIFEST.MF 파일을 저장합니다.
   - JAR의 원래 MANIFEST.MF를 업데이트된 버전으로 바꿉니다
   - JAR 파일을 저장합니다.

   1. 감시할 일반적인 문제:
      - 매니페스트에 중복된 항목이 없는지 확인
      - 적절한 라인 끝 유지
      - 참조된 모든 JAR가 지정된 위치에 있는지 확인합니다.

   1. 확인 단계:
      - 매니페스트가 제대로 업데이트되었는지 확인
      - 모든 봄 종속성이 올바르게 참조되었는지 확인
      - 이전 버전 참조가 남아 있지 않은지 확인합니다.
      - 응용 프로그램을 테스트하여 클래스 로드 문제가 없는지 확인합니다.

1. 구성 관리자를 실행합니다.

1. 서버 다시 시작:
   - JDK 17을 사용하여 로케이터 서버 시작
   - 이전에 사용한 것과 동일한 JDK 버전(JDK 8 또는 JDK 11)을 사용하여 응용 프로그램 서버를 시작합니다.
