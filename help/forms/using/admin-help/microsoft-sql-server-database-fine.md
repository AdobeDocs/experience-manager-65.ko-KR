---
title: 'Microsoft SQL Server 데이터베이스: 구성 세부 조정'
description: Microsoft SQL Server 데이터베이스의 구성을 세부 조정하는 방법을 알아봅니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS, SG_AEMFORMS
exl-id: 9c570827-86e2-47d5-b8ae-66c0767bff2e
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: ht
source-wordcount: '295'
ht-degree: 100%

---

# Microsoft SQL Server 데이터베이스: 구성 세부 조정 {#microsoft-sql-server-database-fine-tuning-the-configuration}

Microsoft SQL Server를 사용하는 경우 기본 구성 설정을 변경해야 합니다. Oracle Enterprise Manager에서 로컬 서버를 마우스 오른쪽 버튼으로 클릭하여 속성 대화 상자에 액세스합니다.

## 메모리 설정 {#memory-settings}

최소 메모리 할당을 가능한 한 큰 숫자로 변경합니다. 데이터베이스가 별도의 컴퓨터에서 실행되는 경우 모든 메모리를 활용하십시오. 기본 설정은 메모리를 적극적으로 할당하지 않으므로 거의 모든 데이터베이스의 성능이 저하됩니다. 프로덕션 컴퓨터에서는 메모리를 가장 적극적으로 할당해야 합니다.

## 프로세서 설정 {#processor-settings}

프로세서 설정을 수정하고 가장 중요한 것은 Windows에서 SQL Server 우선순위 높이기 확인란을 선택하여 서버가 가능한 한 많은 주기를 사용하도록 하는 것입니다. NT 파이버 사용 설정은 그다지 중요하지는 않지만, 해당 설정도 선택하는 것이 좋습니다.

## 데이터베이스 설정 {#database-settings}

데이터베이스 설정을 변경합니다. 가장 중요한 설정은 복구 간격으로, 충돌 후 복구를 기다리는 최대 시간을 지정합니다. 기본 설정은 1분입니다. 5분에서 15분 사이의 더 큰 값을 사용하면 서버에서 데이터베이스 로그의 변경 사항을 데이터베이스 파일에 다시 쓸 수 있는 시간이 더 많아지므로 성능이 향상됩니다.

>[!NOTE]
>
>이 설정은 시작 시 수행해야 하는 로그 파일 재생 길이만 변경하므로 트랜잭션 동작에는 영향을 미치지 않습니다.

로그와 데이터 파일 모두의 할당 공간 크기를 초기 데이터베이스보다 훨씬 크게 설정합니다. 데이터베이스가 1년 동안 얼마나 커질 수 있는지를 고려하십시오. 이상적으로는 로그 파일과 데이터 파일을 연속된 범위에 할당하여 데이터가 디스크 전체에 분산되지 않는 것이 좋습니다.
