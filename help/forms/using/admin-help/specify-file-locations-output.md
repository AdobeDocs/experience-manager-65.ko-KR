---
title: 출력에 대한 파일 위치 지정
seo-title: Specify file locations for Output
description: 출력에 대한 파일 위치를 지정하는 방법을 배웁니다.
seo-description: Learn how to specify file locations for Output.
uuid: 3287274f-85b5-4811-8abb-d347a9b80947
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 460bbb31-8187-469c-8102-b310093b6c03
exl-id: 620c69d6-4fe1-46d6-b5d4-3b562142e547
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 1%

---

# 출력에 대한 파일 위치 지정 {#specify-file-locations-for-output}

출력이 필요한 특정 유형의 파일을 찾는 위치를 지정할 수 있습니다.

1. 관리 콘솔에서 서비스 > 출력을 클릭합니다.
1. 위치(Locations)에서 적절한 옵션을 지정합니다.
1. 저장을 클릭합니다.

## 위치 설정 {#locations-settings}

**컨텐츠 루트 URI:** 양식이 검색되는 저장소의 URI 또는 절대 위치입니다. 이 값은 API를 통해 지정된 sForm 매개 변수와 결합하여 검색된 양식의 절대 경로를 구성합니다. 이 값은 HTTP를 사용하여 액세스할 수 있는 디렉터리 또는 웹 위치를 참조할 수 있습니다.

기본값은 빈 문자열입니다.

**XCI 구성 파일:** 출력 서비스에서 렌더링에 사용하는 XCI 구성 파일의 상대 또는 절대 위치입니다. 상대 값의 경우 XCI 파일이 AEM Forms 배포 가능한 EAR 파일에 있다고 가정합니다.

기본값은 `com/adobe/formServer/PA/pa_output.xci`입니다.

**캐시 위치:** 출력 디스크 캐시의 위치를 지정합니다. 이 설정을 변경하면 현재 위치의 모든 기존 캐시 정보가 재설정되고 새 위치에 새 캐시가 만들어집니다. 다음 옵션 중 하나를 선택합니다.

**기본 위치:** 기본 선택 사항입니다. 이 옵션을 선택하면 사용 중인 응용 프로그램 서버에 종속된 위치에 캐시가 만들어집니다.

* **JBoss:** `[JBoss Home]\server\[install type]\svcdata\Output\Cache`
* **WebLogic:** `[WebLogic Home]\user_projects\domains\[aem-forms domain Name]\adobe\[forms server name]\Output\Cache`
* **WebSphere:** `[IBM Home]\WebSphere\AppServer\installedApps\adobe\server1\Output\Cache`

**LC 임시 디렉터리:** 캐시는 AEM Forms temp 디렉토리의 하위 디렉토리에 생성됩니다. 이 디렉토리는 설정 > 핵심 시스템 설정 > 구성 > 임시 디렉토리 위치 아래의 관리 콘솔에 지정됩니다. 하위 디렉토리의 이름은 다음과 같습니다 `adobeoutput_[servername]`.

>[!NOTE]
>
>임시 클리닝 유틸리티를 사용하는 경우 이러한 디렉터리를 삭제하는 동안 새 캐시가 만들어지기 전까지 단시간에 성능에 큰 영향을 줄 수 있습니다. 이 문제를 방지하려면 AEM forms temp 디렉터리를 지울 때 이러한 디렉터리를 삭제하지 마십시오.
