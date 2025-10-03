---
title: Output 파일 위치 지정
description: 콘텐츠 루트 URI, XCI 구성 파일, 캐시 및 기본값과 같은 특정 유형의 파일에 대해 Output 파일 위치를 지정하는 방법을 알아봅니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 620c69d6-4fe1-46d6-b5d4-3b562142e547
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '339'
ht-degree: 100%

---

# Output 파일 위치 지정 {#specify-file-locations-for-output}

>[!NOTE]
> 
> 사용자에게 관리자 콘솔에 액세스할 수 있는 관리자 권한이 있는지 확인하십시오.

Output에서 필요로 하는 특정 유형의 파일을 찾는 위치를 지정할 수 있습니다.

1. 관리 콘솔에서 서비스 > Output을 클릭합니다.
1. 위치에서 적절한 옵션을 지정합니다.
1. 저장을 클릭합니다.

## 위치 설정 {#locations-settings}

**콘텐츠 루트 URI:** 양식을 검색하는 저장소의 URI 또는 절대 위치입니다. 이 값은 API를 통해 지정된 sForm 매개변수와 결합되어 가져온 양식의 절대 경로를 구성합니다. 해당 값은 HTTP를 사용하여 액세스할 수 있는 디렉터리나 웹 위치를 참조할 수 있습니다.

기본값은 빈 문자열입니다.

**XCI 구성 파일:** Output 서비스에서 렌더링할 때 사용하는 XCI 구성 파일의 상대 위치 또는 절대 위치입니다. 상대 값의 경우 XCI 파일이 AEM Forms의 배포 가능한 EAR 파일에 있다고 간주합니다.

기본값은 `com/adobe/formServer/PA/pa_output.xci`입니다.

**캐시 위치:** Output 디스크 캐시의 위치를 지정합니다. 이 설정을 변경하면 현재 위치의 기존 캐시 정보가 모두 재설정되고 새 위치에 새 캐시가 생성됩니다. 다음 옵션 중 하나를 선택하십시오.

**기본 위치:** 기본 선택 항목입니다. 이 옵션을 선택하면 캐시는 사용 중인 애플리케이션 서버에 따라 다른 위치에 생성됩니다.

* **JBoss:** `[JBoss Home]\server\[install type]\svcdata\Output\Cache`
* **WebLogic:** `[WebLogic Home]\user_projects\domains\[aem-forms domain Name]\adobe\[Forms Server name]\Output\Cache`
* **WebSphere:** `[IBM Home]\WebSphere\AppServer\installedApps\adobe\server1\Output\Cache`

**LC 임시 디렉터리:** 캐시는 AEM Forms 임시 디렉터리의 하위 디렉터리에 생성됩니다. 이 디렉터리는 관리 콘솔의 설정 > 핵심 시스템 설정 > 구성 > 임시 디렉터리 위치에서 지정됩니다. 하위 디렉터리의 이름은 `adobeoutput_[servername]`입니다.

>[!NOTE]
>
>임시 정리 유틸리티를 사용하는 경우 해당 디렉터리를 삭제해도 기능에는 영향을 미치지 않지만, 새 캐시가 생성될 때까지 단기간 동안 성능에 상당한 영향을 미칠 수 있습니다. 이 문제를 방지하려면 AEM Forms 임시 디렉터리를 지우는 동안 해당 디렉터리를 삭제하지 마십시오.
