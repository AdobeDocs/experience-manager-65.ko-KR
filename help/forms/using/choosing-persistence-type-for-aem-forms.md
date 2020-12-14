---
title: AEM Forms 설치에 대한 지속성 유형 선택
seo-title: AEM Forms 설치에 대한 지속성 유형 선택
description: 지속성 유형을 현명하게 선택하십시오. 효율적이고 확장 가능한 AEM Forms 환경을 구축할 수 있습니다.
seo-description: 지속성 유형을 현명하게 선택하십시오. 효율적이면서도 확장 가능한 AEM Forms 환경을 구축할 수 있습니다.
uuid: 1c692502-5039-4757-9358-1772772b3904
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: a972fb35-38a7-4b83-99bd-6a6dddf8043b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 1%

---


# AEM Forms 설치에 대한 지속성 유형 선택 {#choosing-a-persistence-type-for-an-aem-forms-installation}

지속성 유형을 현명하게 선택하십시오. 효율적이고 확장 가능한 AEM Forms 환경을 구축할 수 있습니다.

지속성은 컨텐츠를 물리적 저장소에 저장하는 방법입니다. 데이터에 대한 실제 데이터 구조 및 저장 메커니즘을 정의합니다. MicroKernels는 AEM Forms에서 지속성 관리자 역할을 수행합니다. AEM Forms은 TarMK, MongoMK 및 RDBMK 유형의 지속성(MicroKernals)을 지원합니다. AEM Forms 인스턴스의 목적 및 배포 유형(단일 서버, 팜 또는 클러스터)에 따라 AEM Forms에 대한 지속성 유형을 선택할 수 있습니다.

>[!NOTE]
>
>LiveCycle ES4 SP1은 TarPM 지속성을 사용하여 컨텐츠를 저장합니다.

다음 표에는 환경에 대한 지속성 유형을 선택하는 데 도움이 되는 다양한 매개 변수와 함께 지원되는 모든 지속성 유형이 나열됩니다.

<table>
 <tbody>
  <tr>
   <th><strong>설치 유형/비용</strong></th>
   <th><strong>TarMK</strong></th>
   <th><strong>MongoMk</strong></th>
   <th><strong>RDBMK</strong></th>
  </tr>
  <tr>
   <th><strong>독립 실행형 설정</strong></th>
   <td>지원됨<br /> </td>
   <td>지원됨</td>
   <td>지원됨</td>
  </tr>
  <tr>
   <th><strong>클러스터 설정</strong></th>
   <td>지원되지 않음</td>
   <td>지원됨</td>
   <td>지원됨</td>
  </tr>
  <tr>
   <th><strong>라이선스 비용</strong></th>
   <td>AEM에 포함 </td>
   <td>별도의 라이선스 필요</td>
   <td>별도의 라이선스 필요</td>
  </tr>
 </tbody>
</table>

TarMK는 성능을 위해 고안된 반면 MongoMK와 RDBMK는 확장성을 위해 설계되었습니다. Adobe은 작성자 및 게시 인스턴스 모두에 대해 모든 AEM Forms 배포 시나리오에 대해 TarMK의 기본 지속성 기술로 권장하고 있습니다. 단, [Choosing Mongo 또는 Relational Database Microkernel over TarMK](#p-choosing-mongo-or-a-relational-database-microkernel-over-tarmk-p) 섹션에 설명된 사용 사례를 제외합니다.

지원되는 마이크로커널 목록은 OSGi 기술 요구 사항의 [AEM Forms(a1/>) 또는 JEE 지원 플랫폼 조합](/help/forms/using/aem-forms-jee-supported-platforms.md) 문서의 [AEM Forms을 참조하십시오.](/help/sites-deploying/technical-requirements.md)

## TarMK {#choosing-mongo-or-a-relational-database-microkernel-over-tarmk} 위에 Mongo 또는 관계형 데이터베이스 마이크로커널 선택

확장 가능한(클러스터된) AEM Forms 환경은 2개 이상의 가로로 구성된 활성 작성자 인스턴스 세트입니다. 모든 동시 작성 활동을 지원하는 단일 서버가 더 이상 지속되지 않을 경우 둘 이상의 작성자 인스턴스를 실행하도록 선택할 수 있습니다.

JEE 환경에서 확장 가능한(클러스터된) AEM Forms에 대해서는 MongoMK 및 RDBMK 지속성 유형만 지원됩니다. 서버 수 또는 확장 가능한 환경의 크기는 설치 시 다릅니다. 고려 사항 및 예 목록은 [권장 배포](/help/sites-deploying/recommended-deploys.md) 및 [AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md)용 아키텍처 및 배포 토폴로지 문서를 참조하십시오. RDBMK 및 TarMK와 함께 AEM Forms의 용량 계획에 대한 자세한 내용은 AEM Forms 지원에 문의할 수도 있습니다.
