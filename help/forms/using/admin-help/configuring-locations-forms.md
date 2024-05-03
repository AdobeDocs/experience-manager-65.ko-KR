---
title: Forms에 대한 위치 구성
description: AEM Form의 위치를 구성하는 방법에 대해 알아봅니다. 속성의 파일 위치, 양식의 위치, 시드 PDF 파일 및 캐시 위치를 지정할 수 있습니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 0d9eb7fe-28a6-444e-957d-023687158c61
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '822'
ht-degree: 1%

---

# Forms에 대한 위치 구성 {#configuring-locations-for-forms}

웹 루트, 검색할 양식 위치, PDForm 변환에 사용되는 시드 PDF 파일 및 캐시 위치와 같은 속성의 URL, URI 및 파일 위치를 지정할 수 있습니다.

1. 관리 콘솔에서 서비스 > Forms을 클릭합니다.
1. 위치(Locations)에서 적절한 옵션을 지정합니다. 옵션은 아래에 설명되어 있습니다.
1. 저장을 클릭합니다.

## 위치 설정 {#locations-settings}

**기본 URL:** 이미지 및 스크립트와 같은 양식 리소스가 있는 기본 URL입니다. 이 값은 이미지 또는 스크립트와 같은 외부 종속성에 대한 HREF 참조를 포함하는 HTML 변환에 필요합니다. HTML 양식에서 XFA 인텔리전스를 수행하는 데 필요한 xfasubset.js 스크립트가 있습니다. 이 값은 콘텐츠 루트 URI와 동등한 HTTP 값이어야 합니다.

>[!NOTE]
>
>기본 URL은 HTTP 또는 저장소 프로토콜만 지원합니다. file:/// 와 같은 프로토콜은 지원하지 않습니다. 사용자 지정 CSS 또는 디지털 서명 URI와 같은 리소스에 액세스해야 하는 경우 적절한 API 매개 변수 값을 사용하여 절대 위치를 지정하십시오.

종속성 경로가 절대적이면 기본 URL 값이 무시됩니다. 그렇지 않으면 종속성 경로가 기본 URL과 결합됩니다.

기본값은 빈 문자열입니다.

다음 예제는 동일한 콘텐츠(콘텐츠 루트 URI 및 기본 URL 사용)를 가리킵니다.

`(ContentRootURI)/subdir/image1.jpg`

`(BaseURL)/subdir/image1.jpg`

**FS 웹 루트 URI:** Forms 웹 애플리케이션의 URL. Forms 웹 응용 프로그램과 클라이언트 응용 프로그램이 동일한 응용 프로그램 서버에 배포된 경우 이 상자를 비워 둘 수 있습니다. Forms API 웹 루트 URL이 사용됩니다.

Forms 웹 응용 프로그램과 클라이언트 응용 프로그램이 동일한 응용 프로그램 서버에 배포되지 않은 경우 다음 예제와 같이 이 상자에 Forms 웹 응용 프로그램의 URL을 입력합니다.

`https://<host name>:<port>/FormServer`

위치 `host name`및 `port` 는 Forms 웹 애플리케이션을 호스팅하는 서버의 서버 이름 및 포트 번호입니다.

기본값은 빈 문자열입니다.

**웹 루트 URI:** 애플리케이션의 웹 루트. 이 값은 AEM Forms SDK를 통해 지정된 sTargetURL 매개 변수(sTargetURL이 상대적인 값으로 제공되는 경우)와 결합하여 애플리케이션별 웹 콘텐츠에 액세스할 수 있는 절대 URL을 구성합니다.

기본값은 빈 문자열입니다.

**컨텐츠 루트 URI:** 양식을 검색하는 URI 또는 절대 위치입니다. 이 값은 API를 통해 지정된 sFormQuery 매개 변수와 결합하여 검색되는 양식에 대한 절대 경로를 구성합니다. 이 값은 HTTP를 사용하여 액세스할 수 있는 디렉토리 또는 웹 위치를 참조할 수 있습니다.

기본값은 빈 문자열입니다.

**XCI 구성 URI:** 렌더링에 사용된 XCI 파일이 발견되는 상대 위치 또는 절대 위치입니다. 상대적인 값의 경우 XCI 파일이 배포 가능한 AEM Forms EAR 파일에 있다고 가정합니다.

기본값은 `com/adobe/formServer/PA/pa.xci`입니다.

**글꼴 맵 URI:** 글꼴 매핑 파일의 상대 위치 또는 절대 위치입니다. 상대적인 값의 경우 이 파일은 배포 가능한 AEM Forms EAR 파일에 있다고 가정합니다.

글꼴 매핑 파일은 양식의 HTML 변환을 위한 사용자 정의 글꼴 매핑을 생성하는 데 사용되므로 클라이언트의 컴퓨터에서 글꼴을 사용할 수 없는 경우 대체할 글꼴을 지정할 수 있습니다.

기본값은 `com/adobe/formServer/client-font-map.properties`입니다.

다음 항목은 글꼴 매핑 파일의 항목 예입니다.

`Arial=Arial,Helvetica,sans-serif`

**시드 PDF 파일:** 게재를 최적화하기 위해 PDForm 변환에 사용되는 초기 PDF 파일입니다. 시드 PDF 파일은 양식 디자인 및 데이터가 추가된 사용자 지정 PDF 파일(XFA 스트림, 이미지 및 글꼴 리소스만 포함)을 지정합니다. 양식은 Acrobat 7 이상에서 렌더링되며 PDForm 변환에 적용됩니다.

기본값은 빈 문자열입니다.

**캐시 위치:** Forms 디스크 캐시의 위치를 지정합니다. 이 설정을 변경하면 현재 위치의 모든 기존 캐시 정보가 재설정되고 새 위치에 새 캐시가 만들어집니다. 다음 옵션 중 하나를 선택합니다.

**기본 위치:** 이것이 기본 선택입니다. 이 옵션을 선택하면 사용 중인 애플리케이션 서버에 종속된 위치에 캐시가 만들어집니다.

* **JBos:** [JBoss 홈]\server\[설치 유형]\svcdata\FormServer\Cache
* **웹 논리:** [WebLogic 홈]\user_projects\domains\[aem-forms Domain Name]\adobe\[Forms 서버 이름]\FormServer\Cache
* **WebSphere:** [IBM 홈]\WebSphere\AppServer\installedApps\adobe\server1\FormServer\Cache

**LC 임시 디렉터리:** 캐시는 AEM forms 임시 디렉터리의 하위 디렉터리에 생성되며, 이 디렉터리는 설정 > 핵심 시스템 설정 > 구성 > 임시 디렉터리 위치 아래의 관리 콘솔에 지정됩니다. 하위 디렉터리의 이름은 adobeform_입니다.[servername].

>[!NOTE]
>
>임시 청소 유틸리티를 사용하는 경우 이러한 디렉토리를 삭제해도 기능에 영향을 주지 않으므로 새 캐시가 생성될 때까지 잠시 동안 성능에 상당한 영향을 줄 수 있습니다. 이 문제를 방지하려면 AEM Forms 임시 디렉터리를 지우는 동안 이러한 디렉터리를 삭제하지 마십시오.
