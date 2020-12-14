---
title: Apache Maven을 사용하여 AEM 프로젝트를 작성하는 방법
description: 이 문서에서는 Apache Maven을 기반으로 AEM 프로젝트를 설정하는 방법에 대해 설명합니다.
translation-type: tm+mt
source-git-commit: 7bbafbd96ec92ed4278f6fa1d9899a3d59ee69ad
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 22%

---


# Apache Maven을 사용하여 AEM 프로젝트를 작성하는 방법 {#how-to-build-aem-projects-using-apache-maven}

AEM 6.5는 온-프레미스 및 AMS 구현 모두에 대해 최신 AEM Project Lianype에서 구현되는 패키지 관리 및 프로젝트 구조에 대한 최신 모범 사례를 준수합니다.

>[!TIP]
>
>자세한 내용은 다음을 참조하십시오.
>
>* 최신 AEM 프로젝트를 구성하는 방법에 대한 Cloud Service 설명서로 AEM의 [AEM 프로젝트 구조](https://docs.adobe.com/content/help/ko-KR/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) 아티클을 참조하십시오.
>* 원형 유형을 사용하여 새 AEM 프로젝트를 시작하는 방법에 대한 [AEM Project Tranype](https://docs.adobe.com/content/help/ko-KR/experience-manager-core-components/using/developing/archetype/overview.html) 설명서입니다.
>* AEM 응용 프로그램을 배포하는 방법에 대한 Cloud Service 설명서로 AEM의 [Adobe Content Package Maven Plugin](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developer-tools/maven-plugin.html?lang=en#developer-tools) 아티클입니다.

>
>
세 문서 모두 AEM 6.5에 적용됩니다.
