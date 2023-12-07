---
title: ASRP - Adobe 저장소 리소스 제공자
description: 관계형 데이터베이스를 공통 저장소로 사용하도록 AEM Communities 설정
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: 6430ed96-5d96-41b6-866f-90b34ff84f7a
source-git-commit: 04050f31742c926b45235595f6318929d3767bd8
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 1%

---

# ASRP - Adobe 저장소 리소스 제공자 {#asrp-adobe-storage-resource-provider}

## ASRP 정보 {#about-asrp}

AEM Communities이 ASRP를 일반 저장소로 사용하도록 구성된 경우 UGC(사용자 생성 컨텐츠)는 동기화나 복제 없이 모든 작성자 및 게시 인스턴스에서 액세스할 수 있습니다.

참조: [SRP 옵션의 특성](/help/communities/working-with-srp.md#characteristics-of-srp-options) 및 [권장 토폴로지](/help/communities/topologies.md).

## 요구 사항 {#requirements}

ASRP를 사용하려면 추가 라이선스가 필요합니다.

UGC에 ASRP를 사용하도록 AEM Communities 사이트를 구성하려면 다음 주소로 계정 담당자에게 문의하십시오.

* 데이터 센터 URL(ASRP 끝점 주소)
* 소비자 키
* 비밀 키
* 보고서 세트 ID

소비자 및 비밀 키는 회사의 모든 보고서 세트에서 공유됩니다. 테넌트당 보고서 세트가 한 개 있습니다.

## 구성 {#configuration}

### ASRP 선택 {#select-asrp}

다음 [스토리지 구성 콘솔](/help/communities/srp-config.md) 에서는 사용할 SRP 구현을 식별하는 기본 스토리지 구성을 선택할 수 있습니다.

**AEM 작성자 인스턴스에서 다음을 수행합니다.**

* 전역 탐색에서 다음으로 이동 **[!UICONTROL 도구 > 커뮤니티 > 스토리지 구성]** 및 선택 **[!UICONTROL Adobe 저장소 리소스 제공자(ASRP)]**.

![asrp-default](assets/asrp-default.png)

다음 정보는 프로비저닝 프로세스에서 제공됩니다.

* **데이터 센터 URL**: 풀다운 : 계정 담당자가 식별한 프로덕션 데이터 센터를 선택합니다.
* **기본 보고서 세트**: 기본 보고서 세트의 이름을 입력합니다.
* **소비자 키**: 소비자 키를 입력합니다.
* **암호**: 암호를 입력합니다.
* **제출**&#x200B;을 선택합니다.

게시 인스턴스를 준비합니다.

* [암호화 키 복제](#replicate-the-crypto-key)
* [구성 복제](#publishing-the-configuration)

구성을 제출한 후 연결을 테스트합니다.

* 선택 **구성 테스트**.

  각 작성자 및 게시 인스턴스에 대해 스토리지 구성 콘솔에서 데이터 센터에 대한 연결을 테스트합니다.

* 프로필 데이터에 대한 사이트 URL을 다음 방법으로 데이터 센터에서 라우팅할 수 있습니다. [링크 표면화](#externalize-links).

### 암호화 키 복제 {#replicate-the-crypto-key}

소비자 키와 비밀 키는 암호화됩니다. 키를 제대로 암호화/암호 해독하려면 모든 AEM 인스턴스에서 기본 Granite 암호화 키가 동일해야 합니다.

다음 지침을 따르십시오. [암호화 키 복제](/help/communities/deploy-communities.md#replicate-the-crypto-key).

### 링크 외부화 {#externalize-links}

올바른 프로필 및 프로필 이미지 링크를 확인하려면 다음을 올바르게 수행하십시오 [링크 외부화 구성](/help/sites-developing/externalizer.md).

도메인을 데이터 센터 URL(ASRP 끝점)에서 라우팅할 수 있는 URL로 설정해야 합니다.

### 시간 동기화 {#time-synchronization}

ASRP 끝점을 사용한 인증이 성공하려면 호스팅된 AEM Communities을 실행하는 컴퓨터는 과 같이 시간 동기화되어야 합니다. [NTP(Network Time Protocol)](https://www.ntp.org/).

### 구성 게시 {#publishing-the-configuration}

ASRP는 모든 작성자 및 게시 인스턴스에서 공통 저장소로 식별되어야 합니다.

게시 환경에서 동일한 구성을 사용할 수 있도록 하려면 다음을 수행하십시오.

AEM 작성자 인스턴스에서 다음을 수행합니다.

* 메인 메뉴에서 다음으로 이동 **[!UICONTROL 도구]** > **[!UICONTROL 배포]** > **[!UICONTROL 복제]**
* 선택 **트리 활성화**
* **시작 경로**: 다음으로 이동 `/conf/global/settings/communities/srpc/`
* 선택 취소 **수정된 항목만**
* 선택 **활성화**

## AEM 6.0에서 업그레이드 {#upgrading-from-aem}

>[!CAUTION]
>
>게시된 커뮤니티 사이트에서 ASRP를 활성화하는 경우, 모든 UGC가에 이미 저장됨 [JCR](/help/communities/jsrp.md) 온-프레미스 스토리지와 클라우드 스토리지 간에 데이터 동기화가 없으므로 는 더 이상 표시되지 않습니다.

**`AEM Communities Extension`** 는 이전에 AEM 6.0 social communities as a cloud service에 도입되었습니다. AEM 6.1 커뮤니티에서는 클라우드 구성이 필요하지 않으므로 [스토리지 구성 콘솔](/help/communities/srp-config.md).

새로운 스토리지 구조로 인해 다음을 수행해야 합니다. [업그레이드](/help/communities/upgrade.md#adobe-cloud-storage) 소셜 커뮤니티에서 커뮤니티로 업그레이드할 때의 지침입니다.

## 사용자 데이터 관리 {#managing-user-data}

에 관한 정보를 위하여 *사용자*, *사용자 프로필* 및 *사용자 그룹*, 종종 게시 환경에 입력됨, 방문

* [사용자 동기화](/help/communities/sync.md)
* [사용자 및 사용자 그룹 관리](/help/communities/users.md)

## 문제 해결 {#troubleshooting}

### 업그레이드 후 UGC가 사라짐 {#ugc-disappears-after-upgrade}

기존 AEM 6.0 소셜 커뮤니티 사이트에서 업그레이드하는 경우 다음을 따르십시오 [업그레이드 지침](/help/communities/upgrade.md#adobe-cloud-storage), 그렇지 않으면 UGC가 손실된 것 같습니다.

### 인증 오류 {#authentication-errors}

데이터 센터 URL에 대해 인증 오류를 수신하고 AEM error.log에 부실 타임스탬프에 대한 메시지가 포함된 경우 시간 동기화가 발생하고 있는지 확인합니다.

다음과 같은 도구 사용 [NTP(Network Time Protocol)](https://www.ntp.org/) 모든 AEM 작성자 및 게시 서버를 시간 동기화합니다.

### 새 콘텐츠가 검색에 표시되지 않음 {#new-content-does-not-appear-in-searches}

Adobe 클라우드 스토리지 인프라는 *최종 일관성* 확장 및 성능 목표를 달성합니다. 따라서 새 콘텐츠를 즉시 사용할 수 없으며 검색 결과에 표시되기까지 몇 초 정도 걸립니다.

최종 일관성에 영향을 주는 간격이 모니터링되지만, 새 콘텐츠가 검색에 나타나는 데 몇 초 이상 걸리는 경우 계정 담당자에게 문의하십시오.

### ASRP에서 UGC가 표시되지 않음 {#ugc-not-visible-in-asrp}

저장소 옵션의 구성을 확인하여 ASRP가 기본 공급자로 구성되었는지 확인하십시오. 기본적으로 저장소 리소스 공급자는 ASRP가 아닌 JSRP입니다.

모든 작성자 및 게시 AEM 인스턴스에서 저장소 구성 콘솔을 다시 방문하거나 AEM 저장소를 확인합니다.

JCR에서, [/conf/global/settings/communities](https://localhost:4502/crx/de/index.jsp#/etc/socialconfig/):

* 다음을 포함하지 않음 [srpc](https://localhost:4502/crx/de/index.jsp#/conf/global/settings/communities/srp) 즉, 스토리지 공급자가 JSRP입니다.
* srpc 노드가 존재하고 다음을 포함하는 경우 [defaultconfiguration](https://localhost:4502/crx/de/index.jsp#/conf/global/settings/communities/srp/defaultconfiguration) node인 defaultconfiguration의 속성은 ASRP를 기본 공급자로 정의합니다.
