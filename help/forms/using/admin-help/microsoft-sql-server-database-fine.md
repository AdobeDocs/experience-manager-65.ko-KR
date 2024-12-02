---
title: 'Microsoft SQL Server 데이터베이스: 구성 미세 조정'
description: Microsoft SQL Server 데이터베이스의 구성을 미세 조정하는 방법에 대해 알아봅니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS, SG_AEMFORMS
exl-id: 9c570827-86e2-47d5-b8ae-66c0767bff2e
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---

# Microsoft SQL Server 데이터베이스: 구성 미세 조정 {#microsoft-sql-server-database-fine-tuning-the-configuration}

Microsoft SQL Server를 사용할 때는 기본 구성 설정을 변경해야 합니다. oracle Enterprise Manager에서 로컬 서버를 마우스 오른쪽 단추로 눌러 등록 정보 대화 상자에 액세스합니다.

## 메모리 설정 {#memory-settings}

최소 메모리 할당을 가능한 큰 수로 변경합니다. 데이터베이스가 별도의 컴퓨터에서 실행 중인 경우 모든 메모리를 사용합니다. 기본 설정은 적극적으로 메모리를 할당하지 않으므로 거의 모든 데이터베이스에서 성능이 저하됩니다. 당신은 생산 기계에 메모리를 할당하는 데 가장 적극적으로 나서야 한다.

## 프로세서 설정 {#processor-settings}

프로세서 설정을 수정하고 가장 중요한 점은 서버에서 가능한 한 많은 주기를 사용하도록 Windows에서 SQL Server 우선 순위 높이기 확인란을 선택합니다. [NT 섬유 사용] 설정은 덜 중요하지만 선택할 수도 있습니다.

## 데이터베이스 설정 {#database-settings}

데이터베이스 설정을 변경합니다. 가장 중요한 설정은 복구 간격이며, 충돌 후 복구를 기다리는 최대 시간을 지정합니다. 기본 설정은 1분입니다. 5~15분 정도 큰 값을 사용하면 서버가 데이터베이스 로그에서 데이터베이스 파일에 변경 사항을 다시 쓸 수 있는 시간이 늘어나기 때문에 성능이 향상됩니다.

>[!NOTE]
>
>이 설정은 시작 시 수행해야 하는 로그 파일 재생 길이만 변경하므로 트랜잭션 동작을 손상시키지 않습니다.

로그와 데이터 파일 모두에 대해 할당된 공간 크기를 초기 데이터베이스보다 훨씬 크게 설정합니다. 1년 동안 데이터베이스가 얼마나 늘어날 수 있는지 고려합니다. 가장 좋은 방법은 로그 및 데이터 파일을 연속적인 범위로 할당함으로써 데이터가 디스크 전체에 걸쳐 단편화되지 않도록 하는 것입니다.
