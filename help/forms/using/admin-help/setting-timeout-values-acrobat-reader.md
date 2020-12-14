---
title: Acrobat Reader DC 익스텐션에 사용할 시간 초과 값 설정
seo-title: Acrobat Reader DC 익스텐션에 사용할 시간 초과 값 설정
description: Acrobat Reader DC 익스텐션에서 사용할 수 있도록 시간 초과 값을 설정하는 방법을 알아봅니다.
seo-description: Acrobat Reader DC 익스텐션에서 사용할 수 있도록 시간 초과 값을 설정하는 방법을 알아봅니다.
uuid: d6d072a0-0a30-417a-98b1-df8b4ff8f911
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a9aeeb89-45e9-4d5d-aa25-8145c89b64f2
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---


# Acrobat Reader DC 확장 {#setting-timeout-values-for-use-with-acrobat-reader-dc-extensions}에 사용할 시간 초과 값 설정

Acrobat Reader DC Extension에서 많은 PDF 파일을 작업할 때 다음 시간 제한 값이 적절하게 설정되어 작업이 시간 초과와 실패를 방지할 수 있습니다.

**문서 처리 시간 초과**

이 값은 관리 콘솔에서 설정할 수 있습니다. 설정 > 핵심 시스템 설정 > 구성을 클릭하고 기본 문서 처리 시간 초과에 대한 값을 지정합니다.

**사용자 관리자 AEM 양식 시간 초과:** 이 값은 config.xml 파일을 편집하여 설정할 수 있습니다. 관리 콘솔에서 설정 > 사용자 관리 > 구성 > 구성 파일 가져오기 및 내보내기를 클릭한 다음 내보내기를 클릭합니다. 내보낸 config.xml 파일을 열고 다음 줄을 편집합니다.

&lt;entry key=&quot;assertionValidityInMinutes&quot; value=&quot;600&quot; />

&lt;entry key=&quot;SessionTimeout&quot; value=&quot;600&quot; />

config.xml 파일을 저장하고 다시 관리 콘솔로 가져옵니다.

**응용 프로그램 서버 세션 시간 초과:** 이 값은 응용 프로그램 서버에서 설정할 수 있습니다. 자세한 내용은 응용 프로그램 서버와 함께 제공되는 설명서를 참조하십시오.
