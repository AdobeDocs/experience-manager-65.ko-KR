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
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 1%

---

# ASRP - Adobe 저장소 리소스 제공자 {#asrp-adobe-storage-resource-provider}

## ASRP 정보 {#about-asrp}

AEM Communities이 ASRP를 일반 저장소로 사용하도록 구성된 경우 UGC(사용자 생성 컨텐츠)는 동기화나 복제 없이 모든 작성자 및 게시 인스턴스에서 액세스할 수 있습니다.

[SRP 옵션의 특성](/help/communities/working-with-srp.md#characteristics-of-srp-options) 및 [권장 토폴로지](/help/communities/topologies.md)도 참조하세요.

## 요구 사항 {#requirements}

ASRP를 사용하려면 추가 라이선스가 필요합니다.

UGC에 ASRP를 사용하도록 AEM Communities 사이트를 구성하려면 다음 주소로 계정 담당자에게 문의하십시오.

* 데이터 센터 URL(ASRP 끝점 주소)
* 소비자 키
* 암호 키
* 보고서 세트 ID

소비자 및 비밀 키는 회사의 모든 보고서 세트에서 공유됩니다. 테넌트당 보고서 세트가 한 개 있습니다.

## 구성 {#configuration}

### ASRP 선택 {#select-asrp}

[저장소 구성 콘솔](/help/communities/srp-config.md)에서 사용할 SRP 구현을 식별하는 기본 저장소 구성을 선택할 수 있습니다.

**AEM 작성자 인스턴스:**

* 전역 탐색에서 **[!UICONTROL 도구 > 커뮤니티 > 저장소 구성]**(으)로 이동하고 **[!UICONTROL ASRP(저장소 리소스 공급자) Adobe]**&#x200B;을(를) 선택합니다.

![asrp-default](assets/asrp-default.png)

다음 정보는 프로비저닝 프로세스에서 제공됩니다.

* **데이터 센터 URL**: 계정 담당자가 식별한 프로덕션 데이터 센터를 선택하기 위한 풀다운.
* **기본 보고서 세트**: 기본 보고서 세트의 이름을 입력하십시오.
* **소비자 키**: 소비자 키를 입력합니다.
* **암호**: 암호를 입력하십시오.
* **제출**&#x200B;을 선택합니다.

게시 인스턴스를 준비합니다.

* [암호화 키 복제](#replicate-the-crypto-key)
* [구성 복제](#publishing-the-configuration)

구성을 제출한 후 연결을 테스트합니다.

* **구성 테스트**&#x200B;를 선택하십시오.

  각 작성자 및 게시 인스턴스에 대해 스토리지 구성 콘솔에서 데이터 센터에 대한 연결을 테스트합니다.

* [링크를 외부화](#externalize-links)하여 프로필 데이터에 대한 사이트 URL을 데이터 센터에서 라우팅할 수 있는지 확인하십시오.

### 암호화 키 복제 {#replicate-the-crypto-key}

소비자 키와 비밀 키는 암호화됩니다. 키를 제대로 암호화/암호 해독하려면 모든 AEM 인스턴스에서 기본 Granite 암호화 키가 동일해야 합니다.

[암호 키 복제](/help/communities/deploy-communities.md#replicate-the-crypto-key)의 지침을 따르십시오.

### 링크 외부화 {#externalize-links}

올바른 프로필 및 프로필 이미지 링크를 보려면 올바르게 [링크 외부화를 구성](/help/sites-developing/externalizer.md)하십시오.

도메인을 데이터 센터 URL(ASRP 끝점)에서 라우팅할 수 있는 URL로 설정해야 합니다.

### 시간 동기화 {#time-synchronization}

ASRP 끝점을 사용한 인증이 성공하려면 호스팅된 AEM Communities을 실행하는 컴퓨터는 [NTP(네트워크 시간 프로토콜)](https://www.ntp.org/)과 같이 시간을 동기화해야 합니다.

### 구성 게시 {#publishing-the-configuration}

ASRP는 모든 작성자 및 게시 인스턴스에서 공통 저장소로 식별되어야 합니다.

게시 환경에서 동일한 구성을 사용할 수 있도록 하려면 다음을 수행하십시오.

AEM 작성자 인스턴스에서 다음을 수행합니다.

* 메인 메뉴에서 **[!UICONTROL 도구]** > **[!UICONTROL 배포]** > **[!UICONTROL 복제]**(으)로 이동
* **트리 활성화** 선택
* **시작 경로**: `/conf/global/settings/communities/srpc/`(으)로 이동
* **수정된 항목만** 선택 취소
* **활성화** 선택

## AEM 6.0에서 업그레이드 {#upgrading-from-aem}

>[!CAUTION]
>
>게시된 커뮤니티 사이트에서 ASRP를 사용하도록 설정하면 온-프레미스 저장소와 클라우드 저장소 간에 데이터가 동기화되지 않으므로 [JCR](/help/communities/jsrp.md)에 이미 저장된 UGC가 더 이상 표시되지 않습니다.

**`AEM Communities Extension`**&#x200B;은(는) 이전에 AEM 6.0 소셜 커뮤니티에서 클라우드 서비스로 도입되었습니다. AEM 6.1 커뮤니티에서는 클라우드 구성이 필요하지 않으므로 [저장소 구성 콘솔](/help/communities/srp-config.md)에서 ASRP를 선택하면 됩니다.

새 저장소 구조로 인해 소셜 커뮤니티에서 커뮤니티로 업그레이드할 때 [업그레이드](/help/communities/upgrade.md#adobe-cloud-storage) 지침을 따라야 합니다.

## 사용자 데이터 관리 {#managing-user-data}

게시 환경에 종종 입력된 *사용자*, *사용자 프로필* 및 *사용자 그룹*&#x200B;에 대한 자세한 내용을 보려면 다음을 방문하십시오.

* [사용자 동기화](/help/communities/sync.md)
* [사용자 및 사용자 그룹 관리](/help/communities/users.md)

## 문제 해결 {#troubleshooting}

### 업그레이드 후 UGC가 사라짐 {#ugc-disappears-after-upgrade}

기존 AEM 6.0 소셜 커뮤니티 사이트에서 업그레이드하는 경우 [업그레이드 지침](/help/communities/upgrade.md#adobe-cloud-storage)을(를) 따르세요. 그렇지 않으면 UGC가 손실된 것으로 표시됩니다.

### 인증 오류 {#authentication-errors}

데이터 센터 URL에 대해 인증 오류를 수신하고 AEM error.log에 부실 타임스탬프에 대한 메시지가 포함된 경우 시간 동기화가 발생하고 있는지 확인합니다.

[NTP(네트워크 시간 프로토콜)](https://www.ntp.org/)와 같은 도구를 사용하여 모든 AEM 작성자 및 게시 서버를 시간 동기화합니다.

### 새 콘텐츠가 검색에 표시되지 않음 {#new-content-does-not-appear-in-searches}

Adobe 클라우드 스토리지 인프라는 *최종 일관성*&#x200B;을 사용하여 확장 및 성능 목표를 달성합니다. 따라서 새 콘텐츠를 즉시 사용할 수 없으며 검색 결과에 표시되기까지 몇 초 정도 걸립니다.

최종 일관성에 영향을 주는 간격이 모니터링되지만, 새 콘텐츠가 검색에 나타나는 데 몇 초 이상 걸리는 경우 계정 담당자에게 문의하십시오.

### ASRP에서 UGC가 표시되지 않음 {#ugc-not-visible-in-asrp}

저장소 옵션의 구성을 확인하여 ASRP가 기본 공급자로 구성되었는지 확인하십시오. 기본적으로 저장소 리소스 공급자는 ASRP가 아닌 JSRP입니다.

모든 작성자 및 게시 AEM 인스턴스에서 저장소 구성 콘솔을 다시 방문하거나 AEM 저장소를 확인합니다.

JCR에서 [/conf/global/settings/communities](https://localhost:4502/crx/de/index.jsp#/etc/socialconfig/)인 경우:

* [srpc](https://localhost:4502/crx/de/index.jsp#/conf/global/settings/communities/srp) 노드가 없습니다. 저장소 공급자가 JSRP임을 의미합니다.
* srpc 노드가 있고 [defaultconfiguration](https://localhost:4502/crx/de/index.jsp#/conf/global/settings/communities/srp/defaultconfiguration) 노드를 포함하는 경우 defaultconfiguration의 속성은 ASRP를 기본 공급자로 정의합니다.
