---
title: '"Microsoft SQL Server 데이터베이스:구성 미세 조정"'
seo-title: '"Microsoft SQL Server 데이터베이스:구성 미세 조정"'
description: Microsoft SQL Server 데이터베이스의 구성을 세밀하게 조정하는 방법을 알아봅니다.
seo-description: Microsoft SQL Server 데이터베이스의 구성을 세밀하게 조정하는 방법을 알아봅니다.
uuid: 2d618aab-3c67-4edb-a28f-a20904689e6f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS, SG_AEMFORMS
discoiquuid: 70559a94-42ea-411a-a32f-5f38bc17ff96
translation-type: tm+mt
source-git-commit: a929252a13f66da8ac3e52aea0655b12bdd1425f
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---


# Microsoft SQL Server 데이터베이스:구성 {#microsoft-sql-server-database-fine-tuning-the-configuration} 미세 조정

Microsoft SQL Server를 사용할 때는 기본 구성 설정을 변경해야 합니다. oracle Enterprise Manager에서 로컬 서버를 마우스 오른쪽 단추로 클릭하여 속성 대화 상자에 액세스합니다.

## 메모리 설정 {#memory-settings}

최소 메모리 할당을 가능한 한 큰 숫자로 변경합니다. 데이터베이스가 별도의 컴퓨터에서 실행 중인 경우 모든 메모리를 사용합니다. 기본 설정은 메모리를 적극적으로 할당하지 않으므로 거의 모든 데이터베이스의 성능을 저해합니다. 프로덕션 시스템에서 메모리를 할당하는 데 가장 적극적인 역할을 해야 합니다.

## 프로세서 설정 {#processor-settings}

프로세서 설정을 수정하고, 가장 중요한 것은 서버가 가능한 한 많은 주기를 사용하도록 [Windows에서 SQL Server 우선 순위 향상] 확인란을 선택합니다. [NT 섬유 사용] 설정은 덜 중요하지만 이 설정도 선택할 수 있습니다.

## 데이터베이스 설정 {#database-settings}

데이터베이스 설정을 변경합니다. 가장 중요한 설정은 장애 발생 후 복구를 기다리는 최대 시간을 지정하는 복구 간격입니다. 기본 설정은 1분입니다. 5분에서 15분까지의 큰 값을 사용하면 데이터베이스 로그에서 데이터베이스 파일로 다시 변경 내용을 쓸 수 있는 시간을 서버에 주기 때문에 성능이 향상됩니다.

>[!NOTE]
>
>이 설정은 시작할 때 수행해야 하는 로그 파일 재생의 길이만 변경되므로 트랜잭션 비헤이비어를 손상시키지 않습니다.

로그와 데이터 파일의 공간 할당 크기를 초기 데이터베이스보다 훨씬 크게 설정합니다. 1년 동안 얼마나 많은 데이터베이스가 성장할 수 있는지 고려하십시오. 가장 좋은 방법은 로그 및 데이터 파일이 연속적인 범위로 할당되므로 데이터가 디스크 전체에 걸쳐 조각화되지 않습니다.
