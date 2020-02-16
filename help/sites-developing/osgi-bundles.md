---
title: OSGI 번들
seo-title: OSGI 번들
description: OSGi 번들 관리를 위한 팁
seo-description: OSGi 번들 관리를 위한 팁
uuid: 07af7089-a233-4e5b-928c-76ddc0af8839
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 8d3374ac-51dd-4ff5-84c9-495c937ade12
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# OSGI 번들{#osgi-bundles}

## 의미 체계 버전 관리 사용 {#use-semantic-versioning}

의미 체계 버전 번호 매기기에 대한 합의된 우수 사례는 https://semver.org/에서 찾을 수 [있습니다](https://semver.org/).

## OSGi 번들에 반드시 필요한 것보다 더 많은 클래스와 병을 임베드하지 마십시오 {#do-not-embed-more-classes-and-jars-than-strictly-needed-in-osgi-bundles}

공통 라이브러리는 별도의 번들로 분리해야 합니다. 이렇게 하면 번들에서 다시 사용할 수 있습니다. OSGI *번들로 JAR를* 래핑할 때는 온라인 소스를 확인하여 이전에 이미 이러한 작업을 수행했는지 확인해야 합니다. 기존 번들 포장지를 찾을 수 있는 몇 가지 일반적인 위치는 다음과 같습니다.Apache Felix, Apache Sling, Apache Geronimo, Apache ServiceMix, Eclipse Bundle Recipes 및 SpringSource Enterprise Bundle Repository.

## 가장 필요한 번들 버전에 따라 다름 {#depend-on-the-lowest-needed-bundle-versions}

POM 파일의 컴파일 타임 종속성의 경우 항상 필요한 API를 노출하는 가장 낮은 버전에 따라 달라집니다. 이전 버전과의 호환성이 향상되고 이전 릴리스에 대한 백업 수정 작업이 더 쉬워집니다.

## OSGi 번들에서 최소한의 패키지 세트 내보내기 {#export-a-minimal-set-of-packages-from-osgi-bundles}

패키지를 내보내자마자 다른 사람이 신뢰할 수 있는 API를 만들었습니다. 가능한 한 적게 내보내고 내보낼 내용이 API인지 확인합니다. 이전에 내보낸 내용을 가져와서 비공개로 만드는 것보다 비공개 메서드/클래스를 사용하고 공개하는 것이 훨씬 쉽습니다.

구현은 항상 별도의 *구현* 패키지에 넣어야 합니다. 기본적으로 *maven-bundle-plugin* 은 프로젝트에 이름이 *영향을* 받지 않은 모든 항목을 내보냅니다.

## 내보낸 각 패키지에 대해 항상 의미 버전 정의 {#always-explicitly-define-a-semantic-version-for-each-package-exported}

이렇게 하면 API 소비자가 자신과 함께 진화할 수 있습니다. 이때 항상 의미 체계 버전 관리 우수 사례를 따르십시오. 이를 통해 API 사용자는 새로운 버전에서 어떤 유형의 변경 사항을 예상할 수 있는지 알 수 있습니다.

## 노출된 메타데이터 정보 포함 {#include-metatype-information-where-exposed}

의미 있는 메타데이터 유형 정보를 지정하면 Felix 콘솔에서 서비스 및 구성 요소를 쉽게 이해할 수 있습니다. SCR 주석 및 속성 목록은 다음 사이트에서 찾을 수 있습니다.https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html [](https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html).
