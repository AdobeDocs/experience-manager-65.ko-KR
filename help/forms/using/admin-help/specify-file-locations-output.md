---
title: 출력 파일 위치 지정
seo-title: 출력 파일 위치 지정
description: 출력 파일의 위치를 지정하는 방법을 알아봅니다.
seo-description: 출력 파일의 위치를 지정하는 방법을 알아봅니다.
uuid: 3287274f-85b5-4811-8abb-d347a9b80947
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 460bbb31-8187-469c-8102-b310093b6c03
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 0%

---


# 출력 {#specify-file-locations-for-output}의 파일 위치 지정

출력 시 필요한 특정 유형의 파일을 찾는 위치를 지정할 수 있습니다.

1. 관리 콘솔에서 서비스 > 출력을 클릭합니다.
1. 위치에서 적절한 옵션을 지정합니다.
1. 저장을 클릭합니다.

## 위치 설정 {#locations-settings}

**컨텐츠 루트 URI:** 양식이 검색되는 저장소의 절대 위치입니다. 이 값은 API를 통해 지정된 sForm 매개 변수와 결합하여 검색된 양식의 절대 경로를 구성합니다. 이 값은 HTTP를 사용하여 액세스할 수 있는 디렉터리 또는 웹 위치를 참조할 수 있습니다.

기본값은 빈 문자열입니다.

**XCI 구성 파일:** 출력 서비스가 렌더링을 위해 사용하는 XCI 구성 파일의 상대 또는 절대 위치입니다. 상대 값의 경우 XCI 파일은 AEM forms 배포 가능한 EAR 파일에 있다고 가정합니다.

기본값은 `com/adobe/formServer/PA/pa_output.xci`입니다.

**캐시 위치:** 출력 디스크 캐시의 위치를 지정합니다. 이 설정을 변경하면 현재 위치의 모든 기존 캐시 정보가 재설정되고 새 위치에 새 캐시가 만들어집니다. 다음 옵션 중 하나를 선택합니다.

**기본 위치:** 기본 선택입니다. 이 옵션을 선택하면 사용 중인 응용 프로그램 서버에 종속된 위치에서 캐시가 생성됩니다.

* **JBoss:** `[JBoss Home]\server\[install type]\svcdata\Output\Cache`
* **WebLogic:** `[WebLogic Home]\user_projects\domains\[aem-forms domain Name]\adobe\[forms server name]\Output\Cache`
* **WebSphere:** `[IBM Home]\WebSphere\AppServer\installedApps\adobe\server1\Output\Cache`

**LC** 임시 디렉토리: 캐시는 AEM forms temp 디렉토리의 하위 디렉토리에 만들어집니다. 이 하위 디렉토리는 설정 > 핵심 시스템 설정 > 구성 > 임시 디렉토리 위치의 관리 콘솔에서 지정됩니다. 하위 디렉터리의 이름은 `adobeoutput_[servername]`입니다.

>[!NOTE]
>
>임시 정리 유틸리티를 사용하는 경우 이러한 디렉토리를 삭제하는 동안 기능에 영향을 주지 않으므로 새 캐시가 생성될 때까지 짧은 시간 동안 성능에 큰 영향을 줄 수 있습니다. 이 문제를 방지하려면 AEM forms temp 디렉토리를 지우는 동안 이러한 디렉토리를 삭제하지 마십시오.

