---
title: Forms 위치 구성
seo-title: Forms 위치 구성
description: Forms의 위치를 구성하는 방법을 알아봅니다.
seo-description: Forms의 위치를 구성하는 방법을 알아봅니다.
uuid: ba35888b-492c-4678-890b-160b53e7d659
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3d2b7cfb-228c-4cc2-8fcd-d500f0010010
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 0%

---


# Forms {#configuring-locations-for-forms}에 대한 위치 구성

웹 루트와 같은 속성의 URL, URI 및 파일 위치, 검색할 양식의 위치, PDF 형식으로 사용되는 시드 PDF 파일 및 캐시 위치를 지정할 수 있습니다.

1. 관리 콘솔에서 서비스 > Forms을 클릭합니다.
1. 위치 아래에서 적절한 옵션을 지정합니다. 옵션은 아래에 설명되어 있습니다.
1. 저장을 클릭합니다.

## 위치 설정 {#locations-settings}

**기본 URL:** 이미지 및 스크립트와 같은 양식 리소스가 있는 기본 URL입니다. 이미지 또는 스크립트와 같은 외부 종속성에 대한 HREF 참조를 포함하는 HTML 변환에 이 값이 필요합니다. 이러한 스크립트 중 하나는 xfasubset.js로, HTML 양식에서 XFA 인텔리전스를 수행하는 데 필요합니다. 이 값은 컨텐츠 루트 URI와 동일한 HTTP여야 합니다.

>[!NOTE]
>
>기본 URL은 HTTP 또는 저장소 프로토콜만 지원합니다. file:///과 같은 프로토콜을 지원하지 않습니다. 사용자 지정 CSS 또는 디지털 서명 URI와 같은 리소스에 액세스해야 하는 경우 적절한 API 매개 변수 값을 사용하여 절대 위치를 지정합니다.

종속성 경로가 절대이면 기본 URL 값이 무시됩니다. 그렇지 않으면 종속성 경로가 기본 URL과 결합됩니다.

기본값은 빈 문자열입니다.

다음 예제에서는 동일한 컨텐츠를 가리킵니다(컨텐츠 루트 URI 및 기본 URL 사용).

`(ContentRootURI)/subdir/image1.jpg`

`(BaseURL)/subdir/image1.jpg`

**FS 웹 루트 URI:** Forms 웹 응용 프로그램의 URL입니다. Forms 웹 응용 프로그램 및 클라이언트 응용 프로그램이 동일한 응용 프로그램 서버에 배포된 경우 이 상자를 비워 둘 수 있습니다.forms API 웹 루트 URL이 사용됩니다.

Forms 웹 응용 프로그램과 클라이언트 응용 프로그램이 동일한 응용 프로그램 서버에 배포되지 않은 경우 다음 예제와 같이 이 상자에 Forms 웹 응용 프로그램의 URL을 제공합니다.

`https://<host name>:<port>/FormServer`

여기서 `host name`과 `port`은 Forms 웹 응용 프로그램을 호스팅하는 서버의 서버 이름과 포트 번호입니다.

기본값은 빈 문자열입니다.

**웹 루트 URI:** 응용 프로그램의 웹 루트입니다. 이 값은 AEM 양식 SDK를 통해 지정된 sTargetURL 매개 변수(sTargetURL이 상대 형식으로 제공되는 경우)와 결합하여 응용 프로그램별 웹 콘텐츠에 액세스하기 위한 절대 URL을 생성합니다.

기본값은 빈 문자열입니다.

**컨텐츠 루트 URI:** 양식을 검색할 URI 또는 절대 위치입니다. 이 값은 API를 통해 지정된 sFormQuery 매개 변수와 결합하여 검색된 양식의 절대 경로를 구성합니다. 이 값은 HTTP를 사용하여 액세스할 수 있는 디렉토리 또는 웹 위치를 참조할 수 있습니다.

기본값은 빈 문자열입니다.

**XCI 구성 URI:** 렌더링에 사용되는 XCI 파일이 있는 상대 또는 절대 위치입니다. 상대 값의 경우 XCI 파일이 배포 가능한 AEM 양식 EAR 파일에 있다고 가정합니다.

기본값은 `com/adobe/formServer/PA/pa.xci`입니다.

**Font Map URI:** 글꼴 매핑 파일의 상대 또는 절대 위치입니다. 상대 값의 경우 이 파일은 배포 가능한 AEM 양식 EAR 파일에 있다고 가정합니다.

글꼴 매핑 파일은 양식의 HTML 변형에 대한 사용자 정의 글꼴 매핑을 만드는 데 사용되므로 클라이언트의 컴퓨터에서 글꼴을 사용할 수 없을 때 대체할 글꼴을 지정할 수 있습니다.

기본값은 `com/adobe/formServer/client-font-map.properties`입니다.

다음 항목은 글꼴 매핑 파일에 있는 항목의 예입니다.

`Arial=Arial,Helvetica,sans-serif`

**시드 PDF 파일:** 전달을 최적화하기 위해 PDF 양식 변환에 사용되는 초기 PDF 파일입니다. 시드 PDF 파일은 양식 디자인 및 데이터에 추가되는 사용자 정의 PDF 파일(XFA 스트림, 이미지 및 글꼴 리소스만 포함)을 지정합니다. 양식은 Acrobat 7 이상에서 렌더링되어 PDF 양식 변환에 적용됩니다.

기본값은 빈 문자열입니다.

**캐시 위치:** Forms 디스크 캐시의 위치를 지정합니다. 이 설정을 변경하면 현재 위치의 모든 기존 캐시 정보가 재설정되고 새 위치에 새 캐시가 만들어집니다. 다음 옵션 중 하나를 선택합니다.

**기본 위치:** 기본 선택입니다. 이 옵션을 선택하면 사용 중인 응용 프로그램 서버에 종속적인 위치에 캐시가 만들어집니다.

* **JBoss:** [JBoss 홈]\server\[설치 유형]\svcdata\FormServer\Cache
* **WebLogic:** [WebLogic 홈] \user_projects\domains\[aem-forms 도메인 이름]\adobe\[양식 서버 이름]\FormServer\Cache
* **WebSphere:** [IBM 홈]\WebSphere\AppServer\installedApps\adobe\server1\FormServer\Cache

**LC 임시 디렉토리:** 캐시는 AEM 양식 임시 디렉토리의 하위 디렉토리에 생성되며, 이 디렉토리는 설정 > 핵심 시스템 설정 > 구성 > 임시 디렉토리 위치의 관리 콘솔에서 지정됩니다. 하위 디렉토리의 이름은 adobeform_[servername]입니다.

>[!NOTE]
>
>임시 정리 유틸리티를 사용하는 경우에는 이러한 디렉토리를 삭제해도 기능에 영향을 주지 않으므로 새 캐시가 만들어지기 전까지 짧은 시간 동안 성능에 큰 영향을 줄 수 있습니다. 이 문제를 방지하려면 AEM 양식 임시 디렉토리를 지울 때 이 디렉토리를 삭제하지 마십시오.

