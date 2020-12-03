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
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 1%

---


# OSGI 번들{#osgi-bundles}

## 의미 체계 버전 관리 {#use-semantic-versioning} 사용

의미 체계 버전 번호 매기기에 대한 우수 사례를 [https://semver.org/](https://semver.org/)에서 참조할 수 있습니다.

## OSGi 번들 {#do-not-embed-more-classes-and-jars-than-strictly-needed-in-osgi-bundles}에 반드시 필요한 것보다 더 많은 클래스와 병을 포함시키지 마십시오

공통 라이브러리를 별도의 번들로 팩토링해야 합니다. 이를 통해 번들에서 재사용할 수 있습니다. OSGI 번들의 *JAR*&#x200B;을 둘러싸는 경우 온라인 소스를 확인하여 이전에 이미 이 작업을 수행했는지 확인하십시오. 기존 번들 포장지를 찾을 수 있는 몇 가지 일반적인 위치는 다음과 같습니다.Apache Felix, Apache Sling, Apache Geronimo, Apache ServiceMix, Eclipse Bundle Recipes 및 SpringSource Enterprise Bundle Repository.

## 가장 필요한 번들 버전 {#depend-on-the-lowest-needed-bundle-versions}에 따라 다름

POM 파일의 컴파일 시간 종속성의 경우, 항상 필요한 API를 노출하는 가장 필요한 버전에 따라 달라집니다. 이전 버전과의 호환성이 향상되고 이전 릴리스에 대한 백업 수정 작업이 더 쉬워집니다.

## OSGi 번들에서 최소 패키지 세트 내보내기 {#export-a-minimal-set-of-packages-from-osgi-bundles}

패키지를 내보내자마자 다른 사람이 사용할 수 있는 API를 만들었습니다. 가능한 한 내보내야 하며 내보낼 내용이 API인지 확인합니다. 이전에 내보낸 것을 가져와 비공개로 만드는 것보다 비공개 메서드/클래스를 가져와 공개하는 것이 훨씬 쉽습니다.

구현은 항상 별도의 *impl* 패키지에 넣어야 합니다. 기본적으로 *maven-bundle-plugin*&#x200B;은 프로젝트의 이름에 *impl*&#x200B;이 없는 모든 것을 내보냅니다.

## 항상 내보낸 각 패키지의 의미 체계 버전을 명시적으로 정의합니다. {#always-explicitly-define-a-semantic-version-for-each-package-exported}

이를 통해 API 소비자가 자신과 함께 진화할 수 있습니다. 이때 항상 의미 체계 버전 관리 우수 사례를 따르십시오. 이를 통해 API 사용자는 새로운 버전에서 어떤 유형의 변경 사항을 예상할 수 있는지 알 수 있습니다.

## {#include-metatype-information-where-exposed}이(가) 노출되는 메타데이터 정보 포함

의미 있는 메타데이터 정보를 지정하면 Felix 콘솔에서 서비스 및 구성 요소를 쉽게 이해할 수 있습니다. SCR 주석 및 속성 목록은 다음 위치에 있습니다.[https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html](https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html).
