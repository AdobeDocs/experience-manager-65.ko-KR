---
title: CIF(Commerce Integration Framework) 추가 기능의 주요 변경 사항
description: 이전 CIF 버전과 비교하여 CIF(Commerce Integration Framework) 추가 기능의 주요 변경 사항입니다.
exl-id: 5a526960-96a1-421e-9fb0-0825e7df8f32,c136763f-56aa-450e-8796-bc84bf6c205d
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---

# 전자 상거래 통합 프레임워크(CIF) 추가 기능의 주요 변경 사항{#notable-changes}

이 문서에서는 주로 CIF Classic(Quickstart)과 CIF Open-source로 알려진 CIF(Commerce Integration Framework) 추가 기능과 이전 CIF 버전 간의 중요한 차이점을 조명합니다.

## 설치 및 업데이트

AEM CIF 추가 기능 패키지가 설치되고 AEM Package Manager로 업데이트됩니다.

**이전 CIF 버전**

* CIF Classic:설치할 필요가 없습니다. CIF가 Quickstart의 일부입니다. CIF 업데이트는 일반적인 AEM 또는 서비스 팩 업데이트에 포함되어 있습니다
* CIF 오픈 소스:GitHub를 통해 설치. 업데이트는 수동 업데이트/유지 관리 작업의 일부입니다.

## 끝점 구성

엔드포인트는 OSGi 콘솔을 통해 구성됩니다.

**이전 CIF 버전**

* CIF Classic:AEM의 OSGi 구성을 통해
* CIF 오픈 소스:CIF 구성 브라우저 사용

## CIF Venia Project 배포

[GitHub AEM Guides - CIF Venia Project](https://github.com/adobe/aem-cif-guides-venia)에 프로젝트를 사용할 수 있으며 AEM Package Manager를 통해 배포됩니다.

**이전 CIF 버전**

* CIF Classic:AEM 패키지 설치를 통해

## 제품 카탈로그 데이터

필요한 GraphQL API를 지원하는 외부 엔드포인트에 대한 실시간 호출을 통해 제품 카탈로그 데이터가 요청 시 수신됩니다. 이러한 API는 지정된 날짜에 라이브 또는 스테이징된 데이터에 대한 액세스를 지원합니다. 복제가 필요하지 않습니다.

**이전 CIF 버전**

* CIF Classic:라이브 및 스테이징된 제품 데이터는 전체 또는 델타 제품 가져오기를 통해 AEM Author의 JCR에서 가져오고 유지됩니다. 라이브 제품 데이터가 AEM Publish에 복제됩니다.

## AEM 렌더링을 사용한 제품 카탈로그 경험

AEM은 제품 및 카테고리에 할당된 AEM 카탈로그 템플릿을 사용하여 제품 카탈로그 경험을 즉시 렌더링합니다. 복제가 필요하지 않습니다.

**이전 CIF 버전**

* CIF Classic:AEM 작성자는 카탈로그 블루프린트 도구를 사용하여 모든 카테고리/제품에 대한 AEM 페이지를 만듭니다. 이러한 페이지가 AEM Publish에 복제됩니다.

>[!NOTE]
>
>AEM Managed Service 또는 AEM On-Premise에서 CIF를 사용하는 방법에 대한 추가 설명서는 [Commerce Integration Framework](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html) 를 참조하십시오
