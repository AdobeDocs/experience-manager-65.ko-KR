---
title: CIF(Commerce Integration Framework) Add-On의 주목할 만한 변경 사항
description: 이전 CIF 버전과 비교하여 CIF(Commerce Integration Framework) Add-On의 주목할 만한 변경 사항입니다.
exl-id: 5a526960-96a1-421e-9fb0-0825e7df8f32,c136763f-56aa-450e-8796-bc84bf6c205d
translation-type: tm+mt
source-git-commit: a8dba82029168660b84b085ab46d0406b19961ef
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---

# 상거래 통합 프레임워크(CIF) Add-on{#notable-changes}에 대한 주목할 만한 변경 사항

이 문서에서는 주로 CIF Classic(Quickstart)과 CIF Open-source로 알려진 CEF(Commerce Integration Framework) Add-on 버전과 이전 CIF 버전 간의 중요한 차이점을 강조 표시합니다.

## 설치 및 업데이트

AEM CIF Add-on 패키지는 AEM 패키지 관리자로 설치 및 업데이트됩니다.

**이전 CIF 버전**

* CIF Classic:설치할 필요가 없습니다. CIF는 Quickstart의 일부입니다. CIF 업데이트는 일반 AEM 또는 서비스 팩 업데이트에 포함되어 있습니다.
* CIF 오픈 소스:GitHub를 통해 설치 업데이트는 수동 업데이트/유지 관리 작업의 일환입니다.

## 끝점 구성

끝점은 OSGi 콘솔을 통해 구성됩니다.

**이전 CIF 버전**

* CIF Classic:AEM의 OSGi 구성을 통해
* CIF 오픈 소스:CIF 구성 브라우저 사용

## CIF Venia 프로젝트 배포

[GitHub AEM Guides - CIF Venia Project](https://github.com/adobe/aem-cif-guides-venia)에서 프로젝트를 사용할 수 있으며 패키지 AEM 관리자를 통해 배포합니다.

**이전 CIF 버전**

* CIF Classic:AEM 패키지 설치를 통해

## 제품 카탈로그 데이터

필수 GraphQL API를 지원하는 외부 끝점에 대한 실시간 호출을 통해 제품 카탈로그 데이터가 요청 시 수신됩니다. 이러한 API는 지정된 날짜에 라이브 또는 스테이지된 데이터에 대한 액세스를 지원합니다. 복제할 필요가 없습니다.

**이전 CIF 버전**

* CIF Classic:라이브 및 단계 제품 데이터는 전체 또는 델타 제품 가져오기를 통해 AEM 작성자의 JCR에서 가져와 계속 보관됩니다. 라이브 제품 데이터가 AEM 게시에 복제됩니다.

## AEM 렌더링을 통한 제품 카탈로그 경험

AEM은 제품 및 카테고리에 할당된 AEM 카탈로그 템플릿을 사용하여 제품 카탈로그 경험을 신속하게 렌더링합니다. 복제할 필요가 없습니다.

**이전 CIF 버전**

* CIF Classic:AEM 작성자는 카탈로그 블루프린트 도구를 사용하여 모든 카테고리/제품에 대한 AEM 페이지를 만듭니다. 이러한 페이지는 AEM 게시로 복제됩니다.

>[!NOTE]
>
>AEM Managed Service 또는 AEM 온프레미스에서 CIF를 사용하는 방법에 대한 추가 문서는 [Commerce Integration Framework](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html)를 참조하십시오.
