---
title: 시스템 정보 보기
seo-title: View system information
description: 리소스 모니터링 차트 및 AEM Forms를 실행하는 서버에 대한 정보를 보는 방법에 대해 알아봅니다.
seo-description: Learn how you can view resource monitoring charts and information about the server that is running AEM forms.
uuid: 983c1cc7-a8b3-48b2-a4c8-7b28a2e32537
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d51460d9-c96c-4661-b93e-e015427878ab
exl-id: 27a2e81c-47b0-4de8-95bd-7cb34b9450da
source-git-commit: c4cd9a61a226ace2a72d60b5b7b7432de12cb873
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 0%

---

# 시스템 정보 보기 {#view-system-information}

시스템 탭에는 리소스 모니터링 차트와 AEM Forms를 실행 중인 서버에 대한 정보가 표시됩니다. 이 정보에 액세스하려면 관리 콘솔에서 페이지 오른쪽 상단의 상태 모니터 를 클릭합니다. 클러스터된 환경에서 AEM Forms를 실행하는 경우 서버 목록에서 선택한 노드에 대한 정보가 표시됩니다.

현재 시스템 정보를 등록 정보 파일로 저장하려면 저장을 누릅니다.

시스템 탭의 오른쪽 창에는 다음 정보가 그래픽으로 표시됩니다.

* 작업 및 작업 수 항목
* 힙 및 커밋된 힙 사용량
* 비더미 및 커밋된 비더미 사용

포인터를 타임라인을 따라 드래그하여 특정 시점의 값을 가져올 수 있습니다.

>[!NOTE]
>
>그래프 데이터, 서버 정보값, 시계 시간은 10분마다 업데이트된다. 정보가 실시간으로 표시되지 않습니다.

시스템 탭의 왼쪽 창에는 서버 또는 노드에 대한 다음 정보가 표시됩니다.

**가상 컴퓨터:** 서버의 JVM(Java Virtual Machine) 버전입니다.

**가상 시스템 공급업체:** JVM 제조업체.

**가상 컴퓨터 버전:** JVM 버전 번호

**컴퓨터 이름:** AEM Forms가 설치된 서버의 호스트 이름입니다.

**작동 시간:** 서버가 실행되는 시간(시간 및 분)입니다.

**Just-In-Time 컴파일러:** 사용 중인 컴파일러의 이름입니다.

**컴파일 시간:** 컴파일 시 소요된 시간입니다.

**라이브 Threads 수:** 현재 AEM Forms 시스템에 있는 총 스레드 수입니다.

**Threads 피크 수:** 시스템에 기록된 최대 라이브 스레드 수입니다.

**로드된 클래스 수:** JVM으로 로드된 클래스 수입니다.

**언로드된 클래스 수:** JVM에서 언로드된 클래스 수

**최소 더미:** 사용된 힙의 최소 양입니다.

**최대 더미:** 사용된 힙의 최대 양입니다.

**운영 체제 이름:** AEM Forms 서버에서 실행 중인 운영 체제의 이름입니다.

**운영 체제 버전:** AEM Forms 서버에서 실행 중인 운영 체제의 버전 번호입니다.

**운영 체제 Arch:** JVM이 실행 중인 운영 체제 아키텍처입니다.

**프로세서 수:** 시스템의 프로세서 수입니다.

**가상 컴퓨터 인수:** JVM에서 사용하는 인수입니다.

**클래스 경로:** JVM에서 사용하는 클래스 경로입니다.

**라이브러리 경로:** JVM에서 사용하는 라이브러리 경로입니다.

**부팅 클래스 경로:** JVM에서 사용하는 부트 클래스 경로입니다.

**응용 프로그램 서버 유형:** AEM Forms를 실행하는 데 사용되는 응용 프로그램 서버 유형입니다.

**응용 프로그램 서버 버전:** AEM Forms를 실행하는 데 사용되는 응용 프로그램 서버의 버전 번호입니다.

**애플리케이션 서버 공급업체:** AEM Forms를 실행하는 데 사용되는 응용 프로그램 서버 제조업체.

**설치 날짜:** AEM Forms가 설치된 날짜(yyyy-mm-dd 형식)입니다.

**AEM forms 버전:** 설치된 AEM Forms 버전입니다.

**패치 버전:** AEM forms 패치 번호입니다.

**데이터베이스 이름:** AEM Forms에서 사용하는 데이터베이스의 유형입니다.

**데이터베이스 버전:** AEM Forms에서 사용하는 데이터베이스의 버전 번호입니다.

**데이터베이스 드라이브 이름:** JVM에서 데이터베이스에 연결하는 데 사용하는 드라이버의 이름입니다.

**데이터베이스 드라이버 버전:** JVM에서 데이터베이스에 연결하는 데 사용하는 드라이버 버전입니다.

다음 **저장** 단추를 사용하면 이 시스템 정보를 속성 파일에 저장할 수 있습니다.
